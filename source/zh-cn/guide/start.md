---
title: 快速入门
type:  tutorials
language: zh-cn
order: 5
---

搭建一个 FIBOS 开发环境需要安装 fibos 和 fibos.js，安装过程请参考 【[快速安装](./installation.html)】 章节。 

本章节示例代码的目录结构：

```
hello_fibos/
├── fibos_client
│   ├── call.js  //调用合约接口脚本文件
│   ├── initClient.js  //FIBOS连接文件
│   ├── deploy.js  //加载、发布合约脚本文件
│   ├── hello
│   │   ├── hello.abi  //合约abi文件
│   │   └── hello.js  //合约代码文件
│   └── package.json
└── start_fibos
    └── node.js
```

本章节示例代码地址：https://github.com/FIBOSIO/samples  下`basic`文件夹示例。

## 启动节点

**环境配置脚本**

创建 `start_fibos` 文件夹，保存如下代码至 `node.js`

```js
var fibos = require('fibos');

fibos.load('chain');
fibos.load('chain_api');
fibos.load('history_api');
fibos.load('producer', {
    'producer-name': 'eosio',
    'enable-stale-production': true
});
fibos.load('http', {
    'http-server-address': '0.0.0.0:8888'
});

fibos.load('net', {
    'p2p-listen-endpoint': '0.0.0.0:9876'
});
fibos.config_dir = 'fibos_config_dir/';
fibos.data_dir = 'fibos_data_dir/';
fibos.enableJSContract = true;
fibos.start();
```

运行 FIBOS 开发环境

```
hello_fibos$ fibos start_fibos/node.js
```

运行结果日志（部分）：

```
……
2018-07-30T03:29:01.004 thread-1   producer_plugin.cpp:1194      produce_block        ] Produced block 00000002e091c956... #2 @ 2018-07-30T03:29:01.000 signed by eosio [trxs: 0, lib: 0, confirmed: 0]
```

如果你看到了以上的消息，说明运行成功，`fibos` 已经开始区块生产。

## JavaScript 合约代码
>注意：需新建窗口，保证 node.js 节点正常运行

创建文件夹 `fibos_client`，保存如下代码至 `hello/hello.js`：

```js
exports.hi = user => console.error('in contract:', user);
```

## 合约 ABI 文件

保存如下代码至 `hello/hello.abi`：

```abi
{
    "version": "eosio::abi/1.0",
    "structs": [{
        "name": "player",
        "base": "",
        "fields": [{
            "name": "title",
            "type": "string"
        }, {
            "name": "age",
            "type": "int64"
        }]
    }, {
        "name": "hi",
        "base": "",
        "fields": [{
            "name": "user",
            "type": "name"
        }]
    }],
    "actions": [{
        "name": "hi",
        "type": "hi",
        "ricardian_contract": ""
    }]
}
```

## 连接 FIBOS 节点

在文件夹`fibos_client`下，新建 `initClient.js`，保存如下代码：

```javascript
var FIBOS = require('fibos.js');

function initClient(_keyProvider) {
    return FIBOS({
        chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
        keyProvider: _keyProvider, 
        httpEndpoint: 'http://127.0.0.1:8888',
        logger: {
            log: null,
            error: null
        }
    });
}

module.exports = initClient;
```

## 加载、发布合约脚本

在文件夹`fibos_client`下，新建 `deploy.js`，保存如下代码：

```js
var FIBOS = require('./initClient.js')
var fs = require('fs');
var config = {
    'public-key': 'FO6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV',
    'private-key': '5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3',
    'contractName': 'hello'
};

// new FIBOS client
var fibos = FIBOS(config['private-key']);
// create account hello
fibos.newaccountSync({
    creator: 'eosio',
    name: 'hello',
    owner: config['public-key'],
    active: config['public-key']
});
//setcode
var js_code = fs.readTextFile('./hello/hello.js');
fibos.setcodeSync(config['contractName'], 0, 0, fibos.compileCode(js_code));

//getcode
var code = fibos.getCodeSync(config['contractName'], true);
console.log('code:', code);

//setabi
var abi = JSON.parse(fs.readTextFile('./hello/hello.abi'));
fibos.setabiSync(config['contractName'], abi);
```

运行脚本：

```
hello_fibos$ fibos fibos_client/deploy.js
```

输出结果（部分）：

```
code: {
  "account_name": "hello",
  "code_hash": "383a12daacaf124eea9afc529822d990853b5b99570401b8394534b746ea3977",
  "wast": "",
  "wasm": "504b03042d00000008002cadfe4c6a9400a2360000003900000008001400696e6465782e6a7301001000000000000000000000000000000000004bad28c82f2a29d6cbc854b055282d4e2d52b0b55348cecf2bcecf49d54b2d2aca2fd250cfcc0389941425269758a9eb8055695a0300504b010200001400000008002cadfe4c6a9400a23600000039000000080000000000000001000000000000000000696e6465782e6a73504b0506000000000100010036000000700000000000"
}
```
备注：`wasm` 是一个低层级的、轻便式的字节码,它致力于实现接近原生的执行速度。

## 调用合约

使用 fibos.js 中的 API 去调用合约。

在文件夹`fibos_client`下，新建 `call.js`，保存如下代码：

```js
var FIBOS = require('./initClient.js')
var config = {
    'public-key': 'FO6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV',
    'private-key': '5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3',
    'contractName': 'hello'
};

// new FIBOS client
var fibos = FIBOS(config['private-key']);

//call abi
var ctx = fibos.contractSync(config['contractName']);
let i = ctx.hiSync('hello', {
    authorization: config['contractName']
});
console.log(i)
```

执行脚本：

```
hello_fibos$ fibos fibos_client/call.js
```

控制台打印结果如下：

```
{
  "broadcast": true,
  "transaction": {
    "compression": "none",
    "transaction": {
      "expiration": "2018-10-29T09:54:38",
      "ref_block_num": 45,
      "ref_block_prefix": 552314262,
      "max_net_usage_words": 0,
      "max_cpu_usage_ms": 0,
      "delay_sec": 0,
      "context_free_actions": [],
      "actions": [
        {
          "account": "hello",
          "name": "hi",
          "authorization": [
            {
              "actor": "hello",
              "permission": "active"
            }
          ],
          "data": "00000000001aa36a"
        }
      ],
      "transaction_extensions": []
    },
    "signatures": [
      "SIG_K1_JxKj8whii1gosSY6S5b3JcNxZ7x7xTUFkWg3fsjpiQ3K8eTfY6N8van5PqoUFYGJVRGNzdxapWLc6NAcieJgPCh8e8hkDA"
    ]
  },
  "transaction_id": "5d7262907ab645168f6a1fdd1e17988ca7f50a07d2ef6bb90f5891a6c2cb8bb9",
  "processed": {
    "id": "5d7262907ab645168f6a1fdd1e17988ca7f50a07d2ef6bb90f5891a6c2cb8bb9",
    "block_num": 47,
    "block_time": "2018-10-29T09:53:39.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 3510,
      "net_usage_words": 13
    },
    "elapsed": 7273,
    "net_usage": 104,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "hello",
          "act_digest": "35c685a9391997dfe62291f39ead19cde36bbfb29f411deb9019592ed6be5b4f",
          "global_sequence": 50,
          "recv_sequence": 1,
          "auth_sequence": [
            [
              "hello",
              3
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "hello",
          "name": "hi",
          "authorization": [
            {
              "actor": "hello",
              "permission": "active"
            }
          ],
          "data": {
            "user": "hello"
          },
          "hex_data": "00000000001aa36a"
        },
        "context_free": false,
        "elapsed": 7011,
        "cpu_usage": 0,
        "console": "in contract: hello\n",
        "total_cpu_usage": 0,
        "trx_id": "5d7262907ab645168f6a1fdd1e17988ca7f50a07d2ef6bb90f5891a6c2cb8bb9",
        "block_num": 47,
        "block_time": "2018-10-29T09:53:39.000",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "inline_traces": []
      }
    ],
    "except": null
  }
}
```
同时在 FIBOS 节点服务控制台显示 `trxs:1` 显示结果如下：
```
2018-8-30T14:28:22.005 thread-1   producer_plugin.cpp:1196      produce_block        ] Produced block 00000e57c573a33b... #3671 @ 2018-07-30T14:28:22.000 signed by eosio [trxs: 1, lib: 3670, confirmed: 0]
```

本章带领大家快速了解以及发布了一个简单的 JavaScript 合约，下面为大家准备了一个示例可以在【[教程](./tutorials-instructions.html)】章节中查阅。

