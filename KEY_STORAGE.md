# CryptoKeyStorage

Crypto storage for `private`, `public` and `secret` keys keeping. Extends [CryptoStorage](CRYPTO_STORAGE.md#CryptoStorage-interface).

## Interfaces

### CryptoKeyStorage interface
```ts
interface CryptoKeyStorage extends CryptoStorage<CryptoKey> {

  getItem(index: string): Promise<CryptoKey>;
  getItem(index: string, algorithm: ImportAlgorithms, extractable: boolean, keyUsages: KeyUsage[]): Promise<CryptoKey>;

}
```

## Operations

### Get item
Returns [CryptoKey](https://www.w3.org/TR/WebCryptoAPI/#dfn-CryptoKey) from key storage.

Key getting with default params
```ts
const key = await crypto.keyStorage.getItem("0001");
```

Key getting with import params
```ts
const key = await crypto.keyStorage.getItem("0001", {name: "RSASSA-PKCS1-v1_5", hash: "SHA-256"}, false, ["sign"]);
```
