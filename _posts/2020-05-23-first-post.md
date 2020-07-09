---
title: nnlp：exercise1
author: wuxuan
layout: post
---
[TOC]

部分答案参考 github.com/nndl/solutions/issues
如有错误，欢迎指正。

## 2-1 
因为分类问题中的标签没有连续的概念，1-hot作为分类标签的一种表示形式，标签间的距离没有实际意义，所以平方差不能反应这个问题的优化程度。如果是将类别号直接做标签，比如分类 1,2,3, 真实分类是1, 而被分类到2和3错误程度应该是一样的, 但是平方损失函数的损失却不相同。

## 2-2

* $X\in \mathbb{R}^{k\times N}$，$Y\in N\times 1$, $R\in N\times1,w\in k\times 1$

$$\frac{\partial \mathcal{R}(w)}{\partial w } = \frac{1}{2}\frac{\partial \left\|R\cdot (Y-X^Tw)\right\|^2_2}{\partial w} = -X\cdot R\cdot (Y-X^Tw)$$

用到了这样的求导式：

$$\frac{\partial \left\|x\right\|^2}{\partial x} = 2x$$

令$\frac{\partial \mathcal{R}(w)}{\partial w} = 0$，
如果$XX^T$可逆，得到最优参数$w^*$为$(XX^T)^{-1}XY$，
否则，若使用梯度下降法来估计参数，先初始化$w=0$再用

$$w\leftarrow w+\alpha XR(Y-X^Tw)$$

迭代，得到最优参数$w^*$

* 可见，当估计最优参数时，每次更新w，R可以给每个样本的残差加一个权重，使得w的训练结果有考虑到不同样本的重要程度（比如给判定为outlier的样本小一点的权重），这样可以减小线性回归的敏感性。

## 2-3
对于$XX^T\in R^{(D+1)\times(D+1)}$，$rank(XX^T)=rank(X)<=N$（$rank(XX^T)=rank(X)$证明见 (https://zh.wikipedia.org/wiki/%E7%A7%A9_(%E7%BA%BF%E6%80%A7%E4%BB%A3%E6%95%B0)[wiki-rank-证明3]）

## 2-4
令$\frac{\partial \mathcal{R}(w)}{\partial w} = 0$可得到

$$w^*=(XX^T+\lambda I)^{-1}Xy$$

## 2-5
令

$$\frac{\partial log(p(y|x;w,\delta))}{\partial w} = 0$$

就是

$$X(y-w^Tx)=0$$

## 2-6

