# Aula 3 - Modos de Cifra

## Cifra AES

### *Eletronic Code Book* (ECB)
O **ECB** é um modo de operação de cifra que consiste em cifrar cada bloco de dados de forma independente. Ou seja, o bloco de dados é cifrado com a mesma chave, mas o resultado é diferente (caso os blocos não sejam iguais) para cada bloco de dados.

Nota: **Não é recomendado** o uso para mensagens acima de 12 bytes não pseudo-aleatórios.

Exemplo para **cifrar**:
| Texto     | Bloco 1       | Bloco 2       | Bloco 3       |
| --------- | ------------- | ------------- | ------------- |
| Limpo     | aaaaaaa       | bbbbbbb       | aaaaaaa       |
| Algoritmo | AES-e(k,m[0]) | AES-e(k,m[1]) | AES-e(k,m[2]) |
| Cifrado   | 934fafa       | 9f9f9f9       | 934fafa       |

Exemplo para **decifrar**:
| Texto     | Bloco 1       | Bloco 2       | Bloco 3       |
| --------- | ------------- | ------------- | ------------- |
| Cifrado   | 934fafa       | 9f9f9f9       | 934fafa       |
| Algoritmo | AES-d(k,c[0]) | AES-d(k,c[1]) | AES-d(k,c[2]) |
| Limpo     | aaaaaaa       | bbbbbbb       | aaaaaaa       |

**Vantagens** deste modo:
 - Permite o acesso aleatório a dados cifrados.
 - Permite processamento paralelo da informação.
 - Não tem problemas de propagação de erros entre blocos.
**Desvantagens** deste modo:
 - Não é seguro a ataques COA (*Cipher-Only attack*) e ataques por *code book* (compilação de pares texto limpo/criptograma).
 - Não permite pré-processamento.
 - O último bloco necessita sempre de preenchimento.
 - Erros de sincronização são irrecuperáveis.

### *Cipher Block Chaining* (CBC)
O **CBC** é um modo de operação de cifra que consiste em cifrar cada bloco de dados de forma dependente do bloco anterior. Ou seja, o bloco de dados é cifrado com a mesma chave, mas o resultado é diferente (mesmo os blocos sendo iguais) para cada bloco de dados. Este método evita **alguns** ataques por maninupulação de blocos.

Exemplo para **cifrar**:
 - Recebe um bloco de texto-limpo;
 - Recebe um vetor de inicialização (IV) - gerado aleatóriamente, único para cada mensagem e partilhado entre as duas partes;
 - É feito o XOR entre o bloco de texto-limpo e o IV;
 - O resultado do XOR é cifrado com a chave;
 - O resultado cifrado é enviado para o bloco seguinte e irá ser feito o XOR com o bloco seguinte;
 - Processo repete-se até ao fim da mensagem;

Exemplo para **decifrar**:
 - Recebe um bloco de texto-cifrado;
 - Este bloco é decifrado com a chave;
 - É feito o XOR entre o bloco de decifrado e o IV;
 - Esse bloco cifrado é enviado para o bloco seguinte e irá ser feito o XOR com o bloco seguinte após ser decifrado;
 - Processo repete-se até ao fim da mensagem;

**Vantagens** deste modo:
 - É seguro contra ataques CPA (*Chosen-Plaintext Attack*).
 - Os padrões são mascarados pelo XOR e efeito cascata.
 - Textos limpos iguais resultam em criptogramas distintos, inviabilizando ataques por *code book*.
 - Permite o acesso aleatório a dados cifrados.
 - Permite processamento paralelo da informação cifrada.
**Desvantagens** deste modo:
 - Ataques por manipulação do IV podem não ser detetáveis.
 - Não permite processamento paralelo da informação na cifragem. 
 - Erros de perda de bits são irrecuperáveis e um erro num bit afeta o bloco de texto limpo correspondente e o seguinte (cascata).

#### *Padding* (Preenchimento)
O **padding** é uma técnica de preenchimento de dados que consiste em adicionar um número de bytes ao final de um bloco de dados, de forma a que o tamanho do bloco de dados seja múltiplo do tamanho do bloco de dados da cifra.

Nota: O último bloco tem sempre *padding*, mesmo que o bloco da mensagem seja múltiplo do tamanho do bloco da cifra é acrescentado um bloco de *padding*.

### Output Feeback Mode (OFM)
O **OFM**  é um modo de operação de cifra que consiste...

Exemplo a **cifrar**:
- Recebe um bloco de texto-limpo;
- Recebe um vetor de inicialização (IV) - gerado aleatóriamente, único para cada mensagem e partilhado entre as duas partes;
- É cifrado o IV **anterior** com a chave;
- É feito o XOR entre o bloco de texto-limpo e o resultado do IV cifrado;
- Processo repete-se, usando o IV do bloco anterior, até ao fim da mensagem;

### Ciphertext Feedback Mode (CFM)
O **CFM**  é um modo de operação de cifra que consiste...

Exemplo a **cifrar**:
 - Recebe um bloco de texto-limpo;
 - Recebe um vetor de inicialização (IV);
 - É cifrado o IV **anterior** com a chave (neste caso o IV é obtido através da operação xOr entre o IV cifrado e o bloco de texto-limpo);
 - Processo repete-se, usando o IV do bloco anterior, até ao fim da mensagem;

Exemplo a **decifrar**:
 - Recebe um bloco de texto-cifrado;
 - Recebe um vetor de inicialização (IV);
 - É decifrado usando o IV cifrado na primeira iteração;
 - As restantes iterações usa como IV o bloco de texto-cifrado anterior e é feito o xOr com o bloco de texto-cifrado atual;
 - Processo repete-se, até ao fim da mensagem;

### *Randomized Couter Mode* (CTR)
O **CTR** é um modo de operação de cifra que consiste em cifrar através de uma chave de cifra de forma simétrica e continua a partir de uma cifra de blocos.

Exemplo para **cifrar**:
 - Recebe um bloco de texto-limpo;
 - Cria um contador (CTR) - do mesmo tamanho que o bloco, gerado aleatóriamente através da chave de cifra;
 - Faz o XOR entre o bloco de texto-limpo e o contador;

Exemplo para **decifrar**:
 - Recebe um bloco de texto-cifrado;
 - Cria um contador (CTR) - do mesmo tamanho que o bloco, gerado aleatóriamente através da chave de cifra;
 - Faz o XOR entre o bloco de texto-cifrado e o contador;

**Vantagens** deste modo:
 - É seguro contra ataques CPA (*Chosen-Plaintext Attack*).
 - Os padrões do texto-limpo são mascarados por imitar o processo de uma cifra contínua.
 - Textos-limpos iguais resultam em criptogramas distintos, inviabilizando ataques por *code book*.
 - Permite o acesso aleatório a dados cifrados.
 - Permite o processamento paralelo da informação.
**Desvantagens** deste modo:
 - Sendo ela uma cifra de chave simétrica contínua, ela fica **maneável**.
 - Erros de perda bits são irrecuperáveis.