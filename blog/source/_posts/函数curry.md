---
title: 函数curry
date: 2018-06-20 20:48:37
tags: curry
categories: javascript
---
函数柯里化
# 函数柯里化

	function curryIt(fn) {
		// 函数fn的参数的长度
		var n = fn.length;
		n    3
		var args = []; 
		// 直接返回该函数
		return function(arg) {
			arg 
			args.push(arg);
			args
			if(args.length < n) {
			return arguments.callee
			}else {
				return fn.apply(null,args)
			}
		}
	}
	function add(a,b,c) {
		return [a,b,c]
	}
	// 第一步，看函数内部参数的演变
	var c = curryIt(add)
	var c1 = c(1)

	function curryIt {
		// 函数fn的参数的长度`
		var n = fn.length;
		n    3
		var args = [];
		return function(arg) {   ****
			arg  1,2
			args.push(arg); 
			args  [1], [1,2]
			// 2 < 3，即此时只传入了二个参数，返回****这个函数
			if(args.length < n) {
			return arguments.callee
			}else {
				return fn.apply(null,args)
			}
		}
	}
	function add(a,b,c) {
		return [a,b,c]
	}
	var c = curryIt(add)
	var c1 = c(1)
	var c2 = c(2)

	function curryIt {
		// 函数fn的参数的长度
		var n = fn.length;
		n    3
		var args = [];
		return function(arg) {   ****
			arg  1,2,3
			args.push(arg); 
			args  [1], [1,2],[1,2,3]
			// 3 < 3，即此时传入了三个参数，直接执行
			// fn.apply(null,args),相当于执行fn(a,b,c)
			if(args.length < n) {
			return arguments.callee
			}else {
				return fn.apply(null,args)
			}
		}
	}
	function add(a,b,c) {
		return [a,b,c]
	}
	var c = curryIt(add)
	var c1 = c(1)
	var c2 = c(2)
	var c3 = c(3)
	console.log(c3); // [1,2,3]


<iframe width="560" height="315" src="https://www.youtube.com/embed/RrkC2lTl2TY" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>