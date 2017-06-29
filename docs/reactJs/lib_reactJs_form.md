## 表单

用户在表单填入的内容，属于用户跟组件的互动，所以不能用 this.props 读取。

```javascript
var Input = React.createClass({
    getInitialState(){
      return {value:'hello'}
    },
    handleChange(e){
      this.setState({
        value:e.target.value
      })
    },
    render(){
      var val = this.state.value;
      return <div>
        <input type="text" onChange={this.handleChange} value={val} />
        <p>{val}</p>
      </div>
    }
})

ReactDOM.render(<Input/>, document.getElementById('example'));
```
文本输入框的值，不能用 this.props.value 读取，而要定义一个 onChange 事件的回调函数，通过 event.target.value 读取用户输入的值。textarea 元素、select元素、radio元素都属于这种情况，更多介绍请参考[官方文档](https://facebook.github.io/react/docs/forms.html)。