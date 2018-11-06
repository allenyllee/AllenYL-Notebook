# NLP__資料收集1-2_機器翻譯

[toc]
<!-- toc --> 


# 機器翻譯

## seq2seq

- [从Encoder到Decoder实现Seq2Seq模型](https://zhuanlan.zhihu.com/p/27608348)

- [Neural Machine Translation (seq2seq) Tutorial  |  TensorFlow](https://www.tensorflow.org/tutorials/seq2seq)

- [深度学习笔记——Word2vec和Doc2vec训练实例以及参数解读 - CSDN博客](https://blog.csdn.net/mpk_no1/article/details/72510655)

- [序列到序列的语言翻译模型代码(tensorflow)解析 - grt1st博客](https://www.grt1st.cn/posts/seq2seq-code/)

- [用seq2seq with attention实现中文歌词生成](https://zhuanlan.zhihu.com/p/25280463)

- [tensorflow代码全解析 -3- seq2seq 自动生成文本 - 简书](https://www.jianshu.com/p/9766b317ffa4)

- [從零開始的 Sequence to Sequence | 雷德麥的藏書閣](https://zake7749.github.io/2017/09/28/Sequence-to-Sequence-tutorial/)

- [教電腦寫作：AI球評——Seq2seq模型應用筆記(PyTorch + Python3) – Yi-Hsiang Kao – Medium](https://medium.com/@gau820827/%E6%95%99%E9%9B%BB%E8%85%A6%E5%AF%AB%E4%BD%9C-ai%E7%90%83%E8%A9%95-seq2seq%E6%A8%A1%E5%9E%8B%E6%87%89%E7%94%A8%E7%AD%86%E8%A8%98-pytorch-python3-31e853573dd0)

## ByteNet

- [《Neural Machine Translation in Linear Time》阅读笔记](https://zhuanlan.zhihu.com/p/23795111)

    - [[1610.10099] Neural Machine Translation in Linear Time](https://arxiv.org/abs/1610.10099)
    
    > **问题：** 提出了新型的source--target网络结构ByteNet，并通过两个扩张卷积神经网络（Dilated Convolution）堆叠实现,完成了机器翻译任务，并且将时间复杂度控制在线性范围。
    > 
    > **相关工作：**
    > 
    > 1、扩张卷积神经网络
    > 
    > Dilated Convolution network最近很火，2016ICLR上才被提出，本身是用在图像分割领域，但立马被deepmind拿来应用到语音(WaveNet)和nlp领域，且均取得不错的效果。
    > 
    > Dilated Convolution的产生是为了解决全卷积网络（FCN）在图像分割领域的问题，图像分割需要输入和输出在像素的shape保持一致，但由于池化层的存在导致FCN需要通过上采样扩增size,但是上采样并不能将丢失的信息无损的找回所以存在不足。
    > 
    > Dilated Convolution想法很粗暴，既然池化的下采样操作会带来信息损失，那么就把池化层去掉。但是池化层去掉随之带来的是网络各层的感受野变小，这样会降低整个模型的预测精度。Dilated convolution的主要贡献就是，如何在去掉池化下采样操作的同时，而不降低网络的感受野。
    > 
    > ![](https://pic1.zhimg.com/80/v2-3cd4e5ebcae5fa15019c9f4df03bc734_hd.png)
    > 
    > 以![3\times 3](http://www.zhihu.com/equation?tex=3%5Ctimes+3)的卷积核为例，传统卷积核在做卷积操作时，是将卷积核与输入张量中"连续"的![3\times 3](http://www.zhihu.com/equation?tex=3%5Ctimes+3)的patch逐点相乘再求和（如上图a，红色圆点为卷积核对应的输入"像素"，绿色为其在原输入中的感知野）。而dilated convolution中的卷积核则是将输入张量的![3\times 3](http://www.zhihu.com/equation?tex=3%5Ctimes+3)patch隔一定的像素进行卷积运算。如上图b所示，在去掉一层池化层后，需要在去掉的池化层后将传统卷积层换做一个"dilation=2"的dilated convolution层，此时卷积核将输入张量每隔一个"像素"的位置作为输入patch进行卷积计算，可以发现这时对应到原输入的感知野已经扩大（dilate）为![7\times 7](http://www.zhihu.com/equation?tex=7%5Ctimes+7)；同理，如果再去掉一个池化层，就要将其之后的卷积层换成"dilation=4"的dilated convolution层，如上图c所示。这样一来，即使去掉池化层也能保证网络的感受野，从而确保图像语义分割的精度。
    > 
    > ![](https://pic3.zhimg.com/80/v2-d1b7575900e42c5189997de03059d126_hd.png)
    > 
    > 上图是WaveNet里的Dilated Convolution的示意图，理解起来更容易，卷积的的输入像素的间距由1-2-4-8，虽然没有池化层，但是随着层数越深覆盖的原始输入信息依旧在增加。
    > 
    > **主要内容：**
    > 
    > （1）网络结构ByteNet
    > 
    > ![](https://pic1.zhimg.com/80/v2-0d72713562d4015e420f159e703958a8_hd.png)
    > 
    > ByteNet的核心分别是蓝色网络为target network, 红色网络为source network,相比其他encode-decode网络的区别在于，不再仅仅通过一个encode vector或者attention vector连接两个网络，而是将source network每一个输出都作为target vector对应位置上的输入。
    > 
    > 上图示例是以Dilated Convolution实现，实际本文提出的ByteNet的两个部分target network和source network均可以用RNN实现。
    > 
    > ![](https://pic3.zhimg.com/80/v2-b6f86867a9721e9874a65c65772d54ee_hd.png)
    > 
    > 本文就一个公式，理解起来就是当前预测词的输出概率由已预测词和当前token的source network encode vector决定。
    > 
    > 以下为本文的几个关键知识点
    > 
    > （2）Dynamic Unfolding
    > 
    > ![](https://pic2.zhimg.com/80/v2-e79507690ba294fbd8324cdd0033fb75_hd.png)
    > 
    > target网络的结束标志是以生成结束符EOS为标志，但由网络结构可以看到，target network的当前token的source vector输入长度和source input length是一致，由于翻译任务的长度存在变化，所以EOS出现位置可能长于source input length，因此byteNet当超出source input length时，target network的输出只有已解码词决定。
    > 
    > （3）Masked One-dimensional Convolutions
    > 
    > 为了避免在解决的时候卷积过程引入为解码词信息，引入Masked One-dimensional Convolutions，即卷积核只与当前token之前的输入进行卷积操作。
    > 
    > （4）Residual Blocks
    > 
    > ![](https://pic2.zhimg.com/80/v2-6163436971c333afb27f7567807be145_hd.png)
    > 
    > 卷积网络使用残差卷积网络。残差卷积网络的特点就是卷积层的最终输出由卷积结果和输入相加而得，因而变相理解为每一层只拟合输入和输出的残差，因而得名残差网络
    > 
    > （5）Sub-Batch Normalization
    > 
    > batch normalization是为了保持隐层的输出分布不发生漂移，而进行正规化操作，比如限定输出分布服从正态分布。好处是防止过拟合，防止梯度弥散，加大搜索跳出局部最小，保证源控件和目标空间一致（官方）
    > 
    > 标准的batch normalization会平均所有token的隐层输出，这会导致在target网络中要将未来时间步的考虑进来操作,这不符合时序关系，所以作者对BN层进行了改进，提出了sub batch normalization，大致意思，batch normalization分为两步，在全部训练完之前只用batch个sample里当前token以前的结果，训练完后再用所有结果一起normalization操作。
    > 
    > （6）Bag of Character n-Grams
    > 
    > 为了提高模型的信息容量，输入的每个token的vector不再单独是单独的词向量，而是相邻的n-grams的词的词向量求和。考虑到没有RNN模型特征融合的那么好而做的弥补吧。
    > 
    > **实验结果：**
    > 
    > （1）模型性能对比
    > 
    > ![](https://pic2.zhimg.com/80/v2-e17c18d8a0f70fa5ac08e76eeb4a311d_hd.png)
    > 
    > 作者还实验了将target network和source network分别用RNN实现，在上图实验列表里名为Recurrent ByteNet，注意和seq2seq的区别，seq2seq是取encode 网络的最后一个hidden state的输出作为decode网络的输入，而ByteNet中target network解码每个词的输入是由对应位置的source network输出决定，对应到RNN即source network第n个timeStep的输出作为target network第n个timestep的输入。
    > 
    > resolution preserving表示需要开辟额外空间保存历史信息。
    > 
    > Time代表时间复杂度，RP代表resolution preserving，Paths代表source网络从输入到输出的路径长度，Patht代表target网络从输入到输出的路径长度。Path越短代表反向传播的层数越少，网络越容易收敛，因为网络越浅越不容易出现梯度扩散。
    > 
    > （2）语言模型实验
    > 
    > 1、任务：字符生成预测，数据集为Hutter Prize version of the Wikipedia dataset
    > 
    > ![](https://pic4.zhimg.com/80/v2-7942cb10517176e4d562045f98bb4f13_hd.png)
    > 
    > ByteNet Decoder采用RNN实现，在交叉熵的评价指标上取得了state of the art结果。
    > 
    > 2、任务：机器翻译。数据集为WMT English to German translation task
    > 
    > ![](https://pic1.zhimg.com/80/v2-e81bdedfc7c6e9c6641325d8a0fadfdc_hd.png)
    > 
    > **简评：**
    > 
    > 1、虽然Dilated Convolution在某些实验任务上取得了不错的实验结果，但不能否认带池化层的卷积网络的优势，池化层存在特征选择的意义保留了强特征，从下采样的角度出发它降低了卷积网络的计算复杂度，因为随着卷积层的增加，通道个数也是呈倍数增加，如果不对应降低feature map的size,随着层数越深计算量就会变得相当大。
    > 
    > 2、但是没有池化层的Dilated Convolution使得卷积网络更适用于语音和文本，因为池化层的ave或者max操作要从全局出发，使得模型必须fix输入的规模。对于输入长度存在波动的语音和文本非常不方便。但是去掉池化层后使得前馈操作变得更灵活。
    > 
    > 3、本文的网络结构相比传统的seq2seq模型，优势在于训练时source network和target network均可并行计算，在预测时source network可并行计算。另外它在长输入问题上的优势应该更大。该网络可能将目前局限于两三句输入的自动摘要任务扩展到一个文档的输入。
    > 

## Attention model

### How Does Attention Work in Encoder-Decoder Recurrent Neural Networks

- [How Does Attention Work in Encoder-Decoder Recurrent Neural Networks](https://machinelearningmastery.com/how-does-attention-work-in-encoder-decoder-recurrent-neural-networks/)

    > Encoder-Decoder Model
    > ---------------------
    > 
    > The Encoder-Decoder model for recurrent neural networks was introduced in two papers.
    > 
    > Both developed the technique to address the sequence-to-sequence nature of machine translation where input sequences differ in length from output sequences.
    > 
    > Ilya Sutskever, et al. do so in the paper "[Sequence to Sequence Learning with Neural Networks](https://arxiv.org/abs/1409.3215)" using LSTMs.
    > 
    > Kyunghyun Cho, et al. do so in the paper "[Learning Phrase Representations using RNN Encoder--Decoder for Statistical Machine Translation](https://arxiv.org/abs/1406.1078)". This work, and some of the same authors (Bahdanau, Cho and Bengio) developed their specific model later to develop an attention model. Therefore we will take a quick look at the Encoder-Decoder model as described in this paper.
    > 
    > From a high-level, the model is comprised of two sub-models: an encoder and a decoder.
    > 
    > -   **Encoder**: The encoder is responsible for stepping through the input time steps and encoding the entire sequence into a fixed length vector called a context vector.
    > -   **Decoder**: The decoder is responsible for stepping through the output time steps while reading from the context vector.
    > 
    > ![Encoder-Decoder Recurrent Neural Network Model.](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2017/08/Encoder-Decoder-Recurrent-Neural-Network-Model.png)
    > 
    > Encoder-Decoder Recurrent Neural Network Model.\
    > Taken from "Learning Phrase Representations using RNN Encoder--Decoder for Statistical Machine Translation"
    > 
    > > we propose a novel neural network architecture that learns to encode a variable-length sequence into a fixed-length vector representation and to decode a given fixed-length vector representation back into a variable-length sequence.
    > 
    > --- [Learning Phrase Representations using RNN Encoder--Decoder for Statistical Machine Translation](https://arxiv.org/abs/1406.1078), 2014.
    > 
    > Key to the model is that the entire model, including encoder and decoder, is trained end-to-end, as opposed to training the elements separately.
    > 
    > The model is described generically such that different specific RNN models could be used as the encoder and decoder.
    > 
    > Instead of using the popular Long Short-Term Memory (LSTM) RNN, the authors develop and use their own simple type of RNN, later called the Gated Recurrent Unit, or GRU.
    > 
    > Further, unlike the Sutskever, et al. model, the output of the decoder from the previous time step is fed as an input to decoding the next output time step. You can see this in the image above where the output y2 uses the context vector (C), the hidden state passed from decoding y1 as well as the output y1.
    > 
    > > ... both y(t) and h(i) are also conditioned on y(t-1) and on the summary c of the input sequence.
    > 
    > --- [Learning Phrase Representations using RNN Encoder--Decoder for Statistical Machine Translation](https://arxiv.org/abs/1406.1078), 2014
    > 
    > Attention Model
    > ---------------
    > 
    > Attention was presented by Dzmitry Bahdanau, et al. in their paper "[Neural Machine Translation by Jointly Learning to Align and Translate](https://arxiv.org/abs/1409.0473)" that reads as a natural extension of their previous work on the Encoder-Decoder model.
    > 
    > Attention is proposed as a solution to the limitation of the Encoder-Decoder model encoding the input sequence to one fixed length vector from which to decode each output time step. This issue is believed to be more of a problem when decoding long sequences.
    > 
    > > A potential issue with this encoder--decoder approach is that a neural network needs to be able to compress all the necessary information of a source sentence into a fixed-length vector. This may make it difficult for the neural network to cope with long sentences, especially those that are longer than the sentences in the training corpus.
    > 
    > --- [Neural Machine Translation by Jointly Learning to Align and Translate](https://arxiv.org/abs/1409.0473), 2015.
    > 
    > Attention is proposed as a method to both align and translate.
    > 
    > Alignment is the problem in machine translation that identifies which parts of the input sequence are relevant to each word in the output, whereas translation is the process of using the relevant information to select the appropriate output.
    > 
    > > ... we introduce an extension to the encoder--decoder model which learns to align and translate jointly. Each time the proposed model generates a word in a translation, it (soft-)searches for a set of positions in a source sentence where the most relevant information is concentrated. The model then predicts a target word based on the context vectors associated with these source positions and all the previous generated target words.
    > 
    > --- [Neural Machine Translation by Jointly Learning to Align and Translate](https://arxiv.org/abs/1409.0473), 2015.
    > 
    > Instead of decoding the input sequence into a single fixed context vector, the attention model develops a context vector that is filtered specifically for each output time step.
    > 
    > ![Example of Attention](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2017/08/Example-of-Attention.png)
    > 
    > Example of Attention\
    > Taken from "Neural Machine Translation by Jointly Learning to Align and Translate", 2015.
    > 
    > As with the Encoder-Decoder paper, the technique is applied to a machine translation problem and uses GRU units rather than LSTM memory cells. In this case, a bidirectional input is used where the input sequences are provided both forward and backward, which are then concatenated before being passed on to the decoder.
    > 
    > Rather than re-iterate the equations for calculating attention, we will look at a worked example.
    > 
    > Worked Example of Attention
    > ---------------------------
    > 
    > In this section, we will make attention concrete with a small worked example. Specifically, we will step through the calculations with un-vectorized terms.
    > 
    > This will give you a sufficiently detailed understanding that you could add attention to your own encoder-decoder implementation.
    > 
    > This worked example is divided into the following 6 sections:
    > 
    > 1.  Problem
    > 2.  Encoding
    > 3.  Alignment
    > 4.  Weighting
    > 5.  Context Vector
    > 6.  Decode
    > 
    > ### 1\. Problem
    > 
    > The problem is a simple sequence-to-sequence prediction problem.
    > 
    > There are three input time steps:
    > ```
    > x1, x2, x3
    > ```
    > 
    > The model is required to predict 1 time step:
    > ```
    > y1
    > ```
    > 
    > In this example, we will ignore the type of RNN being used in the encoder and decoder and ignore the use of a bidirectional input layer. These elements are not salient to understanding the calculation of attention in the decoder.
    > 
    > ### 2\. Encoding
    > 
    > In the encoder-decoder model, the input would be encoded as a single fixed-length vector. This is the output of the encoder model for the last time step.
    > ```
    > h1 = Encoder(x1, x2, x3)
    > ```
    > 
    > The attention model requires access to the output from the encoder for each input time step. The paper refers to these as "*annotations*" for each time step. In this case:
    > ```
    > h1, h2, h3 = Encoder(x1, x2, x3)
    > ```
    > 
    > ### 3\. Alignment
    > 
    > The decoder outputs one value at a time, which is passed on to perhaps more layers before finally outputting a prediction (y) for the current output time step.
    > 
    > The alignment model scores (e) how well each encoded input (h) matches the current output of the decoder (s).
    > 
    > The calculation of the score requires the output from the decoder from the previous output time step, e.g. s(t-1). When scoring the very first output for the decoder, this will be 0.
    > 
    > Scoring is performed using a function a(). We can score each annotation (h) for the first output time step as follows:
    > 
    > ```
    > e11 = a(0, h1)
    > 
    > e12 = a(0, h2)
    > 
    > e13 = a(0, h3)
    > ```
    > 
    > We use two subscripts for these scores, e.g. e11 where the first "1" represents the output time step, and the second "1" represents the input time step.
    > 
    > We can imagine that if we had a sequence-to-sequence problem with two output time steps, that later we could score the annotations for the second time step as follows (assuming we had already calculated our s1):
    > 
    > ```
    > e21 = a(s1, h1)
    > 
    > e22 = a(s1, h2)
    > 
    > e23 = a(s1, h3)
    > ```
    > 
    > The function a() is called the alignment model in the paper and is implemented as a feedforward neural network.
    > 
    > This is a traditional one layer network where each input (s(t-1) and h1, h2, and h3) is weighted, a hyperbolic tangent (tanh) transfer function is used and the output is also weighted.
    > 
    > ### 4\. Weighting
    > 
    > Next, the alignment scores are normalized using a [softmax function](https://en.wikipedia.org/wiki/Softmax_function).
    > 
    > The normalization of the scores allows them to be treated like probabilities, indicating the likelihood of each encoded input time step (annotation) being relevant to the current output time step.
    > 
    > These normalized scores are called annotation weights.
    > 
    > For example, we can calculate the softmax annotation weights (a) given the calculated alignment scores (e) as follows:
    > 
    > ```
    > a11 = exp(e11) / (exp(e11) + exp(e12) + exp(e13))
    > 
    > a12 = exp(e12) / (exp(e11) + exp(e12) + exp(e13))
    > 
    > a13 = exp(e13) / (exp(e11) + exp(e12) + exp(e13))
    > ```
    > 
    > If we had two output time steps, the annotation weights for the second output time step would be calculated as follows:
    > 
    > ```
    > a21 = exp(e21) / (exp(e21) + exp(e22) + exp(e23))
    > 
    > a22 = exp(e22) / (exp(e21) + exp(e22) + exp(e23))
    > 
    > a23 = exp(e23) / (exp(e21) + exp(e22) + exp(e23))
    > ```
    > 
    > ### 5\. Context Vector
    > 
    > Next, each annotation (h) is multiplied by the annotation weights (a) to produce a new attended context vector from which the current output time step can be decoded.
    > 
    > We only have one output time step for simplicity, so we can calculate the single element context vector as follows (with brackets for readability):
    > 
    > ```
    > c1 = (a11 * h1) + (a12 * h2) + (a13 * h3)
    > ```
    > 
    > The context vector is a weighted sum of the annotations and normalized alignment scores.
    > 
    > If we had two output time steps, the context vector would be comprised of two elements [c1, c2], calculated as follows:
    > 
    > ```
    > c1 = a11 * h1 + a12 * h2 + a13 * h3
    > 
    > c2 = a21 * h1 + a22 * h2 + a23 * h3
    > ```
    > 
    > ### 6\. Decode
    > 
    > Decoding is then performed as per the Encoder-Decoder model, although in this case using the attended context vector for the current time step.
    > 
    > The output of the decoder (s) is referred to as a hidden state in the paper.
    > 
    > ```
    > s1 = Decoder(c1)
    > ```
    > 
    > This may be fed into additional layers before ultimately exiting the model as a prediction (y1) for the time step.
    > 
    > Extensions to Attention
    > -----------------------
    > 
    > This section looks at some additional applications of the Bahdanau, et al. attention mechanism.
    > 
    > ### Hard and Soft Attention
    > 
    > In the 2015 paper "[Show, Attend and Tell: Neural Image Caption Generation with Visual Attention](https://arxiv.org/abs/1502.03044)", Kelvin Xu, et al. applied attention to image data using convolutional neural nets as feature extractors for image data on the problem of captioning photos.
    > 
    > They develop two attention mechanisms, one they call "*soft attention*," which resembles attention as described above with a weighted context vector, and the second "*hard attention*" where the crisp decisions are made about elements in the context vector for each word.
    > 
    > They also propose double attention where attention is focused on specific parts of the image.
    > 
    > ### Dropping the Previous Hidden State
    > 
    > There have been some applications of the mechanism where the approach was simplified so that the hidden state from the last output time step (s(t-1)) is dropped from the scoring of annotations (Step 3. above).
    > 
    > Two examples are:
    > 
    > -   [Hierarchical Attention Networks for Document Classification](https://www.microsoft.com/en-us/research/publication/hierarchical-attention-networks-document-classification/), 2016.
    > -   [Attention-Based Bidirectional Long Short-Term Memory Networks for Relation Classification](http://aclweb.org/anthology/P/P16/P16-2034.pdf), 2016
    > 
    > This has the effect of not providing the model with an idea of the previously decoded output, which is intended to aid in alignment.
    > 
    > This is noted in the equations listed in the papers, and it is not clear if the mission was an intentional change to the model or merely an omission from the equations. No discussion of dropping the term was seen in either paper.
    > 
    > ### Study the Previous Hidden State
    > 
    > Minh-Thang Luong, et al. in their 2015 paper "[Effective Approaches to Attention-based Neural Machine Translation](https://arxiv.org/abs/1508.04025)" explicitly restructure the use of the previous decoder hidden state in the scoring of annotations. Also, see [the presentation](https://vimeo.com/162101582) of the paper and [associated Matlab code](https://github.com/lmthang/nmt.matlab/tree/master/code/layers).
    > 
    > They developed a framework to contrast the different ways to score annotations. Their framework calls out and explicitly excludes the previous hidden state in the scoring of annotations.
    > 
    > Instead, they take the previous attentional context vector and pass it as an input to the decoder. The intention is to allow the decoder to be aware of past alignment decisions.
    > 
    > > ... we propose an input-feeding approach in which attentional vectors ht are concatenated with inputs at the next time steps [...]. The effects of having such connections are two-fold: (a) we hope to make the model fully aware of previous alignment choices and (b) we create a very deep network spanning both horizontally and vertically
    > 
    > --- [Effective Approaches to Attention-based Neural Machine Translation](https://arxiv.org/abs/1508.04025), 2015.
    > 
    > Below is a picture of this approach taken from the paper. Note the dotted lines explictly showing the use of the decoders attended hidden state output (ht) providing input to the decoder on the next timestep.
    > 
    > ![Feeding Hidden State as Input to Decoder](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2017/08/Feeding-Hidden-State-as-Input-to-Decoder.png)
    > 
    > Feeding Hidden State as Input to Decoder\
    > Taken from "Effective Approaches to Attention-based Neural Machine Translation", 2015.
    > 
    > They also develop "*global*" vs "*local*" attention, where local attention is a modification of the approach that learns a fixed-sized window to impose over the attentional vector for each output time step. It is seen as a simpler approach to the "*hard attention*" presented by Xu, et al.
    > 
    > > The global attention has a drawback that it has to attend to all words on the source side for each target word, which is expensive and can potentially render it impractical to translate longer sequences, e.g., paragraphs or documents. To address this deficiency, we propose a local attentional mechanism that chooses to focus only on a small subset of the source positions per target word.
    > 
    > --- [Effective Approaches to Attention-based Neural Machine Translation](https://arxiv.org/abs/1508.04025), 2015.
    > 
    > Analysis in the paper of global and local attention with different annotation scoring functions suggests that local attention provides better results on the translation task.
    > 
    > Further Reading
    > ---------------
    > 
    > This section provides more resources on the topic if you are looking go deeper.
    > 
    > ### Encoder-Decoder Papers
    > 
    > -   [Learning Phrase Representations using RNN Encoder--Decoder for Statistical Machine Translation](https://arxiv.org/abs/1406.1078), 2014.
    > -   [Sequence to Sequence Learning with Neural Networks](https://arxiv.org/abs/1409.3215), 2014.
    > 
    > ### Attention Papers
    > 
    > -   [Neural Machine Translation by Jointly Learning to Align and Translate](https://arxiv.org/abs/1409.0473), 2015.
    > -   [Show, Attend and Tell: Neural Image Caption Generation with Visual Attention](https://arxiv.org/abs/1502.03044), 2015.
    > -   [Hierarchical Attention Networks for Document Classification](https://www.microsoft.com/en-us/research/publication/hierarchical-attention-networks-document-classification/), 2016.
    > -   [Attention-Based Bidirectional Long Short-Term Memory Networks for Relation Classification](http://aclweb.org/anthology/P/P16/P16-2034.pdf), 2016
    > -   [Effective Approaches to Attention-based Neural Machine Translation](https://arxiv.org/abs/1508.04025), 2015.
    > 
    > ### More on Attention
    > 
    > -   [Attention in Long Short-Term Memory Recurrent Neural Networks](http://machinelearningmastery.com/attention-long-short-term-memory-recurrent-neural-networks/)
    > -   [Lecture 10: Neural Machine Translation and Models with Attention](https://www.youtube.com/watch?v=IxQtK2SjWWM), Stanford, 2017
    > -   [Lecture 8 -- Generating Language with Attention](https://www.youtube.com/watch?v=ah7_mfl7LD0), Oxford.

### A Brief Overview of Attention Mechanism

- [A Brief Overview of Attention Mechanism – SyncedReview – Medium](https://medium.com/syncedreview/a-brief-overview-of-attention-mechanism-13c578ba9129)

    > Math is shown below:
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/0*4y96boGNMiNVHNo8.)
    > 
    > To understand the seemingly complicated math, we need to keep three key points in mind:
    > 
    > 1.  During decoding, context vectors are computed for every output word. So we will have a 2D matrix whose size is # of target words multiplied by # of source words. Equation (1) demonstrates how to compute a single value given one target word and a set of source word.
    > 2.  Once context vector is computed, attention vector could be computed by context vector, target word, and attention function `f`.
    > 3.  We need attention mechanism to be trainable. According to equation (4), both styles offer the trainable weights (W in Luong's, W1 and W2 in Bahdanau's). Thus, different styles may result in different performance.

### 深度学习笔记——Attention Model（注意力模型）学习总结

- [Deep Learning for NLP Best Practices](http://ruder.io/deep-learning-nlp-best-practices/)


- [深度学习笔记——Attention Model（注意力模型）学习总结 - mpk_no1的博客 - CSDN博客](https://blog.csdn.net/mpk_no1/article/details/72862348)

    > 深度学习里的Attention model其实模拟的是人脑的注意力模型，举个例子来说，当我们观赏一幅画时，虽然我们可以看到整幅画的全貌，但是在我们深入仔细地观察时，其实眼睛聚焦的就只有很小的一块，这个时候人的大脑主要关注在这一小块图案上，也就是说这个时候人脑对整幅图的关注并不是均衡的，是有一定的权重区分的。这就是深度学习里的Attention Model的核心思想。
    > 
    > AM刚开始也确实是应用在图像领域里的，AM在图像处理领域取得了非常好的效果！于是，就有人开始研究怎么将AM模型引入到NLP领域。最有名的当属"Neural machine translation by jointly learning to align and translate"这篇论文了，这篇论文最早提出了Soft Attention Model，并将其应用到了机器翻译领域。后续NLP领域使用AM模型的文章一般都会引用这篇文章（目前引用量已经上千了！！！）
    > 
    > 如下图所示，机器翻译主要使用的是Encoder-Decoder模型，在Encoder-Decoder模型的基础上引入了AM，取得了不错的效果：
    > 
    > ![](https://i.imgur.com/xMT2S5Q.jpg)
    > 
    > **Soft Attention Model：**
    > 
    > 这里其实是上面图的拆解，我们前面说过，"Neural machine translation by jointly learning to align and translate"这篇论文提出了soft Attention Model，并将其应用到了机器翻译上面。其实，所谓Soft，意思是在求注意力分配概率分布的时候，对于输入句子X中任意一个单词都给出个概率，是个概率分布。
    > 
    > 即上图中的ci是对Encoder中每一个单词都要计算一个注意力概率分布，然后加权得到的。如下图所示：
    > 
    > ![](https://i.imgur.com/lQ93nkI.jpg)
    > 
    > 其实有Soft AM，对应也有一个Hard AM。既然Soft是给每个单词都赋予一个单词对齐概率，那么如果不这样做，直接从输入句子里面找到某个特定的单词，然后把目标句子单词和这个单词对齐，而其它输入句子中的单词硬性地认为对齐概率为0，这就是Hard Attention Model的思想。Hard AM在图像里证明有用，但是在文本里面用处不大，因为这种单词一一对齐明显要求太高，如果对不齐对后续处理负面影响很大。
    > 
    > 但是，斯坦福大学的一篇paper"Effective Approaches to Attention-based Neural Machine Translation"提出了一个混合Soft AM 和Hard AM的模型，论文中，他们提出了两种模型：Global Attention Model和Local Attention Model，Global Attention Model其实就是Soft Attention Model，Local Attention Model本质上是Soft AM和 Hard AM的一个混合。一般首先预估一个对齐位置Pt，然后在Pt左右大小为D的窗口范围来取类似于Soft AM的概率分布。
    > 
    > **Global Attention Model和Local Attention Model**
    > 
    > ![](https://i.imgur.com/Sl63CQW.jpg)
    > 
    > Global AM其实就是soft AM，Decoder的过程中，每一个时间步的Context vector需要计算Encoder中每一个单词的注意力权重，然后加权得到。
    > 
    > ![](https://i.imgur.com/Xg3CJii.jpg)
    > 
    > Local AM则是首先找到一个对其位置，然后在对其位置左右一个窗口内来计算注意力权重，最终加权得到Context vector。这其实是Soft AM和Hard AM的一个混合折中。
    > 
    > **静态AM**
    > 
    > 其实还有一种AM叫做静态AM。所谓静态AM，其实是指对于一个文档或者句子，计算每个词的注意力概率分布，然后加权得到一个向量来代表这个文档或者句子的向量表示。跟soft AM的区别是，soft AM在Decoder的过程中每一次都需要重新对所有词计算一遍注意力概率分布，然后加权得到context vector，但是静态AM只计算一次得到句子的向量表示即可。（这其实是针对于不同的任务而做出的改变）
    > 
    > ![](https://i.imgur.com/MfEv6TI.jpg)
    > 
    > **强制前向AM**
    > 
    > Soft AM在逐步生成目标句子单词的时候，是由前向后逐步生成的，但是每个单词在求输入句子单词对齐模型时，并没有什么特殊要求。强制前向AM则增加了约束条件：要求在生成目标句子单词时，如果某个输入句子单词已经和输出单词对齐了，那么后面基本不太考虑再用它了，因为输入和输出都是逐步往前走的，所以看上去类似于强制对齐规则在往前走。
    > 
    > 看了这么多AM模型以及变种，那么我们来看一看AM模型具体怎么实现，涉及的公式都是怎样的。
    > 
    > 我们知道，注意力机制是在序列到序列模型中用于注意编码器状态的最常用方法，它同时还可用于回顾序列模型的过去状态。使用注意力机制，系统能基于隐藏状态 s_1，...，s_m 而获得环境向量（context vector）c_i，这些环境向量可以和当前的隐藏状态 h_i 一起实现预测。环境向量 c_i 可以由前面状态的加权平均数得出，其中状态所加的权就是注意力权重 a_i：
    > 
    > ![](https://i.imgur.com/gM3GyYU.jpg)
    > 
    > 注意力函数 f_att(h_i,s_j) 计算的是目前的隐藏状态 h_i 和前面的隐藏状态 s_j 之间的非归一化分配值。
    > 
    > 而实际上，注意力函数也有很多种变体。接下来我们将讨论四种注意力变体：加性注意力（additive attention）、乘法（点积）注意力（multiplicative attention）、自注意力（self-attention）和关键值注意力（key-value attention）。
    > 
    > **加性注意力（additive attention）**
    > 
    > 加性注意力是最经典的注意力机制 (Bahdanau et al., 2015) [15]，它使用了有一个隐藏层的前馈网络（全连接）来计算注意力的分配：
    > 
    > ![](https://i.imgur.com/GJWc12g.jpg)
    > 
    > 也就是：![](https://i.imgur.com/q7fZcQZ.jpg)
    > 
    > 
    > **乘法（点积）注意力（multiplicative attention）**
    > 
    > 乘法注意力（Multiplicative attention）(Luong et al., 2015) [16] 通过计算以下函数而简化了注意力操作：
    > 
    > ![](https://i.imgur.com/FZc2qim.jpg)
    > 
    > 加性注意力和乘法注意力在复杂度上是相似的，但是乘法注意力在实践中往往要更快速、具有更高效的存储，因为它可以使用**矩阵操作**更高效地实现。两个变体在低维度 d_h 解码器状态中性能相似，但加性注意力机制在更高的维度上性能更优。
    > 
    > **自注意力（self-attention）**
    > 
    > 注意力机制不仅能用来处理编码器或前面的隐藏层，它同样还能用来获得其他特征的分布，例如阅读理解任务中作为文本的词嵌入 (Kadlec et al., 2017) [37]。然而，注意力机制并不直接适用于分类任务，因为这些任务并不需要情感分析（sentiment analysis）等额外的信息。在这些模型中，通常我们使用 LSTM 的最终隐藏状态或像最大池化和平均池化那样的聚合函数来表征句子。
    > 
    > 自注意力机制（Self-attention）通常也不会使用其他额外的信息，但是它能使用自注意力关注本身进而从句子中抽取相关信息 (Lin et al., 2017) [18]。自注意力又称作内部注意力，它在很多任务上都有十分出色的表现，比如阅读理解 (Cheng et al., 2016) [38]、文本继承 (textual entailment/Parikh et al., 2016) [39]、自动文本摘要 (Paulus et al., 2017) [40]。
    > 
    > ![](https://i.imgur.com/GQvAi4l.jpg)
    > 
    > **关键值注意力（key-value attention）**
    > 
    > 关键值注意力 (Daniluk et al., 2017) [19] 是最近出现的注意力变体机制，它将形式和函数分开，从而为注意力计算保持分离的向量。它同样在多种文本建模任务 (Liu & Lapata, 2017) [41] 中发挥了很大的作用。具体来说，关键值注意力将每一个隐藏向量 h_i 分离为一个键值 k_i 和一个向量 v_i：[k_i;v_i]=h_i。键值使用加性注意力来计算注意力分布 a_i：
    > 
    > ![](https://i.imgur.com/IdY49Rt.jpg)
    > 
    > 其中 L 为注意力窗体的长度，I 为所有单元为 1 的向量。然后使用注意力分布值可以求得环境表征 c_i：
    > 
    > ![](https://i.imgur.com/4Nsa1N0.jpg)
    > 
    > 其中环境向量 c_i 将联合现阶段的状态值 v_i 进行预测。
    > 
    > 最后的最后，再加一个自己用keras实现的简单的静态AM（自注意力）层的代码吧：
    > 
    > ```python
    > from keras import backend as K
    > from keras.engine.topology import Layer
    > from keras import initializers, regularizers, constraints
    > 
    > class Attention_layer(Layer):
    >     """
    >         Attention operation, with a context/query vector, for temporal data.
    >         Supports Masking.
    >         Follows the work of Yang et al. [https://www.cs.cmu.edu/~diyiy/docs/naacl16.pdf]
    >         "Hierarchical Attention Networks for Document Classification"
    >         by using a context vector to assist the attention
    >         # Input shape
    >             3D tensor with shape: `(samples, steps, features)`.
    >         # Output shape
    >             2D tensor with shape: `(samples, features)`.
    >         :param kwargs:
    >         Just put it on top of an RNN Layer (GRU/LSTM/SimpleRNN) with return_sequences=True.
    >         The dimensions are inferred based on the output shape of the RNN.
    >         Example:
    >             model.add(LSTM(64, return_sequences=True))
    >             model.add(AttentionWithContext())
    >         """
    > 
    >     def __init__(self,
    >                  W_regularizer=None, b_regularizer=None,
    >                  W_constraint=None, b_constraint=None,
    >                  bias=True, **kwargs):
    > 
    >         self.supports_masking = True
    >         self.init = initializers.get('glorot_uniform')
    > 
    >         self.W_regularizer = regularizers.get(W_regularizer)
    >         self.b_regularizer = regularizers.get(b_regularizer)
    > 
    >         self.W_constraint = constraints.get(W_constraint)
    >         self.b_constraint = constraints.get(b_constraint)
    > 
    >         self.bias = bias
    >         super(Attention_layer, self).__init__(**kwargs)
    > 
    >     def build(self, input_shape):
    >         assert len(input_shape) == 3
    > 
    >         self.W = self.add_weight((input_shape[-1], input_shape[-1],),
    >                                  initializer=self.init,
    >                                  name='{}_W'.format(self.name),
    >                                  regularizer=self.W_regularizer,
    >                                  constraint=self.W_constraint)
    >         if self.bias:
    >             self.b = self.add_weight((input_shape[-1],),
    >                                      initializer='zero',
    >                                      name='{}_b'.format(self.name),
    >                                      regularizer=self.b_regularizer,
    >                                      constraint=self.b_constraint)
    > 
    >         super(Attention_layer, self).build(input_shape)
    > 
    >     def compute_mask(self, input, input_mask=None):
    >         # do not pass the mask to the next layers
    >         return None
    > 
    >     def call(self, x, mask=None):
    >         uit = K.dot(x, self.W)
    > 
    >         if self.bias:
    >             uit += self.b
    > 
    >         uit = K.tanh(uit)
    > 
    >         a = K.exp(uit)
    > 
    >         # apply mask after the exp. will be re-normalized next
    >         if mask is not None:
    >             # Cast the mask to floatX to avoid float64 upcasting in theano
    >             a *= K.cast(mask, K.floatx())
    > 
    >         # in some cases especially in the early stages of training the sum may be almost zero
    >         # and this results in NaN's. A workaround is to add a very small positive number to the sum.
    >         # a /= K.cast(K.sum(a, axis=1, keepdims=True), K.floatx())
    >         a /= K.cast(K.sum(a, axis=1, keepdims=True) + K.epsilon(), K.floatx())
    >         print a
    >         # a = K.expand_dims(a)
    >         print x
    >         weighted_input = x * a
    >         print weighted_input
    >         return K.sum(weighted_input, axis=1)
    > 
    >     def compute_output_shape(self, input_shape):
    >         return (input_shape[0], input_shape[-1])
    > ```
    > 


### Attention Model 注意力机制


- [Attention Mechanism |](https://blog.heuritech.com/2016/01/20/attention-mechanism/)


- [Attention Model 注意力机制 | 记录思考](https://ilewseu.github.io/2018/02/12/Attention%20Model%20%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%9C%BA%E5%88%B6/)

    > ## Attention for Image Captioning
    > 
    > 我们通过介绍一个例子，去解释注意力机制。这个任务是我们想实现给图片加标题：对于给定的图片，根据图片中的内容给图片配上标题(说明/描述)。一个典型的image captioning系统会对图片进行编码，使用预训练的卷积神经网络产生一个隐状态h。然后，可以使用RNN对这个隐状态h进行解码，生成标题。这种方法已经被不少团队采用，包括\[11\]，如下图所示：
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/27GEF0IlE8.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/27GEF0IlE8.png?imageslim)
    > 
    > 这种方法的问题是：当模型尝试去产生标题的下一个词时，这个词通常是描述图片的一部分。使用整张图片的表示h去调节每个词的生成，不能有效地为图像的不同部分产生不同的单词。这正是注意力机制有用的地方。  
    > 使用注意力机制，图片首先被划分成n个部分，然后我们使用CNN计算图像每个部分的表示 $h_1,…,h_n$，也就是对n个部分的图像进行编码。当使用RNN产生一个新的词时，注意力机制使得系统只注意图片中相关的几个部分，所以解码仅仅使用了图片的特定的几个部分。如下图所示，我们可以看到标题的每个词都是用图像(白色部分)的一部分产生的。
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/cIDeG9Jgl9.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/cIDeG9Jgl9.png?imageslim)
    > 
    > 更多的例子如下图所示，我们可看到图片相关的部分产生标题中划线的单词。
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/IiaGamlfj5.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/IiaGamlfj5.png?imageslim)
    > 
    > 现在我们要解释注意力机制是怎么工作的，文献\[3\]详细介绍了基于注意力机制的Encoder-Decoder Network的实现。
    > 
    > ## [](https://ilewseu.github.io/2018/02/12/Attention%20Model%20%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%9C%BA%E5%88%B6/#What-is-an-attention-model "What is an attention model")What is an attention model
    > 
    > 在一般情况下，什么是注意力机制？
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/K49GLi96C2.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/K49GLi96C2.png?imageslim)
    > 
    > 一个attention model通常包含n个参数
    > 
    > $y_1,..,y_n$(在前面的例子中，$y_i$可以是$h_i$) ,和一个上下文c。它返回一个z向量，这个向量可以看成是对$y_i$的总结，关注与上下文c相关联的信息。更正式地说是，它返回的$y_i$的加权算术平均值，并且权重是根据 $y_i$与给定上下文c的相关性来选择的。
    > 
    > 在上面的例子中，上下文是刚开始产生的句子， $y_i$是图像的每个部分的表示($h_i$)，输出是对图像进行一定的过滤（例如：忽略图像中的某些部分）后的表示，通过过滤将当前生成的单词的重点放在感兴趣的部分。  
    > 
    > 注意力机制有一个有趣的特征：计算出的权重是可访问的并且可以被绘制出来。这正是我们之前展示的图片，如果权重越高，则对应部分的像素越白。
    > 
    > 但是，这个黑盒子做了什么？下图能够清晰的表示Attention Model的原理：
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/mmcbj2eK5C.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/mmcbj2eK5C.png?imageslim)
    > 
    > 可能这个网络图看起来比较复杂，我们一步一步来解释这个图。  
    > 
    > 首先，我们能够看出 一个输入c，是上下文， $y_i$是我们正在研究的“数据的一部分”。
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/591aa4eId3.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/591aa4eId3.png?imageslim)
    > 
    > 然后，网络计算 $m_1,…,m_n$通过一个tanh层。这意味着我们计算$y_i$和c的一个”聚合”。重要的一点是，每个$m_i$的计算都是在不考虑其他 $y_j,j \neq i$的情况下计算出来的。它们是独立计算出来的。
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/fejdk9cA73.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/fejdk9cA73.png?imageslim)
    > 
    > $$m_i = tanh(W_{cm}c+W_{ym}y_i)$$
    > 
    > 然后，我们计算每个weight使用softmax。softmax，就像他的名字一样，它的行为和argmax比较像，但是稍有不同。 $argmax(x_1,…,x_n)=(0,..,0,1,0,..,0)$,在输出中只有一个1，告诉我们那个是最大值。但是，softmax的定义为：$softmax(x_1,…,x_n)=(\frac {e^{x_i}}{\sum_j e^{x_j}})_i$。如果其中有一个$x_i$比其他的都大，$softmax(x_1,…,x_n)将会非常接近argmax(x_1,…,x_n)$。  
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/g3JgH62d65.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/g3JgH62d65.png?imageslim)
    > 
    > $$s_i 正比于 exp(w_m, m_i)\\\ \sum_i s_i=1$$  
    > 
    > 这里的$s_i$是通过softmax进行归一化后的值。因此，softmax可以被认为是“相关性”最大值的变量，根据上下文。  
    > 
    > 输出$z$是所有$y_i$的算术平均，每个权重值表示 $y_i,..,y_n$和上下文c的相关性。
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/43eLlm4gDb.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/43eLlm4gDb.png?imageslim)
    > 
    > $$z = \sum_i s_iy_i$$
    > 
    > ## [](https://ilewseu.github.io/2018/02/12/Attention%20Model%20%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%9C%BA%E5%88%B6/#An-other-computation-of-“relevance” "An other computation of “relevance”")An other computation of “relevance”
    > 
    > 上面介绍的attention model是可以进行修改的。首先，tanh层可以被其他网络或函数代替。重要的是这个网络或函数可以综合c和 $y_i$。比如可以只使用点乘操作计算c和 $y_i$的内积，如下图所示：
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/8b2LBfc266.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/8b2LBfc266.png?imageslim)
    > 
    > 这个版本的比较容易理解。上面介绍的Attention是softly-choosing与上下文最相关的变量（$y_i$）。据我们所知，这两种系统似乎都能产生类似的结果。  
    > 
    > 另外一个比较重要的改进是hard attention。
    > 
    > ## [](https://ilewseu.github.io/2018/02/12/Attention%20Model%20%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%9C%BA%E5%88%B6/#Soft-Attention-and-Hard-Attention "Soft Attention and Hard Attention")Soft Attention and Hard Attention
    > 
    > 上面我们描述的机制称为Soft Attention，因为它是一个完全可微的确定性机制，可以插入到现有的系统中，梯度通过注意力机制进行传播，同时它们通过网络的其余部分进行传播。  
    > 
    > Hard Attention是一个随机过程：系统不使用所有隐藏状态作为解码的输入，而是以概率 $s_i$对隐藏状态 $y_i$进行采样。为了进行梯度传播，使用蒙特卡洛方法进行抽样估计梯度。
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/5c1A061BL6.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/5c1A061BL6.png?imageslim)
    > 
    > 这两个系统都有自己的优缺点，但是研究的趋势是集中于Soft Attention，因为梯度可以直接计算，并不是通过随机过程来估计的。
    > 
    > ## [](https://ilewseu.github.io/2018/02/12/Attention%20Model%20%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%9C%BA%E5%88%B6/#Return-to-the-image-captioning "Return to the image captioning")Return to the image captioning
    > 
    > 现在，我们来理解一下image captioning 系统是怎样工作的。
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/E6AGi93bJ9.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/E6AGi93bJ9.png?imageslim)
    > 
    > 从上面的图我们可以看到image captioning的典型模型，但是添加了一个新的关于attention model的层。当我们想要预测标题的下一个单词时，发生了什么？如果我们要预测第i个词，LSTM的隐藏状态是 $h_i$。我们选择图像相关的部分通过把$h_i$作为上下文。然后，attention model的输出是$z_i$，这是被过滤的图像的表示，只有图像的相关部分被保留，用作LSTM的输入。然后，LSTM预测一个下一个词，并返回一个隐藏状态 $h_{i+1}$。
    > 
    > ## [](https://ilewseu.github.io/2018/02/12/Attention%20Model%20%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%9C%BA%E5%88%B6/#Learning-to-Align-in-Machine-Translation "Learning to Align in Machine Translation")Learning to Align in Machine Translation
    > 
    > Bahdanau, et al\[5\]中的工作提出了一个神经翻译模型将句子从一种语言翻译成另一种语言，并引入注意力机制。在解释注意力机制之前，vanillan神经网络翻译模型使用了编码-解码(Encoder-Decoder)框架。编码器使用循环神经网络(RNN,通常GRU或LSTM)将用英语表示的句子进行编码，并产生隐藏状态h。这个隐藏状态h用于解码器RNN产生正确的法语的句子。
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/JL6JJK2g25.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/JL6JJK2g25.png?imageslim)
    > 
    > 编码器不产生与整个句子对应的单个隐藏状态，而是产生与一个词对应的隐藏状态 $h_j$。每当解码器RNN产生一个单词时，取决于每个隐藏状态作为输入的贡献，通常是一个单独的参数（参见下图）。这个贡献参数使用Softmax进行计算：这意味着attention weights $a_j$在$\sum a_j=1$的约束下进行计算并且所有的隐藏状态$h_j$给解码器贡献的权重为 $a_j$。  
    > 
    > 在我们的例子中，注意力机制是完全可微的，不需要额外的监督，它只是添加在现有的编码-解码框架的顶部。  
    > 
    > 这个过程可以看做是对齐，因为网络通常在每次生成输出词时都会学习集中于单个输入词。这就意味着大多数的注意力权重是0(黑)，而一个单一的被激活(白色)。下面的图像显示了翻译过程中的注意权重，它揭示了对齐方式，并使解释网络所学的内容成为可能（这通常是RNNs的问题！）。
    > 
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/fbb3Gee98c.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/fbb3Gee98c.png?imageslim)
    > 
    > ## [](https://ilewseu.github.io/2018/02/12/Attention%20Model%20%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%9C%BA%E5%88%B6/#Attention-without-Recurrent-Neural-Networks "Attention without Recurrent Neural Networks")Attention without Recurrent Neural Networks
    > 
    > 到现在为止，我们仅介绍了注意力机制在编码-解码框架下的工作。但是，当输入的顺序无关紧要时，可以考虑独立的隐藏状态
    > 
    > $h_j$。这个在Raffel et Al\[10\]中进行了介绍，这里attention model是一个前向全连接的网络。同样的应用是Mermory Networks\[6\]（参见下一节）。
    > 
    > ## [](https://ilewseu.github.io/2018/02/12/Attention%20Model%20%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%9C%BA%E5%88%B6/#From-Attention-to-Memory-Addressing "From Attention to Memory Addressing")From Attention to Memory Addressing
    > 
    > NIPS 2015会议上提出了一个非常有趣的工作叫做 RAM for Reasoning、Attention and Memory。它的工作包含Attention，但是也包括Memory Networks\[6\],Neural Turing Machines\[7\]或 Differentiable Stack RNNS\[8\]以及其他的工作。这些模型都有共同之处，它们使用一种外部存储器的形式，这种存储器可以被读取（最终写入）。  
    > 
    > 比较和解释这些模型是超出了这个本文的范围, 但注意机制和记忆之间的联系是有趣的。例如，在Memory Networks中，我们认为外部存储器-一组事实或句子
    > 
    > $x_i$和一个输入q。网络学习对记忆的寻址，这意味着选择哪个事实$x_i$去关注来产生答案。这对应了一个attention model在外部存储器上。In Memory Networks, the only difference is that the soft selection of the facts (blue Embedding A in the image below) is decorrelated from the weighted sum of the embeddings of the facts (pink embedding C in the image).（PS：实在读不懂了）。在Neural Turing Machine中，使用了一个Soft Attention机制。这些模型将会是下个博文讨论的对象。  
    > [![mark](http://of6h3n8h0.bkt.clouddn.com/blog/180212/cHmIh83088.png?imageslim)](http://of6h3n8h0.bkt.clouddn.com/blog/180212/cHmIh83088.png?imageslim)

### [1705.03122] Convolutional Sequence to Sequence Learning

- [[1705.03122] Convolutional Sequence to Sequence Learning](https://arxiv.org/abs/1705.03122)

- [facebookresearch/fairseq: Facebook AI Research Sequence-to-Sequence Toolkit](https://github.com/facebookresearch/fairseq)

    > ![Model](https://github.com/facebookresearch/fairseq/raw/master/fairseq.gif)

- [tobyyouup/conv_seq2seq: A tensorflow implementation of Fairseq Convolutional Sequence to Sequence Learning(Gehring et al. 2017)](https://github.com/tobyyouup/conv_seq2seq)

- [sdanaipat/fairseq-translator: A quick Tensorflow implementation of Facebook FairSeq[1] for character-level neural machine translation (EN -> JP).](https://github.com/sdanaipat/fairseq-translator)

- [从《Convolutional Sequence to Sequence Learning》到《Attention Is All You Need》](https://zhuanlan.zhihu.com/p/27464080)

    > **ConvS2S**
    > -----------
    > 
    > **Model Architecture**
    > 
    > ![](https://pic3.zhimg.com/80/v2-6ceb749ee1edfa407e6132ddd2710384_hd.jpg)
    > 
    > 图1 ConvS2S模型
    > 
    > **Symbols**
    > 
    > 1）模型的输入序列![\boldsymbol{e}=\{e_{1},...,e_{m}\}](https://www.zhihu.com/equation?tex=%5Cboldsymbol%7Be%7D%3D%5C%7Be_%7B1%7D%2C...%2Ce_%7Bm%7D%5C%7D)：![e_{i}=w_{i}+p_{i}](https://www.zhihu.com/equation?tex=e_%7Bi%7D%3Dw_%7Bi%7D%2Bp_%7Bi%7D)，![w_{i}](https://www.zhihu.com/equation?tex=w_%7Bi%7D)表示词![x_{i}](https://www.zhihu.com/equation?tex=x_%7Bi%7D)的word embedding，![p_{i}](https://www.zhihu.com/equation?tex=p_%7Bi%7D)表示![x_{i}](https://www.zhihu.com/equation?tex=x_%7Bi%7D)的position embedding。
    > 
    > 2）Decoder在每一个时刻的输入序列![\boldsymbol{g}=\{g_{1},...,g_{m}\}](https://www.zhihu.com/equation?tex=%5Cboldsymbol%7Bg%7D%3D%5C%7Bg_%7B1%7D%2C...%2Cg_%7Bm%7D%5C%7D)：同样由两部分组成：上一时刻Decoder输出词的word embedding以及对应的position embedding。
    > 
    > 3）Decoder Network中第![l](https://www.zhihu.com/equation?tex=l)个block（block的定义与layer类似）的输出![\boldsymbol{h}^{l}=(h_{1}^{l},...,h_{n}^{l})](https://www.zhihu.com/equation?tex=%5Cboldsymbol%7Bh%7D%5E%7Bl%7D%3D%28h_%7B1%7D%5E%7Bl%7D%2C...%2Ch_%7Bn%7D%5E%7Bl%7D%29)。
    > 
    > 4）Encoder Network中第![l](https://www.zhihu.com/equation?tex=l)个block的输出![\boldsymbol{z}^{l}=(z_{1}^{l},...,z_{m}^{l})](https://www.zhihu.com/equation?tex=%5Cboldsymbol%7Bz%7D%5E%7Bl%7D%3D%28z_%7B1%7D%5E%7Bl%7D%2C...%2Cz_%7Bm%7D%5E%7Bl%7D%29)。
    > 
    > **Convolutional Architecture**
    > 
    > 每个block包括一维卷积运算与一个非线性运算。当对 ![a](https://www.zhihu.com/equation?tex=a) 层 block 进行堆叠时，若卷积窗口大小为k，则每个输出要依赖于![1+a(k-1)](https://www.zhihu.com/equation?tex=1%2Ba%28k-1%29)个输入。
    > 
    > 每个卷积核的大小为![W\in\mathbb{R}^{2d\times kd}](https://www.zhihu.com/equation?tex=W%5Cin%5Cmathbb%7BR%7D%5E%7B2d%5Ctimes+kd%7D)，偏置向量为![b_{w}\in\mathbb{R}^{2d}](https://www.zhihu.com/equation?tex=b_%7Bw%7D%5Cin%5Cmathbb%7BR%7D%5E%7B2d%7D)。输入为![X\in\mathbb{R}^{k\times d}](https://www.zhihu.com/equation?tex=X%5Cin%5Cmathbb%7BR%7D%5E%7Bk%5Ctimes+d%7D)，其中，![kd](https://www.zhihu.com/equation?tex=kd)中的![k](https://www.zhihu.com/equation?tex=k)表示卷积窗的宽度，![d](https://www.zhihu.com/equation?tex=d)表示每个元素embedding所得到的向量的大小，![2d](https://www.zhihu.com/equation?tex=2d)表示feature map的个数。卷积核可以将每个卷积窗内的输入映射为一个大小为![Y=[A,B]\in\mathbb{R}^{2d}](https://www.zhihu.com/equation?tex=Y%3D%5BA%2CB%5D%5Cin%5Cmathbb%7BR%7D%5E%7B2d%7D)的向量（A，B的维度均为d）。在Y上，该模型又使用了一个GLU（Gated Linear Units）进行了处理，得到了对输入句的最终表示：
    > 
    > ![](https://pic2.zhimg.com/80/v2-e8c5892c1037cd085d5c6a1a2dc5c05f_hd.jpg)
    > 
    > 其中，![v(A,B)\in\mathbb{R}^{d}](https://www.zhihu.com/equation?tex=v%28A%2CB%29%5Cin%5Cmathbb%7BR%7D%5E%7Bd%7D)。
    > 
    > 为了增加网络深度，使encoder的每个隐层输出都能包含输入序列中的更多信息，在这里，使用了残差连接[3]:
    > 
    > ![](https://pic3.zhimg.com/80/v2-72fa5b64059ba588f4ffa4732f951340_hd.jpg)
    > 
    > 其中，![W^{l}](https://www.zhihu.com/equation?tex=W%5E%7Bl%7D)表示第![l](https://www.zhihu.com/equation?tex=l)层的卷积核。单层残差连接实际的结构如下图所示（原图中仅画了一层），为了区分![l](https://www.zhihu.com/equation?tex=l)与1，在图中使用大写L代替了小写![l](https://www.zhihu.com/equation?tex=l)。实际上在这里可以进行堆叠（在本文中，encoder堆叠了![u](https://www.zhihu.com/equation?tex=u)层，decoder堆叠了![L](https://www.zhihu.com/equation?tex=L)层），灰色方块表示PADDING。
    > 
    > ![](https://pic1.zhimg.com/80/v2-02a34d1001c56da69669e435ec3a9cae_hd.jpg)
    > 
    > 图2 ： 单层block的情况
    > 
    > ![](https://pic1.zhimg.com/80/v2-8cd444bdac2ff1ead58d548288aceae1_hd.jpg)
    > 
    > 图3： 多层block。可以看到，经过堆叠之后，第三层的每个输出都与输入中的7列有关\
    > **Multi-step Attention**
    > 
    > 在解码器的每一层，都单独使用了attention机制：解码器第![l](https://www.zhihu.com/equation?tex=l)层的attention计算公式为：
    > 
    > ![](https://pic3.zhimg.com/80/v2-18a21ee65de638b1c487a6462c2615ef_hd.jpg)
    > 
    > ![](https://pic2.zhimg.com/80/v2-2c6e3507593858525b63ace201a54591_hd.jpg)
    > 
    > ![](https://pic3.zhimg.com/80/v2-7178b3b3d911c0a0f722da6bd0f7c272_hd.jpg)
    > 
    > 其中，![W_{d}^{l}](https://www.zhihu.com/equation?tex=W_%7Bd%7D%5E%7Bl%7D)与![b_{d}^{l}](https://www.zhihu.com/equation?tex=b_%7Bd%7D%5E%7Bl%7D)为解码器第![l](https://www.zhihu.com/equation?tex=l)层attention的参数矩阵，![g_{i}](https://www.zhihu.com/equation?tex=g_%7Bi%7D)表示上一个时刻解码器输出词对应的embedding（含word embedding与position embedding）；![z_{j}^{u}](https://www.zhihu.com/equation?tex=z_%7Bj%7D%5E%7Bu%7D)表示encoder第![u](https://www.zhihu.com/equation?tex=u)层（也就是最后一层）的第![j](https://www.zhihu.com/equation?tex=j)个**隐层状态**；最后可以得到![z^{u}](https://www.zhihu.com/equation?tex=z%5E%7Bu%7D)相对于decoder第![l](https://www.zhihu.com/equation?tex=l)层的context vector ![c^{l}](https://www.zhihu.com/equation?tex=c%5E%7Bl%7D)（在计算每个![c^{l}](https://www.zhihu.com/equation?tex=c%5E%7Bl%7D)时，还要使用encoder输入的embedding矩阵 ![e](https://www.zhihu.com/equation?tex=e)（模型结构图中右上角的圆角箭头））。
    > 
    > 得到![c^{l}](https://www.zhihu.com/equation?tex=c%5E%7Bl%7D)之后，将其加到decoder当前层的隐层状态![h^{l}](https://www.zhihu.com/equation?tex=h%5E%7Bl%7D)中，然后再输入到decoder的第![l+1](https://www.zhihu.com/equation?tex=l%2B1)层中。最后，在decoder的第L层（最后一层），可以得到最终的隐层状态![h^{L}](https://www.zhihu.com/equation?tex=h%5E%7BL%7D)。
    > 
    > **Generation**
    > 
    > 得到了最终的隐层状态之后，就可以使用softmax层来计算decoder在![i](https://www.zhihu.com/equation?tex=i)时刻的输出结果了：
    > 
    > ![](https://pic2.zhimg.com/80/v2-a237ec8b1aa76332d4ea6210b80c7f22_hd.jpg)
    > 


- [<模型汇总-7>基于CNN的Seq2Seq模型-Convolutional Sequence ... - 简书](https://www.jianshu.com/p/0f2396f0d98f)

    > 2、Convolutional Seq2Seq中采用各种trick
    > 
    > FaceBook发布的这篇文章的工作持续时间比较长了，依赖于《Language Modeling with Gated Convolutional Networks》文章中的工作。个人认为，FaceBook的Convolutional SeqSeq取得了超越Google翻译的成果，重要原因在于采用了很多的trick，很多工作值得借鉴：
    > 
    > 1. Position Embedding，在输入信息中加入位置向量P=（p1,p2,....），把位置向量与词向量W=（w1，w2,.....）求和构成向量E=(w1+p1,w2+p2)，做为网络输入，使由CNN构成的Encoder和Decoder也具备了RNN捕捉输入Sequence中词的位置信息的功能。
    > 
    > 2. 层叠CNN构成了hierarchical representation表示。层叠的CNN拥有3个优点：
    > 
    >     （1）捕获long-distance依赖关系。底层的CNN捕捉相聚较近的词之间的依赖关系，高层CNN捕捉较远词之间的依赖关系。通过层次化的结构，实现了类似RNN（LSTM）捕捉长度在20个词以上的Sequence的依赖关系的功能。
    > 
    >     （2）效率高。假设一个sequence序列长度为n，采用RNN（LSTM）对其进行建模 需要进行n次操作，时间复杂度O（n）。相比，采用层叠CNN只需要进行n/k次操作，时间复杂度O（n/k）,k为卷积窗口大小。
    > 
    >     （3）可以并行化实现。RNN对sequence的建模依赖于序列的历史信息，因此不能并行实现。相比，层叠CNN正个sequence进行卷积，不依赖序列历史信息，可以并行实现，模型训练更快，特别是在工业生产，面临处理[大数据](https://link.jianshu.com?t=http://lib.csdn.net/base/hadoop)量和实时要求比较高的情况下。
    > 
    > 3. 融合了Residual connection、liner mapping的多层attention。通过attention决定输入的哪些信息是重要的，并逐步往下传递。把encoder的输出和decoder的输出做点乘（dot products），再归一化，再乘以encoder的输入X之后做为权重化后的结果加入到decoder中预测目标语言序列。
    > 
    > 4. 采用GLU做为gate mechanism。GLU单元激活方式如下公式所示：
    > 
    >     ![](//upload-images.jianshu.io/upload_images/5739377-b37e9aa4dfa4ac62?imageMogr2/auto-orient/strip%7CimageView2/2/w/330)
    > 
    >     每一层的输出都是一个线性映射X*W + b，被一个门gate：o（X*V+c）控制，通过做乘法来控制信息向下层流动的力度，o采用双曲正切S型激活函数。这个机制类似LSTM中的gate mechanism，对于语言建模非常有效，使模型可以选择那些词或特征对于预测下一个词是真的有效的。
    > 
    > 5. 进行了梯度裁剪和精细的权重初始化，加速模型训练和收敛。
    > 


### [1706.03762] Attention Is All You Need

- [[1706.03762] Attention Is All You Need](https://arxiv.org/abs/1706.03762)

- [(4 封私信 / 23 条消息)如何理解谷歌团队的机器翻译新作《Attention is all you need》？ - 知乎](https://www.zhihu.com/question/61077555)

- [tensorflow/nmt: TensorFlow Neural Machine Translation Tutorial](https://github.com/tensorflow/nmt)

- [Attention Is All You Need：基於注意力機制的機器翻譯模型 – Youngmi huang – Medium](https://medium.com/@cyeninesky3/attention-is-all-you-need-%E5%9F%BA%E6%96%BC%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%A9%9F%E5%88%B6%E7%9A%84%E6%A9%9F%E5%99%A8%E7%BF%BB%E8%AD%AF%E6%A8%A1%E5%9E%8B-dcc12d251449)

- [Kyubyong/transformer: A TensorFlow Implementation of the Transformer: Attention Is All You Need](https://github.com/Kyubyong/transformer)

- [《Attention is All You Need》浅读（简介+代码） - 科学空间|Scientific Spaces](https://kexue.fm/archives/4765)

    > 2017年中，有两篇类似同时也是笔者非常欣赏的论文，分别是FaceBook的《Convolutional Sequence to Sequence Learning》和Google的《Attention is All You Need》，它们都算是Seq2Seq上的创新，本质上来说，都是抛弃了RNN结构来做Seq2Seq任务。
    > 
    > 这篇博文中，笔者对[《Attention is All You Need》](https://arxiv.org/pdf/1706.03762.pdf)做一点简单的分析。当然，这两篇论文本身就比较火，因此网上已经有很多解读了（不过很多解读都是直接翻译论文的，鲜有自己的理解），因此这里尽可能多自己的文字，尽量不重复网上各位大佬已经说过的内容。
    > 
    > ## 序列编码 
    > 
    > 深度学习做NLP的方法，基本上都是先将句子分词，然后每个词转化为对应的词向量序列。这样一来，每个句子都对应的是一个矩阵
    > 
    > $\boldsymbol{X}=(\boldsymbol{x}_1,\boldsymbol{x}_2,\dots,\boldsymbol{x}_t)$，其中$\boldsymbol{x}_i$都代表着第$i$个词的词向量（行向量），维度为$d$维，故 $\boldsymbol{X}\in \mathbb{R}^{n\times d}$。这样的话，问题就变成了编码这些序列了。
    > 
    > 第一个基本的思路是RNN层，RNN的方案很简单，递归式进行：  
    > 
    > $$\boldsymbol{y}_t = f(\boldsymbol{y}_{t-1},\boldsymbol{x}_t)$$  
    > 不管是已经被广泛使用的LSTM、GRU还是最近的SRU，都并未脱离这个递归框架。RNN结构本身比较简单，也很适合序列建模，但RNN的明显缺点之一就是无法并行，因此速度较慢，这是递归的天然缺陷。另外我个人觉得RNN无法很好地学习到全局的结构信息，因为它本质是一个马尔科夫决策过程。
    > 
    > 第二个思路是CNN层，其实CNN的方案也是很自然的，窗口式遍历，比如尺寸为3的卷积，就是  
    > 
    > $$\boldsymbol{y}_t = f(\boldsymbol{x}_{t-1},\boldsymbol{x}_t,\boldsymbol{x}_{t+1})$$  
    > 在FaceBook的论文中，纯粹使用卷积也完成了Seq2Seq的学习，是卷积的一个精致且极致的使用案例，热衷卷积的读者必须得好好读读这篇文论。CNN方便并行，而且容易捕捉到一些全局的结构信息，笔者本身是比较偏爱CNN的，在目前的工作或竞赛模型中，我都已经尽量用CNN来代替已有的RNN模型了，并形成了自己的一套使用经验，这部分我们以后再谈。
    > 
    > Google的大作提供了第三个思路：**纯Attention！单靠注意力就可以！** RNN要逐步递归才能获得全局信息，因此一般要双向RNN才比较好；CNN事实上只能获取局部信息，是通过层叠来增大感受野；Attention的思路最为粗暴，它一步到位获取了全局信息！它的解决方案是：  
    > 
    > $$\boldsymbol{y}_t = f(\boldsymbol{x}_{t},\boldsymbol{A},\boldsymbol{B})$$  
    > 其中$\boldsymbol{A},\boldsymbol{B}$是另外一个序列（矩阵）。如果都取$\boldsymbol{A}=\boldsymbol{B}=\boldsymbol{X}$，那么就称为Self Attention，它的意思是直接将$\boldsymbol{x}_t$与原来的每个词进行比较，最后算出$\boldsymbol{y}_t$！
    > 
    > ## Attention层 
    > 
    > ### Attention定义 
    > 
    > [![Attention](https://kexue.fm/usr/uploads/2018/01/458889390.png)](https://kexue.fm/usr/uploads/2018/01/458889390.png "点击查看原图")
    > 
    > Attention
    > 
    > Google的一般化Attention思路也是一个编码序列的方案，因此我们也可以认为它跟RNN、CNN一样，都是一个序列编码的层。
    > 
    > 前面给出的是一般化的框架形式的描述，事实上Google给出的方案是很具体的。首先，它先把Attention的定义给了出来：  
    > 
    > $$Attention(\boldsymbol{Q},\boldsymbol{K},\boldsymbol{V}) = softmax\left(\frac{\boldsymbol{Q}\boldsymbol{K}^{\top}}{\sqrt{d_k}}\right)\boldsymbol{V}$$  
    > 这里用的是跟Google的论文一致的符号，其中$\boldsymbol{Q}\in\mathbb{R}^{n\times d_k}, \boldsymbol{K}\in\mathbb{R}^{m\times d_k}, \boldsymbol{V}\in\mathbb{R}^{m\times d_v}$。如果忽略激活函数$softmax$的话，那么事实上它就是三个$n\times d_k,d_k\times m, m\times d_v$的矩阵相乘，最后的结果就是一个$n\times d_v$的矩阵。于是我们可以认为：这是一个Attention层，将$n\times d_k$的序列$\boldsymbol{Q}$编码成了一个新的 $n\times d_v$的序列。
    > 
    > 那怎么理解这种结构呢？我们不妨逐个向量来看。  
    > 
    > $$Attention(\boldsymbol{q}_t,\boldsymbol{K},\boldsymbol{V}) = \sum_{s=1}^m \frac{1}{Z}\exp\left(\frac{\langle\boldsymbol{q}_t, \boldsymbol{k}_s\rangle}{\sqrt{d_k}}\right)\boldsymbol{v}_s$$  
    > 其中$Z$是归一化因子。事实上$q,k,v$分别是$query,key,value$的简写，$\boldsymbol{K},\boldsymbol{V}$是一一对应的，它们就像是key-value的关系，那么上式的意思就是通过$\boldsymbol{q}_t$这个query，通过与各个$\boldsymbol{k}_s$内积的并softmax的方式，来得到$\boldsymbol{q}_t$与各个$\boldsymbol{v}_s$的相似度，然后加权求和，得到一个$d_v$维的向量。其中因子 $\sqrt{d_k}$起到调节作用，使得内积不至于太大（太大的话softmax后就非0即1了，不够“soft”了）。
    > 
    > 事实上这种Attention的定义并不新鲜，但由于Google的影响力，我们可以认为现在是更加正式地提出了这个定义，并将其视为一个层地看待；此外这个定义只是注意力的一种形式，还有一些其他选择，比如 $query$跟$key$的运算方式不一定是点乘（还可以是拼接后再内积一个参数向量），甚至权重都不一定要归一化，等等。
    > 
    > ### Multi-Head Attention
    > 
    > [![Multi-Head Attention](https://kexue.fm/usr/uploads/2018/01/2809060486.png)](https://kexue.fm/usr/uploads/2018/01/2809060486.png "点击查看原图")
    > 
    > Multi-Head Attention
    > 
    > 这个是Google提出的新概念，是Attention机制的完善。不过从形式上看，它其实就再简单不过了，就是把 $\boldsymbol{Q},\boldsymbol{K},\boldsymbol{V}$通过参数矩阵映射一下，然后再做Attention，把这个过程重复做$h$次，结果拼接起来就行了，可谓“大道至简”了。具体来说  
    > $$head_i = Attention(\boldsymbol{Q}\boldsymbol{W}_i^Q,\boldsymbol{K}\boldsymbol{W}_i^K,\boldsymbol{V}\boldsymbol{W}_i^V)$$  
    > 这里$\boldsymbol{W}_i^Q\in\mathbb{R}^{d_k\times \tilde{d}_k}, \boldsymbol{W}_i^K\in\mathbb{R}^{d_k\times \tilde{d}_k}, \boldsymbol{W}_i^V\in\mathbb{R}^{d_v\times \tilde{d}_v}$，然后  
    > $$MultiHead(\boldsymbol{Q},\boldsymbol{K},\boldsymbol{V}) = Concat(head_1,...,head_h)$$  
    > 最后得到一个 $n\times (h\tilde{d}_v)$的序列。**所谓“多头”（Multi-Head），就是只多做几次同样的事情（参数不共享），然后把结果拼接**。
    > 
    > ### Self Attention 
    > 
    > 到目前为止，对Attention层的描述都是一般化的，我们可以落实一些应用。比如，如果做阅读理解的话，$\boldsymbol{Q}$可以是篇章的词向量序列，取$\boldsymbol{K}=\boldsymbol{V}$为问题的词向量序列，那么输出就是所谓的Aligned Question Embedding。
    > 
    > 而在Google的论文中，大部分的Attention都是Self Attention，即“自注意力”，或者叫内部注意力。
    > 
    > 所谓Self Attention，其实就是$Attention(\boldsymbol{X},\boldsymbol{X},\boldsymbol{X})$，$\boldsymbol{X}$就是前面说的输入序列。也就是说，在序列内部做Attention，寻找序列内部的联系。Google论文的主要贡献之一是它表明了内部注意力在机器翻译（甚至是一般的Seq2Seq任务）的序列编码上是相当重要的，而之前关于Seq2Seq的研究基本都只是把注意力机制用在解码端。类似的事情是，目前SQUAD阅读理解的榜首模型R-Net也加入了自注意力机制，这也使得它的模型有所提升。
    > 
    > 当然，更准确来说，Google所用的是Self Multi-Head Attention：  
    > 
    > $$\boldsymbol{Y}=MultiHead(\boldsymbol{X},\boldsymbol{X},\boldsymbol{X})$$
    > 
    > ## Position Embedding 
    > 
    > 然而，只要稍微思考一下就会发现，这样的模型**并不能捕捉序列的顺序**！换句话说，如果将$\boldsymbol{K},\boldsymbol{V}$按行打乱顺序（相当于句子中的词序打乱），那么Attention的结果还是一样的。这就表明了，到目前为止，Attention模型顶多是一个非常精妙的“词袋模型”而已。
    > 
    > 这问题就比较严重了，大家知道，对于时间序列来说，尤其是对于NLP中的任务来说，顺序是很重要的信息，它代表着局部甚至是全局的结构，学习不到顺序信息，那么效果将会大打折扣（比如机器翻译中，有可能只把每个词都翻译出来了，但是不能组织成合理的句子）。
    > 
    > 于是Google再祭出了一招——**Position Embedding**，也就是“位置向量”，将每个位置编号，然后每个编号对应一个向量，通过结合位置向量和词向量，就给每个词都引入了一定的位置信息，这样Attention就可以分辨出不同位置的词了。
    > 
    > Position Embedding并不算新鲜的玩意，在FaceBook的《Convolutional Sequence to Sequence Learning》也用到了这个东西。但在Google的这个作品中，它的Position Embedding有几点区别：
    > 
    > > 1、以前在RNN、CNN模型中其实都出现过Position Embedding，但在那些模型中，Position Embedding是锦上添花的辅助手段，也就是“有它会更好、没它也就差一点点”的情况，因为RNN、CNN本身就能捕捉到位置信息。但是在这个纯Attention模型中，Position Embedding是位置信息的唯一来源，因此它是模型的核心成分之一，并非仅仅是简单的辅助手段。
    > > 
    > > 2、在以往的Position Embedding中，基本都是根据任务训练出来的向量。而Google直接给出了一个构造Position Embedding的公式：  
    > 
    > $$\left\{\begin{aligned}&PE_{2i}(p)=\sin\Big(p/10000^{2i/{d_{pos}}}\Big)\\ &PE_{2i+1}(p)=\cos\Big(p/10000^{2i/{d_{pos}}}\Big) \end{aligned}\right.$$  
    > 这里的意思是将id为$p$的位置映射为一个$d_{pos}$维的位置向量，这个向量的第$i$个元素的数值就是$PE_i(p)$。Google在论文中说到他们比较过直接训练出来的位置向量和上述公式计算出来的位置向量，效果是接近的。因此显然我们更乐意使用公式构造的Position Embedding了。
    > 
    > 3、Position Embedding本身是一个绝对位置的信息，但在语言中，相对位置也很重要，Google选择前述的位置向量公式的一个重要原因是：由于我们有 $\sin(\alpha+\beta)=\sin\alpha\cos\beta+\cos\alpha\sin\beta$以及$\cos(\alpha+\beta)=\cos\alpha\cos\beta-\sin\alpha\sin\beta$，这表明位置$p+k$的向量可以表示成位置$p$的向量的线性变换，这提供了表达相对位置信息的可能性。
    > 
    > 结合位置向量和词向量有几个可选方案，可以把它们拼接起来作为一个新向量，也可以把位置向量定义为跟词向量一样大小，然后两者加起来。FaceBook的论文和Google论文中用的都是后者。直觉上相加会导致信息损失，似乎不可取，但Google的成果说明相加也是很好的方案。看来我理解还不够深刻。
    > 
    > ## 一些不足之处 
    > 
    > 到这里，Attention机制已经基本介绍完了。**Attention层的好处是能够一步到位捕捉到全局的联系，因为它直接把序列两两比较（代价是计算量变为$\mathscr{O}(n^2)$，当然由于是纯矩阵运算，这个计算量相当也不是很严重）；相比之下，RNN需要一步步递推才能捕捉到，而CNN则需要通过层叠来扩大感受野，这是Attention层的明显优势。**
    > 
    > 
    > Google论文剩下的工作，就是介绍它怎么用到机器翻译中，这是个应用和调参的问题，我们这里不特别关心它。当然，Google的结果表明将纯注意力机制用在机器翻译中，能取得目前最好的效果，这结果的确是辉煌的。
    > 
    > 然而，我还是想谈谈这篇论文本身和Attention层自身的一些不足的地方。
    > 
    > > 1、论文标题为《Attention is All You Need》，因此论文中刻意避免出现了RNN、CNN的字眼，但我觉得这种做法过于刻意了。事实上，论文还专门命名了一种Position-wise Feed-Forward Networks，事实上它就是窗口大小为1的一维卷积，因此有种为了不提卷积还专门换了个名称的感觉，有点不厚道。（也有可能是我过于臆测了）
    > > 
    > > 2、Attention虽然跟CNN没有直接联系，但事实上充分借鉴了CNN的思想，比如Multi-Head Attention就是Attention做多次然后拼接，这跟CNN中的多个卷积核的思想是一致的；还有论文用到了残差结构，这也源于CNN网络。
    > > 
    > > 3、无法对位置信息进行很好地建模，这是硬伤。尽管可以引入Position Embedding，但我认为这只是一个缓解方案，并没有根本解决问题。举个例子，用这种纯Attention机制训练一个文本分类模型或者是机器翻译模型，效果应该都还不错，但是用来训练一个序列标注模型（分词、实体识别等），效果就不怎么好了。那为什么在机器翻译任务上好？我觉得原因是机器翻译这个任务并不特别强调语序，因此Position Embedding所带来的位置信息已经足够了，此外翻译任务的评测指标BLEU也并不特别强调语序。
    > > 
    > > 4、并非所有问题都需要长程的、全局的依赖的，也有很多问题只依赖于局部结构，这时候用纯Attention也不大好。事实上，Google似乎也意识到了这个问题，因此论文中也提到了一个restricted版的Self-Attention（不过论文正文应该没有用到它），它假设当前词只与前后$r$个词发生联系，因此注意力也只发生在这$2r+1$个词之间，这样计算量就是$\mathscr{O}(nr)$，这样也能捕捉到序列的局部结构了。但是很明显，这就是卷积核中的卷积窗口的概念！
    > 
    > 通过以上讨论，我们可以体会到，把Attention作为一个单独的层来看，跟CNN、RNN等结构混合使用，应该能更充分融合它们各自的优势，而不必像Google论文号称Attention is All You Need，那样实在有点“矫枉过正”了（“口气”太大），事实上也做不到。就论文的工作而言，也许降低一下身段，称为Attention is All Seq2Seq Need（事实上也这标题的“口气”也很大），会获得更多的肯定。
    > 
    > ## 代码实现 
    > 
    > 最后，为了使得本文有点实用价值，笔者试着给出了论文的Multi-Head Attention的实现代码。有需要的读者可以直接使用，或者参考着修改。
    > 
    > 注意的是，Multi-Head的意思虽然很简单——重复做几次然后拼接，但事实上不能按照这个思路来写程序，这样会非常慢。因为tensorflow是不会自动并行的，比如
    > 
    > ```python
    > a = tf.zeros((10, 10))
    > b = a + 1
    > c = a + 2
    > ```    
    > 
    > 其中b,c的计算是串联的，尽管b、c没有相互依赖。因此我们必须把Multi-Head的操作合并到一个张量来运算，因为单个张量的乘法内部则会自动并行。
    > 
    > 此外，我们要对序列做Mask以忽略填充部分的影响。一般的Mask是将填充部分置零，但Attention中的Mask是要在softmax之前，把填充部分减去一个大整数（这样softmax之后就非常接近0了）。这些内容都在代码中有对应的实现。
    > 
    > ### tensorflow版 
    > 
    > 下面是tf的实现：  
    > [https://github.com/bojone/attention/blob/master/attention_tf.py](https://github.com/bojone/attention/blob/master/attention_tf.py)
    > 
    > ### Keras版 
    > 
    > Keras仍然是我最喜爱的深度学习框架之一，因此必须也得给Keras写一个出来：  
    > [https://github.com/bojone/attention/blob/master/attention_keras.py](https://github.com/bojone/attention/blob/master/attention_keras.py)
    > 
    > ### 代码测试 
    > 
    > 在Keras上对IMDB进行简单的测试（不做Mask）：
    > 
    > ```python
    > from __future__ import print_function
    > from keras.preprocessing import sequence
    > from keras.datasets import imdb
    > 
    > max_features = 20000
    > maxlen = 80
    > batch_size = 32
    > 
    > print('Loading data...')
    > (x_train, y_train), (x_test, y_test) = imdb.load_data(num_words=max_features)
    > print(len(x_train), 'train sequences')
    > print(len(x_test), 'test sequences')
    > 
    > print('Pad sequences (samples x time)')
    > x_train = sequence.pad_sequences(x_train, maxlen=maxlen)
    > x_test = sequence.pad_sequences(x_test, maxlen=maxlen)
    > print('x_train shape:', x_train.shape)
    > print('x_test shape:', x_test.shape)
    > 
    > from keras.models import Model
    > from keras.layers import *
    > 
    > S_inputs = Input(shape=(None,), dtype='int32')
    > embeddings = Embedding(max_features, 128)(S_inputs)
    > # embeddings = Position_Embedding()(embeddings) # 增加Position_Embedding能轻微提高准确率
    > O_seq = Attention(8,16)([embeddings,embeddings,embeddings])
    > O_seq = GlobalAveragePooling1D()(O_seq)
    > O_seq = Dropout(0.5)(O_seq)
    > outputs = Dense(1, activation='sigmoid')(O_seq)
    > 
    > model = Model(inputs=S_inputs, outputs=outputs)
    > # try using different optimizers and different optimizer configs
    > model.compile(loss='binary_crossentropy',
    >               optimizer='adam',
    >               metrics=['accuracy'])
    > 
    > print('Train...')
    > model.fit(x_train, y_train,
    >           batch_size=batch_size,
    >           epochs=5,
    >           validation_data=(x_test, y_test))
    > ```
    >     
    > 
    > 无Position Embedding的结果：
    > 
    > ```
    > Train on 25000 samples, validate on 25000 samples
    > 25000/25000 [==============================] - 9s - loss: 0.4090 - acc: 0.8126 - val_loss: 0.3541 - val_acc: 0.8430
    > Epoch 2/5
    > 25000/25000 [==============================] - 9s - loss: 0.2528 - acc: 0.8976 - val_loss: 0.3962 - val_acc: 0.8284
    > Epoch 3/5
    > 25000/25000 [==============================] - 9s - loss: 0.1731 - acc: 0.9335 - val_loss: 0.5172 - val_acc: 0.8137
    > Epoch 4/5
    > 25000/25000 [==============================] - 9s - loss: 0.1172 - acc: 0.9568 - val_loss: 0.6185 - val_acc: 0.8009
    > Epoch 5/5
    > 25000/25000 [==============================] - 9s - loss: 0.0750 - acc: 0.9730 - val_loss: 0.9310 - val_acc: 0.7925
    > ```
    > 
    > 有Position Embedding的结构：
    > 
    > ```
    > Train on 25000 samples, validate on 25000 samples
    > Epoch 1/5
    > 25000/25000 [==============================] - 9s - loss: 0.5179 - acc: 0.7183 - val_loss: 0.3540 - val_acc: 0.8413
    > Epoch 2/5
    > 25000/25000 [==============================] - 9s - loss: 0.2880 - acc: 0.8786 - val_loss: 0.3464 - val_acc: 0.8447
    > Epoch 3/5
    > 25000/25000 [==============================] - 9s - loss: 0.1584 - acc: 0.9404 - val_loss: 0.4398 - val_acc: 0.8313
    > Epoch 4/5
    > 25000/25000 [==============================] - 9s - loss: 0.0588 - acc: 0.9803 - val_loss: 0.5836 - val_acc: 0.8243
    > Epoch 5/5
    > 25000/25000 [==============================] - 9s - loss: 0.0182 - acc: 0.9947 - val_loss: 0.8095 - val_acc: 0.8178
    > ```
    > 
    > 貌似最高准确率比单层的LSTM准确率还高一点，另外还可以看到Position Embedding能提高准确率、减弱过拟合。
    > 
    > ### 计算量分析 
    > 
    > 可以看到，事实上**Attention的计算量并不低**。比如Self Attention中，首先要对$\boldsymbol{X}$做三次线性映射，这计算量已经相当于卷积核大小为3的一维卷积了，不过这部分计算量还只是$\mathscr{O}(n)$的；然后还包含了两次序列自身的矩阵乘法，这两次矩阵乘法的计算量都是 $\mathscr{O}(n^2)$的，要是序列足够长，这个计算量其实是很难接受的。
    > 
    > 这也表明，restricted版的Attention是接下来的研究重点，并且将Attention与CNN、RNN混合使用，才是比较适中的道路。
    > 
    > 




## UNSUPERVISED MACHINE TRANSLATION 

- [《UNSUPERVISED MACHINE TRANSLATION USING MONOLINGUAL CORPORA ONLY》阅读笔记](https://zhuanlan.zhihu.com/p/32375955)

- [【Science】無監督式機器翻譯，不需要人類干預和平行文本 - 壹讀](https://read01.com/Rnzx84N.html)

    > 這兩篇使用非常相似的方法的新論文也可以在句子層面進行翻譯。它們都使用兩種訓練策略，稱為反向翻譯和去噪（Back translation and Denoising）。在反向翻譯中，先把一種語言的句子大致翻譯成另一種語言，然後再翻譯回原來的語言。如果翻譯後的句子與最初的句子不一致，則調整神經網絡再次翻譯，直到變得越來越接近。
    > 
    > 去噪與反向翻譯類似，但不是從一種語言到另一種語言然後再回來，而是從一種語言（通過重新排列或刪除單詞）中添加噪聲，並嘗試將其翻譯回最開始的語言。這些方法的組合，能夠教給網絡更深層次的語言結構。
    > 
    > 但是兩種技術之間還是有著細微的差異。 UPV的系統在訓練期間更頻繁地進行反向翻譯。由位於賓夕法尼亞州匹茲堡的 Facebook 計算機科學家Guillaume Lample和合作者創建的另一個系統在翻譯過程中則增加了一個額外的步驟。在將一個語言解碼為另一種語言之前，這兩個系統都將其從一種語言編碼為更抽象的表示，但Facebook系統的研究員認為，其系統的「中間語言」是真正抽象的。 Artetxe和Lample都表示，他們可以通過應用對方論文的技巧來改善結果。
    > 
    > 兩篇論文之間唯一可以直接比較的結果是從以包含了3000萬句子的英法文本資料庫中進行的翻譯，兩個系統都在雙語評估替補評分（用來衡量翻譯的準確性）上的得分都在15分左右 。這個數字還比不上谷歌翻譯。谷歌翻譯使用有監督的方法，在同類測試上的得分是40多左右，人類水平是50分左右。但是，這些方法都比詞對詞的翻譯要好。


## Phrase-Based & Neural Unsupervised Machine Translation

- [[1804.07755] Phrase-Based & Neural Unsupervised Machine Translation](https://arxiv.org/abs/1804.07755)

    - [facebookresearch/UnsupervisedMT: Phrase-Based & Neural Unsupervised Machine Translation](https://github.com/facebookresearch/UnsupervisedMT)


- [FAIR新一代无监督机器翻译：模型更简洁，性能更优 | 机器之心](https://www.jiqizhixin.com/articles/Phrase-Based-Neural-Unsupervised-Machine-Translation)

    > ![](https://image.jiqizhixin.com/uploads/editor/84b75cea-df8a-4e0f-b315-8580b97e2703/1524896803075.jpg)
    > 
    > *图 1：无监督 MT 三原则的图示。*
    > 
    > A）两个单语数据集。标记对应于句子（详细信息请参见图例）。B）原则一：初始化。比如，这两个分布通过使用推断的双语词典执行逐词翻译而大致对齐。C）原则二：语言建模。在每个域中独立地学习语言模型，以推断数据中的结构（下面的连续曲线）；它在对句子进行去噪/纠正之前充当数据驱动（如图所示，借助弹簧将曲线外的句子拉回）。D）原则三：回译。从观察到的源语句（红色实心圆）开始，我们使用当前的源语→目标语模型进行翻译（虚线箭头），从而产生可能不正确的翻译（空心圆附近的蓝色十字）。从这次（反向）翻译开始，我们使用目标语→源语模型（连续箭头）来重建初始语言中的句子。重建结果与初始语句的差异为训练目标语→源语模型参数提供了误差信号。在相反的方向上应用相同的步骤来训练源语→目标语模型。
    > 
    > 



## CipherGAN

- [无平行文本照样破解密码，CipherGAN有望提升机器翻译水平](https://zhuanlan.zhihu.com/p/33672256)

    > 针对CipherGAN可以使用非平行文本作输入的特点，Gomez在接受Newsweek外媒采访的时候，也提到了，“密码破译的模型思路也能迁移到非监督学习的翻译上。”
    > 
    > 因为语言翻译常面临的难题是，缺乏足够的平行语料。
    > 
    > 正好和非配对明文密文的密码破译过程很相似。
    > 
    > 


