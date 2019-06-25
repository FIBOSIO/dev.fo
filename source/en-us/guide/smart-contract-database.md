---
title: Database
type: tutorials
language: en
order: 202
---

##  Introduction

- In order to persist data to the database, and provide the data query capability and services, we will quote the FIBOS db module.
- Database operations require 3 modules, Respectively is: db, table and DBIterator。

## To access the database

```javascript
const table = db.table(scope, code, indexes);
```

- table：The table name of the data table defined in the abi file
- scope： The name of the publisher of contract pointed to
- code：The account_name to which the data in table belongs to
- index：index

db is the global module in FIBOS, The data tables we defined in the abi file will be mounted under the db module, This way we can access the data table defined in the abi file through the db module.

We will demonstrate the addition, deletion and modification of the data table:

> The operation on the data table is written in the JS contract!

### Save

```javascript
exports.emplace = param => {
    var players = db.players(action.account, action.account);
    players.emplace(action.account, { 
        title: 'ceo',
        age:48, 
        nickname:'lion1',
        id:123
    });
};
```

Save the data to the data table via the `emplace` function under the `table` module. 

### View

```javascript
exports.find = param => {
    var players = db.players(action.account, action.account);
    var record_id = 123;
    var itr = players.find(record_id);
    console.log('find =>', itr.data);
};
```

Find data from the data table via the `find` function under the `table` module, Returning a [DBIterator](../api/smartcontract/dbiterator.html).  The data property in [DBIterator](../api/smartcontract/dbiterator.html)  shows the data we want to query. For details, please refer to [DBIterator](../api/smartcontract/dbiterator.html) in the API. 

### Modify

```javascript
exports.update = param => {
    var players = db.players(action.account, action.account);
    var record_id = 123; 
    var itr = players.find(record_id);
    itr.data.title = 'cto';
    itr.data.age = 23;
    itr.update(action.account);
};
```

Modify the data from the data table via the `update` function under the `DBIterator` module, We can modify the data property in [DBIterator](../api/smartcontract/dbiterator.html) by looking up the data, and finally save and modify it with 'update'.

### Delete

```javascript
exports.remove = param => {
    var players = db.players(action.account, action.account);
    var record_id = 123;
    var itr = players.find(record_id); 
    itr.remove();
};
```

The specified data is deleted from the data table via the `remove` function under the `DBIterator` module.

## Set up index

```javascript
const indexes = {
   detail1:[128, o => [o.age,o.weight]],
};

exports.hi = v => {
     var players = db.players(action.account, action.account, indexes);
}
```

The above code defines one or more indexes, Add the indexes parameter when accessing the table, so you can use the index when working on the table.

**Index based query**

```javascript
var itr = players.indexes.age.find({age:48,weight:100});
console.log(itr.data);
```

## Conclusion

* Module db is the base module in FIBOS - a database access module that can be used to create and manipulate database resources.
* The data table can be added, deleted, and changed through the db object.
