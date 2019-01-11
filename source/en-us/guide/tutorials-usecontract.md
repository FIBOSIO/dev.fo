---
title: Develop DApp Client
type: tutorials
language: en
order: 16
---

This article uses the front-end framework of React to create a TodoList example, and call the contract to perform the data addition. 
> Note: This article will apply the front-end framework React. If you are not familiar with React, you may learn React first. [React](https://react.docschina.org/) 。

## Obtain the data
In the the file of dapp/components/app.js of the project todomvc,  the getTableRows() method can be used to obtain the data. 

Note: the configuration of file config.js has been completed in the previous chapter of Deployment of Contract.

```javascript
const FIBOS = require('fibos.js');
const config = require('../config');

const fibosClient = FIBOS(config.client)

fibosClient.getTableRows(
      true,
      config.contract.sender,
      config.contract.name,
      'todos').then((data)=>{
        this.setState({todos: data.rows}) //this.setState is method for changing React visual layer
      }).catch((e) => {
        console.error(e)
      }   
)
```

## Call the contract

In the todomvc project, the dapp/components/app.js file is used to call the contract. The contract can be called by the methods of contract().

```js
fibosClient.contract(config.contract.name)
```

Take data inserting as an example, call the emplacetodo method exposed in the contract, and pass in three parameters: id, text, completed. At the same time, authorization should be configured as the account of contract caller.


```js
 fibosClient.contract(config.contract.name).then((contract) => {
      contract.emplacetodo(
        {
          id: todo_id,
          text,
          completed: 0
        },
        { authorization: [config.contract.sender] }
      ).then((res) => {
        const todos = [
          {
            id: todo_id,
            completed: 0,
            text: text
          },
          ...this.state.todos
        ]
        this.setState({todos})   ///this.setState is method for changing React visual layer
       }
      )
      .catch((err) => { console.log(err) })
    }) 
```

## Conclusion

This article takes data addition as an example. For more examples of todo operations you can refer to `dapp`at https://github.com/fengluo/fibos-todomvc!



