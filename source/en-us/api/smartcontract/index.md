---
title: action
type: manual
language: en
order: 1
---
# action module
action object

 Usage：use in js contract of [fibos](../fibos/index.html)

```JavaScript
var js_code = `exports.hi = v => console.error(action.is_account(action.account), action.is_account("notexists"));`;
fibos.setcodeSync(name, 0, 0, fibos.compileCode(js_code));
```

## Static function

### is_account
**check whether the account exist**

```JavaScript
action.is_account(name);
```

Parameter Usage:
* name: String, account name

Results:
* Boolean, if the account exist then return true, otherwise retrun false

Example：

```JavaScript
exports.hi = v => {
    if (action.is_account(account)) console.notice("account exists");
    else console.error("account notexists")
};
```


### has_recipient
**after action executed，the account names name will receive a notification**

```JavaScript
action.has_recipient(name);
```

Parameter Usage:
* name: String, 

Results:
* Boolean, if the account names name received notification then returns true，otherwise returns false

Example：

```JavaScript
exports.hi = v => {
    if (action.has_recipient(receiver)) console.notice("action received")
    else console.error("action not received");
};
```


### require_recipient
**add specific account to notification list**

```JavaScript
action.require_recipient(name);
```

Parameter Usage:
* name: String, account name

Example：

```JavaScript
exports.hi = v => {
    action.require_recipient(action.receiver);
};

exports.on_hi = v => {
    console.log(action.receiver, action.account , v)
};
```

Note：A notification message sent by one contract to another is a message received by the contract, including code, action, and parameters.

### has_auth

**Verify that the action requires authorization for a specific account**

```JavaScript
action.has_auth(name);
```

Parameter Usage:
* name: String, the account name to be verified

Results:
* Boolean, if this account authorization is required then returns true，otherwise returns false

Example：

```JavaScript
exports.hi = v => {
    if (action.has_auth(account));
    console.notice("action be authed");
};
```


### require_auth
**Add a specific account and corresponding permissions to the action's authorization list, and an exception is returned if the addition fails**

```JavaScript
action.require_auth(name, permission);
```

Parameter Usage:
* name: String, The account name to be verified.
* permission: String, Permission to authorize this account is required

Example：

```JavaScript
exports.hi = v => {
    if (action.require_auth(account));
    console.notice("auth success");
};
```

## Static Property


### name
**action name**

**Type: String**


Example：

```JavaScript
exports.hi = v => {
    console.log(action.name)
};
```


### account
**action sender account name**

**Type: String**


Example：

```JavaScript
exports.hi = v => {
    console.log(action.account)
};
```


### receiver
**action receiver**

**Type: String**

Example：

```JavaScript
exports.hi = v => {
    console.log(action.receiver)
};
```


### publication_time
**Return the millisecond number of block produced since 1970.01.01 0pm 0min 0sec (UTC)**

**Type: Number**


Example：

```JavaScript
exports.hi = v => {
    console.log(action.publication_time)
};
```


### authorization
**Executing action requires all the accounts in array authorized**

**Type: Array**


Example：

```JavaScript
exports.hi = v => {
    console.log(action.authorization)
};
```

