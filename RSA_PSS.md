# RSA-PSS

[W3 specification](https://www.w3.org/TR/WebCryptoAPI/#rsa-pss)

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [generateKey](#generate-key) | [RsaHashedKeyGenParams](https://www.w3.org/TR/WebCryptoAPI/#RsaHashedKeyGenParams-dictionary) | [CryptoKeyPair](https://www.w3.org/TR/WebCryptoAPI/#keypair) |
| [importKey](#import-key) | [RsaHashedImportParams](https://www.w3.org/TR/WebCryptoAPI/#RsaHashedImportParams-dictionary) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [exportKey](#export-key) | None | [JsonWebKey](https://www.w3.org/TR/WebCryptoAPI/#JsonWebKey-dictionary) or [BufferSource](https://heycam.github.io/webidl/#common-BufferSource) |
| [sign](#sign) | [RsaPssParams](https://www.w3.org/TR/WebCryptoAPI/#RsaPssParams-dictionary) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [verify](#verify) | [RsaPssParams](https://www.w3.org/TR/WebCryptoAPI/#RsaPssParams-dictionary) | Boolean |

### Generate key
```js
const keys = await crypto.subtle.generateKey(
  {
    name: "RSA-PSS",
    hash: "SHA-256",     // SHA-1, SHA-256, SHA-384, or SHA-512
    publicExponent: new Uint8Array([1, 0, 1]), // 0x03 or 0x010001
    modulusLength: 2048, // 1024, 2048, or 4096
  },
  false,
  ["sign", "verify"],
);
```

### Import key
```js
const publicKey = await crypto.subtle.importKey(
  "jwk",
  {
    alg: "PS256",
    ext: true,
    key_ops: ["verify"],
    kty: "RSA",
    e: "AQAB",
    n: "vqpvdxuyZ6rKYnWTj_ZzDBFZAAAlpe5hpoiYHqa2j5kK7v8U5EaPY2bLib9m4B40j-n3FV9xUCGiplWdqMJJKT-4PjGO5E3S4N9kjFhu57noYT7z7302J0sJXeoFbXxlgE-4G55Oxlm52ID2_RJesP5nzcGTriQwoRbrJP5OEt0",
  },
  {
    name: "RSA-PSS",
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
  publicKey);
```

### Sign
```js
const signature = await crypto.subtle.sign(
  {
    name: "RSA-PSS",
    saltLength: 128,
  },
  privateKey, // RSA private key
  data,       // BufferSource
);
```

### Verify
```js
const ok = await crypto.subtle.verify(
  {
    name: "RSA-PSS",
    saltLength: 128,
  },
  publicKey, // RSA public key
  signature, // BufferSource
  data,      // BufferSource
);
```