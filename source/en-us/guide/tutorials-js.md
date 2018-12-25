---
title: Smart Contract——JS Contract
type: tutorials
language: en
order: 13
---
> Important Note：
> The time in the JS contract is UTC time. If you desire to show other time zones, please add the time difference manually!

In the previous ABI file, we have designed actions, tables, structs, and types. The data stored in the table is as todo and is lastly stored in the database table.
The JS contract is used to apply the method of defining the action in the ABI file. 


Under the `contracts` folder，save the code to `contracts/todo.js`:


## Emplace information

The method for defining the action of emplacetodo in the ABI file is used to emplace data to the todo table, including the fields id(int64), text(string), completed(bool).

**Code: Write a JS contract to apply the emplacetodo method**

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

The todos.emplace(action.account,{text,completed,id}) refers to the method of emplacing information to table in fibos.js.


**emplace function descriptions:**

Table.emplace(String payer,Object val);

Call parameters:

payer: String, the account that will pay for this operation.

val: Object, refers to the value to be stored in table.


## Query Information

The method of defining the action of findtodo in the ABI file is used to find the information about the todo table, including the fields id(int64).


**Code: Write a JS contract to apply the findtodo method**

```javascript
exports.findtodo = (id) => {
    var todos = db.todos(action.account, action.account);
    console.log(todos.find(id))
};
```

The todos.find(id) refers to the method to query the table in fibos.js.

**get function descriptions:**

DBIterator Table.find(Value id);

Call parameters:

- id: Value,  refers to the parameters to be found. 


## Update information

The method of defining the action of updatetodo in the ABI file is used to modify the data of todo table, including the fields id(int64), text(string)， completed(bool).


**Code: Write a JS contract to apply the updatetodo method**

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

The todos.update(id,action.account,{text,completed,id}); refers to the method of modifying the information in the table in fibos.js.

**modify function descriptions：**

DBIterator Table.modify(Value id,String payer,Object val);

Call Parameters:

- id:Value, refers to the parameters to be modified.
- payer:String, refers to the account that will pay for this operation.
- val：Object, refers to the value to be stored in table. 


## Destroy Information

The method of defining the action of destroytodo in the ABI file is used to destroy the data of todo table, including the fields id(int64).


**Code: Write a JS contract to apply the destroytodo method**

```javascript
exports.destorytodo = (id) => {
    var todos = db.todos(action.account, action.account);
    var itr = todos.find(id);
    itr.remove();
    console.log('todos#', id, 'removed');
};
```

The todos.remove(id) refers to the method of removing the information in the table in fibos.js.

**remove function description：**

DBIterator.remove(Value id);

Call parameters:

- id: Value, refers to the parameters to be destroyed.


## JS contract code example

The following code is saved to contracts/todo.js, and used to process the information about the defined todo table in the contract ABI.

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
The GitHub source code of this article: under `contracts` folder of
 <https://github.com/fengluo/fibos-todomvc> 

**Next Chapter**
👉 【[Deploy Contract](deploy.html)】