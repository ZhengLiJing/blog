---
title: vim learn
date: 2018-06-20 20:42:01
tags: vim
categories: editor
---
学习vim的一些笔记。
####
使用命令计数

10 azheng < esc >
    zhengzhengzheng...zheng
cool!

    ####另起一行

// 当前行的下面另起一行
normal > o
// 当前行的上面另起一行
normal > O

#### a追加

3 a! < esc >
    当前光标后面追加3个！

#### 重做

u: 撤销上一次修改 <
    ctrl + r >: 重做上一次修改， u的逆过程

#### 滚动屏幕

    Ctrl + e: 向上滚动
    Ctrl + y: 向下滚动
    zz: 当前行置于屏幕中间
    zt: 当前行置于屏幕顶部
    zb: 当前行置于屏幕底部

#### 查找忽略大小写

    :set ignorecase

#### 在文本中查找下一个word

    光标定位到待查找的word,按*

#### 高亮搜索结果

    :set hlsearch
    :set nohlsearch
    :nohlsearch

#### 调理搜索命令
    
    // 键入目标字符串就开始搜索工作
    :set incsearch

