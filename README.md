# HILL CIPHER
## Name : Raghu Ram VR
## Reg No : 212224220075
## Date : 30/01/2026
## EX. NO: 3 
IMPLEMENTATION OF HILL CIPHER
## AIM:
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#define SIZE 100
int keymat[3][3] = { {1, 2, 1}, {2, 3, 2}, {2, 2, 1} };
int invkeymat[3][3] = { {-1, 0, 1}, {2, -1, 0}, {-2, 2, -1} };
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
void toUpperCase(char str[]) {
for (int i = 0; str[i] != '\0'; i++) {
if (islower(str[i])) {
str[i] = toupper(str[i]);
}
}
}
void padMessage(char msg[]) {
int n = strlen(msg) % 3;
if (n != 0) {
for (int i = 0; i < (3 - n); i++) {
strcat(msg, "X");
}
}
}
void encode(char a, char b, char c, char ret[]) {
int posa = a - 'A';
int posb = b - 'A';
int posc = c - 'A';
int x = (posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0]) % 26;
int y = (posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1]) % 26;
int z = (posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2]) % 26;
ret[0] = key[x];
ret[1] = key[y];
ret[2] = key[z];
ret[3] = '\0';
}
void decode(char a, char b, char c, char ret[]) {
int posa = a - 'A';
int posb = b - 'A';
int posc = c - 'A';
int x = (posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0]) % 26;
int y = (posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1]) % 26;
int z = (posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2]) % 26;
ret[0] = key[(x < 0) ? (26 + x) : x];
ret[1] = key[(y < 0) ? (26 + y) : y];
ret[2] = key[(z < 0) ? (26 + z) : z];
ret[3] = '\0';
}
int main() {
char msg[SIZE], enc[SIZE] = "", dec[SIZE] = "";
printf("Enter the message: ");
fgets(msg, SIZE, stdin);
msg[strcspn(msg, "\n")] = 0;
toUpperCase(msg);
padMessage(msg);
printf("Padded message: %s\n", msg);
for (int i = 0; i < strlen(msg); i += 3) {
char encBlock[4];
encode(msg[i], msg[i + 1], msg[i + 2], encBlock);
strcat(enc, encBlock);
}
printf("Encoded message: %s\n", enc);
for (int i = 0; i < strlen(enc); i += 3) {
char decBlock[4];
decode(enc[i], enc[i + 1], enc[i + 2], decBlock);
strcat(dec, decBlock);
}
printf("Decoded message: %s\n", dec);
return 0;
}
```
## OUTPUT
<img width="1430" height="722" alt="image" src="https://github.com/user-attachments/assets/c0e1de9d-44e9-449e-899c-d22551818ddc" />


## RESULT
The Program Hill Cipher executed succesfully
