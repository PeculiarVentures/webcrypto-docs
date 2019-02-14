# CryptoX509Certificate

## Interfaces

This specification provides interface for X509 certificate. See [RFC 5280](https://tools.ietf.org/html/rfc5280) for more information about X509 certificate structure.

### CryptoX509Certificate interface
```ts
interface CryptoX509Certificate extends CryptoCertificate {
  type: "x509";
  notBefore: Date;
  notAfter: Date;
  serialNumber: string;
  issuerName: string;
  subjectName: string;
}
```

## Interface data types

### type

Type of [CryptoCertificate](CRYPTO_CERT.md#CryptoCertificate-interface). The recognized type value is `x509`.

### notBefore

The date on which the certificate validity period begins.

### notAfter

The date on which the certificate validity period ends.

### serialNumber

The serial number is a hex string which is a positive integer assigned by the CA to each certificate.

### issuerName

The issuer field identifies the entity that has signed and issued the certificate. It's [RFC 4514](https://tools.ietf.org/html/rfc4514.html) compliant string.

### subjectName

The subject field identifies the entity associated with the public key stored in the public key field. It's [RFC 4514](https://tools.ietf.org/html/rfc4514.html) compliant string.