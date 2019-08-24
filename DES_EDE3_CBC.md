# DES-EDE3-CBC

> WARNING: This is not compliant with the W3 WebCrypto specification.

## Interfaces

### DesCbcParams interface

```ts
interface DesEde3CbcParams {
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
| [encrypt](#encrypt) | [DesEde3CbcParams](#DesEde3CbcParams-interface) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [decrypt](#decrypt) | [DesEde3CbcParams](#DesEde3CbcParams-interface) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [wrapKey](#wrap-key) | [DesEde3CbcParams](#DesEde3CbcParams-interface) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [unwrapKey](#unwrap-key) | [DesEde3CbcParams](#DesEde3CbcParams-interface) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |

### Generate key
```js
const key = await crypto.subtle.generateKey(
  {
    name: "DES-EDE3-CBC",
    length: 192, // 192-bit only
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
  "DES-EDE3-CBC",
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
    name: "DES-EDE3-CBC",
    iv, // BufferSource
  },
  key,  // DES key
  data, // BufferSource
);
```

### Decrypt
```js
const data = await crypto.subtle.decrypt(
  {
    name: "DES-EDE3-CBC",
    iv, // BufferSource
  },
  key,  // DES key
  encData, // BufferSource
);
```

### Wrap key
```js
const iv = crypto.getRandomValues(new Uint8Array(8));

const wrappedKey = await crypto.subtle.wrapKey(
  "pkcs8",   // raw, pkcs8, spki, or jwk
  anyKey,    // Crypto key
  key,       // DES key
  {
    name: "DES-EDE3-CBC",
    iv, // BufferSource
  },
);
```

### Unwrap key
```js
const unwrappedKey = await crypto.subtle.unwrapKey(
  "pkcs8",    // raw, pkcs8, spki, or jwk
  wrappedKey, // BufferSource
  key,        // DES key
  {
    name: "DES-EDE3-CBC",
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

