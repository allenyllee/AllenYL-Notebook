# 深度學習算法1-6_Generative

[toc]
<!-- toc --> 


# autoencoder

- [Neural networks [6.1] : Autoencoder - definition - YouTube](https://www.youtube.com/watch?v=FzS3tMl4Nsc&list=PL6Xpj9I5qXYEcOhn7TqghAJ6NAPrNmUBH&index=44)

- [Hugo Larochelle](http://info.usherbrooke.ca/hlarochelle/neural_networks/content.html)



## deep autoencoder

- [(47) ML Lecture 16: Unsupervised Learning - Auto-encoder - YouTube](https://www.youtube.com/watch?v=Tk5B4seA-AU&t=2s)

- [Hung-yi Lee](http://speech.ee.ntu.edu.tw/~tlkagk/courses_ML16.html)

- [Deep Auto-encoder - yang_mang的博客 - CSDN博客](https://blog.csdn.net/yang_mang/article/details/77574120)

    > autoencoder可以用于数据压缩、降维，预训练神经网络，生成数据等等。
    > 
    > autoencoder的架构
    > --------------
    > 
    > autoencoder的架构是这样的：
    > 
    > ![](https://i.imgur.com/tzVudvS.jpg)
    > 
    > 需要分别训练一个Encoder和一个Decoder。
    > 
    > 比如，一张数字图片784维，放入Encoder进行压缩，编程code，通常要小于原来的784维；
    > 
    > 然后可以将压缩后的code，放入Decoder进行reconsturct，产生和原来相似的图片。
    > 
    > Encoder和Decoder需要一起进行训练。
    > 
    > 下面看看PCA对于数据的压缩：
    > 
    > ![](https://i.imgur.com/6losAUC.jpg)
    > 
    > 输入同样是一张图片，通过选择W，找到数据的主特征向量，压缩图片得到code，然后使用W的转置，恢复图片。
    > 
    > 我们知道，PCA对数据的降维是线性的(linear)，恢复数据会有一定程度的失真。上面通过PCA恢复的图片也是比较模糊的。
    > 
    > 所以，我们也可以把PCA理解成为一个线性的autoencoder，W就是encode的作用，w的转置就是decode的作用，最后的目的是decode的结果和原始图片越接近越好。
    > 
    > ![](https://i.imgur.com/RH1KTtr.jpg)
    > 
    > 现在来看真正意义上的Deep Auto-encoder的结构。通常encoder每层对应的W和decoder每层对应的W不需要对称(转置)。
    > 
    > ![](https://i.imgur.com/ZWR0QtO.jpg)
    > 
    > 从上面可以看出，Auto-encoder产生的图片，比PCA还原的图片更加接近真实图片。
    > 
    > ![](https://i.imgur.com/bPO9Elm.jpg)
    > 
    > 上面是使用PCA和autoencoder对于数字图片压缩后的可视化结果，明显autoencoder的区分度更高。
    > 
    > De-noising auto-encoder
    > -----------------------
    > 
    > 为了让aotoencoder训练的更好，更加robust，我们在训练的时候加入一些noise，这就是De-noising auto-encoder。
    > 
    > ![](https://i.imgur.com/QSRs9dC.jpg)
    > 
    > examples
    > --------
    > 
    > 接下来再看两个例子。
    > 
    > ![](https://i.imgur.com/50rJjCM.jpg)
    > 
    > ![](https://i.imgur.com/QvYNnpe.jpg)
    > 
    > 文本检索，简单的词袋模型，将文本转化成词向量。
    > 
    > 当搜索的词和文本向量角度越接近，就说明内容越相关。
    > 
    > ![](https://i.imgur.com/Im9jK3k.jpg)
    > 
    > 将词向量放入autoencoder中进行压缩，得到code，内容相近的文本，code也越接近。
    > 
    > 不同主题的文本被明显的分开，得到右上的2维图像。
    > 
    > 搜索图片的相似性。
    > 
    > 搜索红框中的迈克杰克逊的照片，下面是使用像素点之间的欧式距离得到的搜索结果。
    > 
    > ![](https://i.imgur.com/MovaYJN.jpg)
    > 
    > 下面使用autoencoder编码后的code，进行相似性的搜索结果。
    > 
    > ![](https://i.imgur.com/xywhJIe.jpg)
    > 
    >  ![](https://i.imgur.com/EYhsrvX.jpg)
    > 
    > 使用CNN实现autoencoder
    > 
    > ![](https://i.imgur.com/YryEfzX.jpg)
    > 
    > 经过多次convolution和pooling后的code，可以再经过deconvolution和unpooling恢复。
    > 
    > 下面将如何实现unpooling和deconvolution。
    > 
    > ![](https://i.imgur.com/op0cxZN.jpg)
    > 
    > 在maxpooling时，需要记住max值在图片中的位置。
    > 
    > 当进行unpooling时，把小的图片做扩展，先把max值恢复到之前的位置，然后在之前进行maxpooling的field内的像素都置为0.
    > 
    > 接下来看Deconvolution
    > 
    > ![](https://i.imgur.com/k4rsM88.jpg)
    > 
    > 现在假设一个field里面有3个像素点，每个filter的3个weight作用下得到一个output，如图左。
    > 
    > 而deconvolution就是要让这3个output复原成原来那么多的点，一个output变成3各点，把重叠的点加起来，如图中。
    > 
    > 现在，将3个output进行扩展，给扩展的点的值为0，然后就依然做convolution，还是可以得到和图中相同的结果。
    > 
    > 所以，deconvolution其实就是convolution。
    > 
    > 最后，我们可以使用autoencoder压缩后的code，输入到decoder里，得到一张新的图像，如下所示。
    > 
    > ![](https://i.imgur.com/yhoNMg4.jpg)
    > 

### Why do the number of neurons in the hidden layer of an autoencoder need to be less than the input/output layer

- [Why do the number of neurons in the hidden layer of an autoencoder need to be less than the input/output layer? - Quora](https://www.quora.com/Why-do-the-number-of-neurons-in-the-hidden-layer-of-an-autoencoder-need-to-be-less-than-the-input-output-layer)

    > When experimenting on autoencoders with the MNIST dataset, I discovered that having large first layers and thinner last layers led to significantly better performance than more obvious architectures. Why, you ask?
    > 
    > Large layers allow your net to compute powerful representations of your data, which will help your smaller layers when computing denser representations.
    > 


## sparse autoencoder

- https://web.stanford.edu/class/cs294a/sparseAutoencoder.pdf

### What are the differences between sparse coding and autoencoder?

- [machine learning - What are the differences between sparse coding and autoencoder? - Cross Validated](https://stats.stackexchange.com/questions/118199/what-are-the-differences-between-sparse-coding-and-autoencoder)

    > Finding the differences can be done by looking at the models. Let's look at sparse coding first.
    > 
    > ## Sparse coding
    > 
    > Sparse coding minimizes the objective
    > 
    > $$\mathcal{L}_{\text{sc}} = \underbrace{||WH - X||_2^2}_{\text{reconstruction term}} + \underbrace{\lambda ||H||_1}_{\text{sparsity term}} $$ where $W$ is a matrix of bases, H is a matrix of codes and $X$ is a matrix of the data we wish to represent. $\lambda$ implements a trade of between sparsity and reconstruction. Note that if we are given $H$, estimation of $W$ is easy via least squares.
    > 
    > In the beginning, we do not have $H$ however. Yet, many algorithms exist that can solve the objective above with respect to $H$. Actually, this is how we do inference: **we need to solve an optimisation problem** if we want to know the $h$ belonging to an unseen $x$.
    > 
    > ## Auto encoders
    > 
    > Auto encoders are a family of unsupervised neural networks. There are quite a lot of them, e.g. deep auto encoders or those having different regularisation tricks attached--e.g. denoising, contractive, sparse. There even exist probabilistic ones, such as generative stochastic networks or the variational auto encoder. Their most abstract form is
    > 
    > $$D(d(e(x;\theta^r); \theta^d), x) $$ but we will go along with a much simpler one for now:$$\mathcal{L}_{\text{ae}} = ||W\sigma(W^TX) - X||^2 $$ where $\sigma$ is a nonlinear function such as the logistic sigmoid $\sigma(x) = {1 \over 1 + \exp(-x)}$.
    > 
    > ## Similarities
    > 
    > Note that $\mathcal{L}_{sc}$ looks _almost_ like $\mathcal{L}_{ae}$ once we set $H = \sigma(W^TX)$. The difference of both is that i) auto encoders do not encourage sparsity in their general form ii) an autoencoder uses a model for finding the codes, while sparse coding does so by means of optimisation.
    > 
    > For natural image data, regularized auto encoders and sparse coding tend to yield very similar $W$. However, auto encoders are _much more efficient_ and are easily generalized to much more complicated models. E.g. the decoder can be highly nonlinear, e.g. a deep neural network. Furthermore, one is not tied to the squared loss (on which the estimation of $W$ for $\mathcal{L}_{sc}$ depends.)
    > 
    > Also, the different methods of regularisation yield representations with different characteristica. Denoising auto encoders have also been shown to be equivalent to a certain form of RBMs etc.
    > 
    > ## But why?
    > 
    > If you want to solve a prediction problem, you will not need auto encoders _unless_ you have only little labeled data and a lot of unlabeled data. Then you will generally be better of to train a deep auto encoder and put a linear SVM on top instead of training a deep neural net.
    > 
    > However, they are very powerful models for capturing characteristica of distributions. This is vague, but research turning this into hard statistical facts is currently conducted. Deep latent Gaussian models aka Variational Auto encoders or generative stochastic networks are pretty interesting ways of obtaining auto encoders which provably estimate the underlying data distribution.




## sparse autoencoder 和 restricted boltzmann machine

- [(1 封私信 / 83 条消息)简单解释一下sparse autoencoder, sparse coding和restricted boltzmann machine的关系？ - 知乎](https://www.zhihu.com/question/22906027)

    > 最近也在看这一块的内容，抛砖引玉一下，有错误还请大家指点。\
    > 我认为autoencoder和RBM是一类的，都属于学习模型；而稀疏编码更像是施加在这些基本模型上的一种优化手段。\
    > 先说说autoencoder和RBM的不同之处：
    > 
    > 1.  autoencoder的神经元是确定型的，用的是sigmold函数，就像传统的ff网络一样。而RBM的神经元是随机的。（最基本的RBM神经元只有0和1两种状态，但是扩展后可以在![\left[ 0,1 \right] ](https://www.zhihu.com/equation?tex=%5Cleft%5B+0%2C1+%5Cright%5D+)这个区间上取任何值）
    > 2.  由于autoencoder的确定性，它可以用BP方法来训练。但是RBM就只能用采样的方法来得到一个服从RBM所表示分布的随机样本。(Gibbs采样，CD采样等等）
    > 
    > 在深度学习里面，可以把autoencoder和RBM都看作是一块块砖头，我们可以用许多这样的砖头构造出深层次的网络。基本思路是前面先用这些"砖头"搭出几层网络，自动学习出数据的一些特征后，后面再用一个分类器来分类，得到最后的结果。如果用autoencoder作砖头，得到的就是stacked autoencoder；如果用RBM作砖头，得到的就是deep belief network。
    > 
    > 再说稀疏编码，它是把大多数的神经元限制为0，只允许少量的神经元激活，来达到"稀疏"的效果。这主要是为了模拟人眼视觉细胞的特性。在算法里，其实就是在用来优化的目标函数里面加入一个表示稀疏的正则项，一般可以通过L1范数或者KL divergence来实现。正如题主所说，稀疏性可以加到autoencoder上，也可以加到RBM上。
    > 
    > -----------------------------------------------题外话------------------------------------\
    > 再扯几句RBM，这个模型实在是太神奇了，感觉要补物理了。。\
    > RBM是由BM简化得到的。（BM允许所有神经元之间的相连，而RBM只允许visible node和hidden node之间相连）而BM又是根据一种叫做EBM（Energy based model）的基本框架产生的。EBM把模型里的所有参数和一个能量函数联系起来，通过使这个能量函数最小化的方式来使整个系统达到稳定状态。
    > 
    > ---
    > 
    > 这个问题是几天前问的，现在资料读着读着也有了自己的理解，和楼上不太一样呢......
    > 
    > 一、有些文章上写这三种方法都是用来构建deep network的基本方法，也就是说它们都是可以stack起来的，倒也不是说sparse coding 就是shallow的，它们都是砖块吧......
    > 
    > 二、似乎前两个技术都是确定性的变换，而RBM是概率性的变换（所以我一直无法在情感上接受它T_T）。
    > 
    > 三、sparse coding的编码函数是隐式的（就是写不出）而后两种的编码函数是显式的（表现为一个权值矩阵和偏置向量），然后它们仨的解码函数都是显式的。
    > 
    > 四、spase autoencoder编码（去）和解码（来）的权值矩阵是可以不一样的，而RBM去和来的权值矩阵是一样的。
    > 
    > 五、其实RBM也可以加上稀疏限制，就变成sparse RBM了，论文上说效果会更好。
    > 
    > 六、对于构建convolutional neural network而言，后两种方法可以通过随机取方便地训练出几十上百种滤波器（特征检测器），但是sparse coding因为训练出来的是隐式的编码函数所以感觉train完之后在test阶段运算不方便，因为是要去"找"一个系数向量来让那些bases的线性组合逼近原始图像，而不是直接乘一个矩阵映射过去......
    > 
    > ---
    > 
    > 首先，你可以说RBM和Autoencoder是一个东西，之前也有人回答过有人证明了两者在sigmoid下的等价。他们的目标是相同的，就是给定一个输入，得到一个中间层，并利用中间层去重构一个和输入相同的样本，然后利用不同的评价指标（欧几里得距离、输入输出样本的KL散度等），通过某种优化方法（SGD或者CD，注：bp不是一种优化方法）尽可能的缩小输出样本与输入样本之间的差异。所以广义上来讲，RBM也是一种编码器，之前提到的中间层在训练完成后，就可以看做是每个样本所提取出的特征（这个就和稀疏编码有关了，待会再讲）。\
    > 那么，这两种方法到底有什么区别，以至于从我的角度来看，并不认为二者可以混为一谈。\
    > 1.出发点不一样：\
    > Autoencoder作为确定模型，它的输入和输出之间有着严格的数学公式，也就是当你输入1+1的时候必然得到2。然而RBM作为一个不确定性模型，它的输入和输出是通过概率连接的，也就是说当你输入1+1的时候，整个网络只能告诉你，它之所以输出2，是因为模型中1+1=2的几率最大，这就要拜RBM中的一个叫采样的东西所赐。\
    > 2.训练过程不同：\
    > Autoencoder采用的是梯度下降的方式，而RBM采用的是散度（也就是概率的梯度）。所以从道理上来讲两者的优化目的并不相同。\
    > 上面两点的不同也就直接导致了为什么这两种方法都有各自存在道理的原因：\
    > autoencoder可以直接做梯度下降（直接看成一个层的BP神经网络即可），所以训练速度快，可以在短时间内达到比较不错的效果，然而，快速的训练导致的直接结果就是模型过于呆板，对于轻微的扰动就出出现不稳定的现象（可以参考对抗学习中举的误差累积的例子）。因此才有了在样本中加入扰动项的Denoising Autoencoder，从而提高泛化性能。\
    > 而RBM呢，由于概率本身带来的不确定性，导致了即便是针对同一个样本每次输出的结果也无法完全相同，在这种情况下就可以很好的提高模型的泛化能力。\
    > 笼统点讲，确定性模型只是尽可能的记住了你的所有样本，并通过某些扰动去尽可能的制造更多样的样本。而RBM则是通过概率的方式去尽可能的逼近样本的原始分布，所以从本质上来讲RBM比Autoencoder更接近问题的根本。\
    > 至于RBM为什么效果没有Autoencoder或者CNN，LSTM等网络好，我也不太清楚，以下只是猜想：\
    > --------------------纯属蒙的，不要见怪--------------------\
    > 1.训练太麻烦，好像即便用了简化Gibbs sample的CD，收敛速度也没有sgd的效果好\
    > 2.原始分布未知，评价模型困难\
    > 3.速度+调参，这个真的很重要，你运行一遍别人跑了十几遍，怎么破啊
    > 
    > 


## Contractive Autoencoder (CAE) 


### Jacobian Matrix

- [[深度学习]Contractive Autoencoder - 落痕月极的博客 - CSDN博客](https://blog.csdn.net/LuohenYJ/article/details/78394060)

    > 雅克比矩阵是一阶偏导，假设(x1,x2,....,xn)到(y1,y2,...,ym)的映射，相当于m个n元函数，它的Jacobian Matrix如下
    > 
    > ![](https://i.imgur.com/oScfmlD.jpg)
    > 
    > 该矩阵表示x的微小波动对y的影响。
    > 
    > 雅克比矩阵与Hessian矩阵不同，hessian矩阵表示二阶偏导。
    > 
    > 可以用雅克比矩阵表示函数的一阶泰勒展开 ![](https://i.imgur.com/ZKwIJXW.jpg)


### Calculating Jacobian

- [python - Computing jacobian matrix in Tensorflow - Stack Overflow](https://stackoverflow.com/questions/50244270/computing-jacobian-matrix-in-tensorflow)

    > Assuming that `X` and `Y` are Tensorflow tensors and that `Y` depends on `X`:
    > 
    > ```python
    > from tensorflow.python.ops.parallel_for.gradients import jacobian
    > J=jacobian(Y,X)
    > ```
    > 
    > The result has the shape `Y.shape + X.shape` and provides the partial derivative of each element of `Y` with respect to each element of `X`.

- [Gradients of non-scalars (higher rank Jacobians) · Issue #675 · tensorflow/tensorflow](https://github.com/tensorflow/tensorflow/issues/675)

    > ```python
    > def Jacobian(X, y):
    >     J = tf.map_fn(lambda m: tf.gradients(y[:,:,m:m+1], X)[0], tf.range(tf.shape(y)[-1]), tf.float32)
    >     J = tf.transpose(tf.squeeze(J), perm = [1,0,2])
    >     return J
    > ```

- [jacobian.py · d62c4e57ba82da8d0944f1b28d9d80a1078be5ca · Christian Baumgartner / fast_jacobian · GitLab](https://git.ee.ethz.ch/baumgach/fast_jacobian/blob/d62c4e57ba82da8d0944f1b28d9d80a1078be5ca/jacobian.py)

    > ```python
    > # A fast Jacobian implementation with inspiration from the discussions here:
    > # https://github.com/tensorflow/tensorflow/issues/675
    > 
    > # Produces the following output:
    > # >>> Naive Computation
    > # >>> 17 Seconds: (16, 40, 200)
    > # >>> Lisa's Implementation
    > # >>> 9 Seconds: (16, 40, 200)
    > # >>> Fast Implementation
    > # >>> 0 Seconds: (16, 40, 200)
    > 
    > def jacobian(y, x, bs):
    >     loop_vars = [
    >         tf.constant(0, tf.int32),
    >         tf.TensorArray(tf.float32, size=bs),
    >     ]
    > 
    >     # This loop iteratores over the batches
    >     _, jacobian = tf.while_loop(
    >         lambda b, _: b < bs,
    >         lambda b, result: (b+1, result.write(b, body(y[b], x, b))),
    >         loop_vars,
    >         parallel_iterations=10)
    > 
    >     return jacobian.stack()
    > 
    > def jacobian_naive(y, x, bs):
    >     y_list = tf.unstack(y, num = bs)
    >     jacobian_list = [[tf.gradients(y_, x)[0][i] for y_ in tf.unstack(y_list[i])] for i in range(bs)]
    >     return tf.stack(jacobian_list)
    > 
    > def jacobian_lisa(y,x,bs):
    > 
    >     num_outputs = y.get_shape().as_list()[1]
    >     num_inputs = x.get_shape().as_list()[1]
    > 
    >     jac_row_tensors = []
    >     for dd in range(num_outputs):
    >         jac_row = [tf.reshape(tf.gradients(y[ii, ..., dd], x)[0][ii, :], (1, 1, num_inputs)) for ii in range(bs)]
    >         jac_row_tensors.append(tf.concat(jac_row, axis=0))
    >     jac_dec_batch_tensor = tf.concat(jac_row_tensors, axis=1)
    >     return jac_dec_batch_tensor
    > 
    > ```

- [The Living Thing / Notebooks : Tensorflow](https://livingthing.danmackinlay.name/tensorflow.html)


    > here's mine -- works for high-dimensional Jacobians (numerator and denominator have >1 dimension), undefined batch sizes, and tensors that are not statically known.
    > 
    > Remember to use an interactive session, otherwise tf.get_default_session() will not be able to find the session.
    > 
    > ```python 
    > def tf_jacobian(tensor2, tensor1, feed_dict, sess = tf.get_default_session()): 
    >     """ 
    >     Computes the tensor d(tensor2)/d(tensor1) recursively. 
    >     :param tensor2: numerator of Jacobian 
    >     :param tensor1: denominator of Jacobian 
    >     :param feed_dict: input data (need this if tensors are not statically known) 
    >     :return: a tensor of dimension (dim_tensor2 x dim_tensor1) 
    >     """ 
    > 
    >     # can't do tensor.get_shape() because it doesn't work for undefined batch size 
    >     shape = list(sess.run(tf.shape(tensor2), feed_dict)) 
    > 
    >     if shape: 
    >         # split tensor2 along first dimension and recur 
    >         # int trick from https://github.com/tensorflow/tensorflow/issues/7754 
    >         tensor2_split = tf.split(axis = 0, num_or_size_splits = int(shape[0]), value = tensor2) 
    >         grad_split = [tf_jacobian(tf.squeeze(M, squeeze_dims = 0), tensor1, feed_dict) for M in tensor2_split] 
    >         return tf.stack(grad_split) 
    >     
    >     else: # calculate gradient of scalar 
    >         grad = tf.gradients(tensor2, tensor1) 
    >     
    >         if grad[0] != None: 
    >             return tf.squeeze(grad, squeeze_dims = [0])   
    >         else: 
    >             # replace any undefined gradients with zeros 
    >             return tf.zeros_like(tensor1)
    > ```
    > 
    > And here's one for batched tensors:
    > 
    > ```python 
    > def batch_tf_jacobian(tensor2, tensor1, feed_dict, sess = tf.get_default_session()): 
    >     """ 
    >     Computes the matrix d(tensor2)/d(tensor1) recursively. 
    >     Tensorflow doesn't really have its own Jacobian operator 
    >     (tf.gradients sums over all dims of tensor2).
    >     :param tensor2: numerator of Jacobian, first dimension is batch
    >     :param tensor1: denominator of Jacobian, first dimension is batch
    >     :param feed_dict: input data (need this if tensors are not statically known)
    >     :return: batch Jacobian tensor
    >     """
    >     shape2 = list(sess.run(tf.shape(tensor2), feed_dict))
    >     shape1 = list(sess.run(tf.shape(tensor1), feed_dict))
    > 
    >     jacobian = tf_jacobian(tensor2, tensor1, feed_dict)
    >     batch_size = shape2[0]
    > 
    >     batch_jacobian = [tf.slice(jacobian, [i] + [0]*(len(shape2)-1) + [i] + [0]*(len(shape1)-1),  [1] + [-1]*(len(shape2)-1) + [1] + [-1]*(len(shape1)-1)) for i in range(batch_size)]
    >     batch_jacobian = [tf.squeeze(tensor, squeeze_dims = (0, len(shape2))) for tensor in batch_jacobian]
    >     batch_jacobian = tf.stack(batch_jacobian)
    > return batch_jacobian
    > 
    > ```
    > 


- [Computing the Jacobian matrix of a neural network in Python](https://medium.com/unit8-machine-learning-publication/computing-the-jacobian-matrix-of-a-neural-network-in-python-4f162e5db180)

    > #### Autograd
    > 
    > [Autograd](https://github.com/HIPS/autograd) is a very nice library, which notably performs automatic differentiation on top of Numpy. To use it, we first have to specify our feedforward function *f* using Autograd's encapsulated Numpy:
    > ```python
    > import autograd.numpy as anp
    > 
    > def ffpass_anp(x):
    >     a1 = anp.dot(x, w1) + b1   # affine
    >     a1 = anp.maximum(0, a1)    # ReLU
    >     a2 = anp.dot(a1, w2) + b2  # affine
    > 
    >     exps = anp.exp(a2 - anp.max(a2))  # softmax
    >     out = exps / exps.sum()
    >     return out
    > ```
    > 
    > First, let's check that this function is correct, by comparing it with our previous Tensorflow feedforward function `ffpass_tf()`.
    > ```python
    > out_anp = ffpass_anp(x0)
    > out_keras = ffpass_tf(x0)
    > 
    > np.allclose(out_anp, out_keras, 1e-4)
    > 
    > >> True
    > ```
    > 
    > OK, we have the same function f. Let's now compute the Jacobian matrix. It's straightforward with Autograd:
    > ```python
    > from autograd import jacobian
    > 
    > def jacobian_autograd(x):
    >     return jacobian(ffpass_anp)(x)
    > 
    > is_jacobian_correct(jacobian_autograd, ffpass_np)
    > 
    > >> True
    > ```
    > 
    > OK good, we have the function and it looks correct. And how long does it take?
    > ```python
    > %timeit jacobian_autograd(x0)
    > 
    > >> 3.69 ms ± 135 µs
    > ```
    > 

### Calculate first and second derivative of the contractive auto-encoder regularization term

- [neural networks - How to calculate derivative of the contractive auto-encoder regularization term? - Cross Validated](https://stats.stackexchange.com/questions/14827/how-to-calculate-derivative-of-the-contractive-auto-encoder-regularization-term)

    > **Setup**
    > 
    > I found a paper on that has a varient on normal auto-encoders (contractive) which for its gradient uses the following regularization penalty:
    > 
    > $$\left|\left|J_f(x)\right|\right|^2_F = \sum_{ij}{\left( \frac{\partial h_j(x)}{\partial x_i} \right)}^2$$
    > 
    > where $\left|\left|\cdot\right|\right|_F^2$ is the Frobenius norm, $h$ is the hidden units, and $x$ is the input. The paper also gives an alternative form (when a sigmoid is used for 
    > 
    > $f$) to the equation that looks like:
    > 
    > $$\left|\left|J_f(x)\right|\right|^2_F = \sum_{i=1}^{d_h}(h_i(1-h_i))^2\sum_{j=1}^{d_x}W^2_{ij}$$
    > 
    > **Question 1**
    > 
    > As per usual, no actual derivation is given to get the second form of the equation in the paper. I attempted to derive it myself, but would _greatly_ appreciate it if someone could check my work and let me know what mistakes I might have made.
    > 
    > $$a(x) = W^T x + b$$
    > 
    > $$h(x) = f(a(x))$$
    > 
    > 
    > $$f(x) = \frac{1}{1+e^{-x}}$$
    > 
    > Then, using the chain rule:
    > 
    > $$\frac{\partial h(x)}{\partial x} = \frac{\partial h(x)}{\partial a(x)} \frac{\partial a(x)}{\partial x}$$
    > 
    > Using the standard derivation of the sigmoid:
    > 
    > $$\frac{\partial h(x)}{\partial a(x)} = f(a(x))(1 - f(a(x))) = h(1- h)$$
    > 
    > ---
    > 
    > when I interpret your equations correctly, the $W$ is supposed to be a matrix. This means that $a(x)$ is a vector and the then chain rule actually reads:
    > 
    > $$\frac{\partial h_i}{\partial x_j} = \sum_k \frac{\partial h_i}{\partial a_k} \frac{\partial a_k}{\partial x_j}.$$
    > 
    > In matrix notation, the second term is $\frac{\partial a}{\partial x} = W^\top$. If I interpret your equations correctly, $f(x)$ is applied to each element of $a$ individually. Therefore, $\frac{\partial h_i}{\partial a_j} = \delta_{ij}h(a_j)(1-h(a_j))$ which means that it is a diagonal matrix with the term $h(a_j)(1-h(a_j))$ as the $j$th entry. Therefore
    > 
    > $$\frac{\partial h_i}{\partial x_j} = \sum_k \delta_{ik} h(a_k)(1-h(a_k)) W_{kj} = h(a_i)(1-h(a_i)) W_{ij}.$$
    > 
    >  Thus,
    > 
    > $$\sum_{ij}\left(\frac{\partial h_i}{\partial x_j}\right)^2 =\sum_{ij} h(a_i)^2(1-h(a_i))^2 W_{ij}^2 = \sum_{i} h(a_i)^2(1-h(a_i))^2 \sum_{i} W_{ij}^2$$
    > 
    > ---
    > 
    > However, that is the penalty of my cost function, so I actually need to get the second derivative to find the gradient. – Ranon Aug 27 '11 at 22:30
    > 
    > ---
    > 
    > To simplify the notation, let 
    > 
    > $h'_i = \frac{\partial h_i}{\partial a_i}$.
    > 
    > The term is:
    > 
    > $$\| J_f \|_F^2 = \sum_{i} \left( h'_i \right)^2 \sum_j W_{i,j}^2$$
    > 
    > The gradient is:
    > 
    > $$\frac{\partial }{\partial W_{k,l}} \| J_f \|_F^2 = 2 (h'_k)^2 W_{kl} + \left(\sum_j W_{kj}^2\right) \frac{\partial (h'_k)^2}{\partial a_k} x_l$$
    > 
    > You can then use any activation functions. Let's see some examples.
    > 
    > ### Sigmoid
    > 
    > $h_k = \text{sig}(a_k)$
    > 
    > $(h'_k)^2 = h_k^2 (1 - h_k)^2$
    > 
    > $\frac{\partial (h'_k)^2}{\partial a_k} = 2 h_k^2 (1 -h_k)^2 (1 - 2 h_k)$
    > 
    > You can verify that you get the same term as fabee's.
    > 
    > ### SoftPlus
    > 
    > $h_k = \ln (1 + \exp(a_k))$
    > 
    > $(h'_k)^2 = \text{sig}(a_k)^2$
    > 
    > $\frac{\partial (h'_k)^2}{\partial a_k} = 2 \text{sig}(a_k)^2 - 2 \text{sig}(a_k)^3$
    > 
    > ### Tanh
    > 
    > $h_k = \tanh(a_k)$
    > 
    > $(h'_k)^2 = (1 - h_k^2)^2$
    > 
    > $\frac{\partial (h'_k)^2}{\partial a_k} = -4 h_k (1 - h_k^2)^2$
    > 

## Variational Autoencoder(VAE)

- [Variational Autoencoders Explained](http://kvfrans.com/variational-autoencoders-explained/)
    
    - [[1312.6114] Auto-Encoding Variational Bayes](https://arxiv.org/abs/1312.6114)
    
    - [VAE(Variational Autoencoder)的原理 - Shiyu_Huang - 博客园](https://www.cnblogs.com/huangshiyu13/p/6209016.html)

    > In an autoencoder, we add in another component that takes in the original images and encodes them into vectors for us. The deconvolutional layers then "decode" the vectors back to the original images.
    > 
    > ![](http://kvfrans.com/content/images/2016/08/autoenc.jpg)
    > 
    > We've finally reached a stage where our model has some hint of a practical use. We can train our network on as many images as we want. If we save the encoded vector of an image, we can reconstruct it later by passing it into the decoder portion. What we have is the standard autoencoder.
    > 
    > However, we're trying to build a generative model here, not just a fuzzy data structure that can "memorize" images. We can't generate anything yet, since we don't know how to create latent vectors other than encoding them from images.
    >
    > ---
    > 
    > We let the network decide this itself. For our loss term, we sum up two separate losses: the generative loss, which is a mean squared error that measures how accurately the network reconstructed the images, and a latent loss, which is the KL divergence that measures how closely the latent variables match a unit gaussian.
    > 
    > ```
    > generation_loss = mean(square(generated_image - real_image))
    > latent_loss = KL-Divergence(latent_variable, unit_gaussian)
    > loss = generation_loss + latent_loss
    > ```
    > 
    > In order to optimize the KL divergence, we need to apply a simple reparameterization trick: instead of the encoder generating a vector of real values, it will generate a vector of means and a vector of standard deviations.
    > 
    > ---
    > 
    > ![](http://kvfrans.com/content/images/2016/08/vae.jpg)
    > 
    > Let's say you were given a bunch of pairs of real numbers between [0, 10], along with a name. For example, 5.43 means apple, and 5.44 means banana. When someone gives you the number 5.43, you know for sure they are talking about an apple. We can essentially encode infinite information this way, since there's no limit on how many different real numbers we can have between [0, 10].
    > 
    > However, what if there was a gaussian noise of one added every time someone tried to tell you a number? Now when you receive the number 5.43, the original number could have been anywhere around [4.4 ~ 6.4], so the other person could just as well have meant banana (5.44).
    > 
    > The greater standard deviation on the noise added, the less information we can pass using that one variable.
    > 
    > Now we can apply this same logic to the latent variable passed between the encoder and decoder. The more efficiently we can encode the original image, the higher we can raise the standard deviation on our gaussian until it reaches one.


## Variational Deep Embedding : A Generative Approach to Clustering (VaDE)

- [[1611.05148] Variational Deep Embedding: An Unsupervised and Generative Approach to Clustering](https://arxiv.org/abs/1611.05148)

- [slim1017/VaDE: Python code for paper - Variational Deep Embedding : A Generative Approach to Clustering](https://github.com/slim1017/VaDE)




# energy based model

## A Tutorial on Energy-Based Learning

- [paper2.dvi - lecun-06.pdf](http://yann.lecun.com/exdb/publis/pdf/lecun-06.pdf)


## [1708.06008] Boltzmann machines and energy-based models

- [[1708.06008] Boltzmann machines and energy-based models](https://arxiv.org/abs/1708.06008)


## 什么是Energy Based Model（EBM）

- [(1 封私信 / 83 条消息)什么是Energy Based Model（EBM）？ - 知乎](https://www.zhihu.com/question/59264464)

    > 我感觉就是为了方便建模。
    > 
    > 比如在一个复杂系统里你要表示一个变量 ![x\in X](https://www.zhihu.com/equation?tex=x%5Cin+X) 的概率 P(x)，要满足如下性质：
    > 
    > -   P(x)>0
    > -   所有变量概率之和为1
    > -   方便计算
    > 
    > 你就可以想到用指数函数（因为大于0）。
    > 
    > 所以 P(x) 可以表示为：
    > 
    > ![P(x)=\frac{1}{Z}e^{f(x)}](https://www.zhihu.com/equation?tex=P%28x%29%3D%5Cfrac%7B1%7D%7BZ%7De%5E%7Bf%28x%29%7D)
    > 
    > f(x) 是关于 x 的函数，其中 Z 是normalize项 :
    > 
    > ![Z=\sum_{x\in X} e^{f(x)}](https://www.zhihu.com/equation?tex=Z%3D%5Csum_%7Bx%5Cin+X%7D+e%5E%7Bf%28x%29%7D)
    > 
    > 所以：
    > 
    > ![P(x)=\frac{e^{f(x)}}{\sum_{x\in X}e^{f(x)}}](https://www.zhihu.com/equation?tex=P%28x%29%3D%5Cfrac%7Be%5E%7Bf%28x%29%7D%7D%7B%5Csum_%7Bx%5Cin+X%7De%5E%7Bf%28x%29%7D%7D)
    > 
    > 哇是不是很像softmax。
    > 
    > 统计物理中玻尔兹曼(吉布斯)分布有着差不多的形式：
    > 
    > ![P(x)=\frac{e^{-E(x)}}{\sum_{x\in X} e^{-E(x)}}](https://www.zhihu.com/equation?tex=P%28x%29%3D%5Cfrac%7Be%5E%7B-E%28x%29%7D%7D%7B%5Csum_%7Bx%5Cin+X%7D+e%5E%7B-E%28x%29%7D%7D)
    > 
    > 这里的E表示状态的能量。
    > 
    > 之前的f(x)就可以写成：
    > 
    > ![f(x)=-E(x)](https://www.zhihu.com/equation?tex=f%28x%29%3D-E%28x%29)
    > 
    > 所以这样的建模方法就叫做能量模型啦。
    > 
    > 通常在机器学习中 E(x)通常可以表示为似然函数或者对数似然或者值函数，所以有时候求最大似然就可以被表示为求最小能量。
    > 
    > 比如在分类问题中，对于特征 ![X=\{x_1,x_2,...x_n\}](https://www.zhihu.com/equation?tex=X%3D%5C%7Bx_1%2Cx_2%2C...x_n%5C%7D) 和标签 ![y\in Y](https://www.zhihu.com/equation?tex=y%5Cin+Y) ,我们可以建立能量函数 E(X,y)，这时候能量函数代表着 X 和 y 的匹配程度，能量越低匹配程度越好。
    > 
    > 所以：
    > 
    > ![y*=\text{argmin}_{y\in Y}E(X,y)](https://www.zhihu.com/equation?tex=y%2A%3D%5Ctext%7Bargmin%7D_%7By%5Cin+Y%7DE%28X%2Cy%29)
    > 
    > 注意这时候最小化这个能量是用来推断结果的的，区别于最小化损失函数可以用来训练能量函数E。
    > 
    > 更多可以参考：[A Tutorial on Energy-Based Learning](https://link.zhihu.com/?target=http%3A//yann.lecun.com/exdb/publis/pdf/lecun-06.pdf)
    > 



## Boltzmann Machines in TensorFlow with examples

- [monsta-hd/boltzmann-machines: Boltzmann Machines in TensorFlow with examples](https://github.com/monsta-hd/boltzmann-machines)

## Restricted Boltzmann Machines (RBM)

- [Neural networks [5.1] : Restricted Boltzmann machine - definition - YouTube](https://www.youtube.com/watch?v=p4Vh_zMw-HQ&index=36&list=PL6Xpj9I5qXYEcOhn7TqghAJ6NAPrNmUBH)

- [Hugo Larochelle](http://info.usherbrooke.ca/hlarochelle/neural_networks/content.html)


- [Restricted Boltzmann Machines (RBM) — DeepLearning 0.1 documentation](http://deeplearning.net/tutorial/rbm.html)

- [Restricted Boltzmann Machine implementation in TensorFlow, before and after code refactoring. Blog post: http://blackecho.github.io/blog/programming/2016/02/21/refactoring-rbm-tensor-flow-implementation.html](https://gist.github.com/blackecho/db85fab069bd2d6fb3e7)


### Boltzmann distribution

- [umdberg / Boltzmann distribution](http://umdberg.pbworks.com/w/page/50584034/Boltzmann%20distribution)

    > ***Prerequisites:***
    > 
    > -   [Kinetic theory: the ideal gas law](http://umdberg.pbworks.com/w/page/48369572/Kinetic%20theory%3A%20the%20ideal%20gas%20law)
    > -   [The second law of thermodynamics: A probabilistic law](http://umdberg.pbworks.com/w/page/47845840/The%20Second%20Law%20of%20Thermodynamics%3A%20%20A%20Probabilistic%20Law) 
    > -   [Probability](http://umdberg.pbworks.com/w/page/42023832/Probability)
    > -   [Thermodynamic equilibrium and equipartition](http://umdberg.pbworks.com/w/page/50324802/Thermodynamic%20equilibrium%20and%20equipartition)   
    > 
    > The [Second Law of Thermodynamics](http://umdberg.pbworks.com/w/page/47845840/The%20Second%20Law%20of%20Thermodynamics%3A%20%20A%20Probabilistic%20Law) says that in response to random interactions (such as molecular collisions), an isolated system will tend to move toward more probable states.  To demonstrate this, [we used an example with coin tosses](http://umdberg.pbworks.com/w/page/42023832/Probability), saying that the arrangements HHHHHTTTTT and HHHHHHHHHH were equally probable, but there are many more ways to get 5 heads and 5 tails than to get 10 heads and 0 tails.  But real-life situations can be more complicated than coin tosses!  Sometimes each arrangement is **not** equally probable.  In particular, in a physical system, the probability of an arrangement may depend on its **energy**.  Therefore, to figure out what's going to happen when there are different energies involved, we need to take into account both energy and entropy.
    > 
    > For example, when two molecules collide in an thermal environment, some of the kinetic energy might go into the internal energy of one or both of the molecules. It could set the molecule vibrating or spinning, putting energy into the internal degrees of freedom of the molecule. So for all the molecules of a particular type in a block of matter, we expect that some of them will have more energy in their rotational degree of freedom than others. Let's try to figure out how the probability of an arrangement depends on its energy.
    > 
    > What we can infer from how two systems must combine
    > ---------------------------------------------------
    > 
    > Let's imagine splitting our system into two parts, which we'll call A and B.  Now we can make two observations:
    > 
    > -   The energy of the entire system equals the energy of subsystem A plus the energy of subsystem B, or if you like, *E*~AB~ *= E*~A~ *+ E*~B~ .  This should need no explanation!
    > -   The two parts of the system are each in some arrangement.  If *P*~AX~ is the probability that subsystem A is in arrangement X, and *P*~BY~ is the probability that subsystem B is in arrangement Y, then what is the probability that the entire system (AB) is in this combined arrangement (XY)?  From the rules of probability, we know that we have to **multiply** them: *P*~(AB)(XY)~ = (*P*~AX~ * *P*~BY~).  For example, if you flip a coin and roll a die at the same time, the probability that you **both** flip tails **and** roll 5 is (1/2)*(1/6) = (1/12).  (This is related to the principle that you saw in this ['80s music video](http://www.youtube.com/watch?v=w0i_ZFlGTVY).)
    > 
    > In summary,
    > 
    > *When systems combine, energies add and probabilities multiply. *
    > 
    > So if we express the probability of a given state as a function of the energy, it must satisfy the relationship *P*(*E*~A~ + *E*~B~) = *P*(*E*~A~) * P(*E*~B~) for all possible values of *E*~A~ and *E*~B~.
    > 
    > Creating a distribution that has the right properties
    > -----------------------------------------------------
    > 
    > We need a probability distribution for energy that satisfies that when you add the energies in two parts of the system, the probabilities multiply. What types of functions satisfy this relationship?  Let's try exponential, since we know e^*x+y*^ = e^*x*^ * e^*y*^ for all *x* and *y*.
    > 
    > So can we just say the probability of arrangement i (with energy *E*~i~) is just *P*(i) = e^*E*~i~^ ?  No way!  *E*~i~ has units of energy, and you can't take an exponential of a quantity that has units. You wouldn't want to get a different result if you calculated in calories instead of Joules! The exponent has to be dimensionless.  So we have to divide *E*~i~ (in the exponent) by something else with units of energy so that the units cancel.  Where can we get another energy?  Is there a natural energy scale to which we can compare the energy of a given arrangement (so that we end up with just a dimensionless ratio)?  Yes, there is:  As we [saw before](http://umdberg.pbworks.com/w/page/48369572/Kinetic%20theory%3A%20the%20ideal%20gas%20law), we can use the Boltzmann constant *k*~B~ to convert the temperature of the system into an energy, so *k*~B~*T* has units of energy, and *E*i/*k*~B~*T* is dimensionless.
    > 
    > So can we say that the probability function is *P*(i) = e^*E*~i~/*k*~B~*T*^?  That's not **obviously** wrong in the way that e^*E*~i~^ is - at least the expression makes mathematical sense.  But let's play the [implications game](http://umdberg.pbworks.com/41981131/Playing%20the%20implications%20game) to see whether it makes **physical** sense.  If you plug in numbers to this expression, you see that an arrangement with greater energy has a greater probability than another arrangement (at the same temperature) with less energy.  But that can't be right.  It should be more difficult to get to an arrangement with greater energy (and therefore **less** probable).
    > 
    > ---
    > 
    > Let's try putting in a negative sign:  *P*(i) = e^*-E*~i~/*k*~B~*T*^*.* Now does this make physical sense?  A graph of the relationship between probability and energy (at a given temperature) is shown at the right.
    > 
    > So as the energy of an arrangement increases, the probability decreases.  At very high energies, the probability never quite reaches zero, but becomes **very** small.  This distribution is known as the ***Boltzmann distribution***.
    > 
    > 
    > 
    > ![](http://umdberg.pbworks.com/f/1322594209/P%20vs%20E.png)
    > 
    > 
    > ---
    > 
    > Now let's see how this probability distribution depends on temperature.  *T* is in the denominator inside the exponent (not something we're accustomed to seeing!).  As *T* increases, the denominator gets larger, which means the fraction *E*i/*k*~B~*T* gets smaller.  But this fraction in the exponent is negative, so the exponent actually gets less negative, i.e. larger, so the probability of a given arrangement increases as you go to higher temperature.  In other words, raising the temperature of the whole system makes it easier to get to higher-energy arrangements.  This relationship looks like the figure at the right.
    > 
    > 
    > ![](http://umdberg.pbworks.com/f/1322594750/P%20vs%20T.png)
    > ---
    > 
    > There's just one part of this result that can't possibly be right:  Try plugging in 0 for the energy, and you get e^0^ = 1 for the probability, suggesting that there is a 100% probability that the system will be in a state with zero energy!  Impossible, because the sum of **all** the probabilities has to add up to 1.  To fix this, we can put a normalization constant out in front:  *P*(i) = *c* e^*-E*~i~/*k*~B~*T*^ *.* But we won't worry about what this constant actually is, because we're mainly concerned about the **relative** probabilities of two different states at the same temperature, and when we take the ratio of two probabilities, the constant cancels out:  P(i)/P(j) = e^*-*(*E*~i~-*E*~j~)/*k*~B~*T*^
    > 
    > For example, at room temperature (300 K), *k*~B~*T* = 1/40 eV = 4.14 x 10^-21^ J or *RT* = *N~A~k~B~T* = 2.5 kJ/mol.  So if there are two different arrangements with an energy difference of 5 kJ/mol between them, then the lower-energy arrangement is 7.4 times as probable as the higher-energy arrangement.  (Run the numbers for yourself to check this.)  However, if we heat the system up to 600 K, then the lower-energy arrangement is only 2.7 times as probable: it becomes easier to access the higher-energy arrangement.
    > 
    > Here's what the Boltzmann distribution looks like at different temperatures:
    > 
    > ![](http://umdberg.pbworks.com/f/1328468704/Boltzmann.png)
    > 
    > Note that at different T's at high energies of excitation, the ordering is as we would expect. Higher excitation energies are more probable at higher temperatures. But at low energy is works the opposite! This is because of the normalization constant, c, which depends on temperature. A good way of thinking about it is this: If we start at a temperature T~1~, we have the distribution shown. If we add heat and raise the temp, the higher energy excitations get more probable. But that probability has to come from somewhere! It comes from depleting the highly probable low energy excitations and moving them up to a higher energy. Since we are plotting a probability, the area under the curve has to be 1. If we raise it at the high end, we have to lower it at the low end.
    > 
    > **Postscript**
    > 
    > The Boltzmann distribution only applies to individual arrangements of particles.  But if there are multiple arrangements that give the same overall energy (just as we showed that there are multiple ways to flip 10 coins and get 5 heads and 5 tails), we still need to multiply the probability of each arrangement by the number of arrangements.  We'll explore the consequences of combining energy and entropy (probability) in the follow-on page. 
    > 
    > ***Follow-ons:***
    > 
    > -   [Boltzmann distribution and Gibbs free energy](http://umdberg.pbworks.com/Boltzmann-distribution-and-Gibbs-free-energy).
    > 
    > Ben Dreyfus 11/29/11


### Boltzmann distribution and Gibbs free energy

- [umdberg / Boltzmann distribution and Gibbs free energy](http://umdberg.pbworks.com/w/page/49681668/Boltzmann%20distribution%20and%20Gibbs%20free%20energy)

    > ***Prerequisites:***
    > 
    > -   [Gibbs free energy](http://umdberg.pbworks.com/Gibbs-free-energy)
    > -   [Boltzmann distribution](http://umdberg.pbworks.com/Boltzmann-distribution)
    > 
    > The Boltzmann factor, e^-*E*/*k*~B~*T*^,tells us the relative probability of a particular arrangement (with a given energy).  And if we're dealing with a system at constant pressure, we can use enthalpy as the relevant energy, and call it e^-*H*/*k*~B~*T*^.
    > 
    > But as we discussed at the end of the [Boltzmann distribution](http://umdberg.pbworks.com/Boltzmann-distribution) page, that's not the whole story:  we need to multiply it by the number of different arrangements at a given energy.  Let's do the math and see what happens.
    > 
    > We know *S* = *k*~B~ ln *W* (where *S* is the entropy and *W* is the number of arrangements), so solving for *W* we get *W* = e^*S*/*k*~B~^
    > 
    > So to find the overall probability that a system is in a given state, we multiply these together:
    > 
    > *W* * e^-*H*/*k*~B~*T*^ = e^*S*/*k*~B~^ *  e^-*H*/*k*~B~*T*^ = e^*TS*/*k*~B~*T*^ * e^-*H*/*k*~B~*T*^ = e^-(*H*-*TS*)/*k*~B~*T*^
    > 
    > What's *H - TS*?  Hey, it's Gibbs free energy!
    > 
    > So the overall probability is actually proportional to e^-*G*/*k*~B~*T*^.
    > 
    > This tells us two things:
    > 
    > 1) It's another way to illustrate that Gibbs free energy combines the effects of energy (here, that's the original Boltzmann factor) and of entropy (the number of possible arrangements)
    > 
    > 2) This means that (for systems at constant pressure and temperature) Gibbs free energy is what **really** tells us which states are more probable, and therefore what a system is actually going to do.  That's why Gibbs free energy gets so much attention in chemistry and biology.
    > 
    > Ben Dreyfus 1/9/12


### Gibbs free energy

- [umdberg / Gibbs free energy](http://umdberg.pbworks.com/w/page/50493326/Gibbs%20free%20energy)

    > ***Prerequisites:***
    > 
    > -   [Enthalpy](http://umdberg.pbworks.com/Enthalpy)
    > -   [Entropy and heat flow](http://umdberg.pbworks.com/w/page/50394314/Entropy%20and%20heat%20flow)
    > -   [Motivating the Gibbs free energy](http://umdberg.pbworks.com/w/page/50542917/Motivating%20the%20Gibbs%20free%20energy)
    > 
    > When we have a transformation within a system -- a chemical reaction, a change in pressure or volume, the transfer of thermal energy from one place to another -- the interaction of that transfer with the external world is constrained by the second law of thermodynamics: the total entropy of the universe must increase. This means that if the entropy of the system we are considering decreases, some of our energy must be dumped into the external world.  And it has to be enough so that the entropy of the world external to our system increases by at least as much as the entropy of our system is decreasing. As a result, we can't use all the energy in the transformation: some of it has to be dumped outside.  What remains after that has been given away is the *free energy.* The *sign* of the free energy tells us whether or not *enough* energy has indeed been dumped into the environment such that the overall entropy of the universe increases (as it must for a process to occur).  **If the sign of the free energy change is negative, enough energy was dumped into the environment and the process can happen spontaneously.  If the sign of the free energy change is positive, not enough energy was dumped into the environment and the process cannot happen spontaneously!***\
    > *
    > 
    > Exactly what free energy we use depends on what system we are describing. Since most biological systems function at a constant pressure and temperature, the appropriate form is called the *Gibbs free energy*.
    > 
    > Using the simple model of a heat dump, we can now figure out how much energy we can't use. If our entropy decreases by Δ*S*, then we have to dump an amount of heat equal to
    > 
    > *Q* = *T*Δ*S*.
    > 
    > This has to be subtracted off the energy we have available from our transformation.
    > 
    > Because we're dealing with systems at constant pressure, the energy we're using here (and balancing with entropy) includes the work done to keep the system at constant pressure:  i.e., **enthalpy**.
    > 
    > Putting this together, Gibbs free energy (*G*) is defined as *H* - *TS*.  But we only care about the **change** in Gibbs free energy, and so (remembering that we're also at constant temperature) we get the expression you've seen in chemistry:   Δ*G* = Δ*H* - *T*Δ*S*.
    > 
    > The sign of *G* is defined so that a system will tend to evolve in the direction of **decreasing** *G*.  (This is a somewhat arbitrary choice:  we could have defined *G* as *TS - H* instead, and then systems would evolve in the direction of increasing *G*.)
    > 
    > To understand why this expression for *G* makes sense, let's look at each part of the equation individually:
    > 
    > First of all, look at the minus sign.  This means there are two terms (Δ*H* and *T*Δ*S*) influencing Δ*G* in opposite directions.  Depending on which one is larger, Δ*G* can be either positive or negative.
    > 
    > Now look at Δ*H*.  It has the same sign as Δ*G* in the equation, so a negative Δ*G* (the direction in which things will proceed) is more likely if there is a negative Δ*H*.  Remember that Δ*H* = Δ*U* + *p*Δ*V*, so a negative Δ*H* can happen when we have decreasing internal energy (e.g. forming chemical bonds), and/or decreasing volume (taking up less space).  This term represents the tendency of systems to move to lower energy.
    > 
    > Next, look at the *-T*Δ*S* term.  It has a negative sign in front of it, so Δ*G* is more likely to be negative when Δ*S* is **positive**.  In other words, systems are likely to proceed in the direction of increasing entropy.  Since entropy has units of energy/temperature (J/K), this means that *T*Δ*S* has units of energy.  (If it didn't, this equation would make no sense!)
    > 
    > What is the role of temperature?  If the temperature is low, then the *T*Δ*S* term is small, and the Δ*H* term (which doesn't depend on temperature) is what matters.  In other words, things move towards lower energy and that's all there is.  Think about the Energy Skate Park, with the skateboarder starting from rest (or very small initial velocity); she's just going to go downhill.  It's just plain old classical mechanics; there's no random motion to worry about.  But if the temperature is high, then the *T*Δ*S* term is large (relative to the magnitude of Δ*H*), so random thermal motion is going to have more influence.  The system has enough thermal energy to access higher-energy states (and won't just "fall down" to the lowest state), and because of probability, it will move to higher entropy.
    > 
    > What if Δ*H* is very small?  Then Δ*G* is basically just -*T*Δ*S*, and only entropy matters in determining which direction a system will evolve.  An example of such a process is [diffusion](http://umdberg.pbworks.com/w/page/48208992/Diffusion%3A%20%20A%20Mechanistic%20View) (of particles that aren't interacting significantly).  This process is entropy-driven, and will proceed in the direction of particles being more spread out.  All the arrangements of particles have the same energy, so energy differences aren't significant in this process. 
    > 
    > What if Δ*S* is very small instead?  Then Δ*G* is basically just Δ*H*, and only energy matters.  It's like single-particle mechanics, where we only need to worry about the energy of (or the forces on) a single object, rather than the different arrangements of particles.
    > 
    > But sometimes Δ*H* and *T*Δ*S* have comparable magnitudes, and neither term can be ignored.  In such cases, Δ*G* tells us which tendency wins.  Those are the cases when the quantitative expression is most useful, since it's not qualitatively obvious (and the answer will change depending on the temperature).
    > 
    > A final note:  The sign of Δ*G* tells us which direction a reaction (or other process) will proceed.  But what impact does this have on the **rate** of the process?  Answer:  NONE!  Δ*G* is totally unrelated to how fast things happen!  There are some processes that have a negative Δ*G* (and are therefore "spontaneous") and yet proceed incredibly slowly.  This is why, in biological systems, we need enzymes (and other catalysts) to speed things up (without changing Δ*G*).
    > 
    > One more note just to bring things full circle.  The equation that we have written for Gibbs free energy is that for the system (reaction vessel or organism) that we are considering.  As such we can write:
    > 
    >    Δ*G*~system~ = Δ*H*~system~ - *T*Δ*S~system~*
    > 
    > As noted above, any change in enthalpy of the system is exchanged with the surroundings.  That enthalpy (or heat) will go towards altering the entropy of the surroundings.  Therefore:
    > 
    >    Δ*H*~system~ = -Δ*H*~surroundings~ = *-T*Δ*S~surroundings~*
    > 
    > We can therefore plug this into the equation for Δ*G*~system ~ to get:       
    > 
    >    Δ*G*~system~ = Δ*H*~system~ - *T*Δ*S~system~ = -TΔ*S~surroundings~ *- *T*Δ*S~system~
    > 
    > Since the change in entropy of the surroundings plus that of the system is just the change in entropy of the universe, we then get
    > 
    >    Δ*G*~system~ = -TΔ*S~universe~*
    > 
    > We know that for a spontaneous reaction, the entropy of the universe must increase.  As a result, spontaneous reactions must have
    > 
    >    Δ*G*~system~ < 0
    > 
    > Follow ons: [Gibbs free energy - non standard states](http://umdberg.pbworks.com/w/page/100500557/Gibbs%20free%20energy%20-%20non%20standard%20states)
    > 
    > Ben Dreyfus 1/11/12, intro and edits by Joe Redish 2/3/12; additions by Karen Carleton 9/13/15
    > 


### Why is the free energy minimized by the Boltzmann distribution

- [statistical mechanics - Why is the free energy minimized by the Boltzmann distribution? - Physics Stack Exchange](https://physics.stackexchange.com/questions/54692/why-is-the-free-energy-minimized-by-the-boltzmann-distribution?newreg=70af4ea1e11d43b187dee92fed9cc078)

    > You are on the right track.
    > 
    > Let me begin by being super explicit about what we are trying to prove for the benefit of all readers.
    > 
    > We assume, for the sake of simplicity (both mathematical and conceptual) that the system in question is finite-dimensional so that the probability distribution that describes its statistical mechanical state can be represented as a finite sequence of $p_i$'s that sum to one;
    > 
    > $$\begin{align} \rho = (p_1, \dots, p_n), \qquad \sum_{i=1}^n p_i = 1. \end{align}$$
    > 
    >  Next, we define a function $F$ as follows
    > 
    > $$\begin{align} F(\rho, T) = E(\rho) - TS(\rho) \end{align}$$
    > 
    >  where the ensemble average energy $E$ and entropy $S$ are defined as
    > 
    > $$\begin{align} E(\rho) = \sum_{i=1}^n p_iU_i, \qquad S(\rho) = -k_B \sum_{i=1}^np_i\ln p_i. \end{align}$$
    > 
    >  for a given distribution $\rho$, and for a given value of $T$. For notational convenience, be denote the Boltzmann probability distribution corresponding to temperature $T$ by
    > 
    > $$\begin{align} \rho^B(T) = (p_1^B(T), \dots, p_n^B(T)), \qquad p_i^B(T) = \frac{e^{-U_i/k_BT}}{\sum_i e^{-U_i/k_BT}} \end{align}$$
    > 
    >  Then I claim that
    > 
    > > 1.  The distribution $\rho^B(T)$ is a critical point of $F(\rho, T)$ in the space of all possible probability distributions $\rho$.
    > > 2.  The distribution $\rho^B(T)$ is a global minimum of $F(\rho, T)$ in the space of probability distributions whose energy matches that of the $\rho^B(T)$.
    > 
    > **Proof.** To prove statement 1, that $\rho^B(T)$ is a critical point of $F(\rho, T)$, we note that the claim we want to prove is a _constrained_ optimization problem because we want to verify that $F$ has a critical point among all _probability_ distributions, which are described by special sequences of $p_i$'s, namely those that sum to one. We therefore can't just take derivatives of $F$ with respect to $p_i$ and call it a day; we need to enforce the constraint that changes in 
    > 
    > $F$ that we consider preserve the property that the sum of the probabilities is one.
    > 
    > The standard way to do this is to introduce a Lagrange multiplier to enforce the desired constraint, but let's do this in a more direct, intuitive way. Suppose that we want to perturb the distribution $\rho = (p_1, \dots, p_n)$, but make sure that this perturbation doesn't affect the fact that the probabilities sum to 1. If we write our perturbations as $p_i +\delta p_i$, then this means that
    > 
    > $$\begin{align} 1 = \sum_{i=1}^n (p_i + \delta p_i) = \sum_{i=1}^n p_i + \sum_{i=1}^n \delta p_i \end{align}$$
    > 
    >  which, gives
    > 
    > $$\begin{align} \sum_{i=1}^n \delta p_i = 0. \tag{$\star$} \end{align}$$
    > 
    >  This condition ensures that we never stray away from probability distributions when we do these perturbations.
    > 
    > Next, let's examine what happens to $F$ to first order in $\delta p_i$ when we perturb the distribution $\rho$ in this way. The first order change in $F$ is given by
    > 
    > $$\begin{align} \delta F(\rho, T) &=\sum_{i=1}^n\frac{\partial F}{\partial p_i}(\rho, T)\delta p_i\\ &= \sum_{i,j=1}^n \frac{\partial}{\partial p_i}(p_jU_j -k_BTp_j\ln p_j)\delta p_i \\ &= \sum_{i,j=1}^n (\delta_{ij}U_j + k_B T (\delta_{ij}\ln p_j - \frac{p_j}{p_j}\delta_{ij}))\delta p_i \\ &= \sum_i(U_i + k_BT\ln p_i - k_BT)\delta p_i. \end{align}$$
    > 
    >  Now here is where the magic happens. Let us evaluate this first order change on the Boltzmann distribution at temperature $T$;
    > 
    > $$\begin{align} \delta F(\rho^B(T), T) &= \sum_i(U_i + k_BT(-\frac{U_i}{k_BT} - \ln Z) - k_BT)\delta p_i\\ &= \sum_{i=1}^n(U_i - U_i - k_BT(\ln Z +1))\delta p_i \\ &= -k_BT(\ln Z +1)\sum_{i=1}^n\delta p_i \\ &= 0 \end{align}$$
    > 
    >  where in the last step, we used the constraint $(\star)$. This is exactly the desired result! The first order change around the Boltzmann distribution vanishes which is precisely the statement that this distribution is a critical point of 
    > 
    > $F$.
    > 
    > To prove statement 2, we consider $F(\rho)$ for any $\rho$ whose ensemble average energy is equal to that of the Boltzmann distribution;
    > 
    > $$\begin{align} E(\rho) = E(\rho^B(T)). \end{align}$$
    > 
    >  If we compute the difference on the free energies of $\rho$ and $\rho^B(T)$, we find that
    > 
    > $$\begin{align} F(\rho, T) - F(\rho^B(T)) &= E(\rho) - T S(\rho) - E(\rho^B(T)) + TS(\rho^B(T)) \\ &= T\Big(S(\rho^B(T))-S(\rho)\Big) \end{align}$$
    > 
    >  Now, recall that the Boltzmann distribution is precisely that which _maximizes_ the entropy among all distributions that share the same ensemble average energy $E$, in other words
    > 
    > $$\begin{align} S(\rho^B(T)) \geq S(\rho). \end{align}$$
    > 
    >  It follows immediately that
    > 
    > $$\begin{align} F(\rho^B(T))\leq F(\rho) \end{align}$$
    > 
    >  which is exactly the desired result; the free energy for any other distribution with the same ensemble average energy is greater than that of the Boltzmann distribution!
    >  


### Musical TensorFlow

- [Musical TensorFlow, Part 1 - How to build an RBM in TensorFlow for making music](http://danshiebler.com/2016-08-10-musical-tensorflow-part-one-the-rbm/)

- [Musical TensorFlow, Part 2 - How to build an RNN-RBM for longer musical compositions in TensorFlow](http://danshiebler.com/2016-08-17-musical-tensorflow-part-two-the-rnn-rbm/)

### Is there a tool similar as Keras, Tensorflow that provides Restricted Boltzmann Machine model?

- [Is there a tool similar as Keras, Tensorflow that provides Restricted Boltzmann Machine model? - Quora](https://www.quora.com/Is-there-a-tool-similar-as-Keras-Tensorflow-that-provides-Restricted-Boltzmann-Machine-model)

    > RBM s aren't really preferred anymore, but caffe has them [Add a Restricted Boltzmann Machine layer by elezar - Pull Request #3568 - BVLC/caffe](https://github.com/BVLC/caffe/pull/3568/commits)
    > 
    > And tensorflow has them [https://gist.github.com/blackech...](https://gist.github.com/blackecho/db85fab069bd2d6fb3e7)
    > 
    > ---
    > 
    > Scikit learn has an RBM
    > 
    > I am currently working on an extension to this.
    > 
    > 

# GAN

## Mode colapse

- [整體 or 局部？用全新幾何角度構建 GAN 模型 - 幫趣](http://bangqu.com/2bx137.html#utm_source=Facebook_PicSee&utm_medium=Social)

    > ### 從幾何角度研究 Mode collapse 問題
    > 
    > 當然，從幾何和流型參數化的角度還可以給出對 GAN 更深入的理解，比如對 mode collapse 問題。在 GAN 的相關研究中，mode collapse 是一個被廣泛關注的問題。有很多相關的論文在從不同角度來研究和解決這個問題。
    > 
    > 而基於 Localized GAN 所揭示的幾何方法，我們可以從流型局部崩潰的角度來**解釋和避免 GAN 的 mode collapse**。具體來說，給定了一個 z，當 z 發生變化的時候，對應的 G(z) 沒有變化，那麼在這個局部，GAN 就發生了 mode collapse，也就是不能產生不斷連續變化的樣本。這個現象從幾何上來看，就是對應的流型在這個局部點處，沿着不同的切向量方向不再有變化。換言之，所有切向量不再彼此相互獨立--某些切向量要麼消失，要麼相互之間變得線性相關，從而導致流型的維度在局部出現缺陷（dimension deficient）。
    > 
    > 爲了解決這個問題，最直接的是我們可以給流型的切向量加上一個正交約束 (Orthonormal constraint)，從而避免這種局部的維度缺陷。下圖是在 CelebA 數據集上得到的結果。可以看到，通過對不同的切向量加上正交化的約束，我們可以在不同參數方向上成功地得到不同的變化。
    > 
    > ![整體 or 局部？阿里 CVPR 論文用全新幾何角度構建 GAN 模型](http://i2.bangqu.com/lf1/news/20180606/5b0625c47435b.png)
    > 
    > 上圖：在給定輸入圖像的局部座標系下對人臉的不同屬性進行編輯。



# 圖片生成


## CVE-GAN

- [漫談生成模型，從AE到CVAE-GAN - 幫趣](http://bangqu.com/7yE1f6.html#utm_source=Facebook_PicSee&utm_medium=Social)
    - [[1703.10155v1] CVAE-GAN: Fine-Grained Image Generation through Asymmetric Training](https://arxiv.org/abs/1703.10155v1)

    > 它有 4 大組件，對應到 4 個神經網絡，互爲補充，互相促進： 
    > 
    > *   E：編碼器（Encoder），輸入圖像 x，輸出編碼 z。
    > 
    >     如果還給定了類別 c，那麼生成的 z 就會質量更高，即更隨機，因爲可移除c中已包含的信息。
    > 
    > -   G：生成器（Generator）。輸入編碼 z，輸出圖像 x。
    > 
    >     如果還給定了類別 c，那麼就會生成屬於類別 c 的圖像。
    > 
    > -   C：分類器（Classifier）。輸入圖像 x，輸出所屬類別 c。這是我們的老朋友。
    > 
    > -   D：辨別器（Discriminator）。輸入圖像 x，判斷它的真實度。
    > 
    > 
    > 我們先看如果只使用部分組件會是怎樣。首先是 CVAE，如下圖所示：
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f615287833141444NYmU.png)
    > 
    > 然後是 CGAN，其中 y 代表對於真實度的判別，如下圖所示： 
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f615287833149608p5TH.png)
    > 
    > 它們的效果如下圖所示。
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f61528783315326X13z5.png)
    > 
    > 可見： 
    > 
    > -   CVAE 生成的圖像中規中矩，但是模糊。
    > 
    > -   CGAN 生成的圖像清晰，但有時會有明顯錯誤。
    > 
    > 所以 AE 和 GAN 的方法剛好是互補。 
    > 
    > CVAE-GAN 的架構如下圖所示：
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f61528783317230u9w9y.png)
    > 
    > 其中的 G 有 3 個主要目標： 
    > 
    > -   對於從 x 生成的 z，G 應能還原出接近 x 的 x'（像素上的接近）。這來自 AE 的思想。
    > 
    > -   G 生成的圖像應可由 D 鑑別爲屬於真實圖像。這來自 GAN 的思想。
    > 
    > -   G 生成的圖像應可由 C 鑑別爲屬於 c 類別。這與 InfoGAN 的思想有些相似。
    > 
    > 最終得到的 z 可相當好地刻畫圖像。例如，同樣的 z 在不同 c 下的效果如下圖所示。
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f61528783317884d633g.png)
    > 
    > 這裏的不同 c，代表不同的明星。相同的 z，代表其他的一切語義特徵（如表情，角度，光照等等）都一模一樣。
    > 
    > 於是，通過保持 z，改變 c，可輕鬆實現真實的換臉效果，如下圖所示。
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f6152878331967516B73.png)
    > 
    > CVAE-GAN 在語義插值上的效果也很出色，如下圖所示。
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f6152878332247033Vla.png)
    > 
    > 由於 CVAE-GAN 生成的樣本質量很高，還可用於增強訓練樣本集，使其他模型（如圖像分類網絡）得到更好的效果。


## SAGAN 自注意生成式對抗網絡

- [帶自注意力機制的生成對抗網絡，實現效果怎樣？ - 幫趣](http://bangqu.com/8833oT.html#utm_source=Facebook_PicSee&utm_medium=Social)

    > 在這個實現中，自注意機制會應用到生成器和鑑別器的兩個網絡層。像素級的自注意力會增加 GPU 資源的調度成本，且每個像素有不同的注意力掩碼。Titan X GPU 大概可選擇的批量大小爲 8，你可能需要減少自注意力模塊的數量來減少內存消耗。
    > 
    > ![](http://i2.bangqu.com/j/news/20180606/8833oT1528261215554cR2q2.png)
    > 
    > 


## VQ-VAE (Neural Discrete Representation Learning)

- [[1711.00937] Neural Discrete Representation Learning](https://arxiv.org/abs/1711.00937)

- [優拓 Paper Note ep.16: Neural Discrete Representation Learning](https://blog.yoctol.com/%E5%84%AA%E6%8B%93-paper-note-ep-16-neural-discrete-representation-learning-601d80f7f9ff)

    > 其中最中心的思想為 VQ-VAE (Vector Quantization-Variational Auto-Encoder)，最重要的一部份是 Vector Quantization，這樣的做法主要是為了解決所謂的 Posterior Collapse，避免在 Decoder 太強的情況下導致所得到的 Latents 是無用的，同時也能夠讓 Variance 不要太大。
    > 
    > 整體的模型圖如下：
    > 
    > ![](https://cdn-images-1.medium.com/max/2000/1*qyyhTBejuVXejVnA4BUwtQ.png)
    > 
    > 其中最重要的是 Embedding Space，將整體的 Latent Space 作為 K-way 分類，限定 Embedding Space 中僅有 k 個 Representation Vector。此為 Vector Quatization 的中心思想。
    > 
    > 舉例來說，我們可以將一張圖壓縮為許多的 Latent Class 的組合，像是上圖中下方即為其中一例，過 CNN Encoder 後再比較 Z(x) 與哪類 Embedding 較為接近，就轉換為該類 Embedding，依據則為下列方程式：
    > 
    > ![](https://cdn-images-1.medium.com/max/1600/0*MHdNg7oKXsT6TyYF.png)
    > 
    > ![](https://cdn-images-1.medium.com/max/1600/0*mDH_BkddkGK9WbbN.png)
    > 
    > 而其 Loss Function 為：
    > 
    > ![](https://cdn-images-1.medium.com/max/1600/0*DhHI4JBum108cTwj.png)
    > 
    > 第一項為 Reconstruction Loss，在做 Error Backpropagation 的時候傳到 Decoder Input 時就將其 Gradient 複製到 Encoder output，再繼續做 Back Propagation。
    > 
    > 第二項為 Error Backpropagate on Embedding Space，會將該類型的 Embedding e 拉近 Encoder Output Z(x)。
    > 
    > 第三項為 Commitment Loss，其用意為讓 Z(x) 能夠真正影響 Embedding Space，讓其訓練速度能夠跟上 Encoder Parameter 的訓練速度。
    > 
    > 
    > ---
    > 
    > 註：
    > 1.  在 [論文連結](https://arxiv.org/pdf/1711.00937.pdf) 中有許多圖片的例子可以參考。
    > 2.  在 [範例參考](https://avdnoord.github.io/homepage/vqvae/) 中也有許多人聲的例子，能夠做到不錯的人聲轉換。
    > 

## UNIT

- [UNIT 介紹 — Unsupervised Image-to-Image Translation – xiao sean – Medium](https://medium.com/@xiaosean5408/unit-%E4%BB%8B%E7%B4%B9-unsupervised-image-to-image-translation-1f9dc2a17cdd)

    > 我們可以先看一下 [Two Minute Papers](https://www.youtube.com/watch?v=dqxqbvyOnMY&feature=youtu.be)當中如何的介紹他。
    > 
    > 作者有將程式碼釋出 [Github](https://github.com/mingyuliutw/UNIT)：
    > 
    > > *請注意，目前版本的實作可能會和論文的有出入，要將branch切去version_02*
    > 
    > ### 成果圖
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/1*hCooeJFioz4JDZjOsNppRw.png)
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/1*jrI0vYc9InlvIiAjTdL1sw.png)
    > 
    > ### 簡介
    > 
    > 本文是在說圖片的風格轉換（style transfer），如貓轉成狗，
    > 
    > 這幾年風格轉換（style transfer)在GAN領域中算是很火紅的話題，
    > 
    > 大概從2015年紅到現在，相關的論文不少，有興趣的可以自己理解。
    > 
    > ### 概念
    > 
    > ### Unsupervised
    > 
    > 標題為：Unsupervised Image-to-Image Translation
    > 
    > 這邊的Unsupervised的概念如下
    > 
    > -   將兩個不同的dataset的圖片一起訓練， 例如：貓和狗
    > -   以往都是成對的資料輸入，以手勢來說，就是兩個人都比同樣的手勢，而這篇論文是可以不用成對的輸入。
    > 
    > ### Latent Space
    > 
    > 此paper的核心概念為Latent Space(共同特徵)。
    > 
    > 假如我們輸入的dataset是貓和狗，
    > 
    > 他們其實會有一些共同的特徵，如眼睛、鼻子、嘴巴、耳朵。
    > 
    > 我們的目標是希望可以學會這些特徵，
    > 
    > 如我們輸入大眼睛的狗狗，可以生成出大眼睛的貓咪照片
    > 
    > 架構如下
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/1*M1_BU7alWKfOk_x-Mj8jGQ.png)
    > 
    > 如上圖我們可以看到
    > 
    > -   2個encoder(下方稱作 Encoder-A, Encoder-B)
    > -   latent space(中間灰色部分)
    > -   2個decoder(下方稱作 Decoder-A, Decoder-B)
    > -   2個discriminator
    > 
    > 作者很貼心的幫我們列出每個model的結合，如Encoder + Decoder(Generator) = VAE。
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/1*eRcdtlI_EytNnNGC0UbuRg.png)
    > 
    > 這部分就屬於歷史演進了，有興趣的可以去研究GAN的進展。
    > 
    > 大家都是站在巨人的肩膀上做研究。
    > 


## On Unifying Deep Generative Models

- [[1706.00550] On Unifying Deep Generative Models](https://arxiv.org/abs/1706.00550)

- [(2 封私信 / 82 条消息)如何评价 On Unifying Deep Generative Models 这篇 paper? - 知乎](https://www.zhihu.com/question/60697472)

    > 
    > 回复评论里的提问：关于我们的工作与最近"试图统一VAE和GAN"工作比如 "[Adversarial Variational Bayes: Unifying Variational Autoencoders and Generative Adversarial Networks](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1701.04722.pdf)" 的关系：
    > 
    > [我们的论文（最近做了大的更新）](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1706.00550.pdf)里有讨论这些工作（see section 6）。Generally，这些论文提出了新的结合VAE和GAN的deep generative models (DGMs)，因此这里的"unifying"指combine两种model变成一个joint model。而我们则是试图对这些DGM models and algorithms建立一个统一的视角("unified view")，发现他们之间的关系，而不是设计新的model instance.
    > 
    > Specifically, 这篇Adversarial Variational Bayes主要是用implicit distribution作为VAE的inference model （而标准的VAE是assume 一个explicit inference distribution，比如Gaussian）。为了learn这个implicit distribution, 论文用了adversarial loss (因为implicit distribution不支持likelihood evaluation, 传统的reconstruction loss不适用)。最近类似的工作还有很多，比如我们论文里已经cite的[26,36,49,54], 大体思想都是用implicit distribution作为inference model。这些工作可以看做是我们提出的统一视角的一个特例，具体的说(专有名词太多就用英文写了)：
    > 
    > Briefly, these works are instances of the general idea proposed in our paper, i.e., **symmetric modeling of generation and inference** (section 6) --- we can apply implicit distributions and adversarial loss for *generation* (i.e., GANs). Symmetrically, we can apply implicit distributions and adversarial loss for *inference* with exact the same formulation, which are essentially what these works do. For example, if we let z be the observed data and x the latent code, InfoGAN is exactly a VAE with implicit distribution as its inference model.
    > 
    > The idea of symmetric view of generation and inference is one of the key insights of our work. It helps reveal the connections between GANs and ADA, as well as the resemblance of GANs to variational inference.
    > 
    > ===============分割线以下为原答案===========
    > 
    > 谢谢关注我们的工作。我们会对论文初稿继续改进，对不足之处也欢迎大家指正和交流。
    > 
    > 这个工作里我们的目标不是提出新的模型，而是希望对deep generative model （DGM）的几类基本方法重新formulate，揭示他们间的关系，建立统一的interpretation。统一的框架主要有两个好处：
    > 
    > （1）对已有模型以及种类繁多的变种有更好或者新的理解，把握算法演进的脉络；
    > 
    > （2）促进 后续研究中，各个本来相互独立的DGM研究方向的融合。期待论文提出的分析框架能促进后续更多的DGM算法/模型的提出。
    > 
    > 对于（1），论文的主要结论是: GANs 和 VAEs 大体上是在minimize 不同方向的KL Divergence。 *Roughly speaking*, 对优化generator P来说，GANs 做 min_{P} KL(P||Q)，VAEs 做 min_{P} KL(Q||P)。由此带来一些insights:
    > 
    > 1) GAN 的这个形式和贝叶斯推断的variational inference类似：把P看做inference model，Q看做posterior。因此我们是在用*inference*来解释*generation*。这一点在论文最后的discussion section有更具体的讨论。
    > 
    > 2) 优化两个方向的KL，正好和经典的wake sleep算法的两个phase对应。GAN可以看做sleep phase的extension，VAE可以看做wake phase的extension。
    > 
    > 3) 根据KL的不对称性质，GANs优化的KL(P||Q)决定了GANs倾向于miss mode，而VAEs倾向于cover mode。这点在之前的一些论文 e.g. [1][29],也有涉及。
    > 
    > 对于（2）,我们举了两个例子，来说明各种加强VAEs的方法能直接应用在GANs上来提高GANs，反之，之前用来提高GANs的方法也能用来提高VAEs。前者，我们从importance weighted VAEs出发可以很轻松推导出importance weighted GANs；后者，我们将GANs的对抗机制直接复制到VAEs上。实验基本没调过参数，不过对base model基本都有提高。



## Glow

- [[1807.03039] Glow: Generative Flow with Invertible 1x1 Convolutions](https://arxiv.org/abs/1807.03039)
    - [下一個GAN？OpenAI提出可逆生成模型Glow - 幫趣](http://bangqu.com/nNcD1K.html#utm_source=Facebook_PicSee&utm_medium=Social)
    - [Glow: Better Reversible Generative Models](https://blog.openai.com/glow/)
    - [[D] Glow: Better Reversible Generative Models：MachineLearning](https://www.reddit.com/r/MachineLearning/comments/8xe5lx/d_glow_better_reversible_generative_models/)

## GLANN

- [爲什麼讓GAN一家獨大？Facebook提出非對抗式生成方法GLANN - 幫趣](http://bangqu.com/KPA545.html)

    > GAN 有明顯的優勢，但也有一些關鍵的缺點：1）GAN 很難訓練，具體表現包括訓練過程非常不穩定、訓練突然崩潰和對超參數極其敏感。2）GAN 有模式丟失（mode-dropping）問題------只能建模目標分佈的某些模式而非所有模式。例如如果我們用 GAN 生成 0 到 9 十個數字，那麼很可能 GAN 只關注生成「1」這個數字，而很少生成其它 9 個數字。
    > 
    > 一般我們可以使用生日悖論（birthday paradox）來衡量模式丟失的程度：生成器成功建模的模式數量可以通過生成固定數量的圖像，並統計重複圖像的數量來估計。對 GAN 的實驗評估發現：學習到的模式數量顯著低於訓練分佈中的數量。
    > 
    > GAN 的缺陷讓研究者開始探索用非對抗式方案來訓練生成模型，GLO 和 IMLE 就是兩種這類方法。Bojanowski et al. 提出的 GLO 是將訓練圖像嵌入到一個低維空間中，並在該嵌入向量輸入到一個聯合訓練的深度生成器時重建它們。GLO 的優勢有：1）無模式丟失地編碼整個分佈；2）學習得到的隱含空間能與圖像的形義屬性相對應，即隱含編碼之間的歐幾里德距離對應於形義方面的含義差異。但 GLO 有一個關鍵缺點，即沒有一種從嵌入空間採樣新圖像的原則性方法。儘管 GLO 的提出者建議用一個高斯分佈來擬合訓練圖像的隱編碼，但這會導致圖像合成質量不高。
    > 
    > IMLE 則由 Li and Malik 提出，其訓練生成模型的方式是：從一個任意分佈採樣大量隱含編碼，使用一個訓練後的生成器將每個編碼映射到圖像域中並確保對於每張訓練圖像都存在一張相近的生成圖像。IMLE 的採樣很簡單，而且沒有模式丟失問題。類似於其它最近鄰方法，具體所用的指標對 IMLE 影響很大，尤其是當訓練集大小有限時。回想一下，儘管經典的 Cover-Hart 結果告訴我們最近鄰分類器的誤差率漸進地處於貝葉斯風險的二分之一範圍內，但當我們使用有限大小的示例樣本集時，選擇更好的指標能讓分類器的表現更好。當使用 L2 損失直接在圖像像素上訓練時，IMLE 合成的圖像是模糊不清的。
    > 
    > 在本研究中，我們提出了一種名爲「生成式隱含最近鄰（GLANN：Generative Latent Nearest Neighbors）」的新技術，能夠訓練出與 GAN 質量相當或更優的生成模型。我們的方法首次使用了 GLO 來嵌入訓練圖像，從而克服了 IMLE 的指標問題。由 GLO 爲隱含空間引入的迷人的線性特性能讓歐幾里德度量在隱含空間 Z 中具有形義含義。我們訓練了一個基於 IMLE 的模型來實現任意噪聲分佈 E 和 GLO 隱含空間 Z 之間的映射。然後，GLO 生成器可以將生成得到的隱含編碼映射到像素空間，由此生成圖像。我們的 GLANN 方法集中了 IMLE 和 GLO 的雙重優勢：易採樣、能建模整個分佈、訓練穩定且能合成銳利的圖像。圖 1 給出了我們的方法的一種方案。
    > 
    > ![](http://i2.bangqu.com/j/news/20181227/KPA54515458940876679XGj9.png)
    > 
    > *圖 1：我們的架構的示意圖：採樣一個隨機噪聲向量 e 並將其映射到隱含空間，得到隱含編碼 z = T(e)。該隱含編碼再由生成器投射到像素空間，得到圖像 I = G(z)*
    > 
    > 我們使用已確立的指標評估了我們的方法，發現其顯著優於其它的非對抗式方法，同時其表現也比當前的基於 GAN 的模型更優或表現相當。GLANN 也在高分辨率圖像生成和 3D 生成上得到了出色的結果。最後，我們表明 GLANN 訓練的模型是最早的能真正執行非對抗式無監督圖像轉換的模型。
    > 
    > **論文：使用生成式隱含最近鄰的非對抗式圖像合成**
    > 
    > ![](http://i2.bangqu.com/j/news/20181227/KPA5451545894088871peq21.png)
    > 
    > 論文鏈接：https://arxiv.org/pdf/1812.08985v1.pdf
    > 
    > 生成對抗網絡（GAN）近來已經主導了無條件圖像生成領域。GAN 方法會訓練一個生成器和一個判別器，其中生成器根據隨機噪聲向量對圖像進行迴歸操作，判別器則會試圖分辨生成的圖像和訓練集中的真實圖像。GAN 已經在生成看似真實的圖像上取得了出色的表現。GAN 儘管很成功，但也有一些關鍵性缺陷：訓練不穩定和模式丟失。GAN 的缺陷正促使研究者研究替代方法，其中包括變分自編碼器（VAE）、隱含嵌入學習方法（比如 GLO）和基於最近鄰的隱式最大似然估計（IMLE）。不幸的是，目前 GAN 仍然在圖像生成方面顯著優於這些替代方法。在本研究中，我們提出了一種名爲「生成式隱含最近鄰（GLANN）」的全新方法，可不使用對抗訓練來訓練生成模型。GLANN 結合了 IMLE 和 GLO 兩者之長，克服了兩種方法各自的主要缺點。結果就是 GLANN 能生成比 IMLE 和 GLO 遠遠更好的圖像。我們的方法沒有困擾 GAN 訓練的模式崩潰問題，而且要穩定得多。定性結果表明 GLANN 在常用數據集上優於 800 個 GAN 和 VAE 構成的基線水平。研究還表明我們的模型可以有效地用於訓練真正的非對抗式無監督圖像轉換。
    > 
    > **方法**
    > 
    > 我們提出的 GLANN（生成式隱含最近鄰）方法克服了 GLO 和 IMLE 兩者的缺點。GLANN 由兩個階段構成：1）使用 GLO 將高維的圖像空間嵌入到一個「行爲良好的」隱含空間；2）使用 IMLE 在一個任意分佈（通常是一個多維正態分佈）和該低維隱含空間之間執行映射。
    > 
    > **實驗**
    > 
    > 爲了評估我們提出的方法的表現，我們執行了定量和定性實驗來比較我們的方法與已確立的基線水平。
    > 
    > ![](http://i2.bangqu.com/j/news/20181227/KPA54515458940897055N94z.png)
    > 
    > *表 1：生成質量（FID/ Frechet Inception Distance）*
    > 
    > ![](http://i2.bangqu.com/j/news/20181227/KPA5451545894091353BqE4s.png)
    > 
    > *圖 2：在 4 個數據集上根據衡量的精度-召回率情況。這些圖表來自 [31]。我們用星標在相關圖表上標出了我們的模型在每個數據集上的結果。*
    > 
    > ![](http://i2.bangqu.com/j/news/20181227/KPA5451545894093264jd35e.png)
    > 
    > *圖 3：IMLE [24]、GLO [5]、GAN [25] 與我們的方法的合成結果比較。第一排：MNIST。第二排：Fashion。第三排：CIFAR10。最後一排：CelebA64。IMLE 下面空缺的部分在 [24] 中沒有給出。GAN 的結果來自 [25]，對應於根據精度-召回率指標評估的 800 個生成模型中最好的一個。*
    > 
    > ![](http://i2.bangqu.com/j/news/20181227/KPA545154589409658782q2A.png)
    > 
    > *圖 4：在 CelebA-HQ 上以 256×256 的分辨率得到的插值實驗結果。最左邊和最右邊的圖像是根據隨機噪聲隨機採樣得到的。中間的插值圖像很平滑而且視覺質量很高。*
    > 
    > ![](http://i2.bangqu.com/j/news/20181227/KPA5451545894099154q632A.png)
    > 
    > *圖 5：在 CelebA-HQ 上以 1024×1024 的分辨率得到的插值實驗結果*
    > 
    > ![](http://i2.bangqu.com/j/news/20181227/KPA5451545894101003762zK.png)
    > 
    > *圖 6：GLANN 生成的 3D 椅子圖像示例*
    > 
    > **討論**
    > 
    > **損失函數**：在這項研究中，我們用一種感知損失（perceptual loss）代替了標準的對抗損失函數。在實踐中我們使用了 ImageNet 訓練後的 VGG 特徵。Zhang et al. [40] 宣稱自監督的感知損失的效果並不比 ImageNet 訓練的特徵差。因此，我們的方法很可能與自監督感知損失有相似的表現。
    > 
    > **更高的分辨率**：分辨率從 64×64 到 256×256 或 1024×1024 的增長是通過對損失函數進行簡單修改而實現的：感知損失是在原始圖像以及該圖像的一個雙線性下采樣版本上同時計算的。提升到更高的分辨率只簡單地需要更多下采樣層級。研究更復雜精細的感知損失也許還能進一步提升合成質量。
    > 
    > **其它模態**：我們這項研究關注的重點是圖像合成。我們相信我們的方法也可以擴展到很多其它模態，尤其是 3D 和視頻。我們的方法流程簡單，對超參數穩健，這些優點使其可比 GAN 遠遠更簡單地應用於其它模態。我們在 4.4 節給出了一些說明這一點的證據。未來的一大研究任務尋找可用於 2D 圖像之外的其它域的感知損失函數。
    > 


# 動作合成

## Synthesizing Images of Humans in Unseen Poses

- [只需一張照片，運動視頻分分鐘僞造出來 | MIT新算法 - 幫趣](http://bangqu.com/o64789.html)

    > 將源圖像和它對應的2D姿勢信息，以及目標姿勢輸入到這個模型中，它就能合成出一張輸出圖像，把源圖像上的人物形象和目標姿勢結合在一起。
    > 
    > ![](http://i2.bangqu.com/liang/news/20180624/v2-610ea5c421549009d23e203874b1cc6c.jpg)
    > 
    > 這個方法的精髓，就在於把這個艱鉅的大任務分成四塊簡單的、模塊化的子任務，大概如下圖所示：
    > 
    > ![](http://i2.bangqu.com/liang/news/20180624/v2-9918a32aa0bd9bf16c94fdc1de943cca.jpg)
    > 
    > 製造新姿勢的流程分五步。
    > 
    > 第一步得**表示姿勢**，研究人員將2D的姿勢Ps和Pt表示成3D形式RH×W×J，其中H代表輸入圖像的高度，W代表寬度，每個J通道都包含一個以不同節點(x,y)爲中心的高斯凸起。這種方法能快速利用姿態輸入的空間特性，而不僅僅是個扁平、密集的表示。
    > 
    > 表示完動作後，就需要對圖像整體大局進行**原圖分割**，爲合成動作做準備了。
    > 
    > 運動時身體每個部分軌跡不同通常會分段仿射運動場出現，通過將原圖Is分割成前景層和背景層，並將前景的身體部位分割成頭、上臂、下臂、大腿、小腿和軀幹等部分，基於UNet-style架構將原圖分割。
    > 
    > 之後進行**前景空間變形**，將這些被拆分的身體重新組合起來。
    > 
    > ![](http://i2.bangqu.com/liang/news/20180624/v2-63974e2c09e6c375cd5974eed97009c8.jpg)
    > 
    > 之後進行**前景合成**，將轉換後的主體部分合並，進一步細化外觀。下圖顯示了這個階段的Mask Mt(第3列)和yfg(第4列)的幾個輸出示例。
    > 
    > ![](http://i2.bangqu.com/liang/news/20180624/v2-7b2ba05c1b01640201dad24b7179af6e.jpg)
    > 
    > 可以看出，即使一開始是很誇張的姿勢，合成出效果看起來也很真實。可惜的是，高爾夫球杆、網球拍等持有物，在合成後不會被保留。
    > 
    > 此時，完事具備，就差背景了。**背景合成**也就是填補前景動作中開始被遮擋的部分，如上圖第五列所示~
    > 



# 風格變換/跨域生成

## Learning to Discover Cross-Domain Relations with Generative Adversarial Networks

- [论文阅读：Learning to Discover Cross-Domain Relations with Generative Adversarial Networks - CSDN博客](https://blog.csdn.net/u010886794/article/details/78141357)


    > 一、目的
    > ====
    > 
    > 
    >    提出一个基于GAN的网络框架来学习发现跨域关系（cross-domain relation），把寻找这种关系变成了用一种风格的图片生成另一种风格。
    > 
    > 
    >    下面是论文列举的手提包生成鞋、鞋生成手提包的示意图。
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/TnLF6wB.jpg)
    > 
    > 二、模型
    > ====
    > 
    > 
    > GAB表示域A到域B的生成器，GBA表示域B到域A的生成器。为了找到有意义的对应关系，需要将这个映射限制成一对一映射，意思就是说，GAB和GBA应该是刚好相反的映射。对于所有的A里面的真实样本xA，GAB(xA)都要在B里面，对于GBA(xB)也一样。
    > 
    > 
    > 
    > 标准的GAN模型
    > --------
    > 
    > ![这里写图片描述](https://i.imgur.com/YveUKp5.jpg)
    > 
    > 
    >   图中xA、xB分别表示A里面和B里面的真实样本，xAB表示真实样本xA经生成器GAB生成的样本。
    > 
    > 
    > 
    > 标准的GAN模型很容易发生模式崩溃。
    > 
    > 带有重建损失的GAN模型
    > ------------
    > 
    > 
    > 基于前面所提出的一对一映射，对于所有的A里面的真实样本xA，GAB(xA)都要在B里面，这相当于要满足GBA(GAB(xA))=xA这个条件，但是这个条件很难优化，于是改为最小化距离d(GBA(GAB(xA)),xA)，这个d可以是L1，L2等等的度量函数。
    > 
    >    于是，标准的GAN模型就被改成了这样：
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/FeNhHMB.jpg)
    > 
    > 
    > 生成器的损失函数如下：
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/ZD7hIsg.jpg)
    > ![这里写图片描述](https://i.imgur.com/VXPONyc.jpg)
    > 
    > 
    > 生成器GAB收到两个损失，一个是重建损失(reconstruction loss),描述经过两个生成器之后的重建效果与原始真实样本的差距，另外一个是原始GAN的生成损失，表示GAB生成的样本来自B的逼真性。
    > 
    > 判别器的损失如下：
    > 
    > 
    > 
    > ![](https://i.imgur.com/OyQEgQE.jpg)
    > D表示相应域的判别器。
    > 
    > 
    > 相对于原始的GAN模型，这里的重建约束虽然迫使重建样本与原始的一样，但是这仍然会导致类似的模式崩溃问题。
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/gSM7ZGa.jpg)
    > 
    > 
    >  (a)是我们理想的映射，一对一的；(b)是原始GAN的结果，A中的多个模式映射到了B中的一个模式，就是模式崩溃的情况；(c)是加入了重建损失的GAN，A中两个模式的数据都映射到了B中的一个模式，而B中一个模式的数据只能映射到A中这两个模式中的一个。重建损失使得模型在(c)中的两个状态之间震荡，而并不能解决模式崩溃问题。
    >  
    >  个人的理解是，当A的数据放进去一起训练，由于不管是放进哪一个模式，GAB都会产生B中对应的一个模式,而GBA再生成的时候，当生成A中的第一个模式，和第二个模式就不像了，于是接下来重建损失会使得GBA再生成的数据往第二个模式靠拢，但是又不像A里面的第一个模式了，于是模型在这两者之间来回震荡，导致无法收敛。
    > 
    > 
    > 
    > DiscoGAN
    > --------
    > 
    > 
    > 为了解决模式崩溃的问题，就要使得不管是GAB还是GBA，不同模式生成出来的就应该是不同的，于是很自然地想到了对称结构，就是再加一个反过来的生成网络，迫使A和B中的数据一一对应。
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/xiyblG8.jpg)
    > 
    > 
    > 模型中包含两个生成器GAB，这两个GAB是一样的，还有两个生成器GBA，这两个也是一样的。这样就实现了一对一的映射。
    > 
    > 
    > 
    > 损失函数如下：
    > ![这里写图片描述](https://i.imgur.com/CkepbyO.jpg)
    > 
    > 记号和结构
    > -----
    > 
    > ![这里写图片描述](https://i.imgur.com/XlhPBAD.jpg)
    > 
    > 三、实验
    > ====
    > 
    > toy实验
    > -----
    > 
    > 
    >  首先为了证明所提出的这种对称模型对于模式崩溃问题的良好性能，做了一个演示实验。A和B中的数据都是二维的，真实样本都取自混合高斯模型。用3个线性层和一个ReLU激活层作为生成器，判别器用5个线性层，每层后面接一个ReLU层，最后再接一个sigmoid层将输出限定在[0,1]之间。
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/mPdhwfQ.jpg)
    > 
    > 
    >  彩色背景表示判别器的输出值，"x"表示B种不同的模式。(a)标示了10个目标模式和最初的转换结果；(b)是标准的GAN迭代40000次的结果；(c)是加入重建损失的网络迭代40000次的结果；(d)是文章提出的DiscoGAN迭代40000次后的结果。
    >  
    >  标准GAN的许多不同颜色的转换点都位于B相同的模式下，海蓝和浅蓝色的点离得很近，橙色和绿色的点也在一起，多种颜色的点（A中的多种模式）都映射到B的同一种模式下。带有重建损失的GAN的模式崩溃问题已经不那么严重了，但是海蓝、绿色和浅蓝色的点仍然会在少数几个模式上重叠。
    >  
    >  标准的GAN和带有重建损失的GAN都没有覆盖B中的所有模式，DiscoGAN将A中的样本转换为B中有边界不重叠的区域，避免了模式崩溃，并且产生的B样本覆盖了所有10种模式，因此这个映射是双射，从A转换的样本也把B的鉴别器个骗过了。
    > 
    > 
    > 
    > 转换实验
    > ----
    > 
    > 汽车到汽车\
    > ![这里写图片描述](https://i.imgur.com/iI9Uu90.jpg)
    > 
    > 人脸到人脸\
    > ![这里写图片描述](https://i.imgur.com/IjQXPjS.jpg)
    > 
    > 性别转换\
    > ![这里写图片描述](https://i.imgur.com/QVRQCWT.jpg)
    > 
    > 头发颜色转换\
    > ![这里写图片描述](https://i.imgur.com/mBwgxPl.jpg)
    > 
    > 是否戴眼镜转换\
    > ![这里写图片描述](https://i.imgur.com/4Mo3BtL.jpg)
    > 
    > 先转换性别，再转换头发颜色\
    > ![这里写图片描述](https://i.imgur.com/1fJYHMe.jpg)
    > 
    > 头发颜色、性别来回转\
    > ![这里写图片描述](https://i.imgur.com/kEyJymW.jpg)
    > 
    > 椅子到汽车，汽车到人脸\
    > ![这里写图片描述](https://i.imgur.com/KAGyOXT.jpg)
    > 
    > 轮廓和图像互转\
    > ![这里写图片描述](https://i.imgur.com/bF3shTp.jpg)
    > 
    > 附录
    > ==
    > 
    > 论文链接\
    > <https://arxiv.org/pdf/1703.05192.pdf>\
    > 论文相关博客\
    > <http://blog.csdn.net/u011636567/article/details/72678625>\
    > 代码地址\
    > 官方代码：<https://github.com/SKTBrain/DiscoGAN>\
    > 其他代码：<https://github.com/carpedm20/DiscoGAN-pytorch>\
    > Tensorflow简洁版本：<https://github.com/ChunyuanLI/DiscoGAN>
    > 


## [1808.04537] Learning Linear Transformations for Fast Arbitrary Style Transfer

- [New AI Style Transfer Algorithm Allows Users to Create Millions of Artistic Combinations - NVIDIA Developer News CenterNVIDIA Developer News Center](https://news.developer.nvidia.com/new-ai-style-transfer-algorithm-allows-users-to-create-millions-of-artistic-combinations/)

- [[1808.04537] Learning Linear Transformations for Fast Arbitrary Style Transfer](https://arxiv.org/abs/1808.04537)



# 異常偵測

## Anomaly Detection with Robust Deep Autoencoders

- [Anomaly Detection with Robust Deep Autoencoders](https://dl.acm.org/citation.cfm?id=3098052)




## [1805.12511] Cyberattack Detection using Deep Generative Models with Variational Inference
- [[1805.12511] Cyberattack Detection using Deep Generative Models with Variational Inference](https://arxiv.org/abs/1805.12511)

    > ![](https://screenshotscdn.firefoxusercontent.com/images/26a3753d-b194-4233-a6ec-9f8df472989b.png) 

## 杜倫大學提出GANomaly：無需負例樣本實現異常檢測 - 掃文資訊

- [杜倫大學提出GANomaly：無需負例樣本實現異常檢測 - 掃文資訊](https://hk.saowen.com/a/60fb44584916b0e9ae3f29c138f878161923e2ae74559cce432b6c1431913864?fbclid=IwAR0T_-rgy_AbvPQZM3N8hIWEdQ6kAIp0xHxEO433yac4QdfCbu4l2uUJqFg)

# 對抗樣本

- [對抗樣本的基本原理 - 幫趣](http://bangqu.com/5292n6.html#utm_source=Facebook_PicSee&utm_medium=Social)

    > 在原理上介紹對抗樣本，以經典的二分類問題爲例，機器學習模型通過在樣本上訓練，學習出一個分割平面，在分割平面的一側的點都被識別爲類別一，在分割平面的另外一側的點都被識別爲類別二。
    > 
    > ![對抗樣本的基本原理](http://i2.bangqu.com/lf1/news/20180601/5b10cf2ee3682.png)
    > 
    > 生成攻擊樣本時，我們通過某種算法，針對指定的樣本計算出一個變化量，該樣本經過修改後，從人類的感覺無法辨識，但是卻可以讓該樣本跨越分割平面，導致機器學習模型的判定結果改變。
    > 
    > ![對抗樣本的基本原理](http://i2.bangqu.com/lf1/news/20180601/5b10cf3a03ee8.png)
    > 
    > 如何高效的生成對抗樣本，且讓人類感官難以察覺，正是對抗樣本生成算法研究領域的熱點。


- [[1612.06299] Simple Black-Box Adversarial Perturbations for Deep Networks](https://arxiv.org/abs/1612.06299)






# 醫療

- [GAN打一個響指，假牙就設計好了（上臨牀測試ing - 幫趣](http://bangqu.com/9uu241.html)

# 生物

## 預測蛋白質折疊(AlphaFold)

- [AlphaFold: Using AI for scientific discovery | DeepMind](https://deepmind.com/blog/alphafold/)



# Generate Discrete data

- [Boundary-seeking GANs: A new method for adversarial generation of discrete data - Microsoft Research](https://www.microsoft.com/en-us/research/blog/boundary-seeking-gans-new-method-adversarial-generation-discrete-data/)


- [生成式对抗网络GAN有哪些最新的发展，可以实际应用到哪些场景中？ - 知乎](https://www.zhihu.com/question/52602529/answer/155743699)

    > 作者：莫驚蟄\
    > 链接：https://www.zhihu.com/question/52602529/answer/155743699\
    > 来源：知乎\
    > 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
    > 
    > 直接把GAN应用到NLP领域（主要是生成序列），有两方面的问题：
    > 
    > 1\. GAN最开始是设计用于生成连续数据，但是自然语言处理中我们要用来生成离散tokens的序列。因为生成器(Generator，简称G)需要利用从判别器(Discriminator，简称D)得到的梯度进行训练，而G和D都需要完全可微，碰到有离散变量的时候就会有问题，只用BP不能为G提供训练的梯度。在GAN中我们通过对G的参数进行微小的改变，令其生成的数据更加"逼真"。若生成的数据是基于离散的tokens，D给出的信息很多时候都没有意义，因为和图像不同。图像是连续的，微小的改变可以在像素点上面反应出来，但是你对tokens做微小的改变，在对应的dictionary space里面可能根本就没有相应的tokens.
    > 
    > 2.GAN只可以对已经生成的完整序列进行打分，而对一部分生成的序列，如何判断它现在生成的一部分的质量和之后生成整个序列的质量也是一个问题。
    > 
    > 近几篇重要的工作：
    > 
    > 1\. 为了解决这两个问题，比较早的工作是上交的这篇发表在AAAI 2017的文章：**SeqGAN: Sequence Generative Adversarial Nets with Policy Gradient，** 16年9月就放上了Arxiv上面了，而且也公布了源代码。
    > 
    > 利用了强化学习的东西来解决以上问题。如图，针对第一个问题，首先是将D的输出作为Reward，然后用Policy Gradient Method来训练G。针对第二个问题，通过蒙特卡罗搜索，针对部分生成的序列，用一个Roll-Out Policy（也是一个LSTM）来Sampling完整的序列，再交给D打分，最后对得到的Reward求平均值。
    > 
    > ![](https://pic3.zhimg.com/50/v2-4f2d3324ac0a945434860e3432e7c7d1_hd.jpg)
    > 
    > ![](https://pic3.zhimg.com/80/v2-4f2d3324ac0a945434860e3432e7c7d1_hd.jpg)
    > 
    > 完整算法如图：
    > 
    > ![](https://pic1.zhimg.com/50/v2-6008ee3851e7609fe3ab5a4c4cb6394c_hd.jpg)
    > 
    > ![](https://pic1.zhimg.com/80/v2-6008ee3851e7609fe3ab5a4c4cb6394c_hd.jpg)
    > 
    > 原文链接：[https://arxiv.org/pdf/1609.05473v5.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1609.05473v5.pdf)
    > 
    > Github链接：[LantaoYu/SeqGAN](https://link.zhihu.com/?target=https%3A//github.com/LantaoYu/SeqGAN)
    > 
    > 2\. 第二篇是C.Manning组大神Li Jiwei的文章：**Adversarial Learning for Neural Dialogue Generation，**用GAN和强化学习来做对话系统，如果我没有记错，这篇paper是最早引用SeqGAN的，有同学还说这篇是最早将RL用到GAN上的，主要是Jiwei大神名气太大，一放上Arxiv就引起无数关注。
    > 
    > 如图，文章也是用了Policy Gradient Method来对GAN进行训练，和SeqGAN的方法并没有很大的区别，主要是用在了Dialogue Generation这样困难的任务上面。还有两点就是：第一点是除了用蒙特卡罗搜索来解决部分生成序列的问题之外，因为MC Search比较耗费时间，还可以训练一个特殊的D去给部分生成的序列进行打分。但是从实验效果来看，MC Search的表现要更好一点。
    > 
    > 第二点是在训练G的时候同时还用了Teacher-Forcing（MLE）的方法，这点和后面的MaliGAN有异曲同工之处。
    > 
    > 为什么要这样做的原因是在对抗性训练的时候，G不会直接接触到真实的目标序列（gold-standard target sequence），当G生成了质量很差的序列的时候（生成质量很好的序列其实相当困难），而D又训练得很好，G就会通过得到的Reward知道自己生成的序列很糟糕，但却又不知道怎么令自己生成更好的序列， 这样就会导致训练崩溃。所以通过对抗性训练更新G的参数之后，还通过传统的MLE就是用真实的序列来更新G的参数。类似于有一个"老师"来纠正G训练过程中出现的偏差，类似于一个regularizer。
    > 
    > ![](https://pic1.zhimg.com/50/v2-46fa3718cd1bd1504b57d7feb07a97f0_hd.jpg)
    > 
    > ![](https://pic1.zhimg.com/80/v2-46fa3718cd1bd1504b57d7feb07a97f0_hd.jpg)
    > 
    > 原文链接：[https://arxiv.org/pdf/1701.06547.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1701.06547.pdf)
    > 
    > Github链接：[jiweil/Neural-Dialogue-Generation](https://link.zhihu.com/?target=https%3A//github.com/jiweil/Neural-Dialogue-Generation)
    > 
    > 3\. Yoshua Bengio组在二月底连续放了三篇和GAN有关的paper，其中我们最关心的是大神Tong Che和Li yanran的这篇：**Maximum-Likelihood Augmented Discrete Generative Adversarial Networks（MaliGAN），**简称读起来怪怪的。。。
    > 
    > 这篇文章的工作主要是两个方面：
    > 
    > 1.为G构造一个全新的目标函数，用到了Importance Sampling，将其与D的output结合起来，令训练过程更加稳定同时梯度的方差更低。尽管这个目标函数和RL的方法类似，但是相比之下更能狗降低estimator的方差（强烈建议看原文的3.2 Analysis，分析了当D最优以及D经过训练但并没有到最优两种情况下，这个新的目标函数仍然能发挥作用）
    > 
    > 2.生成较长序列的时候需要用到多次random sampling，所以文章还提出了两个降低方差的技巧：第一个是蒙特卡罗树搜索，这个大家都比较熟悉; 第二个文章称之为Mixed MLE-Mali Training，就是从真实数据中进行抽样，若序列长度大于N，则固定住前N个词，然后基于前N个词去freely run G产生M个样本，一直run到序列结束。
    > 
    > 基于前N个词生成后面的词的原因在于条件分布Pd比完整分布要简单，同时能够从真实的样本中得到较强的训练信号。然后逐渐减少N（在实验三中N=30, K=5， K为步长值，训练的时候每次迭代N-K）
    > 
    > ![](https://pic3.zhimg.com/50/v2-423a1050fa9b5636e682d92dd7501136_hd.jpg)
    > 
    > ![](https://pic3.zhimg.com/80/v2-423a1050fa9b5636e682d92dd7501136_hd.jpg)
    > 
    > Mixed MLE训练的MaliGAN完整算法如下：
    > 
    > ![](https://pic2.zhimg.com/50/v2-9c2bcba753585641ce1507802ace64f8_hd.jpg)
    > 
    > ![](https://pic2.zhimg.com/80/v2-9c2bcba753585641ce1507802ace64f8_hd.jpg)
    > 
    > 在12，梯度更新的时候，第二项（highlight的部分）貌似应该是logP![\theta](https://www.zhihu.com/equation?tex=%5Ctheta)（我最崇拜的学长发邮件去问过一作） 。至于第一部分为什么梯度是近似于这种形式，可以参考Bengio组的另一篇文章：**Boundary-Seeking Generative Adversarial Networks**
    > 
    > 这个BGAN的Intuition就是：令G去学习如何生成在D决策边界的样本，所以才叫做boundary-seeking。作者有一个特别的技巧：如图，当D达到最优的时候，满足如下条件，Pdata是真实的分布，Pg是G生成的分布。
    > 
    > ![](https://pic4.zhimg.com/50/v2-2642ebda15e8f1d2b29e497c40197bb9_hd.jpg)
    > 
    > ![](https://pic4.zhimg.com/80/v2-2642ebda15e8f1d2b29e497c40197bb9_hd.jpg)
    > 
    > 我们对它进行一点微小的变换：这个形式厉害之处在于，尽管我们没有完美的G，但是仍然可以通过对Pg赋予权重来得到真实的分布，这个比例就是如图所示，基于该G的最优D和（1-D）之比。当然我们很难得到最优的D，但我们训练的D越接近最优D，bias越低。而训练D（标准二分类器）要比G简单得多，因为G的目标函数是一个会随着D变动而变动的目标。
    > 
    > ![](https://pic3.zhimg.com/50/v2-49ee11359e258c14dfa4c0f787f2b589_hd.jpg)
    > 
    > ![](https://pic3.zhimg.com/80/v2-49ee11359e258c14dfa4c0f787f2b589_hd.jpg)
    > 
    > 文章后面给出了如何求梯度的数学公式，这里就不贴了。
    > 
    > 回到MaliGAN，作者给出了实验数据，比SeqGAN的效果要更好，看BLEU score.
    > 
    > ![](https://pic4.zhimg.com/50/v2-274b3811dc752bd302e50c8b30cc2594_hd.jpg)
    > 
    > ![](https://pic4.zhimg.com/80/v2-274b3811dc752bd302e50c8b30cc2594_hd.jpg)
    > 
    > 原文链接：[https://arxiv.org/pdf/1702.07983v1.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1702.07983v1.pdf)
    > 
    > 4\. 用SeqGAN做机器翻译，中科院自动化所在三月中旬放出了这篇文章：**Improving Neural Machine Translation with Conditional Sequence Generative Adversarial Nets，**这篇文章主要的贡献就是第一次将GAN应用到了NLP的传统任务上面，而且BLEU有2的提升。
    > 
    > 这个模型他们称之为CSGAN-NMT，G用的是传统的attention-based NMT模型，而D有两种方案，一种是CNN based，另一种是RNN based，通过实验比较发现CNN的效果更好。推测的原因是RNN的分类模型在训练早期能够有极高的分类准确率，导致总能识别出G生成的数据和真实的数据，G难以训练（因为总是negative signal）,
    > 
    > 这篇文章的重点我想是4.训练策略，GAN极难训练，他们首先是用MLE来pretrain G，然后再用G生成的样本和真实样本来pretrain D，当D达到某一个准确率的时候，进入对抗性训练的环节，GAN的部分基本和SeqGAN一样，用policy gradient method+MC search，上面已经讲过了不再重复。但是由于在对抗性训练的时候，G没有直接接触到golden target sentence，所以每用policy gradient更新一次G都跑一次professor forcing。这里我比较困惑，我觉得是不是像Jiwei那篇文章，是用D给出的Reward来更新G参数之后，又用MLE来更新一次G的参数（保证G能接触到真实的样本，这里就是目标语言的序列），但这个方法是teacher-forcing不是professor forcing。
    > 
    > 最后就是训练Trick茫茫，这篇文章试了很多超参数，比如D要pretrain到f=0.82的时候效果最好，还有pretrain要用Adam，而对抗性训练要用RMSProp，同时还要和WGAN一样将每次更新D的权重固定在一个范围之内。
    > 
    > 原文链接：[https://arxiv.org/pdf/1703.04887.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1703.04887.pdf)
    > 
    > 5.最后3月31号放到Arxiv上的文章：**Improved Training of Wasserstein GANs,** WGAN发布之后就引起轰动，比如Ian在Reddit上就点评了这篇文章，NYU的又祭出了这篇，令WGAN在NLP上也能发挥威力。
    > 
    > 在WGAN中，他们给出的改进方案是：
    > 
    > -   判别器最后一层去掉sigmoid
    > -   生成器和判别器的loss不取log
    > -   每次更新判别器的参数之后把它们的绝对值截断到不超过一个固定常数c
    > -   不要用基于动量的优化算法（包括momentum和Adam），推荐RMSProp，SGD也行
    > 
    > 这里引用自知乎专栏：[令人拍案叫绝的Wasserstein GAN - 知乎专栏](https://zhuanlan.zhihu.com/p/25071913)
    > 
    > 文章写得深入浅出，强烈推荐。
    > 
    > 其中第三项就是机器翻译文章中也用到的weight clipping，在本文中，他们发现通过weight clipping来对D实施Lipschitz限制（为了逼近难以直接计算的Wasserstein距离），是导致训练不稳定，以及难以捕捉复杂概率分布的元凶。所以文章提出通过梯度惩罚来对Critic（也就是D，WGAN系列都将D称之为Critic）试试Lipschitz限制。
    > 
    > 如图：损失函数有原来的部分+梯度惩罚，现在不需要weight clipping以及基于动量的优化算法都可以使用了，他们在这里就用了Adam。同时可以拿掉Batch Normalization。
    > 
    > ![](https://pic3.zhimg.com/50/v2-f345da0e5c68b1a7a6f2273bb9d3c19b_hd.jpg)
    > 
    > ![](https://pic3.zhimg.com/80/v2-f345da0e5c68b1a7a6f2273bb9d3c19b_hd.jpg)
    > 
    > 如图所示，实验结果很惊人，这种WGAN---GP的结构，训练更加稳定，收敛更快，同时能够生成更高质量的样本，而且可以用于训练不同的GAN架构，甚至是101层的深度残差网络。
    > 
    > ![](https://pic2.zhimg.com/50/v2-79721ebf87289ad49ffe8f3afd4c425e_hd.jpg)
    > 
    > ![](https://pic2.zhimg.com/80/v2-79721ebf87289ad49ffe8f3afd4c425e_hd.jpg)
    > 
    > 同时也能用于NLP中的生成任务，而且是character-level 的language model，而MaliGAN的实验是在Sentence-Level上面的。而且前面几篇提到的文章2,3,4在对抗性训练的时候或多或少都用到了MLE，令G更够接触到Ground Truth，但是WGAN-GP是完全不需要MLE的部分。
    > 
    > ![](https://pic2.zhimg.com/50/v2-59b2e1d2bf0701f02e9e847df1bb56da_hd.jpg)
    > 
    > ![](https://pic2.zhimg.com/80/v2-59b2e1d2bf0701f02e9e847df1bb56da_hd.jpg)
    > 
    > 原文链接：[https://arxiv.org/pdf/1704.00028.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1704.00028.pdf)
    > 
    > github地址：[https://github.com/igul222/improved_wgan_training](https://link.zhihu.com/?target=https%3A//github.com/igul222/improved_wgan_training)
    > 
    > 代码一起放出简直业界良心。
    > 
    > 6.3月31号还谷歌还放出了一篇BEGAN: Boundary Equilibrium Generative
    > 
    > Adversarial Networks，同时代码也有了是carpedm20用pytorch写的，他复现的速度真心快。。。
    > 
    > 最后GAN这一块进展很多，同时以上提到的几篇重要工作的一二作，貌似都在知乎上，对他们致以崇高的敬意。
    > 
    > 以上。
    > 



# Generate Functions 

- [[1807.04106] VFunc: a Deep Generative Model for Functions](https://arxiv.org/abs/1807.04106)




