# Aula 1

## Teórica - História e conceitos fundamentais da criptografia

### Conceitos base


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