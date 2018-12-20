---
title: 兑换
type: tutorials
order: 251
---

> 如果你只是普通用户而不是开发者，可以通过 FO 钱包兑换。[下载 FO 钱包](http://wallet.fo/) ，先选择你要兑换的源智能通证，输入要兑换的数量，再选择你要兑换的目标通证。点击兑换，稍等片刻即可兑换成功。

## 通证互兑

整个兑换过程是在 FIBOS 主网执行，所以使用的是执行过程中使用的是 FIBOS 主网的私钥以及账户信息。

```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
    priKey: '你的 FIBOS 主网私钥',
    httpEndpoint: 'http://ca-rpc.fibos.io:8870',
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
let result = ctx.exchangeSync(owner, quantity, tosymbol, memo);
```

**方法说明:**

使用 `exchangeSync()` 方法，在 FIBOS 使用 Bancor 进行通证之间兑换

**参数说明:**

| 参数     | 含义             |
| -------- | ---------------- |
| owner    | 兑换账号         |
| quantity | 兑换通证数量     |
| tosymbol | 兑换通证目标类型 |
| memo | 兑换备注信息 |

假设用户 `fibostest123` 发行了一个智能通证叫做 `VAYNE` ，用户 `fibostest321` 发行了一个叫做了 `HASAKI` 的智能通证。那么用户 `fibostest123` 想要用 `VAYNE` 兑换得到一定数量的 `HASAKI` 是怎么实现的呢？调用接口 `exchangeSync` 接口进行兑换。

```javascript
//初始化 FIBOS 客户端
...
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.exchangeSync(
    'fibostest123',
    '1.0000 VAYNE@fibostest123',
    '0.0000 HASAKI@fibostest321',
    'exchenge VAYNE to HASAKI',
    {
        authorization: 'fibostest123'
    });
```

如果想要兑换成 `FIBOS` 中的 `EOS` 通证，那么只需将 `0.0000 HASAKI@fibostst321` 换成 `0.0000 EOS@eosio` 即可。



##  EOS 通证兑换 FO 通证

### 发起 EOS 兑换 FO

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let owner = '你的 FIBOS 账户名';
let eos2fo_quantity = '10.0000 EOS@eosio';
let memo = 'exchange EOS to FO';

var result = ctx.exchangeSync(owner, eos2fo_quantity ,'0.0000 FO@eosio', memo, {
    authorization: owner
});
console.log(result);
```

### 查询兑换的 FO 通证

```javascript
var rs = fibos_client.getTableRowsSync(true, 'eosio.token', '你的 FIBOS 账户名', 'accounts');
console.log(rs);
```



## FO 通证兑换 EOS 通证

### 发起 FO 兑换 EOS

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let owner = '你的 FIBOS 账户名';
let fo2eos_quantity = '10.0000 FO@eosio';
let memo = 'exchange FO to EOS';

var result = ctx.exchangeSync(owner, fo2eos_quantity, `0.0000 EOS@eosio`, memo, {
    authorization: owner
});
console.log(result);
```

### 查询兑换的 EOS 通证

```javascript
var rs = fibos_client.getTableRowsSync(true, 'eosio.token', '你的 FIBOS 账户名', 'accounts');
console.log(rs);
```



## 钱包一键兑换

[下载 FO 钱包](http://wallet.fo/) ，先选择你要兑换的源智能通证，输入要兑换的数量，再选择你要兑换的目标通证，点击兑换，稍等片刻即可兑换成功。