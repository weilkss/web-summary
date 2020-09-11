# web 前端面试题

想进大厂？首先基础得扎实，技术面试得过，你才能有机会和 hr 小姐姐谈工资

## 性能优化篇

### css 性能优化

1. 内联首屏关键 CSS（Critical CSS）

   把首屏所需要的 css 内联

2. 异步加载 CSS

   CSS 会阻塞渲染，在 CSS 文件请求、下载、解析完成之前，浏览器将不会渲染任何已处理的内容

   那么将首屏关键 CSS 内联后，剩余的 CSS 内容的阻塞渲染就不是必需的了，可以使用外部 CSS，并且异步加载

   ```html
   <link rel="stylesheet" href="/styles.css" media="print" onload="this.media='all'" />
   ```

3. 文件压缩
4. 去除无用 CSS
5. 有选择地使用选择器，最好使用 class 选择器，减少后代选择器的使用
6. 减少使用昂贵的属性

   编写 CSS 时，我们应该尽量减少使用昂贵属性，如 box-shadow/border-radius/filter/透明度/:nth-child 等

7. 优化重排与重绘
8. 不要使用`@import`

### html 性能优化

1. HTML 标签有始终。 减少浏览器的判断时间
2. 把 script 标签移到 HTML 文件末尾，因为 JS 会阻塞后面的页面的显示
3. 减少 iframe 的使用，因为 iframe 会增加一条 http 请求，阻止页面加载，即使内容为空，加载也需要时间
4. class 和 id 规范命名，以中划线连接
5. 减少不必要的嵌套，尽量扁平化，因为当浏览器编译器遇到一个标签时就开始寻找它的结束标签，直到它匹配上才能显示它的内容，所以当嵌套很多时打开页面就会特别慢
6. 减少注释，因为过多注释不光占用空间，如果里面有大量关键词会影响搜索引擎的搜索
7. 使用 css+div 代替 table 布局，去掉格式化控制标签如：strong，b，i 等，使用 css 控制
8. 代码要结构化、语义化
9. css 和 javascript 尽量全部分离到单独的文件中
10. 尽量少使用废弃的标签，如 b、i 等，尽管高版本浏览器是向后兼容的

### javascript 性能优化

1. 删除未使用的 js 代码
2. 数组和对象操作避免使用构造函数
3. 尽量避免使用非必要的全局变量
4. 合理使用缓存机制
5. 减少循环中的活动,循环条件用 `break` 结束
6. 减少不必要的变量
7. 并不是代码量越少性能就越好
8. 原生方法更快
9. 尽量避免使用闭包

### react 性能优化

1. Code Splitting

   改写成动态 import 的形式

2. shouldComponentUpdate 避免重复渲染
3. 使用不可突变数据结构

   数组、对象改变是最好使用 扩展运算符

4. 组件尽可能的进行拆分、解耦
5. 列表类组件优化
6. bind 函数优化

- constructor 绑定

```js
constructor(props) {
super(props);
this.handleClick = this.handleClick.bind(this); //构造函数中绑定
}
//然后可以
<p onClick={this.handleClick}>
```

- 使用时绑定

```js
<p onClick={this.handleClick.bind(this)}>
```

- 使用箭头函数

```js
<button click={() => this.handleClick()} />
```

7. 不要滥用 props

   props 尽量只传需要的数据，避免多余的更新，尽量避免使用`{...props}`

8. ReactDOMServer 进行服务端渲染组件

9. 在离开页面时在 componentWillUnmount 里清除`setInterval` `setTimeout` 定时器

### vue 性能优化

1. 代码模块化
2. 避免 for 和 if 同时使用
3. Vue 路由设置成懒加载
4. 更加理解 Vue 的生命周期，不要造成内部泄漏，使用过后的全局变量在组件销毁后重新置为 null
5. 可以使用 keep-alive,keep-alive 是 Vue 提供的一个比较抽象的组件，用来对组件进行缓存，从而节省性能
6. 按需引入
7. 在离开页面时在 destroyed 周期里 清除`setInterval` `setTimeout` 定时器

### 网站性能优化

1. http 请求方面,减少请求数量,请求体积,对应的做法是,对项目资源进行压缩,控制项目资源的 dns 解析在 2 到 4 个域名,提取公告的样式,公共的组件,雪碧图,缓存资源,

2. 压缩资源,提取公共资源压缩,提取 css ,js 公共方法

3. 不要缩放图片,使用雪碧图,使用字体图表(阿里矢量图库)

4. 使用 CDN,抛开无用的 cookie

5. 减少重绘重排,CSS 属性读写分离,最好不要用 js 修改样式,dom 离线更新,渲染前指定图片的大小

6. js 代码层面的优化,减少对字符串的计算,合理使用闭包,首屏的 js 资源加载放在最底部

### 用户体验优化

3. 图片懒加载
4. 分片渲染（从上往下渲染）


## 更多面试题

- [常见 css 的面试题](./css.md)
- [常见 html 的面试题](./html.md)
- [常见 javascript 的面试题](./javascript.md)
- [常见 typescript 的面试题](./typescript.md)
- [常见 vue 的面试题](./vue.md)
- [常见 react 的面试题](./react.md)
- [常见 webpack 的面试题](./webpack.md)
- [常见 node 的面试题](./node.md)
- [前端工程化](./eng.md)
- [优化相关](./optimize.md)