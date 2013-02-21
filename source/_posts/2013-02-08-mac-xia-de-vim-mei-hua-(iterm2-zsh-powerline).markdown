---
layout: post
title: "mac 下的vim 美化（iterm2 zsh Powerline）"
date: 2013-02-08 19:29
comments: true
categories: vim
---


因为近期一直在写前端，在自己喜欢的emacs下写比较麻烦，所以配置一些vim来写前端

### 1. 安装oh-my-zsh(这个强大的东西作为一个ruby开发者怎么可以没有)
```bash
curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh
```
并在.zshrc 里面添加或修改ZSH_THEME为ZSH_THEME="agnoster"  
note: 以后需要添加或者修改环境变量的时候记得要在~/.zshrc 里面做

### 2. 配置好看的主题和字体
1. 下载并安装需要用到的字体，下载地址如下
https://gist.github.com/qrush/1595572/raw/417a3fa36e35ca91d6d23ac961071094c26e5fad/Menlo-Powerline.otf
2. 在iterm2里面配置好字体preferences > profiles > text > Non-ASCll font 改为刚刚安装上去的字体
3. 配置正确的显示色彩 preferences > profiles > Terminal
将Report Terminal Type: 选择为xterm-256color <br>
并且勾上Set locale variables automatically

### 3. 配置vim
1. 安装插件pathogen（用来管理vim的插件的）  
```
mkdir -p ~/.vim/autoload ~/.vim/bundle; \
curl -Sso ~/.vim/autoload/pathogen.vim \
    https://raw.github.com/tpope/vim-pathogen/master/autoload/pathogen.vim
```
配置插件  
打开vim ~/.vimrc  
将execute pathogen#infect()添加加在第一行

### 4. 安装vim-powerline
这个插件必须安装，一个很好vim状态栏  
```
cd ~/.vim/bundle
git clone https://github.com/Lokaltog/vim-powerline.git
```

### 5.打开状态栏
将set laststatus=2 添加到 ~/.vimrc 里面



