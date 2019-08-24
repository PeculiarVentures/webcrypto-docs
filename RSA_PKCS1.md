# RSA-PKCS1

> WARNING: Is not W3 WebCrypto specification

## Interfaces

### RsaPkcs1EncryptParams interface

```ts
interface RsaPkcs1EncryptParams extends Algorithm {
}
```

### RsaPkcs1SignParams interface

```ts
interface RsaPkcs1SignParams extends Algorithm {
  // The hash algorithm to use 
  hash: HashAlgorithmIdentifier;
}
```

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [generateKey](#generate-key) | [RsaHashedKeyGenParams](https://www.w3.org/TR/WebCryptoAPI/#RsaKeyGenParams-dictionary) | [CryptoKeyPair](https://www.w3.org/TR/WebCryptoAPI/#keypair) |
| [importKey](#import-key) | [RsaHashedImportParams](https://www.w3.org/TR/WebCryptoAPI/#algorithm-dictionary) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [exportKey](#export-key) | None | [JsonWebKey](https://www.w3.org/TR/WebCryptoAPI/#JsonWebKey-dictionary) or [BufferSource](https://heycam.github.io/webidl/#common-BufferSource) |
| [sign](#sign) | [RsaPkcs1SignParams](#RsaPkcs1SignParams-interface) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [verify](#verify) | [RsaPkcs1SignParams](#RsaPkcs1SignParams-interface) | Boolean |
| [encrypt](#encrypt) | [RsaPkcs1EncryptParams](#RsaPkcs1EncryptParams-interface) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [decrypt](#decrypt) | [RsaPkcs1EncryptParams](#RsaPkcs1EncryptParams-interface) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [wrapKey](#wrap-key) | [RsaPkcs1EncryptParams](#RsaPkcs1EncryptParams-interface) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [unwrapKey](#unwrap-key) | [RsaPkcs1EncryptParams](#RsaPkcs1EncryptParams-interface) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |

### Generate key
```js
const keys = await crypto.subtle.generateKey(
  {
    name: "RSA-PKCS1",
    publicExponent: new Uint8Array([1, 0, 1]), // 0x03 or 0x010001
    modulusLength: 2048, // 1024, 2048, or 4096
  },
  false,
  ["sign", "verify", "encrypt", "decrypt", "wrapKey", "unwrapKey"],
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
    name: "RSA-PKCS1",
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
    name: "RSA-PKCS1",
    hash: "SHA-256",
  },
  privateKey, // RSA private key
  data,       // BufferSource
);
```

### Verify
```js
const ok = await crypto.subtle.verify(
  {
    name: "RSA-PKCS1",
    hash: "SHA-256",
  },
  publicKey, // RSA public key
  signature, // BufferSource
  data,      // BufferSource
);
```

### Encrypt
```js
const encData = await crypto.subtle.encrypt(
  "RSA-PKCS1",
  publicKey,  // RSA public key
  data,       // BufferSource
);
```

### Decrypt
```js
const data = await crypto.subtle.decrypt(
  "RSA-PKCS1",
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
  "RSA-PKCS1",
);
```

### Unwrap key
```js
const unwrappedKey = await crypto.subtle.unwrapKey(
  "raw",      // raw, pkcs8, spki, or jwk
  wrappedKey, // BufferSource
  privateKey, // RSA private key
  "RSA-PKCS1",,
  {
    name: "AES-CBC",
    label: 128,
  }
  false,      // extractable
  ["encrypt", "decrypt"],
);
```