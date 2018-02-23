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


