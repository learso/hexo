---
title: VPS上搭建自动发布hexo博客的环境
date: {}
tags:
  - vps
  - hexo
categories: 行
published: true
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

### 07-11 16：09
之前部署在[网易蜂巢](http://c.163.com)上，觉得后期可能不再续费，所以另外部署到了[Vultr](http://www.vultr.com)上。

### 07-11 22：21
整体迁移到github上

### 07-12 11:55
买了个新的VPS，打算放弃vultr，重新部署。现在彻底放到搬瓦工上，刚整理好环境。还是不行。？？？

```sh
yum install openssl-devel
```
