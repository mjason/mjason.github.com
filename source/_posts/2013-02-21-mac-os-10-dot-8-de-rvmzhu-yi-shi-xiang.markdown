---
layout: post
title: "mac os 10.8 的rvm注意事项"
date: 2013-02-21 15:23
comments: true
categories: rvm osx xcode4.6
---

因为xcode4.6把系统的gcc版本改成了llvm，如果没有设置好的话，在安装gem和rubu的时候会出错
下面是解决办法
```
brew update
brew tap homebrew/dupes
brew install apple-gcc42
rvm get stable
```

edit ~/.zshrc

```
export CC=gcc-4.2
```

install ruby
```
rvm install ruby-1.9.3 --enable-shared --without-tk --without-tcl
```


