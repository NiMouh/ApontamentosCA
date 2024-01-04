# Aula 8

## Cartão do Cidadão

## Diagrama de CAPI

```mermaid
graph LR

A[Aplicação] --> B[Lib PKCS#11]
B --> C[Cryto Token]
A --> D[CAPI]
D --> E[Crypto Service Provider]
E --> B
E --> C
```