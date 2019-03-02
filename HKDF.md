# HKDF

[W3 specification](https://www.w3.org/TR/WebCryptoAPI/#hkdf)

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [importKey](#import-key) | None | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [deriveBits](#derive-bits) | [HkdfParams](https://www.w3.org/TR/WebCryptoAPI/#hkdf-params) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [deriveKey](#derive-key) | [HkdfParams](https://www.w3.org/TR/WebCryptoAPI/#hkdf-params) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |

### Import key
```js
const key = await crypto.subtle.importKey(
  "raw", // only raw format
  password, // BufferSource
  "HKDF",
  false, // only false
  ["deriveBits", "deriveKey"],
);
```

### Derive bits
```js
const salt = crypto.getRandomValues(new Uint8Array(4));
const info = crypto.getRandomValues(new Uint8Array(4));

const derivedBits = await crypto.subtle.deriveBits(
  {
    name: "HKDF",
    salt,
    info,
    hash: "SHA-256",
  },
  key,
  128,
);
```

### Derive key
```js
const salt = crypto.getRandomValues(new Uint8Array(4));
const info = crypto.getRandomValues(new Uint8Array(4));

const derivedKey = await crypto.subtle.deriveKey(
  {
    name: "HKDF",
    salt,
    info,
    hash: "SHA-256",
  },
  key,
  {
    name: "AES-CBC",
    length: 128,
  },
  false,
  ["encrypt", "decrypt"],
);
```