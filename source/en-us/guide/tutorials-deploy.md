---
title: Deploy Contracts
type: tutorials
language: en
order: 14
---

In the previous article, we have finished the js contract code and ABI file, and initiated the local test node. 
Now, we will deploy the contract to the environment and test the contract.


## Create an account

Create `config.js` under the root directory and save the following code for configuring the basic information.

```javascript
const config = {
    client: {
        chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
        httpEndpoint: 'http://127.0.0.1:8888',
        keyProvider: '5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3'
    },
    contract: {
        name: 'todo',
        sender: 'todo'
    },
    testContract:{
        name: 'testtodo',
        sender: 'testtodo'
    },
    account: {
        publicKey: 'FO6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV',
        privateKey: '5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3'
    }
}

module.exports = config
```

The release of contract needs to be performed via a fibos account, so initially, we need to create a fibos account and call the method of `newaccountSync()` to create the contract account.

Create a new folder named `scripts`，and save the code to `scripts/deploy.js`:

```js
const FIBOS = require('fibos.js');
const config = require('../config');
const fibosClient = FIBOS(config.client);
const fs = require('fs');

fibosClient.newaccountSync({
    creator: 'eosio',
    name: 'todo',
    owner: config.account.publicKey,
    active: config.account.publicKey,
});
```



## Compile the contract

We can read the js contract file via the fs module and compile the contract into a wasm file by method of `compileCode()`. 

Save the following code to `scripts/deploy.js` ：

```js
const jsCode = fs.readTextFile(`${__dirname}/../contracts/todo.js`);
const wasm = fibosClient.compileCode(jsCode);
```

### Deploy wasm file

Call `setcodeSync()` method to deploy wasm file to the node. 

Save the following code to `scripts/deploy.js` ：

```js
fibosClient.setcodeSync(config.contract.name, 0, 0, wasm);
```

### Obtain js files. 

Use `getCodeSync()` method to read js files，and it is suggested to compare the js files with the provided js contracts from projects and see whether the two are consistent with each other.

Save the following code to `scripts/deploy.js` ：

```js
const code = fibosClient.getCodeSync(config.contract.name, true);
console.log(code);
```


## Deploy contracts

We need to deploy the compiled wasm and ABI files to the node.


### 部署 ABI 文件

Obtain the ABI file using the fs module and deploy the ABI file to the node via  
`setabiSync()` 

Save the following code to `scripts/deploy.js` ：

```js
const abi = JSON.parse(fs.readTextFile(`${__dirname}/../contracts/todo.js`));
fibosClient.setabiSync(config.contract.name, abi);
```

Run command 

```javascript
fibos-todomvc$ fibos  scripts/deploy.js
```

> Note: A new window is required to ensure that the node.js is working properly. If an account already exist error is reported, it is suggested to close the node and restart `fibos  start_fibos/node.js`.

Output (partial):

```
code: {
  "account_name": "todo",
  "code_hash": "383a12daacaf124eea9afc529822d990853b5b99570401b8394534b746ea3977",
  "wast": "",
  "wasm": "504b03042d00000008002cadfe4c6a9400a2360000003900000008001400696e6465782e6a7301001000000000000000000000000000000000004bad28c82f2a29d6cbc854b055282d4e2d52b0b55348cecf2bcecf49d54b2d2aca2fd250cfcc0389941425269758a9eb8055695a0300504b010200001400000008002cadfe4c6a9400a23600000039000000080000000000000001000000000000000000696e6465782e6a73504b0506000000000100010036000000700000000000"
}

```

So far, the contract has been successfully deployed to the node! 

The GitHub source code of this article: under `scripts` folder of 
<https://github.com/fengluo/fibos-todomvc> 

**Next Chapter**
👉 【[Test Contract](testcase.html)】

