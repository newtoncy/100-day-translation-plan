## 章节

- 介绍
- 描述整个过程
- 如何用代码表示、
- 总结

## 用tensorflow做线性回归（肯定不如我的卡西欧算得快:smirk:）

这个教程是关于在tensorflow训练一个线性模型来适应数据。另外，你可以去看看这篇博客 [blog post](http://www.machinelearninguru.com/deep_learning/tensorflow/machine_learning_basics/linear_regresstion/linear_regression.html)

## 介绍

在机器学习和统计中，线性回归是一个变量之间的模型，需要有一个Y和至少一个独立的变量X。在线性回归中，线性关系会用一个预测函数建模，它的参数会用数据估计，这被称为线性模型。线性回归算法最大的有点是它用起来很简单，能直接的把数据转换到新的模型，并映射到数据到新的空间。在此文中，我们会介绍如何训练一个线性模型，如何展示这个模型。

## 描述整个过程

为了训练这个模型，tensorflow要循环遍历数据并找到理想的直线（因为我们有一个线性模型），使它适应数据。这个在X和Y