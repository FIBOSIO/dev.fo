---
title: 权限
type: tutorials
order: 241
---

## 什么是权限

FIBOS 账户权限有2种： owner、active，一个账户必须“关联” owner、active 权限。

- owner 拥有超级权限，代表着账户的归属者，因为拥有此权限者可以用于操作其他权限配置，该权限常用事务中（转账、合约 action 等）一般不会使用。
- active 常用业务的权限，比如：转账、投票等。



## 账户和权限关系

### 创建 FIBOS 账户

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

//账户 hellofibos01的公私钥对
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

输出结果如下：

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

结果中 `permissions` 字段  owner、active 权限控制者确实是公钥 `FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR` 的拥有者。

### 分析账户与权限

截选部分执行脚本：

```javascript
fibos.newaccountSync({
    creator: 'eosio',
    name: name,
    owner: pubkey,
    active: pubkey
});
```

以上代码可以看到把 owner、active 权限的控制权限给了公钥 `FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR`，也就说此公钥对应的私钥拥有者，有 owner、active 的权限。

截选部分输出结果：

```bash
'ram_quota': -1,
'net_weight': -1,
'cpu_weight': -1,
```

使用 eosio 账户创建 hellofibos01，资源是无限的，所以 RAM、NET、CPU 资源都是 `-1`。其余创建的资源都是 `0`，0 代表没有资源。



## 配置权限

更改账户 hellofibos01 的 active 权限。

```javascript
var FIBOS = require('fibos.js');

//账户 hellofibos01 的公私钥对
let pubkey = 'FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR';
let prikey = '5KMx2vJR1L2rsrKuND4N6YM1gu26jwUjn5ZLorBeWnK15DfraQW';

//账户 hellofibos02 的公私钥对
let pubkey2 = 'FO5UFAzxUsbjQCijL5LtS6TaTtkJgPJACZ8qwDpXyLaW3sE9Ed2D';
let prikey2 = '5JhJaiRmvpR8MmvrxGFYGoC7tG9icYkooLFUdVMDJ5cAsLTbsob';

var name = 'hellofibos01';
var name2 = 'hellofibos02';

//创建 hellofibos02 账户

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


//修改hellofibos01 的active权限,客户端 需要更改为 hellofibos01 的私钥
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

输出结果如下：

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

以上代码新建了账户 hellofibos02，并且调用 `updateauthSync` 方法，进行权限变更操作。我们把 hellofibos01 的 active 权限转移给了公钥 `FO5UFAzxUsbjQCijL5LtS6TaTtkJgPJACZ8qwDpXyLaW3sE9Ed2D`。



## 多签

### 什么是多签

多签即多重签名, 我们在使用区块链进行授权操作时, 都是通过私钥进行签名的。

### 阈值和权重

阈值（threshold）是你可以动用账户所需的最小权限, 而权重（weight）则代表你该私钥所拥有的权限级别。

### 实例

**单签账户**

|  权限  |                       所属公钥                       | 权重 | 阀值 |
| :----: | :--------------------------------------------------: | :--: | :--: |
| owner  |                                                      |      |  1   |
|        | FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR |  1   |  -   |
| active |                                                      |      |  1   |
|        | FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR |  1   |  -   |

如表所示，如果要获得 owner 权限授权，拥有者的权重必须大于等于 owner 所对应的阈值，上面的示例 owner 的阈值是1，而所属公钥 `FO6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV` 的权重是1，所以这个所属公钥就可以直接获取 owner 进行操作。

active 权限同上面的解释,我们把这种只有一个所属公钥的账户理解为单签账户。

**多签账户**

要满足阀值的授权才能被正确签名。

|  权限  |                       所属公钥                       | 权重 | 阀值 |
| :----: | :--------------------------------------------------: | :--: | :--: |
| owner  |                                                      |      |  2   |
|        | FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR |  1   |  -   |
|        | FO5UFAzxUsbjQCijL5LtS6TaTtkJgPJACZ8qwDpXyLaW3sE9Ed2D |  1   |  -   |
| active |                                                      |      |  1   |
|        | FO5dZut9MG9ZdqrT1WYdPkp1Txxi6JLRYEgYCtAUDWH6ymNqdJpR |  1   |  -   |

如表所示，要想获得 owner 权限，必须2个所属公钥同时授权才可以获得。

