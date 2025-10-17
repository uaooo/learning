# **view_source**

右键无法查看源代码，可以ctrl u或者url前加入view-source: 查看源代码。


<img width="889" height="487" alt="image" src="https://github.com/user-attachments/assets/fc63ad9e-9990-4a0e-a509-5d1c4f4a0792" />


# **get_post**
<img width="1919" height="528" alt="image" src="https://github.com/user-attachments/assets/012786b4-5ccb-496b-8ef0-3964a4ecf2f7" />
<img width="1910" height="636" alt="image" src="https://github.com/user-attachments/assets/f84b6365-423e-46bd-bdcb-66338e16ac2b" />



# **robots**

<img width="503" height="152" alt="image" src="https://github.com/user-attachments/assets/ca0f9b47-601e-4eb4-8088-e5f1c57197cb" />
<img width="648" height="113" alt="image" src="https://github.com/user-attachments/assets/13af2a43-96c0-4f50-81d8-eb9db87f9d46" />


# linux搭建

<img width="1919" height="985" alt="image" src="https://github.com/user-attachments/assets/d9b3b043-3765-48d0-8cfd-3976e212cf32" />


# python脚本

```
import hashlib
import itertools
import string
import time

def find_md5_with_prefix(target_prefix, max_length=8, charset=None):
    """
    寻找MD5哈希值前6位为指定前缀的字符串
    
    参数:
    target_prefix (str): 目标MD5前缀
    max_length (int): 搜索的最大字符串长度
    charset (str): 字符集，默认为小写字母和数字
    """
    if charset is None:
        charset = string.ascii_lowercase + string.digits
    
    target_prefix = target_prefix.lower()
    print(f"开始搜索MD5前6位为 '{target_prefix}' 的字符串...")
    print(f"字符集: {charset}")
    print(f"最大长度: {max_length}")
    print("-" * 50)
    
    start_time = time.time()
    tested_count = 0
    
    # 尝试不同长度的字符串
    for length in range(1, max_length + 1):
        print(f"正在测试长度为 {length} 的字符串...")
        
        # 生成所有可能的组合
        for combo in itertools.product(charset, repeat=length):
            test_string = ''.join(combo)
            tested_count += 1
            
            # 计算MD5哈希值
            md5_hash = hashlib.md5(test_string.encode()).hexdigest()
            
            # 检查前6位是否匹配
            if md5_hash[:6] == target_prefix:
                end_time = time.time()
                print("\n" + "=" * 50)
                print("找到匹配的字符串!")
                print(f"原始字符串: {test_string}")
                print(f"MD5哈希值: {md5_hash}")
                print(f"测试次数: {tested_count}")
                print(f"耗时: {end_time - start_time:.2f} 秒")
                print("=" * 50)
                return test_string, md5_hash
            
            # 每100000次显示一次进度
            if tested_count % 100000 == 0:
                print(f"已测试 {tested_count} 个组合...")
    
    end_time = time.time()
    print(f"\n在长度为1-{max_length}的字符串中未找到匹配项")
    print(f"总测试次数: {tested_count}")
    print(f"总耗时: {end_time - start_time:.2f} 秒")
    return None, None

def find_md5_sequential(start=0, step=1000000, target_prefix="15af95"):
    """
    使用顺序数字进行搜索（适用于纯数字情况）
    """
    target_prefix = target_prefix.lower()
    print(f"开始顺序搜索MD5前6位为 '{target_prefix}' 的数字...")
    print(f"起始值: {start}, 步长: {step}")
    print("-" * 50)
    
    start_time = time.time()
    
    for i in range(start, start + step):
        test_string = str(i)
        md5_hash = hashlib.md5(test_string.encode()).hexdigest()
        
        if md5_hash[:6] == target_prefix:
            end_time = time.time()
            print("\n" + "=" * 50)
            print("找到匹配的数字!")
            print(f"原始数字: {test_string}")
            print(f"MD5哈希值: {md5_hash}")
            print(f"耗时: {end_time - start_time:.2f} 秒")
            print("=" * 50)
            return test_string, md5_hash
        
        if i % 100000 == 0:
            print(f"已测试到数字: {i}")
    
    end_time = time.time()
    print(f"\n在范围 {start}-{start+step-1} 中未找到匹配项")
    print(f"耗时: {end_time - start_time:.2f} 秒")
    return None, None

if __name__ == "__main__":
    # 方法1: 使用字母数字组合搜索（推荐先尝试这个）
    print("方法1: 字母数字组合搜索")
    result1, hash1 = find_md5_with_prefix("15af95", max_length=6)
    
    if result1 is None:
        print("\n" + "="*50)
        print("方法1未找到结果，尝试方法2...")
        print("="*50 + "\n")
        
        # 方法2: 使用纯数字搜索
        print("方法2: 纯数字搜索")
        result2, hash2 = find_md5_sequential(start=0, step=10000000, target_prefix="15af95")
        
        if result2 is None:
            print("\n两种方法都未找到结果，可能需要扩大搜索范围或调整字符集。")
```

# linux指令

#### pwd：显示当前工作目录的路径

<img width="624" height="52" alt="image" src="https://github.com/user-attachments/assets/bcde47b5-0f37-4fb8-aab4-165c578fd19f" />


#### cd：切换工作目录

```
cd /path/to/directory
cd ..      返回上一级目录
```

<img width="301" height="82" alt="image" src="https://github.com/user-attachments/assets/dd4c4fc2-7e21-4023-8509-f25f1462e6bf" />




#### mkdir：创建新目录

```
mkdir directory_name
```

┌──(alvaro2006㉿kali)-[~/桌面]
└─$ mkdir alvaro2007

<img width="227" height="103" alt="image" src="https://github.com/user-attachments/assets/d14eccbc-d42d-426a-a023-c3ca67bf5009" />


、

#### rmdir：删除空目录

然后alvaro2007就被我删了

####  rm：删除文件或目录

```
rm file_name
rm -r directory_name  # 递归删除目录及其内容
```

alvaro2007下创建alvaro2008 ,alvaro2009

2009下创建ex1和ex2

ex2创建ex3

<img width="1314" height="196" alt="image" src="https://github.com/user-attachments/assets/2d08a9a9-a760-4e25-8d0e-144bca94d3e8" />


#### mv：移动或重命名文件或目录

```
mv old_name new_name
```

<img width="1373" height="245" alt="image" src="https://github.com/user-attachments/assets/0ba6c31d-d04a-4374-95dc-697d9ffd9ac9" />


#### touch：创建空文件或更新文件的时间戳

```
touch file_name
```

这个不试了，感觉比较鸡肋）

#### cat：连接和显示文件内容

```
cat file_name
```

<img width="1325" height="220" alt="image" src="https://github.com/user-attachments/assets/baa2bdec-ed85-4489-a891-8d9017d2dd87" />


#### more/less：逐页显示文本文件内容

```
more file_name
less file_name
```

<img width="1300" height="502" alt="image" src="https://github.com/user-attachments/assets/ee341862-0d42-4100-960a-9003a0d34bff" />


#### head/tail：显示文件的前几行或后几行

```
head -n 10 file_name  # 显示文件的前10行
tail -n 20 file_name  # 显示文件的后20行
```

<img width="1311" height="487" alt="image" src="https://github.com/user-attachments/assets/0f66a51f-0d3a-41f8-a96b-f8d82a6bfdbd" />


#### grep：在文件中搜索指定文本

```
grep search_term file_name
```

<img width="1356" height="466" alt="image" src="https://github.com/user-attachments/assets/2e2137ff-1333-4c31-9f3b-23b4d8fa7d64" />


grep 目标文件  目标文件里你要找的文本的名字       然后他会为你跳转至文本所在的地址

#### ps：显示当前运行的进程

```
ps aux
```

摘一个网图

<img width="1292" height="785" alt="image" src="https://github.com/user-attachments/assets/462b515b-4215-4bcb-bef9-1db808798a43" />

####  kill：终止进程

```
kill process_id
```

process_id对应上图的pid

#### ifconfig/ip：查看和配置网络接口信息

```
ifconfig
ip addr show

```

#### ping：测试与主机的连通性

```
ping host_name_or_ip

```

#### wget/curl：从网络下载文件

```
wget URL
curl -O URL
```

这个下载dirsearch时会用到

## 接下来的不再试探，只把名字和语法抄过来

#### chmod：修改文件或目录的权限

```
chmod permissions file_name
```

#### chown：修改文件或目录的所有者

```
chown owner:group file_name
```

这个看不懂

#### tar：用于压缩和解压文件和目录

```
tar -czvf archive.tar.gz directory_name  # 压缩目录
tar -xzvf archive.tar.gz  # 解压文件
```

#### df/du：显示磁盘使用情况

```
df -h  # 显示磁盘空间使用情况
du -h directory_name  # 显示目录的磁盘使用情况
```

#### mount/umount：挂载和卸载文件系统

```
mount /dev/sdX1 /mnt  # 挂载分区到指定目录
umount /mnt  # 卸载挂载的文件系统
```

#### psql/mysql：用于与PostgreSQL或MySQL数据库交互的命令行工具

```
psql -U username -d database_name  # 连接到PostgreSQL数据库
mysql -u username -p  # 连接到MySQL数据库
```

#### top/htop：显示系统资源的实时使用情况和进程信息

```
top
htop
```

#### ssh：远程登录到其他计算机

```
ssh username@remote_host
```

####  scp：安全地将文件从本地复制到远程主机，或从远程主机复制到本地

```
scp local_file remote_user@remote_host:/remote/directory
```

#### find：在文件系统中查找文件和目录

```
find /path/to/search -name "file_pattern"
```

#### grep：在文本中搜索匹配的行，并可以使用正则表达式进行高级搜索

```
grep -r "pattern" /path/to/search
```

#### sed：流编辑器，用于文本处理和替换

```
sed 's/old_text/new_text/' file_name
```



