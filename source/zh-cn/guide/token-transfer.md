---
title: 转账
type: tutorials
language: zh-cn
order: 250
---

## 链内转账

转账的目标账户必须要在 FIBOS 中存在，且转账的最大数量不能超过你的余额，精度也要与转账的 Token 精度一致。

调用 `extransfer` 方法，方法和参数名如下：

| 参数     | 含义       |
| -------- | ---------- |
| from     | 通证转出方 |
| to       | 通证转入方 |
| quantity | 通证数量   |
| memo     | 附言       |

```javascript
//初始化 fibos 客户端
...
let ctx = fibos.contractSync('eosio.token');
var r = ctx.extransferSync(
    'fibostest123',  //通证转出方
    'fibostest321',   //通证转入方
    '10.0000 ADC@fibostest123',  //通证数量
    'trasnfer to fibostest321',  //附言
    {
  authorization: 'fibostest123'
});
console.log(r);
```