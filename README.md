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
```python
import math

# Function to compute gcd
def gcd(a, b):
    while b:
        a, b = b, a % b
    return a

# Function to compute modular inverse
def mod_inverse(e, phi):
    for d in range(1, phi):
        if (e * d) % phi == 1:
            return d
    return None

# Step 1: Choose two prime numbers
p = int(input("Enter prime number p: "))
q = int(input("Enter prime number q: "))

# Step 2: Compute n and phi
n = p * q
phi = (p - 1) * (q - 1)

# Step 3: Choose public exponent e
e = int(input("Enter public exponent e: "))
if gcd(e, phi) != 1:
    print("e and phi(n) are not coprime. Restart and choose different e.")
    exit()

# Step 4: Compute private key d
d = mod_inverse(e, phi)
if d is None:
    print("Modular inverse not found. Restart.")
    exit()

print("\nPublic Key (e, n):", (e, n))
print("Private Key (d, n):", (d, n))

# Step 5: Encryption
message = int(input("\nEnter message (number form): "))
ciphertext = pow(message, e, n)
print("Encrypted message:", ciphertext)

# Step 6: Decryption
decrypted_message = pow(ciphertext, d, n)
print("Decrypted message:", decrypted_message)
```

## Output:

<img width="1231" height="878" alt="Screenshot 2026-02-23 153800" src="https://github.com/user-attachments/assets/4d814614-4900-4d55-995d-4f6a04700c66" />


## Result:
 The program is executed successfully.
