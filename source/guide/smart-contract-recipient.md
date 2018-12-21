---
title: 通知
type: tutorials
order: 204
---

* Recipient 是 JavaScript 合约通知机制，用户在转账交易时可以给接收者发送消息通知。
* require_recipient 和 has_recipient 分别是模块 action 的静态函数。

## require_recipient

**将指定的帐户添加到要通知的帐户集。**

实例：

```javascript
exports.hi = v => {
    action.require_recipient(action.receiver);
};

exports.on_hi = v => {
    console.log(action.receiver, action.account , v)
};
```

## has_recipient

**当 action 执行成功后，账号是否会收到通知**。

实例：

```javascript
exports.hi = v => {
    if (action.has_recipient(receiver)) console.notice('action received')
    else console.error('action not received');
};
```

## 如何使用

```javascript
const FIBOS = require('fibos.js');

const fibos_client = FIBOS({
  // fibos 主网 chainId
  chainId: 'cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f',
  keyProvider: '你的私钥',
  httpEndpoint: "http://127.0.0.1:8888",
});

var js_code = `exports.on_transfer = (from, to, quantity, memo) => {
	console.log(from ,to ,quantity, memo);
 }`;
fibos_client.setcodeSync(name, 0, 0, fibos.compileCode(js_code));

let ctx = fibos_client.contractSync('eosio.token');
var r = ctx.transferSync(
    'fibostest123',  //通证转入方
    'fibostest321',   //通证转出方
    '1.0000 FO',  //通证数量
    'trasnfer to fibostest321',  //附言
    {
  authorization: 'fibostest123'
});
console.log(r);
```

成功调用合约后，接收方能获取到这笔转账的详细信息。



## 结语

* 一个合约向另一个合约发出的通知消息会被另一个合约收到，不管有没有 ABI 定义接口，都会在应用层收到。
* 一个合约向另一个合约发送的通知消息就是本合约收到的消息，包括 code、action 和参数。
* 账户处理处理通知信息和处理正常的消息一样，根据 code、action 和参数进行逻辑处理。