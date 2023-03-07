## 求 $F_{2^4}=F_2[x]/(x^4+x^3+1)$ 中的生成元 $g(x)$，并计算 $g(x)^t$，$t=0,1,\cdots,14$ 和所有生成元。

1. 因为 $|F_{2^4}^*|=16-1=15=3\cdot5$，所以满足$$\begin{align}
g(x)^3\not\equiv1\pmod{x^4+x^3+1}\\
g(x)^5\not\equiv1\pmod{x^4+x^3+1}
\end{align}$$的元素 $g(x)$ 都是生成元。
2. 对于 $g(x)=x$，有$$\begin{align}
x^3\equiv x^3\not\equiv1\pmod{x^4+x^3+1}\\
x^5\equiv x^4+x\not\equiv1\pmod{x^4+x^3+1}
\end{align}$$所以 $g(x)=x$ 是 $F_2[x]/(x^4+x^3+1)$ 的生成元。
3. 对于 $t=0,1,2,\cdots,14$，计算 $g(x)^t\pmod{x^4+x^3+1}$ 。生成元为 $g(x)^t$，$(t,15)=1$ 。$$\begin{equation}
\begin{aligned}
&g(x)^1\equiv x,\\
&g(x)^8\equiv x^3+x^2+x,\\
\end{aligned}
\quad
\begin{aligned}
&g(x)^2\equiv x^2,\\
&g(x)^{11}\equiv x^3+x^2+1,\\
\end{aligned}
\quad
\begin{aligned}
&g(x)^4\equiv x^3+1,\\
&g(x)^{13}\equiv x^3+x+1,\\
\end{aligned}
\quad
\begin{aligned}
&g(x)^7\equiv x^2+x+1,\\
&g(x)^{14}\equiv x^2+x,\\
\end{aligned}
\end{equation}$$生成元的集合为 $\{x,x^2,x^2+x,x^2+x+1,x^3+1,x^3+x+1,x^3+x^2+1,x^3+x^2+x\}$ 。