<h1 style='text-align:center'>Hashing Tools</h1>

## Rainbow Table Attacks on Hashes

1. [Crackstation](https://crackstation.net/)
2. [Hashes.com](https://hashes.com/en/decrypt/hash)

## Identifying Hash Types

1. [hashID](https://pypi.org/project/hashID/) - not always relyable.
2. [Hashcat Example Hashes](https://hashcat.net/wiki/doku.php?id=example_hashes)

## Password Cracking

1. [Hashcat](https://hashcat.net/hashcat/)
2. [John the Ripper](https://www.openwall.com/john/)
3. [rockyou.txt](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) - password list.

Use thse with the rockyou.txt password list.

On Linux, password hashes are stored in `/etc/shadow` (usually only readable by root). They used to be stored in `/etc/passwd` which was readable by everyone.

- **The Shadow File**:

  - Contains password information.
  - Each line has nine fields separated by colons (`:`).

    - **First Two Fields**: Login name and encrypted password.
    - For details on other fields, run: `man 5 shadow`.

  - Components:
    - Format: `$prefix$options$salt$hash`
    - **Prefix**: Identifies the hashing algorithm.
    - **Options**: Parameters for the algorithm.
    - **Salt**: Random value added for uniqueness.
    - **Hash**: The resulting hashed password.

- Prefix helps recognize Unix/Linux-style passwords and their hashing algorithm.

---

## Common Password Prefixes and Algorithms

| Prefix                         | Algorithm                                                                               |
| ------------------------------ | --------------------------------------------------------------------------------------- |
| `$y$`                          | **yescrypt**: Scalable hashing scheme, recommended for new systems.                     |
| `$gy$`                         | **gost-yescrypt**: Uses GOST R 34.11-2012 and yescrypt hashing.                         |
| `$7$`                          | **scrypt**: Password-based key derivation function.                                     |
| `$2b$`, `$2y$`, `$2a$`, `$2x$` | **bcrypt**: Hash based on Blowfish cipher; supported on many platforms.                 |
| `$6$`                          | **sha512crypt**: Based on SHA-2 (512-bit output); commonly used on older Linux systems. |
| `$md5`                         | **SunMD5**: Hash based on MD5, originally developed for Solaris.                        |
| `$1$`                          | **md5crypt**: Hash based on MD5, originally developed for FreeBSD.                      |

- To learn more about these algorithms, use: `man 5 crypt`.

## MS Windows Passwords

### Hashing Algorithm

- **Windows Passwords**:
  - Hashed using **NTLM** (a variant of MD4).
  - Visually identical to MD4 and MD5 hashes.
    - Use **context** to determine the hash type accurately.

---

### Password Hash Storage

- **Storage Location**:

  - Password hashes are stored in the **SAM (Security Accounts Manager)** file.
  - MS Windows restricts normal users from dumping these hashes.

- **Hash Types**:
  - **NT Hashes**: Primary password hashes.
  - **LM Hashes**: Legacy hashes; less secure and often disabled in modern systems.

---

## Circumventing Security

- Tools like **mimikatz** can bypass MS Windows security measures to dump hashes from the SAM file.

---

## Additional Resources

- For more hash formats and password prefixes, refer to the [Hashcat Example Hashes](https://hashcat.net/wiki/doku.php?id=example_hashes) page.
- Identifying hash types often involves:
  - Checking **length** or **encoding**.
  - Researching the application that generated the hash.

---

## Pro Tip

- **Research** is a powerful tool when dealing with unknown hash types. Never underestimate its importance.
