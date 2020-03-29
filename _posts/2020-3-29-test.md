---
layout: post
title: A review for NOMA
---

分类：power domain NOMA / code domain NOMA

优点:   

1. 相比OMA更高的频谱效率和小区吞吐量
2. 巨维连接
3. 不用接入许可，延时1ms<低于LTE的15.5ms
4. channel feedback 的需要降低

缺点：

​	1.接受端需SIC，复杂度增加



### power domain NOMA

------

比OFDMA高 30% 的小区吞吐

#### 1）依赖于SIC的NOMA

考虑单个BS服务K用户，发射信号是K和用户信号的功率加权
$$
x=\sum_{i=1}^K{\sqrt{p_i}}x_i \tag{4}
$$
其中$p_i$满足功率约束$$P=\sum_{i=1}^{K}p_i$$ 则用户$$i$$ 的接收信号是
$$
y_i = h_ix+v_i \tag{5}
$$
其中$$v_i$$ 的功率谱密度是$$ N_i $$ ，包括高斯噪声和小区内干扰

最优的SIC顺序是信道增益$|h_i|^2/N_i$ 从强到弱的顺序，因为信道增益强的用户有更高的正确检测概率，而基站侧对相应用户的功率分配则应该是由小到大以提高SINR。这样，用户$i$ 的可达速率为
$$
R_i =W{\mathrm {log}}(1+\frac{p_i|h_i|^2}{N_iW+(\sum_{j=i}^{i-1}p_j)|h_i|^2}) \tag{6}
$$
**例：双用户下行**

![_config.yml]({{ site.baseurl }}/images/2020-3-29-1.png)
R_1={\mathrm{log}}(1+\frac{p_1|h_1|^2}{N_1})\tag{7}\\
$$

$$
R_2={\mathrm{log}}(1+\frac{p_2|h_2|^2}{p_1|h2|^2+N_2})\tag{8}
$$

基站通过功率分配可以调节不同用户的可达速率

**例：上行传输**
$$
y=\sum_{i=1}^{K}h_i\sqrt{p_i}x_i +v,\tag{9}
$$
假设$p_1|h_1|^2 \ge p_2|h_2|^2\ge \cdots \ge p_K|h_K|^2$ ，最优检测顺序是$x_1,x_2,\cdots,  x_K$ ,那么基站在检测第$i $ 个用户信号时，它先检测 $j<i$ 的$i-1$个信号，并从观测y中除去，剩下的$K-i$ 个信号则是干扰，那么$R_i$ 为
$$
R_i = W\mathrm{log}(1+\frac{p_i|h_i|^2}{N_0W+\sum_{j=i+1}^K |h_j|^2p_j}) \tag{10}
$$
这种方案在上下行都能达到最大可达速率，实现SE 与用户公平性的折中

**缺点** ：误差传播



#### 2) NOMA in MIMO

### ![1584861271(1)](C:\Users\lenovo\Desktop\戴玲珑\NOMA\1584861271(1).png)

**下行**
$$
\mathbf{x_0} =\sum_{b=1}^B\mathbf{m_b}\sum_{i=1}^{k_b}\sqrt{p_{b,i}x_{b,i}}\tag{11}
$$

$$
\mathbf{y}_{b,i} =\mathbf{H}_{b,i}\mathbf{x}_0+\mathbf{v}_{b,i} \tag{12}
$$

考虑**用户多天线**，波束间干扰可以用过空间滤波抑制，波束间干扰可以通过类似SIC方法抑制

**上行**
$$
\mathbf{y} =\sum_{i=1}^K \mathbf{h}_i\sqrt{p_i}x_i
$$
考虑**用户单天线** ，基站可以通过MMSE-SIC接收机检测，用户的解码顺序可以根据实际需要调整



#### 3) cooperative NOMA

与1)中不同，可以利用短距离通信方案如蓝牙和UBW来讲信道质量好的用户信号传递给信道质量差的用户。

**下行**

1st—信道最差，Kth—信道最好

1）广播阶段：与1）中basic NOMA with SIC相同

2）协作传输：利用短距通信信道(如蓝牙，UWB), 包括K-1个时隙。第1时隙，第K个用户广播K-1个叠加的信号,K-1个用户再次进行SIC,以此类推。

缺点：短距通信信道的实现较为困难 



#### 4) NOMA in CoMP

![1584862891(1)](C:\Users\lenovo\Desktop\戴玲珑\NOMA\1584862891(1).png)

#### 5）power domain NOMA的应用

ASTC 3.0 美国下一代广播标准：LDM()分层复用， upper layer用于移动终端， lower layer 用于固定高速率设备，如HDTV



### Code Domain NOMA

------

与CDMA区别：扩频序列是**稀疏序列**或者是**非正交**的互相关程度低的序列

#### 1) Low-Density Spreading CDMA (LDS-CDMA) 

不足之处是多径信道会破坏这种LDS结构，不同于CDMA中经典正交扩频码，LDS-CDMA使用稀疏码序列，发送符号被调制到这种稀疏序列上，因此每个码片上叠加的用户信号数远小于活跃用户数，从而减少用户间干扰。

第n个码片处接受信号可以写成
$$
y_n = \sum_{k \in N(n)}g_{n,k}s_{n,k}x_{k}+w_n = \sum_{k \in N(n)}h_{n,k}x_{k}+w_n \tag{19}
$$
其中 $g_{n,k}$是用户k在第n个码片上的信道增益，$s_{n,k}$ 是扩频序列，$N(n) = \{k|s_{n,k} \ne 0\}$  

![1584876037(1)](C:\Users\lenovo\Desktop\戴玲珑\NOMA\1584876037(1).png)

根据sum-product算法，结点的更新如下：
$$
m_{d\rightarrow e}^{(t)} \propto \sum_{\{x_i|i \in N(d) \backslash d\}}f_d(X_d) \prod_{i \in N(d)\backslash e}m_{i\rightarrow d}^{(t-1)}(x_i) \tag{22}
$$

$$
m_{e \rightarrow d}^{(t)}(x_e) \propto \prod_{i \in N(d)\backslash e} m_{i \rightarrow e}^{(t-1)}(x_e) \tag{23}
$$

在迭代T次后，变量结点的边沿概率分布是所有从函数结点收到信息的函数
$$
p(x_e) \propto \prod_{d \in N(e)}m_{d \rightarrow e}^{(T)}(x_e)
$$
  另外，全局概率密度
$$
p(x_1,x_2,\cdots,x_E) = \frac{1}{Z} \prod_{d=1}^D f_d(X_d)
$$
可通过设计LDS改变因子图的连通性和环，结果能接近单用户场景[64]

#### 2) LDS-OFDM

与MC-CDMA类似，如果扩频码的chips数与OFDM子载波数相同，都相当于将每个用户的序号扩到所有子载波上。可采用正交的Walsh-Hadamard码，或者非正交的m序列，LDSs等。

在LDS-OFDM中，**传输符号先乘以LDSs序列(长度与子载波数相同)，结果再在不同子载波上传输**。(相当于单用户用了所有OFDM子载波资源)，这样既能对抗多径衰落，即使某些子载波数据损坏，仍然可通过消息传递算法恢复。

#### 3) SCMA (Sparse Code Multiple Access)

#### 3) SCMA

![1584879854(1)](C:\Users\lenovo\Desktop\戴玲珑\NOMA\1584879854(1).png)

**将比特-星座点映射和扩频操作融合一起，一步实现**。若扩频码长$K_l$ 等于载波数，码字非零元数目为$N_{nz}$ ,则最多可支持$C_{K_l}^{N_{nz}}$ 个码本

SCMA能带来其他NOMA方案没有的"constelltion shaping gain"星座成型增益，其实也是平均符号能量增益。

若不同码本非零元素数目不同，则用户的QoS也不同[89]

**然而，最优的多维星座图的码本设计是一个复杂的问题，18年时仍未解决**

**优点：设计码本和导频后，可以实现grant-free 的多址接入** [90]



**上行**

![1584880861(1)](C:\Users\lenovo\Desktop\戴玲珑\NOMA\1584880861(1).png)

上图上行中，J 个码本，每码本L个导频序列，共享一个竞争传输单元，接收端可以借助盲检测或压缩感知实现联合活跃用户检测与数据检测[91]



**下行**

MU-SCMA优点：不需要提供接近瞬时的CSI反馈信息，是开环接入方案



## 其他NOMA方案

1.Multi-User Shared Access (MUSA)

2.Successive Inference Cancellation Aided Multiple Access(SAMA)

3.Spatial Division Multiple Access(SDMA)

4.Pattern Division Multiple Access (PDMA)

5.Signature-Based NOMA

6.Interleaver-Based NOMA

7.Spreading-Based NOMA

8.Bit Division Multiplexing(BDM)

9.Compressive Sensing (CS)-based NOMA



### Challenging work

1.扩频序列与码本设计

2.接收机设计

3.信道估计

5.Grant-free NOMA

6.资源分配

7.扩展到MIMO

8.认知无线电

9.降低PAPR等...

