---
title: Transfer
type: tutorials
language: en
order: 250
---

## In-chain Transfer

the transfer target account must exists in FIBOS. Also the maximum amount to transfer should not be larger than your balance, the precision should equal to the token precision.

`extransfer` method and parameters:

| parameter| note             |
| -------- | ---------------- |
| from     | token transferor |
| to       | token recipient  |
| quantity | token amount     |
| meno     | memo             |

```javascript
//Initialize fibos client
...
let ctx = fibos.contractSync('eosio.token');
var r = ctx.extransferSync(
    'fibostest123',  //token transferee
    'fibostest321',   //token transferor
    '10.0000 ADC@fibostest123',  //token amount
    'trasnfer to fibostest321',  //memo
    {
  authorization: 'fibostest123'
});
console.log(r);
```



## Cross-chain Transfer


>Important note：In order to prevent cross-chain transfer failure:
>1. Please do not transfer directly through exchange accounts (it is recommended to use EOS wallet to transfer). When transferring through exchange accounts, if the memo is wrongly filled in and the transfer is made, the asset will be lost and cannot be recovered!
>2. Please confirm again and again whether the memo is filled in correctly (please fill in the memo with "your successfully registered account name on the main net of FIBOS"). If the memo is filled in incorrectly, the asset may be lost:
>3. If the memo account you filled in does not exist and the asset is lost, the system will check it and transfer the asset back to your payment account.
>4. If the memo you filled in is wrong, but it happens to be someone else's FIBOS account, the assets cannot be transferred back to your account.

### Cross-chain transfer from EOS to FIBOS

Use the account of the EOS main net to initiate transfer to the EOS account (fiboscouncil), and fill in the name of the registered account of the FIBOS main network in the memo to complete a cross-chain transfer.

#### Initiate transfer on EOS main web

EOS main web RPC address(recommended)：http://api-mainnet.starteos.io

```javascript
var FIBOS = require('fibos.js');

var config = {
    chainId: 'aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906',
    priKey: 'your EOS active permission private key',
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
let eosaccount = '' // your EOS account name
let value = '1.0000 EOS'; //amount of transfer to fiboscouncil account
let ctx = eos_client.contractSync('eosio.token');
let memo = 'fibosmainnet'; //Enter registered FIBOS account
let result = ctx.transferSync(eosaccount, 'fiboscouncil', value, memo, {
    authorization: eosaccount
});
console.log(result);
```

**Example:**

A real operation example， after EOS MainNet, EOS RPC Address, EOS private key are configured, an EOS client is initiated, by calling `transferSync` method pass with 4 parameters: 

| parameter      | note                     |
| -------------- | ------------------------ |
| eosaccount     | transferor               |
| fiboscouncil   | transferee               |
| value          | Amount: 1.0000 EOS       |
| memo           | memo                     |

#### Check transfer information on EOS main web

After initializing a cross-chain transfer on FIBOS main web. You need to wait for 300 or so safe block time, about 2 min, the transfer information can then be checked on EOS main net 

Check via FIBOS client，using the FIBOS main net chainID and RPC interface address.

```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
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
var rs = fibos_client.getTableRowsSync(true, 'eosio.token', 'your FIBOS account name', 'accounts');
console.log(rs);
```

**Example:**

Configuration of main FIBOS chainId Http service address, then a FIBOS client is initialized, call ` getTableRowsSync ` method to query asset information of account.

### Cross-chain transfer from FIBOS to EOS

Use the account of the main net of FIBOS to initiate transfer to the EOS account (fiboscouncil), and fill in the name of the registered account of the main network of EOS in the memo to complete a cross-chain transfer.

#### Initiate transfer operation on FIBOS main web

**Calling method:**

```javascript
let ctx = client.contractSync('eosio.token');
let result = ctx.transferSync(eosaccount, 'fiboscouncil', value, memo);
```

**method description:**

Eosio.token contract is invoked using the fibos.js client to initiate a transfer operation

**Parameters**

| parameters     | Note                                 |
| -------------- | ------------------------------------ |
| eosaccount     | transferor                           |
| fiboscouncil   | transferee                           |
| value          | amount:1.0000 EOS                    |
| memo           | Note:EOS account you have registered |


```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
    priKey: 'your FIBOS private key',
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
let fibosaccount = '' // your FIBOS account name
let value = '1.0000 EOS'; //transfer EOS amount
let ctx = fibos_client.contractSync('eosio.token');
let memo = 'eoseoseoseos'; //EOS account you have registered
let result = ctx.transferSync(fibosaccount, 'fiboscouncil', value, memo, {
    authorization: fibosaccount
});
console.log(result);
```

#### Check transfer info on EOS main web

After initializing a cross-chain transfer on FIBOS main web, You need to wait for 300 or so safe block time, about 2 min, then the transfer information can be checked on EOS main net. 

Check via EOS client，EOS main web chainID and RPC interface address is used.

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
var rs = fibos_client.getTableRowsSync(true, 'eosio.token', 'your EOS account name', 'accounts');
console.log(rs);
```


**Example:**

After configuring EOS main web chainId and RPC server address,then an EOS client is initialized. Call `getTableRowsSync` method to check the assets information of the account.
