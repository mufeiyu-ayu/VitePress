# Node


## 1.常用包

-  [commander](https://github.com/tj/commander.js/blob/970ecae402b253de691e6a9066fea22f38fe7431/Readme_zh-CN.md) 一款高度自定义命令行界面的 Node.js 模块。
- [inquirer](https://github.com/SBoudrias/Inquirer.js) 常见交互式命令行用户界面的集合
- [ora](https://github.com/sindresorhus/ora) 命令行加载指示器
- [chalk](https://github.com/chalk/chalk) 命令行颜色
- [execa](https://github.com/sindresorhus/execa) 命令行执行
- [log-symbols](https://github.com/sindresorhus/log-symbols) 命令行符号


## 2.常用命令
```bash
npm config list # 查看 npm 配置
npm ls  # 查看可执行依赖(-g全局)

```

## 3.全局变量
```js
global.name='child'
console.log(global.name) // child
globalThis.name = 'ayu' // 根据环境自动判断，浏览器为 window，node 为 global
console.log(globalThis.name) // ayu
console.log(window.name) // ayu (浏览器环境下 globalthis 定义的变量可通过 window 访问

// __dirname
console.log(__dirname) // /Users/UserName/ayu/node/learn-commander/src/global-api dirname 获取当前目录的绝对路径

//__filename
console.log(__filename) // /Users/UserName/ayu/node/learn-commander/src/global-api filename 获取当前文件的绝对路径

//Buffer,process,require,
```

## 4.CSR,SSR

*CSR**
CSR指的是客户端渲染，即浏览器端，浏览器会向服务器发送请求，服务器返回数据后，浏览器渲染页面。 
**SSR**
SSR指的是服务器端渲染，即服务器端，服务器会向浏览器发送请求，浏览器返回数据后，服务器渲染页面。

**CSR与 SSR的区别**

页面加载方式：

1. 页面加载方式：
 - CSR：在 CSR 中，服务器返回一个初始的 HTML 页面，然后浏览器下载并执行 JavaScript 文件，JavaScript 负责动态生成并更新页面内容。这意味着初始页面加载时，内容较少，页面结构和样式可能存在一定的延迟。
 - SSR：在 SSR 中，服务器在返回给浏览器之前，会预先在服务器端生成完整的 HTML 页面，包含了初始的页面内容。浏览器接收到的是已经渲染好的 HTML 页面，因此初始加载的速度较快。

2. 内容生成和渲染：

 - CSR：在 CSR 中，页面的内容生成和渲染是由客户端的 JavaScript 脚本负责的。当数据变化时，JavaScript 会重新生成并更新 DOM，从而实现内容的动态变化。这种方式使得前端开发更加灵活，可以创建复杂的交互和动画效果。
 - SSR：在 SSR 中，服务器在渲染页面时会执行应用程序的代码，并生成最终的 HTML 页面。这意味着页面的初始内容是由服务器生成的，对于一些静态或少变的内容，可以提供更好的首次加载性能。

3. 用户交互和体验：

 - CSR：在 CSR 中，一旦初始页面加载完成，后续的用户交互通常是通过 AJAX 或 WebSocket 与服务器进行数据交互，然后通过 JavaScript 更新页面内容。这种方式可以提供更快的页面切换和响应速度，但对于搜索引擎爬虫和 SEO（搜索引擎优化）来说，可能需要一些额外的处理。
 - SSR：在 SSR 中，由于页面的初始内容是由服务器生成的，因此用户交互可以直接在服务器上执行，然后服务器返回更新后的页面。这样可以提供更好的首次加载性能和对搜索引擎友好的内容。

**SEO（Search Engine Optimization，搜索引擎优化）**
CSR应用对SEO并不是很友好,因为在首次加载获取HTML信息较少，搜索引擎爬虫可能无法获取完整的页面内容，而SSR就不一样了 由于 SSR 在服务器端预先生成完整的 HTML 页面，搜索引擎爬虫可以直接获取到完整的页面内容。这有助于搜索引擎正确理解和评估页面的内容<br/>

CSR 应用例如 ToB 后台管理系统 大屏可视化 都可以采用CSR渲染不需要很高的SEO支持

SSR 应用例如 内容密集型应用大部分是ToC 新闻网站 ，博客网站，电子商务，门户网站需要更高的SEO支持


## 5.path
path 是 Node.js 中用于处理文件和目录路径的模块。 

### 1.path.dirname(path)

**path.dirname()方法返回path的目录名**
```js
 console.log(path.dirname('/Users/UserName/ayu/node/learn-commander/src/global-api/index.js')) // /Users/UserName/ayu/node/learn-commander/src/global-api
 ```

### 2.path.extname(path)

**path.extname()方法返回path的扩展名,若有多个点则返回最后的带点的后缀**
```js
console.log(path.extname('/Users/UserName/ayu/node/learn-commander/src/global-api/index.js')) // .js
```

### 3.path.join([...paths])
**path.join()方法使用平台特定的分隔符作为分隔符将所有给定的path段连接在一起，然后规范化结果路径**
```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// Returns: '/foo/bar/baz/asdf'

path.join('/foo','/cxk','/ikun')
// /foo/cxk/ikun

path.join('foo', {}, 'bar');2
// Throws 'TypeError: Path must be a string. Received {}'
```


### path.resolve([...paths])
**path.resolve()方法将一个或多个路径或路径片段解析为绝对路径,如果没有传递path段， path.resolve()将返回当前工作目录的绝对路径。**
```js
path.resolve('/foo', 'bar', 'baz/asdf', 'quux', '..');
// Returns: '/foo/bar/baz/asdf'


path.resolve('/foo/bar', './baz');
// Returns: '/foo/bar/baz'

// 如果传递多个绝对路径，path.resolve()会返回最后一个路径的绝对路径
path.resolve('/foo/bar', '/tmp/file/');
// Returns: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// If the current working directory is /home/myself/node,
// this returns '/home/myself/node/wwwroot/static_files/gif/image.gif'
```
