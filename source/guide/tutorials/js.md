---
title: 智能合约——JS 合约
type: tutorials
order: 13
---
>重要提示：
>JS 合约里的时间是 UTC 时间，如需用到其他时区的时间，请手动添加时间差！

​前面的 ABI 文件中我们设计了 actions 、tables、structs、types。表中存的数据为 todo ，最终存到数据库表里，JS 合约就是用来实现 ABI 文件中定义 action 的方法。

在 `contracts` 文件夹下，保存代码至 `contracts/todo.js`:

## 添加信息

在 ABI 文件中定义了 emplacetodo 的 action 方法，用来给 todo 表添加数据，其中包含字段 id(int64)，text(string)，completed(bool)。

**代码：编写 JS 合约实现 emplacetodo 方法**

```javascript
exports.emplacetodo = (id, text, completed) => {
    var todos = db.todos(action.account, action.account);
    todos.emplace(action.account, {
        text,
        completed,
        id
    });
};
```

内部的 todos.emplace(action.account,{text,completed,id}) 是 fibos.js 向 table 中添加信息的方法。

**emplace 函数描述：**

Table.emplace(String payer,Object val);

调用参数:

payer: String, 为此次操作付费的账户。

val: Object, 将要存入到 table 的值。

## 查找信息

在 ABI 文件中定义了 findtodo 的 action 方法，用来查询 todo 表信息，其中包含字段 id(int64)。

**代码：编写 JS 合约实现 findtodo 方法**

```javascript
exports.findtodo = (id) => {
    var todos = db.todos(action.account, action.account);
    console.log(todos.find(id))
};
```

内部的 todos.find(id) 是 fibos.js 中对 table 查询的方法。

**get 的函数描述:**

DBIterator Table.find(Value id);

调用参数:

- id: Value, 查询的参数。

## 更新信息

在 ABI 文件中定义了 updatetodo 的 action 方法，用来修改 todo 表数据，其中包含字段 id(int64)，text(string)，completed(bool)。

**代码：。编写 JS 合约实现 updatetodo 方法**

```javascript
exports.updatetodo = (id, text, completed) => {
    var todos = db.todos(action.account, action.account);
    var itr = todos.find(id);
    itr.data.text = text;
    itr.data.completed = completed;
    itr.update(action.account);
    console.log('todos#', id, 'updated');
};
```

内部的 todos.update(id,action.account,{text,completed,id}); 是 fibos.js 中对 table 信息的修改方法。

**modify 函数描述：**

DBIterator Table.modify(Value id,String payer,Object val);

调用参数:

- id:Value,修改的参数。
- payer:String，为此次操作付费的账户。
- val：Object，将要存入到table的值。

## 销毁信息

在 ABI 文件中定义了 destorytodo 的 action 方法，用来销毁 todo 表数据，其中包含字段 id(int64)。

**代码：编写 JS 合约实现 destorytodo 方法**

```javascript
exports.destorytodo = (id) => {
    var todos = db.todos(action.account, action.account);
    var itr = todos.find(id);
    itr.remove();
    console.log('todos#', id, 'removed');
};
```

内部的 todos.remove(id) 是 fibos.js 中的对 table 信息的删除方法。

**remove 函数描述：**

DBIterator.remove(Value id);

调用参数:

- id: Value, 要销毁的参数。

## JS 合约代码实例

下面代码保存至 contracts/todo.js ：用来处理合约 ABI 中定义的 todo 表信息。

```javascript
exports.emplacetodo = (id, text, completed) => {
    var todos = db.todos(action.account, action.account);
    todos.emplace(action.account, {
        text,
        completed,
        id
    });
    //console.log('todo#', id, ' created');
};
exports.findtodo = (id) => {
    var todos = db.todos(action.account, action.account);
    console.log(todos.find(id))
};
exports.updatetodo = (id, text, completed) => {
    var todos = db.todos(action.account, action.account);
    var itr = todos.find(id);
    itr.data.text = text;
    itr.data.completed = completed;
    itr.update(action.account);
    console.log('todos#', id, 'updated');
};
exports.destorytodo = (id) => {
    var todos = db.todos(action.account, action.account);
    var itr = todos.find(id);
    itr.remove();
    console.log('todos#', id, 'removed');
};

```
本文 GitHub 源码：<https://github.com/fengluo/fibos-todomvc> 下的 `contracts` 文件夹。

**下一章节**
👉 【[部署合约](deploy.html)】