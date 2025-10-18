# 24-web-Elios-杨玉禄

## 工具

### HackBar

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20150046.png)

### Burp Suite

下载压缩包+解压+破解

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20224658.png)

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20190545.png)

### AI

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20151113.png)

## 攻防世界

### view_source

F12或ctrl+u查看源码找flag

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20205052.png)

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20201706.png)

### get_post

打开hackbar

get: URL后拼接？a=1 提交

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20204608.png)

post: b=2 提交

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20204638.png)

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20204700.png)

## Linux

### 环境搭建

打开powershell,输入指令 `wsl --install`

打开Microsoft，安装Ubuntu22.04LTS

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20251017220334.jpg)

![](https://cdn.jsdelivr.net/gh/yulu-yang/picture@main/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-10-17%20114946.png)

### 笔记

#### 目录与文件操作

| 命令 | 功能说明 | 示例 |
|------|----------|------|
| pwd | 显示当前所在目录的绝对路径 | `pwd` |
| ls | 列出目录内容 | `ls` 列出当前目录中的文件和子目录<br>`ls -l` 列出详细信息 |
| cd | 切换目录 | `cd /home`<br>`cd ..` 回到上一级目录 |
| mkdir | 创建新的目录 | `mkdir demo` 创建一个名为demo的目录 |
| cp | 复制文件或目录 | `cp -r demo1 demo2` 复制demo1到demo2<br>`cp file1.txt file2.txt` 复制file1.txt为file2.txt |
| touch | 创建空文件或更新文件时间戳 | `touch file.txt` |
| mv | 移动文件/目录或重命名 | `mv old.txt new.txt` 重命名<br>`mv file.txt /home/user` 移动 |
| rm | 删除文件或目录 | `rm file.txt` |
| cat | 查看整个文件的内容 | `cat file.txt` |

#### 权限管理

| 命令 | 功能说明 | 示例 |
|------|----------|------|
| sudo | 以管理员权限执行命令 | `sudo apt update` |
| chmod | 修改文件权限 |  |
| chown | 修改文件所有者 |  |

#### 压缩与解压

| 命令 | 功能说明 |
|------|----------|
| tar | 打包和解包文件 |
| zip/unzip | 压缩为zip格式/解压zip文件 |

#### 系统信息与进程管理

| 命令 | 功能说明 | 示例 |
|------|----------|------|
| ps | 显示当前进程快照 | `ps aux` 查看所有进程 |
| top/htop | 查看系统进程和资源占用 | `top` |
| kill | 根据进程ID结束进程 | `kill 1234` |
| df | 查看磁盘空间使用情况 |  |
| du | 查看文件或目录的磁盘使用量 |  |
| free | 查看内存使用情况 |  |
| uname | 显示系统信息 |  |
| whoami | 显示当前登录的用户名 |  |
