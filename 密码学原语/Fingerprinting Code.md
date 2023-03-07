A fingerprinting code $FC = (Gen, Dec)$ with message space $[1, N ]$ and code length $l$ consists of the following algorithms: 

- $Gen(1^\lambda) \rightarrow (td,\varGamma=(\bar{w}_m)_{m\in[N]})$ : On input the security parameter $\lambda$ , the code generation algorithm outputs the trapdoor $td$ and $N$ codewords $\bar{w}_1,\cdots,\bar{w}_N$ (for messages $1,\cdots,N$ respectively) in $\{0, 1\}^l$ . 
- $Dec(td, w) \rightarrow m$ : On input the trapdoor $td$ and a word $w\in\{0, 1\}^l$ ($w$ is not necessarily in $\varGamma$ ), the decoding algorithm outputs a message $m\in [1, N ]\cup \{\perp\}$ . 

The correctness property requires that the the decoding algorithm will decode codewords in $\varGamma$ correctly.

> $Gen(1^\lambda)$ 中的 $1^\lambda$ 是安全参数，它表示安全参数有 $\lambda$ 位
