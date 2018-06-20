---
title: new 关键字实现原理
date: 2018-06-20 20:55:57
tags: javascript
categories: javascript
---
new 关字做了些什么？
从直观上来看，使用new会返回一个对象，该对象的原型对象也是存在的，和构造函数的原型一致。具体new都做了些什么？
	1. 创建了一个空对象，因为最后是要返回对象的
	2. 设置该对象的原型，这里原型使用的是构造函数的原型，不能使用对象的__proto__属性
	3. 使用apply指定this为第一步创建的对象，参数数组是arguments对象的包含第二个参数后的参数。
	4. 返回该对象
	const  new2 = function () {
		const obj = {}
		Object.setPrototypeOf(obj,constructor.prototype)
		let argArr = Array.prototype.slice.apply(arguments)
		constructor.apply(obj,argArr.slice(1))
		return obj;
	}

	note: 如果构造函数返回的是一个对象，那么通过new得到会是构造函数返回的对象，this指向的也是这个返回的对象，这可以和我们预期的有些不符。
	function Person (saying) {
	    this.saying = saying
	    // 返回的是一个对象
	    return {
	        name: 'jingke123'
	    }
	}
	
	Person.prototype.talk = function () {
	    console.log(this.saying)
	}
	// 如果构造函数有返回对象，直接返回该对象
	// 否则返回构造函数的实例
	var p = new Person('hahahha')
	console.log(p)
	
	
	const new1 = function(constructor) {
	    const obj = {}
	    Object.setPrototypeOf(obj,constructor.prototype)
	    let argArr = Array.from(arguments)
	    argArr
	   // 需要考虑到构造函数返回一个对象的情况
	    return constructor.apply(obj,argArr.slice(1)) || obj;
	}
	
	var p2 = new1(Person,'lijing')
	// p2.talk()
	console.log(p2)