---
title: hexo博客换电脑？
author: 刘小宅
avatar: 'https://pic2.superbed.cn/item/5d024654451253d1783b7967.jpg'
authorAbout: 热爱技术的人
authorDesc: 热爱技术的人
categories: 技术
comments: true
tags:
  - hexo
keywords: 技术
description: 热爱技术的人
photos: 'https://pic.superbed.cn/item/5d024595451253d1783b6202.jpg'
date: 2019-12-08 13:21:56
authorLink:
---

我搭建的博客是基于Hexo的，是比较简单的搭建方式，基于hexo是静态博客，所以一个麻烦事就是你的博客文章是写在你当前的电脑里面的，如果换电脑了话，所有的文章你需要自己再拷贝一份，比较麻烦。如果你编写博客的电脑gg了，那你的文章就都丢失了。

---

因此，该怎么办呢？最简单的方法，使用git的分支功能。

一个分支发布静态的网站文件，一个分支发布你编写的原始文件。

master分支：静态网站文件

hexo：原始文件。

### 机制

hexo d 上传部署到github的其实只是hexo编译后的文件，是用来生成静态网站的，不包含源文件，上传的文件是在：.deploy_git文件夹下的文件。

其他文件，例如我们编写的原始文件：source，配置文件：_config.yml文件，主题文件：theme等，都是没有上传到github上面的。

利用git分支的管理功能，将源文件上传到github的另一个分支即可。

### 创建分支

首先，在你的github上的项目下新建一个分支：

![创建分支](https://pic.superbed.cn/item/5dec8ca5f1f6f81c50761611.jpg)

这里，我已经创建好了，所以在你们的项目下是没有hexo分支的！！！

然后，在仓库是setting中，将hexo分支设置为默认分支（这样的好处是，以后你push的时候，不需要指定分支，默认是上传到hexo分支中。）

![](https://pic2.superbed.cn/item/5dec8dd8f1f6f81c50764309.jpg)

### 克隆

在任意的文件夹下，打开：git bash

```
git clone git@github.com:gakkiofzhuo/gakkiofzhuo.github.io.git
```

注意：换成你的项目的地址！！！

<font color="red">如果你有多个github账号，请记住换成你对应的github的账号地址，如果不清楚的，可以看我最早的博客文件，里面说明！！！</font>

<font color="red">此处就是：将@后面的地址换成你的.ssh下的config配置文件里面配置的地址。</font>

因为，hexo已经是默认分支了，所以clone下来的就是hexo分支的内容，不是master。

把之前，我们博客中的源文件拷贝过来，除了 .deploy_git 。

这里还需要说明一点就是，拷贝过来的文件中，还有一个 .gitgonre文件，这是用来忽略不需要提交到git的文件：

```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```

<font color="red">**注意：克隆过来的主题文件如果有.git文件，请将它删除，因为git不支持嵌套上传。查看有么有.git文件时，请打开隐藏文件可见！**</font>

---

### 上传

```
git add .
git commit -m "xxxx"
git push origin hexo  //这里可以不写 origin hexo，因为我们的远程仓库默认分支就是hexo
```

这样就大功告成了，可以去你的github看一眼，hexo分支此时：node_modules、public、db.json已经被忽略。

![](https://pic3.superbed.cn/item/5dec91acf1f6f81c50770a48.jpg)

### 另一台电脑

- 安装git

  ```
  sudo apt-get install git
  ```

- 设置git的全局用户和邮箱

  ```
  git config user.name "xxxx" --global
  git config user.email "xxxx@dddd.com" --global
  ```

- 设置ssh key

  ```
  ssh-keygen -t rsa -C "you email"
  ssh -T git@github.com
  ssh -T git@git.coding.net # 有coding平台的话
  ```

- 安装nodejs

  ```
  sudo apt-get install nodejs
  sudo apt-get install npm
  ```

  或者，你直接到nodejs的官网下载即可。

  ```
  node -v
  npm -v
  ```

  npm下载速度太慢，可以下载淘宝的镜像(Mac配置)

  ```
  sudo npm install -g cnpm --registry=https://registry.npm.taobao.org --verbose
  cnpm -v
  ```

- 安装hexo

  ```
  sudo npm install hexo-cli -g
  ```

- 克隆hexo分支

  ```
  git clone xxxxxxxx
  ```

- 安装hexo的部署工具

  ```
  cd xxxx # 进入你clone下来的目录中
  npm install
  npm install hexo-deployer-git --save
  ```

  <font color="red">PS：以上npm的命令，都可以换成cnpm（如果你下载速度过慢的话）</font>

- 生成、部署

  ```
  hexo g
  hexo s -p 8000
  hexo d
  ```

  