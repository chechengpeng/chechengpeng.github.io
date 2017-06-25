---
title: 在 Vue.js 中使用混合
date: 2017-06-24 23:22:38
tags:  [JavaScript, 翻译]
---

_译者水平有限，原汁原味请移步：[原文链接](https://css-tricks.com/using-mixins-vue-js/?utm_campaign=Revue%20newsletter&utm_medium=Newsletter&utm_source=revue/)_

有一种很常见的情况：有两个非常相似的组件，它们共享同样的基本函数，并且它们之间也有足够的不同，这时你站在了一个十字路口：我是把它拆分成两个不同的组件？还是只使用一个组件，创建足够的属性来改变不同的情况。

这些解决方案都不够完美：如果你拆分成两个组件，你就不得不冒着如果功能变动你要在两个文件中更新它的风险，这违背了 DRY 前提。另一方面，太多的属性会很快会变得混乱不堪，对维护者很不友好，甚至是你自己，为了使用它，需要理解一大段上下文，这会让你感到失望。

使用混合。Vue 中的混合对编写函数式风格的代码很有用，因为函数式编程就是通过减少移动的部分让代码更好理解（引用于 [Michael Feathers](https://twitter.com/mfeathers/status/29581296216?lang=en) ）。混合允许你封装一块在应用的其他组件中都可以使用的函数。如果被正确的使用，他们不会改变函数作用域外部的任何东西，所以多次执行，只要是同样的输入你总是能得到一样的值。这真的很强大。

### 基础实例

我们有一对不同的组件，它们的作用是切换一个状态布尔值，一个模态框和一个提示框。这些提示框和模态框除了在功能上，没有其他共同点：它们看起来不一样，用法不一样，但是逻辑一样。

```
// 模态框
const Modal = {
  template: '#modal',
  data() {
    return {
      isShowing: false
    }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    }
  },
  components: {
    appChild: Child
  }
}

// 提示框
const Tooltip = {
  template: '#tooltip',
  data() {
    return {
      isShowing: false
    }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    }
  },
  components: {
    appChild: Child
  }
}

```

我们可以提取出这个逻辑并创建可以被重用的项：

```
const toggle = {
  data() {
    return {
      isShowing: false
    }
  },
  methods: {
    toggleShow() {
      this.isShowing = !this.isShowing;
    }
  }
}

const Modal = {
  template: '#modal',
  mixins: [toggle],
  components: {
    appChild: Child
  }
};

const Tooltip = {
  template: '#tooltip',
  mixins: [toggle],
  components: {
    appChild: Child
  }
};

```

查看 Sarah Drasner([@sdras](https://codepen.io/sdras)) 在[CodePen](https://codepen.io)上编写 [混合](https://codepen.io/sdras/pen/101a5d737b31591e5801c60b666013db/)的例子

为了更容易理解混合，这个例子故意编写的简单一些。真实应用中使用混合的有，包含但不限于：获取视窗和组件的尺寸，采集特定的鼠标事件和图表的基本元素。Paul Pflugradt 有一个关于 [Vue Mixins 的优秀项目](https://github.com/paulpflug/vue-mixins)，但值得一提的是它是用 coffeescript 编写的。

### 用法

这个例子没有告诉我们在一个真实的应用中如何使用，所以，我们看看接下来要怎么做。

你可以按照你喜欢的任意方式设置你的目录结构，但为了更好的组织结构我喜欢新建一个 `mixin` 目录。我们创建的这个文件含有`.js`扩展名（跟`.vue`相对，就像我们的其他文件），并且为了混合我们需要输出一个对象。

![directory structure shows mixins in a folder in components directory](http://p0.qhimg.com/t0195da96ce6d7eb510.jpg)

接着在 Modal.vue 中使用它，通过像下面这样的引入方式：

```
import Child from './Child'
import { toggle } from './mixins/toggle'

export default {
  name: 'modal',
  mixins: [toggle],
  components: {
    appChild: Child
  }
}

```

即使我们使用的是一个对象而不是一个组件，生命周期函数对我们来说仍然是可用的，理解这点很重要。我们可以在这使用`mounted()`钩子函数，它将被应用于组件的生命周期上，这种工作方式真的很灵活也很强大。

### 合并

看最后这个例子，我们可以看到，我们不仅有自己的函数，而且来自于混合的生命周期函数对我们来说也是可用的，所以当在组件上注册重复的过程时，顺序很重要。默认混合上会首先被注册，组件上的接着注册，这样如有必要我们可以重写它。**组件拥有最终发言权**当有一个冲突并且这个组件不得不“决定”哪个胜出的时候，这真的变得很重要，否则，所有的东西都被放在一个数组当中执行，混合中的先执行，组件中的接着执行。

```
//mixin
const hi = {
  mounted() {
    console.log('hello from mixin!')
  }
}

//vue instance or component
new Vue({
  el: '#app',
  mixins: [hi],
  mounted() {
    console.log('hello from Vue instance!')
  }
});

//Output in console
> hello from mixin!
> hello from Vue instance!

```

如果这两个冲突了，我们看看 Vue实例或组件是如何取胜的：

```
//mixin
const hi = {
  methods: {
    sayHello: function() {
      console.log('hello from mixin!')
    }
  },
  mounted() {
    this.sayHello()
  }
}

//vue instance or component
new Vue({
  el: '#app',
  mixins: [hi],
  methods: {
    sayHello: function() {
      console.log('hello from Vue instance!')
    }
  },
  mounted() {
    this.sayHello()
  }
})

// Output in console
> hello from Vue instance!
> hello from Vue instance!

```

你可能已经注意到这有两个`console.log`而不是一个——这是因为第一个函数被调用时，没有被销毁，它被重写了。我们两次调用的都是`sayHello()`函数。


### 全局混合

当我们使用全局混合时，我们不是指能够在每个组件上访问它们，就像是过滤器一样。我们能够通过`mixins:[toggle]`访问组件上的混合对象。

全局混合被注册到了_每个单一组件上_。因此，它们的使用场景极其有限并且要非常的小心。一个我能想到的用途就是它像一个插件，你需要赋予它访问所有东西的权限。但即使在这种情况下，我也对你正在做的保持警惕，尤其是你在应用中扩展的函数，可能对你来说是不可知的。

为了创建一个全局实例，我们可以把它放在 Vue 实例之上。在一个典型的 Vue-cli 初始化的项目中，它可能在你的`main.js`文件中。

```
Vue.mixin({
  mounted() {
    console.log('hello from mixin!')
  }
})

new Vue({
  ...
})

```

再次提醒，小心使用它！那个 `console.log`将会出现在每个组件上。这种情况还不算坏（除了控制台上有多余的输出），但如果它被错误的使用，你将能看到它会多么的有害。

### 结论

混合对于封装一小段想要复用的代码来讲是有用的。对你来说它们当然不是唯一可行的选择：高阶组件，例如，允许组合相似函数，这只是实现的一种方式。我喜欢混合，因为我不需要传递状态，但是这种模式当然也可能会被滥用，所以，仔细思考哪种选择对你的应用最有意义。
                