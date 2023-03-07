且 $p\equiv 1\pmod 4$，证明：

### （i）$1,2,\cdots,\frac{p-1}{2}$ 中模 $p$ 的二次剩余与二次非剩余的个数均为 $\frac{p-1}{4}$ 个

定理：$1,2,\cdots,p-1$ 中模 $p$ 的二次剩余模 $p$ 的二次剩余与二次非剩余的个数均为$\frac{p-1}{2}$个  

已知 $p\equiv 1\pmod 4$，那么勒让德符号 $\left(\frac{-1}{p}\right)=(-1)^{\frac{p-1}{2}} =1$  ，所以 $-1$ 是模 $p$ 的二次剩余。
那么若 $x$ 是模 $p$ 的平方剩余，$p-x$ 也是模 $p$ 的平方剩余。
若 $x$ 是模 $p$ 的平方非剩余，$p-x$ 也是模 $p$ 的平方非剩余。
> $\left(\frac{p-x}{p}\right)=\left(\frac{-x}{p}\right)=\left(\frac{-1}{p}\right)\left(\frac{x}{p}\right)=\left(\frac{x}{p}\right)$

设 $1,2,\cdots,\frac{p-1}{2}$ 中有 $k$ 个模 $p$ 的二次剩余，设为$x_1,x_2,\cdots,x_k$  
设 $\frac{p-1}{2}+1$ ,$\frac{p-1}{2}+ 2,\cdots,p-1$ 中有 $m$ 个模 $p$ 的二次剩余，设为$y_1,y_2,\cdots,y_m$  

注意 $p-x_1,p-x_2,\cdots,p-x_n$ 也是模 $p$ 的二次剩余，而 $\frac{p+1}{2}\le p-x_i\le p-1$，所以有 $k\le m$ 
反过来 $p-y_1,p-y_2,\cdots,p-y_m$ 也是模 $p$ 的二次剩余，而 $1≤p-y_j≤\frac{p-1}{2}$ ，所以有 $m \le k$  
因此 $k=m$ 注意 $k+m=\frac{p-1}{2}$ 所以$k=m=\frac{p-1}{4}$ 


### （iv）$1,2,\cdots,(p-1)$ 中全体模 $p$ 的二次剩余之和等于 $\frac{p(p-1)}{4}$ 

假设模 $p$ 的二次剩余的和是 $A$ ，二次非剩余的和是 $B$ ，不难看出
$$A+B=\frac{p(p−1)}{2}
$$
这是因为 $1,2,\cdots,p−1$ 这 $p−1$ 个数中，一半是模 $p$ 的二次剩余，一半是模 $p$ 的二次非剩余，$A+B$ 就是 $p-1$ 个值全部相加

前面已经证明了若 $x$ 是模 $p$ 的二次剩余，则 $p−x$ 也是模 $p$ 的二次剩余

于是我们就可以把模 $p$ 的 $\frac{p−1}{2}$ 个二次剩余写成

$x_1,x_2,\cdots,x_{\frac{p−1}{4}}$
$p−x_1,p−x_2,\cdots,p−x_{\frac{p−1}{4}}.$

$\frac{p-1}{4}$ 组 $x_i$ 和 $p-x_i$ 两两相加，就有 $A=\frac{p(p−1)}{4}$ . 

进而可知， 二次非剩余的和 $B=A=\frac{p(p−1)}{4}$ .