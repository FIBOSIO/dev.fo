---
title: 账户权限
type: tutorials
order: 202
---

跟所有的系统设计一样，我们也会在智能合约开发中需要对账户验证权限。[action](../api/smartcontract/index.html) 模块中提供了多个函数可以满足我们的需求。

## 验证账户是否存在

在验证账户权限之前，我们可以先确认账户的有效性。[action](../api/smartcontract/index.html) 模块的 `is_account` 函数可以帮你轻松实现。

```javascript
exports.hi = account => {
  if (action.is_account(account)) {
    console.notice("account exists");
  } else {
    console.error("account notexists");
  }
};
```

## 验证账户授权

就像传统系统中需要检查用户登陆情况，智能合约开发中也可以检查用户账户的授权。我们可以使用 `has_auth` 函数来检查 `action` 是否需要指定账户的授权。

```javascript
exports.hi = account => {
  if (action.has_auth(account)){
    console.notice("action be authed");
  }
};
```

## 验证账户权限

如果只是验证账户授权，[action](../api/smartcontract/index.html) 模块中的 `require_auth` 函数可以实现跟 `has_auth` 类似的效果。不过这两者还是有所不同。

1. `has_auth` 验证没有指定账户授权，会返回 `false` 的布尔值。而 `require_auth` 添加指定账户失败后会抛出异常，中断执行后退出合约。

2. `require_auth` 函数不仅可以检查账户是否授权，还可以检查账户是否提供了相应权限。

FIBOS 账户有2种原生权限： `owner`、`active`。

* `owner` 拥有超级权限，代表着账户的归属者，因为拥有此权限者可以用于操作其他权限配置，该权限常用事务中（转账、合约 action 等）一般不会使用。
* `active` 常用业务的权限，比如：转账、投票等。

下面的代码示例中，如果客户端调用合约方法 `hi` 的时候，没有提供所传参数 `account` 对应账户的授权，合约会抛出异常，中断执行。
```javascript
exports.hi = account => {
  action.require_auth(account);
  console.log("auth success");
};
```

下面的代码示例中，`require_auth` 要求提供 `account` 对应账户的 `active` 权限。否则会抛出异常，中断执行。

```javascript
exports.hi = account => {
  action.require_auth(account, 'active');
  console.log("action be authed");
};
```

当然除了默认的两种原生权限，开发者也可以给账户添加自定义权限，然后在合约中验证。