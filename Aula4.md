# Aula 4 - Hashes (Resumos Criptográficos)

## Hashes
Funções que dado um input de qualquer tamanho, produzem um output de um **tamanho fixo**. 
 - Estas funções são **one-way** (não há forma de obter o input a partir do output). 
 - São **resistentes a colisões**, ou seja, é difícil encontrar dois inputs diferentes que produzam o mesmo output (em tempo útil). 
 - São **resistentes a previsão de uma pré-imagem** e a **resistência a previsão de uma segunda pré-imagem**, ou seja, é difícil encontrar um input que produza um output conhecido.

## Rainbow Tables
São tabelas que contêm **pares de valores** (input, output) de uma função de hash. Estas tabelas são usadas para encontrar o input a partir do output, mas para isso é necessário que o output esteja na tabela.

## Message Authentication Code (MAC)
Tem como propósito garantir que uma determinada mensagem não foi alterada e que foi enviada por uma determinada entidade (autenticidade).

Há várias formas de construir um MAC, algumas delas são:
- **HMAC** (Hash-based Message Authentication Code): este MAC tem dois algoritmos, um para construção e outro para verificação e recebe dois inputs, um é a chave e o outro é a mensagem;

As **três formas** possíveis de combinar os dois mecanismos são:
 - *MAC and Encrypt*: Processo onde é calculado o MAC **através da mensagem** e depois é cifrada a mensagem concatenando o com o MAC (e.g. SSH);
 - *MAC then Encrypt*: Processo onde é calculado o MAC **através da mensagem** e depois é cifrada a mensagem concatenando o com o MAC (e.g. TLS);
 - *Encrypt then MAC*: Processo onde é calculado o MAC **através da mensagem cifrada** (e.g. IPsec).

**Nota:** A forma considerada **correta** é a *encrypt then MAC*, e devem ser usadas **chaves diferentes** para o MAC e para a cifragrem.

Continua na [Aula 5](Aula5.md)