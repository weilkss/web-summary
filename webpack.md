# web 前端面试题

想进大厂？首先基础得扎实，技术面试得过，你才能有机会和 hr 小姐姐谈工资

## webpack 篇

### 1. 什么是 webpack？

webpack 是一个打包模块化 javascript 的工具，在 webpack 里一切文件皆模块，通过 loader 转换文件，通过 plugin 注入钩子，最后输出由多个模块组合成的文件，webpack 专注构建模块化项目

WebPack 可以看做是模块打包机：它做的事情是，分析你的项目结构，找到 JavaScript 模块以及其它的一些浏览器不能直接运行的拓展语言（Scss，TypeScript 等），并将其打包为合适的格式以供浏览器使用

### 2. 说几个常见的 loader？

- **file-loader：** 把文件输出到一个文件夹中，在代码中通过相对 URL 去引用输出的文件
- **url-loader：** 和 file-loader 类似，但是能在文件很小的情况下以 base64 的方式把文件内容注入到代码中去
- **source-map-loader：** 加载额外的 Source Map 文件，以方便断点调试
- **image-loader：** 加载并且压缩图片文件
- **babel-loader：** 把 ES6 转换成 ES5
- **css-loader：** 加载 CSS，支持模块化、压缩、文件导入等特性
- **style-loader：** 把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS。
- **eslint-loader：** 通过 ESLint 检查 JavaScript 代码
- **vue-loader：** 把 .vue 文件 代码转换成可阅读的代码

### 3. 说几个常见的 plugin？

- define-plugin：定义环境变量
- terser-webpack-plugin：通过 TerserPlugin 压缩 ES6 代码
- html-webpack-plugin 为 html 文件中引入的外部资源，可以生成创建 html 入口文件
- mini-css-extract-plugin：分离 css 文件
- clean-webpack-plugin：删除打包文件
- happypack：实现多线程加速编译

### 3. webpack 常见配置,6 个核心概念？

- **entry：** 入口,这是 Webpack 执行构建的第一步
- **chunk：** 代码块，一个 Chunk 由多个模块组合而成，它用于代码合并与分割
- **module：** 模块，在 Webpack 中一切皆模块，一个模块即为一个文件
- **loader** 在 resolve.rules 中配置 loader
- **plugin：** 配置插件，扩展功能
- **output：** 出口

- [更多配置](./webpack.config.md)

### 4. webpack 与 grunt、gulp 的不同？

gulp 和 grunt 需要开发者将整个前端构建过程拆分成多个 Task，并合理控制所有 Task 的调用关系，webpack 需要开发者找到入口，并需要清楚对于不同的资源应该使用什么 Loader 做何种解析和加工

### 5. webpack 有哪些优点

- 专注于处理模块化的项目，能做到开箱即用，一步到位
- 可通过 plugin 扩展，完整好用又不失灵活
- 使用场景不局限于 web 开发
- 社区庞大活跃，经常引入紧跟时代发展的新特性，能为大多数场景找到已有的开源扩展
- 良好的开发体验

### 6. webpack 的缺点

webpack 的缺点是只能用于采用模块化开发的项目

### 7. 分别介绍 bundle，chunk，module 是什么？

**bundle：** 是由 webpack 打包出来的文件

**chunk：** 代码块，一个 chunk 由多个模块组合而成，用于代码的合并和分割

**module：** 是开发中的单个模块

在 webpack 的世界，一切皆模块，一个模块对应一个文件，webpack 会从配置的 entry 中递归开始找出所有依赖的模块。

### 8. 分别介绍什么是 loader?什么是 plugin?

**loader：** 模块转换器，用于将模块的原内容按照需要转成你想要的内容

**plugin：** 在 webpack 构建流程中的特定时机注入扩展逻辑，来改变构建结果，是用来自定义

### 9. 什么 是模块热更新？

模块热更新是 webpack 的一个功能，他可以使得代码修改过后不用刷新浏览器就可以更新，是高级版的自动刷新浏览器

1. 配置 devServer

```js
devServer: {
  hot: true;
}
```

2. 通过命令行 加入 `--hot`

```js
"scripts":{
  "dev":"webpack --hot"
}
```

### 10. 什么是 Tree-shaking

Tree-shaking 可以用来剔除 javascript 中不用的死代码，它依赖静态的 es6 模块化语法，例如通过哦 import 和 export 导入导出，Tree-shaking 最先在 rollup 中出现，webpack 在 2.0 中将其引入，css 中使用 Tree-shaking 需要引入 Purify-CSS

### 11. 通过 webpack 处理长缓存

浏览器在用户访问页面的时候，为了加快加载速度，会对用户访问的静态资源进行存储，但是每一次代码升级或是更新，都需要浏览器去下载新的代码，最方便和简单的更新方式就是引入新的文件名称。在 webpack 中可以在 output 纵输出的文件指定 chunkhash,并且分离经常更新的代码和框架代码。通过 NameModulesPlugin 或是 HashedModuleIdsPlugin 使再次打包文件名不变

### 12. 如何提高 webpack 的构建速度

- 通过 externals 配置来提取常用库
- 使用 Happypack 实现多线程加速编译

  要注意的第一点是，它对 file-loader 和 url-loader 支持不好，所以这两个 loader 就不需要换成 happypack 了，其他 loader 可以类似地换一

- 使用 Tree-shaking 和 Scope Hoisting 来剔除多余代码
- 使用 fast-sass-loader 代替 sass-loader
- 优化构建时的搜索路径 善于用下 resolve.alias 别名

### 13. Webpack 构建流程

Webpack 在启动后，会从 Entry 开始，递归解析 Entry 依赖的所有 Module，每找到一个 Module，就会根据 Module.rules 里配置的 Loader 规则进行相应的转换处理，对 Module 进行转换后，再解析出当前 Module 依赖的 Module，这些 Module 会以 Entry 为单位进行分组，即为一个 Chunk。因此一个 Chunk，就是一个 Entry 及其所有依赖的 Module 合并的结果。最后 Webpack 会将所有的 Chunk 转换成文件输出 Output。在整个构建流程中，Webpack 会在恰当的时机执行 Plugin 里定义的逻辑，从而完成 Plugin 插件的优化任务

### 14. 做了哪些 Webpack 性能优化？

- 优化 Loader 的文件搜索范围
  ```js
  module.exports = {
    module:{
      rules:[
        {
          //js文件才使用babel
          test:/\.js$/,
          loader:'babel-loader',
          //只在src文件夹下查找
          include:[resolve('src')]，
          //不会去查找的路径
          exclude:/node_modules/
        }
      ]
    }
    }
  ```
- 把 Babel 编译过的文件缓存起来

  > 下次只需要编译更改过的代码文件即可

```js
loader: 'babel-loader?cacheDirectory=ture';
```

- HappyPack
  > 因为 Node 是单线程运行的，所以 Webpack 在打包的过程中也是单线程的，特别是在执行 Loader 的时候，这样会导致等待的情况
  > HappyPack 可以将 Loader 的同步执行转换为并行的
  ```js
  module:{
    loader:[
        {
          //js文件才使用babel
          test:/\.js$/,
          //只在src文件夹下查找
          include:[resolve('src')]，
          exclude:/node_modules/,
          //id后面的内容对应下面
          loader:'happypack/loader?id=happypack'
        }
    ]
    },
    plugins:[
      new HappyPack({
        id:'happypack',
        loaders:['babel-loader?cacheDirectory'],
        //开启4个线程
        threads:4
      })
    ]
  ```
- DllPlugin
  > DllPlugin 可以将特定的类库提前打包然后引入。这种方式可以极大的减少打包类库的次数，只有当类库更新版本才有需要重新打包，并且也实现了将公共代码抽离成单独文件的优化方案

```js
//单独配置在一个文件里
//webpack.dll.conf.js
const path = require('path');
const webpack = require('webpack');
module.exports = {
  entry: {
    //想统一打包的库
    vendor: ['react']
  },
  output: {
    path: path.join(__dirname, 'dist'),
    filename: '[name].dll.js',
    library: '[name]-[hash]'
  },
  plugins: [
    new webpack.DllPlugin({
      //name必须和output.library一致
      name: '[name]-[hash]',
      //该属性需要与DllReferencePlugin中一致
      context: __dirname,
      path: path.join(__dirname, 'dist', '[name]-mainfest.json')
    })
  ]
};
```

然后需要执行这个配置文件生成依赖文件，接下来需要使用 DllReferencePluhin 将依赖文件引入项目中

```js
//webpack.conf.js
module.exports = {
  //...省略其他配置
  plugins: [
    new webpack.DllReferencePlugin({
      context: __dirname,
      mainfest: require('./dist/vendor-mainfest.json')
    })
  ]
};
```

- Tree Shaking
  > Tree Shaking 可以实现删除项目中未被引用的代码

## 更多面试题

- [常见 css 的面试题](./css.md)
- [常见 html 的面试题](./html.md)
- [常见 javascript 的面试题](./javascript.md)
- [常见 typescript 的面试题](./typescript.md)
- [常见 vue 的面试题](./vue.md)
- [常见 react 的面试题](./react.md)
- [常见 node 的面试题](./node.md)
- [前端工程化](./eng.md)
- [优化相关](./optimize.md)
