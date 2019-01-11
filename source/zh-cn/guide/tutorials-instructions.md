---
title: 简介
type: tutorials
language: zh-cn
order: 10
---

## DApp 简介

DApp 是 Decentralized Application 的缩写，中文是去中心化应用，被认为开启了区块链3.0时代。

不同的 DApp 采用不同的底层区块链开发平台和共识机制。这里所说的不同的底层区块链开发平台就好比手机的 IOS 系统和 Android 系统，是各个 DApp 的底层生态开发环境。DApp 就是在底层区块链平台生态上衍生的各种分布式应用，也是区块链世界中的基础服务提供方。DApp 于区块链，就好比 APP 之于 IOS 和 Android。

具体的底层区块链开发平台是什么样子的呢？

目前比较流行的开发平台由以太坊、eos、fibos 等。

以太坊的核心是有智能合约功能的公共区块链平台，它允许任何人在上面中建立和使用通过区块链技术运行的分布式应用，编程语言为 solidity 。

EOS 是一个允许开发者在其协议顶端创建区块链应用的新平台，与 ETH 相比，运行速度更快更稳定，主要解决了高交易频率的问题，每秒交易可达百亿次，且可同时运行上千个 APP ，编程语言为 c++。

FIBOS 是一个由 fibjs+eos 设计的一个全新的区块链 js 开发平台，相比以上两者做到兼顾速度、稳定之外，对开发者更友好。

## 教程说明

Todo DApp 是用 React 和 fibos.js 编写的一款在 FIBOS 平台上运行的 DApp。通过它我们可以创建一个 TodoList 示例，并且进行以下操作：
- 搭建本地节点
- 编写 ABI 文件
- 编写 JavaScript 合约
- 部署合约
- 调用合约

代码文件目录结构

```

fibos-todomvc/
├── .babelrc  前端配置文件
├── config.js  保存了主链、合约和账户的基本信息
├── dist 
│   └──index.html 前端测试页面
├── start_fibos 
│   ├── node.js  节点，生成区块
├── contracts
│   ├── todo.js  合约代码文件
│   └── todo.abi 合约abi文件
├── script
│   ├── deploy.js  加载、发布合约脚本文件
│   ├── server.js  本地fibos服务
│   └── webpack.dev.js  前端html配置脚本
└── dapp
    ├── index.js  前端配置脚本
    └── components
   	├── app.js  dapp开发文件
   	├── footer.js 
   	├── header.js
   	├── main-section.js
   	├── todo-item.js
   	└── todo-text-input.js
	   
```

>注意：本文重点讲解的是 fibos 以及如何开发 DApp 。前端运用的框架为 React，开发语言为 JavaScript。如果不具备 React 以及 JS 开发的新手，建议先学习 React 及 JavaScript。

另外本教程的运行环境仅在本地开发环境中，如果需要在生产环境（实际开发）中，得结合实际的账户和秘钥等信息进行现场测试。

## 学习资源

本项目 GitHub 源码：<https://github.com/fengluo/fibos-todomvc> 
JavaScript 学习： <https://developer.mozilla.org/bm/docs/Web/JavaScript>
React 学习：<https://react.docschina.org/>

**下一章节**
👉 【[搭建本地测试节点](tutorials-setnode.html)】