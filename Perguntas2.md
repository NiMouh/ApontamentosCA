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

8.1. Estender o protocolo de "one-of-two oblivious transfer" para permitir que quatro entidades troquem informações de modo que cada uma delas possa obter um item específico, sem que as outras saibam qual item foi solicitado. Explique como.

R:
- Alice gera quatro valores aleatórios, m0, m1, m2 e m3, mantendo-os em segredo;
- Bob escolhe qual item deseja, chamado de b, podendo ser 0, 1, 2 ou 3;
- Bob gera um número aleatório k e calcula v = (x_b + k*e) mod N, onde x_b representa o valor escolhido por Bob (0, 1, 2 ou 3). Em seguida, envia v para Alice;
- Usando sua chave privada, Alice calcula quatro versões cifradas dos itens de informação: m'_0 = (m0 + (v - x_0)^d) mod N, m'_1 = (m1 + (v - x_1)^d) mod N, m'_2 = (m2 + (v - x_2)^d) mod N e m'_3 = (m3 + (v - x_3)^d) mod N. Ela envia todas as versões cifradas para Bob;
- Bob realiza um cálculo para decifrar apenas um dos itens recebidos de acordo com sua escolha: m_b = (m'_b - k) mod N;
- Finalmente, Bob obtém o valor correspondente a m0, m1, m2 ou m3, dependendo da escolha b, sem que Alice saiba qual dos quatro itens foi selecionado.

9. Os resíduos quadráticos são indiretamente usados em protocolos de prova de identidade que não revelam informação (zero knowledge). Qual é o problema matemático que os torna atrativos neste contexto?

R:
O problema matemático que torna os resíduos quadráticos atrativos neste contexto é o problema da raiz quadrada modular, que consiste em dado um número inteiro a e um primo p, é computacionalmente dificil encontrar um número inteiro x tal que x^2 = a mod p, sem que se conheça a fatorização de p. Esta dificuldada está intimamente relacionada com o problema do logartimo discreto, que é a base de muitos sistemas criptográficos.

# Frequência 2/Exame 2022