---
title: Permission
type: tutorials
language: en
order: 242
---

## What is permission

There are 2 types of FIBOS account permissions： owner、active. An account must be “associated” with owner、active permissions.

- owner: 
Has super privileges. Represents the owner of the account. Because the owner of this permission can operate the other permissions' configuration, this permission is commonly used in transactions (Transfer, contract action, etc) It is not usually used.

- active: 
Common business permissions，Exp：transfer，vote，etc.



## Relationships Between Account and Permission 

### Create FIBOS account

```javascript
var FIBOS = require('fibos.js');

var fibos = FIBOS({
  chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
  keyProvider: '5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3',
  httpEndpoint: 'http://127.0.0.1:8888',
  logger: {
    log: null,
    error: null
  }
});

//Account hellofibos01 public key to
let pubkey = 'FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR';
let prikey = '5KMx2vJR1L2rsrKuND4N6YM1gu26jwUjn5ZLorBeWnK15DfraQW';

var name = 'hellofibos01';
fibos.newaccountSync({
  creator: 'helloeosio12',
  name: name,
  owner: pubkey,
  active: pubkey
});

var c = fibos.getAccountSync(name);
console.notice(c);
```

Result：

```bash
{
  'account_name': 'hellofibos01',
  'head_block_num': 10,
  'head_block_time': '2018-08-21T09:58:50.500',
  'privileged': false,
  'last_code_update': '1970-01-01T00:00:00.000',
  'created': '2018-08-21T09:58:51.000',
  'ram_quota': -1,
  'net_weight': -1,
  'cpu_weight': -1,
  'net_limit': {
    'used': -1,
    'available': -1,
    'max': -1
  },
  'cpu_limit': {
    'used': -1,
    'available': -1,
    'max': -1
  },
  'ram_usage': 2724,
  'permissions': [
    {
      'perm_name': 'active',
      'parent': 'owner',
      'required_auth': {
        'threshold': 1,
        'keys': [
          {
            'key': 'FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR',
            'weight': 1
          }
        ],
        'accounts': [],
        'waits': []
      }
    },
    {
      'perm_name': 'owner',
      'parent': '',
      'required_auth': {
        'threshold': 1,
        'keys': [
          {
            'key': 'FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR',
            'weight': 1
          }
        ],
        'accounts': [],
        'waits': []
      }
    }
  ],
  'total_resources': null,
  'self_delegated_bandwidth': null,
  'refund_request': null,
  'voter_info': null
}
```

For the string `permissions` in the result, owner、active permission controller is indeed the owner of public key: `FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR` .

### Analyze Accounts and Permissions

Select part of the execution script:

```javascript
fibos.newaccountSync({
    creator: 'eosio',
    name: name,
    owner: pubkey,
    active: pubkey
});
```

the codes above transferred owner, active permissions to the public key `FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR`. That is to say the private key owner corresponding to the public key has owner, active permissions.

Select the part of the execution script:

```bash
'ram_quota': -1,
'net_weight': -1,
'cpu_weight': -1,
```

Use eosio account to create hellofibos01，the resources is unlimited，so RAM、NET、CPU are all `-1`. The rest of resources we created are all `0`，0 represents no resources.



## Permission Configuration

Change the active permission of account hellofibos01.

```javascript
var FIBOS = require('fibos.js');

//Public and private key pair of hellofibos01
let pubkey = 'FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR';
let prikey = '5KMx2vJR1L2rsrKuND4N6YM1gu26jwUjn5ZLorBeWnK15DfraQW';

//Public and private key pair of hellofibos02 
let pubkey2 = 'FO5UFAzxUsbjQCijL5LtS6TaTtkJgPJACZ8qwDpXyLaW3sE9Ed2D';
let prikey2 = '5JhJaiRmvpR8MmvrxGFYGoC7tG9icYkooLFUdVMDJ5cAsLTbsob';

var name = 'hellofibos01';
var name2 = 'hellofibos02';

//create hellofibos02 account

var fibos = FIBOS({
  chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
  keyProvider: '5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3',
  httpEndpoint: 'http://127.0.0.1:8888',
  logger: {
    log: null,
    error: null
  }
});
fibos.newaccountSync({
  creator: 'eosio',
  name: name2,
  owner: pubkey2,
  active: pubkey2
});


//Change the active permission of hellofibos01, Client needs to change to the private key of hellofibos01.
fibos = FIBOS({
  chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
  keyProvider: '5KMx2vJR1L2rsrKuND4N6YM1gu26jwUjn5ZLorBeWnK15DfraQW',
  httpEndpoint: 'http://127.0.0.1:8888',
  logger: {
    log: null,
    error: null
  }
});

let ctx = fibos.contractSync('eosio');
ctx.updateauthSync({
  account: name,
  permission: 'active',
  parent: 'owner',
  auth: {
    threshold: 1,
    keys: [{
      key: 'FO5UFAzxUsbjQCijL5LtS6TaTtkJgPJACZ8qwDpXyLaW3sE9Ed2D',
      weight: 1
    }]
  }
});

var c = fibos.getAccountSync(name);
console.notice(c);
```

Results:

```bash
{
  'account_name': 'hellofibos01',
  'head_block_num': 66,
  'head_block_time': '2018-08-21T09:59:18.500',
  'privileged': false,
  'last_code_update': '1970-01-01T00:00:00.000',
  'created': '2018-08-21T09:58:51.000',
  'ram_quota': -1,
  'net_weight': -1,
  'cpu_weight': -1,
  'net_limit': {
    'used': -1,
    'available': -1,
    'max': -1
  },
  'cpu_limit': {
    'used': -1,
    'available': -1,
    'max': -1
  },
  'ram_usage': 2724,
  'permissions': [
    {
      'perm_name': 'active',
      'parent': 'owner',
      'required_auth': {
        'threshold': 1,
        'keys': [
          {
            'key': 'FO5UFAzxUsbjQCijL5LtS6TaTtkJgPJACZ8qwDpXyLaW3sE9Ed2D',
            'weight': 1
          }
        ],
        'accounts': [],
        'waits': []
      }
    },
    {
      'perm_name': 'owner',
      'parent': '',
      'required_auth': {
        'threshold': 1,
        'keys': [
          {
            'key': 'FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR',
            'weight': 1
          }
        ],
        'accounts': [],
        'waits': []
      }
    }
  ],
  'total_resources': null,
  'self_delegated_bandwidth': null,
  'refund_request': null,
  'voter_info': null
}
```

The codes above created hellofibos02，and called `updateauthSync` method to do permission change operation. We transferred active permiision of hellofibos01 to the public key.`FO5UFAzxUsbjQCijL5LtS6TaTtkJgPJACZ8qwDpXyLaW3sE9Ed2D`.



## Multiple Signature

### What is Multiple Signature?

Multiple signiture means signing multiple times. While we use blockchain to do authorized operations, the private key is used to sign all. 

### Thresholds and Weights

Threshold is the minimum permission you need to access an account. Weight represents the permission level owned by your private key.

### Example

**Single Signature Account**

|  permission  |                       Public Key                     | Weight | Threshold |
| :----------: | :--------------------------------------------------: | :----: | :-------: |
|     owner    |                                                      |        |     1     |
|              | FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR |    1   |     -     |
|    active    |                                                      |        |     1     |
|              | FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR |    1   |     -     |

As the table above shows，if you want to get owner permission，the weight of the owner must be greater than or equal to the threshold corresponding to the owner，the example above shows the threshold of owner is 1，and the weight of public key `FO6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV` is 1. Therefore, the owner of the public key can be directly obtained for operation.

Active permissions are the same as explained above, we understand this type of account that only has one public key as the single signature account.

**Multi-Signature Account**

For correct signature, must satisfy the threshold authorization

|  Permission  |                       Public Key                     | Weight | Threshold |
| :----------: | :--------------------------------------------------: | :----: | :-------: |
|    owner     |                                                      |        |     2     |
|              | FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR |    1   |     -     |
|              | FO5UFAzxUsbjQCijL5LtS6TaTtkJgPJACZ8qwDpXyLaW3sE9Ed2D |    1   |     -     |
|    active    |                                                      |        |     1     |
|              | FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR |    1   |     -     |

As the table above shows，if you want to get owner permission，two public keys must be authorized at the same time.

