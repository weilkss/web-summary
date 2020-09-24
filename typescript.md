# web 前端面试题

想进大厂？首先基础得扎实，技术面试得过，你才能有机会和 hr 小姐姐谈工资

## typescript 篇

### 1. 什么是 Typescript?

TypeScript 是一种由微软开发和维护的免费开源编程语言。它是一个强类型的 JavaScript 超集，可编译为纯 JavaScript。它是一种用于应用级 JavaScript 开发的语言

### 2. TypeScript 和 JavaScript 有什么不同？

| TypeScript                         | JavaScript                                              |
| ---------------------------------- | ------------------------------------------------------- |
| 它是由网景公司在 1995 年开发的     | 它是 2012 年由安德斯·海尔斯伯格(Anders Hejlsberg)开发的 |
| JavaScript 源文件在`.js`扩展       | TypeScript 源文件是`.ts`扩展名                          |
| 它是解释语言，在运行时突出显示错误 | 它编译代码并在开发期间突出显示错误                      |

### 3. 我们为什么需要 TypeScript？

**我们需要 TypeScript:**

- TypeScript 快速、简单，最重要的是，容易学习。
- TypeScript 支持面向对象的编程特性，比如类、接口、继承、泛型等等。
- TypeScript 在编译时提供了错误检查功能。它将编译代码，如果发现任何错误，它将在运行脚本之前突出显示这些错误。
- TypeScript 支持所有 JavaScript 库，因为它是 JavaScript 的超集。
- TypeScript 通过使用继承来支持可重用性。
- TypeScript 使应用程序开发尽可能的快速和简单，并且 TypeScript 的工具支持为我们提供了自动完成、类型检查和源文档。
- TypeScript 支持最新的 JavaScript 特性，包括 ECMAScript 2015。
- TypeScript 提供了 ES6 的所有优点和更高的生产力。
- TypeScript 支持静态类型、强类型、模块、可选参数等。

### 4. 列出 Typescript 的一些特性

- 类
- 继承
- 接口
- 类型批注
- 箭头函数表达式(lambda 表达式)

### 5. 使用 Typescript 的一些优点?

- 它提供了可选静态类型的优点。在这里，Typescript 提供了可以添加到变量、函数、属性等的类型。
- Typescript 能够编译出一个能在所有浏览器上运行的 JavaScript 版本。
- TypeScript 总是在编译时强调错误，而 JavaScript 在运行时指出错误。
- TypeScript 支持强类型或静态类型，而这不是在 JavaScript 中。
- 它有助于代码结构。
- 它使用基于类的面向对象编程。
- 它提供了优秀的工具支持和智能感知，后者在添加代码时提供活动提示。
- 它通过定义模块来定义名称空间概念。

### 6. Typescript 的缺点是什么?

- TypeScript 需要很长时间来编译代码。
- TypeScript 不支持抽象类。
- 如果我们在浏览器中运行 TypeScript 应用程序，需要一个编译步骤将 TypeScript 转换成 JavaScript。
- Web 开发人员使用了几十年的 JavaScript，而 TypeScript 不是都是新东西。
- 要使用任何第三方库，必须使用定义文件。并不是所有第三方库都有可用的定义文件。
- 类型定义文件的质量是一个问题，即如何确保定义是正确的?

### 7. TypeScript 的不同组件是什么?

- 语言 language

  该语言由新语法、关键字、类型注释等元素组成，允许我们编写 TypeScript

- 编译器 compiler

  TypeScript 编译器是开源的、跨平台的，是用 TypeScript 编写的。它将用 TypeScript 编写的代码转换为 JavaScript 代码。它执行从 TypeScript 代码到 JavaScript 代码的解析和类型检查。它还可以帮助将不同的文件连接到单个输出文件，并生成源映射

- 语言服务 language service

  语言服务提供信息，帮助编辑器和其他工具提供更好的辅助功能，如自动重构和智能感知

### 8. Typescript 是谁开发的，目前稳定的 Typescript 版本是什么？

- typescript 是由 Anders Hejlsberg 开发的，他也是 c#语言开发团队的核心成员之一

- 目前稳定的 TypeScript 版本是 3.2，于 2018 年 9 月 30 日发布

### 9. 说说安装 Typescript 的最低要求?

至少要安装 `node` 和 `npm`

### 10. 列出在 Typescript 中的内置类型

- 数字类型：`number`
- 字符串类型：`string`
- 布尔类型：`boolean`
- Null 类型 ：`null`
- 未定义类型：`undefined`
- Void 类型：`void`
- 未知类型：`unknown`

### 11. Typescript 中的变量是什么？如何在 Typescript 中创建变量？

变量是存储位置，用于存储要被程序引用和使用的值/信息

我们可以通过以下四种方式之一声明一个变量:

- 在一条语句中声明类型和值。语法:var [identifier]: [type-annotation] = value;
- 声明没有值的类型。语法:var [identifier]: [type-annotation];
- 在没有类型的情况下声明它的值。语法:var [identifier] = value;
- 声明没有值和类型。语法:var(标识符);

### 12. 如何编译 Typescript 文件？

```shell
$ tsc helloworld.ts
```

编译成功后

`helloworld.js`

### 13. 是否可以将多个.ts 文件合并成一个.js 文件？如果是，那么如何做？

我们需要添加——outFILE [OutputJSFileName]编译选项

```shell
$ tsc --outFile comman.js file1.ts file2.ts file3.ts
```

上面的命令将编译所有这三个.ts 文件和结果将存储在一个 comman.js 文件中

```shell
$ tsc --outFile file1.ts file2.ts file3.ts
```

然后 file2.ts 和 file3.ts 将被编译，并将输出放在 file1.ts 中

### 14. 能否自动编译.ts 文件，并实时修改.ts 文件？

```shell
tsc --watch file1.ts
```

### 15. Typescript 的接口是什么意思？参照 Typescript 来解释它们

使用 `interface` 来定义接口

```js
interface interface_name {
  // 字段声明
  // 方法声明
}
```

接口只是声明方法和字段，它不能用来建造任何东西。不需要将接口转换为 JavaScript 来执行，它们对运行时 JavaScript 没有任何影响

### 16. 你如何理解 Typescript 中的类？列出类的一些特性

TypeScript 是一种面向对象的 JavaScript 语言，支持 OOP 编程特性，比如类、接口等。与 Java 一样，类是用于创建可重用组件的基本实体。它是一组具有公共属性的对象。类是创建对象的模板或蓝图。它是一个逻辑实体。“class”关键字用于在 Typescript 中声明一个类

**类的特征：**

- 继承
- 封装
- 多态性
- 抽象

17. JavaScript 不支持函数重载，但 TypeScript 是否支持函数重载？

TypeScript 支持函数重载。 但实施很奇怪。 当在 TypeScript 中执行函数重载时，我们只能实现一个具有多个签名的函数

```js

function demo(a:string,b:string):string

function demo(a:number,b:number):number

function demo(a:any,b:any){
    return a+b
}

```

### 18. 可以调试任何 TypeScript 文件吗？

要调试任何 TypeScript 文件，我们需要.js 源映射文件。因此，使用—sourcemap 标志编译.ts 文件以生成源映射文件

```shell
$ tsc -sourcemap file1.ts
```

### 19. 什么是 TypeScript Declare 关键字?

我们知道所有的 JavaScript 库/框架都没有 TypeScript 声明文件，但是我们希望在 TypeScript 文件中使用它们时不会出现编译错误。为此，我们使用 declare 关键字

### 20. 如何从任何.ts 文件生成 TypeScript 定义文件?

我们可以使用 tsc 编译器从任何.ts 文件生成 TypeScript 定义文件。它将生成一个 TypeScript 定义，使我们的 TypeScript 文件可重用

```shell
tsc --declaration file1.ts
```

### 21. interface 和 type 的区别

> 首先，在 ts 中，定义类型由两种方式：接口（interface）和类型别名（type alias）

- interface 只能定义对象类型，type 声明的方式可以定义组合类型，交叉类型和原始类型，如果用 type alias 声明的方式，会导致一些功能的缺失
- interface 方式可以实现接口的 extends/implements，而 type 不行
- interface 可以实现接口的 merge，但是 type 不行

## 更多面试题

- [常见 css 的面试题](./css.md)
- [常见 html 的面试题](./html.md)
- [常见 javascript 的面试题](./javascript.md)
- [常见 vue 的面试题](./vue.md)
- [常见 react 的面试题](./react.md)
- [常见 webpack 的面试题](./webpack.md)
- [常见 node 的面试题](./node.md)
- [常见 web 算法面试题](./algorithm.md)
- [前端工程化](./eng.md)
- [优化相关](./optimize.md)
