---
layout:		post
title:		python里的数据科学之Numpy实战
categories:
- TECHNOLOGY
tags:
- Python
- ML
- Numpy
permalink:  Explore-Numpy-Python
comments:	true
date:		2015-12-04 14:00:06
---
Python的强大就不多说了，而对于Numpy的教程网上也多得数不清，这里只是将Numpy在日常中的实用方法做个梳理小结，方便以后查阅上手。
<!-- more -->


## 简介
对于数据科学，它是Python创建的所有更高层工具的基础，因为它和最基础的数据结构--矩阵有关。其核心也就是这个多维矩阵（**n**-**d**imesional **array**）,这是一个表示多维度、同质并且固定大小的阵列。Numpy这个库提供了以下内容：

1. N维数组，一种多维度、同质、能快速、高效使用内存的阵列 。
2. 提供基于矩阵的数学运算
3. 提供线性代数，傅里叶变换和随机数生成

## 多维矩阵
Numpy的主要对象是多维矩阵（ndarray），这是一个所有的元素都是一种类型、通过一个正整数元组索引的元素表格。在Numpy中维度（dimensions）叫做轴（axes），轴的个数叫做秩（rank）。其有如下属性：  

* ndim   
矩阵轴的个数，也就是秩
* shape  
矩阵的维度
* size      
矩阵元素的总个数，等于shape属性中所有元素的乘积
* dtype   
矩阵中元素类型
* itemsize  
矩阵中每个元素的字节大小
* data      
包含实际矩阵存放在内存的地址
* I  
矩阵的逆，等价于linalg.pinv，而不等价于linalg.inv
* T  
矩阵的转置，等价于ndarray.transpose().
*


多维矩阵（ndarray）除了基本属性外，还有很多处理函数。

1. 构建  
    * reshape/flatten    
    重构矩阵/将矩阵拉伸成一维向量，等价于ndarry.reshape(ndarray.size)
    * copy/fill      
    深拷贝矩阵（直接赋值只是浅拷贝）/向矩阵中填充数值，和memset功能类似
    * sort  
    对矩阵进行排序
    *
2. 提取
    * clip/diagonal  
    提取范围里的元素/提取对角线上的元素
    *
2. 方法
    * sum/prod/min/max/argmin/argmax  
    求矩阵中所有元素的和/积/最小值/最大值/最小值索引/最大值索引
    * mean/var/std  
    求矩阵中所有元素的均值方差/标准差
    *
4. 转换
    * tolist/tostring    
    转换成链表/字符串

> **Tips:**
> 这里的很多函数都用来处理多维矩阵（m×n），有如下特性：  
>
> 1. 不加axis参数，则该函数是对矩阵所有元素起作用，即将多维矩阵拉伸成一维后进行相应操作，最后获得一个数。
> 2. 加axis=0，则该函数是对每一列起作用，即按照列对相应元素进行运算，最终获得一个1×n的一维向量。
> 3. 加axis=1，则该函数是对每一行起作用，即按照行对相应元素进行运算，最终获得一个m×1的一维向量。
>


## 基本操作
1. 构建
    * concatenate  
    把多个矩阵串起来，通过axis参数调节横向（1）和纵向（0/默认）
    * ones/zeros/ones_like/zeros_like  
    创建全1/0矩阵/创建和矩阵相同维度的全1/0矩阵
    * identity  
    创建单位矩阵
    * eye  
    创建方阵（长宽都相当的矩阵），指定莫个对角线为1,其它为0
2. 提取
    * logical_and/logical_not/logical_or  
    逻辑与/逻辑非/逻辑或
    * where  
    跟if类似
    * isnan/isfinite  
    是否是一个数/无穷
    * take/put  
    将一个矩阵里的元素当索引提取/存放矩阵
    *
3. 方法
    * abs/sign/sqrt/log/log10/exp  
    绝对值/取符号位/开根号/以2为底的对数/以10为底的对数/指数
    * floor/ceil/rint  
    向下取整/向上取整/四舍五入取整
    * sin/cos/tan/arcsin/arccos/arctan  
    正弦/余弦/正切/反正弦/反余弦/反正切
    * sinh/cosh/tanh/arcsinh/arccoh/arctanh  
    双曲正弦/双曲余弦/反双曲正弦/反双曲余弦/反双曲正切
    * dot/outer/inner/cross  
    点乘/外积/内积/向量积
    * median/corrcoef/cov  
    求中位数/相关系数/协方差
    *


## 线性代数
包含线性代数的所有的函数都包含在linalg子库中。

* det/eig/inv/pinv/svd  
求矩阵的行列式/特征值和向量/逆/伪逆/奇异值分解
*


## 傅里叶变换
关于傅里叶变换的函数包含在fft子库中。

## 随机数生成
关于随机数的生成函数都在random子库中。

* seed  
设定随机种子
* rand  
构建随机矩阵
* random  
获取一个随机数
*

## 多项式
关于多项处理的函数都在polynomial子库中。



## 测试工具
关于测试工具的函数在testing子库中。


## 参考文献
1. [python官网][python]
2. [Python27入门指南][python27]
3. [Python35入门指南][python35]
4. [numpy源码][numpy_src]
5. [numpy快速入门][numpy_quick]
6. [numpy教程][numpy_jc]
7. [numpy初入门][numpy_js]

[python]:   https://www.python.org/
[python27]: http://www.pythondoc.com/pythontutorial27/
[python35]: http://www.pythondoc.com/pythontutorial3/index.html
[numpy_src]:    https://github.com/numpy/numpy
[numpy_quick]:  https://docs.scipy.org/doc/numpy-dev/user/quickstart.html
[numpy_jc]:     http://reverland.org/python/2012/08/22/numpy/
[numpy_js]:     http://www.engr.ucsb.edu/~shell/che210d/numpy.pdf
