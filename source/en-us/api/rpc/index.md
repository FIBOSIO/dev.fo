---
title: 
type: rpc
language: en
order: 1
---
# RPC API

## CHAIN

### get_info

return the object includes each detail info of blockchain

```
POST http://127.0.0.1:8888/v1/chain/get_info
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_info
```

Results：

```
{
  "server_version":"8f0f54cf",
  "chain_id":"6aa7bd33b6b45192465afa3553dedb531acaaff8928cf64b70bd4c5e49b7ec6a",
  "head_block_num":14880710,
  "last_irreversible_block_num":14880380,
  "last_irreversible_block_id":"00e30e7c94815385d5edb134f88a1a40bf6c9342a01763cdad44b250641bf0a8",
  "head_block_id":"00e30fc6c584a6c2090a91fc34eaa05d8e3a392f910c757c6c22376b68b9bd84",
  "head_block_time":"2018-11-23T03:42:20.500",
  "head_block_producer":"eosteaeostea",
  "virtual_block_cpu_limit":200000000,
  "virtual_block_net_limit":1048576000,
  "block_cpu_limit":199900,
  "block_net_limit":1048576,
  "server_version_string":"v1.3.1.6"
}                                                                                              
```



### get_block

Return an object includes each specific detail info of blockchain

```
POST http://127.0.0.1:8888/v1/chain/get_block
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_block \
  --data '{"block_num_or_id": "5"}'
```

**Main Parameters**

| Parameters                | Type   | Description                                     |          |
| ------------------- | ------ | ---------------------------------------- | -------- |
| **block_num_or_id** | string | Provide a `block number` or a `block id` | REQUIRED |

Results：

```
{
  "timestamp":"2018-08-28T00:00:02.000",
  "producer":"eosio",
  "confirmed":0,
  "previous":"000000046fedbd93f736747cd5c5f1de844d1fb9b1076dc967b6344016e5fa16",
  "transaction_mroot":"0000000000000000000000000000000000000000000000000000000000000000",
  "action_mroot":"d0f15919364427f0f51e6b421929815bcafa0081bb3a1825fa7c2e16818931c6",
  "schedule_version":0,
  "new_producers":null,
  "header_extensions":[],
  "producer_signature":"SIG_K1_Ki4tfnaYVYdfT7Lh9iffU7zNw3qusUPMtEMbpxqrNYwQcHtmfdFc35jicervubFQN3R37bbGt5k6zZojzU77Ya2KneUBxg",
  "transactions":[],
  "block_extensions":[],
  "id":"00000005ebf9997c1924f5f79d63e699da5db5ebdc72c4df4b7c213602cd11e1",
  "block_num":5,
  "ref_block_prefix":4160037913
}
```



### get_block_header_state

Return reversible block head status.

```
POST http://127.0.0.1:8888/v1/chain/get_block_header_state
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_block_header_state \
  --data '{"block_num_or_id":"118"}'
```

**Main Parameters**

| Parameters                | Type   | Description                                      |      |
| ------------------- | ------ | ---------------------------------------- | ---- |
| **block_num_or_id** | string | Provide a `block number` or a `block id` | /    |



### get_account

Return an object includes each detail info of specific account.

```
POST http://127.0.0.1:8888/v1/chain/get_account
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_account \
  --data '{"account_name": "eosio"}'
```

**Main Parameters**

| Parameters             | Type   | Description                     |          |
| ---------------- | ------ | ----------------------- | -------- |
| **account_name** | string | Provide an account name | REQUIRED |

Results：

```
{
  "account_name":"eosio",
  "head_block_num":14882625,
  "head_block_time":"2018-11-23T03:58:18.500",
  "privileged":true,
  "last_code_update":"2018-09-15T17:48:36.000",
  "created":"2018-08-28T00:00:00.000",
  "ram_quota":-1,
  "net_weight":-1,
  "cpu_weight":-1,
  "net_limit":{
    "used":-1,
    "available":-1,
    "max":-1
  },
  "cpu_limit":{
    "used":-1,
    "available":-1,
    "max":-1
  },
  "ram_usage":1229057,
  "permissions":[
    {
      "perm_name":"active",
      "parent":"owner",
      "required_auth":{
        "threshold":1,
        "keys":[],
        "accounts":[
          {
            "permission":{
              "actor":"eosio.prods",
              "permission":"active"
            },
            "weight":1
          }
        ],
        "waits":[]
      }
    },
    {
      "perm_name":"owner",
      "parent":"",
      "required_auth":{
        "threshold":1,
        "keys":[],
        "accounts":[
          {
            "permission":{
              "actor":"eosio.prods",
              "permission":"active"
            },
            "weight":1
          }
        ],
        "waits":[]
      }
    }
  ],
  "total_resources":null,
  "self_delegated_bandwidth":null,
  "refund_request":null,
  "voter_info":null
}
```



### get_abi

Get account abi data 

```
POST http://127.0.0.1:8888/v1/chain/get_abi
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_abi \
  --data '{"account_name": "hello"}'
```

**Main Parameters**

| Parameters             | Type   | Description                                 |      |
| ---------------- | ------ | ----------------------------------- | ---- |
| **account_name** | string | name of account to retrieve ABI for | /    |

Results：

```
{
  "account_name":"hello",
  "abi":{
    "version":"eosio::abi/1.0",
    "types":[],
    "structs":[
      {
        "name":"player",
        "base":"",
        "fields":[
          {
            "name":"title",
            "type":"string"
          },
          {
            "name":"age",
            "type":"int64"
          }
        ]
      },
      {
        "name":"hi",
        "base":"",
        "fields":[
          {
            "name":"user",
            "type":"name"
          }
        ]
      }
    ],
    "actions":[
      {
        "name":"hi",
        "type":"hi",
        "ricardian_contract":""
      }
    ],
    "tables":[],
    "ricardian_clauses":[],
    "error_messages":[],
    "abi_extensions":[],
    "variants":[]
  }
}
```



### get_raw_code_and_abi

Get account original code and abi data

```
POST http://127.0.0.1:8888/v1/chain/get_raw_code_and_abi
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_raw_code_and_abi \
  --data '{"account_name":"hello"}'
```

**Main Parameters**

| Parameters             | Type   | Description                                  |      |
| ---------------- | ------ | ------------------------------------ | ---- |
| **account_name** | string | Account name to get code and abi for | /    |

Results：

```
{
  "account_name":"hello"
  "wasm":"UEsDBC0AAAAIAPCEd01qlACiNgAAADkAAAAIABQAaW5kZXguanMBABAAAAAAAAAAAAAAAAAAAAAAAEutKMgvKinWy8hUsFUoLU4tUrC1U0jOzyvOz0nVSy0qyi/SUM/MA4mUFCUml1ip64BVaVoDAFBLAQIAABQAAAAIAPCEd01qlACiNgAAADkAAAAIAAAAAAAAAAEAAAAAAAAAAABpbmRleC5qc1BLBQYAAAAAAQABADYAAABwAAAAAAA=="
  "abi":"DmVvc2lvOjphYmkvMS4wAAIGcGxheWVyAAIFdGl0bGUGc3RyaW5nA2FnZQVpbnQ2NAJoaQABBHVzZXIEbmFtZQEAAAAAAACAawJoaQAAAAAA="
}
```



### get_table_rows

Return an object includes specific rows of table.

```
POST http://127.0.0.1:8888/v1/chain/get_table_rows
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_table_rows \
  --data '{"scope":"dabingguozi","code":"eosio.token","table":"accounts","json":true}'
```

**Main Parameters**

| Parameters            | Type    | Description                             |          |
| --------------- | ------- | ------------------------------- | -------- |
| **scope**       | string  | Provide the account name        | REQUIRED |
| **code**        | string  | Provide the smart contract name | REQUIRED |
| **table**       | string  | Provide the table name          | REQUIRED |
| **json**        | boolean | return result in JSON format    | REQUIRED |
| **lower_bound** | int32   | Provide the lower bound         | /        |
| **upper_bound** | int32   | Provide the upper bound         | /        |
| **limit**       | int32   | Provide the limit               | /        |

Results：

```
{
  "rows": [{
    "balance": "554.0000 SYS"
    }],
  "more": false
}
```



### abi_json_to_bin

Serialize json to binary or hexadecimal. Generated binary or hexadecimal 

```
POST http://127.0.0.1:8888/v1/chain/abi_json_to_bin
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/abi_json_to_bin \
  --data '{"code":"eosio.token","action":"transfer","args":{"from":"testnetyy111","to":"testneths111","quantity":"100.0000 EOS", "memo":"hi there"}}'
```

**Main Parameters**

| Parameters       | Type   | Description                          |      |
| ---------- | ------ | ---------------------------- | ---- |
| **code**   | string | Provide the account name     | /    |
| **action** | string | Provide the action arguments | /    |
| **args**   | json   | Provide the json arguments   | /    |

Results：

```
{
  "binargs": "1042f03eab99b1ca1042c02dab99b1ca40420f000000000004454f5300000000086869207468657265",
}
```



### abi_bin_to_json

Serialize binary or hexadecimal to json.

```
POST http://127.0.0.1:8888/v1/chain/abi_bin_to_json
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/abi_bin_to_json \
  --data '{"code":"eosio.token","action":"transfer","binargs":"1042f03eab99b1ca1042c02dab99b1ca40420f000000000004454f5300000000086869207468657265"}'
```

**Main Parameters**

| Parameters        | Type   | Description                                     |          |
| ----------- | ------ | --------------------------------------- | -------- |
| **code**    | string | Provide the smart contract account name | REQUIRED |
| **action**  | string | Provide the action name                 | REQUIRED |
| **binargs** | string | Provide the binary arguments            | REQUIRED |

Results：

```
{
  "args": {
    "from": "testnetyy111",
    "to": "testneths111",
    "quantity": "100.0000 EOS",
    "meno": "hi there"
  }
}
```



### get_required_keys

Return requiring key of registration.

```
POST http://127.0.0.1:8888/v1/chain/get_required_keys
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_required_keys \
  --data '{"transaction":transaction_object,"action":available_keys}'
```

**Main Parameters**

| Parameters               | Type             | Description                            |          |
| ------------------ | ---------------- | ------------------------------ | -------- |
| **transaction**    | json             | Provide the transaction object | REQUIRED |
| **available_keys** | array of strings | Provide the available keys     | REQUIRED |

Results：

```
{
  "required_keys": [
    "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV"
  ]
}
```

#### Example

`transaction`

```json
{
  "ref_block_num": "100",
  "ref_block_prefix": "137469861",
  "expiration": "2017-09-25T06:28:49",
  "scope": ["initb", "initc"],
  "actions": [{
    "code": "currency",
    "type": "transfer",
    "recipients": ["initb", "initc"],
    "authorization": [{
      "account": "initb",
      "permission": "active"
    }],
    "data": "000000000041934b000000008041934be803000000000000"
  }],
  "signatures": [],
  "authorizations": []
}
```

`available_keys`

```json
["EOS4toFS3YXEQCkuuw1aqDLrtHim86Gz9u3hBdcBw5KNPZcursVHq",
 "EOS7d9A3uLe6As66jzN8j44TXJUqJSK3bFjjEEqR4oTvNAB3iM9SA",
 "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV"]

```



### get_currency_stats

Get details about some assets

```
POST http://127.0.0.1:8888/v1/chain/get_currency_stats
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_currency_stats \
  --data '{"code":"eosio.token","symbol":"EOS"}'
```

**Main Parameters**

| Parameters       | Type   | Description                                  |      |
| ---------- | ------ | ------------------------------------ | ---- |
| **code**   | string |                                      | /    |
| **symbol** | string | currency symbol to get the stats for | /    |



### get_producers

Get the producer info

```
POST http://127.0.0.1:8888/v1/chain/get_producers
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_producers
```

**Main Parameters**

| Parameters            | Type    | Description                                   |      |
| --------------- | ------- | ------------------------------------- | ---- |
| **limit**       | string  | total number of producers to retrieve | /    |
| **lower_bound** | string  |                                       | /    |
| **json**        | boolean | return result in JSON format?         | /    |



### push_block

Push block.

```
POST http://127.0.0.1:8888/v1/chain/push_block
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/push_block
```

**Main Parameters**

| Parameters                   | Type             | Description  |      |
| ---------------------- | ---------------- | ---- | ---- |
| **timestamp**          | date-time        |      | /    |
| **producer**           | string           |      | /    |
| **confirmed**          | int32            |      | /    |
| **previous**           | string           |      | /    |
| **transaction_mroot**  | string           |      | /    |
| **action_mroot**       | int32            |      | /    |
| **version**            | string           |      | /    |
| **new_producers**      | array of strings |      | /    |
| **header_extensions**  | array of strings |      | /    |
| **producer_signature** | string           |      | /    |
| **transactions**       | array            |      | /    |
| **block_extensions**   | array of strings |      | /    |



### push_transaction

This method requires JSON format, and try to use it in blockchain.

```
POST http://127.0.0.1:8888/v1/chain/push_transaction
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/push_transaction
```

**Main Parameters**

| Parameters                         | Type             | Description                                                   |      |
| ---------------------------- | ---------------- | ----------------------------------------------------- | ---- |
| **signatures**               | array of strings | array of signatures required to authorize transaction | /    |
| **compression**              | string           | compression used, usually false                       | /    |
| **packed_context_free_data** | string           | json to hex                                           | /    |
| **packed_trx**               | string           | json to hex                                           | /    |

Results：

```
{
	'transaction_id' = "1..."
}
```

#### Example

**Note**

The `ref_block_num`和`ref_block_prefix` here is the result of `last_irreversible_block`and`/v1/chain/get_block`。 You can use`/v1/chain/get_info`to find`last_irreversible_block`。 You also need to use`/v1/wallet/sign_transaction`to get the right signature.



### push_transactions

This method requires json format object and try to use it in blockchain. This method will push multiple objects per time.

```
POST http://127.0.0.1:8888/v1/chain/push_transaction
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/push_transaction \
  --data '{"body":transaction}'
```

**Main Parameters**

| Parameters     | Type | Description                                            |          |
| -------- | ---- | ---------------------------------------------- | -------- |
| **body** | json | Provide the authorizations for the transaction | REQUIRED |

Results：

```
{
	'transaction_id' = "1..."
}
```

#### Example 

**Note**

The`ref_block_num`和`ref_block_prefix` here is the result of `last_irreversible_block`and`/v1/chain/get_block` You can use`/v1/chain/get_info`to find`last_irreversible_block`。 You also need to use `/v1/wallet/sign_transaction` to get the right signature.



## HISTORY

> Note: history-api plugin needs to be started.

### get_key_accounts

Check account according to the public key.

```
POST http://127.0.0.1:8888/v1/history/get_key_accounts
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/history/get_key_accounts
```

**Main Parameters**

| Parameters           | Type  |      |
| -------------- | ----- | ---- |
| **public_key** | int32 | /    |



## NET

> Note: net plugin is required.

### connect

```
POST http://127.0.0.1:8888/v1/net/connect
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/net/connect
```

**Parameters**

string



### disconnect

```
POST http://127.0.0.1:8888/v1/net/disconnect
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/net/disconnect \
  --data '""'
```

**Parameters**

string



### connections

```
POST http://127.0.0.1:8888/v1/net/connections
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/net/connections
```



### status

```
POST http://127.0.0.1:8888/v1/net/status
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/net/status
```



## PRODUCER

> producer plugin is required.

### pause

```
POST http://127.0.0.1:8888/v1/producer/pause
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/pause
```



### resume

```
POST http://127.0.0.1:8888/v1/producer/resume
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/resume
```



### paused

```
POST http://127.0.0.1:8888/v1/producer/paused
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/resume
```



### get_runtime_options

```
POST http://127.0.0.1:8888/v1/producer/get_runtime_options
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/get_runtime_options
```



### update_runtime_options

```
POST http://127.0.0.1:8888/v1/producer/update_runtime_options
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/update_runtime_options
```

**Main Parameters**

| Parameters                           | Type  |      |
| ------------------------------ | ----- | ---- |
| **max_transaction_time**       | int32 | /    |
| **max_irreversible_block_age** | int32 | /    |
| **produce_time_offset_us**     | int32 | /    |
| **last_block_time_offset_us**  | int32 | /    |
| **incoming_defer_ratio**       | int32 | /    |
| **subjective_cpu_leeway_us**   | int32 | /    |



### get_greylist

```
POST http://127.0.0.1:8888/v1/producer/get_greylist
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/get_greylist
```

Results：

```
{"accounts":["a11111111111","aaa","bbb"]}
```



### add_greylist_accounts

```
POST http://127.0.0.1:8888/v1/producer/add_greylist_accounts
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/add_greylist_accounts
```

**Main Parameters**

| Parameters         | Type             | Description                         |      |
| ------------ | ---------------- | --------------------------- | ---- |
| **accounts** | array of strings | Accounts to add to greylist | /    |



### remove_greylist_accounts

```
POST http://127.0.0.1:8888/v1/producer/remove_greylist_accounts
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/remove_greylist_accounts
```

**Main Parameters**

| Parameters         | Type             | Description                         |      |
| ------------ | ---------------- | --------------------------- | ---- |
| **accounts** | array of strings | Accounts to add to greylist | /    |



### get_whitelist_blacklist

```
POST http://127.0.0.1:8888/v1/producer/get_whitelist_blacklist
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/get_whitelist_blacklist
```



### set_whitelist_blacklist

```
POST http://127.0.0.1:8888/v1/producer/set_whitelist_blacklist
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/set_whitelist_blacklist
```





## DBSIZE

### get

```
POST http://127.0.0.1:8888/v1/db_size/get
```

Example：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/db_size/get
```

