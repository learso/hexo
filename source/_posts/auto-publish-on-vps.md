---
title: VPS上搭建自动发布hexo博客的环境
date: 2016-07-09 10:55:03
tags: [vps,hexo]
categories: 行
---


### 10:55第一次尝试
今天在VSP上搭了环境，自动发布hexo博客，这是一篇测试稿，成功后会详细介绍。

### 11:19第二次尝试
第一次尝试失败了，因为oschina的webhooks发的是post请求，而我VPS上的Flask用的是GET请求。修改程序后再试一次。
已经验证成功了!

### 12:54在手机上用网页编辑
手机登入网页，编辑，提交，测试能不能触发webhooks

### 07-10 5:54 发布到多平台
手机上发布还是有点不方便，主要问题时iphone上没有好用得git软件支持oschina。今天折腾了一下hexo发布到多平台，分别发不到github和coding.net，然后cname解析是设定国内的到coding.net，国外的到github，这样提高一下速度。现在可以通过网页写文章了
