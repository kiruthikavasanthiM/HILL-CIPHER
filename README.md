# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
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
```#include <stdio.h>
#include <string.h>
#include <ctype.h>

int key[3][3] = {
    {1, 2, 1},
    {2, 3, 2},
    {2, 2, 1}
};

int inv[3][3] = {
    {23, 0, 1},
    {2, 25, 0},
    {24, 2, 25}
};

void cipher(char *in, char *out, int mat[3][3]) {
    int p[3], x;

    for (int i = 0; i < 3; i++)
        p[i] = in[i] - 'A';

    for (int i = 0; i < 3; i++) {
        x = 0;
        for (int j = 0; j < 3; j++)
            x += p[j] * mat[i][j];

        out[i] = (x % 26 + 26) % 26 + 'A';
    }
    out[3] = '\0';
}

int main() {
    char msg[1000] = "VELAN";
    char enc[1000] = "", dec[1000] = "";
    char temp[4];

    printf("Hill Cipher\n");
    printf("Input message: %s\n", msg);

    int n = strlen(msg);

    for (int i = 0; i < n; i++)
        msg[i] = toupper((unsigned char)msg[i]);

    while (n % 3 != 0)
        msg[n++] = 'X';

    msg[n] = '\0';

    printf("Padded message: %s\n", msg);

    for (int i = 0; i < n; i += 3) {
        cipher(msg + i, temp, key);
        strcat(enc, temp);
    }

    printf("Encoded message: %s\n", enc);

    for (int i = 0; i < n; i += 3) {
        cipher(enc + i, temp, inv);
        strcat(dec, temp);
    }

    printf("Decoded message: %s\n", dec);

    return 0;
}
```

## OUTPUT
```
Hill Cipher
Input message: KIRUTHIKA
Padded message: KIRUTHIKAX
Encoded message: HZJQZV
Decoded message: KIRUTHIKAX
```

## RESULT
Thus, the Hill Cipher encryption and decryption program was implemented and executed successfully using C language.
