# 快速上手教程

## 前提条件

在阅读本教程之前你需要先知道一些python的知识。如果你想刷新你的记忆，来看看python教程吧 [Python tutorial](http://docs.python.org/tut/)

如果你希望使用本教程中的示例，有一些软件需要安装在你的电脑上，请看教程<http://scipy.org/install.html>

## 基础

NumPy的主要对象是同质的多维数组，它是一个元素组成的表（通常是数字），所有的元素是同一类型的，用一个正整数元组索引。在NumPy中这被称为轴。

举个栗子，一个三维空间中的点[1, 2, 1]有一个轴。这个轴的长度为3。在下面的例子中，这个数组有两个轴，第一个轴长度是2，第二个轴长度是3.

```python
[[ 1., 0., 0.],
 [ 0., 1., 2.]]
```

NumPy的数组类名叫 `ndarray`，它也有一个别名叫`array`.注意 `numpy.array` 与python标准库中的`array.array`一点也不同,python的array只提供了一维的数组和少量的函数,`ndarray`比较重要的属性有:

- ndarray.ndim

  数组轴的数量

- ndarray.shape

  数组的维度.这是一个整数元组,指出了每一个维度的大小.一个n行m列矩阵的这个值会是`(n,m)`,元组的长度和轴的个数,即`ndim`是相当的.

- ndarray.size

  数组的元素总数.他等于shape各元素的乘积

- ndarray.itemsize

  数组中每个元素的大小,例如float64的`itemsize`是8,`complex32`的`itemsize`是4.它与`ndarry.dtype.size`是相当的

- ndarray.data

  这个buffer储存了array实际元素.通常,我们不会使用这个属性,因为你可以通过索引值功能来访问元素

### 一个例子

```python
>>> import numpy as np
>>> a = np.arange(15).reshape(3, 5)
>>> a
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14]])
>>> a.shape
(3, 5)
>>> a.ndim
2
>>> a.dtype.name
'int64'
>>> a.itemsize
8
>>> a.size
15
>>> type(a)
<type 'numpy.ndarray'>
>>> b = np.array([6, 7, 8])
>>> b
array([6, 7, 8])
>>> type(b)
<type 'numpy.ndarray'>
```

## 数组的创建

这里提供了几种创建数组的方法 

举个栗子,你可以用常规的python列表和元组来使用`array`函数.数组的类型会从给的类型中推导出来.

```python
>>> import numpy as np
>>> a = np.array([2,3,4])
>>> a
array([2, 3, 4])
>>> a.dtype
dtype('int64')
>>> b = np.array([1.2, 3.5, 5.1])
>>> b.dtype
dtype('float64')
```

一个常见的错误是把数字当作参数传给array而不是提供一个数字列表作为参数

```python
>>> a = np.array(1,2,3,4)    # WRONG
>>> a = np.array([1,2,3,4])  # RIGHT
```

数组转换可以用序列套序列的方式转化成二维数组,也可以用序列套序列套序列的方式创建一个三维数组,以此类推

```python
>>> b = np.array([(1.5,2,3), (4,5,6)])
>>> b
array([[ 1.5,  2. ,  3. ],
       [ 4. ,  5. ,  6. ]])
```

元素的类型也可以在创建的时候明确给出

```python
>>> c = np.array( [ [1,2], [3,4] ], dtype=complex )
>>> c
array([[ 1.+0.j,  2.+0.j],
       [ 3.+0.j,  4.+0.j]])
```

经常我们初始时并不知道数组中的元素时什么,但是我们知道元素的大小.因此，NumPy提供了几个函数用占位符初始化数组内容。创建一个最小化的，但是可以增长的数组，是非常昂贵的操作。

```python
>>> np.zeros( (3,4) )
array([[ 0.,  0.,  0.,  0.],
       [ 0.,  0.,  0.,  0.],
       [ 0.,  0.,  0.,  0.]])
>>> np.ones( (2,3,4), dtype=np.int16 )                # dtype can also be specified
array([[[ 1, 1, 1, 1],
        [ 1, 1, 1, 1],
        [ 1, 1, 1, 1]],
       [[ 1, 1, 1, 1],
        [ 1, 1, 1, 1],
        [ 1, 1, 1, 1]]], dtype=int16)
>>> np.empty( (2,3) )                                 # uninitialized, output may vary
array([[  3.73603959e-262,   6.02658058e-154,   6.55490914e-260],
       [  5.30498948e-313,   3.14673309e-307,   1.00000000e+000]])
```

为了创建一个数组序列，Numpy提供了一个类似于`range`的函数,只是它返回的是一个array而不是list

```python
>>> np.arange( 10, 30, 5 )
array([10, 15, 20, 25])
>>> np.arange( 0, 2, 0.3 )                 # it accepts float arguments
array([ 0. ,  0.3,  0.6,  0.9,  1.2,  1.5,  1.8])
```

当arange用于浮点数时,因为有限的浮点精度,我们不能确定最终会生成多少个元素.因此,我们通常使用函数`linspace`,它接受想要多少个元素作为步长的代替

```python
>>> from numpy import pi
>>> np.linspace( 0, 2, 9 )                 # 9 numbers from 0 to 2
array([ 0.  ,  0.25,  0.5 ,  0.75,  1.  ,  1.25,  1.5 ,  1.75,  2.  ])
>>> x = np.linspace( 0, 2*pi, 100 )        # useful to evaluate function at lots of points
>>> f = np.sin(x)
```

See also

[`array`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.array.html#numpy.array), [`zeros`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.zeros.html#numpy.zeros), [`zeros_like`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.zeros_like.html#numpy.zeros_like), [`ones`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ones.html#numpy.ones), [`ones_like`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ones_like.html#numpy.ones_like), [`empty`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.empty.html#numpy.empty), [`empty_like`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.empty_like.html#numpy.empty_like), [`arange`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.arange.html#numpy.arange), [`linspace`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.linspace.html#numpy.linspace),[`numpy.random.rand`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.random.rand.html#numpy.random.rand), [`numpy.random.randn`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.random.randn.html#numpy.random.randn), [`fromfunction`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.fromfunction.html#numpy.fromfunction), [`fromfile`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.fromfile.html#numpy.fromfile)

## 打印数组

当你打印一个数组的时候,NumPy提供了一个机智的嵌套列表打印方法,按照以下规则

- 不重要

```
>>> a = np.arange(6)                         # 1d array
>>> print(a)
[0 1 2 3 4 5]
>>>
>>> b = np.arange(12).reshape(4,3)           # 2d array
>>> print(b)
[[ 0  1  2]
 [ 3  4  5]
 [ 6  7  8]
 [ 9 10 11]]
>>>
>>> c = np.arange(24).reshape(2,3,4)         # 3d array
>>> print(c)
[[[ 0  1  2  3]
  [ 4  5  6  7]
  [ 8  9 10 11]]
 [[12 13 14 15]
  [16 17 18 19]
  [20 21 22 23]]]
```

[省略一段不译]

## 基础运算

数组四则运算会对每个元素分别进行.一个细腻的数组被创建然后填上值.

```python
>>> a = np.array( [20,30,40,50] )
>>> b = np.arange( 4 )
>>> b
array([0, 1, 2, 3])
>>> c = a-b
>>> c
array([20, 29, 38, 47])
>>> b**2
array([0, 1, 4, 9])
>>> 10*np.sin(a)
array([ 9.12945251, -9.88031624,  7.4511316 , -2.62374854])
>>> a<35
array([ True, True, False, False])
```

不像很多矩阵描述那样,操作符*对每个元素做乘法.矩阵的积可以用@运算符表示(在python>3.5中)或者用`dot`函数或方法

```
>>> A = np.array( [[1,1],
...             [0,1]] )
>>> B = np.array( [[2,0],
...             [3,4]] )
>>> A * B                       # elementwise product
array([[2, 0],
       [0, 4]])
>>> A @ B                       # matrix product
array([[5, 4],
       [3, 4]])
>>> A.dot(B)                    # another matrix product
array([[5, 4],
       [3, 4]])
```

一些运算符像+= *=将修改已经存在的数组而不是创建一个

```python
>>> a = np.ones((2,3), dtype=int)
>>> b = np.random.random((2,3))
>>> a *= 3
>>> a
array([[3, 3, 3],
       [3, 3, 3]])
>>> b += a
>>> b
array([[ 3.417022  ,  3.72032449,  3.00011437],
       [ 3.30233257,  3.14675589,  3.09233859]])
>>> a += b                  # b is not automatically converted to integer type
Traceback (most recent call last):
  ...
TypeError: Cannot cast ufunc add output from dtype('float64') to dtype('int64') with casting rule 'same_kind'
```

When operating with arrays of different types, the type of the resulting array corresponds to the more general or precise one (a behavior known as upcasting).

```python
>>> a = np.ones(3, dtype=np.int32)
>>> b = np.linspace(0,pi,3)
>>> b.dtype.name
'float64'
>>> c = a+b
>>> c
array([ 1.        ,  2.57079633,  4.14159265])
>>> c.dtype.name
'float64'
>>> d = np.exp(c*1j)
>>> d
array([ 0.54030231+0.84147098j, -0.84147098+0.54030231j,
       -0.54030231-0.84147098j])
>>> d.dtype.name
'complex128'
```

在默认情况下,对数组做这些操作时数组就像一个数字列表一样,不管它是什么形状.然而通过指定`axis`参数你可以把操作应用到某一个轴上.

```python
>>> b = np.arange(12).reshape(3,4)
>>> b
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11]])
>>>
>>> b.sum(axis=0)                            # sum of each column
array([12, 15, 18, 21])
>>>
>>> b.min(axis=1)                            # min of each row
array([0, 4, 8])
>>>
>>> b.cumsum(axis=1)                         # cumulative sum along each row
array([[ 0,  1,  3,  6],
       [ 4,  9, 15, 22],
       [ 8, 17, 27, 38]])
```

