# NLP__資料收集

[toc]
<!-- toc --> 


## 實作中文 auto tagging 流程

1. 訓練中文word2vec: 
https://zake7749.github.io/2016/08/28/word2vec-with-gensim/
   a. 搜集大量中文語料(wiki, ptt, 新聞...)
   b. gensim 做格式處理、opencc做簡繁轉換
   c. jieba 做斷詞，調整辭典對繁體的支援，加入停用詞(你我他的之....)
   d. gensim中的word2vec 做訓練產生model
   e. 載入model 並做相似詞排序的檢查
2. 訓練seq2seq:
   a. 由word2vec model 建立word2id, id2word 字典對照表
   b. jieba 將training set 文章斷詞，並與target tag 一起轉成id，作為model的input, target
   c. 訓練model
3. 產生tag:
   a. jieba 將testing set 文章斷詞並轉成id 送入seq2seq model
   b. model產生出來的序列轉成word即為tag

## 網頁介面前端範例

- [zkwi/textSummary: 文本智能摘要提取](https://github.com/zkwi/textSummary)

## 中文字

- [認識中文字元碼](http://idv.sinica.edu.tw/bear/charcodes/Section05.htm)

## 斷詞工具

- [Colearo/HuhuSeg: Simple Chinese segmentator, keywords extractor and other examples](https://github.com/Colearo/HuhuSeg)

    > 在TF-IDF实现的关键词提取之外，这里还实现了基于TextRank[5]的提取算法，不依赖于庞大的IDF模型，而是试图在文本中词语的共现关系图里找到被Rank最高的词语。当然，除此之外，这里的代码实现的关键词提取还使用了一个小trick，在通过TextRank提取完关键词之后，会再次扫描文本，找到top关键词中是否有邻接词可以组成短语


## gensim


Parameters:	

- __sg (int {1, 0})__ – Defines the training algorithm. If 1, skip-gram is employed; otherwise, CBOW is used.
- __size (int)__ – Dimensionality of the feature vectors.
- __window (int)__ – The maximum distance between the current and predicted word within a sentence.
- __alpha (float)__ – The initial learning rate.
- __min_alpha (float)__ – Learning rate will linearly drop to min_alpha as training progresses.
- __seed (int)__ – Seed for the random number generator. Initial vectors for each word are seeded with a hash of the concatenation of word + str(seed). Note that for a fully deterministically-reproducible run, you must also limit the model to a single worker thread (workers=1), to eliminate ordering jitter from OS thread scheduling. (In Python 3, reproducibility between interpreter launches also requires use of the PYTHONHASHSEED environment variable to control hash randomization).
- __min_count (int)__ – Ignores all words with total frequency lower than this.
- __max_vocab_size (int)__ – Limits the RAM during vocabulary building; if there are more unique words than this, then prune the infrequent ones. Every 10 million word types need about 1GB of RAM. Set to None for no limit.
- __sample (float)__ – The threshold for configuring which higher-frequency words are randomly downsampled, useful range is (0, 1e-5).
- __workers (int)__ – Use these many worker threads to train the model (=faster training with multicore machines).
- __hs (int {1,0})__ – If 1, hierarchical softmax will be used for model training. If set to 0, and negative is non-zero, negative sampling will be used.
- __negative (int)__ – If > 0, negative sampling will be used, the int for negative specifies how many “noise words” should be drawn (usually between 5-20). If set to 0, no negative sampling is used.
- __cbow_mean (int {1,0})__ – If 0, use the sum of the context word vectors. If 1, use the mean, only applies when cbow is used.
- __hashfxn (function)__ – Hash function to use to randomly initialize weights, for increased training reproducibility.
- __iter (int)__ – Number of iterations (epochs) over the corpus.
- __trim_rule (function)__ – Vocabulary trimming rule, specifies whether certain words should remain in the vocabulary, be trimmed away, or handled using the default (discard if word count < min_count). Can be None (min_count will be used, look to keep_vocab_item()), or a callable that accepts parameters (word, count, min_count) and returns either gensim.utils.RULE_DISCARD, gensim.utils.RULE_KEEP or gensim.utils.RULE_DEFAULT. Note: The rule, if given, is only used to prune vocabulary during build_vocab() and is not stored as part of the model.
- __sorted_vocab (int {1,0})__ – If 1, sort the vocabulary by descending frequency before assigning word indexes.
- __batch_words (int)__ – Target size (in words) for batches of examples passed to worker threads (and thus cython routines).(Larger batches will be passed if individual texts are longer than 10000 words, but the standard cython code truncates to that maximum.)
- __compute_loss (bool)__ – If True, computes and stores loss value which can be retrieved using model.get_latest_training_loss().
- __callbacks__ – List of callbacks that need to be executed/run at specific stages during training.



## char-rnn

- [Tensorflow lyrics generation · Lei's Blog](http://leix.me/2016/11/28/tensorflow-lyrics-generation/)

    - [leido/char-rnn-cn: 基于char-rnn和tensorflow生成周杰伦歌词](https://github.com/leido/char-rnn-cn)

- [從字符級的語言建模開始，瞭解語言模型與序列建模的基本概念 - 幫趣](http://bangqu.com/24EJ36.html)



## 1D-CNN for text

- [Implementing a CNN for Text Classification in TensorFlow – WildML](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow/)

- [dennybritz/cnn-text-classification-tf: Convolutional Neural Network for Text Classification in Tensorflow](https://github.com/dennybritz/cnn-text-classification-tf)

- [[Deep Learning] Convolution Neural Network on NLP](https://unilight.github.io/2017/07/04/Convolution-Neural-Network-on-NLP/)

- [Convolutional Methods for Text – Tal Perry – Medium](https://medium.com/@TalPerry/convolutional-methods-for-text-d5260fd5675f)

- [Understanding Convolutional Neural Networks for NLP – WildML](http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/)

## tf-idf

- [tf–idf - Wikiwand](https://www.wikiwand.com/en/Tf%E2%80%93idf)








## word2Vec

- [以 gensim 訓練中文詞向量 | 雷德麥的藏書閣](https://zake7749.github.io/2016/08/28/word2vec-with-gensim/)

- [zake7749/word2vec-tutorial: 中文詞向量訓練教學](https://github.com/zake7749/word2vec-tutorial)

- [使用tensorflow实现word2vec中文词向量的训练](https://zhuanlan.zhihu.com/p/28979653)

- [類神經網路 -- word2vec (part 1 : Overview) « MARK CHANG'S BLOG](http://cpmarkchang.logdown.com/posts/773062-neural-network-word2vec-part-1-overview)

- [Alex-CHUN-YU/Word2vec: 訓練中文詞向量 Word2vec, Word2vec was created by a team of researchers led by Tomas Mikolov at Google.](https://github.com/Alex-CHUN-YU/Word2vec)

- [用中文資料測試 word2vec - 翼之都, City of Wings](http://city.shaform.com/blog/2014/11/04/word2vec.html)

- [自然語言處理入門- Word2vec小實作 – PyLadies Taiwan – Medium](https://medium.com/pyladies-taiwan/%E8%87%AA%E7%84%B6%E8%AA%9E%E8%A8%80%E8%99%95%E7%90%86%E5%85%A5%E9%96%80-word2vec%E5%B0%8F%E5%AF%A6%E4%BD%9C-f8832d9677c8)

- [詞向量介紹](https://fgc.stpi.narl.org.tw/activity/videoDetail/4b1141305ddf5522015de5479f4701b1)

## fasttext

- [Word vectors for 157 languages · fastText](https://fasttext.cc/docs/en/crawl-vectors.html)



## skip-gram or CBOW

- [Is skip gram (negative sampling) better than CBOW (NS) for word2vec? If so, why? - Quora](https://www.quora.com/Is-skip-gram-negative-sampling-better-than-CBOW-NS-for-word2vec-If-so-why)

> Please see [Stephan Gouws](https://www.quora.com/profile/Stephan-Gouws) excellent answer here: [How does word2vec work? Can someone walk through a specific example?](https://www.quora.com/How-does-word2vec-work-Can-someone-walk-through-a-specific-example)
> 
> >For the skipgram, the direction of the prediction is simply inverted, i.e. now we try to predict P(citizens | X), P(of | X), etc. This turns out to learn finer-grained vectors when one trains over more data. The main reason is that the CBOW smooths over a lot of the distributional statistics by averaging over all context words while the skipgram does not. With little data, this "regularizing" effect of the CBOW turns out to be helpful, but since data is the ultimate regularizer the skipgram is able to extract more information when more data is available.
> 








## auto tagging

- [memray/seq2seq-keyphrase](https://github.com/memray/seq2seq-keyphrase)

- [udibr/headlines: Automatically generate headlines to short articles](https://github.com/udibr/headlines)

- [fudannlp16/KeyPhrase-Extraction](https://github.com/fudannlp16/KeyPhrase-Extraction)

- [Tensorflow：基于LSTM轻松生成各种古诗 - CSDN博客](https://blog.csdn.net/meyh0x5vdtk48p2/article/details/78987402)

- [[代码]基于RNN的文本生成算法 - CSDN博客](https://blog.csdn.net/clayanddev/article/details/53955850)

- [How can I use machine learning to propose tags for content? - Quora](https://www.quora.com/How-can-I-use-machine-learning-to-propose-tags-for-content)

- [Deep Learning for Text Understanding from Scratch](https://www.kdnuggets.com/2015/03/deep-learning-text-understanding-from-scratch.html)

- [neural network - Keyword/phrase extraction from Text using Deep Learning libraries - Data Science Stack Exchange](https://datascience.stackexchange.com/questions/10077/keyword-phrase-extraction-from-text-using-deep-learning-libraries)

- [attardi/deepnl: Deep Learning for Natural Language Processing](https://github.com/attardi/deepnl)

- [Intro to text classification with Keras: automatically tagging Stack Overflow posts | Google Cloud Big Data and Machine Learning Blog  |  Google Cloud](https://cloud.google.com/blog/big-data/2017/10/intro-to-text-classification-with-keras-automatically-tagging-stack-overflow-posts)

- [snkim/AutomaticKeyphraseExtraction: Data for Automatic Keyphrase Extraction Task](https://github.com/snkim/AutomaticKeyphraseExtraction)

- [lvsh/keywordfinder: Automatic keyword extraction - no alchemy required!](https://github.com/lvsh/keywordfinder)

- [Natural Language Toolkit — NLTK 3.2.5 documentation](http://www.nltk.org/)

- [nlp - How to auto-tag content, algorithms and suggestions needed - Stack Overflow](https://stackoverflow.com/questions/6039238/how-to-auto-tag-content-algorithms-and-suggestions-needed)

## Doc2Vec

- [A gentle introduction to Doc2Vec – ScaleAbout – Medium](https://medium.com/scaleabout/a-gentle-introduction-to-doc2vec-db3e8c0cce5e)

- [基于gensim的Doc2Vec简析 - CSDN博客](https://blog.csdn.net/lenbow/article/details/52120230)

- [基于jieba和doc2vec的中文情感语料分类 - 个人文章 - SegmentFault 思否](https://segmentfault.com/a/1190000012203525)

- [用 Doc2Vec 得到文档／段落／句子的向量表达 - 简书](https://www.jianshu.com/p/854a59b93e09)



- [jhlau/doc2vec: Python scripts for training/testing paragraph vectors](https://github.com/jhlau/doc2vec)

- [RaRe-Technologies/gensim: Topic Modelling for Humans](https://github.com/RaRe-Technologies/gensim)
    - [gensim/doc2vec-lee.ipynb at develop · RaRe-Technologies/gensim](https://github.com/RaRe-Technologies/gensim/blob/develop/docs/notebooks/doc2vec-lee.ipynb)
    - [gensim/doc2vec-IMDB.ipynb at develop · RaRe-Technologies/gensim](https://github.com/RaRe-Technologies/gensim/blob/develop/docs/notebooks/doc2vec-IMDB.ipynb)
    - [gensim/doc2vec-wikipedia.ipynb at develop · RaRe-Technologies/gensim](https://github.com/RaRe-Technologies/gensim/blob/develop/docs/notebooks/doc2vec-wikipedia.ipynb)

- [abtpst/Doc2Vec: Doc2Vec algorithm for solving moview review sentiment analysis](https://github.com/abtpst/Doc2Vec)

- [hiyijian/doc2vec: C++ implement of Tomas Mikolov's word/document embedding](https://github.com/hiyijian/doc2vec)

- [fbkarsdorp/doc2vec: Tutorial and review of word2vec / doc2vec](https://github.com/fbkarsdorp/doc2vec)

- [ibrahimsharaf/doc2vec: Text classification using Doc2Vec & Random Forest](https://github.com/ibrahimsharaf/doc2vec)

- [Doc2vec tutorial | RARE Technologies](https://rare-technologies.com/doc2vec-tutorial/)

- [How Quid uses deep learning with small data](https://quid.com/feed/how-quid-uses-deep-learning-with-small-data)

- [[1405.4053] Distributed Representations of Sentences and Documents](https://arxiv.org/abs/1405.4053)


- [情感分析的新方法——基于Word2Vec/Doc2Vec/Python - OPEN 开发经验库](http://www.open-open.com/lib/view/open1444351655682.html)

- [doc2vec计算文档相似度 - 程序园](http://www.voidcn.com/article/p-fiwnobtj-dx.html)

- [Doc2Vec tutorial using Gensim – Andreas Klintberg – Medium](https://medium.com/@klintcho/doc2vec-tutorial-using-gensim-ab3ac03d3a1)

- [How does doc2vec represent feature vector of a document? Can anyone explain mathematically how the process is done? - Quora](https://www.quora.com/How-does-doc2vec-represent-feature-vector-of-a-document-Can-anyone-explain-mathematically-how-the-process-is-done)

- [jhlau/doc2vec: Python scripts for training/testing paragraph vectors](https://github.com/jhlau/doc2vec)


## seq2seq

- [从Encoder到Decoder实现Seq2Seq模型](https://zhuanlan.zhihu.com/p/27608348)

- [Neural Machine Translation (seq2seq) Tutorial  |  TensorFlow](https://www.tensorflow.org/tutorials/seq2seq)

- [深度学习笔记——Word2vec和Doc2vec训练实例以及参数解读 - CSDN博客](https://blog.csdn.net/mpk_no1/article/details/72510655)

- [序列到序列的语言翻译模型代码(tensorflow)解析 - grt1st博客](https://www.grt1st.cn/posts/seq2seq-code/)

- [用seq2seq with attention实现中文歌词生成](https://zhuanlan.zhihu.com/p/25280463)

- [tensorflow代码全解析 -3- seq2seq 自动生成文本 - 简书](https://www.jianshu.com/p/9766b317ffa4)

- [從零開始的 Sequence to Sequence | 雷德麥的藏書閣](https://zake7749.github.io/2017/09/28/Sequence-to-Sequence-tutorial/)

- [教電腦寫作：AI球評——Seq2seq模型應用筆記(PyTorch + Python3) – Yi-Hsiang Kao – Medium](https://medium.com/@gau820827/%E6%95%99%E9%9B%BB%E8%85%A6%E5%AF%AB%E4%BD%9C-ai%E7%90%83%E8%A9%95-seq2seq%E6%A8%A1%E5%9E%8B%E6%87%89%E7%94%A8%E7%AD%86%E8%A8%98-pytorch-python3-31e853573dd0)


## Chinese Character Embeddings

- [干货|NLP领域中文vs英文有什么异同点，中文NLP有什么独特的地方?_搜狐科技_搜狐网](http://www.sohu.com/a/138840703_642762)

- [Leonard-Xu/CWE](https://github.com/Leonard-Xu/CWE)




## Entity extraction

- [Entity extraction using Deep Learning – Towards Data Science](https://towardsdatascience.com/entity-extraction-using-deep-learning-8014acac6bb8)

- [Sequence Tagging with Tensorflow](https://guillaumegenthial.github.io/sequence-tagging-with-tensorflow.html)

- [dlnd-other/embeddings at master · dkarunakaran/dlnd-other](https://github.com/dkarunakaran/dlnd-other/tree/master/embeddings)

- [Pretrained Character Embeddings for Deep Learning and Automatic Text Generation](http://minimaxir.com/2017/04/char-embeddings/)

- [Introduction to Conditional Random Fields](http://blog.echen.me/2012/01/03/introduction-to-conditional-random-fields/)





## Models
- [DeepMind丨深度學習最新生成記憶模型，遠超RNN的GTMM](http://www.bigdatafinance.tw/index.php/tech/557-deepmind-rnn-gtmm)




## 新聞

### 語音助理

- [個人語音助理時代已經來臨！ - EE Times Taiwan 電子工程專輯網](https://www.eettaiwan.com/news/article/20180416NT31-season-voice-based-personal-assistants?utm_source=EETT%20Article%20Alert&utm_medium=Email&utm_campaign=2018-04-17)

    > 過程和原理
    > 
    > 作為一名開發者和設計師，要充份使用這項技術，重要的是瞭解如下的完整命令互動過程：
    > 
    > * 虛擬助理使用一個觸發詞(如‘Ok Google’、‘Hey Siri’)來「喚醒」，以確保它只在命令下達時才執行。
    > * 音訊被記錄在設備上，經過壓縮並透過Wi-Fi傳輸到雲端。通常會採用降噪演算法來記錄音訊，以便雲端「大腦」更容易理解用戶的命令。
    > * 使用專有的「語音轉文本」(voice-to-text)平台將音訊轉換成文本命令。透過指定的頻率對類比訊號進行採樣，將類比聲波轉換為數位資料。分析數位資料以確定英語音素(‘bb’、‘oo’、‘sh’等)的出現位置。 一旦辨識別出音素，就使用統計建模演算法(如Hidden Markhov模型)來確定特定單詞的可能性。
    > * 使用自然語言處理技術來處理文本以確定所需的操作。 該演算法首先使用詞性標註來確定哪些詞是形容詞、動詞和名詞等，然後將這種標記與統計機器學習模型相結合起來，推斷句子的含義。
    > * 如果命令操作需要進一步的搜尋，系統將立即進行搜尋。例如，「嘿！Siri，什麼是Snapdragon行動平台？」將觸發網際網路搜尋，並返回所得到的資訊。如果該命令類似於「Ok Google，傳簡訊給媽媽」，那麼命令資料(操作：發送簡訊；收件人：媽媽)就會被直接傳送到虛擬助理。
    > 
    > 

