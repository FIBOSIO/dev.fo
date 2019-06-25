---
title: 
type: msig
language: zh-cn
order: 1
---
# Msig Contract

**msig** 是 **multiple signature（多重签名）**的简写，顾名思义，就是让多个账户对一起事务进行签名。可以异步提出、批准、发布经过多方同意的事务。多重签名是根据账户或公钥所拥有权限的**权重**来决定的，权重达到阈值才能签名成功。

## propose

发起提案

#### 参数

| name              | type   | description            |
| ----------------- | ------ | ---------------------- |
| **proposer**      | string | 提案人                 |
| **proposal_name** | string | 提案名                 |
| **requested**     | string | 提案通过所需权限       |
| **trx**           | string | 提案具体执行的交易内容 |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio.msig');

var r = ctx.proposeSync({
      proposer: 'account_name',
      proposal_name: 'name',
      requested: [{
            "actor": "popo11111111",
            "permission": "active"
          }],
      trx: 'transaction'    
}, {
  authorization: '私钥对应的账号'
});
console.log(r);
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio.msig').then((contract)=>{
    contract.propose({
      proposer: 'account_name',
      proposal_name: 'name',
      requested:  [{
            "actor": "popo11111111",
            "permission": "active"
          }],
      trx: 'transaction'
    },{
        authorization: '私钥对应的账号'
    })
})
```



## approve

同意提案

#### 参数

| name              | type   | description              |
| ----------------- | ------ | ------------------------ |
| **proposer**      | string | 提案人                   |
| **proposal_name** | string | 提案名                   |
| **level**         | string | 使用哪个权限批准这个提案 |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://api.testnet.fo',
});

let ctx = fibos_client.contractSync('eosio.msig');

var r = ctx.approveSync({
      proposer: 'account_name',
      proposal_name: 'name',
      level:{"actor":"bob", "permission":"active"}    
}, {
  authorization: '私钥对应的账号'
});
console.log(r);
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio.msig').then((contract)=>{
    contract.approve({
      proposer: 'account_name',
      proposal_name: 'name',
      level: {"actor":"bob", "permission":"active"}
    },{
        authorization: '私钥对应的账号'
    })
})
```



## unapprove

不同意提案

#### 参数

| name              | type   | description              |
| ----------------- | ------ | ------------------------ |
| **proposer**      | string | 提案人                   |
| **proposal_name** | string | 提案名                   |
| **level**         | string | 使用哪个权限拒绝这个提案 |

#### 示例

fibos 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://api.testnet.fo',
});

let ctx = fibos_client.contractSync('eosio.msig');

var r = ctx.unapproveSync({
      proposer: 'account_name',
      proposal_name: 'name',
      level: {"actor":"bob", "permission":"active"}   
}, {
  authorization: '私钥对应的账号'
});
console.log(r);
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio.msig').then((contract)=>{
    contract.unapprove({
      proposer: 'account_name',
      proposal_name: 'name',
      level:{"actor":"bob", "permission":"active"}
    },{
        authorization: '私钥对应的账号'
    })
})
```



## cancel

取消提案

#### 参数

| name              | type   | description |
| ----------------- | ------ | ----------- |
| **proposer**      | string | 提案人      |
| **proposal_name** | string | 提案名      |
| **canceler**      | string | 取消账户    |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://api.testnet.fo',
});

let ctx = fibos_client.contractSync('eosio.msig');

var r = ctx.cancelSync({
      proposer: 'account_name',
      proposal_name: 'name',
      canceler: 'account_name'
}, {
  authorization: '私钥对应的账号'
});
console.log(r);
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio.msig').then((contract)=>{
    contract.cancel({
      proposer: 'account_name',
      proposal_name: 'name',
      canceler: 'account_name'
    },{
        authorization: '私钥对应的账号'
    })
})
```



## exec

执行提案

#### 参数

| name              | type   | description |
| ----------------- | ------ | ----------- |
| **proposer**      | string | 提案人      |
| **proposal_name** | string | 提案名      |
| **executer**      | string | 执行账户    |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://api.testnet.fo',
});

let ctx = fibos_client.contractSync('eosio.msig');

var r = ctx.execSync({
      proposer: 'account_name',
      proposal_name: 'name',
      executer: 'account_name'
}, {
  authorization: '私钥对应的账号'
});
console.log(r);
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio.msig').then((contract)=>{
    contract.exec({
      proposer: 'account_name',
      proposal_name: 'name',
      executer: 'account_name'
    },{
        authorization: '私钥对应的账号'
    })
})
```

