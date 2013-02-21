---
layout: post
title: "简单的rails部署"
date: 2013-01-08 22:37
comments: true
categories: ruby 部署
---

rails的部署现在最流行的肯定是capistrano
刚开始学习的rails的时候，我也是用这个方式部署，不过每一次写部署脚本太伤了，各种错误，各种调试

自从有一次在ruby-toolbox看到了mina，终于有点感觉得到解救了

根据自己的使用mina的特点主要有：

1. 更加简洁的写法
2. 更加友好的提示界面

所以部署方式现在采用的是（rvm + mina + unicorn)

这里详细记录操作步骤

### 安装mina
```ruby
#in Gemfile

group :development do
  gem 'mina'
end
```

### 初始化mina 配置文件
```
#cd your app project dir
bundle
mina init
```

### 配置mina文件
```ruby
require 'mina/bundler'
require 'mina/rails'
require 'mina/git'
require 'mina/rvm'    # for rvm support. (http://rvm.io)

set :domain, 'foobar.com' #设置你的服务ip地址，或者域名
set :deploy_to, '/var/www/foobar.com' #部署的文件目录
set :repository, 'git://...' # git 地址
set :branch, 'master' # 确定分支

set :shared_paths, ['config/database.yml', 'log']

# Optional settings:
set :user, 'foobar'    # ssh 用的用户名.
#   set :port, '30000'     # SSH 端口，默认22.

task :environment do
  invoke :'rvm:use[ruby-1.9.3-p125@default]'
end

#mina setup 时会执行的操作
task :setup => :environment do
  queue! %[mkdir -p "#{deploy_to}/shared/log"] # 创建日志目录
  queue! %[chmod g+rx,u+rwx "#{deploy_to}/shared/log"] # 设置日志目录的权限

  queue! %[mkdir -p "#{deploy_to}/shared/config"] #创建目录
  queue! %[chmod g+rx,u+rwx "#{deploy_to}/shared/config"] # 目录权限设置

  queue! %[touch "#{deploy_to}/shared/config/database.yml"] # 生成服务器的database.yml
  queue  %[-----> Be sure to edit 'shared/config/database.yml'.] #提示编辑服务器的database.yml， 可以删除 
end

# 进行mina deploy会进行的操作
desc "Deploys the current version to the server."
task :deploy => :environment do
  deploy do
    # Put things that will set up an empty directory into a fully set-up
    # instance of your project.
    invoke :'git:clone'
    invoke :'deploy:link_shared_paths'
    invoke :'bundle:install'
    invoke :'rails:db_migrate'
    invoke :'rails:assets_precompile'

    to :launch do
      queue 'touch tmp/restart.txt' # 服务器重启服务器用的
    end
  end
end
```

根据自己的项目和服务器信息进行设置之后运行
```
# 服务器目录初始化
mina setup
# 进行项目部署
mina deploy
```

这样第一步就完成了

ssh 登录进服务器
然后建立一个专门用来部署的用户，安装rvm和ruby
网上的方法很多，这里就直接贴命令了,基于ubuntu12.04

```
ssh root@ip
adduser deploy
su deploy
curl -L https://get.rvm.io | bash -s stable
# 安装rvm的依赖
rvm requirements
rvm install 1.9.3
rvm use 1.9.3
gem install unicorn
# bootup可以自由写，推荐写项目名称
rvm wrapper ruby-1.9.3 bootup unicorn_rails
vim $HOME/.rvm/bin/bootup_unicorn_rails
```

因为mina的gem是安装在项目的vendor/bundle下面
所以需要修改一下rvm自动生成的脚本
将文件中的unicorn_rails 改为 你的项目地址+current/bin/unicorn_rails
eg: /home/deploy/test1/current/bin/unicorn_rails

接下来就是写启动脚本了，我的shell是以Ruby China的mimosa配置写的，这里就不重复<br>
直接贴上原帖地址和git地址 <br>
原帖地址：http://ruby-china.org/topics/471<br>
他提供的git地址: https://gist.github.com/3547765<br>

收工！！！



