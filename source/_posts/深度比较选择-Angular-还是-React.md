---
title: 深度比较选择 Angular 还是 React
date: 2017-06-07 18:00:04
tags: [JavaScript, 翻译]
---
![Two knights jousting, with React and Angular logos on their shields](http://p0.qhimg.com/t01f5158142a5d7c41c.png)

_译者水平有限，原汁原味请移步：[原文链接](https://www.sitepoint.com/react-vs-angular/)_

应该选择 Angular 还是 React？现在JS框架两强的格局让许多开发者选择起来很纠结。无论你是一个正在思考如何入门的新手，还是一个为下个项目挑选框架的设计者，或是一个架构师为公司做长远的规划，你都有可能从学习这个主题中受益。

为了节省你的时间，提前做出如下声明：在哪个框架更好这个问题上，本文不会给你一个明确的答案。但是，不想其他类似主题的文章。我不能告诉你答案，是因为一项特定的技术是否适合你的开发环境和使用场景取决于多种因素。

由于不能直接回答这个问题，我们会尝试从其他的方面进行解释。我们将会通过对比 Angular（2+，不是老版本的AngularJS）和 React 来演示在两个类型相似的框架中，如何选择并调试适合自己环境的框架。你知道的，“授人以鱼不如授人以渔”。这样在以后，当这两者被更好的框架取代的时候，你能再次用同样的思路做出最优的选择。

## 开始

在选择任何工具之前，你都需要回答两个简单的问题：“它本身是好的工具吗？”，“它是否适合我的使用场景？”他们本身没有什么意义，所以你需要把这两个问题时刻放在脑海中。好吧，问题可能不是那么的简单，所以，我们尝试把他们分解成一些小的问题。

工具本身的问题：

* 它的成熟度如何以及背后支持它的是谁？
* 它有什么样的特性？
* 它使用什么样的架构，开发范式，和模式？
* 围绕它的生态圈怎么样？

自我反思的问题：

* 我和我的同事能否轻松的学会如何使用它？
* 它适合我的项目吗？
* 它的开发体验怎么样？

用这一系列问题，你可以评估任何工具，而我们将以 Angular 和 React 为基础进行比较。

还有另外一件事我们需要说明。严格来说，拿 Angular 比较 React 不是完全公平的，因为 Angular 是一个成熟、功能完备的框架，而 React 只是一个 UI 组件库。为了弥补差距，我们谈论 React 的时候，包含了一些它经常使用的库。

## 完备性

作为一个熟练开发者的主要能力就是能够在旧技术和前沿技术之间保持平衡。惯例是，当采用还未成熟的新工具时，应注意一些风险：

* 工具可能有缺陷并且不稳定
* 它可能会被供应商意外的抛弃
* 假设你需要帮助，可能没有一个大型的知识库或者成熟的社区

React 和 Angular 都有良好的出身，所以从这方面来看，我们是没必要担心的。

### React

React 是由 Facebook 开发并维护的，并且用在了他们自己的产品线上， [包括 Instagram 和 WhatsApp](https://github.com/facebook/react/wiki/sites-using-react). 它已经出现大约 [3年半](https://facebook.github.io/react/blog/2013/06/05/why-react.html) 了， 所以它已经不算新了。它也是Github上[最流行的库之一](https://github.com/search?q=stars:%3E1&s=stars&type=Repositories) ，在撰写本文的时候，它大约有60,000多个 star。听起来不错。

### Angular

Angular（2及以上）出现的比 React 晚一点，但是如果算上之前的版本 AngularJS，情况就反过来了。它主要由 Google 维护并且用在[AdWords 和 Google Fiber](http://angularjs.blogspot.com/2015/11/how-google-uses-angular-2-with-dart.html) 产品上，很明显他们对此很有信心，显然它不会短时间内消失。

## 特性

像前文提到的，Angular 比 React 多些开箱即用的特性。这是有两面性的，取决于你看待它的角度。
两者的核心功能是相似的：组件，数据绑定和平台无关的渲染

### Angular

Angular 提供了很多现代 web 应用所需的开箱即用的特性。一些标准特性是：

* 依赖注入
* 以 HTML 的扩展版本为基础实现模板
* 由 @angular/router 提供路由功能
* 利用 @angular/http 实现 Ajax 请求
* 利用 @angular/forms 创建表单
* CSS 组件化
* XSS 防御
* 单元测试组件

当你自己不想花费时间去挑选类库的时候，有这么多开箱即用的特性是很方便的。 而这也意味着你被它们束缚在了一起，即使你不需要它们。并且，通常替换它们需要付出更多的努力。例如，考虑到依赖注入可以用引入来替代，我们相信使用它的小的项目相对于收益会付出更多的开销。

### React

使用 React，你的入门更加简单。如果我们只看 React，那么只有：

* 无依赖注入
* JSX模板，通过 JavaScript 实现的类 XML 语言
* XSS 防御
* 单元测试组件

特性不多，未必不是好事。这意味着根据需求选择第三方类库的时候，你有更多的自由度。不好的是你不得不自己做出选择。经常与 React 一起使用的流行类库有：

* 路由 [React-router](https://reacttraining.com/react-router/)
* HTTP请求 [Fetch](https://developer.mozilla.org/en/docs/Web/API/Fetch_API) (or [axios](https://github.com/mzabriskie/axios))
* CSS 封装 [wide variety of techniques](https://github.com/MicheleBertoli/css-in-js)
* 额外的单元测试工具 [Enzyme](https://github.com/airbnb/enzyme)

我们拥有了选择类库时的自由。这让我们可以根据每个项目的特定需求来调整我们的技术栈，并且不会产生很高的学习成本。

## 语言、范式和模式

回顾一下两个框架的特性，让我来看一下有哪些流行的高级概念。

### React

当研究 React 的时候，有一些重要的概念涌上心头：JSX，Flow，Redux

#### JSX

许多开发者对 [JSX](https://facebook.github.io/react/docs/introducing-jsx.html) 持不同的看法：有的人喜欢它，有的人认为这是技术的巨大退步。不是遵循内容与逻辑分离的传统方法，React 决定用一种类 XML 语言把两者组合在一起放到组件中，这样你可以在 JavaScript 代码中直接编写内容标记。

虽然关于标记和逻辑混合写法这个话题是有争议的，但是它有一个明显的优势：静态分析。如果你的 JSX 标记中有错误，编译器不会保持沉默，它会报出这个错误。这能帮助我们立即发现拼写错误和其他一些愚蠢的错误。

#### Flow

[Flow](https://flow.org/)也是由 Facebook 开发的一款 JavaScript 的类型检查工具。它能解析代码并检查一些常规的类型错误，像隐式转换或空引用。

不像有着相似目的的 TypeScript，它不需要你迁移到一个新语言并且通过注释你的代码来进行类型检查。对 Flow 来说，类型注释是可选的，可以当做分析器的额外提示。如果你想用静态代码分析，但又不想重写已有的代码，对此而言 Flow 是一个不错的选择。

[**扩展阅读**: [Writing Better JavaScript with Flow](https://www.sitepoint.com/writing-better-javascript-with-flow/)]

#### Redux

[Redux](http://redux.js.org/) 是一个清晰的管理状态变化的类库。它受 [Flux](http://facebook.github.io/flux/) 的启发，但是做了一些简化。Redux 的核心思想是用单个对象来代表应用的整个状态，该对象被叫做 reducers，通过函数实现。reducers 是纯函数，通过组件分别实现。这能更好的做到关注点与测试分离。

如果你正在做一个简单的项目，引入 Redux 可能会更加复杂，但是对中大型项目来说，它是一个很好的选择。这个类库变得非常流行，也可以用在 Angular 项目中实现。

所有的三项特性可以显著的增强你的开发体验：JSX 和 Flow 允许你快速的定位潜在错误，Redux 帮助你搭建一个整洁的项目架构。

### Angular

Angular 也有一些有趣的东西，叫 TypeScript 和 RxJS。

#### TypeScript

[TypeScript](https://www.typescriptlang.org/) 是一门在 JavaScript 基础上，由微软开发的新语言。他是 ES2015 的超集，并且包含了JS语言即将到来的新版本的一些特性。你能用它替代 Babel 来编写最新的 JavaScript。它也提供了一个极其强大的类型检查系统，能够通过注释和类型推理静态分析你的代码。

还有一个相当微妙的优势。TypeScript 受 Java 和 .NET 的影响很深，所以如果开发者有那些语言背景，他们会发现 TypeScript 比原生 JavaScript 学起来更轻松（注意我们如何根据个人情况选择工具）。虽然 Angular 是第一个采用 TypeScript 的主要框架，但它和 React 用在一起，也是可行的。

[**扩展阅读**: [An Introduction to TypeScript: Static Typing for the Web](https://www.sitepoint.com/introduction-to-typescript/)]

#### RxJS

[RxJS](http://reactivex.io/rxjs/) 是一个响应式的编程类库，允许对异步的操作和事件做更加灵活的处理。它是利用函数式编程把观察者模式和迭代器模式混合的组合体。RxJS 允许你把一切都当做是一个连续的流值，并且在此之上实现各种各样的操作，像映射，过滤，拆分或合并。

该类库被 Angular 的 HTTP 模块采用，也在一些内部使用。当你执行一个 HTTP 请求，它返回一个 Observable 替代通常的 Promise。虽然这个库极其强大，但它也相当的复杂。想要精通它，你需要知道不同类型的 “观察者”，“主题” ，以及[上百种方法和操作符](http://reactivex.io/rxjs/manual/overview.html#operators)。呀，这看起来只是执行 HTTP 请求的一点小工作。

当需要很多连续的数据流方面的工作的时候，比如 web sockets，在这种情况下 RxJS 是十分有用的，然而，这看起来仍然很复杂。无论如何，当使用 Angular 的时，你至少要对此要有基本的了解。

[**扩展阅读**: [Introduction to Functional Reactive Programming with RxJS](https://www.sitepoint.com/functional-reactive-programming-rxjs/)]

我们发现在提高项目的可维护性上，TypeScript 是一个强大的工具，尤其是那些代码量巨大或业务逻辑十分复杂的项目。用 TypeScript 写的代码更容易阅读与跟进。虽然 Angular 已经采用了 TypeScript，我们仍然希望更多的项目使用它。RxJS，换句话说，看起来只在特定情况下有用并且要小心使用。否则，它能给你的项目带去难以想象的复杂度。

## 生态圈

关于开源框架很重要的事情是围绕它而衍生出的工具数量。有时候，那些工具甚至比框架本身更有用。我们来看一下这两个框架最流行的工具和类库。

### Angular

#### Angular 命令行工具

现代框架的流行趋势是通过一个命令行工具来帮助初始化项目，而不必亲自配置。Angular 的工具叫 [Angular CLI](https://cli.angular.io/)。它允许通过一系列的命令来生成和启动项目。所有与创建应用，启开发环境，跑测试有关的脚本都被巧妙的隐藏在叫 `node_modules` 的文件夹中。你也能在开发期间通过它生成新的代码。这使得创建新项目十分的简单。

[**扩展阅读**: [The Ultimate Angular CLI Reference](https://www.sitepoint.com/ultimate-angular-cli-reference/)]

#### Ionic 2

[Ionic 2](http://ionic.io/2) 是一款用来开发移动端混合应用的流行框架的新版本。它提供了一个完美集成了 Angular 2 的 Cordova 容器，和一个漂亮的组件库。通过它，可以轻松的创建移动端应用。如果相比原生应用更倾向于混合应用，那么它将是一个不错的选择。

#### Material design 组件

如果你钟爱于 material design，你可能很高兴听到 [Material 组件库](https://material.angular.io/)可以用于 Angular。虽然当前得到了诸多支持，但其仍然处于早期阶段并且有点简陋，所以，我们希望不久的将来能有所改善。

#### Angular universal

[Angular universal](https://github.com/angular/universal) 是一个种子项目，被用来创建支持服务端渲染的项目。

#### @ngrx/store

[@ngrx/store](https://github.com/ngrx/store) 是受 Redux 启发，利用 pure reducers 基于状态突变，用于 Angular 状态管理的类库。通过集成 RxJS，可以利用变化侦测策略达到更好的性能。

[**扩展阅读**: [Managing State in Angular 2 Apps with ngrx/store](https://www.sitepoint.com/managing-state-angular-2-ngrx/)]

> 这里有更多的类库与工具 [the Awesome Angular list](https://github.com/AngularClass/awesome-angular).

### React

#### Create react app

[Create-react-app](https://github.com/facebookincubator/create-react-app) 是用于快速创建 React 项目的命令行工具。跟 Angular CLI 相似，它允许生成一个新项目，启动开发服务和打包。它用 [Jest](https://www.sitepoint.com/test-react-components-jest/) 做单元测试，一款来自于 Facebook 的比较新的测试工具，本身有一些好的特性。它也支持通过环境变量做灵活的应用分析，本地环境的后端代理，Flow，和其他特性。更多内容请查看 [introduction to create-react-app](https://www.sitepoint.com/create-react-app/)

#### React Native

[React Native](https://facebook.github.io/react-native/) 是由 Facebook 开发的，用 React 编写移动端原生应用的平台。不像提供混合应用的 Ionic，React Native 提供真正的原生界面。它提供了一套用于绑定原生控件的标准 React 组件。也允许使用Objective-C，Java 或 Swift等原生代码编写的组件绑定到它们上。

#### Material UI

同样，这是用于 React 的 [material design 组件库](http://www.material-ui.com)。跟 Angular 的版本相比，这个更加成熟并且已经有很多可用的组件。

#### Next.js

[Next.js](https://github.com/zeit/next.js/) 是用于 React 应用在服务端渲染的框架。它提供了一个灵活的方式在服务端全部或部分渲染应用，返回结果给客户端并继续保持在浏览器中。它尝试完成一项复杂的任务，尽可能简单的创建一个通用应用，所以设置也被设计的尽可能简单。

#### MobX

[MobX](https://github.com/mobxjs/mobx) 是一个管理应用状态的可选库。代替在一个单一稳定的仓库中保存状态，就像 Redux 所做的，它鼓励你尽量存储所必须的最小状态并且推导出剩下的。它提供了一套修饰符来定义可见性和观察者和介绍状态的逻辑变化。

[**扩展阅读**: [How to Manage Your JavaScript Application State with MobX](https://www.sitepoint.com/manage-javascript-application-state-mobx/)]

#### Storybook

[Storybook](https://getstorybook.io/) 是 React 的组件开发环境。它允许快速的创建单个应用来展示你的组件。在此基础上，它还提供了许多组件来记录，开发，测试和设计你的组件。在应用的其他部分，我们发现它在独立开发组件上是极其有用的。在上一篇文章中，你能学到 [关于 Storybook 的更多知识](https://www.sitepoint.com/react-storybook-develop-beautiful-user-interfaces-with-ease/)。

> 这里有更多的类库与工具 [the Awesome React list](https://github.com/enaqx/awesome-react).

## 接受度，学习曲线和开发体验

选择一项新技术的重要标准就是学习它有多么的容易。当然，答案取决于很多因素，比如你之前的经验，熟悉相关的概念和模式。不管怎样，给定一个框架我们仍然能评估必须学习的新东西的数量。现在，我们假设你已经了解 ES6+，构建工具和所有的这些，让我们看看你还必须要理解什么。

### React

使用 React 遇到的第一个障碍就是 JSX。对有些开发者而言，它写起来颇为棘手，然而，它并没有增加太多的复杂性；就像真正的  JavaScript 表达式，和特殊的类 HTML 语法。你也需要学习如何编写组件，用属性来配置和管理内部状态。你不需要学习任何新的逻辑结构与循环，因为所有的这些都是原生 JavaScript。

[官方教程](https://facebook.github.io/react/docs/hello-world.html)是入门 React 的优秀资源。一旦你完成了它，那么[开始熟悉路由](https://reacttraining.com/react-router/web/guides/quick-start)。React 路由 v4 版本可能有一些复杂和特别，但无需担心。使用 Redux 需要转变范式，学会利用类库建议的方式完成已经熟悉的任务。免费视频教程 [Getting Started with Redux](https://egghead.io/courses/getting-started-with-redux) 能够帮助你快速熟悉一些核心概念。根据项目的大小和复杂度你可能不得不寻找和学习一些额外的类库，这可能是比较棘手的部分，但在这之后，一切都会顺风顺水。

我们很惊喜入门 React 是如此的简单。甚至有后端经验和前端经验有限的人都能快速上手。有完善清晰的错误提示，并且提供了如何解决潜在问题的解释说明。最难的部分可能就是为所需功能寻找合适的类库，但构建和开发一个应用真的十分简单。

### Angular

学习 Angular 需要比 React 了解更多的概念。首先，你需要熟悉 TypeScript。对于有静态类型语言像 Java 或 .NET 使用经验的开发者来说要比 JavaScript 更好理解，但对纯 JavaScript 开发者而言，可能需要付出一些努力。

框架背身就有很多主题需要学习，从基础的开始像模块、依赖注入、装饰器、组件、服务、管道、模板和指令，到高级主题像变化侦测、区块、AoT编译和 RxJS。这些此[文档](https://angular.io/docs/ts/latest/quickstart.html)中都可以找到。RxJS 本身就是很繁重的主题，在[官方网站](http://reactivex.io/)上有更多的描述。虽然从基础水平上使用它比较容易，但要使用高级主题会十分的复杂。

总而言之，我们注意到使用 Angular 要比 React 难得多。眼花缭乱的新概念对新手来讲十分的困惑。即使你已经入门了，你也需要时刻注意像 RxJS 订阅管理，变化侦测性能和[未知的东西](https://angular.io/docs/ts/latest/guide/template-syntax.html)（是的，这是来自文档实际建议）。我们会经常遇到难以理解的错误信息，所以不得不经常检索它们并祈求得到一个精准的匹配。

这看起来好像我们更倾向于 React，的确是。结合我们利用同样大小和复杂度的 Angular 和 React 项目，对新手开发者进行培训的经验，React 更加的顺滑。但是，像我之前所说的，这取决于多种因素，可能对你来说会有所不同。

## 契合度

你可能已经注意到每个框架都有它本身一系列的功能，有好的也有坏的。但在特定环境外的分析已经完成并且没能在选择哪个框架上给出答案。为了做出决定，你不得不从你自己项目的角度来考查它。这些事情需要你自己来做。

现在，结合你的项目试着回答下面这些问题，顺便想想是否符合关于这两个框架你已经学到的特性。列表可能还不完全，但是应该够开始讨论了：

1. 项目有多大？
2. 要维护多久？
3. 所有的功能都被提前定义好还是你希望灵活一些？
4. 如果所有的特性已经明确，你需要什么功能？
5. 应用场景和业务逻辑是否复杂？
6. 针对哪些平台？Web端，移动端，桌面端？
7. 是否需要服务端渲染？ SEO 重要么？
8. 是否需要处理许多实时事件流？
9. 你的团队有多大？
10. 开发者的经验和他们的知识背景如何？
11. 是否有一些你想用的现成组件库？

如果你打算启动一个大项目，你可能想最小化做出不当选择的风险，首先考虑做一个概念性的验证产品。使用框架，通过简单方式，试着实现项目的一些关键特性。这通常不会花费你太多的时间，但会给你一些有价值的经验来验证关键技术需求。如果你对结果满意，你可以继续进行完整的开发。如果不满意，从长远来看其实节省了你的时间。

## 一招绝？

一旦你为你的项目选择了一个框架，你将会在接下来的项目中忍不住的想用同样的技术栈。不要这样。虽然保持技术栈统一是一个不错的注意，但不要总是使用同样的方法。每一个项目开始之前，花点时间再回答一遍上面的问题。可能对下个项目而言，答案就不一样了。另外，如果你想用不熟悉的技术栈做一个小项目，做吧。这些经历会带给你宝贵的经验。开放你的思维，并且从错误中不断学习。在某一点，一项特定的技术会让你自然而然的觉得正确。

_此文由同行 [Jurgen Van de Moere](https://www.sitepoint.com/author/mbrown/) 和 [Joan Yin](https://www.sitepoint.com/author/jvandemoere/) 校对. 谢谢 SitePoint 所有的校对人员，你们让 SitePoint 的内容更加的优秀!_

### 作者的更多文章
*   [Automated Accessibility Checking with aXe](https://www.sitepoint.com/automated-accessibility-checking-with-axe/?utm_source=sitepoint&utm_medium=relatedinline&utm_term=&utm_campaign=relatedauthor)
*   [React Storybook: Develop Beautiful User Interfaces with Ease](https://www.sitepoint.com/react-storybook-develop-beautiful-user-interfaces-with-ease/?utm_source=sitepoint&utm_medium=relatedinline&utm_term=&utm_campaign=relatedauthor)
                