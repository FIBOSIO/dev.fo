---
title: 通知
type: tutorials
order: 204
---

FIBOS 的通知机制可以帮助智能合约之间的通讯，实现了异步解耦。当合约执行的时候，可以向指定的账户集发送通知，对应账户的合约接受通知的话，可以做相应处理。

## 发送通知

我们可以使用 [action](../api/smartcontract/index.html) 模块中的 `require_recipient` 方法将指定的帐户添加到要通知的帐户集合。当该合约方法被执行时，就会向账户集合所有账户发送通知。

实例：

```javascript
exports.hi = v => {
    action.require_recipient(action.receiver);
};
```

## 监听通知

当我们需要监听某个合约函数的通知，需要在合约中编写监听函数。函数名为需要监听的方法的名称前加 `on_`。例如，上述例子中我们定义了一个名为 `hi` 的函数，并且在该函数中通过 `require_recipient` 发送通知。我们需要在合约创建一个名为 `on_hi` 的函数用以监听通知，其参数是其监听的函数的参数。

```javascript
exports.on_hi = v => {
    console.log(action.receiver, action.account , v)
};
```

监听通知最常使用的场景是监听转账操作。Token 合约的转账方法 —— `extransfer` 函数中转账成功后会对转账的双方账户发送通知。开发者可以监听该函数，做到账后的处理，比如：给用户开通相关服务等。

```javascript
exports.on_extransfer = (from, to, quantity, memo) => {
	console.log(from ,to ,quantity, memo);
}；
```

> Tips:
> 1. 一个合约向另一个合约发出的通知消息会被另一个合约收到，不管有没有 ABI 定义接口，都会在应用层收到。
> 2. 一个合约向另一个合约发送的通知消息就是本合约收到的消息，包括 `code`、`action` 和参数。
> 3. 账户处理处理通知信息和处理正常的消息一样，根据 `code`、`action` 和参数进行逻辑处理。
> 4. 可以使用 `has_recipient` 函数来检查对应账户是否在通知账户集合中。