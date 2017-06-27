## props

this.props 对象的属性与组件的属性一一对应，但是有一个例外，就是 this.props.children 属性。它表示组件的所有子节点。
```javascript
var NotesList = React.createClass({
  render(){
    return(
      <ol>{
          React.Children.map(this.props.children,function(child,index){
            return <li key={index}>{child}</li>
          })
        }
      </ol>
    ) 
  }
});

ReactDOM.render(
<NotesList>
  <span>hello</span>
  <span>world</span>
</NotesList>,
document.getElementById('example')
);
```
**注意点**

this.props.children 的值有三种可能：

1、如果当前组件没有子节点，它就是 undefined;

2、如果有一个子节点，数据类型是 object ；

3、如果有多个子节点，数据类型就是 array 。

所以，处理 this.props.children 的时候要小心。
React 提供一个工具方法 React.Children 来处理 this.props.children 。我们可以用 React.Children.map 来遍历子节点，而不用担心 this.props.children 的数据类型是 undefined 还是 object。更多的 React.Children 的方法，请参考[官方文档](https://facebook.github.io/react/docs/react-api.html)。

## PropTypes

组件的属性可以接受任意值，字符串、对象、函数等。有时，我们需要一种机制，验证别人使用组件时，提供的参数是否符合要求。组件类的PropTypes属性，就是用来验证组件实例的属性是否符合要求。
```javascript
var data = 123;

var MyTitle = React.createClass({
propTypes: {
  title: React.PropTypes.string.isRequired,
},

render: function() {
  return <h1> {this.props.title} </h1>;
}
});

ReactDOM.render(
<MyTitle />,
document.getElementById('example')
);
//输出123，但是控制台有报错
```
上面的Mytitle组件有一个title属性。PropTypes 告诉 React，这个 title 属性是必须的，而且它的值必须是字符串。现在，我们设置 title 属性的值是一个数值，就会不通过验证，控制台会报错。

此外，getDefaultProps 方法可以用来设置组件属性的默认值。
```javascript
var MyTitle = React.createClass({

getDefaultProps(){
  return {
    title:'hello react'
  }
},

render(){
  return <h1>{this.props.title}</h1>
}
})

ReactDOM.render(
<MyTitle />,
document.getElementById('example')
);
// hello react
```