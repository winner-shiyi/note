# 我的前端小窝

我必须是你近旁的一株木棉，做为树的形象和你站在一起。

[![cover](images/cover3.jpg)](images/cover3.jpg)

2017-01-02

hublider 编辑器中打开页面会自己起一个静态服务器？？  emmet插件 补全

ul>li*5  div.name  a[href=""]

dg = getElementById

ife = if(){}else{}

ctrl + r 打开窗口预览页面

2017-01-03

匿名函数：1，不能直接声明,如果直接声明会报错；2，匿名函数要怎么调用：当它是以被赋值的形式出现的时候，并且被事件调用

比如window.onload = function(){
	
};

2017-01-04

操作属性的方式：1,通过(.);2,通过[]

btn.style["font-size"]  =  btn.style.fontSize

btn["value"] = btn.value

href 链接的地址；src 图片的地址

<img id="pic" src="2.jpg">

<a href="1.html" id="link">js</a>

link.href 取到的是 绝对地址，pic.src 取到的是 绝对地址;切忌不要拿这属性取到的值来做判断

pic.style.background=???  自己写demo证明，行间样式是 style="background:#000;"，获取到打印出来的是rgb(0,0,0)

2017-01-05

属性操作的两个注意点：
1,点操作属性的时候，后面只能跟真正的属性名称，不能跟变量名
2,[]操作的时候，里面可以放属性名称或者变量名，如果放的是属性名称，则需要加引号；如果放的是变量名，则不需要加引号
```javascript
	var name=text1.value;
	var val=text2.value;
	//box.style.name=val;会报错
	box.style[name]=val;  box.style.["width"]=val;是属性名称就需要加引号；

```
字符串：
var str3=1;
console.log(str3+'str3');//得到结果是？ 1str3 变量+字符串
流程控制语句-if：
一个非0数字转布尔值的结果是true;
牢记牢记：一个等号表示赋值。两个等号 表示对比
所以下面的例子中，无论n=0;还是n=1;还是n="1";得到的结果永远都是第二种
```javascript
	var n=12;
	if(n<0){
		alert('n小于10');
	}else if(n=10){
		alert('n等于10');
	}else{
		alert("n大于10");
	}
```
当一个条件满足的时候，代码只会走满足条件对呀的大括号的内容，其他的不会走；
```javascript
	var n=4;
	if(n<5){
		alert('n小于5');
	}else if(n<10){
		alert('n小于10');
	}else{
		alert("n大于10");
	}
```
2017-01-08

牢记，obj.style.xxx  是读和写行间样式

由此引发另外一种思路：

demo1：
<style>
#box{
	width:100px;
	height:100px;
	border:1px solid red;
}
</style>
<script>
window.onload=function(){
	var btn=document.getElementById('btn');
	var box=document.getElementById('box');
	//因为一开始box的display:block 不是行间样式，通过style拿不到
	var on="block";
	btn.onclick=function(){
		if(on=="block"){
			box.style.display="none";
			on="none";//影响第二次点击
		}else{
			box.style.display="block";
			on="block";//影响第三次点击
		}
	}
}
</script>
<input type="button" id="btn" value="按钮">
<div id="box"></div>

demo2:
	<style>
	#box{
		width:200px;
		height:200px;
		border:1px solid red;
	}
	</style>
	<script>
	window.onload=function(){
		var text=document.getElementById('text');
		var btn=document.getElementById('btn');
		var box=document.getElementById('box');
		//因为一开始box的display:block 不是行间样式，通过style拿不到
		btn.onclick=function(){
			var val=text.value;
			var newTxt='<p>'+val+'</p>';//最好用变量存一下，或者（）起来，不然+之间拼接运算符优先级
			//console.log(box.innerHTML);
			//box.innerHTML=box.innerHTML+newTxt;//插入的新内容在最后面
			box.innerHTML=newTxt+box.innerHTML;//插入的新内容在最前面
		}
	}
	</script>
	<input type="text" id="text" value="">
	<input type="button" id="btn" value="提交">
	<div id="box"></div>

2017-01-10:
累加：
n=n+1;  n+=1;  n++
累减：
n=n-1;  n-=1;  n--

有 var aa = ["11","22","33"];
console.dir(aa);用来打印一个集合

2017-01-13:

getElementsByTagName  前面的主语  可以是document  也可以是其他父级
通过这个获取到的是 一个元素的集合，类似数组，但是不是数组，因为它只具有数组的length
和下标获取，数组的其他方法它没有哦

var lis=document.getElementsByTagName('li');
lis[2].background="red";
console.dir(lis); 这个打印有一个好处  在控制台直接可以看到其长度

getElementsByClassName 前面的主语  可以是document  也可以是其他父级
getElementsByClassName 在ie8以下不兼容？？？

querySelector(css选择器)  前面的主语  可以是document  也可以是其他父级通过css选择器去获取一个元素，强调：只获取一个，如果有重复的，那它只取第一个

2017-01-14:
querySelectAll(css选择器)   前面的主语  可以是document  也可以是其他父级通过css选择器 
通过css选择器获取到一组元素，它也是一个类数组,通过下标操作具体某一项
var lis = document.querySelectorAll('#color ul li');
lis[lis.length-1].style.background='red';




