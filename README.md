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
#include <string.h>

#define MAX 100

// Encryption using Rail Fence technique
void encrypt(char text[], int rails, char cipher[]) {
    char rail[MAX][MAX];
    int len = strlen(text);
    int row = 0, col = 0;
    int direction = 1;
    int k = 0;

    // Initialize matrix
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\0';

    // Place characters in rows
    for (int i = 0; i < len; i++) {
        rail[row][col++] = text[i];

        if (row == 0)
            direction = 1;
        else if (row == rails - 1)
            direction = -1;

        row += direction;
    }

    // Read row by row
    for (int i = 0; i < rails; i++) {
        for (int j = 0; j < len; j++) {
            if (rail[i][j] != '\0')
                cipher[k++] = rail[i][j];
        }
    }

    cipher[k] = '\0';
}

// Decryption
void decrypt(char cipher[], int rails, char text[]) {
    char rail[MAX][MAX];
    int len = strlen(cipher);
    int row = 0, col = 0;
    int direction = 1;
    int k = 0;

    // Initialize matrix
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\0';

    // Mark the positions
    for (int i = 0; i < len; i++) {
        rail[row][col++] = '*';

        if (row == 0)
            direction = 1;
        else if (row == rails - 1)
            direction = -1;

        row += direction;
    }

    // Fill marked positions with cipher text
    for (int i = 0; i < rails; i++) {
        for (int j = 0; j < len; j++) {
            if (rail[i][j] == '*')
                rail[i][j] = cipher[k++];
        }
    }

    // Read in zigzag order
    row = 0;
    col = 0;
    direction = 1;

    for (int i = 0; i < len; i++) {
        text[i] = rail[row][col++];

        if (row == 0)
            direction = 1;
        else if (row == rails - 1)
            direction = -1;

        row += direction;
    }

    text[len] = '\0';
}

int main() {
    char text[MAX], cipher[MAX], decrypted[MAX];
    int rails;

    printf("Enter the plaintext: ");
    fgets(text, MAX, stdin);

    // Remove newline
    text[strcspn(text, "\n")] = '\0';

    printf("Enter number of rows (rails): ");
    scanf("%d", &rails);

    if (rails < 2 || rails >= strlen(text)) {
        printf("Invalid number of rows.\n");
        return 1;
    }

    encrypt(text, rails, cipher);
    printf("\nEncrypted text: %s\n", cipher);

    decrypt(cipher, rails, decrypted);
    printf("Decrypted text: %s\n", decrypted);

    return 0;
}
```
# OUTPUT
<img width="470" height="180" alt="image" src="https://github.com/user-attachments/assets/1769e0c3-6674-43ec-8d26-9190f571d443" />

# RESULT
The implementation of rail fence transposition technique using c program is successful.
