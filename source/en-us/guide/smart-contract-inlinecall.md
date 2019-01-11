---
title: Call In-contract
type: tutorials
language: en
order: 204
---

Usually we use the client to invoke the contract under the chain to implement our operation. If we want to invoke other contract's methods in the contract, we need to use the  [trans](../api/smartcontract/trans.html) module to implement the internal invocation.

For example, user `fibostest123` defines the following contract functions.

```javascript
exports.hi = name => {
    console.log(name);
}
```

Then the user `fibostest456` can call the `hi` function of the `fibostest123` contract in the following way.

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

There is no need to verify permissions in the `hi` function of the user `fibostest123 `contract, so we can use the `send_context_free_inline` function to exempt authorized invocation of contract methods.

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

The most common scenario for internal invocation is to invoke a Token contract for transfer operations within a contract.

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

Like so we can transfer fund by calling the `helloworld` function.