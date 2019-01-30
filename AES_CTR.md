# AES-CTR

[W3 specification](https://www.w3.org/TR/WebCryptoAPI/#aes-ctr)

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [generateKey](#generate-key) | [AesKeyGenParams](https://www.w3.org/TR/WebCryptoAPI/#aes-keygen-params) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [importKey](#import-key) | None | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [exportKey](#export-key) | None | [JsonWebKey](https://www.w3.org/TR/WebCryptoAPI/#JsonWebKey-dictionary) or [BufferSource](https://heycam.github.io/webidl/#common-BufferSource) |
| [encrypt](#encrypt) | [AesCtrParams](https://www.w3.org/TR/WebCryptoAPI/#aes-ctr-params) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [decrypt](#decrypt) | [AesCtrParams](https://www.w3.org/TR/WebCryptoAPI/#aes-cbc-params) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [wrapKey](#wrap-key) | [AesCtrParams](https://www.w3.org/TR/WebCryptoAPI/#aes-cbc-params) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [unwrapKey](#unwrap-key) | [AesCtrParams](https://www.w3.org/TR/WebCryptoAPI/#aes-cbc-params) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |

### Generate key
```js
const key = await crypto.subtle.generateKey(
  {
    name: "AES-CTR",
    length: 128, // 128, 192, or 256
  },
  false, // extractable
  ["encrypt", "decrypt", "wrapKey", "unwrapKey"], // key usages
);
```

### Import key
```js
const key = await crypto.subtle.importKey(
  "raw", // raw or jwk
  new Uint8Array([1, 2, 3, 4, 5, 6, 7, 8, 9, 0, 1, 2, 3, 4, 5, 6]), // raw data
  "AES-CTR",
  false, // extractable
  ["encrypt", "decrypt"],
);
```

### Export key
```js
const raw = await crypto.subtle.exportKey(
  "raw", // raw or jwk
  key,
);
```

### Encrypt
```js
const counter = crypto.getRandomValues(new Uint8Array(16));

const encData = await crypto.subtle.encrypt(
  {
    name: "AES-CTR",
    counter,     // BufferSource
    length: 128, // 1-128
  },
  key,  // AES key
  data, // BufferSource
);
```

### Decrypt
```js
const data = await crypto.subtle.decrypt(
  {
    name: "AES-CTR",
    counter,     // BufferSource
    length: 128, // 1-128
  },
  key,  // AES key
  encData, // BufferSource
);
```

### Wrap key
```js
const counter = crypto.getRandomValues(new Uint8Array(16));

const wrappedKey = await crypto.subtle.wrapKey(
  "pkcs8",   // raw, pkcs8, spki, or jwk
  anyKey,    // Crypto key
  key,       // AES key
  {
    name: "AES-CTR",
    counter,     // BufferSource
    length: 128, // 1-128
  },
);
```

### Unwrap key
```js
const unwrappedKey = await crypto.subtle.unwrapKey(
  "pkcs8",    // raw, pkcs8, spki, or jwk
  wrappedKey, // BufferSource
  key,        // AES key
  {
    name: "AES-CTR",
    counter,     // BufferSource
    length: 128, // 1-128
  },
  {
    name: "RSA-PSS",
    hash: "SHA-256",
  }
  false,      // extractable
  ["sign", "verify"],
);
```
