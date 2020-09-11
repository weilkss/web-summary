# web 前端面试题

想进大厂？首先基础得扎实，技术面试得过，你才能有机会和 hr 小姐姐谈工资

## node 篇

### 1. 什么是错误优先的回调函数？

错误优先的回调函数用于传递错误和数据。第一个参数始终应该是一个错误对象， 用于检查程序是否发生了错误。其余的参数用于传递数据。

```js
fs.readFile(filePath, function (err, data) {
  if (err) {
    //handle the error
  }
  // use the data object
});
```

### 2. 如何避免回调地狱

- 模块化：将回调函数分割为独立的函数
- 使用 Promises
- 使用 yield
- 来计算生成器或 Promise

### 3. 如何用 Node 监听 80 端口

好像不太推荐监听 80 端口，如果非要监听的话就`反向代理`来实现

### 4. 什么是事件循环？

node 能实现高并发的诀窍就在于事件循环机制

node 是单线程的机制，将耗时阻塞的 I/O 操作交给线程池中的某个线程去完成，主线程本身只负责不断地调度，并没有执行真正的 I/O 操作，也就是说 node 实现的是异步非阻塞式

node 每次事件循环机制都包含了 6 个阶段：

**timers 阶段：** 这个阶段执行已经到期的 timer(setTimeout、setInterval)回调

**I/O callbacks 阶段：** 执行 I/O（例如文件、网络）的回调

**idle, prepare 阶段：** node 内部使用

**poll 阶段：** 获取新的 I/O 事件, 适当的条件下 node 将阻塞在这里

**check 阶段：** 执行 setImmediate 回调

**close callbacks 阶段：** 执行 close 事件回调，比如 TCP 断开连接

### 5. 哪些工具可以用来保证一致性的代码风格

- JSLint
- JSHint
- ESLint
- JSCS - 推荐

### 6. 使用 NPM 有哪些好处？

通过 NPM，你可以安装和管理项目的依赖，并且能够指明依赖项的具体版本号。 对于 Node 应用开发而言，你可以通过 package.json 文件来管理项目信息，配置脚本， 以及指明项目依赖的具体版本

### 7. npm、cnpm、yarn 的区别

**npm：** 基于 node.js 的包管理工具;
**cnpm：** 跟 npm 是一样的,这是淘宝出的下载工具,服务器在国内,所以下载速度比 npm 快很多，但是安装有点乱，并且容易出错
**yarn：** Yarn 是为了弥补 npm 的一些缺陷而出现的，比 npm 更块，并行下载依赖，从本地获取

### 7. 什么是测试金字塔？

> 当我们在编写测试用例时，底层的单元测试应该远比上层的端到端测试要多

- 有很多针对模型的底层单元测试
- 但你需要测试模型间如何交互时，需要减少集成测试

### 8. 说出几个 node 框架？

- koa
- express

### 9. 什么是 nodejs？

nodejs 是服务端的一门技术，它是基于 Google js v8 引擎而开发的，用来开发可扩展的服务端程序。nodejs 让我们的编程工作变得简单

### 10. nodejs 有那些特点？

- 单线程
- 很高的扩展性
- 使用 js 作为编程语言，对前端开发者友好
- 使用的异步处理机制和事件驱动

## 更多面试题

- [常见 css 的面试题](./css.md)
- [常见 html 的面试题](./html.md)
- [常见 javascript 的面试题](./javascript.md)
- [常见 typescript 的面试题](./typescript.md)
- [常见 vue 的面试题](./vue.md)
- [常见 react 的面试题](./react.md)
- [常见 webpack 的面试题](./webpack.md)
- [前端工程化](./eng.md)
- [优化相关](./optimize.md)