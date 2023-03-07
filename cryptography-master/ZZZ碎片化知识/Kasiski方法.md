卡西斯基试验是基于类似the这样的常用单词有可能被同样的密钥字母进行加密，从而在密文中重复出现。例如，明文中不同的CRYPTO可能被密钥ABCDEF加密成不同的密文：

```
        密钥：ABCDEF AB CDEFA BCD EFABCDEFABCD

        明文：CRYPTO IS SHORT FOR CRYPTOGRAPHY

        密文：CSASXT IT UKSWT GQU GWYQVRKWAQJB
```

此时明文中重复的元素在密文中并不重复。然而，如果密钥相同的话，结果可能便为（使用密钥ABCD）：
```
        密钥：ABCDAB CD ABCDA BCD ABCDABCDABCD

        明文：CRYPTO IS SHORT FOR CRYPTOGRAPHY

        密文：CSASTP KV SIQUT GQU CSASTPIUAQJB
```

此时卡西斯基试验就能产生效果。对于更长的段落此方法更为有效，因为通常密文中重复的片段会更多。如通过下面的密文就能破译出密钥的长度：

```
密文：DYDUXRMHTVDV_NQD_QNWDYDUXRMHARTJGW_NQD_
```

其中，两个DYDUXRMH的出现相隔了18个字母。因此，可以假定密钥的长度是18的约数，即长度为18、9、6、3或2。而两个NQD则相距20个字母，意味着密钥长度应为20、10、5、4或2。取两者的交集，则可以基本确定密钥长度为2。