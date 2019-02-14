# CryptoCertStorage

Crypto storage for `x509` certificate and certificate `request` keeping. Extends [CryptoStorage](CRYPTO_STORAGE.md#CryptoStorage-interface).

## Types

### CryptoCertificateFormat type

Specifies a serialization format for a certificate. The recognized key format values are:

- "raw"
  An unformatted sequence of bytes. Intended for secret keys.

- "pem"
  The PEM encoding of the certificate. See [RFC 7468](https://tools.ietf.org/html/rfc7468)

```ts
type CryptoCertificateFormat = "raw" | "pem";
```

### ImportAlgorithms type

```ts
type ImportAlgorithms = Algorithm | RsaHashedImportParams | EcKeyImportParams;
```

## Interfaces

### CryptoCertificateStorage interface
```ts
interface CryptoCertificateStorage extends CryptoStorage<CryptoCertificate> {

  getItem(index: string): Promise<CryptoCertificate>;
  getItem(index: string, algorithm: ImportAlgorithms, keyUsages: KeyUsage[]): Promise<CryptoCertificate>;

  exportCert(format: CryptoCertificateFormat, item: CryptoCertificate): Promise<ArrayBuffer | string>;
  exportCert(format: "raw", item: CryptoCertificate): Promise<ArrayBuffer>;
  exportCert(format: "pem", item: CryptoCertificate): Promise<string>;

  importCert(format: CryptoCertificateFormat, data: BufferSource | string, algorithm: ImportAlgorithms, keyUsages: KeyUsage[]): Promise<CryptoCertificate>;
  importCert(format: "raw", data: BufferSource, algorithm: ImportAlgorithms, keyUsages: KeyUsage[]): Promise<CryptoCertificate>;
  importCert(format: "pem", data: string, algorithm: ImportAlgorithms, keyUsages: KeyUsage[]): Promise<CryptoCertificate>;
}
```

## Operations

### Get item

Returns [CryptoCertificate](CRYPTO_CERT.md#CryptoCertificate-interface) from the storage.

Request getting with default params
```ts
const request = await crypto.certStorage.getItem("0001");
```

Certificate getting with import params
```ts
const cert = await crypto.certStorage.getItem("0001", {name: "RSASSA-PKCS1-v1_5", hash: "SHA-256"}, ["verify"]);
```

### Export certificate

Exports certificate to needed format.

```ts
const pem = await crypto.certStorage.exportCert("pem", x509);
// -----BEGIN CERTIFICATE-----
// MIICLDCCAdKgAwIBAgIBADAKBggqhkjOPQQDAjB9MQswCQYDVQQGEwJCRTEPMA0G
// A1UEChMGR251VExTMSUwIwYDVQQLExxHbnVUTFMgY2VydGlmaWNhdGUgYXV0aG9y
// ...
// -----END CERTIFICATE-----
```

### Import certificate

Imports certificate.
```ts
const pem = "-----BEGIN CERTIFICATE-----\n" +
"MIICLDCCAdKgAwIBAgIBADAKBggqhkjOPQQDAjB9MQswCQYDVQQGEwJCRTEPMA0G\n" +
"A1UEChMGR251VExTMSUwIwYDVQQLExxHbnVUTFMgY2VydGlmaWNhdGUgYXV0aG9y\n" +
"...\n" +
"-----END CERTIFICATE-----\n";
const x509 = await crypto.certStorage.importCert("pem", pem, {name: "RSASSA-PKCS1-v1_5", hash: "SHA-256"}, ["verify"]);
```