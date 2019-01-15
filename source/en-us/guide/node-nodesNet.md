---
title: Add to nodes network 
type: tutorials
language: en
order: 301
---

In the last chapter, we introduced FIBOS' node network. Now, we will join in as a node, and feel the charm of the blockchain. 


## fibos-nodes

fibos-nodes is a scripting tool provided by the FIBOS community, used to quick start FIBOS main net nodes. It can help developers quick start three different types of nodes. 

Project link: https://github.com/FIBOS-Community/fibos-nodes


### Installation 

```
git clone https://github.com/FIBOS-Community/fibos-nodes.git
cd fibos-nodes
```

### Start Up

```
fibos bp.js   // Quick start a BP node 

fibos full.js // Quick start a full node 

fibos seed.js // Quick start a sync node
```

The default data & config storage location is /blockData/data

### Full node data synchronization

Full node block data synchronization takes a long time, so the FIBOS community provides the latest mirror start serive to significantly reduce the block synch time. 

Server address: http://ghost.bp.fo/


#### Usage

1. Download data: 

    Visit http://ghost.bp.fo/ghost/ and select the data packs you want to synch, and click download. 

    Or obtain the file URL, and use WGET to perform download. 

   ```
   weget http://ghost.bp.fo/ghost/data_15600397.tar.gz
   ```

2. Uncompress files：

   ```
   tar -zxvSf data.tar.gz
   ```

3. Edit quick start script config file config.json : 

   Direct the data_dir parameters to the fibos-data directory from the uncompressed data files. 

   ```json
   "data_dir": "fibos-data/",
   ```

4. Start full node

   ```
   fibos full.js
   ```

## Manual entry to FIBOS node network 

If you dont use the fibos-node tool to start a node, you can also edit the start script yourself to enter into the node network. 

Entering the FIBOS network confi requires and involves a few key info: 


#### Obtain the node network chainId

TestNet：

```
chainId : '68cee14f598d88d340b50940b6ddfba28c444b46cd5f33201ace82c78896793a'
```

FIBOS Main Net：

```
chainId : '6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a'
```

#### Provide the P2P listening address and interface 

```
'p2p-listen-endpoint' : '0.0.0.0:9870'
```

#### Block data synch target node information 

Block data synch must first synch data from current running BP nodes. 

Currently, the TestNet BP node will be provided by the FIBOS foundation, the p2p address is p2p-testnet.fibos.fo:9870 and p2p-testnet-02.fibos.fo:9870

```
'p2p-peer-address' : ['p2p-testnet.fibos.fo:9870','p2p-testnet-02.fibos.fo:9870']
```

FIBOS Main Net nodes have already all been replaced by community nodes, for specific BP node info, please visit https://www.fibos123.com/#!/bp

```
'p2p-peer-address' : ['p2p.mainnet.fibos.me:80','seed-mainnet.fibscan.io:9103']
```

Note: the FIBOS Main Net BP P2P address demonstrated will variable, so please pay attention.  

#### genesis.json File

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

FIBOS Main Net：

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

### How to becojme a synch node 

If the node is only a synch of FIBOS block data, it is very easy. Save the following codes to 
`sync_node.js`: 

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

In the codes above, `net` module's `p2p-peer-address` is a variable value, so please pay attention to change it. 

Run synch node: 

```
fibos sync_node.js
```

## How to become a BP node

(* BP Block Producer)

> Important Note: Use Producer ID to initiate registration application, producer key is best different from active key! 

- Config Producer information to start FIBOS node servies
- Use Producer ID to initialize registration application
- Initialize voting to become a Producer. 


### Config Producer info to start FIBOS node services 

Only if the number of votes reach a certain amount, will a FIBOS node really become a Producer, having rights to block production. Other situations are merely for existence of ID for synch block data

The following codes realize config of a Producer, saving the codes to `producer_node.js`:

```javascript
var fibos = require('fibos');
var fs = require('fs');
var config = {
	'producer-name': 'producer-name',
	'public-key': 'producer public key',
	'private-key': 'producer private key'
};


console.notice('Starting FIBOS name:', config['producer-name']);
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

Explanation for varaiable configs in the codes above: 

```javascript
var config = {
	'producer-name': 'producer-name', // producer name
	'public-key': 'producer public key', // producer public key
	'private-key': 'producer private key' // producer private key
};
```

Run a Producer node: 

```
fibos producer_node.js
```

### Use Producer ID to initialize registration application 

**Call Method：** 

```javascript
// Initialize a fibos client
var ctx = fibos.contractSync('eosio');
var a = ctx.regproducerSync('prducerName', 'publickey', 'url', 'location');
```

**Method Clarification：**

Use fibos.js client to call eosio contract to initialize registration of BP operations 

**Example：**

The following coves are saved to `register_bp.js` :

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

**Example Clarification:**

In the example, after configuring the FIBOS MainNe and FIBOS RPC address and FIBOS private key, initializes a FIBOS client, calling `regproducerSync` to pass four parameters: 

| Parameter         | Explanation                                        |
| ----------------- | -------------------------------------------------- |
| producerName      | Block Producer Account Name                        |
| publicKey         | Block Producer Public Key                          |
| url               | Blopck Producer Public Website                     |
| location          | Block Producer Server Address and Location Code    |

### Obtain votes to become Producer

To become BP requires a certain amount of votes, you can let others vote for you, or vote for yourself. Voting requires mortgaging FO to obtain resources. Here we will explain how to mortgage for resources and how to vote. 

#### Mortgage resources 

**Call Method：**

```javascript
//Initialize a fibos client
var ctx = fibos.contractSync('eosio');
var a = ctx.delegatebwSync({
	from: 'buyer_name',
	receiver: 'recevier_name',
	stake_net_quantity: 'quality',
	stake_cpu_quantity: 'quality',
	transfer: 0
});
```

**Method Clarification：**

Use `delegatebwSync` method to mortgage FO to get NET and CPU resources, used for voting.

**Example：**

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
	from: 'fibos account', // Mortgagor's account 
	receiver: 'fibos account', // Resource recipient account 
	stake_net_quantity: '1.0000 FO',
	stake_cpu_quantity: '1.0000 FO',
	transfer: 0
});
```

**Example Clarification:**

By configuring FIBOS Main Net chainId and Http Server address, initializes a FIBOS client, calling `delegatebwSync` method, mortgaging FO to obtain resources.  

| Parameter          | Explanation                                                         |
| ------------------ | ------------------------------------------------------------------- |
| from               | Mortgagor                                                           |
| receiver           | Resource Recipient                                                  |
| stake_net_quantity | Num of FO Mortgaged to obtain NET                                   |
| stake_cpu_quantity | Num of FO Mortgaged to obtain CPU                                   |
| transfer           | 0: Means using own resource to mortgage for others 1: Represents giving resource to others and mortgaging them. Note: When you are mortaging resource for yourslef, can only input 0                                                                 |


#### Perform Voting

**Call Method：**

```javascript
//Initialize a FIBOS client
var ctx = fibos.contractSync('eosio');
var a = ctx.voteproducerSync('voter', 'proxy', 'producers');
```

**Method Clarification：**

 Use `voteproducerSync` method to vote for BP. 

**Example：**

Following codes are saved to `vote_bp.js`

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
 
var fibosnodes = ['fibosbpnodec','fibosbpnodeb','fibosbpnodea']; // 
Specific account data requires developer to write in according to actual situation 

fibosnodes.sort()；

var a = ctx.voteproducerSync('fibostest123', '', fibosnodes); // 
Specific account data requires developer to write in according to actual situation 
```

**Example Clarification：**


In the codes above, the user `fibostest123` votes for `fibosbpnodea, fibosbpnodeb, fibosbpnodec`, the node vote list requires the developer to organize alphabetically, and the one time max is voting for 30 BP. The empty parameter represents an agent. If left empty it means voting for BP directly, if filled in represents voting through an agent to BP.  

Perform Voting:

```
fibos vote_bp.js
```

Note: After voting is completed, a rank in the TOP 21 is required to be selected as block producer BP. 

### Claim Rewards 

Producing a block as BP will earn rewards. One can use the following interface to claim the rewards: 

**Call Method：**

```javascript
//Initialize a FIBOS client
var a = fibos.claimrewardsSync('producer');
```

**Method Clarification：**

 Use `claimrewardsSync` method to claim BP rewards. 

**Example：**

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
var a = fibos.claimrewardsSync('fibosbpnode1') //
Specific account data requires developer to write in according to actual situation 
```

**Example Clarification：**

The above codes shows `fibosbpnode1` claiming rewards for its own block production! 
