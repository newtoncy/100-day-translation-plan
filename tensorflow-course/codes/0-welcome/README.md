# 欢迎来到TensorFlow的世界

这个文档致力于说明如何运行这个教程的python脚本

## 测试TensorFlow的环境

``警告：``如果TensorFlow安装在任何环境（虚拟环境，……），它必须先被激活才能运行。所以首先确定tensorFlow在当前环境下是可用的，使用以下脚本

```shell
cd code/
python TensorFlow_Test.py
```



## 如何在终端中运行

请切到code/路径，然后用以下这种常用形式运行python脚本

```shell
python [python_code_file.py] --log_dir='absolute/path/to/log_dir'
```

举例来说，这个代码应该像下面这样执行

```shell
python 1-welcome.py --log_dir='~/log_dir'
```

``--log_dir``标志是为了提供一个“事件文件”存放的路径（为了在Tensorboard中可视化）。这个标志不是必须的，因为在源文件中它是有默认值的，向下面这样：

```python
tf.app.flags.DEFINE_string(
'log_dir', os.path.dirname(os.path.abspath(__file__)) + '/logs',
'Directory where event logs are written to.')
```

## 如何在IDE中打代码

因为代码是随时可用的，所以只要TensorFlow可以被IDE调用（pycharm，spyder）这个代码就可以成功执行

## 如何用Tensorboard

Teensorboard是TensorFlow提供的图形可视化工具，用谷歌的话来说：“你将用tensorflow做的计算——比如大数据量的深度学习网络——是复杂又令人迷茫的，为了让它更容易理解，调试，和优化TensorFlow程序，我们包括了一套可视化工具叫做TensorBoard”。

TensorBoard可以被这样在终端中运行：

```shell
tensorboard --logdir="absolute/path/to/log_dir"
```

**接下来去翻译对应的ducument文件夹了**