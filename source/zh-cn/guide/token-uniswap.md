---
title: uniswap
type: tutorials
language: zh-cn
order: 250
---

## uniswap 交易
> 在 uniswap 的所有接口中，tokenx 与 tokeny 的顺序并不影响执行结果。例如，`FO@eosio - EOS@eosio`和`EOS@eosio - FO@eosio`属于同一个市场。
### 加仓

整个兑换过程是在 FIBOS 主网执行，所以执行过程中使用的是 FIBOS 主网的私钥以及账户信息。

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

#### 调用方法:

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.addreservesSync(owner, tokenx, tokeny);
```

#### 方法说明:

使用 `addreservesSync()` 方法，可以为 uniswap 市场进行加仓，特殊的，如果没有该市场，则会创建该市场。

#### 参数说明:

| 参数     | 含义             |
| -------- | ---------------- |
| owner    | 操作账户         |
| tokenx | x 通证     |
| tokeny|  y 通证|
#### 限制：

以下所有的限制均不包含常规限制，例如权限不对，精度不对等。本文提到的限制都是特定的限制。

- 已成为`bancor`交易市场的，不能再成为`uniswap`的交易市场。否则报错。
- 加仓后正负价格不能超过 0.1%。否则报错。
- 加仓后个人权重增加必须大于0。否则报错。

该行为会对 X-Y 的 uniswap 通证市场进行加仓，如果该市场不存在，则会创建该市场。

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

#### 市场份额表查询：
```javascript
fibos.getTableRowsSync(true, "eosio.token", "eosio.token", "swapmarket")
// output:
{
  "rows": [
    {
      "primary": 0,
      "tokenx": {
        "quantity": "140.0000 FO",
        "contract": "eosio"
      },
      "tokeny": {
        "quantity": "10030.0000 EOS",
        "contract": "eosio"
      },
      "total_weights": "11849.89451429842847574"
    }
  ],
  "more": false
}
```

```js
fibos.getTableRowsSync(true, "eosio.token", 0, "swappool") // 此处的"0"对应的对应币币对的 primary
// output:
{
  "rows": [
    {
      "owner": "fibos",
      "weights": "11356.56329871202615323"
    },
    {
      "owner": "user1",
      "weights": "493.33121558640181092"
    }
  ],
  "more": false
}
```
上例的情况是，`EOS@eosio-FO@eosio`的`uniswap`的市场中，`EOS@eosio`的总额为`10030.0000 EOS`，`FO@eosio`的总额为`140.0000 FO`，所有持仓者总权重为`11849.89451429842847574`。

在该市场中，有两个持仓者，分别为`fibos`和`user1`。他们在总市场中的权重分别为`11356.56329871202615323`和`493.33121558640181092`。

### 提仓

**调用方法:**

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.outreservesSync(owner, symbolx, symboly, rate);
```

**方法说明:**

使用 `outreservesSync()` 方法，可以在特定的 uniswap 市场中进行提仓，提出我们在该 uniswap 市场中的份额。

**参数说明:**

| 参数     | 含义             |
| -------- | ---------------- |
| owner    | 操作账户         |
| symbolx | x 通证     |
| symboly|  y 通证|
| rate|  提取比例|

#### 限制：

- $0<rate\leq1$。否则报错。
- 该`uniswap`必须存在。否则报错。
- 该用户在该`uniswap`市场中必须拥有份额。否则报错。
- 用户提取出来的`token`数必须大于该币种的最小精度。否则报错。
- 用户提取结束后剩余的权重必须大于总权重部分的0.1%。否则报错。

该行为会对 X-Y 的 uniswap 通证市场进行提仓，通过`rate`比例提出我们自己的通证份额。
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
在上面的例子中，我们在`FO@eosio-EOS@eosio`的 uniswap 市场进行提仓，比例为`0.1`。操作过后，我们会按`个人权重/总权重 * rate`的比例等比得提取该市场中`FO@eosio`通证数量和`EOS@eosio`通证数量。


#### 公式说明：

在 `uniswap`市场中，用户所拥有的`token`份额以权重的形式展示。在减仓的时候**不能**设置提取某一个数额的`token`出来，只能设置提取的比例，按照对应的比例获得对应的币币对。详细公式见下：

$$
\begin{gather}
a\times{b}=S\\
填仓:\; a_{new}\times{b_{new}}=S_{new}\\
计算权重：\;\frac{\sqrt{S_{new}}-\sqrt{S}}{\sqrt{S}}\times{weights}\\
减仓比例：\;r=\frac{weigehts_{个人}}{weights_{全部}}\times{rate}_{传入值}\\
减仓提取：(a_{new}\times{r})\quad(b_{new}\times{r})
\end{gather}
$$

### 市价交易\限价交易

uniswap 的市价交易、限价交易和 Bancor 共用`exchange`接口。
| 参数     | 含义             |
| -------- | ---------------- |
| owner    | 操作账户        |
| quantity | 兑换通证数量     |
| to | 兑换通证目标数量 |
| price | 价格(仅在 uniswap 限价交易中填值) |
| id | 渠道商 id (仅在 uniswap 交易中使用) |
| memo | 兑换备注信息 |

#### 限制

- `bancor` 交易和 `uniswap`共用一个接口，**互为`bancor`交易对的不可以做`uniswap`交易**。否则报错。

- 在市价交易的时候，**`quantity`的值必须不为0，`to`和`price`的值必须为0**。否则报错。
- 在限价交易的时候，**`price`的价值必须不为0，`quantity`和`to`二者必须有且只一个值**。否则报错。
- 该`uniswap`市场必须存在。负责报错。
- 用户兑换出来的`token`数必须大于该币种的最小精度。否则报错。

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
上面的例子中，用户`fibos`想用`200.0000 EOS@eosio`兑换`FO@eosio`，不论价格是多少，兑换完`200.0000 EOS@eosio`为止。

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
上面的例子中，用户`fibos`需要以不高于`1.2`的价格兑换出`100.0000 FO@eosio`。对于高于`1.2`的价格，仍未兑换完的部分，则会挂单。

#### 挂单表查询示例：
```js
fibos.getTableRowsSync(true, "eosio.token", 0, "swaporder")

// output:
{
  "rows": [
    {
      "primary": 0,
      "owner": "fibos",
      "price": "4294967296", 
      "quantity": {
        "quantity": "100.0000 EOS",
        "contract": "eosio"
      }
    }
  ],
  "more": false
}
```

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
撤单会撤销用户的此 ID 的挂单，挂单金额打回账户
