#### Chrome 调试

1.  debugger

    ```
    console.log('1');
    debuger;
    console.log('2');

    // 通过命令🙆管理代码
    function debug(arg) {
    	let allDebugger = false;
    	if(arg || allDebugger) {
    		debugger;
    	}
    }
    console.log('1')
    debug(1)
    console.log('2');
    debug(0);
    console.log('3')
    ```

2.  console.table

    ```
    var obj = {
    name: 'jingke',
    age: 26,
    family: {
    	father: 'qing',
    	mother: 'nv'
    	}
    }
    console.table(obj)
    ```

3.  显示堆栈调用

    **使用场景**  
    (1) 在你 发现有一个函数 fn1 被执行，但不能确定是谁调用了 fn1  
    (2) fn1 你预期只执行了一次，但实际上却发现执行了多次

    ```
    function fn1 () {
    	console.trace('fn1')
    }

    function fn2 () {
    	fn1()
    }

    function fn3 () {
    	fn2()
    }

    function fn4 () {
    	fn1()
    }
    fn3(
    fn4()
    ```

4.  console 颜色输出

    ```
    console.log('%c%s', 'color: red', 'zhenglijing')
    %c: css格式字符串
    %s: 字符串
    %d: 数字
    %f: 浮点数
    %i: 整数
    ```

5.  当函数被调用时，提示和显示参数

    ```
    function foo(a, b, c) {
    	console.log(arguments)
    }

    monitor(foo);
    foo(1, 2)
    ```

6.  DOM 被移除，修改，属性被修改时自动断点
7.  console.debug

    > 默认情况下，console.debug 输出的信息不会显示，只有在打开显示级别在 verbose 的情况下，才会显示

8.  覆盖 console 对象的方法

    ```
    	['log', 'info', 'warn', 'error'].forEach(function(method) {
    		console[method] = console[method].bind(
    		console,
    		new Date().toISOString()
    		);
    	});

    console.log("出错了！");
    // 2014-05-18T09:00.000Z 出错了！
    ```

9.  console.count()

    > count 方法用于计数，输出它被调用了多少次

        ```
        function greet(user) {
        console.count();
        return 'hi ' + user;
        }

        greet('bob')
        //  : 1
        // "hi bob"

        greet('alice')
        //  : 2
        // "hi alice"

        greet('bob')
        //  : 3
        // "hi bob"
        ```

    > 该方法可以接受一个字符串作为参数，作为标签，对执行次数进行分类

        ```
        function greet(user) {
        console.count(user);
        return "hi " + user;
        }

        greet('bob')
        // bob: 1
        // "hi bob"

        greet('alice')
        // alice: 1
        // "hi alice"

        greet('bob')
        // bob: 2
        // "hi bob"
        ```

10. console.dir()

> dir 方法用来对一个对象进行检查（inspect），并以易于阅读和打印的格式显示。

    ```
    console.log(document.body)
    ```

> Node 环境之中，还可以指定以代码高亮的形式输出。

    ```
    const obj = {
        name: 'zheng',
        age: 25
    }
    console.log(obj, {colors: true})
    ```

11. console.dirxml

> dirxml 方法主要用于以目录树的形式，显示 DOM 节点

    ```
    console.dirxml(document.body);
    ```

12. console.assert()

    > console.assert 方法主要用于程序运行过程中，进行条件判断，如果不满足条件，就显示一个错误，但不会中断程序执行。这样就相当于提示用户，内部状态不正确。它接受两个参数，第一个参数是表达式，第二个参数是字符串。只有当第一个参数为 false，才会提示有错误，在控制台输出第二个参数，否则不会有任何结果。

        ```
            console.assert(false, '判断条件不成立')
        // Assertion failed: 判断条件不成立

        // 相当于
        try {
            if (false) {
                throw new Error('判断条件不成立');
            }
        } catch(e) {
            console.error(e);
        }
        ```

13. console.time(), console.timeEnd()

>这两个方法用于计时，可以算出一个操作所花费的准确时间。

    ```
    console.time('Array initialize');

    var array= new Array(1000000);
    for (var i = array.length - 1; i >= 0; i--) {
    array[i] = new Object();
    };

    console.timeEnd('Array initialize');
    ```

>time方法表示计时开始，timeEnd方法表示计时结束。它们的参数是计时器的名称。调用timeEnd方法之后，控制台会显示“计时器名称: 所耗费的时间”

14. console.group(),console.groupEnd()

>console.group和console.groupEnd这两个方法用于将显示的信息分组。它只在输出大量信息时有用，分在一组的信息，可以用鼠标折叠/展开。

    ```
    console.group('一级分组');
    console.log('一级分组的内容');

    console.group('二级分组');
    console.log('二级分组的内容');

    console.groupEnd(); // 一级分组结束
    console.groupEnd(); // 二级分组结束
    ```



15. console.groupCollapsed()

>console.groupCollapsed方法与console.group方法很类似，唯一的区别是该组的内容，在第一次显示时是收起的（collapsed），而不是展开的。

    ```
    console.groupCollapsed('Fetching Data');

    console.log('Request Sent');
    console.error('Error: Server not responding (500)');

    console.groupEnd();
    ```

16. 命令行API

    (1). $_

    >$_属性返回上一个表达式的值。

    (2). $(selector)

    >$(selector)返回第一个匹配的元素，等同于document.querySelector()。
    注意，如果页面脚本对$有定义，则会覆盖原始的定义。比如，页面里面有 jQuery，
    控制台执行$(selector)就会采用 jQuery 的实现，返回一个数组。

    (3). $$(selector)

    >$$(selector)返回选中的 DOM 对象，等同于document.querySelectorAll

    (4). $x(path)

    >$x(path)方法返回一个数组，包含匹配特定 XPath 表达式的所有 DOM 元素。

    ```
    $x("//p[a]")
    ```

    (5). getEventListeners(object)
    
    >getEventListeners(object)方法返回一个对象，
    该对象的成员为object登记了回调函数的各种事件（
    比如click或keydown），每个事件对应一个数组，
    数组的成员为该事件的回调函数。
    getEventListeners($0)

    (6). monitorEvents(object[, events]), monitorEvents(window, "resize");

    >monitorEvents(object[, events])方法监听特定对象上发生的特定事件。
    事件发生时，会返回一个Event对象，包含该事件的相关信息。
    unmonitorEvents方法用于停止监听。

    ```
    monitorEvents(window, "resize");
    monitorEvents(window, ["resize", "scroll"])
    ```

    >monitorEvents允许监听同一大类的事件。所有事件可以分成四个大类

    ```
    mouse：”mousedown”, “mouseup”, “click”, “dblclick”, “mousemove”, “mouseover”, “mouseout”, “mousewheel”
    key：”keydown”, “keyup”, “keypress”, “textInput”
    touch：”touchstart”, “touchmove”, “touchend”, “touchcancel”
    control：”resize”, “scroll”, “zoom”, “focus”, “blur”, “select”, “change”, “submit”, “reset”
    ```

    (7). copy(object)
    
    >复制特定 DOM 元素到剪贴板。

    ```
    copy($0)
    <a href="https://github.com/ruanyf/jstutorial" target="_blank">GitHub <i class="foundicon-edit"></i></a>
    ```

#### console.time,console.timeEnd

    // method1
    var startTime = new Date().getTime();
    var arr = new Array(1000000)
        arr.forEach((item,index,array) {
            array[index] = new Object()
    })
    console.log('spend time:' + new Date().getTime() - startTime);