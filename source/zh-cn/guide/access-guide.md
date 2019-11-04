---
title: FO 接入安全指南
type: tutorials
language: zh-cn
order: 400
---


该指南旨在帮助各项目方完成与 FO 通证的安全对接，保障各项目方 FO 充提业务的安全稳定以及 FIBOS 节点的安全。

## 交易所充值提现接入方案

### 基本逻辑

**充值：** 交易所需要给交易所中充值的账户生成平台内唯一的可识别标识，用户充值至交易所账户时需在转账操作的 memo 字段中填入交易所平台为该用户生成的唯一标识。

**提现：** 用户提现时填入自己的 FIBOS 账户，交易所通过转账方式将用户所提现 FO 的数量转给用户所填账户名，从而完成提币。在此过程中，memo 字段可能也是必要的，因为用户有可能从一交易所提现至另一交易所。

### 注意事项

> FIBOS 上 FO 的充提币逻辑与 EOS 主网基本一致，但其中的不同之处需要各大交易所提起注意：

#### FIBOS 的转账类型：

FIBOS 网络中的转账函数分为两种：`transfer` 和 `extransfer`

**transfer**

其中  `transfer` 函数表示的是转账方法，函数原型为：

```javascript
void transfer(account_name from, account_name to, asset quantity, string memo)
```

示例：

```javascript
transfer('accountfrom', 'accountto', '1.0000 FO', 'memo field')
```

在链上获取到的 action 示例为：

```bash
{
  "timestamp": "2019-03-20T02:20:05.000",
  "producer": "lijialintest",
  "confirmed": 0,
  "previous": "021472cd66b01c2ee4b43d2980713df90b4c6f67b025b32556e7177c1a130e64",
  "transaction_mroot": "a321fade674c1e0d0dbe0dadf003c38768356ce608874b79dde7ca4174330436",
  "action_mroot": "32e5ac06a722acad9d89ae068957e3e8aa83a114b739d7e728f8d04d57d267fe",
  "schedule_version": 334,
  "new_producers": null,
  "header_extensions": [],
  "producer_signature": "SIG_K1_KWgntpfkMjR52MC8NTJ4o6rE9pe3ZUEG7Q1ioFFRYfUBTcPYPDgucKVzZiCe293aU3yJhJMRR7pBBGwMasaQ4AbbK5KTjK",
  "transactions": [
    {
      "status": "executed",
      "cpu_usage_us": 568,
      "net_usage_words": 18,
      "trx": {
        "id": "183416881a4eb8e45da548d429eff1566d5416d6fb53cf5a5ec2f56e942a95e0",
        "signatures": [
          "SIG_K1_K7Qc7GbKyhpwaGKB8ZgtXKkk8ei2RJhBZ6vRTXrycSXYtNneyDpTes87vGGDP12EXkCBJjcXiVKfjBgig4neQinQkr7hqp"
        ],
        "compression": "none",
        "packed_context_free_data": "",
        "context_free_data": [],
        "packed_trx": "8fa3915c81712c0f4f49000000000100a6823403ea3055000000572d3ccdcd01504f520a514c8f5b00000000a8ed323233504f520a514c8f5b204408d3683f8dee817fcf000000000004464f0000000000125468616e6b7320666f7220737570706f727400",
        "transaction": {
          "expiration": "2019-03-20T02:21:03",
          "ref_block_num": 29057,
          "ref_block_prefix": 1229917996,
          "max_net_usage_words": 0,
          "max_cpu_usage_ms": 0,
          "delay_sec": 0,
          "context_free_actions": [],
          "actions": [
            {
              "account": "eosio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "accountfrom",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "accountfrom",
                "to": "accountto",
                "quantity": "1.0000 FO",
                "memo": "memo field"
              },
              "hex_data": "504f520a514c8f5b204408d3683f8dee817fcf000000000004464f0000000000125468616e6b7320666f7220737570706f7274"
            }
          ],
          "transaction_extensions": []
        }
      }
    }
  ],
  "block_extensions": [],
  "id": "021472cefdf8687fcf4b21560c5d4b0d660eb499e40722bbaeea28b7c5d74c71",
  "block_num": 34894542,
  "ref_block_prefix": 1445022671
}
```

**extransfer：**

其中 `extransfer` 函数表示的是与 FIBOS 主网扩展的转账方法，该方法支持在 FIBOS 上发行的所有通证的转账，函数原型为：

```javascript
void extransfer(account_name from, account_name to, extended_asset quantity, string memo)
```

示例：

```javascript
extransfer('accountfrom', 'accountto', '1.0000 FO@eosio', 'memo field')
```

其中，@ 字符后表示的是该通证的发行方，系统通证 FO 为 FO@eosio，eosio 表示的是该通证是系统原生发行的通证。

在链上获取到的 action 示例为：

```bash
{
  "timestamp": "2019-03-20T01:09:45.000",
  "producer": "fibos123comm",
  "confirmed": 0,
  "previous": "021451fbb65c4e1e657eeea22de95dd3b78fc2c1a5dcd82e0eef87e594b63e43",
  "transaction_mroot": "803bd6b19aa480d78195fd950c336a60d2a6d03d6c9639b29b2023dea65cec7c",
  "action_mroot": "c5c7cf621fa707e37ef2cb4fe26f40217056583e92a6340b210708a365b0700b",
  "schedule_version": 334,
  "new_producers": null,
  "header_extensions": [],
  "producer_signature": "SIG_K1_KWgbyfa68s7XisFW37xA8RobkA9NZAVcdSqWRNmcyfkv1NdoZdg4Ux3phnLn713kYwLk8sAM2a8TFzJCyCvjyfy7HEA6yz",
  "transactions": [
    {
      "status": "executed",
      "cpu_usage_us": 524,
      "net_usage_words": 17,
      "trx": {
        "id": "7a3fcf6b41a314139004c523e051105761baa410727b7daf811c9a66d15d73d8",
        "signatures": [
          "SIG_K1_KAcz3Z2Yd7NCAdW4TA3RFLPESz6RJoNzjbF8SSpXtXxFWeDsYFb5AHob3TRDqNPM6NCUTzq3hT7FHNJ2VyaXwLYcEF42ek"
        ],
        "compression": "none",
        "packed_context_free_data": "",
        "context_free_data": [],
        "packed_trx": "0a93915c9a501d9a32be000000000100a6823403ea305500c0550b4f7373570130c455d85c95318d00000000a8ed32322930c455d85c95318d20c255d85c95318d102700000000000004464f00000000000000000000ea30550000",
        "transaction": {
          "expiration": "2019-03-20T01:10:34",
          "ref_block_num": 20634,
          "ref_block_prefix": 3190987293,
          "max_net_usage_words": 0,
          "max_cpu_usage_ms": 0,
          "delay_sec": 0,
          "context_free_actions": [],
          "actions": [
            {
              "account": "eosio.token",
              "name": "extransfer",
              "authorization": [
                {
                  "actor": "accountfrom",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "accountfrom",
                "to": "accountto",
                "quantity": {
                  "quantity": "1.0000 FO",
                  "contract": "eosio"
                },
                "memo": "memo field"
              },
              "hex_data": "30c455d85c95318d20c255d85c95318d102700000000000004464f00000000000000000000ea305500"
            }
          ],
          "transaction_extensions": []
        }
      }
    }
  ],
  "block_extensions": [],
  "id": "021451fcb2c4621ffd29f10205e88e7d815f7e0952af0b1acbe2231cde4043bd",
  "block_num": 34886140,
  "ref_block_prefix": 49359357
}

```

> **注意：**
>  **FO 通证的转账支持上述两种转账方法，因此为防止用户充值记录的丢失，交易所需要对上述两种转账方法提供支持。**



## 交易所充提业务安全指南

该部分内容总结了在交易所对接 FO 业务时可能遭受的一系列攻击，并且给出了对应的安全解决方案。

### 不可逆高度判断

由于 FIBOS 公链的使用了 DPOS 的共识机制，在判断一笔转账（一笔 Transaction）是否可信需要对当前转账动作所在的块高度进行判断。在 FIBOS 网络中，一笔交易所在的高度如果在不可逆高度之内，我们就可以认定该交易已经被 FIBOS 网络中的 BP（Block Producer）节点所确认，进入了不可逆状态，不可被回滚。

因此交易所在判断一笔用户充值交易是否有效时，需要判断该转账所在高度小于当前 FIBOS 的不可逆高度，获取 FIBOS 的不可逆高度可以通过 fibos.js 客户端或者 RPC 获取链上基本信息：

```bash
{
  "server_version": "a09083c8",
  "chain_id": "6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a",
  "head_block_num": 34904892,
  "last_irreversible_block_num": 34904564,
  "last_irreversible_block_id": "021499f464cdb1a97f3ec896cda2ddb889b1aaba256b5f4d6d0e6c0e9c72ef4e",
  "head_block_id": "02149b3c233fc770517a8a9afc49496b28d883bc57f1f2757fd65156c18e0fbe",
  "head_block_time": "2019-03-20T03:47:14.500",
  "head_block_producer": "fibos123comm",
  "virtual_block_cpu_limit": 200000000,
  "virtual_block_net_limit": 1048576000,
  "block_cpu_limit": 199900,
  "block_net_limit": 1048576,
  "server_version_string": "v1.5.4.1"
}
```

其中的 `last_irreversible_block_num` 字段表示的即为 FIBOS 网络当前的最新不可逆高度。

一笔交易从被打包进某区块的状态变为不可逆状态大概需要耗费 164 秒，因此该时间即为用户充值到账的延迟时间。

### "假币"充值

因为 FIBOS 公链上有众多用户都发行了自己的通证，如果交易所的业务处理不慎，会导致有用户自行发行的通证充值进入交易所参与交易，我们称这种攻击为“假币充值”，对于这种假币充值行为，交易所需要在充值业务中做好防范。

对于 `transfer` 转账（ action.name 为 transfer ）来说，示例如下：

```bash
"actions": [
    {
      "account": "eosio.token",
      "name": "transfer",
      "authorization": [
        {
          "actor": "accountfrom",
          "permission": "active"
        }
      ],
      "data": {
        "from": "accountfrom",
        "to": "accountto",
        "quantity": "1.0000 FO",
        "memo": "memo field"
      },
      "hex_data": "504f520a514c8f5b204408d3683f8dee817fcf000000000004464f0000000000125468616e6b7320666f7220737570706f7274"
    }
  ]
```

需要判断：

- `action.account ` 必须为 'eosio.token'
- `actions.data.to` 必须为交易所充值账户名
- `actions.data.quantity` 必须为 'xxx.xxxx FO'

对于 `extransfer` 转账（ action.name 为 extransfer）来说，示例如下：

```bash
 "actions": [
    {
      "account": "eosio.token",
      "name": "extransfer",
      "authorization": [
        {
          "actor": "accountfrom",
          "permission": "active"
        }
      ],
      "data": {
        "from": "accountfrom",
        "to": "accountto",
        "quantity": {
          "quantity": "1.0000 FO",
          "contract": "eosio"
        },
        "memo": "memo field"
      },
      "hex_data": "30c455d85c95318d20c255d85c95318d102700000000000004464f00000000000000000000ea305500"
    }
  ]
```

需要判断：

- `action.account ` 必须为 'eosio.token'
- `actions.data.to` 必须为交易所充值账户名
- `actions.data.quantity` 必须为 'xxx.xxxx FO'
- `actions.data.quantity.contract` 必须为 'eosio'

### Hard - failed 状态攻击

FIBOS 链上交易的执行状态存在多种，其中有一种状态为 hard-failed，处于这种状态下的交易的特点是，没有被成功执行，但是依旧在链上留下了记录，攻击者可以利用 FIBOS 的这一交易特性对交易所造成威胁，从而进行虚假充值。对这一安全威胁的防范办法是，在不可逆高度的基础上，对交易的状态进行判断，如果发现充值交易的状态是 `hard-failed` 则认定为是假充值。对于以下的示例交易来说，交易所应当判断：**transactions.status** 为 **executed**。只有处于 `executed` 状态并且已经在不可逆高度下的交易才能认定是真实、不可篡改的充值记录。

```bash
{
  "timestamp": "2019-03-20T01:09:45.000",
  "producer": "fibos123comm",
  "confirmed": 0,
  "previous": "021451fbb65c4e1e657eeea22de95dd3b78fc2c1a5dcd82e0eef87e594b63e43",
  "transaction_mroot": "803bd6b19aa480d78195fd950c336a60d2a6d03d6c9639b29b2023dea65cec7c",
  "action_mroot": "c5c7cf621fa707e37ef2cb4fe26f40217056583e92a6340b210708a365b0700b",
  "schedule_version": 334,
  "new_producers": null,
  "header_extensions": [],
  "producer_signature": "SIG_K1_KWgbyfa68s7XisFW37xA8RobkA9NZAVcdSqWRNmcyfkv1NdoZdg4Ux3phnLn713kYwLk8sAM2a8TFzJCyCvjyfy7HEA6yz",
  "transactions": [
    {
      "status": "executed",
      "cpu_usage_us": 524,
      "net_usage_words": 17,
      "trx": {
        "id": "7a3fcf6b41a314139004c523e051105761baa410727b7daf811c9a66d15d73d8",
        "signatures": [
          "SIG_K1_KAcz3Z2Yd7NCAdW4TA3RFLPESz6RJoNzjbF8SSpXtXxFWeDsYFb5AHob3TRDqNPM6NCUTzq3hT7FHNJ2VyaXwLYcEF42ek"
        ],
        "compression": "none",
        "packed_context_free_data": "",
        "context_free_data": [],
        "packed_trx": "0a93915c9a501d9a32be000000000100a6823403ea305500c0550b4f7373570130c455d85c95318d00000000a8ed32322930c455d85c95318d20c255d85c95318d102700000000000004464f00000000000000000000ea30550000",
        "transaction": {
          "expiration": "2019-03-20T01:10:34",
          "ref_block_num": 20634,
          "ref_block_prefix": 3190987293,
          "max_net_usage_words": 0,
          "max_cpu_usage_ms": 0,
          "delay_sec": 0,
          "context_free_actions": [],
          "actions": [
            {
              "account": "eosio.token",
              "name": "extransfer",
              "authorization": [
                {
                  "actor": "accountfrom",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "accountfrom",
                "to": "accountto",
                "quantity": {
                  "quantity": "1.0000 FO",
                  "contract": "eosio"
                },
                "memo": "memo field"
              },
              "hex_data": "30c455d85c95318d20c255d85c95318d102700000000000004464f00000000000000000000ea305500"
            }
          ],
          "transaction_extensions": []
        }
      }
    }
  ],
  "block_extensions": [],
  "id": "021451fcb2c4621ffd29f10205e88e7d815f7e0952af0b1acbe2231cde4043bd",
  "block_num": 34886140,
  "ref_block_prefix": 49359357
}
```

## 交易所 FIBOS 节点安全配置

对于交易所来说，搭建的 FIBOS 节点的安全也是不容忽视的，在交易所中 FIBOS API 节点承载着充币记录以及提币操作的功能，一旦出现安全问题，所带来的损失可能是不可估量的。这一部分内容为交易所搭建安全可靠的 FIBOS 网络节点提供了部分指导。

### 节点配置

为了满足交易所充提币业务，推荐搭建 FIBOS 节点机器的物理配置如下：

|          | 推荐配置                 | 最低配置                 |
| -------- | ------------------------ | ------------------------ |
| 系统类型 | Ubuntu Server 16.04+,X64 | Ubuntu Server 16.04+,X64 |
| CPU      | 4核                      | 2核                      |
| 内存     | 8GB                      | 4GB                      |
| 硬盘     | 300GB + （SSD）          | 100GB + （SSD）          |

### RPC 安全

交易所 API 节点建议禁用外网 RPC，如果节点需要 RPC 访问，建议使用内网 HTTP，对应配置示例代码如下：

```javascript
fibos.load("http", {
  "http-server-address": "127.0.0.1:8870", //内网RPC地址和端口 
});
```

### P2P 安全

为了保证 API 节点的稳定可靠，节点的 P2P 广播网络需要尽可能保证可靠，FIBOS 维护了目前主网稳定可用的 P2P 节点地址列表，地址为：<https://github.com/FIBOS-Community/fibos-p2p/blob/master/p2p.json>，请节点按照最新的 P2P 节点列表进行节点启动，同时建议各大交易所节点应该定期对该文件进行更新，重新启动节点。

示例 P2P 列表如下：

```bash
[
  "p2p.eosays.com:37106",
  "p2p.otclook.com:9870",
  "seed.bitze.site:9870",
  "47.74.181.212:27672",
  "api.xxq.pub:8888",
  "fibos.eosforum.one",
  "p2p.fibos.pw:59898",
  "p2p.fometa.io:59877",
  "p2p-mainnet.fibos123.com:9977",
  "p2p.eosas.io:37717",
  "p2p.fibos.fi:59595",
  "p2p-mainnet.fobp.pro:9873",
  "104.243.24.188:9870",
  "va-p2p.fibos.io:9870",
  "ca-p2p.fibos.io:9870",
  "sl-p2p.fibos.io:9870",
  "api.fibosgenesis.com:9870",
  "p2p-mainnet.fibosironman.io:9999",
  "fibosiseos.xyz:9870",
  "47.92.122.2:9870",
  "se-p2p.fibos.io:9870",
  "p2p.fophoenix.com:37398",
  "seed.fopool.xyz:9870",
  "p2p.fibospubg.top:9870",
  "seed.fibos.rocks:10100",
  "47.96.101.244:9898",
  "p2p.fospider.com:9933",
  "47.100.103.213:9870",
  "fibos.tokenasst.com:9870",
  "seed-mainnet.fibscan.io:9103",
  "p2p.mainnet.fibos.me:9870",
  "40.115.179.182:9870",
  "p2p.foshenzhenbp.com:9877",
  "p2p.xm.fo:10300",
  "34.73.46.1:9870",
  "p2p.mainnet.hellofibos.com:9876",
  "p2p-mainnet.ilovefibos.com:9876",
  "fibos.koalakoala.club:9870",
  "p2p-mainnet.loveyy.xyz:9870",
  "linyuezhan.com:9870",
  "p2p.fibos.team:9876",
  "ln-p2p.fibos.io:9870",
  "seed.fomaya.club:9870",
  "seed.fiboso.com:9965",
  "185.243.57.158:9870",
  "fibos.smr123.com:7890",
  "fibos-p2p.slowmist.io:9870",
  "superfibos.com:9870",
  "to-p2p.fibos.io:9870",
  "p2p.touch-me.club:9870",
  "ppray.com:9870",
  "p2p-mainnet.qingah.com:9870"
]
```

> **注：**对于如何启动 FIBOS 的节点，参考 <https://github.com/FIBOS-Community/fibos-nodes/>



如有其他相关技术疑问，请前往  <https://dev.fo/zh-cn/index.html>  或 <https://github.com/fibosio>  了解更多。也可以直接微信搜索  FIBOSio 添加 FIBSO 社区小助理，加入开发者群与我们交流。