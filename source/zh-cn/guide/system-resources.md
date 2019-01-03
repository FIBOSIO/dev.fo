---
title: 资源
type: tutorials
language: zh-cn
order: 240
---

FIBOS的资源分为两种类型：一种是抵押型资源，包括CPU和NET；另一种是消耗性资源，叫做RAM，也称存储。

用户拥有发布一个合约的资源，包括足够的 RAM、CPU 和 NET。

## 内存和资源

### 内存（RAM）

- RAM 是在区块链上存储数据的必备资源，需要用户向系统购买，存储的数据越多，需要的 RAM 越多。
- RAM的价格是由市场决定的，RAM的价格会根据市场自动的调整，当程序使用完RAM的时候，可以释放RAM空间，并以当前市场价卖出。
- 不论是购买 RAM，还是卖出 RAM，都是参与者与系统账户之间的交互，而不是直接的市场交易行为。只是，价格会按照bancor算法来决定。

### 网络宽带（Network Bandwidth）

- 用户可以通过抵押更多的 FO，来获得更大的带宽。也可以随时取消抵押，降低网络带宽，并取回 FO。
- 网络带宽，可以比作手机流量的 “使用量”。可以根据需求，灵活的按需获取。

### CPU 宽带（CPU Bandwidth）

- CPU带宽，用来衡量你最近3天内，合约执行过程中的运算时间消耗（按毫秒计算）。
- CPU带宽和网络带宽一样，是一个临时性的消耗。当调用量减少时，消耗随之减少，最小可以降到0。
- 随时可以通过抵押 FO，来获得更大的 CPU，以及取消抵押来降低 CPU，并取回抵押的 FO。



## 如何购买内存、抵押资源

### 购买内存

1. 在链上存贮账户信息是需要消耗内存的，创建者需为被创建者购买内存来存放新账户的信息。

通过调用 `buyrambytes` 方法，参数和解释说明如下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.buyrambytesSync({
      payer: "fibosmaster1",  //创建者的账户名
      receiver: "yunyu1212122", //被创建者的账户名
      bytes: 4096  //购买的内存大小（字节）
},{
    authorization: '私钥对应的账号' 
});
console.log(r);
```

2. 购买存储资源，区别是买特定数量的通证还是买特定大小的内容。

通过调用 `buyram` 方法，参数和解释说明如下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.buyramSync({
      payer: "silver123451", //购买存储资源的账号
      receiver: "silver123451", //接受存储资源的账号
      quant: "0.1273 FO" //购买存储资源所用的通证数量
},{
    authorization: '私钥对应的账号' 
});
console.log(r);
```



### 抵押资源

创建者为被创建者抵押 FO 获取 CPU 和 NET ，让新账户能够进行转账。

通过调用 `delegatebw` 方法，参数和解释说明如下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.delegatebwSync({
      from: "slowmistioio",  //资源抵押者的账户名
      receiver: "slowmistioio",  //资源接受者的账户名
      stake_net_quantity: "3193.0000 FO",  //抵押者为接受者抵押 FO 获取 NET
      stake_cpu_quantity: "30000.0000 FO",  //  抵押者为接受者抵押 FO 获取 CPU
      transfer: 0  // 代表抵押资源同时是否将对应通证转账给接受者
},{
    authorization: '私钥对应的账号' 
});
console.log(r);
```



### 取消抵押

用来解除抵押，释放资源，收回通证。

通过调用 `updelegatebw` 方法，参数和解释说明如下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.undelegatebwSync({
      from: 'hoffercq1211',  //解除用哪个账号所抵押的通证
      receiver: 'hoffercq1211',  //解除作用在哪个账号上的抵押通证
      unstake_net_quantity: '649540.0000 FO', //解除用来获取带宽资源的通证数量
      unstake_cpu_quantity: '649540.0000 FO' //解除用来获取计算资源的通证数量
},{
    authorization: '私钥对应的账号' 
});
console.log(r);
```



### 出售资源

通过调用 `sellram` 方法，参数和解释说明如下：

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.sellramSync({
      account: "silver123451", //出售资源通证的接受账号
      bytes: 789438000 //出售多少空间的存储资源
},{
    authorization: '私钥对应的账号' 
});
console.log(r);
```
