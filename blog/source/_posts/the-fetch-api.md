---
title: the fetch api
date: 2018-06-20 20:51:00
tags: fetch api
categories: javascript
---
The Fetch Api
## fetch()

 fetch()方法是window下的一个方法，使用该方法执行请求。该方法返回一个Promise。

fetch()接受一个参数URL，例子如：
	fetch('https://www.reddit.com/r/javascript/top/.json?limit=5')
	.then(res => console.log(res));

如果在谷歌控制台执行，结果请求是成功的，但是却没有我们要的top5 posts
fetch()方法返回一个Promise（一个代表未来结果的对象），然后接着我们使用了then()方法来等待服务器返回响应，并将其打印出来。

其实，返回的响应res对象暴露出一个json()方法，该方法返回json格式的响应的主体数据。即：
let url = 'https://www.reddit.com/r/javascript/top/.json?limit=5'
window.fetch(url)
		.then(res => res.json())
		.then(json => console.log(json));
json()方法返回的也是一个Promise，所以我们可以再次使用then()方法，得到数据。

## Async … await

	ES2017规范是2018年提出的，引入了新的语法，即async ... await,意味着我们可以将函数标记为async异步的。然后使用await关键字等待承诺的结果。例子如：
	async function fetchTopFive(sub) {
		const url = `https://www.reddit.com/r/${sub}/top/.json?limit=5`
		// 使用fetch()方法得到Promise，
		const fetchResult = fetch(url)
		// await Promise 得到结果
		const res = await fetchResult;
		// await Promise得到json格式的数据
		const jsonData = await res;
		console.log(jsonData)
	}
	fetchTopFive('javascript')

## Handling Erros

	如果我们向服务器请求一个不存在的资源或需要授权的资源，我们必须处理如404之类的响应，上面我们讲到fetch()方法返回一个Response对象，该对象具有一个OK属性，如果这个属性值为true，说明响应是成功了。那我们得考虑到返回的不是成功的响应的情况，如：
	asycn function fetchTopFive(sub) {
		const URL = http://httpstat.us/404; // Will return a 404
		const fetchResult = fetch(url);
		const res = await fetchResult;
		if(res.ok) {
			const jsonData = await res.json();
		}else {
			throw Error(res.statusText);
		}
	}
	fetchTopFive('javascript')
	但是，对于不同远程服务器的响应而言，请求的资源即使不存在，响应也有可能是返回200，这种情况下，我们就可以使用try...catch进行捕获错误。如：
	async function fetchTopFive(sub) {
	'' 	const URL = https://www.reddit.com/r/${sub}/top/.json?limit=5;
			try {
				const fetchResult = fetch(URL);
				const res = await fetchResult;
				const jsonData = await res。json();
				console.log(jsonData)
			}cache(e) {
				throw Error(e)
			}
		}
	fetchTopFive('javavvvvvv');

## 更改请求方法和请求头

	fetch()远不及这么一个用途，我们可以向fetch()方法中传递一个Request构造函数，该构造函数的首参是URL，第二个参数是配置请求的选项对象，如：
	async function fetchTopFive(sub) {
		const URL = https://www.reddit.com/r/${sub}/top/.json?limit=5;
		try {
			const fetchResult = fetch(
				new Request(URL, { method: 'GET', cache: 'reload'}
			)
			const res = await fetchResult;
			const jsonData = await res;
			console.log(jsonData)
		}cache(e) {
			throw Error(e)
		}
	}
	除此之外，我们还可以更改请求头，比如下面是更改请求头中的Accept头信息
	const headers = new Headers();
	headers.append('Accept', 'application/json');
	const request = new Request(URL, {
		method: 'GET', cache: 'reload', headers; headers
	})

	该例子值得学习的一些地方
	1. const result = document.querySelector('#result');注意有#
	这个也可以只用getElementById('result')替代，
	2. 只有拿到数据才可以操纵DOM，拿到数据后，将数据传递给一个函数进行处理。
	3. 数据参数的命名：posts,datas,params,options,customers
	4. <ol></ol>有序列表
	5. fetchTopFive(subInput.value);// 直接将输入框内的内容传递给函数 
	
	const button = document.querySelector('button');
	const subInput = document.querySelector('input');
	const result = document.querySelector('#result');
	
	async function fetchTopFive(sub) {
	    const URL = `https://www.reddit.com/r/${sub}/top/.json?limit=5`;
	    try {
	        const fetchResult = fetch(new Request(URL, {
	            method: 'GET', cache: 'reload'
	        }))
	        const response = await fetchResult;
	        if(response.ok) {
	            jsonData = await response.json();
	            result.innerHTML = renderList(jsonData);
	        }else {
	            result.innerHTML = `Response.status: ${response.status}`;
	        }
	    } catch (error) {
	        result.innerHTML = error;
	    }
	}
	
	function renderList(json) {
	    const posts = json.data.children;
	    return `<ol>
	        ${posts.map(post) => {
	            `<li>${post.data.title} <a href="${post.data.url}">link</a></li>`
	        }}
	    </ol>`
	}
	
	button.addEventListener('click', () => {
	    fetchTopFive(subInput.value)
	})

	自己的实现方式的缺点
	1. 使用ul（有序列表），配合css的list-style-type: decimal才实现有序列表
	2. 响应没有判断是否ok
	3. 没有使用ES6的模板语法（``)
	4. 没有直接将输入框的值传递给fetchTopFive()函数，而是引入了一个变量。增加了命名冲突的可能。
	如何使用webpack搭建开发fetchAPI的开发环境？
	async function fetchTopFive(sub) {
		 const URL = `https://www.reddit.com/r/${sub}/top/.json?limit=5`;
	  try {
		    const fetchRes = fetch(URL);
		    const res = await fetchRes;
		    const jsonData = await res.json();
		    renderList(jsonData)
	  }catch(e) {
		    throw new Error(e.statusText)
	  }finally {
	    
	  }
	}
		  const button = document.querySelector('button');
			  button.onclick = function () {
		  const subInput = document.querySelector('input');
		  const inputValue = subInput.value;
		  fetchTopFive(inputValue)
	}
	
	function renderList(arr) {
		  const result = document.querySelector('#result');
		  const datas = arr.data.children;
		  let ulEle = document.createElement('ul');
		  let html = '';
		  datas.map((data) => {
			    html += `<li>${data.data.title} <a href="${data.data.url}">link</a></li>`
		  });
		  result.innerHTML = html;
		  document.body.appendChild(result)
	}






