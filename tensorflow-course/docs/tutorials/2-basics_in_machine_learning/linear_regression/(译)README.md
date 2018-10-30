## 章节

- 介绍
- 描述整个过程
- 如何用代码实现
- 总结

## 用tensorflow做线性回归（肯定不如我的卡西欧算得快:smirk:）

这个教程是关于在tensorflow训练一个线性模型来适应数据。另外，你可以去看看这篇博客 [blog post](http://www.machinelearninguru.com/deep_learning/tensorflow/machine_learning_basics/linear_regresstion/linear_regression.html)

## 介绍

在机器学习和统计中，线性回归是一个变量之间的模型，需要有一个Y和至少一个独立的变量X。在线性回归中，线性关系会用一个预测函数建模，它的参数会用数据估计，这被称为线性模型。线性回归算法最大的有点是它用起来很简单，能直接的把数据转换到新的模型，并映射到数据到新的空间。在此文中，我们会介绍如何训练一个线性模型，如何展示这个模型。

## 描述整个过程

为了训练这个模型，tensorflow要循环遍历数据并找到理想的直线（因为我们有一个线性模型），使它适应数据。通过设计一个有恰当的代价函数的优化问题来估计x和y的关系。可以在[Stanford course CS 20SI](http://web.stanford.edu/class/cs20si/index.html): TensorFlow for Deep Learning Research.找到可用的数据集

## 如何用代码实现

这段代码用来加在必要的库和数据集

```python
# 数据文件由Stanford course CS 20SI: TensorFlow for Deep Learning Research.提供
# https://github.com/chiphuyen/tf-stanford-tutorials
DATA_FILE = "data/fire_theft.xls"

# 从.xls文件中读数据
book = xlrd.open_workbook(DATA_FILE, encoding_override="utf-8")
sheet = book.sheet_by_index(0)
data = np.asarray([sheet.row_values(i) for i in range(1, sheet.nrows)])
num_samples = sheet.nrows - 1

#######################
#######设置标志#########
#######################
tf.app.flags.DEFINE_integer(
    'num_epochs', 50, 'The number of epochs for training the model. Default=50')
# 将所有标志存在FLAGS中
FLAGS = tf.app.flags.FLAGS
```

然后定义和初始化必要的变量：

```python
# 创建权重和偏移
# 默认值会被设置为0.
W = tf.Variable(0.0, name="weights")
b = tf.Variable(0.0, name="bias")
```

然后我们定义必要的功能。不同的标签演示了函数定义：

```python
def inputs():
    """
    定义占位符.
    :返回:
            返回数据和标签持有者（什么鬼）.
    """
    X = tf.placeholder(tf.float32, name="X")
    Y = tf.placeholder(tf.float32, name="Y")
    return X,Y
```

```python
def inference(X):#原文中写掉了X
    """
    向前传递x
    :参数 X: 输入.
    :返回: X*W + b.
    """
    return X * W + b
```

```python
def loss(X, Y):
    """
    计算预测值和准确值之间的loss
    :param X: The input.
    :param Y: The label.
    :return: The loss over the samples.
    """

    # 做预估
    Y_predicted = inference(X)
    return tf.squared_difference(Y, Y_predicted)
```

接下来，我们开始循环遍历一批批数据，执行优化过程：

```
with tf.Session() as sess:

    # 初始化权重和偏移
    sess.run(tf.global_variables_initializer())

    # 取得输入张量
    X, Y = inputs()

    # Return the train loss and create the train_op.
    train_loss = loss(X, Y)
    train_op = train(train_loss)

    # Step 8: train the model
    for epoch_num in range(FLAGS.num_epochs): # run 100 epochs
        for x, y in data:
          train_op = train(train_loss)

          # Session runs train_op to minimize loss
          loss_value,_ = sess.run([train_loss,train_op], feed_dict={X: x, Y: y})

        # Displaying the loss per epoch.
        print('epoch %d, loss=%f' %(epoch_num+1, loss_value))

        # save the values of weight and bias
        wcoeff, bias = sess.run([W, b])
```

