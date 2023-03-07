# 混淆电路（Garbled Circuits，GC）

## 逻辑电路基础

我们不妨认为 $Alice$ 和 $Bob$ 的财富是用二进制表示的一个整数 $a_na_{n-1}\dots a_1, b_nb_{n-1}\dots b_1$ 其中 $a_i,b_i\in\{0,1\}$ 。我们可以用归纳法来判断它们的大小。

我们定义变量 $c_i$

$c_i := \begin{cases} 1 & \text{if } a_{i-1}...a_1 > b_{i-1}...b_1\\ 0 & \text{otherwise} \tag{1} \end{cases}$

以及其初始值 $c_1=0$ 。在已知 $a_i,b_i,c_i$ 的情况下， $c_{i+1}$ 可以做如下推导。

$c_{i+1} =1 \Leftrightarrow (a_i>b_i) \text{ or } (a_i = b_i \text{ and } c_i = 1) \tag{2}$

公式（2）描述的逻辑也很直接，即 $a_{i}...a_1 > b_{i}...b_1$ 的充分必要条件是 $a_i>b_i$ ，或 $a_i=b_i$ 且 $a_{i-1}...a_1>b_{i-1}...b_1$ 。通过这个方法，我们可以依次获得 $c_2,c_3,...,c_{n+1}$ 。对应到逻辑电路，由于 $a_i,b_i,c_i \in {0,1}$ ，公式（2）可以转化成如下逻辑电路。

![[Pasted image 20221013093619.png]]

我们将上述电路封装成一个三个输入（ $a_i,b_i,c_i$ ）一个输出（ $c_{i+1}$ ）的模块 $>$ 。我们将 $n$ 个这样的模块串联起来，就完成了判断 $a_na_{n-1}\dots a_1 > b_nb_{n-1}\dots b_1$ 的电路。

![[Pasted image 20221013093804.png]]

在这个电路中，中 $c_{n+1}$ 为整个电路的输出。当输出是 1 时， $a_na_{n-1}\dots a_1 > b_nb_{n-1}\dots b_1$ 成立。

正文中提到的电路用到了多处取反，并不是最优的。通过观察，我们不难发现 $c_{i+1}=a_i \oplus[(a_i\oplus c_i)\land (b_i\oplus c_i)]$

$\begin{array}{|c|c|c|c|c|} \hline a_i & b_i & c_i & c_{i+1} & a_i \oplus[(a_i\oplus c_i) \land (b_i\oplus c_i)] \\ \hline 0 & 0 & 0 & 0 & 0 \\ \hline 0 & 0 & 1 & 1 & 1 \\ \hline 0 & 1 & 0 & 0 & 0 \\ \hline 0 & 1 & 1 & 0 & 0 \\ \hline 1 & 0 & 0 & 1 & 1 \\ \hline 1 & 0 & 0 & 1 & 1 \\ \hline 1 & 1 & 0 & 0 & 0 \\ \hline 1 & 1 & 1 & 1 & 1 \\ \hline \end{array}\\ \tag{3}$

所以我们可以将电路简化为

![[Pasted image 20221013094304.png]]


## 混淆电路原理

混淆电路协议分为三个部分。

-   Step 1: $Alice$ 生成混淆电路
-   Step 2: $Alice$ 和 $Bob$ 进行通信
-   Step 3: $Bob$ evaluate 生成的混淆电路
-   Step 4: 分享结果

### **Step 1: $Alice$ 生成混淆电路**

首先，$Alice$ 基于上述电路生成对应的混淆电路。生成过程主要分四步。

第一步，$Alice$ 对电路中的每一线路（Wire）进行标注。如下图所示，$Alice$ 一共标注了七条线路，包括模块的输入输出 $W_{a_0},W_{b_0},W_{c_0},W_{c_1}$，和模块内的中间结果 $W_d,W_e,W_f$ 。对于每一条线路 $W_i$ ，$Alice$ 生成两个长度为 $k$ 的字符串 $X_{i}^0,X_{i}^1$ 。这两个字符串分别对应逻辑上的 0 和 1。**这些生成的标注会在 Step 2 有选择性地发给 $Bob$，但 $Bob$ 并不知道 $X_{i}^0,X_{i}^1$ 对应的逻辑值。**

![[Pasted image 20221013095212.png]]

第二步，$Alice$ 对电路中的每一个逻辑门的 Truth Table 用 $X_{i}^0,X_{i}^1$ 进行替换，由 $X_{i}^0$ 替换 0，由 $X_{i}^1$ 替换 1。比如电路图中左上方的 $XOR$ 门的输入是 $a_0,c_0$ 输出是 $d$ ，对应的 Truth Table 可以做如下转换。

![[Pasted image 20221013095602.png]]

第三步，$Alice$ 对每一个替换后的 Truth Table 的输出进行两次对称密匙加密（即加密和解密的密匙相同），加密的密匙是 Truth Table 对应行的两个输入。比如 Truth Table 的第一行是 $X_{a_0}^0,X_{c_0}^0,X_d^0$ ，我们就用 $X_{a_0}^0,X_{c_0}^0$ 加密 $X_d^0$ 生成 $\text{Enc}_{X_{a_0}^0,X_{c_0}^0}(X_d^0)$ 。

第四步，$Alice$ 对第三步加密过后的 Truth Table 的行打乱得到 Garbled Table。所以 Garbled Table 的内容和行号就无关了。混淆电路的混淆二字便来源于这次打乱。

### **Step 2: $Alice$ 和 $Bob$ 通信**

第一步，$Alice$ 将她的输入对应的字符串发送给 $Bob$。比如 $a_0=1$ ，那 $Alice$ 会发送 $X_{a_0}^1$ 给 $Bob$。**由于 $Bob$ 不知道 $X_{a_0}^1$ 对应的逻辑值，也就无从知晓 $Alice$ 的秘密了。**

第二步，$Bob$ 通过 [[不经意传输 OT]] 协议从 $Alice$ 获得他的输入对应的字符串。不经意传输保证了 $Bob$ 在 $\{{X_{b_0}^0,X_{b_0}^1}\}$ 中获得一个，且 $Alice$ 不知道 $Bob$ 获得了哪一个。**所以 $Alice$ 也就无从知晓 $Bob$ 的** $b_0$ **了。**

最后，$Alice$ 将所有逻辑门的 Garbled Table 都发给 $Bob$。在这个例子中，一共有四个 Garbled Table。

### **Step 3: $Bob$ evaluate 生成的混淆电路**

$Alice$ 和 $Bob$ 通信完成之后，$Bob$ 便开始沿着电路进行解密。

因为 $Bob$ 拥有所有输入的标签和所有 Garbled Table，他可以逐一对每个逻辑门的输出进行解密。在这个例子中，假设 $Bob$ 拥有的输入标签为 $X_{a_0}^1,X_{b_0}^1,X_{c_0}^0$ 。他可以

1.  对于电路图左上方的 $XOR$，用 $X_{a_0}^1,X_{c_0}^0$ 解密获得 $X_d^1$
2.  对于电路图左下方的 $XOR$，用 $X_{b_0}^1,X_{c_0}^0$ 解密获得 $X_e^1$
3.  对于电路图中间的 $AND$，用 $X_d^1,X_e^1$ 解密获得 $X_f^1$
4.  对于电路图右侧的 $XOR$，用 $X_{a_0}^1,X_f^1$ 解密 $X_{c_1}^0$

值得注意的是，由于 Garbled Table 每一行的密匙都不同，所以 $Bob$ 只能解密其中一行。**而且 $Bob$ 并不知道解密出来的 $X_d^1,X_e^1,X_f^1,X_{c_1}^0$ 对应的逻辑值，也就无从获得更多信息了。而 $Alice$ 全程不参与 $Bob$ 的解密过程，所以也如法获得更多信息。**

### **Step 4: 共享结果**

最后 $Alice$ 和 $Bob$ 共享结果。$Alice$ 分享 $\{X_{c_1}^0,X_{c_1}^1\}$ 或者 $Bob$ 分享 $X_{c_1}^1$ ，双方就能获得电路输出的逻辑值了。