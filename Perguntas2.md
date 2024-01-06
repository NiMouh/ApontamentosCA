# Frequência 2/Exame 2021

1. A criptografia assimétrica pode ser usada para comunicação segura ou para a autenticação de mensagens. Em qualquer dos casos, é fundamental o conhecimento por terceiros da chave pública de um interlocutor. Neste contexto, explique a importância fulcral que têm os certificados de chave pública no âmbito da assinatura de documentos.

R: Os certificados de chave pública desempenham um papel crucial, pois atestam a autenticidade da chave pública associada e do seu criador, integridade da mensagem recebida, e não repúdio, garantindo que uma determinada mensagem veio de uma determinada pessoa sem qualquer tipo de manipulação e sem a mesma a poder negar ter assinado.

2. A validação de um certificado de chave pública envolve diversos passos, sendo um deles a verificação do seu período de validade. Indique, justificando:
    a. Como se estabelece esse período de validade?
    b. Qual a relação que terá de ser verificada entre esse período de validade e uma assinatura realizada com a respetiva chave privada?

R: Os pares de chaves têm um período de validade limitado para proteger contra comprometimento da chave privada. Os certificados de chave pública, com validade estabelecida pela autoridade certificadora, garantem essa limitação. A relação crítica a ser verificada com a assinatura é temporal: se dentro do período de validade do certificado, a assinatura é válida; caso contrário, é considerada inválida.

3. Como é que é normalmente indicada a identidade de uma entidade que produz uma assinatura de um documento? Explique porquê.

R: A identidade de uma autoridade certificadora é indicada pela assinatura da mesma que se encontra no certificado de chave pública emitido. O mesmo contém a chave pública da autoridade certificadora com o devido certificado de chave pública, com o respetivo período de validação e lista de certificados de revogação, que é assinado pela autoridade certificadora superior, e assim sucessivamente até à raiz da cadeia de certificação.

4. As assinaturas digitais de documentos são tipicamente realizadas usando RSA e assinaturas com apêndice. Neste último caso, explique:
    a. Por que razão são calculadas com uma função de síntese (digest function)?
    b. Como é que o validador da assinatura sabe qual é a função que foi usada?

R: As assinaturas com apêndice são calculadas usando uma função de síntese (digest) do documento para eficiência e segurança. O digest, de tamanho fixo, representa o conteúdo de forma única. Qualquer alteração mínima no documento resulta em um digest drasticamente diferente, assegurando detecção confiável de modificações. O validador da assinatura identifica a função de síntese ao examinar um prefixo no digest, conhecido como identificador de algoritmo de hash, indicando a função utilizada durante a assinatura.

5.  Qual é a relevância das TSA (Time Stamping Authorities) no âmbito das assinaturas digitais de documentos?

R: A relevância de serviços fornecidos por uma TSA provém do facto de fornecer uma maior confiança á data da assinatura, pois a mesma é assinada pela TSA, que é uma entidade de confiança.

6. Explique como se pode partilhar um segredo entre n entidades, em que todas as entidades são necessárias para revelar o segredo.

R:
- Representando o segredo como um inteiro S com k bits. O segredo é dividido em n partes, nesse caso, n-1 partes são geradas aleatoriamente (s1 a sn-1) e a última parte (sn) é calculada como a operação de exclusivo ou (XOR) entre o segredo e todas as outras partes.

- Para reaver o segredo original, basta fazer a operação de exclusivo ou (XOR) entre todas as partes compartilhadas, pois, de acordo com a propriedade do operador XOR, o resultado dessa operação é igual ao segredo original.
Portanto, para recuperar o segredo, todas as n partes devem estar presentes e serem combinadas usando a operação XOR (ou operações equivalentes, como adição e subtração módulo m, dependendo do caso).

7. Explique como se pode partilhar um segredo em que 3 de 5 entidades são necessárias para revelar o segredo.

R:
O processo começa representando o segredo como o coeficiente independente de um polinômio de grau t - 1. Neste caso em específico onde 3 de 5 entidades são requeridas para reconstruir o segredo, o polinômio será de grau 2, pois t - 1 é igual a 2.

Para realizar a partilha do segredo o método envolve a geração de um polinômio A(x) com coeficientes aleatórios, sendo o coeficiente independente do segredo a ser compartilhado. Selecionam-se cinco pontos distintos (x_k), garantindo que cada entidade receba um par de valores (x_k, A(x_k)), onde A(x_k) é o valor do polinômio A(x) calculado para o ponto x_k.

Durante todo o processo, é crucial utilizar aritmética modular para realizar operações matemáticas, como soma, multiplicação e exponenciação. A aritmética modular é essencial para manter os cálculos dentro de um intervalo específico, preservando a segurança e a integridade do esquema de partilha de segredo.

Por fim, para reconstruir o segredo original, é necessário o consentimento e a colaboração de pelo menos 3 das 5 entidades. Utilizando métodos de interpolação polinomial, como o método de Lagrange, essas 3 ou mais entidades combinam suas partes do segredo (pares de valores) para reconstruir o polinômio original e, consequentemente, revelar o segredo a ser protegido.

8. A técnica one-of-two oblivious transfer permite que uma entidade extraia um item de informação (de um conjunto de dois itens) de uma outra entidade sem que esta consiga saber qual dos itens foi extraído. Explique como.

R: 
- Alice gera dois valores aleatórios, m0 e m1, mantendo-os em segredo;
- Bob escolhe qual item deseja, chamado de b, podendo ser 0 ou 1;
- Bob gera um número aleatório k e calcula v = (x_b + k*e) mod N, onde x_b representa o valor escolhido por Bob (0 ou 1). Em seguida, envia v para Alice;
- Usando sua chave privada (d), Alice calcula duas versões cifradas dos itens de informação: m'_0 = (m0 + (v - x_0)^d) mod N e m'_1 = (m1 + (v - x_1)^d) mod N. Ela envia ambas as versões cifradas para Bob;
- Bob realiza um cálculo para decifrar apenas um dos itens recebidos de acordo com sua escolha: m_b = (m'_b - k) mod N;
- Finalmente, Bob obtém o valor correspondente a m0 ou m1, dependendo da escolha b, sem que Alice saiba qual dos dois itens foi selecionado. 

9. Os resíduos quadráticos são indiretamente usados em protocolos de prova de identidade que não revelam informação (zero knowledge). Qual é o problema matemático que os torna atrativos neste contexto?

R:
O problema matemático que torna os resíduos quadráticos atrativos neste contexto é o problema da raiz quadrada modular, que consiste em dado um número inteiro a e um primo p, é computacionalmente dificil encontrar um número inteiro x tal que x^2 = a mod p, sem que se conheça a fatorização de p. Esta dificuldada está intimamente relacionada com o problema do logartimo discreto, que é a base de muitos sistemas criptográficos.

# Frequência 2/Exame 2022

1.  Um elemento fundamental de uma assinatura digital é o instante temporal em que foi gerada. Como se consegue garantir que o seu valor é confiável, ou seja, que a assinatura não foi produzida num instante diferente do indicado na mesma?

R: Através de um serviço feito pela *Time-Stamping Autority* (TSA), uma entidade de confiança, onde a data de assinatura é assinada pela TSA, garantindo assim a sua autenticidade.

2. Long Term Validation (LTV) é uma expressão que é usada para referir a capacidade de uma assinatura digital ser verificável de forma confiável muitos anos depois de ter sido produzida. Qual é o principal problema que a passagem do tempo cria na validação de assinaturas, e que levou à criação dos mecanismos que permitem a LTV (não os descreva!)?

R: O principal problema que a passagem do tempo cria na validação de assinaturas é a possibilidade do certificado poder vir a ser revogado (seja por comprometimento da chave privada, ou por outros motivos). Para evitar este problema, foram criados mecanismos que permitem a Long-Term Validation (LTV).

3. Qual é a relevância que dispositivos criptográficos, como o Cartão de Cidadão, têm no que diz respeito à qualidade de uma assinatura digital?

R: Os dispositivos criptográficos, como *Smartcards*, permitem assinaturas digitais com um maior segurança, pois a chave privada nunca sai do dispositivo. Neste, as operações criptográficas são feitas no mesmo e é pedido credênciais para efetuar, garantindo assim a autenticidade do utilizador, pois é necessário autenticação física e lógica.

4.  Imagine que tem de validar uma assinatura colocada num documento. Indique, de forma sucinta, os todos os passos que terá de executar (assuma, que a assinatura contém todos os elementos necessários que normalmente são necessários para essa validação, como cadeias de certificação).

R: Ao receber a assinatura, é necessário verificar a sua validade, para tal, é necessário verificar a cadeia de certificação, a data de assinatura, e a integridade da assinatura. Para verificar a cadeia de certificação, é necessário verificar a assinatura do certificado com a chave pública da autoridade certificadora superior, e assim sucessivamente até à raiz da cadeia de certificação. Para verificar a data de assinatura, é necessário verificar se a mesma está dentro do período de validade do certificado. Para verificar a integridade da assinatura, é necessário verificar se a mesma foi feita com a chave privada do certificado, para isso é feita a decifragem da assinatura com a chave pública do certificado, e verificar se o digest do documento é igual ao digest da assinatura.

5. Um certificado de chave pública X.509 v3 é constituído por uma parte obrigatória e por
um conjunto arbitrário de extensões.

    a. Como são identificadas estas extensões?
    b. Uma extensão pode ser crítica ou não-crítica. Explique as implicações desta classificação.

R: As extensões são identificadas pelo seu **OID** (Object Identifier). Uma **extensão crítica** é uma extensão que deve ser reconhecida e processada por qualquer aplicação que processe o certificado, caso contrário, a é considerada uma **extensão não-crítica**.

6. Explique como se pode partilhar um segredo entre n entidades, n ≥ 2, em que apenas t entidades, 2 ≤ t ≤ n, são necessárias para revelar o segredo. Considere os casos t < n e t = n.

R: 
- Representando o segredo como um inteiro S com k bits. O segredo é dividido em n partes, nesse caso, t partes são geradas aleatoriamente (s1 a st) e as restantes (sn-t+1 a sn) são calculadas como a operação de exclusivo ou (XOR) entre o segredo e todas as outras partes.
- Para reaver o segredo original, basta fazer a operação de exclusivo ou (XOR) entre todas as partes compartilhadas, pois, de acordo com a propriedade do operador XOR, o resultado dessa operação é igual ao segredo original.
- Portanto, para recuperar o segredo, pelo menos t das n partes devem estar presentes e serem combinadas usando a operação XOR (ou operações equivalentes, como adição e subtração módulo m, dependendo do caso).
- No caso em que t = n, todas as partes são necessárias para reconstruir o segredo original.
- No caso em que t < n, apenas t das n partes são necessárias para reconstruir o segredo original.
- No caso em que t = 2, apenas 2 das n partes são necessárias para reconstruir o segredo original. 

1. A técnica one-of-two oblivious transfer permite que uma entidade extraia um item de informação (de um conjunto de dois itens) de uma outra entidade sem que esta consiga saber qual dos itens foi extraído. Explique como pode adaptar essa técnica para extrair um de n, com n > 2. A técnica é escalável, isto é, a sua utilização para n grande é prática?

R: 
- Alice gera dois valores aleatórios, m0 e m1, mantendo-os em segredo;
- Bob escolhe qual item deseja, chamado de b, podendo ser 0 ou 1;
- Bob gera um número aleatório k e calcula v = (x_b + k*e) mod N, onde x_b representa o valor escolhido por Bob (0 ou 1). Em seguida, envia v para Alice;
- Usando sua chave privada (d), Alice calcula duas versões cifradas dos itens de informação: m'_0 = (m0 + (v - x_0)^d) mod N e m'_1 = (m1 + (v - x_1)^d) mod N. Ela envia ambas as versões cifradas para Bob;
- Bob realiza um cálculo para decifrar apenas um dos itens recebidos de acordo com sua escolha: m_b = (m'_b - k) mod N;
- Finalmente, Bob obtém o valor correspondente a m0 ou m1, dependendo da escolha b, sem que Alice saiba qual dos dois itens foi selecionado.

8. Os resíduos quadráticos são indiretamente usados em protocolos de prova de identidade que não revelam informação (zero knowledge proofs). Qual é o problema matemático que os torna atrativos neste contexto?

R: O problema matemático que torna os resíduos quadráticos atrativos neste contexto é o problema da raiz quadrada modular, que consiste em dado um número inteiro a e um primo p, é computacionalmente dificil encontrar um número inteiro x tal que x^2 = a mod p, sem que se conheça a fatorização de p. Esta dificuldada está intimamente relacionada com o problema do logartimo discreto, que é a base de muitos sistemas criptográficos.


9. A aritmética modular é usada extensivamente em aplicações criptográficas. O que é que a torna tão útil?

R: A aritmética modular é essencial para manter os cálculos dentro de um intervalo específico, preservando a segurança e a integridade do esquema de partilha de segredo.

10. Para que é que serve uma cifra homomórfica?

R: Uma cifra homomórfica é uma cifra que permite que operações matemáticas sejam realizadas sobre os textos cifrados, sem que seja necessário decifrados o texto. Isso permite que os dados sejam processados sem revelar o seu conteúdo, o que é útil em muitos cenários, como a computação em cloud.

# Extras

5. Estender o protocolo de "one-of-two oblivious transfer" para permitir que quatro entidades troquem informações de modo que cada uma delas possa obter um item específico, sem que as outras saibam qual item foi solicitado. Explique como.

R:
- Alice gera quatro valores aleatórios, m0, m1, m2 e m3, mantendo-os em segredo;
- Bob escolhe qual item deseja, chamado de b, podendo ser 0, 1, 2 ou 3;
- Bob gera um número aleatório k e calcula v = (x_b + k*e) mod N, onde x_b representa o valor escolhido por Bob (0, 1, 2 ou 3). Em seguida, envia v para Alice;
- Usando sua chave privada, Alice calcula quatro versões cifradas dos itens de informação: m'_0 = (m0 + (v - x_0)^d) mod N, m'_1 = (m1 + (v - x_1)^d) mod N, m'_2 = (m2 + (v - x_2)^d) mod N e m'_3 = (m3 + (v - x_3)^d) mod N. Ela envia todas as versões cifradas para Bob;
- Bob realiza um cálculo para decifrar apenas um dos itens recebidos de acordo com sua escolha: m_b = (m'_b - k) mod N;
- Finalmente, Bob obtém o valor correspondente a m0, m1, m2 ou m3, dependendo da escolha b, sem que Alice saiba qual dos quatro itens foi selecionado.

6. Explique em que consiste Zero-knowledge proofs of identity?

R: Zero-knowledge proofs of identity é um protocolo de prova de identidade que não revela informação (zero knowledge). Ele consiste num protocolo de autenticação que permite a um indivíduo provar a sua identidade a um terceiro sem revelar qualquer informação adicional sobre si mesmo. 


7. Em que consiste Zero-knoledge proof, explique o seu funcionamento?

R: O esquema Feige-Fiat-Shamir funciona da seguinte maneira:
- Preparação dos Parâmetros Públicos:
Peggy seleciona um número grande, n, que é o resultado da multiplicação de dois números primos de Blum. Ela divulga esse número, juntamente com outras informações, porém mantém algumas partes dessas informações em segredo.
- Geração e Verificação da Prova de Identidade:
Durante cada execução do protocolo, Peggy escolhe aleatoriamente um valor, R, e envia para Victor o valor X = ±R^2 mod n. Peggy também decide aleatoriamente um sinal (+ ou -) para gerar o valor, garantindo que X seja ou não seja um resíduo quadrático. Isso é feito sem revelar qual escolha foi feita.
Victor desafia Peggy, enviando um vetor aleatório de bits chamado E.
Com base no desafio de Victor, Peggy calcula e envia para Victor o valor Y = ±R multiplicado pelo produto dos valores S_j elevados à potência dos bits E_j, tudo isso mod n. Mais uma vez, Peggy escolhe aleatoriamente o sinal (+ ou -) para gerar Y.
Victor então verifica se X é igual a ±Y^2 multiplicado pelo produto dos valores I_j elevados à potência dos bits E_j, tudo isso mod n.
- Validação e Conclusão:
Se a verificação for bem-sucedida para várias execuções (determinado por T), Victor fica convencido da identidade de Peggy.
O esquema Feige-Fiat-Shamir aproveita propriedades matemáticas dos números Blum e a complexidade computacional associada ao cálculo de raízes quadradas modulares para garantir que a identidade de Peggy seja comprovada sem revelar informações adicionais.
Assim, uma prova de conhecimento zero, como o esquema Feige-Fiat-Shamir, permite que uma parte prove a veracidade de uma afirmação (neste caso, sua identidade) sem divulgar qualquer informação adicional, apenas demonstrando a validade da afirmação por meio de um protocolo matemático seguro.

8. Explique em que consiste Quadratic residues?

R: Quando lidamos com um número primo p que segue a forma 4k + 3, há uma maneira direta de calcular as raízes quadradas de um resíduo quadrático a. Se a é um resíduo quadrático módulo p, as suas raízes quadradas podem ser calculadas usando a fórmula r ≡ ±a^((p+1)/4) mod p.
Isso é possível porque, se a é um resíduo quadrático módulo p, então a elevado à potência de (p-1) / 2 é congruente a 1 (mod p), de acordo com o Pequeno Teorema de Fermat. Assim, a^(p+1) / 2 é congruente a (mod p). Como (p+1) / 2 é um número par, as raízes quadradas podem ser calculadas usando essa fórmula.
Quando lidamos com um número composto n que é o produto de dois primos p e q, ambos seguindo a forma 4k + 3, e a é um resíduo quadrático módulo n, então a terá quatro raízes quadradas. Essas quatro raízes podem ser calculadas usando o Teorema Chinês dos Restos (Chinese Remainder Theorem). Dessas quatro raízes, duas têm o símbolo de Jacobi +1 e as outras duas têm o símbolo de Jacobi -1.

9. Explique o problema matemático relacionado aos resíduos quadráticos?

R: O problema matemático relacionado aos resíduos quadráticos e à busca por raízes quadradas modulares está intimamente ligado ao campo da teoria dos números. Este problema é frequentemente utilizado em criptografia e segurança da informação.
O problema fundamental envolve encontrar soluções para a equação x^2 = a mod p, onde \(a\) é um número inteiro e \(p\) é um número primo.
Em outras palavras, o objetivo é determinar se um número \(a\) é um resíduo quadrático módulo um número primo \(p\) específico e, em caso afirmativo, encontrar os valores de \(x\) que satisfazem a congruência x^2 = a mod p.
Por exemplo, se \(a = 3\) e \(p = 7\), a equação x^2 = 3 mod7 teria como solução \(x = 5\) e \(x = 2\) , pois 5^2 = 3 mod7 e 2^2 = 3 mod7.