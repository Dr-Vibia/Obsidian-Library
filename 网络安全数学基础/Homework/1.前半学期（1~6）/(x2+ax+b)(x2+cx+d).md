证明：对任意素数 $p$ ，必有整数 $a,b,c,d$ 使得
$$x^4+1\equiv (x^2+ax+b)(x^2+cx+d)\pmod p$$

右边展开
$$
\begin{equation*}
\begin{split}
&\ \quad (x^2+ax+b)(x^2+cx+d)\\
&=x^4+(a+c)x^3+(ac+b+d)x^2+(ad+bc)x+bd\\
&\equiv x^4+1\pmod p
\end{split}
\end{equation*}
$$
因此在模 $p$ 下 $a+c=0,ac+b+d=0,ad+bc=0,bd=1$
得到 $a=-c,b+d=c^2,c(b-d)=0,bd=1$


若 $p\equiv 1 \pmod 4$，可知 $-1$ 是模 $p$ 的平方剩余，存在 $y$ 使得 $y^2\equiv -1\pmod p$
可取 $a=c=0,b=y,d=-y$ 
即 $x^4+1\equiv (x^2+y)(x^2-y)=x^4-y^2\pmod p$ 
> 若 $p\equiv1\pmod 4$ ，则 $\left(\frac{-1}{p}\right)=1$ 。


若 $p\equiv7\pmod 8$，$2$ 是 $\bmod p$ 的平方剩余，存在 $y$ 使得 $y^2\equiv2\pmod p$ 
可取 $b=d=1,c=y,a=-y$ 
即 $x^4+1\equiv(x^2-yx+1)(x^2+yx+1)=x^4+(2-y^2)x^2+1\pmod p$
>若 $p\equiv\pm1\pmod 8$ ，则 $\left(\frac{2}{p}\right)=1$ 。


若 $p\equiv3\pmod 8$，勒让德符号
$$\left(\frac{-2}{p}\right)=\left(\frac{-1}{p}\right)\left(\frac{2}{p}\right)=-1\times-1=1$$
可知 $-2$ 是模 $p$ 的平方剩余，仍设 $y^2\equiv-2\pmod p$  
可取 $b=d=-1,c=y,a=-y$ 
则 $x^4+1\equiv(x^2-yx-1)(x^2+yx-1)=x^4-(2+y^2)x^2+1\pmod p$ 
> 若 $p\equiv\pm3\pmod 8$ ，则 $\left(\frac{2}{p}\right)=-1$ 。


若 $p=2$，
可取 $b=d=1,c=0,a=0$ 
$x^4+1\equiv(x^2+1)(x^2+1)=x^4+2x^2+1\pmod p$  


所以对任意 $p$，均可分解 $x^4+1$  
为$(x^2+ax+b)(x^2+cx+d)$ 

> 所有 $>2$ 的素数 $\bmod 8$ 之后可以分为 $1,3,5,7\pmod 8$ ，其中 $1,5\pmod 8$ 可以合并成 $1\pmod 4$ 。