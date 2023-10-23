# Aula 5

## RSA
Um cifra de chave pública que precisa de:

- Gerador de chaves: 
  1. Primeiramente geramos dois números primos extremamente grandes, X e Y.
  2. Calcula-mos Z que é o produto de X e Y.
  3. Calcular números phi de Z, que é o mínimo múltiplo comum de X-1 e Y-1.
  4. Finalmente, arranjamos dois números que multiplicados preencham esta condição: ((E * D) mod phi(Z)) = 1. 
  5. O número (Z,E) é a chave pública e o (Z,D) é a chave privada;

- Um algoritmo para cifrar: Para cifrar fazemos a seguinte operação: C = M^E mod Z, sendo o M a mensagem a cifrar e C a mensagem cifrada;
- Um algoritmo para decifrar: Para decifrar fazemos a seguinte operação: M = C^D mod Z, sendo o C a mensagem cifrada e M a mensagem decifrada.

A segurança desta cifra basea-se no problema do logaritmo discreto e no problema da fatorização de números primos.

Nota: Normalmente não se utiliza o **Text Book RSA** (apenas cifrar o conteúdo pretendido). Invés disso é acrescentado um padding aleatório para aumentar a segurança (OAEP ou Optimal Assimetric Encription Padding).


## Criptografia de chave pública
A criptografia de chave pública moderna é baseada na teoria dos números e em problemas difíceis de resolver. Alguns exemplos são os protocolos de acordos de chaves, assinaturas digitais e cifras de chave pública.

Exemplos de problemas intratáveis com mais relevância:
- O problema do logaritmo discreto;
- O problema da fatorização de números compostos em números primos;

### Problema do logaritmo discreto
Consiste em encontrar o valor de um número inteiro (exponencial) que é utilizado para cifrar uma mensagem, conhecido o valor da base e o resultado da exponenciação, num grupo finito. Esse problema é considerado difícil de resolver computacionalmente quando se trabalha com números grandes, tornando-o fundamental para garantir a segurança da criptografia de chave pública.

Nota: A definição mais geral do problema recorre apenas a grupos cíclicos, aplicando-se, por isso a outros grupos diferentes de números primos. O melhor algoritmo conhecido para resolver o problema do logaritmo discreto é conhecido por *general number field sieve*, determinando o tamanho que o número tem de ter para que o problema seja considerado seguro.

### Problema da fatorização de números compostos
Consiste em decompor um número composto nos seus fatores primos. Por exemplo, se tivermos o número 15, ele pode ser decomposto em 3 e 5, que são números primos. O problema da fatorização torna-se difícil à medida que os números tornam-se maiores, e isso é utilizado em esquemas de criptografia de chave pública baseados em algoritmos como o RSA. A segurança desses esquemas depende do fato de que a fatorização de números grandes em fatores primos é computacionalmente difícil de ser realizada em tempo razoável, tornando a criptografia de chave pública segura contra ataques de criptoanálise.

## Assinatura Digital
Os esquemas de assinatura digital atuais são normalmente construídos usando criptografia de chave pública. Estas são algumas das propriedades:

- Autenticidade da Informação
- Integridade dos Dados
- Garantia de Não Repúdio
- Autenticação da Origem da Informação
- Dificuldade de Falsificação 

Repare-se que, na verdade, enquanto que a assinatura digital pode garantir todas as propriedades anteriores, o mesmo não costuma acontecer para as assinaturas manuscritas.

## Protocolos de acordos de chaves
Neste capítulo é apresentado formas de trocar ou estabelecer um segredo entre duas entidades sem haver nada secreto acordado à partida. Essa troca é realizada por uma comunicação segura, aonde as partes enviam mensagens encriptadas uma para a outra e usam técnicas de criptografia e matemática para garantir que apenas elas possam obter a chave secreta compartilhada. O objetivo é garantir a segurança e a privacidade das comunicações entre as partes envolvidas.

Nota: Este tipo de protocolo deve ser utilizado em situações de ataque ao homem no meio passivo, onde o atacante não consegue modificar as mensagens que são enviadas entre as partes.

## Protocolo de Diffie-Hellman
Este é um exemplo de um protocolo de acordo de chaves, onde duas partes podem concordar sobre uma chave secreta, mesmo que nunca tenham trocado qualquer informação secreta anteriormente. A sua segurança basea-se no problema do logaritmo discreto.

Funciona da seguinte forma:
1. Alice e Bob escolhem um número primo P e um número G que seja raiz primitiva de P;
2. Alice escolhe um número secreto A e Bob escolhe um número secreto B;
3. Alice calcula G^A mod P e envia para Bob;
4. Bob calcula G^B mod P e envia para Alice;
5. Alice calcula (G^B mod P)^A mod P;
6. Bob calcula (G^A mod P)^B mod P;
7. Ambos obtêm o mesmo resultado, que é a chave secreta partilhada.

## NÃO SAÍ ELGAMAL!! 


Continua na [Aula 6](Aula6.md)