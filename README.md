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
src 的内容，是页面必不可少的一部分，是引入。href 的内容，是与该页面有关联，是引用。区别就是，引入和引用。       
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
```	
### 4. var numberArray = [3,6,2,4,1,5]; 实现倒排，排序。	
```javascript
var numberArray = [3,6,2,4,1,5];
numberArray.sort(function(value1,value2){return value2-value1})
```	
### 5. 怎样添加、移除、移动、复制、创建和查找节点	
```javascript

```	
### 6. 判断一个正整数数是不是质数，注意优化~	
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
### 7. 取得指定数字到0的所有质数，比如给了3，那么质数为1、3	
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
### 8. 单行写一个评级组件
```javascript
"★★★★★☆☆☆☆☆".slice(5 - rate, 10 - rate); 
//用法：rate是一个1-5的值，自定义
```	
### 9. 检查字符串不为空
```javascript
!!stringVar
```
### 10.惰性载入函数,不必每次重新进行判断，只需判断一次
```javascript
//第一种方式		
var setEvent=setClick();
setEvent(document.getElementById('box'));
function setClick(){
	if( window.addEventListener ){
		return setClick=function(ele){
			ele.addEventListener('click',function(){
				alert(this)
			},false)
		}
		}else{
			return setClick=function(ele){
			ele.onclick=function(ele){
			alert('方式2')
		}
		}
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

### 11. 原生实现bind函数    
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

### 12. new 一个类的时候，都发生了什么    
``` javascipt
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
### 13.Object.create兼容实现
``` javascript
Object._create=function(o){
	var Fn=function(){};
	Fn.prototype=o;
	return new Fn;
}
```

### 13.深拷贝
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
### 14.手写ajax
``` javscript
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

### 15.字符串是否符合回文规则
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
```