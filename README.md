# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
int modular_exponentiation(int base, int exp, int mod) {
    int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}
int main() {
    int p, g, x, k, M;
    int y, C1, C2, decrypted_message;

    printf("Enter a prime number p: ");
    scanf("%d", &p);
    printf("Enter a primitive root g of p: ");
    scanf("%d", &g);
    printf("Enter the private key x: ");
    scanf("%d", &x);

    y = modular_exponentiation(g, x, p);
    printf("Public key y: %d\n", y);

    printf("Enter the message (integer) to encrypt: ");
    scanf("%d", &M);
    printf("Enter a random integer k: ");
    scanf("%d", &k);

    C1 = modular_exponentiation(g, k, p);
    C2 = (M * modular_exponentiation(y, k, p)) % p;
    printf("Encrypted message: (C1, C2) = (%d, %d)\n", C1, C2);

    decrypted_message = (C2 * modular_exponentiation(C1, p - 1 - x, p)) % p;
    printf("Decrypted message: %d\n", decrypted_message);

    return 0;
}
```
## Output:
![ex 12](https://github.com/user-attachments/assets/b7398d60-f26e-4118-942b-2aa53346789a)
## Result:
The program is executed successfully.
