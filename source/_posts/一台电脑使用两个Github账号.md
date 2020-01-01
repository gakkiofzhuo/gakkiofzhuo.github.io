---
title: 一台电脑使用两个Github账号
date: 2018-10-27 11:33:29
author: 刘小宅
avatar: https://pic.downk.cc/item/5e0c344476085c3289327a49.jpg
authorLink: 
authorAbout: 热爱技术的人
authorDesc: 热爱技术的人
categories:
  - 技术
tags:
  - git
comments: true
keywords: git
description: 一台电脑使用两个Github账号
photos: https://pic1.superbed.cn/item/5d024569451253d1783b5d00.jpg
---
起因，主要是作者本人想在github上面部署两个静态博客，可是一个账号只能部署一个，所以只好申请两个账号。


### 思路

管理两个 SHH key

### 解决方案

#### 生成两个SSH key

为了举例方便，这里使用“one”和“two”两个账户。下同。
```
$ ssh-keygen -t rsa -C "one@gmail.com"

$ ssh-keygen -t rsa -C "two@gmail.com"
```

不要一路回车，分别在**第一个对话框**的时候输入重命名（id_rsa_one和id_rsa_two），这样会生成：  

id_rsa_one  
id_rsa_one.pub

id_rsa_two  
id_rsa_two.pub

两份包含私钥和公约的4个文件。

ps：ssh-keygen是linux命令，可以让两个机器之间使用ssh而不需要用户名和密码

一定要在~/.ssh路径下运行命令行，不然生成的文件不会出现在当前目录

#### 添加私钥

1、打开ssh-agent

(1)、如果你是github官方的bash：  
```
$ ssh-agent -s
```

(2)、如果是其他
```
eval `ssh-agent -s`
```

注意这里不是单引号，是键盘数值1的左边的按键(在英文模式下)。

2、添加私钥

以前是直接使用：$ ssh-add ~/.ssh/id_rsa（默认的情况下）

现在是：

```
$ ssh-add ~/.ssh/id_rsa_one

$ ssh-add ~/.ssh/id_rsa_two
```

可以通过ssh-add -l来确认结果

3、配置.ssh/config

在C:\Users\用户名\.ssh下。如果没有config文件就创建一个。

```
$ touch config
```
---

```
$ vi .ssh/config
 
# 加上以下内容
#default github
Host github.com
  HostName github.com
  IdentityFile ~/.ssh/id_rsa

# one(one@gmail.com)
Host one.github.com
  HostName github.com
  IdentityFile ~/.ssh/id_rsa_one

# two(two@ gmail.com)
Host two.github.com
  HostName github.com
  IdentityFile ~/.ssh/id_rsa_two

```

4、这样的话，你就可以通过使用别名github.com、one.github.com、two.github.com来明确说你要是使用哪个SSH key来连接github，即使用工作账号进行操作。

```
#本地建库
$ git init
$ git commit -am "first commit'
#push到github上去
$ git remote add origin git@one.github.com:xxxx/test.git
$ git push origin master
```
注意的是：git@后面使用我们指定的别名：github.com、one.github.com、two.github.com

#### 部署SSH key

分别登陆两个github账号，进入Personal settings –> SSH and GPG keys：
<img src="/imgs/QQ截图20181027141203.png"/>

点击 new SSH key,把在C:\Users\用户名\.ssh下的两个.pub结尾的文件里面的内容填写到Key里。Title：随便写
<img src="/imgs/QQ截图20181027142019.png"/>


#### 远程测试【可跳过】
```
$ ssh –T one.github.com

$ ssh –T two.github.com
```

#### 使用

1、Clone到本地

(1)、原来的写法
```
$ git clone git@github.com: one的用户名/learngit.git
```

(2)、现在的写法：
```
$ git clone git@one.github.com: one的用户名/learngit.git

$ git clone git@two.github.com: two的用户名/learngit.git
```

2、记得给这个本地仓库设置局部的用户名和邮箱：
```
$ git config user.name "one_name" ; git config user.email "one_email"

$ git config user.name "two_name" ; git config user.email "two_email"
```

3、部署成功后，会发现钥匙会由灰色变为绿色。

---

**PS：如果在上面的添加私钥时候。**
```
ssh-add ~/.ssh/id_rsa
```
输入之后，出现错误的话。错误如下：
<img src="/imgs/QQ截图20181027142809.png"/>

使用如下指令：
```
eval `ssh-agent -s`
ssh-add ~/.ssh/id_rsa
```