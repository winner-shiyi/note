# 我的前端小窝

我必须是你近旁的一株木棉，做为树的形象和你站在一起。

[![cover](images/cover3.jpg)](images/cover3.jpg)

2017-01-02：(海棠学院的原生js视频)

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
2017-01-08:

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

2017-01-15:
<script>
window.onload=function(){
	var lis1=document.getElementsByTagName('li');
	var lis2=document.querySelectorAll('li');
	/*这两个相同点：都是获取到一组元素，都是类数组，都可以通过下标操作*/
	/*这两个不同点：getElementsByTagName 是动态获取元素，元素增、删后会跟随变化，而querySelectorAll只获取第一次的一组元素，是静态获取*/

	var elea=document.createElement("li");
	document.getElementById('ul').appendChild(elea);
	
	console.dir(lis1);
	console.dir(lis2);

	//让所有li背景变成红色 
	//lis1.style.background="red";这样会报错，原因：你有一个筐子装满了5个苹果，你想吃一个苹果，必须要一个一个拿，不可能抱着筐子吃苹果，连着筐子都吃了吧！
	lis1[0].style.background="red";
	lis1[1].style.background="red";
	lis1[2].style.background="red";
	lis1[3].style.background="red";
}
</script>
<ul id="ul">
	<li>red</li>
	<li>white</li>
	<li>blue</li>
	<li>green</li>
</ul>

2017-01-16:
var list = [];
if(!list.length){} 这种前面加！否的写法，可以包容了这两种情况（0或者undefined，比如list是对象不是数组）

for(条件初始化;条件判断;条件变化){}  分号一个都不能少

for(var i=0;i<10;i++){
	console.log('aa');
}
for循环 执行代码的步骤，很重要，重要，重要：

第一步：条件初始化（声明了一个变量，给变量一个初始值）
var i=0;

第二步：条件判断（把变量的值限定了一个范围）
i<10;

第三步：走的是花括号里的代码（当条件判断成立的时候，走大括号里的代码）
console.log('aa');

第四步：条件变化（循环一次让变量的值加上1）
i++;

注意：从第二次循环开始，它就不走第一步了。不断的走第二步、第三步、第四步

结束：当判断条件不成立的时候，就结束循环

循环什么时候用：当需要操作一组元素做同一件事的时候就用

for(var i=0;i<10;i++){
	console.log(i,'aa');//也可以打印出i
}
alert(i);//10
for(var i=10;i>0;i--){
	console.log('bb');
}
alert(i);//0

2017-01-18:
for循环嵌套：重点 难点
有嵌套的循环，如果里面的循环没有走完的话，外面的循环步骤是不会走的
外面的循环走一次，里面的循环走3次。当里面的循环走完所有次数，才会跳到外面的循环

注意：如果有嵌套的循环，那里面的变量一定不要与外面的变量相同，如果两个变量相同的话，里面的变量会把外面的变量给覆盖了
demo1:
for(var i=0;i<3;i++){
	for(var j=0;j<3;j++){
		console.log(i);
	}
}
总结：得到0,0,0,1,1,1,2,2,2  
原理：
外层i赋值为0，符合外层条件判断，走外层花括号里面代码，进入内层循环j赋值为0，
符合内层条件判断，走内层花括号，打印外层i为0，走内层j自增j赋值为1，
符合内层条件判断，走内层花括号，打印外层i为0，走内层j自增j赋值为2，
符合内层条件判断，走内层花括号，打印外层i为0，走内层j自增j赋值为3，
不符合内层条件判断，走外层i自增i赋值为1，符合外层外层条件判断，走外层花括号里面代码，
进入内层循环j赋值为0，……

demo2:
for(var i=0;i<3;i++){
	for(var i=0;i<3;i++){
		console.log(i);
	}
}
alert(i);  //4
总结：得到0，1,2
原理：
外层i赋值为0，符合外层条件判断，走外层花括号里面代码，进入内层循环i重新赋值为0，
符合内层条件判断，走内层花括号，打印内层i为0，走内层i自增i赋值为1，
符合内层条件判断，打印内层i为1，走内层i自增i赋值为2，符合内层条件判断，
打印内层i为2，走内层i自增i赋值为3，不符合内层条件判断，进入外层i自增i赋值为4，不符合外层条件判断

demo3:
for(var i=0;i<3;++i){
	for(var i=0;i<3;++i){
		console.log(i);
	}
}
alert(i);  //4
总结：得到0，1,2 即使改成前加加++i ，得到的结果也是一样的，说明上面for循环步骤的原理也是一样适用的

2017-01-19:
需求：点击某个li，让点击的那个li背景色变为红色

循环的速度是非常快的，我们手动点击的时候，for循环已经走完了，那这个时候i的值是5
循环里添加的点击事件，点击事件里的i的值是循环结束后的i的值，而不想象中以为的对应循环的值0,1,2,3,4

window.onload=function(){
	var lis1=document.getElementsByTagName('li');
	var lis2=document.querySelectorAll('li');

	for(var i = 0;i<lis1.length;i++){
		lis1[i].onclick = function(){
			console.log(i);//5
			lis1[i].style.background = "red";//报错
		};	
	}
	alert(i);//5
}
<ul id="ul">
	<li>red</li>
	<li>white</li>
	<li>blue</li>
	<li>green</li>
	<li>black</li>
</ul>
总结：
循环走的是非常快的，按照上面的for循环解析步骤原理来论证，此时i赋值为5
所以当点击的时候只执行的是 lis1[5].style.background = "red";并不存在lis1[5]，因此报错

2017-01-20:
指的是当前对象
this 关键字，不能当变量名
只能读，不能写，意味着：this的值只能用，是不能修改

alert(this);//window
alert(this==window);//true


function fn(){
	alert(this);
}
//这种调用函数等于 window.fn();window可以省略
fn();//window  


document.onclick=fn;//document

btn.onclick=fn;//input.btn

1、this在函数外用：
	this是指向window
2、在函数内使用
	①函数是直接被调用的
		this指向window
	②被事件所调用，并且是以赋值的形式出现
		this指向是，谁调用了函数，那this就指向谁


2017-01-21:
window.onload=function(){
	var lis1=document.getElementsByTagName('li');
	var lis2=document.querySelectorAll('li');

	for(var i = 0;i<lis1.length;i++){
		lis1[i].onclick = function(){
			//在循环的时候，想给每个元素都添加点击事件，想要找到点击事件中的具体那个对象，不能下标i的值作为下标去取，要用this，this指的就是点击的那个对象
			//lis1[i].style.background = "red";//报错
			
			this.style.background = "red";//正确写法
		};	
	}
	alert(i);//5
}
<ul id="ul">
	<li>red</li>
	<li>white</li>
	<li>blue</li>
	<li>green</li>
	<li>black</li>
</ul>

2017-02-04:
属性：元素身上所具有的一些特征

1.系统自带的属性 （type、id、style、value、src）
2.自己添加的属性 

<script>
window.onload=function(){
	var btn=document.getElementById('btn');

	console.log(btn.type); //button
	console.log(btn.id); //btn

	btn.winner = '名字';//添加自定义属性
	//验证属性是否添加成功，操作属性的两种方法
	console.log(btn.winner);//名字
	console.log(btn['winner']);//名字
}
</script>
<input type="button" id="btn" value="按钮" style="width:100px;height:50px;background:#f00;">

选项卡的写法1：

<body>
	<style>
	div{
		width:200px;
		height:200px;
		border:1px solid red;
		display:none;
	}
	</style>
	<script>
	/*
	*需求：点击按钮显示对应的div，让其他的按钮背景色去掉，让其他div都隐藏
	*
	*关键点：如果获取上一个点击的按钮，这个是变化的
	*
	*分析：
	*1、获取到所有的按钮以及div
	*2、给每一个按钮添加点击事件
	*    3.把上一个点击的按钮的背景色去掉
	*    4.把上一个点击的按钮对应的div，隐藏起来
	*    1.给当前点击的按钮添加背景色
	*	 2.让当前点击按钮对应的div，显示出来
	*/
	window.onload=function(){
		var inputs=document.querySelectorAll('input');
		var divs=document.querySelectorAll('div');
		var last=inputs[0];//这个变量保存的是 上一个点击的对象，在这里默认为第0个

		/*
		* 从下面打印的内总结：
		* 每一个按钮都对应一个div，他们的下标值是相同的
		* 如果取到一个下标值，通过下标值就能找到对应的按钮与div
		*/
		console.dir(inputs);
		console.dir(divs);

		//给每个按钮添加点击事件
		for(var i=0;i<inputs.length;i++){

			//每个按钮的下标值恰好也对应循环中的i值，所以给每个按钮添加一个自定义属性index并且等于i
			//这里涉及到事件触发和i赋值，一定要放在点击事件外面
			inputs[i].index=i;

			inputs[i].onclick=function(){
				//inputs[i].index=i;不能放在click事件里面，因为循环是非常快的，点击事件发生的这时候的i是等于3

				//把上一个点击的按钮的背景色去掉
				last.style.background='';

				//把上一个点击的按钮对应的div，隐藏起来
				divs[last.index].style.display='none';

				//给当前点击的按钮添加背景色
				this.style.background="yellow";

				//让当前点击按钮对应的div，显示出来
				divs[this.index].style.display='block';

				//当前对象this相对于下一次点击来说，它就是上一次点击对象
				//把当前对象 变成 上一个点击的对象（一定要放在所有代码之后）
				last=this;

			}

		}
		
	}
	</script>
	<input type="button" id="" value="选项1" style="background:yellow;">
	<input type="button" id="" value="选项2">
	<input type="button" id="" value="选项3">
	<div style="display:block;">内容1</div>
	<div>内容2</div>
	<div>内容3</div>
</body>

选项卡的写法2：
<body>
	<style>
	div{
		width:200px;
		height:200px;
		border:1px solid red;
		display:none;
	}
	</style>
	<script>
	/*
	*需求：点击按钮显示对应的div，让其他的按钮背景色去掉，让其他div都隐藏
	*
	*
	*分析：
	*1、获取到所有的按钮以及div
	*2、给每一个按钮添加点击事件
	*    3.把所有按钮的背景色去掉
	*    4.把所有div都隐藏起来
	*    1.给当前点击的按钮添加背景色
	*	 2.让当前点击按钮对应的div，显示出来
	*/
	window.onload=function(){
		var inputs=document.querySelectorAll('input');
		var divs=document.querySelectorAll('div');


		//给每个按钮添加点击事件
		for(var i=0;i<inputs.length;i++){

			//每个按钮的下标值恰好也对应循环中的i值，所以给每个按钮添加一个自定义属性index并且等于i
			//这里涉及到事件触发和i赋值，一定要放在点击事件外面
			inputs[i].index=i;

			inputs[i].onclick=function(){
				//inputs[i].index=i;不能放在click事件里面，因为循环是非常快的，点击事件发生的这时候的i是等于3

				//把所有按钮的背景色去掉 把所有div都隐藏起来
				//操作一组元素，原生js要使用for循环
				for(var i=0;i<inputs.length;i++){
					//这里的嵌套循环变量i重名是没关系的，是因为这里的变量i是只在这个点击事件内的作用域内，不受外面影响
					inputs[i].style.background='';
					divs[i].style.display='none';
				}

				//给当前点击的按钮添加背景色
				this.style.background="yellow";

				//让当前点击按钮对应的div，显示出来
				divs[this.index].style.display='block';

			}
		}
		
	}
	</script>
	<input type="button" id="" value="选项1" style="background:yellow;">
	<input type="button" id="" value="选项2">
	<input type="button" id="" value="选项3">
	<div style="display:block;">内容1</div>
	<div>内容2</div>
	<div>内容3</div>
</body>

2017-02-05:(李炎恢的原生js视频)

流程控制语句中的if：
var box=50;
//if使用在单行语句里的表达式如果返回的false，只会不执行其后面的一条语句，其后的第二条语句仍然会执行。
//所以最好使用复合语句if（表达式）{}
if(box>50)
	alert(box);
	alert('不管你的if是true还是false，都会执行该语句');
</script>


2017-02-06:

do{}while()循环语句：

//先运行在判断的循环体；先弹出1，累加，在判断，在弹出2，在累加，在判断……，弹出5，累加为6，判断不符合终止
var box=1;
do{
	alert(box);
	box++;
}while(box<=5);
//如果条件一开始不满的话，至少会执行一次。会谈出一次10
var bb=10;
do{
	alert(bb);
	bb++;
}while(bb<=5);
//切忌，循环体的判断要想好，不然可能会进入死循环。如下弹出10，11，12……
var aa=10;
do{
	alert(aa);
	aa++;
}while(aa>5);

while(){}循环语句和for循环语句对比：

//while循环和for循环，这样弹出的结果是一样的；
//不同之处在for循环可以在循环执行之前初始变量，for循环的执行步骤为：初始声明变量，判断条件为true，alert(),最后在累加
var box=1;
while(box<=5){
	alert(box);
	box++;
}

for(var box=1;box<=5;box++){
	alert(box);
}

for(var x in obj){}语句用来枚举对象的属性：
var box={
	'name':'weina',
	'age':28,
	'height':165
};
for(var x in box){
	alert(x);//弹出box对象的所有属性名称：name，age，height
}

break退出循环语句和continue退出当前循环语句的对比：

//break 是退出整个外面的循环，当满足条件的时候，不执行条件判断下面语句
for (var i = 0; i < 10; i++) {
	if(i==5) break;
	document.write(i+'<br/>');//0 1 2 3 4
};

//continue 是退出当前循环，，当满足条件的时候，不执行判断后面的语句，但不影响外面的继续执行循环
for (var b = 0; b < 10; b++) {
	if(b==5) continue;
	document.write(b+'<br/>');//0 1 2 3 4 6 7 8 9
};

with(){}语句，适用于对象：
//with语句的作用是将代码的作用域设置到一个特定的对象中，所以可以省略box.
var box={
	'name':'weina',
	'age':28,
	'height':165
};
var n=box.name;
var a=box.age;
var h=box.height;
alert(n+a+h);
//使用with语句改写如下
with(box){//存放对象的名称
	var n=name;//这里的name 相当于 box.name
	var a=age;
	var h=height;
}
alert(n+a+h);

function函数的return返回值：
//弹出"我只有被调用才可以执行"  
//return的作用是让box() = "我只有被调用才可以执行"
function box(){
	return"我只有被调用才可以执行";
}
alert(box());//或者 var str=box();把返回值保存成一个变量也是ok，alert(str);

//弹出"我只有被调用才可以执行"  继续弹出"undefined"
//因为这里没有return返回值 所以得到undefined
function box2(){
	alert("我只有被调用才可以执行");
}
alert(box2());

//return语句还有一个功能就是退出当前函数，注意和break的区别。ps：break用在循环和switch语句里
//当函数遇到第一个return的时候，就会终止，不会继续往下执行
function box3(){
	return 10;
	return 100;
}
alert(box3());//10  

//遇到传参数的函数，有return值时候
function box4(num){
	if (num<5) return num;
	return 100;
}
alert(box4(6));//100 

arguments数组对象：js函数不介意传递进来多少参数，也不会因为参数不统一而报错，都可以通过arguments对象来接收
//函数参数在定义到时候 和 调用的时候 不统一，并不会报错
function box1(){
	return arguments[0]+'|'+arguments[1];
}
alert(box1('weina',28));//weina|28

arguments是一个数组对象,动态传参，其的具体作用和实例：
通过arguments对象可以实现一个功能：动态计算。比如要实现一个加法运算，把传进来的数字累加，但是传进来的数字又是不确定有几个。
function box1(){
	var sum=0;
	if(arguments.length==0) return sum;//如果没有传参数的时候，返回0，退出
	for (var i = 0; i < arguments.length; i++) {
		sum+=arguments[i];
	};
	return sum;
}
alert(box1());//0
alert(box1(1,2));//3
alert(box1(1,2,3,4));//10

js中的function函数 没有 没有 没有 像其他高级语言的函数重载功能：
//重载功能，就是根据参数，选择相同函数名而参数不同的函数
//重载通俗的说就是：实际调用函数的时候，会根据具体参数个数来选择相同函数名的函数，这里就应该选择上面的函数
//函数同名也不报错，因为第二个会覆盖第一个
function box(num,a) {
	return num+100;
}
function box(num) {
	return num+200;
}
alert(box(50,1));//250 


对象，创建对象的方法，实际常用字面量创建对象来传参：
//创建一个对象的方式：new一个Object，也可以直接Object，字面量方式
function objrun(){
	return '123';
}
var box = new Object();
box.name='weina';
box.age=28;
box.run=objrun;

alert(box.run);//function 函数体
alert(box.run());//123

box.run1=objrun();
alert(box.run1);//123

var box1={
	name:'weina',
	run:function(){
		return 123;
	}
}
alert(box1.run());//123

//使用delete关键字删除对象的属性
var box2={
	name:'weina',
	age:28,
	run:function(){
		return 123;
	}
}
alert(box2.name);//weina
delete box2.name;
alert(box2.name);//undefined

//当函数的参数有很多个的时候，使用字面量创建对象来传参的好处
function box(name,age,height,address){
	alert(name);
	alert(age);
	alert(height);
}
box('weina',28,165,'建阳');

//下面就是使用字面量创建对象传参
var obj ={
	name:'weina',
	age:28,
	height:165,
	address:'建阳'
}
function box1(obj){
	alert(obj.name);
	alert(obj.age);
	alert(obj.height);
}
box1(obj);

//如果实际传参中没有或者确实某个参数
var obj ={
	name:'weina',
	age:28,
	height:165,
	address:'建阳'
}
function box1(obj){
	alert(obj.name);
	alert(obj.love);//实际传的参数中没有love属性，则会打印出undefined
	alert(obj.age);
	alert(obj.height);
}
box1(obj);

//避免出现undefined的方法就是 强大的判断
var obj ={
	name:'weina',
	age:28,
	height:165,
	address:'建阳'
}
function box1(obj){
	if(obj.name!=undefined) alert(obj.name);
	if(obj.love!=undefined) alert(obj.love);
	if(obj.age!=undefined) alert(obj.age);
	if(obj.height!=undefined) alert(obj.height);
}
//box1(obj);
//进一步改写：把很多的参数，当做一个匿名对象传入
box1({
	name:'weina',
	age:28,
	height:165,
	address:'建阳'
})

数组对象：
//创建一个数组对象的方式：new一个Array，也可以直接Array，字面量方式
var box=new Array();
alert(box);//空
alert(typeof box);//object

var box=new Array('weina',28,165);
alert(box);//weina,28,165
alert(box[0]);//weina

//对比下面两种：
var box=new Array(5);//创建数组包含5个元素，必须是数字，必须只能有1个参数
alert(box);//,,,,,   

var box1=new Array(5,2);
alert(box1);// 5,2

//字面量的方式创建数组
//数组中额外的逗号，在ie浏览器中获取到并且计算到length中，产生错误
var box=[1,2,3,];//这里逗号没有删掉
alert(box);//在高级浏览器中是 1,2,3 IE中1,2,3，
alert(box.length);//高级浏览器中是3，IE中是4


//当数组下标是字符串的时候需要注意
var box=[];
box['name']='weina';
box['age']=28;
alert(box);//空 无法打印出来数组，不会提现在数组上
alert(box.name);//weina
//当数组下标是 数字的索引下标的时候，可以打印出来，体现在数组上
var box1=[];
box1[0]='weina';
box1[1]=28;
alert(box1);//weina,28

//通过length可以获取或者设置数组中最后一个元素
var box=['weina',28,'建阳']；
box[box.length]='福建'；
alert(box);

2017-02-07:
对象中的方法：对象或者数组都具有的方法
var box =['weina',28,'建阳',new Date()];
console.log(box);
console.log(box.toString());
console.log(box.valueOf());
console.log(box.toLocaleString());

//join()方法后得到的是字符串，并不影响原来数组
console.log(box.join('|'));
console.log(typeof box.join('|'));
console.log(typeof box);

//栈方法 后进先出的原则  push(),pop()
//push()可以接收任意数量的参数，逐个添加到数组的末尾，返回的是修改后数组的长度
//pop()移除数组中的最末尾元素，返回的是被移除的元素
var box =['weina',28,'建阳'];
console.log(box.push('福建'));
console.log(box);
console.log(box.pop());

//队列方法 先进先出 shift()移除数组中的第一个元素，返回的是这个被移除的元素（也就是开头的元素）
//unshift()在ie浏览器中返回值有问题，很少使用
var box =['weina',28,'建阳'];
console.log(box.push('福建'));
console.log(box.shift());
console.log(box);

//数组中重新排序的方法 reverse()逆向排序,sort()从小到大排序
var box =[1,2,3,4,5];
console.log(box.reverse());//5,4,3,2,2
console.log(box);//5,4,3,2,2 原数组也逆序了，对其引用进行操作

//使用sort()方法注意点：因为数字排序和数字字符串排序的算法是一样的，为了修改这个问题，给sort(参数)方法传递一个函数参数

function compare (value1,value2) {
	if (value1<value2) {
		return -1;
	}else if(value1>value2){
		return 1;
	}else{
		return 0;
	}	
}
var box =[0,1,5,10,15];
var box1 =['0','1','5','10','15'];
var box2=[0,6,5,10,8];
console.log(box.sort());//[0, 1, 10, 15, 5]排序错误了，等同于数字字符串的码表排序
console.log(box1.sort());//["0", "1", "10", "15", "5"]
//给sort()传递一个参数
console.log(box.sort(compare));//[0, 1, 5, 10, 15]
console.log(box1.sort(compare));//["0", "1", "10", "15", "5"]
//如果需要逆序排列，因为此时的sort已经修改了原box数组
console.log(box.reverse());//[15, 10, 5, 1, 0]
console.log(box2.reverse());//[8, 10, 5, 6, 0]直接这样排序是按照码表逆向排序，不正确的

//concat()创建了一个新数组，并不影响原来的数组
var box =['weina',28,'建阳'];
var box2 =box.concat('计算机');
console.log(box2);//["weina", 28, "建阳", "计算机"]
console.log(box);//['weina',28,'建阳'];

//slice()基于当前数组，可以获取指定区域的元素并创建成为一个新数组,不影响原数组
var box =['weina',28,'建阳','计算机'];
var box2=box.slice(1,3);//从第1个位置开始取到第3个位置前的元素，仍然是数组
console.log(box2);//[28, "建阳"]
console.log(box);//['weina',28,'建阳','计算机']


//splice()主要用途是像数组的中部插入元素，影响原数组
//删除功能
var box =['weina',28,'建阳','计算机'];
var box2=box.splice(1,3);//这里表示从第1个开始，取3个元素,创建成一个新数组，但是会影响原来数组
console.log(box2);// [28, "建阳", "计算机"]
console.log(box);//["weina"]
//插入功能
var box =['weina',28,'建阳','计算机'];
var bb = ['dd',26,'江西'];
var box2=box.splice(1,0,'福建');//表示从第1个元素开始，不删除元素，直接添加'福建'
console.log(box2);//[] 返回为空
console.log(box);//["weina", "福建", 28, "建阳", "计算机"]
var box3=bb.splice(1,1,'福建');//表示从第1个元素开始，删除1个元素，在添加'福建'
console.log(bb);//["dd", "福建", "江西"]

2017-02-08:

时间与日期对象：Date()类型
var  box=new Date('January 32 2017');//当传入的参数如期是多出来的（错误的时候），在不同浏览器中将会返回不同的时间
console.log(box);//谷歌是无效日期，IE是2月1号，火狐也是2月1号，opera浏览器是1月30

//UTC()协调世界统一时间
console.log(Date.UTC(2017,2,24));//返回毫秒数量
var box = new Date(Date.UTC(2017,2));
console.log(box);//Wed Mar 01 2017 08:00:00 GMT+0800 (中国标准时间),月份变成3月份，时间要加上个8小时，东八区
console.log(new Date(2017,2));//Wed Mar 01 2017 00:00:00 GMT+0800 (中国标准时间)


时间与日期对象 的相关方法：

对象通用方法：
var box = new Date(2017,10,15,17,22,45);
alert(box.toString());
alert(box.valueOf());//返回的是毫秒数
alert(box.toLocaleString());
组件方法：（获取单独想要的具体时间）
	var box = new Date(2017,10,15,17,22,45);
	alert(box.setTime('2018'));//设置毫秒数
	box.getYear();//方法是废弃的方法
	
	getMonth();//月份要加1
	var box = new Date(2017,10,15,17,22,45);
	console.log(box.getMonth());//10
	var box1 = new Date();//获取到：当前日期是2017、02、09
	console.log(box1.getMonth());//1，，，比实际的 月份少1
	
	getHours()和getUTCHours() 有8个小时的时差,东八区
	var box1 = new Date();//获取到：当前日期是2017-02-09-15:28
	console.log(box1.getHours());//15
	console.log(box1.getUTCHours());//7

	//想在页面上 显示 年月日,时分秒
	var box1 = new Date();//获取到：当前日期是2017-1-9 15:48:55
	//少一个关于获取 星期几的 封装函数???
	var day = box1.getDay();
	console.log(box1.getFullYear()+'-'+box1.getMonth()+'-'+box1.getDate()+' '+box1.getHours()+':'+box1.getMinutes()+':'+box1.getSeconds());//2017-1-9 15:48:55

2017-02-09:
正则表达式:
	//模式修饰符:i 忽略大小写,g 全局匹配,m 多行匹配
	//正则对象 RegExp包含两个方法：test(),exec()
	
	var pattern = new RegExp('box','i');
	var pattern1 = /xox/i;
	var str = 'this is a Box';
	console.log(pattern.test(str));//true
	console.log(pattern1.test(str));//false

	console.log(pattern.exec(str));//["Box", index: 10, input: "this is a Box"]index：表示匹配到开始的位置，input：表示当前被匹配的字符串
	console.log(pattern1.exec(str));//null

	var pat=/g.gle/;//.点符号匹配任意字符，除了换行符
	var str='gogle';
	alert(pat.test(str));//true
	
	var pat=/ga*gle/;//*符号表示匹配0个a，或者1个a，或者多个a
	var str='gaagle';
	alert(pat.test(str));//true
	
	var pat=/ga+gle/;//+符号表示匹配1个a，或者多个a
	var str='gaaagle';
	alert(pat.test(str));//true
	
	var pat=/ga?gle/;//？符号表示匹配1个a，或者0个a
	var str='gaagle';
	alert(pat.test(str));//false
	
	var pat=/ga.?gle/;//.？符号表示匹配1个或者0个任意字符
	var str='gaagle';
	alert(pat.test(str));//true
	
	var pat=/go{2,4}gle/;//o{2,4}表示匹配o2-4次，包含2和4
	var str='goooogle';
	alert(pat.test(str));//true
	
	var pat=/gogle{2,4}/;//e{2,4}，并没有使用$限定结尾
	var str='gogleeeeeeeeee';
	alert(pat.test(str));//true
	
	var pat=/go{3}gle/;//o{3}表示匹配o3次，只能是3次
	var str='gooogle';
	alert(pat.test(str));//true
	
	var pat=/go{3,}gle/;//o{3,}表示匹配o3次,或者3次以上
	var str='goooooogle';
	alert(pat.test(str));//true
	
	var pat=/oogle/;
	var pat1=/[a-z]oogle/;//[a-z]表示26个小写字母都匹配，区分大小写
	var str='gooooogle';
	alert(pat.test(str));//true 匹配到后面oogle，因为没有前导限定
	alert(pat1.test(str));//true
	
	var pat1=/[a-zA-Z0-9]oogle/;//[a-zA-Z0-9]表示26个小写字母,大写字母，数字都匹配
	var str='gooooogle';
	alert(pat1.test(str));//true
	
	var pat1=/[^a-zA-Z0-9]oogle/;//[^a-zA-Z0-9]表示非 0-9,大小写字母的任意字符
	var str='-oogle';
	alert(pat1.test(str));//true
	
	var pat1=/^[0-9]oogle/;//^符号放在/后面，不是[]里面表示前导限定0-9开始
	var str='9oogle';
	alert(pat1.test(str));//true
	
	var pat1=/oogle[0-9]$/;//$符号结尾限定[0-9]
	var str='oogle9';
	alert(pat1.test(str));//true
	
	var pat1=/^[0-9]+oogle/;//^[0-9]+表示前导限定，1个或者多个0-9开始
	var str='9999oogle';
	alert(pat1.test(str));//true
	
	var pat1=/[a-zA-Z0-9_]oogle/;//等同于 /\woogle/, \w 匹配字母数字和_,\W表示完全相反,等同于[^a-zA-Z0-9_]
	var str='_oogle';
	alert(pat1.test(str));//true
	
	var pat1=/\doogle/;//\d匹配[0-9],\D匹配[^0-9]
	var str='9oogle';
	alert(pat1.test(str));//true
	
	var pat1=/goo\sgle/;//\s匹配空格，可以直接使用空格，也可以\s
	var str='goo gle';
	alert(pat1.test(str));//true
	
	var pat1=/google\b/;//\b表示匹配是否到达边界
	var str1='googlee';
	var str2='google';
	alert(pat1.test(str1));//false
	alert(pat1.test(str2));//true
	
	var pat1=/google|baidu|bing/;//|符号表示或者
	var pat2=/^[\w]+\.(zip|rar|7Z)$/;//！选择符号必须使用分组符号()包含起来

	var str1='this is baidu';
	var str2='soso';
	var str3='123.zip';
	alert(pat1.test(str1));//true
	alert(pat1.test(str2));//false
	alert(pat.exec(str));
	
	var pat=/gogle{2,4}$/;//匹配e{2,4}次
	var pat1=/(gogle){2,4}/;//()分组符号，可以看成是一个字符，表示匹配gogle 整个字符串2-4次
	var str='gogleeee';
	var str1='goglegogle';
	alert(pat.test(str));//true
	alert(pat1.test(str1));//true
	//RegExp.$1表示获取 正则模式 中 第一个分组 对应的 匹配字符串
	var pat = /8(.*)8/;
	var str = 'this is a 8google8';
	str.match(pat);//先运行一下
	console.log(pat.$1);//undefined
	console.log(RegExp.$1);//google
	
	//$1的实际应用：
	var pat = /8(.*)8/;
	var str = 'this is a 8google8';
	document.write(str.replace(pat,'<strong>$1</strong>'));//google
	
	//正则实现字符串中位置交换
	var pat = /(.*)\s(.*)/;
	var str = 'google baidu';
	console.log(str.replace(pat,'$2 $1'));//baidu google
	
	//贪婪符号
	var pat = /[a-z]/;
	var pat1 = /[a-z]+/;//使用了贪婪模式
	var pat2 = /[a-z]+?/;//加了一个惰性模式
	var str = 'google';
	console.log(str.replace(pat,'1'));//1oogle
	console.log(str.replace(pat1,'1'));//1  匹配1次或者多次，所有字符串被替换成1
	console.log(str.replace(pat2,'1'));//1oogle 只匹配1次
	
	var pat = /8(.*)8/;//使用了贪婪模式
	var pat1 = /8(.*?)8/g;//加了一个惰性模式  就是加一个?，禁止了贪婪，开启全局
	var str ='8goole8 8goole8 8goole8';
	document.write(str.replace(pat,'<strong>$1</strong>'));//goole8 8goole8 8goole
	document.write(str.replace(pat1,'<strong>$1</strong>'));//goole goole goole 
	
	
	var pat =/^[a-z]+\s[0-9]{4}$/;
	var pat1=/^([a-z]+)\s([0-9]{4})$/;//使用了()分组返回
	var str ='google 2012';
	var a=pat1.exec(str);
	console.log(pat.exec(str));//Array[1]0: "google 2012"index: 0input: "google 2012"length: 1__proto__: Array[0]
	alert(pat.exec(str));//google 2012
	console.log(a);
	console.log(a[0]);//返回匹配到的整个字符串
	console.log(a[1]);//返回匹配到的第一个分组的字符串
	console.log(a[2]);//返回匹配到的第二个分组的字符串
	
	//捕获性分组，非捕获性分组
	var pat =/(\d+)([a-z])/;//这个叫捕获性分组，所有的分组都捕获返回
	var pat1=/(?:\d+)(?:[a-z])/;//非捕获性分组，只要在不需要捕获返回的 分组 前加上 ?:
	var str='123abc';
	var a=pat.exec(str);
	var b=pat1.exec(str);
	console.log(a[0]);//123a返回匹配到的整个字符串
	console.log(a[1]);//123返回匹配到的第一个分组的字符串
	console.log(a[2]);//a回匹配到的第二个分组的字符串
	
	console.log(b[0]);//123a返回匹配到的整个字符串
	console.log(b[1]);//123返回匹配到的第一个分组的字符串
	console.log(b[2]);//undefined

2017-02-11：
function函数类型：
函数声明方式：
1,function aa(num1){};
2,var aa=function(num1);
3,var aa=new Function(num1);//使用function构造函数
ps:不推荐 第三种方式，因为这种方式会导致解析两次代码（第一次解析常规ECMA代码，第二次解析传入构造函数中的字符串），从而影响性能。

function box(sum,num){//把函数本身作为一个值用于参数传递，而不是函数的返回值结果作为参数传递
	return sum(num);
}
function box1(sum,num){//把函数的返回值作为参数传递
	return sum+num;
}
function sum(num){
	return num+10;
}
var result=box(sum,10);
var result1=box1(sum(10),10);
alert(result);//20
alert(result1);//30

1*2*3*4*5……阶乘，递归算法，一般都要在内部调用函数自身，可以使用arguments对象有一个callee的属性，该属性是一个指针，指向拥有这个arguments对象的函数
function box(num){
	if(num<=1){
		return 1;
	}else{
		//return num*box(num-1);
		//如果在内部多次递归调用函数自身，更为简便的操作是
		return num*arguments.callee(num-1);
	}
}
alert(box(4));//1*2*3*4=24

var color='红色的';//这里color是全局变量，而这个全局变量又是window的属性
alert(window.color);//红色的


function函数的属性和方法：每个函数都包含2个属性，length和property。
property原型，有两个方法apply 和call，都可以冒充某个对象，更重要的是可以扩展赖以运行的作用域，apply()要传两个参数，call()只要一个，用着更方便：

function box(num1,num2){
	return num1+num2;
}
function sum(num1,num2){
	return box.apply(this,[num1,num2]);//apply(this表示window作用域，[表示传递参数])
}
function sum2(num1,num2){
	return box.apply(this,arguments);//arguments 可以当数组传递
}
function sum3(num1,num2){
	return box.call(this,num1，num2);//call(this表示window作用域，表示传递参数，表示传递参数)
}
console.log(sum(10,10));//20
console.log(sum2(10,10));//20

//用call实现对象冒充，函数冒充的方法如下：
var color="红色的";
var box={color:'蓝色的'};

function sayColor(){
	alert(this.color);
}
sayColor();//红色的   等同于window.sayColor()
sayColor.call(window);//红色的  冒充window
sayColor.call(this);//红色的   this就是window
sayColor.call(box);//蓝色的

2017-02-12：
变量，作用域，内存：
变量不强制类型，所以js是松散型语言
变量包含两种类型：
1，基本类型值（保存在栈内存中的简单数据段：undefined、null、boolean、number和string，占有固定大小的空间）
2，引用类型值（保存在堆内存中的对象，变量实际上只是一个指针，指向堆内存中的一个对象）

在复制变量值的时候:
基本类型复制的是栈内存中的值本身，而引用类型复制的是存放在栈内存中的数据段（一个名称）
var box ='lee';
var box2=box;
console.log(box);//lee
console.log(box2);//lee

var box ={};
box.name='lee';
var box2=box;
console.log(box2.name);//lee
console.log(box.name);//lee
box2.name='kkk';
console.log(box2.name);//kkk因为box 和 box2指向的是堆内存中同一个对象，不管谁改了，大家都一起修改了
console.log(box.name);//kkk

变量作为传递参数的时候：
js中所有函数的参数都是按照值来传递的，参数是不会按引用传递的，虽然变量有分成基本类型和引用类型

//参数是 基本类型的时候 按照值传递
var num=50;
function box (num) {//这里的形参num相当于是一个局部变量，和外部没有任何联系
	num+=10;
	return num;
}
console.log(box(num));//60
console.log(num);//50

//参数是 引用类型的时候 注意：也是按照值传递，只是传递的参数是引用类型
var obj= {num:50};
function box (test) {
	test.num+=10;
	console.log(test===obj);//true
	return test;
}
console.log(box(obj).num);//60
console.log(obj.num);//60  因为在堆内存中都指向一个对象，不管谁改了，全部都改了

var obj={};
function box(obj){
	obj.name='lee';
	var obj={};//这里其实是断开旧的对象的引用，指向了新的对象的引用
	obj.name='kkk';
	return obj;//这里返回的是新的对象的引用
}
console.log(box(obj));//Object {name: "kkk"}
console.log(box(obj)===obj);//false
console.log(obj.name);//lee


优化内存的最好方式，当一个对象使用完以后 把它设为null

基本包装类型：是基本类型，但又是特殊的引用类型，就称为基本包装类型
var box='mr.lee';
console.log(box.sustring(2));//这种写法就是引用类型的写法，其实调用都是系统内置的方法
box.name='red';
console.log(box.name);//undefined 给基本类型加自定义的属性和方法 是无效的

var box=new String('mr.lee');
box.name='red';
console.log(box.name);//red 通过new运算符 创建的box 就是一个对象可以添加自定义的属性和方法

静态属性：就是直接通过 名称就可以调用的属性，无需new运算创建对象

number类型：有5种方法
var box=1000.784;
console.log(box.toString());
console.log(box.toSLocaleString());
console.log(box.toFixed(2));
console.log(box.toExponential());
console.log(box.toPrecision(2));
console.log(box.toPrecision(8));

2017-02-13：	
字符串对象常用的截取方法：
//ps注意：IE中使用substr(负数参数)会全部返回，，，所以慎用substr
	var box='mr.lee';
	console.log(box.charAt(1));//r  返回指定索引位置的字符
	console.log(box.charCodeAt(1));//114  l的asssii码
	//如果参数只有1个，并且是正数，截取的结果是一样的，都是截取到最后
	console.log(box.substring(1));//r.lee从开始位置1截取到最后
	console.log(box.slice(1));//r.lee 
	console.log(box.substr(1));//r.lee 
	//参数有2个的时候，并且都是正数
	console.log(box.slice(4,6));//ee 从开始位置4截取到位置6(不包括位置6)
	console.log(box.substr(4,2));//ee 从开始位置4截取，选2位字符
	//如果参数只有1个，并且是负数的时候
	console.log(box.slice(-2));//ee  倒数第二个开始截取到最后
	console.log(box.substring(-2));//mr.lee  变成从0开始截取到最后，等同于返回全部字符串
	console.log(box.substr(-2));//ee 倒数第二个开始截取到最后
	//如果参数有2个的时候，并且有负数
	console.log(box.slice(2,-1));//.le 从位置2开始截取，到位置-1(不包括位置-1)
	console.log(box.substring(2,-1));//mr 如果第二个参数比第一个参数小，第二个参数就会提前，变成substring(0,2)
	console.log(box.substring(2,1));//r substring(1,2)
	console.log(box.substring(2,-1));//空   第二个参数为负，直接等于0，选0个
	
	//获取字符串中某个字符的位置的方法：
	var box='mr.lee is lee';
	console.log(box.indexOf('l'));//返回 初始位置开始搜索l第一次出现的位置，3
	console.log(box.lastIndexOf('l'));//返回 末尾位置开始搜索l第一次出现的位置，10
	console.log(box.indexOf('l',5));//从第5个位置开始向后搜索l第一次出现的位置，10
	console.log(box.lastIndexOf('l',5));//第5个位置开始向前搜索l第一次出现的位置，3
	console.log(box.indexOf('a'));//如果没有找到想要的字符串，则 返回-1
	
	//找到字符串中所有的l的位置，放到某个数组中
	var boxarr=[];
	var pos=box.indexOf('l');
	while(pos>-1){
		boxarr.push(pos);
		pos=box.indexOf('l',pos+1);
	}
	console.log(boxarr);//[3,10]
	
	//字符串中的大小写转换方法：
	var box='Mr.lee is lee';
	console.log(box.toLowerCase());//全部小写  mr.lee is lee
	console.log(box.toUpperCase());//全部大写  MR.LEE IS LEE
	console.log(box.match('l'));//找到l 即返回l ["l", index: 3, input: "Mr.lee is lee"]
	console.log(box.match('a'));//找没找到返回 null
	console.log(box.split('.'));//按照传入的参数分割成数组  ["Mr", "lee is lee"]
	
	var box1='百度';
	console.log(box1.link('http://www.baidu.com'));//<a href="http://www.baidu.com">百度</a>
	
	//ECMA 中的内置对象只有两个global 对象和 math 对象:
	
	//global对象的属性和方法：
	//1,(URI编码和解码）
	var box='//lee李';
	var a=encodeURI(box);
	var b=encodeURIComponent(box);
	console.log(a);//只编码了中文，不会对本书属于URI的特殊字符进行编码//lee%E6%9D%8E
	console.log(b);//特殊字符和中文都编码了，编码更彻底，更常用%2F%2Flee%E6%9D%8E
	//解码
	console.log(decodeURI(a));//   //lee李
	console.log(decodeURIComponent(b));//   //lee李
	
	//2,eval()方法 解析字符串的作用 有可能被黑客注入代码
	eval(alert(100));
	//global对象的属性：undefined，NaN,Object，Array，Function等等
	console.log(Array);//返回构造函数 function Array() { [native code] }

	//Math()对象 的属性 和 方法
	var aa='';
	console.log(Math.min(1,5,3,7,9,0,3));//0
	console.log(Math.max(1,5,3,7,9,0,3));//9
	console.log(Math.max([1,5,3,7,9,0,3]));//NaN
	console.log(Math.max([1,5,3,aa,9,0,3]));//NaN
	//ceil()向上舍入
	console.log(Math.ceil(25.9));
	console.log(Math.ceil(25.5));
	console.log(Math.ceil(25.1));
	//floor()向上舍入
	console.log(Math.floor(25.9));
	console.log(Math.floor(25.5));
	console.log(Math.floor(25.1));
	//round()四舍五入
	console.log(Math.round(25.9));
	console.log(Math.round(25.5));
	console.log(Math.round(25.1));

	//随机方法(0-1之间的随机数，但不包含0和1)
	console.log(Math.random()*10);
	//获取1-10的随机整数，5-10的随机整数
	for(var i=0;i<10;i++){
		console.log(Math.floor(Math.random()*10 +1 ));//范围1-10（包含1和10） 公式：10+1-1=10
	}
	for(var i=0;i<10;i++){
		console.log(Math.floor(Math.random()*10 +5 ));//范围5-14（包含5和14） 公式：x+5-1=14 x=10
	}
	for(var i=0;i<10;i++){
		console.log(Math.floor(Math.random()*6 +5 ));//范围5-10（包含5和10） 公式：x+5-1=10 x=6
	}
	//获取随机整数，封装一个函数
	function randomNum (start,end) {
		var total=end-start+1;//公式
		return Math.floor(Math.random()*total +start);
	}
	console.log(randomNum (3,10));
	

2017-02-14:
面向对象与原型
//工厂模式：就是为了解决实例化对象产生大量重复的问题。优点：集中实例化；缺点：分不清是哪个对象的实例；
	function createObj(name,age){
		var obj=new Object();
		obj.name=name;
		obj.age=age;
		obj.run=function(){
			return this.name+this.age+'运行中';
		}
		return obj;//一定要返回对象引用
	}
	function createObj2(name,age){
		var obj=new Object();
		obj.name=name;
		obj.age=age;
		obj.run=function(){
			return this.name+this.age+'运行中';
		}
		return obj;
	}
	
	var box1=createObj('lee',11);
	var box2=createObj('kkk',28);//可以创建多个实例对象
	
	console.log(box1.run());//lee11运行中  打印box1对象实例的run()方法
	console.log(box2.run());//kkk28运行中   打印box2对象实例的run()方法
	
	var box3=createObj2('weina',30);//box1，box2，box3都是对象，分不清是哪个对象的实例
	console.log(box1 instanceof Object);//都是 true
	console.log(box2 instanceof Object);//都是 true
	console.log(box3 instanceof Object);//都是 true

	
	//构造函数(方法)创建
	//构造函数内部没有new Object，但它的后台会自动var obj=new Object，this就相当于obj，构造函数不需要返回对象引用，它是后台自动返回
	function Box(name,age){
		this.name=name;
		this.age=age;
		this.run=function(){
			return this.name+this.age+'运行中';
		}
	}
	function Desk(name,age){
		this.name=name;
		this.age=age;
		this.run=function(){
			return this.name+this.age+'运行中';
		}
	}
	var box1=new Box('lee',11);
	var box2=new Box('kkk',28);
	var box3=new Desk('weina',100);
	console.log(box1.run());//lee11运行中  打印box1对象实例的run()方法
	console.log(box2.run());//kkk28运行中  打印box2对象实例的run()方法
	
	//构造函数怎么解决对象识别问题
	console.log(box1 instanceof Box);//true
	console.log(box2 instanceof Box);//true
	console.log(box3 instanceof Box);//false
	console.log(box3 instanceof Desk);//true box3是Desk对象的引用
	//普通函数调用  构造函数的时候
	console.log(Box('weisi',26));//undefined 构造函数，用普通函数调用一般是无效的，必须使用new运算符
	//使用对象冒充调用 构造函数
	var aa=new Object();
	Box.call(aa,'dudu',100);//对象冒充
	console.log(aa.run());//dudu100运行中
	
//构造函数和工厂模式对比：
不同之处：
1,构造函数没有显示的创建对象（new Object)
2,直接将属性和方法赋值给this对象
3，没有return语句，不需要return obj最后

构造函数的写法规范：
1，函数名和实例化对象名称相同 并且首字母大写
2，通过构造函数创建对象，必须使用new运算符  var box1=new Box('lee',11);

	function Box(name,age){
		this.name=name;
		this.age=age;
		this.run=function(){
			return this.name+this.age+'运行中';
		}
	}
	var box1=new Box('lee',11);
	var box2=new Box('lee',11);
	console.log(box1.name==box2.name);//true
	console.log(box1.run()==box2.run());//true  构造函数体内的方法的值是一样
	console.log(box1.run==box2.run);//false  当比较一个方法的时候，比较的是引用地址（引用类型的比较，这里重复的创建对象，即使是一样的，也是已经断开了旧的对象引用）
	
	//如果实现引用地址的一致性呢，，，实际作用不大 而且不好，只是加深了解
	function Box(name,age){
		this.name=name;
		this.age=age;
		
		this.run=run;
	}
	
	function run(){//构造函数内部的方法通过全局来实现引用地址一致
		return this.name+this.age+'运行中';
	}
	var box1=new Box('lee',11);
	var box2=new Box('lee',11);
	console.log(box1.run()==box2.run());//true
	console.log(box1.run==box2.run);//true 

prototype原型：好处是可以让所有对象实例  共享 它所包含的属性和方法
	//构造函数
	/*function Box(name,age){
		this.name=name;        //实例属性
		this.age=age;          //实例属性
		this.run=function(){   //实例方法
			return this.name+this.age+'运行中';
		}
	}*/
	//原型
	function Box(){}//构造函数体内什么都没有，如果有，叫做实例属性，实例方法
	Box.prototype.name='lee';  //原型属性
	Box.prototype.age=100;     //原型属性
	Box.prototype.run=function(){   //原型方法
		return this.name+this.age+'运行中';
	}
	
	var box1=new Box();
	var box2=new Box();
	var aa=new Object();
	console.log(box1.name);//lee
	console.log(box1.run());//lee100运行中
	console.log(box1.run()==box2.run());//true
	
	//如果是实例方法，不同的实例化，他们的方法地址是不一样的，每个实例化对象都是唯一的
	//如果是原型方法，不同的实例化，那么他们的地址是共享的，大家都是一样的
	console.log(box1.run==box2.run);//true  因为是原型写法，原型是共享的，这里的方法是相同的；对比构造函数
	
	//我们创建的每个函数都有一个prototype属性，这个属性是一个对象
	console.log(box1.prototype);//undefined  这个属性是一个对象，访问不到
	console.log(box1.__proto__);//Object {name: "lee", age: 100}这个是属性是一个指针指向prototype原型对象。IE不支持
	console.log(Box.prototype);//Object {name: "lee", age: 100}
	console.log(box1.constructor);//function Box(){}可以获取构造函数本身
	
	//判断一个对象实例 是不是 指向了 原型对象，基本上只要实例化了，是自动指向原型对象
	console.log(Box.prototype.isPrototypeOf(box1));//true
	console.log(Box.prototype.isPrototypeOf(aa));//false aa虽然实例化了，可是指向的原型对象不是Box
	console.log(Object.prototype.isPrototypeOf(aa));//true
	console.log(Object.prototype.isPrototypeOf(box1));//true

	//原型模式的执行流程 
	//1,先查找实例属性或实例方法，如果有，立刻返回
	//2，如果没有实例对象里面没有，则去原型对象里找
	function Box(){
		//this.name='kkk';   //实例属性，并不是重写原型属性
	}//构造函数体内什么都没有，如果有，叫做实例属性，实例方法
	Box.prototype.name='lee';   //原型属性
	Box.prototype.age=100;      //原型属性
	Box.prototype.run=function(){//原型方法
		return this.name+this.age+'运行中';
	}
	
	var box1=new Box();
	box1.name='kkk';   //实例属性，并不是重写原型属性
	console.log(box1.name);//kkk  得到的是实例属性的值，因为就近原则
	var box2=new Box();
	console.log(box2.name);//lee  因为是box1实例重新修改了name，它并不共享，不影响box2实例的属性，继续继承自原型
	delete box1.name; //删除box1实例中的属性
	console.log(box1.name);//lee

	//如何判断属性是在构造函数实例里，还是在原型里
	function Box(){}//构造函数体内什么都没有，如果有，叫做实例属性，实例方法
	Box.prototype.name='lee';   //原型属性
	Box.prototype.age=100;      //原型属性
	Box.prototype.run=function(){//原型方法
		return this.name+this.age+'运行中';
	}
	
	//判断实例中是否存在指定属性hasOwnProperty()
	var box1=new Box();
	console.log(box1.hasOwnProperty('name'));//false 判断box1实例是否有name属性
	
	/*box1.name='lee';
	console.log(box1.hasOwnProperty('name'));//true */
	
	//in 操作符如果返回true，只要有存在该属性，无论是在原型对象中还是在实例中
	console.log('name' in box1);//true 此时name属性是存在 box1的原型对象中
	
	//判断指定属性是否仅存在原型对象中   只有原型中有属性
	function isProperty(object,property){
		return !object.hasOwnProperty(property) && (property in object);
	}
	console.log(isProperty(box1,'name'));//说明此时name属性 在box1的原型对象中
	
	//使用字面量的方式创建 原型
	//传统构造函数方法
	function Box(){}//构造函数体内什么都没有，如果有，叫做实例属性，实例方法
	Box.prototype.name='lee';   //原型属性
	Box.prototype.age=100;      //原型属性
	Box.prototype.run=function(){//原型方法
		return this.name+this.age+'运行中';
	}
	
	var box1=new Box();
	console.log(Box.prototype);//Object {name: "lee", age: 100} 通过构造函数名可以访问到原型对象
	console.log(box1.constructor);//function Box(){}
	console.log(box1.constructor==Box);//true
	console.log(box1.constructor==Object);//false
	
	//使用字面量方式 创建 原型
	//和使用构造函数创建原型对象区别：字面量创建的原型对象，使用constructor属性不会指向实例，而是指向Object
	function Box(){};
	Box.prototype={//这里原型对象 又创建了一个新的对象
		name:'lee',
		age:100,
		run:function(){
			return this.name+this.age+'运行中';
		}
	}
	var box1=new Box();
	console.log(box1.constructor);//function Object() { [native code] }
	console.log(box1.constructor==Box);//false
	console.log(box1.constructor==Object);//true 
	
	//让box1强制指向Box 而不是一个新创建的对象
	function Box(){};
	Box.prototype={//这里原型对象 又创建了一个新的对象
		constructor:Box,//强制指向Box
		//constructor:String, //也可以强制指向string
		name:'lee',
		age:100,
		run:function(){
			return this.name+this.age+'运行中';
		}
	}
	var box1=new Box();
	console.log(box1.constructor);
	console.log(box1.constructor==Box);//true
	console.log(box1.constructor==Object);//false
	
	//重写了原型对象，会造成原来的原型对象和构造函数实例之前的关系切断
	function Box(){};
	Box.prototype={//这里原型对象 又创建了一个新的对象
		name:'lee',
		age:100,
		run:function(){
			return this.name+this.age+'运行中';
		}
	}
	//重写原型对象，并不仅仅是覆盖
	Box.prototype={//这里不会保留之前原型对象的任何信息
				//把原来的原型对象和构造函数对象实例  之前的 关系切断
		age:200
	}
	var box1=new Box();
	console.log(box1.name);//undefined

2017-02-16：

//原型的缺点 j就是它最大的优点 共享
function Box () {}
Box.prototype={
	constructor:Box,
	name:'lee',
	age:100,
	family:['哥哥','姐姐','妹妹'],
	run:function(){
		return this.name+this.age+'运行中';
	}
};
var box1=new Box();
console.log(box1.family);//["哥哥", "姐姐", "妹妹"]
box1.family.push('弟弟');
console.log(box1.family);//["哥哥", "姐姐", "妹妹", "弟弟"]
box1.name='kkk';
console.log(box1.name);//kkk

var box2=new Box();
//box2共享了box1的family，因为family数组是引用类型，保存的是指针，实际引用指向的都是原型对象
console.log(box2.family);//["哥哥", "姐姐", "妹妹", "弟弟"]

console.log(box1.run==box2.run);//true
console.log(box2.name);//lee

2017-02-17：
//组合构造函数+原型模式    是创建对象比较好的方法
function Box (name,age) {//保持独立的用构造函数
	this.name=name;
	this.age=age;
	this.family=['哥哥','姐姐','妹妹'];
}
Box.prototype={//保持共享的用原型
	constructor:Box,
	run:function(){
		return this.name+this.age+'运行中';
	}
};
var box1=new Box('lee',11);
box1.family.push('弟弟');
console.log(box1.family);//["哥哥", "姐姐", "妹妹", "弟弟"]
console.log(box1.name);//lee

var box2=new Box('kkk',100);
//family数组是引用类型没有使用原型模式，所以没有共享
console.log(box2.family);//["哥哥", "姐姐", "妹妹"]
console.log(box1.run==box2.run);//true
console.log(box2.name);//kkk

//动态原型模式 
//注意需要判断避免多次原型初始化，不可使用字面量方式重写原型，会切断实例和新原型之间的联系
function Box (name,age) {
	this.name=name;
	this.age=age;
	this.family=['哥哥','姐姐','妹妹'];
	/*alert('原型初始化开始');
	Box.prototype.run= function(){//把原型封装到构造函数里，会初始化2次
		return this.name+this.age+'运行中';
	};
	alert('原型初始化结束');*/

	if(typeof this.run!='function'){
		alert('原型初始化开始');
		Box.prototype.run= function(){//把原型封装到构造函数里，会初始化2次
			return this.name+this.age+'运行中';
		};
		alert('原型初始化结束');
	}
}
var box1=new Box('lee',11);
console.log(box1.run());

var box2=new Box('kkk',100);
console.log(box2.run());

//寄生构造函数 工程模式+构造函数
function Box (name,age) {
	var obj=new Object();
	obj.name=name;
	obj.age=age;
	obj.run=function(){
		return this.name+this.age+'运行中';
	}
	return obj;
}
var box1=new Box('lee',11);
console.log(box1.run());

var box2=new Box('kkk',100);
console.log(box2.run());

//稳妥构造函数 在构造函数体内禁止使用this，在外面实例化调用的使用禁止使用new
function Box (name,age) {
	var obj=new Object();
	obj.name=name;
	obj.age=age;
	obj.run=function(){
		return this.name+this.age+'运行中';
	}
	return obj;
}
var box1=Box('lee',11);
console.log(box1.run());

var box2=Box('kkk',100);
console.log(box2.run());


//继承 通过原型链实现
function Box(){   //被继承的函数叫做超类型（父类，基类）
	this.name='lee';
}

function Desk(){  //继承的函数叫做子类型(子类，派生类)
	this.age=100;
}

function Table(){ //孙子
	this.level='aaa';
}
//通过原型链继承，超类型实例化后的对象实例，赋值给子类型的原型属性
//new Box()会将Box构造里的信息和原型里的信息都交给Desk
//Desk的原型，得到的是Box的构造+原型里的信息
Desk.prototype=new Box();
Table.prototype=new Desk();

var box=new Box();
console.log(box.constructor);//function Box(){this.name='lee';}

var desk=new Desk();
console.log(desk.name);//lee

var table=new Table();
console.log(table.name);//lee


//继承 通过原型链实现  就近原则，实例里有就返回实例
function Box(){   //被继承的函数叫做超类型（父类，基类）
	this.name='lee';
}
Box.prototype.name='kkk';

function Desk(){  //继承的函数叫做子类型(子类，派生类)
	this.age=100;
}
//通过原型链继承，超类型实例化后的对象实例，赋值给子类型的原型属性
Desk.prototype=new Box();

var box=new Box();
var desk=new Desk();
console.log(desk.name);//lee 就近原则，实例里有就返回实例
//子类型从属于自己或者他的超类型
console.log(desk instanceof Object);//true
console.log(desk instanceof Desk);//true
console.log(box instanceof Desk);//false


//使用对象冒充继承 缺点是：只能继承构造函数里的信息，无法继承原型中的信息
function Box(name,age){   
	this.name=name;
	this.age=age;
	/*this.run=function(){//方法放在构造函数里，后面每次实例化都会分配一个内存地址，浪费空间，最好放在原型里
		return this.name+this.age+'运行中';
	}*/
}
Box.prototype.family='家庭';
Box.prototype.run=function(){//这个方法是希望 共享的，可是使用对象冒充继承，缺无法传递
	return this.name+this.age+'运行中';
}

function Desk(name,age){   
	Box.call(this,name,age);//冒充了Box对象，但是只能继承构造函数中的信息
}
var desk=new Desk('lee',100);
console.log(desk.name);//lee
console.log(desk.family);//undefined
console.log(desk.run());//报错


//组合模式继承  原型链+借用构造函数 有个缺点：超类型 会被调用两次
function Box(name,age){   
	this.name=name;
	this.age=age;
}
Box.prototype.run=function(){
	return this.name+this.age+'运行中';
}

function Desk(name,age){   
	Box.call(this,name,age);//冒充了Box对象，但是只能继承构造函数中的信息
}
Desk.prototype=new Box();//原型链继承 原型中的信息

var desk=new Desk('lee',100);
console.log(desk.run());//lee100运行中


2017-02-18:
//匿名函数 和 闭包
//匿名函数其中一种：通过自我执行来 执行的匿名函数
(function(){    //(匿名函数)();
	alert('lee');
})();

//自我执行匿名函数的传参
(function(age){
	alert(age);
})(100);

//函数里放一个匿名函数 
function box(){
	return function(){//闭包
		return 'ycc';
	}
}
var bb=box();
console.log(bb());//ycc

console.log(box);//function box(){return function(){return 'ycc';}}
console.log(box());//function(){return 'ycc';}
console.log(box()());//ycc


//闭包
//由于闭包作用域里的局部变量资源不会被立刻销毁回收，所以可能会占用更多的内存，使性能下降，建议非常有必要的时候才使用闭包，使用完成后 设置为null 
//通过闭包返回局部变量
function box(){
	var age=10;
	return function(){
		return age;
	};
}
console.log(box()());//10

//使用全局变量进行累加
var age=100;
function box(){
	age++;
}
console.log(age);//100
box();
console.log(age);//101
box();
console.log(age);//102

//使用局部变量 无法进行累加
function box1(){
	var age1=50;//因为age1每次都被初始化成50
	age1++;
	return age1;
}
//console.log(age1);//报错，访问不到内部变量age1
console.log(box1());//51
console.log(box1());//51

//使用匿名函数（闭包）实现局部变量驻留内存中，从而不断累加
function box(){
	var age=100;
	return function(){
		age++;
		return age;
	}
}
//下面这样调用是无法累加的
console.log(box()());//101
console.log(box()());//101
//应该这样调用
var b=box();
console.log(b());//101
console.log(b());//102
console.log(b());//103
console.log(b());//104
//这个b会驻留在内存中，不用的时候设置为null
b=null;//解除内存占用，等待垃圾回收
console.log(b());//报错  设置为null就不能引用


//闭包在循环数组里的用法
function box () {
	var arr=[];
	for (var i = 0; i <5; i++) {
		arr[i]=i;
	};
	return arr;
}
var b=box();
console.log(b);//[0, 1, 2, 3, 4]


function box () {
	var arr=[];
	for (var i = 0; i <5; i++) {
		arr[i]=function(){//只是匿名函数  不是闭包
			return i;
		}
	};
	//循环已经执行完毕，i最后是5
	return arr;
}

var b=box();
console.log(b.length);//5
console.log(b);//[function, function, function, function, function]
console.log(b[0]());//5
console.log(b[1]());//5
console.log(b[2]());//5

//改1
function box () {
	var arr=[];
	for (var i = 0; i <5; i++) {
		arr[i]=(function(num){//通过及时的  执行匿名函数传参i,自我执行
			return num;
		})(i);
	};
	//循环已经执行完毕，i最后是5
	return arr;
}

var b=box();
console.log(b);//[0, 1, 2, 3, 4]

//改2 利用闭包中局部变量驻留内存中
function box () {
	var arr=[];
	for (var i = 0; i <5; i++) {
		arr[i]=(function(num){//匿名函数 是闭包
			return function(){//因为闭包变量可以驻留在内存中，和前面的变量累加是一个道理
				return num;
			}
			/*return function(){  这一段就是一个闭包
				return num;
			}*/
		})(i);//这里的自我执行有赋值给变量，其实可以去掉(匿名函数)()中第一个圆括号
	};
	//循环已经执行完毕了，num为什么可以为0,1,2,3,4
	return arr;
}

var b=box();
console.log(b);//[function, function, function, function, function]
console.log(b[0]());//0
console.log(b[1]());//1
console.log(b[2]());//2 


//闭包中的this指向  因为闭包不属于这个对象的属性或者方法，闭包在运行时，this指向window的
/*var user='the window';
var box={
	user:'the box',
	getuser:function(){
		return this.user;
	}
}
console.log(this.user);//the window
console.log(box.getuser());//the box

var user='the window';
var box={
	user:'the box',
	getuser:function(){
		return function(){//这里是一个闭包
			return this.user;
		}
	}
}
console.log(this.user);//the window
console.log(box.getuser());//function(){return this.user;}
console.log(box.getuser()());//the window 闭包在运行时候，指向了window*/

//如果想让闭包中的this指向的是box
var user='the window';
var box={
	user:'the box',
	getuser:function(){
		return function(){//这里是一个闭包
			return this.user;
		}
	}
}
//方法一：对象冒充
console.log(box.getuser().call(box));//the box
//方法二：改变this作用域
var user='the window';
var box={
	user:'the box',
	getuser:function(){
		//这里作用域的this指box
		var that=this;
		return function(){//这里是一个闭包
			//这里作用域this是window，但是that是只box
			return that.user;
		}
	}
}
console.log(box.getuser()());//the box

//内存泄漏
//闭包在ie中会导致一些问题，就是内存泄漏问题，就是无法销毁驻留在内存中的元素
/*function box () {
	var oDiv=document.getElementById('oDiv');//oDiv用完之后一直驻留在内存
	oDiv.onclick=function(){
		alert(oDiv.innerHTML);//这里的oDiv导致内存泄漏
	}
	//需要手动解除引用，等待垃圾回收,但是造成点击事件无法响应了
	oDiv=null;
	alert(oDiv);//查看Odiv是否存在  存在
}
box();*/
//改1
function box () {
	var oDiv=document.getElementById('oDiv');//oDiv用完之后一直驻留在内存
	var txt=oDiv.innerHTML;
	oDiv.onclick=function(){
		alert(txt);
	}
	oDiv=null;
	alert(oDiv);//查看Odiv是否存在  不存在
}
box();

//模仿块级作用域，js是没有块级作用域的,匿名函数中私有化问题
function box(){
	for(var i=0;i<5;i++){//这里类似一个块级作用域（js里没这个东西）

	}
	var i;//就算重新声明，也不会影响之前声明初始化的数据，证明了js是没有块级作用域
	//即使后面多次声明(未初始化数据或赋值)，js也只认识 第一次声明
	alert(i);//这个块级作用域外面，仍然能访问到 5
}
box();


2017-02-19：
//模仿块级作用域（私有作用域）
//(function(){})();私有作用域的优点：可以减少闭包占用内存的问题，因为没有指向匿名函数的引用，只要函数执行完毕，就可以销毁其作用域链了
function box(){
	(function(){//包含自我执行的匿名函数，就可以实现私有作用域，网页一打开就会自动执行
		for(var i=0;i<5;i++){
			console.log(i);//0,1,2,3,4
		}
	})();	//出了 这个私有作用域，变量立即被销毁	
	alert(i);//报错
}
box();

//js中私有变量，私有函数的概念；但是属性和方法都是公有的，没有私有的概念
function Box(){
	this.age=100;         //属性，公有的
	this.run=function(){  //方法，公有的
		return '运行中';
	}
}
var box=new Box();   //可以打印出来 属性age，和方法run，说明其是公有的
console.log(box.age);//100 
console.log(box.run());//运行中

function Box(){
	var age=100;         //变量，私有的
	function run(){  //函数，私有的
		return '运行中';
	}
}
var box=new Box();//所以打印不出来
console.log(box.age);//undefined
console.log(box.run());//报错

//提供对外可以见的公共接口，特权方法

function Box(){
	var age=100;         //变量，私有的
	function run(){  //函数，私有的
		return '运行中';
	}
	this.publicGo=function(){//提供对外可以见的公共接口，特权方法
		return age+run();
	}
}
var box=new Box();//可以打印出来
console.log(box.age);//undefined
console.log(box.publicGo());//1.html:67 100运行中

//如何把一个私有变量 变成  静态共享属性
(function(){
	var user='';//私有变量
	//function Box(){};在私有作用域里写构造函数，不支持，外部var box=new Box()访问了
	Box=function(val){//省略var ，Box变成全局变量，这里匿名函数赋值给全局变量，等于构造函数
		user=val;
	}
	Box.prototype.getUser=function(){
		return user;
	}
	Box.prototype.setUser=function(val){
		user=val;
	}
})();
var box1=new Box('lee');
console.log(box1.getUser());//lee
var box2=new Box('kkk');
console.log(box1.getUser());//kkk
box2.setUser('ooo');
console.log(box1.getUser());//ooo 就是box2中设置修改了user，box1中能访问到 


//什么叫单例，就是永远只实例化一次，其实就是字面量对象声明方式
var box={   //第一次实例化了，无法第二次实例化，那么就是单例
	user:'lee';
	run:function(){
		return '运行中';
	}
}

//单例在很多 js框架中的实际应用
var box=function(){  
	var user='lee';//私有变量
	function run(){//私有函数
		return '运行中';
	}
	var obj={
		publicGo:function(){//对外公共的接口 的特权方法
			return user+run();
		}
	};
	return obj;
}();//自我执行(匿名函数)()，当有赋值的时候，可以省略第一个圆括号

console.log(box.publicGo());//lee运行中

2017-2-20:
//定时器
//超时调用 setTimeout  多少毫秒后会执行一次某段代码

//不推荐写法
setTimeout('alert(11)',2000);
//改1：
function box(){
	alert(11);
}
setTimeout(box,2000);//第一个参数，可以直接存放一个函数名，不用调用（）  
//改2  推荐写法，封装性好
setTimeout(function(){
	alert(11);
},2000);

//取消超时调用
var box=setTimeout(function(){//setTimeout有一个返回值，返回的是超时调用的id
	alert(11);
},2000);
console.log(box);//1
clearTimeout(box);//取消超时调用

//间歇调用  setInterval 每隔多少毫秒重复调用某段代码
var box=setInterval(function(){
	console.log(11);
},2000);
clearInterval(box);

//需求：要一个能设置5秒的定时器
//方法一：使用间歇调用模拟     较少使用
var num=0;
var max=5;
var box=setInterval(function(){
	num++;
	if(num==max){
		//clearInterval(this);这种写法是无效的 
		clearInterval(box);
		alert('5秒钟到了！');
	}
	console.log(num);//1,2,3,4,5,6,7…… 如果不清除 间歇调用的话，num会一直每隔1秒自增
},1000);
//方法二：使用超时调用模拟
var num=0;
var max=5;
function box(){
	num++;
	if(num==max){
		alert('5秒钟到了！');
	}else{
		setTimeout(box,1000);
	}
	console.log(num);
}
setTimeout(box,1000);

//获取url中？号后面的键值对  要运行本地服务器，先把页面中的html加上 ?id=5&search=ok
function getArgs(){

	var args=[];//最后要得到这样的格式[id:5,search:ok]
	var str=location.search.substring(1).length?0:location.search.substring(1);
	var arr=str.split('&');
	var item=null;
	var name=null;
	var value=null;

	for (var i = 0; i < arr.length; i++) {
		item=arr[i].split('=');//[id,5]
		name=item[0];
		value=item[1];
		args[name]=value;
	};
	return args;
}
console.log(getArgs()['id']);//5

//重新加载，无历史记录的打开窗口
window.location.reload(); //最有效的重新加载，但有可能是从缓存中加载
window.location.reload(true);//强制加载，从服务器源头重新加载
window.location.replace('https://www.baidu.com/');//不产生任何历史痕迹的跳转，就是没法退后

//alert(navigator.userAgent);//获取浏览器的版本，用户代理字符

2017-02-22:
DOM

2017-02-23:
//获取节点的时候，怎么过滤空白节点，保持各个浏览器统一的方法
	<div id="box">
		<p>aaa</p>
		<p>bbb</p>
		<p>ccc</p>
	</div>
	window.onload=function(){
		var box = document.getElementById('box');
		alert(filterWhiteNode(box.childNodes).length);//3个，如果不用去空白字符的方法 则会打印出7
		alert(removeWhiteNode(box.childNodes).length);//3

		//方法一：忽略空白字符
		function filterWhiteNode (nodes) {
			var ret=[];
			for(var i=0;i<nodes.length;i++){
				if(nodes[i].nodeType===3 && /^\s+$/.test(nodes[i].nodeValue)){
					continue;
				}else{
					ret.push(nodes[i]);
				}
			}
			return ret;
		}
		//方法二：移除空白字符
		function removeWhiteNode (nodes) {
			var ret=[];
			for(var i=0;i<nodes.length;i++){
				if(nodes[i].nodeType===3 && /^\s+$/.test(nodes[i].nodeValue)){
					nodes[i].parentNode.removeChild(nodes[i]);
				}
			}
			return nodes;
		}
	}

//如果使用firstChild，lastChild，previousSibling，nextSibling获取节点的过程中，怎么过滤掉空白节点

var box = document.getElementById('box');
console.log(removeWhiteNode(box).childNodes.length);//3
alert(removeWhiteNode(box).firstChild.nodeName);//p
//方法二：移除空白字符
function removeWhiteNode (obj) {
	for(var i=0;i<obj.childNodes.length;i++){
		if(obj.childNodes[i].nodeType===3 && /^\s+$/.test(obj.childNodes[i].nodeValue)){
			obj.childNodes[i].parentNode.removeChild(obj.childNodes[i]);
		}
	}
	return obj;
}


2017-02-24:
原生js中有insertBefore()方法，在某节点之前插入，但是没有在某节点之后插入的方法
//自己写一个某节点之后插入的方法insertAfter()

<body>
<div id="box">
	<p>aaa</p>
	<p>bbb</p>
	<p>ccc</p>
</div></html>

var box = document.getElementById('box');
var p= document.createElement('p');
p.innerHTML='我是插入在box后的p';
insertAfter(p,box);
function insertAfter(newEle,targerEle){
	var parent=targerEle.parentNode;
	//可以有优化性能的地方，如果这个targerEle目标元素就是最后一个元素了
	if(parent.lastChild===targerEle){
		alert(0);
		parent.appendChild(newEle);//将新节点添加到parent的子节点列表的末尾上
	}else{
	//目标元素的 下一个元素的 前面插入=== 目标元素的后面插入新节点
	parent.insertBefore(newEle,targerEle.nextSibling);
	}
}

//克隆一个节点，如果是true就是把标签内的文本也克隆，如果false，只克隆标签
<body>
<div id="box">
	<p>aaa</p>
	<p>bbb</p>
	<p>ccc</p>
</div></html>

var box = document.getElementById('box');
var clone = removeWhiteNode(box).firstChild.cloneNode(false);
box.appendChild(clone);//box末尾多了一对空白p标签

//移除空白节点
function removeWhiteNode (obj) {
	for(var i=0;i<obj.childNodes.length;i++){
		if(obj.childNodes[i].nodeType===3 && /^\s+$/.test(obj.childNodes[i].nodeValue)){
			obj.childNodes[i].parentNode.removeChild(obj.childNodes[i]);
		}
	}
	return obj;
}

2017-02-26:
得到<html>标签的元素节点方法：document.documentElement(比document.childNodes[1])更好
得到<body>标签的元素节点方法：document.body(比document.getElementsByTagName('body')[0] 更好)

获得有效子节点，可以自动过滤掉空白节点 children属性  box.children.length
获取第一个，或者最后一个有效节点box.children[0],box.children[length-1]
	
innderHtml仅适合在body标签作用域之内的，比如想插入script标签在head标签是不生效的

js的table中，只有table，tbody，th是没有自带的创建方法，其他的都有自带的创建方法

alert(box.style.cssFloat);//非IE浏览器对关键字 保留字的 获取方法前面加css
alert(box.style.styleFloat);//IE浏览器对关键字 保留字的 获取方法前面加style
alert(box.style.cssFloat||box.style.styleFloat);//跨浏览器兼容 获取

typeof box.style.cssFloat!='undefined'?box.style.cssFloat='right':box.style.styleFloat='right';//设置

//获取html中获取到计算后的样式 或者说 内联在<style></style>标签中的样式的方法或者 style行内 或者link链接
window.getComputedStyle(box,null);//谷歌 火狐  window下的方法
window.getComputedStyle(box,':hover');//谷歌 火狐 获取伪类
box.currentStyle属性 //ie浏览器中  某个对象上的属性

//兼容浏览器写法
//window.getComputedStyle(box,null) 在ie中会报错而不会返回null，报错||box.currentSt
var style1 = window.getComputedStyle?window.getComputedStyle(box,null):null || box.currentStyle;
alert(style1.fontSize);

//如何禁用样式，可以禁用内联样式，后者link链接样式，但是不能禁用行内样式
<style>
#box{color:red;font-size:40px;}
</style>
<div id="box" class="aaa bbb ccc" style="background:blue;">sdgsdgsgd</div>

var box = document.getElementById('box');
var sheet = document.styleSheets[0];
sheet.disabled = true;

//cilentWidth 和 clientHeight
//alert(typeof box.clientWidth);返回的数据类型是number，数值，不是字符串
//如果设置了box的width为其他单位，如pt，返回出来的结果还是会转换为px像素
//边框 和 外边距，不算在clientWidth的实际大小里面
//内边距padding会增加大小，而滚动条会减少实际大小，返回结果不会把滚动条的大小算进去



2017-02-27:
//怎么根据实际需求 动态加载js文件
var flag=true;
if(flag){
	loadScript('aaaa.js');
}
function loadScript(url){
	var script=document.createElement('script');
	script.type='text/javascript';
	script.src=url;
	doucument.getElementsByTagName('head')[0].appendChild(script);
}


















