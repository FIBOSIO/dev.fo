---
title: Test Contract
type: tutorials
language: en
order: 15
---

A developer who does not write automated test cases is not a good test developer. We advocate for complete automated test cases at the beginning of all projects developments. With the development of the project, this early-stage investment will be heavily rewarded with returns hundreds of times the initial.


Next, we will use the FIBOS test framework to write the corresponding test cases in terms of the todo contract written in the foregoing article.


Create a new `test` folder, and save the code to `test/index.js`:


## Definition of name of test cases

Define the name and framework of a test case by using the method of describe(name, () => {});. The context for each describe should be ensured to be clean.

```js
describe('todo', () => {})
```


## Preparation of environment

The preparation should be prior to definition of some cases in before(() => {}).

Remarks: the configuration of file `config.js` has been completed in the previous chapter of Deployment of Contract.

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
    })；
})
```

As shown above, we created a fibos account and finished contract deployment.


## Writing of unit case

Each “it” can be considered as a unit case, respectively testing the four methods in the todo contract.

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

Run the command

```
fibos-todomvc$ fibos test/index.js
```



## Display of results

In the test code, we have tested the four methods of adding, deleting, and modifying and finding of the contract, and output the following results (partial):

```j&#39;s
is_producing_block: 1, tm: 16.138
is_producing_block: 1, tm: 15.834
========> time: 0.53
2018-10-16T06:41:20.984 thread-1   apply_context.cpp:28          print_debug          ]
[(todolistdapp,destory)->todolistdapp]: CONSOLE OUTPUT BEGIN =====================
todos# 1n  removed

[(todolistdapp,destory)->todolistdapp]: CONSOLE OUTPUT END   =====================
    √ user delete record (211ms)

  √ 5 tests completed (3709ms)
```

The GitHub source code of this article: in the `test` folder under <https://github.com/fengluo/ﬁbos-todomvc>

Next chapter 
👉 【[Develop the DApp client](usecontract.html)】
