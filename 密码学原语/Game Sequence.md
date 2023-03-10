## Transitions based on indistinguishability

In such a transition, a small change is made that, if detected by the adversary, would imply an efficient method of distinguishing between two distributions that are indistinguishable (either statistically or computationally). For example, suppose $P_1$ and $P_2$ are assumed to be computationally indistinguishable distributions. To prove that $|Pr[S_i]-Pr[S_{i+1}]|$ is negligible, one argues that there exists a distinguishing algorithm $D$ that “interpolates” between Game $i$ and Game $i+1$, so that when given an element drawn from distribution $P_1$ as input, $D$ outputs $1$ with probability $Pr[S_i]$, and when given an element drawn from distribution $P_2$ as input, $D$ outputs $1$ with probabilty $Pr[S_{i+1}]$. The indistinguishability assumption then implies that $|Pr[S_i]-Pr[S_{i+1}]|$ is negligible. Usually, the construction of $D$ is obvious, provided the changes made in the transition are minimal. Typically, one designs the two games so that they could easily be rewritten as a single “hybrid” game that takes an auxilliary input — if the auxiallary input is drawn from $P_1$, you get Game $i$, and if drawn from $P_2$, you get Game $i+1$. The distinguisher then simply runs this single hybrid game with its input, and outputs $1$ if the appropriate event occurs.


## Transitions based on failure events

In such a transition, one argues that Games $i$ and $i + 1$ proceed identically unless a certain “failure event” $F$ occurs. To make this type of argument as cleanly as possible, it is best if the two games are defined on the same underlying probability space — the only differences between the two games are the rules for computing certain random variables. When done this way, saying that the two games proceed identically unless $F$ occurs is equivalent to saying that
$$
S_i\wedge\neg F\Longleftrightarrow S_{i+1}\wedge\neg F,
$$
that is, the events $S_i\wedge\neg F$ and $S_{i+1}\wedge\neg F$ are the same. If this is true, then we can use the following fact, which is completely trivial, yet is so often used in these types of proofs that it deserves a name:
> 除非事件 $F$ 发生，否则两个游戏的进程是相同的。

### Difference Lemma

Let $A,B,F$ be events defined in some probability distribution, and suppose that $A\wedge\neg F\Longleftrightarrow B\wedge\neg F$ . Then $|Pr[A]-Pr[B]|\le Pr[F]$.


## Bridging steps

The third type of transition introduces a bridging step, which is typically a way of restating how certain quantities can be computed in a completely equivalent way. The change is purely conceptual, and $Pr[S_i] =Pr[S_{i+1}]$. The reason for doing this is to prepare the ground for a transition of one of the above two types. While in principle, such a bridging step may seem unnecessary, without it, the proof would be much harder to follow.
> 重申如何以完全等效的方式计算某些数量（纯粹概念上的变化）。
> 它的目的是为上述两种类型之一的过渡做准备。

As mentioned above, in a transition based on a failure event, it is best if the two successive games are understood to be defined on the same underlying probability space. This is an important point, which we repeat here for emphasis — it seems that proofs are easiest to understand if one does not need to compare “corresponding” events across distinct and (by design) quite different probability spaces. Actually, it is good practice to simply have all the games in the sequence defined on the same underlying probability space. However, the Difference Lemma generalizes in the obvious way as follows: if $A, B, F_1$ and $F_2$ are events such that $Pr[A\wedge\neg F_1]=Pr[B\wedge\neg F_2]$ and $Pr[F_1]=Pr[F_2]$, then $|Pr[A]-Pr[B]|\le Pr[F_1]$. With this generalized version, one may (if one wishes) analyze transitions based on failure events when the underlying probability spaces are not the same.
