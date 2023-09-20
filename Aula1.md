# Aula 1

## Teórica - História e conceitos fundamentais da criptografia

### Conceitos base
Objetivo inicial da criptografia: Garantir que a mensagem da pessoa A chegue a pessoa B sem que a pessoa C consiga ler.

1. **Texto-limpo**: mensagem original.
2. **Cifra ou Esquema Criptográfico**: algoritmo que transforma o texto-limpo em texto-cifrado e vice-versa (por norma são dois algoritmos diferentes).
3. **Criptograma**: texto-cifrado.
4. **Chave de cifra**: conjunto de dados que permite a cifrar e/ou decifrar do texto-limpo.
5. **Sistema criptográfico**: conjunto de cifra, chave de cifra, conjunto de decifra e chave de decifra.
6. **Modelo de ataque**: classificação para um possível ataque ao sistema criptográfico.
7. **Ataque**: Tentativa de quebra dos objetivos da técnica criptográfica.
8. **Criptanálise**: Conjunto de técnicas que visam a quebra de sistemas criptográficos. Consistem em decifrar sem saber a chave ou tendo a chave.

### Cifras
Estas são algumas das propriedades que uma cifra segura tem:
 - **Difusão**: Se uma cifra for de qualidade, quaisquer propriedades estatísticas do texto limpo estão completamente **difusas** (sem qualquer tipo de correlação) por todo o criptograma.
 - **Confusão**: Se uma cifra for de qualidade, não são perceptiveis quaisquer relações entre um bloco de texto-limpo, a chave de cifra e o bloco de criptograma.
 - **Não maneável**: Se uma cifra for de qualidade, não é possível **manejar** (alterar) o texto cifrado sem que o texto limpo seja alterado. Esta propriedade é mantida por um código de **autenticação de mensagem**.
 - **Semântica**: Se uma cifra for de qualidade, o adversário não deverá ser capaz de obter informações sobre o texto limpo a partir do texto cifrado.
 - **Não determinística**: Esta propriedade permite que a cifra produza saídas diferentes para o mesmo texto limpo e chave de cifra.

Nota: Todas estas propriedades acima têm que ser balenceadas com a **usabilidade** da cifra.

#### Cifras clássicas
São algoritmos que utilizam a mesma chave para cifrar e decifrar. Cifras clássicas têm **um** algoritmo (para cifrar e para decifrar).

Alguns Exemplos:
 - Cifra de César;
 - Cifra de Vigenère (mais difusa que a de César);
 - Cifra Enigma;
 - Cifra de Vernam (perfeita em termos de secretismo, contudo não é usável);

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
 - Input: Chave pública, Chave secreta
 - Output: Par de chaves

Para **cifrar**:
 - Input: Texto-limpo, Chave pública
 - Output: Texto-cifrado

Para **decifrar**:
 - Input: Texto-cifrado, Chave secreta
 - Output: Texto-limpo


#### Cifras de chave simétrica continuas
As cifras de chave simétrica continuas usam um algoritmo que a partir de uma chave com tamanho **fixo** e **comportável**, geral uma sequência tão grande quanto necessária para cifrar um ficheiro. Este tipo de cifra tem como defeito a sua **maneabilidade** (facilidade da alteração do texto cifrado). Se cifrarmos um ficheiro já antes cifrado com a **mesma chave**, iremos obter o texto-limpo.

Nota: Estas cifras são usadas em situações em que o canal de comunicação não permite a **alteração** da mensagem cifrada ou quando a perda de parte da mensagem na transmissão não é um problema de grande dimensão (ex: streaming de vídeo).

#### Cifras de chave simétrica de bloco
O algoritmo para **decifrar** é diferente que o de **cifrar**. A diferença entre as cifras de chave simétrica de bloco e as cifras de chave simétrica continua é que as cifras de chave simétrica de bloco geram uma cifra de tamanho fixo (bloco) e não uma cifra de tamanho variável. Caso a cifra de chave simétrica de bloco seja alterada (maneada), o texto cifrado perderá toda a sua integridade.

Nota: Este tipo de cifra é mais segura, dependendo de como são usadas, quando o canal de comunicação permite a **alteração** da mensagem cifrada, sem que a mensagem perca a sua **integridade**.

#### *Padding* (Preenchimento)
O **padding** é uma técnica de preenchimento de dados que consiste em adicionar um número de bytes ao final de um bloco de dados, de forma a que o tamanho do bloco de dados seja múltiplo do tamanho do bloco de dados da cifra.

Nota: O último bloco tem sempre *padding*, mesmo que o bloco da mensagem seja múltiplo do tamanho do bloco da cifra é acrescentado um bloco de *padding*.

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

Nota: Não é uma técnica de criptanálise.

#### Ataque do homem no meio
Este tipo de ataque é feito quando a **Pessoa A (Alice)** e a **Pessoa B (Bob)** estão sujeitos a um ataque por uma **Pessoa C (Claire)** que se encontra no meio da comunicação entre as duas pessoas. Existem dois tipos de ataque do homem no meio:
- **Ataque do homem no meio passivo**: A **Pessoa C (Claire)** não consegue alterar (apenas vê) a mensagem cifrada (também chamada de **Pessoa E (Eve)**).
- **Ataque do homem no meio ativo**: A **Pessoa C (Claire)** consegue alterar e ver a mensagem cifrada.

### Funções de Hash
Funções que dado um input de qualquer tamanho, produzem um output de um tamanho fixo. Estas funções são **one-way** (não há forma de obter o input a partir do output). 

Nota: São **resistentes a colisões**, ou seja, é difícil encontrar dois inputs diferentes que produzam o mesmo output (em tempo útil). Também têm como propriedade a **resistência a previsão de uma pré-imagem** e a **resistência a previsão de uma segunda pré-imagem**, ou seja, é difícil encontrar um input que produza um output conhecido.


## Prática

```python
import string


def clean_text(text):
    import re
    pattern = r'[^A-Za-z]'

    clean_text = re.sub(pattern, '', text)
    clean_text = clean_text.lower()

    return clean_text


def letter_frequency(text):
    text = clean_text(text)

    frequency = {}

    for letter in text:
        if letter in frequency:
            frequency[letter] += 1
        else:
            frequency[letter] = 1

    return frequency


def ngram_frequency(text, n):
    text = clean_text(text)

    frequency = {}

    for i in range(len(text) - n + 1):
        ngram = text[i:i+n]
        if ngram in frequency:
            frequency[ngram] += 1
        else:
            frequency[ngram] = 1

    return frequency


def substitution_alphabet(key):
    alphabet = string.ascii_lowercase
    alphabet_substitution = alphabet[key:] + alphabet[:key]
    return alphabet_substitution


def substitution_cipher(plain_text, key):
    new_alphabet = substitution_alphabet(key)
    original_alphabet = substitution_alphabet(0)

    # Clean and normalize the plain text
    plain_text = clean_text(plain_text)

    cipher = ""

    for letter in plain_text:
        index = original_alphabet.index(letter)
        cipher += new_alphabet[index]

    return cipher


def substitution_decipher(cipher_text, key):
    new_alphabet = substitution_alphabet(key)
    original_alphabet = substitution_alphabet(0)

    decipher = ""

    for letter in cipher_text:
        index = new_alphabet.index(letter)
        decipher += original_alphabet[index]

    return decipher


def brute_force_substitution_decipher(cipher_text, language):

    # Define the alphabet and initialize an empty result list
    alphabet = string.ascii_lowercase
    results = []

    if language == "en": # English
        common_bigrams = ['th', 'he', 'in', 'er', 'an']
        common_trigrams = ['the', 'and', 'tha', 'ent', 'ion']
        letter_frequencies = {
            'a': 0.0817, 'b': 0.0149, 'c': 0.0278, 'd': 0.0425, 'e': 0.1270,
            'f': 0.0223, 'g': 0.0202, 'h': 0.0609, 'i': 0.0697, 'j': 0.0015,
            'k': 0.0077, 'l': 0.0403, 'm': 0.0241, 'n': 0.0675, 'o': 0.0751,
            'p': 0.0193, 'q': 0.0010, 'r': 0.0599, 's': 0.0633, 't': 0.0906,
            'u': 0.0276, 'v': 0.0098, 'w': 0.0236, 'x': 0.0015, 'y': 0.0197,
            'z': 0.0007,
        }

    if language == "pt": # Portuguese
        common_bigrams = ['es', 'em', 'os', 'as', 'do']
        common_trigrams = ['que', 'ent', 'ndo', 'com', 'dos']
        letter_frequencies = {
            'a': 0.1463, 'b': 0.0104, 'c': 0.0388, 'd': 0.0499, 'e': 0.1257,
            'f': 0.0102, 'g': 0.0130, 'h': 0.0075, 'i': 0.0618, 'j': 0.0040,
            'k': 0.0002, 'l': 0.0278, 'm': 0.0474, 'n': 0.0445, 'o': 0.0973,
            'p': 0.0252, 'q': 0.0120, 'r': 0.0653, 's': 0.0680, 't': 0.0433,
            'u': 0.0363, 'v': 0.0157, 'w': 0.0004, 'x': 0.0021, 'y': 0.0005,
            'z': 0.0047,
        }

    # Iterate through all possible keys
    for key in range(len(alphabet)):
        deciphered_text = substitution_decipher(cipher_text, key)

        # Calculate the letter and n-gram frequencies of the deciphered text
        deciphered_text_frequency = letter_frequency(deciphered_text)
        deciphered_text_bigram_frequency = ngram_frequency(deciphered_text, 2)
        deciphered_text_trigram_frequency = ngram_frequency(deciphered_text, 3)

        # Calculate the letter frequency error
        letter_frequency_error = 0

        for letter in alphabet:
            letter_frequency_error += abs(letter_frequencies[letter] - deciphered_text_frequency[letter])

        # Calculate the bigram frequency error
        bigram_frequency_error = 0

        for bigram in common_bigrams:
            if bigram in deciphered_text_bigram_frequency:
                bigram_frequency_error += abs(deciphered_text_bigram_frequency[bigram] / len(deciphered_text) - 0.02)

        # Calculate the trigram frequency error
        trigram_frequency_error = 0

        for trigram in common_trigrams:
            if trigram in deciphered_text_trigram_frequency:
                trigram_frequency_error += abs(deciphered_text_trigram_frequency[trigram] / len(deciphered_text) - 0.01)

        # Calculate the total error
        total_error = letter_frequency_error + bigram_frequency_error + trigram_frequency_error

        # Append the results to the results list
        results.append((total_error, key, deciphered_text))

    # Sort the results list by the total error
    results.sort(reverse=True)

    # Return the deciphered text with the lowest error
    return results[0][2]


def vigenere_cipher(plain_text, key):

    # Clean and normalize the plain text and the key
    plain_text = clean_text(plain_text)

    key = clean_text(key)

    cipher = ""

    substitution_alphabets = [substitution_alphabet(letter) for letter in range(26)]

    for i in range(len(plain_text)):
        letter = plain_text[i]
        key_letter = key[i % len(key)]
        key_index = string.ascii_lowercase.index(key_letter)
        cipher += substitution_alphabets[key_index][string.ascii_lowercase.index(letter)]

    return cipher


def vigenere_decipher(text, key):

    # Clean and normalize the plain text and the key
    text = clean_text(text)
    key = clean_text(key)

    decipher = ""

    substitution_alphabets = [substitution_alphabet(i) for i in range(26)]

    for i in range(len(text)):
        letter = text[i]
        key_letter = key[i % len(key)]
        key_index = string.ascii_lowercase.index(key_letter)
        decipher += string.ascii_lowercase[substitution_alphabets[key_index].index(letter)]

    return decipher


def kasiski_exam(cipher_text, max_key_length=20):

    # Create a list to store the distances between repeated trigrams
    trigram_distances = {}

    # Find repeated trigrams and calculate their distances
    for i in range(len(cipher_text) - 2):
        trigram = cipher_text[i:i+3]
        if trigram in trigram_distances:
            trigram_distances[trigram].append(i - trigram_distances[trigram][-1])
        else:
            trigram_distances[trigram] = [i]

    # Find the most common trigrams with distances
    common_trigrams = [(trigram, distances) for trigram, distances in trigram_distances.items() if len(distances) >= 2]

    # Calculate the possible key lengths based on the distances between repeated trigrams
    possible_key_lengths = set()
    for trigram, distances in common_trigrams:
        for i in range(len(distances) - 1):
            for j in range(i + 1, len(distances)):
                distance = distances[j] - distances[i]
                if 2 <= distance <= max_key_length:
                    possible_key_lengths.add(distance)

    return sorted(list(possible_key_lengths))


def index_of_coincidence(cipher_text, key_length):

    sum_of_coicidences = 0.0

    for i in range(key_length):
        substring = cipher_text[i::key_length]
        substring_length = len(substring)

        if substring_length <= 1:  # Avoid division by zero
            continue

        frequencies = {}

        for letter in substring:
            if letter in frequencies:
                frequencies[letter] += 1
            else:
                frequencies[letter] = 1

        numerator = sum(frequency * (frequency - 1) for frequency in frequencies.values())
        denominator = substring_length * (substring_length - 1)
        sum_of_coicidences += numerator / denominator

    return sum_of_coicidences / key_length


def possible_key_lengths(cipher_text, max_key_length=20):

    # Clean and normalize the cipher text
    cipher_text = clean_text(cipher_text)

    possible_lengths = kasiski_exam(cipher_text, max_key_length)
    possible_ic = {length: index_of_coincidence(cipher_text, length) for length in possible_lengths}

    # Filter possible key lengths based on the Index of Coincidence threshold
    ic_threshold = 0.06  # You can adjust this threshold as needed
    filtered_lengths = [length for length in possible_lengths if possible_ic[length] > ic_threshold]

    return filtered_lengths

def vigenere_brute_force(cipher_text, key_length):
    # Calculate the most likely key for each slice of the cipher text
    key = ""
    for key_index in range(key_length):
        substring = cipher_text[key_index::key_length]
        substring_frequencies = letter_frequency(substring)
        most_frequent_letter = max(substring_frequencies, key=substring_frequencies.get)
        key += string.ascii_lowercase[(string.ascii_lowercase.index(most_frequent_letter) - string.ascii_lowercase.index('e')) % 26]

    return key


if __name__ == "__main__":
    text = "The cab arrived late. The inside was in as bad of shape as the outside which was concerning, and it didn't appear that it had been cleaned in months. The green tree air-freshener hanging from the rearview mirror was either exhausted of its scent or not strong enough to overcome the other odors emitting from the cab. The correct decision, in this case, was to get the hell out of it and to call another cab, but she was late and didn't have a choice. Things aren't going well at all with mom today. She is just a limp noodle and wants to sleep all the time. I sure hope that things get better soon. The song came from the bathroom belting over the sound of the shower's running water. It was the same way each day began since he could remember. It listened intently and concluded that the singing today was as terrible as it had ever been. The opened package of potato chips held the answer to the mystery. Both detectives looked at it but failed to realize it was the key to solve the crime. They passed by it assuming it was random trash ensuring that the case would never be solved. The towels had been hanging from the rod for years. They were stained and worn, and quite frankly, just plain ugly. Debra didn't want to touch them but she really didn't have a choice. It was important for her to see what was living within them."
    language_flag = "en"

    cipher = vigenere_cipher(text, "key")
    print("Cipher Text:")
    print(cipher)

    decipher = vigenere_decipher(cipher, "key")
    print("Deciphered Text:")
    print(decipher)

    key_lenghts = possible_key_lengths(cipher)
    print("Possible Key Lengths:")
    print(key_lenghts)

    key = vigenere_brute_force(cipher, key_lenghts[0])
    print("Key:")
    print(key)
```