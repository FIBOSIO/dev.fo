---
title: Build local test node
type: tutorials
language: en
order: 11
---

>Note: **Please make sure to install FIBOS locally before setting up the node.** 
> **【[Install runtime environment](../installation/installation.html)】**

Start a local FIBOS node so that you can develop the specific content of FIBOS locally. In the actual development environment, you need to develop FIBOS nodes through the different plug-ins below.


Create a new `start_fibos` folder, and save the code to `start_fibos/node.js`:

```javascript
var fibos = require('fibos');
```


## Configure HTTP service 

http plugin 

For example: http-server-address can be used to configure the local service address, default value is 127.0.0.1:8888. 

```javascript
fibos.load('http', {
   'http-server-address':'0.0.0.0:8888'
});
```
**Specific http configuration information please see [http plugin](../../api/fibos/index.html#http插件)**


## Configure block info 

chain plugin 

For example: delete-all-blocks can be used to determine whether all state data and block data are deleted, with the default value is false.

```javascript
fibos.load('chain',{
   'delete-all-blocks':true
});
```

**Specific chain configuration information please see [chain plugin](../../api/fibos/index.html#chain插件)**


## Obtain P2P information

net plugin

p2p-listen-endpoint can be used to monitor the address and port of the p2p link, with the default value is 0.0.0.0:9876.

```javascript
fibos.load('net',{
   'p2p-listen-endpoint':'0.0.0.0:9876'
})
```
**Specific net configuration information see [net plugin](../../api/fibos/index.html#net插件)**


## Control block production information

producer plugin

producer-name：refers to the account name that control block production of nodes.

enable-stale-production：: enables the production of blocks, even if the block is static.

```javascript
fibos.load('producer', {
   'producer-name': 'eosio',
   'enable-stale-production': true
});
```
**Specific producer configuration information see [producer plugin](../../api/fibos/index.html#producer插件)**


## Modify and view FIBOS config and data directory

fibos.data_dir：refers to the data storage directory of fibos.

fibos.config_dir：refers to the config storage directory of fibos.

```javascript
fibos.config_dir = 'fibos_config_dir/';
fibos.data_dir = 'fibos_data_dir/';
```


## JS smart contract status

Boolean can be used to query and set the JavaScript smart contract status. When it is True, it can support JavaScript smart contracts.

```javascript
fibos.enableJSContract = true;
```


## Start node
```javascript
fibos.start();
```


## Advanced Config
- Modify FIBOS monitoring port and address

  Enable the HTTP service to monitor the 8889 Port of all addresses

  Enable the P2P service to monitor the 9877 Port of all addresses

```javascript
fibos.load('http', {
    'http-server-address': '0.0.0.0:8889'
});

fibos.load('net', {
    'p2p-listen-endpoint': '0.0.0.0:9877'
});
```

- Modify and view FIBOS config and data directory

```javascript
// View FIBOS config and data directory
console.notice('config_dir:', fibos.config_dir);
console.notice('data_dir:', fibos.data_dir);

// Modify FIBOS config and data directory
fibos.config_dir = 'fibos_config_dir/';
fibos.data_dir = 'fibos_data_dir/';
```

- Set the reset of environment data when the FIBOS service starts

```javascript
fibos.load('chain', {
    'delete-all-blocks': true
});
```

[Click here for more plugins](../../api/fibos/index.html)


## Node code example

The following code is stored to start_fibos/node.js, and used to start a local FIBOS node.

```javascript
var fibos = require('fibos');

fibos.load('http', {
   'http-server-address': '0.0.0.0:8888',
   "access-control-allow-origin": "*"
});
fibos.load('chain', {
   'delete-all-blocks': true
});
fibos.load('net');
fibos.load('chain_api');
// fibos.load('history_api');
fibos.load('producer', {
   'producer-name': 'eosio',
   'enable-stale-production': true
});
fibos.config_dir = 'start_fibos/fibos_config_dir/';
fibos.data_dir = 'start_fibos/fibos_data_dir/';
fibos.enableJSContract = true;
fibos.start();
```
> Note: In case of any problems in subsequent development and testing, please restart the FIBOS node service and try again!

Run the FIBOS development environment:

```
fibos-todomvc$ fibos start_fibos/node.js
```

Run results log (partial) 

```
fibos-todomvc$ fibos start_fibos/node.js
……
2018-07-30T03:29:01.004 thread-1   producer_plugin.cpp:1194      produce_block        ] Produced block 00000002e091c956... #2 @ 2018-07-30T03:29:01.000 signed by eosio [trxs: 0, lib: 0, confirmed: 0]
```

If you see the above, it means operation is successful and `fibos` has started block production. 

The GitHub source code of this article: `start_fibos` folder of  <https://github.com/fengluo/fibos-todomvc> 

**Next Chapter**
👉 【[Write ABI File](abi.html)】