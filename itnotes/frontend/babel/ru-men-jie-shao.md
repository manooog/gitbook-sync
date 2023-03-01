# 入门介绍

[Babel](https://babeljs.io/docs/en/) 是用来转换 JavaScripts 代码的工具，可以单独使用，也可以配合打包工具（如 webpack）使用。由于在开发阶段使用的都是较新语法，而不同浏览器对语法的兼容性不同，所以编写出的代码还需要经过转换，才能尽可能多的适配不同的工作环境。与 Babel 类似的还有 CSS 转换工具。

一般的开发脚手架都会配置好诸如 Babel 这样的代码转换工具，开发者无需关系工具的配置。但当你有个性化需求，就需要自行对 Babel 进行配置。

我在近期的工作中就遇到了这样的需求。

是这样的，我需要为公司平台网站编写一段 ServiceWorker 代码，编码阶段使用了ES6、ES7等规范中的语法，例如 Async/Await。通过网站查询可知，其兼容性如下：

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>红色表示不支持该语法</p></figcaption></figure>

如果需要在IE11中运行，那就必须将 Async 语法转换成更基础的代码。

下面，我会依次介绍实现过程。

### Babel 的两种用法

据我了解，使用 Babel 共有两种方式：

* 在 Node.js 环境下以 npm 模块方式引入
* 直接以命令行方式使用

集成在 webpack 内的属于第一种使用方式，用法如下：

```bash
npm install --save-dev @babel/core
```

```javascript
const babel = require("@babel/core");

babel.transformSync("code", optionsObject);
```

第二种方法，用法如下：

```sh
npm install --save-dev @babel/core @babel/cli

./node_modules/.bin/babel src --out-dir lib
```

两种方法都有对应的使用场景。

### 配置方式

Babel 好比一个厨师，不同的配置就像各式菜谱，能得出不同的结果。为了照顾不会调配菜谱的用户，社区也提供了一些调料包，让用户可以简单操作就能得到一盘符合自己口味的菜。

除此之外，Babel 团队还约定了非常多的方式，可以让用户根据自己的使用场景，将菜谱投喂给 Babel。（详见[文档](https://babeljs.io/docs/en/configuration#babelrcjson)）。

以下我以`babel.config.json` 为例继续介绍。首先，在项目根目录创建该文件。假如编译对象为 JS 文件，就可以使用`@babel/preset-env` 这个调料包，基本囊括了常用的配置：

```javascript
{
  "presets": [
    [
      "@babel/preset-env",
      {
        // ... preset-env 的配置
      }
    ]
  ]
}
```

