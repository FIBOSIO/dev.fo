---
title: 开发 DApp 客户端
type: tutorials
order: 16
---

本文运用前端框架 React 创建了一个 TodoList 示例，并对其调用合约，进行添加数据操作。
> 注意：本文有运用到前端框架 React。如果有对于 React 不熟悉的用户，可以建议先学习 [React](https://react.docschina.org/) 。

## 获取数据
在 todomvc 项目中，dapp/components/app.js 文件。通过 `getTableRows()` 方法来获取数据。

备注：`config.js` 配置文件已经在上一章 [部署合约](deploy.html) 里配置完成。

```javascript
const FIBOS = require('fibos.js');
const config = require('../config');

const fibosClient = FIBOS(config.client)

fibosClient.getTableRows(
      true,
      config.contract.sender,
      config.contract.name,
      'todos').then((data)=>{
        this.setState({todos: data.rows}) //this setState 为React 改变视图层方法
      }).catch((e) => {
        console.error(e)
      }   
)
```

## 调用合约

在 todomvc 项目中，dapp/components/app.js 文件是我们是我们调用合约的地方。通过 `contract()` 方法来获取到合约。

```js
fibosClient.contract(config.contract.name)
```

以插入数据为例，调用合约中暴露的 emplace 方法，并传入 id、text、completed 三个参数。并将 authorization 配置为合约调用者的账户。

```js
 fibosClient.contract(config.contract.name).then((contract) => {
      contract.emplace(
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
        this.setState({todos})   ///this setState 为React 改变视图层方法
       }
      )
      .catch((err) => { console.log(err) })
    }) 
```

## 结语

本文以添加数据为代码示例，更多的 todo 操作示例可以在 <https://github.com/fengluo/fibos-todomvc>下的 `dapp` 文件下学习！



