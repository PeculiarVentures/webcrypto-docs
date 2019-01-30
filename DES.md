# DES

## Mechanisms

- [DES-CBC](DES_CBC.md)
- [DES-EDE3-CBC](DES_EDE3_CBC.md)

## Interfaces

### DesKeyAlgorithm interface
```ts
interface DesKeyAlgorithm extends KeyAlgorithm {
    length: number;
}
```

### DesKeyGenParams interface
```ts
interface DesKeyGenParams extends Algorithm {
    length: number;
}
```

### DesDerivedKeyParams interface
```ts
interface DesDerivedKeyParams extends Algorithm {
    length: number;
}
```
