---
title: Shell 脚本
date: 2018-06-20 20:46:16
tags: shell
categories: shell
---
Shell 脚本学习笔记,
#### cat > nursers

    $ cat > nusers
    // who登录，wc(word count) -l(line)
    who | wc -l
    press <ctrl+D>(^D)
    $ ./nusers

#### 重定向与管道

    以<改变标准输入
    program < file可以将program的标准输入修改为file
    以>改变标准输出
    program > file可以将program的标准输出修改为file

    eg.
    tr -d '\r\n' < dos-file.txt > UNIX-file.txt
    以tr将dos-file.txt里的ASCII 回车换行删除，再将转换完成的数据输出到UNIX-file.txt

#### 基本命令查找
 	$PATH是一个以冒号分割的目录列表，在该列表目录下可以找到所要执行的命令.
    echo $PATH
    /Users/zhenglijing/.npm-global/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Users/zhenglijing/bin
    最后的一个/Users/zhengljing/bin是自己加入的：
    PATH=$PATH:$HOME/bin
    
    永久加入，可以在.profile文件中把你的bin目录加入$PATH,而每次登陆时都将读取.profile文件,例如：
    PATH=$PATH:HOME/bin

#### 简单的执行跟踪

    1. sh -x nusers    打开跟踪功能
    + who 
    + wc -l
        5

    2. 在脚本里，使用set -x命令跟踪功能打开，set +x跟踪功能关闭:
    cat > trace1.sh
    #! /bin/sh

    set -x 打开跟踪功能
    echo 1st echo

    set +x 关闭跟踪功能
    echo 2nd echo
    ^D

<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1526536458673.png" width="314"/>

#### shell脚本的执行方式

    // 不需要权限
    1. sh script.file
    // 需要+x权限 744 chmod +x script.file
    2. ./script-file

#### +运算
   
   $a=10
   $b=20
   echo $(($a+$b))

#### []判断

    1. []必须使用空格来分隔，和赋值刚好相反
    2. []内变量使用双引号括起来
    3. []常数使用单引号括起来
    
#### if
    
    #!/bin/env bash
    filename=/home/zhengljing
    if [ -f $filename  ];then
    echo 'exist'
    fi

    or
    if test -f $filename; then
    echo 'exist'
    fi

#### case
    
    echo 'Please input an number.'
    read number
    case $number in
    1)
        echo 'Your input number is 1';;
    2)
        echo 'Your input number is 2.';;
    3)
        echo 'Your input number is 3.';;
    *)
        echo 'I dont konw what you input';;
    esac
    
#### 循环
    
    // while

    #!/bin/env bash
    i=10

    while (($i>5));do
    echo $i;
    ((i--));
    done;

    or

    while [ $i -gt 5 ];do
    

    // until 表达式不成立执行
    until [ $a -lt 5 ];do
    echo $a;
    ((a--));
    done;

#### for

    for((i=1;i<=10;i++));do
    echo $i;
    done;

#### function

    function print(){
        echo "Your Input is $1"
    }
    echo "this program will print your selection"

    case $1 in
    "a")
        print 1;
    "b")
        print 2;
    "c")
        print 3;
    "*")
        print "useage $0 (one|two|three)";;
    esac
