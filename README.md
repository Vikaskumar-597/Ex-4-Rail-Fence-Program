# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Function declarations                                   
void railfence_encipher(int key,
    const char * plaintext, char * ciphertext);
void railfence_decipher(int key,
    const char * ciphertext, char * plaintext);

int main() {
    // The message to encipher and decipher
    char * plaintext[256];
    int key;
   
    fgets(plaintext, sizeof(plaintext), stdin);
    plaintext[strcspn(plaintext, "\n")] = '\0';
    scanf("%d", &key);

    // Allocate memory for results
    char * ciphertext = malloc(strlen(plaintext) + 1);
    char * result = malloc(strlen(plaintext) + 1);

    // Encrypt and decrypt
    railfence_encipher(key, plaintext, ciphertext);
    railfence_decipher(key, ciphertext, result);

    // Show results
    printf("Original text : %s\n", plaintext);
    printf("Encrypted text: %s\n", ciphertext);
    printf("Decrypted text: %s\n", result);
    // Free memory
    free(ciphertext);
    free(result);

    return 0;
}

void railfence_encipher(int key, const char * plaintext, char * ciphertext) {
    int len = strlen(plaintext);
    int l, i, j = 0, k, skip;

    for (l = 0; l < key - 1; l++) {
        skip = 2 * (key - l - 1);
        k = 0;
        for (i = l; i < len;) {
            ciphertext[j++] = plaintext[i];

            if (l == 0 || k % 2 == 0)
                i += skip;
            else
                i += 2 * (key - 1) - skip;

            k++;
        }
    }

    // Last row (bottom rail)
    for (i = l; i < len; i += 2 * (key - 1))
        ciphertext[j++] = plaintext[i];

    ciphertext[j] = '\0'; // Null-terminate
}

void railfence_decipher(int key, const char * ciphertext, char * plaintext) {
    int len = strlen(ciphertext);
    int l, i, j, k = 0, skip;

    for (l = 0; l < key - 1; l++) {
        skip = 2 * (key - l - 1);
        j = 0;
        for (i = l; i < len;) {
            plaintext[i] = ciphertext[k++];

            if (l == 0 || j % 2 == 0)
                i += skip;
            else
                i += 2 * (key - 1) - skip;

            j++;
        }
    }

    // Last row
    for (i = l; i < len; i += 2 * (key - 1))
        plaintext[i] = ciphertext[k++];

    plaintext[len] = '\0'; // Null-terminate
}
```
# OUTPUT
<img width="445" height="271" alt="image" src="https://github.com/user-attachments/assets/9ec5b92a-2c32-467e-839f-a13a6d74d7d7" />


# RESULT
Thus the rail fence cipher is executed successfully.
