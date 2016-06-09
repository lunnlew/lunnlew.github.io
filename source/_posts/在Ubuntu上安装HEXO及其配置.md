---
title: 在Ubuntu上安装HEXO及其配置
date: 2016-04-13 22:19:43
tags: [Ubuntu,HEXO]
categories: [Linux应用,Ubuntu]
---

## 安装Node.js
``` sh
apt-get update
apt-get install -y python-software-properties software-properties-common
add-apt-repository ppa:chris-lea/node.js
apt-get update
apt-get install nodejs
```
## 安装git
``` sh
apt-get install git
```

## 安装hexo

``` sh
npm install -g hexo
hexo init myblog
cd myblog && npm install
```
