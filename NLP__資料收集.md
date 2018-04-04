# NLP__資料收集

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




## word2Vec

- [以 gensim 訓練中文詞向量 | 雷德麥的藏書閣](https://zake7749.github.io/2016/08/28/word2vec-with-gensim/)

- [zake7749/word2vec-tutorial: 中文詞向量訓練教學](https://github.com/zake7749/word2vec-tutorial)

- [使用tensorflow实现word2vec中文词向量的训练](https://zhuanlan.zhihu.com/p/28979653)

- [類神經網路 -- word2vec (part 1 : Overview) « MARK CHANG'S BLOG](http://cpmarkchang.logdown.com/posts/773062-neural-network-word2vec-part-1-overview)

- [Alex-CHUN-YU/Word2vec: 訓練中文詞向量 Word2vec, Word2vec was created by a team of researchers led by Tomas Mikolov at Google.](https://github.com/Alex-CHUN-YU/Word2vec)

- [用中文資料測試 word2vec - 翼之都, City of Wings](http://city.shaform.com/blog/2014/11/04/word2vec.html)





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



## Entity extraction

- [Entity extraction using Deep Learning – Towards Data Science](https://towardsdatascience.com/entity-extraction-using-deep-learning-8014acac6bb8)

- [Sequence Tagging with Tensorflow](https://guillaumegenthial.github.io/sequence-tagging-with-tensorflow.html)

- [dlnd-other/embeddings at master · dkarunakaran/dlnd-other](https://github.com/dkarunakaran/dlnd-other/tree/master/embeddings)

- [Pretrained Character Embeddings for Deep Learning and Automatic Text Generation](http://minimaxir.com/2017/04/char-embeddings/)

- [Introduction to Conditional Random Fields](http://blog.echen.me/2012/01/03/introduction-to-conditional-random-fields/)





## Models
- [DeepMind丨深度學習最新生成記憶模型，遠超RNN的GTMM](http://www.bigdatafinance.tw/index.php/tech/557-deepmind-rnn-gtmm)

