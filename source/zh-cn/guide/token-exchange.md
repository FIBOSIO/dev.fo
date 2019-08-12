---
title: 兑换
type: tutorials
language: zh-cn
order: 251
---

> 如果你只是普通用户而不是开发者，可以通过 FO 钱包兑换。[下载 FO 钱包](http://wallet.fo/) ，先选择你要兑换的源智能通证，输入要兑换的数量，再选择你要兑换的目标通证。点击兑换，稍等片刻即可兑换成功。

## 通证互兑

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
let result = ctx.exchangeSync(owner, quantity, to, price, id, memo);
```

**方法说明:**

使用 `exchangeSync()` 方法，在 FIBOS 使用 Bancor / uniswap 进行通证之间兑换

该接口既支持 Bancor 协议，也支持 uniswap 协议。

**参数说明:**

| 参数     | 含义             |
| -------- | ---------------- |
| owner    | 兑换账号         |
| quantity | 兑换通证数量     |
| to| 兑换通证目标数量 |
| price| 价格(仅在 uniswap 限价交易中填值) |
| id | 渠道商 id (仅在 uniswap 交易中使用) |
| memo | 兑换备注信息 |

**需要说明的是，在 Bancor 兑换中，`to` 填入目标通证为0的值，假设我需要兑换 FO，则填入`0.0000 FO@eosio`；`price`填`0.0`；`id`填`owner`即可。**

假设用户 `fibostest123` 发行了一个智能通证叫做 `VAYNE` ，用户 `fibostest321` 发行了一个叫做了 `HASAKI` 的智能通证。那么用户 `fibostest123` 想要用 `VAYNE` 兑换得到一定数量的 `HASAKI` 是怎么实现的呢？调用接口 `exchangeSync` 接口进行兑换。

```javascript
//初始化 FIBOS 客户端
...
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.exchangeSync(
    'fibostest123',
    '1.0000 VAYNE@fibostest123',
    '0.0000 HASAKI@fibostest321',
    '0.0',
    'fibostest123',
    'exchenge VAYNE to HASAKI',
    {
        authorization: 'fibostest123'
    });
```

如果想要兑换成 `FIBOS` 中的 `EOS` 通证，那么只需将 `0.0000 HASAKI@fibostst321` 换成 `0.0000 EOS@eosio` 即可。

## uniswap 交易

👉 见【[ uniswap 交易](token-uniswap.html)】部分


## 钱包一键兑换

[下载 FO 钱包](http://wallet.fo/) ，先选择你要兑换的源智能通证，输入要兑换的数量，再选择你要兑换的目标通证，点击兑换，稍等片刻即可兑换成功。