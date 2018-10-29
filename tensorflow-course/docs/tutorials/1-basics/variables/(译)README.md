# 介绍TensorFlow的变量：创建和初始化

这个教程解决创建和初始化变量的问题

## 介绍

定义变量是必要的因为他们包含了参数。没有参数，训练，更新，保存，恢复和其他任何操作都不能被执行。在TensorFlow中定义的变量只能是有特定形状和类型的张量。张量必须被赋予初值才能成为有效的。在这个教程，我们将解释如何定义和初始化变量，源代码在一个专用的github仓库中。

## 创建变量

为了生成变量，类tf.Variable()会被使用。当我们定义变量时，我们基本上通过一个`tensor`，它的值会被标在图像上。基本上会发生以下的事情

> - 一个保存值的张量会被传递给图像
> - 通过使用 tf.assign，一个初始化器设定变量的值

一些随意定义的值如下：

```python
import tensorflow as tf
from tensorflow.python.framework import ops

#######################################
######## Defining Variables ###########
#######################################

# 用一些默认值创建了三个变量
weights = tf.Variable(tf.random_normal([2, 3], stddev=0.1),
                      name="weights")
biases = tf.Variable(tf.zeros([3]), name="biases")
custom_variable = tf.Variable(tf.zeros([3]), name="custom")

# 取得所有张量并把他们存到列表中
all_variables_list = ops.get_collection(ops.GraphKeys.GLOBAL_VARIABLES)
```

在上面的变量，`ops.getcollection`取得所有在图中定义的变量的列表。“name”关键字为每个在图中显示的变量定义了一个特殊的名字

## 初始化

变量们的`initializers`一定要在对模型做其他操作前执行。做个类比，我们可以考虑一个汽车启动器。如果不执行初始化器，变量也可译从保存的模型中恢复，这就像是检查点。变量可以初始化为全局，局部，或者是其他变量。我们接下来将研究不同的选项。

### 初始化具体变量

通过使用tf.variables_initializer，我们可以明确的命令TensorFlow仅仅初始化一个确定的变量。这个脚本像下面这样。

```python
# "variable_list_custom" is the list of variables that we want to initialize.
variable_list_custom = [weights, custom_variable]

# The initializer
init_custom_op = tf.variables_initializer(var_list=all_variables_list)
```

### 初始化全部变量

通过 tf.global_variables_initializer所有变量将被一次性初始化。必须在构建模型后执行此操作。脚本如下：

```python
# Method-1
# Add an op to initialize the variables.
init_all_op = tf.global_variables_initializer()

# Method-2
init_all_op = tf.variables_initializer(var_list=all_variables_list)
```

上述两种方法是相同的。我们仅仅用第二种方法来演示`tf.global_variables_initializer()` 与 `tf.variables_initializer`没什么不同，当你让所有变量作为输入参数的时候

### 用其他变量来初始化变量

新的变量可以用已经存在的其他变量的初始值初始化，初始值通过用initialized_value()来取得

初始化通过预定义的变量值

```python
# Create another variable with the same value as 'weights'.
WeightsNew = tf.Variable(weights.initialized_value(), name="WeightsNew")

# Now, the variable must be initialized.
init_WeightsNew_op = tf.variables_initializer(var_list=[WeightsNew])
```

像在上面的脚本中看到的那样，weightsNew通过weights的预定义值来初始化。

## 运行这个会话

我们目前为止所做的是定义初始化的操作并把他们放到图形中。为了真正初始化变量，定义的初始化操作必须在会话中运行

在会话中运行初始化

```
with tf.Session() as sess:
    # Run the initializer operation.
    sess.run(init_all_op)
    sess.run(init_custom_op)
    sess.run(init_WeightsNew_op)
```

每个初始化会在会话中分开运行。

## 总结

在这个教程里，我们走了一遍变量的定义和初始化。研究了全部，自定义和继承变量的初始化。在以后的帖子中，我们研究如何保存和恢复变量，恢复一个变量。恢复变量消除了初始化他们的必要性

