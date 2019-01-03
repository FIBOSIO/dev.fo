---
title: 数据库
type: tutorials
language: zh-cn
order: 202
---

##  介绍

- 为了将数据持久化到数据库中，并提供数据可查询的能力和服务，我们将引用 FIBOS 中的 db 模块。
- 数据库操作需要3个模块，分别是：db, table and DBIterator。

## 访问数据库 

```javascript
const table = db.table(scope, code, indexes);
```

- table：abi 文件中定义数据表的表名
- scope： 指向合约发布者的名称
- code：table 中数据所属的 account_name
- index：索引

db 是 FIBOS 中的全局模块，我们在 abi 文件中定义的数据表都会被挂载在 db 模块下，这样我们就可以通过 db 模块访问 abi 文件中定义的数据表。

下面我们将演示对数据表进行增删改查操作：

> 对数据表进行的操作是写在 JS 合约里！

### 保存

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

通过 `table` 模块下的 `emplace` 函数向数据表中存入数据。

### 查看

```javascript
exports.find = param => {
    var players = db.players(action.account, action.account);
    var record_id = 123;
    var itr = players.find(record_id);
    console.log('find =>', itr.data);
};
```

通过 `table` 模块下的 `find` 函数从数据表中查找数据，返回的是一个 [DBIterator](../api/smartcontract/dbiterator.html)。 [DBIterator](../api/smartcontract/dbiterator.html) 中的 data 属性展示了我们要查询的数据。详解请参考 API 中的 [DBIterator](../api/smartcontract/dbiterator.html)。

### 修改

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

通过 `DBIterator` 模块下的 `update` 函数从数据表中修改数据，我们可以通过查找该数据，再对 [DBIterator](../api/smartcontract/dbiterator.html)中的 data 属性进行修改，最后通过 `update` 进行保存修改。

### 删除

```javascript
exports.remove = param => {
    var players = db.players(action.account, action.account);
    var record_id = 123;
    var itr = players.find(record_id); 
    itr.remove();
};
```

通过 `DBIterator` 模块下的 `remove` 函数从数据表中进行删除指定数据。

## 建立索引

```javascript
const indexes = {
   detail1:[128, o => [o.age,o.weight]],
};

exports.hi = v => {
     var players = db.players(action.account, action.account, indexes);
}
```

上述代码定义了一个或多个索引，访问表的时候加上 indexes 这个参数，这样在对表操作的时候就可以使用索引了。

**基于索引查询**

```javascript
var itr = players.indexes.age.find({age:48,weight:100});
console.log(itr.data);
```

## 总结

* 模块 db 是 FIBOS 中的基础模块 — 数据库访问模块，可用于创建和操作数据库资源。
* 通过 db 对象可以对数据表进行增删改查操作。
