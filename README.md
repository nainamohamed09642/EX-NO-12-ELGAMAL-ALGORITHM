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
int main() { 
int p, g, bob_private_key, message, k; 
printf("Enter a prime number (p): "); 
scanf("%d", &p); 
printf("Enter a primitive root modulo p (g): "); 
scanf("%d", &g); 
printf("Bob's private key (x): "); 
scanf("%d", &bob_private_key); 
int bob_public_key = 1; 
int base = g; 
int exp = bob_private_key; 
int mod = p; 
while (exp > 0) { 
if (exp % 2 == 1) { 
            bob_public_key = (bob_public_key * base) % mod; 
        } 
        base = (base * base) % mod; 
        exp = exp / 2; 
    } 
     
    printf("Bob's public key (y): %d\n", bob_public_key); 
 
    printf("Alice, enter the message (M) you want to send: "); 
    scanf("%d", &message); 
 
    printf("Alice's private key (k): "); 
    scanf("%d", &k); 
 
    int c1 = 1;  // c1 = g^k % p 
    int c2 = 0;  // c2 = M * y^k % p 
 
    // Compute c1 = g^k % p 
    base = g; 
    exp = k; 
    mod = p; 
     
    while (exp > 0) { 
        if (exp % 2 == 1) { 
            c1 = (c1 * base) % mod; 
        } 
        base = (base * base) % mod; 
        exp = exp / 2; 
    } 
 
    int yk = 1; 
    base = bob_public_key; 
    exp = k; 
    mod = p; 
     
    while (exp > 0) { 
        if (exp % 2 == 1) { 
            yk = (yk * base) % mod; 
        } 
        base = (base * base) % mod; 
        exp = exp / 2; 
    } 
 
    // Compute c2 = M * y^k % p 
    c2 = (message * yk) % p; 
     
    printf("Alice sends encrypted message (c1, c2): (%d, %d)\n", c1, c2); 
 
    int s = 1;  // s = c1^x % p 
 
    // Compute s = c1^x % p 
    base = c1; 
    exp = bob_private_key; 
    mod = p; 
     
    while (exp > 0) { 
        if (exp % 2 == 1) { 
            s = (s * base) % mod; 
        } 
        base = (base * base) % mod; 
        exp = exp / 2; 
    } 
 
    int s_inv = 1; 
    int s_temp = s; 
    int p_temp = p; 
    int t, q; 
    int x0 = 0, x1 = 1; 
 
    while (s_temp > 1) { 
        q = s_temp / p_temp; 
        t = p_temp; 
        p_temp = s_temp % p_temp, s_temp = t; 
        t = x0; 
        x0 = x1 - q * x0; 
x1 = t; 
} 
if (x1 < 0) { 
x1 += p; 
} 
s_inv = x1; 
// Bob decrypts the message: M = c2 * s_inv % p 
int decrypted_message = (c2 * s_inv) % p; 
printf("Bob decrypts the message: %d\n", decrypted_message); 
return 0; 
}
```


## Output:
<img width="743" height="191" alt="image" src="https://github.com/user-attachments/assets/17c38172-c41e-4bcd-b333-ecfcfbdd42cf" />


## Result:
The program is executed successfully.
