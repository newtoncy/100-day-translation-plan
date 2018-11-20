# matplotlib usage guide

原文链接https://matplotlib.org/tutorials/introductory/usage.html#sphx-glr-tutorials-introductory-usage-py

介绍：

matplotlib是一个用来绘制函数图像的包。可以快速方便的展示出数据。计科必备

**ases=轴集：**翻译成**轴集**来和**asis**区别为了区分单复数而创建名词显得很傻屌，但是我没有办法

**asis=轴：**



## usage guide

这个教程涵盖了一些基础的用法范式和一些很好的练习，能帮助你开始matplotlib的使用

## General Concepts

matplotlib有庞大的代码，这可能会让很多新用户望而生畏。然而，大多数matplotlib的知识可以用非常简单的框架和少数重点的知识来理解。

绘图这个行为需要在不同的层次上进行，从最普遍的（例如：描绘一个二维数组）到最特殊的（例如把屏幕上所有像素涂成红色）。这个绘图包的目的就是要帮助你通过必要的控制来尽可能简单的实现数据可视化——这就是说，要在大多数使用相对高层的命令，但是同时当需要的时候也依然有能力使用底层的命令

因此，所有的东西在matplotlib中都是按层次组织的。在最高层是matplotlib的“state-machine environment（不知道啥东西）”，它在matplotlib.pyplot模块中提供。在这个层次，可以用一些简单的函数来添加绘图元素（线，图，文字，等）到当前的图像的当前的轴集。

>注：
>
>pyplot的状态机环境（？？）的行为与matlab很相似。用过matlab的用户会觉得很熟悉。

在下一个层次，是面向对象模型的第一层，在这一层中pypot只使用了少部分功能例如图的创建，用户需要明确的创建和跟踪图和轴集对象。在这个层次中用户使用pypot来创建图形，通过这些图形、一个或多个轴集对像可以被创建。这些轴集对象接着会在很多绘图操作中被使用

对于更多的操作——这对于把matplotlib嵌入到gui程序中是非常必要的——pyplot层可以完全舍弃，留下纯粹的面向对象方法。

```python
fig = plt.figure()  # an empty figure with no axes
fig.suptitle('No axes on this figure')  # Add a title so we know which it is

fig, ax_lst = plt.subplots(2, 2)  # a figure with a 2x2 grid of Axes
```

## 图的成分

![../../_images/anatomy.png](https://matplotlib.org/_images/anatomy.png)

### 图

整个图像。一个图像记录所有的子*轴集*。 a smattering of 'special' artists (titles, figure legends, etc), and the **canvas**（？？？）.（不用过分的关注cavas，作为你绘图的事实上的对象，它是十分关键的。但是对于用户来说它或多或少对你来说是透明的）。一个图可以含有多个轴集，但是要使一个图有用，至少应该包含一个轴集

```
fig = plt.figure()  # an empty figure with no axes
fig.suptitle('No axes on this figure')  # Add a title so we know which it is

fig, ax_lst = plt.subplots(2, 2)  # a figure with a 2x2 grid of Axes
```

![../../_images/sphx_glr_usage_001.png](https://matplotlib.org/_images/sphx_glr_usage_001.png)

![../../_images/sphx_glr_usage_002.png](https://matplotlib.org/_images/sphx_glr_usage_002.png)

### 轴集

这可以看做是“一个图”，这是数据空间的图像的一个区域。一个给定的图可以含有多个轴集。但是一个给定的轴集只能存在于一副图中。一个轴集容器包含了两个（或者三个，在三维的情况下）轴对象，轴对象是负责数据约束的。（数据约束也可以通过设置set_xlim()和set_ylim()两个轴方法来控制）。每个轴集都有一个题目（通过设置set_title()）一个x标签（通过设置set_xlabel()），和一个Y标签（通过设置set_ylabel()）。

轴集类和它的成员函数是面向对象接口的初级入口。

### 轴

这是

（睡了。。。。）