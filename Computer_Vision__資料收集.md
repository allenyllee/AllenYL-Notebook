# Computer_Vision__資料收集

[toc]
<!-- toc --> 

## CNN heat map/activation maps/visuralizing

- [mrgloom/CNN-heatmap](https://github.com/mrgloom/CNN-heatmap)

- [Class activation maps in Keras for visualizing where deep learning networks pay attention](https://jacobgil.github.io/deeplearning/class-activation-maps)


## U-Net/V-Net

- [[1606.04797] V-Net: Fully Convolutional Neural Networks for Volumetric Medical Image Segmentation](https://arxiv.org/abs/1606.04797)

- [How to easily train a 3D U-Net or any other model for lung cancer segmentation.](https://medium.com/data-analysis-center/how-to-easily-train-a-3d-u-net-or-any-other-model-for-lung-cancer-segmentation-fc88f970d53)

- [「Deep Learning」V-Net - CSDN博客](https://blog.csdn.net/dgyuanshaofeng/article/details/78161987)

### NiftyNet

- [niftynet](http://niftynet.io/)

    >An open source convolutional neural networks platform for medical image analysis and image-guided therapy





## Loc2Vec

- [Loc2Vec: Learning location embeddings with triplet-loss networks | Sentiance](http://www.sentiance.com/2018/05/03/loc2vec-learning-location-embeddings-w-triplet-loss-networks/)



## 圖片壓縮

- [體積減半畫質翻倍，他用TensorFlow實現了這個圖像極度壓縮模型 - 幫趣](http://bangqu.com/u62hD2.html)

    - [[1804.02958] Generative Adversarial Networks for Extreme Learned Image Compression](https://arxiv.org/abs/1804.02958)
    - [Justin-Tan/generative-compression: TensorFlow Implementation of Generative Adversarial Networks for Extreme Learned Image Compression](https://github.com/Justin-Tan/generative-compression)


## 超解析度

- [阿里巴巴Poster論文：處理多種退化類型的卷積超分辨率 | CVPR 2018 - 幫趣](http://bangqu.com/kjzIo2.html#utm_source=Facebook_PicSee&utm_medium=Social)



## 圖片去噪/低亮度

- [無需額外硬件，全卷積網絡讓機器學習學會夜視能力 - 幫趣](http://bangqu.com/l1KYa5.html)

    - [[1805.01934] Learning to See in the Dark](https://arxiv.org/abs/1805.01934)

## 文字辨識(OCR)

- [Deep Learning based Text Recognition (OCR) using Tesseract and OpenCV | Learn OpenCV](https://www.learnopencv.com/deep-learning-based-text-recognition-ocr-using-tesseract-and-opencv/)

    > In today’s post, we will learn how to recognize text in images using an open source tool called Tesseract and OpenCV. The method of extracting text from images is also called Optical Character Recognition (OCR) or sometimes simply text recognition.
    > 

## 3D 重建

### 2018

- [Neural scene representation and rendering | DeepMind](https://deepmind.com/blog/neural-scene-representation-and-rendering/)


## 熱力圖

- [凭什么相信你，我的CNN模型？（篇一：CAM和Grad-CAM)](https://bindog.github.io/blog/2018/02/10/model-explanation/)

    > ## 0x01 反卷积和导向反向传播
    > 
    > 关于CNN模型的可解释问题，很早就有人开始研究了，姑且称之为CNN可视化吧。比较经典的有两个方法，反卷积(Deconvolution)和导向反向传播(Guided-backpropagation)，通过它们，我们能够一定程度上“看到”CNN模型中较深的卷积层所学习到的一些特征。当然这两个方法也衍生出了其他很多用途，以反卷积为例，它在图像语义分割中有着非常重要的作用。从本质上说，反卷积和导向反向传播的基础都是反向传播，其实说白了就是对输入进行求导，三者唯一的区别在于反向传播过程中经过ReLU层时对梯度的不同处理策略。在这篇[论文](https://arxiv.org/pdf/1412.6806.pdf)中有着非常详细的说明，如下图所示：
    > 
    > ![diff](http://lc-cf2bfs1v.cn-n1.lcfile.com/eec03f3347b4bbfe2c9e.png)
    > 
    > 虽然过程上的区别看起来没有非常微小，但是在最终的效果上却有很大差别。如下图所示：
    > 
    > ![compare_effect](http://lc-cf2bfs1v.cn-n1.lcfile.com/d3a78959f7bd98e45484.png)
    > 
    > 使用普通的反向传播得到的图像噪声较多，基本看不出模型的学到了什么东西。使用反卷积可以大概看清楚猫和狗的轮廓，但是有大量噪声在物体以外的位置上。导向反向传播基本上没有噪声，特征很明显的集中猫和狗的身体部位上。
    > 
    > 虽然借助反卷积和导向反向传播我们“看到”了CNN模型神秘的内部，但是却并不能拿来解释分类的结果，因为它们对类别并不敏感，直接把所有能提取的特征都展示出来了。在刚才的图片中，模型给出的分类结果是猫，但是通过反卷积和导向反向传播展示出来的结果却同时包括了狗的轮廓。换句话说，我们并不知道模型到底是通过哪块区域判断出当前图片是一只猫的。要解决这个问题，我们必须考虑其他办法。
    > 
    > ---
    > 
    > ## 0x02 CAM
    > 
    > 大家在电视上应该都看过热成像仪生成的图像，就像下面这张图片。
    > 
    > ![热成像仪](http://lc-cf2bfs1v.cn-n1.lcfile.com/b1d76465decdfdd82485.jpg)
    > 
    > 图像中动物或人因为散发出热量，所以能够清楚的被看到。接下来要介绍的CAM(Class Activation Mapping)产生的CAM图与之类似，当我们需要模型解释其分类的原因时，它以热力图（Saliency Map，我不知道怎么翻译最适合，叫热力图比较直观一点）的形式展示它的决策依据，如同在黑夜中告诉我们哪有发热的物体。
    > 
    > 对一个深层的卷积神经网络而言，通过多次卷积和池化以后，它的最后一层卷积层包含了最丰富的空间和语义信息，再往下就是全连接层和softmax层了，其中所包含的信息都是人类难以理解的，很难以可视化的方式展示出来。所以说，要让卷积神经网络的对其分类结果给出一个合理解释，必须要充分利用好最后一个卷积层。
    > 
    > ![CNN](http://lc-cf2bfs1v.cn-n1.lcfile.com/75fc645a087a1c3e6548.png)
    > 
    > CAM借鉴了很著名的论文*[Network in Network](https://arxiv.org/abs/1312.4400)*中的思路，利用GAP(Global Average Pooling)替换掉了全连接层。可以把GAP视为一个特殊的average pool层，只不过其pool size和整个特征图一样大，其实说白了就是求每张特征图所有像素的均值。
    > 
    > ![CNN_GAP](http://lc-cf2bfs1v.cn-n1.lcfile.com/e4a636f667f277cedc74.png)
    > 
    > GAP的优点在NIN的论文中说的很明确了：由于没有了全连接层，输入就不用固定大小了，因此可支持任意大小的输入；此外，引入GAP更充分的利用了空间信息，且没有了全连接层的各种参数，鲁棒性强，也不容易产生过拟合；还有很重要的一点是，在最后的 mlpconv层(也就是最后一层卷积层)强制生成了和目标类别数量一致的特征图，经过GAP以后再通过softmax层得到结果，这样做就给每个特征图赋予了很明确的意义，也就是categories confidence maps。如果你当时不理解这个categories confidence maps是个什么东西，结合CAM应该就能很快理解。
    > 
    > 我们重点看下经过GAP之后与输出层的连接关系(暂不考虑softmax层)，实质上也是就是个全连接层，只不过没有了偏置项，如图所示：
    > 
    > ![GAP_output](http://lc-cf2bfs1v.cn-n1.lcfile.com/2173d395c485a58a4b66.png)
    > 
    > 从图中可以看到，经过GAP之后，我们得到了最后一个卷积层每个特征图的均值，通过加权和得到输出(实际中是softmax层的输入)。需要注意的是，对每一个类别C，每个特征图k的均值都有一个对应的w，记为wck。CAM的基本结构就是这样了，下面就是和普通的CNN模型一样训练就可以了。训练完成后才是重头戏：我们如何得到一个用于解释分类结果的热力图呢？其实非常简单，比如说我们要解释为什么分类的结果是羊驼，我们把羊驼这个类别对应的所有wck
    > 
    > 取出来，求出它们与自己对应的特征图的加权和即可。由于这个结果的大小和特征图是一致的，我们需要对它进行上采样，叠加到原图上去，如下所示。
    > 
    > ![heatmap_sum](http://lc-cf2bfs1v.cn-n1.lcfile.com/42e1796d2fab354daf80.png)
    > 
    > 这样，CAM以热力图的形式告诉了我们，模型是重点通过哪些像素确定这个图片是羊驼了。
    > 
    > ---
    > 
    > ## 0x03 Grad-CAM方法
    > 
    > 
    > 前面看到CAM的解释效果已经很不错了，但是它有一个致使伤，就是它要求修改原模型的结构，导致需要重新训练该模型，这大大限制了它的使用场景。如果模型已经上线了，或着训练的成本非常高，我们几乎是不可能为了它重新训练的。于是乎，Grad-CAM横空出世，解决了这个问题。
    > 
    > Grad-CAM的基本思路和CAM是一致的，也是通过得到每对特征图对应的权重，最后求一个加权和。但是它与CAM的主要区别在于求权重wck
    > 
    > 的过程。CAM通过替换全连接层为GAP层，重新训练得到权重，而Grad-CAM另辟蹊径，用梯度的全局平均来计算权重。事实上，经过严格的数学推导，Grad-CAM与CAM计算出来的权重是等价的。为了和CAM的权重做区分，定义Grad-CAM中第k个特征图对类别c的权重为αck
    > 
    > ，可通过下面的公式计算：
    > 
    > αck=1Z∑i∑j∂yc∂Akij
    > 
    > 其中，Z
    > 
    > 为特征图的像素个数，yc是对应类别c的分数（在代码中一般用logits表示，是输入softmax层之前的值），Akij表示第k个特征图中，(i,j)
    > 
    > 位置处的像素值。求得类别对所有特征图的权重后，求其加权和就可以得到热力图。
    > 
    > LcGrad-CAM=ReLU(∑kαckAk)
    > 
    > Grad-CAM的整体结构如下图所示：
    > 
    > ![Grad-CAM结构](http://lc-cf2bfs1v.cn-n1.lcfile.com/531c1d38e0a0ddaf9553.jpg)
    > 
    > 注意这里和CAM的另一个区别是，Grad-CAM对最终的加权和加了一个ReLU，加这么一层ReLU的原因在于我们只关心**对类别c**
    > 
    > **有正影响的那些像素点**，如果不加ReLU层，最终可能会带入一些属于其它类别的像素，从而影响解释的效果。使用Grad-CAM对分类结果进行解释的效果如下图所示：
    > 
    > ![effect1](http://lc-cf2bfs1v.cn-n1.lcfile.com/2318799bf6bcc13e5218.png)
    > 
    > 除了直接生成热力图对分类结果进行解释，Grad-CAM还可以与其他经典的模型解释方法如导向反向传播相结合，得到更细致的解释。
    > 
    > ![effect2](http://lc-cf2bfs1v.cn-n1.lcfile.com/9c1076aee75f1d4a98ef.png)
    > 
    > 这样就很好的解决了反卷积和导向反向传播对类别不敏感的问题。当然，Grad-CAM的神奇之处还不仅仅局限在对图片分类的解释上，任何与图像相关的深度学习任务，只要用到了CNN，就可以用Grad-CAM进行解释，如图像描述(Image Captioning)，视觉问答(Visual Question Answering)等，所需要做的只不过是把yc
    > 
    > 换为对应模型中的那个值即可。限于篇幅，本文就不展开了，更多细节，强烈建议大家去读读[论文](https://arxiv.org/abs/1610.02391)，包括Grad-CAM与CAM权重等价的证明也在论文中。如果你只是想在自己的模型中使用Grad-CAM，可以参考这个[链接](https://github.com/Ankush96/grad-cam.tensorflow)，熟悉tensorflow的话实现起来真的非常简单，一看就明白。
    > 
    > ---
    > 
    > ## 0x04 扩展
    > 
    > 其实无论是CAM还是Grad-CAM，除了用来对模型的预测结果作解释外，还有一个非常重要的功能：就是用于物体检测。大家都知道现在物体检测是一个非常热门的方向，它要求在一张图片中准确的识别出多个物体，同时用方框将其框起来。物体检测对训练数据量的要求是非常高的，目前常被大家使用的有 PASCAL、COCO，如果需要更多数据，或者想要识别的物体在这些数据库中没有话，那就只能人工来进行标注了，工作量可想而知。
    > 
    > 仔细想想我们不难发现，Grad-CAM在给出解释的同时，不正好完成了标注物体位置的工作吗？虽然其标注的位置不一定非常精确，也不一定完整覆盖到物体的每一个像素。但只要有这样一个大致的信息，我们就可以得到物体的位置，更具有诱惑力的是，我们不需要人工标注的方框就可以做到了。
    > 
    > 顺便吐槽下当前比较火的几个物体检测模型如Faster-RCNN、SSD等，无一例外都有一个Region Proposal阶段，相当于“胡乱”在图片中画各种大小的方框，然后再来判断方框中是否有物体存在。虽然效果很好，但是根本就是违背人类直觉的。相比之下，Grad-CAM这种定位方式似乎更符合人类的直觉。当然这些纯属我个人的瞎扯，业务场景中SSD还是非常好用的，肯定要比Grad-CAM这种弱监督条件下的定位要强的多。
    > 
    > 

### Deconvolution

- [[1311.2901] Visualizing and Understanding Convolutional Networks](https://arxiv.org/abs/1311.2901)

### Guided-backpropagation

- [[1412.6806] Striving for Simplicity: The All Convolutional Net](https://arxiv.org/abs/1412.6806)

### CAM

- [[1512.04150] Learning Deep Features for Discriminative Localization](https://arxiv.org/abs/1512.04150)

### Grad-CAM

- [[1610.02391] Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization](https://arxiv.org/abs/1610.02391)

### Grad-CAM++

- [[1710.11063] Grad-CAM++: Generalized Gradient-based Visual Explanations for Deep Convolutional Networks](https://arxiv.org/abs/1710.11063)



