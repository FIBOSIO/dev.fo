---
title: 
type: fibosjs
order: 1
---

# FIBOS.JS

​	FIBOS 是一个结合 FIBJS 以及 EOS 的 JavaScript 的运行平台，它使得 EOS 提供可编程性，并允许使用 JavaScript 编写智能合约。FIBOS 平台的出现让第三代 EOS 智能合约编程变得简单、快捷!

## ecc 模块

椭圆曲线加密函数,内置多个方法用来生成我们需要的秘钥.

### unsafeRandomKey()

生成不安全的测试私钥

```javascript
fibos.modules.ecc.unsafeRandomKeySync();
```

#### 返回值
* 同步: **String**
* 异步: **Promise**

PrivateKey  返回一个测试私钥

#### 示例
node.js/fibjs:

```js
var privateKey = fibos.modules.ecc.unsafeRandomKeySync();
console.log(privateKey);
/*
运行结果:
5HvSKet1FQBoGitZ7qoN7pWycC6MRF44zQVG7yNPMmGX3wzuSej
*/
```

browser:

```js
Fibos.modules.ecc.unsafeRandomKey().then(unsaferandomkey=>{
    console.log(unsagerandomkey);
})
/*
运行结果:
5Hqd2wRRUYc4zvDBkuQsWFGS9DjrLfgt4BP4wgtHLmiw2N5h1Ar
*/
```

### ecc.randomKey()

生成随机私钥

```
fibos.modules.ecc.randomKey();
```

#### 返回值

- 同步: **String**
- 异步: **Promise**

PrivateKey  返回一个随机私钥

#### 示例

node.js/fibjs:

```js
var randomKey=fibos.modules.ecc.randomKeySync();
console.log(randomKey);
/*
运行结果:
5Hx3XoKxrytPnJZxwpwAWz1ySf3dZFLqAsv92ZpTQf5fnSy6BEy
*/
```

browser:

```js
Fibos.modules.ecc.randomKey().then(randomKey=>{
    console.log(randomKey);
})
/*
运行结果:
5KSYGQW1BhpJnJFF1i5kkyDTvifeCQWZEcXF4if9FafJmAbHgRd
*/
```

### ecc.seedPrivate()

同一种子每次都产生相同的私钥,使用至少128个随机位来产生一个安全的私钥。

```javascript
ecc.seedPrivate(seed);
```

#### 参数

* **seed:** string   任意长度的字符串。

#### 返回值

- 同步: **String**
- 异步: **Promise**

PrivateKey   返回私钥

#### 示例
node.js/fibjs

```js
var seedPrivate=fibos.modules.ecc.seedPrivateSync('secret');
console.log(seedPrivate);
/*
运行结果:
5J9YKiVU3AWNkCa2zfQpj1f2NAeMQhLsYU51N8NM28J1bMnmrEQ
*/
```

browser:

```js
Fibos.modules.ecc.seedPrivate('secret').then(seedprivate=>{
    console.log(seedprivate);
})
/*
运行结果:
5J9YKiVU3AWNkCa2zfQpj1f2NAeMQhLsYU51N8NM28J1bMnmrEQ
*/
```

### ecc.privateToPublic()

通过私钥信息来计算公钥信息

```js
fibos.modules.ecc.privateToPublic(PrivateKey);
```

#### 参数
* **PrivateKey :**PrivateKey   私钥 
* **pubkey_prefix:** string  公钥前缀（可选，默认`'EOS'`）

#### 返回值

- 同步: **String**
- 异步: **Promise**

pubkey  返回公钥

#### 示例
node.js/fibjs:

```javascript
var                  privateToPublic=fibos.modules.ecc.privateToPublicSync("5J9YKiVU3AWNkCa2zfQpj1f2NAeMQhLsYU51N8NM28J1bMnmrEQ");
console.log(privateToPublic);
/*
运行结果:
FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx
*/
```

browser:

```js
Fibos.modules.ecc.privateToPublic("5J9YKiVU3AWNkCa2zfQpj1f2NAeMQhLsYU51N8NM28J1bMnmrEQ").then(privatetopublic={
    console.log(privatetopublic);
})
/*
运行结果:
FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx
*/
```

### ecc.isValidPublic()

判断公钥是否有效

```js
fibos.modules.ecc.isValidPublic(pubkey);
```

#### 参数
* **pubkey:** pubkey 公钥,如EOSKey
* **pubkey_prefix:** string 公钥前缀（可选，默认`'EOS'`）

#### 返回值
- 同步: **boolean**
- 异步: **Promise**

true/false  判断公钥是否有效

#### 示例
node.js/fibjs:

```js
var isValidPublic =fibos.modules.ecc.isValidPublicSync("FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx"); 
console.log(isValidPublic);
/*
运行结果:true
*/
```

browser:

```javascript
Fibos.modules.ecc.isValidPublic("FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx").then(isvalidpublic=>{
    console.log(isvalidpublic);
})
/*
运行结果:true
*/
```

### ecc.isValidPrivate()

判断私钥是否有效

```js
fibos.modules.ecc.isValidPrivate(wif);
```

#### 参数
**wif:** PrivateKey 私钥

#### 返回值

- 同步: **boolean**
- 异步: **Promise**

**true/false:**  判断是否有效

#### 示例
node.js/fibjs:

```js
var isValidPrivate=fibos.modules.ecc.isValidPrivateSync('5Hx3XoKxrytPnJZxwpwAWz1ySf3dZFLqAsv92ZpTQf5fnSy6BEy');
console.log(isValidPrivate);
/*
运行结果:true
*/
```

browser:

```js
Fibos.modules.ecc.isValidPrivate('5Hx3XoKxrytPnJZxwpwAWz1ySf3dZFLqAsv92ZpTQf5fnSy6BEy').then(isvalidprivate=>{
    console.log(isvalidprivate);
})
/*
运行结果:true
*/
```

### ecc.sign()

使用data信息或hash来创建签名

```js
fibos.modules.ecc.sign(data,PrivateKey);
```

#### 参数
* **data:** 字符串  缓冲区

* **PrivateKey:** PrivateKey  私钥

* **encoding: ** string  数据编码（可选，默认`'utf8'`）

#### 返回值

* 同步: **boolean**
* 异步: **Promise**

**sign:** 字符串签名

#### 示例
node.js/fibjs:

```js
var sign = fibos.modules.ecc.signSync('I am OK','5Hx3XoKxrytPnJZxwpwAWz1ySf3dZFLqAsv92ZpTQf5fnSy6BEy');
console.log(sign);
/*
运行结果:
SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

browser:

```js
Fibos.modules.ecc.sign('I am OK','5Hx3XoKxrytPnJZxwpwAWz1ySf3dZFLqAsv92ZpTQf5fnSy6BEy').then(sign=>{
    console.log(sign);
})
/*
运行结果:
SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```


###ecc.signHash()
使用进行hash加密的data信息和私钥来创建签名

```js
fibos.modules.ecc.signHash(dataSha256,PrivateKe);
```

#### 参数
* **dataSha256:** string | buffer  sha256 hash 32字节缓冲区或字符串
* **privateKey:** PrivateKey  私钥
* **encoding:** string dataSha256编码（如果是字符串）（可选，默认`'hex'`）

#### 返回值

- 同步: **string**
- 异步: **Promise**

**signHash:** 带有hash加密的字符串签名

#### 示例
node.js/fibjs:

```js
var signHash = fibos.modules.ecc.signHashSync('8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab','5Hx3XoKxrytPnJZxwpwAWz1ySf3dZFLqAsv92ZpTQf5fnSy6BEy');
console.log(signHash);
/*
运行结果:
SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

browser:
```js
Fibos.modules.ecc.signHash('8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab','5Hx3XoKxrytPnJZxwpwAWz1ySf3dZFLqAsv92ZpTQf5fnSy6BEy').then(signhash=>{
    console.log(signhash);
}))
/*
运行结果:SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8
*/
```

### ecc.verify()

验证签名数据

```js
fibos.modules.ecc.verify(signature,data,pubkey);
```

#### 参数
* **signature:** string | buffer  缓冲区或十六进制字符串
* **data:** string | buffer  字符串数据
* **pubkey:** pubkey | PublicKey 公钥

#### 返回值

- 同步: **boolean**
- 异步: **Promise**

**true/false:**  判断签名数据是否成立

#### 示例
node.js/fibjs:

```js
var pubkey="FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx";
var signature="SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8";
var sha256="8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab";
var verify = fibos.modules.ecc.verifySync(signature, 'I am alive', pubkey);
console.log(verify);
/*
运行结果:false
*/
```

browser:

```js
var pubkey="FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx";
var signature="SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8";
Fibos.modules.ecc.verify(signature, 'I am alive', pubkey).then(verify=>{
    console.log(verify);
})
/*
运行结果:false
*/
```

### ecc.verifyHash()

验证签名数据hash

```js
fibos.modules.ecc.verifyHash(signature, hashData, pubkey);
```

#### 参数
* **signature:** string | buffer  缓冲区或十六进制字符串
* **hashData:**  boolean|sha256  哈希数据（可选，默认`true`）
* **pubkey:** pubkey | PublicKey 公钥
* **encoding:** string encoding（可选，默认`'utf8'`）

#### 返回值

- 同步: **boolean**
- 异步: **Promise**

**true/false:** 判断是否成立

#### 示例
node.js/fibjs:

```js
var pubkey="FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx";
var signature="SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8";
var sha256="8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab";
fibos.modules.ecc.verifyHash(signature, sha256, pubkey);
/*
运行结果:false
*/
```

browser:

```js
var pubkey="FO83msFTj6yv5U91KkiRxHcDZUXJkR6xwC9EjbqqwFqhFa1nxMYx";
var signature="SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8";
var sha256="8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab";
Fibos.modules.ecc.verifyHash(signature, sha256, pubkey).then(verifyhash=>{
    console.log(verifyhash);
})
/*
运行结果:false
*/
```

### ecc.recover()

恢复用于创建签名的公钥

```js
fibos.modules.ecc.recover(signature, data);
```

#### 参数

* **signature:** string | buffer（EOSbase58sig ..，Hex，Buffer）
* **data:** string | buffer 完整数据
* **encoding:** string  数据编码（如果数据是字符串）（可选，默认`'utf8'`）

#### 返回值

- 同步: **string**
- 异步: **Promise**

**pubkey:**  公钥

#### 示例
node.js/fibjs:

```js
signature="SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8";
var recover = fibos.modules.ecc.recoverSync(signature, 'I am alive');
console.log(recover);
/*
运行结果:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/
```

browser:

```js
signature="SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8";
fibos.modules.ecc.recover(signature, 'I am alive').then(recover=>{
    console.log(recover);
})
/*
运行结果:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/
```

### ecc.recoverHash()

恢复用于创建hash签名的公钥

```js
fibos.modules.ecc.recoverHash(signature,dataSha256);
```

#### 参数
* **signature: ** string | buffer（EOSbase58sig ..，Hex，Buffer）
* **dataSha256:** string | buffer  sha256散列32字节缓冲区或十六进制字符串
* **encoding:** string |dataSha256编码（如果dataSha256是字符串）（可选，默认`'hex'`）

#### 返回值

- 同步: **string**
- 异步: **Promise**

**pubkey:**  公钥

#### 示例
node.js/fibjs:

```js
signature="SIG_K1_KBZepHvGX8Vuxycd6LhP3NmEztJ3VBnQh42XQgLjH1LGacVzs8jgyoSegTgDPc7SXUXNcHKNACy4Y2c5gpVBntdzQHeSR8";
dataSha256='8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab'
var recoverHash = fibos.modules.ecc.recoverHash(signature,dataSha256 );
console.log(recoverHash);
/*
运行结果:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/
```

browser:

```js
Fibos.modules.ecc.recoverHash(signature, '8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab').then(recover_hash => {
      console.log(recover_hash);
}
/*
运行结果:
FO4zLK8u81GnVQXZRc1GdoR1PKdLpFmfb9yjA6HcPrMo89j4Bimn
*/                                                                                                              
```

### ecc.sha256()

sha256加密

```js
fibos.modules.ecc.sha256(data);
```

#### 参数
* **data:** string | buffer 二进制数据,需要Buffer.from（data，'hex'）
* **resultEncoding:** string （可选，默认`'hex'`）
* **encoding: ** string  结果编码成'hex'，'binary'或'base64'（可选，默认`'hex'`）

#### 返回值

- 同步: **string | buffer**
- 异步: **Promise**

**sha256:**使用hash.sha256加密后的数据

#### 示例
node.js/fibjs:

```js
var sha256 = fibos.modules.ecc.sha256('I am alive');
console.log(sha256);
/*
运行结果:
8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab
*/
```

browser:

```js
Fibos.modules.ecc.sha256('I am alive').then(recover_hash => {
      console.log(recover_hash);
}
/*
运行结果:
8a72914b5c615a7d1f23298c7efa9d404d69f79e580de122cf0685bc0e9b45ab
*/                                          
```



## BLOCKCHAIN支持

> 在区块链中对用户账户信息操作的各种方法

### API的配置

```js
var FIBOS = require('fibos.js');
var fibos = FIBOS({
	chainId: "68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a",
	keyProvider: "",
	httpEndpoint: "http://testnet.fibos.fo",
	logger: {
		log: null,
		error: null
	}
});
```

### getBlockSync

获取块信息

```j&#39;s
fibos.getBlockSync(block_number);
```

#### 参数

* **block_number:** int  块的高度

#### 示例


```js
var getBlock = fibos.getBlockSync(1);
console.log(getBlock);
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

### 2.getInfoSync

获取区块信息

```js
fibos.getInfoSync();
```

#### 示例

```js
var getInfo = fibos.getInfoSync();
console.log(getInfo);
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

* **server_version:** text服务端版本
* **chain_id:**string 区块链的链地址
* **head_block_num: **number 当前区块高度
* **last_irreversible_block_num: **number 不可逆区块高度
* **last_irreversible_block_i: **string 不可逆区块地址
* **head_block_id: **string 当前区块地址
* **head_block_time: **date 当前区块时间
* **head_block_producer: **string 当前区块进程
* **virtual_block_cpu_limit: **number 虚拟区块cpu限制
* **virtual_block_net_limit: **number 虚拟区块网络限制
* **block_cpu_limit: **number 区块cpu限制
* **block_net_limit: **number 区块网络限制
* **server_version_string: **string 服务端版本字符表示


### 3.newaccountSync

创建一个新的FIBOS账户

#### 参数

* **creator:** string 创建者的账户名
* **name:** string  被创建者的账户名
* **owner:** string 被创建者账户 owner 权限公钥
* **active:** string 被创建者 active 权限公钥  

#### 示例

```js
fibos.newaccountSync({
    creator: 'eosio',
    name: "hellomongodb",
    owner: config["FO76RtZors7WA7y5TyZtGGgnXz18vzUj2TbBsLBepthfENSF6tm1"],
    active: config["FO76RtZors7WA7y5TyZtGGgnXz18vzUj2TbBsLBepthfENSF6tm1"]
});
```

### buyrambytes

创建者调用该方法为被创建者购买内存来存放新账户的信息

#### 参数

* **payer:**string  创建者的账户名

* **receiver:** string 被创建者的账户名

* **bytes:** number 消耗的内存大小(字节)

#### 示例

```js
fibos.buyrambytes({
    payer: 'creator_account',
    receiver: 'your_account',
    bytes: 4096
  });
```
### 5.delegatebw

> 抵押代币获取 cpu 和带宽资源

#### 参数

* **from:**string 创建者的账户名

* **receiver:** string 被创建者的账户名

* **stake_net_quantity:** string 创建者为被创建者抵押FO获取NET

* **stake_cpu_quantity:**string 创建者为被创建者抵押FO获取CPU

* **transfer:**number 通常用1 代表替别人抵押 FO 获取资源,如果你想要自己获取资源需要将其改为0

#### 示例

```js
  fibos.delegatebw({
    from: 'creator_account',
    receiver: 'your_account',
    stake_net_quantity: '0.1000 FO',
    stake_cpu_quantity: '0.1000 FO',
    transfer: 1
  });
```

### getAccountSync

获取账户信息

```js
fibos.getAccountSync(accountName);
```

#### 参数

- **accountName:** string  需要获取的账户名

#### 示例

```js
var getAccount = fibos.getAccountSync("hellomongodb");
console.log(getAccount);
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



## Token contract api

在FIBOS中有两种通证：经典通证和智能通证

###  create token

创建通证

#### 接口

```js
excreateSync(issuer, maximum_supply,  connector_weight, maximum_exchange,reserve_supply, reserve_connector_balance, {
    authorization: issuer
});
```

#### 参数解释

* **issuer:** string 通证发行者                                             
* **maximum_supply:** number 最大可发行通证数量                               
* **connector_weight:** string 连接器权重（值为0时表示为普通通证，0-1之间为智能通证） 
* **maximum_exchange:** string最大可兑换(流通)的通证数量                         
* **reserve_supply:** string 未流通通证数量                                     
* **reserve_connector_balance:** string 未流通通证保证金数量                                   
#### 实例


```js
//初始化 fibos 客户端
...
let name = "fibostest123";
let ctx = fibos.contractSync("eosio.token");
let r = ctx.excreateSync(name, "100000000000.0000 AAA",  0.15,'10000000000.0000 AAA', '3000000000.0000 AAA', '90000.0000 FO', {
    authorization: name
});
console.log(r);excreateSync(issuer, maximum_supply,  connector_weight, maximum_exchange,reserve_supply, reserve_connector_balance, {
    authorization: issuer
});
```

### issue token

增发通证

#### 接口

```js
exissueSync(to, quality, memo, {
				authorization: issuer
			})
```

#### 参数解释

* **to:**  string 增发通证接收账号 
* **quality:** string 数量           
* **memo: ** text 附言             
* **authorization:** string 发行方           

#### 实例

```js
//初始化 fibos 客户端
...
let name = "fibostest123";
let ctx = fibos.contractSync("eosio.token");
let r = ctx.exissueSync(name, "1000000.0000 ABC", "issue to fibostest123",{
				authorization: name
			})
console.log(r);
```

### retire token

撤销通证

#### 接口

```js
exretireSync(from, quantity, memo, {
				authorization: from
			});
```

#### 参数解释
* **from:** string 销毁通证接收账号 
* **quality:** string 数量             
* **memo:** string 附言             
* **authorization:** string 销毁通证账号权限 

#### 实例

```js
//初始化 fibos 客户端
...
let name = "fibostest123";
let ctx = fibos.contractSync("eosio.token");
let r = ctx.exretireSync(name, "1000000.0000 ABC", "retire token", {
				authorization: name
			})
console.log(r);
```

### close token

关闭通证

#### 接口

```js
exissueSync(owner, symbol, {
				authorization: owner
			})
```

#### 参数解释
* **owner:** string 通证持有者账号     
* **symbol :** string 通证代号           
* **authorization:** string 通证持有者账号权限 

#### 实例

```javascript
//初始化 fibos 客户端
...
let owner = "fibostest123";
let ctx = fibos.contractSync("eosio.token");
let r = ctx.exissueSync(owner,"0.0000 ABC", {
				authorization: owner
			})
console.log(r);
```

### destory token

销毁通证

#### 接口

```js
exdestroySync(symbol, {
				authorization: issuer
			})
```

#### 参数解释
* **symbol:** string 通证符号       
* **authorization: **string  通证发行者权限 

#### 实例

```js
//初始化 fibos 客户端
...
let issuer = "fibostest123";
let ctx = fibos.contractSync("eosio.token");
let r = ctx.exdestroySync("0.0000 ABC", {
				authorization: issuer
			})
console.log(r);
```



# Token合约

### transferSync

配置好EOS MainNet 和 EOS RPC 地址 和 EOS 私钥后,便初始化了一个 eos 客户端,通过调用 `transferSync` 方法,实现转账操作

#### 参数

* **eosaccount:** string  转出方                  
* **fiboscouncil:** string 转入方                  
* **value:** string 数量 1.0000 EOS         
* **memo:** string 填入已注册的 FIBOS 账号 

####  示例

```js
let eosaccount = '' // 你的 EOS 账户名
let value = '1.0000 EOS'; //转账给 fiboscouncil 账户的数量
let ctx = eos_client.contractSync('eosio.token');
let memo = 'fibostest123'; //填入已注册的 FIBOS 账号
let result = ctx.transferSync(eosaccount, 'fiboscouncil', value, memo, {
    authorization: eosaccount
});
console.log(result);
```

### getTableRowsSync

查询账户资产信息

#### 参数

* **decode:** boolean 明文展示,解码

* **name:** string FIBOS账户名
* **token_name:**string 合约名
* **accounts:** string 表名

#### 示例
```js
var rs = fibos_client.getTableRowsSync(true, 'eosio.token', '你的 FIBOS 账户名', 'accounts');
console.log(rs);
/*
结果:
{
  "rows": [
    {
      "primary": 0,
      "balance": {
        "quantity": "0.0000 EOS",
        "contract": "eosio"
      }
    },
    {
      "primary": 1,
      "balance": {
        "quantity": "34999.2035 FO",
        "contract": "eosio"
      }
    },
    {
      "primary": 2,
      "balance": {
        "quantity": "0.0000 FWT",
        "contract": "silver123451"
      }
    },
    {
      "primary": 3,
      "balance": {
        "quantity": "129077.8283 AF",
        "contract": "fibosafchain"
      }
    }
  ],
  "more": false
}
*/
```

### exchangeSync

在 FIBOS 使用 Bancor 进行通证之间兑换

#### 参数

* **owner:** string 兑换账号名         
* **quantity:**number 兑换通证数量     
* **tosymbol:** string 兑换通证目标类型 
* **memo:** string 兑换备注信息     

#### 示例

```javascript
let ctx = fibos_client.contractSync('eosio.token');
let owner = '你的 FIBOS 账户名';
let eos2fo_quantity = '10.0000 EOS@eosio';
let memo = 'exchange EOS to FO';

var result = ctx.exchangeSync(owner, eos2fo_quantity, `0.0000 FO@eosio`, memo, {
    authorization: owner
});
console.log(result);
```

### excreateSync

调用 token 合约中的 `excreate` 接口来进行通证的发行

#### 方法参数

* **account_name:** issuer  通证发行账号
* **asset:** maximum_supply  最大可发行通证数量
* **double:** connector_weight  连接器权重
* **asset:** maximum_exchange  最大可兑换(流通)的通证数量
* **asset:** reserve_supply  未流通通证数量
* **asset:** reserve_connector_balance  未流通通证保证金数量
* **time_point_sec:** expiration  项目方预设的项目锁仓期

#### 示例
发行普通通证

```javascript
//初始化 fibos 客户端
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.excreateSync(name, '90000000000.0000 DDD', 0, '10000000000.0000 DDD', '3000000000.0000 DDD', '90000.0000 FO', '2018-10-29T18:54:00', {
  authorization: name
}); //expiration需大于等于当前时间
console.log(r)
```

发行智能通证

```javascript
//初始化 fibos 客户端
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.excreateSync(name, '100000000000.0000 AAA',  0.15,'10000000000.0000 AAA', '3000000000.0000 AAA', '90000.0000 FO', '2018-10-29T18:54:00', {
    authorization: name
});  //expiration需大于等于当前时间
console.log(r);
```

### exissueSync

增发普通通证

#### 参数

* **account_name:** issuer  通证发行账号
* **asset:** maximum_supply  最大可发行通证数量
* **double:** connector_weight  连接器权重
* **asset:** maximum_exchange  最大可兑换(流通)的通证数量
* **asset:** reserve_supply  未流通通证数量
* **asset:** reserve_connector_balance  未流通通证保证金数量
* **time_point_sec:** expiration  项目方预设的项目锁仓期
#### 示例

```javascript
//初始化 fibos 客户端
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exissueSync(name, '1000000.0000 ABC@fibostest123', 'issue to fibostest123', {
  authorization: name
});
console.log(r);
```

### exdestroySync

销毁通证(只有流通量为0才能进行销毁)

#### 参数

- **authorization:**  string  通证账号
- **asset: **string  通证兑换流通量

#### 示例

```js
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exdestroySync(`0.0000 AAA@fibostest123`, {authorization: 'fibostest123'});
```

### exlocktransSync

锁仓(项目方发行智能通证时，填写的 reserve_supply 这个参数的值，锁仓量会随着销毁和解锁通证的操作而变化。)

#### 方法参数

* **account_name:** from  通证转出方
* **account_name:** to  通证转入方
* **extended_asset:** quantity 通证数量
* **time_point_sec:** expiration 待转出锁仓时间
* **time_point_sec:**  expiration_to  待转入锁仓时间
* **string:** memo 附言

#### 示例

```js
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exlocktransSync('nmslwsndhjyz', 'fibostest123', `10000.0000 BBB@5hzuyqumr3l5`, '2018-10-29T18:54:00', '2018-10-29T18:54:00', `transfer 1000  ABC@uepgdzfhucin`, {
    authorization: 'nmslwsndhjyz'
}); //expiration_to必须大于等于expiration
console.notice(r)
```

### exunlockSync

解锁(用户通过解锁操作来讲锁仓中的通证变为流通中的通证)

#### 方法和参数

* **account_name:** owner 通证持有者
* **extended_asset:** quantity 解锁数量
* **time_point_sec:** expiration 锁仓期
* **string:** memo 附言

#### 示例

```js
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exunlockSync('fibostest123', '100.0000 ADC@nmslwsndhjyz', 1537960501, 'unlock 100.0000 ADC', {
    authorization: 'hujzwsndnmsl'
})
console.notice(r);
```

### ctxrechargeSync

合约自钱包充值操作

#### 方法和参数

* **account_name:** owner  账户拥有者
* **extended_asset:** quantity  充值通证数量
* **string:** memo 附言

#### 示例
```js
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.ctxrechargeSync('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxrecharge', {
			authorization: 'tteesstt1122'
		})
console.notice(r);
```

### ctxextractSync

合约子钱包提现操作

#### 方法和操作

* **account_name:** owner  账户拥有者
* **extended_asset:** quantity  提现通证数量
* **string:** memo  附言
#### 示例
```js
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.ctxextractSync('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxextract', {
			authorization: 'tteesstt1122'
		})
console.notice(r);
```

### ctxtransfeSync

合约子钱包转账

#### 方法和操作

* **account_name:** from  通证转出方
* **account_name:** to  通证转入方
* **extended_asset:** quantity  通证数量
* **string:** memo  附言

#### 示例

```js
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.ctxtransferSync('tteesstt1122', 'tteesstt2222', '50.0000 ADC@nmslwsndhjyz', 'ctxtransfer', {		
authorization: 'nmslwsndhjyz'	
})
```