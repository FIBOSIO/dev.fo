---
title: 账户
type: tutorials
language: zh-cn
order: 241
---

> **Tips:**我们将在9.4日关闭免费注册 FIBOS 账号通道，后续想要注册 FIBOS 账号的用户，可以通过学习本文档，让已经拥有 FIBOS 账号的用户替你创建。

## 什么是账户

- 账户有别于 BTC、ETH 中的地址，它是一个可识别、可阅读、便于记录的字符串，例如：你的游戏英文昵称 hellofibos。

- 账户的命名按照 EOS 的账户设计，它是有规则的，规则是：数字必须是1-5，字母a-z（小写），长度不大于12位。

- 目前 EOS BIOS 启动后账户名称长度必须是12位，对于技术工程师来说有一点必须了解，短账户名（小于12位）是由系统合约控制的，大家如果这个感兴趣，可以了解一下 EOS 的短名称竞标的相关信息。

- FIBOS 的账户可以拥有资源以及关联合约，拥有资源可以理解为 FIBOS 中 EOS、RAM、CPU、NET等资源都归属于账户，关联合约可以理解为合约必须所属账户。账户可以被授权做一些事务，比如：转账、合约 action。

## 生成公私钥

>**Tips:**生成的公私钥对需要将私钥妥善保存，并且切勿向任何人泄漏你的私钥！请别人帮人注册 FIBOS 账号只需要提供你的公钥即可，任何以帮忙注册 FIBOS 账号为名索要你的私钥的创建者都是欺骗者！

**使用 fibos.js 的 ecc 生成**

```javascript
var FIBOS = require('fibos.js');
var prikey = FIBOS.modules.ecc.randomKeySync(); //私钥
var pubkey = FIBOS.modules.ecc.privateToPublic(prikey); //公钥
console.log('公钥: %s\n私钥: %s',pubkey,prikey);
```



## 创建账户

### 新账户创建

调用 `newaccount` 方法和参数名解释如下：

```javascript
var FIBOS = require('fibos.js');
var fibos_client = FIBOS({
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'creator_priKey',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
  logger: {
    log: null,
    error: null
  }
});

fibos_client.newaccount({
    creator: "Creator Name", //创建者的账户名
    name: "Account Name", //被创建者的账户名
    owner: "Owner Key", //被创建者账户 owner 权限公钥
    active: "Active Key" //被创建者 active 权限公钥
});  
```

###  购买内存

在链上存贮账户信息是需要消耗内存的，创建者需为被创建者购买内存来存放新账户的信息。

调用 `buyrambytes` 方法和参数名解释如下：

```javascript
var FIBOS = require('fibos.js');
var fibos_client = FIBOS({
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'creator_priKey',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
  logger: {
    log: null,
    error: null
  }
});

fibos_client.buyrambytes({
    payer: 'eosio.token',//创建者的账户名
    receiver: 'Receiver Account',//被创建者的账户名
    bytes: 4096 //消耗的内存大小
});
```

### 抵押资源

创建者为被创建者抵押 FO 获取 CPU 和 NET ，让新账户能够进行转账。

调用 `delegatebw` 方法和参数名解释如下：

```javascript
var FIBOS = require('fibos.js');
var fibos_client = FIBOS({
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'creator_priKey',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
  logger: {
    log: null,
    error: null
  }
});

fibos_client.delegatebw({
    from: 'from',//创建者的账户名
    receiver: 'Your_Account',//被创建者的账户名
    stake_net_quantity: '0.1000 FO',//创建者为被创建者抵押 FO 获取 NET
    stake_cpu_quantity: '0.1000 FO',//创建者为被创建者抵押 FO 获取 CPU
    transfer: 1//代表抵押资源同时是否将对应通证转账给接受者
});
```

#### 实例

```javascript
var FIBOS = require('fibos.js');
var fibos_client = FIBOS({
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'creator_priKey',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
  logger: {
    log: null,
    error: null
  }
});
var r = fibos_client.transactionSync(tr => {
  tr.newaccount({
    creator: 'creator_account',
    name: 'your_account',
    owner: 'your_owner_publicKey',
    active: 'your_active_publicKey'
  });
  tr.buyrambytes({
    payer: 'creator_account',
    receiver: 'your_account',
    bytes: 4096
  });
  tr.delegatebw({
    from: 'creator_account',
    receiver: 'your_account',
    stake_net_quantity: '0.1000 FO',
    stake_cpu_quantity: '0.1000 FO',
    transfer: 1
  });
});
console.log(r);
```

执行代码，即可帮助别人成功注册账号。

打印结果如下（部分截取）：

```
'act': {
  'account': 'eosio',
  'name': 'newaccount',
  'authorization': [{
    'actor': 'fibostest123',
    'permission': 'active'
  }],
  'data': {
    'creator': 'fibostest123',
    'name': 'xinchengdai1',
    'owner': {
      'threshold': 1,
      'keys': [{
        'key': 'FO7yLv8FvFhFCjajcqgnJJFHBUnLLS9BYfZLymQXoDu7wL3a67Xr',
        'weight': 1
      }],
      'accounts': [],
      'waits': []
    },
    'active': {
      'threshold': 1,
      'keys': [{
        'key': 'FO7yLv8FvFhFCjajcqgnJJFHBUnLLS9BYfZLymQXoDu7wL3a67Xr',
        'weight': 1
      }],
      'accounts': [],
      'waits': []
    }
},
```

根据上面的打印信息，可以看到 `fibostest123` 账号创建了一个名为 `xinchengdai1` 的账号，下面 `xinchengdai1` 账号持有者就可以将私钥导入到 FO 钱包中来使用其中的各项功能啦！点击 [下载 FO 钱包](http://wallet.fo/) 来获取 FO 钱包吧 ~