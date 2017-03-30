# 渲染一个 Route 组件

从本质上来讲, React Router 是一个组件.

```js
render(<Router/>, document.getElementById('app'))
```

但在此之前，我们要做一些简单的配置。

打开 `index.js` 并且

1. 引入 `Router`, `Route`, 和 `hashHistory` 模块
2. 渲染一个 `Router` 组件来替代之前的 `App` 组件

```js
// ...
import { Router, Route, hashHistory } from 'react-router'

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}/>
  </Router>
), document.getElementById('app'))
```

确保你本地的服务器一直是运行着的 `npm start` 并访问
[http://localhost:8080](http://localhost:8080)

你应该会看到与之前一样的屏幕，但这一次你会看到一些其他的东西在你的URL地址栏里。We're using `hashHistory`--it manages the routing history
with the hash portion of the url. It's got that extra junk to shim some
behavior the browser has natively when using real urls.  We'll change
this to use real urls later and lose the junk, but for now, this works
great because it doesn't require any server-side configuration.

## 添加更多的页面

创建两个新的组件，如下：

- `modules/About.js`
- `modules/Repos.js`

```js
// modules/About.js
import React from 'react'

export default React.createClass({
  render() {
    return <div>About</div>
  }
})
```

```js
// modules/Repos.js
import React from 'react'

export default React.createClass({
  render() {
    return <div>Repos</div>
  }
})
```

Now we can couple them to the app at their respective paths.

```js
// insert into index.js
import About from './modules/About'
import Repos from './modules/Repos'

render((
  <Router history={hashHistory}>
    <Route path="/" component={App}/>
    {/* add the routes here */}
    <Route path="/repos" component={Repos}/>
    <Route path="/about" component={About}/>
  </Router>
), document.getElementById('app'))
```

现在，再查看一下 [http://localhost:8080/#/about](http://localhost:8080/#/about) 和
[http://localhost:8080/#/repos](http://localhost:8080/#/repos) 页面

---

[接下来: Navigating With Link](../03-navigating-with-link/)
