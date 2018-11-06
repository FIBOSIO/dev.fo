---
title:  Fibos.js 介绍
type: tutorials
order: 150
---

## 概述

FIBOS 和 EOSIS 区块链的通用库

## 入门

安装模块：

```
npm install fibos.js
```

使用 fibos.js 启动 FIBOS 和 EOSIO 区块链之旅：

```javascript
var FIBOSJS = require('fibos.js')

config = {
	chainId: 'Chain ID', // 32 byte (64 char) hex string
	keyProvider: ['PrivateKey'], // WIF string or array of keys..
	httpEndpoint: 'http://127.0.0.1:8888',
	expireInSeconds: 60,
	broadcast: true,
	verbose: false, // API activity
	sign: true
}

var fibos = FIBOSJS(config);
```

## 测试

```
npm test
```

## BLOCKCHAIN支持

- [FIBOS](https://fibos.io/)
- [EOSIO](https://eos.io/)

## 特征

fibos.js 添加了一组上同步版本的方法 [eosjs](https://github.com/EOSIO/eosjs)

## 文档

与 [eosjs](https://github.com/EOSIO/eosjs) 相比，fibos.js 没有添加新功能，开发人员文档可以引用 eosjs。您可以在 [eosjs项目页面](https://github.com/EOSIO/eosjs) 上找到所有功能。对于 fibos.js，您唯一需要做的就是将那些可怕的异步函数调用切换到同步版本。

```javascript
// old-fashioned
fibos.getInfo((error, result) => { console.log(error, result) })

// stylish usage
var chainId = fibos.getInfoSync().chain_id;
```

此外，您可以在中找到用例`test/test.js`。在这些情况下，您将找到应该传递的参数以及预期的返回值。

目前，fibos.js 的初步开发已经完成，但仍有许多工作要做，例如改进用例。在那之后，您将看到更多推进使用 fibos.js 的用法。