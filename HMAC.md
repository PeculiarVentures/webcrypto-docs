# HMAC

[W3 specification](https://www.w3.org/TR/WebCryptoAPI/#hmac)

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [generateKey](#generate-key) | [HmacKeyGenParams](https://www.w3.org/TR/WebCryptoAPI/#hmac-keygen-params) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [importKey](#import-key) | [HmacImportParams](https://www.w3.org/TR/WebCryptoAPI/#hmac-importparams) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [exportKey](#export-key) | None | [JsonWebKey](https://www.w3.org/TR/WebCryptoAPI/#JsonWebKey-dictionary) or [BufferSource](https://heycam.github.io/webidl/#common-BufferSource) |
| [sign](#sign) | None | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [verify](#verify) | None | Boolean |

### Generate key
```js
const keys = await crypto.subtle.generateKey(
  {
    name: "HMAC",
    hash: "SHA-256", // SHA-1, SHA-256, SHA-384, or SHA-512
    length: 128,     // 128, 192, or 256
  },
  false,
  ["sign", "verify"],
);
```

### Import key
```js
const key = await crypto.subtle.importKey(
  "jwk",
  {
    alg: "HS256",
    ext: true,
    k: "AQIDBAUGBwgJAAECAwQFBg",
    key_ops: ["sign", "verify"],
    kty: "oct",
  },
  {
    name: "HMAC",
    hash: "SHA-256",
  },
  false,
  ["verify"],
);
```

### Export key
```js
const jwk = await crypto.subtle.exportKey(
  "jwk",
  key,
);
```

### Sign
```js
const signature = await crypto.subtle.sign(
  "HMAC",
  key,
  data,  // BufferSource
);
```

### Verify
```js
const ok = await crypto.subtle.verify(
  "HMAC",
  key,
  signature, // BufferSource
  data,      // BufferSource
);
```