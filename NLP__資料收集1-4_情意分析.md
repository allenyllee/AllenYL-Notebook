# NLP__資料收集1-4_情意分析

[toc]
<!-- toc --> 


# 情意分析

## CNN-SVM 諷刺偵測

- [[1610.08815] A Deeper Look into Sarcastic Tweets Using Deep Convolutional Neural Networks](https://arxiv.org/abs/1610.08815)

- [Detecting Sarcasm with Deep Convolutional Neural Networks](https://www.kdnuggets.com/2018/06/detecting-sarcasm-deep-convolutional-neural-networks.html#.Wyu7yLVD5OQ.linkedin)

    - [Detecting Sarcasm with Deep Convolutional Neural Networks](https://medium.com/dair-ai/detecting-sarcasm-with-deep-convolutional-neural-networks-4a0657f79e80)

    > ![](https://cdn-images-1.medium.com/max/1200/0*GVbW_tOQMN1F1lcw.)
    > 
    > To obtain the other features — sentiment (S), emotion (E), and personality (P) — CNN models are pre-trained and used to extract features from the sarcasm datasets. Different training datasets were used to train each model. (Refer to paper for more details)


## Differences between Polarity and Topic-based Sentiment Analysis

- [Differences between Polarity and Topic-based Sentiment Analysis](https://blog.bitext.com/polarity-topic-sentiment-analysis)


    > From a business perspective, there is huge difference between plain polarity and topic-based sentiment analysis (also known as aspect-based sentiment analysis)
    > 
    > ##### Why is polarity analysis by itself not enough?
    > 
    > Polarity analysis takes into account the amount of positive or negative terms that appear in a given sentence. It is useful to some extent, since it does a good job of structuring data sets.
    > 
    > Let say I have 1000 reviews on my product that I want to analyze. By using polarity I can identify that 30% are negative, 20% are neutral and 50% are positive -- and that's good for segmentation. But I am left with three chunks of 300, 200 and 500 reviews to go through if I want to get more meaningful insights, rather than just a nice looking pie chart.
    > 
    > And imagine if we have 10 times that data, and in multiple languages! Then we are dealing with some really expensive (and not very delighted) employees that have to spend all day reading through reviews.
    > 
    > Let's have a look at how comments are treated when using polarity analysis by itself.
    > 
    > "The weather is amazing, and I love my XYZ phone."\
    > Clearly positive as we have expressions like *amazing* and love
    > 
    > "The weather is gloomy and sad, and I hate my XYZ phone."\
    > Clearly negative as *gloomy*, sad and hate are objectively negative expressions
    > 
    > "The weather is gloomy and sad, and I love my XYZ phone."\
    > Neutral. Some expressions are good others bad.\
    > As we add them all together we end up with something in between.
    > 
    > It is here, with the neutral cases, that the limitations of a polarity-based approach become clear.
    > 
    > And this is where topic-based sentiment analysis really shines, and why it is becoming a standard in the Text Analytics Industry.
    > 
    > Going back to our example about the weather and the phone, when we can identify exactly what the opinion is about, then the true expressed opinion is not lost in a misleading overall score. And what is even more useful is that XYZ company can filter out the already analyzed data to zoom in on the opinions specifically about their phones. The rest of the noise like comments about the weather, are filtered out.
    > 
    > ##### How does topic-based sentiment analysis work?
    > 
    > To be able to match expressions that bear sentiment with their relevant topic, we need to rely on linguistic knowledge. The industry counts on many methods to do this, such as POS tagging and parsing, and other techniques like n-grams and neural networks models.
    > 
    > Linguistics uncovers the structure of the sentence (known as phrase structure). This is what makes the difference in topic-based analysis. Knowledge of parts of speech and grammar are used to detect the sentiment topic that the expressed opinion is related to:
    > 
    > -   I like this camera (with "like" the topic normally is the direct object)
    > -   This lens is great (with "be" the topic normally is the subject)
    > 
    > ##### Well this is all very interesting, but does it really produce measurable results?
    > 
    > You'd be surprised.
    > 
    > In academic conferences on topic-based sentiment analysis ([SemEval](https://en.wikipedia.org/wiki/SemEval), for example), sentiment analysis platforms are tested against human hand tagging and precision, recall, and F-score performed by contestants.
    > 
    > It's quite amazing to see how sentiment analysis platforms measure up against humans!


## What is the difference between Polarity and Subjectivity

- [What is the difference between Polarity and Subjectivity? - Quora](https://www.quora.com/What-is-the-difference-between-Polarity-and-Subjectivity)

    > In the realm of Sentiment analysis, the main goal would be to classify the **polarity** of a given text at different levels ---whether the expressed opinion in a document, a sentence or an entity feature/aspect is **positive**, **negative**, or **neutral**.
    > 
    > For achieving this goal (polarity classification), you can see the whole process as a pipeline including different stages that can contribute to the accuracy of ending results. **Subjectivity/objectivity identification** can be seen as one of those stages that is commonly defined as classifying a given text (usually a sentence) into one of two classes: **objective** or **subjective**. For example, some researches showed that removing objective sentences from a document before classifying its polarity helped improve performance.
    > 
    > Note that there are unique challenges for subjectivity detection: The **subjectivity** of words and phrases may depend on their context and an objective document may contain subjective sentences (e.g., a news article quoting people's opinions).
    > 
    > ---
    > 
    > **Polarity**
    > 
    > It simply means emotions expressed in a sentence.
    > 
    > Emotions are closely related to sentiments. The strength of a sentiment or opinion is typically linked to the intensity of certain emotions, e.g., joy and anger.
    > 
    > Opinions in sentiment analysis are mostly evaluations(although not always).
    > 
    > According to consumer behavior research, evaluations can be broadly categorized into two types:\
    > **1\. Rational evaluations\
    > 2\. Emotional evaluations**.
    > 
    > **Rational evaluation**: Such evaluations are from rational reasoning, tangible
    > 
    > beliefs, and utilitarian attitudes. For example, the following sentences
    > 
    > **Express rational evaluations:** "The voice of this phone is clear," "This car is worth the price," and "I am happy with this car."
    > 
    > **Emotional evaluation:** Such evaluations are from non-tangible and emotional responses to entities which go deep into people's state of mind.
    > 
    > For example, the following sentences express emotional evaluations: "I love iPhone," "I am so angry with their service people" and "This is the best car ever built."
    > 
    > To make use of these two types of evaluations in practice, we can design 5 sentiment ratings, emotional negative (-2), rational negative (-1), neutral (0), rational positive (+1), and emotional positive (+2). In practice, neutral often means no opinion or sentiment expressed.
    > 
    > **Subjectivity**
    > 
    > Subjective sentence expresses some personal feelings, views, or beliefs.
    > 
    > **An example**
    > 
    > subjective sentence is "I like iPhone." Subjective expressions come in many forms, e.g., opinions, allegations, desires, beliefs, suspicions, and speculations.
    > 
    > A subjective sentence may not express any sentiment.\
    > **For example**, "I think that he went home" and "I want a camera that can take good photos" are a subjective sentences, but does not express any sentiment.
    > 
    > **(Source: Bing Liu. Sentiment Analysis and Opinion Mining, Morgan & Claypool Publishers, May 2012)**
    > 
    > ---
    > 
    > Abtin has already captured it in his response.
    > 
    > -   A sentence could be stating a fact( *objective*) or expressing an opinion( *subjective*). Determining this is a classification of a sentence as being objective or subjective
    > -   For sentences tagged as subjective in the classification step above, one could further classify those sentences as expressing a positive or negative sentiment - weeding out objective statements may help improve the performance of sentiment classification into positive and negative sentiment.
    > -   So in essence given a sentence - one could first use a classifier to label a sentence as subjective or objective and then do another classification to further classify subjective sentences as either positive or negative.
    > 
    > **Reference**
    > 
    > [Sentiment analysis and subjectivity](https://www.cs.uic.edu/~liub/FBS/NLP-handbook-sentiment-analysis.pdf)


## 利用AllenNLP，百行Python代码训练情感分类器


- [利用AllenNLP，百行Python代码训练情感分类器](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650750932&idx=3&sn=30b8412c4d612f52ae5f0c42ae001b07&chksm=871afbaab06d72bc110e2c73eb70b56d5b56acf98faa4bd5f94f5c8cfc91c4e894e5b9c16597&mpshare=1&scene=24&srcid=#rd)

    > 情感分析是一种流行的文本分析技术，用来对文本中的主观信息进行自动识别和分类。它被广泛用于量化观点、情感等通常以非结构化方式记录的信息，而这些信息也因此很难用其他方式量化。情感分析技术可被用于多种文本资源，例如调查报告、评论、社交媒体上的帖子等。
    > 
    > 情感分析最基本的任务之一是极性分类，换句话说，该任务需要判断语言所表达的观点是正面的、负面的还是中性的。具体而言，可能有三个以上的类别，例如：极其正面、正面、中性、消极、极其消极。这有些类似于你使用某些网站时的评价行为（比如 Amazon），人们可以用星星数表示 5 个等级来对物品进行评论（产品、电影或其他任何东西）。
    > 
    > **斯坦福的情感分析树库（TreeBank）**
    > 
    > 目前，研究人员发布了一些公开的情感分类数据集。在本文中，我们将使用斯坦福的情感分析树库（或称 SST），这可能是最广为使用的情感分析数据集之一。SST 与其它数据集最大的不同之处是，在 SST 中情感标签不仅被分配到句子上，句子中的每个短语和单词也会带有情感标签。这使我们能够研究单词和短语之间复杂的语义交互。例如，对下面这个句子的极性进行分析：
    > 
    > > This movie was actually neither that funny, nor super witty.
    > 
    > 这个句子肯定是消极的。但如果只看单个单词（「funny」、「witty」）可能会被误导，认为它的情感是积极的。只关注单个单词的朴素词袋分类器很难对上面的例句进行正确的分类。要想正确地对上述例句的极性进行分类，你需要理解否定词（neither ... nor ...）对语义的影响。由于 SST 具备这样的特性，它被用作获取句子句法结构的神经网络模型的标准对比基准（https://nlp.stanford.edu/~socherr/EMNLP2013_RNTN.pdf）。
    > 
    > **Pytorch 和 AllenNLP**
    > 
    > PyTorch 是我最喜欢的深度学习框架。它提供了灵活、易于编写的模块，可动态运行，且速度相当快。在过去一年中，PyTorch 在科研社区中的使用实现了[爆炸性增长](http://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650749471&idx=1&sn=3b4dfc47cbb81af816b980c1a5f21abb&chksm=871afe61b06d77774acaf05a4b5b7d70735855363263394b3873d40a7628cf3c7d7ba7bc0e2b&scene=21#wechat_redirect)。
    > 
    > 尽管 PyTorch 是一个非常强大的框架，但是自然语言处理往往涉及底层的公式化的事务处理，包括但不限于：阅读和编写数据集、分词、建立单词索引、词汇管理、mini-batch 批处理、排序和填充等。尽管在 NLP 任务中正确地使用这些构建块是至关重要的，但是当你快速迭代时，你需要一次又一次地编写类似的设计模式，这会浪费很多时间。而这正是 AllenNLP 这类库的亮点所在。
    > 
    > AllenNLP 是艾伦人工智能研究院开发的开源 NLP 平台。它的设计初衷是为 NLP 研究和开发（尤其是语义和语言理解任务）的快速迭代提供支持。它提供了灵活的 API、对 NLP 很实用的抽象，以及模块化的实验框架，从而加速 NLP 的研究进展。
    > 
    > 本文将向大家介绍如何使用 AllenNLP 一步一步构建自己的情感分类器。由于 AllenNLP 会在后台处理好底层事务，提供训练框架，所以整个脚本只有不到 100 行 Python 代码，你可以很容易地使用其它神经网络架构进行实验。
    > 
    > 代码地址：https://github.com/mhagiwara/realworldnlp/blob/master/examples/sentiment/sst_classifier.py
    > 
    > 接下来，下载 SST 数据集，你需要将数据集分割成 PTB 树格式的训练集、开发集和测试集，你可以通过下面的链接直接下载：https://nlp.stanford.edu/sentiment/trainDevTestTrees_PTB.zip。我们假设这些文件是在 data/stanfordSentimentTreebank/trees 下进行扩展的。
    > 
    > 注意，在下文的代码片段中，我们假设你已经导入了合适的模块、类和方法（详情参见完整脚本）。你会注意到这个脚本和 AllenNLP 的词性标注教程非常相似------在 AllenNLP 中很容易在只进行少量修改的情况下使用不同的模型对不同的任务进行实验。
    > 
    > **数据集读取和预处理**
    > 
    > AllenNLP 已经提供了一个名为 StanfordSentimentTreeBankDatasetReader 的便捷数据集读取器，它是一个读取 SST 数据集的接口。你可以通过将数据集文件的路径指定为为 read() 方法的参数来读取数据集：
    > 
    > ```pyhton
    > reader = StanfordSentimentTreeBankDatasetReader()train_dataset = reader.read('data/stanfordSentimentTreebank/trees/train.txt')dev_dataset = reader.read('data/stanfordSentimentTreebank/trees/dev.txt')
    > ```
    > 
    > 几乎任何基于深度学习的 NLP 模型的第一步都是指定如何将文本数据转换为张量。该工作包括把单词和标签（在本例中指的是「积极」和「消极」这样的极性标签）转换为整型 ID。在 AllenNLP 中，该工作是由 Vocabulary 类来处理的，它存储从单词/标签到 ID 的映射。
    > 
    > ```python
    > # You can optionally specify the minimum count of tokens/labels.# `min_count={'tokens':3}` here means that any tokens that appear less than three times# will be ignored and not included in the vocabulary.vocab = Vocabulary.from_instances(train_dataset + dev_dataset,                                  min_count={'tokens': 3})
    > ```
    > 
    > 下一步是将单词转换为嵌入。在深度学习中，嵌入是离散、高维数据的连续向量表征。你可以使用 Embedding 创建这样的映射，使用 BasicTextFieldEmbedder 将 ID 转换为嵌入向量。
    > 
    > ```python
    > token_embedding = Embedding(num_embeddings=vocab.get_vocab_size('tokens'),                            embedding_dim=EMBEDDING_DIM)# BasicTextFieldEmbedder takes a dict - we need an embedding just for tokens,# not for labels, which are used unchanged as the answer of the sentence classificationword_embeddings = BasicTextFieldEmbedder({"tokens": token_embedding})
    > ```
    > 
    > **句子分类模型**
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW91whyE5rpeuqBlV8Fd0IzottMhoP0e15x1bok9pQNvzcMGIMYGFgF0icNpMBGzKeC1iacClfd7YFJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
    > 
    > *LSTM-RNN 句子分类模型*
    > 
    > 现在，我们来定义一个句子分类模型。这段代码看起来很多，但是别担心，我在代码片段中添加了大量注释：
    > 
    > ```python
    > # Model in AllenNLP represents a model that is trained.class LstmClassifier(Model):    def __init__(self,                 word_embeddings: TextFieldEmbedder,                 encoder: Seq2VecEncoder,                 vocab: Vocabulary) -> None:        super().__init__(vocab)        # We need the embeddings to convert word IDs to their vector representations        self.word_embeddings = word_embeddings        # Seq2VecEncoder is a neural network abstraction that takes a sequence of something        # (usually a sequence of embedded word vectors), processes it, and returns it as a single        # vector. Oftentimes, this is an RNN-based architecture (e.g., LSTM or GRU), but        # AllenNLP also supports CNNs and other simple architectures (for example,        # just averaging over the input vectors).        self.encoder = encoder        # After converting a sequence of vectors to a single vector, we feed it into        # a fully-connected linear layer to reduce the dimension to the total number of labels.        self.hidden2tag = torch.nn.Linear(in_features=encoder.get_output_dim(),                                          out_features=vocab.get_vocab_size('labels'))        self.accuracy = CategoricalAccuracy()        # We use the cross-entropy loss because this is a classification task.        # Note that PyTorch's CrossEntropyLoss combines softmax and log likelihood loss,        # which makes it unnecessary to add a separate softmax layer.        self.loss_function = torch.nn.CrossEntropyLoss()    # Instances are fed to forward after batching.    # Fields are passed through arguments with the same name.    def forward(self,                tokens: Dict[str, torch.Tensor],                label: torch.Tensor = None) -> torch.Tensor:        # In deep NLP, when sequences of tensors in different lengths are batched together,        # shorter sequences get padded with zeros to make them of equal length.        # Masking is the process to ignore extra zeros added by padding        mask = get_text_field_mask(tokens)        # Forward pass        embeddings = self.word_embeddings(tokens)        encoder_out = self.encoder(embeddings, mask)        logits = self.hidden2tag(encoder_out)        # In AllenNLP, the output of forward() is a dictionary.        # Your output dictionary must contain a "loss" key for your model to be trained.        output = {"logits": logits}        if label is not None:            self.accuracy(logits, label)            output["loss"] = self.loss_function(logits, label)        return output
    > ```
    > 
    > 这里的关键是 Seq2VecEncoder，它基本上使用张量序列作为输入，然后返回一个向量。我们在这里使用 LSTM-RNN 作为编码器（如有需要，可参阅文档 https://allenai.github.io/allennlp-docs/api/allennlp.modules.seq2vec_encoders.html#allennlp.modules.seq2vec_encoders.pytorch_seq2vec_wrapper.PytorchSeq2VecWrapper）。
    > 
    > ```python
    > lstm = PytorchSeq2VecWrapper(    torch.nn.LSTM(EMBEDDING_DIM, HIDDEN_DIM, batch_first=True))model = LstmClassifier(word_embeddings, lstm, vocab)
    > ```
    > 
    > **训练**
    > 
    > 一旦你定义了这个模型，其余的训练过程就很容易了。这就是像 AllenNLP 这样的高级框架的亮点所在。你只需要指定如何进行数据迭代并将必要的参数传递给训练器，而无需像 PyTorch 和 TensorFlow 那样编写冗长的批处理和训练循环。
    > 
    > ```python
    > optimizer = optim.Adam(model.parameters(), lr=1e-4, weight_decay=1e-5)iterator = BucketIterator(batch_size=32, sorting_keys=[("tokens", "num_tokens")])iterator.index_with(vocab)trainer = Trainer(model=model,                  optimizer=optimizer,                  iterator=iterator,                  train_dataset=train_dataset,                  validation_dataset=dev_dataset,                  patience=10,                  num_epochs=20)trainer.train()
    > ```
    > 
    > 这里的 BucketIterator 会根据 token 的数量对训练实例进行排序，从而使得长度类似的实例在同一个批中。注意，我们使用了验证集，在测试误差过大时采用了早停法避免过拟合。
    > 
    > 如果将上面的代码运行 20 个 epoch，则模型在训练集上的准确率约为 0.78，在验证集上的准确率约为 0.35。这听起来很低，但是请注意，这是一个 5 类的分类问题，随机基线的准确率只有 0.20。
    > 
    > **测试**
    > 
    > 为了测试刚刚训练的模型是否如预期，你需要构建一个预测器（predictor）。predictor 是一个提供基于 JSON 的接口的类，它被用于将输入数据传递给你的模型或将输出数据从模型中导出。接着，我便写了一个句子分类预测器（https://github.com/mhagiwara/realworldnlp/blob/master/realworldnlp/predictors.py#L10），将其用作句子分类模型的基于 JSON 的接口。
    > 
    > ```python
    > tokens = ['This', 'is', 'the', 'best', 'movie', 'ever', '!']predictor = SentenceClassifierPredictor(model, dataset_reader=reader)logits = predictor.predict(tokens)['logits']label_id = np.argmax(logits)print(model.vocab.get_token_from_index(label_id, 'labels'))
    > ```
    > 
    > 运行这段代码后，你应该看到分类结果为「4」。「4」对应的是「非常积极」。所以你刚刚训练的模型正确地预测出了这是一个非常正面的电影评论。

