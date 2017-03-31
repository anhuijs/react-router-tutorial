# 使用 Browser History 来简化 URL 地址

现在，我们在程序的 URL 地址中使用了一项黑科技：hash。因为它的出色表现，所以成为了默认配置，但其实还有更好的选择。

现代浏览器允许 JavaScript 在不发起 http 请求的情况下操作 URL 地址，所以我们并不是非要依赖 URL 的 hash (`#`)  部分来进行路由控制，但这里有个陷阱（稍后我们会讲到）。

## 配置 Browser History

打开 `index.js` 文件，并且引入 `browserHistory` 模块替代之前的 `hashHistory` 模块。

```js
// index.js
// ...
// bring in `browserHistory` instead of `hashHistory`
import { Router, Route, browserHistory, IndexRoute } from 'react-router'

render((
  <Router history={browserHistory}>
    {/* ... */}
  </Router>
), document.getElementById('app'))
```

现在，浏览一下新的页面，来欣赏一下简洁的 URL 地址。

好了，接下来就发现陷阱了，点击一个连接，并刷新浏览器，看看会发生什么？

```
Cannot GET /repos
```

## 配置你的服务器

你的服务器需要做到无论是什么样的 URL 地址来请求，都返回你的程序页面，因为你在浏览器中的程序正在操作 URL 地址。我们现在的服务器不知道该如何处理这些 URL。

Webpack Dev Server 服务器正好有一项这个功能选项。打开
`package.json` 文件，并添加一句 `--history-api-fallback` 代码。

```json
    "start": "webpack-dev-server --inline --content-base . --history-api-fallback"
```

We also need to change our relative paths to absolute paths in
`index.html` since the URLs will be at deep paths and the app, if it
starts at a deep path, won't be able to find the files.

```html
<!-- index.html -->
<!-- index.css -> /index.css -->
<link rel="stylesheet" href="/index.css">

<!-- bundle.js -> /bundle.js -->
<script src="/bundle.js"></script>
```

重启服务器, 并再次运行 `npm start` 。好好欣赏一下这些简洁的 URL 地址吧！ :)

---

[接下来: Production-ish Server](../11-productionish-server/)
