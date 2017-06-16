---
title: CSS BEM 命名规则核心概念介绍
date: 2017-06-08 17:57:28
tags: [CSS, 翻译]
---

_译者水平有限，原汁原味请移步：[原文链接](https://en.bem.info/methodology/key-concepts/)_

# 核心概念
- 块
- 元素
- 修饰符
- BEM 实体
- 混合
- BEM 树
- 块的实现
- 块的实现技术
- 块的重新定义
- 重定义层级

## 块  
逻辑和功能独立的页面组件，等同于Web组件。一个块封装了行为（JavaScript），模板，样式（CSS），和其他实现技术。块是相对独立的，可被重复调用，这有助于项目开发和维护。  

### 块特性

#### 嵌套结构

块可以嵌套在任何其他块中

例如，一个`head`块可以包含一个logo`(logo)`,一个搜索表单`(search)`，和一个登录块`(auth)`。

![](https://en.bem.info/kFetIbKxQdABHhUecbic45Il0Bg.png)

#### 随处可放

块即可以在单个页面上移动，也可以在项目内多个页面之间移动。块作为独立实体的实现方式让它可以在页面上改变位置的时候保持它原有的功能和外观。

因此，块中的logo和登录表单可以互换位置，而不用修改CSS或JavaScript代码。

![](https://en.bem.info/v80tUiEPgSQtyW9a7C8rxdn-5EM.png)
![](https://en.bem.info/0bbhZyhaBhRzqBh5nLYQEnFpDTk.png)

#### 重用

一个界面可以包含多个同样的块

![](https://en.bem.info/VBlEdksG7XkL4DLPWe4rcYb5hGo.png)

## 元素

块的组成部分且不能在块之外使用

例如，一个菜单项没有用在菜单块之外，所以它实际就是一个元素 

![](https://en.bem.info/cPrdQL4EZZdhPIrcYOayygPBSm4.png)

> [块或元素，我应该用哪个？](https://en.bem.info/methodology/faq/#a-block-or-an-element-when-should-i-use-which)
>
> [在元素中用元素是 BEM 技术不推荐的](https://en.bem.info/methodology/faq/#why-does-bem-not-recommend-using-elements-within-elements-block__elem1__elem2)

## 修饰符

一个 BEM 实体是用来定义块或元素的外观和行为

修饰符的使用是可选的

修饰符本质上和 HTML 的属性相似。因为修饰符的使用，让之前的块看起来不一样。

例如，菜单块的外观可能因使用了修饰符而发生改变。

![](https://en.bem.info/WSU5nwZla7p44W2tdxiP371xx38.png)

修饰符可以在运行时改变（比如，作为块上 DOM 事件的响应）或者通过其他块。

例如，当用户点击登录按钮的时候，如果提供了一个错误的凭证，`visible` 修饰符将会被用在一个含有错误提示的隐藏块上。

## BEM 实体

块，元素和修饰符都被称作 BEM 实体。

这个概念既可以用于表示一个独立的 BEM 实体，也可以用于表示块，元素和修饰符。

## 混合

例如，不同的多个BEM实体可以同时用于一个DOM节点上

混合允许我们  
 - 合并多个 BEM 实体的行为和样式以避免出现代码重复
 - 在已有 BEM 实体上创建新的语义化的界面组件
 
我们来考虑一下由一个块和另一个块中元素混合的情况

我们假设项目中的链接通过`link`块来实现。我们需要把菜单项设计成链接。有这些方法可以实现。
 - 为菜单项创建指向链接的修饰符。通过修饰符来实现，需要复制`link`块的行为和样式代码。这就造成了代码重复。
 - 让一个混合体包含一个通用的link块和一个menu 块中的link元素。这两个 BEM实体的混合体可以让我们在不用复制代码的情况下使用link块的功能和menu块的样式。
 

## BEM 树

一个Web页面结构包含块，元素和修饰符。这是一个 DOM 树的抽象，描述了 BEM 实体的名字，他们的状态，顺序，嵌套和辅助数据。

在现实项目中，BEM 树可以以任意支持树结构的方式展现。

我们看看一个 DOM 树的例子：

``` HTML
<header class="header">
    <img class="logo">
    <form class="search-form">
        <input type="input">
        <button type="button"></button>
    </form>
    <ul class="lang-switcher">
        <li class="lang-switcher__item">
            <a class="lang-switcher__link" href="url">en</a>
        </li>
        <li class="lang-switcher__item">
            <a class="lang-switcher__link" href="url">ru</a>
        </li>
    </ul>
</header>
```

对应的 BEM 树看起来像：

```
header
    ├──logo
    └──search-form
        ├──input
        └──button
    └──lang-switcher
        └──lang-switcher__item
            └──lang-switcher__link
        └──lang-switcher__item
            └──lang-switcher__link
```

XML 和 BEMJSON 格式的 BEM 树为：

XML

``` XML
<block:header>
    <block:logo/>
    <block:search-form>
        <block:input/>
        <block:button/>
    </block:search-form>
    <block:lang-switcher>
        <elem:item>
            <elem:link/>
        </elem:item>
        <elem:item>
            <elem:link/>
        </elem:item>
    </block:lang-switcher>
</block:header>
```

BEMJSON

``` JSON
{
    block: 'header',
    content : [
        { block : 'logo' },
        {
            block : 'search-form',
            content : [
                { block : 'input' },
                { block : 'button' }
            ]
        },
        {
            block : 'lang-switcher',
            content : [
                {
                    elem : 'item',
                    content : [
                        { elem : 'link' }  
                    ]
                },
                {
                    elem : 'item',
                    content : [
                        { elem : 'link' }
                    ]
                }
            ]
        }
    ]
}
```

## 块实现

一些不同的技术可以决定一个 BEM 实体的以下几个方面：

- 行为
- 外观
- 测试
- 模板
- 文档
- 依赖描述
- 辅助数据

## 实现技术

用来实现块的技术

块可以通过一种或多种技术来实现，比如：
- 行为 —— JavaScript，CoffeeScript
- 外观 —— CSS,Stylus,Sass
- 模板 —— BEMHTML,BH,Pug,HandleBars,XSL
- 文档 —— Markdown,Wiki,XML

举个例子，如果一个块的外观是由 CSS 定义的，这意味着块是用 CSS 技术来实现的。同样，一个块的文档是用 Markdown 格式写得，那么这个块就是由 Markdown 技术实现的。

## 块的重定义

在不同层级上，通过给一个块添加新特性来修改它的实现。

## 重定义层级

一系列的 BEM 实体和它们的部分实现

一个块的最终实现可以分为不同的重定义层级。每个新层级继承或重写了原来的实现方式。最终的结果是在事先确定的顺序下，把不同定义层级的独立的块组装起来。

![](https://en.bem.info/kqvCO2ZXeivuLHCbn2to5chFZrM.png)

BEM 实体的任何实现技术都能被重新定义。

例如，在一个单独的层级上有一个第三方类库链接到了项目上。这个库包含了现成的块的实现。特定项目的块保存在不同的重定义层级上。

比如说，我们要修改这个库中一个块的外观。我们不需要改变库中代表这个块CSS样式的源代码。我们只需要在项目上创建额外的 CSS 规则。在构建过程中，实现结果将会合并类库中的原始规则和项目中的新规则。


