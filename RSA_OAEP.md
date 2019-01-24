# RSA-OAEP

[W3 specification](https://www.w3.org/TR/WebCryptoAPI/#rsa-oaep)

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [generateKey](#generate-key) | [RsaHashedKeyGenParams](https://www.w3.org/TR/WebCryptoAPI/#RsaHashedKeyGenParams-dictionary) | [CryptoKeyPair](https://www.w3.org/TR/WebCryptoAPI/#keypair) |
| [importKey](#import-key) | [RsaHashedImportParams](https://www.w3.org/TR/WebCryptoAPI/#RsaHashedImportParams-dictionary) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [exportKey](#export-key) | None | [JsonWebKey](https://www.w3.org/TR/WebCryptoAPI/#JsonWebKey-dictionary) or [BufferSource](https://heycam.github.io/webidl/#common-BufferSource) |
| [encrypt](#encrypt) | [RsaOaepParams](https://www.w3.org/TR/WebCryptoAPI/#rsa-oaep-params) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [decrypt](#decrypt) | [RsaOaepParams](https://www.w3.org/TR/WebCryptoAPI/#rsa-oaep-params) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [wrapKey](#wrap-key) | [RsaOaepParams](https://www.w3.org/TR/WebCryptoAPI/#rsa-oaep-params) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [unwrapKey](#unwrap-key) | [RsaOaepParams](https://www.w3.org/TR/WebCryptoAPI/#rsa-oaep-params) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |

### Generate key
```js
const keys = await crypto.subtle.generateKey(
  {
    name: "RSA-OAEP",
    hash: "SHA-256",     // SHA-1, SHA-256, SHA-384, or SHA-512
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
    alg: "RSA-OAEP-256",
    ext: true,
    key_ops: ["encrypt"],
    kty: "RSA",
    e: "AQAB",
    n: "vqpvdxuyZ6rKYnWTj_ZzDBFZAAAlpe5hpoiYHqa2j5kK7v8U5EaPY2bLib9m4B40j-n3FV9xUCGiplWdqMJJKT-4PjGO5E3S4N9kjFhu57noYT7z7302J0sJXeoFbXxlgE-4G55Oxlm52ID2_RJesP5nzcGTriQwoRbrJP5OEt0",
  },
  {
    name: "RSA-OAEP",
    hash: "SHA-256",
    publicExponent: new Uint8Array([1, 0, 1]),
    modulusLength: 2048,
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
const label = crypto.getRandomValues(new Uint8Array(5));

const encData = await crypto.subtle.encrypt(
  {
    name: "RSA-OAEP",
    label, // Optional. BufferSource
  },
  publicKey,  // RSA public key
  data,       // BufferSource
);
```

### Decrypt
```js
const data = await crypto.subtle.encrypt(
  {
    name: "RSA-OAEP",
    label, // Optional. BufferSource
  },
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
  {
    name: "RSA-OAEP",
    label, // Optional. BufferSource
  },
);
```

### Unwrap key
```js
const unwrappedKey = await crypto.subtle.unwrapKey(
  "raw",      // raw, pkcs8, spki, or jwk
  wrappedKey, // BufferSource
  privateKey, // RSA private key
  {
    name: "RSA-OAEP",
    label, // Optional. BufferSource
  },
  {
    name: "AES-CBC",
    label: 128,
  }
  false,      // extractable
  ["encrypt", "decrypt"],
);
```
