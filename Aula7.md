# Aula 7

## Assinatura Digital

### Esquema de assinatura digital
Recorrendo a chaves públicas (nomeadamente RSA), são usados **três** algoritmos:

- Algoritmo para gerar chaves: É gerado um par de chaves, uma pública e outra privada;
  - (pub, priv) = RSA(512);
```mermaid
graph LR

A[Gerar chaves] --> B[RSA-512]
B --> C[Chave pública]
B --> D[Chave privada]
```
- Algoritmo para gerar assinatura: É calculado o Hash da mensagem e decifrado com a chave privada;
  - Texto Assinado = RSA(priv, SHA256(Mensagem));
```mermaid
graph LR

A[Gerar assinatura] --> B[Texto a assinar]
A --> C[Chave privada]
B --> D[SHA256]
D --> E[Texto resumido]
E --> F[Texto cifrado]
C --> F
```

- Algoritmo para verificar assinatura: É calculado o Hash da mensagem e decifrado com a chave pública;
  - Verifica = RSA(pub, SHA256(Mensagem)) == Texto Assinado;
```mermaid
graph LR

A[Verificar assinatura] --> B[Chave pública]
A --> C[Texto assinado]
B --> D[RSA-512]
C --> D
D --> E[Verdadeiro ou falso]
```

### Propriedades principais de uma assinatura digital
Estas são as **cinco principais propriedades** de uma assinatura digital:
  - Autenticidade: A mensagem foi assinada pelo dono da chave privada;
  - Autenticação da origem de informação: A assinatura digital é única para cada mensagem;
  - Integridade dos dados: Qualquer alteração na mensagem invalida a assinatura;
  - Dificuldade de falsificação: É difícil falsificar uma assinatura digital;
  - Garantia de não repúdio: O dono da chave privada não pode negar que assinou a mensagem.

### OAEP (Optimal Asymmetric Encryption Padding)

### Proof of Existence (POE)

