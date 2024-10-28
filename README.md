# EX-4-ADVANCED-ENCRYPTION-STANDARD-DES-ALGORITHM

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
typedef uint64_t DES_Block;
DES_Block initial_permutation(DES_Block block) {
return block;
}
DES_Block final_permutation(DES_Block block) {
return block;
}
DES_Block feistel_function(DES_Block right_half, DES_Block subkey) {
return right_half ^ subkey;
}
DES_Block des_encrypt(DES_Block plaintext, DES_Block key) {
DES_Block permuted_block = initial_permutation(plaintext);
DES_Block left = permuted_block >> 32;
DES_Block right = permuted_block & 0xFFFFFFFF;
for (int round = 0; round < 16; round++) {
DES_Block temp = right;
right = left ^ feistel_function(right, key);
left = temp;
}
DES_Block pre_output = (right << 32) | left;
DES_Block ciphertext = final_permutation(pre_output);
return ciphertext;
}
DES_Block des_decrypt(DES_Block ciphertext, DES_Block key) {
return des_encrypt(ciphertext, key);
}
void process_url_encryption(const char* url, DES_Block key) {
size_t len = strlen(url);
size_t blocks = len / 8;
if (len % 8 != 0) blocks++;
for (size_t i = 0; i < blocks; i++) {
DES_Block plaintext = 0;
char chunk[9] = {0}; // Only need 8 characters for each block, plus null
terminator for safety
strncpy(chunk, url + i * 8, 8); // Copy 8 characters to chunk
memcpy(&plaintext, chunk, 8); // Copy only 8 bytes into plaintext
DES_Block ciphertext = des_encrypt(plaintext, key);
printf("Block %zu Encrypted: %lX\n", i, ciphertext);
DES_Block decrypted = des_decrypt(ciphertext, key);
// Copy decrypted block back into a string for printing
char decrypted_chunk[9] = {0}; // Need 9 chars (8 bytes + null
terminator)
memcpy(decrypted_chunk, &decrypted, 8); // Copy back 8 bytes
printf("Block %zu Decrypted: %s\n", i, decrypted_chunk);
}
}
int main() {
printf("**************DES**************\n");
const char* url = "https://shanmathi.com";
DES_Block key = 0x133457799BBCDFF1;
printf("Encrypting URL: %s\n", url);
process_url_encryption(url, key);
return 0;
}
```

## OUTPUT:

![image](https://github.com/user-attachments/assets/3ceddff7-b78d-4f75-a1a4-017680ee9964)


## RESULT: 
Thus Data Encryption Standard (DES) Algorithm has been successfully excecuted
