# React基础知识

## HTML模板

```html
<!DOCTYPE html>
<html>
  <head>
    <script src="../build/react.js"></script>
    <script src="../build/react-dom.js"></script>
    <script src="../build/browser.min.js"></script>
  </head>
  <body>
    <div id="app"></div>
    <script type="text/babel">
      // do something
    </script>
  </body>
</html>

```
**注意点：**

1、&lt;script&gt;标签的type属性为 `text/babel`，因为这是React独有的JSX语法，凡是使用JSX的地方，都有加上`type="text/babel"`。

2、react.js 是 React 的核心库，react-dom.js 是提供与 DOM 相关的功能，Browser.js 的作用是将 JSX 语法转为 JavaScript 语法，它们三个必须先加载。
## ReactDOM.render()

ReactDOM.render 是React中用于将模板渲染为HTML语言，并插入到指定的DOM节点中。

示例：将一个h1标题插入到app节点中

```javascript
ReactDOM.render(
    <h1>hello,world!></h1>,
    document.getElementById('app')
);

```
**注意点：**

1、这里的目标节点应该是单一的DOM节点，但不应是body，虽然这样也能运行。如果确实要在body中渲染，可以动态的添加一个div子标签，如：
```javascript
ReactDOM.render(
    <HelloMessage name="John" />,
    doucument.body.appendChild(document.createElement('div'));
);
```
2、React中自定义的组件名首字母要大写，在JSX中出现的HTML标签名统一小写

3、声明在JSX中的标签属性中的class必须用`className`代替，&lt;label&gt;标签的属性for必须用`htmlFor`代替。因为class和for是js最新语法中的保留字，避免编译器误解。
```html
<div className="aaa"...>

<label htmlFor="app"...>
```
4、行内样式

```javascript
ReactDOM.render(
    <div style={{
      color:'white',
      backgroundImage:'url('+imgUrl+')',
      WebkitTransition:'all',
      msTransition:'all'//浏览器前缀除ms小写之外，其他的前缀首字母要大写
    }}></div>,
    document.getElementById('app')
)
```
5、HTML转义

有时需要处理含有标签的富文本数据，React会默认进行HTML转义，以避免XSS攻击，如果不需要转义，则可以使用dangerouslySetInnerHTML属性，如下：
```javascript
var cont = '<span>文本内容</span>';

ReactDOM.render(
  // <div>{cont}</div>, 会直接连着标签一起输出
  <div dangerouslySetInnerHTML={{__html:cont}}></div>,
  document.getElementById('example')
)  
```
第一种页面中会直接输出带标签的：<span>文本内容</span>
第二种页面中输出：文本内容

## JSX语法

JSX基本语法规则：遇到 HTML 标签（以 `&lt;` 开头），就用 HTML 规则解析；遇到代码块（以 `{` 开头），就用 JavaScript 规则解析。

使用JSX语法的代码：
```html
var app = <helloComp color="blue"/>
```

等价的原生JavaScript的代码：

```javascript
var app = React.createElement(helloComp,{color:"blue"})
```
**注意点：**
JSX中的表达式用{}，大括号里面要求是有返回值的表达式，不能使用if语句，for语句等，可以使用三元或者二元运算符来操作表达式。

```html
<div>hello {this.props.name? this.props.name:"world"}</div>

<div>hello {this.props.name || "world"}</div>
```
如果上述方法不能满足要求，在JSX标签外使用if语句来决定渲染哪一个组件，如：
```javascript
var loginBtn;

if(login){
  loginBtn = <logoutBtn />
}else{
  loginBtn = <loginBtn />
}

return (
    <div><home />{loginBtn}</div>
)
```
JSX也允许直接在模板中插入变量，如果这个变量是一个数组，则会展开这个数组的所有成员：

```javascript
var arr = [
  <h1 key="1">Hello world!</h1>,
  <h2 key="2">React is beautify</h2>,
];

ReactDOM.render(
  <div>{arr}</div>,
  document.getElementById('app')
);
```
JSX展开属性

在React的设定中，初始化props后，props是不可变的。当后续需要增加组件的属性时，定义一个展开属性对象，通过{...extendProps}的方式引入，React会自动将extendProps中的属性复制到组件的props属性中。备注：与ES6的...作为解构赋值中剩余属性的标识，这两者没有直接关系。

```javascript
var Comp = <Component foo={x} bar={y} />
Comp.props.foo = x; //错误写法
Comp.props.bar = y; //错误写法

//给组件增加属性正确写法

var extendProps = {
    foo:1,
    bar:2
}
var Comp = <h1 {...extendProps} title="jiayou"/>;
```







