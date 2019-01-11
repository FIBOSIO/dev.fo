---
title: Token
type: tutorials
language: en
order: 252
---

## Issue Token

The `excreate` api of token contract is used while issuing token. The method and parameters explanations is shown below:

```javascript
void token::excreate(
  account_name issuer, // token issue account
  asset maximum_supply, // Maximum releasable token amount
  double connector_weight, // connector weight
  asset maximum_exchange, // Maximum convertiable(circulation) token amount
  asset reserve_supply, // Not in circulation token amount
  asset reserve_connector_balance, // Not in circulation reserve balance
  time_point_sec expiration, // lock period preset by the project party
  double buy_fee, // Project team preset token exchange fee (in going)
  double sell_fee // Project team preset token cash out fee (out going)  
  account_name connector_balance_issuer //Prepare blondes
)
```

There are two types of token you can issue on FIBOS，one is the traditional token, the other one is smart token. The difference between two types of token is that smart token can be exchanged via bancor protocol. If you are not familliar with bancor protocol. You can refer to [bancor protocol whitepaper](https://www.bancor.network/whitepaper).

### Issue normal token

```javascript
//Initialize FIBOS client
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.excreateSync(name, '90000000000.0000 DDD', 0, '10000000000.0000 DDD', '3000000000.0000 DDD', '90000.0000 FO', '2018-10-29T18:54:00', 0, 0, 'eosio', {
  authorization: name
}); //Custom fee, Greater than 0 is less than or equal to 1, the reserve here is FO, so reserve publisher to fill in eosio
console.log(r)
```

### Issue smart token

```javascript
//Initialize FIBOS client
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.excreateSync(name, '100000000000.0000 AAA',  0.15,'10000000000.0000 AAA', '3000000000.0000 AAA', '90000.0000 FO', '2018-10-29T18:54:00', 0, 0, 'eosio',{
    authorization: name
});  //Custom fee, Greater than 0 is less than or equal to 1, the reserve here is FO, so reserve publisher to fill in eosio
console.log(r);
```

Note：when the value of a token connector weight（CW） is 0，it is a normal token. For smart token, it has to have the corresponding cw（between 0-1）and max_exchange. and calculate the reserve_supply and reserve_connector_balance according to the Bancor protocol.

#### Check issued token

```javascript
//Initialize FIBOS client
...
let r = fibos.getTableRowsSync(true, 'eosio.token', 'fibostest123', 'stats');//the 1st parameter is whther shows in clear text，2nd is the contract name，3rd is FIBOS account name, 4th is the table name.
console.log(r);
```



## additional normal token issuing

> **Tips** : Only normal token supports additional issuing. Smart tokens do not.

```javascript
//Initialize FIBOS client
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exissueSync(name, '1000000.0000 ABC@fibostest123', 'issue to fibostest123', {
  authorization: name
});
console.log(r);
```



## Lock & Unlock Position

### Open Position

The creator of a token needs to call the opening operation before opening smart token exchange. The specific API and operation are as follows:

```javascript
//Initialize FIBOS client
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.setpositionSync('0.0000 AAA@fibostest123', 1, 'set postion state to true', {
    authorization: name
}); // has to be greater than or equal to the current time 1 represents to openning，0 represents to closed.
console.log(r);
```

Note：the open/close state here only effects the transferring in of smart token. Transferring out is not effected. If the smart token is now in a closed lock state, you can still exchange the smart token to reserve or the other opening state smart token, but the reserve can not exchange to this smart token. 

### Lock Position

While the project party issues smart tokens, the value of parameter reserve_supply entered and the locked position amount will change by the destroy and unlock operations. The project party can transfer a part of tokens to user A by lock transfer method exlocktrans）. User A can also transfer the received locking token to user B or project party. While the project is well operated, project party or user can get pay back via unlocking the token.

`exlocktrans`  method and parameters:

```javascript
void token::exlocktrans(
    account_name from, //Token transferror
    account_name to, //Token transferree
    extended_asset quantity, //token amount
    time_point_sec expiration, //待转出锁仓时间
    time_point_sec expiration_to, //待转入锁仓时间
    string memo //memo
)
```

Note：The parameter `expiration_to` in api is for lock period. The project party can set this parameter while transferring the locking token to users. The timestamp format is accurate to seconds. So that users can not unlock before the lock period ends. `expiration` parameter represents to check the user locked token via the lock period. 

#### Example

```javascript
//Initialize fibos client
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exlocktransSync('nmslwsndhjyz', 'fibostest123', `10000.0000 ADC@nmslwsndhjyz`, '2018-10-29T18:54:00', '2018-10-29T18:54:00', `lock transfer to fibostest123`, {
    authorization: 'nmslwsndhjyz'
}); //expiration_to has to be greater than or equal to the expiration
console.notice(r)
```

In the codes above. User `nmslwsndhjyz` transferred 10000.0000 locking ADC tokens to `fibostest123`. 

### Unlock

Project parties and users can unlock the token and convert to circulation token via unlock operation. 

`exunlock` method and parameters: 

```javascript
void token::exunlock(
    account_name owner, //token owner
    extended_asset quantity, //unlock amount
    time_point_sec expiration, //lock position time
    string memo //memo
)
```

Note：The unlock operation can only be proceed when current time is larger than locked period. Here is what you need to note: the value of the `expiration` parameter is not current time, but the lock period set by lock position transfer.

#### Example

```javascript
//Initialize FIBOS client
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exunlockSync('fibostest123', '100.0000 ADC@nmslwsndhjyz', 1537960501, 'unlock 100.0000 ADC', {
    authorization: 'hujzwsndnmsl'
})
console.notice(r);
```



## Dividend

In the token economic models of FIBOS, it provides a method of paying dividends to token holder of community for the token issuer. Issuer can paying dividends via enter some amount of reserves. The token holders in community can enjoy the dividends while they are exchanging their token. 

`exshare` method and parameters:

```javascript
//Initialize FIBOS client
...

let ctx = fibos.contractSync('eosio.token');
let r = ctx.exshareSync('10000.0000 FO@eosio', '0.0000 AAA@fibostest321', 'share 10000.0000 FO to token holders',{
    authorization: 'fibostest123'
}); // the 1st parameter is the amount of margin，the 2rd parameter is the smart token that takes apart in dividends. the 3rd parameter is memo.
```



## Destroy token

> **Tips** : The token can only be destroyed if the circulation amount is 0, that means the token issuer needs to take back all the circulation amount of tokens in the market, after that the token can be destroyed.

If the token is no longer needed, call `exdestroySync` method to destroy it:

```javascript
//Initialize FIBOS client
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exdestroySync('0.0000 AAA@fibostest123', {
    authorization: 'fibostest123'
});
```
