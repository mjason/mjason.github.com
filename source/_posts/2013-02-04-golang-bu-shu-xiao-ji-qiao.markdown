---
layout: post
title: "golang 部署小技巧"
date: 2013-02-04 19:51
comments: true
categories: golang 部署
---

golang的部署是很简单的事情，记录我这几天用到的部署技巧


如果你是第一次进行交叉编译， 那么执行下面的操作
```bash
$ cd /usr/local/go/src
$ CGO_ENABLED=0 GOOS=linux GOARCH=amd64 ./make.bash
```

然后运行
```bash
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build xxx.go
```

之后把编译好的文件发到服务器就好了

下面配置upstart把项目启动
sudo vim /etc/init/xxx.conf 
```bash
description     "xxx"
author          "mjason"

start on (net-device-up
          and local-filesystems
          and runlevel [2345])

stop on runlevel [016]

respawn

exec /path/file                   
```
最后使用sudo service xxx start

大功告成

然后用server