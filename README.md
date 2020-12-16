## Riboshape分析流程

### 1\) 分析流程

本项目主要为Riboshape项目的分析流程教程及说明。主要包括以下几个部分:

![1.png](evernotecid://58A46CB2-04A5-4F32-9233-277C274EDE1B/appyinxiangcom/19737026/ENResource/p321)


* 1.RNAseq数据分析
* * 1.1.差异表达分析
* * 1.2.差异剪切分析
* 2.Riboseq数据分析
* 3.Shapeseq数据分析
* * 3.1.Shapemapper重构
* * 3.2.结构改变区域分析
* * 3.3.motif分析
* 4.交叉分析画图
* * 4.1.结构对翻译的影响
* * 4.2.结构对差异剪切的影响

### 2\) 数据说明

我们目前有两个数据来源：liulab和maolab。

#### 2a) liulab数据

* **原始数据**

|  数据类型 | 数据批次 | 存放位置 | 样本信息说明  |
| :--- | :--- | :--- | :--- |
| Riboseq  | 第一批 | /Share2/home/lulab1/Riboshape/riboshape_liulab_ribo_batch1 | UV1代表不加光，UV2代表加光|
| Riboseq | 第二批  | /Share2/home/lulab1/Riboshape/riboshape_liulab_ribo_batch1  | no代表不加光，uvb代表加光 |
| Shapeseq | 第一批  | /Share2/home/lulab1/Riboshape/riboshape_liulab_batch1  | shape01是白光未标记，shape02是白光+1M7标记，shape04是1h UVB+1M7标记 |
| Shapeseq | 第二批  | /Share2/home/lulab1/Riboshape/riboshape_liulab_batch123/two_20190611  | 样本说明见这里 |
| Shapeseq | 第三批  | /Share2/home/lulab1/Riboshape/riboshape_liulab_batch123/three_1003  | 样本说明见这里 |
| Shapeseq | 第四批  | /Share2/home/lulab1/Riboshape/riboshape_liulab_batch4  | part1_clean,part1_raw为第一次测序结果，part2为加测结果，all为合并两次结果。C代表WT样本，U代表UVR8突变体；D代表不加药样本，N代表加NAI样本；0代表UV+样本，1代表UV- |

* **分析使用数据**

![2.png](evernotecid://58A46CB2-04A5-4F32-9233-277C274EDE1B/appyinxiangcom/19737026/ENResource/p322)


a.WT,UV-不加药时，RNA-seq相关性。
b.不同批次数据差异表达基因数目。
c.HY5的表达水平。
d. batch4的RNA-seq数据相关性。
e. Ribo-seq数据的相关性。
f. Riboseq数据WT_UV-一个样本的周期性。满足3’周期性要求。

从a图中可知，不同批次之间存在batch effect。第一、三批数据与其他相关性较弱，尤其是第一批数据。从b图中可知，第三批样本明显与其他数据不同，差异基因过少。从c图中可知，HY5为受到UVR8调控的下游基因，在加光后表达上调。但是在batch3中却无明显变化。由此可知，batch1,batch3数据质量存在问题，不纳入后续分析过程。

从d图中可知，batch4的三个样本RNA-seq数据重复性较好。另外batch2数据测序深度仅为batch4数据十分之一，所以**后续RNA-seq数据和Shape-seq分析以batch4的三个样本为主**，batch2样本可作为验证样本。

从e图中可知，**Riboseq数据**也有两批，两批之间相关性较差，后续分析**仅使用第二批数据**。


#### 2b) maolab数据

* **原始数据**

|  数据类型 | 数据批次 | 存放位置 | 样本信息说明  |
| :--- | :--- | :--- | :--- |
| Shapeseq | 第一批  | /Share2/home/lulab1/Riboshape/riboshape_maolab_batch1和/Share2/home/lulab1/Riboshape/riboshape_maolab_batch1_2  |riboshape_maolab_batch1为第一次测序数据，riboshape_maolab_batch1_2为第二次加测结果。Coil为Coil突变体，Col-0为WT样本；DMSO为不加药样本，NAI为加NAI样本；CK为不加JA样本，JA为加JA样本  |
| Shapeseq | 第二批  | /Share2/home/lulab1/Riboshape/riboshape_maolab_batch2和/Share2/home/lulab1/Riboshape/riboshape_maolab_batch2_2  | riboshape_maolab_batch2为第一次测序数据，riboshape_maolab_batch2_2为第二次加测结果。Coil为Coil突变体，Col-0为WT样本；DMSO为不加药样本，NAI为加NAI样本；CK为不加JA样本，JA为加JA样本 |


