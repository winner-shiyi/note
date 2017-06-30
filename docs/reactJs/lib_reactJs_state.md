## this.state

React 的一大创新，就是将组件看成是一个状态机，一开始有一个初始状态，然后用户互动，导致状态变化，从而触发重新渲染 UI 。

## 获取真实的DOM节点

组件并不是真实的 DOM 节点，而是存在于内存之中的一种数据结构，叫做虚拟 DOM （virtual DOM）。只有当它插入文档以后，才会变成真实的 DOM 。根据 React 的设计，所有的 DOM 变动，都先在虚拟 DOM 上发生，然后再将实际发生变动的部分，反映在真实 DOM上，这种算法叫做 DOM diff ，它可以极大提高网页的性能表现。
```javascript
var MyComponent = React.createClass({
  fn(){
    this.refs.text.focus()
  },
  render(){
    return(
      <div>
        <input type="text" ref="text"/>
        <input type="button" value="点击focus" onClick={this.fn} />
        // 这里不用bind(this)
      </div>
    )
  }
})

ReactDOM.render(
  <MyComponent />,
  document.getElementById('example')
);
```

**注意点**

由于` this.refs.[refName] `属性获取的是真实 DOM ，所以必须等到虚拟 DOM 插入文档以后，才能使用这个属性，否则会报错。上面代码中，通过为组件指定 Click 事件的回调函数，确保了只有等到真实 DOM 发生 Click 事件之后，才会读取 this.refs.[refName] 属性。