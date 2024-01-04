# Aula 10

## Provas de conhecimento nulo (ZKP)
As provas de conhecimento nulo permitem provar que se conhece um segredo sem revelar o segredo em si. 

Normalmente, esta prova é probabilistica, ou seja, esta prova envolve multiplas iterações. Quanto maior o número de iterações, menor a probabilidade de falsificação.

### One of two oblivious transfer (OT)
O OT permite que um emissor envie uma mensagem para um recetor, sem que o emissor **saiba qual a mensagem enviada** e sem que o recetor **saiba qual a mensagem não foi enviada**.

Funciona da seguinte forma:
- Suponhamos que a Alice tem duas mensagens, m1 e m2;
- Suponhamos que o Bob quer receber uma das mensagens, mas não quer que a Alice saiba qual a mensagem que recebeu;
- Usando as tecnicas do algoritmo RSA, o 'N' corresponde á modulo da chave pública e o 'e' corresponde ao expoente da chave pública, e o 'd' corresponde ao expoente da chave privada;
- O Bob pede á alice para gerar duas mensagens x0 e x1 (números aleatórios menores que N);
- O Bob quer o mb, sendo b 0 ou 1. Então, o Bob gera um valor k e envia para a alice o v = (xb + k^e) mod N;
- A Alice recebe o v e calcula o m'1 = m1 + (v - x0)^d mod N e o m'2 = m2 + (v - x1)^d mod N;
- A Alice envia o m'1 e o m'2 para o Bob;
- O Bob calcula o mb = m'b - k mod N.

### Prova de conhecimento nulo - Prova de identidade
Permite que uma parte quer provar a sua identidade a uma segunda parte via um **segredo**. mas **não quer** que a segunda parte saiba **nada** sobre esse segredo. O problema matemática encontra-se na computação da raiz quadradra modular n = pq;

Funciona da seguinte forma:
- A Alice escolhe um número grande n que é um produto de dois primos grandes p e q, e escolhe k números aleatórios que são coprimos com n;
- De seguida, ela escolhe k I's sendo eles +-Sk^-2 mod n;
- Ela publica o n, e os k I's (sendo os Sk's o segredo);
- Para verificar a identidade, a Alice escolhe um número aleatório R e envia X= +-R^2 mod n, e o Bob envia um vetor E onde cada elemento é 0 ou 1;
- Depois, a Alice envia o vetor Y = +-R * (S1^E1) * (S2^E2) * ... * (Sk^Ek) mod n;
- Caso X seja igual a -+Y^2 mod n, então a Alice provou a sua identidade.

## Cifragem homomórfica
A cifragem homomórfica permite que sejam realizadas operações sobre os dados cifrados, sem que seja necessário decifrar os dados.