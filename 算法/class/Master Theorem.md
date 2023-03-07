### 前置知识

1. 如果存在常数 $c>0,n_0\ge0$，使得对所有的 $n\ge n_0$ 有 $T(n)\le c\cdot f(n)$，那么 $T(n)$ 是 $O(f(n))$ 。
2. 如果存在常数 $\varepsilon>0,n_0\ge0$，使得对所有的 $n\ge n_0$ 有 $T(n)\ge \varepsilon\cdot f(n)$，那么 $T(n)$ 是 $\Omega(f(n))$ 。
3. 如果函数 $T(n)$ 既是 $O(f(n))$ 也是 $\Omega(f(n))$，那么 $T(n)$ 是 $\Theta(n)$ 。
> $O(\cdot)$ 表示渐进的上界，$\Omega(\cdot)$ 表示渐进的下界，$\Theta(\cdot)$ 是渐进的紧的界。

- $\omega(f(n))$ 相比 $\Omega(f(n))$ 是严格小于
  对任意常数 $c>0$，存在常数 $n_0\ge0$，使得对所有的 $n\ge n_0$ 有 $T(n)\ge c\cdot f(n)$，那么 $T(n)$ 是 $\omega(f(n))$ 。


### 定义

$$T(n)=aT(n/b)+f(n)$$
1.  若 $f(n) = O(n^{\log_b a - \varepsilon})$，$\epsilon > 0$，那么 $T(n) = \Theta(n^{\log_b a})$ 。

2.  若 $f(n) = \Theta(n^{\log_b a}\lg^kn)$，那么 $T(n) = \Theta(n^{\log_b a} \lg^{k+1}n)$ 。

3.  若 $f(n) = \Omega(n^{\log_b a + \varepsilon})$，$\varepsilon > 0$，且对于某个常数 $c<1$ 和所有充分大的 $n$ 有 $af(n/b) \leq cf(n)$，那么 $T(n) = \Theta(f(n))$ 。

> 对于三种情况，我们都将函数 $f(n)$ 与函数 $n^{\log_ba}$ 进行比较。直觉上，递归式的解取决于两个函数中的较大者。如情况一是 $n^{\log_ba}$ 较大，情况三是 $f(n)$ 较大。而情况二是两者一样大，这种情况需要乘上一个对数因子。
> 需要注意的是，两个函数比较大小时必须确保多项式意义上的小于，也就是说，两者必须相差一个因子 $n^\varepsilon$，其中 $\varepsilon$ 是大于 $0$ 的常数。另外情况三还需要满足一个额外的条件。

### 例题

[CLRS Solutions | Problem 4-1 | Divide-and-Conquer (atekihcan.github.io)](https://atekihcan.github.io/CLRS/04/P04-01/)