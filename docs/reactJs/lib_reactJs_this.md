## React 中绑定this


React可以使用React.createClass、ES6 classes、纯函数3种方式构建组件。使用React.createClass会自动绑定每个方法的this到当前组件，但使用ES6 classes或纯函数时，就要靠手动绑定this了。举列说明React中三种绑定this的方法：

### bind()

Function.prototype.bind(thisArg [, arg1 [, arg2, …]]) 是ES5新增的函数扩展方法，bind()返回一个新的函数，该函数的this被绑定到thisArg上，并向事件处理器中传入参数。当这个新函数被调用时，它的this值是传递给bind()的第一个参数,跟在this（或其他对象）后面的参数，之后它们会被插入到目标函数的参数列表的开始位置。
```javascript
class Test extends React.Component {
    constructor (props) {
        super(props)
        this.state = {message: 'hello!'}
    }

    handleClick (name, e) {
        alert(this.state.message + name)
    }

    render () {
        return (
            <div>
                <button onClick={ this.handleClick.bind(this, '赵四') }>Say Hello</button>
            </div>
        )
    }
}

ReactDOM.render(
  <Test />,
  document.getElementById('example')
);
```

#### 1、使用React.createClass会自动绑定每个方法的this到当前组件
```javascript
var LikeButton = React.createClass({
  getInitialState(){
    return {liked:false}
  },
  handleClick(){
    this.setState({liked:!this.state.liked})
  },
  render(){
    var text = this.state.liked? 'liked':'haven\'t liked'
    return (
      <p onClick={this.handleClick}>You {text} this. Click to toggle.</p>
    )
  }
})

ReactDOM.render(
  <LikeButton />,
  document.getElementById('example')
);
```

#### 2、构造函数内绑定
在构造函数 constructor 内绑定this，好处是仅需要绑定一次，避免每次渲染时都要重新绑定，函数在别处复用时也无需再次绑定

```javascript
class LikeButton extends React.Component{
  constructor(...args){
    super(...args)
    this.state = {liked:false}
    this.handleClick = this.handleClick.bind(this) //这里绑定
  }
  handleClick(){
    this.setState({liked:!this.state.liked})
  }
  
  render(){
    var text = this.state.liked? 'liked':'haven\'t liked'
    return (
      <p onClick={this.handleClick}>You {text} this. Click to toggle.</p>
    )
  }
}

ReactDOM.render(
  <LikeButton />,
  document.getElementById('example')
);
```

#### 3、箭头函数

箭头函数则会捕获其所在上下文的this值，作为自己的this值，使用箭头函数就不用担心函数内的this不是指向组件内部了。
```javascript
class LikeButton extends React.Component{
  constructor(...args){
    super(...args)
    this.state = {liked:false}
    this.handleClick = (e) =>{// ES6支持的写法
      this.setState({liked:!this.state.liked})
    }
  }
  //下面这种在Classes中直接赋值是ES7的写法，ES6并不支持
  // handleClick = (e) => {
  //   this.setState({liked:!this.state.liked})
  // }
  
  render(){
    var text = this.state.liked? 'liked':'haven\'t liked'
    return (
      <p onClick={this.handleClick}>You {text} this. Click to toggle.</p>
    )
  }
}

ReactDOM.render(
  <LikeButton />,
  document.getElementById('example')
);
```



