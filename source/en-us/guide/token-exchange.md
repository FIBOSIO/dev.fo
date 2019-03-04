---
title: Token Exchange
type: tutorials
language: en
order: 253
---

> If you are a normal user instead of a developer, you can use the FO Wallet to exchange for FO.[Download FO wallet](http://wallet.fo/). First select the source smart token that you want to exchange, then enter the exchange amount. After that select the target token and click exchange. Wait for just a moment and the exchange will be successful.

## Exchange

The whole exchange process is carried out on the FIBOS main net, so the private key and account information of FIBOS main web is used while executing. 

```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
    priKey: 'your FIBOS main web private key',
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

**Calling Method:**

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let result = ctx.exchangeSync(owner, quantity, tosymbol, memo);
```

**Method Statement:**

Use `exchangeSync()` method to exchange token in FIBOS using Bancor

**Parameter Statement:**

| Parameters | Annotation                              |
| ---------- | --------------------------------------- |
| owner      | Exchanger's account                     |
| quantity   | the amount of token to be exchanged     |
| tosymbol   | target exchanging token type            |
| memo       | exchange memo                           |

If a user `fibostest123` issued a smart token named `VAYNE` ，and user `fibostest321` issued a smart token named `HASAKI`. Then how to exchange some  `HASAKI` if the user  `fibostest123` wants to use `VAYNE` ? The answer is to use the `exchangeSync` API.

```javascript
//initialize the FIBOS client
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

If you want to exchange to `EOS` token in `FIBOS`. You only need to change `0.0000 HASAKI@fibostst321` to `0.0000 EOS@eosio`.



##  EOS token exchange to FO token

### Initiate exchanging EOS to FO

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let owner = 'Your FIBOS account name';
let eos2fo_quantity = '10.0000 EOS@eosio';
let memo = 'exchange EOS to FO';

var result = ctx.exchangeSync(owner, eos2fo_quantity ,'0.0000 FO@eosio', memo, {
    authorization: owner
});
console.log(result);
```

### Check the FO token that already been exchanged

```javascript
var rs = fibos_client.getTableRowsSync(true, 'eosio.token', 'your FIBOS account name', 'accounts');
console.log(rs);
```



## FO token converting to EOS token

### initiate FO exchange to EOS

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let owner = 'Your FIBOS account name';
let fo2eos_quantity = '10.0000 FO@eosio';
let memo = 'exchange FO to EOS';

var result = ctx.exchangeSync(owner, fo2eos_quantity, `0.0000 EOS@eosio`, memo, {
    authorization: owner
});
console.log(result);
```

### Check the EOS token that already been converted

```javascript
var rs = fibos_client.getTableRowsSync(true, 'eosio.token', 'Your FIBOS account name', 'accounts');
console.log(rs);
```



## Wallet One-click exchange

[Download fo wallet](http://wallet.fo/), select the source smart token you want to exchange, then enter the amount, after that select the target token you want to exchange, click exchange, wait just a moment for the exchange to be successful.