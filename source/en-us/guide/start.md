---
title: Quick Start
type:  tutorials
language: en
order: 5
---

Building a FIBOS development environment requires installation of fibos and fibos.js. 

For installation proccess please see to 【[Quick Installation](./installation.html)】.  

The directory structure of the code example in this section is as follows:

```
hello_fibos/
├── fibos_client
│   ├── call.js  // Call contract interface script file
│   ├── initClient.js  //FIBOS connection file
│   ├── deploy.js  // Load, publish contract script file
│   ├── hello
│   │   ├── hello.abi  // Contract abi file
│   │   └── hello.js  // Contract code file 
│   └── package.json
└── start_fibos
    └── node.js
```

Find the sample code in this chapter here : https://github.com/FIBOSIO/samples under the `basic` folder.


## Start Node

**Environment configuration script**

Create `start_fibos` folder and save the codes to `node.js`

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

Run the FIBOS development environment:

```
hello_fibos$ fibos start_fibos/node.js
```

Run results log (part):

```
……
2018-07-30T03:29:01.004 thread-1   producer_plugin.cpp:1194      produce_block        ] Produced block 00000002e091c956... #2 @ 2018-07-30T03:29:01.000 signed by eosio [trxs: 0, lib: 0, confirmed: 0]
```

If you see the above message, it means operation is sucessful and `fibos` has started block production.


## JavaScript Contract Code 

> Note: A new window is required to ensure that node,js is operating normally.

Create folder `fibos_client`，and save the following code to `hello/hello.js`：

```js
exports.hi = user => console.error('in contract:', user);
```

## Contract ABI file

Save the following code to `hello/hello.abi`：

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

## Connect to FIBOS node

Create a new `initClient.js` under the folder of `fibos_client`, and save the following code: 

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

## Load and publish contract scripts

Create `deploy.js` under the folder of `fibos_client`, and save the following code: 

```js
var FIBOS = require('./initClient.js')
var fs = require('fs');
var config = {
    'public-key': 'your public key',
    'private-key': 'your private key',
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

Run the script：

```
hello_fibos$ fibos fibos_client/deploy.js
```

Output the results (part)：

```
code: {
  "account_name": "hello",
  "code_hash": "383a12daacaf124eea9afc529822d990853b5b99570401b8394534b746ea3977",
  "wast": "",
  "wasm": "504b03042d00000008002cadfe4c6a9400a2360000003900000008001400696e6465782e6a7301001000000000000000000000000000000000004bad28c82f2a29d6cbc854b055282d4e2d52b0b55348cecf2bcecf49d54b2d2aca2fd250cfcc0389941425269758a9eb8055695a0300504b010200001400000008002cadfe4c6a9400a23600000039000000080000000000000001000000000000000000696e6465782e6a73504b0506000000000100010036000000700000000000"
}
```

Notes: `wasm` is a kind of low-level and easy bytecode that is designed to achieve near-native execution speed.

## Call the contract

Use the API in fibos.js to call the contract. 

Create `call.js` under the folder of `fibos_client`, and save the following code: 

```js
var FIBOS = require('./initClient.js')
var config = {
    'public-key': 'your public key',
    'private-key': 'your private key',
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

Execute the scripts:

```
hello_fibos$ fibos fibos_client/call.js
```

Printed results by Console are as follows:

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

At the same time, the FIBOS node service console displays the `trxs:1`, and the displayed results are as follows:
```
2018-8-30T14:28:22.005 thread-1   producer_plugin.cpp:1196      produce_block        ] Produced block 00000e57c573a33b... #3671 @ 2018-07-30T14:28:22.000 signed by eosio [trxs: 1, lib: 3670, confirmed: 0]
```

This chapter gives you a quick understanding of JavaScript contract and a simple JavaScript contract. There is an example for you in the 【[Instructions](./tutorials-instructions.html)】.