---
title: 
type: token
language: zh-cn
order: 1
---

# Token Contract

## transfer

转账 —— 只有发行方为 eosio 的通证可以调用（FIBOS主网目前只有 EOS 和 FO）

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **from**     | string | 通证转出方  |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

####  示例

fibos.js 环境下：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.transferSync('fibforjeremy', 'fiboscouncil', '20.3375 EOS', 'eosforjeremy', {
  authorization: '私钥对应的账号'
});
console.log(r);

```

浏览器环境下：

```javascript

const FIBOS = require('fibos.js');
<<<<<<< HEAD
require('ssl').loadRootCerts();

const client = FIBOS({
=======

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.issue({
      to: "eosio",
      quantity: "34341.6961 FO",
      memo: "issue tokens for producer pay and savings"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.transfer({
      from: 'fibforjeremy',
      to: 'fiboscouncil',
      quantity: '20.3375 EOS',
      memo: 'eosforjeremy'
    },{
        authorization: '私钥对应的账号'
    })
})
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



<<<<<<< HEAD
## retire
=======
## extransfer

转账
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
<<<<<<< HEAD
| **quantity** | string | asset       |
| **memo**     | string | 备注        |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
| **from**     | string | 通证转出方  |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.retire({
      quantity: 'asset',
      memo: 'string'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## create

#### 参数

| name               | type   | description  |
| ------------------ | ------ | ------------ |
| **issuer**         | string | 发行人       |
| **maximum_supply** | string | 最大发行数量 |

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.extransferSync('dicefobetone', 'zhangjingrui', '10.0000 FO@eosio', 'trasnfer to zhangjingrui', {
  authorization: '私钥对应的账号'
});
console.log(r);
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.create({
      issuer: "eosio",
      maximum_supply: "10000000000.0000 EOS"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.extransfer({
      from: 'dicefobetone',
      to: 'zhangjingrui',
      quantity: '10.0000 FO@eosio',
      memo: 'trasnfer to zhangjingrui'
    },{
        authorization: '私钥对应的账号'
    })
})
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



<<<<<<< HEAD
## close

#### 参数

| name       | type   | description  |
| ---------- | ------ | ------------ |
| **owner**  | string | account_name |
| **symbol** | json   | symbol       |

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
## exissue

增发通证 —— 普通通证支持增发，社区智能通证暂不支持

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

#### 示例

fibos.js 环境下：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.close({
      owner: 'account_name',
      symbol: 'symbol'
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## extransfer

#### 参数

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **from**     | string | 转出方         |
| **to**       | string | 转入方         |
| **quantity** | json   | extended_asset |
| **memo**     | string | 备注           |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.exissueSync('dogfallchina', '10.0000 TAO@dogfallchina', 'issue to dogfallchina', {
  authorization: '私钥对应的账号'
});
console.log(r);
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.extransfer({
      from: "dicefobetone",
      to: "zhangjingrui",
      quantity: {"quantity":"1.5076 FO","contract":"eosio"},
      memo: "4<66 你中奖啦！"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.exissue({
      to: 'dogfallchina',
      quantity: '10.0000 TAO@dogfallchina',
      memo: 'issue to fibostest123'
    },{
        authorization: '私钥对应的账号'
    })
})
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



<<<<<<< HEAD
## exissue

#### 参数

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **to**       | string | 转入方         |
| **quantity** | json   | extended_asset |
| **memo**     | string | 备注           |

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();
=======
## exretire

销毁账户持有的流通通证

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **from**     | string | 通证转出方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.exretireSync('createtest11', '10.0000 FO@eosio', 'retire tokens', {
  authorization: '私钥对应的账号'
});
console.log(r);
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exissue({
      to: "dogfallchina",
      quantity: {"quantity":"100000.0000 TAO","contract":"dogfallchina"},
      memo: ""
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
client.contract('eosio.token').then((contract)=>{
    contract.exretire({
      from: 'createtest11',
      quantity: '10.0000 FO@eosio',
      memo: 'retire tokens'
    },{
        authorization: '私钥对应的账号'
    })
})
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



<<<<<<< HEAD
## exretire

#### 参数

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **from**     | string | 转出方         |
| **quantity** | json   | extended_asset |
| **memo**     | string | 备注           |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
## exshare

向社区中通证持有者进行分红

#### 参数

| name         | type   | description        |
| ------------ | ------ | ------------------ |
| **quantity** | string | 填入保证金的数量   |
| **tosym**    | string | 参与分红的智能通证 |
| **memo**     | string | 附言               |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos.contractSync('eosio.token');
let r = ctx.exshareSync('10000.0000 FO@eosio', '0.0000 AAA@fibostest321', 'share 10000.0000 FO to token holders',{
    authorization: '私钥对应的账号'
}); 
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exretire({
      from: "createtest11",
      quantity: {"quantity":"0.0067 FO","contract":"eosio"},
      memo: "issue tokens for producer pay and savings"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.exshare({
      quantity: '10000.0000 FO@eosio',
      tosym: '0.0000 AAA@fibostest321' 
      memo: 'share 10000.0000 FO to token holders'
    },{
        authorization: '私钥对应的账号'
    })
});
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



## excreate

<<<<<<< HEAD
#### 参数

| name                          | type      | description    |
| ----------------------------- | --------- | -------------- |
| **issuer**                    | string    | account_name   |
| **maximum_supply**            | string    |                |
| **connector_weight**          | float64   |                |
| **maximum_exchange**          | string    |                |
| **reserve_supply**            | string    |                |
| **reserve_connector_balance** | string    |                |
| **expiration**                | date-time | time_point_sec |

#### 示例

```javascript
const client = FIBOS({
=======
发行通证

#### 参数

| name                          | type      | description                |
| ----------------------------- | --------- | -------------------------- |
| **issuer**                    | string    | 通证发行账号               |
| **maximum_supply**            | string    | 最大可发行通证数量         |
| **connector_weight**          | float64   | 连接器权重                 |
| **maximum_exchange**          | string    | 最大可兑换(流通)的通证数量 |
| **reserve_supply**            | string    | 锁仓通证数量               |
| **reserve_connector_balance** | string    | 锁仓通证保证金数量         |
| **expiration**                | date-time | 项目方预设的项目锁仓期     |
| **buy_fee**                   | double    | 项目方预设通证兑入手续费   |
| **sell_fee**                  | double    | 项目方预设通证兑出手续费   |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.excreate({
      issuer: "dogfallchina",
      maximum_supply: "100000.0000 TAO",
      connector_weight: "0.00000000000000000",
      maximum_exchange: "0.0000 TAO",
      reserve_supply: "0.0000 TAO",
      reserve_connector_balance: "0.0000 FO",
      expiration: "2018-11-25T07:47:39"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.excreateSync('dogfallchina', '90000000000.0000 DDD', 0, '10000000000.0000 DDD', '3000000000.0000 DDD', '90000.0000 FO', '2018-10-29T18:54:00', 0,0,{ //手续费自定义,大于0小于等于1 
  authorization: '私钥对应的账号'  //授权
}); //expiration 需大于等于当前时间
console.log(r)
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.excreate({
      issuer: 'dogfallchina',
      maximum_supply: '90000000000.0000 DDD',
      connector_weight: 0,
      maximum_exchange: '10000000000.0000 DDD',
      reserve_supply: '3000000000.0000 DDD',
      reserve_connector_balance: '90000.0000 FO',
      expiration: '2018-10-29T18:54:00',
      buy_fee: 0,
      sell_fee: 0
    },{
        authorization: '私钥对应的账号'
    })
})
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



## exclose

<<<<<<< HEAD
#### 参数

| name       | type   | description     |
| ---------- | ------ | --------------- |
| **owner**  | string | account_name    |
| **symbol** | json   | extended_symbol |

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
删除账户中通证的条目

#### 参数

| name       | type   | description  |
| ---------- | ------ | ------------ |
| **owner**  | string | 通证拥有者   |
| **symbol** | string | 通证目标类型 |

#### 示例

fibos.js 环境下：

```javascript

const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});


let ctx = client.contractSync('eosio.token');

let r = ctx.excloseSync('dreamheartlx', '4,ZC@lixunlixunli', { //4表示通证的精度，ZC表示通证名称，lixunlixunli表示通证的发行人
  authorization: '私钥对应的账号'
}); 
console.log(r)
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exclose({
      owner: "dreamheartlx",
      symbol: {"sym":"4,ZC","contract":"lixunlixunli"}
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.exclose({
      owner: 'dreamheartlx',
      symbol: '4,ZC@lixunlixunli'
    },{
        authorization: '私钥对应的账号'
    })
});
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



## exdestroy

<<<<<<< HEAD
#### 参数

| name       | type | description     |
| ---------- | ---- | --------------- |
| **symbol** | json | extended_symbol |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
永久删除通证

#### 参数

| name       | type   | description  |
| ---------- | ------ | ------------ |
| **symbol** | string | 通证目标类型 |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.exdestroySync('8,QE@dreamheartlx', {
  authorization: '私钥对应的账号'
}); 
console.log(r)
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exdestroy({
      symbol: {"sym":"8,QE","contract":"dreamheartlx"}
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```


=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.exdestroy({
      symbol: '8,QE@dreamheartlx'
    },{
        authorization: '私钥对应的账号'
    })
});
```

备注：销毁通证需要**流通量为0**的时候才可以销毁，也就是说通证发行方需要收回市场上所有流通的通证后才能销毁通证。
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966

## exchange

通证兑换

#### 参数

<<<<<<< HEAD
| name         | type   | description     |
| ------------ | ------ | --------------- |
| **owner**    | string | account_name    |
| **quantity** | json   | extended_asset  |
| **tosym**    | json   | extended_symbol |
| **memo**     | string | 备注            |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exchange({
      owner: "dicefobetone",
      quantity: {"quantity":"0.0130 FO","contract":"eosio"},
      tosym: {"sym":"4,BET","contract":"dicefobetone"},
      memo: "看到没？我回购了，BET兑FO价格又上涨一点点，你丫手里BET又值钱一点点"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
| name         | type   | description      |
| ------------ | ------ | ---------------- |
| **owner**    | string | 兑换账号         |
| **quantity** | string | 兑换通证数量     |
| **tosym**    | string | 兑换通证目标类型 |
| **memo**     | string | 兑换备注信息     |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.exchangeSync('dicefobetone', '0.0130 EOS@eosio', '0.0000 FO@eosio', 'exchange FO to EOS', {
    authorization: '私钥对应的账号'
});
console.log(r)
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

fibos_client.contract('eosio.token').then((contract)=>{
    contract.exchange({
      owner: 'dicefobetone',
      quantity: '0.0130 EOS@eosio',
      tosym: '0.0000 FO@eosio',
      memo: 'exchange FO to EOS'
    },{
        authorization: '私钥对应的账号'
    })
});
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



## ctxrecharge

<<<<<<< HEAD
#### 参数

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **owner**    | string | account_name   |
| **quantity** | json   | extended_asset |
| **memo**     | string | /              |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
合约子钱包 — 充值

#### 参数

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **owner**    | string | 账户拥有者   |
| **quantity** | string | 充值通证数量 |
| **memo**     | string | 附言         |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.ctxrechargeSync('dreamheartlx', '100.0000 QQQ@dreamheartlx','ctxrecharge', {
    authorization: '私钥对应的账号'
});
console.log(r)
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.ctxrecharge({
      owner: "dreamheartlx",
      quantity: {"quantity":"0.10000000 QQQ","contract":"dreamheartlx"},
      memo: ""
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.ctxrecharge({
      owner: 'dreamheartlx',
      quantity: '100.0000 QQQ@dreamheartlx',
      memo: 'ctxrecharge'
    },{
        authorization: '私钥对应的账号'
    })
});
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



## ctxextract

<<<<<<< HEAD
#### 参数

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **owner**    | string | account_name   |
| **quantity** | json   | extended_asset |
| **memo**     | string | /              |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
合约子钱包 — 提现

#### 参数

| name         | type   | description  |
| ------------ | ------ | ------------ |
| **owner**    | string | 账户拥有者   |
| **quantity** | string | 提现通证数量 |
| **memo**     | string | 附言         |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.ctxextractSync('lixunlixunli', '0.000100 LIU@lixunlixunli','ctxextract', {
    authorization: '私钥对应的账号'
});
console.log(r)
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.ctxextract({
      owner: "lixunlixunli",
      quantity: {"quantity":"0.000100 LIU","contract":"lixunlixunli"},
      memo: ""
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.ctxextract({
      owner: 'lixunlixunli',
      quantity: '0.000100 LIU@lixunlixunli',
      memo: 'ctxextract'
    },{
        authorization: '私钥对应的账号'
    })
});
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



## ctxtransfer

<<<<<<< HEAD
#### 参数

| name         | type   | description    |
| ------------ | ------ | -------------- |
| **from**     | string | account_name   |
| **to**       | string | account_name   |
| **quantity** | json   | extended_asset |
| **memo**     | string | /              |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
合约子钱包 — 转账

#### 参数

| name         | type   | description |
| ------------ | ------ | ----------- |
| **from**     | string | 通证转出方  |
| **to**       | string | 通证转入方  |
| **quantity** | string | 通证数量    |
| **memo**     | string | 附言        |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

let ctx = fibos_client.contractSync('eosio.token');

var r = ctx.ctxtransferSync('lixunlixunli','dreamheartlx','1.0000 ZX@lixunlixunli','ctxtransfer', {
    authorization: '私钥对应的账号'
});
console.log(r)
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.ctxtransfer({
      from: "lixunlixunli",
      to: "dreamheartlx",
      quantity: {"quantity":"1.0000 ZX","contract":"lixunlixunli"},
      memo: "ctxtransfer"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.ctxtransfer({
      from: 'lixunlixunli',
      to: 'dreamheartlx',
      quantity: '1.0000 ZX@lixunlixunli',
      memo: 'ctxtransfer'
    },{
        authorization: '私钥对应的账号'
    })
});
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



## exunlock

<<<<<<< HEAD
#### 参数

| name           | type      | description    |
| -------------- | --------- | -------------- |
| **owner**      | string    | account_name   |
| **quantity**   | json      | extended_asset |
| **expiration** | date-time | time_point_sec |
| **memo**       | string    | /              |

#### 示例

=======
解锁

#### 参数

| name           | type      | description      |
| -------------- | --------- | ---------------- |
| **owner**      | string    | 通证持有者       |
| **quantity**   | string    | 解锁数量         |
| **expiration** | date-time | 待解锁通证锁仓期 |
| **memo**       | string    | 附言             |

#### 示例

fibos.js 环境下：

>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

<<<<<<< HEAD
const client = FIBOS({
=======
const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: 'http://ca-rpc.fibos.io:8870',
});

let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.exunlockSync('fibostest123', '100.0000 ADC@nmslwsndhjyz', '2018-11-25T01:00:00', 'unlock 100.0000 ADC', {
    authorization: '私钥对应的账号'
})
console.log(r);
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exunlock({
      owner: "liyuchen1234",
      quantity: {"quantity":"0.5911 BET","contract":"dicefobetone"},
      expiration: "2018-11-25T01:00:00",
      memo: ""
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.exunlock({
      owner: 'fibostest123',
      quantity: '100.0000 ADC@nmslwsndhjyz',
      expiration: '2018-11-25T01:00:00',
      memo: 'unlock 100.0000 ADC'
    },{
        authorization: '私钥对应的账号'
    })
});
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



## exlocktrans

锁仓转账

#### 参数

| name              | type      | description    |
| ----------------- | --------- | -------------- |
<<<<<<< HEAD
| **from**          | string    | account_name   |
| **to**            | string    | account_name   |
| **quantity**      | json      | extended_asset |
| **expiration**    | date-time | time_point_sec |
| **expiration_to** | date-time | time_point_sec |
| **memo**          | string    | /              |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
| **from**          | string    | 锁仓通证转出方 |
| **to**            | string    | 锁仓通证转入方 |
| **quantity**      | string    | 通证数量       |
| **expiration**    | date-time | 待转出锁仓时间 |
| **expiration_to** | date-time | 待转入锁仓时间 |
| **memo**          | string    | 附言           |

#### 示例

fibos.js 环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.exlocktrans({
      from: "dicefobetone",
      to: "eosjianqiang",
      quantity: {"quantity":"0.0008 BET","contract":"dicefobetone"},
      expiration: "1970-01-01T00:00:00",
      expiration_to: "2018-12-02T01:00:00",
      memo: "记得每周日09:00后自己去钱包解锁哟，解锁后，可以去砸盘换FO"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
```



## receipt

#### 参数

| name    | type | description    |
| ------- | ---- | -------------- |
| **in**  | json | extended_asset |
| **out** | json | extended_asset |

#### 示例

```javascript
const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
=======
let ctx = fibos_client.contractSync('eosio.token');

let r = ctx.exlocktransSync('nmslwsndhjyz', 'fibostest123', '10000.0000 BBB@5hzuyqumr3l5', '2018-10-29T18:54:00', '2018-10-29T18:54:00', 'exlocktrans 10000 BBBC@uepgdzfhucin', {
    authorization: '私钥对应的账号'
}); //expiration_to必须大于等于expiration
console.log(r)
```

浏览器环境下：

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

<<<<<<< HEAD
(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.receipt({
      in: {"quantity":"11555.0000 FO","contract":"eosio"},
      out: {"quantity":"20.3375 EOS","contract":"eosio"}
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
fibos_client.contract('eosio.token').then((contract)=>{
    contract.exlocktr不不不``
      from: 'nmslwsndhjyz',
      to: 'fibostest123',
      quantity: '10000.0000 BBB@5hzuyqumr3l5',
      expiration: '2018-10-29T18:54:00',
      expiration_to: '2018-10-29T18:54:00',
      memo: 'exlocktrans 10000 BBB@uepgdzfhucin'
    },{
        authorization: '私钥对应的账号'
    })
});
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```



<<<<<<< HEAD
## snapshot

#### 参数

| name                          | type    | description  |
| ----------------------------- | ------- | ------------ |
| **contract**                  | string  | account_name |
| **max_supply**                | string  |              |
| **cw**                        | float64 |              |
| **max_exchange**              | string  |              |
| **supply**                    | string  |              |
| **reserve_supply**            | string  |              |
| **connector_balance**         | string  |              |
| **reserve_connector_balance** | string  |              |

#### 示例

```javascript

const FIBOS = require('fibos.js');
require('ssl').loadRootCerts();

const client = FIBOS({
  // fibos 主网 chainId
  chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
  keyProvider: '你的私钥',
  httpEndpoint: "http://ca-rpc.fibos.io:8870",
});

(async () => {
  const eosioTokenContract = await client.contract('eosio.token');
  try {
    const ret = await eosioTokenContract.snapshot({
      contract: "eosio",
      max_supply: "100000000000.0000 FO",
      cw: "0.10948151574745998",
      max_exchange: "10025528533.6595 FO",
      supply: "361950483.2024 FO",
      reserve_supply: "5025476157.1198 FO",
      connector_balance: "488116.9226 EOS",
      reserve_connector_balance: "550000.0000 EOS"
    },{
      authorization: '私钥对应的账号'
    });
    
    console.log(ret);
  } catch(e) {
    console.error(e);
  }
})();
=======
## receipt

凭据

#### 参数

| name    | type   | description  |
| ------- | ------ | ------------ |
| **in**  | string | 转入通证凭据 |
| **out** | string | 转出通证凭据 |

#### 示例

```json
"data":{
    "in":{
        "quantity":string"11460.9004 FO"
        "contract":string"eosio"
    }
    "out":{
        "quantity":string"19.8374 EOS"
        "contract":string"eosio"
    }
    "fee":{
        "quantity":string"0.0000 FO"
        "contract":string"eosio"
    }
}
```



## snapshot

快照

#### 参数

| name                          | type    | description          |
| ----------------------------- | ------- | -------------------- |
| **contract**                  | string  | 发币持有者           |
| **max_supply**                | string  | 最大可发行通证数量   |
| **cw**                        | float64 | cw 值                |
| **max_exchange**              | string  | 最大兑换通证数量     |
| **supply**                    | string  | 可发行通证数量       |
| **reserve_supply**            | string  | 锁仓通证数量         |
| **connector_balance**         | string  | 保证金数量           |
| **reserve_connector_balance** | string  | 未流通通证保证金数量 |

```json
"data":{
    "contract":string"eosio"
    "max_supply":string"100000000000.0000 FO"
    "cw":string"0.10944270133906281"
    "max_exchange":string"10027436399.4393 FO"
    "supply":string"350892935.0365 FO"
    "reserve_supply":string"5027379795.1377 FO"
    "connector_balance":string"468809.4805 EOS"
    "reserve_connector_balance":string"550000.0000 EOS"
}
>>>>>>> 1681099d7650c835c422f07d10b7ca35be9a7966
```

