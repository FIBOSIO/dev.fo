---
title: eosioContract
type: contract
order: 100
---

## newaccount

| name        | type   | description  |
| ----------- | ------ | ------------ |
| **creator** | string | account_name |
| **name**    | string | account_name |
| **owner**   | json   | authority    |
| **active**  | json   | authority    |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.newaccount({
      creator: "fibosmaster1",
      name: "yunyu1212122",
      owner: {"threshold":1,"keys":[{"key":"FO8FjsDZ5Po7n7LV8xRXYBurxbiRCiPdSUrcfYvtj4cDwNrzpNVD","weight":1}],"accounts":[],"waits":[]},
      active: {"threshold":1,"keys":[{"key":"FO8FjsDZ5Po7n7LV8xRXYBurxbiRCiPdSUrcfYvtj4cDwNrzpNVD","weight":1}],"accounts":[],"waits":[]}
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## setcode

| name          | type   | description  |
| ------------- | ------ | ------------ |
| **account**   | string | account_name |
| **vmtype**    | uint8  |              |
| **vmversion** | uint8  |              |
| **code**      | string |              |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.setcode({
      account: "dexterdexter",
      vmtype: 0,
      vmversion: 0,
      code: "bytes"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## setabi

| name        | type   | description  |
| ----------- | ------ | ------------ |
| **account** | string | account_name |
| **abi**     | json   |              |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.setabi({
      account: 'account_name',
      abi: 'bytes'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## updateauth

| name           | type   | description     |
| -------------- | ------ | --------------- |
| **account**    | string | account_name    |
| **permission** | string | permission_name |
| **parent**     | string | permission_name |
| **auth**       | json   | authority       |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.updateauth({
      account: "silver123451",
      permission: "owner",
      parent: "",
      auth: {"threshold":1,"keys":[{"key":"FO7dmfQvyYT5JWhEVePELkFZYo4A1GqRTwHsMJEaN4HxSbcTjjrn","weight":1}],"accounts":[],"waits":[]}
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## deleteauth

| name           | type   | description     |
| -------------- | ------ | --------------- |
| **account**    | string | account_name    |
| **permission** | string | permission_name |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.deleteauth({
      account: 'account_name',
      permission: 'permission_name'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## linkauth

| name            | type   | description     |
| --------------- | ------ | --------------- |
| **account**     | string | account_name    |
| **code**        | string | account_name    |
| **type**        | string | action_name     |
| **requirement** | string | permission_name |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.linkauth({
      account: "fiboshanghai",
      code: "eosio",
      type: "claimrewards",
      requirement: "claimer"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## unlinkauth

| name        | type   | description  |
| ----------- | ------ | ------------ |
| **account** | string | account_name |
| **code**    | string | account_name |
| **type**    | string | action_name  |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.unlinkauth({
      account: 'account_name',
      code: 'account_name',
      type: 'action_name'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## canceldelay

| name               | type | description         |
| ------------------ | ---- | ------------------- |
| **canceling_auth** |      | permission_level    |
| **trx_id**         |      | transaction_id_type |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.canceldelay({
      canceling_auth: 'permission_level',
      trx_id: 'transaction_id_type'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## onerror

| name          | type    | description |
| ------------- | ------- | ----------- |
| **sender_id** | uint128 |             |
| **sent_trx**  | string  |             |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.onerror({
      sender_id: "0x815b4e505a7605000000000000000000",
      sent_trx: "7e77a45b10c1b391818f0000010001e0afca9946ffcd450000004a1ac6cd4d01e0afca9946ffcd4500000000a8ed323208660200000000000000"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## buyrambytes

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **payer**    | string | account_name |
| **receiver** | string | account_name |
| **bytes**    | uint32 |              |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.buyrambytes({
      payer: "fibosmaster1",
      receiver: "yunyu1212122",
      bytes: 4096
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## buyram

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **payer**    | string | account_name |
| **receiver** | string | account_name |
| **quant**    | string | asset        |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.buyram({
      payer: "silver123451",
      receiver: "silver123451",
      quant: "0.1273 FO"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## sellram

| name        | type   | description  |
| ----------- | ------ | ------------ |
| **account** | string | account_name |
| **bytes**   | uint64 |              |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.sellram({
      account: "silver123451",
      bytes: 789438000
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## delegatebw

| name                   | type   | description  |
| ---------------------- | ------ | ------------ |
| **from**               | string | account_name |
| **receiver**           | string | account_name |
| **stake_net_quantity** | string | asset        |
| **stake_cpu_quantity** | string | asset        |
| **transfer**           | bool   |              |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.delegatebw({
      from: "slowmistioio",
      receiver: "slowmistioio",
      stake_net_quantity: "3193.0000 FO",
      stake_cpu_quantity: "30000.0000 FO",
      transfer: 0
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## undelegatebw

| name                     | type   | description  |
| ------------------------ | ------ | ------------ |
| **from**                 | string | account_name |
| **receiver**             | string | account_name |
| **unstake_net_quantity** | string | asset        |
| **unstake_cpu_quantity** | string | asset        |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.undelegatebw({
      from: "\"silver123451\"",
      receiver: "\"silver123451\"",
      unstake_net_quantity: "\"0.0000 FO\"",
      unstake_cpu_quantity: "\"104000.0000 FO\""
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## refund

| name      | type   | description  |
| --------- | ------ | ------------ |
| **owner** | string | account_name |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.refund({
      owner: "imeos2imeos2"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## regproducer

| name             | type   | description  |
| ---------------- | ------ | ------------ |
| **producer**     | string | account_name |
| **producer_key** | string | public_key   |
| **url**          | string |              |
| **location**     | uint16 |              |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.regproducer({
      producer: "aaaooooooooo",
      producer_key: "FO75Bt2DwqUz78AZ5AACMJzXtRKBbWctpEAVVAv6hYLqfH7JSZNW",
      url: "http://www.fiboso.com",
      location: 1
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## setram

| name             | type   | description |
| ---------------- | ------ | ----------- |
| **max_ram_size** | uint64 |             |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.setram({
      max_ram_size: 'uint64'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## setramrate

| name                | type   | description |
| ------------------- | ------ | ----------- |
| **bytes_per_block** | uint16 |             |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.setramrate({
      bytes_per_block: 1024
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## bidname

| name        | type   | description  |
| ----------- | ------ | ------------ |
| **bidder**  | string | account_name |
| **newname** | string | account_name |
| **bid**     | string | asset        |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.bidname({
      bidder: "fibscandotio",
      newname: "com",
      bid: "1.0000 FO"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## bidrefund

| name        | type   | description  |
| ----------- | ------ | ------------ |
| **bidder**  | string | account_name |
| **newname** | string | account_name |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.bidrefund({
      bidder: 'account_name',
      newname: 'account_name'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## unregprod

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **producer** | string | account_name |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.unregprod({
      producer: "bitzebitze11"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## regproxy

| name        | type   | description  |
| ----------- | ------ | ------------ |
| **proxy**   | string | account_name |
| **isproxy** | bool   |              |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.regproxy({
      proxy: "fibosking322",
      isproxy: 1
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## voteproducer

| name          | type             | description  |
| ------------- | ---------------- | ------------ |
| **voter**     | string           | account_name |
| **proxy**     | string           | account_name |
| **producers** | array of strings | account_name |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.voteproducer({
      voter: "slowmistioio",
      proxy: "",
      producers: ["slowmistioio"]
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## claimrewards

| name      | type   | description  |
| --------- | ------ | ------------ |
| **owner** | string | account_name |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.claimrewards({
      owner: "linyuezhan12"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## setpriv

| name        | type   | description  |
| ----------- | ------ | ------------ |
| **account** | string | account_name |
| **is_priv** | int8   |              |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.setpriv({
      account: "eosio.msig",
      is_priv: 1
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## rmvproducer

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **producer** | string | account_name |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.rmvproducer({
      producer: 'account_name'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## setalimits

| name           | type   | description  |
| -------------- | ------ | ------------ |
| **account**    | string | account_name |
| **ram_bytes**  | int64  |              |
| **net_weight** | int64  |              |
| **cpu_weight** | int64  |              |

#### Eample

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.setalimits({
      account: 'account_name',
      ram_bytes: 'int64',
      net_weight: 'int64',
      cpu_weight: 'int64'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## setglimits

| name                    | type  | description |
| ----------------------- | ----- | ----------- |
| **cpu_usec_per_period** | int64 |             |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.setglimits({
      cpu_usec_per_period: 'int64'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## setprods

| name         | type             | description  |
| ------------ | ---------------- | ------------ |
| **schedule** | array of strings | producer_key |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.setprods({
      schedule: 'producer_key[]'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## reqauth

| name     | type   | description  |
| -------- | ------ | ------------ |
| **from** | string | account_name |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.reqauth({
      from: 'account_name'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## setparams

| name       | type | description |
| ---------- | ---- | :---------: |
| **params** |      |             |

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
  const eosioContract = await client.contract('eosio');
  try {
    const ret = await eosioContract.setparams({
      params: 'blockchain_parameters'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```

