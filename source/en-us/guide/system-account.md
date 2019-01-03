---
title: Account
type: tutorials
language: en
order: 241
---

> **Tips:** We will close free FIBOS account register channel on Sep 4th. After then, users who want to register FIBOS account can ask the users that already have FIBOS account to help you to register via learning this document.

## What is account

- Account is different from ETH and BTC addresses. It is an identifiable, readable, notable string. For example: your gaming English nickname could be hellofibos.

- The naming of accounts follows the design by EOS. The rule are: composed only of the numbers 1-5 and the letters a-z(lower-case). The length must be 12 characters.

- For now, the account name length must be 12 characters after EOS BIOS is launched. For the engineers there is one thing one should know. The short account name (shorter than 12 characters) is caused by the system contract. If you are interested in this, you can check the informations about EOS' short name bidding.

- FIBOS account can own resources and relational contracts. Owning resources can be understood as the EOS,RAM,CPU,NET in FIBOS are all belong to the account. Relational contracts can be understood as contracts that must belongs to the account. Account can be authorized to do some actions, such as: transferring, contract action.

## Generate public/private key

>**Tips:** The private key generated needs to be saved properly, and make sure it is not leaked to anyone!  Registering a FIBOS account by someone else only requires your public key. Anyone who ask for your private key for the reason of helping you to register a FIBOS account are fraudsters.

**Generate by ecc of fibos.js**

```javascript
var FIBOS = require('fibos.js');
var prikey = FIBOS.modules.ecc.randomKeySync(); //private key
var pubkey = FIBOS.modules.ecc.privateToPublic(prikey); //public key
console.log('public key: %s\nprivate key: %s',pubkey,prikey);
```



## Create Account

### create new account

`newaccount` method and parameters:

```javascript
var FIBOS = require('fibos.js');
var fibos_client = FIBOS({
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'creator_priKey',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
  logger: {
    log: null,
    error: null
  }
});

fibos_client.newaccount({
    creator: "Creator Name", //Creator acount name
    name: "Account Name", //Created account name
    owner: "Owner Key", //Created owner permission public key
    active: "Active Key" //Created active permission public key
});  
```

###  Buy RAM

Saving account information to the chain consumes RAM. The creator needs to buy RAM for the created account informations.

`buyrambytes` method and parameters:


```javascript
var FIBOS = require('fibos.js');
var fibos_client = FIBOS({
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'creator_priKey',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
  logger: {
    log: null,
    error: null
  }
});

fibos_client.buyrambytes({
    payer: 'eosio.token',//Created account name
    receiver: 'Receiver Account',//Created account name
    bytes: 4096 //The amount of memory consumed
});
```

### Mortgage Resources

Creator mortgages FO to get CPU and NET to allow the created account to do transfers.

`delegatebw` method and parameters:


```javascript
var FIBOS = require('fibos.js');
var fibos_client = FIBOS({
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'creator_priKey',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
  logger: {
    log: null,
    error: null
  }
});

fibos_client.delegatebw({
    from: 'from',//Creator account name
    receiver: 'Your_Account',//Created account name
    stake_net_quantity: '0.1000 FO',//Creator mortgage FO to get CPU for created account
    stake_cpu_quantity: '0.1000 FO',//Creator mortgage FO to get NET for created account
    transfer: 1//Represents wether to transfer tokens to receivors while mortgaging resources
});
```

#### Example

```javascript
var FIBOS = require('fibos.js');
var fibos_client = FIBOS({
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: 'creator_priKey',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
  logger: {
    log: null,
    error: null
  }
});
var r = fibos_client.transactionSync(tr => {
  tr.newaccount({
    creator: 'creator_account',
    name: 'your_account',
    owner: 'your_owner_publicKey',
    active: 'your_active_publicKey'
  });
  tr.buyrambytes({
    payer: 'creator_account',
    receiver: 'your_account',
    bytes: 4096
  });
  tr.delegatebw({
    from: 'creator_account',
    receiver: 'your_account',
    stake_net_quantity: '0.1000 FO',
    stake_cpu_quantity: '0.1000 FO',
    transfer: 1
  });
});
console.log(r);
```

Execute the code to help others successfully register an account.

Results (parts) ：

```
'act': {
  'account': 'eosio',
  'name': 'newaccount',
  'authorization': [{
    'actor': 'fibostest123',
    'permission': 'active'
  }],
  'data': {
    'creator': 'fibostest123',
    'name': 'xinchengdai1',
    'owner': {
      'threshold': 1,
      'keys': [{
        'key': 'FO7yLv8FvFhFCjajcqgnJJFHBUnLLS9BYfZLymQXoDu7wL3a67Xr',
        'weight': 1
      }],
      'accounts': [],
      'waits': []
    },
    'active': {
      'threshold': 1,
      'keys': [{
        'key': 'FO7yLv8FvFhFCjajcqgnJJFHBUnLLS9BYfZLymQXoDu7wL3a67Xr',
        'weight': 1
      }],
      'accounts': [],
      'waits': []
    }
},
```

Based on the information printed above，We can see `fibostest123` account created an account named `xinchengdai1` ,next the owner of account `xinchengdai1` can import the private key to FO wallet to use the other functions! click [download FO wallet](http://wallet.fo/) to get FO wallet.