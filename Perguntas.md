# Frequência 2021

6 - O protocolo Diffie-Helman pode ser implementado usando curvas elípticas.Explique como e indique qual é o problema matemático  que o torna "seguro"?
Resposta: 
  - O protocolo Diffie-Helman pode ser implementado usando curvas elípticas, pois a operação de multiplicação de um ponto por um 
  escalar é computacionalmente difícil de ser invertida;
  Este protocolo é implementado por curvas elípticas da seguinte forma:
  - Cada parte escolhe um número inteiro primos secreto x e calcula y = xG;
  - As partes trocam os valores de y;
  - Cada parte calcula a chave secreta compartilhada como k = xY;
  - Considere que Alice e Bob concordaram em usar a curva elíptica y^2 = x^3 + 2x + 2 sobre o corpo finito F_31;
  - Alice escolhe x = 3 e Bob escolhe x = 5;
  - Qual é a chave secreta compartilhada entre Alice e Bob?
  - Resposta: (3, 29);
  - Explicação: 
    - Alice: y = 3(3, 10) = (3, 29)
    - Bob: y = 5(3, 10) = (3, 1)
    - Alice: k = 5(3, 1) = (3, 29)
    - Bob: k = 3(3, 29) = (3, 29)

  - O resultado será o mesmo para os dois, e esse resultado é a chave secreta compartilhada;
  O problema matemático que o torna "seguro" apresenta se da seguinte forma:
  - E o problema do logaritmo discreto, que consiste em encontrar o valor de x, dado y = g^x mod p, onde g e p são números primos 
  e x é um número inteiro; 
  - Esse problema é computacionalmente difícil de ser resolvido, pois não existe um algoritmo eficiente para resolvê-lo;

Protocolo Diffie-Helman:
Resposta: O protocolo Diffie-Helman permite duas partes estabelecerem uma chave secreta compartilhada, mesmo que nunca tenham trocado 
nenhuma informação previamente. 
Para isso, é necessário que ambas as partes concordem com um número primo p e um número inteiro g, chamado de gerador. 
A chave secreta compartilhada é calculada da seguinte forma:
  - Cada parte escolhe um número inteiro primos secreto x e calcula y = g^x mod p;
  - As partes trocam os valores de y;
  - Cada parte calcula a chave secreta compartilhada como k = y^x mod p;
  - Considere que Alice e Bob concordaram em usar p = 23 e g = 5;
  - Alice escolhe x = 6 e Bob escolhe x = 15;
  - Qual é a chave secreta compartilhada entre Alice e Bob?
  - Resposta: 2
  - Explicação: 
    - Alice: y = 5^6 mod 23 = 8
    - Bob: y = 5^15 mod 23 = 19
    - Alice: k = 19^6 mod 23 = 2
    - Bob: k = 8^15 mod 23 = 2 

8- Explique como funciona o protocolo de assinatura digital RSA. Qual é o problema matemático que o torna "seguro"?
Resposta: O RSA é um algoritmo de criptografia assimétrica que utiliza um par de chaves, uma pública e outra privada, 
para cifrar e decifrar.
Explicando de maneira mais profunda o funcionamento do RSA, temos que:
  - O utilizador A gera um par de chaves, uma pública, é composta pelo modulo(N) e o expoente público(e), e uma privada, 
  o par de chave privado é composto pelo modulo(N) e o expoente privado(d);
  - A chave pública é divulgada para todos os utilizadores que desejam enviar mensagens para A;
  - A chave privada é mantida em segredo por A;
  - O utilizador B envia uma mensagem para , mas antes realiza o«a seguinte computação: C = M^e mod N, onde C é a mensagem cifrada;
  - B cifra a mensagem usando a chave pública de A e envia para A, mas antes realiza o seguinte calculo: M = C^d mod N, onde M é a mensagem decifrada;
  - A recebe a mensagem cifrada e a decifra usando sua chave privada;
  - O problema matemático que o torna "seguro" é o problema da fatoração de números inteiros, que consiste em encontrar os fatores primos de um número inteiro;
  - Esse problema é computacionalmente difícil de ser resolvido, pois não existe um algoritmo eficiente para resolvê-lo;
  Exemplo:
  - Seja p = 7 e q = 11, p é a chave privada e q é a chave pública;
  - Seja N = p*q = 7*11 = 77;
  - Seja e = 5, usado para cifrar a mensagem;
  - Seja d = 29, usado para decifrar a mensagem;
  - Seja M = 10, a mensagem original ou decifrada;
  - Seja C = M^e mod N = 10^5 mod 77 = 10, deste modo a mensagem decifrada é 10;

10-Explique como se pode multiplicar eficientemente um ponto de uma curva elíptica por um número inteiro positivo:
Resposta: 
Para multiplicar eficientemente um ponto de uma curva elíptica por um número inteiro positivo, é necessário utilizar o algoritmo 
de multiplicação de um ponto por um escalar.
  - Seja P um ponto de uma curva elíptica e n um número inteiro positivo;
  - Seja Q = P;
  - Seja R = O;
  - Enquanto n > 0 faça:
    - Se n é ímpar então R = R + Q;
    - Q = 2Q;
    - n = n/2;
  - Retorne R;

9-Num sistema RSA em que o expoente usado para cifrar uma mensagem é sempre 3 e em que não se usa padding aleatório, 
enviar a mesma mensagem m para três destinatários diferentes, com chaves públicas (n1, 3), (n2, 3) e n3, 3), é altamente 
desaconselhado, já que se as três mensagens cifradas, m3 mod n1, m3 mod n2 e m3 mod n3, forem intercetadas é possível recuperar 
a mensagem original.Explique como. [Pista lembre-se do Chinês. . . ]
Resposta: 
  - Seja m a mensagem original;
  - Seja n1, n2 e n3 os módulos das chaves públicas;
  - Seja c1 = m^3 mod n1, c2 = m^3 mod n2 e c3 = m^3 mod n3, isto é os residuos da divisão de m^3 por n1, n2 e n3, respectivamente;
  - Seja N = n1*n2*n3, N é o produto dos módulos das chaves públicas;
  - Seja N1 = N/n1, N2 = N/n2 e N3 = N/n3;
  - Seja y1, y2 e y3 os inversos multiplicativos de N1, N2 e N3, respectivamente;
  - Seja x = c1*y1*N1 + c2*y2*N2 + c3*y3*N3;
  - A mensagem original é m = x^(1/3) mod N;
  Exemplo:
  - Seja m = 123;
  - Seja n1 = 5, n2 = 7 e n3 = 11;
  - Seja c1 = 123^3 mod 5 = 3, c2 = 123^3 mod 7 = 6 e c3 = 123^3 mod 11 = 10;
  - Seja N = 5*7*11 = 385;
  - Seja N1 = 385/5 = 77, N2 = 385/7 = 55 e N3 = 385/11 = 35;
  - Seja y1 = 2, y2 = 3 e y3 = 10;
  - Seja x = 3*2*77 + 6*3*55 + 10*10*35 = 12300;
  - A mensagem original é m = 12300^(1/3) mod 385 = 123;
  Como podemos ver no exemplo acima é possivel recuperar a mensagem original, pois o valor de m é igual ao valor da mensagem original;

4-A máquina de cifra contínua (stream) Lorenz foi criptanalizada graças a um erro de um operador, que fez algo que nunca se 
deve fazer com a maioria das cifras contínuas. Explique que erro foi esse, e que o mesmo permite (e permitiu).
Resposta: 
  - O erro cometido pelo operador foi reutilizar a mesma chave para cifrar duas mensagens diferentes;
  - Esse erro permitiu que os criptoanalistas descobrissem a chave usada para cifrar as mensagens;
  - Comparou as duas mensagens cifradas;
  - Notou que as duas mensagens cifradas eram iguais;
  Deste modo o criptoanalista conseguiu descobrir a chave usada para cifrar as mensagens e decifrar as mensagens;

3-As máquinas de rotores, como a Enigma, concretizam cifras polialfabéticas que tipicamente
não permitem a sua criptanálise usando o teste de Kasiski ou o índice de coincidência. Explique porquê.
Resposta: 
  - O teste de Kasiski e o índice de coincidência não podem ser usados para criptanálise de cifras polialfabéticas, pois 
  esses testes são baseados na análise de frequência de letras;
  - Como as cifras polialfabéticas utilizam mais de um alfabeto, a análise de frequência de letras não é eficiente para 
  criptanálise dessas cifras;
  - Deste modo as maquinas de rotores não podem ser criptanalizadas usando o teste de Kasiski ou o índice de coincidência, devido ao facto de
  estás máquinas usares uma estratégia de cifra polialfabética, que consiste em utilizar mais de um alfabeto para cifrar uma mensagem, 
  isto é, as maquinas são construidas de forma a que cada letra do alfabeto seja cifrada de forma diferente, de acordo com o rotor que 
  está a ser utilizado;
