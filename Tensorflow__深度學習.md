# Tensorflow__深度學習

<!-- toc --> 
[toc]


## API Reference

- [All symbols in TensorFlow  |  TensorFlow](https://www.tensorflow.org/api_docs/python/)

- [tf.placeholder  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/placeholder)

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

### Variable

- [tf.get_variable  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/get_variable)

    >Gets an existing variable with these parameters or create a new one.

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


- [DeepDreaming with TensorFlow](https://nbviewer.jupyter.org/github/tensorflow/tensorflow/blob/master/tensorflow/examples/tutorials/deepdream/deepdream.ipynb#deepdream)

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

- [python - How to print the value of a Tensor object in TensorFlow? - Stack Overflow](https://stackoverflow.com/questions/33633370/how-to-print-the-value-of-a-tensor-object-in-tensorflow)

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
    > ```python
    > I tensorflow/core/kernels/logging_ops.cc:79] This is a: [1 3]
    > ```
    > 



### Layers

- [Module: tf.layers  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers)
    - [tf.layers.conv2d  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/conv2d)
    - [tf.layers.max_pooling2d  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/max_pooling2d)
    - [tf.layers.flatten  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/flatten)
    - [tf.layers.dense  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/dense)


### Optimizer

- [tf.train.RMSPropOptimizer  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/train/RMSPropOptimizer)
    - __minimize__
      Add operations to minimize `loss` by updating `var_list`.





### RNN

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

### Graph

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




### CNN

- [tf.nn.conv2d  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/conv2d)

    > Computes a 2-D convolution given 4-D `input` and `filter` tensors.


- [tf.nn.conv2d_transpose  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/conv2d_transpose)

    > The transpose of `conv2d`.
    > 
    > This operation is sometimes called "deconvolution" after [Deconvolutional Networks](http://www.matthewzeiler.com/pubs/cvpr2010/cvpr2010.pdf), but is actually the transpose (gradient) of `conv2d` rather than an actual deconvolution.

## Tutorial

- [Tensorflow学习笔记2：About Session, Graph, Operation and Tensor - lienhua34 - 博客园](https://www.cnblogs.com/lienhua34/p/5998853.html)

    > 简介
    > ==
    > 
    > 上一篇笔记：[Tensorflow学习笔记1：Get Started](http://www.cnblogs.com/lienhua34/p/5998375.html) 我们谈到Tensorflow是基于图（Graph）的计算系统。而图的节点则是由操作（Operation）来构成的，而图的各个节点之间则是由张量（Tensor）作为边来连接在一起的。所以Tensorflow的计算过程就是一个Tensor流图。Tensorflow的图则是必须在一个Session中来计算。这篇笔记来大致介绍一下Session、Graph、Operation和Tensor。
    > 
    > Session
    > =======
    > 
    > [Session](http://www.tensorfly.cn/tfdoc/api_docs/python/client.html)提供了Operation执行和Tensor求值的环境。如下面所示，
    > 
    > 
    > ```python
    > import tensorflow as tf # Build a graph.
    > a = tf.constant([1.0, 2.0])
    > b = tf.constant([3.0, 4.0])
    > c = a * b # Launch the graph in a session.
    > sess = tf.Session() # Evaluate the tensor 'c'.
    > print sess.run(c)
    > sess.close() # result: [3., 8.]
    > ```
    > 一个Session可能会拥有一些资源，例如Variable或者Queue。当我们不再需要该session的时候，需要将这些资源进行释放。有两种方式，
    > 
    > 1.  调用session.close()方法；
    > 2.  使用with tf.Session()创建上下文（Context）来执行，当上下文退出时自动释放。
    > 
    > 上面的例子可以写成,
    > 
    > 
    > ```python
    > import tensorflow as tf # Build a graph.
    > a = tf.constant([1.0, 2.0])
    > b = tf.constant([3.0, 4.0])
    > c = a * b
    > 
    > with tf.Session() as sess: print sess.run(c)
    > ```
    > 
    > 
    > Session类的构造函数如下所示：
    > 
    > > tf.Session.\_\_init\_\_(target='', graph=None, config=None)
    > 
    > 如果在创建Session时没有指定Graph，则该Session会加载默认Graph。如果在一个进程中创建了多个Graph，则需要创建不同的Session来加载每个Graph，而每个Graph则可以加载在多个Session中进行计算。
    > 
    > 执行Operation或者求值Tensor有两种方式：
    > 
    > 1.  调用Session.run()方法： 该方法的定义如下所示，参数fetches便是一个或者多个Operation或者Tensor。
    >     
    >     > tf.Session.run(fetches, feed_dict=None)
    >     
    > 2.  调用Operation.run()或则Tensor.eval()方法： 这两个方法都接收参数session，用于指定在哪个session中计算。但该参数是可选的，默认为None，此时表示在进程默认session中计算。
    >     
    > 
    > 那如何设置一个Session为默认的Session呢？有两种方式：
    > 
    > 1\. 在with语句中定义的Session，在该上下文中便成为默认session；上面的例子可以修改成：
    > 
    > 
    > ```python
    > import tensorflow as tf # Build a graph.
    > a = tf.constant([1.0, 2.0])
    > b = tf.constant([3.0, 4.0])
    > c = a * b
    > 
    > with tf.Session(): print c.eval()
    > ```
    > 
    > 
    > 2\. 在with语句中调用Session.as_default()方法。 上面的例子可以修改成：
    > 
    > 
    > ```python
    > import tensorflow as tf # Build a graph.
    > a = tf.constant([1.0, 2.0])
    > b = tf.constant([3.0, 4.0])
    > c = a * b
    > sess = tf.Session()
    > with sess.as_default(): print c.eval()
    > sess.close()
    > ```
    > 
    > 
    > Graph
    > =====
    > 
    > Tensorflow中使用[tf.Graph](http://www.tensorfly.cn/tfdoc/api_docs/python/framework.html#Graph)类表示可计算的图。图是由操作Operation和张量Tensor来构成，其中Operation表示图的节点（即计算单元），而Tensor则表示图的边（即Operation之间流动的数据单元）。
    > 
    > > tf.Graph.\_\_init\_\_()
    > > 
    > > 创建一个新的空Graph
    > 
    > 在Tensorflow中，始终存在一个默认的Graph。如果要将Operation添加到默认Graph中，只需要调用定义Operation的函数（例如tf.add()）。如果我们需要定义多个Graph，则需要在with语句中调用Graph.as_default()方法将某个graph设置成默认Graph，于是with语句块中调用的Operation或Tensor将会添加到该Graph中。
    > 
    > 例如，
    > 
    > 
    > ```python
    > import tensorflow as tf
    > g1 = tf.Graph()
    > with g1.as_default():
    >     c1 = tf.constant([1.0])
    > with tf.Graph().as_default() as g2:
    >     c2 = tf.constant([2.0])
    > 
    > with tf.Session(graph=g1) as sess1: print sess1.run(c1)
    > with tf.Session(graph=g2) as sess2: print sess2.run(c2) # result: # [ 1.0 ] # [ 2.0 ]
    > ```
    > 
    > 
    > 如果将上面例子的sess1.run(c1)和sess2.run(c2)中的c1和c2交换一下位置，运行会报错。因为sess1加载的g1中没有c2这个Tensor，同样地，sess2加载的g2中也没有c1这个Tensor。
    > 
    > Operation
    > =========
    > 
    > 一个[Operation](http://www.tensorfly.cn/tfdoc/api_docs/python/framework.html#Operation)就是Tensorflow Graph中的一个计算节点。其接收零个或者多个Tensor对象作为输入，然后产生零个或者多个Tensor对象作为输出。Operation对象的创建是通过直接调用Python operation方法（例如tf.matmul()）或者Graph.create_op()。
    > 
    > 例如`c = tf.matmul(a, b)`表示创建了一个类型为MatMul的Operation，该Operation接收Tensor a和Tensor b作为输入，而产生Tensor c作为输出。
    > 
    > 当一个Graph加载到一个Session中，则可以调用Session.run(op)来执行op，或者调用op.run()来执行（op.run()是tf.get\_default\_session().run()的缩写）。
    > 
    > Tensor
    > ======
    > 
    > [Tensor](http://www.tensorfly.cn/tfdoc/api_docs/python/framework.html#Tensor)表示的是Operation的输出结果。不过，Tensor只是一个符号句柄，其并没有保存Operation输出结果的值。通过调用Session.run(tensor)或者tensor.eval()方可获取该Tensor的值。
    > 
    > [](https://github.com/lienhua34/notes/blob/master/tensorflow/2.about_session_graph_operation_tensor.md#关于tensorflow的图计算过程)关于Tensorflow的图计算过程
    > ============================================================================================================================================
    > 
    > 我们通过下面的代码来看一下Tensorflow的图计算过程：
    > 
    > 
    > ```python
    > import tensorflow as tf
    > a = tf.constant(1)
    > b = tf.constant(2)
    > c = tf.constant(3)
    > d = tf.constant(4)
    > add1 = tf.add(a, b)
    > mul1 = tf.mul(b, c)
    > add2 = tf.add(c, d)
    > output = tf.add(add1, mul1)
    > with tf.Session() as sess: print sess.run(output) 
    > # result: 9
    > ```
    > 
    > 
    > 上面的代码构成的Graph如下图所示，
    > 
    >  [![graph_compute_flow](https://github.com/lienhua34/notes/raw/master/tensorflow/asserts/graph_compute_flow.jpg)](https://github.com/lienhua34/notes/blob/master/tensorflow/asserts/graph_compute_flow.jpg)
    > 
    > 当Session加载Graph的时候，Graph里面的计算节点都不会被触发执行。当运行sess.run(output)的时候，会沿着指定的Tensor output来进图路径往回触发相对应的节点进行计算（图中红色线表示的那部分）。当我们需要output的值时，触发Operation tf.add(add1, mul1)被执行，而该节点则需要Tensor add1和Tensor mul1的值，则往回触发Operation tf.add(a, b)和Operation tf.mul(b, c)。以此类推。
    > 
    > 所以在计算Graph时，并不一定是Graph中的所有节点都被计算了，而是指定的计算节点或者该节点的输出结果被需要时。
    > 
    > (done)

    
## Solve Math problem

- [一个利用Tensorflow求解几何问题的例子 - naughty的个人页面](https://my.oschina.net/taogang/blog/1627590?from=20180304)



## DNN

### Before everything start, just remember ...
1. graph = container
2. sess = liquid

### Constant, Placeholder, and Variables
1. constant: fixed item. the value cannot be changed during training
2. placeholder: we can pass item to the graph interactively. (common used for input, ground truth label, and other flags)
3. variable: dynamic item. the value can be changed during training. (need to be initialized for each session)


- constant no need to initial

    ```python
    sess = tf.Session() # start a session

    # constant: fixed item, rarely used, the value cannot be changed during training
    a = tf.constant([[1, 2], [3, 4]], dtype=tf.float32)
    print(a)
    print(sess.run(a))
    ```

- variable need to initial

    ```python
    # variable: we alwayes use this. the value can change during training
    c = tf.Variable([[1, 2], [3, 4]], dtype=tf.float32)

    # initial variables: 使用 variable 之前必須先初始化
    init = tf.global_variables_initializer()
    sess.run(init)

    sess.run(c)
    ```

- palceholder is used for dynamic assign variables

    ```python
    # placeholder: used very often!
    b = tf.placeholder(shape=[2,3], dtype=tf.float32) # placehodler 只能塞進跟定義好的shape 相同的array

    my_input_array = np.array([[1,1,1],[2,4,6]])

    sess.run(b, feed_dict={b: my_input_array }) # 使用dict 將my_input_array assign 給 b 這個 placeholder
    ```


### Basic Math

- tf.matmul
- tf.multiply
- tf.add
- ...


```python
x1 = tf.Variable([[1,2], [3,4]], dtype= tf.float32)
x2 = tf.Variable([[5,6], [7,8]], dtype= tf.float32)

mat_mul_ops = tf.matmul(x1, x2) # np.dot
element_wise_mul_ops = tf.multiply(x1, x2) # element-wise mul
add_ops = tf.add(x1, x2)

init = tf.global_variables_initializer()
sess.run(init)

res1, res2, res3 = sess.run([mat_mul_ops, element_wise_mul_ops, add_ops])
print(res1)
print("---")
print(res2)
print("---")
print(res3)
```

- tf.reduce_sum
- tf.reduce_mean
- ...

```python
take_sum_1 = tf.reduce_sum(x1, axis=0) # np.sum
take_sum_2 = tf.reduce_sum(x1, axis=1)
take_sum_3 = tf.reduce_sum(x1)
take_mean_1 = tf.reduce_mean(x1, axis = 0) # np.mean
take_mean_2 = tf.reduce_mean(x1, axis = 1)
take_mean_3 = tf.reduce_mean(x1)

sess.run(tf.global_variables_initializer())
print(sess.run(x1))
print('---')
print(sess.run(take_sum_1))
print(sess.run(take_sum_2))
print(sess.run(take_sum_3))
print(sess.run(take_mean_1))
print(sess.run(take_mean_2))
print(sess.run(take_mean_3))
```


- tf.assign
- ...

```python
index_counter = tf.Variable(0)
one = tf.constant(1)

new_index = tf.add(index_counter, one)
update_ops = tf.assign(index_counter, new_index) # if the value change, you have to "assign" it

init = tf.global_variables_initializer()
sess.run(init)
for _ in np.arange(10):
    sess.run(new_index) # 沒有assign 結果就是不會更新
    sess.run(update_ops)
    print(sess.run(index_counter))
```

#### A linear regression example

```python
# 將先前的 graph 清除
tf.reset_default_graph() 

# 產生 y=3x+b 包含雜訊的資料
x_in = np.linspace(0, 1, 100)
y_true = (3 * x_in) + np.random.rand(len(x_in))
plt.plot(x_in, y_true, 'b.')
plt.show()

## build the regression fomula
# 隨機初始化 w, b
w1 = tf.Variable(tf.random_uniform([1], -1.0, 1.0), dtype= tf.float32)
b1 = tf.Variable(tf.zeros([1]))

# 預測結果
y_pred = (w1 * x_in) + b1
# 計算 loss
loss = tf.reduce_mean(tf.square(y_pred - y_true))

# 最佳化方法: 使用梯度下降
optim = tf.train.GradientDescentOptimizer(0.1)
# 最小化 loss
train_ops = optim.minimize(loss)

## train the model
sess = tf.Session()
init = tf.global_variables_initializer()
sess.run(init)

for step in np.arange(500):
    # 執行一次 train_ops 定義的流程
    sess.run(train_ops)
    if step % 25 == 0:
        # 印出 w1, b1
        print('step: ' + str(step) + ', weight: ' + str(sess.run(w1)[0]) + ' bias: ' + str(sess.run(b1)[0]) )

# 執行 y_pred 定義的流程，得到預測結果
y_out = sess.run(y_pred)

plt.plot(y_true, y_out, 'r.')
plt.show()

plt.plot(x_in, y_true, 'b.')
plt.plot(x_in, y_out, 'r.')
plt.show()

sess.close()
```

### General writing flow


#### Import required libries and set some parameters

```python
from sklearn.model_selection import train_test_split
from sklearn.utils import shuffle
import numpy as np
import os
import argparse
from tqdm import tqdm
import matplotlib.pyplot as plt
import pprint as pprint
```

```python
parser = argparse.ArgumentParser()
parser.add_argument('--batch_size', default = 32, type = int)
parser.add_argument('--epochs', default = 100, type = int)
parser.add_argument('--lr', default = 0.001, type = float)
parser.add_argument('--train_ratio', default = 0.9, type = float)

FLAGS = parser.parse_args([]) # if not jupyter notebook, remove [reference link]
```



```python
# You should always set visible devices before import tensorflow
#os.environ['CUDA_VISIBLE_DEVICES'] = str(FLAGS.gpu_id)
import tensorflow as tf
```


#### Load data and do some pre-processing


- We use MNIST HERE (with sklearn 8x8 version rather than use tensorflow 28x28 version)

    ```python
    from sklearn.datasets import load_digits
    # load data
    digits = load_digits()
    x_, y_ = digits.data, digits.target

    # do data pre-processing
    x_ = x_ / x_.max()

    y_one_hot = np.zeros((len(y_), 10))
    y_one_hot[np.arange(len(y_)), y_] = 1
    ```

#### split your data into training and validation sets

- use train_test_split

    ```python
    from sklearn.model_selection import train_test_split

    x_train, x_test, y_train, y_test = train_test_split(x_, 
                                                        y_one_hot, 
                                                        test_size = 0.05, 
                                                        stratify  = y_)

    x_train, x_valid, y_train, y_valid = train_test_split(x_train, 
                                                          y_train, 
                                                          test_size = 1.0 - FLAGS.train_ratio,
                                                          stratify = y_train.argmax(axis = 1))
    print("training set data dimension")
    print(x_train.shape)
    print(y_train.shape)
    print("-----------")
    print("training set: %i" % len(x_train))
    print("validation set: %i" % len(x_valid))
    print("testing set: %i" % len(x_test))
    ```

- use custom defined generator

    ```python
    from sklearn.utils import shuffle 

    def simpson_train_batch_generator(x, y, bs, shape):
        x_train = np.array([]).reshape((0, shape))
        y_train = np.array([]).reshape((0, y.shape[1]))
        while True:
            new_ind = shuffle(range(len(x)))
            x = x.take(new_ind)
            y = np.take(y, new_ind, axis=0)
            for i in range(len(x)):
                dir_img = '/data/examples/simpson_preproc/' + x.img.iloc[i]
                img = cv2.imread(dir_img, 0)
                img = cv2.resize(img, (50,50))
                x_train = np.row_stack([x_train, img.flatten()])
                y_train = np.row_stack([y_train, y[i]])
                if x_train.shape[0] == bs:
                    x_batch = x_train.copy()
                    x_batch /= 255.
                    y_batch = y_train.copy()
                    x_train = np.array([]).reshape((0 ,shape))
                    y_train = np.array([]).reshape((0 ,y.shape[1]))        
                    yield x_batch, y_batch # allenlylee: yield 語法，類似 return，但回傳值後不會清除 call stack，
                                           # 當下一次執行 generator.next() 時，就會從這裏的下一行開始執行
    ```




#### build the network

- step 1: define placeholder

    without Regularization:

    ```python
    #### define placeholder ####
    input_data = tf.placeholder(dtype=tf.float32, 
                               shape=[None, img.shape[0]],
                               name='input_data')

    y_true = tf.placeholder(dtype=tf.float32, 
                            shape=[None, y_train.shape[1]],
                            name='y_true')
    ```

    with Regularization:
    
    ```python
    l2 = tf.placeholder(dtype=tf.float32, name = 'l2_regulizers')
    ```

- step 2: create variables and operations

    without Regularization:

    ```python
    #### define variables(weight/bias) ####
    x1 = tf.layers.dense(input_data, 256, activation=tf.nn.relu, name='hidden1')
    x2 = tf.layers.dense(x1, 256, activation=tf.nn.relu, name='hidden2')
    x3 = tf.layers.dense(x2, 128, activation=tf.nn.relu, name='hidden3')
    x4 = tf.layers.dense(x3, 128, activation=tf.nn.relu, name='hidden4')
    x5 = tf.layers.dense(x4, 64, activation=tf.nn.relu, name='hidden5')
    x6 = tf.layers.dense(x5, 64, activation=tf.nn.relu, name='hidden6')
    out = tf.layers.dense(x6, y_train.shape[1], name='output')

    y_pred = out
    ```

    with Regularization:

    ```python
    #### define variables(weight/bias) ####
    x1 = tf.layers.dense(input_data, 
                         256, 
                         activation=tf.nn.relu, 
                         name='hidden1', 
                         kernel_regularizer=tf.contrib.layers.l2_regularizer(scale=l2))
    x2 = tf.layers.dense(x1, 
                         128, 
                         activation=tf.nn.relu, 
                         name='hidden2',
                         kernel_regularizer=tf.contrib.layers.l2_regularizer(scale=l2))
    x3 = tf.layers.dense(x2, 
                         64, 
                         activation=tf.nn.relu, 
                         name='hidden3',
                         kernel_regularizer=tf.contrib.layers.l2_regularizer(scale=l2))
    out = tf.layers.dense(x3, y_train.shape[1], name='output')

    y_pred = tf.nn.softmax(out)
    ```

- step 3: define loss function and calculate loss

    without Regularization:

    ```python
    #### calculate loss ####
    loss = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(labels=y_true, logits=y_pred))
    #loss = tf.reduce_mean(tf.square(y_pred-y_true)) # MSE
    ```

    with Regularization:

    ```python
    #### calculate loss ####
    cross_entropy = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(labels=y_true, logits=out))

    #### optimize variables ####
    opt = tf.train.AdamOptimizer(learning_rate=0.001)

    reg = tf.get_collection(tf.GraphKeys.REGULARIZATION_LOSSES)
    loss = cross_entropy + tf.reduce_sum(reg)
    update = opt.minimize(loss)
    ```


- step 4: define optimizer and define variables update operations

    ```python
    #### optimize variables ####
    #opt = tf.train.GradientDescentOptimizer(learning_rate=0.001)
    opt = tf.train.AdamOptimizer(learning_rate=0.001)

    update = opt.minimize(loss)
    ```

- check global variables (optional)

    ```python
    tf.global_variables() ## 檢查 graph 裏的 global variables
    ```

- with low-level tensor elements

    ```python
    tf.reset_default_graph() # clean graph
    # Declare the input node
    with tf.name_scope('input'):
        x_input = tf.placeholder(shape = (None,x_train.shape[1]), 
                                 name = 'x_input',
                                 dtype=tf.float32)
        y_out = tf.placeholder(shape = (None, y_train.shape[1]), 
                               name = 'y_label',
                               dtype=tf.float32)

    with tf.variable_scope('hidden_layer1'):
        # tf.get_variable 與 tf.Variable 功能一樣，只是 tf.get_variable 可以 reuse，
        # 可以指定變數名稱，如果先前有定義過，就會抓出來用，否則自動生成一個
        w1 = tf.get_variable('weight1', 
                             shape= [x_train.shape[1], 30], # allenyllee: 這一層希望有30 個neuron 的輸出
                             dtype=tf.float32, 
                             initializer=tf.truncated_normal_initializer(stddev=0.1))
        b1 = tf.Variable(tf.zeros(shape=[w1.shape[1]])) # allenyllee: 需要跟 neuron 輸出的數量一致
        x_h1 = tf.nn.relu(tf.add(tf.matmul(x_input, w1), b1))


    with tf.variable_scope('hidden_layer2'):
        # tf.get_variable 與 tf.Variable 功能一樣，只是 tf.get_variable 可以 reuse，
        # 可以指定變數名稱，如果先前有定義過，就會抓出來用，否則自動生成一個
        w2 = tf.get_variable('weight2', 
                             shape= [x_h1.shape[1], 25], # allenyllee: 這一層希望有25 個neuron 的輸出
                             dtype=tf.float32, 
                             initializer=tf.truncated_normal_initializer(stddev=0.1))
        b2 = tf.Variable(tf.zeros(shape=[w2.shape[1]])) # allenyllee: 需要跟 neuron 輸出的數量一致
        x_h2 = tf.nn.relu(tf.add(tf.matmul(x_h1, w2), b2))

    with tf.variable_scope('hidden_layer3'):
        # tf.get_variable 與 tf.Variable 功能一樣，只是 tf.get_variable 可以 reuse，
        # 可以指定變數名稱，如果先前有定義過，就會抓出來用，否則自動生成一個
        w3 = tf.get_variable('weight3', 
                             shape= [x_h2.shape[1], 20], # allenyllee: 這一層希望有20 個neuron 的輸出
                             dtype=tf.float32, 
                             initializer=tf.truncated_normal_initializer(stddev=0.1))
        b3 = tf.Variable(tf.zeros(shape=[w3.shape[1]])) # allenyllee: 需要跟 neuron 輸出的數量一致
        x_h3 = tf.nn.relu(tf.add(tf.matmul(x_h2, w3), b3))

    with tf.variable_scope('output_layer'):

        print(type(x_h3.shape[1]))  # return Dimension object, in order to use in tf.truncated_normal,
                                    # need to cast into int type
                                    # use x_h3.shape[1].value to get its value

        wo = tf.Variable(tf.truncated_normal(shape=[x_h3.shape[1].value, y_train.shape[1]],stddev=0.1), # 上一層有20 個輸出，所以要20 個輸入
                         dtype = tf.float32)
        bo = tf.get_variable('bias2', 
                             shape=[y_train.shape[1]], 
                             dtype=tf.float32, 
                             initializer=tf.constant_initializer(0.0))
        output = tf.add(tf.matmul(x_h3, wo), bo)

    with tf.name_scope('cross_entropy'):
        loss = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(logits=output, labels=y_out))

    with tf.name_scope('accuracy'):
        # 因為output 有10 個，使用argmax 找出值最大的index，如果 predict 結果與原始 label 一樣，表示預測正確
        correct_prediction = tf.equal(tf.argmax(tf.nn.softmax(output),1), tf.argmax(y_out,1)) 
        compute_acc = tf.reduce_mean(tf.cast(correct_prediction, tf.float32))

    with tf.name_scope('train'):
        train_step = tf.train.AdamOptimizer(learning_rate=FLAGS.lr).minimize(loss)
    ```


- with "tf.layers" 

    ```python
    tf.reset_default_graph() # clean graph
    # Declare the input node
    with tf.name_scope('input'):
        x_input = tf.placeholder(shape = (None,x_train.shape[1]), 
                                 name = 'x_input',
                                 dtype=tf.float32)
        y_out = tf.placeholder(shape = (None, y_train.shape[1]), 
                               name = 'y_label',
                               dtype=tf.float32)

    # Declare the network structure
    with tf.variable_scope('hidden_layer1'):
        x_h1 = tf.layers.dense(inputs= x_input, units= 30, activation=tf.nn.relu)

    # Declare the network structure
    with tf.variable_scope('hidden_layer2'):
        x_h2 = tf.layers.dense(inputs= x_h1, units= 25, activation=tf.nn.relu)

    # Declare the network structure
    with tf.variable_scope('hidden_layer3'):
        x_h3 = tf.layers.dense(inputs= x_h2, units= 20, activation=tf.nn.relu)

    with tf.variable_scope('output_layer'):
        output = tf.layers.dense(x_h3, 10) # 這裡不需要再加上 softmax, 因為計算 loss 時已經包含了

    with tf.name_scope('cross_entropy'):
        loss = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(logits=output, labels=y_out))

    with tf.name_scope('accuracy'):
        correct_prediction = tf.equal(tf.argmax(tf.nn.softmax(output),1), tf.argmax(y_out,1))
        compute_acc = tf.reduce_mean(tf.cast(correct_prediction, tf.float32))

    with tf.name_scope('train'):
        train_step = tf.train.AdamOptimizer(learning_rate=FLAGS.lr).minimize(loss)
    ```

#### run session

- step 1: run global variables initialization

```python
#### init ####
init = tf.global_variables_initializer()

sess = tf.Session()
sess.run(init)
```

- step 2: run session to update the variables

    without Regularization:
    
    ```python
    from tqdm import tqdm_notebook
    from sklearn.metrics import accuracy_score

    epoch = 100
    bs = 32
    update_per_epoch = 100

    tr_loss = list()
    tr_acc = list()
    train_gen = simpson_train_batch_generator(x_train_list, y_train, bs, img.shape[0])

    print('start modelling!')

    for i in range(epoch):

        #### calculate training loss & update variables ####
        training_loss = 0
        training_acc = 0
        bar = tqdm_notebook(range(update_per_epoch))

        for j in bar:

            x_batch, y_batch = next(train_gen)

            tr_pred, training_loss_batch, _ = sess.run([y_pred, loss, update], feed_dict={
                input_data:x_batch,
                y_true:y_batch
            })

            training_loss += training_loss_batch

            training_acc_batch = accuracy_score(np.argmax(y_batch, axis=1), np.argmax(tr_pred, axis=1))
            training_acc += training_acc_batch

            if j % 5 == 0:
                bar.set_description('loss: %.4g' % training_loss_batch)

        training_loss /= update_per_epoch
        training_acc /= update_per_epoch

        tr_loss.append(training_loss)
        tr_acc.append(training_acc)

        print('epoch {epochs}: training loss {training_loss}'.format(
                epochs=(i+1), 
                training_loss=training_loss))
    ```

    with Regularization:

    ```python
    for l2_iter in [0.0, 0.5, 0.05, 0.005, 0.0005]:
    
        tr_pred, training_loss_batch, _ = sess.run([y_pred, loss, update], feed_dict={
        input_data:x_batch,
        y_true:y_batch,
        l2: l2_iter})
    ```

- Train the model and collect the performance

```python
train_loss_list, valid_loss_list = [], []
train_acc_list, valid_acc_list = [], []

with tf.Session() as sess:
    # we have to initalize all variables (e.g. weights/biases) at the begin
    sess.run([tf.global_variables_initializer()])
    # writer = tf.summary.FileWriter("./graph/", sess.graph)
    for i in tqdm(range(FLAGS.epochs)):
        # get batch 
        total_batch = int(np.floor(len(x_train) / FLAGS.batch_size)) # just drop last few sample ...
        
        train_loss_collector, train_acc_collector = [], []
        for j in np.arange(total_batch):
            batch_idx_start = j * FLAGS.batch_size
            batch_idx_stop = (j+1) * FLAGS.batch_size

            x_batch = x_train[batch_idx_start : batch_idx_stop]
            y_batch = y_train[batch_idx_start : batch_idx_stop]
            
            this_loss, this_acc, _ = sess.run([loss, compute_acc, train_step],
                                    feed_dict = {x_input: x_batch,
                                                 y_out: y_batch})
            train_loss_collector.append(this_loss)
            train_acc_collector.append(this_acc)
            
        # do validation at the end of each epoch
        valid_acc, valid_loss = sess.run([compute_acc, loss],
                                         feed_dict = {x_input: x_valid,
                                                      y_out : y_valid})
        valid_loss_list.append(valid_loss)
        valid_acc_list.append(valid_acc)
        train_loss_list.append(np.mean(train_loss_collector))
        train_acc_list.append(np.mean(train_acc_collector))

        # at the end of each epoch, shuffle the data
        x_train, y_train = shuffle(x_train, y_train)
    # At the end of the training, do testing set
    test_acc, test_loss = sess.run([compute_acc, loss],
                                    feed_dict = {x_input: x_test,
                                                 y_out : y_test})
print('--- training done ---')
print('testing accuracy: %.2f' % test_acc)

plt.plot(np.arange(len(train_loss_list)), train_loss_list, 'b', label = 'train')
plt.plot(np.arange(len(valid_loss_list)), valid_loss_list, 'r', label = 'valid')
plt.legend()
plt.show()

plt.plot(np.arange(len(train_acc_list)), train_acc_list, 'b', label = 'train')
plt.plot(np.arange(len(valid_acc_list)), valid_acc_list, 'r', label = 'valid')
plt.legend(loc = 4)
plt.show()
```

#### plot model training result

```python
plt.figure(1)
plt.subplot(121)
plt.plot(range(len(tr_loss)), tr_loss, label='training')
plt.title('Loss')
plt.legend(loc='best')
plt.subplot(122)
plt.plot(range(len(tr_acc)), tr_acc, label='training')
plt.title('Accuracy')
```



#### Save Model

- save model to disk

    ```python
    saver = tf.train.Saver()
    saver.save(sess, "saved_models/model.ckpt")
    ```
    
- print current loss

    ```python
    print(sess.run(loss, feed_dict={
                input_data:x_batch,
                y_true:y_batch
            }))
    ```

- clean graph

    ```python
    tf.reset_default_graph()
    tf.global_variables()
    ```

#### Load Model

- load model 之前要先回到前面重建Graph，建好之後再call restore

    ```python
    #rerun the graph
    # allenyllee: 要回到 step1 重建 Graph
    sess = tf.Session()
    saver = tf.train.Saver()
    saver.restore(sess, "saved_models/model.ckpt")
    ```

- 檢查 global variable 是否一致

    ```python
    tf.global_variables()
    ```

- 檢查loss是否與先前一致

    ```python
    print(sess.run(loss, feed_dict={
                input_data:x_batch,
                y_true:y_batch
            }))
    ```
        
### DNN 訓練建議

#### 選擇 Loss Function

- Classification 常用 cross-entropy 當作 loss function

- Regression 則常用 MSE 當作 loss function

- 一般不會用 classification error 來做 loss function , 因為他沒辦法有效衡量模型的好壞

#### 如何選擇 Activation Function

- Sigmoid, Tanh, Softsign
    - Vanishing gradient problem
    原因 : input 被壓縮到一個相對很小的 output range 
    結果 : 很大的 input 變化只能產生很小的 output 變化
            ➔ Gradient 小 ➔ 無法有效地學習
    特別不適用於深的深度學習模型

- ReLU

    當輸入 x 都小於 0，ReLU 就不再更新 
    df/dx = 0 if x < 0.
    可能因為 Learning rate 大 或是 batch size 小 

- 其他
    - Softplus
    - Leaky ReLU (tf.nn.leaky_relu)
    - ELU (tf.nn.elu)
    - SeLU (tf.nn.selu)

- Hidden layers 
    - 通常會用 ReLU

- Output layer
    - Regression 
        常用 linear 
    - Classification 
        Output layer 常用 softmax

#### 選擇 Learning Rate

- 大多要試試看才知道，通常不會大於 0.1
- 一次調一個數量級 
    0.1 ➔ 0.01 ➔ 0.001

#### 選擇 Optimizers

- SGD - tf.train.GradientDescentOptimizer  
- Momentum - tf.train.MomentumOptimizer  
- Adagrad - tf.train.AdagradOptimizer  
- RMSprop - tf.train.RMSPropOptimizer  
- Adam - tf.train.AdamOptimizer

### 避免 Overfitting

#### Regularization

- 限制 weights 的大小讓 output 曲線比較平滑

    怎麼限制 weights 的大小呢？ 
    加入目標函數中，一起優化 
    - α 是用來調整 regularization 的比重 
    - 避免顧此失彼 (降低 weights 的大小而犧牲模型準確性)

    L1 norm 
        - Sum of absolute values 

    L2 norm 
        - Root mean square of absolute values

#### Early Stopping

- 假如能早點停下來就好了

    ![](https://screenshotscdn.firefoxusercontent.com/images/a69f1a06-09f4-4c8c-bb37-d70e7683241a.png)

        
#### Dropout

- What is Dropout?  
    - 原本為 neurons 跟 neurons 之間為 fully connected  
    - 在訓練過程中，隨機拿掉一些連結 (weight 設為0)

- 會造成 training performance 變差 
    - 用全部的 neurons 原本可以做到 
    - 只用某部分的 neurons 只能做到 
    - Error 變大 ➔ 各 neuron 修正較多 ➔ 各 neuron 有機會做得越好

- 不要一開始就加入 Dropout
    - Dropout 會讓 training performance 變差
    - Dropout 是在避免 overfitting

![](https://screenshotscdn.firefoxusercontent.com/images/be407fed-ace8-49d5-8997-8f2351a31d90.png)
        
        
## CNN

影像問題，優先考慮 CNN


### CNN in tensorflow

- normalize for data

    ```python
    x = (x - np.min(x)) / np.max(x)
    ```

- One-hot encode for label

    ```python
    y = np.eye(10,dtype=int)[x]
    ```

- import tensorflow

    ```python
    import tensorflow as tf
    ```

- Create place holder

    ```python
    # data x
    shpae_t = np.append(None,image_shape) # image_shape with batch size set to None
    placeholder_t = tf.placeholder(tf.float32, shape=shpae_t, name="x") # Name the TensorFlow placeholder "x" 
    
    # label y
    shpae_t = np.append(None,n_classes) # n_classes with batch size set to None
    placeholder_t = tf.placeholder(tf.float32, shape=shpae_t, name="y")

    # dropout keep probability
    shpae_t = None
    placeholder_t = tf.placeholder(tf.float32, shape=shpae_t, name="keep_prob")
    ```

- Convolution and Max Pooling Layer

    ```python
    # convolution layer with input "x_tensor", number of filters (outputs) "conv_num_outputs", 
    # kernel_size "conv_ksize", strides "conv_strides", padding "same", activation function "tf.nn.relu"
    conv_layer = tf.layers.conv2d(inputs=x_tensor, filters=conv_num_outputs, kernel_size=conv_ksize, 
                                    strides=conv_strides, padding='same', activation=tf.nn.relu)

    # maxpool layer with inputs "conv_layer" generated in last step, pool_size "pool_ksize", 
    # strides "pool_strides", padding "same"
    maxpool_layer = tf.layers.max_pooling2d(inputs=conv_layer, pool_size=pool_ksize, 
                                                strides=pool_strides, padding='same')
    ```
    
- Flatten Layer
    ```python
    # flatten of x_tensor
    flatten_layer = tf.layers.flatten(inputs=x_tensor)
    ```
    
- Fully-Connected Layer

    ```python
    # fully-connected layer with inputs "x_tensor", units (number of output) "num_outputs"
    # activation function "tf.nn.relu"
    dense_layer = tf.layers.dense(inputs=x_tensor, units=num_outputs, activation=tf.nn.relu)
    ```

- dropout

    ```python
    dense_layer = tf.nn.dropout(dense_layer, keep_prob=keep_prob)
    ```

- Outpur layer

    ```python
    # output layer with inputs "x_tensor", units (number of output) "num_outputs"
    # linear activation function 
    output_layer = tf.layers.dense(inputs=x_tensor, units=num_outputs)
    ```
    
- Build the Neural Network 

    ```python
    # Remove previous weights, bias, inputs, etc..
    tf.reset_default_graph()

    # Inputs
    x = neural_net_image_input((32, 32, 3))
    y = neural_net_label_input(10)
    keep_prob = neural_net_keep_prob_input()

    # Model 的 outpur (注意！這時候還沒有經過 softmax function，這些 output 的值通常稱為 logits)
    logits = conv_net(x, keep_prob)

    # Name logits Tensor, so that is can be loaded from disk after training
    logits = tf.identity(logits, name='logits')

    # Loss and Optimizer
    # 此時透過 softmax_cross_entropy_with_logits 將 model output 的值經過 softmax，再與我們的 label 計算 cross-entropy
    cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(logits=logits, labels=y))
    optimizer = tf.train.AdamOptimizer().minimize(cost)

    # Accuracy
    correct_pred = tf.equal(tf.argmax(logits, 1), tf.argmax(y, 1))
    accuracy = tf.reduce_mean(tf.cast(correct_pred, tf.float32), name='accuracy')
    ```

- train network

    ```python
    session.run(optimizer, feed_dict={x: feature_batch, 
                                      y: label_batch, 
                                      keep_prob: keep_probability})
    ```

- save model

    ```python
    # Save Model
    saver = tf.train.Saver()
    save_path = saver.save(sess, save_model_path)
    ```

- load model

    ```python
    # Load model
    loader = tf.train.import_meta_graph(save_model_path + '.meta')
    loader.restore(sess, save_model_path)

    # Get Tensors from loaded model
    loaded_x = loaded_graph.get_tensor_by_name('x:0')
    loaded_y = loaded_graph.get_tensor_by_name('y:0')
    loaded_keep_prob = loaded_graph.get_tensor_by_name('keep_prob:0')
    loaded_logits = loaded_graph.get_tensor_by_name('logits:0')
    loaded_acc = loaded_graph.get_tensor_by_name('accuracy:0')
    ```

- get testing accuracy

    ```python
    for train_feature_batch, train_label_batch in helper.batch_features_labels(test_features, test_labels, batch_size):
        test_batch_acc_total += sess.run(
            loaded_acc,
            feed_dict={loaded_x: train_feature_batch, loaded_y: train_label_batch, loaded_keep_prob: 1.0})
        test_batch_count += 1

    print('Testing Accuracy: {}\n'.format(test_batch_acc_total/test_batch_count))
    ```

### CNN in Karas

- load data

    ```python
    # this function is provided from the official site
    from keras.datasets import cifar10
    # read train/test data
    (x_train, y_train), (x_test, y_test) = cifar10.load_data()
    # check the data shape
    print("x_train shape:", x_train.shape)
    print("numbers of training smaples:", x_train.shape[0])
    print("numbers of testing smaples:", x_test.shape[0])
    ```

- show images

    ```python
    import matplotlib.pyplot as plt
    %matplotlib inline
    # show the first image of training data
    plt.imshow(x_train[0])
    # show the first image of testing data
    plt.imshow(x_test[0])
    ```

- build CNN model

    ```python
    from keras.models import Sequential
    from keras.layers import Dense, Dropout, Activation, Flatten
    from keras.layers import Conv2D, MaxPooling2D

    # declare sequential model
    model = Sequential()

    # CNN part
    model.add(Conv2D(64, (3, 3), padding='same',
                     input_shape=x_train.shape[1:]))
    model.add(Activation('relu'))
    model.add(Conv2D(128, (3, 3)))
    model.add(Activation('relu'))
    model.add(MaxPooling2D(pool_size=(2, 2)))
    model.add(Dropout(0.25))

    # DNN part
    model.add(Flatten())
    model.add(Dense(512))
    model.add(Activation('relu'))
    model.add(Dropout(0.5))
    model.add(Dense(num_classes))
    model.add(Activation('softmax'))
    ```

- check model parameter

    ```python
    print(model.summary())
    ```
    
    - 第一層為 3\*3 卷積，32 個 filter，作用在3個顏色通道，最後再加上32個 bias => 共 3\*3\*32\*3+32 個參數

    - 第二層為 3\*3 卷積，32 個 filter，作用在上一層 32 個 feature map，最後再加上32個 bias => 共 3\*3\*32\*32+32 個參數

    - DNN 第一層的輸入為 CNN 最後輸出攤平成一維向量，共7200維，輸出512個神經元，加上512個 bias => 共7200\*512+512 個參數
    ![](https://screenshotscdn.firefoxusercontent.com/images/03f5292b-23bd-4548-9c1a-4acad0412d68.png)

- Model Compilation

    ```python
    # initiate Adam optimizer
    opt = keras.optimizers.Adam()

    # Let's train the model using Adam
    model.compile(loss='categorical_crossentropy',
                  optimizer=opt,
                  metrics=['accuracy'])
    ```

- training

    ```python
    # define batch size and # of epoch
    batch_size = 32 # or 64 or 128
    epoch = 10
    # [2] validation data comes from testing data
    model_history = model.fit(x_train, y_train,
    batch_size=batch_size, epochs=epoch, shuffle=True,
    validation_data=(x_test, y_test))
    ```
- set model path

    ```python
    import os
    save_dir = os.path.join(os.getcwd(), 'saved_models')
    model_name = 'keras_cifar10_trained_model.h5'

    if not os.path.isdir(save_dir):
        os.makedirs(save_dir)

    model_path = os.path.join(save_dir, model_name)
    ```
- save model

    ```python
    # saving model
    model.save(model_path)
    del model
    ```

- callback (Checkpoint + Earlystopping)

    ```python
    from keras.callbacks import EarlyStopping, ModelCheckpoint

    checkpoint = ModelCheckpoint(model_path, monitor='val_loss', save_best_only=True, verbose=1)
    earlystop = EarlyStopping(monitor='val_loss', patience=5, verbose=1)

    model.fit(x_train, y_train,
        callbacks=[checkpoint, earlystop])
    ```

- Data augmentation

    ```python
    from keras.preprocessing.image import ImageDataGenerator

    # This will do preprocessing and realtime data augmentation:
    datagen = ImageDataGenerator(
        rotation_range=30,  # randomly rotate images in the range (degrees, 0 to 180)
        width_shift_range=0.1,  # randomly shift images horizontally (fraction of total width)
        height_shift_range=0.1,  # randomly shift images vertically (fraction of total height)
        horizontal_flip=True,  # randomly flip images
        vertical_flip=False)  # randomly flip images

    model.fit_generator(datagen.flow(x_train, y_train))
    ```

- training (with dada generater)

    ```python
    # Fit the model on the batches generated by datagen.flow().
    model_history = model.fit_generator(
        datagen.flow(x_train, y_train, batch_size=batch_size),
        epochs=epochs,
        validation_data=(x_test, y_test),
        workers=4,
        callbacks=[checkpoint, earlystop])
    ```

- load model

    ```python
    # loading our save model
    from keras.models import load_model
    print("Loading trained model")
    model = load_model(model_path)
    ```
    
- prediction

    ```python
    # prediction
    y_pred = model.predict_classes(x_test, batch_size, verbose=0)
    ```

- plot training history

    ```python
    training_loss = model_history.history['loss']
    val_loss = model_history.history['val_loss']

    plt.plot(training_loss, label="training_loss")
    plt.plot(val_loss, label="validation_loss")
    plt.xlabel("Epochs")
    plt.ylabel("Loss")
    plt.title("Learning Curve")
    plt.legend(loc='best')
    plt.show()
    ```

### CNN 架構建議

- 建議使用 3x3 的 filters size
- filters 數量應該要越來越多 64 > 128 > 256
- 盡量別做太多的 Maxpooling 以免丟失過多訊息
- 使用 Data-augmentation 增加資料量
- 使用 Earlystop 避免 Overfitting
- 若嚴重 Overfitting 可嘗試 dropout, L2 regularization


## Callback function

- [deep-learning-experiments/cat_dog_tf_v4_AddCallBacks.ipynb at master · vashineyu/deep-learning-experiments](https://github.com/vashineyu/deep-learning-experiments/blob/master/Tut_cats-dogs/cat_dog_tf_v4_AddCallBacks.ipynb)
- 

## Visualizing TensorFlow

- [Visualizing TensorFlow Graphs in Jupyter Notebooks](https://blog.jakuba.net/2017/05/30/tensorflow-visualization.html)

- [Simple way to visualize a TensorFlow graph in Jupyter? - Stack Overflow](https://stackoverflow.com/questions/38189119/simple-way-to-visualize-a-tensorflow-graph-in-jupyter)


- [TensorBoard: Graph Visualization  |  TensorFlow](https://www.tensorflow.org/programmers_guide/graph_viz)

    > TensorFlow computation graphs are powerful but complicated. The graph visualization can help you understand and debug them. Here's an example of the visualization at work.



## Object Detection

- [Tensorflow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection)

    > The TensorFlow Object Detection API is an open source framework built on top of TensorFlow that makes it easy to construct, train and deploy object detection models.


- [Tensorflow detection model zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md)

    > We provide a collection of detection models pre-trained on the [COCO dataset](http://mscoco.org), the [Kitti dataset](http://www.cvlibs.net/datasets/kitti/), and the [Open Images dataset](https://github.com/openimages/dataset).

- [Object Detection Demo](https://github.com/tensorflow/models/blob/master/research/object_detection/object_detection_tutorial.ipynb)

### Oxford-IIIT Pets Dataset

- [Quick Start: Distributed Training on the Oxford-IIIT Pets Dataset on Google Cloud](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/running_pets.md)

    > This page is a walkthrough for training an object detector using the Tensorflow Object Detection API. In this tutorial, we'll be training on the Oxford-IIIT Pets dataset to build a system to detect various breeds of cats and dogs. The output of the detector will look like the following:
    > 
    > [![](https://github.com/tensorflow/models/raw/master/research/object_detection/g3doc/img/oxford_pet.png)](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/img/oxford_pet.png)




## Troubleshooting

### General
- [tensorflow - what does x = tf.placeholder(tf.float32, [None, 784]) means? - Stack Overflow](https://stackoverflow.com/questions/39305174/what-does-x-tf-placeholdertf-float32-none-784-means)

    From the tutorial: [Deep MNIST for Experts](https://www.tensorflow.org/versions/r0.10/tutorials/mnist/pros/index.html)

    > Here we assign it a shape of \[None, 784\], where 784 is the dimensionality of a single flattened 28 by 28 pixel MNIST image, and **None indicates that the first dimension, corresponding to the batch size, can be of any size**.

- [python - How to find which version of TensorFlow is installed in my system? - Stack Overflow](https://stackoverflow.com/questions/38549253/how-to-find-which-version-of-tensorflow-is-installed-in-my-system)

    ```python
    import tensorflow as tf
    print(tf.VERSION)
    ```
    or

    ```python
    import tensorflow as tf
    tf.__version__
    ```

- [Object detection using GPU on Windows is about 5 times slower than on Ubuntu · Issue #1942 · tensorflow/models](https://github.com/tensorflow/models/issues/1942)

    > Funny thing, I compiled tensorflow myself with GPU support on Windows using cmake as described here:  
    > [https://github.com/tensorflow/tensorflow/tree/master/tensorflow/contrib/cmake](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/contrib/cmake)  
    > and now it's working with the same performance as on Ubuntu!
    > 
    > So it looks like the problem is that the windows wheels (tensorflow-gpu) distributed by Google are not correctly compiled to fully utilize the GPU on Windows... !?

- [GPU is detected but training starts on the CPU · Issue #3366 · tensorflow/models](https://github.com/tensorflow/models/issues/3366)

    > I have installed the tensorflow-gpu 1.5 or 1.6.rc0 in accompany with Cuda-9.0 and CuDNN-7.0.5  
    > When I start training using `train.py`, it detects the GPU, but it starts the training on the CPU and CPU load is 100%. The GPU memory gets filled and its core clocks increases but it does not show any consistent load on the cores.
    > 
    > **Platform:** Windows10-x64  
    > **CUDA:** Cuda-9.0.176.1 and CuDNN-7.0.5 - GTX 1060 6G GPU  
    > **Tested by these Tensorflow versions:** 1.5 and 1.6-rc0 (both shows a similar behavior). Installed through pip (`pip install tensorflow-gpu`)
    > 
    > Training command: (it starts training but with this behavior)
    > 
    > `python train.py --logtostderr --train_dir=results/train --peline_config_path=weight/ssd_inception_v2_coco.config`


### GPU Usage

- [Using GPUs  |  TensorFlow](https://www.tensorflow.org/programmers_guide/using_gpu#allowing_gpu_memory_growth)

    Logging Device placement
    ------------------------

    To find out which devices your operations and tensors are assigned to, create the session with `log_device_placement` configuration option set to `True`.

    ```python
    # Creates a graph.
    a = tf.constant([1.0,   2.0,   3.0,   4.0,   5.0,   6.0], shape=[2,   3], name='a')
    b = tf.constant([1.0,   2.0,   3.0,   4.0,   5.0,   6.0], shape=[3,   2], name='b')
    c = tf.matmul(a, b)  
    # Creates a session with log_device_placement set to True.
    sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))  
    # Runs the op.  
    print(sess.run(c))  
    ```

    Manual device placement
    -----------------------

    If you would like a particular operation to run on a device of your choice instead of what's automatically selected for you, you can use `with tf.device` to create a device context such that all the operations within that context will have the same device assignment.

    ```python
    # Creates a graph.  
    with tf.device('/cpu:0'):
        a = tf.constant([1.0,   2.0,   3.0,   4.0,   5.0,   6.0], shape=[2,   3], name='a')
        b = tf.constant([1.0,   2.0,   3.0,   4.0,   5.0,   6.0], shape=[3,   2], name='b')
    c = tf.matmul(a, b)  
    # Creates a session with log_device_placement set to True.
    sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))  
    # Runs the op.  
    print(sess.run(c))  
    ```

    Allowing GPU memory growth
    --------------------------

    By default, TensorFlow maps nearly all of the GPU memory of all GPUs (subject to [`CUDA_VISIBLE_DEVICES`](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#env-vars)) visible to the process. This is done to more efficiently use the relatively precious GPU memory resources on the devices by reducing [memory fragmentation](https://en.wikipedia.org/wiki/Fragmentation_(computing)).

    In some cases it is desirable for the process to only allocate a subset of the available memory, or to only grow the memory usage as is needed by the process. TensorFlow provides two Config options on the Session to control this.

    The first is the `allow_growth` option, which attempts to allocate only as much GPU memory based on runtime allocations: it starts out allocating very little memory, and as Sessions get run and more GPU memory is needed, we extend the GPU memory region needed by the TensorFlow process. Note that we do not release memory, since that can lead to even worse memory fragmentation. To turn this option on, set the option in the ConfigProto by:

    ```python
    config = tf.ConfigProto()  
    config.gpu_options.allow_growth =   True
    session = tf.Session(config=config,   ...)  
    ```

    The second method is the `per_process_gpu_memory_fraction` option, which determines the fraction of the overall amount of memory that each visible GPU should be allocated. For example, you can tell TensorFlow to only allocate 40% of the total memory of each GPU by:

    ```python
    config = tf.ConfigProto()  
    config.gpu_options.per_process_gpu_memory_fraction =   0.4
    session = tf.Session(config=config,   ...)  
    ```

    This is useful if you want to truly bound the amount of GPU memory available to the TensorFlow process.

    Using multiple GPUs
    -------------------

    If you would like to run TensorFlow on multiple GPUs, you can construct your model in a multi-tower fashion where each tower is assigned to a different GPU. For example:

    ```python
    # Creates a graph.
    c =   []  
    for d in   ['/device:GPU:2',   '/device:GPU:3']: 
        with tf.device(d):
            a = tf.constant([1.0,   2.0,   3.0,   4.0,   5.0,   6.0], shape=[2,   3])
            b = tf.constant([1.0,   2.0,   3.0,   4.0,   5.0,   6.0], shape=[3,   2])  
        c.append(tf.matmul(a, b))  

    with tf.device('/cpu:0'):
        sum = tf.add_n(c)  
    # Creates a session with log_device_placement set to True.
    sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))  
    # Runs the op.  
    print(sess.run(sum))  
    ```

- [Release GPU memory after computation · Issue #1578 · tensorflow/tensorflow](https://github.com/tensorflow/tensorflow/issues/1578)

    ```python
    config = tf.ConfigProto()
    config.gpu_options.allow_growth=True
    sess = tf.Session(config=config)
    ```

- [InternalError: Blas GEMM launch failed · Issue #11812 · tensorflow/tensorflow](https://github.com/tensorflow/tensorflow/issues/11812)

    > Make sure you have no other processes using the GPU running. Run `nvidia-smi` to check this.

    > If multiple TensorFlow processes are used, either [`per_process_gpu_memory_fraction`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/core/protobuf/config.proto#L21) or [`allow_growth`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/core/protobuf/config.proto#L40) should be passed to the TensorFlow Session in a `ConfigProto` to prevent one process from using all the GPU memory. Preferably, multiple TensorFlow processes wouldn't be used at the same time.
    > [name=reedwm]

    > Try 'Shutdown' the running notebooks which uses your GPU. Restart the kernel.  
    > Run the code again.. This time it should work.
    > [name=jidhu-mohan]

    > To be clear, tensorflow will try (by default) to consume all available GPUs. It cannot be run with other programs also active. Closing. Feel free to reopen if this is actually another problem.
    > [name=drpngx]


- [Jupyter notebook Tensorflow GPU Memory 釋放 - 掃文資訊](https://hk.saowen.com/a/744613901932b8b210f4841dbfafb7a505c102ca9d2dc1e693accfe9ad829a0a)

    Jupyter notebook 每次運行完tensorflow的進程，佔着顯存不釋放。而又因為tensorflow是默認申請可使用的全部顯存，就會使得後續進程難以運行。暫時還沒有找到在jupyter notebook裏面自動釋放顯存的方法，但是我們可以做的是通過指定config為使用的顯存按需自動增長，這樣可以避免大多數的問題。代碼如下:

    ```python
    gpu_no = '0' # or '1'
    os.environ["CUDA_VISIBLE_DEVICES"] = gpu_no

    # 定義TensorFlow配置
    config = tf.ConfigProto()

    # 配置GPU內存分配方式，按需增長，很關鍵
    config.gpu_options.allow_growth = True

    # 配置可使用的顯存比例
    config.gpu_options.per_process_gpu_memory_fraction = 0.1

    # 在創建session的時候把config作為參數傳進去
    sess = tf.InteractiveSession(config = config)
    ```

- [TensorFlow 與 Keras 指定 NVIDIA GPU 顯示卡與記憶體用量教學 - G. T. Wang](https://blog.gtwang.org/programming/tensorflow-keras-specify-gpu-and-memory-tutorial/)

    > 在 TensorFlow 或 Keras 中使用 NVIDIA 的 GPU 做運算時，預設會把整台機器上所有的 GPU 卡都獨佔下來，而且不管實際需要多少顯示卡的記憶體，每張卡的記憶體都會被佔滿，以下介紹如何調整設定，讓多張顯示卡可以分給多個程式或多人使用。  
    > 
    > 指定 GPU 顯示卡
    > ----------
    > 
    > 若要只使用特定的 GPU 卡，可以使用 `CUDA_VISIBLE_DEVICES` 這個環境變數來設定，它的值代表 CUDA 程式可以使用的 GPU 卡編號（從 `0` 開始），例如只讓 CUDA 程式使用第一張 GPU 卡：
    > ```shell
    > # 只讓 CUDA 程式使用第一張 GPU 卡
    > export CUDA_VISIBLE_DEVICES=0
    > python my_script.py
    > ```
    > 這樣當 `my_script.py` 這個 Python 程式在執行時，就只會用到機器上的第一張 GPU 卡。若要指定多張 GPU 卡，則以逗號分隔：
    > ```shell
    > # 讓 CUDA 程式使用第一張與第三張 GPU 卡
    > export CUDA_VISIBLE_DEVICES=0,2
    > python my_script.py
    > ```
    > 如果自己會用的 GPU 卡都是固定的，我們可以將 `CUDA_VISIBLE_DEVICES` 的設定寫在 `~/.bashrc` 中，在登入 Linux 系統時就自動設定好。而如果要讓不同的程式用不同的 GPU 卡計算，分散計算量的話，可以在執行程式時直接以 `CUDA_VISIBLE_DEVICES` 指定：
    > ```shell
    > # 使用第一張 GPU 卡
    > CUDA_VISIBLE_DEVICES=0 python my_script1.py
    > 
    > # 使用第二張與第三張 GPU 卡
    > CUDA_VISIBLE_DEVICES=1,2 python my_script2.py
    > ```
    > 另外還有一種方式是直接在 Python 程式中更改 `CUDA_VISIBLE_DEVICES` 這個環境變數，此種方式的原理也是一樣的，只是這樣可以把 GPU 卡的指定邏輯寫在 Python 程式中：
    > ```python
    > import os
    > 
    > # 使用第一張與第三張 GPU 卡
    > os.environ["CUDA_VISIBLE_DEVICES"] = "0,2"
    > ```
    > 指定 GPU 顯示卡記憶體用量上限
    > -----------------
    > 
    > 若在 TensorFlow 中，我們可以使用 `tf.GPUOptions` 來調整程式佔用的 GPU 記憶體：
    > ```python
    > import tensorflow as tf
    > W = tf.constant([1.0, 2.0, 3.0, 4.0], shape=[2, 2], name='W')
    > x = tf.constant([1.3, 2.4], shape=[2, 1], name='x')
    > y = tf.matmul(W, x)
    > 
    > # 只使用 30% 的 GPU 記憶體
    > gpu_options = tf.GPUOptions(per_process_gpu_memory_fraction=0.3)
    > sess = tf.Session(config=tf.ConfigProto(gpu_options=gpu_options))
    > print(sess.run(y))
    > ```
    > 在以 TensorFlow 為 backend 的 Keras 程式中，我們可以透過以下的設定方式來指定 GPU 記憶體的佔用量：
    > ```python
    > import tensorflow as tf
    > 
    > # 只使用 30% 的 GPU 記憶體
    > gpu_options = tf.GPUOptions(per_process_gpu_memory_fraction=0.3)
    > sess = tf.Session(config=tf.ConfigProto(gpu_options=gpu_options))
    > 
    > # 設定 Keras 使用的 TensorFlow Session
    > tf.keras.backend.set_session(sess)
    > 
    > # 使用 Keras 建立模型
    > # ...
    > ```
    > 自動增長 GPU 記憶體用量
    > --------------
    > 
    > 直接設定 GPU 記憶體的用量可以確保程式不會吃掉過多的記憶體，但是如果程式遇到真的需要更大的記憶體時，就會因為記憶體不足而產生 `ResourceExhaustedError`，比較折衷的做法是採用自動增長 GPU 記憶體用量的方式，讓程式需要多少記憶體就拿多少，剩下的才留給別人：
    > ```python
    > import tensorflow as tf
    > W = tf.constant([1.0, 2.0, 3.0, 4.0], shape=[2, 2], name='W')
    > x = tf.constant([1.3, 2.4], shape=[2, 1], name='x')
    > y = tf.matmul(W, x)
    > 
    > # 自動增長 GPU 記憶體用量
    > gpu_options = tf.GPUOptions(allow_growth=True)
    > sess = tf.Session(config=tf.ConfigProto(gpu_options=gpu_options))
    > print(sess.run(y))
    > ```
    > 在 Keras 的部分也是一樣的做法：
    > ```python
    > import tensorflow as tf
    > 
    > # 自動增長 GPU 記憶體用量
    > gpu_options = tf.GPUOptions(allow_growth=True)
    > sess = tf.Session(config=tf.ConfigProto(gpu_options=gpu_options))
    > 
    > # 設定 Keras 使用的 Session
    > tf.keras.backend.set_session(sess)
    > 
    > # 使用 Keras 建立模型
    > # ...
    > ```
    > 參考資料：[Kevin Chan’s blog](https://applenob.github.io/tf_7.html)、[csdn](http://blog.csdn.net/sinat_26917383/article/details/75633754)、[StackOverflow](https://stackoverflow.com/questions/40690598/can-keras-with-tensorflow-backend-be-forced-to-use-cpu-or-gpu-at-will/42750563#42750563)
    > 





### Debug Log

- [Tensorflow documentation's example code on "Logging Device Placement" doesn't print out anything - Stack Overflow](https://stackoverflow.com/questions/39677168/tensorflow-documentations-example-code-on-logging-device-placement-doesnt-pr)

    > For Jupyter (and other) users, there is a recently-added feature that makes it possible to read back the device placement when you make a [`Session.run()`](https://www.tensorflow.org/versions/r0.10/api_docs/python/client.html#Session.run) call and print it in your notebook.
    > 
    > ```
    > # Creates a graph.
    > a = tf.constant([1.0, 2.0, 3.0, 4.0, 5.0, 6.0], shape=[2, 3], name='a')
    > b = tf.constant([1.0, 2.0, 3.0, 4.0, 5.0, 6.0], shape=[3, 2], name='b')
    > c = tf.matmul(a, b)
    > # Creates a session with log_device_placement set to True.
    > sess = tf.Session()
    > 
    > # Runs the op.
    > options = tf.RunOptions(output_partition_graphs=True)
    > metadata = tf.RunMetadata()
    > c_val = sess.run(c, options=options, run_metadata=metadata)
    > 
    > print metadata.partition_graphs
    > 
    > ```
    > 
    > The `metadata.partition_graphs` contains the actual nodes of the graph that executed, partitioned by device. The partitions aren't explicitly labeled with the device they represent, but every `NodeDef` in the graph has its `device` field set.
    > [name=mrry]

    > just use `print metadata` instead of `print metadata.partition_graphs`. You'll see its a set of objects, you can view each by indices, like `print metadata.partition_graphs[0]` – [name=Udayraj Deshmukh]

    > Unfortunately Jupyter doesn't see the C++ error stdout messages that the device placement logging uses. There's a longer thread on the problem here:
    > 
    > [https://github.com/nteract/hydrogen/issues/209](https://github.com/nteract/hydrogen/issues/209)
    > 
    > There's no easy workaround that I know of, other than running your script outside of Jupyter.
    > [name=Pete Warden]

- [tensorflow - What do the options in ConfigProto like allow_soft_placement and log_device_placement mean? - Stack Overflow](https://stackoverflow.com/questions/44873273/what-do-the-options-in-configproto-like-allow-soft-placement-and-log-device-plac)

    > In addition to comments in [tensorflow/core/protobuf/config.proto](https://github.com/tensorflow/tensorflow/blob/r1.2/tensorflow/core/protobuf/config.proto) ([allow\_soft\_placement](https://github.com/tensorflow/tensorflow/blob/r1.2/tensorflow/core/protobuf/config.proto#L248), [log\_device\_placement](https://github.com/tensorflow/tensorflow/blob/r1.2/tensorflow/core/protobuf/config.proto#L251)) it is also explained in TF's [using GPUs tutorial](https://www.tensorflow.org/tutorials/using_gpu).
    > 
    > > To find out which devices your operations and tensors are assigned to, create the session with `log_device_placement` configuration option set to True.
    > 
    > Which is helpful for debugging. For each of the nodes of your graph, you will see the device it was assigned to.
    > 
    > ---
    > 
    > > If you would like TensorFlow to automatically choose an existing and supported device to run the operations in case the specified one doesn't exist, you can set `allow_soft_placement` to True in the configuration option when creating the session.
    > 
    > Which will help you if you accidentally manually specified the wrong device or a device which does not support a particular op. This is useful if you write a code which can be executed in environments you do not know. You still can provide useful defaults, but in the case of failure a graceful fallback.
