---
title: 
type: msig
language: en
order: 1
---

# Eosio.msig

- 'msig' is short for 'multiple signature'(multiple signature), As the name suggests, it is to have multiple accounts sign one transaction. It is possible to propose, approve, and publish transactions that have been approved by multiple parties.
- The multi-signature is determined according to the **weight** of the account or the public key's authority. The weight reaches the threshold to be successful.

## propose

Initiate a proposal

Parameter

| name              | type   | description                                      |
| ----------------- | ------ | ------------------------------------------------ |
| **proposer**      | string | Proposer                                         |
| **proposal_name** | string | Proposal name                                    |
| **requested**     | string | Permissions required to pass the proposal        |
| **trx**           | string | The specific transaction content of the proposal |

#### Example

In fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

let ctx = fibos_client.contractSync('eosio.msig');

var r = ctx.proposeSync({
      proposer: 'account_name',
      proposal_name: 'name',
      requested: 'permission_level[]',
      trx: 'transaction'    
}, {
  authorization: 'Account corresponding to the private key'
});
console.log(r);
```

In the browser:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

fibos_client.contract('eosio.msig').then((contract)=>{
    contract.propose({
      proposer: 'account_name',
      proposal_name: 'name',
      requested: 'permission_level[]',
      trx: 'transaction'
    },{
        authorization: 'Account corresponding to the private key'
    })
})
```



## approve

Agree with proposal

#### Parameter

| name              | type   |description                 |
| ----------------- | ------ | -------------------------- |
| **proposer**      | string | Proposer                   |
| **proposal_name** | string | Proposal Name              |
| **level**         | string | Which permission is used to approve this proposal |

#### Example

In fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://testnet.fibos.fo',
});

let ctx = fibos_client.contractSync('eosio.msig');

var r = ctx.approveSync({
      proposer: 'account_name',
      proposal_name: 'name',
      level: 'permission_level'    
}, {
  authorization: 'Account corresponding to the private key'
});
console.log(r);
```

In the browser:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

fibos_client.contract('eosio.msig').then((contract)=>{
    contract.approve({
      proposer: 'account_name',
      proposal_name: 'name',
      level: 'permission_level'
    },{
        authorization: 'Account corresponding to the private key'
    })
})
```



## unapprove

Reject proposal

#### Parameter

| name              | type   | description                      |
| ----------------- | ------ | -------------------------------- |
| **proposer**      | string | Proposer                         |
| **proposal_name** | string | Proposal name                    |
| **level**         | string | Which permission is used to reject this proposal |

#### Example

In fibos：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://testnet.fibos.fo',
});

let ctx = fibos_client.contractSync('eosio.msig');

var r = ctx.unapproveSync({
      proposer: 'account_name',
      proposal_name: 'name',
      level: 'permission_level'    
}, {
  authorization: 'Account corresponding to the private key'
});
console.log(r);
```

In the browser:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

fibos_client.contract('eosio.msig').then((contract)=>{
    contract.unapprove({
      proposer: 'account_name',
      proposal_name: 'name',
      level: 'permission_level'
    },{
        authorization: 'Account corresponding to the private key'
    })
})
```



## cancel

Cancel proposal

#### Parameter

| name              | type   | description   |
| ----------------- | ------ | ------------- |
| **proposer**      | string | Proposer      |
| **proposal_name** | string | Proposal name |
| **canceler**      | string | Canceler      |

#### Example

In fibos.js：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://testnet.fibos.fo',
});

let ctx = fibos_client.contractSync('eosio.msig');

var r = ctx.cancelSync({
      proposer: 'account_name',
      proposal_name: 'name',
      canceler: 'account_name'
}, {
  authorization: 'Account corresponding to the private key'
});
console.log(r);
```

In the browser:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

fibos_client.contract('eosio.msig').then((contract)=>{
    contract.cancel({
      proposer: 'account_name',
      proposal_name: 'name',
      canceler: 'account_name'
    },{
        authorization: 'Account corresponding to the private key'
    })
})
```



## exec

Execute proposal

#### Parameter

| name              | type   | description       |
| ----------------- | ------ | ---------------   |
| **proposer**      | string | Proposer          |
| **proposal_name** | string | Proposal Name     |
| **executer**      | string | Executer          |

#### Example

In fibos.js:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'Your private key',
  httpEndpoint: 'http://testnet.fibos.fo',
});

let ctx = fibos_client.contractSync('eosio.msig');

var r = ctx.execSync({
      proposer: 'account_name',
      proposal_name: 'name',
      executer: 'account_name'
}, {
  authorization: 'Account corresponding to the private key'
});
console.log(r);
```

In browser：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos main network chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'Your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

fibos_client.contract('eosio.msig').then((contract)=>{
    contract.exec({
      proposer: 'account_name',
      proposal_name: 'name',
      executer: 'account_name'
    },{
        authorization: 'Account corresponding to the private key'
    })
})
```

