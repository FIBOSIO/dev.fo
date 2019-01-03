---
title:  ABI File
type: tutorials
language: en
order: 201
---

Using JavaScript to develop blockchain smart contract is supported in FIBOS. In the previous chapter [Quick Start](./start.html), in the JS smart contract that we wrote, there is another contract ABI file beside the contract code JS file. We didn't make it clear at that time, so here we will go through the details of the ABI file.

## What is ABI

The full name of ABI is Application Binary Interface. It is a Interface file, which describes the data tracsfer format between smart contract and the upper applications. ABI file format is similar to JSON which has a good readablity. It is good for connection between smart contract engineers and upper applications engineers. 

For JavaScript contract, ABI file is needed to define  `actions` and `tables`.

Smart contract ABI files are composed of 5 parts:

```json
{
    "version": "eosio::abi/1.0",//define ABI version
    "types":[...],              //define types alias
    "structs":[...],            //the data structure of each types
    "actions":[...],            //action of smart contract 
    "tables":[...]            //data tables
}
```

We will go through the development method of FIBOS smart contract ABI by the sequence of  `actions` ->  `tables` -> `structs` -> `types` 

## ABI Development

### actions

Part of the usage of action is to define the actions that can be called by the smart contract as shown below:

```json
"actions": [{
    "name": "hi",
    "type": "hi",
    "ricardian_contract": ""
}]
```

Each ` name ` is the action name, while `type` is used to find data structure in `structs `, and `ricardian_contract ` is Ricardian Contract.

Ricardian Contract is a special Structured text, mainly used to declear intentions of both parties in trading. In FIBOS, each action you send can be added with contract. This type of contract is special, it has a fixed format that can be read by both programs and human beings. This is what we called the Ricardian Contract.

**Attention: Action names follow the naming rules of eos.**

Currently, the naming rule: composed of only Numbers 1-5 and lowercase English letters ; The maximum character length is 12.

If any changes are made later, we will modify the document in time.


### tables

`tables`  listed the data tables that need to be build in the smart contract and also the structure name saved in data table.

```json
"tables": [{
    "name": "players",
    "type": "player",
    "index_type": "i64",
    "key_names": ["id"],
    "key_types": ["int64"]
}]
```

The codes above built a table named players, the structure type is player, main key is id, type is int64 data table.

### structs

There is a correspondence between part of the content of `structs` and part of the content of `actions`. We just defined an action name at above `actions`. We also need to define ` structs ` the incoming parameters for each action.

```json
"structs":  [{
    "name": "shape",
    "base": "",
    "fields": [{
        "name": "area",
        "type": "flout64"
    }]
}]
```

```json
"structs":  [{
    "name": "colorshape",
    "base": "shape",
    "fields": [{
        "name": "color",
        "type": "int64"
    }]
}]
```

Through ` base ` field inheritance is equivalent to:

```json
"structs":  [{
    "name": "colorshape",
    "base": "",
    "fields": [{
        "name": "area",
        "type": "flout64"
    },{
        "name": "color",
        "type": "int64"
    }]
}]
```

FIBOS system will find the corresponding data structure in `structs` by the `type` defined by `actions`. In `fields` of  each data structures, name and type of each parameter will listed.

Except that, not only the projects in `actions` need to list detailed data structure in `structs`, but also the projects in `tables`

```json
"structs": [{
    "name": "player",
    "base": "",
    "fields": [{
        "name": "nickname",
        "type": "my_account_name"
    }, {
        "name": "age",
        "type": "int32"
    }]
}, {
    "name": "hi",
    "base": "",
    "fields": [{
        "name": "nickname",
        "type": "my_account_name"
    }]
}]
```

So, in `structs`  we defined a struct named player. It is used to list data table player including 2 strings: `nickname` and `age` , the types are  `my_account_name` and`int32`

### types


`types` is used to define data type:

```json
{
    "new_type_name": "my_account_name",
    "type": "name"
}
```

So in this ABI file, we defined a type name named  `my_account_name` ,the type is `name`, `new_type_name` and `type` are keywords, type `name` is the data type defined by system.

## Conclusion

So, a complete ABI file is now written. 

```json
{
    "version": "eosio::abi/1.0",
    "types": [{
        "new_type_name": "my_account_name",
        "type": "name"
    }],
    "structs": [{
        "name": "player",
        "base": "",
        "fields": [{
            "name": "nickname",
            "type": "my_account_name"
        }, {
            "name": "age",
            "type": "int32"
        }]
    }, {
        "name": "hi",
        "base": "",
        "fields": [{
            "name": "nickname",
            "type": "my_account_name"
        }]
    }],
    "actions": [{
        "name": "hi",
        "type": "hi",
        "ricardian_contract": ""
    }],
    "tables": [{
        "name": "players",
        "type": "player",
        "index_type": "i64",
        "key_names": ["id"],
        "key_types": ["int64"]
    }] 
};
```

Through this ABI file, we defined an action method, it has 3 strings: id, nickname, age; types are: int64, my_account_name, int32; a data table player main key is id and a Passing parameters of nickname, type is my_account_name and the name is hi. 