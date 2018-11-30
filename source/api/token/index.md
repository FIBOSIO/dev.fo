---
title: 
type: token
order: 1
---

# Eosio.token Contract

## transfer

转账

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **from**     | string | 通证转出方  |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

####  示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.transfer({
      from: "fibforjeremy",
      to: "fiboscouncil",
      quantity: "20.3375 EOS",
      memo: "eosforjeremy"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## issue

增发

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 通证附言    |

####  示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.issue({
      to: "eosio",
      quantity: "34341.6961 FO",
      memo: "issue tokens for producer pay and savings"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## retire

销毁

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.retire({
      quantity: 'asset',
      memo: 'string'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## create

发行通证

#### 参数

| name               | type   | description        |
| ------------------ | ------ | ------------------ |
| **issuer**         | string | 通证发行账号       |
| **maximum_supply** | string | 最大可发行通证数量 |

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.create({
      issuer: "eosio",
      maximum_supply: "10000000000.0000 EOS"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## close

回收内存

#### 参数

| name       | type   | description  |
| ---------- | ------ | ------------ |
| **owner**  | string | 通证拥有者   |
| **symbol** | string | 通证目标类型 |

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.close({
      owner: 'account_name',
      symbol: 'symbol'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
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

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.extransfer({
      from: "dicefobetone",
      to: "zhangjingrui",
      quantity: {"quantity":"1.5076 FO","contract":"eosio"},
      memo: "4<66 你中奖啦！"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## exissue

增发通证

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exissue({
      to: "dogfallchina",
      quantity: {"quantity":"100000.0000 TAO","contract":"dogfallchina"},
      memo: ""
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## exretire

销毁流通通证

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **from**     | string | 通证转出方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exretire({
      from: "createtest11",
      quantity: {"quantity":"0.0067 FO","contract":"eosio"},
      memo: "issue tokens for producer pay and savings"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
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
| **reserve_supply**            | string    | 未流通通证数量             |
| **reserve_connector_balance** | string    | 未流通通证保证金数量       |
| **expiration**                | date-time | 项目方预设的项目锁仓期     |

#### 示例

```javascript
const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.excreate({
      issuer: "dogfallchina",
      maximum_supply: "100000.0000 TAO",
      connector_weight: "0.00000000000000000",
      maximum_exchange: "0.0000 TAO",
      reserve_supply: "0.0000 TAO",
      reserve_connector_balance: "0.0000 FO",
      expiration: "2018-11-25T07:47:39"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## exclose

回收内存

#### 参数

| name       | type   | description  |
| ---------- | ------ | ------------ |
| **owner**  | string | 通证拥有者   |
| **symbol** | string | 通证目标类型 |

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exclose({
      owner: "dreamheartlx",
      symbol: {"sym":"4,ZC","contract":"lixunlixunli"}
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## exdestroy

销毁通证

#### 参数

| name       | type   | description  |
| ---------- | ------ | ------------ |
| **symbol** | string | 通证目标类型 |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exdestroy({
      symbol: {"sym":"8,QE","contract":"dreamheartlx"}
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



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

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exchange({
      owner: "dicefobetone",
      quantity: {"quantity":"0.0130 FO","contract":"eosio"},
      tosym: {"sym":"4,BET","contract":"dicefobetone"},
      memo: "看到没？我回购了，BET兑FO价格又上涨一点点，你丫手里BET又值钱一点点"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
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

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.ctxrecharge({
      owner: "dreamheartlx",
      quantity: {"quantity":"0.10000000 QQQ","contract":"dreamheartlx"},
      memo: ""
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
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

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.ctxextract({
      owner: "lixunlixunli",
      quantity: {"quantity":"0.000100 LIU","contract":"lixunlixunli"},
      memo: ""
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
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

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.ctxtransfer({
      from: "lixunlixunli",
      to: "dreamheartlx",
      quantity: {"quantity":"1.0000 ZX","contract":"lixunlixunli"},
      memo: "ctxtransfer"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## exunlock

解锁

#### 参数

| name           | type      | description |
| -------------- | --------- | ----------- |
| **owner**      | string    | 通证持有者  |
| **quantity**   | string    | 解锁数量    |
| **expiration** | date-time | 锁仓期      |
| **memo**       | string    | 附言        |

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exunlock({
      owner: "liyuchen1234",
      quantity: {"quantity":"0.5911 BET","contract":"dicefobetone"},
      expiration: "2018-11-25T01:00:00",
      memo: ""
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## exlocktrans

锁仓转账

#### 参数

| name              | type      | description    |
| ----------------- | --------- | -------------- |
| **from**          | string    | 通证转出方     |
| **to**            | string    | 通证转入方     |
| **quantity**      | string    | 通证数量       |
| **expiration**    | date-time | 待转出锁仓时间 |
| **expiration_to** | date-time | 待转入锁仓时间 |
| **memo**          | string    | 附言           |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exlocktrans({
      from: "dicefobetone",
      to: "eosjianqiang",
      quantity: {"quantity":"0.0008 BET","contract":"dicefobetone"},
      expiration: "1970-01-01T00:00:00",
      expiration_to: "2018-12-02T01:00:00",
      memo: "记得每周日09:00后自己去钱包解锁哟，解锁后，可以去砸盘换FO"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## receipt

凭据

#### 参数

| name    | type   | description  |
| ------- | ------ | ------------ |
| **in**  | string | 转入通证凭据 |
| **out** | string | 转出通证凭据 |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.receipt({
      in: {"quantity":"11555.0000 FO","contract":"eosio"},
      out: {"quantity":"20.3375 EOS","contract":"eosio"}
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
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

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.snapshot({
      contract: "eosio",
      max_supply: "100000000000.0000 FO",
      cw: "0.10948151574745998",
      max_exchange: "10025528533.6595 FO",
      supply: "361950483.2024 FO",
      reserve_supply: "5025476157.1198 FO",
      connector_balance: "488116.9226 EOS",
      reserve_connector_balance: "550000.0000 EOS"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```

