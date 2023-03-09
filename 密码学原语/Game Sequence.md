## Transitions based on indistinguishability

In such a transition, a small change is made that, if detected by the adversary, would imply an efficient method of distinguishing between two distributions that are indistinguishable (either statistically or computationally). For example, suppose $P_1$ and $P_2$ are assumed to be computationally indistinguishable distributions. To prove that $|Pr[S_i]-Pr[Si+1]|$ is negligible, one argues that there exists a distinguishing algorithm D that “interpolates” between Game i and Game i+1, so that when given an element drawn from distribution P1 as input, D outputs 1 with probability Pr[Si], and when given an element drawn from distribution P2 as input, D outputs 1 with probabilty Pr[Si+1]. The indistinguishability assumption then implies that | Pr[Si] − Pr[Si+1]| is negligible. Usually, the construction of D is obvious, provided the changes made in the transition are minimal. Typically, one designs the two games so that they could easily be rewritten as a single “hybrid” game that takes an auxilliary input — if the auxiallary input is drawn from P1, you get Game i, and if drawn from P2, you get Game i + 1. The distinguisher then simply runs this single hybrid game with its input, and outputs 1 if the appropriate event occurs.


## Transitions based on failure events
### Difference Lemma



## Bridging steps

