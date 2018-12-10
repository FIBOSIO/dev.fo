---
title: assert
type: manual
language: zh-cn
order: 2
---
# 模块 assert
断言测试模块，如果测试值为假，则报错，报错行为可设定继续运行或者错误抛出。

引用方法：

```JavaScript
var assert = require('assert');
```

## 静态函数

### Function
**测试数值为真，为假则断言失败**

```JavaScript
assert.Function(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### ok
**测试数值为真，为假则断言失败**

```JavaScript
assert.ok(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### notOk
**测试数值为假，为真则断言失败**

```JavaScript
assert.notOk(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### equal
**测试数值等于预期值，不相等则断言失败**

```JavaScript
assert.equal(actual,expected,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* msg: String, 断言失败时的提示信息


### notEqual
**测试数值不等于预期值，相等则断言失败**

```JavaScript
assert.notEqual(actual,expected,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* msg: String, 断言失败时的提示信息


### strictEqual
**测试数值严格等于预期值，不相等则断言失败**

```JavaScript
assert.strictEqual(actual,expected,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* msg: String, 断言失败时的提示信息


### notStrictEqual
**测试数值不严格等于预期值，相等则断言失败**

```JavaScript
assert.notStrictEqual(actual,expected,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* msg: String, 断言失败时的提示信息


### deepEqual
**测试数值深度等于预期值，不相等则断言失败**

```JavaScript
assert.deepEqual(actual,expected,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* msg: String, 断言失败时的提示信息


### notDeepEqual
**测试数值不深度等于预期值，相等则断言失败**

```JavaScript
assert.notDeepEqual(actual,expected,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* msg: String, 断言失败时的提示信息


### closeTo
**测试数值近似等于预期值，否则断言失败**

```JavaScript
assert.closeTo(actual,expected,delta,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* delta: Value, 近似的小数精度
* msg: String, 断言失败时的提示信息


### notCloseTo
**测试数值不近似等于预期值，否则断言失败**

```JavaScript
assert.notCloseTo(actual,expected,delta,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* delta: Value, 近似的小数精度
* msg: String, 断言失败时的提示信息


### lessThan
**测试数值小于预期值，大于或等于则断言失败**

```JavaScript
assert.lessThan(actual,expected,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* msg: String, 断言失败时的提示信息


### notLessThan
**测试数值不小于预期值，小于则断言失败**

```JavaScript
assert.notLessThan(actual,expected,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* msg: String, 断言失败时的提示信息


### greaterThan
**测试数值大于预期值，小于或等于则断言失败**

```JavaScript
assert.greaterThan(actual,expected,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* msg: String, 断言失败时的提示信息


### notGreaterThan
**测试数值不大于预期值，大于则断言失败**

```JavaScript
assert.notGreaterThan(actual,expected,msg);
```

调用参数:
* actual: Value, 要测试的数值
* expected: Value, 预期的数值
* msg: String, 断言失败时的提示信息


### exist
**测试变量存在，为假则断言失败**

```JavaScript
assert.exist(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### notExist
**测试变量不存在，为真则断言失败**

```JavaScript
assert.notExist(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isTrue
**测试数值为布尔值真，否则断言失败**

```JavaScript
assert.isTrue(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNotTrue
**测试数值不为布尔值真，否则断言失败**

```JavaScript
assert.isNotTrue(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isFalse
**测试数值为布尔值假，否则断言失败**

```JavaScript
assert.isFalse(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNotFalse
**测试数值不为布尔值假，否则断言失败**

```JavaScript
assert.isNotFalse(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNull
**测试数值为 Null，否则断言失败**

```JavaScript
assert.isNull(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNotNull
**测试数值不为 Null，否则断言失败**

```JavaScript
assert.isNotNull(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isUndefined
**测试数值为 undefined，否则断言失败**

```JavaScript
assert.isUndefined(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isDefined
**测试数值不为 undefined，否则断言失败**

```JavaScript
assert.isDefined(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isFunction
**测试数值为函数，否则断言失败**

```JavaScript
assert.isFunction(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNotFunction
**测试数值不为函数，否则断言失败**

```JavaScript
assert.isNotFunction(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isObject
**测试数值为对象，否则断言失败**

```JavaScript
assert.isObject(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNotObject
**测试数值不为对象，否则断言失败**

```JavaScript
assert.isNotObject(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isArray
**测试数值为数组，否则断言失败**

```JavaScript
assert.isArray(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNotArray
**测试数值不为数组，否则断言失败**

```JavaScript
assert.isNotArray(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isString
**测试数值为字符串，否则断言失败**

```JavaScript
assert.isString(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNotString
**测试数值不为字符串，否则断言失败**

```JavaScript
assert.isNotString(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNumber
**测试数值为数字，否则断言失败**

```JavaScript
assert.isNumber(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNotNumber
**测试数值不为数字，否则断言失败**

```JavaScript
assert.isNotNumber(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isBoolean
**测试数值为布尔，否则断言失败**

```JavaScript
assert.isBoolean(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### isNotBoolean
**测试数值不为布尔，否则断言失败**

```JavaScript
assert.isNotBoolean(actual,msg);
```

调用参数:
* actual: Value, 要测试的数值
* msg: String, 断言失败时的提示信息


### typeOf
**测试数值为给定类型，否则断言失败**

```JavaScript
assert.typeOf(actual,type,msg);
```

调用参数:
* actual: Value, 要测试的数值
* type: String, 指定的类型
* msg: String, 断言失败时的提示信息


### notTypeOf
**测试数值不为给定类型，否则断言失败**

```JavaScript
assert.notTypeOf(actual,type,msg);
```

调用参数:
* actual: Value, 要测试的数值
* type: String, 指定的类型
* msg: String, 断言失败时的提示信息


### property
**测试对象中包含指定属性，否则断言失败**

```JavaScript
assert.property(object,prop,msg);
```

调用参数:
* object: Value, 要测试的对象
* prop: Value, 要测试的属性
* msg: String, 断言失败时的提示信息


### notProperty
**测试对象中不包含指定属性，否则断言失败**

```JavaScript
assert.notProperty(object,prop,msg);
```

调用参数:
* object: Value, 要测试的对象
* prop: Value, 要测试的属性
* msg: String, 断言失败时的提示信息


### deepProperty
**深度测试对象中包含指定属性，否则断言失败**

```JavaScript
assert.deepProperty(object,prop,msg);
```

调用参数:
* object: Value, 要测试的对象
* prop: Value, 要测试的属性，以“.”分割
* msg: String, 断言失败时的提示信息


### notDeepProperty
**深度测试对象中不包含指定属性，否则断言失败**

```JavaScript
assert.notDeepProperty(object,prop,msg);
```

调用参数:
* object: Value, 要测试的对象
* prop: Value, 要测试的属性，以“.”分割
* msg: String, 断言失败时的提示信息


### propertyVal
**测试对象中指定属性的值为给定值，否则断言失败**

```JavaScript
assert.propertyVal(object,prop,value,msg);
```

调用参数:
* object: Value, 要测试的对象
* prop: Value, 要测试的属性
* value: Value, 给定的值
* msg: String, 断言失败时的提示信息


### propertyNotVal
**测试对象中指定属性的值不为给定值，否则断言失败**

```JavaScript
assert.propertyNotVal(object,prop,value,msg);
```

调用参数:
* object: Value, 要测试的对象
* prop: Value, 要测试的属性
* value: Value, 给定的值
* msg: String, 断言失败时的提示信息


### deepPropertyVal
**深度测试对象中指定属性的值为给定值，否则断言失败**

```JavaScript
assert.deepPropertyVal(object,prop,value,msg);
```

调用参数:
* object: Value, 要测试的对象
* prop: Value, 要测试的属性，以“.”分割
* value: Value, 给定的值
* msg: String, 断言失败时的提示信息


### deepPropertyNotVal
**深度测试对象中指定属性的值不为给定值，否则断言失败**

```JavaScript
assert.deepPropertyNotVal(object,prop,value,msg);
```

调用参数:
* object: Value, 要测试的对象
* prop: Value, 要测试的属性，以“.”分割
* value: Value, 给定的值
* msg: String, 断言失败时的提示信息


### throws
**测试给定的代码会抛出错误，未抛出则断言失败**

```JavaScript
assert.throws(Function block,msg);
```

调用参数:
* block: Function, 指定测试的代码，以函数形式给出
* msg: String, 断言失败时的提示信息


### doesNotThrow
**测试给定的代码不会抛出错误，抛出则断言失败**

```JavaScript
assert.doesNotThrow(Function block,msg);
```

调用参数:
* block: Function, 指定测试的代码，以函数形式给出
* msg: String, 断言失败时的提示信息


### ifError
**如果参数为真，则抛出**

```JavaScript
assert.ifError(object);
```

调用参数:
* object: Value, 参数

