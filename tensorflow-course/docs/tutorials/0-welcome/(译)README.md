# 欢迎来到tensorflow的世界

这个章节的教程仅仅是你进入tensorflow世界的开始

我们使用tensorboard来展示结果。tensorboard是TensorFlow的图形可视化工具，用谷歌的话来说：“你将用tensorflow做的计算——比如大数据量的深度学习网络——是复杂又令人迷茫的，为了让它更容易理解，调试，和优化TensorFlow程序，我们包括了一套可视化工具叫做TensorBoard”。本课程介绍了tensorboard的一个简单用法

**笔记：**

> - 摘要操作，Tensorboard及其优点的详细信息超出了本教程的范围，将在更高级的教程中介绍。

首先导入必要的包

```python
from __future__ import print_function
import tensorflow as tf
import os
```

如果我们想要用tensorboard，我们需要一个目录来储存信息（操作和相应的结果，如果用户想要的话）。tensorflow会把信息输出到``event files``中。event files。event files可以转化成可视数据，这样用户就可以评估结构和操作是否合理了。这个存储目录可以向下面这样定义：

```python
# 默认的储存路径在python文件相同的文件夹下
tf.app.flags.DEFINE_string(
'log_dir', os.path.dirname(os.path.abspath(__file__)) + '/logs',
'Directory where event logs are written to.')

# 在flages结构体中储存所有元素
FLAGS = tf.app.flags.FLAGS
```

``os.path.dirname(os.path.abspath(__file__))``取得当前的目录名。``tf.app.flags.FLAGS``指向所有定义的标志，用FLAGS来引用它。于是现在标志可以用``FLAGS.标志名``来访问了。

为了方便，仅在绝对目录下工作是很有用的。通过用下面的脚本：

```python
# 用户会被提示输入绝对路径
# os.path.expanduser 用于将'〜'符号转换为相应的路径指示符。
# 	例如：“~/logs”相当于"home/username/logs"
if not os.path.isabs(os.path.expanduser(FLAGS.log_dir)):
    raise ValueError('You must assign absolute path for --log_dir')
```

## 开始

一些句子可以被这样定义：

```python
# Defining some sentence!
welcome = tf.constant('Welcome to TensorFlow world!')
```

## 运行实验

``session``是运行操作的环境，它可以像这样执行：

```python
# Run the session
with tf.Session() as sess:
    writer = tf.summary.FileWriter(os.path.expanduser(FLAGS.log_dir), sess.graph)
    print("output: ", sess.run(welcome))

# Closing the writer.
writer.close()
sess.close()
```

定义``tf.summar.FileWriter``将摘要写入事件文件。在任何``tensor``中为了求出值，命令：sess.run（）必须被使用，否则操作不会被执行，最后调用``writer.close()``，摘要的writer会被关闭。