2015 年的欧密会上 Zahur、Rosulek 和 Evans 等人提出了 Half-gates 技术, 不仅可以实现 XOR 门不需要密文(free), 同时 AND 门只需 2 个密文.

考虑类似于 Free XOR 标签设定的 AND 门, 设 $\Delta$ 为标签偏移量(offset), 上侧输入标签分别为 $A$, $A\oplus \Delta$ , 分别对应真值 $0,1$ , 下侧输入标签 B, $B\oplus \Delta$, 分别对应真值 $0,1$ , 输出标签分别为 C,$C\oplus\Delta$ , 分别对应真值 $0,1$ , 为方便描述, 在下文中输入线路的真值分别记为 $a,b$ , 输出线路的真值记为 $c$ , 我们分别考虑以下三个问题:

1.  假设 Garbler 事先通过某种方式知道上侧线路输入 $a$ 及其对应的标签, 如何计算 $c=a\wedge b$ ?

- 若 $a=0$ , 对应于标签 $A$, 由 AND 门的性质, 我们有输出线路的真值$c\equiv 0$ , 与 $b$ 的取值无关, Garbler 可以和往常一样加密输出标签, 使用 $B$ 来加密 $C$ , 使用 $B\oplus \Delta$ 来加密 $C$ , 此时输出标签表示为$\mathsf{H}(B)\oplus C, \mathsf{H}(B\oplus\Delta)\oplus C$ ;
    
- 若 $a=1$ , 对应于标签 $A\oplus\Delta$ , 由 AND 门的性质, 我们有 $c=b$ , Garbler只需使用 $B$ 来加密 $C$ , 使用 $B\oplus \Delta$ 来加密 $C\oplus \Delta$ , 此时输出标签表示为 $\mathsf{H}(B)\oplus C, \mathsf{H}(B\oplus \Delta)\oplus C\oplus \Delta$.

![[Pasted image 20221018233956.png]]
> 这里的 $H(x)$ 是抗碰撞的哈希函数，如 $AES$

容易看出, 以上两种情况可以合并为 Garbler 使用 $B$ 来加密 $C$ , 使用 $B\oplus \Delta$ 来加密 $C\oplus a\Delta$ , 两个输出标签可表示为$\mathsf{H}(B)\oplus C和\mathsf{H}(B\oplus \Delta)\oplus C\oplus a\Delta$ , 于是混淆表的密文数为 $2$ . Garbler 使用 Point-and-permute 技术, 根据 $B$ 的颜色比特适当地排列密文的次序. 我们可以进一步使用 Garbled Row Reduction 的技巧来减少密文数, 即不再均匀随机选取 $C$ , 而是取 $C:=\mathsf{H}(B)$ , 使得混淆表第一个密文为全零, 于是 Garbler 只需发送第二个密文即可.

这说明, 如果 Garbler 事先通过某种方式知道 AND 门的一个输入 $a$ 及其对应的标签, 则他只需发送一个密文 $\mathsf{H}(B\oplus \Delta)\oplus C\oplus a\Delta$ , 即可混淆计算AND 门. 称这种情况下的 AND 门为 Garbler-half-gate , 它包含一个密文, Garbler 调用 $\mathsf{H}$ 两次, Evaluator调用 $\mathsf{H}$ 一次.

2. 假设 Evaluator 事先通过某种方式获知下侧线路的真值 $b$ 及其对应的输入标签, 如何计算 $c=a\wedge b$?

-   若 Evaluator 知道 $B$ 及其所对应的真值为 $b=0$ , 则 Evaluator 须得到$c=0$ 的输出标签 $C$ , Garbler 只需使用 $B$ 来加密 $C$ 的结果作为密文, 即$\mathsf H(B)\oplus C$ ;  
    
-   若 Evaluator 知道 $B\oplus \Delta$ 及其所对应的真值为 $b=1$ , 此时需要将上侧输入线路的标签转移到输出线路的标签上, 使得当上侧标签为 $A$ 时, Evaluator 得到的输出标签为 $C$ , 当上侧标签为 $A\oplus \Delta$ 时, Evaluator 得到的输出标签为 $C\oplus \Delta$ , 怎么做呢? 只需将上侧标签直接与 $A\oplus C$ 进行XOR 即可. 于是 Garbler 只需用 $B$ 来加密C, 用 $B\oplus \Delta$ 来加密 $A\oplus C$ 的结果作为密文, 即输出标签为 $\mathsf{H}(B)\oplus C,\mathsf{H}(B\oplus\Delta)\oplus A\oplus C$ . 注意, 这种情况下 Garbler 不再使用 Point-and-permute 技术置换密文的次序, 这是因为 Evaluator 已经知道了 $b$,可以根据 $b$ 的取值来判断需要解密哪个密文, 如果 $b=0$ , 则解密第一个密文, $b=1$ , 则解密第二个密文. 但仍可以使用 Garbled Row Reduction 的技巧来减少密文数, 即取$C:=\mathsf{H}(B)$ , 使得混淆表第一个密文为全零, 于是 Garbler 只需发送第二个密文即可.  
    

这说明 Evaluator 如果事先通过某种方式获知下侧线路的真值 $b$ 及其对应的输入标签, Garbler 只需发送一个密文即可混淆计算 AND 门. 下文中, 称这种情况下的 AND 门为 Evaluator-half-gate, 它包含一个密文, Garbler 调用 $\mathsf{H}$ 两次, Evaluator 调用 $\mathsf{H}$ 一次.

![[Pasted image 20221019223155.png]]

3. 现在抛开以上两种假设, $a,b$ 分别是 Gabler, Evaluator 的秘密, 如何计算$c=a\wedge b$ ?  
首先, 将 $c=a\wedge b$ 分解成如下图所示的形式, Garbler 均匀随机选择一个比特 $r$ 用于盲化 $a$ , 并让 Evaluator 获得 $a\oplus r$ , 这不会泄漏 $a$ 的语义真值, 因为这相当于一次一密(OTP). Evaluator 已知 $a\oplus r$ , 可以通过调用一个Evaluator-half-gate 来计算 $(a\oplus r)\wedge b$ . Garbler 已知 $r$ , 可以通过调用一个 Garbler-half-gate 来计算 $r\wedge b$ , 最后将两个 half-gate 的结果通过一个XOR 门计算即可, 而 XOR 门计算是免费的, 于是计算 $c=a\wedge b$ 总的开销仅为 2 个密文, Garbler 调用 $\mathsf{H}$ 四次, Evaluator 调用 $\mathsf{H}$ 两次.  
那么, Garbler 如何选择 $r$ , 又如何让 Evaluator 获得 $a\oplus r$ 呢? 实际上, Garbler 只需将 $r$ 取为真值为 $0$(FALSE)的标签 $A$ 的颜色比特即可做到这一点, 而无需任何额外开销, 此时, $a\oplus r$ 为 Evaluator 所收到的标签 $A$ 或$A\oplus \Delta$ 的颜色比特.

![[Pasted image 20221019223509.png]]

### **开销比较**

下图展示了上述方案与原始的混淆电路方案相比, 密文大小与 Garbler 和Evaluator 的平均计算开销, 其中 $\lambda$ 表示安全参数. 注意到原始混淆电路中每个门理论上只需 4 个密文, 但由于需要进行 Ciphertext expansion, 因此, 这实际上相当于需要 8 个密文. 

![[Pasted image 20221019223544.png]]

易见, Half-gates 技术是当前混淆电路中的最佳优化方案. 很自然的一个问题, 我们能否可以做到比 Half-gates 技术更好? Half-gates 的作者在他们的文章中指出, 如果仅使用标准技术(Standard techniques), 在通用模型下不能以少于两个密文来混淆计算一个 AND 门. 虽然在 CCS'16 会议 Ball 等人和 16 年亚密会 Kempka 等人的两项工作中指出可以仅以一个密文来计算 AND 门, 但都基于特殊假设, 如整个电路只有一个 AND 门等, 在大规模电路中不适用. 因此, 能否在通用模型下做到比 Half-gates 方案更好, 仍然是一个公开问题.

![[Pasted image 20221019223648.png]]