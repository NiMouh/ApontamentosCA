# Aula 0 - Criptografia Clássica

## Objetivos de criptanálise
- Descobrir o texto original;
- Descobrir a chave;
- Descobrir o algoritmo.

Nota: Normalmente os algoritmos não são secretos, mas há exceções.

## Conceitos base
Objetivo inicial da criptografia: Garantir que a mensagem da pessoa A chegue a pessoa B sem que a pessoa C consiga ler.

1. **Texto-limpo**: mensagem original.
2. **Cifra ou Esquema Criptográfico**: algoritmo que transforma o texto-limpo em texto-cifrado e vice-versa (por norma são dois algoritmos diferentes).
3. **Criptograma**: texto-cifrado.
4. **Chave de cifra**: conjunto de dados que permite a cifrar e/ou decifrar do texto-limpo.
5. **Sistema criptográfico**: conjunto de cifra, chave de cifra, conjunto de decifra e chave de decifra.
6. **Modelo de ataque**: classificação para um possível ataque ao sistema criptográfico.
7. **Ataque**: Tentativa de quebra dos objetivos da técnica criptográfica.
8. **Criptanálise**: Conjunto de técnicas que visam a quebra de sistemas criptográficos. Consistem em decifrar sem saber a chave ou tendo a chave.

## Cifras clássicas
São algoritmos que utilizam a mesma chave para cifrar e decifrar. Cifras clássicas têm **um** algoritmo (para cifrar e para decifrar).

### Cifra de substituição Mono alfabética
É uma cifra de substituição, em que cada letra do texto original é substituída por outra letra do alfabeto.

#### Cifra de César
É uma cifra de substituição, em que cada letra do texto original é substituída por outra letra que se encontra um número fixo de posições à sua frente no alfabeto.

Ou seja: C(K, M) = Mi + K mod 26, onde 'K' é a chave, 'Mi' é uma letra da mensagem no índice 'i' e 26 é o número de letras do alfabeto.

### Cifra de substituição Poli alfabética

#### Cifra de Vigenère
É uma cifra de substituição polialfabética, em que cada letra do texto original é substituída por outra letra que se encontra um número fixo de posições à sua frente no alfabeto, mas a chave é uma palavra. 

Esta cifra é mais difusa que a de César, pois ao utilizar uma palavra como chave, a mesma letra da mensagem original pode ser cifrada de várias formas diferentes, alterando assim a estatística das letras.

Ou seja: V(K,M) = Mi + Ki mod 26, onde 'K' é a chave, 'Mi' é uma letra da mensagem no índice 'i' e 26 é o número de letras do alfabeto.

#### Máquinas de Rotores
São máquinas que utilizam rotores para cifrar e decifrar mensagens. Estes rotores são discos com 26 posições, onde cada posição corresponde a uma letra do alfabeto. Cada rotor tem uma posição inicial, que é a chave de cifragem.

A cada letra que é cifrada, o rotor avança uma posição, alterando a cifra. Quando o rotor dá uma volta completa, o rotor à sua direita avança uma posição. Quando o rotor do meio dá uma volta completa, o rotor à sua esquerda avança uma posição. Assim que o rotor da direita dá uma volta completa, o rotor do meio avança uma posição.

Exemplos de máquinas de rotores: Enigma, SIGABA, Purple, Typex, etc.

#### Máquinas de Rotores vs Cifra de Vigenère
Em comparação com a cifra de Vigenère, a máquina de rotores oferece vários aprimoramentos:

**Complexidade Superior**: A cifra de rotores é mais complexa e difícil de quebrar do que a cifra de Vigenère devido à substituição polialfabética, ao movimento dos rotores e aos refletores.

**Segurança Dinâmica**: A cifra de Vigenère usa uma única chave repetida, o que torna a quebra da cifra mais fácil se o tamanho da chave for descoberto. As máquinas de rotores usam uma chave inicial que muda constantemente, tornando a quebra mais desafiadora.

**Resistência à Análise de Frequência**: A cifra de Vigenère ainda é suscetível à análise de frequência, enquanto a cifra de rotores torna essa técnica de quebra menos eficaz devido à constante mudança nas substituições.


## Cifra segura a nível teórico vs Cifra segura a nível computacional

- Segurança da Teoria da Informação (Information-Theoretic Security):
  - O espaço de todas as mensagens possíveis
  - O espaço de todos os textos cifrados possíveis
  - O espaço de todas as chaves possíveis
  - A cifra não pode ser quebrada, mesmo que o adversário tenha poder computacional infinito
  - Segurança perfeita, um conceito onde a criptografia é absolutamente invulnerável. As suas características são a indistinguibilidade, onde a mensagem cifrada é indistinguível de uma mensagem aleatória, a chave aleatória e única para cada mensagem e a chave é tão longa (ou mais) quanto a mensagem.

### Cifra de Vernam (ou cifra de chave única)
Foi o primeiro exemplo de uma cifra segura (contra Cipher-only Attacks ou COA). 

Funciona da seguinte forma:
 - É obtido o texto limpo e a chave, ambos em bits.
 - Para cifrar E(k,m) = k xOR m
 - Para decifrar D(k,c) = k xOR c

Nota: Cada chave deve ser usada apenas uma vez e escolhida aleatoriamente para cada texto-limpo a cifrar.

É de notar que esta cifra tem **limitação**, pois a chave tem de ser **tão grande** quanto o **texto a cifrar** e usadas **apenas uma vez**. Algo que as cifras continuas convencionais **superam**, pois as mesmas permitem **chaves mais curtas** e uma **reutilização segura das chaves**.


Continua na [Aula 1](Aula1.md)