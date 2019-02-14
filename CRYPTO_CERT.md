# CryptoCertificate

### CryptoCertificateType type

Type of certificate item. The recognized key type values are `x509` and `request`.

```ts
type CryptoCertificateType = "x509" | "request";
```

## Interfaces

### CryptoCertificate interface
```ts
interface CryptoCertificate {
  type: CryptoCertificateType;
  publicKey: CryptoKey;
}
```

### Used by

- [CryptoX509Certificate](CRYPTO_X509.md#CryptoX509Certificate-interface)
- [CryptoCertificateRequest](CRYPTO_REQUEST.md#CryptoCertificateRequest-interface)
