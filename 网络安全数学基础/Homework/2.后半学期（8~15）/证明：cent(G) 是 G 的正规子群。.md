## 设 $G$ 是一个群。记 $\text{cent}(G)=\{a\in G\mid ab=ba\ \text{对任意}b\in G\}$。证明：$\text{cent}(G)$ 是 $G$ 的正规子群。 

### 首先证明 $\text{cent}(G)$ 是 $G$ 的子群。

任取 $a_1,a_2\in \text{cent}(G),b\in G$。计算
$$ba_1a_2^{-1}=a_1ba_2^{-1}=a_1(b^{-1})^{-1}a_2^{-1}=a_1(a_2b^{-1})^{-1}=a_1(b^{-1}a_2)^{-1}=a_1a_2^{-1}(b^{-1})^{-1}=a_1a_2^{-1}b$$
因此，$a_1a_2^{-1}\in \text{cent}(G)$，从而 $\text{cent}(G)$ 是 $G$ 的子群。

### 再证明 $\text{cent}(G)$ 是 $G$ 的正规子群。

任取 $a\in G,x\in a\text{cent}(G)a^{-1}$。那么存在 $y\in \text{cent}(G)$，使得 $x=aya^{-1}$。由 $y$ 的交换性，有 $x=aya^{-1}=aa^{-1}y=ey=y\in \text{cent}(G)$。
从而 $a\text{cent}(G)a^{-1}\subset \text{cent}(G)$，$\text{cent}(G)$ 是 $G$ 的正规子群。
> 正规子群 $aNa^{-1}\subset N$ 

