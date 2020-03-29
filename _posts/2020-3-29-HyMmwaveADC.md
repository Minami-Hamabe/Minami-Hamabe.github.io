---
layout: post
title:  On Low-Resolution ADCs in Practical 5G Millimeter-Wave Massive MIMO Systems
---

Key challenge : channel estimation, signal detector, channel information feedback, transmit precoding

![1584932455408](C:\Users\lenovo\Desktop\dll\NOMA\1584932455408.png)

Institution: ADC功耗随采样速率先线性增长，随分辨率比特指数增长。

现代商用ADCs 采样速率$\ge 20$ Gsamples/s ,分辨率 8-12 bits,功耗500mW

采用高分辨率低速ADCs，不同ADCs的不匹配会恶化系统性能下限。

采用低分辨率高速ADCs可以有效减少功耗，主要有算法上的挑战。

![1584930909331](C:\Users\lenovo\Desktop\dll\NOMA\1584930909331.png)



## Performance Analysis

[3] 为达到系统容量限，发射机需要根据CSI对发射符号星座点进行设计；SISO系统中1bit ADCs的最优星座是2进制映射；**1bit ADC若要支持高阶星座，则需要空间过采样的MIMO系统支持** $\how?$；实际毫米波信道的最优星座设计仍需要凸优化解决。

------

AQNM(Additive quantization noise model) [2,5,6]可描述量化噪声模型。

输入信号是高斯分布时，可以推导出容量的下界限[5]。3bit ADC即可接近理想无穷精度，且性能可随天线数增多而提升。Mixed-ADC也是一种可选结构

![1584932500839](C:\Users\lenovo\Desktop\dll\NOMA\1584932500839.png)

AQNM的缺陷：**高SNR不准确** 。原因：它假设输入和噪声都是高斯的，ADC 的量化选择不是MMSE的。实际中，量化MIMO的信道容量，输入分布，量化门限仍然未知。

------

[2] 低SNR是可观的(73%的理想性能)，高SNR可部署一些高精度ADCs来改善

[6] 使容量最优量化比特数目和接收机SNR有关

------

**后续研究：**量化对导频的影响,非理想CSI情况，ADCs的最优量化阈值，毫米波信道下信源符号的最优分布(信息论角度),



## 信道估计

[7] 可靠的CSI估计需要的导频数目是用户数目的50倍长，导频序列过长。

对于毫米波信道采用GAMP估计，将矢量估计转化为标量估计，优于EM

[8] EM算法来最小化MMSE,低SNR可靠，高SNR会由于EM的初始化陷入局部最优，且复杂度高

[9] 利用凸优化进行最大似然估计，高SNR下比EM好

[10] JCD，需要完美CSI，复杂度高

![1584933194858](C:\Users\lenovo\Desktop\dll\NOMA\1584933194858.png)

上述缺陷：未利用毫米波稀疏性，导频过长或者复杂度高

[11] 采用mixed AC减少误差

非相关检测[12]或者贪婪算法是减少导频长度的方案



## 信号检测

扩展到宽带和低精度ADC是一个挑战

[19] 考虑多用户消息传递检测器，适用空间调制SM -based MIMO，只需一根RF。复杂度低，性能优于线性检测，但不能直接用于低精度量化，未考虑毫米波稀疏性。



### 其他挑战

------

#### CSI feedback

#### transmit precoding

#### mixed-ADC 

![1584952296786](C:\Users\lenovo\Desktop\dll\NOMA\1584952296786.png)

包括：某特定信噪比下的最优ADC分配问题？在宽带毫米波信道下的问题？

[11]  N. Liang and W. Zhang, “Mixed-ADC Massive MIMO,” IEEE JSAC, vol. 34, no. 4, May 2016, pp. 983–97.

[14] J. Zhang et al., “Performance Analysis of Mixed-ADC Massive MIMO Systems over Rician Fading Channels,” IEEE JSAC, vol. 35, no. 6, Jun. 2017, pp. 1327–38.

