# web 前端面试题

想进大厂？首先基础得扎实，技术面试得过，你才能有机会和 hr 小姐姐谈工资

## css 篇

### 1. 介绍一下标准的 CSS 的盒子模型？与低版本 IE 的盒子模型有什么不同的？

**盒模型：** 内容(content)、填充(padding)、边界(margin)、 边框(border)

> html 指定 doctype 的话就默认为标准盒模型

**标准盒子模型：** 实际大小(width,height)就为 content 的大小

**IE 盒子模型：** 实际大小(width,height)为 content+border*2+padding*2

### 2. box-sizing 属性？

用来控制元素的盒子模型的解析模式，默认为 content-box

**context-box：** W3C 的标准盒子模型，设置元素的 height/width 属性指的是 content 部分的高/宽

**border-box：** IE 传统盒子模型。设置元素的 height/width 属性指的是 border + padding + content 部分的高/宽

### 3. CSS 选择器有哪些？以及优先级

| 符号                   | 描述           | 权重     |
| ---------------------- | -------------- | -------- |
| `!important`           | important      | 权重最高 |
| `*`                    | 通配符         | 不参与   |
| `# `                   | id 选择器      | 1        |
| `element[name=[name]]` | 属性选择器     | 2        |
| `.`                    | 类选择器       | 3        |
| `element element`      | 后代选择器     | 4        |
| `>`                    | 子选择器       | 4        |
| `+`                    | 直接兄弟选择器 | 4        |
| `~`                    | 之后所有兄弟   | 4        |
| `element`              | 元素选择器     | 5        |
| `::`                   | 伪类选择器     | 5        |

**优先级（就近原则）：** !important > [ id > class > element ]

优先级相同时，则采用就近原则，选择最后出现的样式；继承得来的属性，其优先级最低

**可继承的属性：** font-size, font-family, color

**不可继承的样式：** border, padding, margin, width, height

### 4. CSS 优先级算法如何计算？

选择器的特殊性值表述为 4 个部分，用 0,0,0,0 表示。

- 内嵌样式，加 1,0,0,0。
- ID 选择器的特殊性值，加 0,1,0,0。
- 类选择器、属性选择器或伪类，加 0,0,1,0。
- 元素和伪元素，加 0,0,0,1。
- 通配选择器\*对特殊性没有贡献，即 0,0,0,0。

1. !important 声明的样式优先级最高，如果冲突再进行计算。
2. 如果优先级相同，则选择最后出现的样式。
3. 继承得到的样式的优先级最低。

### 5. CSS3 新增伪类有那些?

**p:first-of-type** 选择属于其父元素的首个元素

**p:last-of-type** 选择属于其父元素的最后元素

**p:only-of-type** 选择属于其父元素唯一的元素

**p:only-child** 选择属于其父元素的唯一子元素

**p:nth-child(2)** 选择属于其父元素的第二个子元素

**:enabled :disabled** 表单控件的禁用状态。

**:checked** 单选框或复选框被选中。

### 6. css 不知宽高的元素居中?

1. 反向移动

```css
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
```

2. flex 布局

```css
display: flex;
align-items: center;
justify-content: center;
```

3. 四向定位

```css
position: absolute;
right: 0;
left: 0;
top: 0;
bottom: 0;
margin: auto;
```

4. 表格 table

```css
/* after */
display: table-cell;
text-align: center;
vertical-align: middle;

/* children */
display: inline-block;
```

5. grid 布局

```css
/* after */
display: grid;

/* children */
align-self: center;
justify-self: center;
```

### 7. display 有哪些值？说明他们的作用?

| 值           | 描述                                  |
| ------------ | ------------------------------------- |
| none         | 此元素不会被显示                      |
| block        | 此元素将显示为块级元素                |
| inline       | 默认。此元素会被显示为内联元素        |
| inline-block | 行内块元素                            |
| table        | 此元素会作为块级表格来显示            |
| list-item    | 此元素会作为列表显示                  |
| inherit      | 规定应该从父元素继承 display 属性的值 |
| flex         | 将对象作为弹性伸缩盒显示              |
| inline-flex  | 将对象作为内联块级弹性伸缩盒显示      |
| grid         | 将对象作为网格布局                    |

### 8. position 的值

| 值       | 描述                                                                                    |
| -------- | --------------------------------------------------------------------------------------- |
| absolute | 生成绝对定位                                                                            |
| relative | 生成相对定位                                                                            |
| fixed    | 生成固定定位                                                                            |
| static   | 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明 |
| sticky   | 粘性定位，该定位基于用户滚动的位置                                                      |
| inherit  | 规定应该从父元素继承 position 属性的值                                                  |
| initial  | 设置该属性为默认值                                                                      |

### 9. CSS3 有哪些新特性？

1. RGBA 和 opacity
2. `background-image` `background-origin(content-box/padding-box/border-box)` `background-size` `background-repeat`
3. word-wrap（对长的不可分割单词换行）word-wrap：break-word
4. 文字阴影：text-shadow： 5px 5px 5px #FF0000;（水平阴影，垂直阴影，模糊距离，阴影颜色）
5. font-face 属性：定义自己的字体
6. 圆角（边框半径）：border-radius 属性用于创建圆角
7. 边框图片：border-image: url(border.png) 30 30 round
8. 盒阴影：box-shadow: 10px 10px 5px #888888
9. 媒体查询：定义两套 css，当浏览器的尺寸变化时会采用不同的属性

### 10. 请解释一下 CSS3 的 flexbox（弹性盒布局模型）,以及适用场景？

该布局模型的目的是提供一种更加高效的方式来对容器中的条目进行布局、对齐和分配空间。在传统的布局方式中，block 布局是把块在垂直方向从上到下依次排列的；而 inline 布局则是在水平方向来排列。弹性盒布局并没有这样内在的方向限制，可以由开发人员自由操作。
试用场景：弹性布局适合于移动前端开发，在 Android 和 ios 上也完美支持。

### 11. 用纯 CSS 创建一个三角形的原理是什么？

> 利用的元素转角填充平分的原理

首先，需要把元素的宽度、高度设为 0。然后设置边框样式。

```css
width: 0;
height: 0;
border-top: 40px solid transparent;
border-left: 40px solid transparent;
border-right: 40px solid transparent;
border-bottom: 40px solid #000;
```

### 12. 一个满屏品字布局如何设计

1. 第一种真正的品字

- 三块高宽是确定的；
- 上面那块用 margin: 0 auto;居中；
- 下面两块用 float 或者 inline-block 不换行；
- 用 margin 调整位置使他们居中。

2. 全屏的品字布局

上面的 div 设置成 100%，下面的 div 分别宽 50%，然后使用 float 或者 inline 使其不换行

### 13. 常见的兼容性问题？

1. 最主要也是最常见的，就是浏览器对标签的默认支持不同，所以我们要统一，就要进行 CSS reset
   - normalize.css
   - neat.css
2. IE6 双边距 bug: 块属性标签添加了浮动 float 之后，若在浮动方向上也有 margin 值，则 margin 值会加倍
   - 给 float 的元素添加 display:inline;将其转换为内联元素
3. 表单元素行高不一致
   - 给表单元素添加 vertical-align:middle
   - 给表单元素添加 float:left
4. IE6（默认 16px 为最小）不识别较小高度的标签（一般为 10px）
   - 给标签添加 overflow:hidden;
   - 给标签添加 font-size:0
5. 图片添加超链接时，在 IE 浏览器中会有蓝色的边框
   - 给图片添加 border:0 或者 border：none
6. 最小高度 min-height 不兼容 IE6

- ```css
  min-height: 100px;
  _height: 100px;
  ```

- ```css
  min-height: 100px;
  height: auto !important;
  height: 100px;
  ```

7. 图片默认有间隙

- 给 img 添加 float
- 给 img 添加 display：block
- 给 img 添加 vertical-align: middle

8. 按钮默认大小不一

- 用 a 标记模拟按钮，使用 JS 实现其他功能

9. 百分比 BUG ，父元素设置 100%，子元素各 50%，在 IE6 下，50%+50%大于 100%

- 给右边的浮动元素添加 clear:right

10. 鼠标指针 BUG

- cursor:hand 只有 IE 浏览器识别
- cursor:pointer;IE 及以上浏览器和其他浏览器都识别

11. 透明度设置，IE 不识别 opacity 属性

- 兼容 IE 浏览器 filter:alpha(opacity=value);(取值范围 1-100)

12. 兄弟级的块之间，margin 这个属性上下边距，经常会发生重叠的情况，以数值大的为准，而不会相加

- float 浮动
- display:inline-block

13. 父子级的块之间，子级的上下 margin 会与父级上下 margin 重叠，以数值大的为准，而不会相加

- 父级加：overflow:hidden
- 父级加：border
- 父级加：float:left
- margin-top 改成 padding-top

### 14. 谈谈 CSS Hack

我们为了让页面形成统一的效果，要针对不同的浏览器或不同版本写出对应可解析的 CSS 样式，所以我们就把这个针对不同浏览器/版本而写 CSS 的过程叫做 CSS hack.

CSS hack 主要有三种：IE 条件注释法、CSS 属性前缀法、选择器前缀法

1. 条件注释法

```css
<!--  lt是小于 gt是大于 lte是小于等于 gte是不小于 !是不等于 -->

<!-- [if IE]>
   font-size:12px
<![endif]-->
```

2. CSS 属性前缀法

```css
/* 可以先使用“\9"标记，将IE分离出来，再用”*"分离出IE6/IE7，最后可以用“_”分离出IE6 */

color: #111; /* all */

color: #222\9; /* IE */
*color: #333; /* IE6/IE7 */
_color: #444; /* IE6 */
```

3. 选择器前缀法

```css
/* IE6可识别 */
*div {
  color: red;
}
/* IE7可识别 */
* + div {
  color: red;
}
```

### 15. display:none 与 visibility：hidden 的区别？

**display：none** 不显示对应的元素，在文档布局中不再分配空间（回流+重绘）

**visibility：hidden** 隐藏对应元素，在文档布局中仍保留原来的空间（重绘）

### 16. position 跟 display、overflow、float 这些特性相互叠加后会怎么样？

position：absolute/fixed 优先级最高，有他们在时，float 不起作用，display 值需要调整。float 或者 absolute 定位的元素，只能是块元素或表格

### 17. 对 BFC 规范(块级格式化上下文：block formatting context)的理解？

**创建 BFC**

- 根元素，即 html
- float 的值不是 none
- position 的值不是 static 或者 relative
- display 的值是 inline-block,table-cell,flex,table-caption 或者 inline-flex
- overflow 的值不是 visible

**BFC 的特性**

- 内部的 Box 会在垂直方向上一个接一个放置。
- Box 垂直方向的距离由 margin 决定，属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠。
- 每个元素的 margin box 的左边，与包含块 border box 的左边相接触。
- BFC 的区域不会与 float box 重叠。
- BFC 是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
- 计算 BFC 的高度时，浮动元素也会参与计算。

### 18. 为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式？

**浮动带来的问题：**

- 父元素的高度无法被撑开，影响与父元素同级的元素
- 与浮动元素同级的非浮动元素（内联元素）会跟随其后
- 若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构。

**清除浮动的方式：**

- 父级 div 定义 height
- 最后一个浮动元素后加空 div 标签 并添加样式 clear:both【一般用::before】
- 包含浮动元素的父标签添加样式 overflow 为 hidden 或 auto。
- 父级 div 定义 zoom

### 19. 设置元素浮动后，该元素的 display 值是多少？

自动变成 display:block

### 20. 移动端的布局用过媒体查询吗？

通过媒体查询可以为不同大小和尺寸的媒体定义不同的 css，适应相应的设备的显示

```css
@media screen and (max-width: 300px) {
  body {
    background-color: lightblue;
  }
}
```

### 21. CSS 优化、提高性能的方法有哪些？

- 避免过度约束
- 避免后代选择符,尽量使用 class 类选择器
- 移除空的 css 规则
- 正确使用 display 的属性
- 使用紧凑的语法
- 不滥用浮动，尽量少用
- 不滥用 web 字体，不声明过多的 font-size
- 使用 CSS 渐变等高级特性，需指定所有浏览器的前缀
- 避免`!important`以及通配符
- 删除多余代码，减少文件体积，删除一些无用的样式，比如 display:inline 后使用 width、height、margin、padding 以及 float 无效

### 22. 浏览器是怎样解析 CSS 选择器的？

CSS 选择器的解析是从右向左解析的。若从左向右的匹配，发现不符合规则，需要进行回溯，会损失很多性能。若从右向左匹配，先找到所有的最右节点，对于每一个节点，向上寻找其父节点直到找到根元素或满足条件的匹配规则，则结束这个分支的遍历。两种匹配规则的性能差别很大，是因为从右向左的匹配在第一步就筛选掉了大量的不符合条件的最右节点（叶子节点），而从左向右的匹配规则的性能都浪费在了失败的查找上面

### 23. 在网页中的应该使用奇数还是偶数的字体？为什么呢？

- ie6 会把奇数字体强制转化为偶数，即 13px 渲染为 14px
- 平分字体
- Windows 自带的点阵宋体（中易宋体）从 Vista 开始只提供 12、14、16 px 这三个大小的点阵，而 13、15、17 px 时用的是小一号的点阵（即每个字占的空间大了 1 px，但点阵没变），于是略显稀疏
- 使用奇数号字体不好的地方是，文本段落无法对齐
- 在谷歌中默认最小是 12px 字体，如果设置 11px 字体会渲染为 12px 字号，chrome27.0 以下通过设置 css 属性-webkit-text-size-adjust: none；以上使用 transform:scale(0.7)

### 24. margin 和 padding 分别适合什么场景使用？

**何时使用 margin：**

- 需要在 border 外侧添加空白
- 空白处不需要背景色
- 上下相连的两个盒子之间的空白，需要相互抵消时。

**何时使用 padding：**

- 需要在 border 内侧添加空白
- 空白处需要背景颜色
- 上下相连的两个盒子的空白，希望为两者之和。

### 25. margin 设置百分比相对于谁？

相对于父级的 `width`

添加属性可以改变为纵向高度

```css
writing-mode: horizontal-tb;
direction: ltr;
```

### 26. 全屏滚动的原理是什么？用到了 CSS 的哪些属性？

- 原理：有点类似于轮播，整体的元素一直排列下去，假设有 5 个需要展示的全屏页面，那么高度是 500%，只是展示 100%，剩下的可以通过 transform 进行 y 轴定位，也可以通过 margin-top 实现
- overflow：hidden；transition：all 1000ms ease；

### 27. 什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的 IE？

响应式网站设计(Responsive Web design)是一个网站能够兼容多个终端，而不是为每一个终端做一个特定的版本。

基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理。

页面头部必须有 meta 声明的 viewport。

### 28. 视差滚动效果？

视差滚动（Parallax Scrolling）通过在网页向下滚动的时候，控制背景的移动速度比前景的移动速度慢来创建出令人惊叹的 3D 效果。

1. CSS3 实现

   优点：开发时间短、性能和开发效率比较好，缺点是不能兼容到低版本的浏览器

2. jQuery 实现

   通过控制不同层滚动速度，计算每一层的时间，控制滚动效果。

优点：能兼容到各个版本的，效果可控性好

缺点：开发起来对制作者要求高

3.  插件实现方式
    例如：parallax-scrolling，兼容性十分好

### 29. ::before 和 :after 中双冒号和单冒号有什么区别？解释一下这 2 个伪元素的作用

- 单冒号(:)用于 CSS3 伪类，双冒号(::)用于 CSS3 伪元素。
- ::before 就是以一个子元素的存在，定义在元素主体内容之前的一个伪元素。并不存在于 dom 之中，只存在在页面之中。

:before 和 :after 这两个伪元素，是在 CSS2.1 里新出现的。起初，伪元素的前缀使用的是单冒号语法，但随着 Web 的进化，在 CSS3 的规范里，伪元素的语法被修改成使用双冒号，成为::before ::after

### 30. 你对 line-height 是如何理解的？

行高是指一行文字的高度，具体说是两行文字间基线的距离。CSS 中起高度作用的是 height 和 line-height，没有定义 height 属性，最终其表现作用一定是 line-height。
单行文本垂直居中：把 line-height 值设置为 height 一样大小的值可以实现单行文字的垂直居中，其实也可以把 height 删除。

多行文本垂直居中：需要设置 display 属性为 inline-block。

### 31. 让页面里的字体变清晰，变细用 CSS 怎么做？

-webkit-font-smoothing 在 window 系统下没有起作用，但是在 IOS 设备上起作用-webkit-font-smoothing：antialiased 是最佳的，灰度平滑。

### 32. position:fixed;在 android 下无效怎么处理？

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no" />
```

### 33. 如果需要手动写动画，你认为最小时间间隔是多久，为什么？

多数显示器默认频率是 60Hz，即 1 秒刷新 60 次，所以理论上最小间隔为 1/60＊1000ms ＝ 16.7ms。

### 34. li 与 li 之间有看不见的空白间隔是什么原因引起的？有什么解决办法？

行框的排列会受到中间空白（回车空格）等的影响，因为空格也属于字符,这些空白也会被应用样式，占据空间，所以会有间隔，把字符大小设为 0，就没有空格了。

解决方法：

- 可以将<li>代码全部写在一排
- 浮动 li 中 float：left
- 在 ul 中用 font-size：0（谷歌不支持）；可以使用 letter-space：-3px

### 35. display:inline-block 什么时候会显示间隙？

- 有空格时候会有间隙 解决：移除空格
- margin 正值的时候 解决：margin 使用负值
- 使用 font-size 时候 解决：font-size:0、letter-spacing、word-spacing

### 40. CSS 属性 overflow 属性定义溢出元素内容区的内容会如何处理?

- 参数是 scroll 时候，必会出现滚动条。
- 参数是 auto 时候，子元素内容大于父元素时出现滚动条。
- 参数是 visible 时候，溢出的内容出现在父元素之外。
- 参数是 hidden 时候，溢出隐藏。

### 41. 阐述一下 CSS Sprites

将一个页面涉及到的所有图片都包含到一张大图中去，然后利用 CSS 的 background-image，background- repeat，background-position 的组合进行背景定位。利用 CSS Sprites 能很好地减少网页的 http 请求，从而大大的提高页面的性能；CSS Sprites 能减少图片的字节。

### 42. 超出省略号和多行省略号

单行

```css
overflow: hidden;
white-space: nowrap;
text-overflow: ellipsis;
```

多行

```css
overflow:hiden;
text-overflow:ellipsis; // 用省略号"..."隐藏超出范围的文本
display:-webkit-box;  //将对象作为弹性伸缩盒子模型显示
-webkit-line-clamp:2; //用来限制在一个块元素显示的文本的行数
-webkit-box-orient:vertical;设置弹性盒对象的子元素的排列方式
```

### 43. flex 布局

```css
.box {
  /* 块元素 */
  display: flex;
  /* 行内元素 */
  display: inline-flex;
}
```

**容器的属性**

```css
.box {
  flex-direction: row | row-reverse | column | column-reverse;
  flex-wrap: nowrap | wrap | wrap-reverse;
  flex-flow: <flex-direction> || <flex-wrap>;
  justify-content: flex-start | flex-end | center | space-between | space-around;
  align-items: flex-start | flex-end | center | baseline | stretch;
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

**项目的属性**

```css
.item{
   // order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0
   order: 0;
   // flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
   flex-grow: 0;
   // flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小
   flex-shrink:1;
   // flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）
   flex-basis: 0 | auto
   // flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto
   flex: 0;
   // align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性
   align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

## 更多面试题

- [常见 html 的面试题](./html.md)
- [常见 javascript 的面试题](./javascript.md)
- [常见 typescript 的面试题](./typescript.md)
- [常见 vue 的面试题](./vue.md)
- [常见 react 的面试题](./react.md)
- [常见 webpack 的面试题](./webpack.md)
- [常见 node 的面试题](./node.md)
- [前端工程化](./eng.md)
- [优化相关](./optimize.md)
