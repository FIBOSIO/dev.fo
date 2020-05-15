---
title: 测试合约
type: tutorials
language: zh-cn
order: 15
---
不写自动测试用例的程序员不是一个好的测试工程师。我们鼓励所有的项目在启动最初，就建立完整的自动化测试用例。随着项目的发展，前期的投入会得到数百倍的回报。

接下里我们将针对上文编写的 todo 合约，使用 FIBOS 的测试框架编写相应的测试用例。


新建 `test` 文件夹，保存代码至 `test/index.js`:

## 用例名定义

通过 describe(name, () => {}); 方法来定义一个测试用例的名称和框架。每一个 describe 中的上下文环境都是干净的。

```js
describe('todo', () => {})
```

## 环境准备

我们在 before(() => {}) 中定义一些用例开始前需要做的一些准备。

备注：`config.js` 配置文件已经在上一章 [部署合约](./tutorials-deploy.html) 里配置完成。

```js
var FIBOS = require('fibos.js');
var config = require('../config');
var fs = require('fs');
var test = require('test');
test.setup();

describe('todo', () => {
    var fibosClient; 
    before(() => {
        fibosClient = FIBOS({
            chainId: config.client.chainId, // 32 byte (64 char) hex string
            keyProvider: config.client.keyProvider, 
            httpEndpoint: config.client.httpEndpoint,
            logger: {
                log: null,
                error: null
            }
        }); 
        fibosClient.newaccountSync({
            creator: 'eosio',
            name: config.testContract.name,
            owner: config.account.publicKey,
            active: config.account.publicKey,
        });
     // setcode
     const jsCode = fs.readTextFile('../contracts/todo.js');
     fibosClient.setcodeSync(config.testContract.name, 0, 0, fibosClient.compileCode(jsCode));
     
     // setabi
     const abi = JSON.parse(fs.readTextFile('../contracts/todo.abi'));
     fibosClient.setabiSync(config.testContract.name, abi);
    });
})
```

上述代码，我们创建了一个 fibos 账号并且部署合约。

## 单元用例编写

每个 it 都相当于一个单元用例，分别对 todo 合约中的四个方法进行了测试。

```js
describe('todo', () => {
    var fibosClient; 
    before(() => {
        ...
        ...
        ...
    });
    it('insert data', () => {
        var ctx = fibosClient.contractSync(config.testContract.name);
        ctx.emplacetodoSync(1,'say something',0, {
            authorization: config.testContract.name
        });
        console.notice('fibos.getTableRowsSync(true, config.testContract.name, user1, todos)',
        fibosClient.getTableRowsSync(true, config.testContract.name, config.testContract.sender, 'todos'));
    });

    it('find data', () => {
        var ctx = fibosClient.contractSync(config.testContract.name);
        ctx.findtodoSync(1,{
            authorization: config.testContract.name
        })
        console.notice('fibos.getTableRowsSync(true, config.testContract.name, user1, todos)', 
        fibosClient.getTableRowsSync(true, config.testContract.name, config.testContract.sender, 'todos'));
    });

    it('user modofy record', () => {
        var ctx = fibosClient.contractSync(config.testContract.name);
        ctx.updatetodoSync(1,'done',1,{
            authorization: config.testContract.name
        })
        assert.isTrue(fibosClient.getTableRowsSync(true, config.testContract.name, config.testContract.sender, 'todos').rows.length === 1);
    });

    it('user delete record', () => {
        var ctx = fibosClient.contractSync(config.testContract.name);
        ctx.destorytodoSync(1,{
            authorization: config.testContract.name
        })
        assert.isTrue(fibosClient.getTableRowsSync(true, config.testContract.name, config.testContract.sender, 'todos').rows.length === 0);
    });
});


require.main === module && test.run(console.DEBUG);
```

运行命令

```
fibos-todomvc$ fibos test/index.js
```



## 结果展示

在测试代码中，我们分别对合约提供的增删改查四个方法进行了测试。并输出如下结果（节选）：

```j&#39;s
is_producing_block: 1, tm: 16.138
is_producing_block: 1, tm: 15.834
========> time: 0.53
2018-10-16T06:41:20.984 thread-1   apply_context.cpp:28          print_debug          ]
[(todolistdapp,destory)->todolistdapp]: CONSOLE OUTPUT BEGIN =====================
todos# 1n  removed

[(todolistdapp,destory)->todolistdapp]: CONSOLE OUTPUT END   =====================
    √ user delete record (211ms)

  √ 4 tests completed (3709ms)
```

本文 GitHub 源码：<https://github.com/fengluo/fibos-todomvc> 下的 `test` 文件夹。

**下一章节**
👉 【[开发 DApp 客户端](./tutorials-usecontract.html)】