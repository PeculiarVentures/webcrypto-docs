# ECDH

[W3 specification](https://www.w3.org/TR/WebCryptoAPI/#ecdh)

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [generateKey](#generate-key) | [EcKeyGenParams](https://www.w3.org/TR/WebCryptoAPI/#EcKeyGenParams-dictionary) | [CryptoKeyPair](https://www.w3.org/TR/WebCryptoAPI/#keypair) |
| [importKey](#import-key) | [EcKeyImportParams](https://www.w3.org/TR/WebCryptoAPI/#EcKeyImportParams-dictionary) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |
| [exportKey](#export-key) | None | [JsonWebKey](https://www.w3.org/TR/WebCryptoAPI/#JsonWebKey-dictionary) or [BufferSource](https://heycam.github.io/webidl/#common-BufferSource) |
| [deriveBits](#derive-bits) | [EcdhKeyDeriveParams](https://www.w3.org/TR/WebCryptoAPI/#dh-EcdhKeyDeriveParams) | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |
| [deriveKey](#derive-key) | [EcdhKeyDeriveParams](https://www.w3.org/TR/WebCryptoAPI/#dh-EcdhKeyDeriveParams) | [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) |

### Generate key
```js
const keys = await crypto.subtle.generateKey(
  {
    name: "ECDH",
    namedCurve: "P-256", // P-256, P-384, or P-521
  },
  false,
  ["deriveKey", "deriveBits"],
);
```

### Import key
```js
const publicKey = await crypto.subtle.importKey(
  "jwk",
  {
    crv: "P-521",
    ext: true,
    key_ops: [],
    kty: "EC",
    x: "Adqn62IVQX8LIauAXrUtxH05DHlRygKcsP9qWAnd9tfJvpaG7bzIs16WMEUe1V-f4AxbQJceU4xCP8dJppK_fzdC",
    y: "AEo3s1eExCOvpuBtBWnWlr7TuFhq_fMzqX9eqDHiy8qWl4I_koQtMePodrAc85mVrJAjvsa77Y3Ul3QtIWpXXBqa",
  },
  {
    name: "ECDH",
    namedCurve: "P-521",
  },
  false,
  [],
);
```

### Export key
```js
const jwk = await crypto.subtle.exportKey(
  "jwk",
  publicKey,
);
```

### Derive bits
```js
const derivedBits = await crypto.subtle.deriveBits(
  {
    name: "ECDH",
    public: publicKey,
  },
  privateKey,
  128,
);
```

### Derive key
```js
const derivedKey = await crypto.subtle.deriveKey(
  {
    name: "ECDH",
    public: publicKey,
  },
  privateKey,
  {
    name: "AES-CBC",
    length: 128,
  },
  false,
  ["encrypt", "decrypt"],
);
```