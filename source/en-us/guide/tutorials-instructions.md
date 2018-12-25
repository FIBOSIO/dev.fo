---
title: Introductions
type: tutorials
language: en
order: 10
---

## Introduction to DApp

DApp is the abbreviation of Decentralized Application, and DApp is considered to initiate the start of the blockchain 3.0 era.

Different DApps adopt different base blockchain development platforms and consensus mechanisms. The mentioned different base blockchain development platforms are like the IOS and Android systems applied of mobile phone, and they are the base ecosystem development environment for each DApp. DApp is a distributed application that is derived from the ecology of the base blockchain platform and is also the basic service provider in the blockchain world. The DApp is to blockchain what the APP is to IOS and Android.

What are these base blockchain development platforms like?

Currently, popular development platforms include Ethereum, EOS, FIBOS and others.

Ethereum, at its core, is public blockchain platform with the function of smart contracts, and it allows anyone to build and use distributed applications based on blockchain technology on the platform through the programming language of solidity.

EOS is a new platform that allows developers to create blockchain applications on the top of the protocols. It runs faster and more stable than ETH, and it solves the problem concerning high transaction frequency, with transactions reaching tens of billions per second. Additionally, it can support running of thousands of APPs at the same time. Its programming language is c++.

FIBOS is a brand new blockchain-based js development platform designed by fibjs + EOS. In addition to better speed and stability, it is also more friendly to developers than the former two.



## Tutorial clarification

TodoDApp is a DApp running on the FIBOS platform and written through React and fibos.js. Through TodoDapp, we can create a TodoList example, and operate the following:
- Build a local node
- Write an ABI file
- Write a JavaScript contract
- Deploy the contract
- Call the contract


Code file directory structure

```

fibos-todomvc/
├── .babelrc            Front end config file
├── config.js           Saves main chain, contract and account basic info
├── dist 
│   └──index.html       Front end test page
├── start_fibos 
│   ├── node.js         Node, produce block
├── contracts
│   ├── todo.js         Contract code file
│   └── todo.abi        Contract abi file
├── script
│   ├── deploy.js       Load, publish contract script files
│   ├── server.js       Local fibos service
│   └── webpack.dev.js  Front end html config script
└── dapp
    ├── index.js        Front end config script 
    └── components
   	├── app.js          dapp development file
   	├── footer.js 
   	├── header.js
   	├── main-section.js
   	├── todo-item.js
   	└── todo-text-input.js
	   
```

> Note: This article focuses on fibos and how to develop DApp. React is set as the front-end framework, and JavaScript is the development language. If you are a newcomer and are unable to develop with React and JS, it's advised to learn React and JavaScript first. 

In addition, the running environment of this tutorial is only confined in the local development environment. If the running environment needs to be in the production environment (actual development), it is necessary to perform on-site testing based on some information such as the actual account and private key.

## Learning Resources

The GitHub source code of this article: <https://github.com/fengluo/fibos-todomvc> 
Learn JavaScript: <https://developer.mozilla.org/bm/docs/Web/JavaScript>
Learn React: <https://reactjs.org/>

**Next Chapter**
👉 【[Build Local Test Nodes](setnode.html)】