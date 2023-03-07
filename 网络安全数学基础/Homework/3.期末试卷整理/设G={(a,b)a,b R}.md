## 设 $G=\{(a,b)\mid a,b\in R,a\ne 0\}$，则 $(G,\cdot)$ 构成群，其中 $(a,b)\cdot(c,d)=(ac,ad+b)$。证明 $K=\{(1,b)\mid b\in R\}$ 是 $G$ 的正规子群且 $G/K\cong R^*$，其中 $R^*=R/\{0\}$ 是非零实数构成的乘法群。

### 求单位元
设 $G$ 的单位元 $e=(x,y)$，对 $\forall d=(a,b)\in G$，$de=(a,b)(x,y)=(ax,ay+b)=(a,b)$
$\therefore x=1,y=0$ 即 $e=(1,0)$
$\therefore d^{-1}=(\frac{1}{a},-\frac{b}{a})$ 

### 证明 $K$ 是 $G$ 的子群。
显然 $K\subseteq G$ ，对 $\forall k_1,k_2\in K$，令 $k_1=(1,k_1'),k_2=(1,k_2')$，则 $k_2^{-1}=(1,-k_2')$ 
$\therefore k_1k_2^{-1}=(1,k_1'-k_2')$
$\because k_1'\in R,k_2'\in R$
$\therefore k_1'-k_2'\in R$
$\therefore k_1k_2^{-1}\in K$
$\therefore K$ 是 $G$ 的子群
> 证明子群：对任意的 $a,b\in H$，有 $ab^{-1}\in H$ 。

### 证明 $K=\{(1,b)\mid b\in R\}$ 是 $G$ 的正规子群
即证明对 $\forall c\in G$，$cKc^{-1}\subseteq K$
对 $\forall A\in cKc^{-1}$，$\exists k\in K$，$A=ckc^{-1}$，分别令 $c=(a,b),k=(1,k')$，则 $c^{-1}=(\frac{1}{a},-\frac{b}{a})$
$\therefore A=(a,b)(1,k')(\frac{1}{a},-\frac{b}{a})=(a,ak'+b)(\frac{1}{a},-\frac{b}{a})=(1,b(1-k'))\in K$
$\therefore K$ 是 $G$ 的正规子群

### 证明 $G/K\cong R^*$
令映射 $f$ 为
$$\begin{align}
G&\longrightarrow R^*\\
(a,b)&\longmapsto a
\end{align}$$
令 $A,B\in G$，$A=(a,b)$，$B=(c,d)$
$f(AB)=f(ac,ad+b)=ac$
$f(A)f(B)=f(a,b)f(c,d)=ac$
$\therefore f(AB)=f(A)f(B)$
$\therefore f$ 是同态
$\because$ 对 $\forall a\in R^*$，$\exists(a,b)\in G$，$b\in R$，使得 $f(a,b)=a$
$\therefore f$ 是满同态
$\therefore f(G)=R^*$
$\therefore$ 由同态基本定义，存在 $G/K\longrightarrow f(G)=R^*$ 的同构 $f'$
$\therefore G/K\cong R^*$
