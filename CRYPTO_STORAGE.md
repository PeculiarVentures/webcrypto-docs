# CryptoStorage

> WARNING: Is not W3 WebCrypto specification

## Interfaces

### CryptoStorage interface

Base interface for all crypto storages

Used by:
 - [CryptoKeyStorage](KEY_STORAGE.md#CryptoKeyStorage-interface)
 - [CryptoCertificateStorage](CERT_STORAGE.md#CryptoCertificateStorage-interface)

```ts
/**
 * Base generic interface for crypto storages
 */
interface CryptoStorage<T> {
  /**
   * Returns list of indexes from storage
   */
  keys(): Promise<string[]>;

  /**
   * Returns index of item in storage
   * @param item Crypto item
   * @returns Index of item in storage otherwise null
   */
  indexOf(item: T): Promise<string | null>;

  /**
   * Add crypto item to storage and returns it's index
   */
  setItem(item: T): Promise<string>;

  /**
   * Returns crypto item from storage by index
   * @param index index of crypto item
   * @returns Crypto item
   * @throws Throws Error when cannot find crypto item in storage
   */
  getItem(index: string): Promise<T>;

  /**
   * Returns `true` if item is in storage otherwise `false`
   * @param item Crypto item
   */
  hasItem(item: T): Promise<boolean>;

  /**
   * Removes all items from storage
   */
  clear(): Promise<void>;

  /**
   * Removes crypto item from storage by index
   * @param index Index of crypto storage
   */
  removeItem(index: string): Promise<void>;

}
```

### CryptoStorages interface

Interface for Crypto extending. Adds properties for storages getting.

```ts
interface CryptoStorages {
  keyStorage: CryptoKeyStorage;
  certStorage: CryptoCertificateStorage;
}
```

## Operations

### Keys getting
```ts
const indexes = await storage.keys();
// ["0001", "0002", ...]
```

### Index of
```ts
const index = await storage.indexOf(key);
// "0001"
```

### Set item
```ts
const index = await storage.setItem(cert);
// "0001"
```

### Get item
```ts
const cert = await storage.getItem("0001");
```

### Remove item
```ts
await storage.removeItem("0001");
```