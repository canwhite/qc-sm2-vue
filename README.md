# qc-sm2-vue
在vue中使用国密sm2，进行非对称加密、签名验签  
sm2被用作替代rsa

## use

```
const cipherMode = 1 // 1 - C1C3C2，0 - C1C2C3，默认为1
//公钥私钥测试用，加密解密的时候客户端只拿公钥
const privateKey = "a2081b5b81fbea0b6b973a3ab6dbbbc65b1164488bf22d8ae2ff0b8260f64853";
const publicKey = "04813d4d97ad31bd9d18d785f337f683233099d5abed09cb397152d50ac28cc0ba43711960e811d90453db5f5a9518d660858a8d0c57e359a8bf83427760ebcbba";


//(1)加密解密，公钥加密，私钥解密
let msgString = "hello world";
let encryptData = sm2.doEncrypt(msgString, publicKey, cipherMode) // 加密结果
console.log("--encode--",encryptData);
let decryptData = sm2.doDecrypt(encryptData, privateKey, cipherMode) // 解密结果
console.log("--decode--",decryptData);
/*
    返回：
    --encode-- 2a9ab59b63725ece7420e9dbed8efc4f0a02e8799e9664b1bf4bd7257569fde6fe2f26f216672347292e019fac46fa8673d9da9636849597e281e8e080d52929b89db84ef82787e339ca7ed1e45c040d254e2c71d947ace11e5a3f3715d1171e6bc2720e8d8bef6feb0f69 Home.vue:64
    --decode-- hello world
*/


//(2)签名验签，私钥签名，公钥验签
let msg = "qc";
let sigValueHex = sm2.doSignature(msg, privateKey) // 签名
let verifyResult = sm2.doVerifySignature(msg, sigValueHex, publicKey) // 验签结果
console.log("--verify",verifyResult);

/*
    返回：
    --verify true
*/




```
