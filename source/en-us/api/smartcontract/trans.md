---
title: trans
type: manual
language: en
order: 10
---
# trans module
trans module provides 2 methods to call between functions，Where the send_inline method requires user authorization and send_context_free_inline does not。

## Static function

### send_inline
**send inline [action](index.html) to specific account**

```javascript
trans.send_inline(account,name,args,authorization);
```

Parameter Usage:

- account: String, [action](index.html) sender account name
- name: String, [action](index.html) name
- args: Object, [action](index.html) required parameters
- authorization: Array, [action](index.html) permission

**Example**

```JavaScript
// hi acction
exports.hi = (user, friend) => {
  //  Trigger hi2 action
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
**send context_free inline [action](index.html) to specific account**

```javascript
trans.send_context_free_inline(account,name,args):
```

Parameter Usage:

- account: String, [action](index.html) sender account name
- name: String, [action](index.html) name
- args: Object, [action](index.html) required parameters

**Example**

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



