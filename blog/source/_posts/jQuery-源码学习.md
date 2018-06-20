---
title: jQuery 源码学习
date: 2018-06-20 21:04:10
tags: jQuery
categories: jQuery
---
jQuery源码学习笔记
架构
    (21, 94) 定义了一些变量和函数 jQuery = function() {};

    (96, 283) 给JQ对象添加一些方法和属性

    (285, 347) extend：JQ的继承方法，扩展

    (349, 817) jQuery.extend(): 扩展一些工具方法

    (2880, 3042) Callbacks: 回调对象,对函数的一个统一管理

    (3043, 3183) 延迟对象， 对于异步的统一管理

    (3184, 3295) support(): 浏览器功能检测方法

    (3308, 3652) data(): 数据缓存

    (3653, 3797) queue()队列管理,dequeue()

    (3803 , 4299) attr() prop() val() addClass()等方法，对元素属性的操作。

    (4300, 5128) on() trigger() : 事件操作的相关方法，事件委托

    (5140, 6057) DOM操作的方法： DOM的添加，获取，删除，包装 DOM筛选

    (6058, 6620) css() : 样式的操作,兼容性，浏览器的支持程度。

    (6621, 7854) 提交的数据和ajax(): ajax(), load(), getJson() ,getScript()

    (7855, 8584) animate(): 运动的操作方法

    (8585, 8792) offset(),scrollTop(): 位置与尺寸的一些方法

    (8804, 8821) JQuery支持模块化的模式

    (8826) window.jQuery = window.$ = jQuery： 对外提供的接口


#### 匿名函数传入window

    (function (window, undefined) {

    })(window)
    1. window:查找速度快，压缩
    2. undefined： 在IE8以下可以被修改，传入undefined防止被修改
    3. rootjQuery: rootjQuery = jQuery(document); // 利用压缩
    
    // 核心之一
    function jQuery() {
    return new jQuery.prototype.init();
    }

    jQuery.prototype = {
        constructor: jQuery,
        init: function () {
            return this;
        },
        css: function () {
            console.log('css');
        }
    }
    jQuery.prototype.init.prototype = jQuery.prototype;
    jQuery().css()

    4. 正则
        rmsPrefix = /^-ms-/,
        作用：Matches dashed string for camelizing
        -webkit-margin-left: 20; => webkitMarginLeft: 20px;
        -ms-margin-left: 20px; => MsMarginLeft: 20px

        var res = /[+-]?(?:\d*\.|)\d+(?:[eE][+-]?\d+|)/;
        匹配: +2.4e12,-2.4E-12

        var res = /^(\w+)\s*\/?>(?:\/\1>|)/$
        匹配： <div>zhengljign</div>
        问题： 最后的竖线代表什么？

        rquickExpr = /^(?:\s*(<[\w\W]+>)[^>]*|#([\w-]*))$/
        匹配： <li>hello  或者 #div-
        问题：|#([\w-])是什么意思？
        
    5. 构造函数

    6. 109 // Handle HTML strings

        $('#div'), $('.box'), $('div'), $('#div1 div.box')

        $('<li>'), $('<li>1</li><li>2</li>');

        if() {
             $('<li>'), $('<li>1</li><li>2</li>');// 标签
             match = [ null, '<li>', null ];
             match = [ null, '<li>1</li><li>2</li>', null ];
        } else {
            $('#div'), $('.box'), $('div'), $('#div1 div.box')// 不是标签
            $('<li>hello');

            match = null; // $('.box'), $('div'), $('#div1 div.box')

            match = [ '#div1', null, 'div1' ]; // $('#div1');

            match = [ 'li>hello', '<li>', null]
        }

        if() 能进入的有：  $('<li>'), $('#div')
        进一步判断： if () { $('<li>') } else { $('#div') }




