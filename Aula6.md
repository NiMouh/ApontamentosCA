# Aula 6

## Princípios para estruturação uma geração de um par de chaves
Estes são os principios para estruturar a geração de um par de chaves:

- Bons algoritmos de geração aleatórios para produzir os segredos;
- Facilidade sem comprometer a segurança;
- Auto-geração das chaves privadas;

## Distribuição de chaves públicas
As chavés publicas são distribuídas para:
- Todos os remetentes de dados confidênciais;
- Todos os destinatários de assinaturas digitais;

Nota: Na disseminação de chaves públicas, existe um fator de confiança **transitivo** entre as partes envolvidas (se A confia em B e B confia em C, então A confia em C).

## Certificados digitais
É um documento que liga dois conceitos, emitido por uma autoridade de certificação (CA). É um documento que contém a chave pública de um determinado utilizador e que é assinado pela autoridade de certificação. É um documento que é usado para garantir a autenticidade de uma chave pública.

Normalmente é utilizado para:
- Autenticação/Distribuição de chaves públicas;
- Assinaturas digitais;
- Emissão de certificados digitais;

### Exemplo de certificado digital
  - **Nome para quem é passado**;
  - **Quem passou o certificado**;
  - **Data de início do certificado**;
  - **Data de fim do certificado**;
  - **Chave pública**;
  - **Algoritmo de assinatura**;
  - **Assinatura**;

Nota: Os sistemas operativos têm uma lista de certificados digitais de confiança e as respetivas chaves públicas.

### Tipos de certificados digitais
 - X.509v3 standard;
 - Formatos binários (i.e. PKCS #7, PKCS #12, ASN.1);
 - PKCS #6;


## Autoridade de certificação (CA)
É uma entidade que emite e assina os certificados (também os pode revogar).

### Tipos de CA
 - CA de raiz: É a entidade que emite os certificados de outras CA (âncora de confiança);
 - CA intermédia: É a entidade que emite os certificados de utilizadores finais e de outras CA intermédias;

### Raiz de confiança (*trust anchor*)

Normalmente o sistema operativo tem uma lista de certificados de confiança e as respetivas chaves públicas. Sempre que é pedido a um determinado site o seu certificado, ele manda em conjunto os certificados as autoridades certificadores e as acima das mesmas que passaram o certificado (cadeia de certificados). Caso estas autoridades do topo não se encontrem no 'browser' ou no sistema operativo, o certificado não é válido. Estas autoridades do topo são denominadas de raiz de confiança.

OBS: Só depois de estabelecer toda a certificação, é que comunicações podem ser feitas.

## Lista de revogação de certificados (CRL)

É um documento com a lista de certificados que foram revogados. A lista que é atualizada regularmente e que é assinada pela CA. É descarregada pelo sistema operativo e pelo 'browser' e que é usada para verificar se um determinado certificado foi revogado (ou seja, se o certificado foi comprometido ou não válido).

## PEM (*Privacy Enhanced Mail*)
É um formato de certificado digital que é usado para trocar mensagens de correio eletrónico de forma segura.

## PGP (*Pretty Good Privacy*)
É um software de criptografia usado para troca de chaves públicas. Utiliza o **web of trust** para verificar a autenticidade das chaves públicas, ou seja, invés de usar uma autoridade de certificação, usa-se a confiança entre os utilizadores (transitividade).

## *Time Stamping Authority* (TSA)
É uma entidade que emite certificados digitais que são usados para assinar digitalmente documentos e que contém a data e hora em que o documento foi assinado.

Funciona da seguinte forma:
- É calculado o hash do documento;
- O hash do documento é concatenado com o *timestamp*;
- É calculado o hash da concatenação;
- É assinado o hash da concatenação com a chave privada da TSA;
- É devolvido á pessoa que solicitou, a assinatura da TSA com o *timestamp*.

## Infraestrutura de chave pública (PKI)
É um conjunto de politicas e processos que trabalham em prol de emitir, gerir, armazenar, distribuir e revogar certificados digitais.

### Entidades de uma PKI

  - **Autoridade de certificação (CA)**: Entidade que emite e assina os certificados digitais;
  - **Autoridade de registo (RA)**: Entidade que valida os pedidos de certificados digitais;
  - **Repositório de certificados**: Entidade que armazena os certificados digitais;
  - **Lista de revogação de certificados (CRL)**: Entidade que armazena os certificados digitais revogados;
  - **Entidade de validação de certificados (OCSP)**: Entidade que valida os certificados digitais.

### Relações de confiança (*trust relationships*)
A PKI define relações de confiança de duas maneiras diferentes:
- Emitindo certificados para chaves públicas de outras CAs;
- Exigindo a certificação da própria chave pública por uma CA de confiança.

Tipos de relações de confiança:
- **Hierárquica**: A CA de topo emite certificados para outras CA;
- **Cruzada**: A certifica B e B certifica A;
- **Mesh**: grafos complexos de certificação;