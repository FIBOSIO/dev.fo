---
title: console
type: manual
order: 4
---
# 模块 console

控制台访问对象

全局对象。可用于提示信息，警告和错误记录。通过启动配置文件，可将日志定位到不同的设备，以便于跟踪。

## 静态函数

### log
**记录普通日志信息，与 info 等同**

```JavaScript
console.log(fmt,...args);
```

调用参数:
* fmt: String, 格式化字符串
* args: ..., 可选参数列表

实例：

```JavaScript
exports.hi = v => {
    console.log('hello :%s', "FIBOS")
};
```

记录一般等级的日志信息。通常用于输出非错误性提示信息。


**记录普通日志信息，与 info 等同**

```JavaScript
console.log(...args);
```

调用参数:
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.log('hello FIBOS')
};
```

记录一般等级的日志信息。通常用于输出非错误性提示信息。


### debug
**记录调试日志信息**

```JavaScript
console.debug(fmt,...args);
```

调用参数:
* fmt: String, 格式化字符串
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.debug('warn %s', 'FIBOS')
};
```

记录调试日志信息。通常用于输出调试信息。不重要。


**记录调试日志信息**

```JavaScript
console.debug(...args);
```

调用参数:
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.debug('warn FIBOS')
};
```

记录调试日志信息。通常用于输出调试信息。不重要。


### info
**记录普通日志信息，与 log 等同**

```JavaScript
console.info(fmt,...args);
```

调用参数:
* fmt: String, 格式化字符串
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.info('hello :%s', 'FIBOS')
};
```

记录一般等级的日志信息。通常用于输出非错误性提示信息。


**记录普通日志信息，与 log 等同**

```JavaScript
console.info(...args);
```

调用参数:
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.info('hello FIBOS')
};
```

记录一般等级的日志信息。通常用于输出非错误性提示信息。


### notice
**记录警告日志信息**

```JavaScript
console.notice(fmt,...args);
```

调用参数:
* fmt: String, 格式化字符串
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.notice('hello :%s', 'FIBOS')
};
```

记录警告日志信息。通常用于输出提示性调试信息。一般重要。


**记录警告日志信息**

```JavaScript
console.notice(...args);
```

调用参数:
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.notice('hello FIBOS')
};
```

记录警告日志信息。通常用于输出提示性调试信息。一般重要。


### warn
**记录警告日志信息**

```JavaScript
console.warn(fmt,...args);
```

调用参数:
* fmt: String, 格式化字符串
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.warn('hello :%s', 'FIBOS')
};
```

记录警告日志信息。通常用于输出警告性调试信息。重要。


**记录警告日志信息**

```JavaScript
console.warn(...args);
```

调用参数:
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.warn('hello FIBOS')
};
```

记录警告日志信息。通常用于输出警告性调试信息。重要。


### error
**记录错误日志信息**

```JavaScript
console.error(fmt,...args);
```

调用参数:
* fmt: String, 格式化字符串
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.error('hello %s', 'FIBOS')
};
```

记录用于错误日志信息。通常用于输出错误信息。非常重要。系统的出错信息也会以此等级记录。


**记录错误日志信息**

```JavaScript
console.error(...args);
```

调用参数:
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.warn('hello FIBOS')
};
```

记录用于错误日志信息。通常用于输出错误信息。非常重要。系统的出错信息也会以此等级记录。


### crit
**记录关键错误日志信息**

```JavaScript
console.crit(fmt,...args);
```

调用参数:
* fmt: String, 格式化字符串
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.crit('hello %s', 'FIBOS')
};
```

记录用于关键错误日志信息。通常用于输出关键错误信息。非常重要。


**记录关键错误日志信息**

```JavaScript
console.crit(...args);
```

调用参数:
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.crit('hello FIBOS')
};
```

记录用于关键错误日志信息。通常用于输出关键错误信息。非常重要。


### alert
**记录警报错误日志信息**

```JavaScript
console.alert(fmt,...args);
```

调用参数:
* fmt: String, 格式化字符串
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.alert('hello %s', 'FIBOS')
};
```

记录用于警报错误日志信息。通常用于输出警报错误信息。非常重要。为最高级别信息。


**记录警报错误日志信息**

```JavaScript
console.alert(...args);
```

调用参数:
* args: ..., 可选参数列表

```JavaScript
exports.hi = v => {
    console.alert('hello FIBOS')
};
```

记录用于警报错误日志信息。通常用于输出警报错误信息。非常重要。为最高级别信息。


### dir
**用 JSON 格式输出对象**

```JavaScript
console.dir(obj);
```

调用参数:
* obj: Value, 给定要显示的对象

```JavaScript
exports.hi = v => {
    var a = {};
    console.dir(a);
};
```


### trace
**输出当前调用堆栈**

```JavaScript
console.trace(label);
```

调用参数:
* label: String, 标题，缺省为空字符串。

通过日志输出当前调用堆栈。


### assert
**断言测试，如果测试值为假，则报错**

```JavaScript
console.assert(value,msg);
```

调用参数:
* value: Value, 测试的数值
* msg: String, 报错信息

## 常量

### FATAL
**loglevel 级别常量**

```JavaScript
const console.FATAL = 0;
```


### ALERT
**loglevel 级别常量**

```JavaScript
const console.ALERT = 1;
```


### CRIT
**loglevel 级别常量**

```JavaScript
const console.CRIT = 2;
```


### ERROR
**loglevel 级别常量**

```JavaScript
const console.ERROR = 3;
```


### WARN
**loglevel 级别常量**

```JavaScript
const console.WARN = 4;
```


### NOTICE
**loglevel 级别常量**

```JavaScript
const console.NOTICE = 5;
```


### INFO
**loglevel 级别常量**

```JavaScript
const console.INFO = 6;
```


### DEBUG
**loglevel 级别常量**

```JavaScript
const console.DEBUG = 7;
```


### PRINT
**loglevel 仅用于输出，信息输出后不换行，file 和 syslog 不保存此级别信息**

```JavaScript
const console.PRINT = 9;
```


### NOTSET
**loglevel 级别常量**

```JavaScript
const console.NOTSET = 10;
```

