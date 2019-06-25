---
title: buffer
type: manual
language: en
order: 3
---
# Object buffer
Binary data cache object for IO read-write data processing

Buffer object is global basic class, can be created with new Buffer(...) by anytime：

```JavaScript
var buf = new Buffer();
```

## Static function
     
### isBuffer
**Detects whether a given variable is a Buffer object**

```JavaScript
Buffer.isBuffer(v);
```

Parameter Usage:
* v: Value, Give the variables to detect

Results:
* Boolean, Whether the incoming object is a Buffer object
Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer("abcd");
    var str = "abcd"
    console.log(Buffer.isBuffer(buf));
    console.log(Buffer.isBuffer(str));
}
```


### from
**Use other Buffer to create Buffer object**

```JavaScript
Buffer.from(buffer,byteOffset,length);   
```

Parameter Usage:
* buffer: Buffer, A Buffer type variable is given to create a Buffer object
* byteOffset: Integer, Specifies the data start position, start with 0
* length: Integer, Specify data length，start with -1，Represents all the remaining data

Results:
* Buffer, Return Buffer Example

Example:

```JavaScript
exports.hi = v => {
    var buf = Buffer.from(new Buffer("abcd"), 1, 2);
    console.log(buf.toString());
}
```


**Use string to create Buffer object**

```JavaScript
Buffer.from(str,byteOffset,length);
```

Parameter Usage:
* str: String, Initialize string，the string will be written in format utf-8
* byteOffset: Integer, Specifies the data start position，start with 0
* length: Integer, Specify data length，start with -1，Represents all the remaining data

Results:
* Buffer, Return Buffer Example

Example:

```JavaScript
exports.hi = v => {
    var buf = Buffer.from("abcd", 0, 2);
    console.log(buf.toString());
}
```


**Use string to create Buffer object**

```JavaScript
Buffer.from(str,codec);
```

Parameter Usage:
* str: String, Initializing string，the string will be written in format utf-8, default is to create a empty object.
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system

Results:
* Buffer, Return Buffer Example

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer(Awesome！", "utf8");
    console.log(buf.toString());
}
```


### concat
**Concatenate data in multiple cache regions**

```JavaScript
Buffer.concat(buflist,cutLength);
```

Parameter Usage:
* buflist: Array, Buffer array to be spliced
* cutLength: Integer, How many Buffer objects to intercept

Results:
* Buffer, new Buffer object spliced result

Example:

```JavaScript
exports.hi = v => {
    var buf1 = new Buffer("abcd");
    var buf2 = new Buffer("efg");
    var buf3 = new Buffer();
    var bufArray = [buf1];
    var bufRes = Buffer.concat(bufArray);
    console.log(bufRes.toString());

    bufArray = [buf1, buf2];
    bufRes = Buffer.concat(bufArray);
    console.log(bufRes.toString());

    bufRes = Buffer.concat(bufArray, 6);
    console.log(bufRes.toString());

    buf1 = new Buffer([0x31, 0x32, 0x33, 0x34]);
    buf2 = new Buffer([0x35, 0x36, 0x37, 0x38]);
    bufArray = [buf1, buf2];
    bufRes = Buffer.concat(bufArray);
    console.log(bufRes.toString());

    var buf2 = Buffer.concat([]);
    console.log(buf2.length);
}
```


### alloc
**Allocates a new cache area of specified length. If the size is 0, a zero-length buffer is created.**

```JavaScript
Buffer.alloc(size,fill,codec);
```

Parameter Usage:
* size: Integer, The required length of the buffer
* fill: Integer, Prepopulate the value of the new buffer, string/buffer/integer value types can be used Default：0
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system

Results:
* Buffer, Populates the new Buffer object

Example:

```JavaScript
exports.hi = v => {
    var buf1 = Buffer.alloc(10, 0, "utf8");
    console.log(buf1.toString());
}
```


**Allocates a new cache area of specified length. If the size is 0, a zero-length buffer is created.**

```JavaScript
Buffer Buffer.alloc(size,fill,codec);
```

Parameter Usage:
* size: Integer, The required length of the buffer
* fill: String, Prepopulate the value of the new buffer，string/buffer/integer value types can be used. Default：0
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system

Results:
* Buffer, Populates the new Buffer object

Example:

```JavaScript
exports.hi = v => {
    var buf1 = Buffer.alloc(11, 'aGVsbG8gd29ybGQ=', 'base64');
    var buf2 = Buffer.alloc(16, 'aGVsbG8gd29ybGQ=', 'base64');
    console.log(buf1.toString());
    console.log(buf2.toString());
}
```


**Allocates a new cache area of specified length. If the size is 0, a zero-length buffer is created.**

```JavaScript
Buffer.alloc(size,fill,codec);
```

Parameter Usage:
* size: Integer, The required length of the buffer
* fill: Buffer, Prepopulate the value of the new buffer, string/buffer/integer value types can be used. Default：0
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system

Results:
* Buffer, Populates the new Buffer object

Example:

```JavaScript
exports.hi = v => {
    var buf1 = Buffer.alloc(11, new Buffer('aGVsbG8gd29ybGQ='), 'base64');
    var buf2 = Buffer.alloc(16, new Buffer('aGVsbG8gd29ybGQ='), 'base64');
    console.log(buf1.toString());
    console.log(buf2.toString());
}
```


### allocUnsafe
**Allocates a new cache area of specified length. If the size is 0, a zero-length buffer is created.**

```JavaScript
Buffer.allocUnsafe(size);
```

Parameter Usage:
* size: Integer, The required length of the buffer

Results:
* Buffer, Specifies the size of the new Buffer object

Example:

```JavaScript
exports.hi = v => {
    var buf1 = Buffer.allocUnsafe(10);
    console.log(buf1.length);
}
```


### allocUnsafeSlow
**Allocates a new cache area of specified length. If the size is 0, a zero-length buffer is created.**

```JavaScript
Buffer.allocUnsafeSlow(size);
```

Parameter Usage:
* size: Integer, The required length of the buffer

Results:
* Buffer, Specifies the size of the new Buffer object

Example:

```JavaScript
exports.hi = v => {
    var buf1 = Buffer.allocUnsafeSlow(10);
    console.log(buf1.length);
}
```


### isEncoding
**Check whether the encoding format is supported**

```JavaScript
Buffer.isEncoding(codec);
```

Parameter Usage:
* codec: String, Encoding format to be check

Results:
* Boolean, wether it is supported

Example:

```JavaScript
exports.hi = v => {
    console.log(Buffer.isEncoding('utf8')); // true
    console.log(Buffer.isEncoding('utf-8')); // true
    console.log(Buffer.isEncoding('gbk')); // false
    console.log(Buffer.isEncoding('gb2312')); // false
    console.log(Buffer.isEncoding('hex')); // true
    console.log(Buffer.isEncoding('base64')); // true
    console.log(Buffer.isEncoding('jis')); // false
    console.log(Buffer.isEncoding('aaabbbccc')); // false
    console.log(Buffer.isEncoding('binary')); // false
    console.log(Buffer.isEncoding('latin1')); // false
    console.log(Buffer.isEncoding('big5')); // false
}
```

## Member attribute
        
### length
**Integer, Get the size of the cached object**

```JavaScript
readonly Integer Buffer.length;
```

## member function
        
### Buffer
**Cache object constructors**

```JavaScript
Buffer.Buffer(Array datas);
```

Parameter Usage:
* datas: Array, Initialize the data array

```JavaScript
exports.hi = v => {
    var buf = new Buffer([0x31, 0x32, 0x33, 0x34])
    console.log(buf.toString());
}
```


**Cache object constructors**

```JavaScript
Buffer.Buffer(ArrayBuffer datas);
```

Parameter Usage:
* datas: ArrayBuffer, Initialize the data array

```JavaScript
exports.hi = v => {
    var arr = new Uint16Array(2);
    arr[0] = 5000;
    arr[1] = 4000;
    var buf = new Buffer(arr.buffer);
    console.log(buf.hex());
}
```


**Cache object constructors**

```JavaScript
Buffer.Buffer(TypedArray datas);
```

Parameter Usage:
* datas: TypedArray, Initializes the data array

```JavaScript
exports.hi = v => {
    var arr = new Uint8Array(2);
    arr[0] = 50;
    arr[1] = 40;
    var buf = new Buffer(arr);
    console.log(buf.hex());

    var arr = new Uint16Array(2);
    arr[0] = 5000;
    arr[1] = 4000;
    var buf = new Buffer(arr);
    console.log(buf.hex());

    var arr = new Uint8Array([0x10, 0x20, 0x30]);
    var arr1 = new Uint8Array(arr.buffer, 1, 2);
    var buf = new Buffer(arr1);
    console.log(buf.hex());
}
```


**Cache object constructors**

```JavaScript
Buffer.Buffer(ArrayBufferView datas);
```

Parameter Usage:
* datas: ArrayBufferView, Initialize the data array

```JavaScript
exports.hi = v => {
    var arr = new DataView(new ArrayBuffer(2));
    arr.setInt8(0, 0x10);
    arr.setInt8(1, 0x20);
    var buf = new Buffer(arr);
    console.log(buf.hex());
}
```


**Cache object constructors**

```JavaScript
Buffer.Buffer(Buffer buffer);
```

Parameter Usage:
* buffer: Buffer, Initialize the buffer object

```JavaScript
exports.hi = v => {
    var buf = new Buffer(new Buffer("abcd"));
    console.log(buf.toString());
}
```


**Cache object constructors**

```JavaScript
Buffer.Buffer(String str,
    String codec = "utf8");
```

Parameter Usage:
* str: String, Initialize string，the string will be written in by the format of utf-8，default is to create an empty object.
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system

```JavaScript
exports.hi = v => {
    var buf = new Buffer("abcd", "utf8");
    console.log(buf.toString());
}
```


**Cache object constructors**

```JavaScript
Buffer.Buffer(Integer size = 0);
```

Parameter Usage:
* size: Integer, Initialize size of buffer area

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer(100);
    console.log(buf.length);
}
```


### resize
**resize cached object**

```JavaScript
Buffer.resize(Integer sz);
```

Parameter Usage:
* sz: Integer, give a new size

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer("abcded");
    buf.resize(10);
    console.log(buf);
}
```


### append
** Write a binary array in the end of cached object**

```JavaScript
Buffer.append(Buffer data);
```

Parameter Usage:
* data: Buffer, Initialize binary data

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer([0x31, 0x32, 0x33, 0x34]);
    buf.append("abcd");
    buf.append([0x31, 0x32, 0x33, 0x34]);
    console.log(buf.toString());
}
```


**Write a string at the end of the cached object, which is written in utf-8 format**

```JavaScript
Buffer.append(String str,
    String codec = "utf8");
```

Parameter Usage:
* str: String, strings need to be written
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer([0x31, 0x32, 0x33, 0x34]);
    buf.append("3132", "hex");
    buf.append("MTIzNA==", "base64");
    console.log(buf.toString());
}
```


### write
**Write specific string to cached object, default string is utf-8, Only part of the data is written when the boundary is crossed**

```JavaScript
Integer Buffer.write(String str,
    Integer offset = 0,
    Integer length = -1,
    String codec = "utf8");
```

Parameter Usage:
* str: String, The string to be written
* offset: Integer, Write start point
* length: Integer, Write lenth（Unit of byte，Default-1），The length of the string to be written if not specified
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system

Results:
* Integer, The length of written data byte

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer(10);
    buf.write("abcd", 0, 4, 'utf8')
    console.log(buf.toString('utf8', 0, 4));
}
```


**Write specific string to cached object, default string is utf-8, Only part of the data is written when the boundary is crossed**

```JavaScript
Integer Buffer.write(String str,
    Integer offset = 0,
    String codec = "utf8");
```

Parameter Usage:
* str: String, The string to be written
* offset: Integer, Write start point
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system

Results:
* Integer, The length of written data byte

Example:

```JavaScript
exports.hi = v => {
    buf = new Buffer(10);
    buf.write("MTIzNA==", 0, "base64");
    console.log(buf.toString("utf8", 0, 4));
}
```


**Write specific string to cached object, default string is utf-8, Only part of the data is written when the boundary is crossed**

```JavaScript
Integer Buffer.write(String str,
    String codec = "utf8");
```

Parameter Usage:
* str: String, The string to be written
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system

Results:
* Integer, The length of written data byte

Example:

```JavaScript
exports.hi = v => {
    buf = new Buffer(10);
    buf.write("MTIzNA==", "base64");
    console.log(buf.toString("utf8"));
}
```


### fill
**Fill in specific content data to buffer object**

```JavaScript
Buffer Buffer.fill(Integer v,
    Integer offset = 0,
    Integer end = -1);
```

Parameter Usage:
* v: Integer, Data that needs to be populated. If offset and end are not specified, the buffer is filled
* offset: Integer, fill in starting point
* end: Integer, fill in ending point

Results:
* Buffer, Return current Buffer object

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer(10);
    buf.fill(1);
    console.log(buf.toString());
}
```


**Fill in specific content data to buffer object**

```JavaScript
Buffer Buffer.fill(Buffer v,
    Integer offset = 0,
    Integer end = -1);
```

Parameter Usage:
* v: Buffer, Data that needs to be populated. If offset and end are not specified, the buffer is filled
* offset: Integer, fill in starting point
* end: Integer, fill in ending point

Results:
* Buffer, Return current Buffer object

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer(10);
    buf.fill(new Buffer("abc"));
    console.log(buf.toString());
}
```


**Fill in specific content data to buffer object**

```JavaScript
Buffer Buffer.fill(String v,
    Integer offset = 0,
    Integer end = -1);
```

Parameter Usage:
* v: String, Data that needs to be populated. If offset and end are not specified, the buffer is filled
* offset: Integer, Write starting position
* end: Integer, Write ending position

Results:
* Buffer, Return current Buffer object

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer(10);
    buf.fill("abc");
    console.log(buf.toString());
}
```


### indexOf
**Return the location in Buffer where the specificdata first appears**

```JavaScript
Integer Buffer.indexOf(Integer v,
    Integer offset = 0);
```

Parameter Usage:
* v: Integer, Data to be looked up，if offset is not defined，start from starting point by default
* offset: Integer, Initial search location

Results:
* Integer, Return the location found，Return -1 if Not found

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer([0x31, 0x32, 0x33, 0x34, 0x00]);
    console.log(buf.indexOf(0x33));
    console.log(buf.indexOf(0x00));
}
```


**Return the location in Buffer where the specificdata first appears**

```JavaScript
Integer Buffer.indexOf(String v,
    Integer offset = 0);
```

Parameter Usage:
* v: String, Data to be looked up，if offset is not defined，start from starting point by default
* offset: Integer, Find starting location

Results:
* Integer, Return the location found，Return -1 if Not found

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer("cacdbfcde");
    console.log(buf.indexOf("cd", 1));

}
```


### compare
**Compares the contents of the cache area**

```JavaScript
Integer Buffer.compare(Buffer buf);
```

Parameter Usage:
* buf: Buffer, Cache objects to be compared

Results:
* Integer, Content comparison results

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer("abcd");
    console.log(buf.compare(new Buffer("abcd")));
    console.log(buf.compare(new Buffer("abc")));
    console.log(buf.compare(new Buffer("abcde")));
}
```


### copy
**Copy data from the source cache object region to the target cache object region**

```JavaScript
Integer Buffer.copy(Buffer targetBuffer,
    Integer targetStart = 0,
    Integer sourceStart = 0,
    Integer sourceEnd = -1);
```

Parameter Usage:
* targetBuffer: Buffer, Target cache object
* targetStart: Integer, The target cache object begins copying the byte location，default is 0
* sourceStart: Integer, Source cache object starting byte location, default is 0
* sourceEnd: Integer, Source cache object ending byte location, default is -1, Represents the length of the source data

Results:
* Integer, copy the length of the data bytes

Example:

```JavaScript
exports.hi = v => {
    var buf1 = new Buffer([0x31, 0x32, 0x33]);
    var arr = [0x34, 0x35, 0x36];

    var buf2 = new Buffer(arr);
    var sz = buf1.copy(buf2);
    console.log(sz);
    console.log(buf2.toString());
}
```


### slice
**Return a new cache object，Contains data that specifies the start to end of the cache**

```JavaScript
Buffer Buffer.slice(Integer start = 0);
```

Parameter Usage:
* start: Integer, Specifies the start of the range, starting from scratch by default

Results:
* Buffer, Return a new cache object

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer(10);
    buf.write("abcdefghih");
    console.log(buf.slice(8).toString());
}
```


**Return a new cache object，Contains data for the specified range, and returns only a valid portion of the data if the range exceeds the cache**

```JavaScript
Buffer Buffer.slice(Integer start,
    Integer end);
```

Parameter Usage:
* start: Integer, Specifies the start of the range
* end: Integer, Specifies the end of the range

Results:
* Buffer, Return a new cache objecrt

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer(10);
    buf.write("abcdefghih");
    console.log(buf.slice(0, 3).toString());
    console.log(buf.slice(0, 11).toString());
}
```


### join
**Puts all elements of the current object into a string**

```JavaScript
String Buffer.join(String separator = ",");
```

Parameter Usage:
* separator: String, split string，default is ","

Results:
* String, Return generated data

Example:

```JavaScript
exports.hi = v => {
    var a = new Buffer([192, 168, 0, 1]);
    console.log(a.join('.'));
}
```


### reverse
**Return a new cache object，Contains the inverted order of the current object data**

```JavaScript
Buffer Buffer.reverse();
```

Results:
* Buffer, Return new cache object

Example:

```JavaScript
exports.hi = v => {
    var a = new Buffer("abcd");
    console.log(a.reverse().toString());
}
```


### equals
**Compares whether the current object is equal to a given object**

```JavaScript
Boolean Buffer.equals(object expected);
```

Parameter Usage:
* expected: object, Set goals for comparison

Results:
* Boolean, Return objects comparing results

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer("abcd");
    console.log(buf.equals(new Buffer("abcd")));
    console.log(buf.equals(new Buffer("abc")));
}
```


### hex
**Use hex to cache object content**

```JavaScript
String Buffer.hex();
```

Results:
* String, Return encoding string


### base64
**use base64 encodes to cache object content**

```JavaScript
String Buffer.base64();
```

Results:
* String, Return encoding string


### keys
**Return all arrays of binary data**

```JavaScript
Iterator Buffer.keys();
```

Results:
* Iterator, Return iterator includes object data index


### values
**Return all arrays of binary data**

```JavaScript
Iterator Buffer.values();
```

Results:
* Iterator, Return iterator includes object data index


### entries
**Return including object data [index, byte] Right iterator**

```JavaScript
Iterator Buffer.entries();
```

Results:
* Iterator, [index, byte] Right iterator


### toArray
**Return all arrays of binary data**

```JavaScript
Array Buffer.toArray();
```

Results:
* Array, Return arrays includes data object

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer("buffer");
    console.log(buf.toArray());
}
```


### toString
**Return encoding string of binary data**

```JavaScript
String Buffer.toString(String codec,
    Integer offset = 0,
    Integer end);
```

Parameter Usage:
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system
* offset: Integer, read starting point
* end: Integer, read ending point

Results:
* String, Return string of the object

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer([0x31, 0x32, 0x33, 0x34]);
    console.log(buf.toString("utf8", 1, 3));
}
```


**Return encoding string of binary data**

```JavaScript
String Buffer.toString(String codec,
    Integer offset = 0);
```

Parameter Usage:
* codec: String, Specifies the encoding format with an allowable value of："hex", "base64", "utf8", Or the character sets supported by the system
* offset: Integer, read start point.

Results:
* String, Return string of the object

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer([0x31, 0x32, 0x33, 0x34]);
    console.log(buf.toString("utf8", 1));
    console.log(buf.toString("hex", 2));
    console.log(buf.toString("base64", 2));
}
```


**Return binary utf8 string**

```JavaScript
String Buffer.toString();
```

Results:
* String, Return string of the object

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer([0x31, 0x32, 0x33, 0x34]);
    console.log(buf.toString());
}
```


### toJSON
**Return JSON format of the object，Return a collection of readable properties defined by an object**

```JavaScript
String Buffer.toJSON();
```

Results:
* String, Return JSON format of the object

Example:

```JavaScript
exports.hi = v => {
    var buf = new Buffer("buffer");
    console.log(buf.toJSON());
}
```
