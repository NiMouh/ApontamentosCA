# Aula 2

## Algoritmos de cifra contínuas mais comuns
- ChaCha20: 256 bits de chave, 64 bits de nonce, 64 bits de contador;
- Salsa20: 256 bits de chave, 64 bits de nonce, 64 bits de contador;
- RC4: 40 a 2048 bits de chave, 0 a 256 bits de IV;
- RCS: 40 a 2048 bits de chave, 0 a 256 bits de IV;

## Redes de Feistel
São funções sempre **invertíveis**, mas construídas a partir de funções que podem não ter inversa. É uma forma engenhosa de construir funções **pseudoaleatórias** (PRFs) e permutações **pseudoaleatórias** (PRPs).

A redes funciona na seguinte forma, para cifrar:
 1. Recebe um bloco de texto-limpo;
 2. Divide o bloco em duas partes (R0 e L0);
 3. Aplica uma função f sobre R, aplica o xOR dela com L e obtém R1;
 4. O R0 transita para L1;
 5. O processo repete-se 'n' vezes;

Para decifrar:
 1. Recebe um bloco de texto-cifrado;
 2. Divide o bloco em duas partes (R0 e L0);
 3. Aplica uma função f sobre o L0, e aplica o xOR dela com o R0 e obtém o L1;
 4. O L0 transita para R1;
 5. O processo repete-se 'n' vezes;

Nota: Rackoff também refere que para uma PRP (Pseudo random permutations) ser **segura**, a rede de feistel tem de ser com pelo menos **três rondas**. O **DES** especifica 16 rondas, enqquanto que o **3DES** usa 48. O **AES** não usa redes de Feistel no seu núcleo.

## Algoritmos de cifra de bloco mais comuns
- DES (Data Encryption Standard): 64 bits de bloco, 56 bits de chave;
- DEA (Digital Encryption Algorithm): 64 bits de bloco, 128 bits de chave;
- AES (Advanced Encryption Standard): 128 bits de bloco, 128, 192 ou 256 bits de chave;
- Cipher Blowfish, RCS, etc.;

## Arquitetura AES (Advanced Encription Standard)
Funciona da seguinte forma:
 1. Divide o texto-limpo em blocos de 128 bits (16 bytes);
 2. É fornecida uma chave de cifragem;
 3. É calculado o **número de rodadas** dependendo do tamanho da chave (128 bits = 10 rondas, 192 bits = 12 rondas, 256 bits = 14 rondas);
 4. A chave é expandida em várias sub-chaves, uma para cada rodada;
 5. Após todas as rodadas é obtido o texto cifrado.

Em cada **rodada**:
 1. AddRoundKey: o bloco é combinado com uma sub-chave exclusiva daquela rodada usando o XOR, o resultado é uma matriz 4x4 (16 bytes);
 2. SubBytes: cada byte no bloco é substituído por outro byte de acordo com uma tabela de substituição (S-box);
 3. Shiftrows: as linhas no bloco são permutadas (movidas) para a esquerda, essas permutação podem variar (0,1,2 e 3);
 4. MixColumns: as colunas no bloco são permutadas;

# Prática 2

## Até ao Exercício 6.1
```py
import sys
import os
from cryptography.hazmat.primitives.kdf.pbkdf2 import PBKDF2HMAC
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
from cryptography.hazmat.primitives.padding import PKCS7
from cryptography.hazmat.backends import default_backend


def gerar_chave(password, salt):

    # Converter a senha em bytes
    password = password.encode()

    chave = PBKDF2HMAC(
        algorithm=hashes.SHA256(),
        length=16,  # 16 bytes = 128 bits
        salt=salt,
        iterations=100000,
    )

    return chave.derive(password)


def guardar_ficheiro(nome_ficheiro, dados):
    with open(nome_ficheiro, 'wb') as ficheiro:
        ficheiro.write(dados)


def ler_ficheiro(nome_ficheiro):
    with open(nome_ficheiro, 'rb') as ficheiro:
        return ficheiro.read()


def carregar_configuracao(nome_ficheiro):
    with open(nome_ficheiro, 'r') as ficheiro:
        return ficheiro.read()


def cifrar_ficheiro(modo, dados, chave, iv):
    if modo == "ECB":
        cifra = Cipher(algorithms.AES(chave), modes.ECB(), backend=default_backend())
    elif modo == "CBC":
        cifra = Cipher(algorithms.AES(chave), modes.CBC(iv), backend=default_backend())

    encriptador = cifra.encryptor()
    preenchedor = PKCS7(algorithms.AES.block_size).padder()

    dados_preenchidos = preenchedor.update(dados) + preenchedor.finalize()
    return encriptador.update(dados_preenchidos) + encriptador.finalize()


def decifrar_ficheiro(modo, dados, chave, iv):
    if modo == "ECB":
        cifra = Cipher(algorithms.AES(chave), modes.ECB())
    elif modo == "CBC":
        cifra = Cipher(algorithms.AES(chave), modes.CBC(iv))

    decifrador = cifra.decryptor()
    despreenchedor = PKCS7(algorithms.AES.block_size).unpadder()

    dados_decifrados = decifrador.update(dados) + decifrador.finalize()
    return despreenchedor.update(dados_decifrados) + despreenchedor.finalize()


if __name__ == "__main__":

    if len(sys.argv) != 3 or len(sys.argv) != 4:
        print("Uso: python3 main.py <ficheiro config> <conteudo> <palavra-passe>")
        sys.exit(1)

    ficheiro_config = sys.argv[1]
    nome_do_ficheiro = sys.argv[2]
    palavra_passe = sys.argv[3]

    config = carregar_configuracao(ficheiro_config)

    iv = None
    modo = config["mode"]

    if config["iv"] == "random":
        iv = os.urandom(16)  # 16 bytes aleatórios

    salt = b'\x00' * 16  # 16 bytes aleatórios
    chave = gerar_chave(palavra_passe, salt)

    conteudo = ler_ficheiro(nome_do_ficheiro)

    # Cifrar o conteúdo do ficheiro
    conteudo_cifrado = cifrar_ficheiro(modo, conteudo, chave, iv)
    guardar_ficheiro(nome_do_ficheiro + ".enc", conteudo_cifrado)

    lixo_conteudo = ler_ficheiro(nome_do_ficheiro + ".enc")

    # Decifrar o conteúdo do ficheiro
    conteudo_decifrado = decifrar_ficheiro(modo, lixo_conteudo, chave, iv)
    guardar_ficheiro(nome_do_ficheiro + ".dec", conteudo_decifrado)
```

## Exercício 6.2
Podemos verificar uma diferença de padrões entre o modo ECB e o modo CBC. No modo ECB, não tem o vetor de inicialização, logo, existe um padrão no conteúdo cifrado. No modo CBC, existe o vetor de inicialização, logo, os padrões não são tão visíveis.

```py
import sys
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives.padding import PKCS7
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.kdf.pbkdf2 import PBKDF2HMAC

# Cipher a BMP image using AES in ECB and CBC modes. (but kept the first 54 bytes untouched)

def gerar_chave(password, salt):

    # Converter a senha em bytes
    password = password.encode()

    chave = PBKDF2HMAC(
        algorithm=hashes.SHA256(),
        length=16,  # 16 bytes = 128 bits
        salt=salt,
        iterations=100000,
    )

    return chave.derive(password)


def open_image(path):
    with open(path, 'rb') as f:
        return f.read()

def save_image(path, data):
    with open(path, 'wb') as f:
        f.write(data)

def encrypt_image(image, cipher_mode, key, iv=b'0'*16):

    # Extract the header
    header = image[:54]

    # Extract the image data
    image = image[54:]

    # Pad the image data
    block_size = 16
    image = image + b'0'*(block_size - len(image) % block_size)

    if cipher_mode == "ecb":
        cipher = Cipher(algorithms.AES(key), modes.ECB(), backend=default_backend())
    elif cipher_mode == "cbc":
        cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())

    encryptor = cipher.encryptor()
    padder = PKCS7(128).padder()

    image_padded = padder.update(image) + padder.finalize()
    image_encrypted = encryptor.update(image_padded) + encryptor.finalize()

    return header + image_encrypted

if __name__ == "__main__":
    if len(sys.argv) != 5:
        print("Usage: python3 image.py <cipher mode> <input file> <output file> <password>")
        sys.exit(1)

    cipher_mode = sys.argv[1]
    input_file = sys.argv[2]
    output_file = sys.argv[3]
    password = sys.argv[4]


    salt = b'0'*16
    key = gerar_chave(password, salt)

    image = open_image(input_file)

    images_encrypted = encrypt_image(image, cipher_mode, key)

    save_image(output_file, images_encrypted)
```

## Exercício 6.3
Neste caso, modos como o CBC têm maior aleatoriadade no criptograma, logo a alteração de um bit no texto limpo, altera um maior número bits no criptograma.

## Exercício 7 (Implementação do DES)
A implementação do triple DES é bastante semelhante.
```c
#include <openssl/des.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define NUMBER_OF_BYTES 8

void cifraDES(char * nomeInput, char * chave, char * nomeOutput, int enc){

FILE * ficheiroInput = fopen(nomeInput, "rb");
FILE * ficheiroOutput = fopen(nomeOutput, "wb");

if(ficheiroInput == NULL || ficheiroOutput == NULL){
	fprintf(stderr,"Não foi possível criar/ler o ficheiro!\n");
	exit(0);
}


DES_cblock keyBlock;
DES_key_schedule schedule;

DES_cblock blockInput,blockOutput;

memcpy(&keyBlock,chave, NUMBER_OF_BYTES);

DES_set_odd_parity(&keyBlock);
DES_set_key_checked(&keyBlock, &schedule);

size_t bytesLidos;
while((bytesLidos = fread(&blockInput, 1, NUMBER_OF_BYTES, ficheiroInput)) == NUMBER_OF_BYTES){
	DES_ecb_encrypt(&blockInput,&blockOutput, &schedule, enc);
	fwrite(&blockOutput, 1, NUMBER_OF_BYTES, ficheiroOutput);
}

if(bytesLidos != 0){
	fwrite(&blockInput, 1, bytesLidos, ficheiroOutput);
}

fclose(ficheiroInput);
fclose(ficheiroOutput);

}


int main(int argc, char **argv){

if(argc != 5){
	fprintf(stderr,"Número de argumentos inválidos\n");
	exit(0);
}
char * flag = argv[1];
char * input = argv[2];
char * key = argv[3];
char * output = argv[4];

if(strcmp(flag,"-e") == 0){
	// Encriptar
	cifraDES(input,key,output,DES_ENCRYPT);
	printf("Ficheiro encriptado com sucesso!\n");
}else if(strcmp(flag,"-d") == 0){
	// Desencriptar
	cifraDES(input,key,output,DES_DECRYPT);
	printf("Ficheiro desencriptado com sucesso!\n");
}else {
	fprintf(stderr, "Flag inserida inválida\n");
}


return 0;
}
```
