<h1 style='text-align:center'>Public Key Cryptography</h1>

# Key Exchange for Symmetric Encryption

Symmetric encryption is efficient for secure communication but requires both parties to share a secret key. A common use of **asymmetric cryptography** is to securely exchange keys for symmetric encryption. Since asymmetric encryption is slower, it’s typically used only for the initial exchange of keys and negotiation of encryption parameters.

### Box with a Lock Analogy

Imagine this scenario:

1. **You have a secret code** (the symmetric encryption cipher and key) and **instructions** for using it.
2. To send the instructions securely to your friend, you ask them for a **lock**.
   - This lock can only be opened with a **key** your friend keeps.
3. You place the instructions in an **indestructible box**, secure it with their lock, and send it to them.
4. When the box arrives, your friend uses their **key** to unlock it and retrieve the instructions.
5. Now, you and your friend can communicate securely using the secret code.

### Cryptographic Metaphor

| **Analogy** | **Cryptographic System**            |
| ----------- | ----------------------------------- |
| Secret Code | Symmetric Encryption Cipher and Key |
| Lock        | Public Key                          |
| Lock’s Key  | Private Key                         |

In this system:

- The **lock** (public key) is freely shared, allowing anyone to secure a message.
- Only the **key** (private key) can unlock the box, ensuring only the intended recipient can access the message.

This process allows the use of **asymmetric encryption** for the key exchange. Once the symmetric key is securely shared, the faster symmetric encryption can be used for ongoing communication.

## Real-World Implementation

In real-world applications, additional cryptographic tools are required to verify the identity of the communicating parties. These tools include:

- **Digital Signatures**: Ensure the message sender is authentic.
- **Certificates**: Verify the legitimacy of the public key and its owner.

# RSA: The Basics of Secure Communication and CTF Challenges

RSA is a public-key encryption algorithm that ensures secure data transmission over insecure channels, even in the presence of eavesdroppers. The security of RSA is rooted in the mathematical difficulty of **factoring large numbers**.

---

## The Math That Makes RSA Secure

### Factoring Large Numbers

RSA relies on the computational disparity between multiplying two large prime numbers and factoring their product. While multiplication is straightforward, factoring is computationally expensive, especially with very large numbers.

**Example:**

- Prime 1: \( 982451653031 \)
- Prime 2: \( 169743212279 \)
- Product: \( 166764499494295486767649 \)

Multiplying the primes is simple. However, finding these prime factors from the product is significantly harder. Modern RSA implementations use primes with **hundreds of digits**, making the factoring process infeasible for attackers.

---

## RSA Encryption and Decryption

RSA uses two keys:

- **Public Key** \((n, e)\): Used for encryption and shared openly.
- **Private Key** \((n, d)\): Used for decryption and kept secret.

### Example Calculation

Bob sets up RSA encryption:

1. **Choose primes**: \( p = 157 \), \( q = 199 \)
2. **Calculate \( n \)**: \( n = p \times q = 31243 \)
3. **Compute \( \phi(n) \)**:
   \[
   \phi(n) = (p-1) \times (q-1) = 31243 - 157 - 199 + 1 = 30888
   \]
4. **Select \( e \)**: \( e = 163 \), where \( \gcd(e, \phi(n)) = 1 \)
5. **Find \( d \)**: \( d \) satisfies \( (e \times d) \mod \phi(n) = 1 \)
   - \( d = 379 \), since \( 163 \times 379 \mod 30888 = 1 \)

- **Public Key**: \( (n, e) = (31243, 163) \)
- **Private Key**: \( (n, d) = (31243, 379) \)

**Encrypting a message \( x = 13 \):**
\[
y = x^e \mod n = 13^{163} \mod 31243 = 16341
\]

**Decrypting \( y = 16341 \):**
\[
x = y^d \mod n = 16341^{379} \mod 31243 = 13
\]

---

## RSA in CTF Challenges

Cryptographic challenges in CTFs often involve manipulating RSA variables to break encryption. Knowing the key variables is critical:

- **Primes**:
  - \( p \), \( q \): Large primes
- **Derived values**:
  - \( n = p \times q \): Modulus
  - \( \phi(n) = (p-1) \times (q-1) \): Euler's totient function
- **Keys**:
  - Public Key: \( (n, e) \)
  - Private Key: \( (n, d) \)
- **Message representations**:
  - \( m \): Original plaintext message
  - \( c \): Encrypted ciphertext

### Tools for CTFs

- **[RsaCtfTool](https://github.com/Ganapati/RsaCtfTool)**: Automates attacks on weak RSA implementations.
- **[rsatool](https://github.com/ius/rsatool)**: Helps generate RSA keys or exploit vulnerabilities.

---

## Key Takeaways

- RSA depends on the difficulty of factoring large numbers.
- Encryption and decryption are achieved using public and private keys, respectively.
- CTF challenges often exploit weak RSA setups or provide partial information to crack RSA encryption.

By understanding the math and tools available, you can effectively tackle RSA challenges in cryptography competitions.

# Diffie-Hellman Key Exchange and RSA: Complementary Roles in Secure Communication

The **Diffie-Hellman Key Exchange** and **RSA** address distinct challenges in secure communication, often working together to ensure both confidentiality and authenticity.

---

## Key Exchange Challenge

The **Diffie-Hellman Key Exchange** provides a method for securely establishing a shared secret key over an insecure channel. This shared key can then be used for symmetric encryption. The process ensures that even if an attacker intercepts all public values and exchanged data, they cannot determine the shared secret without solving the discrete logarithm problem—a computationally hard task with large numbers.

---

## How Diffie-Hellman Works: Numerical Example

1. **Public Values**:

   - A large prime number \( p \): \( 29 \)
   - A generator \( g \): \( 3 \)

2. **Private Keys**:

   - Alice's private key \( a \): \( 13 \)
   - Bob's private key \( b \): \( 15 \)

3. **Calculate Public Keys**:

   - Alice calculates:
     \[
     A = g^a \mod p = 3^{13} \mod 29 = 19
     \]
   - Bob calculates:
     \[
     B = g^b \mod p = 3^{15} \mod 29 = 26
     \]

4. **Exchange Public Keys**:

   - Alice sends \( A = 19 \) to Bob.
   - Bob sends \( B = 26 \) to Alice.

5. **Calculate the Shared Secret**:
   - Alice calculates:
     \[
     S = B^a \mod p = 26^{13} \mod 29 = 10
     \]
   - Bob calculates:
     \[
     S = A^b \mod p = 19^{15} \mod 29 = 10
     \]
   - Both arrive at the same shared secret: \( S = 10 \).

---

## Security Context

The above example uses small numbers for simplicity and is not secure. In real-world applications:

- \( p \) is a 2048-bit or larger prime number.
- The discrete logarithm problem with such large values is computationally infeasible, ensuring the secrecy of the shared key.

---

## Combining Diffie-Hellman and RSA

1. **Key Agreement (Diffie-Hellman)**:

   - Used to establish a shared symmetric key over an insecure channel without directly sharing the key.

2. **Authentication and Integrity (RSA)**:
   - Provides identity verification using digital signatures to prevent man-in-the-middle attacks.
   - Enables secure sharing of public keys.

---

## Practical Applications

Diffie-Hellman and RSA are often combined in protocols like TLS (Transport Layer Security):

- **RSA**: Used for authentication and initial key exchange.
- **Diffie-Hellman**: Ensures forward secrecy by generating unique session keys for each communication.

---

In summary, the **Diffie-Hellman Key Exchange** secures the sharing of symmetric keys, while **RSA** ensures robust identity verification and encrypted key distribution. Together, they form the backbone of modern secure communication protocols.
