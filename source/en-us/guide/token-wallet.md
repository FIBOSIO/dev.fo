---
title: Contract Sub-Wallet
type: tutorials
language: en
order: 256
---

## Why do we use Sub-Wallets

### Scenario 1

Suppose there is such A business scenario where company A releases a product called FO bike. To use the FO bike, user payments should be made by using the FO bicycle token, and the FO bike token can be exchanged with the FO token. If user A wants to use FO bike, he should register an account on the FO bike platform and fill it with a certain amount of FO bike tokens. However, every time he or she use the FO bike, he or she will need to make a payment, but since every payment requires the user to enter a password, it affects the user's experience. So what's a good solution?

Contract sub wallets can solve this problem, we can think of it this way, the FO bike platform is equivalent to the contract, and the sub wallet is equivalent to the platform account. When users want to use FO bikes, they can charge FO bike tokens into the sub-wallet, and the contract will be authorized to operate the balance in your sub-wallet. This way, after each use of the bike, the contract will automatically deduct FO bike tokens, so that users do not need to manually operate their account. When the user no longer needs to use FO bike, the FO bike pass can be extracted from the sub-wallet.

### Scenario 2

Suppose A and B are making a bet and invest 50 FO tokens respectively, but there is no one judges the result of the bet, and both of them can cheat. What should we do then?

Contract sub-wallets can also solve this problem. Here, A and B need a third-party platform C to supervise. Before the competition, A and B respectively transfer 50 FO tokens to the accounts of platform C, and the platform can operate the tokens of accounts A and B for when the result comes out. The platform will directly transfer the losing party's tokens to the winning party. 

In the above two scenarios, one can see how to use contract subwallets simply. There are many more use cases of contract sub-walles waiting to be explored, and the following are the three interfaces of the contract sub-wallet.

## Three uses of the contract sub-wallet

The premise condition：user `nmslwsndhjyz` issued a contract，And the precision is four decimal places，with smart token named `ADC`. user `tteesstt1122` via [exchanging](./token-exchange.html) holds the 1000 ` ADC ` circulating tokens.

### top-up

**Interface**

```js
void token::ctxrecharge(
    account_name owner, //account owner
    extended_asset quantity, //top-up amount
    string memo //memo
)
```

**Example**

```js
//Initialize fibos client
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.ctxrechargeSync('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxrecharge', {
			authorization: 'tteesstt1122'
		})
console.notice(r);
```

In the codes above，`tteesstt1122` called `ctxrechargeSync` method to top-up 200 `ADC` smart token into its own sub-wallet.

After successful top-up, we can call the following method to query the balance of the circulation license and the balance of the contract sub-wallet, respectively.

Check available balance:

```js
//Initialize fibos client
...
let r = fibos.getTableRowsSync(true, 'eosio.token', 'nmslwsndhjyz', 'accounts')
console.notice(r);
```

Check available sub-wallet balance:

```js
//Initialize fibos client
...
let s = fibos.getTableRowsSync(true, 'eosio.token', 'nmslwsndhjyz', 'ctxaccounts')
console.notice(s);
```

### Withdrawal

**Interface**

```js
void token::ctxextract(
    account_name owner,//Account owner
    extended_asset quantity, //withdrawal amount
    string memo //memo
)
```

**Example**

```js
//Initialize fibos client
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.ctxextractSync('tteesstt1122', '100.0000 ADC@nmslwsndhjyz', 'ctxextract', {
			authorization: 'tteesstt1122'
		})
console.notice(r);
```

Call `ctxextractSync` method to withdraw the 100 tokens in your contract sub-wallet back to the circulating token balance.

### Transfer

**Interface**

```javascript
void token::ctxtransfer(
	account_name from, //Token Transferor
	account_name to, //Token transferee
	extended_asset quantity, //Token amount
	string memo //memo
)
```

**Example**

```js
ctx.ctxtransferSync('tteesstt1122', 'tteesstt2222', '50.0000 ADC@nmslwsndhjyz', 'ctxtransfer', {
			authorization: 'nmslwsndhjyz'
		})
```

`ADC` contract issuer `nmslwsndhjyz` calls transfer method `ttteesstt1122` to transfer 50 `ADC` tokens in user contract sub-wallet to the contract sub-wallet of user `tteesstt2222` 

## Preliminary tests

After knowing the above three apis about the recharge, withdrawal and transfer of contract sub-wallet, we can realize many functions. For example, the FO bike in scenario 1, after the user recharges, the user's contract subwallet has the corresponding assets. Imagine a user riding a bike, locking it and leaving. After the user's assets in the contract are settled,  call contract wallet ` ctxtransfer ` . This action will go to the user's sub wallet to deduct the corresponding assets, does not require users to participate or wait the whole time, and is very convenient. Now, let's implement this using JavaScript contracts!

In this contract, we only need to realize one of the most basic functions, which is to deduct the fee after the user finishes using the bike. Assuming that 1 minute of cycling needs to consume 1 FOBIKE token, the amount of assets that the user needs to pay can be settled according to the length. Then, the use of contract in contract call ` eosio.token ` contract's ` ctxtransfer ` . This action will transfer the user sub wallet asset to the contract publishers' contract sub wallet, in order to achieve deducting the user assets.

Let's call this action settle. Save the following code to ` contract. Js `, as the contract code files:

```js
exports.settle = (user, minutes) => {
    assert.isTrue(minutes > 0, 'minutes must be positive');

    let quantity = (minutes * 10n).toString();
    quantity = {
        quantity: `${quantity}.0000 FOBIKE`,
        contract: 'fobikeissuer'
    };
    
    trans.send_inline('eosio.token', 'ctxtransfer', {
        from: user,
        to: 'fobikeissuer',
        quantity: quantity,
        memo: `${user} pays for FO Bike`
    }, [{
        'actor': 'fobikeissuer',
        'permission': 'active'
    }]);
};
```

and also abi file：

```
{
    'version': 'eosio::abi/1.0',
    'structs': [{
        'name': 'settle',
        'base': '',
        'fields': [{
            'name': 'user',
            'type': 'name'
        }, {
            'name': 'minutes',
            'type': 'uint64'
        }]
    }],
    'actions': [{
        'name': 'settle',
        'type': 'settle',
        'ricardian_contract': ''
    }]
}
```

For more on how to release a JavaScript contract，Please refer to [Quick Start](./start.html)。

Through the JavaScript contract above, we can see that `assert.isTrue(minutes > 0, 'minutes must be positive');` is used to judge the correctness of the cycling time. And then, according to the length of the ride we will calculate the user token amount needed to pay, constructing a ` extended_asset ` object, as a parameter, and use the ` send_inline ` method to call ` eosio.token ` contract's ` ctxtransfer `, transfering the user's sub wallet asset  to the contract publisher's (fobikeissuer) sub contract wallet. (We'll cover the invocation between contracts in more detail in the next installment of the documentation, so stay tuned!)

This completes one of the simplest JavaScript contracts for deducting fees. There are many more interesting ways to use the contract wallets, and we welcome everyone to speak up, so let us make progress together!