---
title: 加入节点网络
type: tutorials
language: zh-cn
order: 301
---

上一章中，我们介绍了 FIBOS 的节点网络。这一章中，我们将加入其中，成为一个节点，亲身体会区块链网络的魅力。

## fibos-nodes

fibos-nodes 是由 FIBOS 社区提供的一款快速启动 FIBOS 主网节点的脚本工具，他能帮助开发者快速启动三种不同类型的节点。

项目地址：https://github.com/FIBOS-Community/fibos-nodes

### 安装

```
git clone https://github.com/FIBOS-Community/fibos-nodes.git
cd fibos-nodes
```

### 启动

```
fibos bp.js   // 快速启动一个bp节点

fibos full.js // 快速启动一个全节点

fibos seed.js // 快速启动一个同步节点
```

默认数据，配置存储位置 /blockData/data

### 全节点数据同步

全节点区块数据同步耗时长，FIBOS 社区提供最新镜像启动服务，极大缩短区块同步时间。

服务地址：http://ghost.bp.fo/

#### 使用方法

1. 下载数据：

   访问 http://ghost.bp.fo/ghost/ 选择想要同步的数据包文件，直接点击下载

   或者获取文件URL，使用 wget 命令进行下载

   ```
   weget http://ghost.bp.fo/ghost/data_15600397.tar.gz
   ```

2. 解压文件：

   ```
   tar -zxvSf data.tar.gz
   ```

3. 修改快速启动脚本配置文件 config.json ：

   将 data_dir 参数指向刚刚数据文件解压的 fibos-data 目录即可。

   ```json
   "data_dir": "fibos-data/",
   ```

4. 启动全节点

   ```
   fibos full.js
   ```

## 手动加入 FIBOS 节点网络

如果你不使用 fibos-nodes 这个工具进行节点启动的话，你也可以自行编写启动脚本，加入到节点网络中来。

加入 FIBOS 网络配置需要涉及几个关键信息：

#### 获得节点网络的 chainId

TestNet：

```
chainId : '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a'
```

FIBOS 主网：

```
chainId : '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a'
```

#### 提供 P2P 监听的地址以及端口

```
'p2p-listen-endpoint' : '0.0.0.0:9870'
```

#### 区块数据同步的目标节点信息

区块数据同步必须先从已经在运行的超级节点中同步数据。

目前 TestNet BP 节点由 FIBOS 基金会提供，p2p 地址为 p2p-testnet.fibos.fo:9870 和 p2p-testnet-02.fibos.fo:9870

```
'p2p-peer-address' : ['p2p-testnet.fibos.fo:9870','p2p-testnet-02.fibos.fo:9870']
```

FIBOS 主网的超级节点已全部被社区节点取代，具体的 BP 节点信息，请访问 https://www.fibos123.com/#!/bp 

```
'p2p-peer-address' : ['p2p.mainnet.fibos.me:80','seed-mainnet.fibscan.io:9103']
```

注意：示例中给出的 FIBOS 主网 BP P2P 地址，会发生变动，请时刻关注。

#### genesis.json 文件

TestNet：

```json
{
    "initial_timestamp": "2018-08-01T00:00:00.000",
    "initial_key": "FO6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
    "initial_configuration": {
        "max_block_net_usage": 1048576,
        "target_block_net_usage_pct": 1000,
        "max_transaction_net_usage": 524288,
        "base_per_transaction_net_usage": 12,
        "net_usage_leeway": 500,
        "context_free_discount_net_usage_num": 20,
        "context_free_discount_net_usage_den": 100,
        "max_block_cpu_usage": 200000,
        "target_block_cpu_usage_pct": 1000,
        "max_transaction_cpu_usage": 150000,
        "min_transaction_cpu_usage": 100,
        "max_transaction_lifetime": 3600,
        "deferred_trx_expiration_window": 600,
        "max_transaction_delay": 3888000,
        "max_inline_action_size": 4096,
        "max_inline_action_depth": 4,
        "max_authority_depth": 6
    },
    "initial_chain_id":"68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a"
}
```

FIBOS 主网：

```javascript
{
    "initial_timestamp": "2018-08-28T00:00:00.000",
    "initial_key": "FO6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
    "initial_configuration": {
        "max_block_net_usage": 1048576,
        "target_block_net_usage_pct": 1000,
        "max_transaction_net_usage": 524288,
        "base_per_transaction_net_usage": 12,
        "net_usage_leeway": 500,
        "context_free_discount_net_usage_num": 20,
        "context_free_discount_net_usage_den": 100,
        "max_block_cpu_usage": 200000,
        "target_block_cpu_usage_pct": 1000,
        "max_transaction_cpu_usage": 150000,
        "min_transaction_cpu_usage": 100,
        "max_transaction_lifetime": 3600,
        "deferred_trx_expiration_window": 600,
        "max_transaction_delay": 3888000,
        "max_inline_action_size": 4096,
        "max_inline_action_depth": 4,
        "max_authority_depth": 6
    },
    "initial_chain_id":"6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a"
}
```

### 如何成为一个同步节点

如果节点仅仅作为同步 FIBOS 区块数据，非常简单。以下代码保存至 `sync_node.js`:

```javascript
var fibos = require('fibos');

fibos.config_dir = 'sync_data_Dir';
fibos.data_dir = 'sync_data_Dir';

console.notice('config_dir:', fibos.config_dir);
console.notice('data_dir:', fibos.data_dir);

fibos.load('http', {
	'http-server-address': '0.0.0.0:8870'
});

fibos.load('net', {
	'p2p-listen-endpoint': '0.0.0.0:9870',
	'p2p-peer-address': ['p2p.mainnet.fibos.me:80','seed-mainnet.fibscan.io:9103']
});

fibos.load('producer');
fibos.load('chain',{
	'genesis-json':'genesis.json',
	'delete-all-block':true
});
fibos.load('chain_api');

fibos.start();
```

上述代码中，`net` 模块中的 `p2p-peer-address` 是一个可变值，请注意修改。

运行同步节点:

```
fibos sync_node.js
```

## 如何成为一个 BP 节点

(* BP 区块生产者)

> 重要提示：使用 Producer 身份发起注册申请，最好 producer key 不要和 active key 一样！

如果节点需要申请注册成为 FIBOS 主网的区块生产者，需要涉及到 3 个方面：

- 配置 Producer 信息启动 FIBOS 节点服务
- 使用 Producer 身份发起注册申请
- 发起投票使得成为 Producer

### 配置 Producer 信息启动 FIBOS 节点服务

只有投票数量达到一定的数量，FIBOS 节点才会真正的成为 Producer，拥有生产区块的权限，其他情况仅仅作为同步区块数据的身份存在。

以下代码实现了配置一个 Producer，保存代码至 `producer_node.js`:

```javascript
var fibos = require('fibos');
var fs = require('fs');
var config = {
	'producer-name': 'producer-name',
	'public-key': 'producer public key',
	'private-key': 'producer private key'
};


console.notice('正在启动FIBOS name:', config['producer-name']);
fibos.config_dir = config['producer-name'] + '_Dir';
fibos.data_dir = config['producer-name'] + '_Dir'

console.notice('config_dir:', fibos.config_dir);
console.notice('data_dir:', fibos.data_dir);

if (fs.exists(fibos.data_dir) || fs.exists(fibos.config_dir)) {
	console.warn('data_dir or config_dir is exists');
	process.exit(-1);
}

fibos.load('http', {
	'http-server-address': '0.0.0.0:8870'
});

fibos.load('net', {
	'p2p-listen-endpoint': '0.0.0.0:9870',
	'p2p-peer-address': ['p2p.mainnet.fibos.me:80','seed-mainnet.fibscan.io:9103']
});

fibos.load('producer', {
	'producer-name': config['producer-name'],
	'enable-stale-production': true,
	'private-key': JSON.stringify([config['public-key'], config['private-key']])
});

fibos.load('chain',{
	'genesis-json':'genesis.json',
	'delete-all-block':true
});
fibos.load('chain_api');

fibos.start();
```

上述代码中可变配置说明：

```javascript
var config = {
	'producer-name': 'producer-name', // producer 名称
	'public-key': 'producer public key', // producer 公钥
	'private-key': 'producer private key' // producer 私钥
};
```

运行 Producer 节点:

```
fibos producer_node.js
```

### 使用 Producer 身份发起注册申请

**调用方法：**

```javascript
// 初始化一个 fibos 客户端
var ctx = fibos.contractSync('eosio');
var a = ctx.regproducerSync('prducerName', 'publickey', 'url', 'location');
```

**方法说明：**

使用 fibos.js 客户端 调用 eosio 合约发起注册 BP 操作

**实例：**

以下代码保存至 `register_bp.js` :

```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
    priKey: 'producer privateKey',
    httpEndpoint: 'http://ca-rpc.fibos.io:8870',
    verbose: false,
    location: 1,
    url: 'http://producer-name.io'
}
var fibos = FIBOS({
    chainId: config.chainId,
    keyProvider: config.priKey,
    httpEndpoint: config.httpEndpoint,
    verbose: false,
    logger: {
        log: null,
        error: null
    }
})
var publicKey = ''; // producer publicKey
var producerName = ''; // producer name
var ctx = fibos.contractSync('eosio');
var a = ctx.regproducerSync(producerName, publicKey, config.url, config.location);
console.log(result);
```

**实例说明:**

实例操作中，配置好 FIBOS MainNet 和 FIBOS RPC 地址 和 FIBOS 私钥后，便初始化了一个 FIBOS 客户端，通过调用 `regproducerSync` 方法，传入四个参数：

| 参数         | 含义                         |
| ------------ | ---------------------------- |
| producerName | 区块生产者账户名             |
| publicKey    | 区块生产者公钥               |
| url          | 区块生产者宣传网站           |
| location     | 区块生产者服务器位置地区代码 |

### 获取投票数成为 Producer

成为 BP 需要获得一定数量的投票数，你可以让别人给你投票，也可以自己给自己投票。投票需要抵押 FO 获取资源，下面教会大家如何抵押资源以及进行投票。

#### 抵押资源

**调用方法：**

```javascript
//初始化一个 fibos 客户端
var ctx = fibos.contractSync('eosio');
var a = ctx.delegatebwSync({
	from: 'buyer_name',
	receiver: 'recevier_name',
	stake_net_quantity: 'quality',
	stake_cpu_quantity: 'quality',
	transfer: 0
});
```

**方法说明：**

使用  `delegatebwSync`  方法抵押 FO 获取 NET 和 CPU 资源，用来投票。

**实例：**

```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
    priKey: 'privateKey',
    httpEndpoint: 'http://ca-rpc.fibos.io:8870',
    verbose: false,
}
var fibos = FIBOS({
    chainId: config.chainId,
    keyProvider: config.priKey,
    httpEndpoint: config.httpEndpoint,
    verbose: false,
    logger: {
        log: null,
        error: null
    }
})
var ctx = fibos.contractSync('eosio');
ctx.delegatebwSync({
	from: 'fibos account', // 抵押资源者账号
	receiver: 'fibos account', // 资源接收者账号
	stake_net_quantity: '1.0000 FO',
	stake_cpu_quantity: '1.0000 FO',
	transfer: 0
});
```

**实例说明:**

配置了 FIBOS 主网的 chainId 和 Http 服务地址后，便初始化了一个 FIBOS 客户端。调用  `delegatebwSync` 方法，抵押 FO 获取资源。

| 参数               | 含义                                                         |
| ------------------ | ------------------------------------------------------------ |
| from               | 抵押资源者                                                   |
| receiver           | 资源接收者                                                   |
| stake_net_quantity | 获取 Net 抵押的 FO 数量                                      |
| stake_cpu_quantity | 获取 CPU 抵押的 FO 数量                                      |
| transfer           | 0 : 表示使用自己的资源为他人抵押；1 : 表示赠送资源给他人并抵押。注意：自己为自己抵押资源的时候，只能填 0 |

#### 进行投票

**调用方法：**

```javascript
//初始化一个 fibos 客户端
var ctx = fibos.contractSync('eosio');
var a = ctx.voteproducerSync('voter', 'proxy', 'producers');
```

**方法说明：**

 使用 `voteproducerSync` 方法，来给 BP 进行投票。

**实例：**

以下保存代码至 `vote_bp.js`

```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
    priKey: 'privateKey',
    httpEndpoint: 'http://ca-rpc.fibos.io:8870',
    verbose: false,
}
var fibos = FIBOS({
    chainId: config.chainId,
    keyProvider: config.priKey,
    httpEndpoint: config.httpEndpoint,
    verbose: false,
    logger: {
        log: null,
        error: null
    }
})
var ctx = fibos.contractSync('eosio');
 
var fibosnodes = ['fibosbpnodec','fibosbpnodeb','fibosbpnodea']; // 具体账号数据请开发者根据实际情况自行填写
fibosnodes.sort()；

var a = ctx.voteproducerSync('fibostest123', '', fibosnodes); // 具体账号数据请开发者根据实际情况自行填写
```

**实例说明：**

上述代码的含义为 `fibostest123` 这个用户给 `fibosbpnodea, fibosbpnodeb, fibosbpnodec`  投票，投票节点列表需要由开发者自己按照字母序排序，一次性最多可以给30个 BP 投票。中间空着的参数为代理，不填表示直接给 BP 投票，填入则是通过代理给 BP 投票。

执行投票:

```
fibos vote_bp.js
```

注意：投票结束后，排名必须在 TOP 21 前才可以被选为区块生产者 BP。

### 领取奖励

成为 BP 并成功出块后，会获得相应的奖励，可以调用下面的接口来领取奖励：

**调用方法：**

```javascript
//初始化一个 fibos 客户端
var a = fibos.claimrewardsSync('producer');
```

**方法说明：**

 使用 `claimrewardsSync` 方法，来领取 BP 奖励。

**实例：**

```javascript
var FIBOS = require('fibos.js');
var config = {
    chainId: '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a',
    priKey: 'producer_privateKey',
    httpEndpoint: 'http://ca-rpc.fibos.io:8870',
    verbose: false,
}
var fibos = FIBOS({
    chainId: config.chainId,
    keyProvider: config.priKey,
    httpEndpoint: config.httpEndpoint,
    verbose: false,
    logger: {
        log: null,
        error: null
    }
})
var a = fibos.claimrewardsSync('fibosbpnode1') // 具体账号数据请开发者根据实际情况自行填写
```

**实例说明：**

上述代码为  `fibosbpnode1`  领取了自己出块获得的奖励！

### p2p 自发现配置说明

**开启 p2p 自发现：**

当连接上一个节点后，它如果和你都开启了 p2p 自发现，那么它会把自己连接上的节点共享给你，你也会连上他给你的节点，这样更好增加网络的稳定性。

**fibos 支持版本**

```
v1.7.1.4 +
```

**开启 p2p 自发现实例**

```net ```插件配置 ```p2p-max-nodes-per-host ```

```
fibos.load("net", {
	"p2p-peer-address": [],
	"max-clients": 0,    //允许链接数量无限
	"p2p-listen-endpoint": "0.0.0.0:9870",
	"p2p-max-nodes-per-host": 100,  //允许p2p发现
	"agent-name": "FIBOS node"
}
```

### eth 组件节点配置说明

**fibos 版本要求：**

```
v1.7.1.4 +
```

**普通节点：**

```
//v1.7.1.4 + 
    
fibos.load("ethash");
```

**bp 节点：**

```
//v1.7.1.4 + for eth fox
    
fibos.load("ethash");
fibos.load("bp_signature", {
	"signature-producer": producername,
	"signature-private-key": private_key
});
```