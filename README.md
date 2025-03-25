# Text-Encryption-C
#include <stdio.h>
#include <string.h>

// Function to encrypt text using XOR
void encrypt(char text[], char key) {
    for (int i = 0; i < strlen(text); i++) {
        text[i] = text[i] ^ key;  // XOR operation
    }
}

// Function to decrypt text (XOR works both ways)
void decrypt(char text[], char key) {
    encrypt(text, key);  // XOR again restores the original text
}

// Function to save encrypted text to a file
void saveToFile(const char *filename, char text[]) {
    FILE *file = fopen(filename, "w");
    if (file == NULL) {
        printf("❌ Error opening file!\n");
        return;
    }
    fprintf(file, "%s", text);
    fclose(file);
    printf("✅ Encrypted text saved to: %s\n", filename);
}

int main() {
    char message[256];
    char key;

    printf("🔐 Enter the text to encrypt: ");
    fgets(message, sizeof(message), stdin);  // Read full text

    // Remove newline character if exists
    size_t len = strlen(message);
    if (len > 0 && message[len - 1] == '\n') {
        message[len - 1] = '\0';
    }

    printf("🔑 Enter the encryption key (single character): ");
    scanf(" %c", &key);

    // Encrypt the text
    encrypt(message, key);
    printf("🔒 Encrypted text: %s\n", message);

    // Save to file
    saveToFile("encrypted.txt", message);

    // Decrypt and display the original text
    decrypt(message, key);
    printf("🔓 Decrypted text: %s\n", message);

    return 0;
}
