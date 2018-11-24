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

这是线性的数值状的对象(???无法想象是个啥).它负责设置图的约束和生成刻度(标记在数轴上的)和刻度标签(标记刻度的字串).刻度的位置是由Lacator对象决定的,坐标轴刻度的标示是由Formatter对象格式化的,正确的Formatter和Lacator对象的组合能很好的控制刻度的为中和显示

### 画师

基本上,你在图像中看到的每一样东西都是一个画师(甚至图像,轴集,和轴对象).它包括了文字对象,二维线对象,集合对象,批次对象...(你懂的).当讴歌图像渲染,所有的画师都在canvas上绘制.多数画师绑定了一个轴集,多个轴不能共享一个艺术家,或者把一个艺术家移到另一个上.

## 绘制函数的输入类型

所有的绘图函数都需要`np.array` 或 `np.ma.masked_array` 作为输入.经典的"数组类似"的类型比如 [`pandas`](https://pandas.pydata.org/pandas-docs/stable/index.html#module-pandas)数据对象和 `np.matrix`可能会也可能不会像预期的那样工作. 所以最好在绘图之前将他们转化成`np.array` 对象

举个栗子,转化一个 [`pandas.DataFrame`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html#pandas.DataFrame)

```python
a = pandas.DataFrame(np.random.rand(4,5), columns = list('abcde'))
a_asndarray = a.values
```

以及转化一个 `np.matrix`

```python
b = np.matrix([[1,2],[3,4]])
b_asarray = np.asarray(b)
```

## Matplotlib, pyplot 和pylab:他们有怎样的关系

matplotlib是一个完整的包,; [`matplotlib.pyplot`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.html#module-matplotlib.pyplot)是包中的一个模块,pylab是一个会和matplotlib一起安装的一个模块.

pyplot提供一个state-machine接口到底层的面向对象绘图库.这个state-machine隐式的创建图,轴集来实现预期的绘制,例如:

```python
x = np.linspace(0, 2, 100)

plt.plot(x, x, label='linear')
plt.plot(x, x**2, label='quadratic')
plt.plot(x, x**3, label='cubic')

plt.xlabel('x label')
plt.ylabel('y label')

plt.title("Simple Plot")

plt.legend()  # 图例

plt.show()
```

![../../_images/sphx_glr_usage_003.png](https://matplotlib.org/_images/sphx_glr_usage_003.png)

第一个调用的是 `plt.plot` ,会自动的创建必要的图和轴集来实现预期的绘制.接下来调用 `plt.plot` 复用当前的轴集并每次添加一条曲线,设置标题,图例,和轴标签也是自动的用了当前的轴集并设置了标题,创建图例,和对每个轴分别创建文本框.

pylab是一个方便的模块,它批量的导入了 [`matplotlib.pyplot`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.html#module-matplotlib.pyplot) (为了绘图) 和 [`numpy`](https://docs.scipy.org/doc/numpy/reference/index.html#module-numpy) (为了数学计算和处理数组) 在单个命名空间中.pylab被弃用了并且强烈不建议使用它因为命名空间污染问题.用pyplot来代替它.

作为非互动的绘图,很建议用pyplot来创建图然后用面向对象接口来绘图.