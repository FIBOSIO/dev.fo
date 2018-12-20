---
title: 部署合约
type: tutorials
order: 14
---

上文中，我们已经写好了 js 合约代码和 ABI 文件，并起了本地的测试节点，下面我们将合约部署到环境上，并对合约进行测试。

## 创建账户

在根目录下，新建 `config.js` 保存以下代码，用来配置基本信息。

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



发布合约需要通过一个 fibos 账号进行发布，所以首先我们需要创建一个 fibos 账户，调用 `newaccountSync()` 方法来进行合约账户的创建。

新建 `scripts` 文件夹，保存代码至 `scripts/deploy.js`:

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



## 编译合约

我们通过 fs 模块读取到 js 合约文件，并通过 `compileCode()` 方法将合约编译成 wasm 文件。

以下代码保存至 `scripts/deploy.js` ：

```js
const jsCode = fs.readTextFile(`${__dirname}/../contracts/todo.js`);
const wasm = fibosClient.compileCode(jsCode);
```

### 部署 wasm 文件

调用 `setcodeSync()` 方法将 wasm 部署到节点上。

以下代码保存至 `scripts/deploy.js` ：

```js
fibosClient.setcodeSync(config.contract.name, 0, 0, wasm);
```

### 获取 js 文件

使用 `getCodeSync()` 方法可以读取到 js 文件，与项目方提供的 js 合约文件对比，看看是否一致。

以下代码保存至 `scripts/deploy.js` ：

```js
const code = fibosClient.getCodeSync(config.contract.name, true);
console.log(code);
```

## 部署合约

我们需要将编译生产的 wasm 文件和 abi 文件部署到节点上。


### 部署 ABI 文件

使用 fs 模块获取 ABI 文件，并通过 `setabiSync()` 将 ABI 文件部署到节点上。

以下代码保存至 `scripts/deploy.js` ：

```js
const abi = JSON.parse(fs.readTextFile(`${__dirname}/../contracts/todo.js`));
fibosClient.setabiSync(config.contract.name, abi);
```

运行命令

```javascript
fibos-todomvc$ fibos  scripts/deploy.js
```
>注意：需新建窗口，保证 node.js 节点正常运行。如果报错 `账户已存在` 请关闭节点，重新启动 `fibos  start_fibos/node.js`。

输出结果（部分）

```
code: {
  "account_name": "todo",
  "code_hash": "383a12daacaf124eea9afc529822d990853b5b99570401b8394534b746ea3977",
  "wast": "",
  "wasm": "504b03042d00000008002cadfe4c6a9400a2360000003900000008001400696e6465782e6a7301001000000000000000000000000000000000004bad28c82f2a29d6cbc854b055282d4e2d52b0b55348cecf2bcecf49d54b2d2aca2fd250cfcc0389941425269758a9eb8055695a0300504b010200001400000008002cadfe4c6a9400a23600000039000000080000000000000001000000000000000000696e6465782e6a73504b0506000000000100010036000000700000000000"
}

```

至此，合约已经并成功部署到节点上了！
本文 GitHub 源码：<https://github.com/fengluo/fibos-todomvc> 下的 `scripts` 文件夹。

**下一章节**
👉 【[测试合约](testcase.html)】

