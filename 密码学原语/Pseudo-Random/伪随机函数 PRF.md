## 伪随机函数/pseudorandom function/PRF

- PRF 和 PRG：
	- [PRG](https://blog.csdn.net/qq_41545715/article/details/121255088)：$s:\{0,1\}^n \rightarrow G(s):\{0,1\}^{l(n)}$，讨论的是字符串 $G(s)$ 分布的伪随机性。
	- PRF：$F_k:\{0,1\}^n\rightarrow \{0,1\}^n$ ，讨论的是函数 $F_k$ 分布的伪随机性，是 PRG 的扩展。
- 真随机函数 $f\in Func_n$：
    - 函数族 $Func_n$：所有 $n$ 比特字符串到 $n$ 比特字符串的函数
    - 函数族大小：对于一个函数，输入 $x\in \{0,1\}^n$ ，有 $2^n$ 种；对于每一种输入，有一个 $n$ 长的输出；有 $2^n$ 行， $n$ 列，这个矩阵大小为 $n\cdot 2^n$ ，这表示了一个函数；这个函数族大小为$∣Funcn∣=2^{n\cdot 2^n}$。
    - 如何取真随机函数 $f$ ：由于一个真随机函数要用 $n\cdot 2^n$ 位表示，是一个指数的输入，多项式时间区分者 $D$ 没有足够的时间得到完整输入，需要询问 $oracle\ O$ 。$oracle\ O$ 是一个确定性函数，执行伪随机函数 $F_k$ （$k$ 随机）或真随机函数 $f$ ， $D$ 可以询问多项式次。
- 定义： $F：\{0,1\}^*\times \{0,1\}^*\rightarrow \{0,1\}^*$，如果对于所有 PPT 区分者 $D$  都有 $|Pr[D^{F_k(\cdot)}(1^n)=1]-Pr[D^{f(\cdot)}(1^n)=1]|\le negl(n)$，则 $F$ 是伪随机函数。

## PRF 与 PRG 的区别

- PRG 的输入只需要一个种子，而 PRF 的输入，除了种子，还需要一个上下文数据，通常是由一个随机数或密钥充当。
- PRG 输出是一个伪随机数，而 PRF 的输出是一个可以指定长度的伪随机值，或者说伪随机字符串。


##  不经意伪随机函数(Oblivious Pseudo Random Function, OPRF)

![[Pasted image 20221022115929.png]]

- 假设 Alice 有些输入， Bob 有一个 $key$ 。 OPRF 允许 Alice 将自己的输入与Bob 的 $key$ 结合经过一系列运算转变成相对应的数。
- 在这个过程中，Alice 不能知道 Bob 的 $key$ , Bob 也不知道最后的结果 $F(key,x)$ . 每个输入 $x_ i$ 都可以计算出一个不同于其他输入的数，这些数就可以被看作伪随机数。
