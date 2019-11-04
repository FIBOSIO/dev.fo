---
title: 节点数据持久化
type: tutorials
language: zh-cn
order: 302
---

在业务中我们经常会有查询历史数据的场景，比如：某个账户的历史转账记录，但是考虑到性能的问题，在 EOS 中使用自身查询历史数据并不是个很好的方案，另外 EOS 的 history API 模块部分功能迭代快，甚至即将废弃。

如果能将链上的数据实时同步存放在本地，分离节点服务和查询业务，那将大大提高效率和性能。

在 FIBOS 中，我们提供两种解决方案供大家针对自己的业务场景进行选用。

## Emitter 插件

emitter 是一个监听事件的插件，可以方便的监听到 transaction 、 block 、 irreversible_block 三种事件，你可以使用该监听，根据自己的需求存储对应的数据。

### 优势

- 不受类似与 mongo 插件的约束，能够按照自己的业务需求存储数据。
- 相比较 histroy 插件占用内存小。

### 使用

打开工作目录 `node.js` ，添加 emitter 插件：

```javascript
var fibos = require('fibos');

fibos.load('http');
fibos.load('chain');
fibos.load('net');
fibos.load('chain_api');
fibos.load('emitter'); // 启用 emitter 插件
fibos.on('transaction',at => {
    console.log(at);
}) // 打印 transaction 信息
fibos.on('block',at => {
    console.log(at);
}) // 打印 block 信息
fibos.on('irreversible_block',at => {
    console.log(at);
}) // 打印 irreversible_block 信息
fibos.load('producer', {
    'producer-name': 'eosio',
    'enable-stale-production': true
});
fibos.config_dir = 'fibos_config_dir/';
fibos.data_dir = 'fibos_data_dir/';
fibos.start();
```

运行 FIBOS 开发环境

```javascript
fibos node.js
```

`eosio` 已经开始区块生产，并且打印获取的 transaction 、 block 、 irreversible_block 的数据。 

下面将数据同步保存至 MySql 数据库中，步骤如下：

1. 连接 MySql 数据库

使用 db.open 或 db.openMySQL 创建，创建方式：

```javascript
var mysql = db.openMySQL('mysql://user:pass@host/db');
```

2. 执行一个 sql 命令，并返回执行结果，可根据参数格式化字符串

```javascript
 mysql.execute(String sql,...args);
```

- 调用参数：

  sql：String，格式化字符串，可选参数用 ? 指定。例如：'INSERT INTO TABLENAME (列名…) VALUES (列值);'

  args：...，可选参数列表

```javascript
var fibos = require('fibos');
var db = require('db');
var mysql = db.openMySQL('mysql://user:pass@host/db'); // 修改为自己的 mysql 的配置

fibos.load('http');
fibos.load('chain');
fibos.load('net');
fibos.load('chain_api');
fibos.load('emitter');
fibos.on('transaction',at => {
    console.log(at);
    let acitonname = at.action_traces[0].act.name;
    if(acitonname === 'extransfer') {
        let trx_id = at.action_traces[0].trx_id
        let data = at.action_traces[0].act.data;
        let from = data.from;
        let to = data.to;
        let memo = data.memo;
        let quantity = data.quantity.quantity;
        let contract = data.quantity.contract;
	    mysql.execute('insert into transfer_info(from,to,memo,trx_id,quantity,contract) values(?,?,?,?,?,?)', [from , to, memo , trx_id , quantity , contract]);        
    }
})// 打印 transaction 信息，并将其中的 extransfer 信息写入 mysql 中的 transfer_info 数据表中
fibos.load('producer', {
    'producer-name': 'eosio',
    'enable-stale-production': true
});
fibos.config_dir = 'fibos_config_dir/';
fibos.data_dir = 'fibos_data_dir/';
fibos.start();
```

### 其他

区块上的数据不仅仅可以保存于 **MySql** 数据库，还能同步保存于 `db模块` 下支持的其他数据库。

例如：

- **sqlite**
- <del>**mongodb**</del> 注意 emitter 不支持 mongodb， 因为支持了 eos 的 mongodb 插件， FIBJS 禁用了 mongodb 插件。
- **leveldb**
- **Redis**

## fibos-tracker 框架

fibos-tracker 是一个 FIBOS 区块链数据 GraphQL API 服务框架，基于 [fib-app](https://github.com/fibjs/fib-app) 框架实现，当前版本 v1.1.0。

项目地址：https://github.com/FIBOSIO/fibos-tracker

它主要的功能是：

- 提供对 FIBOS 区块数据的 emitter 监听事件
- 提供 http 服务，支持 GraphQL 调用
- 支持使用 ORM 模型 定制自己的数据模型 model，自定义数据表以及自定义 hook 监听数据

### 快速安装

```
fibos --install fibos-tracker
```

### 框架说明

框架默认存储了 blocks 、transactions 以及 actions 的基础数据

#### blocks 表数据

| 字段              | 类型   | 备注          |
| ----------------- | ------ | ------------- |
| id                | Number | 自增长 id     |
| block_num         | Number | 区块高度      |
| block_time        | Date   | 区块时间      |
| producer_block_id | String | 区块 hash     |
| producer          | String | 区块 producer |
| status            | String | 可逆状态      |
| createdAt         | Date   | 记录创建时间  |
| updatedAt         | Date   | 记录更新时间  |

#### transactions 表数据

| 字段      | 类型   | 备注                    |
| --------- | ------ | ----------------------- |
| id        | Number | 自增长 id               |
| trx_id    | String | 交易 hash               |
| rawData   | JSON   | 原始数据                |
| block_id  | String | 区块高度（关联 blocks） |
| createdAt | Date   | 记录创建时间            |
| updatedAt | Date   | 记录更新时间            |

#### actions 表数据

| 字段           | 类型   | 备注                                    |
| -------------- | ------ | --------------------------------------- |
| id             | Number | 自增长 id                               |
| contract_name  | String | 合约名称                                |
| action         | String | action 名称                             |
| authorization  | Array  | 授权用户                                |
| data           | JSON   | 交易 data                               |
| transaction_id | Number | 交易事务 id （关联 Table transactions） |
| parent_id      | Number | 上级 action id （关联 Table actions）   |
| createdAt      | Date   | 记录创建时间                            |
| updatedAt      | Date   | 记录更新时间                            |

### API 介绍

#### Tracker.Config

Config 是 Tracker 全局属性，可以使用该属性快速修改配置，如：修改存储引擎配置。

示例：

```javascript
const Tracker = require("fibos-tracker");

Tracker.Config.DBconnString = "mysql://root:123456@127.0.0.1/fibos_chain";

Tracker.Config.isFilterNullBlock = false;
```

| name              | desc             | default                  |
| ----------------- | ---------------- | ------------------------ |
| DBconnString      | 数据存储引擎     | 默认使用 SQLite 存储引擎 |
| isFilterNullBlock | 是否过滤空块     | 默认 true                |
| isSyncSystemBlock | 是否存储默认数据 | 默认 false               |

#### tracker.app

fib-app 的实例 app 对象，具体请阅读 [fib-app](https://github.com/fibjs/fib-app) 相关文档。

tracker.app 对象可支持路由访问。

示例：

```javascript
const http = require("http");
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

let httpServer = new http.Server("", 8080, {
	'/1.0/app': tracker.app
});

httpServer.run();
```

#### tracker.emitter

配合 FIBOS 的 action 插件使用。

示例：

```javascript
const fibos = require("fibos");
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

tracker.emitter(fibos);
```

| params | type       | desc |
| ------ | ---------- | ---- |
| fibos  | fibos 对象 | /    |

#### tracker.diagram

生成数据表的关联图，如果自定义了数据表，需要先调用 tracker.use 再执行。

示例：

```javascript
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

//If exist other db modles，please exec tracker.use.

tracker.diagram();
```

#### tracker.stop

使 tracker 安全停止

示例：

```javascript
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

tracker.stop();
```

#### tracker.use

自定义 hook 监听数据，使用 ORM 模型自定义 DB 存储以及处理。

示例：

```javascript
const fibos = require("fibos");
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

tracker.use({
	defines: [(db) => {
		// ORM DB Define
	}, (db) => {
		// ORM DB Define
	}],
	hooks: {
		"eosio.token/transfer": (db, messages) => {
			// hook Tracker messages
		},
		"eosio/newaccount": (db, messages) => {
			// hook Tracker messages
		}
	}
});
```

defines 支持数组形式，满足某个 model 需要多个数据表的操作场景。

tracker.use 参数定义：

| params | type   | desc                                  |
| ------ | ------ | ------------------------------------- |
| model  | Object | 自定义数据对象，包含 defines 和 hooks |

`model` 内部参数定义：

| key     | type     | desc                                   | params                                                       |
| ------- | -------- | -------------------------------------- | ------------------------------------------------------------ |
| defines | Function | 使用 ORM 模型定义数据表，提供 API 访问 | `(db) => {}`参数 db 是 ORM 对象，可用于操作数据层            |
| hooks   | Function | 支持过滤 action 数据的 hook function   | `(db, messages) => {}` 参数 db 是 ORM 对象，参数 messages 是 action 原始数据集合 |

hooks 的过滤规则说明：

- 过滤某个合约，如：`eosio.token`
- 过滤某个合约的 action，如：`eosio.token/transfer`

hooks 的 messages 数据说明：

为了方便 hooks 业务研发，传递 messages 时做了优化：

- 满足过滤规则的所有 action 合并成数组传递
- 数组内每一个满足过滤规则的 action 包含 本层 action 以下所有 inline_action，并且如果存在上层 action，将携带 parent 属性，标识上层 parent 的 action 数据。

注：每层 `parent_id` 是该层 `action` 上级的 DB 自增长 id。

举一个返回示例结构：

```javascript
[
  {
    "inline_traces": [
      {
        "parent": ... parent_id => 1
        "inline_traces": [
          {
            "parent": ... parent_id => 2
                "parent": ... parent_id => 1
          },
          {
            "parent": ... parent_id => 2
                "parent": ... parent_id => 1
          }
        ]
      }
    ]
  }
]
```

#### tracker.Queues

tracker 在处理事件数据时，会优先存入队列，当你恢复数据、重置环境时建议清理环境

示例：

```javascript
const fibos = require("fibos");
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

tracker.Queues.clear(); //清理队列数据

tracker.Queues.stats(); //输出队列统计信息
```

### 快速应用

[Example 源码](https://github.com/FIBOSIO/fibos-tracker/blob/master/examples)

学习了解 fibos-trakcer 之后，让我们开始动手编写，使用框架写一个区块链数据存储展现的应用。

与 FIBOS 的 emiiter 结合，写一个应用。 它可以同步 FIBOS TestNet 网络区块数据，并且使用 GraphQL 获取应用数据。

[FIBOS TestNet WebSite](https://testnet.fibos.fo/#/)：

#### 环境准备

1. 安装 FIBOS

[快速安装](./installation.html)

2. 准备示例目录

```
 :$ mkdir example;cd example
 :$ fibos --init
 :$ fibos --install fibos-tracker
```

#### 编写例子

[genesis.json](https://github.com/FIBOSIO/fibos-tracker/blob/master/examples/genesis.json) 是 FIBOS TestNet 网络的配置。

[index.js](https://github.com/FIBOSIO/fibos-tracker/blob/master/examples/index.js) :

```javascript
const http = require("http");
const fibos = require("fibos");
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

fibos.config_dir = "./data";
fibos.data_dir = "./data";
fibos.load("http", {
	"http-server-address": "0.0.0.0:8870",
	"access-control-allow-origin": "*",
	"http-validate-host": false,
	"verbose-http-errors": true
});

fibos.load("net", {
	"p2p-peer-address": ["p2p-testnet.fibos.fo:9870"],
	"p2p-listen-endpoint": "0.0.0.0:9870"
});

fibos.load("producer");
fibos.load("chain", {
	"contracts-console": true,
	"delete-all-blocks": true,
	"genesis-json": "genesis.json"
});

fibos.load("chain_api");

tracker.emitter(fibos);

fibos.start();

let httpServer = new http.Server("", 8080, [
	(req) => {
		req.session = {};
	}, {
		'^/ping': (req) => {
			req.response.write("pong");
		},
		'/1.0/app': tracker.app,
		"*": [function(req) {}]
	},
	function(req) {}
]);

httpServer.crossDomain = true;
httpServer.asyncRun();
```

#### 启动服务

```
fibos index.js
```

输出下列信息，说明启动成功，正在同步写入数据：

```
putLog emitter-running: 1.54080331e+12ms
```

#### 使用 GraphQL 方式获取应用数据

1. FIBOS GraphQL 客户端

fibjs 示例：

```javascript
const http = require("http");

let graphql = function(body) {
	return http.post(`http://127.0.0.1:8080/1.0/app/`, {
		headers: {
			'Content-Type': 'application/graphql'
		},
		body: body
	});
}
```

2. Web GraphQL 客户端

jQuery Ajax 示例：

```javascript
let graphql = function(body) {
    $.ajax({
        type: "POST",
        url: "http://127.0.0.1:8080/1.0/app",
        data: body,
        headers: {
            "Content-Type": "application/graphql"
        },
        success: (res) => {
            console.log("success");
        },
        error: (res) => {
            console.log("error");
        }
    });
}
```

#### GraphQL 获取应用 - 列表数据

```
graphql(`
{
    find_blocks(
       	skip: 0,
        limit: 10,
        order: "-id"
    ){
        id,
        block_time,
        block_num,
        producer_block_id,
        producer,
        status,
        createdAt,
        updatedAt
    }
}`)
```

#### GraphQL 获取应用 - 详情数据

```
graphql(`
{
    find_blocks(
		where:{
			block_num: 23
		}
	) {
        id,
        block_time,
        block_num,
		producer_block_id,
		producer,
		status,
		createdAt,
		updatedAt,
		actions{
			id,
			trx_id,
			contract_name,
			action,
			authorization,
			data,
			createdAt,
			updatedAt
		}
    }
}`)
```

更多详细内容以及框架的高级应用及其示例，请访问 [项目地址](https://github.com/FIBOSIO/fibos-tracker) 获取更多信息。