# Aula 1 - Criptografia Moderna

### Cifras
Estas são algumas das propriedades que uma cifra segura tem:
 - **Difusão**: Se uma cifra for de qualidade, quaisquer propriedades estatísticas do texto limpo estão completamente **difusas** (sem qualquer tipo de correlação) por todo o criptograma.
 - **Confusão**: Se uma cifra for de qualidade, não são perceptiveis quaisquer relações entre um bloco de texto-limpo, a chave de cifra e o bloco de criptograma.
 - **Não maneável**: Se uma cifra for de qualidade, não é possível **manejar** (alterar) o texto cifrado sem que o texto limpo seja alterado. Esta propriedade é mantida por um código de **autenticação de mensagem**.
 - **Semântica**: Se uma cifra for de qualidade, o adversário não deverá ser capaz de obter informações sobre o texto limpo a partir do texto cifrado.
 - **Não determinística**: Esta propriedade permite que a cifra produza saídas diferentes para o mesmo texto limpo e chave de cifra.

Nota: Todas estas propriedades acima têm que ser balenceadas com a **usabilidade** da cifra.

#### Cifras de chave simétrica
São algoritmos que utilizam a **mesma chave** para **cifrar** e **decifrar** (simétrica). Cifras de chave simétrica têm **dois** algoritmos (para cifrar e para decifrar).

Para **cifrar**:
 - Input: Texto-limpo, Chave de cifra, Algoritmo de geração de chaves (pseudo-aleatório)
 - Output: Texto-cifrado

Para **decifrar**:
 - Input: Texto-cifrado, Chave de cifra
 - Output: Texto-limpo

#### Cifras de chave pública
São algoritmos que utilizam **chaves diferentes** para **cifrar** e **decifrar** (diferente da chave simétrica). Cifras de chave pública têm **três** algoritmos (para cifrar, para decifrar e para gerar chaves).

Para **par de chaves**:
 - Input: Tamanho da chave
 - Output: Par de chaves

Para **cifrar**:
 - Input: Texto-limpo, Chave pública
 - Output: Texto-cifrado

Para **decifrar**:
 - Input: Texto-cifrado, Chave secreta
 - Output: Texto-limpo

Nota: **Não** são recomendas para cifrar **grandes quantidades** de dados (bulk encryption), pois são mais lentas que as cifras de chave simétrica.

#### Cifras de chave simétrica continuas
As cifras de chave simétrica continuas usam um algoritmo que a partir de uma chave com tamanho **fixo** e **comportável**, geral uma sequência tão grande quanto necessária para cifrar um ficheiro. Este tipo de cifra tem como defeito a sua **maneabilidade** (facilidade da alteração do texto cifrado). Se cifrarmos um ficheiro já antes cifrado com a **mesma chave**, iremos obter o texto-limpo.

Nota: Estas cifras são usadas em situações em que o canal de comunicação não permite a **alteração** da mensagem cifrada ou quando a perda de parte da mensagem na transmissão não é um problema de grande dimensão (ex: streaming de vídeo).

#### Cifras de chave simétrica de bloco
O algoritmo para **decifrar** é diferente que o de **cifrar**. A diferença entre as cifras de chave simétrica de bloco e as cifras de chave simétrica continua é que as cifras de chave simétrica de bloco geram uma cifra de tamanho fixo (bloco) e não uma cifra de tamanho variável. Caso a cifra de chave simétrica de bloco seja alterada (maneada), o texto cifrado perderá toda a sua integridade.

Nota: Este tipo de cifra é mais segura, dependendo de como são usadas, quando o canal de comunicação permite a **alteração** da mensagem cifrada, sem que a mensagem perca a sua **integridade**. Cifras de chave pública são sempre por blocos, não existem cifras de chave pública contínuas.

### Tipos de ataques
Alguns exemplos dos tipos de ataques mais comuns:

#### Ataque força bruta (Brute force)
É uma técnica de ataque que consiste em tentar todas as possíveis chaves de cifra até encontrar a chave correta.

#### Ataque com conhecimento de texto-limpo original (Known plaintext attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra a partir de um texto-limpo original e do texto-cifrado correspondente.

#### Ataque com o conhecimento apenas do criptograma (Ciphertext-only attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra ou o texto-limpo, a partir de um texto-cifrado.

#### Ataque com o texto-limpo original escolhido pelo atacante (Chosen plaintext attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra ou o texto-limpo a partir de um texto-limpo original escolhido pelo atacante.

#### Ataque com o texto-limpo original escolhido pelo ataque adaptativo (Adaptative Chosen plaintext attack)
Semelhante ao anterior, porém o atacante obtém exemplos de texto cifrado antes e depois de começar o ataque.

#### Ataques com criptogramas escolhidos pelo atacante (Chosen ciphertext attack)
É uma técnica de ataque que consiste em tentar descobrir a chave de cifra ou o texto-limpo a partir de um conjunto de textos-cifrados escolhidos pelo atacante, diferentes do texto que queremos cifrar.

Nota: *Brute-force* não é uma técnica de criptanálise.

#### Ataque do homem no meio
Este tipo de ataque é feito quando a **Pessoa A (Alice)** e a **Pessoa B (Bob)** estão sujeitos a um ataque por uma **Pessoa C (Claire)** que se encontra no meio da comunicação entre as duas pessoas. Existem dois tipos de ataque do homem no meio:
- **Ataque do homem no meio passivo**: A **Pessoa C (Claire)** não consegue alterar (apenas vê) a mensagem cifrada (também chamada de **Pessoa E (Eve)**).
- **Ataque do homem no meio ativo**: A **Pessoa C (Claire)** consegue alterar e ver a mensagem cifrada.

### Funções de Hash
Funções que dado um input de qualquer tamanho, produzem um output de um tamanho fixo. Estas funções são **one-way** (não há forma de obter o input a partir do output). 

Nota: São **resistentes a colisões**, ou seja, é difícil encontrar dois inputs diferentes que produzam o mesmo output (em tempo útil). Também têm como propriedade a **resistência a previsão de uma pré-imagem** e a **resistência a previsão de uma segunda pré-imagem**, ou seja, é difícil encontrar um input que produza um output conhecido.

Continua na [Aula 2](Aula2.md)