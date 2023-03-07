**Attribute-based encryption** is a type of public-key encryption in which the secret key of a user and the ciphertext are dependent upon attributes (e.g. the country in which they live, or the kind of subscription they have). In such a system, the decryption of a ciphertext is possible only if the set of attributes of the user key matches the attributes of the ciphertext.

A crucial security aspect of attribute-based encryption is collusion-resistance: An adversary that holds multiple keys should only be able to access data if at least one individual key grants access.

## Types of attribute-based encryption schemes

There are mainly two types of attribute-based encryption schemes: Key-policy attribute-based encryption (KP-ABE) and ciphertext-policy attribute-based encryption (CP-ABE).

In KP-ABE, users' secret keys are generated based on an access tree that defines the privileges scope of the concerned user, and data are encrypted over a set of attributes. However, CP-ABE uses access trees to encrypt data and users' secret keys are generated over a set of attributes.

## Relationship to Role-based Encryption

The related concept of role-based encryption refers exclusively to access keys having roles that can be validated against an authoritative store of roles. In this sense, Role-based encryption can be expressed by Attribute-based encryption and within that limited context the two terms can be used interchangeably. Role-based Encryption cannot express Attribute-based encryption.

## Usage

Attribute-based encryption (ABE) can be used for log encryption. Instead of encrypting each part of a log with the keys of all recipients, it is possible to encrypt the log only with attributes which match recipients' attributes. This primitive can also be used for [broadcast encryption](https://en.wikipedia.org/wiki/Broadcast_encryption "Broadcast encryption") in order to decrease the number of keys used. Attribute-based encryption methods are also widely employed in vector-driven search engine interfaces.

### Challenges

Although the ABE concept is very powerful and a promising mechanism, ABE systems suffer mainly from two drawbacks: inefficiency and the lack of a straightforward attribute revocation mechanism.

Other main challenges are:

-   Key coordination
-   Key escrow
-   Key revocation

#### Attribute revocation mechanism

Revocation of users in cryptosystems is a well-studied but nontrivial problem. Revocation is even more challenging in attribute-based systems, given that each attribute possibly belongs to multiple different users, whereas in traditional PKI systems public/private key pairs are uniquely associated with a single user. In principle, in an ABE system, attributes, not users or keys, are revoked. The following paragraph now discusses how the revocation feature can be incorporated.

A simple but constrained solution is to include a time attribute. This solution would require each message to be encrypted with a modified access tree T0, which is constructed by augmenting the original access tree T with an additional time attribute. The time attribute, ζ represents the current ‘time period’. Formally, the new access structure T0 is as follows: {{{1}}}. For example, ζ can be the ‘date’ attribute whose value changes once every day. It is assumed that each non-revoked user receives his fresh private keys corresponding to the ‘date’ attribute once each day directly from the mobile key server MKS (which is the central authority) or via the regional delegates. With a hierarchical access structure, the key delegation property of CP-ABE can be exploited to reduce the dependency on the central authority for issuing the new private keys to all users every time interval. There are significant trade-offs between the extra load incurred by the authority for generating and communicating the new keys to the users and the amount of time that can elapse before a revoked user can be effectively purged. This above solution has the following problems:
1.  Each user X needs to periodically receive from the central authority the fresh private key corresponding to the time attribute, otherwise X will not be able to decrypt any message.
2.  It is a lazy revocation technique. The revoked user is not purged from the system until the current time period expires.
3.  This scheme requires an implicit time synchronization (a loose time synchronization may be sufficient) among the authority and the users.