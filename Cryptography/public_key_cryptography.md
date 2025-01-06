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

# Authentication in SSH: Server and Client Perspectives

## Authenticating the Server

When connecting to a server via SSH, you may encounter a confirmation prompt similar to the one below:

This prompt is the SSH client confirming whether you recognize the server’s public key fingerprint. In this case, the **ED25519** algorithm is used for digital signature generation and verification. If the SSH client doesn't recognize the key, it asks you to confirm whether to proceed. This warning serves as a safeguard against potential man-in-the-middle (MITM) attacks, where a malicious actor could intercept the connection and impersonate the server.

To authenticate the server:

1. Verify the public key signature.
2. Confirm the connection by typing `yes`.
3. The SSH client stores the server’s public key signature for future connections. Subsequent connections will proceed silently unless the server’s key changes.

## Authenticating the Client

Once the server is authenticated, the next step is identifying the client. SSH users are often authenticated with usernames and passwords, but this is not the most secure practice. Instead, **SSH key authentication** is recommended, which uses public and private keys to validate the client.

### SSH Key Pair Generation

The `ssh-keygen` program is used to generate key pairs. Various algorithms are supported, including:

- **DSA**: Digital Signature Algorithm, designed for digital signatures.
- **ECDSA**: Elliptic Curve Digital Signature Algorithm, a smaller key variant of DSA.
- **ECDSA-SK**: ECDSA with a security key for hardware-based private key protection.
- **Ed25519**: A public-key signature system using EdDSA with Curve25519.
- **Ed25519-SK**: Ed25519 with a security key for hardware-based private key protection.

Here is an example of generating a key pair:

### Public and Private Key Files

- **Private Key (`id_ed25519`)**: Must remain confidential. Sharing it compromises your security.
- **Public Key (`id_ed25519.pub`)**: Shared with the server to enable authentication.

The private key must be stored securely, and its permissions should allow only the owner to read or write (e.g., `chmod 600 id_ed25519`).

### Using a Passphrase

A passphrase adds a layer of security by encrypting the private key. However, the passphrase itself does not identify you to the server—it is used solely to decrypt the private key. The passphrase is never transmitted.

### Copying the Public Key to the Server

To use key authentication, copy the public key to the server using `ssh-copy-id`:

This adds the public key to the server's `~/.ssh/authorized_keys` file, allowing key-based login.

## Keys Trusted by the Remote Host

The `~/.ssh/authorized_keys` file on the server holds the public keys authorized to connect. For enhanced security, especially for the root user, disable password-based authentication and rely solely on key authentication.

## Using SSH Keys to Improve Shell Access

During activities like CTFs or penetration testing, leaving an SSH key in the `authorized_keys` file can serve as a backdoor. This method bypasses the instability of reverse shells and provides full SSH functionality, including tab completion and better control.

### Specifying a Key for Connection

Use the `-i` flag to specify a private key when connecting:

# Digital Signatures and Certificates

## What’s a Digital Signature?

In the “analogue” world, signing documents is common. Whether you’re opening a savings account at the bank or filling out an application at the local library, signing a paper often signifies your agreement, authorization, or acknowledgment. However, in the “digital” world, physical signatures, stamps, or fingerprints cannot be used, which is where **digital signatures** come into play.

### Definition:

Digital signatures are a cryptographic mechanism that ensures the authenticity and integrity of a digital message or document. They allow recipients to verify that the sender is indeed who they claim to be and that the content of the message or document hasn’t been altered.

Using **asymmetric cryptography**, a signature is created with a **private key** and verified using the corresponding **public key**. Only the holder of the private key can produce the signature, proving that the document has been signed by them. In many jurisdictions, digital signatures hold the same legal weight as physical signatures.

### Process:

1. A message or document is signed by encrypting it with the sender’s private key.
2. To verify, the recipient uses the sender’s public key to decrypt the signature and check if it matches the original message or document.
3. This ensures the integrity of the file, meaning it hasn't been tampered with after being signed.

#### Example:

- **Bob** encrypts a message with his private key.
- **Alice** decrypts the message with Bob's public key.

> **Note:** While some articles may refer to "electronic signatures" or "digital signatures" interchangeably, it's important to note that simply pasting an image of a signature onto a document does not prove its integrity. This is merely an image, which can be copied, and does not protect the content of the document.

In this task, we focus on **digital signatures** as the process of signing a document using a private key or certificate. The document’s integrity is validated by hashing the file, encrypting the hash with the private key, and sending it along with the original file. The recipient can decrypt the encrypted hash with the sender’s public key and compare it with a hash of the file to verify its integrity.

## Certificates: Prove Who You Are!

Certificates play a vital role in **public key cryptography**, and they are closely linked to digital signatures. A common application of certificates is in **HTTPS** (Hypertext Transfer Protocol Secure), ensuring secure communication between a web browser and a web server.

### How Do Certificates Work?

When you visit a website like `tryhackme.com`, how does your browser know it’s talking to the real site and not a malicious impersonator? The answer lies in **certificates**. A web server has a certificate that asserts its identity as the legitimate `tryhackme.com`.

Certificates rely on a **chain of trust**:

1. **Root Certificate Authorities (CAs)**: Your device, operating system, and browser automatically trust certain root CAs, which act as the foundation of the certificate chain.
2. **Intermediate Certificates**: These certificates are signed by trusted CAs and link the server certificate to the root CA.
3. **Server Certificate**: This is the certificate provided by the website’s server that proves its identity.

### Trust Chain:

- The certificate is signed by an organization.
- The organization is trusted by a CA.
- The CA is trusted by your browser.

This chain of trust ensures that the certificate is legitimate, and therefore, your browser trusts the connection. You can check which CAs are trusted by popular browsers, such as Mozilla Firefox and Google Chrome.

### Getting a Certificate for HTTPS

If you run a website and wish to use HTTPS, you'll need a **TLS certificate** (Transport Layer Security). You can purchase a certificate from a CA for an annual fee, or use services like **Let’s Encrypt** to obtain free certificates for domains you own.

It is highly recommended for website owners to set up HTTPS, as modern websites typically do. This ensures that all communications between the user and the server are encrypted and secure.

# Pretty Good Privacy (PGP) and GPG

## What is PGP?

**PGP (Pretty Good Privacy)** is software designed to enhance security through encryption. It is widely used for encrypting files, performing digital signatures, and various other cryptographic operations.

### What is GPG?

**GPG (GnuPG)**, or GNU Privacy Guard, is an open-source implementation of the OpenPGP standard. GPG is commonly used in email communications to:

- **Protect confidentiality** by encrypting email messages.
- **Ensure integrity** by signing email messages.

## Generating GPG Keys

Below is an example of generating a GPG key pair. During the process:

1. You are asked about the purpose of the key (e.g., signing only or signing and encrypting).
2. You select the cryptographic algorithm to use.
3. You set an expiry date for the generated key.
4. You provide some personal information, such as:
   - Name
   - Email address
   - A comment about the key's purpose (optional).

## Practical Use of GPG

### Key Sharing and Communication

Once your GPG key pair is generated:

- Share your **public key** with your contacts.
- Contacts encrypt their messages to you using your public key.
- To decrypt their messages, use your **private key**.

### Example Commands:

- Import a backup key:  
  `gpg --import backup.key`
- Decrypt a message:  
  `gpg --decrypt confidential_message.gpg`

### CTF and Cracking GPG Passphrases

In Capture The Flag (CTF) challenges, you may need to decrypt files using GPG. Private keys can be protected with passphrases, similar to SSH private keys. If the key is passphrase-protected, you can attempt to crack it using **John the Ripper** and **gpg2john**.

_Note:_ The key provided in this task is **not passphrase-protected**.

## Key Management and Backup

Due to the importance of GPG keys:

- Always keep a **backup copy** of your keys in a secure location.
- If you move to a new computer, import your backup key to continue decrypting your messages.

For more detailed usage, refer to the GPG manual: [GPG Man Page](https://www.gnupg.org/documentation/manpage.html).
