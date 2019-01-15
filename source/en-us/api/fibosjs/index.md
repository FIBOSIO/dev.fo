---
title: 
type: fibosjs
language: en
order: 1
---


# FIBOS.JS

FIBOS and EOSIO blockchain common library.

## Basic

Various ways to manipulate user account information in a blockchain

### Get client example

the example of linking to a test network

```js
var FIBOS = require('fibos.js');
var fibos_clinet = FIBOS({
	chainId: "68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a",
	keyProvider: "KeyProvider",
	httpEndpoint: "http://testnet.fibos.fo",
	logger: {
		log: null,
		error: null
	}
});
```

### getInfo

Get block info

```js
fibos_client.getInfo();
```

#### Example

Synchronous:

```js
var getInfo = fibos_client.getInfoSync();
console.log(getInfo);
```

Asynchronous:

```js
fibos_client.getInfo().then(getInfo => {
      console.log(getInfo);
}
```

#### Return

```js
{
  "server_version": "8f0f54cf",
  "chain_id": "68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a",
  "head_block_num": 6586065,
  "last_irreversible_block_num": 6585732,
  "last_irreversible_block_id": "00647d84b68cc555f7a55e6416445b03de866c3db71b4d734a5ff7383adb848c",
  "head_block_id": "00647ed1bb1917864bd530fd805cd6b448ea496b8e5e8b0282fd25b8908271e8",
  "head_block_time": "2018-11-23T07:56:10.000",
  "head_block_producer": "testnetbppa1",
  "virtual_block_cpu_limit": 200000000,
  "virtual_block_net_limit": 1048576000,
  "block_cpu_limit": 199900,
  "block_net_limit": 1048576,
  "server_version_string": "v1.3.1.5-10-gaf50e5e"
}
```

#### Return value parameter

* **server_version:** text server-end version

* **chain_id:**string blockchain id

* **head_block_num: **number current block hight

* **last_irreversible_block_num: **number Irreversible block hight

* **last_irreversible_block_id: **string Irreversible block id
* **head_block_id: **string Current block id

* **head_block_time: **date Current block time

* **head_block_producer: **string Current block producer

* **virtual_block_cpu_limit: **number virtual block cpu limit

* **virtual_block_net_limit: **number Virtual block NET limit

* **block_cpu_limit: **number Block cpu limit

* **block_net_limit: **number Block NET limit

* **server_version_string: **string Server-end version string

### getBlock

Get block info

```j's
fibos_client.getBlock(block_number);
```

#### Parameter

- **block_number:** int  Block hright

#### Example

Synchronous:

```js
var getBlock = fibos_client.getBlockSync(1);
console.log(getBlock);
```

Asynchronous:

```js
fibos_client.getBlock(1).then(getInfo => {
      console.log(getInfo);
}
```

#### Return

```javascript
{
  "timestamp": "2018-08-01T00:00:00.000",
  "producer": "",
  "confirmed": 1,
  "previous": "0000000000000000000000000000000000000000000000000000000000000000",
  "transaction_mroot": "0000000000000000000000000000000000000000000000000000000000000000",
  "action_mroot": "68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a",
  "schedule_version": 0,
  "new_producers": null,
  "header_extensions": [],
  "producer_signature": "SIG_K1_111111111111111111111111111111111111111111111111111111111111111116uk5ne",
  "transactions": [],
  "block_extensions": [],
  "id": "00000001269a989da17ee0bf745abdcdb62d5440e0e7bf1a37837ba5016f5156",
  "block_num": 1,
  "ref_block_prefix": 3219160737
}
```

### getTableRows

Returns the data in the specified table

```js
fibos_client.getTableRows(json, code, scope, table);
```

#### Parameter

- **json:** boolean Wether show in clear text
- **code:**string contract name
- **scope:** string FIBOS account name
- **table: **string table name

#### Example

Synchronous:

```js
var rs = fibos_client.getTableRowsSync(true, 'contract name', 'Your FIBOS account name', 'accounts');
console.log(rs);
```

Asynchronous:

```js
fibos_client.getTableRows(true, 'contract name', 'Your FIBOS account name', 'accounts').then(rs=>{
    console.log(rs);
});
```

### contract

call contract

```js
fibos_client.contract(contract_name);
```

#### Parameter

- **contract_name: **string contract name

#### Example

Synchronous:

```js
//Init fibos client
...
let ctx = fibos.contractSync('Contract Name'); //contract name
```

Asynchronous:

```js
//Init fibos client
...
let ctx = fibos.contract('Contract Name');  //contract name
```

## ecc module

Elliptic curve encryption function,Multiple methods are built in to generate the secret keys we need

### unsafeRandomKey()

Generate unsafe test key

```javascript
fibos.modules.ecc.unsafeRandomKey();
```

#### Renturn value

- Synchronous: **String**
- Asynchronous: **Promise**

return a testing private key

#### Example

Synchronous:

```js
var privateKey = fibos.modules.ecc.unsafeRandomKeySync();
console.log(privateKey);
/*
result:
5HvSKet1FQBoGitZ7qoN7pWycC6MRF44zQVG7yNPMmGX3wzuSej
*/
```

Asynchronous:

```js
fibos.modules.ecc.unsafeRandomKey().then(unsaferandomkey=>{
    console.log(unsagerandomkey);
})
/*
result:
5Hqd2wRRUYc4zvDBkuQsWFGS9DjrLfgt4BP4wgtHLmiw2N5h1Ar
*/
```

### randomKey()

generate random private key

```
fibos.modules.ecc.randomKey();
```

#### return value

- Synchronous: **String**
- Asynchronous: **Promise**

return an random key

#### Example

Synchronous:

```js
var randomKey=fibos.modules.ecc.randomKeySync();
console.log(randomKey);
/*
result:
5Hx3XoKxrytPnJZxwpwAWz1ySf3dZFLqAsv92ZpTQf5fnSy6BEy
*/
```

Asynchronous:

```js
fibos.modules.ecc.randomKey().then(randomKey=>{
    console.log(randomKey);
})
/*
result:
5KSYGQW1BhpJnJFF1i5kkyDTvifeCQWZEcXF4if9FafJmAbHgRd
*/
```

### seedPrivate()

The same seed produces the same private key each time, using at least 128 random bits to produce a secure private key.

```javascript
ecc.seedPrivate(seed);
```

#### Parameter

- **seed:** string   String of arbitrary length

#### return value

- Synchronous: **String**
- Asynchronous: **Promise**

return private key

#### Example

Synchronous:

```js
var seedPrivate=fibos.modules.ecc.seedPrivateSync(seed);//arbitrary string
console.log(seedPrivate);
/*
result:
5J9YKiVU3AWNkCa2zfQpj1f2NAeMQhLsYU51N8NM28J1bMnmrEQ
*/
```

Asynchronous:

```js
fibos.modules.ecc.seedPrivate(seed).then(seedprivate=>{
    console.log(seedprivate);
})
/*
result:
5J9YKiVU3AWNkCa2zfQpj1f2NAeMQhLsYU51N8NM28J1bMnmrEQ
*/
```

### privateToPublic()

use private key info to calculate the info of public key

```js
fibos.modules.ecc.privateToPublic(PrivateKey);
```

#### Parameter

- **PrivateKey :**PrivateKey   private key 
- **pubkey_prefix:** string  public key prefix（optional, default`'EOS'`）

#### return value

- Synchronous: **String**
- Asynchronous: **Promise**

return public key

#### Example

Synchronous:

```javascript
var privateToPublic=fibos.modules.ecc.privateToPublicSync(PrivateKey);//private key
console.log(privateToPublic);
/*
result:
FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx
*/
```

Asynchronous:

```js
fibos.modules.ecc.privateToPublic(PrivateKey).then(privatetopublic={
    console.log(privatetopublic);
})
/*
result:
FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx
*/
```

### isValidPublic()

Determines whether the public key is valid

```js
fibos.modules.ecc.isValidPublic(pubkey);
```

#### Parameter

- **pubkey:** pubkey public key
- **pubkey_prefix:** string public key prefix（optional，default`'EOS'`）

#### return value

- Synchronous: **boolean**
- Asynchronous: **Promise**

Determines whether the public key is valid
Determines whether the public key is valid


#### Example

Synchronous:

```js
var isValidPublic =fibos.modules.ecc.isValidPublicSync(pubkey);//public key 
console.log(isValidPublic);
/*
result:true
*/
```

Asynchronous:

```javascript
fibos.modules.ecc.isValidPublic(pubkey).then(isvalidpublic=>{
    console.log(isvalidpublic);
})
/*
result:true
*/
```

### isValidPrivate()

Determines whether the private key is valid

```js
fibos.modules.ecc.isValidPrivate(wif);
```

#### Parameter

**wif:** PrivateKey private key

#### return value

- Synchronous: **boolean**
- Asynchronous: **Promise**

Determines validation


#### Example

Synchronous:

```js
var isValidPrivate=fibos.modules.ecc.isValidPrivateSync(wif);//private key
console.log(isValidPrivate);
/*
result:true
*/
```

Asynchronous:

```js
fibos.modules.ecc.isValidPrivate(wif).then(isvalidprivate=>{
    console.log(isvalidprivate);
})
/*
result:true
*/
```

### sign()

Use the data information or hash to create the signature

```js
fibos.modules.ecc.sign(data,PrivateKey);
```

#### Parameter

- **data:** String buffer
- **PrivateKey:** PrivateKey  private key
- **encoding: ** string  data encoding（optional，default`'utf8'`）

#### return value

- Synchronous: **string**
- Asynchronous: **Promise**

string signature

#### Example

Synchronous:

```js
var sign = fibos.modules.ecc.signSync(data,PrivateKey);//string和private key
console.log(sign);
/*
result:
SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

Asynchronous:

```js
fibos.modules.ecc.sign(data,PrivateKey).then(sign=>{//string和private key
    console.log(sign);
})
/*
result:
SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

### signHash()

The signature is created using the data information hashed and private key

```js
fibos.modules.ecc.signHash(dataSha256,PrivateKe);
```

#### Parameter

- **dataSha256:** string | buffer  sha256 hash 32 Byte buffers or strings
- **privateKey:** PrivateKey  private key
- **encoding:** string dataSha256 encoding（If it's a string）（optional，default`'hex'`）

#### return value

- Synchronous: **string**

- Asynchronous: **Promise**

String signature with hash encryption

#### Example

Synchronous:

```js
var signHash = fibos.modules.ecc.signHashSync(dataSha256,PrivateKe);//hash encryption string and private key
console.log(signHash);
/*
result:
SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

Asynchronous:

```js
fibos.modules.ecc.signHash(dataSha256,PrivateKe).then(signhash=>{//hash encryption string and private key
    console.log(signhash);
}))
/*
result:SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

### verify()

validate signature data

```js
fibos.modules.ecc.verify(signature,data,pubkey);
```

#### Parameter

- **signature:** string | buffer  Buffer or hexadecimal string
- **data:** string | buffer  string buffer
- **pubkey:** pubkey | PublicKey public key

#### return value

- Synchronous: **boolean**
- Asynchronous: **Promise**

Determine whether the signature data is valid

#### Example

Synchronous:

```js
var verify = fibos.modules.ecc.verifySync(signature, data, pubkey);//signature,string,public key
console.log(verify);
/*
result:false
*/
```

Asynchronous:

```js
fibos.modules.ecc.verify(signature, data, pubkey).then(verify=>{//signature,string,public key
    console.log(verify);
})
/*
result:false
*/
```

### verifyHash()

validate signature hash data

```js
fibos.modules.ecc.verifyHash(signature, hashData, pubkey);
```

#### Parameter

- **signature:** string | buffer Buffer or hexadecimal string
- **hashData:**  boolean|sha256  Hash data（optional，default`true`）
- **pubkey:** pubkey | PublicKey public key
- **encoding:** string encoding（optional，default`'utf8'`）

#### return value

- Synchronous: **boolean**
- Asynchronous: **Promise**

Validation

#### Example

Synchronous:

```js
fibos.modules.ecc.verifyHash(signature, sha256, pubkey);//signature, hash string,public key
/*
result:false
*/
```

Asynchronous:

```js
fibos.modules.ecc.verifyHash(signature, sha256, pubkey).then(verifyhash=>{//signature, hash string,public key
    console.log(verifyhash);
})
/*
result:false
*/
```

### recover()

revocery public key used for create signature

```js
fibos.modules.ecc.recover(signature, data);
```

#### Parameter

- **signature:** string | buffer（EOSbase58sig ..，Hex，Buffer）
- **data:** string | buffer full data
- **encoding:** string  data encoding（if data is a string）（optional, default`'utf8'`）

#### return value

- Synchronous: **string**
- Asynchronous: **Promise**

 return public key

#### Example

Synchronous:

```js
var recover = fibos.modules.ecc.recoverSync(signature, data);//signature,数据
console.log(recover);
/*
result:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/
```

Asynchronous:

```js
fibos.modules.ecc.recover(signature, 'I am alive').then(recover=>{//signature,数据
    console.log(recover);
})
/*
result:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/
```

### recoverHash()

Recover public key used to create hash signature

```js
fibos.modules.ecc.recoverHash(signature,dataSha256);
```

#### Parameter

- **signature: ** string | buffer（EOSbase58sig ..，Hex，Buffer）
- **dataSha256:** string | buffer  sha256 string 32 byte buffer or hexadecimal string
- **encoding:** string |dataSha256 encoding（if dataSha256 is a string）（optional, default`'hex'`）

#### return value

- Synchronous: **string**
- Asynchronous: **Promise**

reture an public key

#### Example

Synchronous:

```js
var recoverHash = fibos.modules.ecc.recoverHash(signature,dataSha256 );//signature, hash string
console.log(recoverHash);
/*
result:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/
```

Asynchronous:

```js
fibos.modules.ecc.recoverHash(signature, dataSha256).then(recover_hash => {//signature, hash string
      console.log(recover_hash);
}
/*
result:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/                                                                                                              
```

### sha256()

sha256 encryption

```js
fibos.modules.ecc.sha256(data);
```

#### Parameter

- **data:** string | buffer binary data,requiring Buffer.from（data，'hex'）
- **resultEncoding:** string （optional, default`'hex'`）
- **encoding: ** string  result encoding to 'hex'，'binary' or 'base64'（optional, default`'hex'`）

#### return value

- Synchronous: **string | buffer**
- Asynchronous: **Promise**

Encrypted data used by hash.sha256

#### Example

Synchronous:

```js
var sha256 = fibos.modules.ecc.sha256(data);//string
console.log(sha256);
/*
result:
8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab
*/
```

Asynchronous:

```js
fibos.modules.ecc.sha256(data).then(recover_hash => {
      console.log(recover_hash);
}
/*
result:
8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab
*/                                          
```

## System Contract

### newaccount

Create a new FIBOS account

```js
fibos_client.newaccount({
    creator: "eosio", 
    name: "Account Name", 
    owner: "Owner Key", 
    active: "Active Key" 
});
```

#### Parameter

* **creator:** string rreceiver account name
* **name:** string  rreceiver account name
* **owner:** string rreceiver owner permission public key
* **active:** string rreceiver active permission public key  

#### Example

Synchronous:

```js
fibos_client.newaccountSync({
    creator: "Creator Name", //creator account name
    name: "Account Name", //rreceiver account name
    owner: "Owner Key", //rreceiver account owner permission public key
    active: "Active Key" //rreceiver active permission public key
});  
```

Asynchronous:

```js
fibos_client.newaccount({
    creator: "Creator name", //creator account name
    name: "Account Name", //rreceiver account name
    owner: "Owner Key", //rreceiver account owner permission public key
    active: "Active Key" //rreceiver active permission public key
}).then(newaccount => {
    console.log(newaccount);
});
```

### getAccount

get account info

```js
fibos_client.getAccount(account_name);
```

#### Parameter

- **account_name:** string  account name that need to be get

#### Example

Synchronous:

```js
var getAccount = fibos.getAccountSync("Account Name");//account name
console.log(getAccount);
```

Asynchronous:

```js
fibos_client.getAccount("Account Name").then(getAccount => {//account name
      console.log(getAccount);
}
```

#### return value

```js
{
  "account_name": "hellomongodb",
  "head_block_num": 7056896,
  "head_block_time": "2018-11-26T01:44:42.000",
  "privileged": false,
  "last_code_update": "1970-01-01T00:00:00.000",
  "created": "2018-11-26T01:44:01.000",
  "ram_quota": 510873,
  "net_weight": 10000,
  "cpu_weight": 10000,
  ...
}
```

### buyrambytes

The creator calls this method to buy memory for the creator to store information about the new account

```js
fibos_client.buyrambytes({
    payer: 'eosio.token',
    receiver: 'Receiver Account',
    bytes: 4096 
});
```

#### Parameter

* **payer:**string  creator account name

* **receiver:** string receiver account name

* **bytes:** number Memory size consumed (bytes)

#### Example

```js
fibos_client.buyrambytes({
    payer: 'eosio.token',//creator account name
    receiver: 'Receiver Account',//reciever account name
    bytes: 4096 //The amount of memory consumed
});
```
### delegatebw

Mortgage tokens to obtain CPU and NET resources

```js
fibos_client.delegatebw({
    from: 'From Account',
    receiver: 'Receiver Account',
    stake_net_quantity: '0.1000 FO',
    stake_cpu_quantity: '0.1000 FO',
    transfer: 1
});
```

#### Parameter

* **from:** string The name of the mortgagor's account

* **receiver:** string The account name of the resource recipient

* **stake_net_quantity:** string The creator mortgages FO to get NET for the creator

* **stake_cpu_quantity:** string The creator mortgages FO to the creator to get the CPU

* **transfer: ** number usually use 1 to get resources for someone else to mortgage FO, and if you want to get resources for yourself you need to change it to 0
#### Example

```js
fibos_client.delegatebw({
    from: 'from',//creator account name
    receiver: 'Your_Account',//reciever account name
    stake_net_quantity: '0.1000 FO',//The creator mortgages FO to get NET for the creator
    stake_cpu_quantity: '0.1000 FO',//The creator mortgages FO to get CPU for the creator
    transfer: 1// Using 1 represents mortgaging FO for someone else to get resources
});
```

## Token Contract

There are two types of token in FIBOS: classic token and intelligent token

### transfer

Configured EOS MainNet and EOS RPC address and EOS private key and then initialize a EOS, client by calling a ` transferSync ` method, realize the transfer operation

```js
ctx.transfer(from, to, quantity, memo, {
    authorization: 'author_name'
})
```

#### Parameter

* **form:** string  The transferor                  
* **to:** string The transferee                  
* **quantity:** number amount 1.0000 EOS         
* **memo:** string note
* **authorization:** string authorization

####  Example

Synchronous:

```js
let r = ctx.transferSync('FROM Account Name', 'fiboscouncil', '11 FO', 'transfer 11 FO FROM xxx to xxx', {
    authorization: 'fibosaccount'//permission
});
console.log(r);
```

Asynchronous:

```js
ctx.transfer('FROM Account Name', 'fiboscouncil', '11 FO', 'transfer 11 FO FROM xxx to xxx', {
    authorization: 'fibosaccount'//permission
}).then(r=>{
    console.log(r);
});
```

### exchange

Use Bancor for token conversion in FIBOS

```js
ctx.exchange(owner, quantity, tosym, memo, {
    authorization: 'author_name'
});
```

#### Parameter

* **owner:** string exchange account name         
* **quantity:** number exchange token amount     
* **tosym:** string exchange token type
* **memo:** string note
* **authorization:** string authorization    

#### Example

Synchronous:

```javascript
var result = ctx.exchangeSync('Owner Account', '1.0000 VO@fibostest123', '0.0000 FO@eosio', memo, {
    authorization: owner//authorization
});
console.log(result);
```

Asynchronous:

```js
ctx.exchange('Owner Account', '1.0000 VO@fibostest123', '0.0000 FO@eosio', memo, {
    authorization: owner//authorization
}).then(result=>{
    console.log(result);
});
```

### excreate

Call the token contract ` excreate ` interface to access token issue

```js
ctx.excreate(issuer, maximum_supply, connector_weight, maximum_exchange, reserve_supply, reserve_connector_balance, expiration, buy_fee,sell_fee,connector_balance_issuer,{
  authorization: 'author_name'
}); 
```

#### Method Parameter

* **issue:** string  Token issue account
* **maximum_supply:** assert  Maximum number of token issued
* **connector_weight:** number  Connector weight
* **maximum_exchange:** assert  Maximum number of echange(circulation) tokens
* **reserve_supply:** assert  Not circulation token amount
* **reserve_connector_balance:** assert  Amount of outstanding token security deposit
* **expiration:**   time_point_sec Project lock period preset by the project side
* **buy_fee:** double  transaction fee of token presets by project party
* **sell_fee:** double  Cashing fee presets by project party
* **connector_balance_issuer:** string Reserve publisher
* **authorization:** string  permission

#### Example

Issuing common token

Synchronous:

```javascript
//init fibos client
...
let r = ctx.excreateSync(issuer, '90000000000.0000 DDD', 0, '10000000000.0000 DDD', '3000000000.0000 DDD', '90000.0000 FO', '2018-10-29T18:54:00', 0,0, 'eosio',{ //Custom fee, Greater than 0 is less than or equal to 1, the reserve here is FO, so reserve publisher to fill in eosio
  authorization: name  //authorization
}); //expiration needs to larger or equal to current time
console.log(r)
```

Asynchronous:

```js
/init fibos client
...
ctx.excreate(issuer, '90000000000.0000 DDD', 0, '10000000000.0000 DDD', '3000000000.0000 DDD', '90000.0000 FO', '2018-10-29T18:54:00',0,0 , 'eosio',{//Custom fee, Greater than 0 is less than or equal to 1, the reserve here is FO, so reserve publisher to fill in eosio
  authorization: name  //authorization
}).then(r=>{
    console.log(r);
}); //expiration needs to larger or equal to current time
```

Issuing smart token

Synchronous:

```javascript
//init fibos client
...
let r = ctx.excreateSync(issuer, '100000000000.0000 AAA',  0.15,'10000000000.0000 AAA', '3000000000.0000 AAA', '90000.0000 FO', '2018-10-29T18:54:00',0,0 , 'eosio',{//Custom service fee,current is 0,The reserve here is FO, so the issuer of the reserve fills in the eosio
    authorization: name //authorization
});  //expiration needs to larger or equal to current time
console.log(r);
```

Asynchronous:

```js
//init fibos client
...
ctx.excreateSync(issuer, '100000000000.0000 AAA',  0.15,'10000000000.0000 AAA', '3000000000.0000 AAA', '90000.0000 FO', '2018-10-29T18:54:00',0,0, 'eosio',{//Custom service fee,current is 0,The reserve here is FO, so the issuer of the reserve fills in the eosio
    authorization: name //authorization
}).then(r=>{
    console.log(r);
});  //expiration needs to larger or equal to current time
```

### exissue

additional token issuing

```js
ctx.exissue(issuer, maximum_supply, connector_weight, maximum_exchange, reserve_supply, reserve_connector_balance, expiration, {
  authorization: 'author_name'
});
```

#### Parameter

* **issuer:** string  token issuer account
* **maximum_supply:** assert  Maximum number of token issued
* **connector_weight:** number  connector weight
* **maximum_exchange:** assert  Maximum number of echange(circulation) tokens
* **reserve_supply:** assert  Not circulation token amount
* **reserve_connector_balance:** assert  Amount of outstanding token security deposit
* **expiration:**   time_point_sec Project lock period preset by the project side
* **authorization:** string  permission
#### Example

Synchronous:

```javascript
//init fibos client
...
let r = ctx.exissueSync(name, '1000000.0000 ABC@fibostest123', 'issue to fibostest123', {
  authorization: name //authorization
});
console.log(r);
```

Asynchronous:

```js
//init fibos client
...
ctx.exissue(name, '1000000.0000 ABC@fibostest123', 'issue to fibostest123', {
  authorization: name  //authorization
}).then(r=>{
  console.log(r);  
})
```

### exdestroy

destroy token(the token can be destroyed only by the number of circulation is 0)

```js
ctx.exdestroy(symbol, {authorization: 'author_name'});
```

#### Parameter

- **symbol: **string  Token exchange data
- **authorization:**  string  authorization

#### Example

Synchronous:

```js
//init fibos client
...
let r = ctx.exdestroySync(`0.0000 AAA@fibostest123`, {authorization: 'fibostest123'});
```

Asynchronous:

```js
//init fibos client
...
ctx.exdestroy(`0.0000 AAA@fibostest123`, {authorization: 'fibostest123'})
```

### exlocktrans

Locked position(When the project party issues the smart token, the value of the parameter reserve_supply filled in by the project party will vary with the operation of destroying and unlocking the token.)

```js
ctx.exlocktrans(from, to, quantityt, expiration, expiration_to,memo, {
    authorization: 'author_name'
});
```

#### method parameters

* **from:** string  token transferor
* **to:** string  token transferee
* **quantity:** number token amount
* **expiration:** time_point_sec lockout time of rolling out
* **expiration_to:**  time_point_sec lockout time of rolling in
* **memo:** string  note
* **authorization:** string  authorization

#### Example

Synchronous:

```js
//init fibos client
...
let r = ctx.exlocktransSync('nmslwsndhjyz', 'fibostest123', `10000.0000 BBB@5hzuyqumr3l5`, '2018-10-29T18:54:00', '2018-10-29T18:54:00', `transfer 1000  ABC@uepgdzfhucin`, {
    authorization: 'nmslwsndhjyz'  //authorization
}); //expiration_to must larger or equal to expiration
console.notice(r)
```

Asynchronous:

```js
//init fibos client
...
ctx.exlocktrans('nmslwsndhjyz', 'fibostest123', `10000.0000 BBB@5hzuyqumr3l5`, '2018-10-29T18:54:00', '2018-10-29T18:54:00', `transfer 1000  ABC@uepgdzfhucin`, {
    authorization: 'nmslwsndhjyz'  //authorization
}).then(r=>{
    console.notice(r);
}) 
//expiration_to must larger or equal to expiration
```

### exunlock

Unlock (the user can change the token in the lock warehouse into the token in circulation through unlock operation)

```js
ctx.exunlock(owner, quantity, expiration, memo, {
    authorization: 'author_name'//authorization
});
```

#### method and parameters

* **owner:** owner token owner
* **quantity:** number unlock amount
* **expiration:** time_point_sec lock period
* **memo:** string note
* **authorization:** string  authorization

#### Example

Synchronous:

```js
//init fibos client
...
let r = ctx.exunlockSync('fibostest123', '100.0000 ADC@nmslwsndhjyz', 1537960501, 'unlock 100.0000 ADC', {
    authorization: 'hujzwsndnmsl' //authorization
})
console.notice(r);
```

Asynchronous:

```js
//init fibos client
...
ctx.exunlock('fibostest123', '100.0000 ADC@nmslwsndhjyz', 1537960501, 'unlock 100.0000 ADC', {
    authorization: 'hujzwsndnmsl' //authorization
}).then(r=>{
    console.notice(r);
})
```

### ctxrecharge

contract sub-wallet top up

```js
ctx.ctxrecharge(owner, quantity, memo, {
    authorization: 'author_name'//authorization
});
```

#### methods and parameters

* **owner:** string  account owner
* **quantity:** number  top up token amount
* **memo:** string  note
* **authorization:** string  authorization

#### Example

Synchronous top up:

```js
//init fibos client
...
let r = ctx.ctxrechargeSync('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxrecharge', {
			authorization: 'tteesstt1122'
})
console.notice(r);
```

Asynchronous top up:

```js
//init fibos client
...
ctx.ctxrecharge('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxrecharge', {
			authorization: 'tteesstt1122' //authorization
}).then(r=>{
    console.notice(r);
})
```

### ctxextract

contract sub-wallet withdrawal

```js
ctx.ctxextract(owner, quantity, memo, {
    authorization: 'author_name'//authorization
});
```

#### method and operation

* **owner:** string  account owner
* **quantity:** number  top up amount
* **memo:** string  note
* **authorization:** string  authorization
#### Example

Synchronous withdrawal:

```js
//init fibos client
...
let r = ctx.ctxextractSync('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxextract', {
			authorization: 'tteesstt1122'//authorization
})
console.notice(r);
```

Asynchronous withdrawal:

```js
//init fibos client
...
ctx.ctxextract('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxextract', {
			authorization: 'tteesstt1122'  //authorization
}).then(r=>{
    console.notice(r);
})
```

### ctxtransfer

Contract sub-wallet transfer

```js
ctx.ctxtransfer(from, to, quantity, memo, {		
authorization: 'author_name'//authorization
});
```

#### Parameter

* **from:** string  token transferor
* **to:** string  token transferee
* **quantity:** number  token amount
* **memo:** string  note
* **authorization:** string  authorization

#### Example

Synchronous transfer:

```js
//init fibos client
...
let r = ctx.ctxtransferSync('tteesstt1122', 'tteesstt2222', '50.0000 ADC@nmslwsndhjyz', 'ctxtransfer', {		
authorization: 'nmslwsndhjyz'  //authorization	
});
console.notice(r);
```

Asynchronous transfer:

```js
//init fibos client
...
ctx.ctxtransfer('tteesstt1122', 'tteesstt2222', '50.0000 ADC@nmslwsndhjyz', 'ctxtransfer', {		
authorization: 'nmslwsndhjyz'//authorization
}).then(r=>{
    console.notice(r);
})
```


