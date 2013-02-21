---
layout: post
title: "golang解析网页入门"
date: 2013-01-29 09:17
comments: true
categories: golang goquery 
---

这段有个小任务，需要写一个爬虫，进行数据的分析
原本使用ruby写，可是目标网站需要多重的跳转，造成网络io延时很高，分析一次目标网站都需要10秒甚者更长。

这两天使用golang重写，把计算负责的和高io延时的全部并发出去，时间从原来的10秒降低到现在的3秒多一些。

使用的golang的库是goquery
下载方式是：
go get github.com/PuerkitoBio/goquery

使用这个库需要使用golang的exp库
下载这个库的方法是：
```bash
% cd $GOPATH/src
% hg clone https://code.google.com/p/go go-exp
requesting all changes
adding changesets
adding manifests
adding file changes
added 13323 changesets with 50185 changes to 7251 files (+5 heads)
updating to branch default
3464 files updated, 0 files merged, 0 files removed, 0 files unresolved
% mv go-exp/src/pkg/exp .
% rm -rf go-exp
% go install exp/...
%
```

使用这个goquery可以像jquery那样去分析dom

官方的doc可以打开自己本地的
godoc -http=":9090"
查看
也可以到godoc网站去看

