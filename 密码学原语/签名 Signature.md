A signature scheme consists of three PPT algorithms: 

- **KeyGen**. On input the security parameter $1^λ$, the key generation algorithm outputs a public key $pk$ and a secret key $sk$. 
- **Sign**. On input the secret key $sk$ and a message $m$, the sign algorithm outputs a signature $σ$.
- **Verify**. On input the public key $pk$, a message $m$ and a signature $σ$, the verification algorithm outputs a bit $b$. 

Also, it satisfies the following conditions:

- **Correctness**. For any message m, we have 
$$Pr[(pk, sk) ← KeyGen(1^λ), σ ← Sign(sk, m) : Verify(pk, m, σ) \ne 1] ≤ negl(λ)$$
- **Unforgeability**. For any PPT adversary $A$, we have: 
$$Pr [(pk, sk) ← KeyGen(1^λ); (m, σ) ← A^{S(·)}(pk); : m \notin M∧ Verify(pk, m, σ) = 1 ] ≤ negl(λ) $$
- where $S(·)$ is an oracle that takes as input a message $m$ and returns $Sign(sk, m)$, and $M$ consists of all messages submitted to the sign oracle $S(·)$.
> Unforgeability不可伪造性的含义：敌手通过签名预言机伪造的签名不在预言机收录的合法签名内且认证通过的可能性忽略不计