---
title: 合约内调用
type: tutorials
language: zh-cn
order: 203
---

通常我们会使用客户端在链下调用合约方法来实现我们的操作。如果我们希望在合约里调用其他合约的方法，就需要用到 [trans](../api/smartcontract/trans.html) 模块来实现内部调用。

例如：用户 `fibostest123` 定义了如下合约函数。

```javascript
exports.hi = name => {
    console.log(name);
}
```

那么用户 `fibostest456` 就可以通过如下方式来调用 `fibostest123` 合约的 `hi` 函数。

```javascript
exports.hello = user => {
  trans.send_inline(
    'fibostest123', 
    'hi', 
    {
      name: user,
    }, 
    [
        {
            actor: `fibostest456`, 
            permission: 'active'
        }
    ]);
};
```

用户 `fibostest123` 合约的 `hi` 函数中并没有需要验证权限的地方，所以我们可以使用 `send_context_free_inline` 函数来免授权调用合约方法。

```javascript
exports.hello = user => {
  trans.send_context_free_inline(
    'fibostest123', 
    'hi', 
    {
      name: user,
    });
};
```

内部调用最常用的场景是在合约内部调用 Token 合约进行转账操作。

```javascript
exports.helloworld = (from, to, quantity, memo) => {
    console.log(from, to, quantity, memo);
    trans.send_inline('eosio.token', 'extransfer', {
        from: from,
        to: to,
        quantity: quantity,
        memo: memo
    },
    [
        {
            actor: from,
            permission: 'active'
        }
    ]);
};
```

如此我们就可以通过调用 `helloworld` 函数来进行转账操作了。