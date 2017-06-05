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
   
1. 生成[x,y]范围的随机整数    
```javascript
<script>
	function d(min,max){
		return (Math.round(Math.random()*(max-min))+min);
	}
</script>
```	
2. 已知数组var stringArray = [“This”, “is”, “Baidu”, “Campus”]，Alert出”This is Baidu Campus”	
```javascript
<script>
	function a(o){
		return o.join(' ')
	}
</script>
```	
3. 已知有字符串foo=”get-element-by-id”,写一个function将其转化成驼峰表示法”getElementById”	
```javascript
<script>
	function hump(str){
		var reg=/\-[a-z]/g;
		var str1=str.match(reg);
		str1.forEach(function(ele,index,array){
			str=str.replace(ele,ele.substr(-1,1).toUpperCase());
		})
		return str;
	}
</script>
```	
4. var numberArray = [3,6,2,4,1,5]; 实现倒排，排序。	
```javascript
<script>
	var numberArray = [3,6,2,4,1,5];
	numberArray.sort(function(value1,value2){return value2-value1})
</script>
```	
5. 怎样添加、移除、移动、复制、创建和查找节点	
```javascript

```	
6. 判断一个正整数数是不是质数，注意优化~	
```javascript
<script>
	function isN(num){
		if(typeof num!=='number' || num<=0){return;}
			for(var i=2;i<=num/2;i++){
				if( num%i==0 ){       
					return false;
				};
			}
		return true;
	}
</script>
	//这个注意i<=num/2这块，这就是优化了，之前我是除到num-1，现在只需要除到一半，因为再往上除不可能除开，新技能get~
```	
7. 取得指定数字到0的所有质数，比如给了3，那么质数为1、3	
```javascript
<script type="text/javascript">
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
</script>
```
