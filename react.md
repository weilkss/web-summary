# web 前端面试题

想进大厂？首先基础得扎实，技术面试得过，你才能有机会和 hr 小姐姐谈工资

## react 篇

### 1. 当你调用 setState 的时候，发生了什么事？

- 代码中调用 setState 函数之后，React 会将传入的参数对象与组件当前的状态合并，然后触发所谓的调和过程（Reconciliation）。
- 经过调和过程，React 会以相对高效的方式根据新的状态构建 React 元素树并且着手重新渲染整个 UI 界面；
- 在 React 得到元素树之后，React 会自动计算出新的树与老树的节点差异，然后根据差异对界面进行最小化重渲染；
- 在差异计算算法中，React 能够相对精确地知道哪些位置发生了改变以及应该如何改变，这就保证了局部更新，而不是全部重新渲染。

### 2. React 项目用过什么脚手架

- creat-react-app

### 3. 类组件和函数组件之间有什么区别？ 什么时候用类组件 Class Component 和函数组件 Function

**类组件：**
有自己的数据 state，有自己的生命周期，并且有在 render 方法里返回 React 元素

**函数组件**
函数组件接收一个单一的 props 对象并返回了一个 React 元素

**什么时候用？**

以前是有自己的状态 state 或者会用到生命周期就会用 class 组件，其他功能封装静态显示就用函数组件

但是在 hooks 出现后就不那么认为了，一般封装组件都习惯用函数组件，内部的状态可以用 hooks，页面一般都用 class 组件

### 4. 什么是虚拟 DOM？

虚拟 DOM（virtual dom）它是真实 DOM 的内存表示,一种编程概念，一种模式。它会和真实的 DOM 同步，比如通过 ReactDOM 这种库，这个同步的过程叫做调和(reconcilation)

虚拟 DOM 更多是一种模式，不是一种特定的技术

### 5. React 中的 refs 作用是什么？

Refs 是 React 提供给我们的安全访问 DOM 元素或者某个组件实例的句柄

### 6. React 中的 keys 作用是什么？

key 是 react 组件的唯一标识，就和人的身份证一样，如果没有 key 或者 key 一样，在一个域里面，react 会认为是相同的组件，渲染第一个后就不会渲染后面的组件，在 react 中我们用 map 循环渲染出来的列表一般默认是取 `index` 作为 key,但是最好我们用一个独一无二的字符串来做为表示，比如数据中的 `id`

为什么不推荐使用 `index` 作为 key 值，因为我们的数据列表会发生变化，比如排序、增删等，此时的 key 即 index 不会变，react 会认为你的组件不会变，而不会更新组件

```js
//  例子：
//  我们在第一个input中输入值后，通过点击按钮删除第一个input，
//  但是我们发现第一个input是删除了，但是我们第一个input的值转移到第二个input里面了
//  因为我们删除第一个时，第二个的key变成第一个，所以会被认为时第一个组件

export default class App extends React.Component {
  state = {
    list: ['第一个', '第二个', '第三个']
  };

  handleDelete(index) {
    const { list } = this.state;

    list.splice(index, 1);
    this.setState({
      list
    });
  }

  render() {
    console.log(this.state);
    return (
      <div>
        {this.state.list.map((item, index) => (
          <p key={index}>
            <label>{item}</label>
            <input />
            <button onClick={() => this.handleDelete(index)}>delete</button>
          </p>
        ))}
      </div>
    );
  }
}
```

### 7. 描述下 react 的事件处理？和原生事件有什么不同

react 基于 vitrual dom 实现了 syntheticEvent （合成事件），react 事件处理器接收到一个 syntheticEvent 对象，syntheticEvent 和原生浏览器事件一样拥有同样的接口，也支持事件冒泡机制。可以通过 stopPropgation 和 preventDefault  中断。如果需要访问原生事件对象，可以使用 nativeEvent 属性

如果 DOM 上绑定了过多的事件处理函数，整个页面响应以及内存占用可能都会受到影响。React 为了避免这类 DOM 事件滥用，同时屏蔽底层不同浏览器之间的事件系统差异，实现了一个中间层——SyntheticEvent

**区别：**

React 并不是将事件直接绑定在 dom 上面，而是采用事件冒泡的形式冒泡到 document 上面，然后 React 将事件封装给正式的函数处理运行和处理，而原生事件则是绑定在原生 dom 上

**Example：**

- 当用户在为 onClick 添加函数时，React 并没有将 Click 时间绑定在 DOM 上面。
- 而是在 document 处监听所有支持的事件，当事件发生并冒泡至 document 处时，React 将事件内容封装交给中间层 SyntheticEvent（负责所有事件合成）
- 所以当事件触发的时候，对使用统一的分发函数 dispatchEvent 将指定函数执行

### 8. state 和 props 有什么区别？

state 和 props 都是普通的 JavaScript 对象。尽管它们两者都具有影响渲染输出的信息，但它们在组件方面的功能不同

- props 是一个从外部传进组件的参数，主要作为就是从父组件向子组件传递数据，它具有可读性和不变性，只能通过外部组件主动传入新的 props 来重新渲染子组件，否则子组件的 props 以及展现形式不会改变
- state 的主要作用是用于组件保存、控制以及修改自己的状态，它只能在 constructor 中初始化，它算是组件的私有属性，不可通过外部访问和修改，只能通过组件内部的 this.setState 来修改，修改 state 属性会导致组件的重新渲染

### 9. 如何创建 refs？

Refs 是使用 React.createRef() 方法创建的，并通过 ref 属性添加到 React 元素上

```js
class Example extends React.Component {
  inputRef = React.createRef();

  componentDidMount() {
    console.log(this.inputRef.current);
  }

  render() {
    return <input ref={this.inputRef} />;
  }
}
```

### 10. 什么是高阶组件？

- 高阶组件（HOC）是 React 中用于复用组件逻辑的一种高级技巧
- 高阶组件的参数为一个组件返回一个新的组件
- 组件是将 props 转换为 UI，而高阶组件是将组件转换为另一个组件

### 11. constructor 中 super 与 props 参数一起使用的目的是什么？

在调用方法之前，子类构造函数无法使用 this 引用 super()

在 ES6 中，在子类的 constructor 中必须先调用 super 才能引用 this

### 12. 什么是受控组件？

> 在大多数情况下，react 推荐使用 受控组件 来处理表单数据

**先说说非受控组件**

像 `input` `select` `textarea` 这些组件的值是可以用户输入并保存在 dom 中，我们只需要在需要时通过 ref 去获取值，这类叫非受控组件

如果想用非受控组件设置默认值时可以用 `defaultValue` 而不是 `value`

**受控组件**

受控组件就是组件的状态受 React 控制。上面提到过，既然通过设置 input 的 value 属性, 无法改变输入框值,那么我们把它和 state 结合在一起,再绑定 onChange 事件,实时更新 value 值就行了

```js
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: props.value
    };
  }

  handleChange(e) {
    this.setState({
      value: e.target.value
    });
  }

  render() {
    return <input value={this.state.value} onChange={e => this.handleChange(e)} />;
  }
}
```

### 13. 什么是 JSX？

JSX 即 JavaScript XML。一种在 React 组件内部构建标签的类 XML 语法。JSX 为 react.js 开发的一套语法糖，也是 react.js 的使用基础。React 在不使用 JSX 的情况下一样可以工作，然而使用 JSX 可以提高组件的可读性，因此推荐使用 JSX

- 允许使用熟悉的语法来定义 HTML 元素树；
- 提供更加语义化且移动的标签；
- 程序结构更容易被直观化；
- 抽象了 React Element 的创建过程；
- 可以随时掌控 HTML 标签以及生成这些标签的代码；
- 是原生的 JavaScript。

### 14. 为什么不直接更新 state 状态？

直接使用 `this.state.value = '值'` 是可以改变 value 的值，但是不会不会重新渲染组件更新 UI，而且官方也不推荐这么使用，一般会在 EsLint 中配置避免这种写法出现

正确的是使用 `setState()` 方法。它计划对组件状态对象的更新。状态改变时，组件通过重新渲染做出响应

### 15. ReactJS 生命周期有哪些不同阶段？

React 组件的生命周期分为四个不同阶段：

**初始化：** 在此阶段，react 组件准备设置初始状态和默认道具。getDefaultProps、getInitialState

**挂载：** react 组件已准备好挂载在浏览器 DOM 中。此阶段涵盖 componentWillMount 和 componentDidMount 生命周期方法。

**更新：** 在此阶段，组件以两种方式进行更新，即发送新道具和更新状态。此阶段涵盖了 shouldComponentUpdate、componentWillReceiveProps、componentWillUpdate 和 componentDidUpdate 生命周期方法。

**卸载：** 在最后一个阶段，不需要该组件，并且可以从浏览器 DOM 上卸载该组件。此阶段包括 componentWillUnmount 生命周期方法。

### 16. 使用 React Hooks 有什么优势？

**Hook 是什么？**

Hook 是一个特殊的函数，它可以让你“钩入” React 的特性。例如，useState 是允许你在 React 函数组件中添加 state 的 Hook

hooks 只是多了一种写组件的方法，使编写一个组件更简单更方便，同时可以自定义 hook 把公共的逻辑提取出来，让逻辑在多个组件之间共享

**优点：**

- 无需复杂的 DOM 结构
- 简洁易懂

**useEffect**

React 组件需要在渲染后执行某些操作。React 会保存你传递的函数（我们将它称之为 “effect”），并且在执行 DOM 更新之后调用它

针对 effect 的第二个参数接受一个数组，其中传入我们的声明的动态数据 `count` `value` ，然后传入那个在更新值后就会调用 `useEffect`,而且当我们更新的值和上一次的值一样 React 会跳过这个 effect，这就实现了性能的优化，而且异步请求也一般在`useEffect`去拿

```js
const [count, setCount] = useState(1);
const [value, setValue] = useState(1);

useEffect(() => {
  setTimeout(() => {
    setCount(1);
    setTimeout(() => {
      setValue(2);
    }, 1000);
  }, 1000);
}, [count, value]);
```

### 17. react 中 this 绑定的方法？

有三种绑定方法

- 在 constructor 中绑定

```js
  constructor(pops){
    super();
    this.handleClick = this.handleClick.bind(this);
  }
```

- 在使用的时候绑定

```js
<button onClick={this.handleClick.bind(this)}>按钮</button>
```

- 使用箭头函数

```js
// 方式一
handleClick=（）=>{

}
// 方式二
<button onClick={()=>this.handleClick}>按钮</button>
```

### 18. React context 是什么？

**官网说法：**

简单说就是，当你不想在组件树中通过逐层传递 props 或者 state 的方式来传递数据时，可以使用 Context 来实现 跨层级 的组件数据传递

一般不用，因为它使组件重用更加困难，推荐使用 redux 状态管理

### 19. diff 计算？

计算出 Virtual DOM 中真正变化的部分，并只针对该部分进行原生 DOM 操作，而非重新渲染整个页面

- 把树形结构按照层级分解，只比较同级元素。
- 给列表结构的每个单元添加唯一的 key 属性，方便比较。
- React 只会匹配相同 class 的 component（这里面的 class 指的是组件的名字）
- 合并操作，调用 component 的 setState 方法的时候, React 将其标记为 dirty.到每一个事件循环结束, React 检查所有标记 dirty 的 component 重新绘制.
- 选择性子树渲染。开发人员可以重写 shouldComponentUpdate 提高 diff 的性能。

### 20. 了解 redux 么，说一下 redux 把

它是 JavaScript 应用程序的可预测状态容器，用于整个应用程序的状态管理。使用 Redux 开发的应用程序易于测试，可以在不同的环境中运行，表现出一致的行为

### 21. Redux 遵循的三个原则是什么?

- **单一数据源**

  整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中

- **State 是只读的**

  唯一改变 state 的方法就是触发 action，action 是一个用于描述已发生事件的普通对象，而触发 action 的方法是 dispatch

- **使用纯函数来执行修改**

  为了描述 action 如何改变 state tree ，你需要编写 reducers

### 22. 说说 redux 的组成部分

- **Action：**

  Action 是把数据从应用传到 store 的有效载荷。它是 store 数据的唯一来源。一般来说是通过 store.dispatch() 将 action 传到 store

  Action 本质上是 JavaScript 普通对象。我们约定，action 内必须使用一个字符串类型的 type 字段来表示将要执行的动作

- **Reducer：**

  reducer 就是一个纯函数，接收旧的 state 和 action，返回新的 state

  永远不要在 reducer 里做这些操作：

  - 修改传入参数；
  - 执行有副作用的操作，如 API 请求和路由跳转；
  - 调用非纯函数，如 `Date.now()` 或 `Math.random()`

- **Store：**

  Redux 应用只有一个单一的 store, 所有的 state 都在 store 里面管理，使用 `createStore()` 创建一个 store

### 23. Redux 的中间件

- **Redux-logger：** 提供日志输出
- **Redux-thunk：** 处理异步操作
- **Redux-promise：** 处理异步操作，actionCreator 的返回值是 promise

### 24. Store 存储在 Redux 中的意义是什么?

存储是一个 JavaScript 对象，它可以保存应用程序的状态，并提供一些帮助方法来访问状态、分派操作和注册侦听器，应用程序的整个状态/对象树保存在单个存储中

### 25. Redux 和 flux 有什么区别?

**Flux：**

1. Store 包含状态和更改逻辑
2. 有多个 Store
3. 所有 Store 都互不影响且是平级的
4. 有单一调度器
5. React 组件订阅 store
6. 状态是可变的

**Redux：**

1. Store 和更改逻辑是分开的
2. 只有一个 Store
3. 带有分层 reducer 的单一 Store
4. 没有调度器的概念
5. 容器组件是有联系的
6. 状态是不可改变的

### 26. vue 和 react 的区别

**虚拟 DOM：**

vue：计算出虚拟 DOM 的差异，在渲染的过程中跟踪每个组件的依赖关系，不会重新渲染整个组件树

react：当应用的状态改变时，重新渲染全部子组件，可以通过 shouldComponentUpdate 生命周期进行优化

**模板和 jsx：**

vue：具有单文件组件，可以把 html、css、js 写在一个 vue 文件里----MVVM 框架

react：依赖于 jsx，在 JavaScript 中创建 DOM----视图层框架

**数据绑定**

vue 是响应式的数据双向绑定系统，而 react 是单向数据流，没有双向绑定。

**应用**

vue 的语法较为简单，适用于小型项目创建，而 react 更适用于 Web 端和原生 App 的开发，侧重于大型应用。

**组件写法不一样**

react 推荐的做法是 JSX+inline style,也就是把 HTML 和 CSS 全都写进 javaScript 了

**state 对象**

state 对象在 react 应用中是不可变的，需要使用 setState 方法更新状态

在 vue 中，state 对象不是必须的，数据有 data 属性在 vue 对象中管理

**模板渲染方式的不同**

在表层上，模板的语法不同，React 是通过 JSX 渲染模板。而 Vue 是通过一种拓展的 HTML 语法进行渲染，但其实这只是表面现象，毕竟 React 并不必须依赖 JSX。

在深层上，模板的原理不同，这才是他们的本质区别：React 是在组件 JS 代码中，通过原生 JS 实现模板中的常见语法，比如插值，条件，循环等，都是通过 JS 语法实现的，更加纯粹更加原生。而 Vue 是在和组件 JS 代码分离的单独的模板中，通过指令来实现的，比如条件语句就需要 v-if 来实现对这一点，这样的做法显得有些独特，会把 HTML 弄得很乱

### 27. vue 和 react 的 diff 算法的区别

> vue 和 react 的 diff 算法，都是忽略跨级比较，只做同级比较。vue diff 时调动 patch 函数，参数是 vnode 和 oldVnode，分别代表新旧节点

- vue 比对节点，当节点元素类型相同，但是 className 不同，认为是不同类型元素，删除重建，而 react 会认为是同类型节点，只是修改节点属性

- vue 的列表对比，采用从两端到中间的比对方式，而 react 则采用从左到右依次比对的方式。当一个集合，只是把最后一个节点移动到了第一个，react 会把前面的节点依次移动，而 vue 只会把最后一个节点移动到第一个。总体上，vue 的对比方式更高效。

### 28. react 中的三种状态复用

- class 传统组件
- 高阶组件
- mixins 混入

### 29. 高阶组件 详解

[React 中的高阶组件及其应用场景](https://zhuanlan.zhihu.com/p/61711492?utm_source=wechat_session)

## 更多面试题

- [常见 css 的面试题](./css.md)
- [常见 html 的面试题](./html.md)
- [常见 javascript 的面试题](./javascript.md)
- [常见 typescript 的面试题](./typescript.md)
- [常见 vue 的面试题](./vue.md)
- [常见 webpack 的面试题](./webpack.md)
- [常见 node 的面试题](./node.md)
- [前端工程化](./eng.md)
- [优化相关](./optimize.md)
