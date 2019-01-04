---
title: DBIterator
type: manual
language: en
order: 7
---
# DBIterator Object

## Member attribute

### data
**Query the current data and return all data objects, each of which is a new DBIterator object**

**Type: Object**

```JavaScript
DBIterator.data;
```

Example: 
```JavaScript
exports.hi1 = v => {
    var players = db.players(action.account, action.account);
    var itr = players.find(v);
    console.log(itr.data);
}；
```

## Member attribute

### is_begin
**Check whether it is the begin of data**

**Type: Boolean**

```JavaScript
DBIterator.is_begin();
```

Example: 

```JavaScript
exports.hi1 = v => {
    var players = db.players(action.account, action.account);
    var itr = players.find(v);
    console.log(itr.is_begin());
}；
```


### is_end
**Check whether it is the end of data**

**Type: Boolean**

```JavaScript
DBIterator.is_end();
```

Example: 

```JavaScript
exports.hi1 = v => {
    var players = db.players(action.account, action.account);
    var itr = players.find(v);
    console.log(itr.is_end());
}；
```


### next
**Get next data**

```JavaScript
DBIterator.next();
```

Example: 

```JavaScript
exports.hi1 = v => {
    var players = db.players(action.account, action.account);
    var itr = players.find(v);
    var itr1 = itr.next();
    console.log(itr1.toJSON());
}；
```


### previous
**get previous data**

```JavaScript
DBIterator DBIterator.previous();
```

Example: 

```JavaScript
exports.hi1 = v => {
    var players = db.players(action.account, action.account);
    var itr = players.find(v);
    var itr1 = itr.next();
    var itr2 = itr1.previous();
    console.log(itr2.toJSON());
}；
```


### remove
**remove data**

```JavaScript
DBIterator.remove();
```

Example: 

```JavaScript
exports.hi1 = v => {
    var players = db.players(action.account, action.account);
    var itr = players.find(v);
    itr.remove();
}；
```


### update
**update data**

```JavaScript
DBIterator.update(payer);
```

Parameters Usage:
* payer: String, the account pays for this operation

Example: 

```JavaScript
exports.hi1 = v => {
    var players = db.players(action.account, action.account);
    var itr = players.find(v);
    itr.data.age = 18;
    itr.update(action.account);
}；
```


### toString
**Return a string representation of an Object，typically "[Native Object]"，Objects can be reimplemented according to their own characteristics**

```JavaScript
DBIterator.toString();
```

Results: 
* String, Return a string representation of an object


### toJSON
**Return a JSON format representation of an object, which typically returns a collection of human-readable properties defined by the object**

```JavaScript
DBIterator.toJSON(key);
```

Parameters Usage:
* key: String, Not used

Results: 
* Value, Return a value that contains json serialized values


