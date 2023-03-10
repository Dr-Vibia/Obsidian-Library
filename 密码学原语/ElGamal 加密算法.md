## 密钥生成

密钥生成的步骤如下：
- Alice 利用生成元 $g$ 产生一个 $q$ 阶循环群 $G$ 的有效描述。该循环群需要满足一定的安全性质。
- Alice 从 $\{1,\cdots,q-1\}$ 中随机选择一个 $x$ 。
- Alice 计算 $h:=g^x$ 。
- Alice 公开 $h$ 以及 $G,q,g$ 的描述作为其**公钥**，并保留 $x$ 作为其**私钥**。私钥必须保密。


## 加密

使用 Alice 的公钥 $(G,q,g,h)$ 向她加密一条消息 $m$ 的加密算法工作方式如下：
-   Bob 从 $\{1,\cdots,q-1\}$ 随机选择一个 $y$，然后计算 $c_1:=g^y$ 。
-   Bob 计算共享秘密 $s:=h^y$ 。
-   Bob 把他要发送的秘密消息 $m$ 映射为 $G$ 上的一个元素 $m'$ 。
-   Bob 计算 $c_2:=m'\cdot s$ 。
-   Bob 将密文 $(c_1,c_2)=(g^y,m'\cdot h^y)=(g^y,m'\cdot(g^x)^y)$ 发送给 Alice 。
值得注意的是，如果一个人知道了 $m'$，那么它很容易就能知道 $h^y$ 的值。因此对每一条信息都产生一个新的 $y$ 可以提高安全性。所以 $y$ 也被称作临时密钥。


## 解密

利用私钥 $x$ 对密文 $(c_1,c_2)$ 进行解密的算法工作方式如下：
-   Alice 计算共享秘密 $s:=h^y$ 。
-   然后计算 $m':=c_2\cdot s^{-1}$，并将其映射回明文 $m$，其中 $s^{-1}$ 是 $s$ 在群 $G$ 上的逆元。（例如：如果 $G$ 是整数模 $n$ 乘法群的一个子群，那么逆元就是模逆元）。
- 解密算法是能够正确解密出明文的，因为$$c_2\cdot s^{-1}=m'\cdot h^y
\cdot(g^{xy})^{-1}=m'\cdot g^{xy}\cdot g^{-xy}=m'$$
