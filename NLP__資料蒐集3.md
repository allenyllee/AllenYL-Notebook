# NLP__資料蒐集3

[toc]
<!-- toc --> 

## 字串搜尋/模式匹配/拼字修正

### char-rnn

- [The Unreasonable Effectiveness of Recurrent Neural Networks](https://karpathy.github.io/2015/05/21/rnn-effectiveness/)

### scRNN (Robsut Wrod Reocginiton)

- [[1608.02214] Robsut Wrod Reocginiton via semi-Character Recurrent Neural Network](https://arxiv.org/abs/1608.02214)


    > A Brief introduction:
    > 
    > The author of this paper demonstrated a method to recognize jumbled words which like Cmabrigde Uinervtisy(Cambridge University). Training the neural network with correct begin, end characters and the encoded internal characters which doesn't contain it's position information, the neural network can learn to recognize and correct it.
    > 
    > You can easily modify the network structure to adapt your own need, the OCR, as you had mentioned.
    > 
    > ![](https://screenshotscdn.firefoxusercontent.com/images/24464385-3bef-4555-80ce-669d252fe5fe.png)
    > 
    > ![](https://screenshotscdn.firefoxusercontent.com/images/313b52fb-f590-4904-9144-f1044160a0df.png)

### Compare-Aggregate

- [[1611.01747] A Compare-Aggregate Model for Matching Text Sequences](https://arxiv.org/abs/1611.01747)

- [《A COMPARE-AGGREGATE MODEL FOR MATCHING TEXT SEQUENCES》阅读笔记](https://zhuanlan.zhihu.com/p/27805225)

    > **主要方法：**
    > 
    > 这篇论文的方法是基于Compare-Aggregate 框架设计的，这个框架最早是由Google的parikh等人在《A Decomposable Attention Model for Natural Language Inference》这篇文章中提出的，用于解决Natural Language Inference问题。关于这篇文章可以看一下另外一篇阅读笔记[《A Decomposable Attention Model for Natural Language Inference》阅读笔记](https://zhuanlan.zhihu.com/p/26237357)。作者重点比较了几种不同的comparison function，下面还是先整体看一下整个模型。
    > 
    > ![](https://pic4.zhimg.com/80/v2-92f2627d547bfe1b427378d6f93c9bd3_hd.jpg)
    > 
    > Preprocessing：首先对原始的问题和答案进行预处理，使每个词获得句子的上下文信息，具体公式如下：
    > 
    > ![](https://pic1.zhimg.com/80/v2-7ff9a21c3b2b7aed521feb9b65a37ddf_hd.jpg)
    > 
    > 这里类似LSTM的门函数，只是这里做了一点简化，只保留了输入门。 ![\bigodot ](https://www.zhihu.com/equation?tex=%5Cbigodot+) 表示element-wise 乘积，W、b是模型参数。
    > 
    > Attention：这里的attention就是传统的attention机制，用问题对答案加attention。具体公式如下：
    > 
    > ![](https://pic1.zhimg.com/80/v2-f3f409526ef7b722fcfa6d86d5b19acc_hd.jpg)
    > 
    > 这里我们得到了attention-weighted vectors H。
    > 
    > Comparison：这个部分作者比较了多种comparison方式，都是对上一步得到的attention-weighted vector ![H](https://www.zhihu.com/equation?tex=H) 以及 答案向量![\bar{A}](https://www.zhihu.com/equation?tex=%5Cbar%7BA%7D)进行comparison。
    > 
    > ![](https://pic3.zhimg.com/80/v2-be13f06dc5965c997fc687f09b0d6c71_hd.jpg)
    > 
    > Neuralnet就是将两个向量拼接起来，然后过一层神经网络。
    > 
    > ![](https://pic4.zhimg.com/80/v2-cac03e29df3c7500f14d4dc2422eb026_hd.jpg)
    > 
    > Neuraltensornet用张量网络（neural tensor network）连接两个向量，再过一次relu。
    > 
    > ![](https://pic3.zhimg.com/80/v2-0b4fc5b9d4546b24ed81f677f5d1e7bb_hd.jpg)
    > 
    > 这里就是计算两个向量的欧式距离以及它们的余弦相似度，再把两者的结果拼接起来。
    > 
    > ![](https://pic4.zhimg.com/80/v2-17d2b2bbb5b9d1bf65bd5e38936f2ee2_hd.jpg)
    > 
    > 这两种方法主要是基于element-wise的方式对两个向量进行比较。
    > 
    > ![](https://pic4.zhimg.com/80/v2-9b1cae492c4b1afb2b138bfe342ae5dd_hd.jpg)
    > 
    > Submult+nn就是把以上两个比较方式的结果进行拼接，再过一层神经网络。
    > 
    > 注意这里的比较都是针对两个句子对应位置上的每个词进行比较，所以得到的结果向量的长度与答案的长度相同。
    > 
    > Aggregation：对comparison的结果进行整合，这里用CNN来进行aggregation。
    > 
    > ![](https://pic4.zhimg.com/80/v2-3c0acfe5112c72b50b87e57a0aeb4ac1_hd.jpg)
    > 
    > 利用这个向量 ![r](https://www.zhihu.com/equation?tex=r) ，根据不同的任务进行模型的训练和预测，其中文本蕴含就是做一个三分类，对于答案选择任务，则是从多个候选答案中进行选择，那么可以用下式进行预测
    > 
    > ![](https://pic3.zhimg.com/80/v2-7f5743dbd4247a1dacbcb01b17dc044d_hd.jpg)
    > 

### DeepSpeller

- [Deep Spelling – Machine Learnings](https://machinelearnings.co/deep-spelling-9ffef96a24f6)

    - [How to Write a Spelling Corrector](http://norvig.com/spell-correct.html)

    - [MajorTal/DeepSpell: a Deep Learning based Speller](https://github.com/MajorTal/DeepSpell)

### Natural Language Correction

- [Natural Language Correction - DPTX_2016_1_11320_0_477390_0_188260.pdf](https://dspace.cuni.cz/bitstream/handle/20.500.11956/85667/DPTX_2016_1_11320_0_477390_0_188260.pdf?sequence=1)

    ![](https://screenshotscdn.firefoxusercontent.com/images/be769eae-3339-41be-b941-75f78c06bbd0.png)

    ![](https://screenshotscdn.firefoxusercontent.com/images/81ac8738-63d2-4332-8491-2a26097a97f4.png) 
    

### Neural Networks for Text Correction and Completion in Keyboard Decoding

- [[1709.06429] Neural Networks for Text Correction and Completion in Keyboard Decoding](https://arxiv.org/abs/1709.06429)

### CNN Sentence Matching

- [卷积神经网络(CNN)在句子建模上的应用 | Jey Zhang](http://www.jeyzhang.com/cnn-apply-on-modelling-sentence.html)

    - [[1503.03244] Convolutional Neural Network Architectures for Matching Natural Language Sentences](https://arxiv.org/abs/1503.03244)

    > #### 模型结构与原理
    > 
    > **1\. 基于CNN的句子建模**
    > 
    > 这篇论文主要针对的是**句子匹配(Sentence Matching)**的问题，但是基础问题仍然是句子建模。首先，文中提出了一种基于CNN的句子建模网络，如下图：
    > 
    > [![](http://i.imgur.com/kG7AbW3.png)](http://i.imgur.com/kG7AbW3.png)
    > 
    > 图中灰色的部分表示对于长度较短的句子，其后面不足的部分填充的全是0值(Zero Padding)。可以看出，模型解决不同长度句子输入的方法是规定一个最大的可输入句子长度，然后长度不够的部分进行0值的填充；图中的卷积计算和传统的CNN卷积计算无异，而池化则是使用Max-Pooling。
    > 
    > -   **卷积结构的分析**
    > 
    > 下图示意性地说明了卷积结构的作用，作者认为卷积的作用是**从句子中提取出局部的语义组合信息**，而多张`Feature Map`则是从多种角度进行提取，也就是**保证提取的语义组合的多样性**；而池化的作用是对多种语义组合进行选择，过滤掉一些置信度低的组合（可能这样的组合语义上并无意义）。
    > 
    > [![](http://i.imgur.com/yrFS2k1.png)](http://i.imgur.com/yrFS2k1.png)
    > 
    > **2\. 基于CNN的句子匹配模型**
    > 
    > 下面是基于之前的句子模型，建立的两种用于两个句子的匹配模型。
    > 
    > **2.1 结构I**
    > 
    > 模型结构如下图：
    > 
    > [![](http://i.imgur.com/xaP0KNV.png)](http://i.imgur.com/xaP0KNV.png)
    > 
    > 简单来说，首先分别单独地对两个句子进行建模（使用上文中的句子模型），从而得到两个相同且固定长度的向量，向量表示句子经过建模后抽象得来的特征信息；然后，将这两个向量作为一个多层感知机(MLP)的输入，最后计算匹配的分数。
    > 
    > 这个模型比较简单，但是有一个较大的缺点：两个句子在建模过程中是完全独立的，没有任何交互行为，一直到最后生成抽象的向量表示后才有交互行为（一起作为下一个模型的输入），这样做使得句子在抽象建模的过程中会丧失很多语义细节，同时过早地失去了句子间语义交互计算的机会。因此，推出了第二种模型结构。
    > 
    > **2.2 结构II**
    > 
    > 模型结构如下图：
    > 
    > [![](http://i.imgur.com/NWvAPVr.png)](http://i.imgur.com/NWvAPVr.png)
    > 
    > 图中可以看出，这种结构提前了两个句子间的交互行为。
    > 
    > -   **第一层卷积层**
    > 
    > 第一层中，首先取一个固定的卷积窗口k1
    > 
    > ，然后遍历 Sx 和 Sy
    > 
    > 中所有组合的二维矩阵进行卷积，每一个二维矩阵输出一个值（文中把这个称作为一维卷积，因为实际上是把组合中所有词语的vector排成一行进行的卷积计算），构成Layer-2。下面给出数学形式化表述：
    > 
    > [![](http://i.imgur.com/f3DqYsp.png)](http://i.imgur.com/f3DqYsp.png)
    > 
    > -   **第一层卷积层后的Max-Pooling层**
    > 
    > 从而得到Layer-2，然后进行2×2的Max-pooling：
    > 
    > [![](http://i.imgur.com/DaFv3ps.png)](http://i.imgur.com/DaFv3ps.png)
    > 
    > -   **后续的卷积层**
    > 
    > 后续的卷积层均是传统的二维卷积操作，形式化表述如下：
    > 
    > [![](http://i.imgur.com/Pr5Mm9n.png)](http://i.imgur.com/Pr5Mm9n.png)
    > 
    > -   **二维卷积结果后的Pooling层**
    > 
    > 与第一层卷积层后的简单Max-Pooling方式不同，后续的卷积层的Pooling是一种**动态Pooling方法**，这种方法来源于参考文献[1]。
    > 
    > -   **结构II的性质**
    > 
    > 1.  保留了词序信息；
    > 2.  更具一般性，实际上结构I是结构II的一种特殊情况（取消指定的权值参数）；
    > 
    > #### 实验部分
    > 
    > **1\. 模型训练及参数**
    > 
    > -   使用基于排序的自定义损失函数(Ranking-based Loss)
    > -   BP反向传播+随机梯度下降；
    > -   mini-batch为100-200,并行化；
    > -   为了防止过拟合，对于中型和大型数据集，会提前停止模型训练；而对于小型数据集，还会使用Dropout策略；
    > -   Word2Vector：50维；英文语料为Wikipedia(~1B words)，中文语料为微博数据(~300M words)；
    > -   使用ReLu函数作为激活函数；
    > -   卷积窗口为3-word window；
    > -   使用Fine tuning；
    > 
    > **2\. 实验结果**
    > 
    > 一共做了三个实验，分别是(1)句子自动填充任务，(2)推文与评论的匹配，以及(3)同义句识别；结果如下面的图示：
    > 
    > [![](http://i.imgur.com/wLIUAHW.png)](http://i.imgur.com/wLIUAHW.png)
    > 
    > [![](http://i.imgur.com/fO0Xhnj.png)](http://i.imgur.com/fO0Xhnj.png)
    > 
    > [![](http://i.imgur.com/qRfsoB0.png)](http://i.imgur.com/qRfsoB0.png)
    > 
    > 其实结构I和结构II的结果相差不大，结构II稍好一些；而相比于其他的模型而言，结构I和结构II的优势还是较大的。
    > 


### CNN Detect Search term

- [[1708.02238] A Convolutional Neural Network for Search Term Detection](https://arxiv.org/abs/1708.02238)

    ![](https://screenshotscdn.firefoxusercontent.com/images/72627aea-ca71-4827-a342-c3ef9379194c.png)


### dedupe

- [dedupeio/dedupe: A python library for accurate and scaleable fuzzy matching, record deduplication and entity-resolution.](https://github.com/dedupeio/dedupe)



### Generate Regex from examples 

- [classification - Machine Learning technique for learning string patterns - Cross Validated](https://stats.stackexchange.com/questions/233795/machine-learning-technique-for-learning-string-patterns)

    > Could your problem be restated as wanting to discover the regular expressions that will match the strings in each category? This is a "regex generation" problem, a subset of the [grammar induction](https://en.wikipedia.org/wiki/Grammar_induction) problem (see also [Alexander Clark's website](http://www.cs.rhul.ac.uk/home/alexc/)).
    > 
    > The regular expression problem is easier. I can point you to code [frak](https://github.com/noprompt/frak) and [RegexGenerator](https://github.com/MaLeLabTs/RegexGenerator). The [online RegexGenerator++](http://regex.inginf.units.it/demo.html) has references to their academic papers on the problem.
    > 
    > ---
    > 
    > 
    > You could try recurrent neural networks, where your input is a sequence of the letters in the word, and your output is a category. This fits your requirement such that you don't hand code any features.
    > 
    > However for this method to actually work you will require a fairly large training data set.
    > 
    > You can refer [Supervised Sequence Labelling with Recurrent Neural Networks by Alex Graves](http://link.springer.com/chapter/10.1007/978-3-642-24797-2_2) chapter 2 for more details.
    > 
    > This is a link to the [preprint](https://www.cs.toronto.edu/~graves/preprint.pdf)
    > 

- [regex - Is it possible for a computer to "learn" a regular expression by user-provided examples? - Stack Overflow](https://stackoverflow.com/questions/616292/is-it-possible-for-a-computer-to-learn-a-regular-expression-by-user-provided-e)

    - [Inference of Regular Expressions for Text Extraction from Examples - Machine Learning Lab](http://machinelearning.inginf.units.it/publications/international-journal-publications/inferenceofregularexpressionsfortextextractionfromexamples)
    - [MaLeLabTs/RegexGenerator: This project contains the source code of a tool for generating regular expressions for text extraction: 1. automatically, 2. based only on examples of the desired behavior, 3. without any external hint about how the target regex should look like](https://github.com/MaLeLabTs/RegexGenerator)

    > Yes, it is possible, we can generate regexes from examples (text -> desired extractions). This is a working online tool which does the job: <http://regex.inginf.units.it/>
    > 
    > Regex Generator++ online tool generates a regex from provided examples using a GP search algorithm. The GP algorithm is driven by a multiobjective fitness which leads to higher performance and simpler solution structure (Occam's Razor). This tool is a demostrative application by the Machine Lerning Lab, Trieste Univeristy (Università degli studi di Trieste). Please look at the video tutorial [here](http://regex.inginf.units.it/demo.html).
    > 
    > This is a research project so you can read about used algorithms [here](http://regex.inginf.units.it/how.html).
    > 


### Generate Regex from natural language

- [[1608.03000] Neural Generation of Regular Expressions from Natural Language with Minimal Domain Knowledge](https://arxiv.org/abs/1608.03000)

    - [DeepRegex: Neural Generation of Regular Expressions from Natural Language | Hacker News](https://news.ycombinator.com/item?id=12269468)
    - [nicholaslocascio/deep-regex: Code for the paper Neural Generation of Regular Expressions from Natural Language with Minimal Domain Knowledge (EMNLP 2016). http://arxiv.org/abs/1608.03000](https://github.com/nicholaslocascio/deep-regex)
    
    ![](https://raw.githubusercontent.com/nicholaslocascio/deep-regex/master/model5.png)


### Deep Learning for Extract text

- [Deep Learning for RegEx](https://dlacombejr.github.io/2016/11/13/deep-learning-for-regex.html)

    > The Problem
    > -----------
    > 
    > From the competition website, "The objective of this contest is to extract the MPN for a given product from its Title/Description using regex patterns." Now, I didn't know what RegEx patterns were, but I could understand the problem of extracting text from a larger text. For my purposes, given that I wanted to learn representations, it was enough for me to understand that if I had the following:
    > 
    > > EVGA NVIDIA GeForce GTX 1080 Founders Edition 8gb Gddr5x 08GP46180KR
    > 
    > Then I just wanted to extract the MPN "08GP46180KR" using some representations that learned to distinguish MPNs from other text making up the product title and description.
    > 
    > ---
    > 
    > Problem Formulation
    > -------------------
    > 
    > Assuming that we want to build some neural network that we can train using back-propagation, the next question is what is the appropriate output and loss function. The most natural choice seemed to be that the output would be just the MPN in the embedded vectorial format. This, in combination with a loss like [Mean-Squared Error](https://en.wikipedia.org/wiki/Mean_squared_error) that is common of generative models in unsupervised learning just did not do the trick due to technical reasons.
    > 
    > Eventually I converged on the following solution that was sufficient to get some reasonable results. Namely, I defined the output of the network to be two one-hot binary vectors with a length equal to the max length (set to 2000 here), where the first vector indicated the starting index of the MPN and the second vector indicated the ending index of the MPN. Then the loss was simply the summed categorical crossentropy for both vectors.
    > 
    > Given this output, an auxiliary function was then created on the backend to extract the MPN vectorial representation from the input given the two indices and then convert the embedded MPN back to a string representation as the final output. In the cases where no MPN was present, the target was defined as ones at the end of both vectors.
    > 
    > ---
    > 
    > Model Architecture
    > ------------------
    > 
    > Ok, so now that the data has been embedded, and our target has been formulated, the next step was to build a model that would perform the above task well. I tried a bunch of different neural network models, including deep convolutional neural networks with standard architectures (e.g., 2D conv-net with max-pooling layers). These produced good but unsatisfactory results -- nothing that was going to get me a winning spot.
    > 
    > Fortunately, [Google DeepMind](https://deepmind.com/) had just put out a paper on their new model WaveNet that used causal, dilated convolutions that served as the seed of my idea. [WaveNet](https://deepmind.com/blog/wavenet-generative-model-raw-audio/), and other similar models, were very intriguing because they used multiple layers of convolutional operators with no pooling that were able to obtain filters with very large receptive fields while keeping the number of parameters within a reasonable range because of the dilations used at each subsequent layer (see the red portion of the figure below; image source -- [Neural Machine Translation in Linear Time](https://arxiv.org/abs/1610.10099)).
    > 
    > [![](https://dlacombejr.github.io/assets/CAX_blog/dilated_convolution.jpg)](https://dlacombejr.github.io/2016/11/13/deep-learning-for-regex.html)
    > 
    > Illustration of dilated convolutions on single-dimensional data
    > 
    > The final model idea that I converged on was to extract a set of basic features from the input, feed them through a series of dilated convolutions and then branch off two convolutional filters with softmax activation functions to predict start and end indices. In more detail, the model was as follows:
    > 
    > -   Extract basic features from input using 1D convolutions of varying lengths (1, 3, 5, 7 with 75, 75, 50, and 50 fiters for each length, respectively); these represent single-character to multi-character representations of varying length. These representations were then concatenated and feed forward to next layers.
    > -   Next these representations were fed through a series of blocks that perform 1D à trous (or dilated) convolutions with Batch Normalization, Rectified Linear Units, and skip connections. This allowed the network to choose the best matching start and end indices based on scopes that covered almost the entire input due to the dilated convolutions.
    > -   Finally, two 1D convolutional filters with softmax activations were performed over the residual output; the maximum argument represented the index of highest probability for the start and end indices.
    > 
    > The model architecture is represented graphically below, showing the major features of the model.
    > 
    > [![](https://dlacombejr.github.io/assets/CAX_blog/model.png)](https://dlacombejr.github.io/2016/11/13/deep-learning-for-regex.html)
    > 
    > Illustration of dilated convolutions on single-dimensional data
    > 
    > Performance
    > -----------
    > 
    > After training, I observed that the model was close to perfect on the training set, hovered around ~90% accuracy for the validation set, and obtained ~84% on the public leaderboard. Not bad!
    > 
    > One thing that I noticed as I was scrambling to make submissions was that the model overfit the data very quickly due to the relatively small number of samples. I know that with only ~54,000 training examples, learning representations directly from the data was a bit risky, but I believe with a couple hundred thousand, my solution might have placed higher. Because I was late to the competition, I just chose to lower the learning rate and only train for a couple of epochs, which in the end worked out for me. However, provided that there was more time, I would have liked to explore some data augmentation techniques and model regularization which would have helped made the model more expressive and prevented overfitting. Additionally, pretraining on other text might have been a successful strategy. A brute-force effort would have also been increasing the max length parameter slightly, that may have given me some marginal improvements, but at a very high computational cost.
    > 


### time-delay neural networks

- [Fast pattern matching with time-delay neural networks - Semantic Scholar](https://www.semanticscholar.org/paper/Fast-pattern-matching-with-time-delay-neural-Hoffmann-Howard/fd8540b8eae91a20453a3c7af1498393237b0c82)

    - [magicNet.pdf](http://heikohoffmann.de/documents/magicNet.pdf)


### Fuzzy Matching

- [Fuzzy Matching Algorithms To Help Data Scientists Match Similar Data - Data Science Central](https://www.datasciencecentral.com/profiles/blogs/fuzzy-matching-algorithms-to-help-data-scientists-match-similar)

    > [![](https://api.ning.com/files/tFu4DrQFBvHDh0qLT6XdOclOk-HIgLezt4PE48MdyKymJ5s8c*ulck8L7bAZ5tIbNm9ZzVYcIbq*5gj-VLKb7bwSkMmjyL*j/FuzzyMatchPic_Megter.png?width=500)](https://api.ning.com/files/tFu4DrQFBvHDh0qLT6XdOclOk-HIgLezt4PE48MdyKymJ5s8c*ulck8L7bAZ5tIbNm9ZzVYcIbq*5gj-VLKb7bwSkMmjyL*j/FuzzyMatchPic_Megter.png)
    > 
    > A common scenario for data scientists is the marketing, operations or business groups give you two sets of similar data with different variables & asks the analytics team to normalize both data sets to have  a common record for modelling.
    > 
    > Here is an example of two similar data sets:
    > 
    > |**Data Set 1** |  |**Data Set 2** |  |
    > |---------------|--|----------------|--|
    > |Organization Name |Sales |Organization Name |# of Customers |
    > |John Doe Inc |$300 |Sally Harper Cntr |10 |
    > |Saint Rogers |$400 |John Doe Incorporated |50 |
    > |Sally Harper Center |$500 |St. Rogers |100 |
    > 
    > How would you as a data scientist match these two different but similar data sets to have a master record for modelling?
    > 
    > Short of doing it manually, the most common method is fuzzy matching.
    > 
    > So, what is Fuzzy matching? Here is a short description [from Wikipedia](https://en.wikipedia.org/wiki/Fuzzy_matching_(computer-assisted_translation)):
    > 
    > *Fuzzy matching is a technique used in computer-assisted translation as a special case of record linkage. It works with matches that may be less than 100% perfect when finding correspondences between segments of a text and entries in a database of previous translations. It usually operates at sentence-level segments, but some translation technology allows matching at a phrasal level. It is used when the translator is working with translation memory.*
    > 
    > Given below is list of algorithms to implement fuzzy matching algorithms which themselves are available in many open source libraries:
    > 
    > **Levenshtein distance Algorithm**
    > 
    > Levenshtein distance is a string metric for measuring the difference between two sequences. Informally, the Levenshtein distance between two words is the minimum number of single-character edits (i.e. insertions, deletions or substitutions) required to change one word into the other.
    > 
    > **Damerau--Levenshtein distance**
    > 
    > Damerau--Levenshtein distance is a distance (string metric) between two strings, i.e., finite sequence of symbols, given by counting the minimum number of operations needed to transform one string into the other, where an operation is defined as an insertion, deletion, or substitution of a single character, or a transposition of two adjacent characters.
    > 
    > **Bitap algorithm with modifications by Wu and Manber**
    > 
    > Bitmap algorithm is an approximate string matching algorithm. The algorithm tells whether a given text contains a substring which is "approximately equal" to a given pattern, where approximate equality is defined in terms of Levenshtein distance --- if the substring and pattern are within a given distance k of each other, then the algorithm considers them equal.
    > 
    > **n-gram**
    > 
    > n-gram is a contiguous sequence of n items from a given sequence of text or speech. The items can be phonemes, syllables, letters, words or base pairs according to the application. An n-gram model is a type of probabilistic language model for predicting the next item in such a sequence in the form of a (n - 1)--order Markov model.
    > 
    > **BK-tree**
    > 
    > A BK-tree is a metric tree suggested by Walter Austin Burkhard and Robert M. Keller specifically adapted to discrete metric spaces.To understand, let us consider integer discrete metric d(x,y). Then, BK-tree is defined in the following way. An arbitrary element a is selected as root node. The root node may have zero or more subtrees. The k-th subtree is recursively built of all elements b such that d(a,b) = k. BK-trees can be used for approximate string matching in a dictionary
    > 
    > **Soundex**
    > 
    > Soundex is a phonetic algorithm for indexing names by sound, as pronounced in English. The goal is for homophones to be encoded to the same representation so that they can be matched despite minor differences in spelling.
    > 

