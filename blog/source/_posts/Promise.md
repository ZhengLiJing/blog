---
title: Promise
date: 2018-06-20 20:45:27
tags: ES6
categories: javascript
---
Promise的笔记
#### Promise新建后会立即执行

#### 如果resolve和reject函数带有参数，则参数会被传递给回调函数。
    reject的参数一般是一个Error对象，而resolve函数的参数除了正常的值外，还可以是另一个Promise实例。
    // 如果p1是个Promise对象，则直接返回该对象
    resolve(p1);
    eg.
    const p1 = new Promise((res, rej) => {
        setTimeout(() => rej(new Error('fiail')), 3000)
    })

    const p2 = new Promise((res, rej) => {
        setTimeout(() => res(p1), 1000)
    })

    p2.
        .then(res => console.log(res))
        .catch(errconsole.log(err))
    // 上面的代码，p2创建了一个Promise对象，立即得到执行，然后过了1秒后返回了p1对象，
    // 该对象也是Promise对象，所以p2自己的状态无效了，由p1决定p2的状态。
