# Tensorflow__深度學習

## API Reference
- [All symbols in TensorFlow  |  TensorFlow](https://www.tensorflow.org/api_docs/python/)

- [tf.placeholder  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/placeholder)

- [Module: tf.layers  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers)
    - [tf.layers.conv2d  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/conv2d)
    - [tf.layers.max_pooling2d  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/max_pooling2d)
    - [tf.layers.flatten  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/flatten)
    - [tf.layers.dense  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/layers/dense)

- [tf.matmul  |  TensorFlow](https://www.tensorflow.org/versions/master/api_docs/python/tf/matmul)
    Multiplies matrix `a` by matrix `b`, producing `a` \* `b`.

- [tf.multiply  |  TensorFlow](https://www.tensorflow.org/versions/master/api_docs/python/tf/multiply)
    Returns x * y element-wise.

- [tf.trainable_variables  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/trainable_variables)
    Returns all variables created with `trainable=True`.

- [tf.Session.close()  |  TensorFlow](https://www.tensorflow.org/api_docs/python/tf/Session#close)
    Closes this session.
    Calling this method frees all resources associated with the session.


## GPU Usage

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

> If multiple TensorFlow processes are used, either [`per_process_gpu_memory_fraction`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/core/protobuf/config.proto#L21) or [`allow_growth`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/core/protobuf/config.proto#L40) should be passed to the TensorFlow Session in a `ConfigProto` to prevent one process from using all the GPU memory. Preferably, multiple TensorFlow processes wouldn't be used at the same time.
> [name=reedwm]

> Try 'Shutdown' the running notebooks which uses your GPU. Restart the kernel.  
> Run the code again.. This time it should work.
> [name=jidhu-mohan]

> To be clear, tensorflow will try (by default) to consume all available GPUs. It cannot be run with other programs also active. Closing. Feel free to reopen if this is actually another problem.
> [name=drpngx]



## Debug Log

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


We use MNIST HERE (with sklearn 8x8 version rather than use tensorflow 28x28 version)

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

```python
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

#### build the network

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

#### Train the model and collect the performance

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



## CNN



- Create place holder

    ```python=
    shpae_t = np.append(None,image_shape) # image_shape with batch size set to None
    placeholder_t = tf.placeholder(tf.float32, shape=shpae_t, name="x") # Name the TensorFlow placeholder "x" 
    ```

- Convolution and Max Pooling Layer

    ```python=
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
    ```python=
    # flatten of x_tensor
    flatten_layer = tf.layers.flatten(inputs=x_tensor)
    ```
- Fully-Connected Layer

    ```python=
    # fully-connected layer with inputs "x_tensor", units (number of output) "num_outputs"
    # activation function "tf.nn.relu"
    dense_layer = tf.layers.dense(inputs=x_tensor, units=num_outputs, activation=tf.nn.relu)
    ```

- Outpur layer

    ```python=
    # output layer with inputs "x_tensor", units (number of output) "num_outputs"
    # linear activation function 
    output_layer = tf.layers.dense(inputs=x_tensor, units=num_outputs)
    ```
    



## FAQ

- [tensorflow - what does x = tf.placeholder(tf.float32, [None, 784]) means? - Stack Overflow](https://stackoverflow.com/questions/39305174/what-does-x-tf-placeholdertf-float32-none-784-means)

    From the tutorial: [Deep MNIST for Experts](https://www.tensorflow.org/versions/r0.10/tutorials/mnist/pros/index.html)

    > Here we assign it a shape of \[None, 784\], where 784 is the dimensionality of a single flattened 28 by 28 pixel MNIST image, and **None indicates that the first dimension, corresponding to the batch size, can be of any size**.


