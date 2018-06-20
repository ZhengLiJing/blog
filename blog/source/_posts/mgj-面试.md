---
title: mgj 面试
date: 2018-06-20 21:02:11
tags: mgj interview
categories: interview
---
面试相关,Tel面试
    1. 如何获取URL
    2. 在贝贝工作时，做小程序都做了些什么东西TODO
    3. 原价如何使用删除线实现。标签和CSS如何实现，两者的比较
    4. 首行缩进，indent
    5. ++i,i++
    6. 'a'+3,'a'+3+3,'5'+3,'5'-3
    7. 数组去重 TODO
    8. 跨域，jsonp和CORS的优缺点
    9. 布局，中间自适应居中
    10. 段落溢出...
    9. 最后都会有这么个环节，你还有什么问题要问我吗？TODO

#### JS获取页面URL信息

    1. window.location.href(获取URL或设置URL)

    2. window.location.protocol(获取URL的协议部分或设置)
        console.log(window.location.href);// https:

    3. window.location.host(获取URL主机部分或设置)
        console.log(window.location.host);// www.jianshu.com
    
    4. window.location.port(获取URL的端口或设置)
        //返回：空字符(如果采用默认的80端口 (update:即使添加了:80)，
        那么返回值并不是默认的80而是空字符)

    5. window.location.pathname(获取URL的路径部分-文件地址或设置)
        console.log(window.location.pathname)
        //"/p/073f79c5e438"
    
    6. window.location.search(获取href属性中跟在问好后面的部分或设置)

    7. window.location.hash(获取 href 属性中在井号“#”后面的分段 或 设置)

    8. js获取URL中的参数值
        
        1. 正则法
        function getQueryString(name) {
            var reg = new RegExp('(^|&)' + name + '=([^&]*)(&|$)', 'i')
            var r = window.location.search.substr(1).match(reg)
            if(r !== null) {
                return unescape(r[2])
            }
            return null
        }
        // 这样调用：
        alert(GetQueryString("参数名1"));

        2. split拆分法

        function getRequest() {
            let url = window.location.search;
            var theRequest = new Object();

            if(url.indexOf('?') !== -1) {
                var params = url.substr(1);
                var paramsArr = params.split('&');
                paramsArr.forEach((item) => {
                    theRequest[item.split('=')[0]] = 
                            unescape(item.split('=')[1])
                })
            }
            return theRequest;
        }
        // test
        var window = {};
        window.loaction = {};
        window.location.search = '?name=jingke&age=26'
        var request = {};
        request = getRequest()

#### 删除线

    1. 使用标签实现
        <strike>200</strike>
        <del>200</del>
        <s>200</s>

       使用CSS实现
            selector {
                text-decoration: line-through;
            }
        无论是选择CSS样式布局中划线，还是HTML标签布局中划线也好，
        重要的是根据需求合理选择适合布局方式。

#### 布局

<img src="http://p8rhahhu3.bkt.clouddn.com/201801/1527770209843.png" width="718"/>

    三栏布局，左边的商品导航栏和右边的导航栏固定宽度，中间的主要内容随浏览器宽度自适应。

    1. 流体布局，左右固定宽度，左边导航左浮动，右边导航右浮动，中间模块设置margin-left
        ，值为左导航的宽度；margin-right值为右导航的宽度。
        缺点是主要内容无法最先加载，当页面内容较多时会影响用户的体验。
        codepen: https://codepen.io/zhenglijing/pen/XYbdrZ?editors=1111 
    
    2. BFC三栏布局
        BEC区域，不会与浮动元素重叠。利用该特点实现3列布局
        https://codepen.io/zhenglijing/pen/ZRGWJx
        缺点：和流体布局一样，主内容无法最先加载。为了解决这个问题，
            提出双飞翼布局

    3. 双飞翼布局

        利用的是浮动元素margin负值的应用。主体内容可以优先加载，HTML代码
        结构稍微复杂点。

    4. flex布局

        简单实用，未来的趋势，需要考虑浏览器的兼容性

    5. 绝对定位布局

        父元素相对定位，左右两列分别绝对定位，中间设置左右margin值。
        https://codepen.io/zhenglijing/pen/pKJEgv

    总结： 比较好的方法是flex布局，简单实用，代表未来的趋势。
          绝对定位布局容易理解和想的到，左右两列固定宽度，绝对定位。
          中间模块设置左右margin值即可。 

          margin负值实现三栏布局
          <div>
            <div id='main'>
                <div id='body'>body</div>
            </div>
            <div id='left'>left</div>
            <div id='right'>right</div>
          </div>
          // css
          #main {
              width: 100%;
              height: 100%;
              float: left;
          }

#### CSS text-indent属性

    段落第一行缩进：p {text-indent: 50px;}
    text-indent的取值可以是：
    1. 2em,em是相对长度单位，为父元素文本字体尺寸的倍数
    2. 2%,相对父元素的百分比
    3. 2in 英尺
    4. 2cm厘米
    5. 2px
    6. 2pt 磅

    关于em这个相对单位：浏览器的默认字体大小是16px。所有未经调整的
    浏览器都符合，16px = 1em。那么16px : 1em = 10px : x,得到
    x = 0.625em。如果我们想让em单位和px单位直观的对应起来，而不是
    每次都要计算一下。我们body元素的字体大小设置为62.5%,如此一来，
    16px * 62.5% = 10px,也就是10px = 1em。显得直观。

    所以我们在写CSS的时候，需要注意两点：

    1. body选择器中声明Font-size=62.5%；

    2. 将你的原来的px数值除以10，然后换上em作为单位；

    3. 重新计算那些被放大的字体的em数值。避免字体大小的重复声明。
       也就是避免1.2 * 1.2= 1.44的现象。比如说你在#content中声明了字体大小为1.2em，那么在声明p的字体大小时就只能是1em，而不是1.2em, 因为此em非彼em，它因继承#content的字体高而变为了1em=12px。

    获取字体大小：
    var test = document.getElementById('test')
    var ftVal = getComputedStyle(test,undefined);
    console.log(ftVal.fontSize)

#### css rem单位

    rem(root em)，和em类似，也是相对单位，和em所不同的是，其
    相对的是根元素。这个单位可谓集相对大小和绝对大小的优点于一身，通过它既可以做到只修改根元素就成比例地调整所有字体大小，又可以避免字体大小逐层复合的连锁反应。目前，除了IE8及更早版本外，所有浏览器均已支持rem。对于不支持它的浏览器，应对方法也很简单，就是多写一个绝对单位的声明。这些浏览器会忽略用rem设定的字体大小。例如：
    p {font-size:14px; font-size:0.875rem;}

#### jsonp和cors的优缺点

    jsonp和cors使用的目的是相同的，并且都需要服务端和客户端的配合。
    虽然CORS功能更加强大，但是需要根据应用场景进行选择哪一个更适合。

    jsonp(json with padding),利用页面引入静态资源时不受同源
    策略的限制达到跨域的目的。
    CORS，依附于AJAX，通过HTTP Header部分字段请求和获取有权限访问
    的资源。

    JSONP优点：
    1.对浏览器的兼容性好，虽然跨资源共享方案目前主流浏览器都支持，
      但是IE10以下不支持跨资源共享。
    
    JSONP缺点：
    1. JSONP只能用来获取资源，类似于GET方法。跨资源共享支持所有
       类型的HTTP方法，功能完善。
    2. JSONP的错误处理机制不完善，没有办法进行错误处理。跨资源共享
       可以通过onerror事件监听错误，并且浏览器控制台会看到报错信息，
       利于定位错误。
    3. JSONP只会发送一次请求。而对于复杂请求，跨资源共享会发送两次
       请求。

    安全问题：

    始终觉得安全性这个东西是相对的，没有绝对的安全，也做不到绝对的安全。毕竟JSONP并不是跨域规范，它存在很明显的安全问题：callback参数注入和资源访问授权设置。CORS好歹也算是个跨域规范，在资源访问授权方面进行了限制（Access-Control-Allow-Origin），而且标准浏览器都做了安全限制，比如拒绝手动设置origin字段，相对来说是安全了一点。但是回过头来看一下，就算是不安全的JSONP，我们依然可以在服务端端进行一些权限的限制，服务端和客户端也都依然可以做一些注入的安全处理，哪怕被攻克，它也只能读一些东西。就算是比较安全的CORS，同样可以在服务端设置出现漏洞或者不在浏览器的跨域限制环境下进行攻击，而且它不仅可以读，还可以写。

    使用场景：

        要兼容IE低版本浏览器，使用JSONP
        如果要对服务器端资源进行操作，使用CORS

#### 文字内容溢出用点点点(...)省略号表示

    p {
        width: 500px;
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
    }

    对于现代浏览器，例如webkit内核的浏览器，或者移动端，
    是可以实现多行文本内容超出点点点…最后一行显示的，
    典型的CSS组合如下：
    .box {
        display: -webkit-box;
        -webkit-line-clamp: 3;
        -webkit-box-orient: vertical;
    }

#### 电话或现场面试最后的提问环节

    1. 赢得这个岗位需要几轮面试？接下来的流程是什么？
    2. 为了更好的胜任这个岗位，我还需要补充哪些技能？
    3. 入职后是否有产品培训和技能培训？
    4. 这个职位在公司的发展前景是怎么样的？有什么晋升的机会？
        在什么条件下，可以获得晋升机会？
        
    5. 团队成员是多少人？大家怎么分工的？目前团队的核心工作是哪些？
    6. 如果我来到公司后，每天的日常工作是什么？
    7. 公司对我这个职位的期望是什么？
    8. 如何评估员工在试用期的表现？考核标准是什么？

#### 邮件发送简历

    岗位+姓名+学校+专业+毕业时间+可入职时间+每周可实习时间+以往闪光的经验+或者招聘信息的渠道

    A、可以以附件形式发送，但要将文件名称保存为求职者的姓名；

    B、也可以保存成JPG形式，直接粘贴在邮件正文里，增加被HR关注的几率，也便于HR下载保存。

    C、如果是设计同学求职，需要给HR展示作品的，可以将简历和作品分开，简历放在附件中发送，作品以网站链接形式在邮件正文中发送最好，不建议超大附件。

    给自己加分的求职信主要有这几方面：

    A、简单说明跟求职岗位相关的经历经验，说明自己和岗位的匹配度。

    B、表达自己对应聘岗位和应聘公司的兴趣，增加好感。这里不要千篇一律把同一封求职信复制粘贴到处发，好的求职信一定是为某一公司某一岗位定制化撰写的，有针对性的。

    C、求职信要简短，保证300字以内可以说清楚全部内容，长篇大论无法突出重点也没人爱看。

    D、在求职信尾部再次留下自己联系方式，便于HR联系你。

    1. 杭州电子科技大学|研二|web前端开发实习岗位|18367183771
        有2个月的电商公司实习/工作经验，擅长...,希望加入...团队，
        谋求前端实习岗位！

    2. web前端开发实习岗位-郑利京-杭州电子科技大学-研二-5天-6个月
        您好：
            我是杭州电子科技大学研二学生，对前端有浓厚兴趣，并且有
            在一家电商公司有过前端开发实习经历，主要工作是混合APP开发。我经常关注互联网，软件的最新发展和业余知识，希望能
            够有机会到贵公司实习。
        祝您
            万事如意

    3. web前端开发实习岗位-郑利京-杭州电子科技大学-研二-5天-6个月

        尊敬的先生/女士：

        您好，我是杭州电子科技大学2019届学生郑利京，联系方式为：
        183-6718-3771

        我目前是研究生二年级，暑假期间处于空闲期，没有课业的负担，
        可以全心投入到工作中（可以每周五天全职）。

        在此之前我也有过在杭州贝购科技有限公司作为前端开发实习生，对
        前端开发的流程有一定的了解，能更快的融入到团队中。

        附件是我的个人简历，在此我诚挚的申请贵公司的前端实习岗位（可即使上岗）。

        谢谢您的阅读，期待您的恢复，祝您生活愉快!
