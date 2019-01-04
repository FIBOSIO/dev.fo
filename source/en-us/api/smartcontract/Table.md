---
title: table
type: manual
language: en
order: 9
---
# Table Object
multi index table object

## Member Attribute

### name
**table name**

**Type：String**


Example：

```javascript
exports.hi = v => {
    var players = db.players(action.account, action.account); 
    console.log(players.name);
};
```



### code

**Point to the name of the contract issuer**

**Type: String**


Example：

```javascript
exports.hi = v => {
    var players = db.players(action.account, action.account); 
    console.log(players.code);
};
```



### scope

**account_name belongs to the data of table**

**Type: String**


```javascript
exports.hi = v => {
    var players = db.players(action.account, action.account); 
    console.log(players.scope);
};
```



### indexes

**Query the current index，return all index object，Each index is a new Table object**

**Type: Object**


```javascript
exports.hi = v => {
    var players = db.players(action.account, action.account); 
    console.log(players.indexes);
};
```



## member function

### emplace

**save new data to table**

```JavaScript
Table.emplace(payer,val);
```

Parameter Usage:
* payer: String, the account pays for this operation
* val: Object, the value will save in table

Example：

```JavaScript
exports.hi = v => {
    var players = db.players(action.account, action.account);
    players.emplace(action.account, {
        title: "ceo",
        age: 48,
        nickname: "lion1",
        id: 123
    });
};
```



### find

**find data from table**

```JavaScript
Table.find(id);
```

Parameter Usage:
* id: Value, Query parameters

Results：
* [DBIterator](dbiterator.html)，return a database iterator

Example:

```JavaScript
exports.hi = v => {
    var players = db.players(action.account, action.account);
    console.log(players.find(v).data)
};
```



### get_primary_key

**Generate an autoincrement primary key**

```JavaScript
Table.get_primary_key();
```

Example:

```JavaScript
exports.hi = v => {
    var players = db.players(action.account, action.account);
    console.log(players.get_primary_key())
};
```



### lowerbound

**Find the result less than parameter from the table**

```JavaScript
Table.lowerbound(id);
```

Parameter Usage:
* id: Value, Query parameters

Results：
* [DBIterator](dbiterator.html)，return a database iterator

Example:

```JavaScript
exports.hi1 = v => {
    var players = db.players1(action.account, action.account);
    var data = players.lowerbound(123);
    console.log(data.data, data1.data);
};
```



### upperbound

**find results that greater than parameter from table**

```JavaScript
Table.upperbound(id);
```

Parameter Usage:
* id: Value, Query parameters

Results：
* [DBIterator](dbiterator.html)，return a database iterator

Example:

```JavaScript
exports.hi1 = v => {
    var players = db.players1(action.account, action.account);
    var data1 = players.upperbound(123);
    console.log(data.data, data1.data);
};
```



### toString

**Return a string representation of an object，General return "[Native Object]"，Objects can be reimplemented according to their own characteristics**

```JavaScript
Table.toString();
```

Results:
* String, string of returning object

Example：

```javascript
exports.hi1 = v => {
    var players = db.players1(action.account, action.account);
    console.log(players.toString());
};
```





### toJSON

**JSON format of returning object，Returns a collection of readable properties defined by an object**

```JavaScript
Table.toJSON(key);
```

Parameter Usage:
* key: String, Not used

Results:
* Value, return the value that can be json serialized

Example：

```javascript
exports.hi1 = key => {
    var players = db.players1(action.account, action.account);
    console.log(players.toJSON(key));
};
```



