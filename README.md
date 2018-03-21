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
### 5. 怎样添加、删除、替换、复制、创建和查找节点	
```javascript
//** 添加**
appendChild()
var para=document.createElement("p");
var node=document.createTextNode("这是新段落。");
para.appendChild(node);

//** 插入节点 **
node.insertBefore(newnode,existingnode)
//newnode：需要插入的节点对象。
//existingnode：可选。在其之前插入新节点的子节点。如果未规定，则 insertBefore 方法会在结尾插入 newnode。


//** 删除**
node.removeChild(node)

//** 替换 **
replaceChild(newnode,oldnode);

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
Array(100).fill(0).map((_,i)=>i+1);

// 方法三
[...Array(100).keys()]

```