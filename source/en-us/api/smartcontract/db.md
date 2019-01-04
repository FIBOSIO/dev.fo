---
title: db
type: manual
language: en
order: 6
---
# db module
db object

Database accessing object

JS smart contract operation chain database is a common application scenario in FIBOS，one [action](index.html) context variables appear during execution，Including transaction mechanism processing，This content applies the allocated memory resources，and if there is not persistence technique，This context data is lost when the scope is exceeded. So the persistence technique is required to record the key content into chain database. It will not be affected at anytime you use it. The usage of db module is to record data persistently into database, and provide the query capabilities and service for data.

## static function
        
### table
**Access specific data table**

```JavaScript
db.table(scope,code,indexes);
```

Parameter Usage:
* scope: String, Point to contract issuer name
* code: String, the account_name belongs to table
* indexes: object, index

First we need to define the information of data table such as table name, table structure and the primary key in abi file while using db module as shown below:
```
var db_abi = {
      "version": "eosio::abi/1.0",
      "types": [{
          "new_type_name": "my_account_name",
          "type": "name"
      }],
      "structs": [{
          "name": "player2",
          "base": "",
          "fields": [{
              "name": "title",
              "type": "string"
          }, {
              "name": "age",
              "type": "int32"
          }, {
              "name": "weight",
              "type": "int32"
          }, {
              "name": "length",
              "type": "int32"
          }, {
              "name": "width",
              "type": "int32"
          }]
      }, {
          "name": "hi",
          "base": "",
          "fields": [{
              "name": "user",
              "type": "name"
          }]
      }],
      "actions": [{
          "name": "hi",
          "type": "hi",
          "ricardian_contract": ""
      }],
      "tables": [{
          "name": "players",
          "type": "player2",
          "index_type": "i64",
          "key_names": ["id"],
          "key_types": ["int64"]
      }]
  };
```
We defined a players table in db_abi, the type of the table is player2, and the primary key is id.

So how do we access some specific table in js contract? Take example of accessing players table, we only need:
`db.players(scope,code)` .

同样给表建立索引也很简单，以 players 表为例，在 js 合约中作如下定义:
As the same, this very easy to build index to a table, take the example of players table, Make the following definition in the js contract: 

```
const indexes = {
     age: [64, o => [o.age]]
};

exports.hi = v => {
     var players = db.players(action.account, action.account, indexes);
}
```

The code above defines an index called age and adds the indexes parameter when accessing the table, so that it can be used when operating on the table.

DB module also supports multi-index, only need to add other index in indexes as below:
```
const indexes = {
   age:[64, o=>[o.age]],
   detail1:[128, o => [o.age,o.weight]],
   detail2:[192, o => [o.age,o.weight,o.length]],
   detail3:[256, o => [o.age,o.weight,o.length,o.width]]
};
```

The details about how to do CRUD operation, please check [DBIterator](dbiterator.html) and [Table](Table.html)