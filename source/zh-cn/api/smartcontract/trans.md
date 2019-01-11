---
title: trans
type: manual
language: zh-cn
order: 10
---
# 模块 trans
trans 模块提供了两种函数间调用的方法，其中 send_inline 方法需要用户授权，send_context_free_inline 则不需要。

## 静态函数

### send_inline
**向特定帐号发送 inline [action](index.html)**

```javascript
trans.send_inline(account,name,args,authorization);
```

调用参数:

- account: String, [action](index.html) 发送者的帐号名称
- name: String, [action](index.html) 名称
- args: Object, [action](index.html) 所需的参数
- authorization: Array, [action](index.html) 的权限

**实例**

```JavaScript
// hi acction
exports.hi = (user, friend) => {
  // 触发hi2 action
  trans.send_inline(
    'test', 
    'hi2', 
    {
      user: user, 
      friend: friend
    }, 
    [{
      actor: user, 
      permission: 'active'
    }]
  )
};

// hi2 action
exports.hi2 = (user, friend) => {
  console.log(user, friend);
}
```




### send_context_free_inline
**向特定帐号发送 context_free inline [action](index.html)**

```javascript
trans.send_context_free_inline(account,name,args):
```

调用参数:

- account: String, [action](index.html) 发送者的帐号名称
- name: String, [action](index.html) 名称
- args: Object, [action](index.html) 所需的参数

**实例**

```JavaScript
// hi acction
exports.hi = (user, friend) => {
  // 触发hi2 action
  trans.send_context_free_inline(
    'test', 
    'hi2', 
    { 
      user: user, 
      friend: friend 
    }
  );
};

// hi2 action
exports.hi2 = (user, friend) => {
  console.log(user, friend);
}
```



