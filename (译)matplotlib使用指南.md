# matplotlib usage guide

原文链接https://matplotlib.org/tutorials/introductory/usage.html#sphx-glr-tutorials-introductory-usage-py

介绍：

matplotlib是一个用来绘制函数图像的包。可以快速方便的展示出数据。计科必备

## usage guide

这个教程涵盖了一些基础的用法范式和一些很好的练习，能帮助你开始matplotlib的使用

## General Concepts

matplotlib有庞大的代码，这可能会让很多新用户望而生畏。然而，大多数matplotlib的知识可以用非常简单的框架和少数重点的知识来理解。

绘图这个行为需要在不同的层次上进行，从最普遍的（例如：描绘一个二维数组）到最特殊的（例如把屏幕上所有像素涂成红色）。这个绘图包的目的就是要帮助你通过必要的控制来尽可能简单的实现数据可视化——这就是说，要在大多数使用相对高层的命令，但是同时当需要的时候也依然有能力使用底层的命令

因此，所有的东西在matplotlib中都是按层次组织的。在最高层是matplotlib的“state-machine environment（不知道啥东西）”，它在matplotlib.pyplot模块中提供。在这个层次，可以用一些简单的函数来添加绘图元素（线，图，文字，等）到当前的图像的当前的轴。

>注：
>
>pyplot的状态机环境（？？）的行为与matlab很相似。用过matlab的用户会觉得很熟悉。

在下一个层次

（今天。。。。代码混更行不）