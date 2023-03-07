A watermarkable PRF , $WPRF = (Setup, KeyGen, Eval, Mark, Extract)$ with key space $K$, input space $\{0, 1\}^n$, output space $\{0, 1\}^m$, and message space $M$ consists of the following algorithms:

- $Setup(1^λ)\rightarrow(P P, M K, EK)$ : On input the security parameter $\lambda$ , the setup algorithm outputs the public parameter $PP$ , the mark key $MK$ and the extraction key $EK$ . 
- $KeyGen(PP)\rightarrow k$ : On input the public parameter $PP$ , the key generation algorithm outputs a PRF key $k \in K$ .
- $Eval(PP,k,x)\rightarrow y$ : On input the public parameter $PP$ , a PRF key $k\in K$, and an input $x\in\{0,1\}^n$ , the evaluation algorithm outputs an output $y\in\{0,1\}^m$ .
- $Mark(PP,MK,k,msg)\rightarrow C$ : On input the public parameter $PP$ , the mark key $MK$, a PRF key $k\in K$, and a message $msg\in M$, the marking algorithm outputs a marked circuit $C:\{0,1\}^n\rightarrow\{0,1\}^m$ . 
- $Extract(PP,EK,C)\rightarrow msg$ : On input the public parameter $PP$ , the extraction key $EK$, and a circuit $C$, the extraction algorithm outputs a message $m\in M\cup\{\perp\}$ , where $\perp$ denotes that the circuit is unmarked.

## Functionality Preserving

For any $msg\in M$, let $(PP,MK,EK)\leftarrow Setup(1^\lambda)$ , $k\leftarrow KeyGen(PP)$ , $C\leftarrow Mark(PP,MK,k,msg)$ , $x\leftarrow \{0,1\}^n$ , then we have $Pr[C(x)\ne Eval(PP,k,x)]\le negl(\lambda)$ .

> $Eval(P P, k, x)$ 是与 $C(x)$ 进行比较的

## Extraction Correctness

For any $msg\in M$, let $(PP,MK,EK)\leftarrow Setup(1^\lambda)$ , $k\leftarrow KeyGen(PP)$ , $C\leftarrow Mark(PP,MK,k,msg)$ , $x\leftarrow \{0,1\}^n$ , then we have $Pr[Extract(PP,EK,C)\ne msg]\le negl(\lambda)$ .

> 上述的两个 correctness properties 都是仅为了诚实的 PRF keys 而定义的.

## Watermarking Meaningfulness

For any circuit $C:\{0, 1\}n\rightarrow\{0, 1\}^m$ , let $(PP,MK,EK)\leftarrow Setup(1^\lambda)$ ， then we have: $Pr[Extract(PP,EK,C)\ne\perp]\le negl(\lambda)$ .