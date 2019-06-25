---
title: 转账
type: tutorials
language: zh-cn
order: 250
---

## 链内转账

转账的目标账户必须要在 FIBOS 中存在，且转账的最大数量不能超过你的余额，精度也要与转账的 Token 精度一致。

调用 `extransfer` 方法，方法和参数名如下：

| 参数     | 含义       |
| -------- | ---------- |
| from     | 通证转入方 |
| to       | 通证转出方 |
| quantity | 通证数量   |
| meno     | 附言       |

```javascript
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
var r = ctx.extransferSync(
    'fibostest123',  //通证转入方
    'fibostest321',   //通证转出方
    '10.0000 ADC@fibostest123',  //通证数量
    'trasnfer to fibostest321',  //附言
    {
  authorization: 'fibostest123'
});
console.log(r);
```



## 跨链转账


>重要提示：为防止出现跨链转账失败的情况：
>1. 请勿直接通过交易所转账（建议使用 EOS 钱包转账），通过交易所转账时，一旦遇到 memo 填写错误的情况，则资产将会丢失且无法找回！
>2. 请再三确认 memo 的填写是否正确（memo请填写“您在 FIBOS 主网已注册成功的账户名”），一旦填错，可能会导致资产丢失：
>3. 如果因您填写的 memo 账户不存在，导致资产丢失，则系统查到后，会将这笔资产转回您的打款账户；
>4. 如果您填写的 memo 错误，但正好是其他人的 FIBOS 账户，那么很抱歉，这笔资产将无法转回您的账户。

### 从 EOS 到 FIBOS 的跨链转账

使用 EOS 主网的账户向 EOS 账户(fiboscouncil) 发起转账，memo 的内容填写 FIBOS 主网已经注册账户名称，即可完成一次跨链转账。

#### 在 EOS 主网发起转账操作

EOS 主网 RPC 地址(建议)：http://api-mainnet.starteos.io

```javascript
var FIBOS = require('fibos.js');

var config = {
    chainId: 'aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906',
    priKey: '你的 EOS active权限私钥',
    httpEndpoint: 'http://api-mainnet.starteos.io',
    verbose: false,
};

var eos_client = FIBOS({
    chainId: config.chainId,
    keyProvider: config.priKey,
    httpEndpoint: config.httpEndpoint,
    verbose: false,
    logger: {
        log: null,
        error: null
    }
})
let eosaccount = '' // 你的 EOS 账户名
let value = '1.0000 EOS'; //转账给 fiboscouncil 账户的数量
let ctx = eos_client.contractSync('eosio.token');
let memo = 'fibosmainnet'; //填入已注册的 FIBOS 账号
let result = ctx.transferSync(eosaccount, 'fiboscouncil', value, memo, {
    authorization: eosaccount
});
console.log(result);
```

**实例说明:**

实例操作中,配置好 EOS MainNet 和 EOS RPC 地址 和 EOS 私钥后,便初始化了一个 eos 客户端,通过调用 `transferSync` 方法,传入四个参数:

| 参数           | 含义                     |
| -------------- | ------------------------ |
| eosaccount     | 转出方                   |
| fiboscouncil   | 转入方                  |
| value          | 数量：1.0000 EOS         |
| memo           | 填入已注册的 FIBOS 账号 |

#### 在 FIBOS 主网查询转账信息

从 EOS 主网发起的跨链转账后，需要等待300个左右的安全区块时间，大约2分钟，才能在 FIBOS 主网查询到转账信息。

使用 FIBOS 的客户端查询，使用的是 FIBOS 主网的 chainID 以及 RPC 接口地址。


```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
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
var rs = fibos_client.getTableRowsSync(true, 'eosio.token', '你的 FIBOS 账户名', 'accounts');
console.log(rs);
```

**实例说明:**

配置了 FIBOS 主网的 chainId 和 Http 服务地址后,便初始化了一个 FIBOS 客户端,调用 `getTableRowsSync` 方法，查询账户的资产信息。

### 从 FIBOS 到 EOS 的跨链转账

使用 FIBOS 主网的账户向 EOS 账户(fiboscouncil) 发起转账，memo 的内容填写 EOS 主网已经注册账户名称，即可完成一次跨链转账。

#### 在 FIBOS 主网发起转账操作

**调用方法:**

```javascript
let ctx = client.contractSync('eosio.token');
let result = ctx.transferSync(eosaccount, 'fiboscouncil', value, memo);
```

**方法说明:**

使用 fibos.js 客户端 调用 eosio.token 合约发起一笔转账操作

**参数说明**

| 参数           | 含义                   |
| -------------- | ---------------------- |
| eosaccount     | 转出方                 |
| fiboscouncil   | 指定转入方             |
| value          | 数量:1.0000 EOS        |
| memo           | 备注:填入你已注册的 EOS 账号名 |


```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
    priKey: '你的 FIBOS 私钥',
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
let fibosaccount = '' // 你的 FIBOS 账户名
let value = '1.0000 EOS'; //转账 EOS 数量
let ctx = fibos_client.contractSync('eosio.token');
let memo = 'eoseoseoseos'; //填入你已注册的 EOS 账号
let result = ctx.transferSync(fibosaccount, 'fiboscouncil', value, memo, {
    authorization: fibosaccount
});
console.log(result);
```

#### 在 EOS 主网查询转账信息

从 FIBOS 主网发起的跨链转账后，需要等待300个左右的安全区块时间，大约2分钟，才能在 EOS 主网查询到转账信息。

使用 EOS 的客户端查询，使用的是 EOS 主网的 chainID 以及 RPC 接口地址。

```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: 'aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906',
    httpEndpoint: 'http://api-mainnet.starteos.io',
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
var rs = fibos_client.getTableRowsSync(true, 'eosio.token', '你的 EOS 账户名', 'accounts');
console.log(rs);
```


**实例说明:**

配置了 EOS 主网的 chainId 和 RPC 服务地址后,便初始化了一个 EOS 客户端,调用 `getTableRowsSync`方法，查询账户的资产信息。
