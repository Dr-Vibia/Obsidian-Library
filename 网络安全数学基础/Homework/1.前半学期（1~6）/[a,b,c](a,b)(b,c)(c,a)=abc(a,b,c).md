## 【数论关于最小公倍数求证：$[ a,b,c ](a,b)(b,c)(c,a)=abc(a,b,c)$其中$(a,b)$为最大公约数$[a,b]$为最小公倍数$a,b,c$均为正整数】

$$
\begin{equation*}
\begin{split}
(a,b)(b,c)(c,a)  
&=(ab,ac,b²,bc)(c,a)\\ 
&=(abc,a²b,ac²,a²c,b²c,b²a,bc²,abc,abc)\\
&=(ab(c,a,b),ac(b,c,a),bc(a,b,c))\\
&=(a,b,c)(ab,bc,ca)\\
只需证明:abc&=[a,b,c](ab,bc,ca)\\
因为:abc  
&=[a,b](a,b)c\\
&=[[a,b],c]([a,b],c)(a,b)\\
&=[a,b,c]([a,b](a,b),c(a,b))\\
&=[a,b,c](ab,bc,ca)
\end{split}
\end{equation*}
$$
