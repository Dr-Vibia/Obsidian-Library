**ID-based encryption**, or **identity-based encryption** (**IBE**), is an important primitive of [ID-based cryptography](https://en.wikipedia.org/wiki/ID-based_cryptography "ID-based cryptography"). As such it is a type of [public-key encryption](https://en.wikipedia.org/wiki/Public-key_encryption "Public-key encryption") in which the [public key](https://en.wikipedia.org/wiki/Public_key "Public key") of a user is some unique information about the identity of the user (e.g. a user's email address). This means that a sender who has access to the public parameters of the system can encrypt a message using e.g. the text-value of the receiver's name or email address as a key. The receiver obtains its decryption key from a central authority, which needs to be trusted as it generates secret keys for every user.

The [pairing](https://en.wikipedia.org/wiki/Pairing-based_cryptography "Pairing-based cryptography")-based [Boneh–Franklin scheme](https://en.wikipedia.org/wiki/Boneh%E2%80%93Franklin_scheme "Boneh–Franklin scheme") and [Cocks's encryption scheme](https://en.wikipedia.org/wiki/Cocks_IBE_scheme "Cocks IBE scheme")based on [quadratic residues](https://en.wikipedia.org/wiki/Quadratic_residue "Quadratic residue") both solved the IBE problem in 2001.

## Usage

Identity-based systems allow any party to generate a public key from a known identity value such as an ASCII string. A trusted third party, called the [Private Key Generator](https://en.wikipedia.org/w/index.php?title=Private_Key_Generator&action=edit&redlink=1 "Private Key Generator (page does not exist)") (PKG), generates the corresponding private keys. To operate, the PKG first publishes a master public key, and retains the corresponding **master private key** (referred to as _master key_). Given the master public key, any party can compute a public key corresponding to the identity by combining the master public key with the identity value. To obtain a corresponding private key, the party authorized to use the identity _ID_ contacts the PKG, which uses the master private key to generate the private key for identity _ID_.

As a result, parties may encrypt messages (or verify signatures) with no prior distribution of keys between individual participants. This is extremely useful in cases where pre-distribution of authenticated keys is inconvenient or infeasible due to technical restraints. However, to decrypt or sign messages, the authorized user must obtain the appropriate private key from the PKG. A caveat of this approach is that the PKG must be highly trusted, as it is capable of generating any user's private key and may therefore decrypt (or sign) messages without authorization. Because any user's private key can be generated through the use of the third party's secret, this system has inherent [key escrow](https://en.wikipedia.org/wiki/Key_escrow "Key escrow"). A number of variant systems have been proposed which remove the escrow including [certificate-based encryption](https://en.wikipedia.org/wiki/Certificate-based_encryption "Certificate-based encryption"),[secure key issuing cryptography](https://en.wikipedia.org/wiki/Secure_key_issuing_cryptography "Secure key issuing cryptography") and [certificateless cryptography](https://en.wikipedia.org/wiki/Certificateless_cryptography "Certificateless cryptography").

The steps involved are depicted in this diagram:

![[Pasted image 20220928212700.png]]

## Protocol framework

[Dan Boneh](https://en.wikipedia.org/wiki/Dan_Boneh "Dan Boneh") and [Matthew K. Franklin](https://en.wikipedia.org/wiki/Matthew_K._Franklin "Matthew K. Franklin") defined a set of four algorithms that form a complete IBE system:

- **Setup**: This algorithm is run by the PKG one time for creating the whole IBE environment. The master key is kept secret and used to derive users' private keys, while the system parameters are made public. It accepts a [security parameter](https://en.wikipedia.org/wiki/Security_parameter "Security parameter") $k$ (i.e. binary length of key material) and outputs:
	1.  A set $P$ of system parameters, including the message space and ciphertext space $M$ and $C$，
	2.  a master key $K_m$.
- **Extract**: This algorithm is run by the PKG when a user requests his private key. Note that the verification of the authenticity of the requestor and the secure transport of $d$ are problems with which IBE protocols do not try to deal. It takes as input $P$, $K_m$ and an identifier $ID\in \left\{0,1\right\}^{*}$ and returns the private key $d$ for user $ID$.
- **Encrypt**: Takes $P$, a message $m \in {M}$ and $ID\in \left\{0,1\right\}^{*}$ and outputs the encryption $c\in {C}$.
- **Decrypt**: Accepts $d$, $P$ and $c\in {C}$ and returns $m\in{M}$.

### Correctness constraint

In order for the whole system to work, one has to postulate that:${\displaystyle \forall m\in {\mathcal {M}},ID\in \left\{0,1\right\}^{*}:\mathrm {Decrypt} \left(\mathrm {Extract} \left({\mathcal {P}},K_{m},ID\right),{\mathcal {P}},\mathrm {Encrypt} \left({\mathcal {P}},m,ID\right)\right)=m}$

## Encryption schemes

The most efficient identity-based encryption schemes are currently based on [bilinear pairings](https://en.wikipedia.org/wiki/Pairing "Pairing") on [elliptic curves](https://en.wikipedia.org/wiki/Elliptic_curves "Elliptic curves"), such as the [Weil](https://en.wikipedia.org/wiki/Weil_pairing "Weil pairing") or [Tate](https://en.wikipedia.org/wiki/Tate_pairing "Tate pairing") pairings. The first of these schemes was developed by [Dan Boneh](https://en.wikipedia.org/wiki/Dan_Boneh "Dan Boneh") and [Matthew K. Franklin](https://en.wikipedia.org/wiki/Matthew_K._Franklin "Matthew K. Franklin") (2001), and performs [probabilistic encryption](https://en.wikipedia.org/wiki/Probabilistic_encryption "Probabilistic encryption") of arbitrary ciphertexts using an [Elgamal](https://en.wikipedia.org/wiki/ElGamal_encryption "ElGamal encryption")-like approach. Though the [Boneh-Franklin scheme](https://en.wikipedia.org/wiki/BonehFranklinScheme "BonehFranklinScheme") is [provably secure](https://en.wikipedia.org/wiki/Provable_security "Provable security"), the security proof rests on relatively new assumptions about the hardness of problems in certain elliptic curve groups.

Another approach to identity-based encryption was proposed by [Clifford Cocks](https://en.wikipedia.org/wiki/Clifford_Cocks "Clifford Cocks") in 2001. The [Cocks IBE scheme](https://en.wikipedia.org/wiki/Cocks_IBE_scheme "Cocks IBE scheme") is based on well-studied assumptions (the [quadratic residuosity assumption](https://en.wikipedia.org/wiki/Quadratic_residuosity_problem "Quadratic residuosity problem")) but encrypts messages one bit at a time with a high degree of [ciphertext expansion](https://en.wikipedia.org/wiki/Ciphertext_expansion "Ciphertext expansion"). Thus it is highly inefficient and impractical for sending all but the shortest messages, such as a session key for use with a [symmetric cipher](https://en.wikipedia.org/wiki/Symmetric_cipher "Symmetric cipher").

A third approach to IBE is through the use of lattices.

### Identity-based encryption algorithms

The following lists practical identity-based encryption algorithms

-   [Boneh–Franklin](https://en.wikipedia.org/wiki/Boneh%E2%80%93Franklin_scheme "Boneh–Franklin scheme") (BF-IBE).
-   [Sakai–Kasahara](https://en.wikipedia.org/wiki/Sakai%E2%80%93Kasahara_scheme "Sakai–Kasahara scheme") (SK-IBE).
-   Boneh–Boyen (BB-IBE).

All these algorithms have security proofs.

## Advantages

One of the major advantages of any identity-based encryption scheme is that if there are only a finite number of users, after all users have been issued with keys the third party's secret can be destroyed. This can take place because this system assumes that, once issued, keys are always valid (as this basic system lacks a method of key revocation. The majority of derivatives of this system which have key revocation lose this advantage.

Moreover, as public keys are derived from identifiers, IBE eliminates the need for a public key distribution infrastructure. The authenticity of the public keys is guaranteed implicitly as long as the transport of the private keys to the corresponding user is kept secure (authenticity, integrity, confidentiality).

Apart from these aspects, IBE offers interesting features emanating from the possibility to encode additional information into the identifier. For instance, a sender might specify an expiration date for a message. He appends this timestamp to the actual recipient's identity (possibly using some binary format like X.509). When the receiver contacts the PKG to retrieve the private key for this public key, the PKG can evaluate the identifier and decline the extraction if the expiration date has passed. Generally, embedding data in the ID corresponds to opening an additional channel between sender and PKG with authenticity guaranteed through the dependency of the private key on the identifier.

## Drawbacks

- If a Private Key Generator (PKG) is compromised, all messages protected over the entire lifetime of the public-private key pair used by that server are also compromised. This makes the PKG a high-value target to adversaries. To limit the exposure due to a compromised server, the master private-public key pair could be updated with a new independent key pair. However, this introduces a key-management problem where all users must have the most recent public key for the server.
- Because the Private Key Generator (PKG) generates private keys for users, it may decrypt and/or sign any message without authorization. This implies that IBS systems cannot be used for [non-repudiation](https://en.wikipedia.org/wiki/Non-repudiation "Non-repudiation"). This may not be an issue for organizations that host their own PKG and are willing to trust their system administrators and do not require non-repudiation.
- The issue of implicit key escrow does not exist with the current PKI system, wherein private keys are usually generated on the user's computer. Depending on the context key escrow can be seen as a positive feature (e.g., within Enterprises). A number of variant systems have been proposed which remove the escrow including [certificate-based encryption](https://en.wikipedia.org/wiki/Certificate-based_encryption "Certificate-based encryption"), [secret sharing](https://en.wikipedia.org/wiki/Secret_sharing "Secret sharing"), [secure key issuing cryptography](https://en.wikipedia.org/wiki/Secure_key_issuing_cryptography "Secure key issuing cryptography") and [certificateless cryptography](https://en.wikipedia.org/wiki/Certificateless_cryptography "Certificateless cryptography").
- A secure channel between a user and the Private Key Generator (PKG) is required for transmitting the private key on joining the system. Here, a SSL-like connection is a common solution for a large-scale system. It is important to observe that users that hold accounts with the PKG must be able to authenticate themselves. In principle, this may be achieved through username, password or through public key pairs managed on smart cards.
- IBE solutions may rely on cryptographic techniques that are insecure against code breaking quantum computer attacks (see Shor's algorithm)