# Crypto

`crypto` 模块提供了加密功能，包括OpenSSL 的哈希、HMAC、加密、解密、签名、以及验证功能的一整套封装.

Nodejs用C/C++实现这些算法后，通过cypto这个模块暴露为JavaScript接口，这样用起来方便，运行速度也快。

## HASH

哈希算法 MD5 SHA1 SHA256 SHA512

```javascript
const crypto = require('crypto');

// 使用md5哈希算法  md5  sha1  sha256 sha512
const hash = crypto.createHash('sha1');

// 拼接加密
 hash.update('Hello').update('vue')
 hash.update('Hellovue')

// default output buffer value  
 console.log(hash.digest('hex'));

```



## HMAC

增强型哈希算法,自定义secret-key

```
const crypto = require('crypto');

// algorithm key 
const hmac = crypto.createHmac('sha256', 'secret-key');

hmac.update('life is short you need python');

console.log(hmac.digest('hex')); 
```

## AES

对称加密算法 	aes192`，`aes-128-ecb`，`aes-256-cbc

```javascript
const crypto = require('crypto');

const cipher = crypto.createCipher('aes192', 'key')
let crypted = cipher.update('life is short you need python', 'utf8', 'hex')
crypted += cipher.final('hex');
console.log(crypted);

const decipher = crypto.createDecipher('aes192', 'key');
let decrypted = decipher.update(crypted, 'hex', 'utf8')
decrypted += decipher.final('utf8')
console.log(decrypted);
```

## RSA

由一个私钥和一个公钥构成的密钥对,通过私钥加密，公钥解密，或者通过公钥加密，私钥解密。











