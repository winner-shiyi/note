## 生命周期

React组件的生命周期分成三个状态：

```javascript
1. Mounting：正在挂接虚拟DOM到真实DOM

2. Updating：正在被重新渲染

3. Unmounting：正在将虚拟DOM移出真实DOM
```

React 为每个状态都提供了两种处理函数，will 函数在进入状态之前调用，did 函数在进入状态之后调用，三种状态共计五种处理函数。

```javascript
1. componentWillMount()

2. componentDidMount() //进行state数据的填充，ajax请求，集成jquery 

3. componentWillUpdate()

4. componentDidUpdate()

5. componentWillUnmount() //执行清理，比如无效的定时器，清除在DidMount中创建的DOM元素
```

此外，React 还提供两种特殊状态的处理函数:

```javascript
1. componentWillReceiveProps()：已加载组件收到新的参数时调用

2. shouldComponentUpdate()：组件判断是否重新渲染时调用
```

下面来看一个实例：
```javascript
var Hello = React.createClass({
    getInitialState(){
      return {opacity:1}
    },
    componentDidMount(){
      setInterval(()=>{
        var opacity = this.state.opacity;
        opacity-=0.05;
        if(opacity<0.1){
          opacity = 1;
        }
        this.setState({
          opacity:opacity
        })
      },100)
    },
    render(){
      return (
        <p style={{opacity:this.state.opacity}}>hello {this.props.name}</p>
      )
    }
});

ReactDOM.render(
<Hello name="world"/>,
document.getElementById('example')
);
```
在hello组件加载以后，通过 componentDidMount 方法设置一个定时器，每隔100毫秒，就重新设置组件的透明度，从而引发重新渲染。
另外，组件的style属性的设置方式也值得注意，不能写成：
```javascript
style="opacity:{this.state.opacity};"
```
因为 React 组件样式是一个对象，所以第一重大括号表示这是 JavaScript 语法，第二重大括号表示样式对象。而要写成：
```javascript
style={{opacity: this.state.opacity}}
```

更多具体用法参考[官方文档](https://facebook.github.io/react/docs/react-component.html)。


