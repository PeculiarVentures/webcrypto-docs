# DES

## Mechanisms

- [DES-CBC](DES-CBC.md)
- [DES-EDE3-CBC](DES-EDE3-CBC.md)

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
