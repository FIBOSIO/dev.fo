---
title: assert
type: manual
language: en
order: 2
---
#  assert module

Assertion test module, if the test value is false, then return an error, the error behavior can be set to continue or return error result.

Usage：

```JavaScript
var assert = require('assert');
```

## Static Function

### Function
**the test value is true, or if it is false, the assertion fails**

```JavaScript
assert.Function(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails 


### ok
**the test value is false, or if it is true, the assertion fails**

```JavaScript
assert.ok(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails 


### notOk
**the test value is true, or if it is false, the assertion fails**

```JavaScript
assert.notOk(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### equal
**The test value is equal to the expected value, otherwise the assertion fails**

```JavaScript
assert.equal(actual,expected,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* msg: String, Prompt message when assertion fails


### notEqual
**Test values do not equal expectations, if the value is equal, the assertion is invalid**

```JavaScript
assert.notEqual(actual,expected,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* msg: String, Prompt message when assertion fails


### strictEqual
**The test value is strictly equal to the expected value, otherwise the assertion fails**

```JavaScript
assert.strictEqual(actual,expected,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* msg: String, Prompt message when assertion fails


### notStrictEqual
**The test value is not strictly equal to the expected value, and the assertion fails if it is equal**

```JavaScript
assert.notStrictEqual(actual,expected,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* msg: String, Prompt message when assertion fails


### deepEqual
**The test value is deeply equal to the expected value, otherwise the assertion fails**

```JavaScript
assert.deepEqual(actual,expected,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* msg: String, Prompt message when assertion fails


### notDeepEqual
**The test value is not deeply equal to the expected value, otherwise the assertion fails**

```JavaScript
assert.notDeepEqual(actual,expected,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* msg: String, Prompt message when assertion fails


### closeTo
**The test value is approximately equal to the expected value, otherwise the assertion fails**

```JavaScript
assert.closeTo(actual,expected,delta,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* delta: Value, Approximate decimal precision
* msg: String, Prompt message when assertion fails


### notCloseTo
**The test value does not approximate the expected value, otherwise the assertion fails**

```JavaScript
assert.notCloseTo(actual,expected,delta,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* delta: Value, Approximate decimal precision
* msg: String, Prompt message when assertion fails


### lessThan
**The test value is less than the expected value, assertion fails when it is greater or equal to the expected value**

```JavaScript
assert.lessThan(actual,expected,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* msg: String, Prompt message when assertion fails


### notLessThan
**The test value is not less than the expected value, assertion fails when it is less to the expected value**

```JavaScript
assert.notLessThan(actual,expected,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* msg: String, Prompt message when assertion fails


### greaterThan
**The test value is greater than the expected value, the assertion fails when it is less or equal to the expected value**

```JavaScript
assert.greaterThan(actual,expected,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* msg: String, Prompt message when assertion fails


### notGreaterThan
**The test value is not greater than the expected value，greater means the assertion fails**

```JavaScript
assert.notGreaterThan(actual,expected,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* expected: Value, Expected value
* msg: String, Prompt message when assertion fails


### exist
**The test variable exists. If it is false, the assertion fails**

```JavaScript
assert.exist(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### notExist
**The test variable does not exist. If it is true, the assertion fails**

```JavaScript
assert.notExist(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isTrue
**The test value is Boolean true, otherwise the assertion fails**

```JavaScript
assert.isTrue(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNotTrue
**The test value is not Boolean true, otherwise the assertion fails**

```JavaScript
assert.isNotTrue(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isFalse
**The test value is Boolean flase, otherwise the assertion fails**

```JavaScript
assert.isFalse(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNotFalse
**The test value is not Boolean false, otherwise the assertion fails**

```JavaScript
assert.isNotFalse(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNull
**The test value is Null, otherwise the assertion fails**

```JavaScript
assert.isNull(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNotNull
**The test value is not Null, otherwise the assertion fails**

```JavaScript
assert.isNotNull(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isUndefined
**The test value is undefined, otherwise the assertion fails**

```JavaScript
assert.isUndefined(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isDefined
**The test value is not undefined, otherwise the assertion fails**

```JavaScript
assert.isDefined(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isFunction
**The test value is a function, otherwise the assertion fails**

```JavaScript
assert.isFunction(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNotFunction
**The test value is not a function, otherwise the assertion fails**

```JavaScript
assert.isNotFunction(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isObject
**The test value is an object, otherwise the assertion fails**

```JavaScript
assert.isObject(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNotObject
**The test value is not an object, otherwise the assertion fails**

```JavaScript
assert.isNotObject(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isArray
**The test value is an array, otherwise the assertion fails**

```JavaScript
assert.isArray(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNotArray
**The test value is not an array, otherwise the assertion fails**

```JavaScript
assert.isNotArray(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isString
**The test value is a string, otherwise the assertion fails**

```JavaScript
assert.isString(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNotString
**The test value is not a string, otherwise the assertion fails**

```JavaScript
assert.isNotString(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNumber
**The test value is a number, otherwise the assertion fails**

```JavaScript
assert.isNumber(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNotNumber
**The test value is not a number, otherwise the assertion fails**

```JavaScript
assert.isNotNumber(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isBoolean
**The test value is a Boolean, otherwise the assertion fails**

```JavaScript
assert.isBoolean(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### isNotBoolean
**The test value is not a Boolean, otherwise the assertion fails**

```JavaScript
assert.isNotBoolean(actual,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* msg: String, Prompt message when assertion fails


### typeOf
**The test value is a given type, otherwise the assertion fails**

```JavaScript
assert.typeOf(actual,type,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* type: String, 指定的类型
* msg: String, Prompt message when assertion fails


### notTypeOf
**The test value is not a given type, otherwise the assertion fails**

```JavaScript
assert.notTypeOf(actual,type,msg);
```

Parameter Usage:
* actual: Value, The value needs to be tested
* type: String, 指定的类型
* msg: String, Prompt message when assertion fails


### property
**The test value includes given property, otherwise the assertion fails**

```JavaScript
assert.property(object,prop,msg);
```

Parameter Usage:
* object: Value, The object needs to be tested
* prop: Value, Properties to test
* msg: String, Prompt message when assertion fails


### notProperty
**The test value does not includes given property, otherwise the assertion fails**

```JavaScript
assert.notProperty(object,prop,msg);
```

Parameter Usage:
* object: Value, The object needs to be tested
* prop: Value, Properties to test
* msg: String, Prompt message when assertion fails


### deepProperty
**The deep test object contains the specified property, otherwise the assertion fails**

```JavaScript
assert.deepProperty(object,prop,msg);
```

Parameter Usage:
* object: Value, The object needs to be tested
* prop: Value, Properties to test, split by "."
* msg: String, Prompt message when assertion fails


### notDeepProperty
**The deep test object does not contain the specified property, or the assertion fails**

```JavaScript
assert.notDeepProperty(object,prop,msg);
```

Parameter Usage:
* object: Value, The object needs to be tested
* prop: Value, Properties to test, split by "."
* msg: String, Prompt message when assertion fails


### propertyVal
**The value of the property specified in the test object is a given value, otherwise the assertion fails**

```JavaScript
assert.propertyVal(object,prop,value,msg);
```

Parameter Usage:
* object: Value, The object needs to be tested
* prop: Value, Properties to test
* value: Value, Given value
* msg: String, Prompt message when assertion fails


### propertyNotVal
**The value of the property specified in the test object is not a given value, otherwise the assertion fails**

```JavaScript
assert.propertyNotVal(object,prop,value,msg);
```

Parameter Usage:
* object: Value, The object needs to be tested
* prop: Value, Properties to test
* value: Value, Given value
* msg: String, Prompt message when assertion fails


### deepPropertyVal
**The value of the property specified in the deep test object is a given value, otherwise the assertion fails**

```JavaScript
assert.deepPropertyVal(object,prop,value,msg);
```

Parameter Usage:
* object: Value, The object needs to be tested
* prop: Value, Properties to test, split by "."
* value: Value, Given value
* msg: String, Prompt message when assertion fails


### deepPropertyNotVal
**The value of the property specified in the deep test object is not a given value, otherwise the assertion fails**

```JavaScript
assert.deepPropertyNotVal(object,prop,value,msg);
```

Parameter Usage:
* object: Value, The object needs to be tested
* prop: Value, Properties to test, split by "."
* value: Value, Given value
* msg: String, Prompt message when assertion fails


### throws
**Testing a given code returns an error and assertion fails if it is not returned**

```JavaScript
assert.throws(Function block,msg);
```

Parameter Usage:
* block: Function, Specifies the code for the test, given as a function
* msg: String, Prompt message when assertion fails


### doesNotThrow
**The test given code does not return an error, and the assertion fails if returns**

```JavaScript
assert.doesNotThrow(Function block,msg);
```

Parameter Usage:
* block: Function, Specifies the code for the test, given as a function
* msg: String, Prompt message when assertion fails


### ifError
**If the parameter is true,then return**

```JavaScript
assert.ifError(object);
```

Parameter Usage:
* object: Value, Parameter

