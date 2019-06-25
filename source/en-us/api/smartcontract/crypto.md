---
title: crypto
type: manual
language: en
order: 5
---
# crypto module
Encryption algorithm module

crypto module is a encryption module in FIBOS which supports the  encryption algorithm such as SHA1, SHA256, SHA512, it can be used directly in js contract.

## Static Function

### recover_key
**Recover public key from given hash and signature.**

```JavaScript
crypto.recover_key(digest,signature);
```

Parameter Usage:
* digest: String, Hash result from given message.
* signature: String, given signature.

Results:
* String, return the recovered public key

Example: 

```JavaScript
exports.hi1 = sig => {
    var r = crypto.sha256('I am alive');
    var s = crypto.recover_key(r, sig);
    console.notice(s);
}
```


### sha1
**Create a SHA1 information digest operation object**

```JavaScript
crypto.sha1(data);
```

Parameter Usage:
* data: Buffer, Create while updating binary data.

Results:
* String,  Return the hex encoded string for the result of the information digest

Example: 

```JavaScript
exports.hi = v => {
    var r = crypto.sha1("abcdefg");
    console.error(r);
}
```


### sha256
**Create a SHA256 Information digest operation object**

```JavaScript
crypto.sha256(data);
```

Parameter Usage:
* data: Buffer, Create while updating binary data.
Results:
* String, Return the hex encoded string for the result of the information digest

Example: 

```JavaScript
exports.hi = v => {
    var r = crypto.sha256("abcdefg");
    console.error(r);
}
```


### sha512
**Create a SHA512 Information digest operation object**

```JavaScript
crypto.sha512(data);
```

Parameter Usage:
* data: Buffer, Create while updating binary data.

Results:
* String, Return the hex encoded string for the result of the information digest

Example: 

```JavaScript
exports.hi = v => {
    var r = crypto.sha512("abcdefg");
    console.error(r);
}
```


### ripemd160
**Create a RIPEMD160 Information digest operation object**

```JavaScript
crypto.ripemd160(data);
```

Parameter Usage:
* data:  Buffer, Create while updating binary data.

Results:
* String, Return the hex encoded string for the result of the information digest

Example: 

```JavaScript
exports.hi = v => {
    var r = crypto.ripemd160("abcdefg");
    console.error(r);
}
```

