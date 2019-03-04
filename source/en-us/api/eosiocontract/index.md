---
title: 
type: contract
language: en
order: 1
---
# System Contract

## newaccount

Create Contract Account

#### Parameters

| name        | type   | description                 |
| ----------- | ------ | --------------------------- |
| **creator** | string | creator account              |
| **name**    | string | The name of the account created |
| **owner**   | string | The public key of the owner permission of the account created |
| **active**  | string | Is the public key of the creator active permission    |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.newaccountSync({
    creator:'eosio',
    name:'hellocode2',
    owner:'your public key',
    active:'your public key'
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.newaccount({
        creator:'eosio',
        name:'hellocode2',
        owner:'your public key',
        active:'your public key'
    },{
        authorization: 'the account corresponding to private key'
    })
});
```



## setcode

deploy JS contract

#### Parameters

| name          | type   | description  |
| ------------- | ------ | ------------ |
| **account**   | string | contract account |
| **vmtype**    | uint8  | Contract engine type |
| **vmversion** | uint8  | Contract engine version |
| **code**      | string | contract code     |

#### Example

fibos.js Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});
let ctx = fibos_client.contractSync('eosio');

let r = ctx.setcodeSync({
    account: 'dexterdexter',
    vmtype: 0,
    vmversion: 0,
    code: 'bytes',
},{
    authorization: 'the account corresponding to private key'
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.setcode({
        account:'dexterdexter',
        vmtype: 0,
        vmversion: 0,
        code: 'bytes'
    },{
        authorization: 'the account corresponding to private key'
    })
});
```



## setabi

deploy abi file

#### Parameters

| name        | type   | description  |
| ----------- | ------ | ------------ |
| **account** | string | Contract account |
| **abi**     | json   | abi file code |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

let r = ctx.setabiSync({
    account: 'iforedpacket',
    abi: {"version":"eosio::abi/1.0","types":[],"structs":[],"actions":[],"tables":[],"ricardian_clauses":[],"error_messages":[],"abi_extensions":[],"variants":[]}
},{
    authorization: 'the account corresponding to private key'
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.setabi({
        account:'iforedpacket',
        abi: {"version":"eosio::abi/1.0","types":[],"structs":[],"actions":[],"tables":[],"ricardian_clauses":[],"error_messages":[],"abi_extensions":[],"variants":[]}
    },{
        authorization: 'the account corresponding to private key'
    })
});
```



## updateauth

add or edit user permission

#### Parameters

| name           | type   | description                    |
| -------------- | ------ | ------------------------------ |
| **account**    | string | account name                       |
| **permission** | string | An existing permission or a new permission name |
| **parent**     | string | Creates the parent permission of theis permission |
| **auth**       | json   | The composition of this permission |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.updateauthSync({
  account: 'silver123451',
  permission: 'owner',
  parent: '',
  auth: {
    threshold: 1,
    keys: [{
      key: 'FO7dmfQvyYT5JWhEVePELkFZYo4A1GqRTwHsMJEaN4HxSbcTjjrn',
      weight: 1
    }]
  }
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.updateauth({
        account: 'silver123451',
        permission: 'owner',
        parent: '',
        auth: {
            threshold: 1,
            keys: [{
                key: 'FO7dmfQvyYT5JWhEVePELkFZYo4A1GqRTwHsMJEaN4HxSbcTjjrn',
                weight: 1
            }]
        }
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## deleteauth

delete permission

#### Parameters

| name           | type   | description  |
| -------------- | ------ | ------------ |
| **account**    | string | account name     |
| **permission** | string | permission requires to be deleted |

#### Example

fibos.js Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.deleteauthSync({
    account: 'account_name',
    permission: 'permission_name'
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.deleteauth({
        account: 'account_name',
        permission: 'permission_name'
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## linkauth

Specify action for permissions

#### Parameters

| name            | type   | description |
| --------------- | ------ | ----------- |
| **account**     | string | account name    |
| **code**        | string | contract name   |
| **type**        | string | action name     |
| **requirement** | string | permission name    |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.linkauthSync({
   account: "fiboshanghai",
   code: "eosio",
   type: "claimrewards",
   requirement: "claimer"
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.linkauth({
        account: "fiboshanghai",
        code: "eosio",
        type: "claimrewards",
        requirement: "claimer"
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## unlinkauth

actions that permissions can execute

#### Parameters

| name        | type   | description |
| ----------- | ------ | ----------- |
| **account** | string | account name    |
| **code**    | string | contract name    |
| **type**    | string | action name |

#### Example

fibos.js Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.unlinkauthSync({
   account: 'eosio',
   code: 'hello',
   type: 'hi'
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.unlinkauth({
        account: 'eosio',
        code: 'hello',
        type: 'hi'
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## canceldelay

cancel one delay transction

#### Parameters

| name               | type   | description |
| ------------------ | ------ | ----------- |
| **canceling_auth** | String | permission type    |
| **trx_id**         | String | transction hash   |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.canceldelaySync({
    canceling_auth: 'permission_level',
    trx_id: 'transaction_id_type'
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.canceldelay({
        canceling_auth: 'permission_level',
        trx_id: 'transaction_id_type'
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## buyrambytes

payer call this function to storage new account info for receiver.

#### Parameters

| name         | type   | description            |
| ------------ | ------ | ---------------------- |
| **payer**    | string | payer account name   |
| **receiver** | string | receiver account name       |
| **bytes**    | uint32 | size of purchased ram |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.buyrambytesSync({
      payer: "fibosmaster1",
      receiver: "yunyu1212122",
      bytes: 4096
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.buyrambytes({
        payer: "fibosmaster1",
        receiver: "yunyu1212122",
        bytes: 4096
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## buyram

Buy storage resources, difference is whether buy A specific amount of token or size of content.

#### Parameters

| name         | type   | description                |
| ------------ | ------ | -------------------------- |
| **payer**    | string | buy storage account        |
| **receiver** | string | receiving storage account  |
| **quant**    | string | requiring token amount of buying resources |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.buyramSync({
      payer: "silver123451",
      receiver: "silver123451",
      quant: "0.1273 FO"
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.buyram({
        payer: "silver123451",
        receiver: "silver123451",
        quant: "0.1273 FO"
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## sellram

Sell unnecessary resources

#### Parameters

| name        | type   | description            |
| ----------- | ------ | ---------------------- |
| **account** | string | Accept account for selling resource token |
| **bytes**   | uint64 | How much space to sell for storage resources |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.sellramSync({
      account: "silver123451",
      bytes: 789438000
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.sellram({
        account: "silver123451",
        bytes: 789438000
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## delegatebw

Mortgage token to get cpu and bandwidth resources

#### Parameters

| name                   | type   | description                                |
| ---------------------- | ------ | ------------------------------------------ |
| **from**               | string | The account name of the resource mortgagor                         |
| **receiver**           | string | The account name of the resource recipient                         |
| **stake_net_quantity** | string | The mortgagor mortgages FO to obtain NET for the recipient             |
| **stake_cpu_quantity** | string | The mortgagor mortgages FO for the recipient to obtain CPU             |
| **transfer**           | bool   | Represents whether the mortgage resources are transferred to the recipient at the same time |

#### Example

fibos.js Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.delegatebwSync({
      from: "slowmistioio",
      receiver: "slowmistioio",
      stake_net_quantity: "3193.0000 FO",
      stake_cpu_quantity: "30000.0000 FO",
      transfer: 0
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.delegatebw({
        from: "slowmistioio",
        receiver: "slowmistioio",
        stake_net_quantity: "3193.0000 FO",
        stake_cpu_quantity: "30000.0000 FO",
        transfer: 0
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## undelegatebw

Unlock mortgage, release resources, return tokens.

#### Parameters

| name                     | type   | description                    |
| ------------------------ | ------ | ------------------------------ |
| **from**                 | string | Remove the token mortgaged by which account     |
| **receiver**             | string | Remove the token on which the account is used as collateral |
| **unstake_net_quantity** | string | Uncount the number of tokens used to obtain bandwidth resources |
| **unstake_cpu_quantity** | string | Uncount the number of tokens used to get the calculated resource |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.undelegatebwSync({
      from: 'hoffercq1211',
      receiver: 'hoffercq1211',
      unstake_net_quantity: '649540.0000 FO',
      unstake_cpu_quantity: '649540.0000 FO'
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.undelegatebw({
        from: "\"silver123451\"",
        receiver: "\"silver123451\"",
        unstake_net_quantity: "\"0.0000 FO\"",
        unstake_cpu_quantity: "\"104000.0000 FO\""
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## refund

call after undelegatebw fuction mortgage unlocked, in order to refund tokens back to account.

#### Parameters

| name      | type   | description  |
| --------- | ------ | ------------ |
| **owner** | string | return account name |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.refundSync({
    owner: "imeos2imeos2"
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.refund({
        owner: "imeos2imeos2"
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## regproducer

register as a block producer

#### Parameters

| name             | type   | description                  |
| ---------------- | ------ | ---------------------------- |
| **producer**     | string | blcok producer account name  |
| **producer_key** | string | block producer public key    |
| **url**          | string | block producer website       |
| **location**     | uint16 | block producer server location code |

#### Example

fibos.js Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.regproducerSync({
    producer: "aaaooooooooo",
    producer_key: "FO75Bt2DwqUz78AZ5AACMJzXtRKBbWctpEAVVAv6hYLqfH7JSZNW",
    url: "http://www.fiboso.com",
    location: 1
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.regproducer({
        producer: "aaaooooooooo",
        producer_key: "FO75Bt2DwqUz78AZ5AACMJzXtRKBbWctpEAVVAv6hYLqfH7JSZNW",
        url: "http://www.fiboso.com",
        location: 1
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## unregprod

unregister as a block producer.

#### Parameters

| name         | type   | description |
| ------------ | ------ | ----------- |
| **producer** | string | account name    |

#### Example

fibos.js Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.unregprodSync({
    producer: "bitzebitze11"
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.unregprod({
        producer: "bitzebitze11"
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## regproxy

Register as an agent, allow vote proxy from other users.

#### Parameters

| name        | type   | description              |
| ----------- | ------ | ------------------------ |
| **proxy**   | string | registed account name    |
| **isproxy** | bool   | if voter proxy is allowed |

#### Example

fibos.js Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.regproxySync({
    proxy: "fibosking322",
    isproxy: 1
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.regproxy({
        proxy: "fibosking322",
        isproxy: 1
    },{
        authorization: 'the account corresponding to private key'
    })
})
```



## voteproducer

vote for producer

#### Parameters

| name          | type             | description |
| ------------- | ---------------- | ----------- |
| **voter**     | string           | voter      |
| **proxy**     | string           | voter proxy|
| **producers** | array of strings | producers list |

#### Example

fibos.js Runtime：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.voteproducerSync({
    voter: "slowmistioio",
    proxy: "",
    producers: ["slowmistioio"]
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.voteproducer({
        voter: "slowmistioio",
        proxy: "",
        producers: ["slowmistioio"]
    },{
        authorization: 'the account corresponding to private key'
    })
})
```

Note: Node vote list requires developers to sort alphabetically,  up to 30 BP vote maximum is allowed per time. 


## claimrewards

block producer claiming rewoards

#### Parameters

| name      | type   | description    |
| --------- | ------ | -------------- |
| **owner** | string | name of block producer |

#### Example

fibos.js Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.claimrewardsSync({
    owner: "linyuezhan12"
},{
    authorization: 'the account corresponding to private key' 
});
console.log(r);
```

Browser Runtime：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos test network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://api.testnet.fo",
});

fibos_client.contract('eosio').then((contract)=>{
    contract.claimrewards({
        owner: "linyuezhan12"
    },{
        authorization: 'the account corresponding to private key'
    })
})
```
