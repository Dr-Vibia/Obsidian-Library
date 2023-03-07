## 设 $a$ 是群 $G$ 的一个元素。证明：映射 $\sigma:x\rightarrow axa^{-1}$ 是 $G$ 到自身的自同构。

### （1）

任取 $x,y\in G$。计算
$$\sigma(xy)=a(xy)a^{-1}=axeya^{-1}=axa^{-1}aya^{-1}=\sigma(x)\sigma(y)$$
因此 $\sigma$ 是同态映射。

### （2）

若 $x,y\in G$，且 $\sigma(x)=\sigma(y)$。那么 $axa^{-1}=aya^{-1}$，从而
$$x=a^{-1}axa^{-1}a=a^{-1}aya^{-1}a=y$$
因此 $\sigma$ 是单射。

### （3）

任取 $c\in G$。由于 $\sigma(a^{-1}ca)=a(a^{-1}ca)a^{-1}=ece=c$，故 $\sigma$ 是满射。

综上所述，映射 $\sigma:x\rightarrow axa^{-1}$ 是 $G$ 到自身的自同构。
> 同态+单射+满射=同构

