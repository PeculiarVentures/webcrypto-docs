# CryptoCertificateRequest

## Interfaces

This specification provides interface for X509 certificate request. See [RFC 2986](https://tools.ietf.org/html/rfc2986) for more information about X509 certificate request structure.

### CryptoCertificateRequest interface
```ts
interface CryptoCertificateRequest extends CryptoCertificate {
  type: "request";
  subjectName: string;
}
```

## Interface data types

### type

Type of [CryptoCertificate](CRYPTO_CERT.md#CryptoCertificate-interface). The recognized type value is `request`.

### subjectName

The subject field identifies the entity associated with the public key stored in the public key field. It's [RFC 4514](https://tools.ietf.org/html/rfc4514.html) compliant string.
