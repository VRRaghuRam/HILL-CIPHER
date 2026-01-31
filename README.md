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

int mod26(int x) {
    return (x % 26 + 26) % 26;
}

int modInverse(int det) {
    det = mod26(det);
    for (int i = 1; i < 26; i++) {
        if ((det * i) % 26 == 1)
            return i;
    }
    return -1;
}

int determinant(int key[3][3]) {
    int det = 0;
    det = key[0][0] * (key[1][1]*key[2][2] - key[1][2]*key[2][1])
        - key[0][1] * (key[1][0]*key[2][2] - key[1][2]*key[2][0])
        + key[0][2] * (key[1][0]*key[2][1] - key[1][1]*key[2][0]);
    return mod26(det);
}

void adjoint(int key[3][3], int adj[3][3]) {
    adj[0][0] =  (key[1][1]*key[2][2] - key[1][2]*key[2][1]);
    adj[0][1] = -(key[1][0]*key[2][2] - key[1][2]*key[2][0]);
    adj[0][2] =  (key[1][0]*key[2][1] - key[1][1]*key[2][0]);

    adj[1][0] = -(key[0][1]*key[2][2] - key[0][2]*key[2][1]);
    adj[1][1] =  (key[0][0]*key[2][2] - key[0][2]*key[2][0]);
    adj[1][2] = -(key[0][0]*key[2][1] - key[0][1]*key[2][0]);

    adj[2][0] =  (key[0][1]*key[1][2] - key[0][2]*key[1][1]);
    adj[2][1] = -(key[0][0]*key[1][2] - key[0][2]*key[1][0]);
    adj[2][2] =  (key[0][0]*key[1][1] - key[0][1]*key[1][0]);
}

void inverseKey(int key[3][3], int invKey[3][3]) {
    int adj[3][3];
    adjoint(key, adj);

    int det = determinant(key);
    int detInv = modInverse(det);

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            invKey[i][j] = mod26(adj[j][i] * detInv);
}

int main() {
    char plaintext[100], ciphertext[100];
    int key[3][3], invKey[3][3];
    int i, j, len;

    printf("Enter plaintext: ");
    scanf("%s", plaintext);

    for (i = 0; plaintext[i]; i++)
        plaintext[i] = toupper(plaintext[i]);

    len = strlen(plaintext);

    while (len % 3 != 0) {
        plaintext[len++] = 'X';
    }
    plaintext[len] = '\0';

    printf("Enter 3x3 key matrix:\n");
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            scanf("%d", &key[i][j]);

    int detInv = modInverse(determinant(key));
    if (detInv == -1) {
        printf("Key matrix inverse does not exist!\n");
        return 0;
    }

    printf("\nEncrypted Text: ");
    for (i = 0; i < len; i += 3) {
        int p[3], c[3];

        for (j = 0; j < 3; j++)
            p[j] = plaintext[i + j] - 'A';

        for (j = 0; j < 3; j++) {
            c[j] = mod26(key[j][0]*p[0] + key[j][1]*p[1] + key[j][2]*p[2]);
            ciphertext[i + j] = c[j] + 'A';
            printf("%c", ciphertext[i + j]);
        }
    }
    ciphertext[len] = '\0';

    inverseKey(key, invKey);

    printf("\nDecrypted Text: ");
    for (i = 0; i < len; i += 3) {
        int c[3], p[3];

        for (j = 0; j < 3; j++)
            c[j] = ciphertext[i + j] - 'A';

        for (j = 0; j < 3; j++) {
            p[j] = mod26(invKey[j][0]*c[0] + invKey[j][1]*c[1] + invKey[j][2]*c[2]);
            printf("%c", p[j] + 'A');
        }
    }

    return 0;
}

```
## OUTPUT
<img width="1516" height="843" alt="image" src="https://github.com/user-attachments/assets/a1c2c373-807f-408a-b0de-f7332762ced3" />



## RESULT
The Program Hill Cipher executed succesfully
