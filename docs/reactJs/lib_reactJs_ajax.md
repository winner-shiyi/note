## ajax

组件的数据来源，通常是通过 Ajax 请求从服务器获取，可以使用 componentDidMount 方法设置 Ajax 请求，等到请求成功，再用 this.setState 方法重新渲染 UI。


```javascript
var RepoList = React.createClass({
  getInitialState(){
    return {loading:true,error:null,data:null}
  },
  //通常在这里拿到接口返回的数据
  componentDidMount(){
  // promise then基本用法 改写成箭头函数
  // promise.then(function(value){
  //   //success
  // },function(error){
  //   //failure
  // })
    this.props.promise.then(
      value =>this.setState({data:value,loading:false}),
      error =>this.setState({data:error,loading:false})
    )
  },
  render(){
    if(this.state.loading){
      return <span>loading……</span>
    }else if(this.state.error!==null){
      return <span>error:{this.state.error}</span>
    }else{
      var repos = this.state.data.items;
      var repoList = repos.map((repo,index) => {
        return (
          <li key={index}>
            <a href={repo.html_url}>{repo.name}</a>({repo.stargazers_count}stars)
            <br/>
            {repo.description}
          </li>
        )
      })

      return (
        <main>
          <h1>Most Popular JavaScript Projects in Github</h1>
          <ol>{repoList}</ol>
        </main>
      )
    }
    
  }
});

ReactDOM.render(
  <RepoList promise={$.getJSON('https://api.github.com/search/repositories?q=javascript&sort=stars')} />,
  document.getElementById('example')
);
```

上面的例子，从Github的API抓取数据，然后将Promise对象作为属性，传给RepoList组件。
如果Promise对象正在抓取数据（pending状态），组件显示"正在加载"；如果Promise对象报错（rejected状态），组件显示报错信息；如果Promise对象抓取数据成功（fulfilled状态），组件显示获取的数据。


