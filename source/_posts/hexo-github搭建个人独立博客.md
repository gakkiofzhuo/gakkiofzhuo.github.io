---
title: hexo+github搭建个人独立博客
author: 刘小宅
avatar: https://pic.superbed.cn/item/5d024654451253d1783b7967.jpg
authorLink: 
authorAbout: 热爱技术的人
authorDesc: 热爱技术的人
date: 2018-10-27 15:09:35
categories: 技术
tags: 
 - hexo
comments: true
keywords: hexo
description: hexo+github搭建个人独立博客
photos: https://pic.superbed.cn/item/5d024527451253d1783b5564.jpg
---

本人程序猿，秋招完事后，闲来无事就想写写自己的奋斗史，本来打算到一些网站上面写自己的博客的，突然觉得，有一个自己的博客岂不是更好，所以寻思自己搭建一个属于自己的博客。
<!--more-->

这个教程是基于window系统用户，Hexo3版本


### 安装前提软件

<font color="##97FFFF">**Node.js:**</font>  
作用：node.js用来创建hexo博客框架的，我当前安装版本为：node-v5.6.0-x64


<font color="##97FFFF">**Git客户端:**</font>  
作用：把本地的hexo内容提交到github上去，我当前安装的是Git-2.7.0-64-bit

### 安装Hexo

安装前先介绍几个hexo常用的命令,#后面为注释。

利用 npm 命令即可安装。在任意位置点击鼠标右键，选择Git Base

输入安装hexo命令：
```
npm install -g hexo

```

安装完成后，在你喜爱的文件夹下（如E:\Hexo），执行以下指令(在E:\Hexo内点击鼠标右键，选择Git Bash)，Hexo 即会自动在目标文件夹建立网站所需要的所有文件。
```
hexo init

```

安装依赖包:
```
npm install

```

让我们看看刚刚下载的hexo文件带来了什么，在E:\hexo内执行以下命令：
```
hexo g
hexo s

```

然后用浏览器访问http://localhost:4000， 此时，你应该看到了一个漂亮的博客了，当然这个博客只是在本地的，别人是看不到的，hexo3.0使用的默认主题是landscape。轻轻松松就看到了一点成果，是不是很激动，这就是hexo的强大之处，这个本地预览的功能，我真是爱不释手。

### 注册Github帐号

已经有Github帐号跳过此步，首先进入Github进行注册，用户名、邮箱和密码之后都需要用到，自己记好。

### 创建repository

repository相当于一个仓库，用来放置你的代码文件。首先，登陆进入Github，并进入个人页面，选择repositories，然后New一个repository.
<img src="/imgs/QQ截图20181027152902.png"/>

**创建时，只需要填写Repository name即可，当然这个名字的格式必须为youname.github.io，例如我的为liuzhuo.github.io.这里的用户名是你的登入账号的名字，不然后面会很麻烦！！！**

### 部署本地文件到github

既然Repository已经创建了，当然是先把博客放到Github上去看看效果。编辑E：\hexo下的_config.yml文件，建议使用Notepad++。
在_config.yml最下方，添加如下配置(命令中的第一个liuzhuo为Github的用户名,第二个liuzhuo为之前New的Repository的名字,记得改成自己的。**另外记得一点，hexo的配置文件中任何’:’后面都是带一个空格的)**,如果配置以下命令出现ERROR Deployer not found : github，则参考上文的解决方法
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: 
       github: git@github.com:liuzhuo/liuzhuo.github.io.git
  branch: master
```

配置_config.yml并保存。如果你是第一次使用Github或者是已经使用过，但没有配置过SSH，则可能需要配置一下:
在Git Bash输入以下指令（任意位置点击鼠标右键），检查是否已经存在了SSH keys。
```
ls -al ~/.ssh

```
如果不存在就没有关系，如果存在的话，直接删除.ssh文件夹里面所有文件：
<img src="/imgs/QQ截图20181027153549.png"/>

输入以下指令（邮箱就是你注册Github时候的邮箱）后，回车，出现提示让你输入的时候直接先回车，好像需要3次，如下图所示：
```
ssh-keygen -t rsa -C "43448934832@qq.com"
```
<img src="/imgs/QQ截图20181027153749.png"/>

然后键入以下指令：
```
ssh-agent -s

```
<img src="/imgs/QQ截图20181027153928.png"/>

继续输入指令：
```
ssh-add ~/.ssh/id_rsa
```
输入之后，在我这里是出错了，不知道你的有没有出错。
<img src="/imgs/QQ截图20181027154021.png"/>

如果你的也是这样子出错了的话，就输入以下指令：
```
eval `ssh-agent -s`
ssh-add
```
<img src="/imgs/QQ截图20181027154056.png"/>

到了这一步，就可以添加SSH key到你的Github账户了。键入以下指令，拷贝Key（先拷贝了，等一下可以直接粘贴，不放心的在执行下面命令后，先黏贴在记事本上）：
```
clip < ~/.ssh/id_rsa.pub

```

然后到Github里面，点击右上角的设置图标Settings,找到SSH keys,Ttile随便你命名，Key就黏贴上你刚才复制的key,然后点Add SSH key，最后会让你重新输入下gitHub的密码
<img src="/imgs/QQ截图20181027154157.png"/>


最后还是测试一下吧，键入以下命令：
```
ssh -T git@github.com

```

你可能会看到有警告，没事，输入“yes”就好
<img src="/imgs/QQ截图20181027154247.png"/>

以上就表示SSH配置好了，执行以下命令部署到Github上。
```
hexo g
hexo d

```

如果执行hexo d命令报下名错:
<img src="/imgs/QQ截图20181027154329.png"/>

就先安装一下hexo-deployer-git这个模块：
```
npm install hexo-deployer-git --save

```

安装好了继续执行 hexo d 部署命令，输入gitHub的账号密码，就可以访问了。我的是：liuzhuo.github.io
<img src="/imgs/QQ截图20181027154527.png"/>

---

### 发表一篇文章

在Git Bash执行命令：
```
hexo new "my new post"
```

在E:\hexo\source_post中打开my-new-post.md，打开方式使用记事本或者其他文本工具。
hexo中写文章使用的是Markdown，这里推荐使用markdownpad这个工具。 Markdown编写语法自己百度一下，不难。本人的另外一个博客上面有用法：
https://liuzhuo19940206.github.io/2018/10/12/markdown/

```
title: my new post #可以改成中文的，如“新文章”
date: 2016-02-21 16:04:09 #发表日期，一般不改动
categories: blog #文章文类
tags: [文章] #文章标签，多于一项时用这种格式，只有一项时使用tags: blog
--
这里是正文，用markdown写，你可以选择写一段显示在首页的简介后，加上
<!--more-->，在<!--more-->之前的内容会显示在首页，之后的内容会被隐藏，当游客点击Read more    才能看到。

```

写完文章后，你可以使用1.$ hexo g生成静态文件。2.$ hexo s在本地预览效果。3.hexo d同步到github，然后使用http://liuzhuo.github.io 进行访问。

### 参考

[使用Hexo搭建个人博客(基于hexo3.0)](http://opiece.me/2015/04/09/hexo-guide/#%E5%8F%82%E8%80%83)

[HEXO+Github,搭建属于自己的博客](https://www.jianshu.com/p/465830080ea9#)