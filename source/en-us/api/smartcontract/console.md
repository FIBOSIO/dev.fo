---
title: console
type: manual
language: en
order: 4
---
# console module

Console access object

Global object. Can be used for notification, alert and error log. By starting config file, the log can be located to different devices for easy tracking. 

## Static Function

### log
**Save normal log indo, same as info**

```JavaScript
console.log(fmt,...args);
```

Parameter Usage:
* fmt: String, Format string
* args: ..., Optional parameter list

Example：

```JavaScript
exports.hi = v => {
    console.log('hello :%s', "FIBOS")
};
```

Save normal level log info. Typically used to output none error information


**Save normal log indo, same as info**

```JavaScript
console.log(...args);
```

Parameter Usage:
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.log('hello FIBOS')
};
```

Save normal level log info. Typically used to output none error information


### debug
**Save debug log**

```JavaScript
console.debug(fmt,...args);
```

Parameter Usage:
* fmt: String, Format string
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.debug('warn %s', 'FIBOS')
};
```

Save debug log。Typically used to output debug info. not important.


**Save debug log**

```JavaScript
console.debug(...args);
```

Parameter Usage:
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.debug('warn FIBOS')
};
```

Save debug log。Typically used to output debug info. not important.


### info
**Record normal log info, same as log**

```JavaScript
console.info(fmt,...args);
```

Parameter Usage:
* fmt: String, Format string
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.info('hello :%s', 'FIBOS')
};
```

Save normal level log info. Typically used to output none error information


**Record normal log info, same as log**

```JavaScript
console.info(...args);
```

Parameter Usage:
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.info('hello FIBOS')
};
```

Save normal level log info. Typically used to output none error information


### notice
**Record alert log info**

```JavaScript
console.notice(fmt,...args);
```

Parameter Usage:
* fmt: String, Format string
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.notice('hello :%s', 'FIBOS')
};
```

Record alert log info. Typically used to output informative debug info, normal important


**Record alert log info**

```JavaScript
console.notice(...args);
```

Parameter Usage:
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.notice('hello FIBOS')
};
```

Record alert log info. Typically used to output informative debug info, normal important


### warn
**Record alert log info**

```JavaScript
console.warn(fmt,...args);
```

Parameter Usage:
* fmt: String, Format string
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.warn('hello :%s', 'FIBOS')
};
```

Record alert log info. Typically used to output warning debug info, important


**Record alert log info**

```JavaScript
console.warn(...args);
```

Parameter Usage:
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.warn('hello FIBOS')
};
```

Record alert log info. Typically used to output warning debug info, important


### error
**Record error log info**

```JavaScript
console.error(fmt,...args);
```

Parameter Usage:
* fmt: String, Format string
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.error('hello %s', 'FIBOS')
};
```

Used to record error log info. Typically used to output error log, very important. System error messages are also recorded at this level.

**Record error log info**

```JavaScript
console.error(...args);
```

Parameter Usage:
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.warn('hello FIBOS')
};
```

Used to record error log info. Typically used to output error log, very important. System error messages are also recorded at this level.

### crit
**Record key error log info**

```JavaScript
console.crit(fmt,...args);
```

Parameter Usage:
* fmt: String, Format string
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.crit('hello %s', 'FIBOS')
};
```

Used to record key error log info. Typically used to output key error log, very important. 

**Record key error log info**

```JavaScript
console.crit(...args);
```

Parameter Usage:
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.crit('hello FIBOS')
};
```

Used to record key error log info. Typically used to output key error log, very important. 

### alert
**Record alert error log info**

```JavaScript
console.alert(fmt,...args);
```

Parameter Usage:
* fmt: String, Format string
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.alert('hello %s', 'FIBOS')
};
```

Used to record warning error log info. Typically used to output warning error log, very important. The highest level of information

**Record alert error log info**

```JavaScript
console.alert(...args);
```

Parameter Usage:
* args: ..., Optional parameter list

```JavaScript
exports.hi = v => {
    console.alert('hello FIBOS')
};
```

Used to record warning error log info. Typically used to output warning error log, very important. The highest level of information

### dir
**Output object using JSON format**

```JavaScript
console.dir(obj);
```

Parameter Usage:
* obj: Value, Define the object to show.

```JavaScript
exports.hi = v => {
    var a = {};
    console.dir(a);
};
```


### trace
**Output the current calling stack**

```JavaScript
console.trace(label);
```

Parameter Usage:
* label: String, title，default is an empty string.

Prints the current call stack via log.


### assert
**Assertion test, if the test value is false, an error is reported**

```JavaScript
console.assert(value,msg);
```

Parameter Usage:
* value: Value, Value to test
* msg: String, error message

## Constant

### FATAL
**loglevel level constant**

```JavaScript
const console.FATAL = 0;
```


### ALERT
**loglevel level constant**

```JavaScript
const console.ALERT = 1;
```


### CRIT
**loglevel level constant**

```JavaScript
const console.CRIT = 2;
```


### ERROR
**loglevel level constant**

```JavaScript
const console.ERROR = 3;
```


### WARN
**loglevel level constant**

```JavaScript
const console.WARN = 4;
```


### NOTICE
**loglevel level constant**

```JavaScript
const console.NOTICE = 5;
```


### INFO
**loglevel level constant**

```JavaScript
const console.INFO = 6;
```


### DEBUG
**loglevel level constant**

```JavaScript
const console.DEBUG = 7;
```


### PRINT
**loglevel For output only, information output does not break lines, file and syslog do not save this level of information**

```JavaScript
const console.PRINT = 9;
```


### NOTSET
**loglevel level constant**

```JavaScript
const console.NOTSET = 10;
```

