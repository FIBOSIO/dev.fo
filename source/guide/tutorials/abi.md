---
title: 智能合约——ABI 文件
type: tutorials
order: 12
---

ABI 全称 Application Binary Interface，中文名“应用程序二进制接口”，顾名思义是一个接口文件，描述了智能合约与上层应用之间的数据交换格式。ABI 文件格式类似 JSON，具备很好的可读性，有利于智能合约工程师与上层应用工程师之间的工作衔接。

对于 JavaScript 合约来说，需要使用 ABI 文件来定义 actions 以及 tables。

智能合约 ABI 文件由 5 部分组成：

```json
{
    "version": "eosio::abi/1.0",
    "structs":[...],            
    "actions":[...],            
    "tables":[...],            
    "types":[...],              
}
```
`version` ：指定 ABI 的版本号。
`structs` ：代表各个类型的数据结构。
`actions` ：声明智能合约调用的 action。
`tables` ：列出智能合约中的数据表名称，以及数据表中所储存的结构体名称。
`types` ：用于自定义数据的类型。

我们将按照 structs -> actions -> tables -> types 的顺序了解 FIBOS 智能合约 ABI 的开发方法。

新建 `contracts` 文件夹，保存代码至 `contracts/todo.abi`:

## structs

structs 部分的内容与 actions 部分的内容存在一一对应的关系，我们需要在 structs 里声明各个 action 需要传入的参数，如下所示。

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

FIBOS 系统会根据 actions 部分中声明的 type ，在 structs 部分寻找对应的数据结构，每个数据结构的 fields 中，会列出每个参数的名称和类型。

除此以外，不光是 actions 里的项目需要在 structs 里列出详细的数据结构，tables 中的项目也需要。

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

这样，在 structs 中，我们就定义了一个名为 todo_index 的 struct，用来列出数据表 todo_index，包含字段 id(int64) ；一个名为 todo 的 struct ，用来列出数据表 todo ，包含字段 id(int64)，text(string)，completed(bool)。

## actions

action 部分的作用是声明智能合约有哪些可以调用的 action。
以下代码实例中 action 定义了添加数据、查找数据、修改数据、删除数据四个方法。

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

其中每一项的 name 就是 action 的名字，type 用来在 structs 中查找数据结构，ricardian_contract 是李嘉图合约。

李嘉图合约是一种特殊的结构化文本，主要用作交易中明确双方的意图。在 FIBOS 上，你所发送的每一条 action，都是可以附加上合约。这种合约很特殊，有着固定的格式，既能够被程序读取，也能为人类阅读。这一合约，就叫做李嘉图合约。

> 注意： action 取名沿用了 eos 的命名规则。
> 目前 action 中 name 命名规则约束：只支持数字 1 ～ 5 和英文小写字母；字符长度最大为 12。

## tables

tables 列出了智能合约中需要建立的数据表名称，以及数据表中所储存的结构体名称。

```json
"tables": [{
    "name": "todos",
    "type": "todo",
    "index_type": "i64",
    "key_names": ["id"],
    "key_types": ["int64"]
}]
```

上述代码构造了一个 table 名是 todos ，结构体类型是 todo，主键名称是 id，主键类型是 int64 的数据表。

## types

types 用于自定义数据的类型：

```json
{
  "new_type_name": "my_account_name",
  "type": "name"
}
```

这样在这个 ABI 文件里就自定义了一个类型名称为 my_account_name 的类型，类型是 name ，new_type_name 和 type 是关键字，类型 name 是系统定义的数据类型。

## ABI 文件代码实例

按照上面的说明，我们编写本文需要的合约，以下代码保存为 contracts/todo.abi。

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

>**注意：ABI 文件请不要添加任何注释，否则会运行报错！**

通过该 ABI 文件，我们就定义了四个 action ，分别为 emplacetodo(todo)、findtodo(todo_index)、updatetodo(todo)、destorytodo(todo_index) ；对应的 struct 主键为 todo_index，有 id(int64)、text(string)、completed(bool) 三个属性。

本文 GitHub 源码：<https://github.com/fengluo/fibos-todomvc> 下的 `contracts` 文件夹。

**下一章节**
👉 【[编写 JavaScript 智能合约](js.html)】
