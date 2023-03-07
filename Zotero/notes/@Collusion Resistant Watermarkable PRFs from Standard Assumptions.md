# Collusion Resistant Watermarkable PRFs from Standard Assumptions

``` ad-info
title: Metadata
- **CiteKey**: yuCollusionResistantWatermarkable2020
- **Type**: Preprint
- **Author**: Yu, Rupeng Yang, Man Ho Au, Zuoxia; Xu, Qiuliang
- **Editor**: {{editor}}
- **Translator**: {{translator}}
- **Publisher**: {{publisher}}
- **Location**: {{place}}
- **Series**: {{series}}
- **Series Number**: {{seriesNumber}}
- **Journal**: {{publicationTitle}}
- **Volume**: {{volume}}
- **Issue**: {{issue}}
- **Pages**: {{pages}}
- **Year**: 2020 
- **DOI**: {{DOI}}
- **ISSN**: {{ISSN}}
- **ISBN**: {{ISBN}}
```
```ad-quote
title: Abstract
A software watermarking scheme can embed a message into a program without significantly changing its functionality. Moreover, any attempt to remove the embedded message in a marked program will substantially change the functionality of the program. Prior constructions of watermarking schemes focus on watermarking cryptographic functions, such as pseudorandom function (PRF), public key encryption, etc. A natural security requirement for watermarking schemes is collusion resistance, where the adversary’s goal is to remove the embedded messages given multiple marked versions of the same program. Currently, this strong security guarantee has been achieved by watermarking schemes for public key cryptographic primitives from standard assumptions (Goyal et al., CRYPTO 2019) and by watermarking schemes for PRFs from indistinguishability obfuscation (Yang et al., ASIACRYPT 2019). However, no collusion resistant watermarking scheme for PRF from standard assumption is known. In this work, we solve this problem by presenting a generic construction that upgrades a watermarkable PRF without collusion resistance to a collusion resistant one. One appealing feature of our construction is that it can preserve the security properties of the original scheme. For example, if the original scheme has security with extraction queries, the new scheme is also secure with extraction queries. Besides, the new scheme can achieve unforgeability even if the original scheme does not provide this security property. Instantiating our construction with existing watermarking schemes for PRF, we obtain collusion resistant watermarkable PRFs from standard assumptions, offering various security properties.
```
```ad-abstract
title: Files and Links
- **Url**: https://eprint.iacr.org/2020/695
- **Uri**: http://zotero.org/users/9781610/items/9X6IXN57
- **Eprint**: {{eprint}}
- **File**: [Full Text PDF](file:///D:%5CZotero%5Cdata_download%5Cstorage%5C54PZI9RN%5CYu%20%E5%92%8C%20Xu%20-%202020%20-%20Collusion%20Resistant%20Watermarkable%20PRFs%20from%20Standa.pdf)
- **Local Library**: [Zotero](zotero://select/library/items/9X6IXN57)
```
```ad-note
title: Tags and Collections
- **Keywords**: Collusion Resistance; Watermarkable PRF; Watermarking; lattice
- **Collections**: Cryptography; watermark
```

----

## Comments



----

## Extracted Annotations

注释(2022/10/25 下午11:53:09)

- *“Collusion Resistant Watermarkable PRFs from Standard Assumptions”* [(Yu 和 Xu, 2020, p. 1)](zotero://open-pdf/library/items/54PZI9RN?page=1&annotation=APUPWVST) 
> **标准假设下的抗共谋攻击水印伪随机函数** 

> **提出了一种通用的构建方法，可以将不抗共谋攻击的水印PRF升级为抗共谋的。同时，可以在保留原来方案的安全性质的基础上，新加入不可伪造的性质。** [ ](zotero://open-pdf/library/items/9X6IXN57?page=undefined&annotation=)  

- *“either indistinguishability obfuscation or standard (lattice) assumptions”* [(Yu 和 Xu, 2020, p. 2)](zotero://open-pdf/library/items/54PZI9RN?page=2&annotation=YHUWT3JW) 
> **两种构建方案：IO和standard assumptions** 

- *“construct watermarking schemes for public key encryption (PKE) and signature”* [(Yu 和 Xu, 2020, p. 2)](zotero://open-pdf/library/items/54PZI9RN?page=2&annotation=9TE5FCFA) 
> **公钥加密方案和数字签名** 


> **标记算法：输入message和key k，输出水印电路，水印电路可以评估Fk(·)提取算法：输入提取密钥和电路，输出message或记号⊥** [ ](zotero://open-pdf/library/items/54PZI9RN?page=2&annotation=XL93YNQP) 

![[yuCollusionResistantWatermarkable2020_Q6DBK7VY.png]] [(Yu 和 Xu, 2020, p. 2)](zotero://open-pdf/library/items/54PZI9RN?page=2&annotation=XL93YNQP)

- *“unremovability”* [(Yu 和 Xu, 2020, p. 2)](zotero://open-pdf/library/items/54PZI9RN?page=2&annotation=86G3WKSL) 
> **不可移除性：敌人不能在保持输出不变的情况下移除或修改嵌入的信息** 

- *“unforgeability”* [(Yu 和 Xu, 2020, p. 2)](zotero://open-pdf/library/items/54PZI9RN?page=2&annotation=4QMEJFF6) 
> **不可伪造性：没有mark key的人不能创建新的水印电路** 

- *“pseudorandomness against the watermarking authority”* [(Yu 和 Xu, 2020, p. 3)](zotero://open-pdf/library/items/54PZI9RN?page=3&annotation=6H5QFTY6) 
> **可以抵抗拥有mark key和extraction key的敌人（权威）** 

- *“collusion resistant.”* [(Yu 和 Xu, 2020, p. 3)](zotero://open-pdf/library/items/54PZI9RN?page=3&annotation=VH4NGU9E) 
> **如果敌手被允许获得一个以上的水印电路，那么这个方案是抗共谋的** 

- *“public marking”* [(Yu 和 Xu, 2020, p. 3)](zotero://open-pdf/library/items/54PZI9RN?page=3&annotation=5MTMDKC7) 
> **敌手可以获得创建水印电路的key** 

- *“public extraction”* [(Yu 和 Xu, 2020, p. 3)](zotero://open-pdf/library/items/54PZI9RN?page=3&annotation=566ERG9H) 
> **敌手可以获得水印电路的提取key** 

- *“only secure against an adversary that can make at most q queries to the extraction oracle”* [(Yu 和 Xu, 2020, p. 5)](zotero://open-pdf/library/items/54PZI9RN?page=5&annotation=3M9Y2YE5) 
> **局限性** 

- *“constrained PRFs”* [(Yu 和 Xu, 2020, p. 5)](zotero://open-pdf/library/items/54PZI9RN?page=5&annotation=9EW39FDY) 
> **对于PRF，输入k和ck的输出只在x*处不同，敌手不能分辨出x*的值** 

- *“A constrained PRF is constraint-hiding if the constrained key does not reveal the punctured points.”* [(Yu 和 Xu, 2020, p. 5)](zotero://open-pdf/library/items/54PZI9RN?page=5&annotation=4RRTKRU3) 
> **constraint-hiding：ck的穿刺点不能被辨别** 


> **根据k生成ck。对于嵌入的长度为l的msg，生成2l个输入……** [ ](zotero://open-pdf/library/items/54PZI9RN?page=5&annotation=VLMIAPK8) 

![[yuCollusionResistantWatermarkable2020_BMZYWSK5.png]] [(Yu 和 Xu, 2020, p. 5)](zotero://open-pdf/library/items/54PZI9RN?page=5&annotation=VLMIAPK8)

- *“underlying (variants of) constrained PRFs are not collusion resistant”* [(Yu 和 Xu, 2020, p. 6)](zotero://open-pdf/library/items/54PZI9RN?page=6&annotation=BLETUCY3) 
> **潜在的受限PRFs是非抗碰撞的，同一个k生成的两个ck就能恢复k** 

- *“key idea is to encode bits of a message into different “keys” instead of encoding them into different inputs.”* [(Yu 和 Xu, 2020, p. 6)](zotero://open-pdf/library/items/54PZI9RN?page=6&annotation=UC3ULLV3) 
> **核心想法是加密msg进keys而不是inputs** 


> **在第一次尝试中，在两个电路C的情况下，仅可以隐藏一些穿刺位置** [ ](zotero://open-pdf/library/items/54PZI9RN?page=6&annotation=R7K4KMSA) 

![[yuCollusionResistantWatermarkable2020_XFNBR8I4.png]] [(Yu 和 Xu, 2020, p. 6)](zotero://open-pdf/library/items/54PZI9RN?page=6&annotation=R7K4KMSA)

- *“fingerprinting code scheme”* [(Yu 和 Xu, 2020, p. 7)](zotero://open-pdf/library/items/54PZI9RN?page=7&annotation=T6LKXD5K) 
> **指纹码包括两个算法：生成算法和解密算法。生成算法生成一个码书和陷门，密码本给每个msg分配一个唯一的密文，陷门函数可以解密密文。** 

- *“marking assumption”* [(Yu 和 Xu, 2020, p. 7)](zotero://open-pdf/library/items/54PZI9RN?page=7&annotation=7XC93QQQ) 
> **嵌入假设：敌手不能篡改不可见位（密文相同的比特位置）** 

- *“the extraction algorithm of our scheme consists of three steps”* [(Yu 和 Xu, 2020, p. 8)](zotero://open-pdf/library/items/54PZI9RN?page=8&annotation=BJEN6UBE) 
> **1.提取出一个word和一段密文2.解密这个密文得到一个陷门3.用陷门把word恢复成msg** 


