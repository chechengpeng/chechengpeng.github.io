---
title: 深入剖析现代 JavaScript 应用
date: 2017-06-16 18:01:17
tags: [JavaScript, 翻译]
---
![A woman playing a life-size game of Operation; a metaphor for the many components of a modern JavaScript app](http://p0.qhimg.com/t01e14535b49b558b41.png)

_译者能力一般，水平有限，原汁原味请移步：[原文链接](https://www.sitepoint.com/anatomy-of-a-modern-javascript-application/)_

毫无疑问，JS 生态圈变化飞快。不仅仅新的工具与框架被快速的引入和开发，随着 ES2015（又名 ES6）的推出，JS 语言本身也经历了很大的变革。所以，已经有很多文章抱怨现在学习JavaScript 开发是多么的艰难。

在这篇文章中，我将为你介绍现代 JavaScript。我们将看到这门语言最近的发展，并大概了解一下最近编写前端 Web 应用常用的工具与技术。如果你刚开始学习这门语言，或者最近几年没有碰过它并且想知道跟之前相比JavaScript发生了多大的变化，那么这篇文章再好不过。

## 关于 Node.js

Node.js 是一个用 JavaScript 代码编写的服务端程序运行环境。这使得全栈 JavaScript 应用成为可能，应用的前后端用同一种语言编写。虽然这篇文章的重点在客户端开发，但 Node.js 仍然扮演了一个重要的角色。

Node.js 的出现对 JavaScript 生态圈产生了重大的影响，它引入了 npm 包管理工具并且推广了 CommonJS 模块规范。开发者开始发明更具创新性的工具和方法来模糊浏览器、服务器和原生应用之间的界限。

## JavaScript ES2015+

在 2005 年， 第六版 [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript)——制定 JavaScript 语言规范——以 [ES2015](http://www.ecma-international.org/ecma-262/6.0/)（也经常被称为 ES6）的名称发布。新版本添加的大量的特性使得在构建大型 Web 应用的时候更加的轻松和灵活。但是改进的脚步并没有在 ES2015 停止，每年都将发布一个新的版本。

### 变量声明

现在 JavaScript 有两种额外的方式用来声明变量：[**let** 和 **const**](https://www.sitepoint.com/how-to-declare-variables-javascript/)。

`let` 是 `var` 的继任 - 虽然 `var` 依旧可用，`let` 提供了它所声明时所在块的块级作用域（而不是函数作用域），这将减少出错的几率：

```
// ES5
for (var i = 1; i < 5; i++) {
  console.log(i);
}
// <-- 打印数字 1 到 4
console.log(i);
// <-- 5（变量 i 在循环外仍然存在）

// ES2015
for (let j = 1; j < 5; j++) {
  console.log(j);
}
console.log(j);
// <-- 'Uncaught ReferenceError: j is not defined'

```

使用 `const` 允许你定义一个不能被重新绑定到新值的变量。对像字符串和数字的原始值来说，结果与常量类似，一旦你声明一个值，你就不能改变它了。

```
const name = 'Bill';
name = 'Steve';
// <-- 'Uncaught TypeError: Assignment to constant variable.'

// Gotcha
const person = { name: 'Bill' };
person.name = 'Steve';
// person.name is now Steve. 
// As we're not changing the object that person is bound to, JavaScript doesn't complain.

```

### 箭头函数

箭头函数为声明匿名函数提供了一套简洁的语法，当函数体只有一个表达式的时候，省略了 `function` 关键字和 `return` 关键字。这使得可以用更好的方式来编写函数式代码。

```
// ES5
var add = function(a, b) {
  return a + b;
}

// ES2015
const add = (a, b) => a + b;

```

箭头函数另一个重要的特性是在被定义的上下文中他们继承了 `this` 的值

```
function Person(){
  this.age = 0;

  // ES5
  setInterval(function() {
    this.age++; // |this| refers to the global object
  }, 1000);

  // ES2015
  setInterval(() => {
    this.age++; // |this| properly refers to the person object
  }, 1000);
}

var p = new Person();

```

### 改进类的语法

如果你喜欢面向对象编程，你可能喜欢这门语言在基于原型的基础上对类的扩展。虽然它只是语法糖，但对那些试图通过原型来效仿经典的面向对象的开发者来说，它提供了更简洁的语法。

```
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

```

### Promises / Async 函数

JavaScript 的异步特性是长期以来的挑战：当处理像 Ajax 请求这种事情的时候，任何复杂一点的应用都有陷入回调地狱的风险。

幸好，ES2015 用 [promises](https://www.sitepoint.com/deeper-dive-javascript-promises/) 提供了原生支持。Promises 代表着当前不存在但随后可能会存在的值，使得对异步函数调用的管理更加可控，而不必使用多层嵌套回调。

ES2017（今年推出）采用了 [async 函数](https://www.sitepoint.com/simplifying-asynchronous-coding-async-functions/)（参考了 async/await 使得这种情况有所改善，允许用同步的方式处理异步代码）。

```
async function doAsyncOp () {
  const result = await asynchronousOperation();     
  console.log(result);
  return result;
};

```

### 模块

ES2015 增添的另外一个突出特性是一个原生的模块规范，使得模块的定义和使用成为这门语言的一部分。之前模块的加载只能通过第三方类库的方式。在下一节，我们将深入了解一下模块。

其他的特性我们不会在这里讨论，但我们已经顾及到了一些，当学习现代 JavaScript 时，可能会遇到的主要区别。在 [Babel site](https://babeljs.io/) 的 [Learn ES2015](https://babeljs.io/learn-es2015/) 页面上，你能得到完整的实例清单，并且你可能会找到一些有用的东西来帮你了解这门语言的最新特性。这些特性包括模板字符串，迭代器，生成器，像映射和集合新的数据结构等等。

> 想学习 ES2015 的更多内容，关注我们的收费课程: [Diving into ES2015](https://www.sitepoint.com/premium/courses/diving-into-es2015-2924)

### 代码检查

检查器是解析你的代码并对比是否违反一系列规则，检查语法错误，格式化和最佳实践的工具。虽然对每个人来说都推荐使用检查器，但它对新手来讲更加有用。当正确配置了代码编辑器或集成开发工具后，当正在学习一门新的语言特性时，你能得到及时的反馈来确保没有遇到语法错误。

你可以[查看 ESLint](https://www.sitepoint.com/up-and-running-with-eslint-the-pluggable-javascript-linter/)，它是最流行的之一并且支持 ES2015+。

## 模块化编程

现代 Web 应用有几千（甚至几十万）行代码。如果没有一个通过较小组件，模块化的代码和必要的代码复用进行组合的机制，在这样的代码量下工作几乎是不可能的。这就是模块的工作。

### CommonJS 模块

有些模块规范已经出现几年了，最流行的一个是 [CommonJS](https://en.wikipedia.org/wiki/CommonJS)。它是 Node.js 的默认模块规范，可以通过模块绑定的协助用在客户端，一会儿我们将讨论它。

它通过一个 `module` 对象来输出来自于一个 JavaScript 文件的功能，并且通过一个 `require()` 函数来引入你所需要的功能。

```
// lib/math.js
function sum(x, y) {
  return x + y;
}

const pi = 3.141593

module.exports = {
  sum: sum,
  pi: pi
};

// app.js
const math = require("lib/math");

console.log("2π = " + math.sum(math.pi, math.pi));

```

### ES2015 模块

ES2015 采用了在语言中定义和使用组件的方法，之前可能只用在第三方类库中。你能根据你想要的功能来编写单独的文件并且只输出可用于应用的那一部分。

> **Note**: 原生浏览器对 ES2015 模块的支持还在开发中，所以当前你需要一些额外的工具的帮助才能使用它们。

这有一个例子:

```
// lib/math.js

export function sum(x, y) {
  return x + y;
}
export let pi = 3.141593;

```

我们有输出一个函数和一个变量的模块。我们可以将该文件包含在另外一个文件中并且使用这些输出的函数。

```
// app.js

import * as math from "lib/math";

console.log("2π = " + math.sum(math.pi, math.pi));

```

或者我们也可以指定和只引入我们需要的

```
// otherApp.js

import {sum, pi} from "lib/math";

console.log("2π = " + sum(pi, pi));

```

这些例子摘录于 [Babel website](https://babeljs.io/learn-es2015)。想要深入了解，请查看 [Understanding ES6 Modules](https://www.sitepoint.com/understanding-es6-modules/)。

## 包管理

长期以来，其他语言都有它们自己的包存储和管理工具，使得寻找和安装第三方类库与组件非常的容易。Node.js 有它自己的包管理和仓库， [npm](https://www.sitepoint.com/beginners-guide-node-package-manager/)。虽然也有其他可用的包管理工具，但 npm 已经成为事实上的 JavaScript 包管理工具并且据说有着世界上最大的包注册量。

在 [npm 仓库](https://www.npmjs.com/)，通过一个单独的 `npm install` 命令就能把想要的第三方模块轻易下载到并使用在项目中。这个包下载到本地 `node_modules` 目录，其中包含了所有的包和它们各自的依赖包。

你下载的包可作为依赖被注册在项目中的 [package.json](https://docs.npmjs.com/files/package.json) 文件中，以及项目或模块（在 npm 上它本身可以当做一个包发布）的有关信息。

你能为开发环境和生产环境分别定义依赖包。生产依赖包为工作需要，开发依赖包只对开发者是必需的。

**package.json 文件示例**

```
{
  "name": "demo",
  "version": "1.0.0",
  "description": "Demo package.json",
  "main": "main.js",
  "dependencies": {
    "mkdirp": "^0.5.1",
    "underscore": "^1.8.3"
  },
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Sitepoint",
  "license": "ISC"
}

```

## 构建工具

我们开发现代 Web 应用时所写的代码跟将要用在生产环境中的几乎从来不一样。我们编写的最新版 JavaScript 代码可能不被浏览器所支持，我们需要大量使用那些在 `node_modules` 文件夹中第三方包以及它们各自的依赖，我们有静态分析工具或压缩工具等等。构建工具的出现帮助我们把这些转换成更有部署效率并且可以被大多数 Web 浏览器执行的代码。

### 模块打包

当使用 ES2015/CommonJS 模块编写简洁，可复用的代码时，我们需要加载这些模块的方法（至少直到原生浏览器支持 ES2015 模块加载）。HTML 中包含一堆脚本标签对任何严肃的应用来说真不是一个可行的选择，这将很快变得笨重起来，并且所有这些分离的 HTTP 请求将会影响性能。

我们可以使用 ES2015 的 `import` 命令（或CommonJS的 `require`）把我们需要的全部模块引入进来并且通过一个模块打包工具把这些模块组合成一个或多个文件（打包）。我们会把这个打包好的文件上传至服务器并且包含在 HTML 文件中。它将包含你引入的所有模块和它们必需的依赖。

时下有几个热门的选择，最流行的有 [Webpack](http://webpack.js.org), [Browserify](http://browserify.org) 和 [Rollup.js](http://rollupjs.org)。你可根据你的需求，任选一个。

> 如果你想深入学习模块打包机制和如何适应更大规模的应用开发，推荐阅读 [Understanding JavaScript Modules: Bundling & Transpiling](https://www.sitepoint.com/javascript-modules-bundling-transpiling/)。

### 转换编译

虽然[现代浏览器对 ES2015 的支持很好](http://kangax.github.io/compat-table/es6/)，但你的目标用户可能包括低版本浏览器和部分不支持设备的使用者。

为了让现代 JavaScript 代码执行，我们需要把我们所写的代码转化成功能一样的早期版本（通常是 ES5）。执行此项任务的标准工具是 [Babel](https://babeljs.io)；一个把你的代码转换成兼容大多数浏览器的编译器。这样你就不必等着供应商去实现所有的这一切，现在就可以使用现代 JS 的所有特性。

有一些特性仅仅靠语法转换实现不了；Babel 有一个 [Polyfill](http://babeljs.io/docs/usage/polyfill/)， 可以帮助模拟一些更复杂的特性，像 Promises。

### 构建系统和任务自动化

模块打包和转换编译只是我们项目所需要的构建过程中的两步。其他的像代码压缩（为了减小文件大小），分析工具，和一些与 JavaScript 无关的任务，像图像优化和 CSS/HTML 预处理。

任务管理成为一件比较费事的事情，并且我们需要一个自动化的方式来处理它，通过一些简单的命令就能执行所有的一切。最流行的两个工具是 [Grunt.js](http://gruntjs.com) 和 [Gulp.js](http://gulpjs.com)，它们提供了一个方法来把你的任务有序的组成一组。

例如，你能通过一个像 `gulp build` 的命令执行一个代码检查器，Babel 的编译过程和 Browserify 的模块打包过程。而不必按顺序记住三个命令和相关参数，我们只执行可以自动化处理全部过程的一个命令而已。

当你发现需要自己手动处理一些项目中的步骤，考虑它是否能通过任务工具自动化执行。

> **扩展阅读**: [An Introduction to Gulp.js](https://www.sitepoint.com/introduction-gulp-js/)

## 应用架构

跟网站相比，Web 应用有不同的需求。例如，页面重载对一个博客来说可能可以接受，但对应用来说一定不是这样，比如 Google Docs。你的应用应该尽可能表现的像一个桌面应用，否则，可用性将大打折扣。

老式的 Web 应用通常通过 Web 服务器发送几个页面来完成，当需要很多动态变化的时候，根据用户的操作通过 Ajax 替换 HTML 块来加载内容。虽然对动态网页来说，这是一个很大的进步，但它仍有其局限性；用户的每一步操作都要发送 HTML 片段或者整个页面是一种资源的浪费，尤其是从用户的角度来看。可用性仍然达不到桌面应用的响应速度。

为了改善这种状况，我们发明了一种创建 Web 应用的新方法，通过客户端和服务端通信的方式呈现给用户。虽然应用对 JavaScript 需求量大大提高，结果是应用现在的表现跟原生的非常接近；没有页面重载和我们点击按钮时的长时间等待。

### 单页应用

Web 应用最普通的高级架构被称作 [SPA](https://en.wikipedia.org/wiki/Single-page_application)， _Single Page Application_ 的简写。SPAs 是包含了应用可以正确工作所需的 JavaScript 的大块的集合。界面完全在客户端渲染，所以不需要重新加载。唯一需要变化的东西是应用中的数据，通常通过 [Ajax](https://en.wikipedia.org/wiki/Ajax_(programming)) 的远程 API 或者其他的异步通信方法来处理。

这种方式的一个缺点就是应用首次加载需要耗费很长时间。一旦它完成加载，那么，页面之间的切换将非常流畅，因为只是纯数据在客户端和服务端间传递。

### 通用/同构 应用

虽然 SPAs 提供了很好的用户体验，但取决于你的需求，它们可能不是最佳的解决方案。尤其是你是否需要更快的初始响应时间或者搜索引擎优化。

有一个相当接近的办法来解决这些问题叫 [同构](http://isomorphic.net/javascript) (或 通用) JavaScript 应用。在这种类型的架构下，大部分代码在服务端和客户端都可以执行。你可以选择在服务端渲染用来获得更快的首屏加载速度，在这之后，用户和应用之间的交互通过客户端来渲染。因为页面最初在服务端渲染，所以搜索引擎可以正确的拿到索引。

## 部署

现代 JavaScript 应用中，编写的代码和部署到生产环境的代码是不一样的；你只部署构建过程生成的文件。完成这项工作的流程取决于项目的大小，开发人员的数量和使用的工具与类库。

例如，如果你独自编写一个小型项目，每次部署只需要执行构建过程并且上传所生成的文件到 Web 服务器。记住，你只需要上传一个包含了整个应用和依赖的，通过构建过程（转换编译，模块打包，代码压缩等）生成的单个`.js`文件。

你的目录结构可以这样实现：

```
├── dist
│   ├── app.js
│   └── index.html
├── node_modules
├── src
│   ├── lib
│   │   ├── login.js
│   │   └── user.js
│   ├── app.js
│   └── index.html
├── gulpfile.js
├── package.json
└── README

```

使用 ES2015 编写的应用文件在`src`目录，通过 npm 安装外部包，自己的模块在`lib`目录下。

然后你可以运行 Gulp，它将会执行`gulpfile.js`中的指令来构建你的项目：打包模块为一个文件（包括通过npm安装的），转换 ES2015+ 到 ES5，压缩生成的文件等。然后你能配置它生成文件到`dist`目录。

> **Note**: 如果你有不需要做任何处理的文件，可以只把它们从`src`下复制到`dist`目录。你也能通过在构建系统中配置任务来完成这个过程。

现在你可以只上传`dist`目录中的文件到 Web 服务器，不必担心剩下的文件，它们只对开发有用。

### 团队开发

如果你跟其他开发者共同开发，你可能也正在使用一个共享的代码库，像 GitHub，来保存你的项目。在这种情况下，你可在提交之前执行构建过程并把生成的文件上传到 Git 仓库，稍后把它下载到生产服务器。

然而，如果多名开发者一起开发时，保存生成的文件到仓库容易出错，并且你也希望保持代码整洁。幸运的是，有个更好的方法来处理这种情况：你可在构建过程中开启一个像 [Jenkins](http://jenkins.io), [Travis CI](http://travis-ci.org), [CircleCI](http://circleci.com) 等这样的服务，这样在每次有新的提交推送到仓库之后，它都可以自动构建你的项目。开发者只关心推送更改的代码而不必每次都构建这个项目，并且自动生成的文件也和仓库保持干净，最后，你仍然有可用的生成文件用来部署。

## 结论

如果近几年你没有接触 Web 开发，那么从简单的 Web 页面到现代 JavaScript 应用之间的转变看起来是令人生畏的，但我希望这篇文章作为一个起点来说是有用的。每个话题我都尽可能的链接了更深入的文章，所以你可以进一步了解。

并且牢记，如果有时候在了解了全部可用选项之后，所有的一起都看起来还是混乱不堪；那就想想 [KISS 准则](https://en.wikipedia.org/wiki/KISS_principle)，并且只用你认为你需要的而不是所有可用的。最终，解决问题才是最重要的，而不是使用最新的东西。

你是如何学习现代 JavaScript 开发的？有没有我还没提到而你想了解的东西？我希望在评论里听到你的声音。

### 作者的更多文章

*   [Create Your Own Yeoman-Style Scaffolding Tool with Caporal.js](https://www.sitepoint.com/scaffolding-tool-caporal-js/?utm_source=sitepoint&utm_medium=relatedinline&utm_term=&utm_campaign=relatedauthor)

*   [How to Build and Structure a Node.js MVC Application](https://www.sitepoint.com/node-js-mvc-application/?utm_source=sitepoint&utm_medium=relatedinline&utm_term=&utm_campaign=relatedauthor)
                
