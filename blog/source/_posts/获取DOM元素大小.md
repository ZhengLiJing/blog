---
title: 获取DOM元素大小
date: 2018-06-20 21:01:23
tags: dom
categories: HTML
---
获取DOM元素的大小
#### 获取 DOM 元素的大小

<table>
    <thead>
        <tr>
            <th>clientX</th>
            <th>offsetX</th>
            <th>scrollX</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>clientWidth</td>
            <td> offsetWidth </td>
            <td> scrollWidth</td>
        </tr>
        <tr>
            <td>clientHeight</td>
            <td> offsetHeight </td>
            <td> scrollHeight</td>
        </tr>
        <tr>
            <td>clientLeft</td>
            <td> offsetLeft </td>
            <td> scrollLeft</td>
        </tr>
        <tr>
            <td>clientTop</td>
            <td> offsetTop </td>
            <td> scrollTop</td>
        </tr>
    </tbody>
</table>

#### clientLeft

    表示的是一个元素的左边框的宽度。

#### clientWidth

    元素自身宽度 + 元素的padding值
    注意：不包含元素的border和margin值

#### css选择器优先级

    1. id选择器默认优先级最高，权值为100
    2. class，属性选择器和伪类选择器的权值为10
    3. 标签选择器的优先级较低，权值为1
    4. 如果结果相同，后定义的样式优先级更高
    5. 如果样式值含有!important，则该值优先级较高。

    important>内联>id选择器>class=属性=伪类>标签>伪对象>通配符>继承

    1. important的权值最高：1000
    2. id：0100
    3. class=属性=伪类:0010
    4. 标签：0001
    5. 伪对象选择器的权值：0001
    6. 通配符的权值：0000
<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1527666681808.png" width="720"/>

#### 数组去重

    // method1
    // 外层循环传递进来的参数数组，内层循环返回结果数组，

    function unique(arr) {
        let res = [];
        for (var i = 0, len = arr.length; i < len; i++) {
            for(var j = 0, resLen = res.length; j < resLen; j++) {
                if(arr[i] === res[j]) {
                    break;
                }
            }
            if(j === resLen) {
                res.push(arr[i])
            }
        }
        return res;
    }

    // method2
    // 该方法和method1类似，区别在于使用indexOf替代内置循环

    function unique(arr) {
        var res = [];
        for (var i = 0, len = arr.length; i < len; i++) {
            if(res.indexOf(arr[i]) === -1) {
                res.push(arr[i])
            }
        }
        return res;
    }

    // method3
    // 排序后去重
    // 假想高低不同的一群人排成一队，如果直接比较相邻两个人，那他们有可能
        身高一致，也有可能不一致，