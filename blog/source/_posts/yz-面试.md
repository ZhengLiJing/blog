---
title: yz 面试
date: 2018-06-20 21:00:36
tags: yz interview
categories: interview
---
面试相关,Tel面试

    问题第二天回想起来有：
    1. CSS选择器的优先级，如何优化CSS
    2. 垂直居中的方法
    3. HTTP三次握手
    4. git的工作流 TODO
    5. Vue组件 TODO
    6. cookie
    7. 为什么要重置样式。TODO
    关于CSS选择器的优先级答的还不错，优化CSS的方法，我谈到了ID选择器前没有必要
    加上标签选择器，然后就是使用webpack对CSS进行优化压缩

    垂直居中的方法，我提到的有：固定宽度+margin,浮动，定位，就是没有谈到flex
    弹性布局，这个要补一下，虽然在贝贝实习的时候有用到，但是回答的时候竟想不起来
    有哪些属性了！

    HTTP三次握手，回答的不是很好。

    Git工作流，就是最后一部分的pull request 和merge request的区别讲的不是很
    清楚

    Vue组件的话，确实还没有实实在在的考虑一个组件的设计，只是回答了一些概念性的
    东西。

    总结下来：要看一下HTTP三次握手，Flex布局，Git工作流，垂直居中布局。

#### TCP（Transmission Control Protocol）协议中的三次握手

    建立TCP需要三次握手，断开连接需要四次握手
    建立TCP连接的三次握手：
    第一次握手：客户端发送syn包(syn=j)到服务器，并进入SYN_SEND状态，
                等待服务器的确认。
    
    第二次握手：服务器接受到syn包，确认客服端传递过来的syn包(ack=j+1),同时
                也发送一个SYN包(syn=k),即SYN+ACK包，此时服务器处于SYN_RECV状态。

    第三次握手： 客户端接受到服务器传递过来的SYN+ACK包，向服务器发送确认包ACK           (ack=k+1),此包发送完毕，客户端和服务器进入了established状               态。
    为何要三次握手？
        为了保证服务器端能接受客户端的信息并能做出正确的应答而做的前两次
        握手（第一次和第二次），为了保证客户端能接受服务器端的信息并能做出正确的应该而做的后两次握手（第二次和第三次）。

        客户端发送连接请求给服务器，这是第一次握手。服务器确认客户端的请求后予以响应，表示自己能理解客户端的请求，并作出回应，这是第二次握手。客户端收到服务器端的响应，予以回应，表示自己能理解服务器端返回的信息，可以相互发送信息了，这是第三次握手。

<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1527736809728.png" width="681"/>


#### HTTP连接

    HTTP（Hypertext Transfer Protocol），超文本传输协议。建立在TCP协议之上的一种应用。
    特点是:客户端发送的每次请求都需要服务器端予以响应，请求结束后，就主动释放连接。
    1）HTTP1.0协议，客户端每次请求都要建立一次单独的连接，处理本次请求后，自动释放本次连接。
    2）HTTP1.1协议，客户端的一次连接中可以发送多次请求，并且多个请求可以重叠进行，不需要等待一个请求结束后再发送下一个请求。

    因为HTTP连接是一个短连接，每次请求结束后都会主动释放连接。所以要保证客户端的在线状态，通常的做法是:客户端每隔一段时间向服务器发送一次请求，服务器接受到请求后进行回复，表明知道客户端在线。服务器端若长时间没有接受到客户端的请求，则认为客户端已经下线。客户端若长时间没有接收到服务器的响应，则认为网络已经断开。

#### 套接字（socket)

    包含网络通信5中必须信息：连接时使用的协议，本地的IP地址，本地进程的协议端口，远程主机的IP地址，远程进程的协议端口。
    TODO：2018-5-31:11:11
    参考链接：https://github.com/jawil/blog/issues/14

#### Flex（Flexible）Box弹性布局

<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1527737094073.png" width="579"/>


    1. 任何元素都可以指定为Flex布局，包括块级元素和行内元素，
        当元素设置为flex布局后，子元素的float，clear和
        vertical-align属性将失效。
    2. 元素采用flex布局后，称为flex容器，其子元素自动成为容器
        的成员，成为flex项目（flex item）
    3. 容器的属性
        flex-direction:决定主轴的方向（即项目的排列方向）
            row(default)|row-reverse|column|column-reverse

        flex-wrap:默认情况下，项目都排在一条线（又称"轴线"）上。                flex-wrap属性定义，如果一条轴线排不下，如何换行
            nowrap(default)|wrap|wrap-reverse
<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1527737356547.png" width="769"/>

        flex-flow: 是flex-direction和flex-wrap的简写形式，默认为
                    row nowrap
                    <flex-direction> || <flex-wrap>

        justify-content: justify(两端对齐，公平)，定义了项目在主轴上
                         的对齐方式
                         flex-start | flex-end | center | space-between | 
                         space around
                        
                        space-between: 两端对齐，项目之间的间隔都相等。

                        space-around: 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1527737575886.png" width="683"/>

        align-items: 定义在交叉轴如何对齐
                    flext-start | flex-end | center |
                    baseline | stretch(拉伸，默认，如果
                    项目未设置高度或设为auto，将占满这个容器的高度)
<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1527737935042.png" width="643"/>

        align-content：定义多根轴线的对齐方式。如果项目只有一根轴线，
                        该属性不起作用。
                    flex-start | flex-end | center |
                    space-between | space-around | 
                    stretch(default)
<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1527738117668.png" width="633"/>

    4. order属性

        定义项目的排列顺序。数值越小，排列的越靠前，默认为0

    5. flex-grow（扩大选区）

        定义项目的放大比例，默认为0
        如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
    
    6. flex-shrink

        定义项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

    7. flex-basis
<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1527738806090.png" width="642"/>

    8. flex
        
        是flex-grow,flex-shrink,flex-basis的简写，默认值为
        0，1，auto
        该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。
        建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

    9. align-self

        允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items
        属性。默认值为auto，表示继承父元素的align-items属性。如果
        没有父元素，则等同于strentch。
<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1527739079942.png" width="772"/>
