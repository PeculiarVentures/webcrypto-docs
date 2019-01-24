# DES-CBC

> WARNING: Is not W3 WebCrypto specification

## Interfaces

### DesCbcParams interface

```ts
interface DesCbcParams {
    // The initialization vector. MUST be 8 bytes.
    iv: BufferSource;
}
```

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [generateKey](#generate-key) | [DesKeyGenParams](DES.md#DesKeyGenParams-interface) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [importKey](#import-key) | None | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [exportKey](#export-key) | None | [JsonWebKey](https://www.w3.org/TR/WebCryptoAPI/#JsonWebKey-dictionary) or [BufferSource](https://heycam.github.io/webidl/#common-BufferSource) |
| [encrypt](#encrypt) | [DesCbcParams](#DesCbcParams-interface) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [decrypt](#decrypt) | [DesCbcParams](#DesCbcParams-interface) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [wrapKey](#wrap-key) | [DesCbcParams](#DesCbcParams-interface) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [unwrapKey](#unwrap-key) | [DesCbcParams](#DesCbcParams-interface) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |

### Generate key
```js
const key = await crypto.subtle.generateKey(
  {
    name: "DES-CBC",
    length: 64, // 64-bit only
  },
  false, // extractable
  ["encrypt", "decrypt", "wrapKey", "unwrapKey"], // key usages
);
```

### Import key
```js
const key = await crypto.subtle.importKey(
  "raw",   // raw or jwk
  rawData, // BufferSource
  "DES-CBC",
  false,   // extractable
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
const iv = crypto.getRandomValues(new Uint8Array(8));

const encData = await crypto.subtle.encrypt(
  {
    name: "DES-CBC",
    iv, // BufferSource
  },
  key,  // AES key
  data, // BufferSource
);
```

### Decrypt
```js
const data = await crypto.subtle.decrypt(
  {
    name: "DES-CBC",
    iv, // BufferSource
  },
  key,  // AES key
  encData, // BufferSource
);
```

### Wrap key
```js
const iv = crypto.getRandomValues(new Uint8Array(8));

const wrappedKey = await crypto.subtle.wrapKey(
  "pkcs8",   // raw, pkcs8, spki, or jwk
  anyKey,    // Crypto key
  key,       // AES public key
  {
    name: "DES-CBC",
    iv, // BufferSource
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
    name: "DES-CBC",
    iv, // BufferSource
  },
  {
    name: "RSA-PSS",
    hash: "SHA-256",
  }
  false,      // extractable
  ["sign", "verify"],
);
```

