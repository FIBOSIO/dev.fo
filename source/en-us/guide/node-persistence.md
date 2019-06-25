---
title: Node Data Persistence 
type: tutorials
language: en
order: 302
---

In buisness, we often have needs to query history data, such as: a certain account's transfer history, but considering performance, performing self historic data query in EOS is not a great solution, also EOS' history API module has slow iterations, even about to be abandoned.

If the data onchain can be real-time synced locally, seperating node services and buisness query, then efficiency can be greatly improved. 

In FIBOS, we offer three solutions for you to choose for your own scenario.

## Emitter Plug In 

emitter is an event listening plugin, can easily listen to events of transaction, block, and irreversible_block. You can use it to listen in, and store the corresponding data according to your own needs.

### Advantages 

- No restrictions such as that of mongo plugins, and have the ability to store data according to your business needs.
- Compared to history plugin, uses less RAM. 

### Usage

Open the working directory `node.js` and add the emitter plugin: 

```javascript
var fibos = require('fibos');

fibos.load('http');
fibos.load('chain');
fibos.load('net');
fibos.load('chain_api');
fibos.load('emitter'); // start emitter plugin
fibos.on('transaction',at => {
    console.log(at);
}) // print transaction info
fibos.on('block',at => {
    console.log(at);
}) // print block info
fibos.on('irreversible_block',at => {
    console.log(at);
}) // print irreversible_block info
fibos.load('producer', {
    'producer-name': 'eosio',
    'enable-stale-production': true
});
fibos.config_dir = 'fibos_config_dir/';
fibos.data_dir = 'fibos_data_dir/';
fibos.start();
```

Operate FIBOS runtime environment 

```javascript
fibos node.js
```

`eosio` already started block production, print transaction, block, and irreversible_block data obtain. 

Next, synch and swave the data to MySql database, the steps are as follows: 

1. Connect MySql Database

Use db.open or db.openMySQL to create, the create method: 

```javascript
var mysql = db.openMySQL('mysql://user:pass@host/db');
```

2. Run a sql command and return the result, can format string based on parameters

```javascript
 mysql.execute(String sql,...args);
```

- Call Parameters：

  sql：String，formatted string, optional parameters specified with ?. Example: 'INSERT INTO TABLENAME (name…) VALUES (value);'

  args：...，Optional parameter list

```javascript
var fibos = require('fibos');
var db = require('db');
var mysql = db.openMySQL('mysql://user:pass@host/db'); // 
Change to your own mysql configs 

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
})// print transaction info，and write the extransfer info into transfer_info array of mysql
fibos.load('producer', {
    'producer-name': 'eosio',
    'enable-stale-production': true
});
fibos.config_dir = 'fibos_config_dir/';
fibos.data_dir = 'fibos_data_dir/';
fibos.start();
```

### Other

Data on the block can not only be saved to **MySql** database, it can also be sync and sacved to other databses under the `db module`. 

Example：

- **sqlite**
- <del>**mongodb**</del> note that emitter does not support mongob. Because it supports EOS' mongodb plugin, FIBJS disabled the mongodb plugin. 

- **leveldb**
- **Redis**

## fibos-tracker framework 

fibos-tracker is a FIBOS blockchain data GraphQL API service framework, realized based off    [fib-app](https://github.com/fibjs/fib-app), current version is v1.1.0. 

Project Website: https://github.com/FIBOSIO/fibos-tracker

Its main functions are：

- Provide emitter listening events to FIBOS block date
- Provide http service, supports call of GraphQL 
- Supports using ORM model to customize own data model model, custom data table and custom hook listening data

### Quick Installation 

```
fibos --install fibos-tracker
```

### Framework clarification 

Framework defaultly saves block, transaction and actions base data 

#### blocks table data

| Field             | Type   | Note                   |
| ----------------- | ------ | ---------------------- |
| id                | Number | Self-Growing id        |
| block_num         | Number | Block Height           |
| block_time        | Date   | Block Date             |
| producer_block_id | String | block hash             |
| producer          | String | block producer         |
| status            | String | Reversible status      |
| createdAt         | Date   | Record creation time   |
| updatedAt         | Date   | Record update time     |

#### transactions table data

| Field      | Type  | Note                            |
| --------- | ------ | ------------------------------- |
| id        | Number | Self-Growing id                 |
| trx_id    | String | Transaction hash                |
| rawData   | JSON   | Raw Data                        |
| block_id  | String | Block Height (Links blocks)     |
| createdAt | Date   | Record creation time            |
| updatedAt | Date   | record update time              |

#### actions table data

| Field          | Type   | Note                                           |
| -------------- | ------ | ---------------------------------------------- |
| id             | Number | Self-Growing id                                |
| contract_name  | String | Contract Name                                  |
| action         | String | action Name                                    |
| authorization  | Array  | authorize account                              |
| data           | JSON   | Transaction data                               |
| transaction_id | Number | Transaction id (Regard Table transactions)     |
| parent_id      | Number | parent action id (Regard Table actions)        |
| createdAt      | Date   | Record creation time                           |
| updatedAt      | Date   | Record update time                             |

### API Introduction 

#### Tracker.Config

Config is global attribute of Tracker, it can be used to quickly modify settings, such as: modify the storage engine configuration. 


Example：

```javascript
const Tracker = require("fibos-tracker");

Tracker.Config.DBconnString = "mysql://root:123456@127.0.0.1/fibos_chain";

Tracker.Config.isFilterNullBlock = false;
```

| name              | desc                            | default                              |
| ----------------- | ------------------------------- | ------------------------------------ |
| DBconnString      | Data storage engine             | Default use SQLite storage engine    |
| isFilterNullBlock | Whether to filter empty blocks  | Default true                         |
| isSyncSystemBlock | Whether to store default data   | Default false                        |

#### tracker.app

fib-app instance app object, for details please refer to [fib-app](https://github.com/fibjs/fib-app) documentation. 

tracker.app object supports rounting access. 

Example：

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

Uses with action plugin of FIBOS. 


Example：

```javascript
const fibos = require("fibos");
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

tracker.emitter(fibos);
```

| params | type         | desc |
| ------ | ------------ | ---- |
| fibos  | fibos object | /    |

#### tracker.diagram

Generate data table associated diagram, if self-defined data tabled, must call tracker.use then run. 

Example：

```javascript
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

//If exist other db modles，please exec tracker.use.

tracker.diagram();
```

#### tracker.stop

Safe stops tracker

Example：

```javascript
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

tracker.stop();
```

#### tracker.use

Self-define hook listening data, use ORM model to define DB storage and process. 

Example：

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

defines supports arrays, fulfills operational senarios that some model requires multiple tables. 

tracker.use Parameter Definitions：

| params | type   | desc                                          |
| ------ | ------ | --------------------------------------------- |
| model  | Object | Custom data object, includes defines and hook |

`model` Parameter Definitions

| key     | type     | desc                                                    | params                                                        |
| ------- | -------- | ------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| defines | Function | Use ORM model to define data table, provides API access |              `(db) => {}` parameter db is ORM object，can be used to operate data layers               |
| hooks   | Function | supports filter of action data's hook function          |              `(db, messages) => {}` parameter db is ORM object，messages is action Raw data collection |

hooks filter rules clarification: 

- filter certain contract, such as: `eosio.token`
- filter certain action of contract, such as: `eosio.token/transfer`

hooks messages data clarification： 

For easy hooks development, pass of messages is optimized: 

- All action that satisfy the filter rule are merged into an array to pass
- All action in array that satisfy the filter rule including this layer action and all below layer inline_action, if there are action in above layers, will carry parent attribute, identifu]y the action data of the upper parent. 

Note: Each layer `parent_id` is the DB self-growth id of the level's `action`.
 
Example return structure: 

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

When tracker is handling event data, it will first be saved to the queue. When you are restoring data or resetting environment, it is suggested to clean up the environment. 

Example：

```javascript
const fibos = require("fibos");
const Tracker = require("fibos-tracker");
const tracker = new Tracker();

tracker.Queues.clear(); //Clean up queue data

tracker.Queues.stats(); //Output queue stats
```

### Quick Application  

[Example Source Code](https://github.com/FIBOSIO/fibos-tracker/blob/master/examples)

After understanding fibos-tracker, let us start writing, using framework to write a blockchain data storage display application.  

Integrating with FIBOS' emitter, create an application. It can sync FIBOS TestNet network block data, and use GraphQL to obtain application data.  

[FIBOS TestNet WebSite](https://testnet.fibos.fo/#/)：

#### Prepare Environment

1. Install FIBOS

[Quick Installation](./installation.html)

2. Prepare sample directory

```
 :$ mkdir example;cd example
 :$ fibos --init
 :$ fibos --install fibos-tracker
```

#### Write Example

[genesis.json](https://github.com/FIBOSIO/fibos-tracker/blob/master/examples/genesis.json) is the network config of FIBOS TestNet. 

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

#### Startup Services

```
fibos index.js
```

Return the following means startup is sucessful, and is sync writing data. 

```
putLog emitter-running: 1.54080331e+12ms
```

#### Use GraphQL method to obtain application data 

1. FIBOS GraphQL Client

fibjs Example：

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

2. Web GraphQL Client

jQuery Ajax Example：

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

#### GraphQL Get application - data list

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

#### GraphQL Get application - detail data

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

For more detailed information and high level usage and examples of the framework, please visit [project website](https://github.com/FIBOSIO/fibos-tracker) 

## mongoDB Plugin

EOS itself provides pljug in for mongoDB (eosio::mongo_db_plugin), FIBOS also uses this feature. The implementation principle of this module is synching the block data to mongoDB. This makes mongoDB a centralized data storage. 

We will start locally a FIBOS node service, creating account and query within mongoDB. 

#### Start mongod service 

If you have not installed mongoDB, please refer to [Install mongoDB Community Edition](https://docs.mongoDB.com/manual/administration/install-community/). 

First we will start the mongod service, the command is a follows: 

```
fibos$ mongod
```

If it returns the following, it means startup of mongod service is successful. 

```
2018-08-08T09:52:09.459+0800 I CONTROL  [main] Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'
2018-08-08T09:52:09.534+0800 I CONTROL  [initandlisten] mongoDB starting : pid=8061 port=27017 dbpath=/data/db 64-bit host=Velen
2018-08-08T09:52:09.534+0800 I CONTROL  [initandlisten] db version v4.0.1
2018-08-08T09:52:09.534+0800 I CONTROL  [initandlisten] git version: 54f1582fc6eb01de4d4c42f26fc133e623f065fb
2018-08-08T09:52:09.534+0800 I CONTROL  [initandlisten] allocator: system
2018-08-08T09:52:09.534+0800 I CONTROL  [initandlisten] modules: none
2018-08-08T09:52:09.534+0800 I CONTROL  [initandlisten] build environment:
2018-08-08T09:52:09.534+0800 I CONTROL  [initandlisten]     distarch: x86_64
2018-08-08T09:52:09.534+0800 I CONTROL  [initandlisten]     target_arch: x86_64
```

#### Start FIBOS Runtime

If you have not installed FIBOS, please refer to [Install runtime environment](./installation.html). 

To sync data to mongoDB, all thats needed is to add `fibos.load('mongo_db')` to the code in the getting started tutorial, loading the mongo_db module into FIBOS. Only with three lines, FIBOS will sync block data automatically to mongoDB. Its very convieniant. 

The port number and database name can be changedm in this tutorial the port number is 27017, and the database name is eosmain. The following code is saved to `./local/node.js`. 

```javascript
var fibos = require('fibos');

fibos.load('http',{
    'http-server-address': '0.0.0.0:8888'
});
fibos.load('chain', {
    'contracts-console': true,
    'delete-all-blocks': true,
});
fibos.load('net');
fibos.load('chain_api');
fibos.load('history_api');
fibos.load('producer', {
    'producer-name': 'eosio',
    'enable-stale-production': true,
    'max-transaction-time': 3000
});
fibos.load('mongo_db', {
    'mongodb-uri': 'mongodb://localhost:27017/eosmain'
});

fibos.start();
```

Start FIBOS Runtime: 

```
fibos$ fibos ./local/node.js
```

After startup, we will see the following return in the mongd logs: 

```
2018-08-08T11:33:42.867+0800 I NETWORK  [listener] connection accepted from 127.0.0.1:54259 #2 (2 connections now open)
2018-08-08T11:33:42.868+0800 I NETWORK  [conn2] received client metadata from 127.0.0.1:54259 conn2: { driver: { name: 'mongoc / mongocxx', version: '1.10.2 / 3.3.1-pre' }, os: { type: 'Darwin', name: 'macOS', version: '18.0.0', architecture: 'x86_64' }, platform: 'cfg=0x00d6a265 posix=200112 stdc=201112 CC=clang 9.1.0 (clang-902.0.39.2) CFLAGS='' LDFLAGS=''' }
2018-08-08T11:33:42.873+0800 I STORAGE  [conn2] createCollection: eosmain.accounts with generated UUID: 0e553ab1-4c07-436a-abf7-62c6864779ed

...

2018-08-08T11:33:43.925+0800 I COMMAND  [conn2] command eosmain.$cmd command: createIndexes { createIndexes: 'actions', indexes: [ { name: 'trx_id_1', key: { trx_id: 1 } } ], $db: 'eosmain', lsid: { id: UUID('1ee67ce9-d0db-4ad1-9737-c4fba7f850ca') } } numYields:0 reslen:114 locks:{ Global: { acquireCount: { r: 1, w: 1 } }, Database: { acquireCount: { W: 1 } }, Collection: { acquireCount: { w: 1 } } } protocol:op_msg 119ms
2018-08-08T11:33:44.019+0800 I STORAGE  [conn2] createCollection: eosmain.transaction_traces with generated UUID: a637e777-aed4-45d2-9bf6-b149bc4e702b
```

Through the log we can see that FIBOS has done the following for us: 

1. Create collections: accounts, actions, block_states, transaction_traces, transactions 
2. Create the necessary indexes for each collection

We go into mongoDB's client mongo to query, and we see that the eosmain database was successfully created:

```
> show dbs
admin          0.000GB
config         0.000GB
eosmain        0.002GB
local          0.000GB
```

Going to the eosmain database, we find that FIBOS has created 5 collections in mongoDB: 

```
> use eosmain
switched to db eosmain
> show tables
accounts
actions
block_states
blocks
transaction_traces
transactions
```

We can directly query data from the accounts collection:

```
> db.accounts.find()
{ '_id' : ObjectId('5b6a6496bc9b452f1e4750d2'), 'name' : 'eosio', 'createdAt' : ISODate('2018-08-08T03:33:42.869Z') }
```

and will find that a system account eosio's data has already been synched to mongoDB. 