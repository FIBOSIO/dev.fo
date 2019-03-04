---
title: 
type: token
language: zh-cn
order: 1
---

# Token Contract

## transfer

转账 —— 只有发行方为 eosio 的通证可以调用（FIBOS测试网目前只有 EOS 和 FO）

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **from**     | string | 通证转出方  |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

####  示例

fibos.js 环境下：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://api.testnet.fo',
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.transferSync('fibforjeremy', 'fiboscouncil', '20.3375 EOS', 'eosforjeremy', {
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.transfer({
      from: 'fibforjeremy',
      to: 'fiboscouncil',
      quantity: '20.3375 EOS',
      memo: 'eosforjeremy'
    },{
        authorization: '私钥对应的账号'
    })
})
```



## extransfer

转账

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **from**     | string | 通证转出方  |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

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

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.extransferSync('dicefobetone', 'zhangjingrui', '10.0000 FO@eosio', 'trasnfer to zhangjingrui', {
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.extransfer({
      from: 'dicefobetone',
      to: 'zhangjingrui',
      quantity: '10.0000 FO@eosio',
      memo: 'trasnfer to zhangjingrui'
    },{
        authorization: '私钥对应的账号'
    })
})
```



## exissue

增发通证 —— 普通通证支持增发，社区智能通证暂不支持

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

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

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.exissueSync('dogfallchina', '10.0000 TAO@dogfallchina', 'issue to dogfallchina', {
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exissue({
      to: 'dogfallchina',
      quantity: '10.0000 TAO@dogfallchina',
      memo: 'issue to fibostest123'
    },{
        authorization: '私钥对应的账号'
    })
})
```



## exretire

销毁账户持有的流通通证

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **from**     | string | 通证转出方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

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

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.exretireSync('createtest11', '10.0000 FO@eosio', 'retire tokens', {
  authorization: '私钥对应的账号'
});
console.log(r);
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://api.testnet.fo",
});

client.contract('eosio.token').then((contract)=>{
    contract.exretire({
      from: 'createtest11',
      quantity: '10.0000 FO@eosio',
      memo: 'retire tokens'
    },{
        authorization: '私钥对应的账号'
    })
})
```



## exshare

向社区中通证持有者进行分红

#### 参数

| name         | type   | description        |
| ------------ | ------ | ------------------ |
| **quantity** | string | 填入保证金的数量   |
| **tosym**    | string | 参与分红的智能通证 |
| **memo**     | string | 附言               |

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

let ctx = fibos.contractSync('eosio.token');
let r = ctx.exshareSync('10000.0000 FO@eosio', '0.0000 AAA@fibostest321', 'share 10000.0000 FO to token holders',{
    authorization: '私钥对应的账号'
}); 
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exshare({
      quantity: '10000.0000 FO@eosio',
      tosym: '0.0000 AAA@fibostest321' 
      memo: 'share 10000.0000 FO to token holders'
    },{
        authorization: '私钥对应的账号'
    })
});
```



## excreate

发行通证

#### 参数

| name                          | type      | description                |
| ----------------------------- | --------- | -------------------------- |
| **issuer**                    | string    | 通证发行账号               |
| **maximum_supply**            | string    | 最大可发行通证数量         |
| **connector_weight**          | float64   | 连接器权重                 |
| **maximum_exchange**          | string    | 最大可兑换(流通)的通证数量 |
| **reserve_supply**            | string    | 锁仓通证数量               |
| **reserve_connector_balance** | string    | 锁仓通证保证金数量         |
| **expiration**                | date-time | 项目方预设的项目锁仓期     |
| **buy_fee**                   | double    | 项目方预设通证兑入手续费   |
| **sell_fee**                  | double    | 项目方预设通证兑出手续费   |
| **connector_balance_issuer**  | stirng    | 准备金发行方              |
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

let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.excreateSync('dogfallchina', '90000000000.0000 DDD', 0, '10000000000.0000 DDD', '3000000000.0000 DDD', '90000.0000 FO', '2018-10-29T18:54:00', 0, 0, 'eosio', { //手续费自定义,大于0小于等于1,此处准备金为 FO，所以准备金发行方填 eosio
  authorization: '私钥对应的账号'  //授权
}); //expiration 需大于等于当前时间
console.log(r)
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://api.testnet.fo',
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.excreate({
      issuer: 'dogfallchina',
      maximum_supply: '90000000000.0000 DDD',
      connector_weight: 0,
      maximum_exchange: '10000000000.0000 DDD',
      reserve_supply: '3000000000.0000 DDD',
      reserve_connector_balance: '90000.0000 FO',
      expiration: '2018-10-29T18:54:00',
      buy_fee: 0,
      sell_fee: 0,
      connector_balance_issuer: 'eosio'
    },{
        authorization: '私钥对应的账号'
    })
})
```



## exclose

删除账户中通证的条目

#### 参数

| name       | type   | description  |
| ---------- | ------ | ------------ |
| **owner**  | string | 通证拥有者   |
| **symbol** | string | 通证目标类型 |

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


let ctx = client.contractSync('eosio.token');

let r = ctx.excloseSync('dreamheartlx', '4,ZC@lixunlixunli', { //4表示通证的精度，ZC表示通证名称，lixunlixunli表示通证的发行人
  authorization: '私钥对应的账号'
}); 
console.log(r)
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exclose({
      owner: 'dreamheartlx',
      symbol: '4,ZC@lixunlixunli'
    },{
        authorization: '私钥对应的账号'
    })
});
```



## exdestroy

永久删除通证

#### 参数

| name       | type   | description  |
| ---------- | ------ | ------------ |
| **symbol** | string | 通证目标类型 |

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

let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.exdestroySync('8,QE@dreamheartlx', {
  authorization: '私钥对应的账号'
}); 
console.log(r)
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exdestroy({
      symbol: '8,QE@dreamheartlx'
    },{
        authorization: '私钥对应的账号'
    })
});
```

备注：销毁通证需要**流通量为0**的时候才可以销毁，也就是说通证发行方需要收回市场上所有流通的通证后才能销毁通证。

## exchange

通证兑换

#### 参数

| name         | type   | description      |
| ------------ | ------ | ---------------- |
| **owner**    | string | 兑换账号         |
| **quantity** | string | 兑换通证数量     |
| **tosym**    | string | 兑换通证目标类型 |
| **memo**     | string | 兑换备注信息     |

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

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.exchangeSync('dicefobetone', '0.0130 EOS@eosio', '0.0000 FO@eosio', 'exchange FO to EOS', {
    authorization: '私钥对应的账号'
});
console.log(r)
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://api.testnet.fo',
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exchange({
      owner: 'dicefobetone',
      quantity: '0.0130 EOS@eosio',
      tosym: '0.0000 FO@eosio',
      memo: 'exchange FO to EOS'
    },{
        authorization: '私钥对应的账号'
    })
});
```



## ctxrecharge

合约子钱包 — 充值

#### 参数

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **owner**    | string | 账户拥有者   |
| **quantity** | string | 充值通证数量 |
| **memo**     | string | 附言         |

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

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.ctxrechargeSync('dreamheartlx', '100.0000 QQQ@dreamheartlx','ctxrecharge', {
    authorization: '私钥对应的账号'
});
console.log(r)
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.ctxrecharge({
      owner: 'dreamheartlx',
      quantity: '100.0000 QQQ@dreamheartlx',
      memo: 'ctxrecharge'
    },{
        authorization: '私钥对应的账号'
    })
});
```



## ctxextract

合约子钱包 — 提现

#### 参数

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **owner**    | string | 账户拥有者   |
| **quantity** | string | 提现通证数量 |
| **memo**     | string | 附言         |

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

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.ctxextractSync('lixunlixunli', '0.000100 LIU@lixunlixunli','ctxextract', {
    authorization: '私钥对应的账号'
});
console.log(r)
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.ctxextract({
      owner: 'lixunlixunli',
      quantity: '0.000100 LIU@lixunlixunli',
      memo: 'ctxextract'
    },{
        authorization: '私钥对应的账号'
    })
});
```



## ctxtransfer

合约子钱包 — 转账

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **from**     | string | 通证转出方  |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

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

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.ctxtransferSync('lixunlixunli','dreamheartlx','1.0000 ZX@lixunlixunli','ctxtransfer', {
    authorization: '私钥对应的账号'
});
console.log(r)
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.ctxtransfer({
      from: 'lixunlixunli',
      to: 'dreamheartlx',
      quantity: '1.0000 ZX@lixunlixunli',
      memo: 'ctxtransfer'
    },{
        authorization: '私钥对应的账号'
    })
});
```



## exunlock

解锁

#### 参数

| name           | type      | description      |
| -------------- | --------- | ---------------- |
| **owner**      | string    | 通证持有者       |
| **quantity**   | string    | 解锁数量         |
| **expiration** | date-time | 待解锁通证锁仓期 |
| **memo**       | string    | 附言             |

#### 示例

fibos.js 环境下：

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const fibos_client = FIBOS({
  // fibos 测试网 chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://api.testnet.fo',
});

let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.exunlockSync('fibostest123', '100.0000 ADC@nmslwsndhjyz', '2018-11-25T01:00:00', 'unlock 100.0000 ADC', {
    authorization: '私钥对应的账号'
})
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exunlock({
      owner: 'fibostest123',
      quantity: '100.0000 ADC@nmslwsndhjyz',
      expiration: '2018-11-25T01:00:00',
      memo: 'unlock 100.0000 ADC'
    },{
        authorization: '私钥对应的账号'
    })
});
```



## exlocktrans

锁仓转账

#### 参数

| name              | type      | description    |
| ----------------- | --------- | -------------- |
| **from**          | string    | 锁仓通证转出方 |
| **to**            | string    | 锁仓通证转入方 |
| **quantity**      | string    | 通证数量       |
| **expiration**    | date-time | 待转出锁仓时间 |
| **expiration_to** | date-time | 待转入锁仓时间 |
| **memo**          | string    | 附言           |

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

let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.exlocktransSync('nmslwsndhjyz', 'fibostest123', '10000.0000 BBB@5hzuyqumr3l5', '2018-10-29T18:54:00', '2018-10-29T18:54:00', 'exlocktrans 10000 BBBC@uepgdzfhucin', {
    authorization: '私钥对应的账号'
}); //expiration_to必须大于等于expiration
console.log(r)
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

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exlocktrans({
      from: 'nmslwsndhjyz',
      to: 'fibostest123',
      quantity: '10000.0000 BBB@5hzuyqumr3l5',
      expiration: '2018-10-29T18:54:00',
      expiration_to: '2018-10-29T18:54:00',
      memo: 'exlocktrans 10000 BBB@uepgdzfhucin'
    },{
        authorization: '私钥对应的账号'
    })
});
```



## receipt

凭据

#### 参数

| name    | type   | description  |
| ------- | ------ | ------------ |
| **in**  | string | 转入通证凭据 |
| **out** | string | 转出通证凭据 |

#### 示例

```json
"data":{
    "in":{
        "quantity":string"11460.9004 FO"
        "contract":string"eosio"
    }
    "out":{
        "quantity":string"19.8374 EOS"
        "contract":string"eosio"
    }
    "fee":{
        "quantity":string"0.0000 FO"
        "contract":string"eosio"
    }
}
```



## snapshot

快照

#### 参数

| name                          | type    | description          |
| ----------------------------- | ------- | -------------------- |
| **contract**                  | string  | 发币持有者           |
| **max_supply**                | string  | 最大可发行通证数量   |
| **cw**                        | float64 | cw 值                |
| **max_exchange**              | string  | 最大兑换通证数量     |
| **supply**                    | string  | 可发行通证数量       |
| **reserve_supply**            | string  | 锁仓通证数量         |
| **connector_balance**         | string  | 保证金数量           |
| **reserve_connector_balance** | string  | 未流通通证保证金数量 |

```json
"data":{
    "contract":string"eosio"
    "max_supply":string"100000000000.0000 FO"
    "cw":string"0.10944270133906281"
    "max_exchange":string"10027436399.4393 FO"
    "supply":string"350892935.0365 FO"
    "reserve_supply":string"5027379795.1377 FO"
    "connector_balance":string"468809.4805 EOS"
    "reserve_connector_balance":string"550000.0000 EOS"
}
```

