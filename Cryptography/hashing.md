<h1 style="text-align:center">Hashing</h1>

A hash value is a fixed-size string or characters that is computed by a hash function. A hash function takes an input of an arbitrary size and returns an output of fixed length, i.e., a hash value.

# Hash Functions: Basics and Importance

## What is a Hash Function?

A **hash function** differs from encryption in that it:

- Does not use a key.
- Is designed to make it computationally impractical to reverse the process (i.e., go from the hash output back to the input).

### Key Characteristics:

1. **Input-Output Relationship**: Takes input data of any size and generates a fixed-size output (digest).
2. **Unpredictability**: It’s hard to predict the output for a given input or reverse-engineer the input from the output.
3. **Sensitivity to Changes**: Even the slightest change in the input (e.g., a single bit) results in a significantly different output.
4. **Efficiency**: Good hash functions are fast to compute while being computationally prohibitive to reverse.

### Example:

Consider two files, one containing the letter "T" and the other containing "U":

- **ASCII Values**:
  - "T" = `54` (hex) = `01010100` (binary).
  - "U" = `55` (hex) = `01010101` (binary).
- While the two differ by a single bit, their MD5, SHA1, and SHA-256 hash outputs are entirely different.

### Hash Output Encoding:

Hash outputs are raw bytes often encoded for readability:

- Common encodings: **Base64** or **Hexadecimal**.
- Tools like `md5sum`, `sha1sum`, `sha256sum`, and `sha512sum` output hashes in **hexadecimal format**.

---

## Why is Hashing Important?

Hashing plays a critical role in ensuring **data integrity** and **password confidentiality**. It is a backbone of many security systems, often operating transparently to the user.

### Everyday Examples:

1. **Password Security**:
   - Servers store the **hash value** of your password instead of the password itself.
   - When you log in, the server compares the hash of the entered password with the stored hash to verify your credentials.
2. **Data Integrity**:
   - Hashing ensures that data has not been tampered with during transmission.

---

## What’s a Hash Collision?

A **hash collision** occurs when two different inputs produce the same hash output. Although hash functions are designed to minimize collisions, they are theoretically unavoidable due to the **pigeonhole principle**.

### Pigeonhole Principle:

- If the number of possible outputs (pigeonholes) is smaller than the number of possible inputs (pigeons), some inputs will inevitably share the same output.

### Collision in Practice:

- MD5 and SHA1 algorithms have been attacked successfully, making them vulnerable to engineered collisions.
- **Example**:
  - MD5 collisions are demonstrated on the [MD5 Collision Demo page](https://www.mscs.dal.ca/~selinger/md5collision/).
  - Details of the SHA1 collision attack can be found on [Shattered](https://shattered.io/).

---

## Best Practices:

Due to their vulnerabilities:

- **Do not use MD5 or SHA1** for sensitive applications like password storage or data integrity.
- Instead, use more secure algorithms like **SHA-256** or **SHA-3**.
