# Ex-7 -Implement-DES-Encryption-and-Decryption
## AIM:
To write a program to implement Data EncrypƟon Standard (DES).

## ENCRYPTION OF DES:
## ALGORITHM FOR ENCRYPTION(DES):

STEP-1: Read the 64-bit plain text.
STEP-2: Split it into two 32-bit blocks and store it in two different arrays.
STEP-3: Perform XOR operaƟon between these two arrays.
STEP-4: The output obtained is stored as the second 32-bit sequence and the
original second 32-bit sequence forms the first part.
STEP-5: Thus the encrypted 64-bit cipher text is obtained in this way. Repeat
the same process for the remaining plain text characters.
## PROGRAM FOR ENCRYPTION(DES):
```

#include <stdio.h>
#include <string.h>
#include <stdint.h>
uint64_t stringToBinary(const char *str) {
uint64_t binary = 0;
for (int i = 0; i < 8 && str[i] != '\0'; ++i) {
binary <<= 8;
binary |= (uint64_t)str[i];
}
return binary;
}
uint32_t XOR(uint32_t a, uint32_t b) {
return a ^ b;
}
uint64_t encryptDES(uint64_t plainText) {
uint32_t leŌ = (plainText >> 32) & 0xFFFFFFFF;
uint32_t right = plainText & 0xFFFFFFFF;
uint32_t xorResult = XOR(leŌ, right);
uint64_t cipherText = 0;
cipherText = ((uint64_t)right << 32) | xorResult;
return cipherText;
}
int main() {
char plainText[9];
printf("\n *****DES ALGORITHM ENCRYPTION******\n\n");
printf("\n Enter an 8-character plaintext(DES): ");
fgets(plainText, sizeof(plainText), stdin);
plainText[strcspn(plainText, "\n")] = 0;
uint64_t binaryPlainText = stringToBinary(plainText);
uint64_t cipherText = encryptDES(binaryPlainText);
printf(" \n Encrypted Cipher Text in hex(DES): %016llX\n",cipherText);
return 0;
}

```
## OUTPUT FOR ENCRPTION(DES):

![Screenshot 2024-10-14 090710](https://github.com/user-attachments/assets/681e7d8e-7f20-4f99-87ff-364ace15d88e)

## DECRYPTION OF DES:

## ALGORITHM FOR DECRYPTION(DES):
STEP 1: Split the 64-bit cipher text into two 32-bit blocks.
STEP 2: Perform XOR operaƟon to retrieve the original leŌ block.
STEP 3: Combine the two 32-bit blocks to recreate the plaintext.
STEP 4: Convert the 64-bit binary plaintext back to a string.
STEP 5:Thus the decrypted plaintext is obtained in this way. Repeat the same
process for the remaining plain text characters.

## PROGRAM FOR DECRYPTION(DES):
```
#include <stdio.h>
#include <stdint.h>
#include <string.h>
// FuncƟon to convert 64-bit binary back to a string
void binaryToString(uint64_t binary, char *str) {
for (int i = 7; i >= 0; --i) {
str[i] = (char)(binary & 0xFF);
binary >>= 8;
}
str[8] = '\0'; // Null-terminate the string
}
// XOR funcƟon for 32-bit blocks
uint32_t XOR(uint32_t a, uint32_t b) {
return a ^ b;
}
uint64_t decryptDES(uint64_t cipherText) {
uint32_t right = (cipherText >> 32) & 0xFFFFFFFF;
uint32_t xorResult = cipherText & 0xFFFFFFFF;
uint32_t leŌ = XOR(right, xorResult);
uint64_t plainText = 0;
plainText = ((uint64_t)leŌ << 32) | right;
return plainText;
}

int main() {
uint64_t cipherText;
printf("\n\n\n ****DES ALGORITHM DECRYPTION***\n\n\n");
printf(" Enter the encrypted cipher text in hex(DES): ");
scanf("%llx", &cipherText);
// Decrypt the ciphertext back to binary plaintext

uint64_t decryptedBinary = decryptDES(cipherText);
// Convert binary plaintext back to string
char decryptedText[9];
binaryToString(decryptedBinary, decryptedText);
printf("\n Decrypted Text(DES): %s\n", decryptedText);
return 0;
}
```

## OUTPUT FOR DECRPTION(DES):
![Screenshot 2024-10-14 090723](https://github.com/user-attachments/assets/ac3e9c80-1984-4817-b630-bed8d4b3784d)


## RESULT:

Thus the data encrypƟon standard algorithm had been implemented
successfully.
