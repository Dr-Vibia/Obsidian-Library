# 不经意传输（Oblivious Transfer，OT）

标准二选一的不经意传输是一个 $\rm S2PC$ 任务,其中一个参与者发送方（$S$ 表示）持有两个 $n$ 位长的字符串 $x_0$ 和 $x_1$ , 另外一个参与者接受方（$R$ 表示）通过选择位在发送方持有的两个数据字符串之间选择，$\sigma\in\left\{ 0,1\right\}$ 。在完成传输 $d$ 之后， $S$ 没有任何的输出和也不知道接受到的哪个字符串被接受，而 $R$ 已经收到字符串与 $\sigma$ 相对应的 $x_\sigma$ 但是它对其它字符串 $x_{1-\sigma}$ 一无所知。不经意传输被定义成一个函数 $F_{ot}$ ，它形式化的协议如图5所示。

不经意传输扩展。不经意传输在 $SMPC$ 协议中有着广泛的应用。例如，在基于混淆电路的 $SMPC$ 协议中，每条输入线必须运行一个不经意传输协议。在基于秘密共享的 $SMPC$ 协议中，每个与门必须至少运行一个不经意传输协议。因此，数以百万计的不经意传输的实例必须在 $SMPC$ 协议中运行，这导致了过高的操作成本。针对这一问题，提出了一种扩展不经意传输的方法。不经意传输扩展协议通过运行几个“$base$”不经意传输实例来工作。“$base$”实例的数量取决于使用的安全参数。基于这些“$base$”实例，我们可以进一步获得更多的不经意传输实例，而只需使用计算上廉价的对称密码操作就可以进一步获得更多的不经意传输实例。这样，可以高效地实现不经意传输扩展。

![[Pasted image 20221010221216.png]]

## 混淆电路——基于 OT 的实现

现在我们来看一看基于 OT 的实现方式。我们考虑

1.  $Alice$ 拥有值 $v_0,v_1$ 和密匙 $s,r_0,r_1$
2.  $Bob$ 拥有值 $i\in\{0,1\}$ 和密匙 $k$ 。$Bob$ 想获得 $v_i$
3.  $Alice$ 和 $Bob$ 事先统一 $g\in Z_p$ ，其中 $g$ 是 large integer， $p$ 是 large prime number

那么 OT 协议可以通过如下演绎

 1. $Alice \rightarrow Bob: g^s$
	 1. $Bob$ 知道 $g$ 和 $g^s$ 也无法破译 $s$ 因为 Discrete Logarithm Problem 不存在高效解法。
 2. $Bob$ 基于 $i$ 生成 $L_i = \begin{cases} g^k & \text{if }i=0 \\ g^{s-k} & \text{if } i = 1 \end{cases}$
 3. $Bob \rightarrow Alice: L_i$
	 1. $Alice$ 知道 $g$ 和 $g^k$ 也无法破译 $k$ 因为 Discrete Logarithm Problem 不存在高效解法。因此，$Alice$ 无法知道 $Bob$ 发来的是 $g^k$ 还是 $g^{s-k}$，也就无法知道无法知道 $i$。
 4. $Alice$ 生成 $C_0,C_1$
	 1. $C_0 = (g^{r_0},(L_i)^{r_0}\oplus v_0)$ 其中 $\oplus$ 表示 bitwise XOR，下同
	 2. $C_1=(g^{r_1},(g^s/L_i)^{r_1}\oplus v_1)$
 5. $Alice \rightarrow Bob: C_0,C_1$
 6. $Bob$ 知道 $g,g^{r_0},g^{r_1}$ 也无法破译 $r_0,r_1$ 因为 Discrete Logarithm Problem 不存在高效解法。
 7. $Bob$ 解密 $v_i$
	 1. $case\ i=0$
		 1. $Bob$ 可以通过如下方式解密获得 $v_0:C_0[0]^k \oplus C_0[1] = (g^{r_0})^k \oplus (L_i)^{r_0} \oplus v_0 = (g^{r_0})^k \oplus (g^k)^{r_0} \oplus v0=v0$
		 2. $Bob$ 无法获得 $v_1$ 因为 $C_1[1]=(g^s/L_i)^{r_1} \oplus v_1=g^{(s-k)r1} \oplus v_1$ 而 $Bob$ 不知道 $s,r_1$
	 2. $case\ i=1$
		 1. 类似地，$Bob$ 通过如下方式解密获得 $v_1:C_1[0]^k \oplus C_1[1] = (g^{r1})^k \oplus (g^s/L_i)^{r_1} \oplus v_1 = (g^{r_1})^k \oplus (g^k)^{r_1} \oplus v_1 = v_1$
		 2. $Bob$ 无法获得 $v_0$ 因为 $C_0[1]=(L_i)^{r0} \oplus v_0 = g^{(s-k)r0} \oplus v_0$ 而 $Bob$ 不知道 $s,r_0$
	 3. 因此，$Bob$ 只能解密 $v_i$ 而不能解密 $v_{1-i}$


[不经意传输(OT)-总结 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/399361005)