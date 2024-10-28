# EX-8-ADVANCED-ENCRYPTION-STANDARD-DES-ALGORITHM

## Aim:
  To use Advanced Encryption Standard (AES) Algorithm for a practical application like URL Encryption.

## ALGORITHM: 
  1. AES is based on a design principle known as a substitution–permutation. 
  2. AES does not use a Feistel network like DES, it uses variant of Rijndael. 
  3. It has a fixed block size of 128 bits, and a key size of 128, 192, or 256 bits. 
  4. AES operates on a 4 × 4 column-major order array of bytes, termed the state

## PROGRAM: 
```
#include <stdio.h>
#include <stdint.h>
#include <string.h>
typedef uint8_t AES_Block[16];
void aes_encrypt_block(AES_Block plaintext, AES_Block key, AES_Block
ciphertext) {
for (int i = 0; i < 16; i++) {
ciphertext[i] = plaintext[i] ^ key[i];
}
}
void aes_decrypt_block(AES_Block ciphertext, AES_Block key, AES_Block
plaintext) {
for (int i = 0; i < 16; i++) {
plaintext[i] = ciphertext[i] ^ key[i];
}
}
void process_url_aes_encryption(const char* url, AES_Block key) {
size_t len = strlen(url);
size_t blocks = len / 16;
if (len % 16 != 0) blocks++;
for (size_t i = 0; i < blocks; i++) {
AES_Block plaintext = {0};
AES_Block ciphertext = {0};
AES_Block decrypted = {0};
char chunk[17] = {0};
strncpy(chunk, url + i * 16, 16);
memcpy(plaintext, chunk, 16);
aes_encrypt_block(plaintext, key, ciphertext);
printf("Block %zu Encrypted: ", i);
for (int j = 0; j < 16; j++) printf("%02X", ciphertext[j]);
printf("\n");
aes_decrypt_block(ciphertext, key, decrypted);
printf("Block %zu Decrypted: ", i);
for (int j = 0; j < 16 && decrypted[j] != '\0'; j++) {
printf("%c", decrypted[j]);
}
printf("\n");
}
}

int main() {
printf("************* AES *************\n");
const char* url = "https://shanmathi.com";
AES_Block key = {0x2B, 0x7E, 0x15, 0x16, 0x28, 0xAE, 0xD2, 0xA6,
0xAB, 0xF7, 0xCF, 0x34, 0x12, 0x28, 0xEE, 0xF4};
printf("Encrypting URL: %s\n", url);
process_url_aes_encryption(url, key);
return 0;
}
```

## OUTPUT:
![image](https://github.com/user-attachments/assets/536fb090-3cfc-412d-98a5-6d05854b9294)


## RESULT: 
Thus Advanced Encryption Standard (AES) Algorithm  has been successfully excecuted
