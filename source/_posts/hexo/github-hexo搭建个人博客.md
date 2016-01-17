title: github+hexo搭建个人博客
date: 2015-12-26 19:42:35
tags: hexo
categories: hexo
---

## hexo
[hexo](https://hexo.io)是一款基于Node.js的静态博客框架.
先尝试在本地搭建一个hexo博客:
- 安装Node.js
- 安装git
- 安装hexo

### 安装Node.js
>\$wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh  //重新启动Terminal
>\$nvm install v4.2.4  // v4.2.4是一个LTS版本


### 安装git
>\$sudo apt-get install git


### 安装hexo
>\$npm install -g hexo
>\$hexo version   // 此处安装的是3.1.1版本  

![hexo_version](http://7xpjap.com1.z0.glb.clouddn.com/Selection_001.png)


### 本地创建hexo
>\$mkdir you_dir
>\$cd you_dir
>\$hexo init
>\$npm install

### 写一篇博文
>\$hexo new post "Hello World"
>\$hexo generate
>\$hexo server

执行server命令之后即可以在浏览器打开博客页面


## 部署到github
如何建立一个github pages的内容以后再说明
可以在网上搜索类似的文章,本文主要描述将hexo部署到github

### 修改_config.yml文件
>deploy:
&nbsp;&nbsp;&nbsp;&nbsp;type: git
&nbsp;&nbsp;&nbsp;&nbsp;repo: git@github.com:xxxx // github ssh地址

### 安装git插件hexo-deployer-git
>\$npm install hexo-deployer-git --save

### 部署到github
>\$hexo deploy


如果一切顺利就可以看到自己的个人博客了.
