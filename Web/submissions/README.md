# 初识CTF
## 什么是CTF?
CTF（Capture The Flag）中文一般译作夺旗赛，在网络安全领域中指的是网络安全技术人员之间进行技术竞技的一种比赛形式。 

参赛选手通过完成攻击、分析，解密等各类操作，率先从题目给出的沙箱环境或文件样本中得到一串具有一定格式的字符串或其他内容，并将其提交给平台，从而夺得分数。为了方便称呼，我们把这样的内容称之为"Flag"。Flag的一般格式是一个统一的开头名称加上大括号内容，例如 `flag{hello_world}` 或者 `xxxctf{we1c0me!}`。 

**简而言之**，flag是一个答案，这个答案可能藏在任何一个规定的位置，需要你通过题目的关卡一步步拿到这个flag。 

在Web方向中，CTF 题本质是 “模拟真实 Web 漏洞攻防”，聚焦于网站与Web服务的安全问题，题目会搭建一个存在漏洞的网站 / 应用，要求你利用漏洞获取 flag 。

## 一些练习平台
1. [**NSSCTF**](https://www.nssctf.cn/) 提供题库、比赛和 Writeup 资源，国内很多比赛的题目可以在这里复现，非常适合系统练习和社区交流。
2. [**BUUCTF**](https://buuoj.cn/) 包含大量CTF比赛题目的聚合平台，适合题海战术式练习和复现经典题目。
3. [**Hello CTF**](https://hello-ctf.com/)Hello CTF是免费开源的CTF入门教程，拥有全面的知识点锦集、配套的题目靶场和完善的工具系统。
4. [**青少年CTF练习平台**](https://www.qsnctf.com)提供题库、比赛和 Writeup 资源
5. [**CTFSHOW**](https://ctf.show/) 一个适合初学者的 CTF 练习平台

## 一些网课推荐
1. [橙子科技](https://space.bilibili.com/271803648?spm_id_from=333.337.search-card.all.click) web常见安全漏洞学习，讲的很清晰，强推
2. [小迪安全](https://www.bilibili.com/video/BV1JZ4y1c7ro/?spm_id_from=333.337.search-card.all.click) 一些基础安全知识比较详细，网课比较体系
3. [蚁景网安](https://www.bilibili.com/video/BV1JD4y1b778/?spm_id_from=333.337.search-card.all.click&vd_source=6e75fa4663bf3074faec16dc03336d26) 零基础入门到精通

# 工具
## 前言
在web的学习中，我们需要用到一些工具来解题，需要你 **掌握这些工具的用法**。

以下会列出一些常用的工具，要求 **自行上网查找安装方法，提交工具安装的截图。**

后面会附有一些题目帮助你理解这些工具的使用，要求完成并提交 **Writeup**(即解题过程)。

## 列表
1. **浏览器开发者工具F12**（浏览器自带的，不用下）：最权威的一集。 
2. **Hackbar**: 浏览器插件，能够在页面上直接完成 请求/响应内容编辑，完成各种包括但是不限于伪造的工作。 
3. **Burp Suite****/ Yakit **： 代理抓包软件，用于Web应用程序的渗透测试和攻击，也有爆破等功能
4. **AI **：有不懂的都可以问，初学一定要利用好AI

以下这些工具不做要求，但是后面学习会用到，有时间可以自行学习：

+ **dirsearch **：目录扫描神器
+ **sqlmap**：自动化SQL注入工具
+ **蚁剑**： webshell 管理工具
+ **Docker：**拉镜像，搭靶场
+ ......

**工具是永远都找不齐的，重要的是对知识的理解。**

## 题目
这里有一些基础题目，会帮助你理解这些工具的用途，要求完成后提交Writeup。

**攻防世界这几题不用在系统上提交flag，靶机出现一点问题，只需要写wp、截图证明你拿到flag即可**

+ [攻防世界基础题单](https://adworld.xctf.org.cn/challenges/problem-set-index?id=25)：**view_source**
+ [攻防世界基础题单](https://adworld.xctf.org.cn/challenges/problem-set-index?id=25)：**get_post**
+ 用ai写一个python脚本，要求找到一个值经过md5加密后的前6位是`15af95`

暂时不要求：

+ [攻防世界基础题单](https://adworld.xctf.org.cn/challenges/problem-set-index?id=25)：**robots**

# Linux基础（重点）
## 环境搭建
你可以使用以下任意方式**搭建linux环境**，这里需要自行检索学习搭建方式，并提交搭建过程：

+ VMware虚拟机
+ WSL
+ 服务器平台

## 基础知识学习
了解什么是Linux，学习基本Linux命令，这里推

荐一些文章，也可以跟着网课学习：

[Linux入门教程（非常详细）从零基础入门到精通，看完这一篇就够了_linux学习-CSDN博客](https://blog.csdn.net/bigbangbangbang1/article/details/131575669)

[史上最全的Linux常用命令汇总（超全面！超详细！）收藏这一篇就够了！_linux命令汇总-CSDN博客](https://blog.csdn.net/weixin_44895651/article/details/105289038?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522972f9b1a663c2d6aefefccf5ddd72592%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=972f9b1a663c2d6aefefccf5ddd72592&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-105289038-null-null.142%5Ev102%5Epc_search_result_base8&utm_term=linux%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4%E5%A4%A7%E5%85%A8&spm=1018.2226.3001.4187)

[Linux 教程 | 菜鸟教程](https://www.runoob.com/linux/linux-tutorial.html)

**要求提交学习笔记**

# 关于作业的提交
## 作业格式
富文本格式，你需要去学习一下markdown的基本语法

[Markdown 基本语法 | Ma rkdown 教程](https://markdown.com.cn/basic-syntax/)

一些笔记软件：语雀 飞书 Typora

**提交在当前目录下 **[**24-Jatopos**](https://hnusec-star.feishu.cn/wiki/IeA6wWPHHiMELAkZ1XfcSAvMnOg)

## 作业列表
你需要提交以下内容，要求图文结合：

1. 记录工具安装的过程，提交要求题目的Writeup（**攻防世界这几题不用在系统上提交flag，靶机出现一点问题，只需要写writeup、截图证明你拿到flag即可**）
2. 记录linux搭建的过程，提交linux基础命令的学习笔记
3. 学有余力可以继续学习其他内容和知识（如http协议、php基础语法），并提交笔记

## 截止时间
10.19

完成多少就交多少，但不要不交

如果有事导致无法按时完成，向负责人解释清楚原因，否则视为放弃培训，直接移除。

# 结语
万事开头难，如果你对入门比较茫然请不要放弃，学一段时间你会发现Web其实入门很简单，但是想要真正学好Web，就一定要做好吃苦和坚持的决心。

同时希望大家不要只局限于我们任务的布置，也要培养自主学习和检索信息的能力，养成主动去学习的习惯，可以自己去找文章或者网课，这些都是会纳入我们考核的范围的。

有任何问题都可以发在群里，或者联系培训群里web方向的学长，希望大家可以积极起来，多多交流。

希望大家经过我们的培训，都可以有所收获。

