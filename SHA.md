# SHA

[W3 specification](https://www.w3.org/TR/WebCryptoAPI/#sha)

## Operations

| Operation | Parameters | Result |
|-----------|------------|--------|
| [digest](#digest) | None | [ArrayBuffer](https://www.w3.org/TR/WebCryptoAPI/#dfn-ArrayBuffer) |

### Digest
```js
const hash = await crypto.subtle.digest(
  "SHA-256", // SHA-1, SHA-256, SHA-384, or SHA-512
  data,      // BufferSource
);
```