## 组件

React.createClass 方法就用于生成一个组件类。

```javascript
var HelloMessage = React.createClass({
  render: function() {
    return <h1>Hello {this.props.name}</h1>;
  }
});

ReactDOM.render(
  <HelloMessage name="John" />,
  document.getElementById('example')
);
// hello John
```

模板插入 &lt;HelloMessage /&gt; 时，会自动生成 HelloMessage 的一个实例。所有组件类都必须有自己的 render 方法，用于渲染输出组件。

组件的用法与原生的 HTML 标签完全一致，可以任意加入属性，比如 &lt;HelloMessage name="John"&gt; ，就是 HelloMessage 组件加入一个 name 属性，值为 John。

组件的属性可以在组件类的 this.props 对象上获取，比如 name 属性就可以通过 this.props.name 读取。

**注意点**

1、组件类的第一个字母必须大写，否则会报错，比如HelloMessage不能写成helloMessage。

2、另外，组件类只能包含一个顶层标签，否则也会报错。

3、添加组件属性，有一个地方需要注意，就是 class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。















