# web 前端面试题

想进大厂？首先基础得扎实，技术面试得过，你才能有机会和 hr 小姐姐谈工资

## html 篇

### 1. DOCTYPE 有什么作用？标准模式与混杂模式如何区分？它们有何意义?

告诉浏览器使用哪个版本的 HTML 规范来渲染文档。DOCTYPE 不存在或形式不正确会导致 HTML 文档以混杂模式呈现。

标准模式（Standards mode）以浏览器支持的最高标准运行；混杂模式（Quirks mode）中页面是一种比较宽松的向后兼容的方式显示。

- HTML5 不基于 SGML，因此不需要对 DTD 进行引用，但是需要 DOCTYPE 来规范浏览器的行为（让浏览器按照他们应该的方式来运行）
- HTML4.01 基于 SGML，所以需要对 DTD 进行引用，才能告知浏览器文档所使用的文档类型

### 2. HTML5 为什么只需要写 <!DOCTYPE HTML>

HTML5 不基于 SGML（Standard Generalized Markup Language 标准通用标记语言），因此不需要对 DTD（DTD 文档类型定义）进行引用，但是需要 DOCTYPE 来规范浏览器行为。

HTML4.01 基于 SGML，所以需要引用 DTD

### 3. 行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？

**行内元素：** a i span img input select label button textarea

**块级元素：** div ul ol li dl dt dd h1 ～ h6 p table

**空元素：** br hr link meta

### 4. 页面导入样式时，使用 link 和@import 有什么区别？

- link 是 xhtml 标签，除了加载 css 外，还可以定义 RSS 等其他事务；@import 属于 CSS 范畴，只能加载 CSS
- link 引用 CSS 时候，页面载入时同时加载；@import 需要在页面完全加载以后加载，而且@import 被引用的 CSS 会等到引用它的 CSS 文件被加载完才加载
- link 是 xhtml 标签，无兼容问题；@import 是在 css2.1 提出来的，低版本的浏览器不支持
- link 支持使用 javascript 控制去改变样式，而@import 不支持
- link 方式的样式的权重高于@import 的权重
- import 在 html 使用时候需要 `<style type="text/css">` 标签

### 5. 无样式内容闪烁（FOUC）Flash of Unstyle Content

@import 导入 CSS 文件会等到文档加载完后再加载 CSS 样式表。因此，在页面 DOM 加载完成到 CSS 导入完成之间会有一段时间页面上的内容是没有样式的。

**解决方法：** 使用 link 标签加载 CSS 样式文件。因为 link 是顺序加载的，这样页面会等到 CSS 下载完之后再下载 HTML 文件，这样先布局好，就不会出现 FOUC 问题。

### 6. 介绍一下你对浏览器内核的理解？

主要分成两部分：渲染引擎(Layout Engine 或 Rendering Engine)和 JS 引擎。

**渲染引擎：** 负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入 CSS 等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。

**JS 引擎：** 解析和执行 javascript 来实现网页的动态效果。

最开始渲染引擎和 JS 引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎。

### 7. 常见的浏览器内核有哪些？

- Trident( MSHTML )：IE MaxThon TT The World 360 搜狗浏览器
- Geckos：Netscape6 及以上版本 FireFox Mozilla Suite/SeaMonkey
- Presto：Opera7 及以上(Opera 内核原为：Presto，现为：Blink)
- Webkit：Safari Chrome

### 8. HTML5 有哪些新特性,移除了那些元素？如何处理 HTML5 新标签的浏览器兼容问题？如何区分 HTML 和 HTML5

新增加了图像、位置、存储、多任务等功能
**新增元素：**

- canvas
- 用于媒介回放的 video 和 audio 元素
- 本地离线存储。localStorage 长期存储数据，浏览器关闭后数据不丢失;sessionStorage 的数据在浏览器关闭后自动删除
- 语意化更好的内容元素，比如 article footer header nav section
- 位置 API：Geolocation(获取设备的经纬度)
- 表单控件，calendar date time email url search
- 新的技术：web worker(web worker 是运行在后台的 JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 web worker 在后台运行) web socket
- 拖放 API：drag、drop

**移除的元素：**

- 纯表现的元素：basefont big center font s strike tt u
- 性能较差元素：frame frameset noframes

**区分：**

- DOCTYPE 声明的方式是区分重要因素
- 根据新增加的结构、功能来区分

### 9. 简述一下你对 HTML 语义化的理解？

- 去掉或丢失样式的时候能够让页面呈现出清晰的结构。
- 有利于 SEO 和搜索引擎建立良好沟通，有助于爬虫抓取更多的信息，爬虫依赖于标签来确定上下文和各个关键字的权重。
- 方便其它设备解析。
- 便于团队开发和维护，语义化根据可读性。

### 10. HTML5 的文件离线储存怎么使用，工作原理是什么？

在线情况下，浏览器发现 HTML 头部有 manifest 属性，它会请求 manifest 文件，如果是第一次访问，那么浏览器就会根据 manifest 文件的内容下载相应的资源，并进行离线存储。如果已经访问过并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面。然后浏览器会对比新的 manifest 文件与旧的 manifest 文件，如果文件没有发生改变，就不会做任何操作，如果文件改变了，那么就会重新下载文件中的资源，并且进行离线存储

```html
<html manifest="cache.manifest"></html>
```

### 11. cookies，sessionStorage 和 localStorage 的区别？

都是保存在浏览器端，且是同源的

- cookies 是为了标识用户身份而存储在用户本地终端上的数据，始终在同源 http 请求中携带，即 cookies 在浏览器和服务器间来回传递，而 sessionstorage 和 localstorage 不会自动把数据发给服务器，仅在本地保存。
- 存储大小的限制不同。cookie 保存的数据很小，不能超过 4k，而 sessionstorage 和 localstorage 保存的数据大，可达到 5M。
- 数据的有效期不同。cookie 在设置的 cookie 过期时间之前一直有效，即使窗口或者浏览器关闭。sessionstorage 仅在浏览器窗口关闭之前有效。localstorage 始终有效，窗口和浏览器关闭也一直保存，用作长久数据保存。
- 作用域不同。cookie 在所有的同源窗口都是共享；sessionstorage 不在不同的浏览器共享，即使同一页面；localstorage 在所有同源窗口都是共享

### 12. iframe 框架有那些优缺点？

**优点：**

- iframe 跨域通信
- iframe 无刷新文件上传
- 解决加载缓慢的第三方内容如图标和广告等的加载问题
- iframe 能够原封不动的把嵌入的网页展现出来。

**缺点：**

- iframe 会阻塞主页面的 Onload 事件
- 搜索引擎的爬虫程序无法解读这种页面
- 框架结构中出现各种滚动条
- iframe 页面会增加服务器的 http 请求

### 13. label 的作用是什么? 是怎么用的?

label 标签用来定义表单控件间的关系,当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。label 中有两个属性是非常有用的, FOR 和 ACCESSKEY。
FOR 属性功能：表示 label 标签要绑定的 HTML 元素，你点击这个标签的时候，所绑定的元素将获取焦点

```html
<label for="InputBox">姓名</label><input id="InputBox" type="text" />
```

ACCESSKEY 属性功能：表示访问 label 标签所绑定的元素的热键，当您按下热键，所绑定的元素将获取焦点

```html
<Label FOR="InputBox" ACCESSKEY＝"N">姓名</Label><input ID="InputBox" type="text">
```

### 14. HTML5 的 form 如何关闭自动完成功能？

HTML 的输入框可以拥有自动完成的功能，当你往输入框输入内容的时候，浏览器会从你以前的同名输入框的历史记录中查找出类似的内容并列在输入框下面，这样就不用全部输入进去了，直接选择列表中的项目就可以了。但有时候我们希望关闭输入框的自动完成功能，例如当用户输入内容的时候，我们希望使用 AJAX 技术从数据库搜索并列举而不是在用户的历史记录中搜索。

**方法：**

- 在 IE 的 internet 选项菜单中里的自动完成里面设置
- 设置 form 输入框的 autocomplete 为 on 或者 off 来来开启输入框的自动完成功能

```html
<form action="" autocomplete="off"></form>
```

### 15. 如何实现浏览器内多个标签页之间的通信?

- WebSocket SharedWorker
- 也可以调用 localstorge、cookies 等本地存储方式。 localstorge 在另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件，我们通过监听事件，控制它的值来进行页面信息通信。

```js
window.addEventListener('storage', function (e) {
  console.log(e.newValue);
});
```

### 16. webSocket 如何兼容低浏览器？

- Adobe Flash Socket ActiveX HTMLFile (IE) 基于 multipart 编码发送 XHR 基于长轮询的 XHR
- 引用 WebSocket.js 这个文件来兼容低版本浏览器。

### 17. 页面可见性（Page Visibility）API 可以有哪些用途？

- 通过 visibilityState 的值得检测页面当前是否可见，以及打开网页的时间。
- 在页面被切换到其他后台进程时，自动暂停音乐或视频的播放。

### 18. 如何在页面上实现一个圆形的可点击区域？

- map+area 或者 svg
- border-radius

### 19. 网页验证码是干嘛的，是为了解决什么安全问题？

- 区分用户是计算机还是人的程序;
- 可以防止恶意破解密码、刷票、论坛灌水；

### 20. title 与 h1 的区别、b 与 strong 的区别、i 与 em 的区别？

- title 属性没有明确意义，只表示标题；h1 表示层次明确的标题，对页面信息的抓取也有很大的影响
- strong 标明重点内容，语气加强含义；b 是无意义的视觉表示
- em 表示强调文本；i 是斜体，是无意义的视觉表示

**视觉样式标签：** b i u s

**语义样式标签：** strong em ins del code

### 21. meta viewport 是做什么的？怎么用？

移动端浏览器通常都在一个比屏幕更宽的虚拟窗口中渲染页面，这个虚拟窗口就是 viewport，目的是正常展示没有做移动端适配的网页，可以让他们完整的展现给用户。我们有时用移动设备访问桌面版网页就会看到一个横向滚动条，这里可显示区域的宽度就是 viewport 的宽度。

该 meta 标签的作用是让当前 viewport 的宽度等于设备的宽度，同时不允许用户手动缩放

width 设为 width-device 基本是必须

user-scalable=0 禁止用户缩放

### 22. a 标签中 active hover link visited 正确的设置顺序是什么?

a:link 、a:visited 、a:hover 、a:active

### 23. dom 和 bom 是什么？

**DOM：** 文档对象模型，描述了处理网页内容的方法和接口。最根本对象是 document（window.document）。

由于 DOM 的操作对象是文档，所以 DOM 和浏览器没有直接关系。

**BOM：** 浏览器对象模型，描述了与浏览器进行交互的方法和接口。由 navigator、history、screen、location、window 五个对象组成的，最根本对象是 window。

用来获取或设置浏览器的属性、行为，例如：新建窗口、获取屏幕分辨率、浏览器版本号等。

浏览器的标签页、地址栏、搜索栏、菜单栏、滚动条等。

### 24. 对 WEB 标准以及 W3C 的理解与认识？

- web 标准规范要求，书写标签必须闭合、标签小写、不乱嵌套，可提高搜索机器人对网页内容的搜索几率；
- 建议使用外链 css 和 js 脚本，从而达到结构与行为、结构与表现的分离，提高页面的渲染速度，能更快地显示页面的内容；
- 样式与标签的分离，更合理的语义化标签，使内容能被更多的用户所访问、内容能被更广泛的设备所访问、更少的代码和组件， 从而降低维护成本、改版更方便；
- 不需要变动页面内容，便可提供打印版本而不需要复制内容，提高网站易用性；遵循 w3c 制定的 web 标准，能够使用户浏览者更方便的阅读，使网页开发者之间更好的交流。

## 更多面试题

- [常见 css 的面试题](./css.md)
- [常见 javascript 的面试题](./javascript.md)
- [常见 typescript 的面试题](./typescript.md)
- [常见 vue 的面试题](./vue.md)
- [常见 react 的面试题](./react.md)
- [常见 webpack 的面试题](./webpack.md)
- [常见 node 的面试题](./node.md)
- [前端工程化](./eng.md)
- [优化相关](./optimize.md)