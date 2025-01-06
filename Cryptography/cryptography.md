# Cryptography Notes

## Purpose of Cryptography

- **Ultimate Goal**: Ensure secure communication in the presence of adversaries.
- **Key Objectives**:
  - **Confidentiality**: Prevent unauthorized access to data.
  - **Integrity**: Ensure the data remains unchanged and accurate.
  - **Authenticity**: Verify the origin of data.

## Definition of Cryptography

- The practice and study of techniques for secure communication and data protection in adversarial environments.
- Adversaries should not be able to:
  - Disclose the contents of messages.
  - Alter the contents of messages.

## Everyday Use of Cryptography

You encounter cryptography daily, often without realizing it. Examples include:

### Secure Login

- Credentials are encrypted and transmitted securely (e.g., logging into TryHackMe).

### Secure Remote Connections

- SSH creates an encrypted tunnel, preventing eavesdropping during sessions.

### Online Banking

- Browsers verify server certificates to ensure communication with legitimate servers.

### File Verification

- Hash functions confirm downloaded files match the original ones.

## Cryptography in Compliance Standards

Cryptography underpins several compliance standards across industries:

### Payment Card Industry

- **Standard**: PCI DSS (Payment Card Industry Data Security Standard).
- **Requirements**:
  - Encrypt data at rest (stored) and in motion (transmitted).

### Healthcare Records

- **Examples of Regulations**:
  - **USA**: HIPAA, HITECH.
  - **EU**: GDPR.
  - **UK**: DPA.
- **Key Points**:
  - Standards vary by country.
  - Emphasize data protection and encryption requirements.

## Summary

Cryptography is essential in securing data and ensuring compliance with various regulations. Although it operates behind the scenes, its impact is pervasive across digital interactions and legal standards.

# Introduction to Encryption and Key Terms

## Illustration of Encryption and Decryption

- **Plaintext**: The original, readable data. Examples:
  - A simple "hello"
  - A cat photo
  - Credit card information
  - Medical health records
- **Encryption Function**:
  - Converts plaintext into ciphertext using a cipher and a key.
  - **Input**: Plaintext + Key
  - **Output**: Ciphertext
- **Decryption Function**:
  - Converts ciphertext back into plaintext using the same cipher and key.
  - **Input**: Ciphertext + Key
  - **Output**: Plaintext

The process can be summarized as follows:

1. **Encryption**: Plaintext → [Cipher + Key] → Ciphertext
2. **Decryption**: Ciphertext → [Cipher + Key] → Plaintext

---

## Key Terms in Cryptography

### 1. Plaintext

- **Definition**: The original, readable message or data before encryption.
- **Examples**: Documents, images, multimedia files, or binary data.

### 2. Ciphertext

- **Definition**: The scrambled, unreadable version of the message after encryption.
- **Key Point**: No information about the original plaintext can be derived, except its approximate size.

### 3. Cipher

- **Definition**: An algorithm or method used to:
  - Convert plaintext into ciphertext.
  - Convert ciphertext back into plaintext.
- **Development**: Typically designed by mathematicians.

### 4. Key

- **Definition**: A string of bits used by the cipher to encrypt or decrypt data.
- **Key Points**:
  - The cipher is generally public knowledge.
  - The key must remain secret unless it is the public key in asymmetric encryption (to be discussed later).

### 5. Encryption

- **Definition**: The process of converting plaintext into ciphertext.
- **Key Points**:
  - Uses a cipher and a key.
  - The choice of cipher is usually disclosed.

### 6. Decryption

- **Definition**: The reverse process of encryption, converting ciphertext back into plaintext.
- **Key Points**:
  - Uses the same cipher and key.
  - Without the key, recovering the plaintext should be infeasible.

---

# The History of Cryptography and the Caesar Cipher

Cryptography has a rich history, with origins tracing back to ancient Egypt in 1900 BCE. Among the simplest and most famous historical ciphers is the **Caesar Cipher**, dating back to the first century BCE.

---

## The Caesar Cipher: How It Works

### Encryption

1. **Process**: Shift each letter by a fixed number of positions in the alphabet.
2. **Example**:
   - **Plaintext**: `TRYHACKME`
   - **Key**: `3` (right shift by 3)
   - **Cipher**: Caesar Cipher
   - **Resulting Ciphertext**: `WUBKDFNPH`
   - Explanation:
     - `T → W`, `R → U`, `Y → B`, etc.
     - After reaching `Z`, the shift starts back at `A`.

### Decryption

1. **Process**: Shift each letter in the opposite direction (left shift by the same key).
2. **Example**:
   - **Ciphertext**: `WUBKDFNPH`
   - **Key**: `3`
   - **Cipher**: Caesar Cipher
   - **Recovered Plaintext**: `TRYHACKME`

---

## Caesar Cipher's Weaknesses

1. **Limited Keyspace**:
   - The English alphabet has 26 letters.
   - A shift of 26 leaves the letters unchanged.
   - Only **25 valid keys** exist for encryption.
2. **Brute Force Vulnerability**:

   - Decryption by attempting all 25 possible keys is trivial.
   - Example:
     - Given a ciphertext encrypted with Caesar Cipher, all possible keys can be tested, revealing the plaintext (e.g., using Key = 5 to recover `TRYHACKME`).

3. **Modern Standards**:
   - With the cipher publicly known and easy to break, the Caesar Cipher is considered **insecure** today.

---

## Historical Ciphers in Cryptography

While Caesar Cipher is one of the earliest examples, many other historical ciphers have been used over the centuries:

- **The Vigenère Cipher** (16th century): A polyalphabetic cipher that improves upon Caesar Cipher by using multiple shift values.
- **The Enigma Machine** (World War II): An electro-mechanical cipher device used by Germany for military communication.
- **The One-Time Pad** (Cold War): A theoretically unbreakable cipher that uses a single-use key equal in length to the plaintext.

These ciphers highlight the evolution of cryptographic techniques over time and their role in securing communication throughout history.

# Encryption Types: Symmetric and Asymmetric

## Symmetric Encryption

Symmetric encryption, also known as symmetric cryptography, uses the same key for both encryption and decryption. This key must remain secret, hence it is also called **private key cryptography**.

### Key Points:

- The key must be communicated securely to intended parties, which can be challenging.
- Security risks increase with more recipients or a powerful adversary (e.g., industrial espionage).
- Common symmetric encryption algorithms:
  - **DES (Data Encryption Standard)**: Adopted in 1977 with a 56-bit key. It was broken in less than 24 hours by 1999 due to increased computing power.
  - **3DES (Triple DES)**: Applies DES three times with a 168-bit key, but the effective security is 112 bits. Deprecated in 2019.
  - **AES (Advanced Encryption Standard)**: Adopted in 2001 with key sizes of 128, 192, or 256 bits.

### Example Scenario:

- You share a password-protected document with a colleague, but emailing the password along with the document is unsafe. To securely share the password, a different channel must be used, such as meeting in person.

## Asymmetric Encryption

Asymmetric encryption uses a **pair of keys**: one for encryption and the other for decryption. This is also known as **public key cryptography**.

### Key Points:

- **Public key** is used for encryption, while the **private key** is used for decryption.
- Asymmetric encryption tends to be slower than symmetric encryption and uses larger key sizes.
- Examples of asymmetric encryption:
  - **RSA**: Uses key sizes of 2048-bit, 3072-bit, and 4096-bit (2048-bit recommended minimum).
  - **Diffie-Hellman**: Also uses 2048-bit as the minimum, with enhanced security at 3072-bit and 4096-bit.
  - **Elliptic Curve Cryptography (ECC)**: Achieves equivalent security with shorter keys (e.g., a 256-bit key provides security comparable to 3072-bit RSA).

### Security:

- Asymmetric encryption is based on mathematical problems that are easy to compute in one direction but infeasible to reverse within a reasonable time frame (e.g., millions of years).

### Key Concept:

- **Public key**: Shared with everyone.
- **Private key**: Kept secret and secure.

## Summary of New Terms:

- **Alice and Bob**: Fictional characters commonly used in cryptography to represent two parties communicating securely.
- **Symmetric encryption**: Uses the same key for both encryption and decryption. The key must remain secret.
- **Asymmetric encryption**: Uses a public key for encryption and a private key for decryption. The private key must remain secret.

# Building Blocks of Modern Cryptography

Cryptography relies on various mathematical operations. Two key operations used in many cryptographic algorithms are:

- XOR Operation
- Modulo Operation

## XOR Operation

XOR, short for "exclusive OR", is a binary operation that compares two bits and returns:

- `1` if the bits are different
- `0` if the bits are the same

The operation is represented by the symbol ⊕ or ^.

### XOR Truth Table

| A   | B   | A ⊕ B |
| --- | --- | ----- |
| 0   | 0   | 0     |
| 0   | 1   | 1     |
| 1   | 0   | 1     |
| 1   | 1   | 0     |

### Example of XOR Operation

Let’s apply XOR to the binary numbers `1010` and `1100`:

- 1 ⊕ 1 = 0
- 0 ⊕ 1 = 1
- 1 ⊕ 0 = 1
- 0 ⊕ 0 = 0

Result: `0110`

### Properties of XOR

- **Self-inverse**: \( A \oplus A = 0 \)
- **Identity**: \( A \oplus 0 = A \)
- **Commutative**: \( A \oplus B = B \oplus A \)
- **Associative**: \( (A \oplus B) \oplus C = A \oplus (B \oplus C) \)

### XOR in Cryptography

XOR is used in symmetric encryption. If you have a plaintext \( P \) and a secret key \( K \), the ciphertext \( C \) is computed as:
\[
C = P \oplus K
\]

To decrypt:
\[
P = C \oplus K
\]
Since \( C = P \oplus K \), we can recover \( P \) by applying XOR again with \( K \). The associative and self-inverse properties of XOR make this possible.

### Example of XOR Encryption

- Let \( P = 1010 \) and \( K = 1100 \)
- The ciphertext \( C = P \oplus K = 0110 \)
- To decrypt: \( P = C \oplus K = 0110 \oplus 1100 = 1010 \)

## Modulo Operation

The modulo operator, denoted \( X \% Y \) or `mod`, returns the remainder when \( X \) is divided by \( Y \).

### Examples of Modulo

- \( 25 \% 5 = 0 \) because 25 divided by 5 leaves a remainder of 0.
- \( 23 \% 6 = 5 \) because 23 divided by 6 leaves a remainder of 5.
- \( 23 \% 7 = 2 \) because 23 divided by 7 leaves a remainder of 2.

### Key Points About Modulo

- **Non-reversible**: If \( x \% 5 = 4 \), many values of \( x \) could satisfy the equation.
- **Range**: The result of \( a \% n \) is always between 0 and \( n - 1 \), for any integer \( a \) and positive integer \( n \).

### Working with Large Numbers

For cryptographic calculations, you often need to work with large numbers. If a calculator cannot handle large values, programming languages like Python can help, as they handle large integers automatically. Many other programming languages also provide libraries for big integers. Alternatively, WolframAlpha can assist with online calculations.
