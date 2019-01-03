---
title: 账户权限
type: tutorials
language: zh-cn
order: 203
---

## FIBOS 中的账户权限如何应用到合约中

一般的事务中会有转账、合约的action等操作，这些都会涉及到账户权限的知识，学习到这里，大家应该对账户与权限已经有一定了解，FIBOS 提供使用 JavaScript 编写合约，那么如何在 FIBOS 的合约中控制权限呢？下面会通过示例来为大家演示。

让我们先来实现一个简单的合约，保存代码至工作目录 `code.js`:

```javascript
var FIBOS = require('fibos.js');

var fibos = FIBOS({
  chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
  keyProvider: '5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3',
  httpEndpoint: 'http://127.0.0.1:8888',
  logger: {
    log: null,
    error: null
  }
});

//合约所属账户 hellocode 的公私钥对
let pubkey = 'FO5L9g2mnC4zZMZWDR8VBksz3exFmXV4kwfj65oYeKdqRPc2oPFW';
let prikey = '5KMg9oUf5caX9yku7zQQwKZQLukRW7dMHaST8njpBf22puUvjea';

//创建合约账户
var name = 'hellocode';
fibos.newaccountSync({
  creator: 'eosio',
  name: name,
  owner: pubkey,
  active: pubkey
});

//发布一个合约
var abi = {
  'version': 'eosio::abi/1.0',
  'structs': [{
    'name': 'hi',
    'base': '',
    'fields': [{
      'name': 'user',
      'type': 'name'
    }]
  }],
  'actions': [{
    'name': 'hi',
    'type': 'hi',
    'ricardian_contract': ''
  }]
};

//由 hellocode 提供私钥发布合约
fibos = FIBOS({
  chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
  keyProvider: prikey,
  httpEndpoint: 'http://127.0.0.1:8888',
  logger: {
    log: null,
    error: null
  }
});

fibos.setabiSync(name, abi);

var js_code = `exports.hi = v => console.error(action);`;
fibos.setcodeSync(name, 0, 0, fibos.compileCode(js_code));
```

运行脚本：
```
fibos code.js
```


执行结束后，我们使用 hellocode 账户发布了一个合约，合约提供一个 hi 方法，该方法仅仅打印输出了 action 这个对象，那么我们开始尝试调用合约。

action 对象对于权限控制非常重要，请继续阅读。

### 解读合约内 action 对象

让我们写一个调用合约脚本，查看 action 对象是一个什么？保存代码至工作目录 `call.js`:

```javascript
var FIBOS = require('fibos.js');

//合约所属账户 hellocode 的公私钥对
let pubkey = 'FO5L9g2mnC4zZMZWDR8VBksz3exFmXV4kwfj65oYeKdqRPc2oPFW';
let prikey = '5KMg9oUf5caX9yku7zQQwKZQLukRW7dMHaST8njpBf22puUvjea';

var name = 'hellocode';

var fibos = FIBOS({
  chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
  keyProvider: prikey,
  httpEndpoint: 'http://127.0.0.1:8888',
  logger: {
    log: null,
    error: null
  }
});

var ctx = fibos.contractSync(name);
var r = ctx.hiSync(name, {
  authorization: name
});

console.error(r.processed.action_traces[0].console);
```

执行脚本:
```
fibos call.js
```

输出:
```
{
  'is_account': [Function],
  'has_recipient': [Function],
  'require_recipient': [Function],
  'has_auth': [Function],
  'require_auth': [Function],
  'name': 'hi',
  'account': 'hellocode',
  'receiver': 'hellocode',
  'publication_time': 1534845804000000,
  'authorization': [
    {
      'actor': 'hellocode',
      'permission': 'active'
    }
  ]
}
```

分析一下脚本以及结果：

- r.processed.action_traces[0].console 合约执行过程打印的信息会出现在返回值中
- is_account 判断是否是一个账户
- has_auth 判断账户是否拥有权限
- require_auth 获取某个账户是否拥有某个权限
- name action 方法的名称
- account 合约所属账户
- authorization 调用 hi 方法的账户、权限信息

### 让我们来试试 action 的权限控制

首先我们先来更新一下合约，保存代码 `updatecode.js`:

```javascript
var FIBOS = require('fibos.js');

//合约所属账户 hellocode 的公私钥对
let pubkey = 'FO5L9g2mnC4zZMZWDR8VBksz3exFmXV4kwfj65oYeKdqRPc2oPFW';
let prikey = '5KMg9oUf5caX9yku7zQQwKZQLukRW7dMHaST8njpBf22puUvjea';
var name = 'hellocode';

var fibos = FIBOS({
  chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
  keyProvider: prikey,
  httpEndpoint: 'http://127.0.0.1:8888',
  logger: {
    log: null,
    error: null
  }
});

var js_code = `exports.hi = v => console.error(action.has_auth(v));`;
fibos.setcodeSync(name, 0, 0, fibos.compileCode(js_code));
```

运行脚本:

```
fibos updatecode.js
```

这段脚本的含义是判断调用者是否拥有对参数 v 这个用户的 active 权限，让我们写一个脚本开始测试一下吧！

保存以下代码到工作目录 `call2.js`:

```javascript
var FIBOS = require('fibos.js');

//合约所属账户 hellocode 的公私钥对
let pubkey = 'FO5L9g2mnC4zZMZWDR8VBksz3exFmXV4kwfj65oYeKdqRPc2oPFW';
let prikey = '5KMg9oUf5caX9yku7zQQwKZQLukRW7dMHaST8njpBf22puUvjea';
var name = 'hellocode';

var fibos = FIBOS({
  chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
  keyProvider: prikey,
  httpEndpoint: 'http://127.0.0.1:8888',
  logger: {
    log: null,
    error: null
  }
});

var ctx = fibos.contractSync(name);
var r = ctx.hiSync('hellocode', {
  authorization: name
});

console.error(r.processed.action_traces[0].console);


var ctx = fibos.contractSync(name);
var r = ctx.hiSync('eosio', {
  authorization: name
});

console.error(r.processed.action_traces[0].console);
```

执行脚本:

```
fibos call2.js
```

输出结果:

```
true
false
```

根据结果，代表 hellocode 账户 拥有 hellocode 的active 权限，但是并不拥有 eosio 这个账户的 active 权限。

大家可以尝试升级合约使用 `require_auth` 替换 `has_auth`, `require_auth` 执行如果不是预期结果会执行退出合约。