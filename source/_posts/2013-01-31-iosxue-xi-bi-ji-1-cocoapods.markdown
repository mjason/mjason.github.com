---
layout: post
title: "ios学习笔记1--cocoapods"
date: 2013-01-31 19:07
comments: true
categories: ios 
---

###认识工具
在开发ios过程中不可避免要使用第三方的开发库，对于习惯了ruby，golang，python等编程语言的人来说安装这些东西无疑是痛苦的，总结起来步骤就有一下几个<br>

1. 下载源码
2. 根据第三方库的文档进行项目设置
3. 然后解决掉各种可能会出现的错误

遇到新的项目继续上面的工作，这是没办法忍受的事情，好在ios的黑客都是非常酷的人，他们开发出了像ruby的bundley一样方便的东西名字叫做[cocoapods](http://cocoapods.org/ "cocoapods")

因为某些原因官网上不了，请各位看官自备梯子。

###安装cocoapods
1. 首先你要安装好ruby，这个网上有很多，这里我就直接写出命令给各位了
```bash
#安装rvm,并安装ruby，在mac下只需要用下面一条命令
curl -L https://get.rvm.io | bash -s stable --ruby
```
2. 安装cocoapods
```bash
gem gem install cocoapods 
```
3. 好了之后，请进入你的ios项目里面新建一个名字叫做的Podfile的文件，在文件里面写入类似下面的文本
```ruby
platform :ios, '5.0'
pod 'AFNetworking', '~>1.1.0'
```
*注解一下：第一版是说明你使用ios的库，并使用5.0的sdk<br>
第二行就是你的需要用的库，格式是pod '库的名称', '版本号'*<br>
4.使用pod install进行安装库，安装完毕之后是使用项目目录下的xxx.xcworkspace进行编程就可以了