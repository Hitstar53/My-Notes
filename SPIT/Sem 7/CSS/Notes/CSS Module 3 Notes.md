### Module 3.1: Hashing Algorithms
#### Cryptographic Hash Function & Applications


#### Simple Hash Functions & Requirements


#### Secure Hashing Algorithm (SHA)


#### Digital Signatures


#### Digital Signature Schemes



### Module 3.2: Authentication Protocols
#### Key Management & Distribution


#### Kerberos


#### Symmetric Key Agreement


#### Public Key Distribution


#### Entity Authentication
Entity authentication is a technique designed to let one party prove the identity of another party. An entity can be a person, a process, a client, or a server. The entity whose identity needs to be proved is called the claimant; the party that tries to prove the identity of the claimant is called the verifier. When Bob tries to prove the identity of Alice, Alice is the claimant, and Bob is the verifier.
##### Data-Origin Versus Entity Authentication 
There are two differences between message authentication (data-origin authentication), and entity authentication: 
1. **Message authentication** (or data-origin authentication) might not happen in real time; entity authentication does. In the former, Alice sends a message to Bob. When Bob authenticates the message, Alice may or may not be present in the communication process. On the other hand, when Alice requests entity authentication, there is no real message communication involved until Alice is authenticated by Bob. Alice needs to be online and to take part in the process. Only after she is authenticated can messages be communicated between Alice and Bob. Data-origin authentication is required when an email is sent from Alice to Bob. Entity authentication is required when Alice gets cash from an automatic teller machine. 
2. **Message authentication** simply authenticates one message; the process needs to be repeated for each new message. Entity authentication authenticates the claimant for the entire duration of a session. 

In entity authentication the claimant must identify herself to the verifier. This can be done with one of three kinds of witnesses: something known, something possessed, or something inherent.
1. **Something known:** This is a secret known only by the claimant that can be checked by the verifier. Examples are a password, a PIN, a secret key, and a private key.
2. **Something possessed:** This is something that can prove the claimant’s identity. Examples are a passport, a driver’s license, an identification card, a credit card, and a smart card.
3. **Something inherent:** This is an inherent characteristic of the claimant. Exam- ples are conventional signatures, fingerprints, voice, facial characteristics, retinal pattern, and handwriting

##### PASSWORDS 
The simplest and oldest method of entity authentication is the password-based authentication, where the password is something that the claimant knows. A password is used when a user needs to access a system to use the system’s resources (login). Each user has a user identification that is public, and a password that is private. We can divide these authentication schemes into two groups: the fixed password and the one-time password. 

##### Fixed Password 
A fixed password is a password that is used over and over again for every access. Several schemes have been built, one upon the other.

**First Approach**
In the very rudimentary approach, the system keeps a table (a file) that is sorted by user identification. To access the system resources, the user sends her user identification and password, in plaintext, to the system. The system uses the identification to find the password in the table. If the password sent by the user matches the password in the table, access is granted; otherwise, it is denied. Attacks on the First Approach This approach is subject to several kinds of attacks:
1. Eavesdropping
2. Stealing a password
3. Accessing a password file
4. Guessing

**Second Approach**
A more secure approach is to store the hash of the password (instead of the plaintext password) in the password file. Any user can read the contents of the file, but, because the hash function is a one-way function, it is almost impossible to guess the value of the password. Figure 14.2 shows the situation. When the password is created, the system hashes it and stores the hash in the password file. When the user sends the ID and the password, the system creates a hash of the password and then compares the hash value with the one stored in the file. If there is a match, the user is granted access; otherwise, access is denied. In this case, the file does not need to be read protected. This approach is **weak against Dictionary Attack**.

**Third Approach**
The third approach is called **salting** the password. When the password string is created, a random string, called the salt, is concatenated to the password. The salted password is then hashed. The ID, the salt, and the hash are then stored in the file. Now, when a user asks for access, the system extracts the salt, concatenates it with the received password, makes a hash out of the result, and compares it with the hash stored in the file. If there is a match, access is granted; otherwise, it is denied. Salting makes the **dictionary attack more difficult**. If the original password is 6 digits and the salt is 4 digits, then hashing is done over a 10-digit value. This means that Eve now needs to make a list of 10 million items and create a hash for each of them. The list of hashes has 10 million entries, and the comparison takes much longer. Salting is very effective if the salt is a very long random number. The UNIX operating system uses a variation of this method.

**Fourth Approach**
In the fourth approach, two identification techniques are combined. A good example of this type of authentication is the use of an ATM card with a PIN (personal identification number). The card belongs to the category “something possessed ” and the PIN belongs to the category “something known”. The PIN is a password that enhances the security of the card. If the card is stolen, it cannot be used unless the PIN is known. The PIN number, however, is traditionally very short so it is easily remembered by the owner. This makes it vulnerable to the **guessing type of attack**.

##### One Time Password
A one-time password is a password that is used only once. This kind of password makes eavesdropping and salting useless. Three approaches:

**First Approach**
In the first approach, the user and the system agree upon a list of passwords. Each pass- word on the list can be used only once. There are some drawbacks to this approach. First, the system and the user must keep a long list of passwords. Second, if the user does not use the passwords in sequence, the system needs to perform a long search to find the match. This scheme makes eavesdropping and reuse of the password useless. The password is valid only once and cannot be used again

**Second Approach**
In the second approach, the user and the system agree to sequentially update the pass- word. The user and the system agree on an original password, P1, which is valid only for the first access. During the first access, the user generates a new password, P2, and encrypts this password with P1 as the key. P2 is the password for the second access. During the second access, the user generates a new password, P3, and encrypts it with P2; P3 is used for the third access. In other words, Pi is used to create Pi+1. Of course, if Eve can guess the first password (P1), she can find all of the subsequent one

**Third Approach**
In the third approach, the user and the system create a sequentially updated password using a hash function In this approach, elegantly devised by Leslie Lampert, the user and the system agree upon an original password, P0, and a counter, n. The system calculates hn(P0), where hn means applying a hash function n times. In other words, The system stores the identity of Alice, the value of n, and the value of hn(P0).

##### CHALLENGE-RESPONSE
In password authentication, the claimant proves her identity by demonstrating that she knows a secret, the password. However, because the claimant reveals this secret, it is susceptible to interception by the adversary. In challenge-response authentication, the claimant proves that she knows a secret without sending it.

In challenge-response authentication, the claimant proves that she knows a secret without sending it to the verifier. The challenge is a time-varying value sent by the verifier; the response is the result of a function applied on the challenge.

Methods:
1. **Using a Symmetric-key Cipher:** Several approaches to challenge-response authentication use symmetric-key encryption. The secret here is the shared secret key, known by both the claimant and the verifier. The function is the encrypting algorithm applied on the challenge
2. 
3. **Using Keyed-Hash Function:** Instead of using encryption/decryption for entity authentication, we can also use a keyed-hash function (MAC). One advantage to the scheme is that it preserves the integrity of challenge and response messages and at the same time uses a secret, the key. Note that in this case, the timestamp is sent both as plaintext and as text scrambled by the keyed-hash function. When Bob receives the message, he takes the plaintext T, applies the keyed-hash function, and then compares his calculation with what he received to determine the authenticity of Alice.
4. 
5. **Using an Asymmetric-key Cipher:**  Using an Asymmetric-Key Cipher Instead of a symmetric-key cipher, we can use an asymmetric-key cipher for entity authentication. Here the secret must be the private key of the claimant. The claimant must show that she owns the private key related to the public key that is available to everyone. This means that the verifier must encrypt the challenge using the public key of the claimant; the claimant then decrypts the message using her private key. The response to the challenge is the decrypted challenge.
6. 
7. **Using Digital Signature:** Entity authentication can also be achieved using a digital signature. When a digital signature is used for entity authentication, the claimant uses her private key for signing.

##### Zero Knowledge
In zero-knowledge authentication, the claimant does not reveal anything that might endanger the confidentiality of the secret. The claimant proves to the verifier that she knows a secret, without revealing it. The interactions are so designed that they cannot lead to revealing or guessing the secret.

##### Biometrics
Biometrics is the measurement of physiological or behavioral features that identify a person (authentication by something inherent). Biometrics measures features that cannot be guessed, stolen, or shared.

#### Security at Application Layer
