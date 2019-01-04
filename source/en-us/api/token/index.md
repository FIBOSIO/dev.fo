---
title: 
type: token
language: en
order: 1
---

# Token Contract

## transfer

transfer —— It can only be called if the publisher is using eosio's token (FIBOS main network currently only supports EOS and FO)

#### Parameter

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **from**     | string | transfer-out |
| **to**       | string | transfer-in  |
| **quantity** | string | Token amount |
| **memo**     | string | memorandum   |

####  Example

under fibos.js:

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.transferSync('fibforjeremy', 'fiboscouncil', '20.3375 EOS', 'eosforjeremy', {
  authorization: 'The account corresponding to the private key'
});
console.log(r);

```

In the browser environment:

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.transfer({
      from: 'fibforjeremy',
      to: 'fiboscouncil',
      quantity: '20.3375 EOS',
      memo: 'eosforjeremy'
    },{
        authorization: 'The account corresponding to the private key'
    })
})
```



## extransfer

transfer

#### Parameter

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **from**     | string | transfer-out |
| **to**       | string | transfer-in  |
| **quantity** | string | Token amount |
| **memo**     | string | memorandum   |

#### Example

under fibos.js:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.extransferSync('dicefobetone', 'zhangjingrui', '10.0000 FO@eosio', 'trasnfer to zhangjingrui', {
  authorization: 'The account corresponding to the private key'
});
console.log(r);
```

In the browser environment:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.extransfer({
      from: 'dicefobetone',
      to: 'zhangjingrui',
      quantity: '10.0000 FO@eosio',
      memo: 'trasnfer to zhangjingrui'
    },{
        authorization: 'The account corresponding to the private key'
    })
})
```



## exissue

additional token issuing —— commom token only，community token is not supported

#### Parameter

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **to**       | string | transfer-in  |
| **quantity** | string | Token amount |
| **memo**     | string | memorandum   |

#### Example

under fibos.js：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.exissueSync('dogfallchina', '10.0000 TAO@dogfallchina', 'issue to dogfallchina', {
  authorization: 'The account corresponding to the private key'
});
console.log(r);
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exissue({
      to: 'dogfallchina',
      quantity: '10.0000 TAO@dogfallchina',
      memo: 'issue to fibostest123'
    },{
        authorization: 'The account corresponding to the private key'
    })
})
```



## exretire

Destroy the circulation token held by the account

#### Parameter

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **from**     | string | transfer-out |
| **quantity** | string | Token amount |
| **memo**     | string | memorandum   |

#### Example

under fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.exretireSync('createtest11', '10.0000 FO@eosio', 'retire tokens', {
  authorization: 'The account corresponding to the private key'
});
console.log(r);
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

client.contract('eosio.token').then((contract)=>{
    contract.exretire({
      from: 'createtest11',
      quantity: '10.0000 FO@eosio',
      memo: 'retire tokens'
    },{
        authorization: 'The account corresponding to the private key'
    })
})
```



## exshare

Share out profits to token holder in the community

#### Parameter

| name         | type   | description          |
| ------------ | ------ | -------------------- |
| **quantity** | string | quantity of margin   |
| **tosym**    | string | Dividend smart token |
| **memo**     | string | memorandum           |

#### Example

under fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos.contractSync('eosio.token');
let r = ctx.exshareSync('10000.0000 FO@eosio', '0.0000 AAA@fibostest321', 'share 10000.0000 FO to token holders',{
    authorization: 'The account corresponding to the private key'
}); 
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exshare({
      quantity: '10000.0000 FO@eosio',
      tosym: '0.0000 AAA@fibostest321' 
      memo: 'share 10000.0000 FO to token holders'
    },{
        authorization: 'The account corresponding to the private key'
    })
});
```



## excreate

issue token

#### Parameter

| name                          | type      | description                                    |
| ----------------------------- | --------- | ---------------------------------------------- |
| **issuer**                    | string    | token issuing account                          |
| **maximum_supply**            | string    | The maximum amount of token that can be issued |
| **connector_weight**          | float64   | Connector weight                               |
| **maximum_exchange**          | string    | Maximum convertible(in circulation) token      |
| **reserve_supply**            | string    | lock-up token amount                           |
| **reserve_connector_balance** | string    | Amount of margin for lock-up token             |
| **expiration**                | date-time | Preset project lock-up period                  |
| **buy_fee**                   | double    | Preset token exchange fee                      |
| **sell_fee**                  | double    | Preset token cashing fee                       |

#### Example

under fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.excreateSync('dogfallchina', '90000000000.0000 DDD', 0, '10000000000.0000 DDD', '3000000000.0000 DDD', '90000.0000 FO', '2018-10-29T18:54:00', 0,0,{ //手续费自定义,大于0小于等于1 
  authorization: 'The account corresponding to the private key'  //授权
}); //expiration 需大于等于当前时间
console.log(r)
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
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
      sell_fee: 0
    },{
        authorization: 'The account corresponding to the private key'
    })
})
```



## exclose

Delete the token entry in the account

#### Parameter

| name       | type   | description       |
| ---------- | ------ | ----------------- |
| **owner**  | string | token owner       |
| **symbol** | string | token target type |

#### Example

under fibos.js：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});


let ctx = client.contractSync('eosio.token');

let r = ctx.excloseSync('dreamheartlx', '4,ZC@lixunlixunli', { //4 represents the accuracy of token，ZC represents the name of token，lixunlixunli represents the issuer of token
  authorization: 'The account corresponding to the private key'
}); 
console.log(r)
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exclose({
      owner: 'dreamheartlx',
      symbol: '4,ZC@lixunlixunli'
    },{
        authorization: 'The account corresponding to the private key'
    })
});
```



## exdestroy

Delete token permanently

#### Parameter

| name       | type   | description       |
| ---------- | ------ | ----------------- |
| **symbol** | string | token target type |

#### Example

under fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.exdestroySync('8,QE@dreamheartlx', {
  authorization: 'The account corresponding to the private key'
}); 
console.log(r)
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exdestroy({
      symbol: '8,QE@dreamheartlx'
    },{
        authorization: 'The account corresponding to the private key'
    })
});
```

Note: token can only be destroyed if the circulation is 0, that is, token issuer needs to withdraw all the token in circulation in the market before destroying it.

## exchange

token exchange

#### Parameter

| name         | type   | description                    |
| ------------ | ------ | ------------------------------ |
| **owner**    | string | exchange account               |
| **quantity** | string | amount of exchanged token      |
| **tosym**    | string | target type of exchanged token |
| **memo**     | string | Notes on exchange              |

#### Example

under fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.exchangeSync('dicefobetone', '0.0130 EOS@eosio', '0.0000 FO@eosio', 'exchange FO to EOS', {
    authorization: 'The account corresponding to the private key'
});
console.log(r)
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exchange({
      owner: 'dicefobetone',
      quantity: '0.0130 EOS@eosio',
      tosym: '0.0000 FO@eosio',
      memo: 'exchange FO to EOS'
    },{
        authorization: 'The account corresponding to the private key'
    })
});
```



## ctxrecharge

Contract sub-wallet——recharge

#### Parameter

| name         | type   | description                  |
| ------------ | ------ | ---------------------------- |
| **owner**    | string | account owner                |
| **quantity** | string | the total amount of recharge |
| **memo**     | string | memorandum                   |

#### Example

under fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.ctxrechargeSync('dreamheartlx', '100.0000 QQQ@dreamheartlx','ctxrecharge', {
    authorization: 'The account corresponding to the private key'
});
console.log(r)
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.ctxrecharge({
      owner: 'dreamheartlx',
      quantity: '100.0000 QQQ@dreamheartlx',
      memo: 'ctxrecharge'
    },{
        authorization: 'The account corresponding to the private key'
    })
});
```



## ctxextract

Contract sub-wallet——withdraw

#### Parameter

| name         | type   | description                  |
| ------------ | ------ | ---------------------------- |
| **owner**    | string | account owner                |
| **quantity** | string | the total amount of withdraw |
| **memo**     | string | memorandum                   |

#### Example

under fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.ctxextractSync('lixunlixunli', '0.000100 LIU@lixunlixunli','ctxextract', {
    authorization: 'The account corresponding to the private key'
});
console.log(r)
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.ctxextract({
      owner: 'lixunlixunli',
      quantity: '0.000100 LIU@lixunlixunli',
      memo: 'ctxextract'
    },{
        authorization: 'The account corresponding to the private key'
    })
});
```



## ctxtransfer

Contract sub-wallet — transfer

#### Parameter

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **from**     | string | transfer-out |
| **to**       | string | transfer-in  |
| **quantity** | string | Token amount |
| **memo**     | string | memorandum   |

#### Example

under fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.ctxtransferSync('lixunlixunli','dreamheartlx','1.0000 ZX@lixunlixunli','ctxtransfer', {
    authorization: 'The account corresponding to the private key'
});
console.log(r)
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.ctxtransfer({
      from: 'lixunlixunli',
      to: 'dreamheartlx',
      quantity: '1.0000 ZX@lixunlixunli',
      memo: 'ctxtransfer'
    },{
        authorization: 'The account corresponding to the private key'
    })
});
```



## exunlock

unlock

#### Parameter

| name           | type      | description                     |
| -------------- | --------- | ------------------------------- |
| **owner**      | string    | token owner                     |
| **quantity**   | string    | total number of tokens unlocked |
| **expiration** | date-time | Lock up period of token         |
| **memo**       | string    | memorandum                      |

#### Example

under fibos.js：

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.exunlockSync('fibostest123', '100.0000 ADC@nmslwsndhjyz', '2018-11-25T01:00:00', 'unlock 100.0000 ADC', {
    authorization: 'The account corresponding to the private key'
})
console.log(r);
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exunlock({
      owner: 'fibostest123',
      quantity: '100.0000 ADC@nmslwsndhjyz',
      expiration: '2018-11-25T01:00:00',
      memo: 'unlock 100.0000 ADC'
    },{
        authorization: 'The account corresponding to the private key'
    })
});
```



## exlocktrans

Lock up transfer

#### Parameter

| name              | type      | description                   |
| ----------------- | --------- | ----------------------------- |
| **from**          | string    | locked up for transfer-out    |
| **to**            | string    | locked up for transfer-in     |
| **quantity**      | string    | Token amount                  |
| **expiration**    | date-time | Lock up time for transfer-out |
| **expiration_to** | date-time | Lock up time for transfer-in  |
| **memo**          | string    | memorandum                    |

#### Example

under fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.exlocktransSync('nmslwsndhjyz', 'fibostest123', '10000.0000 BBB@5hzuyqumr3l5', '2018-10-29T18:54:00', '2018-10-29T18:54:00', 'exlocktrans 10000 BBBC@uepgdzfhucin', {
    authorization: 'The account corresponding to the private key'
}); //expiration_to must be greater than or equal to expiration
console.log(r)
```

In the browser environment：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main net chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exlocktrans``
      from: 'nmslwsndhjyz',
      to: 'fibostest123',
      quantity: '10000.0000 BBB@5hzuyqumr3l5',
      expiration: '2018-10-29T18:54:00',
      expiration_to: '2018-10-29T18:54:00',
      memo: 'exlocktrans 10000 BBB@uepgdzfhucin'
    },{
        authorization: 'The account corresponding to the private key'
    })
});
```



## receipt

Credential

#### Parameter

| name    | type   | description              |
| ------- | ------ | ------------------------ |
| **in**  | string | transfer-in credentials  |
| **out** | string | transfer-out credentials |

#### Example

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

snapshot

#### Parameter

| name                          | type    | description                        |
| ----------------------------- | ------- | ---------------------------------- |
| **contract**                  | string  | token owner                        |
| **max_supply**                | string  | amount of maximum issued token     |
| **cw**                        | float64 | The cw values                      |
| **max_exchange**              | string  | amount of maximum exchanged token  |
| **supply**                    | string  | issue token amount                 |
| **reserve_supply**            | string  | locked up token amount             |
| **connector_balance**         | string  | margin amount                      |
| **reserve_connector_balance** | string  | Amount of outstanding margin token |

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

