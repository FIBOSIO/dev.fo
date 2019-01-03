---
title: Notification
type: tutorials
language: en
order: 205
---

The FIBOS notification system can help the communication between smart contracts, also realizing asynchronous decoupling. When a contract is running, it can send notifications to specific accounts, if the corresponding account can deal with it if it accepts the notification. 

## Send Notifications

We can use  `require_recipient` method in  [action](../api/smartcontract/index.html) module to add specific account to the account collection that will be sent notifications. When this contract method is executed, the notifications will be sent to all accounts in this account collection.

Example：

```javascript
exports.hi = v => {
    action.require_recipient(action.receiver);
};
```

## Moniter Notifications

When we need to moniter notification of a contract function, the moniter function is needed. The function name is the name of function that needs to moniter with prefix `on_` . In the example above we defined a function named `hi`, and sent notifications in this function through `require_recipient`. We need to create a function named `on_hi` in the contract to moniter notification, the parameter is the monitered function parameter.

```javascript
exports.on_hi = v => {
    console.log(action.receiver, action.account , v)
};
```

The most common scenario of monitering notification is moniter transfer operations. In the transfer method  of token contract -- `extransfer` function, Notifications will be sent to both account after the transfer is done. Developers can moniter this function to do the notification process after transfer is done, such as: open the corresponding services for user and so on. 

```javascript
exports.on_extransfer = (from, to, quantity, memo) => {
	console.log(from ,to ,quantity, memo);
}；
```

> Tips:
> 1. A contract will receive a notification when the other contract sends it, whether or not there is an ABI definition interface, the notification will be received in the application layer. 
> 2. The notification message sent by one contract to another contract is the message received by rhe contract, includes  `code` , `action` and parameters.
> 3. Accounts handle notification information as well as normal messages. Logical processing is performed according to `code` `action` and parameters.
> 4. The `has_recipient` function can be used to check whether the corresponding account is in the notification account collection.