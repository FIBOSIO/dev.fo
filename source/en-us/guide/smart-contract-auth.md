---
title: Account Authority
type: tutorials
language: en
order: 203
---

As with all system designs, we also need to validate the rights of accounts in the development of smart contracts. Several functions are provided in the [action](../api/smartcontract/index.html)  module to meet our requirements.

## Verify the existence of an account

Before verifying account permissions, we can confirm the validity of the account. The `is_account` function of the [action](../api/smartcontract/index.html) module can be used to easily implement this.

```javascript
exports.hi = account => {
  if (action.is_account(account)) {
    console.notice("account exists");
  } else {
    console.error("account notexists");
  }
};
```

## Verify Account Authorization

Just as the traditional system needs to check the user's login status, the authorization of user accounts can also be checked in the development of smart contracts. We can use the `has_auth` function to check whether `action` requires authorization for specified account.

```javascript
exports.hi = account => {
  if (action.has_auth(account)){
    console.notice("action be authed");
  }
};
```

## Verify account permissions

If  is only verification of account authorization, the `require_auth` function in the [action](../api/smartcontract/index.html) module can achieve a similar effect as  `has_auth`. But the two are different.

1. If `Has_auth ` verification sees theres no specific account authorization verification, it returns a Boolean value of `false`. When `require_auth` fails to add a specified account, an exception is thrown and the contract is withdrawn after execution is interrupted.
2. `The require_auth ` function checks not only whether the account is authorized, but also whether the account provides the corresponding permissions.

FIBOS accounts have two privileges： `owner`、`active`。

* `owner` Super privileges, represents the owner of the account, because the owner of this privilege can be used to operate other privilege configurations, which are not commonly used in transactions (transfer, contract action, etc.).
* `active` Common business authority, such as: transfer, voting, etc.



In the following code example, if the client invokes the contract method `hi`, the contract throws an exception and interrupts execution without providing authorization for the account corresponding to the passed parameter `account`.

```javascript
exports.hi = account => {
  action.require_auth(account);
  console.log("auth success");
};
```

In the following code example, `require_auth` requires `active` permissions of `account` corresponding accounts. Otherwise, an exception will be thrown and execution will be interrupted.

```javascript
exports.hi = account => {
  action.require_auth(account, 'active');
  console.log("action be authed");
};
```

Of course, in addition to the default two privileges, developers can also add custom privileges to the account, and then validate them in the contract.