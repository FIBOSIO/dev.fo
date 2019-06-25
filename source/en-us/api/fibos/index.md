---
title: 
type: fibos
language: en
order: 1
---

# FIBOS Module

fibos example objects

Usage：

```JavaScript
var fibos = require('fibos')
```

## Example attribute

### data_dir

Fibos data storage directory

Type：String

```JavaScript
fibos.data_dir = './fibos_data_dir';
```

### config_dir

fibos configuration directory

Type：String

```JavaScript
fibos.config_dir = './fibos_config_dir';
```

### core_symbol

fibos main token name

Type：String

```JavaScript
fibos.core_symbol = 'FO';
```

### pubkey_prefix

fibos public key prefix

Type：String

```JavaScript
fibos.pubkey_prefix = 'FO';
```

### enableJSContract

Query and set the JavaScript smart contract state, support JavaScript smart contracts when True

Type：Boolean

```JavaScript
fibos.enableJSContract = true;
```

## Example function

### load

loading load itself‘s contiguration

```JavaScript
fibos.load(cfgs);
```

Parameters：

- cfgs : Object ，adjust object.

load system plugin and configurations

```JavaScript
fibos.load( name, cfg );
```

Parameters：

- name : String ，system plugin name.
- cfg : Object ，Provide system plugin config.[Optional]

### start

start fibos

```JavaScript
fibos.start();
```

### stop

stop fibos

```JavaScript
fibos.stop();
```

## system plugin

>  Note: Please use system plugin with fibos.load example

### http plugin

start all RPC API on FIBOS node

Configurations：

| Config name                    | Config note                                         | default           | example |
| --------------------------- | ------------------------------------------------ | ---------------- | ------ |
| http-server-address         | local http server address                               | 127.0.0.1:8888   |        |
| https-server-address        | local https server address                              | -                |        |
| max-body-size               | maximum byte allowed for RPC request                             | 1024*1024(bytes) |        |
| verbose-http-errors         | show Http error log                         | false            |        |
| http-validate-host          | verify Http request host                              | true             |        |
| access-control-allow-origin | return special Access-Control-Allow-Origin for each request | -                | *      |

### chain plugin

Core plugin of FIBOS node, used to process and aggregate chain data

configurations：

| config name                     | config note                                                     | default      | example                                                       |
| ---------------------------- | ------------------------------------------------------------ | ----------- | ------------------------------------------------------------ |
| genesis-json                 | Specifies the genesis block data path                                          | -           | file path example file[FIBOS MainNet]https://github.com/FIBOS-Community/fibos-nodes/blob/master/genesis.json) |
| genesis-timestamp            | Overrides the initial timestamp in the genesis block                                     | -           | -                                                            |
| print-genesis-json           | Whether to print genesis data                                             | false       | -                                                            |
| fix-reversible-blocks        | Whether to restore the data to the irreversible height                                   | false       | -(unable to use)                                                  |
| replay-blockchain            | Whether to clear state data and then roll back all data                            | false       | -(Cannot be used, presumably for command line use?)                                |
| hard-replay-blockchain       | Whether to clear state data and then roll back as much data as possible from the block log          | false       | -                                                            |
| delete-all-blocks            | Whether to delete all state data and block data                             | false       | -                                                            |
| truncate-at-block            | stop producing,And roll back at the block height                                 | 0           | -(unable to use)                                                  |
| blocks-dir                   | Block data storage path                                            | blocks      | -                                                            |
| abi-serializer-max-time-ms   | rewrite default ABI serialization timeout                            | 15*1000(ms) | -                                                            |
| chain-state-db-size-mb       | The maximum capacity allowed in a block database                                   | 1024 (MB)   | -                                                            |
| chain-state-db-guard-size-mb | Nodes can be safely closed when the remaining data in the block database is less than this size       | 128(MB)     | -                                                            |
| reversible-blocks-db-size-mb | Maximum amount of data that can be rolled back                                         | 340(MB)     | -                                                            |
| contracts-console            | if print contract output                                             | false       | -                                                            |
| read-mode                    | mode database contains changes done up to the head block plus changes made by transactions not yet included to the blockchain mode database contains changes done up to the current head block. | speculative | -                                                            |

### net plugin

compose a network

configurations：

| config name                  | config note                         | default                      | example                                                       |
| ------------------------- | -------------------------------- | --------------------------- | ------------------------------------------------------------ |
| p2p-listen-endpoint       | listen address and port of p2p link        | 0.0.0.0:9876                | -                                                            |
| p2p-server-addrsss        | Provide p2p service address to other nodes      | p2p-listen-endpoint         | -                                                            |
| p2p-peer-address          | public p2p node address          | -                           | FIBOS TestNet [ 103.80.170.107:9876 ]                        |
| p2p-max-nodes-per-host    | Maximum number of clients that a single IP can connect to | 1                           | -                                                            |
| allowed-connection        | allow to connect                         | any                         | 'any'/'producers'/'specified'/'none'。if 'specified' ，Then the peer key must be specified at least once。if there is only 'producers' ，then the peer key is not required. |
| peer-private-key          | An array of public and private keys        |                             |                                                              |
| max-clients               | Maximum number of clients allowed to connect         | 25                          | 0: Unlimited                                                    |
| connection-cleanup-period | unavailable link clearing cycle               | 30(s)                       | -                                                            |
| network-version-match     | Whether the same version of the network is required           | false                       | -                                                            |
| peer-log-format           | Node log formatting                   | ["${name}" ${_ip}:${_port}] | -                                                            |

### chain_api plugin

make chain_plugin's function release to RPC API managed by http_plugin.

dependency：

- chain_plugin
- http_plugin

configurations：

| api         | request | note                     |
| ----------- | ---- | ------------------------ |
| get_info    | GET  | get info of node |
| get_block   | POST | get info of a block         |
| get_account | POST | get info of an account           |
| get_code    | POST | get code of smart contract         |

### producer plugin

Load necessary function required by block node.

configurations：

| config name                   | config note                      | default | example        |
| -------------------------- | ----------------------------- | ------ | ------------- |
| max-transaction-time       | Maximum transaction timeout              | 30(s)  | -             |
| greylist-account           | account unable to use CPU and NET    | -      | -             |
| enable-stale-production    | start production,even if it is static |        |               |
| max-irreversible-block-age | Maximum irreversible block time            | -1     | >1            |
| producer-name              | Control the account name of the node block          |        | eosio(Can be more parameters) |
| private-key                | The public and private keys of the signature program          |        | (can be more parameters)    |

### bnet plugin

provided a P2P protocol, uses very simple algorithm sync 2 chains permanently

configurations：

| config name                 | config note                                                     | default       | example |
| ------------------------ | ------------------------------------------------------------ | ------------ | ------ |
| bnet-endpoint:           | The endpoint of the incoming link to which are listening                                       | 0.0.0.0:4321 |        |
| bnet-follow-irreversible | Whether to accept only irreversible blocks from other endpoints                             | false        |        |
| bnet-threads             | Number of threads used to process network messages                                     |              |        |
| bnet-connect             | Remote endpoint connections to other nodes; According to the requirement to use multiple bnet-connect option to composite an network |              |        |
| bnet-no-trx              | This peer requests that other nodes have no pending transactions           | false        | false  |

## Example

**bp node**

```JavaScript
var fibos = require('fibos');
var fs = require("fs");
var isInit = false;

var producername = '';
var p2p_peer_address = [
    "se-p2p.fibos.io:9870",
    "sl-p2p.fibos.io:9870",
    "to-p2p.fibos.io:9870",
    "ca-p2p.fibos.io:9870",
    "ln-p2p.fibos.io:9870",
    "va-p2p.fibos.io:9870"
];

console.notice("start FIBOS producer nodes");

fibos.config_dir = "./fibos_config_dir";
fibos.data_dir = "./fibos_data_dir";

console.notice("config_dir:", fibos.config_dir);
console.notice("data_dir:", fibos.data_dir);

fibos.load("net", {
    "p2p-peer-address": p2p_peer_address,
    "p2p-listen-endpoint": "0.0.0.0:9870"
});

fibos.load("producer", {
    'producer-name': producername,
    'enable-stale-production': true,
    'private-key': [active_publickey, active_privateKey]
});
fibos.load("chain", {
    // "contracts-console": true,
    'chain-state-db-size-mb': 8 * 1024,
    'genesis-json': 'genesis.json'
});
//allow js contract
fibos.enableJSContract = true;

fibos.start();
```

**sync node**

```JavaScript
var fibos = require('fibos');
var fs = require("fs");

var producername = '';
var p2p_peer_address = [
    "se-p2p.fibos.io:9870",
    "sl-p2p.fibos.io:9870",
    "to-p2p.fibos.io:9870",
    "ca-p2p.fibos.io:9870",
    "ln-p2p.fibos.io:9870",
    "va-p2p.fibos.io:9870"
];

console.notice("start FIBOS ABI nodes");

fibos.config_dir = "./fibos_config_dir";
fibos.data_dir = "./fibos_data_dir";

console.notice("config_dir:", fibos.config_dir);
console.notice("data_dir:", fibos.data_dir);

fibos.load("http", {
    "http-server-address": "0.0.0.0:8870",
    "access-control-allow-origin": "*"
});

fibos.load("net", {
    "p2p-peer-address": p2p_peer_address,
    "p2p-listen-endpoint": "0.0.0.0:9870"
});

fibos.load("producer");

fibos.load("chain", {
    'chain-state-db-size-mb': 8 * 1024,
    'genesis-json': 'genesis.json'
});
fibos.load("chain_api");
fibos.load("history");
fibos.load("history_api");
//allow js contract
fibos.enableJSContract = true;

fibos.start();
```

#### genesis.json file

```JavaScript
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
    "initial_chain_id": "6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a"
}
```