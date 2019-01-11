---
title: Resources
type: tutorials
language: en
order: 240
---

There are 2 types of FIBOS Resources: one is mortgage type resources, includes CPU and NET; the other one is a consumption resource, called RAM or storage.

Enough RAM,CPU and NET are required if a user wants to release a contract.

## RAM and Resources

### RAM

- RAM is a necessary resource to storage data on blockchain. It requires users to buy from the system, the more data stored, the more is RAM needed.
- The price of RAM is decided by market, it will adjust automatically according to the market. When a program is done using RAM, RAM can be released and sold at current market price.
- No matter buying RAM or selling RAM, the process is only between user and the system account instead of market trading. Only the price will be set by bancor algorithm.

### Network Bandwidth

- User can get larger bandwidth by mortgaging more FO. Also the mortgage can be reversed to unload network bandwidth and get FO back.
- Network bandwidth can be understood as mobile phone flow. It can be obtained flexibly according to requirement. 

### CPU Bandwidth

- CPU bandwidth is used to measure the computing time (milliseconds)  while executing the contract in the last 3 days
- CPU bandwidth is similar to network bandwidth, it is a temporary consumption. When the usage drops. the consumption drops too, the minimum is 0.
- You can get larger CPU by mortgaging FO or cancel the mortgaging to decrease CPU and get your FO back.



## How to buy or mortgage resources

### Buy RAM

1. RAM consumption is required to store account information on chain, thus the creator needs to buy RAM for the user to save new account information.

   This is done by by calling the `buyrambytes` method. The parameters and explanation:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos text net chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.buyrambytesSync({
      payer: "fibosmaster1",  //creator account name
      receiver: "yunyu1212122", //receiver account name
      bytes: 4096  //size of RAM to buy
},{
    authorization: 'account correspoding to private key' 
});
console.log(r);
```

2. Buy storage resources. The difference is to buy specific amount of tokens or specific size of content.

By calling `buyram` method. The parameters and explanation:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos text net chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.buyramSync({
      payer: "silver123451", //payer account
      receiver: "silver123451", //receiver account
      quant: "0.1273 FO" //token amount to buy storage resources
},{
    authorization: 'account correspoding to private key' 
});
console.log(r);
```



### Mortgage Resources

Creator mortgages FO for receiver to get CPU and NET in order to let new account be able to transfer. 

By calling `delegatebw` method,  the parameters and explain are as below:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos text net chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.delegatebwSync({
      from: "slowmistioio",  //mortgager account
      receiver: "slowmistioio",  //receiver account
      stake_net_quantity: "3193.0000 FO",  //mortgage FO to get NET
      stake_cpu_quantity: "30000.0000 FO",  //  mortgage FO to get CPU
      transfer: 0  // whether transfer the token to receiver while mortgaing resources
},{
    authorization: 'account correspoding to private key' 
});
console.log(r);
```



### Cancel Mortgage

Used to cancel mortgaging, release resources and get token back.

By calling `updelegatebw` method, the parameters and explain are as below:

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos text net chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.undelegatebwSync({
      from: 'hoffercq1211',  //Remove the mortgage with which account
      receiver: 'hoffercq1211',  //Lift the role in which account of the mortgage
      unstake_net_quantity: '649540.0000 FO', //Lift the token amount used to obtain bandwidth resources
      unstake_cpu_quantity: '649540.0000 FO' //Lift the token amount used to gain access to computing resources
},{
    authorization: 'account correspoding to private key' 
});
console.log(r);
```



### Sell Resources

By calling `sellram` method,  the parameters and explaination are as below:

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos text net chainId
  chainId: '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a',
  keyProvider: 'your private key',
  httpEndpoint: "http://testnet.fibos.fo",
});

let ctx = fibos_client.contractSync('eosio');

var r = ctx.sellramSync({
      account: "silver123451", //seller account
      bytes: 789438000 //size of storage resource to be sold
},{
    authorization: 'account correspoding to private key' 
});
console.log(r);
```
