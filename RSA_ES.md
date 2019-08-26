# RSAES-PKCS1-v1_5

> WARNING: This is not compliant with the W3 WebCrypto specification.

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [generateKey](#generate-key) | [RsaKeyGenParams](https://www.w3.org/TR/WebCryptoAPI/#RsaKeyGenParams-dictionary) | [CryptoKeyPair](https://www.w3.org/TR/WebCryptoAPI/#keypair) |
| [importKey](#import-key) | [Algorithm](https://www.w3.org/TR/WebCryptoAPI/#algorithm-dictionary) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [exportKey](#export-key) | None | [JsonWebKey](https://www.w3.org/TR/WebCryptoAPI/#JsonWebKey-dictionary) or [BufferSource](https://heycam.github.io/webidl/#common-BufferSource) |
| [encrypt](#encrypt) | [Algorithm](https://www.w3.org/TR/WebCryptoAPI/#algorithm-dictionary) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [decrypt](#decrypt) | [Algorithm](https://www.w3.org/TR/WebCryptoAPI/#algorithm-dictionary) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [wrapKey](#wrap-key) | [Algorithm](https://www.w3.org/TR/WebCryptoAPI/#algorithm-dictionary) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [unwrapKey](#unwrap-key) | [Algorithm](https://www.w3.org/TR/WebCryptoAPI/#algorithm-dictionary) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |

### Generate key
```js
const keys = await crypto.subtle.generateKey(
  {
    name: "RSAES-PKCS1-v1_5",
    publicExponent: new Uint8Array([1, 0, 1]), // 0x03 or 0x010001
    modulusLength: 2048, // 1024, 2048, or 4096
  },
  false,
  ["encrypt", "decrypt", "wrapKey", "unwrapKey"],
);
```

### Import key
```js
const publicKey = await crypto.subtle.importKey(
  "jwk",
  {
    alg: "RS256",
    ext: true,
    key_ops: ["verify"],
    kty: "RSA",
    e: "AQAB",
    n: "vqpvdxuyZ6rKYnWTj_ZzDBFZAAAlpe5hpoiYHqa2j5kK7v8U5EaPY2bLib9m4B40j-n3FV9xUCGiplWdqMJJKT-4PjGO5E3S4N9kjFhu57noYT7z7302J0sJXeoFbXxlgE-4G55Oxlm52ID2_RJesP5nzcGTriQwoRbrJP5OEt0",
  },
  {
    name: "RSAES-PKCS1-v1_5",
  },
  false,
  ["encrypt"],
);
```

### Export key
```js
const jwk = await crypto.subtle.exportKey(
  "jwk",
  publicKey);
```

### Encrypt
```js
const encData = await crypto.subtle.encrypt(
  "RSAES-PKCS1-v1_5",
  publicKey,  // RSA public key
  data,       // BufferSource
);
```

### Decrypt
```js
const data = await crypto.subtle.decrypt(
  "RSAES-PKCS1-v1_5",
  privateKey, // RSA private key
  encData,    // BufferSource
);
```

### Wrap key
```js
const wrappedKey = await crypto.subtle.wrapKey(
  "raw",     // raw, pkcs8, spki, or jwk
  aesKey,    // Crypto key
  publicKey, // RSA public key
  "RSAES-PKCS1-v1_5",
);
```

### Unwrap key
```js
const unwrappedKey = await crypto.subtle.unwrapKey(
  "raw",      // raw, pkcs8, spki, or jwk
  wrappedKey, // BufferSource
  privateKey, // RSA private key
  "RSAES-PKCS1-v1_5",
  {
    name: "AES-CBC",
    label: 128,
  }
  false,      // extractable
  ["encrypt", "decrypt"],
);
```