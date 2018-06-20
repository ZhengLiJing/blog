---
title: wy 面试
date: 2018-06-20 21:03:33
tags: wy interview
categories: interview
---
面试相关
#### 电话面试（一面）

    面试官小哥超好，我都不得不这么说，给我提了很多中肯的建议。
    JS:
    1. 首先是==和===，还有就是哪个涉及到的算法更多？
    2. 作用域，典型问题，for循环里使用回调函数，如何解决这个问题。
    3. ES6，Promise，await，async,Promise和await的执行顺序
    4. JSONP的原理，和优缺点
    5. nodelist，类数组对象的概念，如何将其转化为数组。
    6. 防抖
    CSS：
    1. 垂直居中
    2. 两栏布局，左边定宽，右边自适应
    3. flex，一个div下有三个flex-item，设置属性flex-grow:1,问3个容器的长度一定都是一样的吗？
    4. 雪碧图，优缺点，实现原理
    工作：
    1. 脚手架工具，脚手架框架使用过吗？
    2. Vue的父子间通信，相互通信
    3. weex的优点和缺点


#### ==和===

    JS一共提供三种不同的值比较操作
    1. ==
    2. ===
    3. Object.is()

    两个等号的比较不会比较值的类型，有隐式类型转化。三个等号的比较会比较值的类型，更为严格。
    两个等号的背后使用的算法更为复杂。
    绝大多数应该使用三个等号，只有检测null和undefined时会使用两个等号，因为通常我们不区分
    null和undefined，null == undefined是 x === null || x === undefined的缩写。
    两个等号的缺点是可能会造成类型判断的错误，比如：
    if(x == 10) {x += 5}
    如果x = '10',那么得到的结果就不是15，而是105，后续的运算又会进行另一次转型，从而引起隐蔽的错误。
    两个等于号的便利性无法与其带来的风险相比较。

    Object.is(),行为方式和3个等号相同，但是对于NaN和-0和+0进行特殊的处理。

#### 作用域

    for (var i = 0, len = 10; i < len; i++) {
        setTimeout(() => console.log(i),0)
    }
    // 打印10个10
    解决方法： 方法一，使用ES6的let关键字，使得大括号就有块级作用域
            方法二，使用IIFE，立即执行函数
        for (var i = 0, len = arr.length; i < len; i++) {
            setTimeout((function (i) {
                console.log(i)
            })(i), 0)
        }
        方法三：将setTimeout或其他异步请求抽离成一个函数，然后传值调用他，这样在函数中会保存i的一个副本，从而
        保证结果与预期一致。
    原因：JS的单线程的，setTimeout的回调函数会被放在任务队列中，当主线程的任务完成后，才依次
        从任务队列中取出回调函数到主线程执行。这个时候，变量i已经变成4了。
    作用域：JS只有函数作用域，没有块级作用域。

#### Promise async await

    Promise对象，resolve方法会立即被执行。
    Promise是异步编程的一种解决方案。比传统的事件和回调函数更为合理和强大。
        比事件更为合理的地方在于：当一个promise的实例已经resolve（定型），再对promise对象
        添加回调函数，会立即得到结果。这和事件完全不同，如果错过了它，再去监听，是得不到结果的。(这就话怎么去实践)

    fetch()
        window.fetch(),使用该方法执行请求。返回一个Promise对象。
        返回的响应中暴露出一个json()方法，用该方法可获取json格式的响应的主体数据。
        let url = 'https://www.reddit.component/r/javascript/top/.json?
                    limit="5"');
        window.fetch(url).then(res => res.json())
                            .then(json => {
                                console.log(json);
                            })

    async await

    将函数标记成async异步的，然后使用await关键字等待承诺的结果。
    比如说，我想获取一个reddit(社交新闻站点)上关于javascript的前5名话题。
    先创建一个函数叫fetchTopFive(url) {}
    然后，在该函数前使用async关键字将该函数声明为异步的，在函数内部调用fetch函数时，
    使用await关键字等待Promise的结果。

#### 两栏布局，左边定宽，右边自适应

    codepen

#### CSS 垂直居中

    1. 元素宽高已知，使用position定位，left:50%,top:50%,负margin
    2. 元素宽高已知，使用position定位，left:0,right:0,top:0,bottom:0,
                        margin:auto;
    3. 元素的宽和高不定时（宽高已知也适用），使用position定位,left:50%,top:50%,
    加transfor:translate(-50%, 50%);
    4. 使用flex。宽高可以不确定。
        flex-direction: row;
        justify-content: center;
        align-items: center;

#### flex，一个div下有三个flex-item，设置属性flex-grow:1,问3个容器的长度一定都是一样的吗？

        不一定，如果某个项设置了flex-basis的话就不同了。
        剩余空间的概念：
        假设一个div.container下有三个项,分别为b1,b2,b2
        假设container的宽度为500px,三个子项的宽度为100px;
        那么container多出来的500-100*3=200px就是剩余空间。

        剩余空间用在哪里?
        flex-grow是用来分配这个剩余空间的。其默认是0，假设b2
        设置了flex-grow:1,那么b2将获得这个剩余空间，此时b2的
        宽度为：100+200 = 300px;可以使用$1.clientWidth验证。

        flex-basis又是做什么的？
        简单来说和width相类似，某个项目设置了flex-basis后，会预先向父容器预约这么多空间，然后计算剩余空间。
        假设b2设置了flex-basis: 120;b3设置了flex-grow: 1,
        那么b2的宽度则为120;此时的剩余空间为500-100*2-120=180;
        b3的宽度为：100+180=280；
        flex-basis优先权高于width;

        flex-shrink
        当子项的宽度超出了父容器的宽度，有两种选择，一个是直接换行，
        但是flex子容器默认是不自动换行的，除非在父容器中设置flex-wrap。
        还有一种选择是每一项都压缩一点，使之包裹满父容器。flex-shrink就是
        设置压缩比例的。假设b1的width=300px,b2的width=120px,b3的width=160px;
        此时，各自的压缩比例为1：1：1，假设b1,b2,b3的压缩率为x1=x2=x3=x,则满足如下公式：
        500=300x+120x+160x
        得到x=25/29
        b1此时的空间：300*25/29=258.6,约等于259
        b2此时的空间：120*25/29=103.4,约等于103
        b3此时的空间：120*25/29=137.9,约等于138

#### CSS Sprite

    一种CSS图像合并技术，将小图标和背景图像合并到一张图片上，然后利用css的背景定位来显示需要显示的图片部分。
    雪碧图快速制作工具：CSS Sprite

#### JSONP的原理，和优缺点

    原理是：含src属性的script标签不受浏览器的同源策略限制。

    首先是前端设置好回调函数，比如说叫做callback(para),这个函数接受一个参数，
    在函数里按照需求进行处理和展现。

    然后浏览器端动态创建script标签，在URL上附上callback这个参数，告知服务器我想要
    一段调用callback的的js代码，然后服务器按照客户端的要求，将数据放在callback的参数
    中返回。

    最后，浏览器接受到服务器返回的脚本，立即执行，配合第一步设置好的回调函数，就可以拿到
    想要的数据并按照需求进行处理和展示。

    body下附加子节点
    document.body.appendChild(script);

#### 类数组转换为数组

    类数组对象：类似数组的对象，拥有索引和length属性
    arguments
    nodeList
    字符串String
    TypedAray:该对象描述一个底层的二进制数据缓冲区的一个类数组对象。
    

    1. for in 对象，将每个项目Push到一个新数组中。
        let newArr = [];
        for(var item in nodeListObj) {
            if(nodeListObj.hasOwnProperty(item)) {
                newArr.push(item);
            }
        }
    2. var arr = Array.prototype.slice.call(nodeListObj);
        或者，[].slice.call(nodeListObj);
    3. var arr2 = Array.from(nodeListObj);
    4. var arr3 = [...nodeListObj]

#### 网易研究院电话面试（二面）

    0. 自我介绍

    1. 盒子模型（丁香园面试中有过总结）
        front-end-intervier-1.md中有介绍，这是别人
        对这个问题的介绍。里面有很多有用的知识，找个时间
        看看。
    2. 垂直居中（单独录一个视频，经常被问到。）
        flex
        position + 负margin
        参考：https://www.cnblogs.componentcoco1s/p/444383.html
    3. 事件委托，获取这个目标元素

    4. Vue的核心，双向数据绑定(todo)
    5. 浏览器兼容，浏览器探嗅技术，获取浏览器版本，如何知道浏览器是否支持某个API
    6. 最近在看什么？
    7. BFC
    8. 浮动，清除浮动及原理
    9. 如何调试，source-map
    10. 渲染
    11. 缓存，静态资源缓存，浏览器缓存
    12. 工作中遇到的问题，怎么解决的？
    13. 对前端的理解，如何学习前端？
    14. 对这个岗位有什么期待？
    15. 如何调试移动端
    16. 400 403分别代表什么意思？

    0. 自我介绍

    1. 盒子模型

    2. 垂直居中

    3. 事件流

        事件捕获阶段，处于目标阶段，冒泡阶段。
        事件捕获阶段：从不具体元素到具体元素。比如页面中有一个按钮，然后在window上
                    注册捕获事件，那么该事件只会在捕获阶段起作用。
        处于目标阶段：事件到了具体元素时，在具体元素上发生，并看做是冒泡阶段的一部分。
        冒泡阶段：事件从具体元素冒泡到不具体元素

        阻止事件冒泡方法：event.stopPropagation();
    
    4. vue的核心
        
        Vue是一套构建用户界面的渐进式框架
        Vue.js是一个提供MVVM数据双向绑定的库，核心在于：数据驱动+组件系统
        Vue的核心功能强调的是状态到界面的映射。
        渐进式：声明式渲染，组件系统，客户端路由，大规模状态管理，构建构建。

    5. 浏览器兼容，浏览器探嗅技术，获取浏览器版本，如何知道浏览器是否支持某个API

        let ua = navigator.userAgent;// 获得浏览器代理信息

        客户端检测
        1. 能力检测(特性检测)，指的是探测浏览器的能力，不是针对特定的浏览器。

            两个重要的概念：
                1.1: 先检测最常用的特性
                1.2: 一个特性存在，不代表另一个特性也存在，
                    比如，你检测到document.all存在，就返回document.innerWidth，
                    而innerWidth是在IE9才被支持。也就是说，检测到document.all不
                    一定代表这个浏览器就是IE，可能是Opera，Opera同时支持这两个API。
            // 检测浏览器的能力，不针对特定的浏览器。
            if(document.getElementById) {
                return document.getElementById(id);
            }else if(document.all){
                return document.all[id];
            }else {
                throw new Error('No way to retrieve element');
            }

            // 若要用到某些特性浏览器特性，最好一次性检测完，节省检测能力的时间
            const hasDOM1 = !!(document.getElementById && document.createElement
                                && document.getElementsByTagName);
        
        2. 更为准确的能力检测

            2.1：当检测某个对象是否存在sort()这个函数时，如果使用能力检测，会这么做：
                function isSortable(object) {
                    return !!object.sort;
                }
                但是，这个方法存在隐患，任何含有sort属性的对象都会返回true，而我们
                检测的是sort这个函数是否存在，与我们预期不符。更为正确的做法是检测
                sort是否是函数：
                function isSortable(object) {
                    return typeof object.sort === 'function';
                }
                但是，这个函数还是存在兼容性问题，对于IE8，typeof object.sort
                返回的竟然是object,所以使用typeof不一定返回合理的值。因为IE更
                早的版本的宿主对象使用的是COM而非JScript实现的。IE9才纠正了该
                问题。

        3. bug检测

            最好在脚本开头就检测这些bug，手段是运行一小段代码，尽早排除出错的可能。

        3. 用户代理检测

            万不得已的情况下进行检测，优先级从高到低是能力检测，bug检测，用户代理。
            用户代理检测的原理是：通过检测用户代理字符串来判断实际使用的浏览器。
            每次发送HTTP请求时，浏览器字符串作为响应首部发送的。如：User-Agent:
            Mozilla/5.0 (Window NT 6.1; Win64; x64) AppleWebkit/537.36
            (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36
            服务器根据浏览器根据发送过来的用户代理字符串检测用户使用的浏览器。
            所以就存在浏览器厂商的欺骗性的可能。像Window的IE，Opera就存在
            欺骗服务器的检测。
            客户端通过navigator.userAgent获取用户代理字符串
            浏览器  呈现引擎
            IE      Trident（三叉戟)
            Firefox Gecko(壁虎)
            Chrome  Webkit(最新是Blink)
            Opera   Presto(迅速的)
            Konqueror(Linux) KHTML

#### BFC

    Block Formatting Contexts(块级格式上下文)
    浮动元素float,绝对定位元素，非块盒的块容器，如inline-blocks内联块,table-cell单元格，table-captions，overflow值不为visible的元素
    可构建一个新的块级上下文。
    同属于一个块级上下文中的两个相邻盒子间的垂直外边距会合并。如：
    <div class="wrapper">
        <div>p1</div>
        <div>p2</div>
    </div>
    // CSS
    .wrapper {overflow: hidden;}
    .wrapper div {margin: 100px;}
    因为父容器wrapper是BFC，同属于一个BFC的两个相邻的BOX的margin值会重叠，
    也就是说p1和p2的之间的margin只是100，因为发生了重叠。

    BFC布局规则第3条：
>  在一个块级格式上下文中，每个盒子的左外边界(left outer edge) touch the left edge of the containing block.

    BFC布局规则第4条：
>  BFC的区域不会和浮动盒子相重叠。a box's line boxes may shrink due to the floats
    根据这个应用在两栏布局中

    BFC布局规则第4条：
>  计算BFC的高度时，浮动元素也参与计算
    用来清除浮动
>  同属于一个BFC的两个相邻的BOX的margin值会重叠,也就说，只要不属于
    同一个BFC的box外边距就不会发生重叠。
    用来防止垂直margin重叠

#### 浮动，清除浮动和原理

    什么是浮动？
    通俗的理解为让某个div元素脱离标准的文档流，漂浮在标准文档流之上，和标准流不在一个层次上。
    比如，有四个块级盒子，依次垂直排列，四个盒子处在标准流之中，假设第二个盒子左浮动，那么它就
    脱离标准的文档流，漂浮在标准文档流之上，而其他三个盒子组成了新的标准文档流。因为第二个盒子浮动
    了，所以它会漂浮在第三个盒子之上，如果第二个盒子的长度小于第三个盒子，那么第二个盒子会部分遮盖
    第三个盒子。

    浮动也可以理解为：浮动的框可以左右移动，知道它的外边缘遇到包含块或者另一个浮动框。浮动框不属于
    标准的文档流(普通文档流)，浮动框元素不会影响块级框的布局，而只会影响内联框(通常是文本)的排列，
    标准文档流将浮动元素视为不存在，当浮动框的元素的高度超出包含框时，就会出现包含框不会自动升高
    来闭合浮动元素(高度坍塌现象)。

    假设第二个盒子和第三个盒子都左浮动，那么这两个盒子就脱离了文档流，第一个和第四个盒子组成了新的
    标准文档流，因为第二个盒子之前的盒子属于标准文档流，所以第二个盒子保持相对垂直位置不变，第三个
    盒子前一个盒子处于浮动，所以，第三个盒子可能挨着第二个盒子，排列在同一行上，也有可能因为一行放不下
    这个两个元素，导致第三个盒子被挤到下一行。
<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1528601166549.png" width="454"/>

    高度坍塌：
    <div class="wrapper">
        <div class="box1">box1</div>
        <div class="box1">box2</div>
    </div>
    盒子box1和box2如果都浮动的话，包含框内由于不存在其他普通文档流了，
    那么父容器表现出高度为0，就会产生高度坍塌

    清除浮动的原理


    如何清除浮动？

    clear: 这个规制只能影响使用该规则的元素本身，不能影响其他元素。
            比如说，盒子A和盒子B都左浮动，那么像要让盒子B不挨着A
            盒子，在盒子B上使用清除浮动clear:left就可以达到目的。

    分为两类：
    一类是在浮动元素后面添加一个空元素，
        1. <div class="clearfix"></div>
        2. <br clear="all">
        3. .clearfix:after {
            display: block;
            content: '.';
            visibility: hidden;
            height: 0;
            clear: both;
        }
        /*
            .clearfix:after {
            display: block;
            content: '\200B';
            height: 0;
            clear: both;
        }
        */
        .clearfix {*zoom: 1}

    另一类是父容器触发BFC，因为BFC有条规则规定，BFC的区域不会和浮动盒子相重叠。
    .wrapper {display: table;}其本质是产生了匿名框，匿名框中的display:table-cell创建新的BFC。
    .wrapper {display: inline-block;}
    .wrapper {display: table-cell;}
    .wrapper {overflow: hidden;}


#### 块级元素，内联元素(行内元素),内联块状元素

    块级元素(block)：div,p,h1,form,ul,li等。
    特点：1. 独占一行
         2. 可设置高和宽、行高以及顶和底边距都可以设置
         3. 宽度不设置时，默认是父容器的100%。

    内联元素(inline):span,a,br,em,strike,label,code,cide,strong
    特点：1. 和其他元素在一行上
         2. 不可设置高宽、行高、顶部和底边距
         3. 元素的宽度就是它包含文字和图片的宽度，不可改变。

    内联块状(inline-block),通过设置display:inline-block，
        img、input就是这类元素
    特点：1. 和其他元素在一行上
         2. 可设置元素的宽、高、行高、顶和底部边距。

#### debugger

    1. console.table()
    console.table(obj);
    console.table(arr);

    2. source 断点

    Pause/Resume script execution：暂停/恢复脚本执行（程序执行到下一断点停止）。
    Step over next function call：执行到下一步的函数调用（跳到下一行）。
    Step into next function call：进入当前函数。
    Step out of current function：跳出当前执行函数。
    Deactive/Active all breakpoints：关闭/开启所有断点（不会取消）。
    Pause on exc
    eptions：异常情况自动断点设置。

    3. debugger断点

    4. DOM断点

        subtree modifications:子元素的增删改断点
        attribute modifications:元素属性的修改断点
        node removal:节点删除断点

    5. XHR 断点

        Break when URL contains
        $.get('http://seejs.me?test=ajax', function(data) {})

    6. Event Listener Breakpoints

        Mouse:
            mousemover
            mouseout
            mouseenter
            mouseleave
            mousewheel
            wheel
            contexmenu
        Timer
            setTimeout
            clearTimeout
            setInterval
            clearInterval
            setTimeout fired
            setInterval fired
        XHR
            readystatechange
            load
            loadstart
            loadend
            abort
            error
            progress
            timeout
        drap
            load
            beforeunload
            unload
            abort
            error
            hashchange
            popstate

#### UED

    abbr. 用户体验设计（user experience design）

#### 页面渲染原理、HTTP工作原理、算法及数据结构

#### 离线存储

    随着HTML5标准的一步步确定，现代互联网前端拥有了localStorage、sessionStorage等本地存储技术，
    甚至拥有了建立本地数据库，通过JS调用API完成CURD操作的能力，这一切让离线存储成为了可能，
    但这也意味着我们的前端工程师需要掌握更多更复杂的技能。

#### CSS

    在表现（css）方面，前端的变化同样是一日千里。从最初的固定布局，
    到后来的栅格系统，再到自适应、响应式布局，一步一步见证着css设
    计的日渐强大。为了更加灵活简便的进行css设计，各种css预处理技
    术（LESS、SASS、Stylus）日渐流行，从此前端开发工程师也可以
    像写程序一样编写css样式了。

    css3的出现，让网页更小更美。圆角、阴影、背景渐变，以及
    font-face配合网页图标字体，让网页中图标资源的使用得到
    了有效控制。过渡、动画，带给网页飞一般的流畅体验，
    将界面层面的动画交给css实现，让JS可以更专注的完成业务逻辑处理。

#### HTTPDNS

#### 域名收敛

#### source-map

    1. 源码压缩导致调试困难，难以定位到源码中的原始位置
    2. Source map: 一个信息文件，存储位置信息。源代码压缩后的每一个位置，对应源代码原始的每一个位置。
    3. 启用Source map,在转换后的代码尾部加上： //@ sourceMappingURL=/path/to/file.js.map
    4. 生成Source map,Google Closure编译器
    5. Source map格式
        {
            version: 3,
            file: 'out.js',
            sourceRoot: '',
            sources: ['foo.js', 'bar.js'],
            names: ['src', 'maps', 'are', 'fun'],
            mappings: 'AAgBC,SAAQ,CAAEA'
        }
    6. mappings属性
        压缩后的代码各个位置是如何一一对应到源代码的各个位置。
        第一层是行对应，以分号表示。每个分号对应转换后源码的一行。
        第二层是位置对应，以逗号表示。每个逗号对应转换后源码的一个位置。
        第三层是位置转换，以VLQ(Variable Length Quality)编码表示，代表该位置对应的转换前的源码位置。

        源映射格式详解
        {
            version: 3, // Source map（源映射）版本号，目前统一使用版本3.
            file: 'min.js', // optional, 生成文件的路径（压缩后的文件），相对于Source map本身路径
            names: ['bar', 'baz', 'n'], // optional，所有名称，如变量，函数名。
            sourceRoot: 'http://example.com/www/js/', // optional, 所有源文件的根路径， 相对于Source map本身路径
            sources: ['one.js', 'two.js'], // optional, 所有源文件路径(未压缩文件)
            sourcesContent: ['', ''], // optional，所有源文件的内容
            mappings: 'CAAC,IAAI,IAAM,SAAUA,GAClB,OAAOC,IAAID;CCDb,IAAI,IAAM,SAAUE,GAClB,OAAOA' // 所有的映射点。
        }

        sources，捋一捋：
        源文件source: ['xld.js'],压缩生成了xld.min.js，也就是file: 'xld.min.js',以及生成了xld.min.js.map
        那么，在xld.min.js中需要通过// #sourceMappingURL=xld.min.js.map指定它的源映射。
        在xld.min.js.map中需要通过file: xld.min.js指定它生效的文件。file 并不是必须的字段，该字段只用于检验
        在xld.min.js.map中需要通过sources: ['xld.js']指定真正的源文件地址。

        mappings: 映射关系的核心,表面上看是由很多看似乱码的字符组成，其实mappings是一个数组通过一定的方式编码得到的，
                    这个数组包含了生成文件（压缩后的文件）中每行的映射列表。
        mappings = [
            第1行的映射点列表
            第2行的映射点列表
            ...
        ]
        每行的映射列表又是一个数组，包含了该行中所有列的映射点。
        mappings = [
            [ 第1行第1个映射点， 第1行第2个映射点，... ] // 第1行映射点列表
            [ 第2行第1个映射点， 第2行第2个映射点，... ] // 第2行映射点列表
            ...
        ]
        每个映射点又是一个数组，数组中包含了5个数字：
        [ 生成文件的列， 源文件索引， 源文件行号， 源文件列号， 名称索引 ]
        其中，名称索引可省略。源文件索引, 源文件行号, 源文件列号也可同时省略，
        这表示映射点的数组长度可能是 1、4 或 5。
        源映射所有行列号都是从 0 开始计数的。

        例子：
        {
            version: 3,
            file: 'min.js',
            names: ['bar', 'baz', 'n'],
            sourceRoot: 'http://example.com/www/js/',
            sources: ['one.js', 'two.js'],
            mappings: [
                [],
                [],
                [
                    [1, 0, 2, 5, 1],
                    [4, 0, 3, 6, 0] // #13行
                ]
            ]
        }

        以 #13 行数据为例：#13 行出现在 mappings[2] 里面，因此它表示生成的文件第 2 行的信息。
        #13行包含的5个数字的意思: 4表示生成文件的列，0表示源文件索引，这里指的是sources数组中的one.js,
            3表示源文件行号，6表示源文件的列号，0表示名称索引，这里指的是names数组中的bar
        最终的意思是：生成的文件('min.js')中，第2行第4列的位置是从第0个源码，也就是one.js中第3行第6列的位置生成，
        源码中的相关的名称是0(bar)

        mappings编码
            为了节约存储空间，mappings会被编码成一个字符串。
            第一步：计算相对值，将映射点中每个数字替换成当前映射点和上一个映射点相应位置的差，如：
            mappings: [
                [
                    [1, 0, 2, 5, 1],
                    [2, 0, 3, 6, 0]
                ],
                [
                    [5, 0, 2, 3, 0]
                ]
            ]
            其中第一个映射点不变，以后每个映射点上每个数字都减去上一个映射点(允许跨行)
            对应位置的数字(如果映射点元素个数不足 5，则省略部分按 0 处理)，最后得到：
            [
                [
                    [1, 0, 2, 5, 1],
                    [1, 0, 1, 1, -1],
                ],
                [
                    [3, 0, -1, -3, 0]
                ]
            ]
            第二步：合并数字
            将 mappings 中出现的所有数字写成一行，不同映射点使用,(逗号)隔开，不同的行使用;(分号)隔开。
            1 0 2 5 1 , 1 0 1 1 -1 ; 3 0 -1 -3 0
            第三步：编码数字
            对于每个数字，使用VLQ编码，转换为字母，具体方式是：
            1. 如果数字是负数，则取其反向数。
            2. 将数字转换为等效的二进制。并在末尾补符号位，负数补1，整数补0。
            3. 从右往左分割二进制，一次取5位，不足的左边补0。
            4. 将分好的二进制进行倒序
            5. 每段二进制前面补1，最后一段补0。
            一共是6位数字，范围是从000000-111111,即0-63
<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1528878774921.png" width="379"/>

            例子：170
            1. 正数
            2. 转换为二进制，10101010,符号为0，即101010100
            3. 从右往左5位分割，不足补0，01010 10100
            4. 倒序，10100 01010
            5. 每段二进制前补1，最后一段补0，即110100 001010
            6. 转换为10进制，52， 10.
            7. 查表的： 0K
            任意一个整数都能通过 VLQ 编码得到一串字母和数字表示的文本。

            第四步：合并结果
            将第二步中的每个数字进行 VLQ 编码再拼接就是最终的结果
            CAEKC,CACCC;GADHA
    

        参考链接： https://www.cnblogs.com/xuld/p/5882677.html
                 http://www.alloyteam.com/2014/01/source-map-version-3-introduction/