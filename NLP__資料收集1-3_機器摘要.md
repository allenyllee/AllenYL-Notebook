# NLP__資料收集1-3_機器摘要

[toc]
<!-- toc --> 

# 機器摘要


## deep reinforced summarization


- [Salesforce research](https://einstein.ai/research/your-tldr-by-an-ai-a-deep-reinforced-model-for-abstractive-summarization)

    - [[1705.04304] A Deep Reinforced Model for Abstractive Summarization](https://arxiv.org/abs/1705.04304)

    - [An Algorithm Summarizes Lengthy Text Surprisingly Well - MIT Technology Review](https://www.technologyreview.com/s/607828/an-algorithm-summarizes-lengthy-text-surprisingly-well/)


## A Gentle Introduction to Text Summarization

- [A Gentle Introduction to Text Summarization](https://machinelearningmastery.com/gentle-introduction-text-summarization/)

    > How to Summarize Text
    > ---------------------
    > 
    > There are two main approaches to summarizing text documents; they are:
    > 
    > 1\. Extractive Methods.\
    > 2\. Abstractive Methods.
    > 
    > > The different dimensions of text summarization can be generally categorized based on its input type (single or multi document), purpose (generic, domain specific, or query-based) and output type (extractive or abstractive).
    > 
    > --- [A Review on Automatic Text Summarization Approaches](http://thescipub.com/PDF/jcssp.2016.178.190.pdf), 2016.
    > 
    > Extractive text summarization involves the selection of phrases and sentences from the source document to make up the new summary. Techniques involve ranking the relevance of phrases in order to choose only those most relevant to the meaning of the source.
    > 
    > Abstractive text summarization involves generating entirely new phrases and sentences to capture the meaning of the source document. This is a more challenging approach, but is also the approach ultimately used by humans. Classical methods operate by selecting and compressing content from the source document.
    > 
    > > ... there are two different approaches for automatic summarization: extraction and abstraction. Extractive summarization methods work by identifying important sections of the text and generating them verbatim; [...] abstractive summarization methods aim at producing important material in a new way. In other words, they interpret and examine the text using advanced natural language techniques in order to generate a new shorter text that conveys the most critical information from the original text
    > 
    > --- [Text Summarization Techniques: A Brief Survey](https://arxiv.org/abs/1707.02268), 2017.
    > 
    > Classically, most successful text summarization methods are extractive because it is an easier approach, but abstractive approaches hold the hope of more general solutions to the problem.
    > 
    > Deep Learning For Text Summarization
    > ------------------------------------
    > 
    > Recently deep learning methods have shown promising results for text summarization.
    > 
    > Approaches have been proposed inspired by the application of deep learning methods for automatic machine translation, specifically by framing the problem of text summarization as a sequence-to-sequence learning problem.
    > 
    > > Abstractive text summarization is the task of generating a headline or a short summary consisting of a few sentences that captures the salient ideas of an article or a passage. [...] This task can also be naturally cast as mapping an input sequence of words in a source document to a target sequence of words called summary.
    > 
    > --- [Abstractive Text Summarization Using Sequence-to-Sequence RNNs and Beyond](https://arxiv.org/abs/1602.06023), 2016.
    > 
    > These deep learning approaches to automatic text summarization may be considered abstractive methods and generate a wholly new description by learning a language generation model specific to the source documents.
    > 
    > > ... the recent success of sequence-to-sequence models, in which recurrent neural networks (RNNs) both read and freely generate text, has made abstractive summarization viable
    > 
    > --- [Get To The Point: Summarization with Pointer-Generator Networks](https://arxiv.org/abs/1704.04368), 2017.
    > 
    > The results of deep learning methods are not yet state-of-the-art compared to extractive methods, yet impressive results have been achieved on constrained problems such as generating headlines for news articles that rival or out-perform other abstractive methods.
    > 
    > The promise of the approach is that the models can be trained end-to-end without specialized data preparation or submodels and that the models are entirely data-driven, without the preparation of specialized vocabulary or expertly pre-processed source documents.
    > 
    > > ... we propose a fully data-driven approach to abstractive sentence summarization. [...] the model is structurally simple, it can easily be trained end-to-end and scales to a large amount of training data.
    > 
    > --- [A Neural Attention Model for Abstractive Sentence Summarization](https://arxiv.org/abs/1509.00685), 2015
    > 
    > Further Reading
    > ---------------
    > 
    > This section provides more resources on the topic if you are looking go deeper.
    > 
    > ### Text Summarization Papers
    > 
    > -   [A Review on Automatic Text Summarization Approaches](http://thescipub.com/PDF/jcssp.2016.178.190.pdf), 2016.
    > -   [A Review Paper on Text Summarization](https://www.ijarcce.com/upload/2016/march-16/IJARCCE%2040.pdf), 2016.
    > -   [Text Summarization Techniques: A Brief Survey](https://arxiv.org/abs/1707.02268), 2017.
    > 
    > ### Deep Learning Text Summarization Papers
    > 
    > -   [A Neural Attention Model for Abstractive Sentence Summarization](https://arxiv.org/pdf/1509.00685.pdf), 2015
    > -   [Abstractive Text Summarization Using Sequence-to-Sequence RNNs and Beyond](https://arxiv.org/abs/1602.06023), 2016.
    > -   [Get To The Point: Summarization with Pointer-Generator Networks](https://arxiv.org/abs/1704.04368), 2017.
    > 
    > ### Books
    > 
    > -   [Advances in Automatic Text Summarization](http://amzn.to/2giFqN1), 1999.
    > -   [Automatic Text Summarization](http://amzn.to/2wgob34), 2014.
    > -   [Innovative Document Summarization Techniques: Revolutionizing Knowledge Understanding](http://amzn.to/2gigHIS), 2014.
    > 
    > ### Articles
    > 
    > -   [Automatic summarization](https://en.wikipedia.org/wiki/Automatic_summarization)
    > -   [Text summarization with TensorFlow](https://research.googleblog.com/2016/08/text-summarization-with-tensorflow.html), 2016
    > -   [Has Deep Learning been applied to automatic text summarization (successfully)?](https://www.quora.com/Has-Deep-Learning-been-applied-to-automatic-text-summarization-successfully)
    > -   [Taming Recurrent Neural Networks for Better Summarization](http://www.abigailsee.com/2017/04/16/taming-rnns-for-better-summarization.html), 2017.
    > -   [Deep Learning for Text Summarization](http://deeplearningkit.org/2016/04/23/deep-learning-for-text-summarization/)


## Encoder-Decoder Deep Learning Models for Text Summarization

- [Encoder-Decoder Deep Learning Models for Text Summarization](https://machinelearningmastery.com/encoder-decoder-deep-learning-models-text-summarization/)

    > Facebook Model
    > --------------
    > 
    > This approach was described by Alexander Rush, et al. from Facebook AI Research (FAIR) in their 2015 paper "[A Neural Attention Model for Abstractive Sentence Summarization](https://arxiv.org/abs/1509.00685)".
    > 
    > The model was developed for sentence summarization, specifically:
    > 
    > > Given an input sentence, the goal is to produce a condensed summary. [...] A summarizer takes x as input and outputs a shortened sentence y of length N < M. We will assume that the words in the summary also come from the same vocabulary
    > 
    > This is a simpler problem than, say, full document summarization.
    > 
    > The approach follows the general approach used for neural machine translation with an encoder and a decoder. Three different decoders are explored:
    > 
    > -   **Bag-of-Words Encoder**. The input sentence is encoded using a bag-of-words model, discarding word order information.
    > -   **Convolutional Encoder**. A word embedding representation is used followed by time-delay convolutional layers across words and pooling layers.
    > -   **Attention-Based Encoder**. A word embedding representation is used with a simple attention mechanism over a context vector, providing a type of soft alignment between input sentence and output summary.
    > 
    > ![Network Diagram of Encoder and Decoder Elements](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2017/09/Network-Diagram-of-Encoder-and-Decoder-Elements.png)
    > 
    > Network Diagram of Encoder and Decoder Elements\
    > Taken from "A Neural Attention Model for Abstractive Sentence Summarization".
    > 
    > A beam search is then used in the generation of text summaries, not unlike the approach used in machine translation.
    > 
    > The model was evaluated on the standard [DUC-2014 dataset](http://duc.nist.gov/data.html) that involves generating approximately 14-word summaries for 500 news articles.
    > 
    > The data for this task consists of 500 news articles from the New York Times and Associated Press Wire services each paired with 4 different human-generated reference summaries (not actually headlines), capped at 75 bytes.
    > 
    > The model was also evaluated on the [Gigaword dataset](https://catalog.ldc.upenn.edu/LDC2012T21) of approximately 9.5 million news articles, where a headline was generated given the first sentence of the news article.
    > 
    > Results were reported on both problems using the ROUGE-1, ROUGE-2, and ROUGE-L measures and the tuned system was shown to achieve state-of-the-art results on the DUC-2004 dataset.
    > 
    > > The model shows significant performance gains on the DUC-2004 shared task compared with several strong baselines.
    > 
    > IBM Model
    > ---------
    > 
    > This approach was described by Ramesh Nallapati, et al. from IBM Watson in their 2016 paper "[Abstractive Text Summarization using Sequence-to-sequence RNNs and Beyond](https://arxiv.org/abs/1602.06023)".
    > 
    > The approach is based on the encoder-decoder recurrent neural network with attention, developed for machine translation.
    > 
    > > Our baseline model corresponds to the neural machine translation model used in Bahdanau et al. (2014). The encoder consists of a bidirectional GRU-RNN (Chung et al., 2014), while the decoder consists of a uni-directional GRU-RNN with the same hidden-state size as that of the encoder, and an attention mechanism over the source-hidden states and a soft-max layer over target vocabulary to generate words.
    > 
    > A word embedding for input words is used, in addition to an embedding for tagged parts of speech and discretized TF and IDF features. This richer input representation was designed to give the model better performance on identifying key concepts and entities in the source text.
    > 
    > The model also uses a learned-switch mechanism to decide whether or not to generate an output word or point to a word in the input sequence, designed to handle rare and low-frequency words.
    > 
    > > ... the decoder is equipped with a 'switch' that decides between using the generator or a pointer at every time-step. If the switch is turned on, the decoder produces a word from its target vocabulary in the normal fashion. However, if the switch is turned off, the decoder instead generates a pointer to one of the word-positions in the source.
    > 
    > Finally, the model is hierarchical in that the attention mechanism operates both at the word-level and at the sentence level on the encoded input data.
    > 
    > ![Hierarchical encoder with hierarchical attention](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2017/09/Hierarchical-encoder-with-hierarchical-attention.png)
    > 
    > Hierarchical encoder with hierarchical attention.\
    > Taken from "Abstractive Text Summarization using Sequence-to-sequence RNNs and Beyond."
    > 
    > A total of 6 variants of the approach were evaluated on the DUC-2003/2004 dataset and the Gigaword dataset, both used to evaluate the Facebook model.
    > 
    > The model was also evaluated on a new corpus of news articles from the CNN and Daily Mail websites.
    > 
    > The IBM approach achieved impressive results on the standard datasets compared to the Facebook approach and others.
    > 
    > > ... we apply the attentional encoder-decoder for the task of abstractive summarization with very promising results, outperforming state-of-the-art results significantly on two different datasets.
    > 
    > Google Model
    > ------------
    > 
    > This approach was described by Abigail See, et al. from Stanford in their 2017 paper "[Get To The Point: Summarization with Pointer-Generator Networks](https://arxiv.org/abs/1704.04368)."
    > 
    > A better name might be the "Stanford Model," but I am trying to tie this work in with the co-author Peter Liu (of Google Brain) 2016 post titled "[Text summarization with TensorFlow](https://research.googleblog.com/2016/08/text-summarization-with-tensorflow.html)" on the Google Research Blog.
    > 
    > In their blog post, Peter Liu, et al. at Google Brain introduce a [TensorFlow model](https://github.com/tensorflow/models/tree/master/textsum) that directly applies the Encoder-Decoder model used for machine translation to generating summaries of short sentences for the Gigaword dataset. They claim better than state-of-the-art results for the model, although no formal write-up of the results is presented beyond a text document provided with the code.
    > 
    > In their paper, Abigail See, et al. describe two main shortcomings of the deep learning approaches to abstractive text summarization: they produce factual errors and they repeat themselves.
    > 
    > > Though these systems are promising, they exhibit undesirable behavior such as inaccurately reproducing factual details, an inability to deal with out-of-vocabulary (OOV) words, and repeating themselves
    > 
    > Their approach is designed for summarizing multiple sentences rather than single-sentence summarization and is applied to the CNN/Daily Mail dataset used to demonstrate the IBM model. Articles in this dataset are comprised of approximately 39 sentences on average.
    > 
    > A baseline Encoder-Decoder model is used with a word embedding, bidirectional LSTMs for input, and attention. An extension is explored that uses pointing to words in the input data to address out of vocabulary words, similar to the approach used in the IBM model. Finally, a coverage mechanism is used to help reduce repetition in the output.
    > 
    > ![Pointer-generator model for Text Summarization](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2017/09/Pointer-generator-model-for-Text-Summarization.png)
    > 
    > Pointer-generator model for Text Summarization\
    > Taken from "Get To The Point: Summarization with Pointer-Generator Networks."
    > 
    > Results are reported using ROUGE and METEOR scores, showing state-of-the-art performance compared to other abstractive methods and scores that challenge extractive models.
    > 
    > > Our pointer-generator model with coverage improves the ROUGE and METEOR scores further, convincingly surpassing the best [compared] abstractive model ...
    > 
    > Results do show that the baseline seq-to-seq model (Encoder-Decoder with attention) can be used but does not produce competitive results, showing the benefit of their extensions to the approach.
    > 
    > > We find that both our baseline models perform poorly with respect to ROUGE and METEOR, and in fact the larger vocabulary size (150k) does not seem to help. ... Factual details are frequently reproduced incorrectly, often replacing an uncommon (but in-vocabulary) word with a more common alternative.
    > 
    > Further Reading
    > ---------------
    > 
    > This section provides more resources on the topic if you are looking go deeper.
    > 
    > -   [A Neural Attention Model for Abstractive Sentence Summarization](https://arxiv.org/abs/1509.00685) ([see code](https://github.com/facebook/NAMAS)), 2015.
    > -   [Abstractive Text Summarization Using Sequence-to-Sequence RNNs and Beyond](https://arxiv.org/abs/1602.06023), 2016.
    > -   [Get To The Point: Summarization with Pointer-Generator Networks](https://arxiv.org/abs/1704.04368) ([see code](https://github.com/abisee/pointer-generator)), 2017.
    > -   [Text summarization with TensorFlow](https://research.googleblog.com/2016/08/text-summarization-with-tensorflow.html) ([see code](https://github.com/tensorflow/models/tree/master/textsum)), 2016
    > -   [Taming Recurrent Neural Networks for Better Summarization](http://www.abigailsee.com/2017/04/16/taming-rnns-for-better-summarization.html), 2017.


## Extractive Text Summarization Using Neural Networks

- [Extractive Text Summarization Using Neural Networks](https://heartbeat.fritz.ai/extractive-text-summarization-using-neural-networks-5845804c7701)

    > We divide the document into segments, each having a fixed number of sentences --- let's call these segments "pages" and the fixed number of sentences "length". For each run of the network, we feed it with a single "page" and get a summary of that page. After the last run we concatenate all the summaries. For pages that have less sentences than the "length", the vector can be padded with zeroes. Another advantage of this approach is that we can test the model with different "length" and see which gives the best results.
    > 
    > This proposed model can prove to be extremely useful for generating extractive summaries as shown before, and this would run on devices with limited computational power like mobile phones.
    > 
    > ![](https://cdn-images-1.medium.com/max/1600/0*MQZkr5W0U6DOJqOr.)
    > 
    > Flow Diagram of the model
    > 
    > #### Training and Evaluation
    > 
    > For training this model, [DUC](https://duc.nist.gov/) (Document Understanding Conferences) datasets can be used. These datasets include document-summary pairs, with each document having two summaries (both extractive). The only pre-processing required would be to convert them to text documents as they are provided as XML pages.
    > 
    > The best way to evaluate this model would be to use ROUGE. It stands for Recall-Oriented Understudy for Gisting Evaluation. To evaluate the neural network, ROUGE compares the summaries generated by the network to human generated summaries. This is the reason why it's extensively used for evaluating automatic summaries and sometimes also for machine translations.
    > 
    > ---
    > 
    > #### What can be improved?
    > 
    > The model proposed here is a very accurate and efficient way to generate summaries, but as always, it isn't perfect. The major issue is that it uses the extractive text summarization technique. The problem with this technique is that it uses the exact same sentences as in the original document, and sometimes this may lead to a summary containing less important information because a part of a sentence may contain useful information, but the rest of it may be useless. Another issue is the use of pronouns in the original document. When a certain sentence in the document containing a pronoun is included in the summary, it may be ambiguous to what the pronoun is referring to.
    > 
    > To solve these problems, we would have to shift to abstractive text summarization, but training a neural network for abstractive text summarization requires a lot of computational power and almost 5x more time, and it can not be used on mobile devices efficiently due to limited processing power, which makes it less useful.
    > 
    > Currently, extractive text summarization functions very well, but with the rapid growth in the demand of text summarizers, we'll soon need a way to obtain abstractive summaries using less computational resources.
    > 
    > Refer to these for information on abstractive text summarization --- <https://arxiv.org/abs/1602.06023>
    > 
    > <https://arxiv.org/abs/1509.00685>
    > 
    > Some common models used till now for text summarization can be found [here.](https://github.com/chen0040/keras-text-summarization)



## [1509.00685] A Neural Attention Model for Abstractive Sentence Summarization

- [[1509.00685] A Neural Attention Model for Abstractive Sentence Summarization](https://arxiv.org/abs/1509.00685)


- [论文笔记 - A Neural Attention Model for Abstractive Sentence Summarization | 徐阿衡](http://www.shuang0420.com/2017/08/08/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/)

    > Background
    > ==========
    > 
    > Summarization Phenomena
    > -----------------------
    > 
    > 先来观察下文本摘要的一些现象，一般是通过对源文本进行 **泛化(generalization)、删除(deletion)、改写(paraphrase)** 等操作来产生目标文本，也就是文本摘要。看一下例子
    > 
    > -   **Generalization**\
    >     **Source:** **Russian Defense Minister Ivanov** called Sunday for the creation of a joint front for combating global terrorism.\
    >     **Target:** **Russia** calls for joint front against terrorism.
    > -   **Deletion**\
    >     **Source:** Russian Defense Minister Ivanov called **Sunday** for the creation of a joint front for combating global terrorism.\
    >     **Target:** Russia calls for joint front against terrorism.
    > -   **Paraphrase**\
    >     **Source:** Russian Defense Minister Ivanov called Sunday for the creation of a joint front **for combating** global terrorism.\
    >     **Target:** Russia calls for joint front **against** terrorism.
    > 
    > Types of Sentence Summary
    > -------------------------
    > 
    > 对于上面等一些操作，产生了文本摘要的几类技术模型。
    > 
    > -   **Compressive: deletion-only:**\
    >     压缩，通过对源文本的删除操作产生目标文本。
    > -   **Extractive: deletion and reordering:**\
    >     抽取式，摘要句子完全从源文档中抽取形成，详细见 [NLP 笔记 - Text Summarization](http://www.shuang0420.com/2017/05/10/NLP%20%E7%AC%94%E8%AE%B0%20-%20Text%20Summarization/)
    > -   **Abstractive: arbitary transformation**\
    >     合成式，从源文档中抽取句子并进行改写形成摘要。
    > 
    > 看下几种方法的比较\
    > [![elements.png](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/elements.png)](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/elements.png)
    > 
    > Related work
    > ------------
    > 
    > 目前已经有的一些相关工作
    > 
    > -   **Syntax-Based**\
    >     Dorr, Zajic, and Schwartz 2003; Cohn and Lapata 2008; Woodsend, Fend, and Lapata 2010
    > -   **Topic-Based**\
    >     Zajic, Dorr, and Schwartz 2004
    > -   **Machine Translation-based**\
    >     Banko, Mittal, and Witbrock 2000
    > -   **Semantics-Based**\
    >     Liu et al 2015
    > 
    > Textsum
    > =======
    > 
    > Textsum，论文戳 [A Neural Attention Model for Abstractive Sentence Summarization](https://arxiv.org/pdf/1509.00685.pdf)，tensorflow 代码戳 [tensorflow/models/textsum](https://github.com/tensorflow/models/tree/master/textsum)。Textsum是一种 abstractive model，主要有下面四个组件构成：
    > 
    > -   Neural language model
    > -   Attention-based encoder model
    > -   Generation model
    > -   Beam-search decoder & additional features model extractive elements
    > 
    > 下面逐个进行讨论。
    > 
    > Neural language model
    > ---------------------
    > 
    > 借鉴了机器翻译的思想，在 [A Neural Probabilistic Language Model](http://www.jmlr.org/papers/volume3/bengio03a/bengio03a.pdf) (Bengio et al. 2013)的基础上，加了一个 attention-based encoder(Bahdanau et al. 2014) 来学习输入文本的 latent soft alignment。
    > 
    > 先看一下整体逻辑，看图说话，下面左图圈出来的部分是一个**feed-forward neural network language model(NNLM)**，详情戳[NLP 笔记 - Machine Translation(Neuron models)](http://www.shuang0420.com/2017/07/10/NLP%20笔记%20-%20Machine%20Translation-Neuron%20models/)，它的输入是当前 output 已经产生的上下文 yc
    > 
    > (注意这个 context 窗口的长度是固定的)，与词向量矩阵 E 做个映射，经过线性变化以及激活函数得到得分矩阵 U，再经过一个 softmax 层得到概率分布形式的输出，也就是下一个单词 yi+1，现在我们要加上左边的 attention-based encoder，对输入 source text 和当前我们拥有的 context yc
    > 
    > 做一个 encode，放大的话就是右图。对 context embedding 和 source 的每个单词做一个加权的点乘(weighted dot product)得到 attention distribution 也就是 P，对 source text 做一个局部的平滑(local smoothing)，然后对 source 的 smoothing 版本和 attention distribution 做一个点乘，就得到了我们要的 enc，最后把两边的东西一起扔到 softmax 里得到输出。
    > 
    > [![abs_graph.png](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/abs_graph.png)](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/abs_graph.png)
    > 
    > 看个例子，如下图，行是 source text，列是 output text，假定我们已经产生了 "russia calls"，现在目标是产生下一个单词 for，我们的模型将利用 attention distribution of source 以及 embedding of context，来得到 for 这个 next word。因为我们用了 bag of words 的 smoothing 版本，也就是说我们对 called 周围的单词进行了加权，attention 很大程度上会指向 called，具体逻辑见下一部分 encoders。\
    > [![abs_ex1.png](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/abs_ex1.png)](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/abs_ex1.png)
    > 
    > 上面说到了，这里选择的 encoder 是 attention-based encoder，下面来看一下为什么选这个 encoder。
    > 
    > Encoders
    > --------
    > 
    > Bag-of-words Encoder
    > --------------------
    > 
    > BoW encoder 把 encoder 参数估计看作是一个 uniform distribution，赋予了每个词相同的权重，同时忽略了单词词序。
    > 
    > [![bow_encoder.png](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/bow_encoder.png)](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/bow_encoder.png)
    > 
    > ### Convolutional Encoder
    > 
    > Convolutional Encoder 通过局部卷积来考虑邻近单词的互动，单词/词组权重由网络训练产生。\
    > [![conv%20model2.png](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/conv%20model2.png)](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/conv%20model2.png)\
    > [![conv%20model.png](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/conv%20model.png)](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/conv%20model.png)
    > 
    > ### Attention-Based Encoder
    > 
    > 灵感来自 **Bahdanau et al. (2014) attention-based contextual encoder**。和 BoW 相似的一个简单的模型，只不过把 BoW 的 uniform distribution 替换成一个 input 和 summary 之间的 soft alignment P (如下图)，是一个机器翻译的思路。之后用学习到的这个 soft alignment 来给输入的平滑版本进行加权。比如说，如果当前的上下文和位置 i 能很好的对齐，那么单词 xi-Q,...,xi+Q
    > 
    > 就会被 encoder 赋予更高的权重。与 NNLM 结合的话这个模型可以看作是 attention-based neural machine translation model 的精简版。
    > 
    > G∈RD∗V
    > 
    > : embdding of the context\
    > P∈RH∗(CD): new weight matrix parameter mapping between the context embedding and input embedding\
    > Q
    > 
    > : smoothing window
    > 
    > [![abs_ex1.png](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/abs_ex1.png)](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/abs_ex1.png) [![attention_decoder.png](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/attention_decoder.png)](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/attention_decoder.png)
    > 
    > Generating Summaries
    > --------------------
    > 
    > 用 beam-search decoder 来寻找最好的 summary，这是机器翻译模型的标准化方法(Bahdanau et al., 2014; Sutskever et al., 2014; Luong et al., 2015) ，这里做了一点改进。
    > 
    > [![beam%20search.png](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/beam%20search.png)](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/beam%20search.png)
    > 
    > 算法如上，我们需要维护一个词库 V 以及前 k 个最好的 context，复杂度是 O(KNV)。
    > 
    > Tuning
    > ------
    > 
    > 最后论文提到了一个 tuning，这其实是在 word embedding 维度太低，语义表示不完全时，去人工添加一些特征，这可以 handle 一些 rare/unseen words 的问题，让系统的 extractive/abstractive 趋势更为平衡。\
    > 通过修改评分函数来直接估计 summary 概率，使用对数线性模型。\
    > [![tuning.png](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/tuning.png)](http://ox5l2b8f4.bkt.clouddn.com/images/%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0%20-%20A%20Neural%20Attention%20Model%20for%20Abstractive%20Sentence%20Summarization/tuning.png)
    > 
    > 

## Abstractive Sentence Summarization with Attentive Recurrent Neural Networks - N16-1012

- [Abstractive Sentence Summarization with Attentive Recurrent Neural Networks - N16-1012](http://www.aclweb.org/anthology/N16-1012)


- [自动文摘（六） | PaperWeekly](https://rsarxiv.github.io/2016/04/30/%E8%87%AA%E5%8A%A8%E6%96%87%E6%91%98%EF%BC%88%E5%85%AD%EF%BC%89/)

    > 本文模型简称为RAS（`Recurrent Attentive Summarizer`）
    > 
    > ### Objective
    > 
    > 目标函数如下：
    > 
    > [![](https://rsarxiv.github.io/2016/04/30/自动文摘（六）/NLL2.png)](https://rsarxiv.github.io/2016/04/30/%E8%87%AA%E5%8A%A8%E6%96%87%E6%91%98%EF%BC%88%E5%85%AD%EF%BC%89/NLL2.png)
    > 
    > 两篇paper都是采用NLL，但不同的是第二篇paper目标函数条件概率中的条件与第一篇不同，本文采用decoder的所有上文，而不是一个窗口内的上文。
    > 
    > ### Encoder
    > 
    > encoder的输出是decoder的输入，对于每一个time step，encoder都需要给出一个context vector，本文encoder的重点在于如何计算时间相关的context。
    > 
    > 输入句子每个词最终的embedding是各词的embedding与各词位置的embedding之和，经过一层卷积处理得到aggregate vector：
    > 
    > [![](https://rsarxiv.github.io/2016/04/30/自动文摘（六）/formula21.png)](https://rsarxiv.github.io/2016/04/30/%E8%87%AA%E5%8A%A8%E6%96%87%E6%91%98%EF%BC%88%E5%85%AD%EF%BC%89/formula21.png)
    > 
    > 根据`aggregate vector`计算context（encoder的输出）：
    > 
    > [![](https://rsarxiv.github.io/2016/04/30/自动文摘（六）/formula22.png)](https://rsarxiv.github.io/2016/04/30/%E8%87%AA%E5%8A%A8%E6%96%87%E6%91%98%EF%BC%88%E5%85%AD%EF%BC%89/formula22.png)
    > 
    > 其中权重由下式计算：
    > 
    > [![](https://rsarxiv.github.io/2016/04/30/自动文摘（六）/formula23.png)](https://rsarxiv.github.io/2016/04/30/%E8%87%AA%E5%8A%A8%E6%96%87%E6%91%98%EF%BC%88%E5%85%AD%EF%BC%89/formula23.png)
    > 
    > `Rush组的paper有一个特点，喜欢用CNN多一些，包括那位用CNN做句子分类的童鞋。可能的原因是，Rush是Facebook AI Research的研究人员，Lecun是Leader，所以他们对CNN的理解也更深一些，在model中使用的也就更多一些。`
    > 
    > ### Decoder
    > 
    > decoder的部分是一个RNNLM，这里的RNN Hidden Layer使用的是LSTM单元。decoder的输出由下式计算：
    > 
    > [![](https://rsarxiv.github.io/2016/04/30/自动文摘（六）/formula24.png)](https://rsarxiv.github.io/2016/04/30/%E8%87%AA%E5%8A%A8%E6%96%87%E6%91%98%EF%BC%88%E5%85%AD%EF%BC%89/formula24.png)
    > 
    > 其中c(t)是encoder的输出，h(t)是RNN隐藏层，由下式计算：
    > 
    > [![](https://rsarxiv.github.io/2016/04/30/自动文摘（六）/formula25.png)](https://rsarxiv.github.io/2016/04/30/%E8%87%AA%E5%8A%A8%E6%96%87%E6%91%98%EF%BC%88%E5%85%AD%EF%BC%89/formula25.png)
    > 
    > 这里隐藏层的单元有两种思路，一种是常规的Elman RNN，一种是LSTM。
    > 
    > `RNNLM的Hidden Unit可以不用LSTM或者GRU这么复杂，普通的隐藏层Elman RNN可以解决问题，采用Truncate-BPTT对RNN进行训练（详见Tomas Mikolov的PhD Thesis）。况且LSTM和GRU会带来更多的参数，造成overfit。`
    > 
    > ### Generation
    > 
    > 生成过程中也采用`beam search`算法进行summary生成。
    > 
    > ### Training
    > 
    > 给定一个训练集，包括大量的sentence-summary pairs，用SGD将NLL函数最小化得到最优的参数集，参数包含encoder和decoder两个部分的参数。
    > 
    > `SGD是一种常用的优化算法，在解决NLP问题中非常有效，其中最常见的mini batch训练方法。`



## [1602.06023] Abstractive Text Summarization Using Sequence-to-Sequence RNNs and Beyond

- [[1602.06023] Abstractive Text Summarization Using Sequence-to-Sequence RNNs and Beyond](https://arxiv.org/abs/1602.06023)


