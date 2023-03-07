Goldreich-Micali-Wigderson (GMW) Protocol 也有同样的能力。我们通过三个渐进的模块来构建 GMW。

1.  Extending from $OT_1^2$ to $OT_1^n$
2.  Securely Computing Any Constant Size Function using $OT_1^n$
3.  The GMW Protocol

## Extending from $OT_1^2$ to $OT_1^n$

在之前的不经意传输（Oblivious Transfer, OT）的文章中，我们介绍了 $OT_1^2$ 的一种实现方式。在这一章节，我们通过 $OT_1^2$ 来构造 $OT_1^n$ 。

我们考虑 Alice 持有 $x_1, \dots,x_n\in\{0,1\}^\ell$ ，Bob 持有 $i\in\{1,\dots,n\}$ 。通过 $OT_1^n$ ，Bob 获得 $x_i$ 但 Alice 不知道 $i$ 。

$OT_1^n$ 由如下几步组成。

第一步，Alice 生成 $k_0=0^\ell$ 和**随机生成** $k_j\in\{0,1\}^\ell\ ,j = 1,\dots,n$ 。

第二步，Alice 和 Bob 进行 $n$ 次 $OT_1^2$ 操作。在第 $j$ 次操作中，Alice 提供 $k_0\oplus\cdots\oplus k_{j-1}\oplus x_j$ 和 $k_j$ 。若 $j=i$，Bob 选择前者；若 $j\neq i$，Bob 选择后者。

第三步，Bob 通过第 $1$ 次至第 $i-1$ 次 $OT_1^2$ 获得的 $\{k_0, \dots, k_{i-1}\}$ ，以及第 $i$ 次获得的 $k_0\oplus\cdots\oplus k_{i-1}\oplus x_i$ 即可解密 $x_i$ 。

我们来分析上述 $OT_1^n$ 的安全性。Bob 的安全性可直接继承自 $OT_1^2$ 的安全性，即 $OT_1^2$ 保证了 Alice 无从知晓 Bob 在每一轮选择了前者还是后者，所以 Alice 无从知晓 $i$ 的真实值。Alice 的安全性可以通过分类讨论的方法来论证。我们考虑 Bob 在第 $i$ 轮 $OT_1^2$ 第一次选择了前者。对于 $j<i$ ，Bob 在 $OT_1^2$ 中选择的是 $k_j$ ，从而不会获得任何 $x_j$ 的信息。对于 $j>i$ ，Bob 最多只能获得 $x_j\oplus k_i\oplus \text{others}$ ，由于 Bob 不知道 Alice 随机生成的 $k_i$ ，从而无从知晓 $x_j$ 。

上述 $OT_1^n$ 实现的复杂度为 $O(n)$ ，有兴趣的读者可以了解更高效的 $O(\sqrt{n})$ 的算法。[1]

## Securely Computing Any Constant Size Function using $OT_1^n$

$OT_1^n$ 可以解决很通用的问题：Securely Computing Any Constant Size Function。Constant Size Function 指函数的输入可能值是有限的。

我们考虑 Alice 和 Bob 分别拥有 private input $x\in S_A, y \in S_B$ ，他们想共同计算 $f(x,y)$ 。

1.  Alice 计算 $x$ 与所有 $y$ 的可能值的结果 $A = \{f(x,y_1), f(x,y_2), \dots, f(x,y_n)\}$ 。
2.  Alice 和 Bob 进行 $OT_1^n$ 。Alice 提供 $A$ ，Bob 根据 $y=y_i$ 提供 $i$ 。
3.  Bob 获得 $f(x,y_i)=f(x,y)$ 。如果需要，Bob 结果分享给 Alice。

$OT_1^n$ 保证了 Bob 只能获得最终结果 $f(x,y_i)$ ，所以无从获得更多有关 $x$ 的信息。同时，$OT^n_1$ 保证了 Alice 无从知晓 Bob 的 $i$ 。

## The GMW Protocol

有了上述基础，我们可以构建 GMW Protocol 了。

我们考虑最基础的情况，Alice 和 Bob 拥有一个比特的输入 $x,y\in\{0,1\}$ ，他们想计算 $w=G(x,y)$ ，其中 $G$ 是一个逻辑门电路。在这个情况下，GMW Protocol 包含如下步骤。

1.  Alice **随机生成** $x_a\in\{0,1\}$ ，并发送 $x_b=x\oplus x_a$ 给 Bob。我们将 $\{x_a,x_b\}$ 称为 $x$ 的**分享值**。由于 $x_a$ 的随机性，Bob 无法破译 $x$ 。
2.  Bob **随机生成** $y_b\in\{0,1\}$ ，并发送 $y_a=y\oplus y_b$ 给 Alice。由于 $y_b$ 的随机性，Alice 无法破译 $y$ 。
3.  Alice **随机生成** $z_a\in\{0,1\}$ ，并枚举 $f(x_b,y_b)=z_a\oplus G(x_a\oplus x_b, y_a\oplus y_b)$ 的所有可能值。由于 $x_b,y_b\in\{0,1\}$ ，所以 $f(x_b,y_b)$ 一共有四个可能值，即 $\{f(0,0),f(0,1),f(1,0),f(1,1)\}$ 。
4.  Alice 和 Bob 进行 $OT_1^4$ 。Alice 提供 $\{f(0,0),f(0,1),f(1,0),f(1,1)\}$ ，Bob 提供 $(x_b,y_b)$ 所对应的 $i$ 值。 $OT_1^4$ 保证了 Bob 只获得最终结果 $f(x_b,y_b)$ ，以及 Alice 无从知晓 $i$ 从而无从知晓 $x_b,y_b,f(x_b,y_b)$ 。
5.  Bob 将 $z_b = f(x_b,y_b)$ 。
6.  Alice 和 Bob 可以 reveal $z_a, z_b$ 来获得 $z$ 的真实值。不难验证， $z_a\oplus z_b=z_a\oplus z_a\oplus G(x_a\oplus x_b, y_a\oplus y_b) = G(x_a\oplus x_b, y_a\oplus y_b)=G(x, y)=z$。

对于更复杂逻辑电路，Alice 和 Bob 会通过上述方法依次计算每一个逻辑门 $G$ 从而得到每一条线路 $w$ 的分享值 $\{w_a,w_b\}$ 。GMW 保证了 $w=w_a\oplus w_b$ 。在最后，Alice 和 Bob 只 reveal 电路输出线路的分享值，从而获得逻辑电路的计算结果。Alice 和 Bob 不知道中间电路的真实值，因为每一方只有一半的分享值。

## 结语

本文介绍了一种常用的密码学协议 —— Goldreich-Micali-Wigderson (GMW) Protocol 。通过这个协议，两个 party 能在互相不知晓对方数据的情况下计算某一能被逻辑电路表示的函数。

从秘密分享（secret sharing）的角度来看，GMW 和混淆电路有很多相通性。混淆电路是通过 generator 持有逻辑电路中线路 $W_i$ 可能的标签 $\{W_i^0,W_i^1\}$ ，evaluator 持有 $W_i$ 的真实值 $W_i^x,x\in\{0,1\}$ 来分享秘密的。而 GMW 的秘密分享更加直接，Alice 和 Bob 分别持有比特 $x_a,x_b$ 并保证真实值 $x=x_a \oplus x_b$ 。

## Reference

[1] [Oblivious Transfer (OT) and Private Information Retrieval (PIR)](https://www.cs.princeton.edu/courses/archive/fall07/cos433/lec19.pdf)

[2] [CS 35500 Introduction To Cryptography: GMW Protocol](https://www.cs.purdue.edu/homes/hmaji/teaching/Fall%202017/lectures/39.pdf)


# GMW Protocol - n parties 介绍

## 思路介绍

我们考虑 $P_1,P_2,\dots,P_n$ 共同计算电路 $C$ 。

$P_1, \dots, P_n$ 秘密分享电路的输入。比如 $P_j$ 拥有输入 bit $v \in \{0,1\}$ ，那 $P_j$ 随机生成 $i\neq j, r_i \in \{0,1\}$ 并发送 $r_i$ 给 $P_i$ 。$P_i$ 将 $r_i$ 作为 $v$ 的分享值。 $P_j$ 侧的分享值为 $v\oplus\left(\bigoplus_{i\neq j}r_i\right)$ 。每一个 bit 输入被拆成了 $n$ 份。

$P_1,P_2,\dots,P_n$ 共同计算电路 $C$ 的每一个逻辑门 $G$。

如果 $G$ 是 $XOR$ gate，考虑到如下等式，每一个 party 只需在本地 $XOR$ 分享值。

$$\begin{align} a \oplus b &= (a_1 \oplus \dots \oplus a_n) \oplus (b_1 \oplus \dots \oplus b_n) \\ &= (a_1 \oplus b_1) \oplus \dots \oplus (a_n \oplus b_n) \end{align} \tag{1}$$

如果 $G$ 是 $AND$ gate，考虑如下等式，整个计算过程分为如下几个部分。

$$\begin{align} a\land b &= (a_1 \oplus \cdots \oplus a_n)\land (b_1 \oplus \cdots \oplus b_n) \\ &= \left(\bigoplus_{i\neq j} a_i \land b_j\right) \oplus \left(\bigoplus_{i=1}^n{a_i\land b_i}\right) \end{align} \tag{2}$$

-   第一步：对于 $i\neq j$ ，$P_i$ 和 $P_j$ 利用不经意传输协议共同计算 $a_i \land b_j$ ，分别获得 $c_{i,j},d_{j,i}$ 。

-   $P_i$ 本地随机生成 $c_{i,j}\in\{0,1\}$ ，并根据 $c_{i,j}$ 和 $a_i$ 的真实值构造函数 $f(x)=c_{i,j} \oplus (a_i\land x)$ 并生成 $\{f(0), f(1)\}$ 。
-   $P_i$ 与 $P_j$ 进行 $OT_1^2$ ， $P_i$ 提供 $\{f(0), f(1)\}$ ， $P_j$ 根据 $b_j$ 的真实值选择 $f(b_j)$ 。
-   $P_j$ 定义 $d_{j,i}:=f(b_j)$ 。我们不难验证 $c_{i,j} \oplus d_{j,i} = c_{i,j} \oplus f(b_j) = c_{i,j} \oplus c_{i,j} \oplus (a_i \land b_j) = a_i \land b_j$ 。

-   第二步： $P_i$ 在本地计算 $e_i := \bigoplus_{1\le j \le n,j\neq i} c_{i,j}$ 和 $f_i := \bigoplus_{1\le j \le n,j\neq i} d_{i,j}$。
-   第三步：考虑到等式 (2) 可以作如下转化。$P_i$ 只需在本地计算 $(a_i\land b_i)\oplus e_i \oplus f_i$ ，即完成了 $AND$ gate 的计算。

$$\begin{align} a\land b &= \left(\bigoplus_{i\neq j} a_i \land b_j\right) \oplus \left(\bigoplus_{i=1}^n{a_i\land b_i}\right) \\ &= \left(\bigoplus_{i\neq j} c_{i,j} \oplus d_{i,j}\right) \oplus \left(\bigoplus_{i=1}^n{a_i\land b_i}\right) \\ &= \left(\bigoplus_{i=1}^n e_i \right) \oplus \left(\bigoplus_{i=1}^n f_i \right) \oplus \left(\bigoplus_{i=1}^n{a_i\land b_i}\right) \\ &= \bigoplus_{i=1}^n(a_i\land b_i)\oplus e_i\oplus f_i \\ \end{align} \tag{3}$$

最后， $P_1, \dots, P_n$ 公开 $C$ 的输出导线的分享值，整个计算就完成了。

## 完备性

考虑到 $1 \oplus (x \land y) = \text{NAND}(x,y)$ ， $\{\text{NAND}\}$ 是 [functionally complete](https://en.wikipedia.org/wiki/Functional_completeness) 的，所以任意的逻辑电路都可以用通过上述方法实现。

## 性能分析与优化

我们分析 evaluate $XOR$ 和 $AND$ 所需要的计算量。

**$XOR$ gate**: 所有计算都会在 $P_i$ 本地发生，没有网络通信，所以计算复杂度是 $O(1)$ ，通信复杂度是 $O(0)$ 。

**$AND$ gate**: $P_i$ 的 $n-1$ 次 OT 涉及到 $O(n)$ 的计算与 $O(n)$ 的通信。 $e_i$ 和 $f_i$ 涉及到 $O(n)$ 的计算，最后 $(a_i \land b_i) \land e_i \land f_i$ 涉及到 $O(1)$ 。所以计算复杂度是 $O(n)$ ，通信复杂度 $O(n)$ 。

可以看到，$AND$ gate 由于依赖 $OT$，它的速度会比 $XOR$ gate 慢很多。实际运用中，我们可以通过预先生成的 random triple 来避免 $OT$。[1]

## 结语

本文介绍了 Goldreich-Micali-Wigderson (GMW) Protocol 在 $n$ 方场景下的原理。

## Reference

[1] BGW protocol: [https://people.eecs.berkeley.edu](https://people.eecs.berkeley.edu/~sanjamg/classes/cs294-spring16/scribes/3.pdf)