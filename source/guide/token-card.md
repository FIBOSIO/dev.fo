---
title: 通证
type: tutorials
order: 252
---

## 发行通证

发行通证调用 token 合约中的 `excreate` 接口，方法和参数名解释如下：

```javascript
void token::excreate(
  account_name issuer, // 通证发行账号
  asset maximum_supply, // 最大可发行通证数量
  double connector_weight, // 连接器权重
  asset maximum_exchange, // 最大可兑换(流通)的通证数量
  asset reserve_supply, // 未流通通证数量
  asset reserve_connector_balance, // 未流通通证保证金数量
  time_point_sec expiration, // 项目方预设的项目锁仓期
  double buy_fee, // 项目方预设通证兑入手续费
  double sell_fee // 项目方预设通证兑出手续费
  string connector_balance_issuer //准备金发行方
)
```

在 FIBOS 上你可以发行两种通证，一种是传统通证，一种智能通证。两种通证的不同点在于智能通证可以通过 bancor 协议进行兑换。如果还不了解什么是 bancor 协议的同学，可以参考 [bancor 协议中文白皮书](https://github.com/FIBOSIO/bancor) 一文。

### 发行普通通证

```javascript
//初始化 fibos 客户端
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.excreateSync(name, '90000000000.0000 DDD', 0, '10000000000.0000 DDD', '3000000000.0000 DDD', '90000.0000 FO', '2018-10-29T18:54:00', 0, 0, 'eosio' {
  authorization: name
}); //expiration需大于等于当前时间,此处准备金为 FO，所以准备金发行方填 eosio
console.log(r)
```

### 发行智能通证

```javascript
//初始化 fibos 客户端
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.excreateSync(name, '100000000000.0000 AAA',  0.15,'10000000000.0000 AAA', '3000000000.0000 AAA', '90000.0000 FO', '2018-10-29T18:54:00', 0, 0, 'eosio' {
    authorization: name
});  //expiration需大于等于当前时间,此处准备金为 FO，所以准备金发行方填 eosio
console.log(r);
```

备注：当一个通证的连接器权重（CW）值为0时，它就是传统通证。而对于智能通证来说，它必须要有对应的 cw（0-1之间）和 max_exchange。以及根据 bancor 协议计算出 reserve_supply 和 reserve_connector_balance。

#### 查询发行的通证

```javascript
//初始化 fibos 客户端
...
let r = fibos.getTableRowsSync(true, 'eosio.token', 'fibostest123', 'stats');//第一个参数为是否明文展示，第二个参数为合约名，第三个参数为 FIBOS 账户名，第四个参数为表名
console.log(r);
```



## 增发普通通证

> **Tips** : 只有普通通证可以进行增发操作，智能通证不支持增发！

```javascript
//初始化 fibos 客户端
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exissueSync(name, '1000000.0000 ABC@fibostest123', 'issue to fibostest123', {
  authorization: name
});
console.log(r);
```



## 开仓锁仓

### 开仓

通证的创建者需要调用开仓操作之后才能开启兑换智能通证，具体 API 和操作如下：

```javascript
//初始化 fibos 客户端
...
let name = 'fibostest123';
let ctx = fibos.contractSync('eosio.token');
let r = ctx.setpositionSync('0.0000 AAA@fibostest123', 1, 'set postion state to true', {
    authorization: name
}); // 第二个参数为 1 表示开仓，0 表示关仓
console.log(r);
```

备注：这里的开仓/关仓状态仅仅影响智能通证的兑入，不影响智能通证的兑出功能。如果智能通证为关仓状态，仍然可以将智能通证兑换成保证金或者其他状态为开仓的智能通证，但是并不能将保证金兑换成为该智能通证了。

### 锁仓

项目方发行智能通证时，填写的 reserve_supply 这个参数的值，锁仓量会随着销毁和解锁通证的操作而变化。项目方可以把锁仓中的一部分通证通过锁仓转账（exlocktrans）的方法给到用户 A ，用户 A 也可以将得到这部分锁仓的通证转给用户 B 或者说转给项目方。当项目运营良好的时候，项目方或者用户可以通过解锁通证来获取回报。

调用 `exlocktrans`  方法和参数名解释如下：

```javascript
void token::exlocktrans(
    account_name from, //通证转出方
    account_name to, //通证转入方
    extended_asset quantity, //通证数量
    time_point_sec expiration, //待转出锁仓时间
    time_point_sec expiration_to, //待转入锁仓时间
    string memo //附言
)
```

备注：接口中的 `expiration_to` 参数是锁仓期，项目方给用户锁仓转账的时候可以设置这个参数，时间戳格式精确到秒，这样用户就可以在锁仓期到达之前是无法进行解锁操作的。 `expiration` 参数表示通过该锁仓期查找用户锁仓对应的通证。

#### 实例

```javascript
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exlocktransSync('nmslwsndhjyz', 'fibostest123', `10000.0000 ADC@nmslwsndhjyz`, '2018-10-29T18:54:00', '2018-10-29T18:54:00', `lock transfer to fibostest123`, {
    authorization: 'nmslwsndhjyz'
}); //expiration_to必须大于等于expiration
console.notice(r)
```

上述代码中 `nmslwsndhjyz` 给用户 `fibostest123` 锁仓转账了 10000.0000 个 ADC 通证。

### 解锁

项目方和用户可以通过解锁操作来解锁仓中的通证变为流通中的通证。

调用 `exunlock` 方法和参数名解释如下：

```javascript
void token::exunlock(
    account_name owner, //通证持有者
    extended_asset quantity, //解锁数量
    time_point_sec expiration, //锁仓期
    string memo //附言
)
```

备注：解锁操作只有在当前时间大于锁仓期时候可以进行，这里需要注意的是 `expiration` 参数的值不是当前时间，而是锁仓转账时设定的锁仓期时间。

#### 实例

```javascript
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exunlockSync('fibostest123', '100.0000 ADC@nmslwsndhjyz', 1537960501, 'unlock 100.0000 ADC', {
    authorization: 'hujzwsndnmsl'
})
console.notice(r);
```



## 分红

FIBOS 的 token 经济模型中为通证发行方提供了向社区中通证持有者进行分红的方法，发行方可通过填入一定数量的保证金进行分红，社区中的通证持有者将会在兑换过程中享受这部分保证金的红利。

调用 `exshare` 方法和参数名解释如下：

```javascript
//初始化 fibos 客户端
...

let ctx = fibos.contractSync('eosio.token');
let r = ctx.exshareSync('10000.0000 FO@eosio', '0.0000 AAA@fibostest321', 'share 10000.0000 FO to token holders',{
    authorization: 'fibostest123'
}); // 第一个参数为填入保证金的数量，第二个参数为参与分红的智能通证，第三个参数为备注
```



## 销毁通证

> **Tips** : 销毁通证需要**流通量为0**的时候才可以销毁，也就是说通证发行方需要收回市场上所有流通的通证后才能销毁通证。

当不再需要该通证时，调用 `exdestroySync` 方法来销毁通证：

```javascript
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
let r = ctx.exdestroySync('0.0000 AAA@fibostest123', {
    authorization: 'fibostest123'
});
```
