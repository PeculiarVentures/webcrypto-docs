# ECDSA

[W3 specification](https://www.w3.org/TR/WebCryptoAPI/#ecdsa)

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [generateKey](#generate-key) | [EcKeyGenParams](https://www.w3.org/TR/WebCryptoAPI/#EcKeyGenParams-dictionary) | [CryptoKeyPair](https://www.w3.org/TR/WebCryptoAPI/#keypair) |
| [importKey](#import-key) | [EcKeyImportParams](https://www.w3.org/TR/WebCryptoAPI/#EcKeyImportParams-dictionary) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [exportKey](#export-key) | None | [JsonWebKey](https://www.w3.org/TR/WebCryptoAPI/#JsonWebKey-dictionary) or [BufferSource](https://heycam.github.io/webidl/#common-BufferSource) |
| [sign](#sign) | [EcdsaParams](https://www.w3.org/TR/WebCryptoAPI/#EcdsaParams-dictionary) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [verify](#verify) | [EcdsaParams](https://www.w3.org/TR/WebCryptoAPI/#EcdsaParams-dictionary) | Boolean |

### Generate key
```js
const keys = await crypto.subtle.generateKey(
  {
    name: "ECDSA",
    namedCurve: "P-256", // P-256, P-384, or P-521
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
    crv: "P-521",
    ext: true,
    key_ops: ["verify"],
    kty: "EC",
    x: "Adqn62IVQX8LIauAXrUtxH05DHlRygKcsP9qWAnd9tfJvpaG7bzIs16WMEUe1V-f4AxbQJceU4xCP8dJppK_fzdC",
    y: "AEo3s1eExCOvpuBtBWnWlr7TuFhq_fMzqX9eqDHiy8qWl4I_koQtMePodrAc85mVrJAjvsa77Y3Ul3QtIWpXXBqa",
  },
  {
    name: "ECDSA",
    namedCurve: "P-521",
  },
  false,
  ["verify"],
);
```

### Export key
```js
const jwk = await crypto.subtle.exportKey(
  "jwk",
  publicKey,
);
```

### Sign
```js
const signature = await crypto.subtle.sign(
  {
    name: "ECDSA",
    hash: "SHA-256", // SHA-1, SHA-256, SHA-384, or SHA-512
  },
  privateKey, // ECDSA private key
  data,       // BufferSource
);
```

### Verify
```js
const ok = await crypto.subtle.verify(
  {
    name: "ECDSA",
    hash: "SHA-256", // SHA-1, SHA-256, SHA-384, or SHA-512
    hash: "SHA-256", // SHA-1, SHA-256, SHA-384, or SHA-512
  },
  publicKey, // ECDSA public key
  signature, // BufferSource
  data,      // BufferSource
);
```