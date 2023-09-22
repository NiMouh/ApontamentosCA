# Aula 2

# Algoritmos de cifra contínuas mais comuns
- ChaCha20: 256 bits de chave, 64 bits de nonce, 64 bits de contador;
- Salsa20: 256 bits de chave, 64 bits de nonce, 64 bits de contador;
- RC4: 40 a 2048 bits de chave, 0 a 256 bits de IV;
- RCS: 40 a 2048 bits de chave, 0 a 256 bits de IV;

# Redes de Feistel
São funções sempre **invertíveis**, mas construídas a partir de funções que podem não ter inversa. É uma forma engenhosa de construir funções **pseudoaleatórias** (PRFs) e permutações **pseudoaleatórias** (PRPs).

A redes funciona na seguinte forma:
 1. Recebe um bloco de texto-limpo;
 2. Divide o bloco em duas partes (R0 e L0);
 3. Aplica uma função f sobre R, aplica o xOR dela com L e obtém R1;
 4. O R0 transita para L1;
 5. O processo repete-se 'n' vezes;

Nota: Rackoff também refere que para uma PRP (Pseudo random permutations) ser **segura**, a rede de feistel tem de ser com pelo menos **três rondas**. O **DES** especifica 16 rondas, enqquanto que o **3DES** usa 48. O **AES** não usa redes de Feistel no seu núcleo.

# Algoritmos de cifra de bloco mais comuns
- DES (Data Encryption Standard): 64 bits de bloco, 56 bits de chave;
- DEA (Digital Encryption Algorithm): 64 bits de bloco, 128 bits de chave;
- AES (Advanced Encryption Standard): 128 bits de bloco, 128, 192 ou 256 bits de chave;
- Cipher Blowfish, RCS, etc.;

# Linear Feedback Shift Register (LFSR)
