---
title: RPC
type: manual
order: 250
---
## CHAIN

### get_info

Returns an object containing various details about the blockchain.

```
POST http://127.0.0.1:8888/v1/chain/get_info
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_info
```

执行结果：

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

Returns an object containing various details about a specific block on the blockchain.

```
POST http://127.0.0.1:8888/v1/chain/get_block
```
示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_block \
  --data '{"block_num_or_id": id}'
```

**BODY PARAMS**

| parameter           | type   | description                              |          |
| ------------------- | ------ | ---------------------------------------- | -------- |
| **block_num_or_id** | string | Provide a `block number` or a `block id` | REQUIRED |

执行结果：

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

```
POST http://127.0.0.1:8888/v1/chain/get_block_header_state
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_block_header_state
  --data '{"block_num_or_id": id}'
```

**BODY PARAMS**

| parameter           | type   | description                              |      |
| ------------------- | ------ | ---------------------------------------- | ---- |
| **block_num_or_id** | string | Provide a `block number` or a `block id` | /    |



### get_account

Returns an object containing various details about a specific account on the blockchain.

```
POST http://127.0.0.1:8888/v1/chain/get_account
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_account \
  --data '{"account_name": name}'
```

**BODY PARAMS**

| parameter        | type   | description             |          |
| ---------------- | ------ | ----------------------- | -------- |
| **account_name** | string | Provide an account name | REQUIRED |

执行结果：

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

```
POST http://127.0.0.1:8888/v1/chain/get_abi
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_abi
```

**BODY PARAMS**

| parameter        | type   | description                         |      |
| ---------------- | ------ | ----------------------------------- | ---- |
| **account_name** | string | name of account to retrieve ABI for | /    |

执行结果：

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

```
POST http://127.0.0.1:8888/v1/chain/get_raw_code_and_abi
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_raw_code_and_abi
  --data '{"account_name": name}'
```

**BODY PARAMS**

| parameter        | type   | description                          |      |
| ---------------- | ------ | ------------------------------------ | ---- |
| **account_name** | string | Account name to get code and abi for | /    |

执行结果：

```
{
  "account_name":"hello"
  "wasm":"UEsDBC0AAAAIAPCEd01qlACiNgAAADkAAAAIABQAaW5kZXguanMBABAAAAAAAAAAAAAAAAAAAAAAAEutKMgvKinWy8hUsFUoLU4tUrC1U0jOzyvOz0nVSy0qyi/SUM/MA4mUFCUml1ip64BVaVoDAFBLAQIAABQAAAAIAPCEd01qlACiNgAAADkAAAAIAAAAAAAAAAEAAAAAAAAAAABpbmRleC5qc1BLBQYAAAAAAQABADYAAABwAAAAAAA=="
  "abi":"DmVvc2lvOjphYmkvMS4wAAIGcGxheWVyAAIFdGl0bGUGc3RyaW5nA2FnZQVpbnQ2NAJoaQABBHVzZXIEbmFtZQEAAAAAAACAawJoaQAAAAAA="
}
```



### get_table_rows

Returns an object containing rows from the specified table.

```
POST http://127.0.0.1:8888/v1/chain/get_table_rows
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_table_rows \
  --data '{"scope":account_name,"code":smart_contract_name,"table":table_name,"json":true or false}'
```

**BODY PARAMS**

| parameters      | type   | description                     |          |
| --------------- | ------ | ------------------------------- | -------- |
| **scope**       | string | Provide the account name        | REQUIRED |
| **code**        | string | Provide the smart contract name | REQUIRED |
| **table**       | string | Provide the table name          | REQUIRED |
| **json**        | string | Provide true or false           | REQUIRED |
| **lower_bound** | int32  | Provide the lower bound         | /        |
| **upper_bound** | int32  | Provide the upper bound         | /        |
| **limit**       | int32  | Provide the limit               | /        |

执行结果：

```
{
  "rows": [
    {
      "account": "account",
      "balance": 1000
    }
  ],
  "more": false
}
```



### abi_json_to_bin

Serializes json to binary hex. The resulting binary hex is usually used for the data field in push_transaction.

```
POST http://127.0.0.1:8888/v1/chain/abi_json_to_bin
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/abi_json_to_bin \
  --data '{"code":account_name,"action":action_arguments,"args":arguments}'
```

**BODY PARAMS**

| parameters | type   | description                  |      |
| ---------- | ------ | ---------------------------- | ---- |
| **code**   | string | Provide the account name     | /    |
| **action** | string | Provide the action arguments | /    |
| **args**   | json   | Provide the json arguments   | /    |

执行结果：

```
{
  "binargs": "000000008093dd74000000000094dd74e803000000000000",
  "required_scope": [],
  "required_auth": []
}
```



### abi_bin_to_json

Serializes binary hex to json.

```
POST http://127.0.0.1:8888/v1/chain/abi_bin_to_json
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/abi_bin_to_json \
  --data '{"code":account_name,"action":action_name,"binargs":binary arguments}'
```

**BODY PARAMS**

| parameters  | type   | description                             |          |
| ----------- | ------ | --------------------------------------- | -------- |
| **code**    | string | Provide the smart contract account name | REQUIRED |
| **action**  | string | Provide the action name                 | REQUIRED |
| **binargs** | string | Provide the binary arguments            | REQUIRED |

执行结果：

```
{
  "args": {
    "from": "initb",
    "to": "initc",
    "quantity": 1000
  },
  "required_scope": [],
  "required_auth": []
}
```



### get_required_keys

Returns the required keys needed to sign a transaction.

```
POST http://127.0.0.1:8888/v1/chain/get_required_keys
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_required_keys \
  --data '{"transaction":transaction_object,"action":available_keys}'
```

**BODY PARAMS**

| parameters         | type             | description                    |          |
| ------------------ | ---------------- | ------------------------------ | -------- |
| **transaction**    | json             | Provide the transaction object | REQUIRED |
| **available_keys** | array of strings | Provide the available keys     | REQUIRED |

执行结果：

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

```
POST http://127.0.0.1:8888/v1/chain/get_currency_stats
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_currency_stats
```

**BODY PARAMS**

| parameters | type   | description                          |      |
| ---------- | ------ | ------------------------------------ | ---- |
| **code**   | string |                                      | /    |
| **symbol** | string | currency symbol to get the stats for | /    |



### get_producers

```
POST http://127.0.0.1:8888/v1/chain/get_producers
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_producers
```

**BODY PARAMS**

| parameters      | type    | description                           |      |
| --------------- | ------- | ------------------------------------- | ---- |
| **limit**       | string  | total number of producers to retrieve | /    |
| **lower_bound** | string  |                                       | /    |
| **json**        | boolean | return result in JSON format?         | /    |



### push_block

```
POST http://127.0.0.1:8888/v1/chain/push_block
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/push_block
```

**BODY PARAMS**

| parameters             | type             | description |      |
| ---------------------- | ---------------- | ----------- | ---- |
| **timestamp**          | date-time        |             | /    |
| **producer**           | string           |             | /    |
| **confirmed**          | int32            |             | /    |
| **previous**           | string           |             | /    |
| **transaction_mroot**  | string           |             | /    |
| **action_mroot**       | int32            |             | /    |
| **version**            | string           |             | /    |
| **new_producers**      | array of strings |             | /    |
| **header_extensions**  | array of strings |             | /    |
| **producer_signature** | string           |             | /    |
| **transactions**       | array            |             | /    |
| **block_extensions**   | array of strings |             | /    |



### push_transaction

This method expects a transaction in JSON format and will attempt to apply it to the blockchain.

```
POST http://127.0.0.1:8888/v1/chain/push_transaction
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/push_transaction
```

**BODY PARAMS**

| parameters                   | type             | description                                           |      |
| ---------------------------- | ---------------- | ----------------------------------------------------- | ---- |
| **signatures**               | array of strings | array of signatures required to authorize transaction | /    |
| **compression**              | string           | compression used, usually false                       | /    |
| **packed_context_free_data** | string           | json to hex                                           | /    |
| **packed_trx**               | string           | json to hex                                           | /    |

执行结果：

```
{
	'transaction_id' = "1..."
}
```

#### Example

**Note**

The ref_block_num and ref_block_prefix here are provided as a result of /v1/chain/get_block of the last_irreversible_block. The last_irreversible_block can be found by calling /v1/chain/get_info. You also need to use /v1/wallet/sign_transaction to get the right signature.



### push_transactions

This method expects a transactions in JSON format and will attempt to apply it to the blockchain. This method push multiple transactions at once.

```
POST http://127.0.0.1:8888/v1/chain/push_transaction
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/push_transaction \
  --data '{"body":transaction}'
```

**BODY PARAMS**

| parameter | type | description                                    |          |
| --------- | ---- | ---------------------------------------------- | -------- |
| **body**  | json | Provide the authorizations for the transaction | REQUIRED |

执行结果：

```
{
	'transaction_id' = "1..."
}
```

#### Example 

**Note**

The ref_block_num and ref_block_prefix here are provided as a result of /v1/chain/get_block of the last_irreversible_block. The last_irreversible_block can be found by calling /v1/chain/get_info. You also need to use /v1/wallet/sign_transaction to get the right signature.



## HISTORY

### get_key_accounts

```
POST http://127.0.0.1:8888/v1/history/get_key_accounts
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/history/get_key_accounts
```

**BODY PARAMS**

| parameter      | type  |      |
| -------------- | ----- | ---- |
| **public_key** | int32 | /    |



### get_controlled_accounts

```
POST http://127.0.0.1:8888/v1/history/get_controlled_accounts
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/history/get_controlled_accounts
```

**BODY PARAMS**

| parameter               | type   |      |
| ----------------------- | ------ | ---- |
| **controlling_account** | string | /    |



## NET

### connect

```
POST http://127.0.0.1:8888/v1/net/connect
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/net/connect
```

**BODY PARAMS**

string



### disconnect

```
POST http://127.0.0.1:8888/v1/net/disconnect
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/net/disconnect \
  --data '""'
```

**BODY PARAMS**

string



### connections

```
POST http://127.0.0.1:8888/v1/net/connections
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/net/connections
```



### status

```
POST http://127.0.0.1:8888/v1/net/status
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/net/status
```



## PRODUCER

### pause

```
POST http://127.0.0.1:8888/v1/producer/pause
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/pause
```



### resume

```
POST http://127.0.0.1:8888/v1/producer/resume
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/resume
```



### paused

```
POST http://127.0.0.1:8888/v1/producer/paused
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/resume
```



### get_runtime_options

```
POST http://127.0.0.1:8888/v1/producer/get_runtime_options
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/get_runtime_options
```



### update_runtime_options

```
POST http://127.0.0.1:8888/v1/producer/update_runtime_options
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/update_runtime_options
```

**BODY PARAMS**

| parameters                     | type  |      |
| ------------------------------ | ----- | ---- |
| **max_transaction_time**       | int32 | /    |
| **max_irreversible_block_age** | int32 | /    |
| **produce_time_offset_us**     | int32 | /    |
| **last_block_time_offset_us**  | int32 | /    |
| **incoming_defer_ratio**       | int32 | /    |
| **subjective_cpu_leeway_us**   | int32 | /    |



### get_greylist

Returns producer greylist

```
POST http://127.0.0.1:8888/v1/producer/get_greylist
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/get_greylist
```

执行结果：

```
{"accounts":["a11111111111","aaa","bbb"]}
```



### add_greylist_accounts

```
POST http://127.0.0.1:8888/v1/producer/add_greylist_accounts
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/add_greylist_accounts
```

**BODY PARAMS**

| parameter    | type             | description                 |      |
| ------------ | ---------------- | --------------------------- | ---- |
| **accounts** | array of strings | Accounts to add to greylist | /    |



### remove_greylist_accounts

```
POST http://127.0.0.1:8888/v1/producer/remove_greylist_accounts
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer/remove_greylist_accounts
```

**BODY PARAMS**

| parameter    | type             | description                 |      |
| ------------ | ---------------- | --------------------------- | ---- |
| **accounts** | array of strings | Accounts to add to greylist | /    |



### get_whitelist_blacklist

```
POST http://127.0.0.1:8888/v1/producer
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer
```

Lorem ipsum dolor sit amet, consectetur adipiscing elit.

```javascript
$.get('http://yoursite.com/test/' + id, function(data) {
    console.log(data);
})
```



### set_whitelist_blacklist

```
POST http://127.0.0.1:8888/v1/producer
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/producer
```

Lorem ipsum dolor sit amet, consectetur adipiscing elit.

```javascript
$.get('http://yoursite.com/test/' + id, function(data) {
    console.log(data);
});
```



## DBSIZE

### get

```
POST http://127.0.0.1:8888/v1/db_size/get
```

示例：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/db_size/get
```

