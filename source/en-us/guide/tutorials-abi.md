---
title: Smart Contract - ABI Files
type: tutorials
language: en
order: 12
---

ABI, called the Application Binary Interface, as the name implies, refers to an interface file which describes the data interchange format between the smart contract and the upper-layer application. The ABI file format is similar to JSON format, and it is highly readable so as to facilitate the work connection between smart contract developers and upper application developers. 

For contracts developed by JavaScript, it is required to use ABI files to define the definition of actions and tables. 

The Smart Contract ABI file consists of five parts:

```json
{
    "version": "eosio::abi/1.0",
    "structs":[...],            
    "actions":[...],            
    "tables":[...],            
    "types":[...],              
}
```
`version` ：refers to the version number of specified ABI
`structs` ：represents various types of data structures
`actions` ：states the called action of smart contracts
`tables` ：lists the name of the data tables in the smart contracts, and the name of the struct stored in the data tables
`types` ：used for customized data

We will illustrate the development method of Smart Contract ABI on FIBOS in the order of structs -> actions -> tables -> types.

Create new  `contracts` folder，and save the code to `contracts/todo.abi`:


## structs

There is a one-to-one correspondence relationship between the content of the structs section and the content of the actions section. It is necessary to declare the parameters required to be passed to each action in the structs as following.

```json
"structs": [
    {
      "name": "todo_index",
      "base" : "",
      "fields": [
        {
          "name": "id",
          "type": "int64"
        }
      ]
    },
    {
      "name": "todo",
      "base" : "",
      "fields": [
        {
          "name": "id",
          "type": "int64"
        },
        {
          "name": "text",
          "type": "string"
        }
      ]
    }
]
```

The FIBOS system will look for the corresponding data structure in the structs section according to the type declared in the actions section. Furthermore, the name and type of each parameter will also be listed in the fields of each data structure.

In addition, the detailed data structure of both items in actions section and items in tables is require to be listed in structs.

```json
"structs": [
    {
      "name": "todo_index",
      "base" : "",
      "fields": [
        {
          "name": "id",
          "type": "int64"
        }
      ]
    },
    {
      "name": "todo",
      "base" : "",
      "fields": [
        {
          "name": "id",
          "type": "int64"
        },
        {
          "name": "text",
          "type": "string"
        }，
        {
          "name": "completed",
          "type": "bool"
        }
      ]
    }
]
```

Thus, we define a struct named todo_index in structs, so as to list the data table of todo_index, including the field id(int64); a struct named todo is used to list the data table of todo, including the field id(int64), text(string), and completed(bool).


## actions

The action section is used to declare which action the smart contract can call. In the following code example, the action defines four methods which are adding data, finding data, modifying data, and deleting data.

```json
    "actions": [{
        "name": "emplacetodo",
        "type": "todo",
        "ricardian_contract": ""
    },{
        "name": "findtodo",
        "type": "todo_index",
        "ricardian_contract": ""
    },{
        "name": "updatetodo",
        "type": "todo",
        "ricardian_contract": ""
    },{
        "name": "destorytodo",
        "type": "todo_index",
        "ricardian_contract": ""
    }],
```

The name in each item refers to the name of the action, while type is used to find the data structure in structs, and the ricardian_contract is a Ricardian Contract

The Ricardian Contract is a special structured text that is used primarily to clarify the intentions of both parties of the transaction. On FIBOS, contracts can be attached to every action you send. Such a kind of contract is very special and has a fixed format so that it can be read by both programs and humans. This contract is called the Ricardian Contract.

> Note: An action is named following the naming rule of EOS. 
> The current naming rule on naming of action: only consisting of numbers from 1 to 5 and English lowercase letters; the maximum length of characters is 12.


## tables

tables lists the names of the data table that needs to be created in the smart contract, and also the name of the structs stored in the data table.

```json
"tables": [{
    "name": "todos",
    "type": "todo",
    "index_type": "i64",
    "key_names": ["id"],
    "key_types": ["int64"]
}]
```

The above codes construct a data table with the name todos, the structure type todo, the primary key name is id, and the primary key type is int64.


## types

types are used to customize the type of data:

```json
{
  "new_type_name": "my_account_name",
  "type": "name"
}
```

In this way, in this ABI file, a type with the type name of my_account_name is customized, and the type is determined as “name”. Moreover, “new_type_name” and “type” are the keywords, and the “name” type is a system-defined data type.



## ABI file code example

According to the instructions above, we wrote the contract required for this article. The following code is saved as contracts/todo.abi.

```json
{
  "version": "eosio::abi/1.0",
  "structs": [
    {
      "name": "todo_index", 
      "base": "",
      "fields": [
        {
          "name": "id", 
          "type": "int64"
        }
      ]
    },
    {
      "name": "todo", 
      "base": "",
      "fields": [
        {
          "name": "id", 
          "type": "int64"
        },
        {
          "name": "text",
          "type": "string"
        },
        {
          "name": "completed", 
          "type": "bool"
        }
      ]
    }
  ],
  "actions": [
    {
      "name": "emplacetodo", 
      "type": "todo",
      "ricardian_contract": ""
    },
    {
      "name": "findtodo",
      "type": "todo_index",
      "ricardian_contract": ""
    },
    {
      "name": "updatetodo", 
      "type": "todo",
      "ricardian_contract": ""
    },
    {
      "name": "destorytodo", 
      "type": "todo_index",
      "ricardian_contract": ""
    }
  ],
  "tables": [
    {
      "name": "todos", 
      "type": "todo", 
      "index_type": "i64", 
      "key_names": ["id"], 
      "key_types": ["int64"]
    }
  ]
}
```

>**Note: Please do not add any annotations to the ABI file, otherwise an error will be reported!**

Through the ABI file, we define four actions, including emplacetodo(todo), findtodo(todo_index), updatetodo(todo), and destorytodo(todo_index); the primary key of corresponding structs is todo_index, qualified with three attributes of id(int64), text(string), completed(bool) 

The GitHub source code for this article: under the `contracts` folder of 
<https://github.com/fengluo/fibos-todomvc> 

**Next Chapter**
👉 【[Write JavaScript Smart Contracts](js.html)】
