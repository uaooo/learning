# **view_source**

右键无法查看源代码，可以ctrl u或者url前加入view-source: 查看源代码。

![image-20251017195516561](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20251017195516561.png)

# **get_post**

![image-20251017195630960](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20251017195630960.png)

![image-20251017195827907](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20251017195827907.png)

# **robots**

![image-20251017200001697](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20251017200001697.png)

![image-20251017200018173](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20251017200018173.png)

# linux搭建

![image-20251017200458720](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20251017200458720.png)

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

