---
title: uniswap
type: tutorials
language: zh-cn
order: 250
---

## uniswap 交易
> 在 uniswap 的所有接口中，tokenx 与 tokeny 的顺序并不影响执行结果。例如，`FO@eosio - EOS@eosio`和`EOS@eosio - FO@eosio`属于同一个市场。
### 加仓

整个兑换过程是在 FIBOS 主网执行，所以使用的是执行过程中使用的是 FIBOS 主网的私钥以及账户信息。

```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
    priKey: '你的 FIBOS 主网私钥',
    httpEndpoint: 'http://api.testnet.fo',
    verbose: false,
}
var fibos_client = FIBOS({
    chainId: config.chainId,
    keyProvider: config.priKey,
    httpEndpoint: config.httpEndpoint,
    verbose: false,
    logger: {
        log: null,
        error: null
    }
})
```

**调用方法:**

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.addreservesSync(owner, tokenx, tokeny);
```

**方法说明:**

使用 `addreservesSync()` 方法，可以为 uniswap 市场进行加仓，特殊的，如果没有该市场，则会创建该市场。

**参数说明:**

| 参数     | 含义             |
| -------- | ---------------- |
| owner    | 加仓账号         |
| tokenx | x 通证     |
| tokeny|  y 通证|

该行为会对 X-Y 的 uniwap 通证市场进行加仓，如果该市场不存在，则会创该市场。
```javascript
//初始化 FIBOS 客户端
...
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.addreservesSync(
    "fibos", 
    "20.0000 FO@eosio", 
    "10.0000 EOS@eosio", {
    authorization: "fibos"
});
```
在上面的例子中，我们为`FO@eosio-EOS@eosio`的 uniswap 市场进行加仓，数额分别是`20.0000 FO@eosio`和`10.0000 EOS@eosio`。同样的，如果没有该市场，则会创建`FO@eosio-EOS@eosio`的 uniswap 市场。

### 减仓

**调用方法:**

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.outreservesSync(owner, symbolx, symboly, rate);
```

**方法说明:**

使用 `outreservesSync()` 方法，可以在特定的 uniswap 市场中进行减仓，提出我们在该 uniswap 市场中的份额。

**参数说明:**

| 参数     | 含义             |
| -------- | ---------------- |
| owner    | 加仓账号         |
| symbolx | x 通证     |
| symboly|  y 通证|
| rate|  提取比例|

该行为会对 X-Y 的 uniwap 通证市场进行减仓，通过`rate`比例提出我们自己的通证份额。
```javascript
//初始化 FIBOS 客户端
...
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.outreservesSync(
    name, 
    "0.0000 FO@eosio", 
    "0.0000 EOS@eosio", 
    0.1, { 
    authorization: name
});
```
在上面的例子中，我们在`FO@eosio-EOS@eosio`的 uniswap 市场进行减仓，减仓比例为`0.1`。操作过后，我们会按`个人权重/总权重 * rate`的比例等比得提取该市场中`FO@eosio`通证数量和`EOS@eosio`通证数量。

### 市价交易\限价交易

市价交易、限价交易和 Bancor 共用`exchange`接口。
| 参数     | 含义             |
| -------- | ---------------- |
| owner    | 兑换账号         |
| quantity | 兑换通证数量     |
| to | 兑换通证目标数量 |
| price | 价格(仅在 uniswap 限价交易中填值) |
| id | 渠道商 id (仅在 uniswap 交易中使用) |
| memo | 兑换备注信息 |
在市价交易的时候，`quantity的`值必须不为0，`to`和`price`的值必须为0。

在限价交易的时候，`price`的值必须不为0，`quantity`和`to`二者必须有且只一个值。

市价交易：
```javascript
//初始化 FIBOS 客户端
...
let ctx = fibos_client.contractSync('eosio.token');
ctx.exchangeSync(
    "fibos", 
    "200.0000 EOS@eosio", 
    "0.0000 FO@eosio", 
    0,
    'fibos',
    "test", {
    authorization: "fibos"
});
```
上面的例子中，用户`fibos`需要用`200.0000 EOS@eosio`兑换`FO@eosio`，不论价格是多少，兑换完`200.0000 EOS@eosio`为止。

限价交易：
```javascript
//初始化 FIBOS 客户端
...
let ctx = fibos_client.contractSync('eosio.token');
ctx.exchangeSync(
    "fibos", 
    "0.0000 EOS@eosio", 
    "100.0000 FO@eosio", 
    1.2, 
    "fibos", 
    "uniswap ", {
   authorization: "fibos"
});
```
上面的例子中，用户`fibos`需要以不高于`1.2`的价格兑换出`100.0000 FO@eosio`。对于高于`1.2`的价格，扔未兑换完的部分，则会挂单。

### 撤单
**调用方法:**

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.withdrawSync(name, symbolx, symboly, bid_id);
```

**方法说明:**

使用 `withdrawSync()` 方法，可以在 uniswap 市场撤销自己的挂单。

**参数说明:**

| 参数     | 含义             |
| -------- | ---------------- |
| owner    | 撤单账号         |
| symbolx | x 通证     |
| symboly|  y 通证|
| bid_id|  撤单id|

```javascript
//初始化 FIBOS 客户端
...
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.withdrawSync(
    "fibos",
    "0.0000 FO@eosio", 
    "0.0000 EOS@eosio", 
    bid_id, {
	authorization: "fibos"
});
```
在上面的例子中，我们在`FO-EOS`的 uniswap 市场进行撤销订单 ID 为 `bid_id` 的挂单。
