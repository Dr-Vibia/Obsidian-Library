**Functional encryption** (**FE**) is a generalization of [public-key encryption](https://en.wikipedia.org/wiki/Public-key_encryption "Public-key encryption") in which possessing a secret key allows one to learn a function of what the [ciphertext](https://en.wikipedia.org/wiki/Ciphertext "Ciphertext") is encrypting.

## Formal definition

More precisely, a functional encryption scheme for a given functionality $f$ consists of the following four algorithms:

- $(pk,msk)←Setup(1^{\lambda})$:creates a public key $pk$ and a master secret key $msk$.
- $sk←Keygen(msk,f)$:uses the master secret key to generate a new secret key $sk$ for the function $f$.
- $c←Enc(pk,x)$:uses the public key to encrypt a message $x$.
- $y←Dec(sk,c)$:uses secret key to calculate $y=f(x)$ where $x$ is the value that $c$ encrypts.

The [security](https://en.wikipedia.org/wiki/Provable_security "Provable security") of FE requires that any information an adversary learns from an encryption of $x$ is revealed by $f(x)$. Formally, this is defined by simulation.

## Applications

Functional encryption generalizes several existing primitives including [Identity-based encryption](https://en.wikipedia.org/wiki/ID-based_encryption "ID-based encryption") (IBE) and [attribute-based encryption](https://en.wikipedia.org/wiki/Attribute-based_encryption "Attribute-based encryption") (ABE). In the IBE case, define $F(k,x)$ to be equal to $x$ when $k$ corresponds to an identity that is allowed to decrypt, and $\perp$ otherwise. Similarly, in the ABE case, define $F(k,x)=x$ when  $k$ encodes attributes with permission to decrypt and $\perp$ otherwise.

- [[Identity-based encryption (IBE)]] 身份基加密
- [[Attribute-based encryption (ABE)]] 属性基加密
- [[Predicate Encryption (PE)]] 谓词加密
- Inner Product Encryption 内积加密

![[Pasted image 20220927230124.png]]

[函数加密最后解密得到的结果是什么？](https://www.zhihu.com/question/390740283/answer/1857107970)
