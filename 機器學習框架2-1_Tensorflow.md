# 機器學習框架2-1_Tensorflow

[toc]
<!-- toc --> 


# API Reference

- [All symbols in TensorFlow  |  TensorFlow](https://www.tensorflow.org/api_docs/python/)



- [tf.matmul  |  TensorFlow](https://www.tensorflow.org/versions/master/api_docs/python/tf/matmul)
    Multiplies matrix `a` by matrix `b`, producing `a` \* `b`.

- [tf.multiply  |  TensorFlow](https://www.tensorflow.org/versions/master/api_docs/python/tf/multiply)
    Returns x * y element-wise.

- [tf.trainable_variables  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/trainable_variables)
    Returns all variables created with `trainable=True`.

- [tf.Session.close()  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/Session#close)
    Closes this session.
    Calling this method frees all resources associated with the session.

- [tf.Dimension.value  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/Dimension#value)
    The value of this dimension, or None if it is unknown.

- [tf.argmax  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/argmax)
    Returns the index with the largest value across axes of a tensor. (deprecated arguments)

- [tf.truncated_normal  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/truncated_normal)
    Outputs random values from a truncated normal distribution.

- [tf.identity  |  TensorFlow](https://www.tensorflow.org/versions/r1.2/api_docs/python/tf/identity)
    Return a tensor with the same shape and contents as the input tensor or value.
    
- [tf.nn.dropout  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/dropout)
    Computes dropout.
    With probability `keep_prob`, outputs the input element scaled up by `1 / keep_prob`, otherwise outputs `0`. The scaling is so that the expected sum is unchanged.

    

- [tf.Session  |  TensorFlow](https://www.tensorflow.org/versions/r1.1/api_docs/python/tf/Session#run)
    - __run__
        Runs operations and evaluates tensors in `fetches`.


## Graph

### List of tensor names in graph

- [python - List of tensor names in graph in Tensorflow - Stack Overflow](https://stackoverflow.com/questions/35336648/list-of-tensor-names-in-graph-in-tensorflow/35337827)

    > To answer your first question, `sess.graph.get_operations()` gives you a list of operations. For an op, `op.name` gives you the name and `op.values()` gives you a list of tensors it produces (in the inception-v3 model, all tensor names are the op name with a ":0" appended to it, so `pool_3:0` is the tensor produced by the final pooling op.)
    > 

- [python - In Tensorflow, get the names of all the Tensors in a graph - Stack Overflow](https://stackoverflow.com/questions/36883949/in-tensorflow-get-the-names-of-all-the-tensors-in-a-graph)

    > You can do
    > 
    > ```
    > [n.name for n in tf.get_default_graph().as_graph_def().node]
    > ```
    > 
    > Also, if you are prototyping in an IPython notebook, you can show the graph directly in notebook, see `show_graph` function in Alexander's Deep Dream [notebook](http://nbviewer.jupyter.org/github/tensorflow/tensorflow/blob/master/tensorflow/examples/tutorials/deepdream/deepdream.ipynb)

### embed TensorBoard graph visualizations into Jupyter notebooks

- [DeepDreaming with TensorFlow](https://nbviewer.jupyter.org/github/tensorflow/tensorflow/blob/master/tensorflow/examples/tutorials/deepdream/deepdream.ipynb#deepdream)

    {% raw %}
    ```python
    from IPython.display import display, HTML

    def show_graph(graph_def, max_const_size=32):
        """Visualize TensorFlow graph."""
        if hasattr(graph_def, 'as_graph_def'):
            graph_def = graph_def.as_graph_def()
        strip_def = strip_consts(graph_def, max_const_size=max_const_size)
        code = """
            <script>
              function load() {{
                document.getElementById("{id}").pbtxt = {data};
              }}
            </script>
            <link rel="import" href="https://tensorboard.appspot.com/tf-graph-basic.build.html" onload=load()>
            <div style="height:600px">
              <tf-graph-basic id="{id}"></tf-graph-basic>
            </div>
        """.format(data=repr(str(strip_def)), id='graph'+str(np.random.rand()))

        iframe = """
            <iframe seamless style="width:800px;height:620px;border:0" srcdoc="{}"></iframe>
        """.format(code.replace('"', '&quot;'))
        display(HTML(iframe))


    # Visualizing the network graph. Be sure expand the "mixed" nodes to see their 
    # internal structure. We are going to visualize "Conv2D" nodes.
    tmp_def = rename_nodes(graph_def, lambda s:"/".join(s.split('_',1)))
    show_graph(tmp_def)
    ```
    {% endraw %}



- [tf.GraphKeys  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/GraphKeys)

    > Standard names to use for graph collections.
    > 
    > The standard library uses various well-known names to collect and retrieve values associated with a graph. For example, the `tf.Optimizer` subclasses default to optimizing the variables collected under `tf.GraphKeys.TRAINABLE_VARIABLES` if none is specified, but it is also possible to pass an explicit list of variables.

- [tf.control_dependencies  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/control_dependencies)

    > Returns:
    > 
    > A context manager that specifies control dependencies for all operations constructed within the context.

- [python - TensorFlow saving into/loading a graph from a file - Stack Overflow](https://stackoverflow.com/questions/38947658/tensorflow-saving-into-loading-a-graph-from-a-file)

    > There are many ways to approach the problem of saving a model in TensorFlow, which can make it a bit confusing. Taking each of your sub-questions in turn:
    > 
    > 1.  The checkpoint files (produced e.g. by calling [`saver.save()`](https://www.tensorflow.org/versions/r0.10/api_docs/python/state_ops.html#Saver.save) on a [`tf.train.Saver`](https://www.tensorflow.org/versions/r0.10/api_docs/python/state_ops.html#Saver) object) contain only the weights, and any other variables defined in the same program. To use them in another program, you must re-create the associated graph structure (e.g. by running code to build it again, or calling [`tf.import_graph_def()`](https://www.tensorflow.org/versions/r0.10/api_docs/python/framework.html#import_graph_def)), which tells TensorFlow what to do with those weights. Note that calling `saver.save()` also produces a file containing a [`MetaGraphDef`](https://www.tensorflow.org/versions/r0.10/how_tos/meta_graph/index.html), which contains a graph and details of how to associate the weights from a checkpoint with that graph. See [the tutorial](https://www.tensorflow.org/versions/r0.10/how_tos/meta_graph/index.html) for more details.
    >     
    > 2.  [`tf.train.write_graph()`](https://www.tensorflow.org/versions/r0.10/api_docs/python/train.html#write_graph) only writes the graph structure; not the weights.
    >     
    > 3.  Bazel is unrelated to reading or writing TensorFlow graphs. (Perhaps I misunderstand your question: feel free to clarify it in a comment.)
    >     
    > 4.  A frozen graph can be loaded using [`tf.import_graph_def()`](https://www.tensorflow.org/versions/r0.10/api_docs/python/framework.html#import_graph_def). In this case, the weights are (typically) embedded in the graph, so you don't need to load a separate checkpoint.
    >     
    > 5.  The main change would be to update the names of the tensor(s) that are fed into the model, and the names of the tensor(s) that are fetched from the model. In the TensorFlow Android demo, this would correspond to the `inputName` and `outputName` strings that are passed to [`TensorFlowClassifier.initializeTensorFlow()`](https://github.com/tensorflow/tensorflow/blob/d67ce6c449fabb3bebccd85815d9d291f114e6e4/tensorflow/examples/android/src/org/tensorflow/demo/TensorFlowClassifier.java#L34).
    >     
    > 6.  The `GraphDef` is the program structure, which typically does not change through the training process. The checkpoint is a snapshot of the state of a training process, which typically changes at every step of the training process. As a result, TensorFlow uses different storage formats for these types of data, and the low-level API provides different ways to save and load them. Higher-level libraries, such as the [`MetaGraphDef`](https://www.tensorflow.org/versions/r0.10/how_tos/meta_graph/index.html) libraries, [Keras](https://keras.io/getting-started/faq/#how-can-i-save-a-keras-model), and [skflow](https://github.com/tensorflow/skflow#saving--restoring-models) build on these mechanisms to provide more convenient ways to save and restore an entire model.
    > 


## Scope/Variable

### tf.Variable

- [tf.Variable  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/Variable)



### tf.get_variable

- [tf.get_variable  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/get_variable)

    >Gets an existing variable with these parameters or create a new one.

### tf.name_scope()/tf.variable_scope()

- [(2 封私信 / 83 条消息)tensorflow里面name_scope, variable_scope等如何理解？ - 知乎](https://www.zhihu.com/question/54513728)

    > 主要是因为 变量共享 的需求。\
    > 而这就不得不谈到tf. get_variable()了。因为如果使用Variable 的话每次都会新建变量，但是大多数时候我们是希望一些变量重用的，所以就用到了get_variable()。它会去搜索变量名，然后没有就新建，有就直接用。\
    > 既然用到变量名了，就涉及到了名字域的概念。通过不同的域来区别变量名，毕竟让我们给所有变量都直接取不同名字还是有点辛苦的。所以为什么会有scope 的概念。\
    > name_scope 作用于操作，variable_scope 可以通过设置reuse 标志以及初始化方式来影响域下的变量。\
    > 当然对我们而言还有个更直观的感受就是：在tensorboard 里可视化的时候用名字域进行封装后会更清晰
    > 
    > ---
    > 
    > tf.name_scope() 主要用在 tensorboard 區分模塊；tf.variable_scope() 用於共享變數，在同一個variable_scope 底下的變數可以重用，重用前呼叫 scope.reuse_variables() 開啟共用，使用 tf.get_variable() 取得共用的變數 [name=Ya-Lun Li]

- [scope 命名方法 - Tensorflow | 莫烦Python](https://morvanzhou.github.io/tutorials/machine-learning/tensorflow/5-12-scope/)

    > 如果想要达到重复利用变量的效果, 我们就要使用 `tf.variable_scope()`, 并搭配 `tf.get_variable()` 这种方式产生和提取变量. 不像 `tf.Variable()` 每次都会产生新的变量, `tf.get_variable()` 如果遇到了同样名字的变量时, 它会单纯的提取这个同样名字的变量(避免产生新变量). 而在重复使用的时候, 一定要在代码中强调 `scope.reuse_variables()`, 否则系统将会报错, 以为你只是单纯的不小心重复使用到了一个变量.
    > 
    > 
    > ```python
    > with tf.variable_scope("a_variable_scope") as scope:
    >     initializer = tf.constant_initializer(value=3)
    >     var3 = tf.get_variable(name='var3', shape=[1], dtype=tf.float32, initializer=initializer)
    >     scope.reuse_variables()
    >     var3_reuse = tf.get_variable(name='var3',)
    >     var4 = tf.Variable(name='var4', initial_value=[4], dtype=tf.float32)
    >     var4_reuse = tf.Variable(name='var4', initial_value=[4], dtype=tf.float32)
    > 
    > with tf.Session() as sess:
    >     sess.run(tf.global_variables_initializer())
    >     print(var3.name)            # a_variable_scope/var3:0
    >     print(sess.run(var3))       # [ 3.]
    >     print(var3_reuse.name)      # a_variable_scope/var3:0
    >     print(sess.run(var3_reuse)) # [ 3.]
    >     print(var4.name)            # a_variable_scope/var4:0
    >     print(sess.run(var4))       # [ 4.]
    >     print(var4_reuse.name)      # a_variable_scope/var4_1:0
    >     print(sess.run(var4_reuse)) # [ 4.]
    > 
    > ```
    > 


## Layers

- [Module: tf.layers  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers)
    - [tf.layers.conv2d  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/conv2d)
    - [tf.layers.max_pooling2d  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/max_pooling2d)
    - [tf.layers.flatten  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/flatten)
    - [tf.layers.dense  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/dense)

### tf.layers.Flatten

- [tf.layers.Flatten  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/Flatten)

### tf.nn.dropout

- [tf.nn.dropout  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/dropout)

- [谈谈Tensorflow的dropout - 简书](https://www.jianshu.com/p/c9f66bc8f96c)

    > 使输入tensor中某些元素变为0，其它没变0的元素变为原来的1/keep_prob大小！

    > 个人总结：个人感觉除非是大型网络，才采用dropout，不然我感觉自己在一些小型网络上，训练好像很是不爽。之前搞一个比较小的网络，搞人脸特征点定位的时候，因为训练数据不够，怕过拟合，于是就采用dropout，最后感觉好像训练速度好慢，从此就对dropout有了偏见，感觉训练过程一直在波动，很是不爽。

- [tensorflow: what's the difference between tf.nn.dropout and tf.layers.dropout - Stack Overflow](https://stackoverflow.com/questions/44395547/tensorflow-whats-the-difference-between-tf-nn-dropout-and-tf-layers-dropout)

    > A quick glance through [tensorflow/python/layers/core.py](https://github.com/tensorflow/tensorflow/blob/r1.1/tensorflow/python/layers/core.py) and [tensorflow/python/ops/nn_ops.py](https://github.com/tensorflow/tensorflow/blob/r1.1/tensorflow/python/ops/nn_ops.py) reveals that `tf.layers.dropout` is a wrapper for `tf.nn.dropout`.
    > 
    > The only differences in the two functions are:
    > 
    > 1.  The `tf.nn.dropout` has parameter `keep_prob`: "Probability that each element is kept"\
    >     `tf.layers.dropout` has parameter `rate`: "The dropout rate"\
    >     Thus, `keep_prob = 1 - rate` as defined [here](https://github.com/tensorflow/tensorflow/blob/r1.1/tensorflow/python/layers/core.py#L256)
    > 2.  The `tf.layers.dropout` has `training` parameter: "Whether to return the output in training mode (apply dropout) or in inference mode (return the input untouched)."




## Optimizer

- [tf.train.RMSPropOptimizer  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/train/RMSPropOptimizer)
    - __minimize__
      Add operations to minimize `loss` by updating `var_list`.







## weight initialize


### tf.truncated_normal / tf.random_normal

- [tf.random.truncated_normal  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/random/truncated_normal)

- [math - What is difference between tf.truncated_normal and tf.random_normal? - Stack Overflow](https://stackoverflow.com/questions/41704484/what-is-difference-between-tf-truncated-normal-and-tf-random-normal)

    > The [documentation](https://www.tensorflow.org/api_docs/python/tf/truncated_normal) says it all: For truncated normal distribution:
    > 
    > > The generated values follow a normal distribution with specified mean and standard deviation, except that values whose magnitude is more than 2 standard deviations from the mean are dropped and re-picked.
    > 
    > Most probably it is easy to understand the difference by plotting the graph for yourself (%magic is because I use jupyter notebook):
    > 
    > ```
    > import tensorflow as tf
    > import matplotlib.pyplot as plt
    > 
    > %matplotlib inline
    > 
    > n = 500000
    > A = tf.truncated_normal((n,))
    > B = tf.random_normal((n,))
    > with tf.Session() as sess:
    >     a, b = sess.run([A, B])
    > 
    > ```
    > 
    > And now
    > 
    > ```
    > plt.hist(a, 100, (-4.2, 4.2));
    > plt.hist(b, 100, (-4.2, 4.2));
    > 
    > ```
    > 
    > [![enter image description here](https://i.stack.imgur.com/fXqXs.png)](https://i.stack.imgur.com/fXqXs.png)
    > 
    > * * * * *
    > 
    > The point for using truncated normal is to overcome saturation of tome functions like sigmoid (where if the value is too big/small, the neuron stops learning).


- [backpropagation - What is the benefit of the truncated normal distribution in initializing weights in a neural network? - Cross Validated](https://stats.stackexchange.com/questions/228670/what-is-the-benefit-of-the-truncated-normal-distribution-in-initializing-weights)

    > I think its about saturation of the neurons. Think about you have an activation function like sigmoid.
    > 
    > [![enter image description here](https://i.stack.imgur.com/5VmI7.png)](https://i.stack.imgur.com/5VmI7.png)
    > 
    > If your weight val gets value >= 2 or <=-2 your neuron will not learn. So, if you truncate your normal distribution you will not have this issue(at least from the initialization) based on your variance. I think thats why, its better to use truncated normal in general.
    > 

### tf.constant_initializer()/tf.random_normal_initializer()

- [tf.constant  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/constant)



- [tensorflow 1.0 学习：参数初始化（initializer) - denny402 - 博客园](https://www.cnblogs.com/denny402/p/6932956.html)

    > CNN中最重要的就是参数了，包括W,b。 我们训练CNN的最终目的就是得到最好的参数，使得目标函数取得最小值。参数的初始化也同样重要，因此微调受到很多人的重视，那么tf提供了哪些初始化参数的方法呢，我们能不能自己进行初始化呢？
    > 
    > 所有的初始化方法都定义在[`tensorflow/python/ops/init_ops.py`](https://www.github.com/tensorflow/tensorflow/blob/r1.1/tensorflow/python/ops/init_ops.py)
    > 
    > **1、`tf.constant_initializer()`**
    > 
    > 也可以简写为tf.Constant()
    > 
    > 初始化为常数，这个非常有用，通常偏置项就是用它初始化的。
    > 
    > 由它衍生出的两个初始化方法：
    > 
    > a、 tf.zeros_initializer()， 也可以简写为tf.Zeros()
    > 
    > b、tf.ones_initializer(), 也可以简写为tf.Ones()
    > 
    > 例：在卷积层中，将偏置项b初始化为0，则有多种写法：
    > 
    > ```
    > conv1 = tf.layers.conv2d(batch_images,
    >                          filters=64,
    >                          kernel_size=7,
    >                          strides=2,
    >                          activation=tf.nn.relu,
    >                          kernel_initializer=tf.TruncatedNormal(stddev=0.01)
    >                          bias_initializer=tf.Constant(0),
    >                         )
    > ```
    > 
    > 
    > 或者：
    > ```
    > bias_initializer=tf.constant_initializer(0)
    > ```
    > 或者：
    > ```
    > bias_initializer=tf.zeros_initializer()
    > ```
    > 或者：
    > ```
    > bias_initializer=tf.Zeros()
    > ```
    > 
    > 例：如何将W初始化成拉普拉斯算子？
    > ```
    > value = [1, 1, 1, 1, -8, 1, 1, 1，1]
    > init = tf.constant_initializer(value)
    > W= tf.get_variable('W', shape=[3, 3], initializer=init)
    > ```
    > **2、tf.truncated_normal_initializer()**
    > 
    > 或者简写为tf.TruncatedNormal()
    > 
    > 生成截断正态分布的随机数，这个初始化方法好像在tf中用得比较多。
    > 
    > 它有四个参数（mean=0.0, stddev=1.0, seed=None, dtype=dtypes.float32)，分别用于指定均值、标准差、随机数种子和随机数的数据类型，一般只需要设置stddev这一个参数就可以了。
    > 
    > 例：
    > 
    > 
    > ```
    > conv1 = tf.layers.conv2d(batch_images,
    >                          filters=64,
    >                          kernel_size=7,
    >                          strides=2,
    >                          activation=tf.nn.relu,
    >                          kernel_initializer=tf.TruncatedNormal(stddev=0.01)
    >                          bias_initializer=tf.Constant(0),
    >                         )
    > ```
    > 
    > 
    > 或者：
    > 
    > 
    > ```
    > conv1 = tf.layers.conv2d(batch_images,
    >                          filters=64,
    >                          kernel_size=7,
    >                          strides=2,
    >                          activation=tf.nn.relu,
    >                          kernel_initializer=tf.truncated_normal_initializer(stddev=0.01)
    >                          bias_initializer=tf.zero_initializer(),
    >                         )
    > ```
    > 
    > 
    > **3、tf.random_normal_initializer()**
    > 
    > 可简写为 tf.RandomNormal()
    > 
    > 生成标准正态分布的随机数，参数和truncated_normal_initializer一样。
    > 
    > **4、random_uniform_initializer = RandomUniform()**
    > 
    > 可简写为tf.RandomUniform()
    > 
    > 生成均匀分布的随机数，参数有四个（minval=0, maxval=None, seed=None, dtype=dtypes.float32)，分别用于指定最小值，最大值，随机数种子和类型。
    > 
    > **5、tf.uniform_unit_scaling_initializer()**
    > 
    > 可简写为tf.UniformUnitScaling()
    > 
    > 和均匀分布差不多，只是这个初始化方法不需要指定最小最大值，是通过计算出来的。参数为（factor=1.0, seed=None, dtype=dtypes.float32)
    > ```
    > max_val = math.sqrt(3 / input_size) * factor
    > ```
    > 这里的input_size是指输入数据的维数，假设输入为x, 运算为x * W，则input_size= `W.shape[0]`
    > 
    > 它的分布区间为[ -max_val, max_val]
    > 
    > **6、tf.variance_scaling_initializer()**
    > 
    > 可简写为tf.VarianceScaling()
    > 
    > 参数为（scale=1.0,mode="fan_in",distribution="normal",seed=None，dtype=dtypes.float32)
    > 
    > scale: 缩放尺度（正浮点数）
    > 
    > mode:  "fan_in", "fan_out", "fan_avg"中的一个，用于计算标准差stddev的值。
    > 
    > distribution：分布类型，"normal"或"uniform"中的一个。
    > 
    > 当 distribution="normal" 的时候，生成truncated normal   distribution（截断正态分布） 的随机数，其中stddev = sqrt(scale / n) ，n的计算与mode参数有关。
    > 
    >     如果mode = "fan_in"， n为输入单元的结点数；
    > 
    >     如果mode = "fan_out"，n为输出单元的结点数；
    > 
    >     如果mode = "fan_avg",n为输入和输出单元结点数的平均值。
    > 
    > 当distribution="uniform"的时候 ，生成均匀分布的随机数，假设分布区间为[-limit, limit]，则
    > 
    >       limit = sqrt(3 * scale / n)
    > 
    > **7、tf.orthogonal_initializer()**
    > 
    > 简写为tf.Orthogonal()
    > 
    > 生成正交矩阵的随机数。
    > 
    > 当需要生成的参数是2维时，这个正交矩阵是由均匀分布的随机数矩阵经过SVD分解而来。
    > 
    > **8、tf.glorot_uniform_initializer()**
    > 
    > 也称之为Xavier uniform initializer，由一个均匀分布（uniform distribution)来初始化数据。
    > 
    > 假设均匀分布的区间是[-limit, limit],则
    > ```
    > limit=sqrt(6 / (fan_in + fan_out))
    > ```
    > 其中的fan_in和fan_out分别表示输入单元的结点数和输出单元的结点数。
    > 
    > **9、glorot_normal_initializer（）**
    > 
    > 也称之为 Xavier normal initializer. 由一个 truncated normal distribution来初始化数据.
    > ```
    > stddev = sqrt(2 / (fan_in + fan_out))
    > ```
    > 其中的fan_in和fan_out分别表示输入单元的结点数和输出单元的结点数。
    > 

### tf.random.uniform

- [tf.random.uniform  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/random/uniform)




## loss function

### l2_loss

- [tf.nn.l2_loss  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/l2_loss)



### logit

- [neural network - What is the meaning of the word logits in TensorFlow? - Stack Overflow](https://stackoverflow.com/questions/41455101/what-is-the-meaning-of-the-word-logits-in-tensorflow)

    > **Logit** is a function that maps probabilities `[0, 1]` to `[-inf, +inf]`.
    > 
    > **Softmax** is a function that maps `[-inf, +inf]` to `[0, 1]` similar as Sigmoid. But Softmax also normalizes the sum of the values(output vector) to be 1.
    > 
    > **Tensorflow "with logit"**: It means that you are applying a softmax function to logit numbers to normalize it. The input_vector/logit is not normalized and can scale from \[-inf, inf\].
    > 
    > This normalization is used for multiclass classification problems. And for multilabel classification problems sigmoid normalization is used i.e. `tf.nn.sigmoid_cross_entropy_with_logits`


    > [Logit](https://en.wikipedia.org/wiki/Logit) is a function that maps probabilities (`[0, 1]`) to R (`(-inf, inf)`)
    > 
    > [![enter image description here](https://i.stack.imgur.com/zto5q.png)](https://i.stack.imgur.com/zto5q.png)
    > 
    > Probability of 0.5 corresponds to a logit of 0. Negative logit correspond to probabilities less than 0.5, positive to > 0.5.
    > 

### What's the difference between softmax and softmax_cross_entropy_with_logits

- [python - What's the difference between softmax and softmax_cross_entropy_with_logits? - Stack Overflow](https://stackoverflow.com/questions/34240703/whats-the-difference-between-softmax-and-softmax-cross-entropy-with-logits)

    > Logits simply means that the function operates on the unscaled output of earlier layers and that the relative scale to understand the units is linear. It means, in particular, the sum of the inputs may not equal 1, that the values are _not_ probabilities (you might have an input of 5).
    > 
    > `tf.nn.softmax` produces just the result of applying the [softmax function](https://en.wikipedia.org/wiki/Softmax_function) to an input tensor. The softmax "squishes" the inputs so that sum(input) = 1; it's a way of normalizing. The shape of output of a softmax is the same as the input - it just normalizes the values. The outputs of softmax _can_ be interpreted as probabilities.
    > 
    > ```
    > a = tf.constant(np.array([[.1, .3, .5, .9]]))
    > print s.run(tf.nn.softmax(a))
    > [[ 0.16838508  0.205666    0.25120102  0.37474789]]
    > ```
    > 
    > In contrast, `tf.nn.softmax_cross_entropy_with_logits` computes the cross entropy of the result after applying the softmax function (but it does it all together in a more mathematically careful way). It's similar to the result of:
    > 
    > ```
    > sm = tf.nn.softmax(x)
    > ce = cross_entropy(sm)
    > ```
    > 
    > If you want to do optimization to minimize the cross entropy, AND you're softmaxing after your last layer, you should use `tf.nn.softmax_cross_entropy_with_logits` instead of doing it yourself, because it covers numerically unstable corner cases in the mathematically right way. Otherwise, you'll end up hacking it by adding little epsilons here and there.



### sigmoid_cross_entropy_with_logits, softmax_cross_entropy_with_logits, sparse_softmax_cross_entropy_with_logits

- [TF里几种loss和注意事项 - 知乎](https://zhuanlan.zhihu.com/p/33560183)

    > **准备1、** 先说一下什么是logit，logit函数定义为：
    > 
    > ![L(p)=ln\frac{p}{1-p}](https://www.zhihu.com/equation?tex=L%28p%29%3Dln%5Cfrac%7Bp%7D%7B1-p%7D)
    > 
    > 是一种将取值范围在\[0,1\]内的概率映射到实数域\[-inf,inf\]的函数，如果p=0.5，函数值为0；p<0.5，函数值为负；p>0.5，函数值为正。
    > 
    > **相对地** ，softmax和sigmoid则都是将\[-inf,inf\]映射到\[0,1\]的函数。
    > 
    > 在tensorflow里的"logits"指的其实是，该方法是在**logit数值** 上使用softmax或者sigmoid来进行normalization的，也暗示用户**不要**将网络输出进行sigmoid或者softmax，这些过程可以在函数内部更高效地计算。
    > 
    > **准备2、** 独立和互斥
    > 
    > 有事件A和B
    > 
    > 独立：P(AnB) = P(A) * P(B)
    > 
    > 互斥：P(AUB) = P(A) + P(B), P(AnB) = 0
    > 
    > **准备3、** cross entropy loss + softmax + sigmoid
    > 
    > 请看之前的文章，[复习：常见的损失函数](https://zhuanlan.zhihu.com/p/33542937)
    
    > - [tf.nn.sigmoid_cross_entropy_with_logits  |  TensorFlow](https://www.tensorflow.org/versions/r1.4/api_docs/python/tf/nn/sigmoid_cross_entropy_with_logits)
    > 
    >     计算网络输出logits和标签labels的sigmoid cross entropy loss，衡量独立不互斥离散分类任务的误差，说独立不互斥离散分类任务是因为，在这些任务中类与类之间是独立但是不互斥的，拿多分类任务中的多目标检测来举例子，一张图中可以有各种instance，比如有一只狗和一只猫。对于一个总共有五类的多目标检测任务，假如网络的输出层有5个节点，label的形式是[1,1,0,0,1]这种，1表示该图片有某种instance，0表示没有。那么，每个instance在这张图中有没有这显然是独立事件，但是多个instance可以存在一张图中，这就说明事件们并不是互斥的。所以我们可以直接将网络的输出用作该方法的logits输入，从而进行输出与label的cross entropy loss。
    > 
    >     更加直白的来说，这种网络的输入不需要进行one hot处理，网络输出即是函数logits参数的输入。
    > 
    >     剖开函数内部，因为labels和logits的形状都是[batch_size, num_classes]，那么如何计算他们的交叉熵呢，毕竟它们都不是有效的概率分布（一个batch内输出结果经过sigmoid后和不为1）。其实loss的计算是element-wise的，方法返回的loss的形状和labels是相同的，也是[batch_size, num_classes]，再调用reduce_mean方法计算batch内的平均loss。所以这里的cross entropy其实是一种class-wise的cross entropy，每一个class是否存在都是一个事件，对每一个事件都求cross entropy loss，再对所有的求平均，作为最终的loss。
    > 
    > - [tf.nn.softmax_cross_entropy_with_logits  |  TensorFlow](https://www.tensorflow.org/versions/r1.4/api_docs/python/tf/nn/softmax_cross_entropy_with_logits)
    > 
    >     计算网络输出logits和标签labels的softmax cross entropy loss，衡量独立互斥离散分类任务的误差，说独立互斥离散分类任务是因为，在这些任务中类与类之间是独立而且互斥的，比如VOC classification、Imagenet、CIFAR-10甚至MNIST，这些都是多分类任务，但是一张图就对应着一个类，class在图片中是否存在是独立的，并且一张图中只能有一个class，所以是独立且互斥事件。
    > 
    >     该函数要求每一个label都是一个有效的概率分布，对于Imagenet中的ILSVRC2012这种任务，那么label应该就对应一个one hot编码，ILSVRC2012提供的数据集中一共有1000个类，那么label就应该是一个1x1000的vector，形式为[0,0,...,1,0,....0]，1000个元素中有且只有一个元素是1，其余都是0。
    > 
    >     这样要求的原因很简单，因为网络的输出要进行softmax，得到的就是一个有效的概率分布，这里不同与sigmoid，因为sigmoid并没有保证网络所有的输出经过sigmoid后和为1，不是一个有效的概率分布。
    > 
    >     有了labels和softmax后的logits，就可以计算交叉熵损失了，最后得到的是形状为[batch_size, 1]的loss。
    > 
    > - [tf.nn.sparse_softmax_cross_entropy_with_logits  |  TensorFlow](https://www.tensorflow.org/versions/r1.4/api_docs/python/tf/nn/sparse_softmax_cross_entropy_with_logits)
    > 
    >     这个版本是tf.nn.softmax_cross_entropy_with_logits的易用版本，这个版本的logits的形状依然是[batch_size, num_classes]，但是labels的形状是[batch_size, 1]，每个label的取值是从[0, num_classes)的离散值，这也更加符合我们的使用习惯，是哪一类就标哪个类对应的label。
    > 
    >     如果已经对label进行了one hot编码，则可以直接使用tf.nn.softmax_cross_entropy_with_logits。




- [[tensorflow损失函数系列]sigmoid_cross_entropy_with_logits - 遗世独立的乌托邦 - CSDN博客](https://blog.csdn.net/u013555719/article/details/77601385)

    > ### 推导过程
    > 
    > 设`x = logits`, `z = labels`.\
    > logistic loss 计算式为:\
    > 其中交叉熵(cross entripy)基本函数式
    > 
    > ```
    > z * -log(sigmoid(x)) + (1 - z) * -log(1 - sigmoid(x))
    > = z * -log(1 / (1 + exp(-x))) + (1 - z) * -log(exp(-x) / (1 + exp(-x)))
    > = z * log(1 + exp(-x)) + (1 - z) * (-log(exp(-x)) + log(1 + exp(-x)))
    > = z * log(1 + exp(-x)) + (1 - z) * (x + log(1 + exp(-x))
    > = (1 - z) * x + log(1 + exp(-x))
    > = x - x * z + log(1 + exp(-x))
    > ```
    > 
    > 对于x<0时,为了避免计算exp(-x)时溢出,我们使用以下这种形式表示
    > 
    > ```
    > x - x * z + log(1 + exp(-x))
    > = log(exp(x)) - x * z + log(1 + exp(-x))
    > = - x * z + log(1 + exp(x))
    > ```
    > 
    > 综合x>0和x<0的情况,我们使用以下函数式
    > ```
    > max(x,0)-x∗z+log(1+exp(-abs(x)))
    > ```




## Tensor

### tf.stack() (old: tf.pack())

- [tf.stack  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/stack)

- [TF1.2.1 tf.stack() 替代 tf.pack() - 简书](https://www.jianshu.com/p/a745119b32b4)

    > tf.stack(values , name=''pack'')    旧：tf.pack(values , name=""pack"")
    > 
    > 说明：该函数使用方法无变化，仅仅名称变化。
    > 
    > 用法：values是一个tensor张量，name指示了名称。 该函数实现rank=K的tensor**打包**成rank=k+1的tensor。
    > 
    > 举例： a = tf.constant([1,2,3])   b=tf.constant([4,5,6])
    > 
    > sess.run([a,b]) 输出：[array([1, 2, 3]), array([4, 5, 6])]
    > 
    > sess.run(tf.stack([a,b],name='rank'))  输出：[[1,2,3],[4,5,6]]
    > 

### tf.reshape() of a tensor with an unknown dimension (None) (tf.shape())

- [tf.reshape  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/reshape)

- [tf.reshape() of a tensor with an unknown dimension (None) does not seem to work · Issue #7253 · tensorflow/tensorflow](https://github.com/tensorflow/tensorflow/issues/7253)

    > `tf.shape(x)[0]` gives a scalar tensor with the variable batch size. Try passing it to reshape.
    > 


### How does tf.reshape() work

- [python - How does tf.reshape() work internally ? - Stack Overflow](https://stackoverflow.com/questions/51706848/how-does-tf-reshape-work-internally)

    > Tensor before and after `tf.reshape` have the **same flatten order**.
    > 
    > In tensorflow runtime, a Tensor is consists of raw data(byte array), shape, and dtype, `tf.reshape` only change shape, with raw data and dtype not changed. `-1` or `None` in `tf.reshape` means that thsi value can be calculated.
    > 
    > For example,
    > 
    > ```
    > # a tensor with 6 elements, with shape [3,2]
    > a = tf.constant([[1,2], [3,4], [5,6]])
    > # reshape tensor to [2, 3, 1], 2 is calculated by 6/3/1
    > b = tf.reshape(a, [-1, 3, 1])
    > ```
    > 
    > In this example, `a` and `b` have the same flatten order, namely `[1,2,3,4,5,6]`, `a` has the shape `[3,2]`, its value is `[[1,2], [3,4], [5,6]]`, `b` has the shape `[2,3,1]`, its value is `[[[1],[2],[3]],[[4],[5],[6]]]`.



### get Tensorflow tensor dimensions (shape) as int values (tensor.get_shape().as_list())

- [python - How to get Tensorflow tensor dimensions (shape) as int values? - Stack Overflow](https://stackoverflow.com/questions/40666316/how-to-get-tensorflow-tensor-dimensions-shape-as-int-values)

    > To get the shape as a list of ints, do `tensor.get_shape().as_list()`.

### tf.shape()与tensor.get_shape()

- [tf.shape  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/shape)

- [tensorflow学习笔记（九）：tf.shape()与tensor.get_shape() - Keith - CSDN博客](https://blog.csdn.net/u012436149/article/details/52905166)

    > tf.shape(x)
    > -----------
    > 
    > **其中x可以是tensor，也可不是tensor，返回是一个tensor.**
    > 
    > ```
    > shape=tf.placeholder(tf.float32, shape=[None, 227,227,3] )
    > ```
    > 
    > 我们经常会这样来`feed`数据,如果在运行的时候想知道`None`到底是多少,这时候,只能通过`tf.shape(x)[0]`这种方式来获得.
    > 
    > tensor.get_shape()
    > ------------------
    > 
    > **只有tensor有这个方法， 返回是一个tuple**
    > 


### tf.expand_dims()

- [tf.expand_dims  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/expand_dims)

    > ```python
    > # 't' is a tensor of shape [2]
    > tf.shape(tf.expand_dims(t, 0))  # [1, 2]
    > tf.shape(tf.expand_dims(t, 1))  # [2, 1]
    > tf.shape(tf.expand_dims(t, -1))  # [2, 1]
    > 
    > # 't2' is a tensor of shape [2, 3, 5]
    > tf.shape(tf.expand_dims(t2, 0))  # [1, 2, 3, 5]
    > tf.shape(tf.expand_dims(t2, 2))  # [2, 3, 1, 5]
    > tf.shape(tf.expand_dims(t2, 3))  # [2, 3, 5, 1]
    > ```

### tf.nn.embedding_lookup

- [tf.nn.embedding_lookup函数的用法 - UESTC_C2_403的博客 - CSDN博客](https://blog.csdn.net/UESTC_C2_403/article/details/72779417)

    > tf.nn.embedding_lookup函数的用法主要是选取一个张量里面索引对应的元素。tf.nn.embedding_lookup（tensor, id）:tensor就是输入张量，id就是张量对应的索引，其他的参数不介绍。
    > 
    > 例如：
    > 
    > ```python
    > import tensorflow as tf;
    > import numpy as np; 
    > c = np.random.random([10,1])
    > b = tf.nn.embedding_lookup(c, [1, 3]) 
    > with tf.Session() as sess:
    > 	sess.run(tf.initialize_all_variables())
    > 	print sess.run(b)
    > 	print c
    > ```
    > 
    > 输出：
    > 
    > [[ 0.77505197]\
    >  [ 0.20635818]]\
    > [[ 0.23976515]\
    >  [ 0.77505197]\
    >  [ 0.08798201]\
    >  [ 0.20635818]\
    >  [ 0.37183035]\
    >  [ 0.24753178]\
    >  [ 0.17718483]\
    >  [ 0.38533808]\
    >  [ 0.93345168]\
    >  [ 0.02634772]]
    > 
    > 分析：输出为张量的第一和第三个元素。
    > 



## math


### Matrix norm (tf.norm)

- [tf.norm  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/norm)

- [python - Matrix norm in TensorFlow - Stack Overflow](https://stackoverflow.com/questions/43917456/matrix-norm-in-tensorflow)

    > So the Frobenius norm is a sum over a `nxm` matrix, but `tf.norm` allows to process several vectors and matrices in batch.
    > 
    > To better understand, imagine you have a rank 3 tensor:
    > 
    > `t = [[[2], [4], [6]], [[8], [10], [12]], [[14], [16], [18]]]`
    > 
    > It can be seen as several matrices aligned over one direction, but the function can't figure by itself which one. It could be either a batch of the following matrices:
    > 
    > `[2, 4, 6] , [8 ,10, 12], [14, 16, 18]`
    > 
    > or
    > 
    > `[2 8 14], [4, 10, 16], [6, 12, 18]`
    > 
    > So basically `axis` will tells which directions you want to consider when doing the summation in the Frobenius norm.
    > 
    > In your case, any of `[1,2]` or `[-2,-1]` would do the trick.
    > 


### tf.pow

- [tf.math.pow  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/math/pow)

### tf.reduce_mean

- [tf.math.reduce_mean  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/math/reduce_mean)

    > ```python
    > x = tf.constant([[1., 1.], [2., 2.]])
    > tf.reduce_mean(x)  # 1.5
    > tf.reduce_mean(x, 0)  # [1.5, 1.5]
    > tf.reduce_mean(x, 1)  # [1.,  2.]
    > 
    > ```

### tf.argmax

- [tf.math.argmax  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/math/argmax)

    > Returns the index with the largest value across axes of a tensor.


## condition

### tf.cond

- [tf.cond  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/cond)

    > Return `true_fn()` if the predicate `pred` is true else `false_fn()`.


### tf.math.less

- [tf.math.less  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/math/less)

    > Returns the truth value of (x < y) element-wise.

### tf.math.equal

- [tf.math.equal  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/math/equal)

    > Returns the truth value of (x == y) element-wise.





## tf.print()/tensor.eval()/sess.run()/tf.InteractiveSession()

- [tf.print  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/print)

- [python - How to print the value of a Tensor object in TensorFlow? - Stack Overflow](https://stackoverflow.com/questions/33633370/how-to-print-the-value-of-a-tensor-object-in-tensorflow)

    > The easiest^[A]^ way to evaluate the actual value of a `Tensor` object is to pass it to the `Session.run()` method, or call `Tensor.eval()` when you have a default session (i.e. in a `with tf.Session():` block, or see below). In general^[B]^, you cannot print the value of a tensor without running some code in a session.
    > 
    > If you are experimenting with the programming model, and want an easy way to evaluate tensors, the [`tf.InteractiveSession`](https://www.tensorflow.org/api_docs/python/tf/InteractiveSession) lets you open a session at the start of your program, and then use that session for all `Tensor.eval()` (and `Operation.run()`) calls. This can be easier in an interactive setting, such as the shell or an IPython notebook, when it's tedious to pass around a `Session` object everywhere.
    > 
    > This might seem silly for such a small expression, but one of the key ideas in Tensorflow is *deferred execution*: it's very cheap to build a large and complex expression, and when you want to evaluate it, the back-end (to which you connect with a `Session`) is able to schedule its execution more efficiently (e.g. executing independent parts in parallel and using GPUs).
    > 
    > * * * * *
    > 
    > [A]: To print the value of a tensor without returning it to your Python program, you can use the [`tf.Print()`](https://www.tensorflow.org/api_docs/python/tf/Print) operator, as [Andrzej suggests in another answer](https://stackoverflow.com/a/36296783/3574081). Note that you still need to run part of the graph to see the output of this op, which is printed to standard output. If you're running distributed TensorFlow, `tf.Print()` will print its output to the standard output of the task where that op runs. This means that if you use <https://colab.research.google.com> for example, or any other Jupyter Notebook, then you will *not see* the output of [`tf.Print()`](https://www.tensorflow.org/api_docs/python/tf/Print) in the notebook; in that case refer to [this answer](https://stackoverflow.com/questions/49969193/no-result-of-tf-print-in-kerass-model-fit/49969365#49969365) on how to get it to print still.
    > 
    > [B]: You *might* be able to use the experimental [`tf.contrib.util.constant_value()`](https://www.tensorflow.org/api_docs/python/tf/contrib/util/constant_value) function to get the value of a constant tensor, but it isn't intended for general use, and it isn't defined for many operators.
    > 
    > ---
    > 
    > While other answers are correct that you cannot print the value until you evaluate the graph, they do not talk about one easy way of actually printing a value inside the graph, once you evaluate it.
    > 
    > The easiest way to see a value of a tensor whenever the graph is evaluated (using `run` or `eval`) is to use the [`Print`](https://www.tensorflow.org/versions/master/api_docs/python/control_flow_ops.html#Print) operation as in this example:
    > 
    > ```python
    > # Initialize session
    > import tensorflow as tf
    > sess = tf.InteractiveSession()
    > 
    > # Some tensor we want to print the value of
    > a = tf.constant([1.0, 3.0])
    > 
    > # Add print operation
    > a = tf.Print(a, [a], message="This is a: ")
    > 
    > # Add more elements of the graph using a
    > b = tf.add(a, a)
    > ```
    > 
    > Now, whenever we evaluate the whole graph, e.g. using `b.eval()`, we get:
    > 
    > ```
    > I tensorflow/core/kernels/logging_ops.cc:79] This is a: [1 3]
    > ```
    > 
    > ---
    > 
    > it is VERY Important that you use the a from a=tf.print into something else! tf.print(a,[a]) won't do anything otherwise – Fábio Dias Oct 14 '16 at 21:58


- [python - In TensorFlow, what is the difference between Session.run() and Tensor.eval()? - Stack Overflow](https://stackoverflow.com/questions/33610685/in-tensorflow-what-is-the-difference-between-session-run-and-tensor-eval)

    > The FAQ session on tensor flow has an [answer to exactly the same question](https://www.tensorflow.org/resources/faq#running_a_tensorflow_computation). I would just go ahead and leave it here:
    > 
    > * * * * *
    > 
    > If `t` is a `Tensor` object, `t.eval()` is shorthand for `sess.run(t)` (where `sess` is the current default session. The two following snippets of code are equivalent:
    > 
    > ```python
    > sess = tf.Session()
    > c = tf.constant(5.0)
    > print sess.run(c)
    > 
    > c = tf.constant(5.0)
    > with tf.Session():
    >   print c.eval()
    > ```
    > 
    > In the second example, the session acts as a context manager, which has the effect of installing it as the default session for the lifetime of the with block. The context manager approach can lead to more concise code for simple use cases (like unit tests); if your code deals with multiple graphs and sessions, it may be more straightforward to explicit calls to `Session.run()`.
    > 

### tf.InteractiveSession()

- [TensorFlow 的 tf.InteractiveSession 互動式 Session 使用教學 - G. T. Wang](https://blog.gtwang.org/programming/tensorflow-interactivesession-tutorial/)

    > 本篇是 TensorFlow 的 `tf.InteractiveSession` 互動式 Session 使用教學。
    > 
    > 在 TensorFlow 中，所有的運算都要放在 session 中執行，而如果在 shell 或 IPython notebooks 中執行 TensorFlow 的程式時，我們可以改用比較方便使用的 [`tf.InteractiveSession`](https://www.tensorflow.org/api_docs/python/tf/InteractiveSession)。
    > 
    > 正常來說，TensorFlow 的程式放在 `tf.Session` 中跑的時候，我們會這樣寫：
    > ```python
    > import tensorflow as tf
    > a = tf.constant(5.0)
    > b = tf.constant(6.0)
    > c = a * b
    > sess = tf.Session()
    > 
    > # 使用 sess 這個 session 執行
    > print(sess.run(c))
    > 
    > sess.close()
    > ```
    > 
    > 而 `tf.InteractiveSession` 與 `tf.Session` 的作用相同，只不過 `tf.InteractiveSession` 在建立時，會自動將自己設定為預設的 session，這樣可以讓我們少打一些字。
    > ```python
    > import tensorflow as tf
    > a = tf.constant(5.0)
    > b = tf.constant(6.0)
    > c = a * b
    > 
    > # 自動設定為預設的 session
    > sess = tf.InteractiveSession()
    > 
    > # 直接使用 tf.Tensor.eval 執行，不需要指定 sess 變數
    > print(c.eval())
    > 
    > sess.close()
    > ```
    > 
    > 這裡的 `c` 在呼叫 [`tf.Tensor.eval`](https://www.tensorflow.org/api_docs/python/tf/Tensor#eval) 執行時，會自動使用預設的 session（也就是 `sess`）來執行。
    > 
    > 而一般的 `tf.Session` 只有在 `with` 環境之下才會將自己設定為預設的 session：
    > ```python
    > import tensorflow as tf
    > a = tf.constant(5.0)
    > b = tf.constant(6.0)
    > c = a * b
    > with tf.Session():
    >   # 亦可使用 tf.Tensor.eval 執行
    >   print(c.eval())
    > ```

## feed data

- [tf.placeholder  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/placeholder)

### what does x = tf.placeholder(tf.float32, [None, 784]) means

- [tensorflow - what does x = tf.placeholder(tf.float32, [None, 784]) means? - Stack Overflow](https://stackoverflow.com/questions/39305174/what-does-x-tf-placeholdertf-float32-none-784-means)

    > From the tutorial: [Deep MNIST for Experts](https://www.tensorflow.org/versions/r0.10/tutorials/mnist/pros/index.html)
    > 
    > > Here we assign it a shape of [None, 784], where 784 is the dimensionality of a single flattened 28 by 28 pixel MNIST image, and **None indicates that the first dimension, corresponding to the batch size, can be of any size**.
    > > 





### Inject values into the middle of TensorFlow graph

- [python - How to inject values into the middle of TensorFlow graph? - Stack Overflow](https://stackoverflow.com/questions/41621053/how-to-inject-values-into-the-middle-of-tensorflow-graph)


    > I'm not allowed to comment on your post, @iramusa, so I'll give an answer. You don't need to use a placeholder_with_default. You can just feed in the values to whatever node you want:
    > 
    > ```python
    > import tensorflow as tf
    > 
    > x = tf.placeholder(tf.float32,(), name='x')
    > z = x + tf.constant(5.0)
    > y = z*tf.constant(0.5)
    > 
    > with tf.Session() as sess:
    >     print(sess.run(y, feed_dict={x: 2}))  # get 3.5
    >     print(sess.run(y, feed_dict={z: 5}))  # get 2.5
    >     print(sess.run(y, feed_dict={y: 5}))  # get 5
    > ```
    > 

## metrics

### auc
- [tf.metrics.auc  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/metrics/auc)

    > Computes the approximate AUC via a Riemann sum.

### AUC的错误/问题与修正

- [Tensorflow： AUC的错误/问题与修正 - 知乎](https://zhuanlan.zhihu.com/p/41461872)

    > AUC是评价模型的常用指标，Tensorflow作为著名的机器学习框架，自然有对这一指标的计算API，其官网API文档为[AUC](http://link.zhihu.com/?target=https%3A//www.tensorflow.org/api_docs/python/tf/metrics/auc)。
    > 
    > 问题
    > --
    > 
    > 但是，这一API不是很好用，在此举一个很简单的例子：
    > 
    > ```python
    > import tensorflow as tf
    > 
    > x_1 = [0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.8, 0.8, 0.9, 1]
    > y_1 = [1, 1, 1, 1, 1, 0, 0, 0, 0, 0]
    > x_2 = [1, 0.9, 0.8, 0.7, 0.6, 0.5, 0.4, 0.3, 0.2, 0.1]
    > y_2 = [1, 1, 1, 1, 1, 0, 0, 0, 0, 0]
    > 
    > x_placeholder = tf.placeholder(tf.float64, [10])
    > y_placeholder = tf.placeholder(tf.bool, [10])
    > auc = tf.metrics.auc(labels=y_placeholder, predictions=x_placeholder)
    > initializer = tf.group(tf.global_variables_initializer(), tf.local_variables_initializer())
    > 
    > with tf.Session() as sess:
    >     sess.run(initializer)
    >     for i in range(3):
    >         auc_value, update_op = sess.run(auc, feed_dict={x_placeholder: x_1, y_placeholder: y_1})
    >         print('auc_1: ' + str(auc_value) + ", update_op: " + str(update_op))
    >         auc_value, update_op = sess.run(auc, feed_dict={x_placeholder: x_2, y_placeholder: y_2})
    >         print('auc_2: ' + str(auc_value) + ", update_op: " + str(update_op))
    > 
    > # output
    > # auc_1: 0.0, update_op: 1.999999e-07
    > # auc_2: 1.999999e-07, update_op: 0.48999995
    > # auc_1: 0.48999995, update_op: 0.32444444
    > # auc_2: 0.32444444, update_op: 0.48999995
    > # auc_1: 0.489999, update_op: 0.3904
    > # auc_2: 0.3904, update_op: 0.48999998
    > 
    > ```
    > 
    > 总的来说，上面这段代码反映出的令人困惑的问题有三个：
    > 
    > 1.  使用AUC时，一定要定义local variable initializer，不然就会报错，但是众所周知，AUC这个指标的计算过程不应该和"变量"产生关联
    > 2.  每次计算输出的update_op和下次输出的auc值总是相等
    > 3.  同样的输入，计算出的AUC不同
    > 
    > 这三个问题我是在2017年夏天发现的，截止2018年8月，TF 1.10rc版本并未解决这一问题，官方文档中也未说明这一现象。
    > 
    > 
    > ---
    > 
    > 解决
    > --
    > 
    > 经过认真阅读相关的源代码，可以发现，出现这些问题的原因是：Tensorflow在计算AUC这一问题上，采取了一种比较令人困惑的计算真阳性，假阳性，假阴性，真阴性值的计算策略。
    > 
    > 为说明这一问题，我简单的贴一段Tensorflow中计算不同阈值下真阳性样本数量的源代码。
    > 
    > ```python
    > # assume num_threshold = 200
    > # label_is_pos is a tensor with shape (200,) dtype is tf.bool.
    > # pred_is_pos is a tensor with shape (200,) dtype is tf.bool
    > true_p = metric_variable([num_thresholds], dtypes.float32, name='true_positives')
    > is_true_positive = math_ops.to_float(math_ops.logical_and(label_is_pos, pred_is_pos))
    > update_ops['tp'] = state_ops.assign_add(true_p, math_ops.reduce_sum(is_true_positive, 1))
    > values['tp'] = true_p
    > return values, update_ops
    > 
    > ```
    > 
    > 这段代码说明了产生上述三个问题的原因：
    > 
    > 1.  计算tp会涉及到一个名为"true_positives"的变量，这是一个tensorflow的局部变量（local variable），这个变量记录了之前调用这一函数时的真阳性数量之和。因此使用auc时，一定要加入local variable initializer，不然就会报错。在第一次调用时，这一变量会被初始化为0。
    > 2.  可以确定，assign_add函数是造成update_op和下次输出的auc值总是相等的原因，但是官方的assign_add函数文档写的闪烁其词，源代码依赖太复杂，我还不能阐释这其中的具体细节是什么。
    > 3.  update_op计算的**其实并不是本次输入数据的auc**，而是metrics.auc这一函数自从被第一次调用以来，所有单次计算出的auc的累计平均值。因此，每次计算出的AUC总是在变动。
    > 
    > 理论上来说，只有第一次使用auc函数时，输出的update_op值是真正的auc，只要多调用几次，后面输出的AUC全部都是平均值，而非当前输入的数据的AUC。**按照Tensorflow的官方说法，输出平均值似乎并不是一种错误，而是有意设计成这样的**。但是这一设计就使得我们很难追踪测试集的AUC的实时变化，而且说句实在话我也不明白这到底有什么意义。
    > 
    > 如果一定要用原生的tf框架，那么每次计算auc前，都要reset一次local variable。然后取auc函数返回的update_ops而非values作为auc的值
    > 
    > ---
    > 
    > 设计成这样其实是为了计算整个epoch的auc， 一个batch的auc并不能表征整个epoch数据的auc。但由于我们要分batch去预测，所以这样设计的用法是在每一个预测的batch都进行auc的更新，最终输出的auc为整个epoch的均值。
    > 

### TensorFlow踩坑记要(1)

- [TensorFlow踩坑记要(1)](https://bourneli.github.io/tensorflow/2017/08/23/tensorflow-pit-1.html)

    > 避免在初始化变量后构建tensor
    > -----------------
    > 
    > 在计算auc时，需要使用tf.metrics.auc这个函数构建tensor，由于对tensorflow先构建计算图，在计算的流程理解不够深刻，导致在初始化变量后定义auctensor
    > 
    > ```python
    > sess.run(tf.global_variables_initializer())
    > sess.run(tf.local_variables_initializer())
    > 
    > # ... 建模过程，这里省略
    > 
    > auc = tf.metrics.auc(...)
    > sess.run(auc,[...])
    > ```
    > 
    > 代码执行时，总是抛出异常，导致意思是部分内部tensor没有初始化，在网上找到了[参这个解决方案](https://stackoverflow.com/questions/39435341/how-to-calculate-auc-with-tensorflow)，该方案确实没有问题，但是我的问题不是这里，正确的解决方法是将auc的定义提前init前，这样才能够被初始化，膝盖如下，
    > 
    > ```python
    > auc = tf.metrics.auc(...) # 定义提前
    > 
    > sess.run(tf.global_variables_initializer())
    > sess.run(tf.local_variables_initializer())
    > 
    > # ... 建模过程，这里省略
    > 
    > sess.run(auc,[...])
    > ```
    > 
    > 修改后，问题迎刃而解。感谢[xiaoxiwang(王晓曦)](https://github.com/vshallc)同学指点迷津，尽快走出了这个坑，才有时间王者上钻石。
    > 
    > 尽可能在session.run执行完可以执行的tensor
    > -----------------------------
    > 
    > 假如有多个tensor，复用同一个feed_dict，建议一次性批量执行run，而不是要分开run，这样可以提高执行效率，虽然可能代码有点丑陋，但是效率是有明显提高的，本人试验亲测有效。
    > 
    > ```python
    > # Block 1
    > t1_rst, t2_rst, t3_rst = sess.run([t1,t2,t3], feed_dict = some_dict)  # 快
    > 
    > # Block 2
    > t1_rst = sess.run(t1, feed_dict = some_dict)
    > t2_rst = sess.run(t2, feed_dict = some_dict)
    > t3_rst = sess.run(t3, feed_dict = some_dict)
    > ```
    > 
    > Block 1与Block 2的效果一样，但是Block 1块很多。
    > 
    > 常用二元分类度量tensor
    > --------------
    > 
    > -   tf.metrics.recall
    > -   tf.metrics.precision
    > -   tf.metrics.auc
    > -   tf.metrics.accuracy
    > 
    > 这些tesnfor的输入基本上可以通用，非常方便。
    > 
    > tf.gather切分tensor的例子
    > --------------------
    > 
    > tf.gather用于切分tensor，取出需要的部分。假如有如下tensor
    > 
    > ```python
    > t = tf.Variable([[1, 1.1],
    >                  [2, 2.2],
    >                  [3, 3.3],
    >                  [4, 4.4]])
    > 
    > tf.gather(t, axis = 1, indices = 0) # 第一列 [1, 2, 3, 4]
    > tf.gather(t, axis = 1, indices = 1) # 第二列 [1.1, 2.2, 3.3, 4.4]
    > ```
    > 
    > tensor t的shape=(4,2)，使用axis指定是4的维度还是2的维度，所以如果取列，axis = 1，如果区行，axis = 0。
    > 


## RNN

- [tf.contrib.rnn.BasicRNNCell  |  TensorFlow](https://www.tensorflow.org/versions/r1.0/api_docs/python/tf/contrib/rnn/BasicRNNCell)
    - zero_state(batch_size, dtype)
        Return zero-filled state tensor(s).

- [tf.truncated_normal  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/truncated_normal)
    Outputs random values from a truncated normal distribution.

    The generated values follow a normal distribution with specified mean and standard deviation, except that values whose magnitude is more than 2 standard deviations from the mean are dropped and re-picked.
    
- [tf.gradients  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/gradients)
    Constructs symbolic derivatives of sum of `ys` w.r.t. x in `xs`.

- [tf.trainable_variables  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/trainable_variables)
    Returns all variables created with `trainable=True`.

    When passed `trainable=True`, the `Variable()` constructor automatically adds new variables to the graph collection `GraphKeys.TRAINABLE_VARIABLES`. This convenience function returns the contents of that collection.

- [tf.clip_by_global_norm  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/clip_by_global_norm)
    Clips values of multiple tensors by the ratio of the sum of their norms.

    To perform the clipping, the values `t_list[i]` are set to:

    `t_list[i]   * clip_norm / max(global_norm, clip_norm)  
    `

    where:

    `global_norm = sqrt(sum([l2norm(t)**2   for t in t_list]))  
    `

- [tf.train.GradientDescentOptimizer  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/train/GradientDescentOptimizer)
    - apply_gradients
        Apply gradients to variables.

- [tf.nn.dynamic_rnn  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/dynamic_rnn)
    Creates a recurrent neural network specified by RNNCell `cell`.

    Performs fully dynamic unrolling of `inputs`.

    - [Analysis of the output from tf.nn.dynamic_rnn tensorflow function - Stack Overflow](https://stackoverflow.com/questions/44162432/analysis-of-the-output-from-tf-nn-dynamic-rnn-tensorflow-function)

        > [`tf.dynamic_rnn`](https://www.tensorflow.org/api_docs/python/tf/nn/dynamic_rnn) provides two outputs, `outputs` and `state`.
        > 
        > -   `outputs` contains the output of the RNN cell at every time instant. Assuming the default `time_major == False`, let's say you have an input composed of 10 examples with 7 time steps each and a feature vector of size 5 for every time step. Then your input would be 10x7x5 (`batch_size`x`max_time`x`features`). Now you give this as an input to a RNN cell with output size 15. Conceptually, each time step of each example is input to the RNN, and you would get a 15-long vector for each of those. So that is what `outputs` contains, a tensor in this case of size 10x7x15 (`batch_size`x`max_time`x`cell.output_size`) with the output of the RNN cell at each time step. If you are only interested in the last output of the cell, you can just slice the time dimension to pick just the last element (e.g. `outputs[:, -1, :]`).
        > -   `state` contains the state of the RNN after processing all the inputs. Note that, unlike `outputs`, this doesn't contain information about every time step, but only about the last one (that is, the state _after_ the last one). Depending on your case, the state may or may not be useful. For example, if you have very long sequences, you may not want/be able to processes them in a single batch, and you may need to split them into several subsequences. If you ignore the `state`, then whenever you give a new subsequence it will be as if you are beginning a new one; if you remember the state, however (e.g. outputting it or storing it in a variable), you can feed it back later (through the `initial_state` parameter of `tf.nn.dynamic_rnn`) in order to correctly keep track of the state of the RNN, and only reset it to the initial state (generally all zeros) after you have completed the whole sequences. The shape of `state` can vary depending on the RNN cell that you are using, but, in general, you have some state for each of the examples (one or more tensors with size `batch_size`x`state_size`, where `state_size` depends on the cell type and size).



- [tf.nn.embedding_lookup  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/embedding_lookup)
    Looks up `ids` in a list of embedding tensors.









## CNN



- [tf.nn.conv2d  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/conv2d)

    > Computes a 2-D convolution given 4-D `input` and `filter` tensors.


- [tf.nn.conv2d_transpose  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/conv2d_transpose)

    > The transpose of `conv2d`.
    > 
    > This operation is sometimes called "deconvolution" after [Deconvolutional Networks](http://www.matthewzeiler.com/pubs/cvpr2010/cvpr2010.pdf), but is actually the transpose (gradient) of `conv2d` rather than an actual deconvolution.

### 步伐(stride)和填充(padding)

- [卷積神經網路(Convolutional neural network, CNN):卷積計算中的步伐(stride)和填充(padding)](https://medium.com/@chih.sheng.huang821/%E5%8D%B7%E7%A9%8D%E7%A5%9E%E7%B6%93%E7%B6%B2%E8%B7%AF-convolutional-neural-network-cnn-%E5%8D%B7%E7%A9%8D%E8%A8%88%E7%AE%97%E4%B8%AD%E7%9A%84%E6%AD%A5%E4%BC%90-stride-%E5%92%8C%E5%A1%AB%E5%85%85-padding-94449e638e82)

    > #### **是不是卷積計算後，卷積後的圖是不是就一定只能變小?**
    > 
    > **ANS: 用zero padding**
    > 
    > 這個手法就是看你會消失多少的大小，在輸入的圖部份就給你加上0元素進去，這個手法稱為zero padding，實際作法如下圖。
    > 
    > ![](https://cdn-images-1.medium.com/max/960/1*9kqLUr7bMEYryGNtAHyL8A.png)
    > 
    > 此刻的卷積計算如下，這樣卷積後的圖就不會變小了。
    > 
    > ![](https://cdn-images-1.medium.com/max/960/1*GwxhjA7-FLIRrtl__RkRgg.png)
    > 
    > 上圖舉的例子是kernel map是3x3，假設kernel map為5x5，此刻在輸入的圖上下左右行和列都各加2行和2列的0，讓圖變成14x14，就可以了。
    > 
    > * * * * *
    > 
    > #### **卷積計算是不是一次只能移動一格?**
    > 
    > **ANS: 當然不是，也可以2格3格，但此時卷積後的圖就會變的更小。**
    > 
    > ![](https://cdn-images-1.medium.com/max/960/1*Hy3dNn5siu4_q7jE7yO9eA.png)
    > 
    > 在tensorflow，padding那邊給了兩個選項「padding = 'VALID'」和「padding = 'SAME'」
    > 
    > **padding = 'VALID' 等於最一開始敘述的卷積計算，圖根據filter大小和stride大小而變小。**
    > 
    > 公式如下: new_height = new_width = (W --- F + 1) / S （结果向上取整數，假設算出來結果是4.5，取5）
    > 
    > 剛剛的例子\
    > filter 3x3, stride=1, 卷積後的大小: (10--3+1)/1=8\
    > filter 3x3, stride=2, 卷積後的大小: (10--3+1)/2=4
    > 
    > **padding = 'SAME'，會用zero-padding的手法，讓輸入的圖不會受到kernel map的大小影響。**
    > 
    > new_height = new_width = W / S （结果向上取整數）
    > 
    > > 剛剛的例子，filter 3x3, stride=2, 卷積後的大小: 10/2=5 (這邊我沒有做這張圖，可以自己想像一下，做法如下所述)\
    > > 這邊的作法會先補zero-padding的0元素，然後在作stride=2的卷積，所以實際上是最(10+2)*(10+2)的圖做padding = 'VALID'的事情，(12--3+1)/2=5。
    > 

### 1X1 convolution

- [卷积神经网络中用1*1 卷积有什么作用或者好处呢？ - 简书](https://www.jianshu.com/p/04c2a9ccaa75)

    > 1X1卷积核最开始是在颜水成论文 [[1312.4400] Network In Network](https://link.jianshu.com?t=https%3A%2F%2Farxiv.org%2Fabs%2F1312.4400) 中提出的，后来被[[GoogLeNet 1409.4842] Going Deeper with Convolutions](https://link.jianshu.com?t=https%3A%2F%2Farxiv.org%2Fabs%2F1409.4842)的Inception结构继续应用了。能够使用更小channel的前提就是sparse比较多 不然1*1效果也不会很明显
    > 
    > [Network in Network　and 1×1 convolutions](https://link.jianshu.com?t=http%3A%2F%2Fmooc.study.163.com%2Flearn%2F2001281004%3Ftid%3D2001392030%23%2Flearn%2Fcontent%3Ftype%3Ddetail%26id%3D2001729330)
    > ====================================================================================================================================================================================================
    > 
    > Lin et al., 2013. Network in network
    > 
    > 1x1 卷积可以压缩信道数。池化可以压缩宽和高。\
    > １x1卷积给神经网络增加非线性，从而减少或保持信道数不变，也可以增加信道数
    > 
    > ![](//upload-images.jianshu.io/upload_images/1496926-8a2f31f55ed4ebaa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)
    > 
    > 11c.png
    > 
    > ![](//upload-images.jianshu.io/upload_images/1496926-4720f541e8a72f11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)
    > 
    > 11c1.png
    > 
    > 1.实现跨通道的交互和信息整合
    > ===============
    > 
    > 1×1的卷积层（可能）引起人们的重视是在NIN的结构中，论文中林敏师兄的想法是利用MLP代替传统的线性卷积核，从而提高网络的表达能力。文中同时利用了跨通道pooling的角度解释，认为文中提出的MLP其实等价于在传统卷积核后面接cccp层，从而实现多个feature map的线性组合，实现跨通道的信息整合。而cccp层是等价于1×1卷积的，因此细看NIN的caffe实现，就是在每个传统卷积层后面接了两个cccp层（其实就是接了两个1×1的卷积层）
    > 
    > ![](//upload-images.jianshu.io/upload_images/1496926-0c124b0efc8f16d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/300)
    > 
    > 1.png
    > 
    > 2.进行卷积核通道数的降维和升维
    > ================
    > 
    > 由于3X3卷积或者5X5卷积在几百个filter的卷积层上做卷积操作时相当耗时，所以1X1卷积在3X3卷积或者5X5卷积计算之前先降低维度。那么，1X1卷积的主要作用有以下几点：\
    > 1、降维（ dimension reductionality ）。比如，一张500 X500且厚度depth为100 的图片在20个filter上做1X1的卷积，那么结果的大小为500X500X20。\
    > 2、加入非线性。卷积层之后经过激励层，1X1的卷积在前一层的学习表示上添加了非线性激励（ non-linear activation ），提升网络的表达能力；
    > 
    > [What is Depth of a convolutional neural network?](https://link.jianshu.com?t=https%3A%2F%2Fstackoverflow.com%2Fquestions%2F32294261%2Fwhat-is-depth-of-a-convolutional-neural-network)
    > 
    > * * * * *
    > 
    > 如果卷积的输出输入都是一个平面，那么１X1卷积核并没有什么意义，它是完全不考虑像素与周边其他像素关系。但卷积的输出输入是长方体，所以１X1卷积实际上对每个像素点，在不同的channels上进行线性组合（信息整合），且保留原有平面结构，调控depth,从而完成升维或降维的功能。\
    > 下图所示，如果选择２个filters的１X1卷积层，那么数据就从原来的depth3降到了２。若用４个filters,则起到了升维的作用。
    > 
    > ![](//upload-images.jianshu.io/upload_images/1496926-e4edc99affc4e90f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/600)
    > 
    > 1.png
    > 
    > MSRA的ResNet同样也利用了1×1卷积，并且是在3×3卷积层的前后都使用了，不仅进行了降维，还进行了升维，使得卷积层的输入和输出的通道数都减小，参数数量进一步减少，如下图的结构。
    > 
    > ![](//upload-images.jianshu.io/upload_images/1496926-cc829d9950e0a330.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)
    > 
    > 1.png
    > 
    > **Simple Answer**
    > =================
    > 
    > Most simplistic explanation would be that 1x1 convolution leads to dimension reductionality. For example, an image of 200 x 200 with 50 features on convolution with 20 filters of 1x1 would result in size of 200 x 200 x 20. But then again, is this is the best way to do dimensionality reduction in the convoluational neural network? What about the efficacy vs efficiency?
    > 
    > * * * * *
    > 
    > [One by One [ 1 x 1 ] Convolution - counter-intuitively useful](https://link.jianshu.com?t=http%3A%2F%2Fiamaaditya.github.io%2F2016%2F03%2Fone-by-one-convolution%2F)
    > 
    > **Complex Answer**
    > ==================
    > 
    > **Feature transformation**
    > 
    > Although 1x1 convolution is a 'feature pooling' technique, there is more to it than just sum pooling of features across various channels/feature-maps of a given layer. 1x1 convolution acts like coordinate-dependent transformation in the filter space[[https://plus.google.com/118431607943208545663/posts/2y7nmBuh2ar]](https://link.jianshu.com?t=https%3A%2F%2Fplus.google.com%2F118431607943208545663%2Fposts%2F2y7nmBuh2ar%255D). It is important to note here that this transformation is strictly linear, but in most of application of 1x1 convolution, it is succeeded by a non-linear activation layer like ReLU. This transformation is learned through the (stochastic) gradient descent. But an important distinction is that it suffers with less over-fitting due to smaller kernel size (1x1).
    > 
    > 3.可以在保持feature map 尺寸不变（即不损失分辨率）的前提下大幅增加非线性特性，把网络做得很deep
    > ========================================================
    > 
    > **Deeper Network**
    > 
    > One by One convolution was first introduced in this paper titled [Network in Network](https://link.jianshu.com?t=https%3A%2F%2Farxiv.org%2Fabs%2F1312.4400). In this paper, the author's goal was to generate a deeper network without simply stacking more layers. It replaces few filters with a smaller perceptron layer with mixture of 1x1 and 3x3 convolutions. In a way, it can be seen as "going wide" instead of "deep", but it should be noted that in machine learning terminology, 'going wide' is often meant as adding more data to the training. Combination of 1x1 (x F) convolution is mathematically equivalent to a multi-layer perceptron[[https://www.reddit.com/r/MachineLearning/comments/3oln72/1x1_convolutions_why_use_them/cvyxood/]](https://link.jianshu.com?t=https%3A%2F%2Fwww.reddit.com%2Fr%2FMachineLearning%2Fcomments%2F3oln72%2F1x1_convolutions_why_use_them%2Fcvyxood%2F%255D)
    > 
    > **Inception Module**
    > ====================
    > 
    > In GoogLeNet architecture, 1x1 convolution is used for two purposes
    > 
    > ```
    > To make network deep by adding an "inception module" like Network in Network paper, as described above.
    > To reduce the dimensions inside this "inception module".
    > To add more non-linearity by having ReLU immediately after every 1x1 convolution.
    > 
    > ```
    > 
    > Here is the scresnshot from the paper, which elucidates above points :
    > 
    > ![](//upload-images.jianshu.io/upload_images/1496926-00c775249b533922.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)
    > 
    > inception_1x1.png
    > 
    > It can be seen from the image on the right, that 1x1 convolutions (in yellow), are specially used before 3x3 and 5x5 convolution to reduce the dimensions. It should be noted that a two step convolution operation can always to combined into one, but in this case and in most other deep learning networks, convolutions are followed by non-linear activation and hence convolutions are no longer linear operators and cannot be combined.
    > 
    > In designing such a network, it is important to note that initial convolution kernel should be of size larger than 1x1 to have a receptive field capable of capturing locally spatial information. According to the NIN paper, 1x1 convolution is equivalent to cross-channel parametric pooling layer. From the paper - "This cascaded cross channel parameteric pooling structure allows complex and learnable interactions of cross channel information".
    > 
    > Cross channel information learning (cascaded 1x1 convolution) is biologically inspired because human visual cortex have receptive fields (kernels) tuned to different orientation. For e.g
    > 
    > ![](https://i.imgur.com/pIcX5D3.jpg)
    > RotBundleFiltersListPlot3D.gif
    > 
    > **Different orientation tuned receptive field profiles in the human visual cortex [Source](https://link.jianshu.com?t=http%3A%2F%2Fbmia.bmt.tue.nl%2Feducation%2Fcourses%2Ffev%2Fcourse%2Fnotebooks%2FConvolution.html)**
    > 
    > **More Uses**
    > =============
    > 
    > **1x1 Convolution can be combined with Max pooling**
    > 
    > ![](//upload-images.jianshu.io/upload_images/1496926-c4c0ccc5e35862c0.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/337)
    > 
    > numerical_max_pooling.gif
    > 
    > **1x1 Convolution with higher strides leads to even more redution in data by decreasing resolution, while losing very little non-spatially correlated information.**
    > 
    > ![](//upload-images.jianshu.io/upload_images/1496926-5551a64fb67ac2ca.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/294)
    > 
    > no_padding_strides.gif
    > 
    > **Replace fully connected layers with 1x1 convolutions as Yann LeCun believes they are the same**
    > 
    > > -In Convolutional Nets, there is no such thing as "fully-connected layers". There are only convolution layers with 1x1 convolution kernels and a full connection table.-- Yann LeCun
    > 
    > *Convolution gif images generated using [this wonderful code](https://link.jianshu.com?t=https%3A%2F%2Fgithub.com%2Fvdumoulin%2Fconv_arithmetic), more images on 1x1 convolutions and 3x3 convolutions can be* [found here](https://link.jianshu.com?t=http%3A%2F%2Fgpgpu.cs-i.brandeis.edu%2Fconvolution_images%2F)
    > 
    > **参考文献**
    > ========
    > 
    > [https://www.zhihu.com/question/56024942](https://link.jianshu.com?t=https%3A%2F%2Fwww.zhihu.com%2Fquestion%2F56024942)
    > 

- [(2 封私信 / 83 条消息)卷积神经网络中用1*1 卷积有什么作用或者好处呢？ - 知乎](https://www.zhihu.com/question/56024942)

    > 为什么没有人从解耦合的角度回答呢？我来从这个角度回答一下。
    > 
    > 大部分的朋友从降维或者升维的角度进行了回答。那么可以追问一个更加深入的问题，为什么采用这种方式进行降维是有效的？在google net的论文中其实给出了回答，那就是使用1x1的卷积基于这样一个假设：cross-channel correlations and spatial correlations are sufficiently decoupled that it is preferable not to map them jointly。即cross-channel correlation 和 spatial correlation的学习可以进行解耦。1x1的卷积相当于学习了feature maps之间的cross-channel correlation。实验证明了这种解耦可以在不损害模型表达能力的情况下大大减少参数数量和计算量。
    > 
    > 但是需要注意的是，1x1的卷积层后面加上一个正常的卷积层的情况下，这种解耦合并不彻底，正常卷积层仍然存在对部分的cross-channel correlation的学习。
    > 
    > 于是，后来人们就有了一个更加大胆的想法，那就是depth-wise seperable convolution。在depth-wise seperable convolution中，1x1的卷积层后是一个特殊的组卷积，这个特殊的组卷积将每一个channel分为一组，那么就不存在对cross-channel correlation的学习了，就实现了对cross-channel correlation和spatial correlation的彻底解耦合。这种完全解耦的方式虽然可以大大降低参数数量和计算量，但是正如在mobile net中所看到的，性能会受到很大的损失。
    > 
    > 那么mobile net之后提出的shuffle net跟解耦合又有什么联系呢？
    > 
    > shuffle net中的结构中使用了两个组卷积，在下图中，第一个组卷积将feature map分成了三组，第一个组卷积可以学习同一组内的feature map之间的cross-channel correlation，但是不是同一组的feature map之间的cross-channel correlation是无法学习的。第二个组卷积通过一个shuffle操作，使每一组都包含了第一个组卷积不同组输出的feature map，这就使得第一个组卷积没有学习到的cross-channel correlation得到了学习。
    > 
    > 从以上的分析中我们可以看出，shuffle net实际上是对depth-wise seperable的完全解耦的方式做了一定的妥协，将cross-channel correlation的学习通过组卷积的方式分解为两步，第一个组卷积只学习组内的cross-channel correlation，第二个组卷积在shuffle操作之后，可以学习第一个组卷积中组间feature map的cross-channel correlation。
    > 
    > 此外，微软亚洲研究院的Interleaved Group Convolutions跟shuffle net的工作基本相同，但是对于如何分组能达到网络宽度最大有一个的理论推导，这个理论推导非常漂亮。
    > 
    > ![](https://pic2.zhimg.com/v2-272fef4df5c95be67a6ff7baa23d373d_b.jpg)
    > 
    > ![](https://pic2.zhimg.com/80/v2-272fef4df5c95be67a6ff7baa23d373d_hd.jpg)
    > 
    > 最后有一个题外话。1x1的卷积在NIN中被发明的时候，并没有从解耦合的角度来进行解释。真正从解耦合的角度来理解1x1的卷积是inception、xception和mobile net系列，这对卷积神经网络结构的发展以及在移动设备上的应用产生了深远的影响。1x1的卷积被发明的时候，作者也许没有意识到它会产生这么大的影响力，也算是无心插柳柳成荫的典范。
    > 

### max pooling

- [tf.nn.max_pool  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/max_pool)

### convolution

- [tf.nn.conv2d  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/conv2d)


### conv2d_transpose is dependent on batch_size when making predictions

- [python - conv2d_transpose is dependent on batch_size when making predictions - Stack Overflow](https://stackoverflow.com/questions/38822411/conv2d-transpose-is-dependent-on-batch-size-when-making-predictions)

    > So I came across a solution based on the issues forum of tensorflow at <https://github.com/tensorflow/tensorflow/issues/833>.
    > 
    > In my code
    > 
    > ```python
    >  conv4 = layers.deconvLayer(conv3['layer_output'],
    >                                     filter_shape=[2, 2, 64, 128],
    >                                     output_shape=[batch_size, 32, 40, 64],
    >                                     strides=[1, 2, 2, 1])
    > ```
    > 
    > my output shape that get passed to deconvLayer was hard coded with a predetermined batch shape when training. By altering this to the following:
    > 
    > ```python
    > def deconvLayer(input, filter_shape, output_shape, strides):
    >     W1_1 = weight_variable(filter_shape)
    > 
    >     dyn_input_shape = tf.shape(input)
    >     batch_size = dyn_input_shape[0]
    > 
    >     output_shape = tf.pack([batch_size, output_shape[1], output_shape[2], output_shape[3]])
    > 
    >     output = tf.nn.conv2d_transpose(input, W1_1, output_shape, strides, padding="SAME")
    > 
    >     return output
    > ```
    > 
    > This allows the shape to be dynamically inferred at run time and can handle a variable batch size.
    > 
    > 
    > So where we would usually use None for the batch_size in normal convolutional ops, we must provide a shape, and since this could vary based on input, we must go through the effort of dynamically determining it.
    > 


### tf.nn.depthwise_conv2d()

- [tf.nn.depthwise_conv2d  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/depthwise_conv2d)

- [【Tensorflow】tf.nn.depthwise_conv2d如何实现深度卷积? - xf__mao的博客 - CSDN博客](https://blog.csdn.net/mao_xiao_feng/article/details/77938385)

    > depthwise_conv2d来源于深度可分离卷积
    > 
    > [Xception: Deep Learning with Depthwise Separable Convolutions](https://arxiv.org/abs/1610.02357)
    > 
    > ### `tf.nn.depthwise_conv2d(input,filter,strides,padding,rate=None,name=None,data_format=None)`
    > 
    > 除去`name`参数用以指定该操作的name，`data_format`指定数据格式，与方法有关的一共五个参数：
    > 
    > 第一个参数`input`：指需要做卷积的输入图像，要求是一个4维Tensor，具有`[batch, height, width, in_channels]`这样的shape，具体含义是`[训练时一个batch的图片数量, 图片高度, 图片宽度, 图像通道数]`
    > 
    > 第二个参数`filter`：相当于CNN中的卷积核，要求是一个4维Tensor，具有`[filter_height, filter_width, in_channels, channel_multiplier]`这样的shape，具体含义是`[卷积核的高度，卷积核的宽度，输入通道数，输出卷积乘子]`，同理这里第三维`in_channels`，就是参数value的第四维
    > 
    > 
    > 第三个参数`strides`：卷积的滑动步长。
    > 
    > 
    > 第四个参数`padding`：string类型的量，只能是`"SAME"`,`"VALID"`其中之一，这个值决定了不同边缘填充方式。
    > 
    > 第五个参数`rate`：这个参数的详细解释见[【Tensorflow】tf.nn.atrous_conv2d如何实现空洞卷积？](http://blog.csdn.net/mao_xiao_feng/article/details/77924003)
    > 
    > 
    > 
    > 
    > 
    > 结果返回一个Tensor，shape为`[batch, out_height, out_width, in_channels * channel_multiplier]`，注意这里输出通道变成了`in_channels * channel_multiplier`
    > 
    > 为了形象的展示`depthwise_conv2d`，我们必须要建立自定义的输入图像和卷积核
    > 
    > ```python
    > img1 = tf.constant(value=[[[[1],[2],[3],[4]],[[1],[2],[3],[4]],[[1],[2],[3],[4]],[[1],[2],[3],[4]]]],dtype=tf.float32)
    > img2 = tf.constant(value=[[[[1],[1],[1],[1]],[[1],[1],[1],[1]],[[1],[1],[1],[1]],[[1],[1],[1],[1]]]],dtype=tf.float32)
    > img = tf.concat(values=[img1,img2],axis=3)
    > ```
    > 
    > ```python
    > filter1 = tf.constant(value=0, shape=[3,3,1,1],dtype=tf.float32)
    > filter2 = tf.constant(value=1, shape=[3,3,1,1],dtype=tf.float32)
    > filter3 = tf.constant(value=2, shape=[3,3,1,1],dtype=tf.float32)
    > filter4 = tf.constant(value=3, shape=[3,3,1,1],dtype=tf.float32)
    > filter_out1 = tf.concat(values=[filter1,filter2],axis=2)
    > filter_out2 = tf.concat(values=[filter3,filter4],axis=2)
    > filter = tf.concat(values=[filter_out1,filter_out2],axis=3)
    > ```
    > 建立好了img和filter，就可以做卷积了
    > 
    > ```python
    > out_img = tf.nn.conv2d(input=img, filter=filter, strides=[1,1,1,1], padding='VALID')
    > ```
    > 好了，用一张图来详细展示这个过程
    > 
    > ![](https://i.imgur.com/r2Bw6nI.jpg)
    > ![](https://i.imgur.com/yixHCYu.jpg)
    > 
    > 这是普通的卷积过程，我们再来看深度卷积。
    > 
    > ```python
    > out_img = tf.nn.depthwise_conv2d(input=img, filter=filter, strides=[1,1,1,1], rate=[1,1], padding='VALID')
    > ```
    > ![](https://i.imgur.com/vfN8yLb.jpg)
    > 
    > ![](https://i.imgur.com/glFGscn.jpg)
    > 
    > 现在我们可以形象的解释一下`depthwise_conv2d`卷积了。看普通的卷积，我们对卷积核每一个`out_channel`的两个通道分别和输入的两个通道做卷积相加，得到feature map的一个channel，而`depthwise_conv2d`卷积，我们对每一个对应的`in_channel`，分别卷积生成两个`out_channel`，所以获得的feature map的通道数量可以用`in_channel* channel_multiplier`来表达，这个`channel_multiplier`，就可以理解为卷积核的第四维。
    > 
    > 代码清单：
    > 
    > ```python
    > import tensorflow as tf  
    > 
    > img1 = tf.constant(value=[[[[1],[2],[3],[4]],[[1],[2],[3],[4]],[[1],[2],[3],[4]],[[1],[2],[3],[4]]]],dtype=tf.float32)
    > img2 = tf.constant(value=[[[[1],[1],[1],[1]],[[1],[1],[1],[1]],[[1],[1],[1],[1]],[[1],[1],[1],[1]]]],dtype=tf.float32)
    > img = tf.concat(values=[img1,img2],axis=3)filter1 = tf.constant(value=0, shape=[3,3,1,1],dtype=tf.float32)
    > filter2 = tf.constant(value=1, shape=[3,3,1,1],dtype=tf.float32)
    > filter3 = tf.constant(value=2, shape=[3,3,1,1],dtype=tf.float32)
    > filter4 = tf.constant(value=3, shape=[3,3,1,1],dtype=tf.float32)
    > filter_out1 = tf.concat(values=[filter1,filter2],axis=2)
    > filter_out2 = tf.concat(values=[filter3,filter4],axis=2)
    > filter = tf.concat(values=[filter_out1,filter_out2],axis=3) 
    > 
    > out_img = tf.nn.depthwise_conv2d(input=img, filter=filter, strides=[1,1,1,1], rate=[1,1], padding='VALID')  
    > 
    > with tf.Session() as sess:
    >      print 'rate=1, VALID mode result:'
    >      print(sess.run(out_img))
    > ```
    > 输出：
    > 
    > ```python
    > rate=1, VALID mode result:
    > [[[[  0.  36.   9.  27.]
    >    [  0.  54.   9.  27.]]
    >   [[  0.  36.   9.  27.]
    >    [  0.  54.   9.  27.]]]]
    > ```
    > 


- [python - Difference between tf.nn_conv2d and tf.nn.depthwise_conv2d - Stack Overflow](https://stackoverflow.com/questions/44226932/difference-between-tf-nn-conv2d-and-tf-nn-depthwise-conv2d)

    > For example,
    > 
    > ```python
    > input_size: (_, 14, 14, 32)
    > filter of conv2d: (3, 3, 32, 64)
    > params of conv2d filter: 3x3x32x64
    > filter of depthwise_conv2d: (3, 3, 32, 64)
    > params of depthwise_conv2d filter: 3x3x32x64
    > ```
    > 
    > suppose stride = 1 with padding, then
    > 
    > ```python
    > output of conv2d: (_, 14, 14, 64)
    > output of depthwise_conv2d: (_, 14, 14, 32*64)
    > ```
    > 
    > Some more insights:
    > 
    > -   Standard convolution operation can be split into 2 steps: depthwise convolution and reduction (sum).
    > -   Depthwise Convolution is equivalent to setting the number of group to input channel in Group Convolution.
    > -   Usually, `depthwise_conv2d` is followed by `pointwise_conv2d`(a 1x1 convolution for reduction purpose), making a `separable_conv2d`. Check [Xception](https://arxiv.org/pdf/1610.02357.pdf), [MobileNet](https://arxiv.org/pdf/1704.04861.pdf) for more details.
