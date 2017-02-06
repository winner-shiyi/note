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



数组对象：




















