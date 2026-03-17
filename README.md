# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:

Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```C
#include <stdio.h>

// Function to compute (base^exp) % mod
long long power(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;

    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;

        exp = exp / 2;
        base = (base * base) % mod;
    }
    return result;
}

// Function to find GCD
long long gcd(long long a, long long b) {
    while (b != 0) {
        long long temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Function to find modular inverse of e
long long modInverse(long long e, long long phi) {
    long long d = 1;
    while ((d * e) % phi != 1)
        d++;
    return d;
}

int main() {
    long long p, q, n, phi, e, d;
    long long msg, cipher, decrypted;

    // Input primes
    printf("Enter prime number p: ");
    scanf("%lld", &p);

    printf("Enter prime number q: ");
    scanf("%lld", &q);

    // Calculate n and phi
    n = p * q;
    phi = (p - 1) * (q - 1);

    // Choose e
    printf("Enter public exponent e: ");
    scanf("%lld", &e);

    // Check if e is valid
    if (gcd(e, phi) != 1) {
        printf("Invalid e! It must be coprime with phi.\n");
        return 0;
    }

    // Compute private key d
    d = modInverse(e, phi);

    printf("\nPublic Key (e, n): (%lld, %lld)\n", e, n);
    printf("Private Key (d, n): (%lld, %lld)\n", d, n);

    // Input message
    printf("\nEnter message (integer < n): ");
    scanf("%lld", &msg);

    // Encryption
    cipher = power(msg, e, n);
    printf("Encrypted Message: %lld\n", cipher);

    // Decryption
    decrypted = power(cipher, d, n);
    printf("Decrypted Message: %lld\n", decrypted);

    return 0;
}
```

## Output:
<img width="1228" height="892" alt="Screenshot 2026-03-17 144617" src="https://github.com/user-attachments/assets/9b4a0f4f-6bf4-4583-972f-b0e6cc461a2f" />


## Result:
 The program is executed successfully.
