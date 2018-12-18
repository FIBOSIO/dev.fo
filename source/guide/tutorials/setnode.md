---
title: 搭建本地测试节点
type: tutorials
order: 11
---

>注意：**搭建节点前请确保本地安装 FIBOS 【[安装运行环境](../installation/installation.html)】**

启动一个本地 FIBOS 节点，这样你就能在本地开发 FIBOS 的具体内容了，实际开发环境中，需要通过下面的不同插件来开发 FIBOS 节点。

新建 `start_fibos` 文件夹，保存代码至 `start_fibos/node.js`:

```javascript
var fibos = require('fibos');
```

## 配置 HTTP 服务 

http 插件

如：http-server-address 用于配置本地服务地址，默认值为127.0.0.1:8888。

```javascript
fibos.load('http', {
   'http-server-address':'0.0.0.0:8888'
});
```
**具体 http 配置信息请参考 [http 插件](../../api/fibos/index.html#http插件)**

## 配置区块信息

chain 插件

如：delete-all-blocks 用于确定是否删除所有状态数据和区块数据，默认值为 false。

```javascript
fibos.load('chain',{
   'delete-all-blocks':true
});
```

**具体 chain 配置信息请参考 [chain 插件](../../api/fibos/index.html#chain插件)**

## 获取 P2P 信息

net 插件

p2p-listen-endpoint 用于监听 p2p 链接的地址和端口，默认值为：0.0.0.0:9876。

```javascript
fibos.load('net',{
   'p2p-listen-endpoint':'0.0.0.0:9876'
})
```
**具体 net 配置信息请参考 [net 插件](../../api/fibos/index.html#net插件)**

## 控制区块生产的信息

producer 插件

producer-name：控制节点出块的账户名。

enable-stale-production：启用产生区块,即使区块是静止的。

```javascript
fibos.load('producer', {
   'producer-name': 'eosio',
   'enable-stale-production': true
});
```
**具体 producer 配置信息请参考 [producer 插件](../../api/fibos/index.html#producer插件)**

## 修改及查看 FIBOS 配置以及数据目录

fibos.data_dir：fibos 的数据存放目录。

fibos.config_dir：fibos 的配置存放目录。

```javascript
fibos.config_dir = 'fibos_config_dir/';
fibos.data_dir = 'fibos_data_dir/';
```

## JS 智能合约状态

Boolean, 查询和设置 JavaScript 智能合约状态，为 True 时支持 JavaScript 智能合约。

```javascript
fibos.enableJSContract = true;
```

## 启动节点
```javascript
fibos.start();
```

## 高级配置
- 修改 FIBOS 监听端口以及地址

  开启 HTTP 服务对所有地址的 8889 端口监听

  开启 P2P 服务对所有地址的 9877 端口监听

```javascript
fibos.load('http', {
    'http-server-address': '0.0.0.0:8889'
});

fibos.load('net', {
    'p2p-listen-endpoint': '0.0.0.0:9877'
});
```

- 修改及查看 FIBOS 配置以及数据目录

```javascript
// 查看 FIBOS 配置以及数据目录
console.notice('config_dir:', fibos.config_dir);
console.notice('data_dir:', fibos.data_dir);

// 修改 FIBOS 配置以及数据目录
fibos.config_dir = 'fibos_config_dir/';
fibos.data_dir = 'fibos_data_dir/';
```

- 设置 FIBOS 服务启动时重置环境数据

```javascript
fibos.load('chain', {
    'delete-all-blocks': true
});
```

[更多插件请点击这里](../../api/fibos/index.html)


## 节点代码实例

下面代码存为 start_fibos/node.js，用来启动一个本地 FIBOS 节点。

```javascript
var fibos = require('fibos');

fibos.load('http', {
   'http-server-address': '0.0.0.0:8888',
   "access-control-allow-origin": "*"
});
fibos.load('chain', {
   'delete-all-blocks': true
});
fibos.load('net');
fibos.load('chain_api');
// fibos.load('history_api');
fibos.load('producer', {
   'producer-name': 'eosio',
   'enable-stale-production': true
});
fibos.config_dir = 'start_fibos/fibos_config_dir/';
fibos.data_dir = 'start_fibos/fibos_data_dir/';
fibos.enableJSContract = true;
fibos.start();
```
>注意：如后面开发和测试遇见问题，请重启 FIBOS 节点服务再尝试！

运行 FIBOS 开发环境：

```
fibos-todomvc$ fibos start_fibos/node.js
```

运行结果日志（部分）

```
fibos-todomvc$ fibos start_fibos/node.js
……
2018-07-30T03:29:01.004 thread-1   producer_plugin.cpp:1194      produce_block        ] Produced block 00000002e091c956... #2 @ 2018-07-30T03:29:01.000 signed by eosio [trxs: 0, lib: 0, confirmed: 0]
```

如果你看到了以上的消息，说明运行成功，`fibos` 已经开始区块生产。

本文 GitHub 源码：<https://github.com/fengluo/fibos-todomvc> 下的 `start_fibos` 文件夹。

**下一章节**
👉 【[编写 ABI 文件](abi.html)】