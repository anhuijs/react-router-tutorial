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

Oh yeah, the catch. Click on a link and then refresh your browser. What
happens?

```
Cannot GET /repos
```

## Configuring Your Server

Your server needs to deliver your app no matter what URL comes in,
because your app, in the browser, is manipulating the URL. Our current
server doesn't know how to handle the URL.

The Webpack Dev Server has an option to enable this. Open up
`package.json` and add `--history-api-fallback`.

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

Stop your server if it's running, then `npm start` again. Look at those
clean URLs :)

---

[Next: Production-ish Server](../11-productionish-server/)
