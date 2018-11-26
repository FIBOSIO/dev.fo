---
title: eosio.token
type: manual
order: 150
---

## transfer

转账

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **from**     | string | account_name |
| **to**       | string | account_name |
| **quantity** | string | asset        |
| **memo**     | string | /            |

####  Example

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

发行token

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **to**       | string | account_name |
| **quantity** | string | asset        |
| **memo**     | string | /            |

####  Example

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

| name         | type   | description |
| ------------ | ------ | ----------- |
| **quantity** | string | asset       |
| **memo**     | string | /           |

#### Example

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

| name               | type   | description  |
| ------------------ | ------ | ------------ |
| **issuer**         | string | account_name |
| **maximum_supply** | string | asset        |

#### Example

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

| name       | type   | description  |
| ---------- | ------ | ------------ |
| **owner**  | string | account_name |
| **symbol** | json   | symbol       |

#### Example

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

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **from**     | string | account_name   |
| **to**       | string | account_name   |
| **quantity** | json   | extended_asset |
| **memo**     | string |                |

#### Example

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
      memo: "4<66 你中奖啦！【欢迎来玩FO骰子：https://dice.fobet.one/】"
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

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **to**       | string | account_name   |
| **quantity** | json   | extended_asset |
| **memo**     | string | /              |

#### Example

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

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **from**     | string | account_name   |
| **quantity** | json   | extended_asset |
| **memo**     | string |                |

#### Example

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

| name                          | type      | description    |
| ----------------------------- | --------- | -------------- |
| **issuer**                    | string    | account_name   |
| **maximum_supply**            | string    |                |
| **connector_weight**          | float64   |                |
| **maximum_exchange**          | string    |                |
| **reserve_supply**            | string    |                |
| **reserve_connector_balance** | string    |                |
| **expiration**                | date-time | time_point_sec |

#### Example

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

| name       | type   | description     |
| ---------- | ------ | --------------- |
| **owner**  | string | account_name    |
| **symbol** | json   | extended_symbol |

#### Example

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

| name       | type | description     |
| ---------- | ---- | --------------- |
| **symbol** | json | extended_symbol |

#### Example

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

| name         | type   | description     |
| ------------ | ------ | --------------- |
| **owner**    | string | account_name    |
| **quantity** | json   | extended_asset  |
| **tosym**    | json   | extended_symbol |
| **memo**     | string | /               |

#### Example

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
      memo: "看到没？我回购了，BET兑FO价格又上涨一点点，你丫手里BET又值钱一点点，欧耶～【欢迎来玩FO骰子：https://dice.fobet.one/】"
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

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **owner**    | string | account_name   |
| **quantity** | json   | extended_asset |
| **memo**     | string | /              |

#### Example

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

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **owner**    | string | account_name   |
| **quantity** | json   | extended_asset |
| **memo**     | string | /              |

#### Example

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

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **from**     | string | account_name   |
| **to**       | string | account_name   |
| **quantity** | json   | extended_asset |
| **memo**     | string | /              |

#### Example

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

| name           | type      | description    |
| -------------- | --------- | -------------- |
| **owner**      | string    | account_name   |
| **quantity**   | json      | extended_asset |
| **expiration** | date-time | time_point_sec |
| **memo**       | string    | /              |

#### Example

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

| name              | type      | description    |
| ----------------- | --------- | -------------- |
| **from**          | string    | account_name   |
| **to**            | string    | account_name   |
| **quantity**      | json      | extended_asset |
| **expiration**    | date-time | time_point_sec |
| **expiration_to** | date-time | time_point_sec |
| **memo**          | string    | /              |

#### Example

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
      memo: "记得每周日09:00后自己去钱包解锁哟，解锁后，可以去砸盘换FO【欢迎来玩FO骰子：https://dice.fobet.one/】"
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

| name    | type | description    |
| ------- | ---- | -------------- |
| **in**  | json | extended_asset |
| **out** | json | extended_asset |

#### Example

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

| name                          | type    | description  |
| ----------------------------- | ------- | ------------ |
| **contract**                  | string  | account_name |
| **max_supply**                | string  |              |
| **cw**                        | float64 |              |
| **max_exchange**              | string  |              |
| **supply**                    | string  |              |
| **reserve_supply**            | string  |              |
| **connector_balance**         | string  |              |
| **reserve_connector_balance** | string  |              |

#### Example

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

