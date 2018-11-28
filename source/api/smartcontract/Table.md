---
title: table
type: manual
order: 9
---
# 对象 Table
multi index table 对象

## 成员属性
        
### name
**table 名**

**类型：String**

```JavaScript
readonly String Table.name;
```

--------------------------
### code
**指向合约发布者的名称**

**类型：String**

```JavaScript
readonly String Table.code;
```

--------------------------
### scope
**table 中数据所属的 account_name**

**类型：String**

```JavaScript
readonly String Table.scope;
```

--------------------------
### indexes
**查询当前索引，返回所有索引对象，每个索引是一个新的 Table 对象**

**类型：Object**

```JavaScript
readonly Object Table.indexes;
```

## 成员函数
        
### emplace
**向 table 存入新数据**

```JavaScript
Table.emplace(String payer,
    Object val);
```

调用参数:
* payer: String, 为此次操作付费的账户
* val: Object, 将要存入到 table 的值

实例：

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

--------------------------
### find
**从 table 查找数据**

```JavaScript
DBIterator Table.find(Value id);
```

调用参数:
* id: Value, 查询的参数

实例:

```JavaScript
exports.hi = v => {
    var players = db.players(action.account, action.account);
    console.log(players.find(v).data)
};
```

--------------------------
### get_primary_key
**生成自增主键**

```JavaScript
Value Table.get_primary_key();
```

实例:

```JavaScript
exports.hi = v => {
    var players = db.players(action.account, action.account);
    console.log(players.get_primary_key())
};
```

--------------------------
### lowerbound
**从 table 查找小于参数结果**

```JavaScript
DBIterator Table.lowerbound(Value id);
```

调用参数:
* id: Value, 查询的参数

实例:

```JavaScript
exports.hi1 = v => {
    var players = db.players1(action.account, action.account);
    var data = players.lowerbound(123);
    console.log(data.data, data1.data);
};
```

--------------------------
### upperbound
**从 table 查找大于参数结果**

```JavaScript
DBIterator Table.upperbound(Value id);
```

调用参数:
* id: Value, 查询的参数

实例:

```JavaScript
exports.hi1 = v => {
    var players = db.players1(action.account, action.account);
    var data1 = players.upperbound(123);
    console.log(data.data, data1.data);
};
```

--------------------------
### toString
**返回对象的字符串表示，一般返回 "[Native Object]"，对象可以根据自己的特性重新实现**

```JavaScript
String Table.toString();
```

返回结果:
* String, 返回对象的字符串表示

--------------------------
### toJSON
**返回对象的 JSON 格式表示，一般返回对象定义的可读属性集合**

```JavaScript
Value Table.toJSON(String key = "");
```

调用参数:
* key: String, 未使用

返回结果:
* Value, 返回包含可 JSON 序列化的值

