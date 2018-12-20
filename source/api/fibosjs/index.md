---
title: 
type: fibosjs
order: 1
---


# FIBOS.JS

FIBOS 和 EOSIO 区块链的通用库。

## Basic

在区块链中对用户账户信息操作的各种方法

### 获取客户端实例

以链接到测试网为例

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

获取区块信息

```js
fibos_client.getInfo();
```

#### 示例

同步:

```js
var getInfo = fibos_client.getInfoSync();
console.log(getInfo);
```

异步:

```js
fibos_client.getInfo().then(getInfo => {
      console.log(getInfo);
}
```

#### 返回值

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

#### 返回值参数说明

* **server_version:** text 服务端版本

* **chain_id:**string 区块链的链地址

* **head_block_num: **number 当前区块高度

* **last_irreversible_block_num: **number 不可逆区块高度

* **last_irreversible_block_id: **string 不可逆区块地址

* **head_block_id: **string 当前区块地址

* **head_block_time: **date 当前区块时间

* **head_block_producer: **string 当前区块进程

* **virtual_block_cpu_limit: **number 虚拟区块 cpu 限制

* **virtual_block_net_limit: **number 虚拟区块网络限制

* **block_cpu_limit: **number 区块 cpu 限制

* **block_net_limit: **number 区块网络限制

* **server_version_string: **string 服务端版本字符表示

### getBlock

获取块信息

```j's
fibos_client.getBlock(block_number);
```

#### 参数

- **block_number:** int  块的高度

#### 示例

同步:

```js
var getBlock = fibos_client.getBlockSync(1);
console.log(getBlock);
```

异步:

```js
fibos_client.getBlock(1).then(getInfo => {
      console.log(getInfo);
}
```

#### 返回值

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

返回指定表中的数据

```js
fibos_client.getTableRows(json, code, scope, table);
```

#### 参数

- **json:** boolean 是否明文展示
- **code:**string 合约名
- **scope:** string FIBOS 账户名
- **table: **string 表名

#### 示例

同步:

```js
var rs = fibos_client.getTableRowsSync(true, '合约名', '你的 FIBOS 账户名', 'accounts');
console.log(rs);
```

异步:

```js
fibos_client.getTableRows(true, '合约名', '你的 FIBOS 账户名', 'accounts').then(rs=>{
    console.log(rs);
});
```

### contract

调用合约

```js
fibos_client.contract(contract_name);
```

#### 参数

- **contract_name: **string 合约名

#### 示例

同步:

```js
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('Contract Name'); //合约名
```

异步:

```js
//初始化 fibos 客户端
...
let ctx = fibos.contract('Contract Name');  //合约名
```

## ecc 模块

椭圆曲线加密函数,内置多个方法用来生成我们需要的秘钥

### unsafeRandomKey()

生成不安全的测试私钥

```javascript
fibos.modules.ecc.unsafeRandomKey();
```

#### 返回值

- 同步: **String**
- 异步: **Promise**

返回一个测试私钥

#### 示例

同步:

```js
var privateKey = fibos.modules.ecc.unsafeRandomKeySync();
console.log(privateKey);
/*
运行结果:
5HvSKet1FQBoGitZ7qoN7pWycC6MRF44zQVG7yNPMmGX3wzuSej
*/
```

异步:

```js
fibos.modules.ecc.unsafeRandomKey().then(unsaferandomkey=>{
    console.log(unsagerandomkey);
})
/*
运行结果:
5Hqd2wRRUYc4zvDBkuQsWFGS9DjrLfgt4BP4wgtHLmiw2N5h1Ar
*/
```

### randomKey()

生成随机私钥

```
fibos.modules.ecc.randomKey();
```

#### 返回值

- 同步: **String**
- 异步: **Promise**

返回一个随机私钥

#### 示例

同步:

```js
var randomKey=fibos.modules.ecc.randomKeySync();
console.log(randomKey);
/*
运行结果:
5Hx3XoKxrytPnJZxwpwAWz1ySf3dZFLqAsv92ZpTQf5fnSy6BEy
*/
```

异步:

```js
fibos.modules.ecc.randomKey().then(randomKey=>{
    console.log(randomKey);
})
/*
运行结果:
5KSYGQW1BhpJnJFF1i5kkyDTvifeCQWZEcXF4if9FafJmAbHgRd
*/
```

### seedPrivate()

同一种子每次都产生相同的私钥,使用至少 128 个随机位来产生一个安全的私钥。

```javascript
ecc.seedPrivate(seed);
```

#### 参数

- **seed:** string   任意长度的字符串。

#### 返回值

- 同步: **String**
- 异步: **Promise**

返回私钥

#### 示例

同步:

```js
var seedPrivate=fibos.modules.ecc.seedPrivateSync(seed);//任意字符串
console.log(seedPrivate);
/*
运行结果:
5J9YKiVU3AWNkCa2zfQpj1f2NAeMQhLsYU51N8NM28J1bMnmrEQ
*/
```

异步:

```js
fibos.modules.ecc.seedPrivate(seed).then(seedprivate=>{
    console.log(seedprivate);
})
/*
运行结果:
5J9YKiVU3AWNkCa2zfQpj1f2NAeMQhLsYU51N8NM28J1bMnmrEQ
*/
```

### privateToPublic()

通过私钥信息来计算公钥信息

```js
fibos.modules.ecc.privateToPublic(PrivateKey);
```

#### 参数

- **PrivateKey :**PrivateKey   私钥 
- **pubkey_prefix:** string  公钥前缀（可选，默认`'EOS'`）

#### 返回值

- 同步: **String**
- 异步: **Promise**

返回公钥

#### 示例

同步:

```javascript
var privateToPublic=fibos.modules.ecc.privateToPublicSync(PrivateKey);//私钥
console.log(privateToPublic);
/*
运行结果:
FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx
*/
```

异步:

```js
fibos.modules.ecc.privateToPublic(PrivateKey).then(privatetopublic={
    console.log(privatetopublic);
})
/*
运行结果:
FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx
*/
```

### isValidPublic()

判断公钥是否有效

```js
fibos.modules.ecc.isValidPublic(pubkey);
```

#### 参数

- **pubkey:** pubkey 公钥
- **pubkey_prefix:** string 公钥前缀（可选，默认`'EOS'`）

#### 返回值

- 同步: **boolean**
- 异步: **Promise**

判断公钥是否有效

#### 示例

同步:

```js
var isValidPublic =fibos.modules.ecc.isValidPublicSync(pubkey);//公钥 
console.log(isValidPublic);
/*
运行结果:true
*/
```

异步:

```javascript
fibos.modules.ecc.isValidPublic(pubkey).then(isvalidpublic=>{
    console.log(isvalidpublic);
})
/*
运行结果:true
*/
```

### isValidPrivate()

判断私钥是否有效

```js
fibos.modules.ecc.isValidPrivate(wif);
```

#### 参数

**wif:** PrivateKey 私钥

#### 返回值

- 同步: **boolean**
- 异步: **Promise**

判断是否有效

#### 示例

同步:

```js
var isValidPrivate=fibos.modules.ecc.isValidPrivateSync(wif);//私钥
console.log(isValidPrivate);
/*
运行结果:true
*/
```

异步:

```js
fibos.modules.ecc.isValidPrivate(wif).then(isvalidprivate=>{
    console.log(isvalidprivate);
})
/*
运行结果:true
*/
```

### sign()

使用 data 信息或 hash 来创建签名

```js
fibos.modules.ecc.sign(data,PrivateKey);
```

#### 参数

- **data:** 字符串  缓冲区
- **PrivateKey:** PrivateKey  私钥
- **encoding: ** string  数据编码（可选，默认`'utf8'`）

#### 返回值

- 同步: **string**
- 异步: **Promise**

字符串签名

#### 示例

同步:

```js
var sign = fibos.modules.ecc.signSync(data,PrivateKey);//字符串和私钥
console.log(sign);
/*
运行结果:
SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

异步:

```js
fibos.modules.ecc.sign(data,PrivateKey).then(sign=>{//字符串和私钥
    console.log(sign);
})
/*
运行结果:
SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

### signHash()

使用进行 hash 加密的 data 信息和私钥来创建签名

```js
fibos.modules.ecc.signHash(dataSha256,PrivateKe);
```

#### 参数

- **dataSha256:** string | buffer  sha256 hash 32 字节缓冲区或字符串
- **privateKey:** PrivateKey  私钥
- **encoding:** string dataSha256 编码（如果是字符串）（可选，默认`'hex'`）

#### 返回值

- 同步: **string**

- 异步: **Promise**

带有 hash 加密的字符串签名

#### 示例

同步:

```js
var signHash = fibos.modules.ecc.signHashSync(dataSha256,PrivateKe);//hash加密字符串和私钥
console.log(signHash);
/*
运行结果:
SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

异步:

```js
fibos.modules.ecc.signHash(dataSha256,PrivateKe).then(signhash=>{//hash加密字符串和私钥
    console.log(signhash);
}))
/*
运行结果:SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

### verify()

验证签名数据

```js
fibos.modules.ecc.verify(signature,data,pubkey);
```

#### 参数

- **signature:** string | buffer  缓冲区或十六进制字符串
- **data:** string | buffer  字符串数据
- **pubkey:** pubkey | PublicKey 公钥

#### 返回值

- 同步: **boolean**
- 异步: **Promise**

判断签名数据是否成立

#### 示例

同步:

```js
var verify = fibos.modules.ecc.verifySync(signature, data, pubkey);//签名,字符串,公钥
console.log(verify);
/*
运行结果:false
*/
```

异步:

```js
fibos.modules.ecc.verify(signature, data, pubkey).then(verify=>{//签名,字符串,公钥
    console.log(verify);
})
/*
运行结果:false
*/
```

### verifyHash()

验证签名数据hash

```js
fibos.modules.ecc.verifyHash(signature, hashData, pubkey);
```

#### 参数

- **signature:** string | buffer  缓冲区或十六进制字符串
- **hashData:**  boolean|sha256  哈希数据（可选，默认`true`）
- **pubkey:** pubkey | PublicKey 公钥
- **encoding:** string encoding（可选，默认`'utf8'`）

#### 返回值

- 同步: **boolean**
- 异步: **Promise**

判断是否成立

#### 示例

同步:

```js
fibos.modules.ecc.verifyHash(signature, sha256, pubkey);//签名, hash 字符串,公钥
/*
运行结果:false
*/
```

异步:

```js
fibos.modules.ecc.verifyHash(signature, sha256, pubkey).then(verifyhash=>{//签名, hash 字符串,公钥
    console.log(verifyhash);
})
/*
运行结果:false
*/
```

### recover()

恢复用于创建签名的公钥

```js
fibos.modules.ecc.recover(signature, data);
```

#### 参数

- **signature:** string | buffer（EOSbase58sig ..，Hex，Buffer）
- **data:** string | buffer 完整数据
- **encoding:** string  数据编码（如果数据是字符串）（可选，默认`'utf8'`）

#### 返回值

- 同步: **string**
- 异步: **Promise**

 返回公钥

#### 示例

同步:

```js
var recover = fibos.modules.ecc.recoverSync(signature, data);//签名,数据
console.log(recover);
/*
运行结果:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/
```

异步:

```js
fibos.modules.ecc.recover(signature, 'I am alive').then(recover=>{//签名,数据
    console.log(recover);
})
/*
运行结果:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/
```

### recoverHash()

恢复用于创建 hash 签名的公钥

```js
fibos.modules.ecc.recoverHash(signature,dataSha256);
```

#### 参数

- **signature: ** string | buffer（EOSbase58sig ..，Hex，Buffer）
- **dataSha256:** string | buffer  sha256 散列 32 字节缓冲区或十六进制字符串
- **encoding:** string |dataSha256 编码（如果 dataSha256 是字符串）（可选，默认`'hex'`）

#### 返回值

- 同步: **string**
- 异步: **Promise**

返回一个公钥

#### 示例

同步:

```js
var recoverHash = fibos.modules.ecc.recoverHash(signature,dataSha256 );//签名, hash 字符串
console.log(recoverHash);
/*
运行结果:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/
```

异步:

```js
fibos.modules.ecc.recoverHash(signature, dataSha256).then(recover_hash => {//签名, hash 字符串
      console.log(recover_hash);
}
/*
运行结果:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/                                                                                                              
```

### sha256()

sha256 加密

```js
fibos.modules.ecc.sha256(data);
```

#### 参数

- **data:** string | buffer 二进制数据,需要 Buffer.from（data，'hex'）
- **resultEncoding:** string （可选，默认`'hex'`）
- **encoding: ** string  结果编码成 'hex'，'binary' 或 'base64'（可选，默认`'hex'`）

#### 返回值

- 同步: **string | buffer**
- 异步: **Promise**

使用 hash.sha256 加密后的数据

#### 示例

同步:

```js
var sha256 = fibos.modules.ecc.sha256(data);//字符串
console.log(sha256);
/*
运行结果:
8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab
*/
```

异步:

```js
fibos.modules.ecc.sha256(data).then(recover_hash => {
      console.log(recover_hash);
}
/*
运行结果:
8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab
*/                                          
```

## System Contract

### newaccount

创建一个新的 FIBOS 账户

```js
fibos_client.newaccount({
    creator: "eosio", 
    name: "Account Name", 
    owner: "Owner Key", 
    active: "Active Key" 
});
```

#### 参数

* **creator:** string 创建者的账户名
* **name:** string  被创建者的账户名
* **owner:** string 被创建者账户 owner 权限公钥
* **active:** string 被创建者 active 权限公钥  

#### 示例

同步:

```js
fibos_client.newaccountSync({
    creator: "Creator Name", //创建者的账户名
    name: "Account Name", //被创建者的账户名
    owner: "Owner Key", //被创建者账户 owner 权限公钥
    active: "Active Key" //被创建者 active 权限公钥
});  
```

异步:

```js
fibos_client.newaccount({
    creator: "Creator name", //创建者的账户名
    name: "Account Name", //被创建者的账户名
    owner: "Owner Key", //被创建者账户 owner 权限公钥
    active: "Active Key" //被创建者 active 权限公钥
}).then(newaccount => {
    console.log(newaccount);
});
```

### getAccount

获取账户信息

```js
fibos_client.getAccount(account_name);
```

#### 参数

- **account_name:** string  需要获取的账户名

#### 示例

同步:

```js
var getAccount = fibos.getAccountSync("Account Name");//账户名
console.log(getAccount);
```

异步:

```js
fibos_client.getAccount("Account Name").then(getAccount => {//账户名
      console.log(getAccount);
}
```

#### 返回值

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

创建者调用该方法为被创建者购买内存来存放新账户的信息

```js
fibos_client.buyrambytes({
    payer: 'eosio.token',
    receiver: 'Receiver Account',
    bytes: 4096 
});
```

#### 参数

* **payer:**string  创建者的账户名

* **receiver:** string 被创建者的账户名

* **bytes:** number 消耗的内存大小(字节)

#### 示例

```js
fibos_client.buyrambytes({
    payer: 'eosio.token',//创建者的账户名
    receiver: 'Receiver Account',//被创建者的账户名
    bytes: 4096 //消耗的内存大小
});
```
### delegatebw

抵押代币获取 cpu 和带宽资源

```js
fibos_client.delegatebw({
    from: 'From Account',
    receiver: 'Receiver Account',
    stake_net_quantity: '0.1000 FO',
    stake_cpu_quantity: '0.1000 FO',
    transfer: 1
});
```

#### 参数

* **from:** string 抵押方的账户名

* **receiver:** string 资源接收方的账户名

* **stake_net_quantity:** string 创建者为被创建者抵押FO获取NET

* **stake_cpu_quantity:** string 创建者为被创建者抵押FO获取CPU

* **transfer: ** number 通常用1 代表替别人抵押 FO 获取资源,如果你想要自己获取资源需要将其改为0

#### 示例

```js
fibos_client.delegatebw({
    from: 'from',//创建者的账户名
    receiver: 'Your_Account',//被创建者的账户名
    stake_net_quantity: '0.1000 FO',//创建者为被创建者抵押 FO 获取 NET
    stake_cpu_quantity: '0.1000 FO',//创建者为被创建者抵押 FO 获取 CPU
    transfer: 1//用 1 代表替别人抵押 FO 获取资源
});
```

## Token Contract

在 FIBOS 中有两种通证：经典通证和智能通证

### transfer

配置好 EOS MainNet 和 EOS RPC 地址 和 EOS 私钥后,便初始化了一个 eos 客户端,通过调用 `transferSync` 方法,实现转账操作

```js
ctx.transfer(from, to, quantity, memo, {
    authorization: 'author_name'
})
```

#### 参数

* **form:** string  转出方                  
* **to:** string 转入方                  
* **quantity:** number 数量 1.0000 EOS         
* **memo:** string 备注
* **authorization:** string 授权

####  示例

同步:

```js
let r = ctx.transferSync('FROM Account Name', 'fiboscouncil', '11 FO', 'transfer 11 FO FROM xxx to xxx', {
    authorization: 'fibosaccount'//权限
});
console.log(r);
```

异步:

```js
ctx.transfer('FROM Account Name', 'fiboscouncil', '11 FO', 'transfer 11 FO FROM xxx to xxx', {
    authorization: 'fibosaccount'//权限
}).then(r=>{
    console.log(r);
});
```

### exchange

在 FIBOS 使用 Bancor 进行通证之间兑换

```js
ctx.exchange(owner, quantity, tosym, memo, {
    authorization: 'author_name'
});
```

#### 参数

* **owner:** string 兑换账号名         
* **quantity:** number 兑换通证数量     
* **tosym:** string 兑换通证目标类型 
* **memo:** string 备注信息 
* **authorization:** string 授权    

#### 示例

同步:

```javascript
var result = ctx.exchangeSync('Owner Account', '1.0000 VO@fibostest123', '0.0000 FO@eosio', memo, {
    authorization: owner//授权
});
console.log(result);
```

异步:

```js
ctx.exchange('Owner Account', '1.0000 VO@fibostest123', '0.0000 FO@eosio', memo, {
    authorization: owner//授权
}).then(result=>{
    console.log(result);
});
```

### excreate

调用 token 合约中的 `excreate` 接口来进行通证的发行

```js
ctx.excreate(issuer, maximum_supply, connector_weight, maximum_exchange, reserve_supply, reserve_connector_balance, expiration, buy_fee,sell_fee,{
  authorization: 'author_name'
}); 
```

#### 方法参数

* **issuer:** string  通证发行账号
* **maximum_supply:** assert  最大可发行通证数量
* **connector_weight:** number  连接器权重
* **maximum_exchange:** assert  最大可兑换(流通)的通证数量
* **reserve_supply:** assert  未流通通证数量
* **reserve_connector_balance:** assert  未流通通证保证金数量
* **expiration:**   time_point_sec项目方预设的项目锁仓期
* **buy_fee:** double  项目方预设通证兑入手续费
* **sell_fee:** double  项目方预设通证兑出手续费
* **authorization:** string  权限

#### 示例
发行普通通证

同步:

```javascript
//初始化 fibos 客户端
...
let r = ctx.excreateSync(issuer, '90000000000.0000 DDD', 0, '10000000000.0000 DDD', '3000000000.0000 DDD', '90000.0000 FO', '2018-10-29T18:54:00', 0,0{ //手续费自定义,目前为0
  authorization: name  //授权
}); //expiration 需大于等于当前时间
console.log(r)
```

异步:

```js
//初始化 fibos 客户端
...
ctx.excreate(issuer, '90000000000.0000 DDD', 0, '10000000000.0000 DDD', '3000000000.0000 DDD', '90000.0000 FO', '2018-10-29T18:54:00',0,0 {//手续费自定义,目前为0
  authorization: name  //授权
}).then(r=>{
    console.log(r);
}); //expiration 需大于等于当前时间
```

发行智能通证

同步:

```javascript
//初始化 fibos 客户端
...
let r = ctx.excreateSync(issuer, '100000000000.0000 AAA',  0.15,'10000000000.0000 AAA', '3000000000.0000 AAA', '90000.0000 FO', '2018-10-29T18:54:00',0,0 {//手续费自定义,目前为0
    authorization: name //授权
});  //expiration 需大于等于当前时间
console.log(r);
```

异步:

```js
//初始化 fibos 客户端
...
ctx.excreateSync(issuer, '100000000000.0000 AAA',  0.15,'10000000000.0000 AAA', '3000000000.0000 AAA', '90000.0000 FO', '2018-10-29T18:54:00',0,0 {//手续费自定义,目前为0
    authorization: name //授权
}).then(r=>{
    console.log(r);
});  //expiration 需大于等于当前时间
```

### exissue

增发通证

```js
ctx.exissue(issuer, maximum_supply, connector_weight, maximum_exchange, reserve_supply, reserve_connector_balance, expiration, {
  authorization: 'author_name'
});
```

#### 参数

* **issuer:** string  通证发行账号
* **maximum_supply:** assert  最大可发行通证数量
* **connector_weight:** number  连接器权重
* **maximum_exchange:** assert  最大可兑换(流通)的通证数量
* **reserve_supply:** assert  未流通通证数量
* **reserve_connector_balance:** assert  未流通通证保证金数量
* **expiration:**   time_point_sec项目方预设的项目锁仓期
* **authorization:** string  权限
#### 示例

同步:

```javascript
//初始化 fibos 客户端
...
let r = ctx.exissueSync(name, '1000000.0000 ABC@fibostest123', 'issue to fibostest123', {
  authorization: name //授权
});
console.log(r);
```

异步:

```js
//初始化 fibos 客户端
...
ctx.exissue(name, '1000000.0000 ABC@fibostest123', 'issue to fibostest123', {
  authorization: name  //授权
}).then(r=>{
  console.log(r);  
})
```

### exdestroy

销毁通证(只有流通量为 0 才能进行销毁)

```js
ctx.exdestroy(symbol, {authorization: 'author_name'});
```

#### 参数

- **symbol: **string  通证兑换流通量
- **authorization:**  string  授权

#### 示例

同步:

```js
//初始化 fibos 客户端
...
let r = ctx.exdestroySync(`0.0000 AAA@fibostest123`, {authorization: 'fibostest123'});
```

异步:

```js
//初始化 fibos 客户端
...
ctx.exdestroy(`0.0000 AAA@fibostest123`, {authorization: 'fibostest123'})
```

### exlocktrans

锁仓(项目方发行智能通证时，填写的 reserve_supply 这个参数的值，锁仓量会随着销毁和解锁通证的操作而变化。)

```js
ctx.exlocktrans(from, to, quantityt, expiration, expiration_to,memo, {
    authorization: 'author_name'
});
```

#### 方法参数

* **from:** string  通证转出方
* **to:** string  通证转入方
* **quantity:** number 通证数量
* **expiration:** time_point_sec 待转出锁仓时间
* **expiration_to:**  time_point_sec 待转入锁仓时间
* **memo:** string  附言
* **authorization:** string  授权

#### 示例

同步:

```js
//初始化 fibos 客户端
...
let r = ctx.exlocktransSync('nmslwsndhjyz', 'fibostest123', `10000.0000 BBB@5hzuyqumr3l5`, '2018-10-29T18:54:00', '2018-10-29T18:54:00', `transfer 1000  ABC@uepgdzfhucin`, {
    authorization: 'nmslwsndhjyz'  //授权
}); //expiration_to 必须大于等于 expiration
console.notice(r)
```

异步:

```js
//初始化 fibos 客户端
...
ctx.exlocktrans('nmslwsndhjyz', 'fibostest123', `10000.0000 BBB@5hzuyqumr3l5`, '2018-10-29T18:54:00', '2018-10-29T18:54:00', `transfer 1000  ABC@uepgdzfhucin`, {
    authorization: 'nmslwsndhjyz'  //授权
}).then(r=>{
    console.notice(r);
}) 
//expiration_to 必须大于等于 expiration
```

### exunlock

解锁(用户通过解锁操作来讲锁仓中的通证变为流通中的通证)

```js
ctx.exunlock(owner, quantity, expiration, memo, {
    authorization: 'author_name'//授权
});
```

#### 方法和参数

* **owner:** owner 通证持有者
* **quantity:** number 解锁数量
* **expiration:** time_point_sec 锁仓期
* **memo:** string 附言
* **authorization:** string  授权

#### 示例

同步:

```js
//初始化 fibos 客户端
...
let r = ctx.exunlockSync('fibostest123', '100.0000 ADC@nmslwsndhjyz', 1537960501, 'unlock 100.0000 ADC', {
    authorization: 'hujzwsndnmsl' //授权
})
console.notice(r);
```

异步:

```js
//初始化 fibos 客户端
...
ctx.exunlock('fibostest123', '100.0000 ADC@nmslwsndhjyz', 1537960501, 'unlock 100.0000 ADC', {
    authorization: 'hujzwsndnmsl' //授权
}).then(r=>{
    console.notice(r);
})
```

### ctxrecharge

合约子钱包充值操作

```js
ctx.ctxrecharge(owner, quantity, memo, {
    authorization: 'author_name'//授权
});
```

#### 方法和参数

* **owner:** string  账户拥有者
* **quantity:** number  充值通证数量
* **memo:** string  附言
* **authorization:** string  授权

#### 示例

同步充值:

```js
//初始化 fibos 客户端
...
let r = ctx.ctxrechargeSync('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxrecharge', {
			authorization: 'tteesstt1122'
})
console.notice(r);
```

异步充值:

```js
//初始化 fibos 客户端
...
ctx.ctxrecharge('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxrecharge', {
			authorization: 'tteesstt1122' //授权
}).then(r=>{
    console.notice(r);
})
```

### ctxextract

合约子钱包提现操作

```js
ctx.ctxextract(owner, quantity, memo, {
    authorization: 'author_name'//授权
});
```

#### 方法和操作

* **owner:** string  账户拥有者
* **quantity:** number  提现通证数量
* **memo:** string  附言
* **authorization:** string  授权
#### 示例

同步提现:

```js
//初始化 fibos 客户端
...
let r = ctx.ctxextractSync('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxextract', {
			authorization: 'tteesstt1122'//授权
})
console.notice(r);
```

异步提现:

```js
//初始化 fibos 客户端
...
ctx.ctxextract('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxextract', {
			authorization: 'tteesstt1122'  //授权
}).then(r=>{
    console.notice(r);
})
```

### ctxtransfer

合约子钱包转账

```js
ctx.ctxtransfer(from, to, quantity, memo, {		
authorization: 'author_name'//授权
});
```

#### 参数

* **from:** string  通证转出方
* **to:** string  通证转入方
* **quantity:** number  通证数量
* **memo:** string  附言
* **authorization:** string  授权

#### 示例

同步转账:

```js
//初始化 fibos 客户端
...
let r = ctx.ctxtransferSync('tteesstt1122', 'tteesstt2222', '50.0000 ADC@nmslwsndhjyz', 'ctxtransfer', {		
authorization: 'nmslwsndhjyz'  //授权	
});
console.notice(r);
```

异步转账:

```js
//初始化 fibos 客户端
...
ctx.ctxtransfer('tteesstt1122', 'tteesstt2222', '50.0000 ADC@nmslwsndhjyz', 'ctxtransfer', {		
authorization: 'nmslwsndhjyz'//授权
}).then(r=>{
    console.notice(r);
})
```


