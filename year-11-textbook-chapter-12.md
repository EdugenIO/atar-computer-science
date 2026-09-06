# Unit 2 — Chapter 12: Defensive Security & Cryptography

This chapter explores how computer systems defend sensitive user databases using robust authentication policies and mathematical encryption. You will study how password protocols, multi-factor authentication (MFA), and biometrics control system access. You will also dive into the mathematical mechanisms of cryptography, comparing symmetric and asymmetric encryption models, manually calculating substitution and polyalphabetic ciphers, and applying cryptanalysis techniques (brute force and frequency analysis) to evaluate cipher strength.

These concepts form a vital portion of the theoretical foundations of **SCSA Unit 2**, and they directly support the implementation of secure transactions in your **SCSA School-Based Assessments (Task 6 and Task 7)**.

---

## Lesson 12.1: Authentication & Password Policy

### Your Goal
Formulate comprehensive password policies and multi-factor authentication (MFA) frameworks to secure user access to relational databases.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 10.4: The AAA Security Framework](./year-11-textbook-chapter-10.md#lesson-104-the-aaa-security-framework) (specifically authentication concepts).

### The Idea
Before a database allows a user to read or modify records, it must prove their identity. This is **Authentication** (proving *who* you are). Standard security practices divide authentication credentials into three distinct categories, known as the **Factors of Authentication**:
1.  **Something you know:** A piece of knowledge (e.g., password, PIN, passphrase).
2.  **Something you have:** A physical object (e.g., hardware token, SMS code, authenticator app OTP, smart card).
3.  **Something you are:** A physical biological metric (e.g., fingerprint, retina scan, facial geometry, voiceprint).

A secure system must combine these factors rather than relying on a single weak barrier. This is called **Multi-Factor Authentication (MFA)**.

**The Analogy:**
Imagine entering a high-security vault. 
*   A simple lock requiring only a key is single-factor. If an intruder steals the key, they get in.
*   To secure the vault, the manager installs a combination lock (something you know), a physical keyhole (something you have), and a thumbprint scanner (something you are). An intruder must steal all three to break in.

#### **Password Complexity vs. Entropy**
Historically, organizations forced users to create short, complex passwords with symbols and numbers (e.g., `P@ssw0rd1!`). Today, modern security agencies (like the Australian Signals Directorate - ASD) recommend **Passphrases** (e.g., `correcthorsebatterystaple`). Long passphrases have higher mathematical **entropy** (unpredictability), making them exponentially harder for computers to brute-force, while remaining significantly easier for humans to remember.

#### **Biometric Performance Metrics**
When implementing "something you are" biometric systems, developers must balance two conflicting performance metrics:
*   **False Acceptance Rate (FAR):** The probability that the system incorrectly authorizes an unauthorized user (security failure).
*   **False Rejection Rate (FRR):** The probability that the system incorrectly rejects a legitimate authorized user (usability failure).

#### **SCSA Key Terms**
*   **Authentication:** The process of verifying the identity of a user, device, or system.
*   **Multi-Factor Authentication (MFA):** A security system that requires multiple distinct methods of authentication from independent categories to verify a user's identity.
*   **Passphrase:** A sequence of random words or text used as a password, providing high entropy and ease of recall.
*   **Biometrics:** Technical systems that measure and analyze unique human physical or behavioral characteristics for authentication.
*   **False Acceptance Rate (FAR):** The rate at which a biometric security system mistakenly authorizes an unregistered person.
*   **False Rejection Rate (FRR):** The rate at which a biometric security system mistakenly denies access to an authorized user.

---

### See It Worked
#### **The Scenario**
The **WA Junior Sports Carnival** treasurer accesses a sensitive Web portal to distribute payout reimbursements to regional athletic clubs. Initially, their portal only requires a standard password (`Carnival2026`). 

Let's evaluate the vulnerability of this single-factor authentication and design an enterprise-grade multi-factor upgrade:

```
[ SINGLE-FACTOR SYSTEM ]
- User inputs Password: "Carnival2026"
- Vulnerability: If a shoulder-surfer or phishing email steals "Carnival2026", the account is completely compromised.
- Risk: High financial fraud.

           |
           v

[ MULTI-FACTOR UPGRADE (MFA) ]
Factor 1 (Something You Know): User enters a strong Passphrase (e.g., "fast-sprint-gold-javelin")
Factor 2 (Something You Have): The system prompts for a 6-digit One-Time Password (OTP) sent to the treasurer's registered authenticator app on their phone.
Factor 3 (Something You Are): The physical laptop requires a fingerprint scan to unlock the local cryptographic storage keys.
```

#### **How the Logic Flows**
*   If a remote attacker phishes the passphrase `"fast-sprint-gold-javelin"`, they still cannot log in because they do not have physical possession of the treasurer's mobile phone to read the live OTP (Factor 2).
*   If an attacker physically steals the phone, they still cannot complete the login because they do not know the passphrase (Factor 1) and cannot replicate the treasurer's biometric fingerprint (Factor 3).
*   By combining distinct factors, the system's security profile increases exponentially.

---

### Try It with Help
#### **The Problem**
A database administrator for the Western Australian SCSA school registration portal is drafting a revised Password and Authentication Policy. The current system allows students to use 6-character passwords and locks accounts for only 2 minutes after 5 failed attempts.

Identify the structural vulnerabilities in this policy and complete the table below to propose secure, SCSA-compliant design upgrades.

#### **Structural Hints**
1.  **Length & Complexity:** Short passwords (6 characters) can be cracked in seconds using automated brute-force tools. Introduce passphrases.
2.  **Lockout Threshold:** A 2-minute lockout is too short; automated brute-force bots can throttle their requests and continue guessing indefinitely.
3.  **Factor Inclusion:** Relying solely on password entry is single-factor. Integrate MFA.

#### **Scaffolded Student Matrix**
Fill in the missing fields to justify the security upgrades:

| Current Policy Element | Security Vulnerability | Proposed Upgrade | Security Justification |
| :--- | :--- | :--- | :--- |
| 6-character password | Low mathematical entropy; highly vulnerable to brute-force. | Minimum 14-character passphrase. | Exponentially increases search-space size, stalling dictionary attacks. |
| 2-minute lockout after 5 fails | Allows automated scripts to slowly cycle guesses over time. | Lock account for **30 minutes** or require admin reset after 5 fails. | ??? (Fill in) |
| Password-only login | Single-factor authentication; prone to credential theft. | ??? (Fill in) | ??? (Fill in) |

---

### Try It Yourself
#### **The Problem**
A high-performance regional athletic institute in WA is deploying a secure mobile app where coaches upload athlete physiological diagnostics and drug-testing logs. The app development team is deciding between two authentication options:
*   **Option A:** A standard fingerprint scanner on the coach's tablet.
*   **Option B:** A password combined with an SMS-based verification code.

Evaluate both options. Identify which factor categories are utilized by each option, discuss the trade-offs of using biometrics (referencing FAR and FRR), and write a justified recommendation for which system provides the highest security profile for sensitive medical files. (Write approximately 150 words).

---

### Check Your Reasoning
#### **The Answer**
```
1. Option A (Fingerprint scanner) utilizes "Something you are" (Biometric).
   - Pros: Highly convenient; cannot be easily forgotten or shared.
   - Cons: Prone to False Rejection (FRR) if a coach's hands are sweaty/dirty on the field, locking out legitimate users. Prone to False Acceptance (FAR) on cheaper hardware sensors.

2. Option B (Password + SMS Code) utilizes:
   - Factor 1: "Something you know" (Password)
   - Factor 2: "Something you have" (SMS code sent to mobile device)
   - This represents Multi-Factor Authentication (MFA).

3. Recommendation:
   Option B is superior for securing highly sensitive diagnostics. While biometrics (Option A) are convenient, they function as a single-factor lock on a device. Option B combines two distinct factors (knowledge and physical possession), meaning a remote hacker cannot breach the files with compromised passwords alone, and a thief who steals the physical tablet cannot log in without the secret password. Thus, Option B delivers a significantly stronger security defense.
```

#### **Common SCSA Student Errors**
*   **Conflating multi-step with multi-factor:** Believing that entering a password *and* answering a security question (like "What was your first pet?") is MFA. Both of these are "something you know," making it a multi-step *single-factor* authentication system.
*   **Ignoring Biometric Trade-offs:** Believing that biometrics are "100% secure and infallible." SCSA theory questions require students to acknowledge physical error states like False Acceptance (FAR) and physical wear/dirt on field sensors.

---

### Review and Connect
In this lesson, you explored how password policies and MFA secure system access at the boundary. However, once users log in, data must travel across networks. On the next page, we will study how to scramble data during transmission using symmetric and asymmetric encryption models.

---

## Lesson 12.2: Symmetrical vs Asymmetrical Encryption

### Your Goal
Contrast the performance, key management, and security characteristics of symmetric and asymmetric encryption systems, and explain how they collaborate to secure network traffic.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 9.1: DoD TCP/IP Model and Protocols](./year-11-textbook-chapter-9.md#lesson-91-dod-tcpip-model-and-protocols) (specifically HTTP vs. HTTPS operations).

### The Idea
When we transmit athlete registration details, parent contact numbers, or SQL queries over a network, anyone intercepting the raw data packets can read them. To prevent unauthorized reading, we use **Encryption**—the mathematical process of converting readable data (**Plaintext**) into unreadable scrambled data (**Ciphertext**) using a cryptographic key.

There are two primary models of encryption, distinguished by how they handle keys:

#### **1. Symmetric Encryption**
In symmetric encryption, the **same secret key** is used to both encrypt and decrypt the data. Both the sender and the receiver must possess a copy of this identical key.
*   **Analogy:** A sturdy padlocked wooden chest. You lock the chest with a brass key (encryption). You send the chest to a friend. For them to open it, you must somehow send them a copy of the exact same brass key (decryption).
*   **SCSA Core Limitation (The Key Distribution Problem):** If you transmit the key over the internet to your friend, an eavesdropper can intercept the key, copy it, and decrypt all your future chests. If you must meet in person to exchange keys, it is impractical on a global scale.
*   **SCSA Advantage:** Mathematically simple and extremely fast. Excellent for encrypting large databases or local hard drives.
*   **Common Standard:** AES (Advanced Encryption Standard).

#### **2. Asymmetric (Public Key) Encryption**
Asymmetric encryption resolves the key distribution problem by using a mathematically linked **Key Pair**:
*   **Public Key:** Made freely available to the entire world. Anyone can use this key to encrypt data.
*   **Private Key:** Kept strictly secret by the owner. Only this key can decrypt data encrypted by its corresponding public key.
*   *Note:* The public key *cannot* decrypt the data it just encrypted. Only the private key can reverse the mathematical process.
*   **Analogy:** A lockbox with a slot in the lid. The box is bolted to a public wall. Anyone can drop a secret letter through the slot (encrypting using the public key). However, once the letter drops in, nobody can retrieve it. Only the owner, who holds the physical brass key (the private key) to the back door, can open the box and read the messages.
*   **SCSA Limitation:** Extremely slow and computationally intensive compared to symmetric systems.
*   **Common Standard:** RSA, ECC.

```
[ SYMMETRIC ENCRYPTION ]
Plaintext  +  Secret Key  ──►  [Encrypt]  ──►  Ciphertext  ──►  [Decrypt]  +  Secret Key  ──►  Plaintext
                                                     ^                                 ^
                                                     +───────── IDENTICAL KEYS ────────+

[ ASYMMETRIC ENCRYPTION ]
Plaintext  +  PUBLIC Key  ──►  [Encrypt]  ──►  Ciphertext  ──►  [Decrypt]  +  PRIVATE Key  ──►  Plaintext
                                                     ^                                 ^
                                                     +──────── MATHEMATICALLY LINKED ──+
```

#### **SCSA Key Terms**
*   **Symmetric Encryption:** A cryptographic method where a single, identical key is used for both encryption and decryption.
*   **Asymmetric Encryption (Public Key Cryptography):** A cryptographic method using a pair of mathematically linked keys (a public key for encryption and a private key for decryption).
*   **Plaintext:** The original, unencrypted, readable data input.
*   **Ciphertext:** The encrypted, scrambled, unreadable output of a cryptographic operation.
*   **Key Distribution Problem:** The vulnerability of having to securely share a symmetric key between parties over an untrusted network before secure communication can occur.

---

### See It Worked
#### **The Scenario**
A coach at the **WA Junior Sports Carnival** wants to submit official race times securely to the central database server over an unsecured outdoor Wi-Fi link. Rather than choosing only one encryption method, the systems developer implements **HTTPS (SSL/TLS)**, which combines both symmetric and asymmetric cryptography to gain the speed of symmetric and the security of asymmetric:

```
[ THE HTTPS HYBRID HANDSHAKE ]

1. Client Connects  ──► Requests secure connection to Server.
2. Server Responds  ──► Sends its ASYMMETRIC PUBLIC KEY.
3. Client Generates ──► Creates a brand-new, temporary SYMMETRIC SESSION KEY.
4. Client Encrypts  ──► Encrypts the Session Key using the Server's PUBLIC KEY.
5. Client Sends     ──► Transmits encrypted key to Server.
6. Server Decrypts  ──► Uses its private key to extract the raw Session Key.
                        [ BOTH NOW SHARE THE SAME SYMMETRIC SESSION KEY SECURELY ]
7. Secure Transfer  ──► All athlete data is now encrypted/decrypted using fast Symmetric AES.
```

#### **How the Logic Flows**
1.  The asymmetric key pair is used *only* during the opening seconds of the handshake to safely exchange the symmetric session key.
2.  Because the client encrypted the session key with the server's *public* key, only the server's *private* key can decrypt it. Eavesdroppers intercepting the handshake cannot read the session key.
3.  Once the symmetric session key is securely shared, the system transitions to symmetric encryption to process high-volume athlete logs rapidly without overloading the tablet's processors.

---

### Try It with Help
#### **The Problem**
A database system designer is configuring backup replication between a local sports office in Albany and a primary cloud storage center in Perth. They are deciding whether to encrypt the nightly 10GB database backup using **Symmetric AES-256** or **Asymmetric RSA-4096**.

Help them evaluate their choices by completing the comparative matrix below:

#### **Structural Hints**
*   **Computation Speed:** Symmetric algorithms are roughly 1,000 to 10,000 times faster than asymmetric algorithms. Think about the resource cost of encrypting a massive 10GB file.
*   **Key Security:** Asymmetric cryptography excels when two unknown parties need to connect over a public web space. For an internal company office transferring files to its own secure cloud center, key distribution can be set up securely beforehand.

#### **Scaffolded Student Matrix**
Fill in the blanks to complete the evaluation:

| Evaluation Metric | Symmetric System (AES-256) | Asymmetric System (RSA-4096) | Recommended Choice for 10GB Backup |
| :--- | :--- | :--- | :--- |
| **Number of Keys** | Single shared secret key. | ??? (Fill in) | Symmetric (Single key is easier to store locally in script). |
| **Encryption Speed** | Fast; low processing overhead. | ??? (Fill in) | ??? (Fill in) |
| **Key Exchange Risk** | High; if the key is leaked, all backups are compromised. | Low; only the public key is sent over the network. | Asymmetric is safer over open lines, but keys can be hard-coded securely. |
| **Ideal Use Case** | Bulk data storage; local disk encryption. | Handshakes; digital signatures. | **Symmetric (AES-256)** because of its superior speed on large files. |

---

### Try It Yourself
#### **The Problem**
Explain how asymmetric public-key cryptography resolves the **Key Distribution Problem** associated with symmetric encryption. In your response, clearly trace how a sender (User A) transmits a confidential document to a receiver (User B) without exchanging any secret keys in advance. Use correct SCSA terminology (approx. 100 words).

---

### Check Your Reasoning
#### **The Answer**
```
Symmetric encryption suffers from the Key Distribution Problem because both sender and receiver require an identical secret key, which cannot be safely transmitted over an unsecure network. 

Asymmetric cryptography resolves this issue by utilizing a linked key pair: a public key and a private key. When User A wants to send a confidential document to User B:
1. User B freely sends their Public Key to User A over the open internet.
2. User A encrypts the document using User B's Public Key, generating ciphertext.
3. User A transmits this ciphertext over the open internet.
4. User B receives the ciphertext and decrypts it using their Private Key, which has never left User B's possession.

Since the private key is never shared or transmitted, eavesdroppers cannot decrypt the data, successfully eliminating the distribution risk.
```

#### **Common SCSA Student Errors**
*   **Encrypting with the Private Key for confidentiality:** A frequent, major error is writing that a sender encrypts data with their *own private key* to ensure privacy. If you encrypt with your private key, anyone with your *public* key can decrypt it! Privacy is achieved by encrypting with the *receiver's public key*.
*   **Mixing up key properties:** Forgetting that a public key cannot decrypt the message it just encrypted.

---

### Review and Connect
You have mastered high-level symmetric and asymmetric architectures. On the next page, we step back into the classroom history of cryptography to examine how individual characters are scrambled using manual **Substitution Ciphers**.

---

## Lesson 12.3: Substitution Ciphers

### Your Goal
Encrypt and decrypt alphabetical messages manually using Caesar rotation and random substitution mapping algorithms.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 1.1: Characters as Binary Numbers](./year-11-textbook-chapter-1.md#lesson-11-characters-as-binary-numbers) (character strings and mappings).
*   [Lesson 5.1: Arithmetic Operators and MOD](./year-11-textbook-chapter-5.md#lesson-51-arithmetic-operators-and-mod) (modulo math wrapping).

### The Idea
The simplest form of encryption is a **Substitution Cipher**, where each character in the original plaintext is systematically replaced by another character to create ciphertext.

#### **1. The Rotation (Caesar) Cipher**
The Caesar cipher is a monoalphabetic substitution cipher where each letter in the plaintext is shifted a fixed number of places down the alphabet.
*   **The Key:** The integer value representing the offset shift (e.g., a key of `+3` means `A` shifts to `D`, `B` to `E`, and `C` to `F`).
*   **SCSA Mathematical Formula:**
    To calculate shifts programmatically (where $A=0, B=1, \dots, Z=25$), we use modulo-26 arithmetic to wrap around the alphabet borders:
    $$	ext{CipherLetter} = (	ext{PlainLetter} + 	ext{Key}) \pmod{26}$$
    $$	ext{PlainLetter} = (	ext{CipherLetter} - 	ext{Key}) \pmod{26}$$

**The Analogy:**
Imagine an alphabet wheel. You align the inner wheel (plaintext) with the outer wheel (ciphertext). By rotating the outer wheel by 3 positions, every letter aligns with its scrambled substitute.

```
Plaintext Alphabet:  A  B  C  D  E  F  G  H  I  J  K  L  M  N  O  P  Q  R  S  T  U  V  W  X  Y  Z
                                 │  │  │
                                 ▼  ▼  ▼  (Shift of +3)
Ciphertext Alphabet: D  E  F  G  H  I  J  K  L  M  N  O  P  Q  R  S  T  U  V  W  X  Y  Z  A  B  C
```

#### **2. Random Substitution Cipher**
Instead of a uniform shift, a random substitution cipher uses a completely randomized lookup array of all 26 letters as the key.
*   **The Key:** A mixed alphabet string (e.g., `XYZABCDEFGHIJKLMNOPQRSTUVW`).
*   **SCSA Limitation:** This is harder to break than Caesar because you cannot simply guess 26 shift offsets; there are $26! pprox 4 	imes 10^{26}$ possible keys. However, it is still vulnerable to pattern analyses.

#### **SCSA Key Terms**
*   **Substitution Cipher:** A method of encryption by which units of plaintext are replaced with ciphertext according to a fixed system.
*   **Caesar Cipher (Rotation Cipher):** A substitution cipher where each letter in the plaintext is rotated a fixed number of positions down the alphabet.
*   **Monoalphabetic Substitution:** A cipher system that uses a single, unchanging substitution alphabet to encrypt an entire message.

---

### See It Worked
#### **The Scenario**
To prevent rival schools from spying on team tactics sheets during the **WA Junior Sports Carnival**, ovals marshals encrypt tactical codes using a Caesar rotation cipher with a key shift of **`+5`**.

Let's encrypt the plaintext message `"RUN"` and then decrypt the ciphertext `"YFQQ"` back to plaintext.

#### **1. Encryption of "RUN" (Key = +5)**
*   **Step 1: Map letters to alphabet index values (0-25):**
    *   `R` $ightarrow$ 17
    *   `U` $ightarrow$ 20
    *   `N` $ightarrow$ 13
*   **Step 2: Add key shift (+5) and apply modulo 26:**
    *   `R`: $(17 + 5) \pmod{26} = 22 ightarrow$ **`W`**
    *   `U`: $(20 + 5) \pmod{26} = 25 \pmod{26} = 25 ightarrow$ **`Z`**
    *   `N`: $(13 + 5) \pmod{26} = 18 ightarrow$ **`S`**
*   **Plaintext `"RUN"` becomes Ciphertext `"WZS"`**.

#### **2. Decryption of "YFQQ" (Key = +5)**
*   **Step 1: Map letters to index values:**
    *   `Y` $ightarrow$ 24, `F` $ightarrow$ 5, `Q` $ightarrow$ 16, `Q` $ightarrow$ 16
*   **Step 2: Subtract key shift (5) and apply modulo 26:**
    *   `Y`: $(24 - 5) \pmod{26} = 19 ightarrow$ **`T`**
    *   `F`: $(5 - 5) \pmod{26} = 0 ightarrow$ **`A`**
    *   `Q`: $(16 - 5) \pmod{26} = 11 ightarrow$ **`L`**
    *   `Q`: $(16 - 5) \pmod{26} = 11 ightarrow$ **`L`**
*   **Ciphertext `"YFQQ"` decrypts to Plaintext `"TALL"`**.

---

### Try It with Help
#### **The Problem**
Encrypt the sports team name `"GOLD"` using a random substitution cipher key. 

#### **The Key Matrix**
Use this specific, non-shifting random lookup key to convert the plaintext:

```
Plaintext:  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
            │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │
            ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼ ▼
Lookup Key: Q W E R T Y U I O P A S D F G H J K L Z X C V B N M
```

#### **Structural Hints**
*   Find `G` in the top plaintext row. The corresponding key letter below it is `U`.
*   Find `O` in the top row. Trace down to find the key letter `G`.
*   Complete the rest of the letters carefully.

#### **Scaffolded Student Guide**
*   `G` $ightarrow$ `U`
*   `O` $ightarrow$ `G`
*   `L` $ightarrow$ ???
*   `D` $ightarrow$ ???
*   Ciphertext = `UG`??

---

### Try It Yourself
#### **The Problem**
Write a complete, annotated Python function `caesar_encrypt(plaintext, key)` that takes a string of uppercase letters and an integer shift key, and returns the encrypted ciphertext. 
*   *Requirement:* Ensure your code mathematically handles uppercase letter wrapping using the `% 26` operator.
*   *Test Input:* `caesar_encrypt("WEST", 4)`

---

### Check Your Reasoning
#### **The Answer**
```python
def caesar_encrypt(plaintext, key):
    ciphertext = ""
    for char in plaintext:
        # Check if character is an uppercase letter
        if char.isupper():
            # 1. Convert character to an index from 0 to 25 (ord('A') is 65)
            plain_index = ord(char) - 65
            # 2. Add the key shift and wrap using modulo 26
            cipher_index = (plain_index + key) % 26
            # 3. Convert back to character and append to output string
            ciphertext += chr(cipher_index + 65)
        else:
            # Leave non-alphabet characters unchanged
            ciphertext += char
            
    return ciphertext

# Test
print(caesar_encrypt("WEST", 4)) # Expected output: "AIWT"
```

#### **How the Math wrapped on 'W':**
*   `W` $ightarrow$ Index 22.
*   Shift by +4 $ightarrow 22 + 4 = 26$.
*   `26 % 26 = 0` $ightarrow$ Index 0, which maps back to **`A`**.

#### **Common SCSA Student Errors**
*   **Forgetting to wrap boundaries:** Writing loops that increment ASCII values past `Z` (ASCII 90) into non-alphabet symbols like `[` or `\`. Modulo math is mandatory.
*   **Hardcoding static ASCII offsets:** Forgetting that `ord('A')` is 65, leading to wrong arithmetic offsets if they subtract or add incorrect constant bounds.

---

### Review and Connect
While monoalphabetic substitution is simple to calculate, it has a fatal flaw: an eavesdropper can easily crack it using letter pattern distributions. On the next page, we will study a more advanced, secure manual cipher: the polyalphabetic **Vigenère Cipher**.

---

## Lesson 12.4: Polyalphabetic Cryptography (Vigenère)

### Your Goal
Encrypt and decrypt alphabetical messages manually using a polyalphabetic Vigenère algebraic cipher table (tabula recta) and keystreams.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 12.3: Substitution Ciphers](./year-11-textbook-chapter-12.md#lesson-12-3-substitution-ciphers) (basic character mappings).

### The Idea
Monoalphabetic ciphers are weak because they use a single shifting rule: if `E` is shifted to `H` in one word, it is shifted to `H` everywhere else in the message. 

To break this predictable pattern, a **Polyalphabetic Cipher** changes the shift offset for *every single letter* in the message using a repeating **Keyword Keystream**.

The most famous polyalphabetic cipher is the **Vigenère Cipher**.

#### **The Keystream**
Instead of a single integer key, we use a keyword. We write the keyword repeatedly over the plaintext to create the keystream:
```
Plaintext:  S P R I N T
Keyword:    W A S  W A S  (Keyword "WAS" is repeated)
Keystream:  W A S  W A S
```
Each letter in the keystream represents a different Caesar shift key:
*   `A` means a shift of `0`, `B` means `1`, `C` means `2`, ..., `W` means `22`.
*   This means the first letter `S` is shifted by 22, the second letter `P` is shifted by 0, and the third letter `R` is shifted by 18.

#### **The Tabula Recta (Vigenère Grid)**
To encrypt manually without calculating modulo math, we use a **Tabula Recta** (Vigenère Grid). The grid contains 26 rows of alphabets, each shifted by one extra step:

```
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
  +───────────────────────────────────────────────────
A | A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
B | B C D E F G H I J K L M N O P Q R S T U V W X Y Z A
C | C D E F G H I J K L M N O P Q R S T U V W X Y Z A B
...
W | W X Y Z A B C D E F G H I J K L M N O P Q R S T U V
...
```

#### **SCSA Key Terms**
*   **Polyalphabetic Substitution:** A cipher system that uses multiple shifting alphabets throughout the encryption of a single message.
*   **Vigenère Cipher:** A cryptographic method that encrypts alphabetic text using a series of interwoven Caesar ciphers based on the letters of a keyword.
*   **Tabula Recta:** A square grid of alphabets shifted sequentially, used to perform Vigenère encryption and decryption.

---

### See It Worked
#### **The Scenario**
The **WA Junior Sports Carnival** coordinator needs to encrypt the secure database administrative password `"SCSA"` using the keyword key `"WEST"`.

Let's trace this manual encryption step-by-step using the Tabula Recta:

```
Plaintext Letter:  S      C      S      A
Keystream Letter:  W      E      S      T
                   │      │      │      │
                   ▼      ▼      ▼      ▼
(Vigenère Grid)  Row W  Row E  Row S  Row T
                 Col S  Col C  Col S  Col A
                   │      │      │      │
                   ▼      ▼      ▼      ▼
Ciphertext:        O      G      K      T
```

#### **How the Logic Flows**
1.  **For the first letter 'S':**
    *   Find the row starting with the keystream letter **`W`** on the left vertical axis.
    *   Find the column starting with the plaintext letter **`S`** on the top horizontal axis.
    *   Trace their intersection in the grid. The letter at the intersection is **`O`**.
2.  **For the second letter 'C':**
    *   Find row **`E`** and column **`C`**. Their intersection is **`G`**.
3.  **For the third letter 'S':**
    *   Find row **`S`** and column **`S`**. Their intersection is **`K`**.
4.  **For the fourth letter 'A':**
    *   Find row **`T`** and column **`A`**. Their intersection is **`T`**.
5.  **Plaintext `"SCSA"` encrypted with key `"WEST"` results in Ciphertext `"OGKT"`**.

*Observe:* Plaintext letters `S` at index 0 and index 2 encrypted to *different* ciphertext characters (`O` and `K`) because their matching keystream letters were different (`W` and `S`). This completely flattens simple single-character pattern traces!

---

### Try It with Help
#### **The Problem**
Decrypt the ciphertext `"XGZF"` using the Vigenère keyword `"RUN"`.

#### **Structural Hints**
*   **Write out the Keystream:** Match the repeating keyword letters to the ciphertext:
    ```
    Ciphertext:  X  G  Z  F
    Keystream:   R  U  N  R  (Keyword "RUN" repeated)
    ```
*   **Reverse Grid Tracing:**
    *   To decrypt, go to the vertical row of the keystream letter (e.g., Row **`R`**).
    *   Search along Row **`R`** horizontally until you locate the ciphertext letter (e.g., **`X`**).
    *   Trace straight up to the top header column to identify the plaintext letter (e.g., **`G`**).

#### **Scaffolded Student Steps**
1.  Row **`R`** $ightarrow$ Search for **`X`** $ightarrow$ Trace Up $ightarrow$ **`G`**.
2.  Row **`U`** $ightarrow$ Search for **`G`** $ightarrow$ Trace Up $ightarrow$ ???
3.  Row **`N`** $ightarrow$ Search for **`Z`** $ightarrow$ Trace Up $ightarrow$ ???
4.  Row **`R`** $ightarrow$ Search for **`F`** $ightarrow$ Trace Up $ightarrow$ ???
5.  Plaintext = `G` ???

---

### Try It Yourself
#### **The Problem**
The sports registrar's office needs to manually decrypt a Vigenère-encrypted team list code: `"NGLZWP"`. The secret keyword key is `"WIN"`.

Using the algebraic shift decryption formula:
$$	ext{PlainLetter} = (	ext{CipherLetter} - 	ext{KeyLetter}) \pmod{26}$$
decrypt `"NGLZWP"` to reveal the underlying team name. Write out your index calculations for each of the six letters.

---

### Check Your Reasoning
#### **The Answer**
```
Ciphertext:  N   G   L   Z   W   P
Keystream:   W   I   N   W   I   N

1. Letter 1: 'N' (13) and 'W' (22)
   (13 - 22) % 26 = -9 % 26 = 17 -> 'R'
2. Letter 2: 'G' (6) and 'I' (8)
   (6 - 8) % 26 = -2 % 26 = 24 -> 'Y'
3. Letter 3: 'L' (11) and 'N' (13)
   (11 - 13) % 26 = -2 % 26 = 24 -> 'Y'
4. Letter 4: 'Z' (25) and 'W' (22)
   (25 - 22) % 26 = 3 % 26 = 3 -> 'D'
5. Letter 5: 'W' (22) and 'I' (8)
   (22 - 8) % 26 = 14 % 26 = 14 -> 'O'
6. Letter 6: 'P' (15) and 'N' (13)
   (15 - 13) % 26 = 2 % 26 = 2 -> 'C'

The decrypted plaintext is "RYYDOC".
```

#### **Common SCSA Student Errors**
*   **Incorrect Negative Modulo Calculations:** Students often calculate negative values incorrectly (e.g., writing `-9 % 26 = -9`). Under standard clock arithmetic (used in Python and cryptography), adding 26 corrects negative indices: `-9 + 26 = 17`.
*   **Using Row and Column interchangeably during decryption:** Attempting to look up ciphertext on the top horizontal bar instead of finding it within the horizontal row of the keystream letter.

---

### Review and Connect
You have mastered substitution and polyalphabetic encryption systems. Now, put on your hacker hat. On the next page, we will learn how cryptanalysts crack these codes using **Brute Force** and **Frequency Analysis** algorithms.

---

## Lesson 12.5: Cryptanalysis & Codebreaking

### Your Goal
Compare cryptanalysis attacks and manually execute letter frequency analysis to break monoalphabetic substitution ciphers.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 10.1: Ethical Hacking vs Unethical Hacking](./year-11-textbook-chapter-10.md#lesson-101-ethical-hacking-vs-unethical-hacking).
*   [Lesson 12.3: Substitution Ciphers](./year-11-textbook-chapter-12.md#lesson-12-3-substitution-ciphers).

### The Idea
**Cryptanalysis** is the study of analyzing information systems in order to study the hidden aspects of the systems, commonly used to find paths to decrypt encrypted data without knowing the secret key. There are two primary manual and programmatic approaches to breaking ciphers:

#### **1. Brute-Force Attack**
A brute-force attack involves systematically checking every single possible key combination until the correct plaintext is revealed.
*   **On Caesar Ciphers:** Since there are only 25 possible key shifts ($1$ to $25$), a computer (or a human with a pen) can brute-force a Caesar cipher in milliseconds by printing out all 25 shift options. The correct shift is immediately recognizable as readable English.
*   **On Modern Systems:** Unfeasible. An AES-128 bit key has $2^{128}$ combinations. If a supercomputer checked 1 trillion keys per second, it would still take $10^{18}$ years to scan the keyspace.

#### **2. Frequency Analysis**
Frequency analysis exploits the structural patterns of human language. In any standard written language, certain letters appear far more frequently than others.
*   **The English Rule:** In written English, the letter **`E`** is overwhelmingly the most common (appearing $pprox 12.7\%$ of the time), followed by **`T`** ($pprox 9.1\%$), **`A`** ($pprox 8.2\%$), and **`O`** ($pprox 7.5\%$).
*   **Applying the Crack:** If we intercept a long ciphertext encrypted with a monoalphabetic substitution cipher, we can count the frequency of each character. If the character **`X`** appears $13\%$ of the time, we can reasonably assume that `X` is the substitute for `E`. We then map other high-frequency characters to `T` and `A` until the text becomes legible.

```
[ MONOALPHABETIC VULNERABILITY ]
Ciphertext letter frequencies mirror the distribution curve of normal English.

[ POLYALPHABETIC DEFENSE ]
Because Vigenère rotates the shift per character, the letter frequencies are flattened, making simple frequency analysis impossible.
```

#### **SCSA Key Terms**
*   **Cryptanalysis:** The analysis and cracking of cryptographic systems without authorized possession of keys.
*   **Brute-Force Attack:** An attack method that systematically tries all possible values or keys until the correct one is found.
*   **Frequency Analysis:** The study of the frequency of letters or groups of letters in a ciphertext to decode monoalphabetic substitution ciphers.

---

### See It Worked
#### **The Scenario**
A security student at the **WA Junior Sports Carnival** intercepts a simple Caesar-encrypted telemetry broadcast containing athlete scores: `"PZA"` and wants to crack it using brute-force.

Let's brute-force `"PZA"` by testing all possible negative key shifts (1 to 10 shown here):

```
Shift Key | Decrypted Test Output | Readable?
----------|-----------------------|-----------
-1        | OYZ                   | No
-2        | NXY                   | No
-3        | MWX                   | No
-4        | LVW                   | No
-5        | KUV                   | No
-6        | JTU                   | No
-7        | IST                   | No
-8        | HRS                   | No
-9        | GQR                   | No
-10       | FPQ                   | No
...       | ...                   | ...
-19       | RUN                   | YES (Valid English Word!)
```

#### **How the Logic Flows**
*   At a shift index offset of `-19` (which is mathematically equivalent to `+7`), the ciphertext `"PZA"` resolves to the word **`RUN`**. 
*   Since all other outputs are meaningless letter salads, the system is cracked.

---

### Try It with Help
#### **The Problem**
You intercept a long paragraphs-long scrambled email from a competing sports academy encrypted with a monoalphabetic substitution cipher. You run a Python analysis script to count the occurrences of each ciphertext letter.

Help decode the first words by mapping the character counts to standard English frequencies.

#### **The Intercepted Frequency Counts**
*   Total characters analyzed: `850`
*   Top occurrences in ciphertext:
    1.  Character **`K`** $ightarrow$ Count: `108` ($12.7\%$)
    2.  Character **`P`** $ightarrow$ Count: `78` ($9.1\%$)
    3.  Character **`Q`** $ightarrow$ Count: `71` ($8.3\%$)

#### **Structural Hints**
*   Map the highest frequency character (`K` at $12.7\%$) to the most common English letter: **`E`**.
*   Map the second highest (`P` at $9.1\%$) to: **`T`**.
*   Map the third highest (`Q` at $8.3\%$) to: **`A`**.

#### **Scaffolded Decoding Template**
If the ciphertext starts with `"K Q P"`, replace the letters using your frequency mappings:
*   `K` $ightarrow$ `E`
*   `Q` $ightarrow$ `A`
*   `P` $ightarrow$ `T`
*   Decoded plaintext: `"E A T"` (meaningful English word!).

---

### Try It Yourself
#### **The Problem**
Explain why a polyalphabetic Vigenère cipher is highly resilient against simple letter frequency analysis attacks, whereas a Caesar cipher is highly vulnerable. Reference how character mapping distributions change under both models (approx. 100 words).

---

### Check Your Reasoning
#### **The Answer**
```
A Caesar cipher is vulnerable to frequency analysis because it is a monoalphabetic substitution system. This means it maintains a static 1:1 mapping: every plaintext letter 'E' always maps to the same ciphertext letter. Consequently, the statistical frequency distribution curve of the plaintext is preserved in the ciphertext, allowing cryptanalysts to map the most common ciphertext letters directly to 'E', 'T', and 'A'.

Conversely, a Vigenère cipher is polyalphabetic, utilizing a repeating keyword to dynamically shift each letter. This results in a 1-to-many mapping: a single plaintext 'E' can encrypt to multiple different ciphertext letters depending on its index position. This flattens the frequency distribution curve into a near-uniform spread, neutralizing simple frequency analysis.
```

#### **Common SCSA Student Errors**
*   **Believing Vigenère is "unbreakable":** Describing Vigenère as completely immune to all cryptanalysis. While resistant to *simple* frequency analysis, it can be broken using advanced techniques (like Kasiski examination) that identify repeating keyword cycle patterns.
*   **Confusing terms:** Conflating brute-force attacks (trying keys randomly/sequentially) with frequency analysis (structural pattern profiling).

---

## Teacher Support & Exam Module (Chapter 12)

### SCSA Syllabus Mapping
*   **Unit 2 Syllabus Link:** Authentication: characteristics of strong passwords, password policies, multi-factor authentication, biometrics (FAR, FRR).
*   **Unit 2 Syllabus Link:** Encryption: symmetric vs. asymmetric, key-pairs, key distribution.
*   **Unit 2 Syllabus Link:** Cryptography: plaintext vs. ciphertext, Caesar and Vigenère ciphers, brute-force, frequency analysis.

### Prerequisite Diagnostic Checklist
Before delivering this chapter, ensure students have complete mastery over:
1.  **Modulo Math (Chapter 5):** Students must understand how to calculate `A % B` for negative numbers, as this is essential for manual cipher decryption.
2.  **DoD Model (Chapter 9):** Students should know how the Application and Transport layers operate to understand where encryption handshake certificates fit.

### Classroom Misconception Busters
1.  **The MFA Trap:** Many students believe entering a password and a security question is MFA. Emphasize that both are "something you know." MFA *must* cross-categorical boundaries (e.g., password + physical SMS token).
2.  **The Biometric Myth:** Students assume biometrics are impenetrable. Teach them about FAR and FRR, and explain that fingerprints can be lifted and spoofed.
3.  **The Key-Exchange Confusion:** Students often get confused about which key encrypts and which decrypts in asymmetric cryptosystems. Drill this rule: **"Encrypt with the receiver's public key; decrypt with the receiver's private key."**

---

## Chapter 12: Classroom Assessment
**Time Allowed: 25 minutes**  
**Total Marks: 20 marks**

### Section A: Short Answer (10 marks)

#### **Question 1 (3 marks)**
The WA Junior Sports Carnival registration portal is upgrading its security profile.
*   State the **three factors of authentication** (1.5 marks).
*   Explain how combining two of these factors improves system resilience compared to standard password entry (1.5 marks).

#### **Question 2 (4 marks)**
A medical imaging database in Bunbury needs to encrypt its cloud storage backup files.
*   Compare symmetric and asymmetric encryption systems, discussing **one advantage** and **one disadvantage** of each (2 marks).
*   Justify which system is most appropriate for encrypting a 50GB database backup archive stored locally (2 marks).

#### **Question 3 (3 marks)**
A client is worried about biometric fingerprint sensors deployed on laptops for regional coaches.
*   Define **False Acceptance Rate (FAR)** and **False Rejection Rate (FRR)** (2 marks).
*   State which metric, if set too high, poses the greatest security breach risk to the system (1 mark).

---

### Section B: Practical Cryptography (10 marks)

#### **Question 4 (4 marks)**
Encrypt the following plaintext team code: `"WIN"` using a Caesar rotation cipher with a shift key of **`+8`**. Show your mathematical step-by-step calculations for each letter index.

#### **Question 5 (6 marks)**
An administrative message has been intercepted during the sports carnival: `"XKOZ"`. Cryptanalysts know the message was encrypted using a Vigenère cipher with the keyword key **`"RUN"`**.
*   Write out the keystream alignment for the intercepted message (2 marks).
*   Manually decrypt `"XKOZ"` to reveal the secret word. Show your step-by-step index offset calculations (4 marks).

---

## Classroom Assessment Marking Guide & Solutions

### Section A: Short Answer Solutions

#### **Question 1 Marking Guidelines**
*   **Award 0.5 marks per factor listed:** Something you know, something you have, and something you are. (Max 1.5 marks).
*   **Award 1.5 marks for explanation:** Explaining that a remote hacker who steals a password (something you know) cannot log in because they do not have physical possession of the secondary device (something you have) or the physical biometric profile (something you are). Must mention the independence of factors.

#### **Question 2 Marking Guidelines**
*   **Award 2 marks for comparison:**
    *   Symmetric: Advantage is execution speed; disadvantage is the Key Distribution Problem.
    *   Asymmetric: Advantage is secure key sharing (resolves distribution issue); disadvantage is slow computational speed.
*   **Award 2 marks for justification:** Symmetric (AES) is the appropriate choice. A 50GB database is exceptionally large; encrypting it using asymmetric systems is computationally unfeasible and would throttle server hardware resources. Key distribution is not a risk because the backup is stored and restored internally by trusted local admins.

#### **Question 3 Marking Guidelines**
*   **Award 1 mark for FAR definition:** FAR is the probability that a biometric system incorrectly authorizes an unregistered/unauthorized user.
*   **Award 1 mark for FRR definition:** FRR is the probability that a biometric system incorrectly denies access to an authorized user.
*   **Award 1 mark for identifying the greatest risk:** **False Acceptance Rate (FAR)** poses the greatest security risk because it allows an attacker to bypass authorization boundaries and access sensitive data records.

---

### Section B: Practical Cryptography Solutions

#### **Question 4 Marking Guidelines**
*   **Award 1 mark per correct letter encryption calculation (3 marks total).**
*   **Award 1 mark for the correct final ciphertext: `"EQV"` (1 mark).**

*Mathematical Trace:*
*   `W` (22) $ightarrow (22 + 8) = 30 ightarrow 30 \% 26 = 4 ightarrow$ **`E`**
*   `I` (8) $ightarrow (8 + 8) = 16 ightarrow 16 \% 26 = 16 ightarrow$ **`Q`**
*   `N` (13) $ightarrow (13 + 8) = 21 ightarrow 21 \% 26 = 21 ightarrow$ **`V`**

#### **Question 5 Marking Guidelines**
*   **Award 2 marks for correct keystream alignment (1 mark for key letter matching, 1 mark for index identification):**
    ```
    Ciphertext:  X (23)   K (10)   O (14)   Z (25)
    Keystream:   R (17)   U (20)   N (13)   R (17)
    ```
*   **Award 4 marks for decryption trace calculations (1 mark per letter):**
    *   Letter 1: $(23 - 17) \% 26 = 6 \% 26 = 6 ightarrow$ **`G`**
    *   Letter 2: $(10 - 20) \% 26 = -10 \% 26 = 16 ightarrow$ **`Q`**
    *   Letter 3: $(14 - 13) \% 26 = 1 \% 26 = 1 ightarrow$ **`B`**
    *   Letter 4: $(25 - 17) \% 26 = 8 \% 26 = 8 ightarrow$ **`I`**
*   **The decrypted plaintext is `"GQBI"`**.
