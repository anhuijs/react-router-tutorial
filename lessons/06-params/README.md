# URL 参数

考虑一下URLs：

```
/repos/reactjs/react-router
/repos/facebook/react
```

这些URL将与以下路由路径匹配：

```
/repos/:userName/:repoName
```

以`:`开始的部分是是URL参数，其值将被解析并可用于路由组件在
`this.props.params[name]`.

## 使用参数添加路由

我们来教我们的应用程序如何渲染 `/repos/:userName/:repoName`.

首先，我们需要一个在路由上渲染的组件，在`modules/Repo.js`上创建一个新文件，如下所示：


```js

	// modules/Repo.js
	import React from 'react'
	
	export default React.createClass({
	  render() {
	    return (
	      <div>
	        <h2>{this.props.params.repoName}</h2>
	      </div>
	    )
	  }
	})

```

现在打开`index.js`并添加新路由

```js

	// ...
	// import Repo
	import Repo from './modules/Repo'
	
	render((
	  <Router history={hashHistory}>
	    <Route path="/" component={App}>
	      <Route path="/repos" component={Repos}/>
	      {/* add the new route */}
	      <Route path="/repos/:userName/:repoName" component={Repo}/>
	      <Route path="/about" component={About}/>
	    </Route>
	  </Router>
	), document.getElementById('app'))

```

现在我们可以在`Repos.js`中添加一些这个新路由的链接。

```js

	// Repos.js
	import { Link } from 'react-router'
	// ...
	export default React.createClass({
	  render() {
	    return (
	      <div>
	        <h2>Repos</h2>
	
	        {/* add some links */}
	        <ul>
	          <li><Link to="/repos/reactjs/react-router">React Router</Link></li>
	          <li><Link to="/repos/facebook/react">React</Link></li>
	        </ul>
	
	      </div>
	    )
	  }
	})

```

现在去测试你的链接。 请注意路由中的参数名称
`path`成为组件中的属性名称。 
`repoName`和
`userName`在您的组件的`this.props.params`上可用。
你应该可以添加一些道具类型，以帮助别人和自己。

---

[接下来: More Nesting](../07-more-nesting/)
