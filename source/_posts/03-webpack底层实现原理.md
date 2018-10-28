---
title: Webpack底层实现原理
date: 2016-07-28
tags: Webpack
categories: 编程原理
---
webpack是Web前端流行的项目打包工具，所以了解其底层实现的原理，能够在实际开发中更好的开展工作。
<!--more-->

### Webpack的实现

webpack的实现原理，是通过node.js的读取文件操作，将项目中src目录，自动生成dist目录，src目录中的所有js文件，最后生成一个build.js文件，将所有js代码封装在一个函数中，并使用数组对象形式的参数传递到这个函数中，内部通过require的方式，将文件进行关联，从而实现了代码的运行。