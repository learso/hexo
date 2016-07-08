---
title: hexo多电脑同步
date: 2016-07-08 14:15:00
categories: 行
tags: [hexo,blog,git,vps]
---


hexo功能强大，主题精美，所以毅然从pelican转向了hexo。然而，只要是静太博客生成项目，普遍存在的问题就是在不同电脑上使用没法做到同步。因为程序安装在地本的PC机上必不得不依赖于本地电脑，所以要解决在多台电脑上同步使用的问题，切入之处也在这里：<stong>程序需要放到服务器上</strong>。下面谈的方法对各表态博客都适用，这里以hexo为例。

<!-- more -->

## 可选方案
把程序放到服务器上的方式其实就这么几种：

### 网盘同步
这是最先想到的方法，也最先偿试了一下，用的是OneDrive，因为办公和家里的电脑都是Win10。操作起来很方便，就是把`hexo init <folder>`出来的folder放到OneDrive同步文件夹下，然后两台电脑上的OneDrive都开启自动同步，就这么简单。当然用Dropbox，百度云等工具都可以。

优点：操作简单

缺点：没有明显缺点

注意：所选择的网盘最好支持各操作系统，而且在linux下安装方便，否则只能在windows下写博客了

### git仓库同步
这种方案就是用免费的git仓库，把本地的hexo文件夹提交仓库进行版本管理，当在某一台电脑上需要时就`git pull`下来，更新完成后`git push`回去。这种方法操上比网盘同步复杂，但却显得更高大上，应该是Geeker最爱。

优点：适用于各种平台

缺点：部署、操作略复杂

注意：因为这种方法本身把博客当作一个软件项目来管理了，所以更具扩展性，后面说到的进阶方案就是基于此

### vps同步
如果有自己的VPS，就等于有了一个无限可能的平台，理论上只要你愿意，就有无限可能。可以在VPS上建立自己的git仓库，也可以在VPS上建立自己的网盘，只有想不到，没有做不到。

优点：完全由自己控制，想怎么搞就怎么搞

缺点：相关知识要求非常高，给你个VPS自己不会用也没用


## 暂时选择的方案
现在网盘和git两种方法同时在用，但慢慢会转向git方式。git方式部署环境还是比较复杂，记录一下流程：

### git安装
1. windows下去[https://git-scm.com/download](https://git-scm.com/download)下载安装包安装
2. centos可以用`yum install git`安装

### git仓库选择
可以选择的仓库很多，可以随便挑选一个：

1. [github](http://github.com)	全球最著名的git仓库
2. [coding.net](http://coding.net)	原来的gitcafe，现在改成coding.net
3. [oschina](http://git.oschina.net/)	免费支持private库，所以我选择了他

### 操作步骤

1. 删除hexo工作目录及其子目录下所有的.git文件夹，特别是`git clone`下来的主题目录
2. 在hexo工作目录下执行下列命令，初始化
```
git init
git remote add origin <your remote server url>

```
3. 把public目录以及一些不需要同步的文件放入.gitignore，不提交git仓库
```
*.log
public/
.deploy*/
.gitignore
```
4. 添加本地仓库并同步上git
```
git add .  
git commit -m "first commit" 
git push -u origin master
```
5. 在任何一台其他电脑上作如下操作可以把整个hexo环境下载到本机
```
git init
git remote add origin <server> #将本地文件和云端仓库映射起来。这步不可以跳过
git fetch --all #将云端所有内容拉取下来
git reset --hard origin/master #不做任何合并处理
```
6. 在新电脑上写完博客，发布文章
```
hexo d -g
```
7. 把更新提交到git仓库
```
git add .
git commit -m 'commit'
git push
```

## 进阶方案
进阶方案在我看来是最终的完美方案，需要有自己的VPS，并配合git仓库的WebHooks功能实现。暂时还只是设想阶段：

1. hexo项目已按照前文说的方法同步到git仓库
2. 在VPS上部署Nodejs, hexo运行环境
3. 在VPS上`git fetch`整个项目到本地
4. VPS的hexo工作目录下放一个可供http访问的脚本，可以用PHP,或者Python_Flask, 或者Nodejs+express，作用是执行`git pull`然后`hexo d -g`的功能
5. 把这个脚本的http地址配置进oschina的WebHook中，条件是项目有更新

已经有不少人通过这种方法实现了想要的功能，可以参考一下。

## 参考

[《利用git解决hexo博客多PC间同步问题》](http://chitanda.me/2015/06/18/hexo-sync-in-multiple-pc/)

[《VPS搭配Github Webhook实现Hexo自动发布》](https://xuanwo.org/2015/02/05/VPS-Hexo-Autodeploy/)

[《hexo利用github webhooks自动发布文章》](http://blog.sunnyyan.com/2015/05/01/hexo-auto-generate/)
