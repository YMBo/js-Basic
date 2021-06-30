# js-基础知识总结   
这里是对一些基本js知识点和小技巧进行总结，持续更新，如有遗漏和缺陷欢迎补充！    
***
## 一、基本知识        
### 1.盒子模型   
> 标准盒子模型 width=content；IE盒子模型width=padding+content+border   
----------    
### 2.元素类型 
* 行内元素：a、b、span、img、input、strong、em、button    
* 块级元素：div、ul、li、dl、dt、dd、p、h1-h6     
----------      
### 3.引入和引用      
> href 表示超文本引用（hypertext reference），在 link和a 等元素上使用。src 表示来源地址，在 img、script、iframe 等元素上。
src 的内容，是页面必不可少的一部分，是引入。href 的内容，是与该页面有关联，是引用。区别就是，引入和引用。`src用于替换当前元素，href用于在当前文档和引用资源之间确认联系`       
*********       
### 4.js中==转换规则     
* number类型与string类型比较，string会转换为number类型     
* null和undefined始终相等        
* 布尔类型与其他任何类型进行比较，布尔类型将会转换为number类型     
* number类型或string类型与object类型进行比较，number或者string类型都会转换为object类型      
*****       
### 5.运算过程的转换原则      
* 字符串与数字相加，变成字符串
* 字符串与数字相减，变成数字     
----------      
## 二、基础代码使用技巧  
   
### 1. 生成[x,y]范围的随机整数    
```javascript
function d(min,max){
	return (Math.round(Math.random()*(max-min))+min);
}
```	
### 2. 已知数组var stringArray = [“This”, “is”, “Baidu”, “Campus”]，Alert出”This is Baidu Campus”	
```javascript
function a(o){
	return o.join(' ')
}
```	
### 3. 已知有字符串foo=”get-element-by-id”,写一个function将其转化成驼峰表示法”getElementById”	
```javascript
function hump(str){
	var reg=/\-[a-z]/g;
	var str1=str.match(reg);
	str1.forEach(function(ele,index,array){
		str=str.replace(ele,ele.substr(-1,1).toUpperCase());
	})
	return str;
}
//正则
function hump(str){
	return str.replace(/\-[a-z]/g,function(ele){
		return ele.substr(-1,1).toUpperCase();
	})
}

// 上面两种方法有点墨迹    
function hump(str) {
  let newStr = '';
  for (let i = 0; i < str.length; i++) {
    if (str[i] == '_') {
      let next = str[i + 1];
      next && (newStr += next.toUpperCase());
      i += 1;
    } else {
      newStr += str[i];
    }
  }
  return newStr;
}

function hump(str) {
  return str.replace(/_(\w)/, (_, k) => {
    return k.toUpperCase();
  });
}
// match和exec区别
// 1.match是字符串的方法，exec是正则的方法
// 2.如果都是全局匹配且没有子表达式的话，match会返回所有的匹配结果（即使有字表达式也不会返回），而exec会返回第一个匹配的结果（如果有子表达式，会返回一次匹配） "abbb34eftab0modabbbbb6".match(/a(b)+(\d+)/g)
// 3.如果不是全局匹配，且有字表达式，match和exec返回结果一样，都是一个完整匹配和一个子表达式匹配
var a='asd888asdf';
var b=a.match(/\asd/g)		//b=['asd','asd'];
var c=/asd/g.exec(a) 		//c=['asd']
var d=/as(d)/g.exec(a) 		//d=["asd", "d"]
    
总结：    
1.match如果是全局匹配，则不支持子表达式，如果不是全局匹配则支持子表达式
2.exec不支持全局匹配，全局和非全局返回结果一样
3.match 字符串方法，exec正则的方法    

```	
### 4. var numberArray = [3,6,2,4,1,5]; 实现倒排，排序。	
```javascript
var numberArray = [3,6,2,4,1,5];
numberArray.sort(function(value1,value2){return value2-value1})
```	
### 5. 怎样添加、删除、替换、复制、创建和查找节点	
```javascript
//** 添加**
appendChild()
var para=document.createElement("p");
var node=document.createTextNode("这是新段落。");
para.appendChild(node);

//** 插入节点 **
insertedNode=parentNode.insertBefore(newnode,referenceNode)
- newNode：将要插入的节点
- referenceNode：被参照的节点（即要插在该节点之前,必须是parentNode的直接子节点）
- insertedNode：插入后的节点
- parentNode：父节点


//** 删除**
parentNode.removeChild(node)

//** 替换 **
parentNode.replaceChild(newnode,oldnode);

//** 复制 **
var node=document.getElementById("myList2").lastChild.cloneNode(true);
document.getElementById("myList1").appendChild(node);
//克隆所有后代，请把 deep 参数设置 true，否则设置为 false。

//** 创建 **
//创建元素节点
document.createElement('div')
//创建文本节点
document.createTextNode('文本节点')

//** 查找节点 **
document.getElementsByTagName("")    //通过标签名称
document.getElementsByName("")    //通过元素的Name属性的值
document.getElementById("")    //通过元素Id，唯一性
document.getElementsByClassName("");  //通过类查找，NodeList 对象，表示指定类名的元素集合
document.querySelector("")	//匹配指定 CSS 选择器的第一个元素
```
### 6. 常用dom操作api

* element.nextSibling 	//返回位于相同节点树层级的下一个节点。
* element.previousSibling	//返回位于相同节点树层级的前一个元素。
* element.nodeName 	//返回元素的名称。注意tagName只对元素节点有用，而nodeName没有限制
* element.nodeType 	//返回元素的节点类型。 1 2 3 
* element.lastChild 	//返回元素的最后一个子元素。
* element.firstChild	//返回元素的首个子元素。
* element.parentNode 	//返回元素的父节点。
* element.childNodes	//返回元素子节点的 NodeList。注意空格有的浏览器视为 文本节点返回
* element.classList 	//item() 、add(添加类名)、remove(删除类名) 、toggle(ele里如果有此类名就不添加，否则添加)、contains(是否含有指定类名)
*******************
位置信息    
**element.getBoundingClientRect()**
> ![getBoundingClientRect](/img/000.png)

**clientheight** :内容的可视区域，不包含border。clientheight=padding+height-横向滚动轴高度。 
> ![client](/img/111.png)

**clientTop**:一个元素顶部边框的宽度（以像素表示）。不包括顶部外边距或内边距(就是边框宽)    
*************
**offsetheight**：=padding+height+border+横向滚动轴高度    
> ![offsetheight](/img/222.png)    

**offsetLeft**: HTMLElement.offsetLeft 是一个只读属性，返回当前元素左上角相对于  HTMLElement.offsetParent(指的是position的元素，否则就向上查找) 节点的左边界偏移的像素值。    
offsetParent和parentNode的区别：    
offsetParent离当前元素最近的含有position的祖先元素    
parentNode 当前元素的父节点

*********************
**scrollheight**：可滚动高度    
> ![scrollheight](/img/333.png)    

**scrollTop**: 代表在有滚动条时，滚动条向下滚动的距离也就是元素顶部被遮住部分的高度。在没有滚动条时scrollTop==0恒成立。单位px，可读可设置    
> ![scrollTop](/img/444.png)

**********************
**event**    
* clientX		当事件被触发时鼠标指针向对于浏览器页面（或当前窗口）的水平坐标。
* clientY		同上
* screenX 	可返回事件发生时鼠标指针相对于屏幕的水平坐标。
* screenX	同上    

### 7. 判断一个正整数数是不是质数，注意优化~	   
```javascript
function isN(num){
	if(typeof num!=='number' || num<=0){return;}
		for(var i=2;i<=num/2;i++){
			if( num%i==0 ){       
				return false;
			};
		}
	return true;
}
//这个注意i<=num/2这块，这就是优化了，之前我是除到num-1，现在只需要除到一半，因为再往上除不可能除开，新技能get~
```	
### 8. 取得指定数字到0的所有质数，比如给了3，那么质数为1、3	
```javascript
function getZ( num ){
	var isZ=[];
	for(var i=1;i<=num;i++){
		if(isN( i )){
			isZ.push(i);
		};
	}
	return isZ;
}
function isN(num){
if(typeof num!=='number' || num<=0){return;}
	for(var i=2;i<=num/2;i++){
		if( num%i==0 ){       
			return false;
		};
	}
	return true;
}
```	
### 9. 单行写一个评级组件
```javascript
"★★★★★☆☆☆☆☆".slice(5 - rate, 10 - rate); 
//用法：rate是一个1-5的值，自定义
```	
### 10. 检查字符串不为空
```javascript
!!stringVar
```
### 11.惰性载入函数,不必每次重新进行判断，只需判断一次
```javascript
//第一种方式		
var setEvent = setClick();
setEvent(document.getElementById('box'));
function setClick() {
if (window.addEventListener) {
  return (setClick = function (ele) {
    ele.addEventListener(
      'click',
      function () {
	alert(this);
      },
      false
    );
  });
} else {
  return (setClick = function (ele) {
    ele.onclick = function (ele) {
      alert('方式2');
    };
  });
}
}	
		
		
//第二种方式,这种方式在开始加载的时候就会初始化相比上次少了一行代码				
var setClick=(function (){
			if( window.addEventListener ){
				return function(ele){
					ele.addEventListener('click',function(){
						alert(this)
					},false)
				}
			}else{
				return function(ele){
				ele.onclick=function(ele){
				alert('方式2')
			}
		}
	}
})();
setClick(document.getElementById('box'));
```

### 12. 原生实现bind函数    
``` javascript
Function.prototype._bind=function(context){
	if(typeof this !=='function'){return;}
	var fn=this;
	var params=Array.prototype.slice.call(arguments,1);
	return function(){
		fn.apply(context,params.concat(Array.prototype.slice.call(arguments)))
	}
}

注意点：
1. 保证函数this指向
2. 保证函数所有参数都传递到目标参数
3. 保证函数的返回值
```

### 13. new 一个类的时候，都发生了什么    
``` javascript
//代码模拟
/*
@param func被new的类（构造函数）
*/
function new2(func){
	//创建一个实例对象o，并将该对象原型（__proto__）指向func（构造函数）的原型对象
	var o = Object.create(func.prototype);
	//将o作为构造函数的this执行构造函数
	var k= func.call(o);
	// 如果构造函数返回值是引用类型则将实例对象o代替
	return typeof k==='object' ? k : o;	
}
```
### 14.Object.create兼容实现
``` javascript
Object._create=function(o){
	var Fn=function(){};
	Fn.prototype=o;
	return new Fn;
}
```

### 15.深拷贝
``` javascript
function deepCopy(obj){
	if(typeof obj!=='object'){return obj};
	var newObj=obj.constructor.name==='Array'	? [] : {};
	for(var key in obj){
		newObj[key]=typeof obj[key] == 'object' ? deepCopy(obj[key]) : obj[key];
	}
	return newObj;
}
```
### 16.手写ajax
``` javascript
//GET
var xhr=new XMLHttpRequest();
xhr.open('get',url,true);
xhr.onreadystatechange=function(){
	if(xhr.readyState==4){
		console.log(xhr.responseText)
	}
}
/*转码，否则会出现解析错误*/
function addParams(url,name,value){
	url+=url.indexOf('?') == -1 ? '?':'&';
	url+=encodeURIComponent(name)+'='+encodeURIComponent(value);
	return url;
}
xhr.send(null)

//POST
var xhr=new XMLHttpRequest();
xhr.open('post',url,true);
xhr.onreadystatechange=function(){
	if(xhr.readyState==4){
		console.log(xhr.responseText)
	}
}
xhr.send("name=YMBo&age=200");

```

### 17.字符串是否符合回文规则
``` javascript
let str = 'My age is 0, 0 si ega ym.';
//方法一
function palindrome(params){
	params=params.replace(/[\W\s_]/g,'');
	return params.toLowerCase()===params.split('').reverse().join('').toLowerCase();
}

//方法二
function palindrome(params){
	params=params.replace(/[\W\s_]/g,'').toLowerCase();
	for(var i=0,j=params.length-1;i<j;i++,j--){
		if(params[i]!==params[j]){return false}
	}
	return true;
}
//方法三
function palindrome(params){
	let length=params.length
	let halflength=(length-1)/2
	for(let i=0;i<halflength;i++){
		let a=params[i]
		if(params.indexOf(a)+params.lastIndexOf(a)!=length-1){return false}
	}
	return true
}
//递归
function palindrome(str) {
    // 排除干扰项
    str = str.toLowerCase().replace(/[^a-z0-9]/g, '');
    // 设置边界条件
    if (str.length < 2) {
	return true;
    }
    // 检测首尾是否相等不相等，如果不等就直接返回 false
    if (str[0] !== str[str.length - 1]) {
	return false;
    }

    // 递归调用
    return palindrome(str.slice(1, -1));
}
```

### 18.找出数据中重复出现过的元素
``` javascript
function repeat(arr){
	var result,map={};
	arr.map(function(num){
		if(map[num]===1){result.push(num)}
		map[num]=(map[num] || 0) + 1;	//当前值出现次数计数
	})
	return result;
}
```

### 19.数组中按照数字重复出现的次数进行排序
``` javascript
//[1,2,1,2,1,3,4,5,4,5,5,2,2] => [3, 4, 4, 1, 1, 1, 5, 5, 5, 2, 2, 2, 2]
function repeatSort(arr){
	var result=[],map={},c=[];
	arr.map(function(num){
		map[num]=(map[num] || 0) +1;
	})
	for(var key in map){
		result.push({
			num:Number(key),
			value:map[key]
		})
	};
	result.sort(function(a,b){
		return a.value-b.value
	})
	result.forEach(function(value,index){
		for(var i=0;i<value.value;i++){
			c.push(value.num)
		}
	})
	return c;
}
```

### 20.不用循环，创建一个长度为 100 的数组，并且每个元素的值等于它的下标
``` javascript
//方法一
function createArray(len, arr = []) {
	if (len > 0) {
		arr[--len] = len;
		createArray(len, arr);
	}
	return arr;
}

//方法二
Array(100).fill(0).map((_,i)=>i);

// 方法三,Array()返回一个新的数组，但是如果只有一个参数，则是指定数组长度，大于一个参数则返回新的数组
[...Array(100).keys()]

// 方法四，又发现一种
Array.from({length:100},(e,i)=>i)

// 方法五
[...Array(100)].map((e,i)=>i)

```
### 21.数据双向绑定
``` html
<input class="inputText" type="text" />
<p class="text"></p>
```	
``` javascript
var inputText=document.querySelector('.inputText');
var text=document.querySelector('.text');
//module
var obj={_txt:null};
Object.defineProperty(obj,'txt',{
	get:function(){
		return this._txt;
	},
	set:function(value){
		this._txt=value;
		text.innerHTML=value;
		inputText.value=value
	}
})
//view
inputText.addEventListener('input',function(e){
	const text=e.target.value;
	obj.txt=text;
},false)
```	
有疑问？=>[defineProperty解析](https://ymbo.github.io/2018/02/28/javascript%E7%9A%84%E6%95%B0%E6%8D%AE%E5%B1%9E%E6%80%A7%E5%92%8C%E8%AE%BF%E9%97%AE%E5%99%A8%E5%B1%9E%E6%80%A7/) 

### 22.Set 和 Map 数据结构
### 23.怎么判断两个对象相等
``` javascript
//方法一
function isEqual(a,b){
    for(let i in a){
        if(typeof a[i] == 'object' && typeof b[i] == 'object'){
            if(!isEqual(a[i],b[i]))return false
        }else if(a[i]!=b[i]){
             return false
        }
    }
    return true
}

//方法二
JSON.stringify(obj1) === JSON.stringify(obj2)
```
### 24.let与var区别
* let声明的变量作用域为所在代码块，不允许重复声明，没有变量提升
* var声明的变量作用域为所在的函数，允许重复声明，有变量提升

### 25.301与302区别
301重定向是永久的重定向，搜索引擎在抓取新内容的同时也将旧的网址替换为重定向之后的网址。

302重定向是临时的重定向，搜索引擎会抓取新的内容而保留旧的网址。因为服务器返回302代码，搜索引擎认为新的网址只是暂时的。

### 26.cookie是什么，和session有什么区别
1. session 在服务器端，cookie 在客户端（浏览器）
2. session 默认被存在在服务器的一个文件里（不是内存）
3. session 的运行依赖 session id，而 session id 是存在 cookie 中的，也就是说，如果浏览器禁用了 cookie ，同时 session 也会失效（但是可以通过其它方式实现，比如在 url 中传递 session_id）
4. session 可以放在 文件、数据库、或内存中都可以。
5. 用户验证这种场合一般会用 session因此，维持一个会话的核心就是客户端的唯一标识，即 session id

### 25.BFC
[BFC](https://zhuanlan.zhihu.com/p/25321647) 

### 26.如何从浏览器URL获取查询字符串参数
``` javascript
function search(name){
	var href=window.location.href;
	var reg=new RegExp('[?&#]'+name+'=([^&#]*)','g');
	var result=reg.exec(href);
	return result?result[1]:result;
}
//方法2
// 获取URL的查询参数
q={};location.search.replace(/([^?&=]+)=([^&]+)/g,(_,k,v)=>q[k]=v);q;
```
### 27.防抖    
原理：指定时间内多次触发事件，则每次出发事件重新计时    
例：电梯如果5秒内进人，则重新计时，如果超过5秒则运作    
应用场景：input搜索实时查询    

``` javascript
function debounce(fn,delay){
    return args=>{
        clearTimeout(fn.id)
        fn.id=setTimeout(()=>{
            fn(args)
        },delay)
    }
}
```
### 28.节流    
原理：指定时间内的多次事件只触发一次    
例：电梯5秒内进人时间不重置，5秒后运行    
应用场景：上拉加载数据    
``` javascript
function throttle(fn,delay){
    return args=>{
        if(fn.id){return}
        fn.id=setTimeout(()=>{
            fn(args)
            clearTimeout(fn.id)
            fn.id=null
        },delay)
    }
}
```
### 29.逗号操作符
描述：对它的每个操作数求值（从左到右），并返回最后一个操作数的值。
``` javascript
var x = 1;
x = (x++, x);
console.log(x);
// expected output: 2

a=1
while(a++,a<5){code...}
```
### 30、异步任务  

``` javascript 
new Promise((resolve,reject)=>{
    console.log(3);
    let p = new Promise((resolve, reject)=>{
        console.log(7);
        setTimeout(()=>{
           console.log(5);
           resolve(6); 
        },0)
        resolve(1);
    });
    resolve(2);
    p.then((arg)=>{
        console.log(arg);
    });

}).then((arg)=>{
    console.log(arg);
});
console.log(4);
```    
3 7 4 1 2 5    
涉及到的知识点：异步任务中的宏任务、微任务
### 31、遍历
tree:
``` javascript
tree = {
    name: "F",
    children: [{
        name: 1,
        children: [{
            name: "1-1",
            children: [{
                name: "1-1-1"
            }]
        }]
    },
    {
        name: 2,
        children: [{
            name: "2-1",
            children: [{
                name: "2-1-1"
            }]
        }]
    }]
}

```
#### 1、深度优先遍历
原理：类似先序遍历
``` javascript
function deepe(node,sta=[]){
	let name=node.name
	let children=node.children
	if(name){
		sta.push(name)
	}
	if(children){
		for(let i=0;i<children.length;i++){
			deepf(children[i],sta)
		}
	}
	return sta
}
deepe(tree)
// ["F", 1, "1-1", "1-1-1", 2, "2-1", "2-1-1"]
```

#### 2、广度优先遍历 
原理：优先广度
``` javascript
function breadthe(node){
	// 广度优先遍历
	let all=[];
	let stash=[]
	stash.push(node)
	while(stash.length){
		let n=stash.shift();
		all.push(n.name)
		let children=n.children
		if(children){
			for(let i=0;i<children.length;i++){
				stash.push(children[i])
			}
		}
	}
	return all
}
breadthe(tree)
// ["F", 1, 2, "1-1", "2-1", "1-1-1", "2-1-1"]
```

### 32、今年还剩几天
``` javascript
	function time(){
		var start = new Date();
        var end = new Date(start.getFullYear()+1, 0,25);
        var cu = Math.floor((end - start) / 1000);

        var seconds = cu % 60 ;
        var minutes = Math.floor(cu / 60) % 60;
        var hours = Math.floor(cu / (60 * 60)) % 24;
        var days = Math.floor(cu / (60 * 60 * 24)) % 30;
        var months = Math.floor(cu / (60 * 60 * 24 * 30)) % 12;
        var years = Math.floor(cu / (60 * 60 * 24 * 30 * 12));
 	document.getElementById('time').innerText=start.getFullYear() + '年还剩' + years + '年' + months + '月' + days + '日'
            + hours + '小时' + minutes + '分' + seconds + '秒';
}
```
