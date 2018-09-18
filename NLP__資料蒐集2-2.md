# NLP__資料蒐集2-2

[toc]
<!-- toc --> 

## 文章向量

### 概觀

- [當前最好的詞句嵌入技術概覽：從無監督學習到監督、多任務學習 - 幫趣](http://bangqu.com/59R436.html#utm_source=Facebook_PicSee&utm_medium=Social)

    - [📚The Current Best of Universal Word Embeddings and Sentence Embeddings](https://medium.com/huggingface/universal-word-sentence-embeddings-ce48ddc8fc3a)

    > FastText 相對於原始的 word2vec 向量最主要的提升是它引入了 n 元字符（n-gram），這使得對沒有在訓練數據中出現的單詞（詞彙表外的單詞）計算單詞的表徵成爲了可能。
    >     
    > ---
    >     
    > 深度上下文單詞表徵（ELMo）在很大的程度上提高了目前最先進的詞嵌入模型的性能。它們由 Allen 人工智能研究所研發，並將在 6 月初的 NAACL 2018 （ https://arxiv.org/abs/1802.05365 ） 中展示。
    > 
    > ELMo 模型會爲每一個單詞分配一個表徵，該表徵是它們所屬的整個語料庫中的句子的一個函數。詞嵌入將從一個兩層的雙向語言模型（LM）的內部狀態中計算出來，因此該模型被命名爲「ELMo」： Embeddings from Language Models（E 代表「嵌入」，LM 代表「語言模型」）。
    > 
    > ELMo 模型的特點：
    > 
    > - ELMo 模型的輸入是字符而不是單詞。因此，它們可以利用子詞單元的優勢來計算有意義的單詞表示，即使這些單詞可能在詞彙表之外（就像 FastText 一樣）。
    > 
    > - ELMo 是在雙向語言模型中的一些層上的激勵函數的串接。一個語言模型的不同層會對一個單詞的不同類型的信息進行編碼（例如，詞性標註（Part-Of-Speech tagging）由雙向 LSTM（biLSTM）的較低層很好地預測，而詞義排歧則由較高層更好地進行編碼）。將所有的層串接起來使得自由組合各種不同的單詞表徵成爲了可能，從而在下游任務中得到更好的模型性能。
    > 
    > ---
    > 
    > 在這個領域有一個廣泛的共識（ http://arxiv.org/abs/1805.01070 ） ，那就是：直接對句子的詞嵌入取平均（所謂的詞袋模型（Bag-of-Word，BoW））這樣簡單的方法可以爲許多下游任務提供一個很強大的對比基線。
    > 
    > Arora 等人在 ICLR 2017 上提出了「A Simple but Tough-to-Beat Baseline for Sentence Embeddings」 （ https://openreview.net/forum?id=SyK00v5xx ） ，這是一個很好的能夠被用於計算這個基線（BoW）的算法，算法的大致描述如下：選擇一個流行的詞嵌入方法，通過詞向量的線性的加權組合對一個句子進行編碼，並且刪除共有的部分（刪除它們的第一個主成分上的投影）。
    > 
    > ---
    > 
    > 除了簡單的詞向量平均，第一個主要的提議是使用無監督學習訓練目標，這項工作是起始於 Jamie Kiros 和他的同事們在 2015 年提出的「Skip-thought vectors」（ https://arxiv.org/abs/1506.06726 ） 。
    > 
    > 「Skip-thoughts vector」是一個典型的學習無監督句子嵌入的案例。它可以被認爲相當於爲詞嵌入而開發的「skip-gram」模型的句子向量，我們在這裏試圖預測一個給定的句子周圍的句子，而不是預測一個單詞周圍的其他單詞。該模型由一個基於循環神經網絡的編碼器—解碼器結構組成，研究者通過訓練這個模型從當前句子中重構周圍的句子。
    > 
    > Skip-Thoughts 的論文中最令人感興趣的觀點是一種詞彙表擴展方案：Kiros 等人通過在他們的循環神經網絡詞嵌入空間和一個更大的詞嵌入空間（例如，word2vec）之間學習一種線性變換來處理訓練過程中沒有出現的單詞。
    > 
    > 「Quick-thoughts vectors」（ https://openreview.net/forum?id=rJvJXZb0W ） 是研究人員最近對「Skip-thoughts vectors」的一個改進，它在今年的 ICLR 上被提出。在這項工作中，在給定前一個句子的條件下預測下一個句子的任務被重新定義爲了一個分類問題：研究人員將一個用於在衆多候選者中選出下一個句子的分類器代替瞭解碼器。它可以被解釋爲對生成問題的一個判別化的近似。
    > 
    > 該模型的運行速度是它的優點之一（與 Skip-thoughts 模型屬於同一個數量級），使其成爲利用海量數據集的一個具有競爭力的解決方案。
    > 
    > ![](http://i2.bangqu.com/j/news/20180606/59R4361528261210081r28S2.png)*「Quick-thoughts」分類任務示意圖。分類器需要從一組句子嵌入中選出下一個句子。圖片來自 Logeswaran 等人所著的「An efficient framework for learning sentence representations」。*
    > 
    > ---
    > 
    > 在很長一段時間內，人們認爲監督學習技術比無監督學習技術得到的句子嵌入的質量要低一些。然而，這種假說最近被推翻了，這要部分歸功於「InferSent」（ https://arxiv.org/abs/1705.02364 ） 的提出。
    > 
    > InferSent 具有非常簡單的架構，這使得它成爲了一種非常有趣的模型。它使用 Sentence Natural Language Inference（NLI）數據集（該數據集包含 570,000 對帶標籤的句子，它們被分成了三類：中立、矛盾以及蘊含）訓練一個位於句子編碼器頂層的分類器。兩個句子使用同一個編碼器進行編碼，而分類器則是使用通過兩個句子嵌入構建的一對句子表徵訓練的。Conneau 等人採用了一個通過最大池化操作實現的雙向 LSTM 作爲編碼器。
    > 
    > ![](http://i2.bangqu.com/j/news/20180606/59R4361528261211217433N2.png)
    > 
    > 
    > ---
    >
    > 在 ICLR 2018 上發表的描述 MILA 和微軟蒙特利爾研究院的工作的論文《Learning General Purpose Distributed Sentence Representation via Large Scale Multi-Task Learning》（ https://arxiv.org/abs/1804.00079 ）中，Subramanian 等人觀察到，爲了能夠在各種各樣的任務中泛化句子表徵，很有必要將一個句子的多個層面的信息進行編碼。
    > 
    > 因此，這篇文章的作者利用了一個一對多的多任務學習框架，通過在不同的任務之間進行切換去學習一個通用的句子嵌入。被選中的 6 個任務（對於下一個/上一個句子的 Skip-thoughts 預測、神經機器翻譯、組別解析（constituency parsing），以及神經語言推理）共享相同的由一個雙向門控循環單元得到的句子嵌入。實驗表明，在增添了一個多語言神經機器翻譯任務時，句法屬性能夠被更好地學習到，句子長度和詞序能夠通過一個句法分析任務學習到，並且訓練一個神經語言推理能夠編碼語法信息。
    > 
    > 谷歌在 2018 年初發布的的通用句子編碼器（ https://arxiv.org/abs/1803.11175 ）也使用了同樣的方法。他們的編碼器使用一個在各種各樣的數據源和各種各樣的任務上訓練的轉換網絡，旨在動態地適應各類自然語言理解任務。該模型的一個預訓練好的版本可以在 TensorFlow 獲得。


### TF-IDF

- [tf–idf - Wikiwand](https://www.wikiwand.com/en/Tf%E2%80%93idf)

- [[文件探勘] TF-IDF 演算法：快速計算單字與文章的關聯 – David's Perspective](https://taweihuang.hpd.io/2017/03/01/tfidf/)

    > ### BoW (Bag of Words) 與詞彙數量-文件矩陣
    > 
    > 假設現在有 ![D](https://s0.wp.com/latex.php?latex=D&bg=ffffff&fg=000&s=0 "D") 篇文件 (document)，而所有文件中總共使用了 ![~T~](https://s0.wp.com/latex.php?latex=%7ET%7E&bg=ffffff&fg=000&s=0 "~T~") 個詞彙 (term)，我們就可以將文章轉換成以下類型的矩陣，其中第一欄第一列的「12」代表的是「文件 1」 中出現了12個「文字 1」。如此一來，我們可以用 ![[12,~0,~3,~\cdots,~2]](https://s0.wp.com/latex.php?latex=%5B12%2C%7E0%2C%7E3%2C%7E%5Ccdots%2C%7E2%5D&bg=ffffff&fg=000&s=0 "[12,~0,~3,~\cdots,~2]") 這個向量來代表「文件 1」，同理也可用「文件 D」也可以用 ![[0,~2,~8,~\cdots,~0]](https://s0.wp.com/latex.php?latex=%5B0%2C%7E2%2C%7E8%2C%7E%5Ccdots%2C%7E0%5D&bg=ffffff&fg=000&s=0 "[0,~2,~8,~\cdots,~0]") 來表示。
    > 
    > ![圖片1](https://taweihuang.hpd.io/wp-content/uploads/2017/03/圖片1.png)
    > 
    > 這樣的方法就是「BoW (Bag of Word)演算法」，這種方法雖然很簡單，但有2個主要的問題 ─ 一是每篇文章的總字數不一樣，比如說文字 2在文件 2中出現9次，在文件 D中卻只出現2次，這樣是否代表文字 2 對文件 2 比較重要，對文件 D 比較不重要呢？答案是否定的，說不定文件2有10000個字，而文件D只有50個字，如此一來文字2應該對文件D比較重要才對。
    > 
    > 另一個問題是，時常重複出現的慣用詞彙對一個文件的影響很大。比如說，上圖中的文字 3在每個文件中都出現好多次，可能是「the」之類的常用字，如此一來「文件 D」的向量就會被  the 這個字所主導，但 the 這個字其實沒什麼特別的意義。
    > 
    > 為了處理以上兩個問題，歷史悠久但非常好用的 TF-IDF演算法就被發明出來了。
    > 
    > ### TF-IDF 演算法
    > 
    > TF-IDF 演算法包含了兩個部分：**詞頻**（term frequency，TF）跟**逆向文件頻率**（inverse document frequency，IDF）。詞頻指的是某一個給定的詞語在該文件中出現的頻率，第 ![t](https://s0.wp.com/latex.php?latex=t&bg=ffffff&fg=000&s=0 "t")個詞出現在第 ![~d~](https://s0.wp.com/latex.php?latex=%7Ed%7E&bg=ffffff&fg=000&s=0 "~d~") 篇文件的頻率記做 ![~tf_{t,d}~](https://s0.wp.com/latex.php?latex=%7Etf_%7Bt%2Cd%7D%7E&bg=ffffff&fg=000&s=0 "~tf_{t,d}~")，舉例來說，如果文件 1 總共有100個字，而第 1 個字在文件 1 出現的次數是12次，因此![~tf_{1,1}=12/100~](https://s0.wp.com/latex.php?latex=%7Etf_%7B1%2C1%7D%3D12%2F100%7E&bg=ffffff&fg=000&s=0 "~tf_{1,1}=12/100~")，如此一來，我們就可以針對上述的第一個問題進行修正，以頻率而不是次數來看待文字的重要性，讓文章與文章之間比較有可比較性。
    > 
    > 而逆向文件頻率則是用來處理常用字的問題。假設詞彙 ![t](https://s0.wp.com/latex.php?latex=t&bg=ffffff&fg=000&s=0 "t") 總共在 ![d_t](https://s0.wp.com/latex.php?latex=d_t&bg=ffffff&fg=000&s=0 "d_t") 篇文章中出現過，則詞彙 ![t](https://s0.wp.com/latex.php?latex=t&bg=ffffff&fg=000&s=0 "t") 的 IDF 定義成 ![~idf_t = \log\left(\frac{D}{d_t}\right)~](https://s0.wp.com/latex.php?latex=%7Eidf_t+%3D+%5Clog%5Cleft%28%5Cfrac%7BD%7D%7Bd_t%7D%5Cright%29%7E&bg=ffffff&fg=000&s=0 "~idf_t = \log\left(\frac{D}{d_t}\right)~")。比如說，假設文字 1 總共出現在 25 篇不同的文件，則 ![~~idf_1 = \log\left(\frac{D}{25}\right)~~](https://s0.wp.com/latex.php?latex=%7E%7Eidf_1+%3D+%5Clog%5Cleft%28%5Cfrac%7BD%7D%7B25%7D%5Cright%29%7E%7E&bg=ffffff&fg=000&s=0 "~~idf_1 = \log\left(\frac{D}{25}\right)~~")。如果詞彙 ![t](https://s0.wp.com/latex.php?latex=t&bg=ffffff&fg=000&s=0 "t")在非常多篇文章中都出現過，就代表 ![~d_t~](https://s0.wp.com/latex.php?latex=%7Ed_t%7E&bg=ffffff&fg=000&s=0 "~d_t~") 很大，此時![~idf_t~](https://s0.wp.com/latex.php?latex=%7Eidf_t%7E&bg=ffffff&fg=000&s=0 "~idf_t~") 就會比較小。
    > 
    > 而一個字對於一篇文件重要性的分數 (score) 就可以透過TF與IDF兩個指標計算出來，我們將第 ![t](https://s0.wp.com/latex.php?latex=t&bg=ffffff&fg=000&s=0 "t")個詞彙對於第 ![~d~](https://s0.wp.com/latex.php?latex=%7Ed%7E&bg=ffffff&fg=000&s=0 "~d~") 篇文件的TF-IDF權重定義為 ![~w_{t,d} =  tf_{t,d} \times  idf_t ~](https://s0.wp.com/latex.php?latex=%7Ew_%7Bt%2Cd%7D+%3D%C2%A0+tf_%7Bt%2Cd%7D+%5Ctimes+%C2%A0idf_t+%7E&bg=ffffff&fg=000&s=0 "~w_{t,d} =  tf_{t,d} \times  idf_t ~")。如此一來，當詞彙 ![~t~](https://s0.wp.com/latex.php?latex=%7Et%7E&bg=ffffff&fg=000&s=0 "~t~") 很常出現在文件  ![~d~](https://s0.wp.com/latex.php?latex=%7Ed%7E&bg=ffffff&fg=000&s=0 "~d~") 時，他的 ![~tf_{t,d} ~](https://s0.wp.com/latex.php?latex=%7Etf_%7Bt%2Cd%7D+%7E&bg=ffffff&fg=000&s=0 "~tf_{t,d} ~") 就會比較大，而如果詞彙![~~ t](https://s0.wp.com/latex.php?latex=%7E%7Et&bg=ffffff&fg=000&s=0 "~~t") 也很少出現在其他篇文章，則 ![~idf_t~](https://s0.wp.com/latex.php?latex=%7Eidf_t%7E&bg=ffffff&fg=000&s=0 "~idf_t~") 也會比較大，使 ![~w_{t,d}~](https://s0.wp.com/latex.php?latex=%7Ew_%7Bt%2Cd%7D%7E&bg=ffffff&fg=000&s=0 "~w_{t,d}~")整體來說比較大，也就是說詞彙![~t~](https://s0.wp.com/latex.php?latex=%7Et%7E&bg=ffffff&fg=000&s=0 "~t~") 對於文件  ![~d~](https://s0.wp.com/latex.php?latex=%7Ed%7E&bg=ffffff&fg=000&s=0 "~d~") 來說是很重要的。如此一來，我們就可以計算出 TF-IDF 矩陣，如下圖所示。
    > 
    > ![圖片1](https://taweihuang.hpd.io/wp-content/uploads/2017/03/圖片1-1.png)
    > 
    > 另一方面， TF-IDF 時常被用來作資訊檢索 (information retrieval)，比如說，給定一串指令 (query)「文字 1 + 文字 3 + 不在現有詞彙裡面的文字」，則這串指令跟第 ![d](https://s0.wp.com/latex.php?latex=d&bg=ffffff&fg=000&s=0 "d") 的關聯分數就可以定義文 ![tf_{1,d} + tf_{3,d} ](https://s0.wp.com/latex.php?latex=tf_%7B1%2Cd%7D+%2B+tf_%7B3%2Cd%7D%C2%A0&bg=ffffff&fg=000&s=0 "tf_{1,d} + tf_{3,d} ")。
    > 
    > ### 大鼻是怎麼用 TF-IDF？
    > 
    > TF-IDF 常被我用在3個地方，一個是作為 baseline model的特徵 (feature)，比如說作文件分類 (text classification) 時，我就會把 tf 跟 idf 都當作文件的特徵(所以一篇文章總夠會有 ![2T](https://s0.wp.com/latex.php?latex=2T&bg=ffffff&fg=000&s=0 "2T")個特徵)，去跑分類模型，作為 baseline。有時候我會把一個詞彙對於每篇的文章的 tf-idf 值當作該詞彙的特徵，去跑文字的分群。還有一個是大鼻好友ㄐㄓ告訴我的妙招，就是如果我們想要用word2vec得出來的詞向量去表示一個文件的話，可以用tf-idf的值當作權重，再把該文件中每個詞向量用tf-idf當作權重加起來，效果也很不錯喔！






### Doc2Vec

#### 原理



- [深度学习笔记——Word2vec和Doc2vec原理理解并结合代码分析 - CSDN博客](https://blog.csdn.net/mpk_no1/article/details/72458003)

- [A gentle introduction to Doc2Vec – ScaleAbout – Medium](https://medium.com/scaleabout/a-gentle-introduction-to-doc2vec-db3e8c0cce5e)

- [How does doc2vec represent feature vector of a document? Can anyone explain mathematically how the process is done? - Quora](https://www.quora.com/How-does-doc2vec-represent-feature-vector-of-a-document-Can-anyone-explain-mathematically-how-the-process-is-done)

    - [[1405.4053] Distributed Representations of Sentences and Documents](https://arxiv.org/abs/1405.4053)

    > Doc2Vec explores the above observation by adding additional input nodes representing documents as additional context. Each additional node can be thought of just as an id for each input document.
    > 
    > ![](https://qph.ec.quoracdn.net/main-qimg-3449ced3d53f653ebfd9b73db1065056)
    > 
    > D represent the features representing the document context and W
    > 
    > represent the word context in a window surrounding the target word. Training is similar to word2vec, with additional document context. The objective of doc2vec learning is
    > 
    > max∑∀(tar,con,doc)logP
    > 
    > (target word|context words, document context)
    > 
    > At the end of the training process, you will have word embeddings, W
    > 
    > and document embedding D
    > 
    > for documents in the training corpus.
    > 
    > Great! We got document embeddings for input corpus but what about new unseen documents that appear in the test set. The idea is to learn their representation at test time by solving an optimization problem for inference.
    > 
    > ![](https://qph.ec.quoracdn.net/main-qimg-0112c98875541c958abee17d10fccdaa)
    > 
    > The optimization problem is not any different from the training problem. max∑∀(tar,con)logP
    > 
    > (target word|context words, document = test doc). One may however, choose to keep W and W′ fixed and learn variable D as document embedding.
    > 
    > The other resource is my (unfinished and unedited) notes on W2V and P2V derivations: "[Understanding Word2Vec and Paragraph2Vec](http://piyushbhardwaj.github.io/documents/w2v_p2vupdates.pdf)".
    > 

- [Distributed representations of sentences and documents | the morning paper](https://blog.acolyer.org/2016/06/01/distributed-representations-of-sentences-and-documents/)

    > the word vectors are asked to contribute to a prediction task about the next word in the sentence.
    > 
    > The paragraph vectors are also asked to contribute to the prediction task of the next word given many contexts sampled from the paragraph. 
    > 
    > ![](https://adriancolyer.files.wordpress.com/2016/05/paragraph-vectors-fig-2.png?w=566&zoom=2)
    > 
    > The only change compared to word vector learning is that the paragraph vector is concatenated with the word vectors to predict the next word in a context. Contexts are fixed length and sampling from a sliding window over a paragraph. Paragraph vectors are shared for all windows generated from the same paragraph, but not across paragraphs.
    > 
    > It acts as a memory that remembers what is missing from the current context – or the topic of the paragraph. For this reason, we often call this model the Distributed Memory Model of Paragraph Vectors (PV-DM).
    > 
    > In summary, the algorithm itself has two key stages: 1) training to get word vectors W, softmax weights U, b and paragraph vectors D on already seen paragraphs; and 2) “the inference stage” to get paragraph vectors D for new paragraphs (never seen before) by adding more columns in D and gradient descending on D while holding W, U, b fixed. We use D to make a prediction about some particular labels using a standard classifier, e.g., logistic regression. 
    > 
    > A variation on the above scheme is ignore context words in the input (i.e., do away with the sliding window), and instead force the model to predict words randomly sampled from the paragraph in the output.
    > 
    > we sample a text window, then sample a random word from the text window and form a classification task given the Paragraph Vector… We name this version the Distributed Bag of Words version of Paragraph Vector (PV-DBOW)
    > 
    > ![](https://adriancolyer.files.wordpress.com/2016/05/paragraph-vectors-fig-3.png?w=566&zoom=2)
    > 
    > PV-DM performs better than PV-DBOW, but in tests combining both PV-DM and PV-DBOW gives the best results of all




#### 實作

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




- [情感分析的新方法——基于Word2Vec/Doc2Vec/Python - OPEN 开发经验库](http://www.open-open.com/lib/view/open1444351655682.html)

- [doc2vec计算文档相似度 - 程序园](http://www.voidcn.com/article/p-fiwnobtj-dx.html)

- [Doc2Vec tutorial using Gensim – Andreas Klintberg – Medium](https://medium.com/@klintcho/doc2vec-tutorial-using-gensim-ab3ac03d3a1)


- [jhlau/doc2vec: Python scripts for training/testing paragraph vectors](https://github.com/jhlau/doc2vec)


- [TensorFlow-Machine-Learning-Cookbook/doc2vec.py at master · PacktPublishing/TensorFlow-Machine-Learning-Cookbook](https://github.com/PacktPublishing/TensorFlow-Machine-Learning-Cookbook/blob/master/Chapter%2007/doc2vec.py#L112:1)


- [Coding doc2vec - Luminis Amsterdam](https://amsterdam.luminis.eu/2017/02/21/coding-doc2vec/)

    - [blog-doc2vec/pvdbow.ipynb at master · luminis-ams/blog-doc2vec](https://github.com/luminis-ams/blog-doc2vec/blob/master/pvdbow.ipynb)

    > Training the network
    > --------------------
    > 
    > In Tensorflow, training a network is done in two steps. First, you define the model. You can think of the model as a graph. Second, you run the model. We'll take a look at the first step, how our model is defined. First: the input.
    > 
    > 
    > ```python=
    > # Input data
    > 
    > dataset = tf.placeholder(tf.int32, shape=[BATCH_SIZE])
    > 
    > labels = tf.placeholder(tf.int32, shape=[BATCH_SIZE, 1])
    > ```
    >  
    > 
    > The `dataset` is defined as a placeholder with the shape of a simple array that contains ints. When we run the model, it will contain document ids. Nothing more, nothing less. It will contain as many document ids as we want to feed the stochastic gradient descent algorithm in a single iteration. The `labels` placeholder is also a vector. It will contain integers that represent words from the vocabulary. So, basically, for each document id we want to predict a word that occurs in it. In our implementation, we make sure that a batch contains one or more text windows. So if we use a text window of size 8, a batch will contain one or more sequences of eight consecutive words. Next, we take a look at the weights in our neural network:
    > 
    > 
    > ```python=
    > # Weights
    > 
    > embeddings = tf.Variable(
    > 
    >     tf.random_uniform([len(doclens), EMBEDDING_SIZE],
    >                     -1.0, 1.0))
    > 
    > softmax_weights = tf.Variable(
    >     tf.truncated_normal(
    >             [vocab_size, EMBEDDING_SIZE],
    >             stddev=1.0 / np.sqrt(EMBEDDING_SIZE)))
    > 
    > softmax_biases = tf.Variable(tf.zeros([vocab_size]))
    > ```
    > 
    > 
    > You can think of `embeddings` as the transpose of the matrix ![D](https://amsterdam.luminis.eu/wp-content/ql-cache/quicklatex.com-4b9ef1bbd23fd1b198de883813285620_l3.svg "Rendered by QuickLaTeX.com") from our [previous post](https://amsterdam.luminis.eu/2017/01/30/implementing-doc2vec/) [2]. In its rows, it has a document vector of length `EMBEDDING_SIZE` for each document id. This document vector is also called an "input vector". You can also think of `embeddings` as the weights between the input layer and the middle layer of our small doc2vec network. When we run the session, we will initialize the `embeddings` variable with random weights between ![-1.0](https://amsterdam.luminis.eu/wp-content/ql-cache/quicklatex.com-ee8fa04fc2bf1dbbff787fc33f469ffe_l3.svg "Rendered by QuickLaTeX.com") and ![1.0](https://amsterdam.luminis.eu/wp-content/ql-cache/quicklatex.com-2b23fc34a5447966d71dba505f0d8e9c_l3.svg "Rendered by QuickLaTeX.com").
    > 
    > The `softmax_weights` are the weights between the middle layer and the output layer of our network. You can also think of them as the matrix ![U](https://amsterdam.luminis.eu/wp-content/ql-cache/quicklatex.com-2b60fc262803f27ba3717d8ec4eb656d_l3.svg "Rendered by QuickLaTeX.com") from our previous post. On its rows, it has an "output vector" of length `EMBEDDING_SIZE` for each word in the vocabulary. When we run the model in our session, we will initialize these weights with (truncated) normally distributed random variables with mean zero and a standard deviation that is inversely proportional to `EMBEDDING_SIZE`. Why are these variables initialized using a normal distribution, instead of with a uniform distribution like we used for the embeddings? The short answer is: because this way of initialisation has apparently worked well in the past. You can try different initialisation schemes yourself, and see what it does to your end-to-end performance. The long answer; well, perhaps that's food for another blog post.
    > 
    > The `softmax_biases` are initialised here with zeroes. In our previous post, we mentioned that softmax biases are often used, but omitted them in our final loss function. Here, we used them, because the word2vec implementation we based this notebook on used them. And the function we use for negative sampling wants them, too.
    > 
    > The activation in the middle layer, or, alternatively, the estimated document vector for a document id is given by `embed`:
    > 
    > ```python=
    > embed = tf.nn.embedding_lookup(embeddings, dataset)
    > ```
    > 
    > `tf.nn.embedding_lookup` will provide us with fast lookup of a document vector for a given document id.
    > 
    > Finally, we are ready to compute the loss function that we'll minimise:
    > 
    > ```python=
    > 
    > loss = tf.reduce_mean(
    >         tf.nn.sampled_softmax_loss(
    >                 softmax_weights, softmax_biases, embed,
    >                 labels, NUM_SAMPLED, vocab_size))
    > 
    > ```
    > 
    > Here, `tf.nn.sampled_softmax_loss` takes care of negative sampling for us. `tf.reduce_mean` will compute the average loss over all the training examples in our batch.
    > 
    > As an aside, if you take a look at the complete source code in the notebook, you'll notice that we also have a function `test_loss`. That function does not use negative sampling. It should not, because negative sampling underestimates the true loss of the network. It is only used because it is faster to compute than the real loss. When you run the notebook, you will see that the training losses it prints are always lower than the test losses. One other remark about the test loss is the following: the test examples are taken from the same set of documents as the training examples! This is because in our network, we have no input to represent a document that we have never seen before. The text windows that have to be predicted for a given document id are different though, in the test set.
    > 
    > ---
    > 
    > Q: i want to change your code for my dataset which is a numpy lists of a list of documents. Am i suppose to give them each a file id or divide them by training and test label?
    > 
    > ---
    > 
    > A: There are a bunch of things you can do. One of them is include your test set in the training set while fitting this doc2vec model. That would not be cheating if you are aware of the locations of the points in your test set at the time you want to classify them (as you do not use the class labels while training doc2vec). This kind of learning task is sometimes called semi-supervised learning, or transductive learning. The doc2vec embeddings are then your feature vectors. Once you have them, for the document classification task (I assume you are doing), you divide your data in training and test sets as usual.
    > 


### LDA

- [Latent Dirichlet Allocation](http://www.jmlr.org/papers/v3/blei03a.html)

- [LDA-math-汇总 LDA数学八卦 | 我爱自然语言处理](http://www.52nlp.cn/lda-math-%e6%b1%87%e6%80%bb-lda%e6%95%b0%e5%ad%a6%e5%85%ab%e5%8d%a6)


- [LDA(Latent Dirichlet Allocation)主题模型 - CSDN博客](https://blog.csdn.net/aws3217150/article/details/53840029)

    > LDA于2003年由 David Blei, Andrew Ng和 Michael I. Jordan提出，因为模型的简单和有效，掀起了主题模型研究的波浪。虽然说LDA模型简单，但是它的数学推导却不是那么平易近人，一般初学者会深陷数学细节推导中不能自拔。于是牛人们看不下去了，纷纷站出来发表了各种教程。国内方面rickjin有著名的《[LDA数学八卦](http://www.52nlp.cn/author/rickjin)》，国外的Gregor Heinrich有著名的《[Parameter estimation for text analysis](https://users.soe.ucsc.edu/~amichelo/docs/text-est2.pdf)》。其实有了这两篇互补的通俗教程，大家沉住心看个4、5遍，基本就可以明白LDA为什么是简单的了。那么其实也没我什么事了，然而心中总有一种被大牛点播的豁然开朗的快感，实在是不吐不快啊。
    > 
    > 什么是主题
    > =====
    > 
    > 因为LDA是一种主题模型，那么首先必须明确知道LDA是怎么看待主题的。对于一篇新闻报道，我们看到里面讲了昨天NBA篮球比赛，那么用大腿想都知道它的主题是关于体育的。为什么我们大腿会那么聪明呢？这时大腿会回答因为里面出现了"科比"、"湖人"等等关键词。那么好了，我们可以定义主题是一种关键词集合，如果另外一篇文章出现这些关键词，我们可以直接判断他属于某种主题。但是，亲爱的读者请你想想，这样定义主题有什么弊端呢？按照这种定义，我们会很容易给出这样的条件：一旦文章出现了一个球星的名字，那么那篇文章的主题就是体育。可能你马上会骂我在瞎说，然后反驳说不一定，文章确实有球星的名字，但是里面全部在讲球星的性丑闻，和篮球没半毛钱关系，此时主题是娱乐还差不多。所以一个词不能硬性地扣一个主题的帽子，如果说一篇文章出现了某个球星的名字，我们只能说有很大概率他属于体育的主题，但也有小概率属于娱乐的主题。于是就会有这种现象：**同一个词，在不同的主题背景下，它出现的概率是不同的**。并且我们都可以基本确定，一个词不能代表一种主题，那么到底什么才是主题呢？耐不住性子的同学会说，既然一个词代表不了一种主题，那我就把所有词都用来代表一种主题，然后你自己去慢慢意会。没错，这样确实是一种完全的方式，主题本来就蕴含在所有词之中，这样确实是最保险的做法，但是你会发现这样等于什么都没做。老奸巨猾的LDA也是这么想的，但他狡猾之处在于它用非常圆滑手段地将主题用所有词汇表达出来。怎么个圆滑法呢？手段便是概率。LDA认为天下所有文章都是用基本的词汇组合而成，此时假设有词库V={v1,v2,....,vn}
    > 
    > ，那么如何表达主题k
    > 
    > 呢？LDA说通过词汇的概率分布来反映主题！多么狡猾的家伙。我们举个例子来说明LDA的观点。假设有词库
    > 
    > {科比，篮球，足球，奥巴马，希拉里，克林顿}
    > 
    > 假设有两个主题
    > 
    > {体育，政治}
    > 
    > LDA说体育这个主题就是：
    > 
    > {科比:0.3，篮球:0.3，足球:0.3，奥巴马:0.03，希拉里:0.03，克林顿:0.04}
    > 
    > (数字代表某个词的出现概率)，而政治这个主题就是：
    > 
    > {科比:0.03，篮球:0.03，足球:0.04，奥巴马:0.3，希拉里:0.3，克林顿:0.3}
    > 
    > LDA就是这样说明什么是主题的，竟说得我无言以对，细思之下也是非常合理。
    > 
    > 文章在讲什么
    > ======
    > 
    > 给你一篇文章读，然后请你简要概括文章在讲什么，你可能会这样回答：80%在讲政治的话题，剩下15%在讲娱乐，其余都是废话。这里大概可以提炼出三种主题：政治，娱乐，废话。也就是说，对于某一篇文章，很有可能里面不止在讲一种主题，而是几种主题混在一起的。读者可能会问，LDA是一种可以从文档中提炼主题模型，那他在建模的时候有没有考虑这种情形啊，他会不会忘记考虑了。那您就大可放心了，深谋远虑的LDA早就注意到这些了。LDA认为，文章和主题之间并不一定是一一对应的，也就是说，文章可以有多个主题，一个主题可以在多篇文章之中。这种说法，相信读者只能点头称是。假设现在有K
    > 
    > 个主题，有M
    > 
    > 篇文章，那么每篇文章里面不同主题的组成比例应该是怎样的呢？由于上一小节我们知道不能硬性的将某个词套上某个主题，那么这里我们当然不能讲某个主题套在某个文章中，也就是有这样的现象：**同一个主题，在不同的文章中，他出现的比例(概率)是不同的**，看到这里，读者可能已经发现，文档和主题之间的关系和主题和词汇的关系是多么惊人的类似！LDA先人一步地将这一发现说出来，它说，上一节我们巧妙地用词汇的分布来表达主题，那么这一次也不例外，我们巧妙地用主题的分布来表达文章！同样，我们举个例子来说明一下，假设现在有两篇文章：
    > 
    > 《体育快讯》，《娱乐周报》
    > 
    > 有三个主题
    > 
    > 体育，娱乐，废话
    > 
    > 那么
    > 
    > 《体育快讯》是这样的:[废话,体育,体育,体育,体育,....,娱乐,娱乐]
    > 
    > 而
    > 
    > 《娱乐周报》是这样的:[废话,废话,娱乐,娱乐,娱乐,....,娱乐,体育]
    > 
    > 也就是说，一篇文章在讲什么，通过不同的主题比例就可以概括得出。
    > 
    > 文章是如何生成的
    > ========
    > 
    > 在前面两小节中，LDA认为，每个主题会对应一个词汇分布，而每个文档会对应一个主题分布，那么一篇文章是如何被写出来的呢？读者可能会说靠灵感+词汇。LDA脸一沉，感觉完蛋，灵感是什么玩意？LDA苦思冥想，最后没办法，想了个馊主意，它说
    > 
    > 灵感=随机
    > 
    > 这也是没办法中的办法。因此对于某一篇文章的生产过程是这样的：
    > 
    > 1.  确定主题和词汇的分布
    > 2.  确定文章和主题的分布
    > 3.  随机确定该文章的词汇个数N
    > 
    > -\
    >     -   如果当前生成的词汇个数小于N
    > 
    > 1.  执行第5步，否则执行第6步
    > 2.  由文档和主题分布随机生成一个主题，通过该主题由主题和词汇分布随机生成一个词，继续执行第4步
    > 3.  文章生成结束
    > 
    > 只要确定好两个分布(主题与词汇分布，文章与主题分布)，然后随机生成文章各个主题比例，再根据各个主题随机生成词，词与词之间的顺序关系被彻底忽略了，这就是LDA眼中世间所有文章的生成过程！聪明的读者肯定觉得LDA完全就是一个骗子，这样认为文章的生成未免也太过天真了吧。然而事实就是如此，这也是为什么说LDA是一个很简单的模型。幸好我们这是用LDA来做主题分析，而不是用来生成文章，而从上上节的分析我们知道，主题其实就是一种词汇分布，这里并不涉及到词与词的顺序关系，所以LDA这种BOW(bag of words)的模型也是有它的简便和实用之处的。
    > 
    > LDA数学分析
    > =======
    > 
    > 上一小节，我们忽略了一个问题，就是如何确定主题和词汇分布，还有文档与词汇的分布，但是要搞明白这个问题，就避免不了一些数学分析了。再次强烈推荐rickjin的《[LDA数学八卦](http://www.52nlp.cn/author/rickjin)》还有Gregor Heinrich有著名的《[Parameter estimation for text analysis](https://users.soe.ucsc.edu/~amichelo/docs/text-est2.pdf)》。此处我只做一些关键扼要的理论推导 :-)
    > 
    > 多项式分布
    > -----
    > 
    > 回忆一下概率论学的东西，假设一个硬币正面朝上的概率是p
    > 
    > ，如果重复抛n次硬币，正面朝上的次数为k
    > 
    > 的概率分布就是二项分布，也就是
    > 
    > Cknpk(1-p)n-k
    > 
    > 如果抛n次k个不同的硬币，假设每个硬币正面朝上的概率分别是p1,p2,....,pk,那么抛n次之后，各个硬币正面朝上的次数n1,n2,....,nk的概率分布就是多项式分布了，记为
    > 
    > n!n1!n2!,....,nk!p1n1p2n2....pknk
    > 
    > LDA出来说话了：**主题和词汇的分布就是多项式分布**！因为一个主题里面不同词汇出现的概率不同，如果只有1个词汇，那么它就是二项分布，但是词汇不可能只有1个，所以它理所当然就是符合多项式分布。这是挺合理的假设，反正我们现在研究的内容是为词汇按主题给出不同的概率分布，其实也就是给出不同词汇在不同主题下的出现比例，我们并不关系词汇之间的顺序关系，所以多项式分布已经很好地刻画出这种关系了。LDA又说：**文章和主题之间的分布也是符合多项式分布**！因为一篇文章要确定不同主题的出现概率，和主题要确定每个词汇的出现概率是完全可以类比的！思考一下我们也接受了LDA的说法，接下来我们介绍一些记号：
    > 
    > -   V
    > 
    > -   代表我们字典的词汇个数-   K-   代表主题的个数-   M-   代表文章的个数-   ϕk→代表第k个主题的多项式分布参数，长度为V，因此Φ是一个K∗V-   的矩阵，每一行代表一个主题的多项式分布参数-   θm→代表第m篇文章的多项式分布参数，长度为K，因此Θ是一个M∗K-   的矩阵，没一行代表一篇文章的多项式分布参数-   Nm代表第m-   篇文章的长度-   zm,n代表第m篇文章第n-   个词由哪个主题产生的-   wm,n代表第m篇文章第n
    > 
    > -   个词
    > 
    > 对于第m
    > 
    > 篇文章，令z
    > 
    > 代表一次实验产生的主题随机变量，那么它就服从:
    > 
    > z∼Multi(z|θm→)\
    > 那么对于第k个主题，令w代表一次实验产生的词随机变量，那么它就服从：
    > 
    > w∼Multi(w|ϕk→)
    > 
    > 然后为了产生第m篇文章，只要简单的按顺序利用Multi(z|θm→)随机生成zm,1,zm,2,zm,3,...,zm,Nm，然后对号入座，再利用Multi(w|ϕzm,n→)，生成wm,1,wm,2,wm,3,...,wm,Nm即可。
    > 
    > Dirichlet分布
    > -----------
    > 
    > 忘记告诉大家，LDA属于江湖中的贝叶斯学派，在贝叶斯学派眼中，像上面提到的ϕk→
    > 
    > 和θm→
    > 
    > 都是随机变量，随机变量怎么可以没有先验概率分布呢？这岂不是贻笑大方吗？所以LDA整理了一下衣领，马上提出了他们的先验概率分布：
    > 
    > ϕ⃗ ∼Dirichlet(α⃗ )
    > 
    > 而
    > 
    > θ⃗ ∼Dirichlet(β⃗ )
    > 
    > 为什么LDA要说它的先验分布是Dirichlet分布呢？其中最大的原因是因为多项式分布和Dirichlet分布是一对共轭分布，共轭分布有什么好处呢？好处在于计算后验概率有极大的便利！说到底是LDA看中它计算方便。增加了先验概率分布，那么在确定文章与主题分布还有主题与词汇分布的时候，就由先验概率分布先随机生成确定多项式分布的参数。用一个联合概率分布来描述第m篇文章生成过程：
    > 
    > p(zm→,wm→,θm→,Φ|α⃗ ,β⃗ )=∏nNmp(wm,n|ϕzm,n→)p(zm,n|θm→)p(θm→|α⃗ )p(Φ|β⃗ )\
    > 对于习惯了使用极大似然法的同学，为了使用极大似然法，我们必须将隐含变量消除，那么对于第m篇文章其生成的边缘概率为：
    > 
    > p(wm→|α⃗ ,β⃗ )=∫θm∫Φ∫zm→∏nNmp(wm,n|ϕzm,n→)p(zm,n|θm→)p(θm→|α⃗ )p(Φ|β⃗ )=∫θm∫Φ∑zm→∏nNmp(wm,n|ϕzm,n→)p(zm,n|θm→)p(θm→|α⃗ )p(Φ|β⃗ )=∫θm∫Φ∑zm1∑zm2...∑zmNm∏nNmp(wm,n|ϕzm,n→)p(zm,n|θm→)p(θm→|α⃗ )p(Φ|β⃗ )=∫θm∫Φ∏nNm∑zmnp(wm,n|ϕzm,n→)p(zm,n|θm→)p(θm→|α⃗ )p(Φ|β⃗ )\
    > 以上可以看到，边缘概率分布实在是太复杂了，靠普通极大似然法来求解基本无望。不过这并不能难倒我们聪明的计算机科学家，下面我们来介绍一种近似求解法。
    > 
    > Gibbs 采样算法
    > ----------
    > 
    > ### 采样算法的思想
    > 
    > 对于一个概率分布p(x⃗ )
    > 
    > ，我们想得到它得概率分布，无奈有些概率分布形式实在复杂，我们无法直接求解，那么怎么办呢？假设我们的随机变量为：
    > 
    > x⃗ =[x1,x2,x3,...,xi,...,xn]\
    > 其中xi∈{0,1}，假设我们知道p(x⃗ )的概率分布，那么我们可以通过采样的方式得到每一次的样本值：
    > 
    > x⃗ (1)=[0,0,0,0,....0]x⃗ (2)=[1,1,0,0,....0]x⃗ (3)=[1,0,0,0,....0]x⃗ (4)=[1,1,0,0,....0].......x⃗ (N)=[1,1,0,0,....0]\
    > 那么我们可以统计每个样本出现的次数，然后除以总的采样次数N来得到相应概率分布。比如我们观察样本值[1,1,0,0,....]出现了K次，那么样本出现的概率就可以如下求得：
    > 
    > p(x1=1,x2=1,x3=0,....,xn=0)=KN\
    > 这是采样的基本思想，但是这里有令人匪夷所思的地方，首先我们不知道概率分布想得到概率分布我们必须通过采样方法来求得，但是采样方法又依赖于我们知道对应的概率分布才能得到相应的采样值，这是一个"鸡生蛋，蛋生鸡"的矛盾，足以令人百思不得其解，此时神奇的Gibbs采样更加令人充满敬畏。
    > 
    > ### 神奇的Gibbs采样
    > 
    > 实际应用中，我们通常是有一堆文章，然后要我们去自动提取主题，或者通过现有的文章训练出LDA模型，然后预测新的文章所属主题分类。也就是我们的兴趣点在于求出Θ
    > 
    > 和Φ
    > 
    > 的后验概率分布。虽然LDA的模型思想很简单，但是要精确求出参数的后验概率分布却是不可行的，只能通过近似的方式求解。幸好前人已经发现了很多近似求解方法，其中比较简单的就是Gibbs采样，Gibbs的采样精神很简单，对于一个很复杂的高维概率分布:
    > 
    > p(x⃗ )\
    > 我们想获得p(x⃗ )的样本，从而确定p(x⃗ )的参数值，也就是我们无法直接求取概率分布的参数，但是我们可以通过神奇的Gibbs采样，获得需要求解的概率分布的样本值，从而反过来确定概率分布。Gibbs采样很简单，它说如果你能很容易求解（通常都是很容易求解，因为此时的分布是一个一维的条件分布）
    > 
    > p(xi|x¬i→)\
    > 这样的条件分布，那么想获得联合分布的样本，只需执行如下过程：
    > 
    > -   随机初始化x⃗ 0={x01,x02,...,x0N}
    > 
    > -\
    >     -   对于 t=1,2,3,4,....T:
    > 
    >     -   xt1∼p(x1|xt-1¬1→)-\
    >     -   xt2∼p(x2|xt-1¬2→)-\
    >     -   xt3∼p(x3|xt-1¬3→)-\
    >     -   ....-   xtN∼p(xN|xt-1¬N→)-\
    >     -   得到一个样本值x⃗ (t)=[xt1,xt2,xt3,....,xtN]
    > 
    > -   -
    > 
    > 当采样过程收敛之后，通过以上采样得到的样本就是真实的 p(x⃗ )
    > 
    > 样本。为什么可以如此神奇地操作，再次推荐rickjin的《LDA数学八卦》！
    > 
    > Collapsed Gibbs Sampler
    > -----------------------
    > 
    > 对于LDA的Inference问题，有了万能的Gibbs采样算法，问题求解变得简单了。上面我们已经知道LDA模型的文档建模的联合分布：
    > 
    > p(zm→,wm→,θm→,Φ|α⃗ ,β⃗ )\
    > 为了采样方便，对于参数θm→，Φ，它们本身就是关联z⃗ 和w⃗ 的，也就是我们如果得到z⃗ 和w⃗ 的采样，参数θm→，Φ自然可以得知。那么可以积分化简，得到最终要采样的模型：
    > 
    > p(z⃗ ,w⃗ |α⃗ ,β⃗ )\
    > 有了联合分布，Gibbs万能算法就可以套用了，首先它必须先解决一个问题(为了表达方便，超参数α⃗ ,β⃗ 省略)：
    > 
    > p(zm,i|zm,¬i,wm→)
    > 
    > 其中zm→={zm,i＝k,zm,¬i}，zm,¬i代表第m篇文章里面去除主题zm,i的其他所有主题。其具体推导一开始推荐的文章都有详尽严格的过程，这里实在没有必要在赘述，直接给出结果(为了表达方便，这里去除下标m)：
    > 
    > p(zi=k|z¬i,w⃗ )=p(w⃗ ,z⃗ )p(w⃗ ,z¬i→)=p(w⃗ |z⃗ )p(w¬i|z¬i→)p(wi)p(z⃗ )p(z¬i)→∝p(w⃗ |z⃗ )p(w¬i|z¬i→)p(z⃗ )p(z¬i)→∝n(t)k,¬i+βt∑Vt=1n(t)k,¬i+βtn(k)m,¬i+αk∑Kk=1n(k)m,¬i+αk∝n(t)k,¬i+βt∑Vt=1n(t)k,¬i+βt(n(k)m,¬i+αk)
    > 
    > 其中n(t)k代表第m篇文章中词汇t属于主题k出现的次数，n(t)k,¬i代表除去其中zi的剩余个数，也就是说
    > 
    > n(t)k,¬i=n(t)k-1
    > 
    > 类似的，n(k)m代表第m篇文章中主题k出现的次数，n(k)m,¬i代表除去其中zi的剩余个数，也就是说
    > 
    > n(k)m,¬i=n(k)m-1
    > 
    > 所以计算p(zi|z¬i,w⃗ )变成简单地在计数的问题。通过Gibbs采样算法后，最后的模型参数可以这样得出：
    > 
    > ϕk,t=n(t)k+βt∑Vt=1n(t)k+βt
    > 
    > θm,k=n(k)m+αk∑Kk=1n(k)m+αk
    > 
    > 判断新文章的主题分布
    > ----------
    > 
    > 由上一小节，我们可以通过大量文章求解出LDA这个模型，那么对于一篇新的文章，如何计算它的主题分布呢？一个方式是将文章加入到原来的训练集合里面{z~⃗ ,z⃗ ;w~⃗ ,w⃗ }
    > 
    > ，然后得到它的采样条件概率为：
    > 
    > p(zi~=k|z~⃗ ¬i,z⃗ ,w⃗ ,w~⃗ )∝n(t)k+n~(t)k,¬i+βt∑Vt=1n(t)k+n~(t)k,¬i+βtn(k)m~,¬i+αk∑Kk=1n(k)m~,¬i+αk
    > 
    > 再重新跑一次Gibbs采样，然后得到它的分布。实际上这种做法确实是最优的，但是太慢了，怎么办呢？因为新来的文章，它的词汇是固定的，我们上节已经求出ϕk,t，也就是词汇和主题的分布已经是确定的，我们没必要再浪费计算力了，也就是我们认为对一篇新文章，它已经难以撼动之前成千上万文章的统计结果了，也就是说：
    > 
    > n(t)k+n~(t)k,¬i+βt∑Vt=1n(t)k+n~(t)k,¬i+βt≈n(t)k+βt∑Vt=1n(t)k+βt
    > 
    > 所以我们新的条件采样概率变成了：
    > 
    > p(zi~=k|w~i=t,z~⃗ ¬i,z⃗ ,w⃗ ,w~¬i→)∝ϕk,t∗(n(k)m~,¬i+αk)
    > 
    > 然后我们又可以开动Gibbs采样发动机，得到最终的分布结果：
    > 
    > θm~,k=n(k)m~+αk∑Kk=1n(k)m~+αk
    > 
    > LDA的Gibbs采样实现
    > =============
    > 
    > 对于程序员来说，看惯代码，没有代码有点无所适从，有没有简单LDA的实现漂亮代码呢？答案是有的，LingPipe里面的LatentDirichletAllocation这个类，完整地按照Gregor Heinrich有著名的《[Parameter estimation for text analysis](https://users.soe.ucsc.edu/~amichelo/docs/text-est2.pdf)》介绍的算法实现了，代码非常简单，并且可读性极高，建议抓来一看，必然大有毗益。此处我们贴出Gregor中提供的伪代码，以供查看：
    > 
    > -   初始化阶段，出乎意料的简单，只要初始化4个统计量，分别是:
    > 
    >     -   文档m
    > 
    > 对应主题k的计数： nkm-\
    >     -   文档m的词汇数：nm-\
    >     -   主题k对应的词汇为t的计数：ntk-\
    >     -   主题k的词汇数：nk-   -\
    >         -   将nkm,nm,ntk,nk内存清0，然后根据以下程序随机初始化值：
    > 
    > -   遍历每一个文档m∈[1,M]
    > 
    > -   遍历每个词汇n∈[1,Nm]
    > 
    > -   从多项式分布Mult(1/K)
    > 
    > 得到一个采样值：zmn=k-\
    >     -   nkm=nkm+1-\
    >     -   nm=nm+1-\
    >     -   ntk=ntk+1-\
    >     -   nk=nk+1-   -   -   -\
    >                 -   Gibbs采样过程，以下是一个采样周期的执行过程：
    > 
    >     -   遍历每一个文档m∈[1,M]
    > 
    > -   遍历每个词汇n∈[1,Nm]
    > 
    > -   对于当前的wm,n
    > 
    > 的主题k对应的词汇t执行：
    > 
    > -   nkm=nkm-1
    > 
    > -\
    >     -   nm=nm-1-\
    >     -   ntk=ntk-1-\
    >     -   nk=nk-1-\
    >     -   根据p(zi=k|z¬i,w⃗ )获得一个采样值：k^=zm,n并执行：
    > 
    > -   nk^m=nk^m+1
    > 
    > -\
    >     -   nm=nm+1-\
    >     -   ntk^=ntk^+1-\
    >     -   nk^=nk^+1
    > 
    > -   -   -   -   -   -
    > 
    > 难以置信的简单，一般在收敛之前，需要跑一定数量的采样次数让采样程序大致收敛，这个次数一般称为：burnin period。我们希望从采样程序中获得独立的样本，但是显然以上的采样过程明显依赖上一个采样结果，那么我们可以在上一次采样后，先抛弃一定数量的采样结果，再获得一个采样结果，这样可以大致做到样本独立，这样真正采样的时候，总有一定的滞后次数，这样的样本与样本的间隔称为：SampleLag。
    > 
    > LDA为什么能work
    > ===========
    > 
    > 如果您反复读了前面反复强调的两篇LDA科普大作，并清楚了解它的实现细节，有一些问题可能会慢慢萦绕在心中，挥之不去------为什么LDA能够work？为什么LDA能产生如下结果：\
    > ![这里写图片描述](https://img-blog.csdn.net/20170831143634112?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYXdzMzIxNzE1MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)\
    > 为什么它的结果会这么神奇，每个主题下面的词分布基本符合我们的直觉。比如computers这个主题下面的词汇分布是"computer，model，information，data，......"。\
    > 前面我们提到，LDA模型生成过程很简单，基本上是极其naive的，但是为什么它就能产生这样符合直觉的结果呢？（虽然说从直觉上，判断一篇文章的主题，即使文章词的顺序打乱了，我们还是能大致判断主题的，也就是LDA这种BOW模型有它的合理性，但是这并不能解释它为什么能产生如上结果）
    > 
    > 现在我们再回顾一下，对于LDA模型，我们推断的目标是它背后的隐结构，也就是"文档-主题分布"和"主题-词汇分布"，那么我们再来仔细观察它的后验概率分布（原谅我为了表达方便，改变了一些记号）：
    > 
    > p(z|w,θ)∝p(w,z,θ|α)=∏mp(θm|α)∏np(zmn|θm)p(wmn|zmn,Φ)\
    > 首先需要明确的是**隐变量的后验概率分布是正比于联合概率分布**的。在极大似然法中，**我们会希望模型越接近实际越好，也就是模型在数据上的概率越大越好**。我们先只考虑上面表达式的数据似然项p(wmn|zmn,Φ)，为了使这一似然项越大越好，我们会希望某个**主题下对应的词的概率越大越好**，由于主题-词汇分布由Φ决定，理想情况下，我们希望Φ矩阵应该是长下面这个样子：\
    > ![这里写图片描述](https://img-blog.csdn.net/20170831181756008?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYXdzMzIxNzE1MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)\
    > 横向代表主题，总共有K行，列向代表词汇，总共有V列。
    > 
    > 我们希望每个主题的词汇概率质量如上图蓝色方块所示（方块的概率和为1），也就是词汇按照主题个数不重叠地切割，这样可以保证词汇在所属主题下概率值最大，因为每一行概率和为1，我们希望概率密度集中在某些词上面，而不是分散地落在每个词上面（请读者思考一下为什么这样会使最终的概率值增大，这里比较难以用文字表达清楚，可以设想一下，假如每个主题的概率密度均匀分配到每个词上面，那么最终每一项p(wmn|zmn,Φ)
    > 
    > 会很小，这与我们的愿望是违背的）。为了使模型在数据上的概率最大，算法会倾向于将主题词汇分布按照上图的形式拟合，也就是"主题-词汇"分布会倾向于成为一个稀疏的分布。
    > 
    > 有了上面的讨论，我们再来想想，每个主题会选哪些词汇作为自己的主题词呢？ 也就是主题应该选哪些词来将自己的概率质量散落在他们身上。答案是那些经常出现在一起的词。假设主题A下面有主题词：a1,a2,...,an
    > 
    > ，为了使概率值变大，那么这些词一定是同时出现在很多个文档里面，并且在多个文档中，这些词大部分都同时出现。可以想想为什么要这样，假设不是这样，比如在文档1种主题A的词汇是a1,a2,a3,a4，在文档2中主题A的词汇是a5,a6,a7,a8，在文档3中主题A的词汇是a9,a10,a11,a12
    > 
    > ，以此类推，如果主题A的词汇真的是这个样子------文档中同一主题都没有在另一个文档中出现，那么主题A下面的词会很多，但是我们上面分析了，为了使模型概率值大，每个主题下面的词必须越少越好，所以这也是有违背愿望的。因此**主题下面的词都会倾向于同时出现在多个文档中**，到这里为止，读者应该可以大概明白为什么LDA可以产生那么符合直觉的词汇分布了，因为在我们人类自己的概念中，主题词汇就是这样的东西，他们会经常一起出现，比如"银行"，"存款"这些金融主题词汇会很频繁同时出现在多个场合中，所以我们会将他们归为一个主题，而LDA恰恰能捕获这种特性。
    > 
    > Edwin Chen的博客《[Introduction to Latent Dirichlet Allocation](http://blog.echen.me/2011/08/22/introduction-to-latent-dirichlet-allocation/)》也比较直观地介绍了LDA的直觉特性。至于怎么从理论上来说明为什么具有稀疏性质， [Quora上面有一个相对直观的解释](https://www.quora.com/Why-does-LDA-work)，我大概总结一下，由于LDA用Dirichlet作为Prior分布，而作为Prior的Dirichlet在其分布参数α⃗ 
    > 
    > 取很小的时候（一般α取K/50, β
    > 
    > 取值0.01），可以使得其采样的多项式参数变得稀疏。LDA有两对稀疏对抗，主题与文档的稀疏性和主题与词汇的稀疏性之间的对抗，而LDA会从数据中学习到一个权衡结果。为什么Dirichlet会有稀疏性质呢？可以参照以这篇：\
    > 《[Notes on Multinomial sparsity and the Dirichlet concentration parameter α](http://www.cs.cmu.edu/~dbamman/notes/dirichletConcentration.pdf)》\
    > 这篇note提到的Dirichlet其实可以看成几个Gamma分布变换而来，具体变换证明可以参照Quora另一个解答：[Construction of Dirichlet distribution with Gamma distribution](http://stats.stackexchange.com/questions/36093/construction-of-dirichlet-distribution-with-gamma-distribution)。另一个好处是，多了先验分布的模型比pLSA更加健壮，不容易导致overfiting，如果看回上面推导Gibbs Sampling的公式，Dirichlet其实起到一种Smooth的效果。可以再参考Kevin Gimpel写的《[Modeling Topics](http://www.cs.cmu.edu/~nasmith/LS2/gimpel.06.pdf)》，对于几种常见基础的主题模型的对比，也可以解除不少困惑。
    > 
    > 参考文献
    > ====
    > 
    > -   《[LDA数学八卦](http://www.52nlp.cn/author/rickjin)》
    > -   《[Parameter estimation for text analysis](https://users.soe.ucsc.edu/~amichelo/docs/text-est2.pdf)》
    > -   《[gibbs sampling for the uninitiated](http://wwwold.cs.umd.edu/~hardisty/papers/gsfu.pdf)》
    > -   《[text mining and topic models](http://cseweb.ucsd.edu/~elkan/250B/topicmodels.pdf)》
    > -   《[A Theoretical and Practical Implementation Tutorial on Topic Modeling and Gibbs Sampling](http://u.cs.biu.ac.il/~89-680/darling-lda.pdf)》
    > -   《[Probabilistic Latent Semantic Analysis](http://dl.acm.org/citation.cfm?id=2073829)》
    > -   [LingPipe](http://alias-i.com/lingpipe/)
    > -   《[Modeling Topics](http://www.cs.cmu.edu/~nasmith/LS2/gimpel.06.pdf)》
    > -   《[Notes on Multinomial sparsity and the Dirichlet concentration parameter α](http://www.cs.cmu.edu/~dbamman/notes/dirichletConcentration.pdf)》
    > -   [Why does LDA works？](https://www.quora.com/Why-does-LDA-work)
    > -   [Construction of Dirichlet distribution with Gamma distribution](http://stats.stackexchange.com/questions/36093/construction-of-dirichlet-distribution-with-gamma-distribution)
    > -   Dave Blei's video lecture on topic models: <http://videolectures.net/mlss09uk_blei_tm>

- [Conjugate prior - Wikiwand](https://www.wikiwand.com/en/Conjugate_prior)

    > Example
    > -------
    > 
    > The form of the conjugate prior can generally be determined by inspection of the [probability density](https://www.wikiwand.com/en/Probability_density_function) or [probability mass function](https://www.wikiwand.com/en/Probability_mass_function) of a distribution. For example, consider a [random variable](https://www.wikiwand.com/en/Random_variable) which consists of the number of successes ![s](https://wikimedia.org/api/rest_v1/media/math/render/svg/01d131dfd7673938b947072a13a9744fe997e632) in ![n](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) [Bernoulli trials](https://www.wikiwand.com/en/Bernoulli_trial) with unknown probability of success ![q](https://wikimedia.org/api/rest_v1/media/math/render/svg/06809d64fa7c817ffc7e323f85997f783dbdf71d) in [0,1]. This random variable will follow the [binomial distribution](https://www.wikiwand.com/en/Binomial_distribution), with a probability mass function of the form
    > 
    > ![{\displaystyle p(s)={n \choose s}q^{s}(1-q)^{n-s))](https://wikimedia.org/api/rest_v1/media/math/render/svg/db06457d8f50347a044b7672740227e722331976)
    > 
    > The usual conjugate prior is the [beta distribution](https://www.wikiwand.com/en/Beta_distribution) with parameters (![\alpha ](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3), ![\beta ](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8)):
    > 
    > ![p(q)={q^{\alpha -1}(1-q)^{\beta -1} \over \mathrm {B} (\alpha ,\beta )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c924d010fed83e219416a1ffb41331aa429ada9c)
    > 
    > where ![\alpha ](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3) and ![\beta ](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8) are chosen to reflect any existing belief or information (![\alpha ](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3) = 1 and ![\beta ](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8) = 1 would give a [uniform distribution](https://www.wikiwand.com/en/Uniform_distribution_(continuous) "Uniform distribution (continuous)")) and *Β*(![\alpha ](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3), ![\beta ](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8)) is the [Beta function](https://www.wikiwand.com/en/Beta_function) acting as a [normalising constant](https://www.wikiwand.com/en/Normalising_constant).
    > 
    > In this context, ![\alpha ](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3) and ![\beta ](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8) are called *[hyperparameters](https://www.wikiwand.com/en/Hyperparameter)* (parameters of the prior), to distinguish them from parameters of the underlying model (here *q*). It is a typical characteristic of conjugate priors that the dimensionality of the hyperparameters is one greater than that of the parameters of the original distribution. If all parameters are scalar values, then this means that there will be one more hyperparameter than parameter; but this also applies to vector-valued and matrix-valued parameters. (See the general article on the [exponential family](https://www.wikiwand.com/en/Exponential_family), and consider also the [Wishart distribution](https://www.wikiwand.com/en/Wishart_distribution "Wishart distribution"), conjugate prior of the [covariance matrix](https://www.wikiwand.com/en/Covariance_matrix) of a [multivariate normal distribution](https://www.wikiwand.com/en/Multivariate_normal_distribution), for an example where a large dimensionality is involved.)
    > 
    > If we then sample this random variable and get *s* successes and *f* failures, we have
    > 
    > ![{\displaystyle {\begin{aligned}P(s,f\mid q=x)&={s+f \choose s}x^{s}(1-x)^{f},\\P(x)&={x^{\alpha -1}(1-x)^{\beta -1} \over \mathrm {B} (\alpha ,\beta )},\\P(q=x\mid s,f)&={\frac {P(s,f\mid x)P(x)}{\int P(s,f\mid x)P(x)dx))\\&=(({s+f \choose s}x^{s+\alpha -1}(1-x)^{f+\beta -1}/\mathrm {B} (\alpha ,\beta )} \over \int _{y=0}^{1}\left({s+f \choose s}y^{s+\alpha -1}(1-y)^{f+\beta -1}/\mathrm {B} (\alpha ,\beta )\right)dy}\\&={x^{s+\alpha -1}(1-x)^{f+\beta -1} \over \mathrm {B} (s+\alpha ,f+\beta )},\\\end{aligned))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cb14cab68a14e4ae9b49c0d3acea79ecf00c97ca)
    > 
    > which is another Beta distribution with parameters (![\alpha ](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3) + *s*, ![\beta ](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8) + *f*). This posterior distribution could then be used as the prior for more samples, with the hyperparameters simply adding each extra piece of information as it comes.

### 用 neural network 加速 LDA 推論

- [[1508.01011] Learning from LDA using Deep Neural Networks](https://arxiv.org/abs/1508.01011)


### LDA2vec

- [[1605.02019] Mixing Dirichlet Topic Models and Word Embeddings to Make lda2vec](https://arxiv.org/abs/1605.02019)

- [Introducing our Hybrid lda2vec Algorithm | Stitch Fix Technology – Multithreaded](https://multithreaded.stitchfix.com/blog/2016/05/27/lda2vec/#topic=38&lambda=1&term=)

    ![](https://multithreaded.stitchfix.com/assets/posts/2016-05-27-lda2vec/lda2vec_network_publish_text_header.gif)

- [How to easily do Topic Modeling with LSA, PSLA, LDA & lda2Vec](https://medium.com/nanonets/topic-modeling-with-lsa-psla-lda-and-lda2vec-555ff65b0b05)

- [《Mixing Dirichlet Topic Models and Word Embeddings to Make lda2vec》阅读笔记](https://zhuanlan.zhihu.com/p/23767128)

- [LDA2vec: Word Embeddings in Topic Models (article) - DataCamp](https://www.datacamp.com/community/tutorials/lda2vec-topic-model)


### DSSM

#### 原理

- [A Latent Semantic Model with Convolutional-Pooling Structure for Information Retrieval - Microsoft Research](https://www.microsoft.com/en-us/research/publication/a-latent-semantic-model-with-convolutional-pooling-structure-for-information-retrieval/)


- [DSSM - Microsoft Research](https://www.microsoft.com/en-us/research/project/dssm/)


- [炼丹师读源码之细究DSSM Embedding实现](https://zhuanlan.zhihu.com/p/37082976)


- [用于Sentence Embedding的DSSM与LSTM：管中窥豹 – D&C](https://boweihe.me/2016/08/26/dssm%E4%B8%8Elstm/)


- [学习记录一下深度语义匹配模型-DSSM | Kubi Code'Blog](http://kubicode.me/2017/04/21/Deep%20Learning/Study-With-Deep-Structured-Semantic-Model/)

- [Deep Learning for Web Search and Natural Language Processing - wsdm2015.v3.pdf](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/wsdm2015.v3.pdf)



#### 實作

- [airalcorn2/Deep-Semantic-Similarity-Model: My Keras implementation of the Deep Semantic Similarity Model (DSSM)/Convolutional Latent Semantic Model (CLSM) described here: http://research.microsoft.com/pubs/226585/cikm2014_cdssm_final.pdf.](https://github.com/airalcorn2/Deep-Semantic-Similarity-Model)

- [Model DSSM on Tensorflow](https://liaha.github.io/models/2016/06/21/dssm-on-tensorflow.html)
    - [liaha/dssm](https://github.com/liaha/dssm)



### TopicRNN

- [TopicRNN: A Recurrent Neural Network with Long-Range Semantic Dependency阅读笔记](https://zhuanlan.zhihu.com/p/27151433)

    - [[1611.01702] TopicRNN: A Recurrent Neural Network with Long-Range Semantic Dependency](https://arxiv.org/abs/1611.01702)

    > ![](https://pic1.zhimg.com/v2-8876dcef7d93048672d0b47f94cea481_r.jpg)
    > 
    > ![](https://pic1.zhimg.com/v2-994789251b56dad24d19e292b89de36c_r.jpg)




### TreeRNN(TreeLSTM)

- [[1503.00075] Improved Semantic Representations From Tree-Structured Long Short-Term Memory Networks](https://arxiv.org/abs/1503.00075)


- [基于TreeLSTM的情感分析](https://zhuanlan.zhihu.com/p/35252733)


- [machine learning - How can a tree be encoded as input to a neural network? - Stack Overflow](https://stackoverflow.com/questions/26022866/how-can-a-tree-be-encoded-as-input-to-a-neural-network)

    > You need a **recursive neural network**. Please see this repository for an example implementation: <https://github.com/erickrf/treernn>
    > 
    > The principle of a recursive (not recurrent) neural network is shown in this picture.
    > 
    > It learns representation of each leaf, and then goes up through the parents to finally construct the representation of the whole structure. [![enter image description here](https://i.stack.imgur.com/1BW1F.png)](https://i.stack.imgur.com/1BW1F.png)
    > 
    > ---
    > 
    > Encode each leaf node using (i) the sequence of nodes that connects it to the root node and (ii) the encoding of the leaf node that comes before it.
    > 
    > For (i), use a recurrent network whose input is tags. Feed this RNN the root tag, the second level tag, ..., and finally the parent tag (or their embeddings). Combine this with the leaf itself (the word or its embedding). Now, you have a feature that describes the leaf and its ancestors.
    > 
    > For (ii), also use a recurrent network! Simply start by computing the feature described above for the left most leaf and feed it to a second RNN. Keep doing this for each leaf moving from left to right. At each step, the second RNN will give you a vector that represents the current leaf with its ancestors, the leaves that come before it and their ancestors.
    > 
    > Optionally, do (ii) bi-directionally and you will get a leaf feature that incorporates the whole tree!


### Recursive RNN 與 Recurrent RNN 比較

- [在NLP中深度学习模型何时需要树形结构？ - 人工智能 - 掘金](https://juejin.im/entry/5ad838805188252ea02c0bb5)

    - [[1503.00185] When Are Tree Structures Necessary for Deep Learning of Representations?](https://arxiv.org/abs/1503.00185)

    > 该文在NLP领域中4种类型5个任务进行了实验，具体的实验数据大家可以从论文中查阅，这里我主要分析一下每个任务的特点，以及最后实验的结果：
    > 
    > - Sentiment Classification on the Stanford Sentiment Treebank
    > 
    >     这是一个细粒度的情感分类问题，根据Stanford的句法树库，在每一个节点上都标注了情感类型，所以实验分为了句子级别和短语级别，从结果来看，树形结构对于句子级别有点帮助，对于短语级别并没什么作用。
    > 
    > - Binary Sentiment Classification
    > 
    >     这同样是一个情感分类问题，与上面不同的是，它只有二元分类，并且只有在句子级别上进行了标注，且每个句子都比较长。实验结果是树形结构并没有起到什么作用，可能原因是句子较长，而且并没有丰富的短语级别标注，导致在长距离的学习中丢失了学习到的情感信息。
    > 
    > - Question-Answer Matching
    > 
    >     这个任务是机智问答，就是给出一段描述一般由4~6句组成，然后根据描述给出一个短语级别的答案，例如地名，人名等。在这个任务上，树形结构也没有发挥作用。
    >     
    > - Semantic Relation Classification
    > 
    >     这个任务是给出两个句子中的名词，然后判断这两个名词是什么语义关系。树形结构的方法在这个任务上有明显的提升。
    >     
    > - Discourse Parsing
    > 
    >     是一个分类任务，特点是其输入的单元很短，树形结构也没有什么效果。
    > 
    > ## 结论
    > 
    > 通过上面的实验，作者总结出下面的结论。
    > 
    > 需要树形结构：
    > 
    > 1. 需要长距离的语义依存信息的任务（例如上面的语义关系分类任务）Semantic relation extraction
    > 2. 输入为长序列，即复杂任务，且在片段有足够的标注信息的任务（例如句子级别的Stanford情感树库分类任务），此外，实验中作者还将这个任务先通过标点符号进行了切分，每个子片段使用一个双向的序列模型，然后总的再使用一个单向的序列模型得到的结果比树形结构的效果更好一些。
    > 
    > 不需要树形结构：
    > 
    > 1. 长序列并且没有足够的片段标注任务（例如上面的二元情感分类，Q-A Matching任务）
    > 2. 简单任务（例如短语级别的情感分类和Discourse分析任务），每个输入片段都很短，句法分析可能没有改变输入的顺序。
    > 
    > 此外，哈工大的车万翔在哈工大的微信公众号也发表了《自然语言处理中的深度学习模型是否依赖于树结构？》[3]，其中提到了"即使面对的是复杂问题，只要我们能够获得足够的训练数据"也可以无需树形结构。
    > 
    > 通过这篇论文和车老师的博文以及一些相关资料，句法树形结构是否需要值得我们关注，我们应该根据自己做的任务以及句法分析的优缺点进行判断，我自己总结如下：
    > 
    > 句法分析能够带给我们什么？
    > 
    > - 长距离的语义依赖关系
    > - 包含语言学知识的序列片段
    > - 简化复杂句子提取核心
    > 
    > 句法分析的缺点
    > 
    > - 自身分析存在错误，引入噪声
    > - 简单任务复杂化
    > - 句法分析时间长
    > 

- [cs224n-2018-lecture14-TreeRNNs - lecture14.pdf](http://web.stanford.edu/class/cs224n/lectures/lecture14.pdf)

    > ![](https://screenshotscdn.firefoxusercontent.com/images/3cae62c7-0187-430c-ace7-3d06d7916c32.png)
    > 
    > ![](https://screenshotscdn.firefoxusercontent.com/images/a4c3699b-8329-41be-bdd5-435672db5d05.png)
    > 
    > ![](https://screenshotscdn.firefoxusercontent.com/images/40460542-2e9f-43c1-aa64-cd2cb9c405f4.png)
    > 
    > ![](https://screenshotscdn.firefoxusercontent.com/images/09f57e08-4475-4a29-8444-f47472718a88.png)
    > 
    > ![](https://screenshotscdn.firefoxusercontent.com/images/612baa6f-7b85-49f5-ae4e-1b3d2ea6364f.png)
    > 

### Tree-Based CNN

- [[1409.5718] Convolutional Neural Networks over Tree Structures for Programming Language Processing](https://arxiv.org/abs/1409.5718)

- [[1504.01106] Discriminative Neural Sentence Modeling by Tree-Based Convolution](https://arxiv.org/abs/1504.01106)

- [[1512.08422] Natural Language Inference by Tree-Based Convolution and Heuristic Matching](https://arxiv.org/abs/1512.08422)



### Neural Bag-of-Ngrams

- [Neural Bag-of-Ngrams - Association for the Advancement of Artificial ...](https://www.aaai.org/ocs/index.php/AAAI/AAAI17/paper/download/14513/14079)

- [libofang/Neural-BoN: code for AAAI-17 paper "Neural Bag-of-Ngrams"](https://github.com/libofang/Neural-BoN)

- [Neural Bag-of-Ngrams - CSDN博客](https://blog.csdn.net/qq_22548549/article/details/78213004)

    > 该文一共提出了三种ngram向量创建的方法。分别是Context guided N-gram representation, Text Guided N-gram representation以及Label guided N-gram representation. 其中前两个模型都是无监督的，最后一个模型是监督算法，需要对文本打标签。\
    > ![](https://img-blog.csdn.net/20171012123832474?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjI1NDg1NDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
    > 
    > Context guided N-gram representation
    > ------------------------------------
    > 
    > Context guided N-gram representation简称CGNR，借鉴的是Skip-gram模型生成词向量的方法。CGNR用当前ngram向量预测其上下文中的ngram向量。其形式化表示如下\
    > ![](https://img-blog.csdn.net/20171012124622467?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjI1NDg1NDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)\
    > 其中g表示其是第i篇文章第j个ngram，vg是其对应的向量，c表示g的第q个上下文中的ngram。其中上下文集合表示如下\
    > ![](https://img-blog.csdn.net/20171012124917166?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjI1NDg1NDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)\
    > 其中win是上下文窗口的大小，m是最大的gram值。上下文集合创建的例子如下图所示\
    > ![](https://img-blog.csdn.net/20171012125347703?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjI1NDg1NDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)\
    > 其中绿色表示目标gram，蓝色表示该gram的上下文集合，gram最大值是3，即包含1gram, 2gram和3gram。\
    > CGNR依然存在一些问题，因为有相似上下文的词它们的词义不一定相似，可能刚好相反，如词"good"和"bad"。所以作者又提出了Text Guided N-gram representation以及Label guided N-gram representation.
    > 
    > Text Guided N-gram representation
    > ---------------------------------
    > 
    > 一般而言，同一篇文章里出现的词，他们的词义也是相似的，尤其是有关评论的文章里，经常会出现"good", "not bad"等词。他们所表达的词义是一样的。因此，该文提出要用ngram向量预测该ngram所属的文本，形式化表述如下\
    > ![](https://img-blog.csdn.net/20171012130421982?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjI1NDg1NDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)\
    > 其中ti表示第i篇文档。TGNR模型适合于长文本，比如在一篇消极的电影影评中，可能会同时出现"terrible", "waste of time"等词，TGNR模型能将这些词聚集在一起，而对于短文本，可能并不会出现这么多词。由此，该文进一步提出了Label guided N-gram representation模型。
    > 
    > Label guided N-gram representation
    > ----------------------------------
    > 
    > 当词"good"和"perfect"出现在不同的文档里是，CGNR和TGNR可能都不能达到较好的效果。但是当两篇文档归属于同一个标签时，其中的词可能具有相似的语义。由此该文提出了Label guided N-gram representation方法，用当前ngram预测其所属的文档的标签，形式化表示如下\
    > ![](https://img-blog.csdn.net/20171012131351485?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjI1NDg1NDk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)\
    > 相对而言，LGNR更适合短文本。


### Neural Network 處理動態長度的方法

- [machine learning - How can neural networks deal with varying input sizes? - Artificial Intelligence Stack Exchange](https://ai.stackexchange.com/questions/2008/how-can-neural-networks-deal-with-varying-input-sizes)

    > Others already mentioned:
    > 
    > - zero padding
    > - RNN
    > - recursive NN
    > - using convolutions different number of times depending on the size of input. 




### CNN 在句子建模上的应用

- [卷积神经网络(CNN)在句子建模上的应用 | Jey Zhang](http://www.jeyzhang.com/cnn-apply-on-modelling-sentence.html)

#### Kim Y’s Paper

- [Implementing a CNN for Text Classification in TensorFlow – WildML](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow/)

- [dennybritz/cnn-text-classification-tf: Convolutional Neural Network for Text Classification in Tensorflow](https://github.com/dennybritz/cnn-text-classification-tf)

- [[Deep Learning] Convolution Neural Network on NLP](https://unilight.github.io/2017/07/04/Convolution-Neural-Network-on-NLP/)

- [Convolutional Methods for Text – Tal Perry – Medium](https://medium.com/@TalPerry/convolutional-methods-for-text-d5260fd5675f)

- [Understanding Convolutional Neural Networks for NLP – WildML](http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/)


- [How Quid uses deep learning with small data](https://quid.com/feed/how-quid-uses-deep-learning-with-small-data)

    - [[1408.5882v2] Convolutional Neural Networks for Sentence Classification](https://arxiv.org/abs/1408.5882v2)

    > ![](https://d15wj1jyee7mbq.cloudfront.net/cnnpic.png?mtime=20161117183048)
    > 
    > ![](https://d15wj1jyee7mbq.cloudfront.net/results.png?mtime=20161117180824)
    > 
    > we managed to achieve near the same level of performance with an approach based on deep learning as did we with an approach that relied on fancy manual feature engineering, even for very small data.
    > 
    > ---
    > 
    > A downfall of CNNs for text is that unlike for images, the input sequences are varying sizes (i.e., varying size sentences), which means most text inputs must be “padded” with some number of 0’s, so that all inputs are the same size. This means that a particularly long sentence will have many fewer zeros than most sentences, and, the model may act unpredictably in this context.
    > 
    > ---
    > 
    > The take-away here, though, is that you can do deep learning with a very low number of training examples and still get tangible benefits in model performance and representational efficiency over manual feature engineering.
    > 

### DCNN 

- [[1404.2188] A Convolutional Neural Network for Modelling Sentences](https://arxiv.org/abs/1404.2188)

- [卷积神经网络(CNN)在句子建模上的应用 | Jey Zhang](http://www.jeyzhang.com/cnn-apply-on-modelling-sentence.html)

    > Kal的这篇文章引用次数较高，他提出了一种名为DCNN(Dynamic Convolutional Neural Network)的网络模型，在上一篇（Kim's Paper）中的实验结果部分也验证了这种模型的有效性。这个模型的精妙之处在于Pooling的方式，使用了一种称为 **`动态Pooling`** 的方法。
    > 
    > 下图是这个模型对句子语义建模的过程，可以看到底层通过组合邻近的词语信息，逐步向上传递，上层则又组合新的Phrase信息，从而使得句子中即使相离较远的词语也有交互行为（或者某种语义联系）。从直观上来看，这个模型能够通过词语的组合，提取出句子中重要的语义信息（通过Pooling），某种意义上来说，层次结构的 **`feature graph`** 的作用类似于一棵语法解析树。
    > 
    > [![](http://i.imgur.com/3IbLJX4.png)](http://i.imgur.com/3IbLJX4.png)
    > 
    > DCNN能够处理可变长度的输入，网络中包含两种类型的层，分别是**一维的卷积层**和**动态k-max的池化层(Dynamic k-max pooling)**。其中，动态k-max池化是最大化池化更一般的形式。之前LeCun将CNN的池化操作定义为一种非线性的抽样方式，返回一堆数中的最大值，原话如下：
    > 
    > > The max pooling operator is a non-linear subsampling function that returns the maximum of a set of values (LuCun et al., 1998).
    > 
    > 而文中的k-max pooling方式的一般化体现在：
    > 
    > -   pooling的结果不是返回一个最大值，而是返回k组最大值，这些最大值是原输入的一个子序列；
    > -   pooling中的参数k可以是一个动态函数，具体的值依赖于输入或者网络的其他参数；
    > 
    > #### 模型结构及原理
    > 
    > DCNN的网络结构如下图：
    > 
    > [![](http://i.imgur.com/CNMa0VL.png)](http://i.imgur.com/CNMa0VL.png)
    > 
    > 网络中的卷积层使用了一种称之为 **`宽卷积(Wide Convolution)`** 的方式，紧接着是动态的k-max池化层。中间卷积层的输出即`Feature Map`的大小会根据输入句子的长度而变化。下面讲解一下这些操作的具体细节：
    > 
    > **1\. 宽卷积**
    > 
    > 相比于传统的卷积操作，宽卷积的输出的`Feature Map`的宽度(width)会更宽，原因是卷积窗口并不需要覆盖所有的输入值，也可以是部分输入值（可以认为此时其余的输入值为0，即填充0）。如下图所示：
    > 
    > [![](http://i.imgur.com/YgM3Tsg.png)](http://i.imgur.com/YgM3Tsg.png)
    > 
    > 图中的右图即表示宽卷积的计算过程，当计算第一个节点即s1
    > 
    > 时，可以假使s1
    > 
    > 节点前面有四个输入值为0的节点参与卷积（卷积窗口为5）。明显看出，狭义上的卷积输出结果是宽卷积输出结果的一个子集。
    > 
    > **2\. k-max池化**
    > 
    > 给出数学形式化的表述是，给定一个k
    > 
    > 值，和一个序列p∈Rp(其中p≥k)，`k-max pooling`选择了序列p中的前k
    > 
    > 个最大值，这些最大值保留原来序列的次序（实际上是原序列的一个子序列）。
    > 
    > `k-max pooling`的好处在于，既提取除了句子中的较重要信息（不止一个），同时保留了它们的次序信息（相对位置）。同时，由于应用在最后的卷积层上只需要提取出k
    > 
    > 个值，所以这种方法允许不同长度的输入（输入的长度应该要大于k）。然而，对于中间的卷积层而言，池化的参数k
    > 
    > 不是固定的，具体的选择方法见下面的介绍。
    > 
    > **3\. 动态k-max池化**
    > 
    > 动态k-max池化操作，其中的k
    > 
    > 是`输入句子长度`和`网络深度`两个参数的函数，具体如下：
    > 
    > $$
    > K_{l}=\max \left( k_{top}, \left \lceil \frac {L-l}{L} s \right \rceil \right)
    > $$
    > 
    > 其中$l$
    > 
    > 表示当前卷积的层数（即第几个卷积层），L是网络中总共卷积层的层数；ktop为最顶层的卷积层pooling对应的k值，是一个固定的值。举个例子，例如网络中有三个卷积层，ktop=3，输入的句子长度为18；那么，对于第一层卷积层下面的pooling参数k1=12，而第二层卷积层对于的为k2=6，而k3=ktop=3
    > 
    > 。
    > 
    > 动态k-max池化的意义在于，从不同长度的句子中提取出相应数量的语义特征信息，以保证后续的卷积层的统一性。
    > 
    > **4\. 非线性特征函数**
    > 
    > pooling层与下一个卷积层之间，是通过与一些权值参数相乘后，加上某个偏置参数而来的，这与传统的CNN模型是一样的。
    > 
    > **5\. 多个Feature Map**
    > 
    > 和传统的CNN一样，会提出多个Feature Map以保证提取特征的多样性。
    > 
    > **6\. 折叠操作(Folding)**
    > 
    > 之前的宽卷积是在输入矩阵d×s
    > 
    > 中的每一行内进行计算操作，其中d是word vector的维数，s
    > 
    > 是输入句子的词语数量。而 **`Folding`** 操作则是考虑相邻的两行之间的某种联系，方式也很简单，就是将两行的vector相加；该操作没有增加参数数量，但是提前（在最后的全连接层之前）考虑了特征矩阵中行与行之间的某种关联。
    > 
    > #### 模型的特点
    > 
    > -   保留了句子中词序信息和词语之间的相对位置；
    > -   宽卷积的结果是传统卷积的一个扩展，某种意义上，也是n-gram的一个扩展；
    > -   模型不需要任何的先验知识，例如句法依存树等，并且模型考虑了句子中相隔较远的词语之间的语义信息；
    > 
    > #### 实验部分
    > 
    > **1\. 模型训练及参数**
    > 
    > -   输出层是一个类别概率分布（即softmax），与倒数第二层全连接；
    > -   代价函数为交叉熵，训练目标是最小化代价函数；
    > -   L2正则化；
    > -   优化方法：mini-batch + gradient-based (使用Adagrad update rule, Duchi et al., 2011)
    > 
    > **2\. 实验结果**
    > 
    > 在三个数据集上进行了实验，分别是(1)电影评论数据集上的情感识别，(2)TREC问题分类，以及(3)Twitter数据集上的情感识别。结果如下图：
    > 
    > [![](http://i.imgur.com/zuf2bSu.png)](http://i.imgur.com/zuf2bSu.png)
    > 
    > [![](http://i.imgur.com/6lWY7zC.png)](http://i.imgur.com/6lWY7zC.png)
    > 
    > [![](http://i.imgur.com/PX9N2JB.png)](http://i.imgur.com/PX9N2JB.png)
    > 
    > 可以看出，DCNN的性能非常好，几乎不逊色于传统的模型；而且，DCNN的好处在于不需要任何的先验信息输入，也不需要构造非常复杂的人工特征。


- [《A Convolutional Neural Network for Modelling Sentences 》阅读笔记](https://zhuanlan.zhihu.com/p/29925124)

    > 6 折叠操作
    > 
    > 之前的宽卷积是在输入矩阵d×s中的每一行内进行计算操作，其中d是word vector的维数，s是输入句子的词语数量。而Folding操作则是考虑相邻的两行之间的某种联系，方式也很简单，就是将两行的vector相加；该操作没有增加参数数量，但是提前（在最后的全连接层之前）考虑了特征矩阵中行与行之间的某种关联
    > 
    > ![](https://pic2.zhimg.com/80/v2-2917de002ed6a7d410de8e6ca46198fa_hd.jpg)
    > 
    > 传统CNN和加入folding后的词的表示。增强了表示能力：![\varphi(\sum_{i=1}^{3}\sum_{j=1}^{4}w_{ij}x_{ij})（左图） \\\varphi[\sum_{j=1}^{2}\varphi(\sum_{i=1}^{3}w_{ij}x_{ij})]+\varphi[\sum_{j=3}^{4}\varphi(\sum_{i=1}^{3}w_{ij}x_{ij})]（右图）](https://www.zhihu.com/equation?tex=%5Cvarphi%28%5Csum_%7Bi%3D1%7D%5E%7B3%7D%5Csum_%7Bj%3D1%7D%5E%7B4%7Dw_%7Bij%7Dx_%7Bij%7D%29%EF%BC%88%E5%B7%A6%E5%9B%BE%EF%BC%89+%5C%5C%5Cvarphi%5B%5Csum_%7Bj%3D1%7D%5E%7B2%7D%5Cvarphi%28%5Csum_%7Bi%3D1%7D%5E%7B3%7Dw_%7Bij%7Dx_%7Bij%7D%29%5D%2B%5Cvarphi%5B%5Csum_%7Bj%3D3%7D%5E%7B4%7D%5Cvarphi%28%5Csum_%7Bi%3D1%7D%5E%7B3%7Dw_%7Bij%7Dx_%7Bij%7D%29%5D%EF%BC%88%E5%8F%B3%E5%9B%BE%EF%BC%89)


- [自然语言处理中CNN模型几种常见的Max Pooling操作 - CSDN博客](https://blog.csdn.net/lujiandong1/article/details/52628953)

    > CNN是目前自然语言处理中和RNN并驾齐驱的两种最常见的深度学习模型。图1展示了在NLP任务中使用CNN模型的典型网络结构。一般而言，输入的字或者词用Word Embedding的方式表达，这样本来一维的文本信息输入就转换成了二维的输入结构，假设输入X包含m个字符，而每个字符的Word Embedding的长度为d，那么输入就是m*d的二维向量。
    > 
    > ![](https://img-blog.csdn.net/20160922223900354?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
    > 
    > 这里可以看出，因为NLP中的句子长度是不同的，所以CNN的输入矩阵大小是不确定的，这取决于m的大小是多少。卷积层本质上是个特征抽取层，可以设定超参数F来指定设立多少个特征抽取器（Filter），对于某个Filter来说，可以想象有一个k*d大小的移动窗口从输入矩阵的第一个字开始不断往后移动，其中k是Filter指定的窗口大小，d是Word Embedding长度。对于某个时刻的窗口，通过神经网络的非线性变换，将这个窗口内的输入值转换为某个特征值，随着窗口不断往后移动，这个Filter对应的特征值不断产生，形成这个Filter的特征向量。这就是卷积层抽取特征的过程。每个Filter都如此操作，形成了不同的特征抽取器。Pooling层则对Filter的特征进行降维操作，形成最终的特征。一般在Pooling层之后连接全联接层神经网络，形成最后的分类过程。
    > 
    > 可见，卷积和Pooling是CNN中最重要的两个步骤。下面我们重点介绍NLP中CNN模型常见的Pooling操作方法。
    > 
    > |CNN中的Max Pooling Over Time操作
    > 
    > MaxPooling Over Time是NLP中CNN模型中最常见的一种下采样操作。意思是对于某个Filter抽取到若干特征值，只取其中得分最大的那个值作为Pooling层保留值，其它特征值全部抛弃，值最大代表只保留这些特征中最强的，而抛弃其它弱的此类特征。
    > 
    > CNN中采用Max Pooling操作有几个好处：首先，这个操作可以保证特征的位置与旋转不变性，因为不论这个强特征在哪个位置出现，都会不考虑其出现位置而能把它提出来。对于图像处理来说这种位置与旋转不变性是很好的特性，但是对于NLP来说，这个特性其实并不一定是好事，因为在很多NLP的应用场合，特征的出现位置信息是很重要的，比如主语出现位置一般在句子头，宾语一般出现在句子尾等等，这些位置信息其实有时候对于分类任务来说还是很重要的，但是Max Pooling 基本把这些信息抛掉了。
    > 
    > 其次，MaxPooling能减少模型参数数量，有利于减少模型过拟合问题。因为经过Pooling操作后，往往把2D或者1D的数组转换为单一数值，这样对于后续的Convolution层或者全联接隐层来说无疑单个Filter的参数或者隐层神经元个数就减少了。
    > 
    >  再者，对于NLP任务来说，Max Pooling有个额外的好处；在此处，可以把变长的输入X整理成固定长度的输入。因为CNN最后往往会接全联接层，而其神经元个数是需要事先定好的，如果输入是不定长的那么很难设计网络结构。前文说过,CNN模型的输入X长度是不确定的，而通过Pooling操作，每个Filter固定取1个值，那么有多少个Filter，Pooling层就有多少个神经元，这样就可以把全联接层神经元个数固定住（如图2所示），这个优点也是非常重要的。
    > 
    > ![](https://img-blog.csdn.net/20160922223943493?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
    > 
    > 但是，CNN模型采取MaxPooling Over Time也有一些值得注意的缺点：首先就如上所述，特征的位置信息在这一步骤完全丢失。在卷积层其实是保留了特征的位置信息的，但是通过取唯一的最大值，现在在Pooling层只知道这个最大值是多少，但是其出现位置信息并没有保留；另外一个明显的缺点是：有时候有些强特征会出现多次，比如我们常见的TF.IDF公式，TF就是指某个特征出现的次数，出现次数越多说明这个特征越强，但是因为Max Pooling只保留一个最大值，所以即使某个特征出现多次，现在也只能看到一次，就是说同一特征的强度信息丢失了。这是Max Pooling Over Time典型的两个缺点。
    > 
    > 其实，我们常说"危机危机"，对这个词汇乐观的解读是"危险就是机遇"。同理，发现模型的缺点是个好事情，因为创新往往就是通过改进模型的缺点而引发出来的。那么怎么改进Pooling层的机制能够缓解上述问题呢？下面两个常见的改进Pooling机制就是干这个事情的。
    > 
    > |K-Max Pooling
    > 
    > K-MaxPooling的意思是：原先的Max Pooling Over Time从Convolution层一系列特征值中只取最强的那个值，那么我们思路可以扩展一下，K-Max Pooling可以取所有特征值中得分在Top --K的值，并保留这些特征值原始的先后顺序（图3是2-max Pooling的示意图），就是说通过多保留一些特征信息供后续阶段使用。
    > 
    > ![](https://img-blog.csdn.net/20160922224134153?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
    > 
    > 很明显，K-Max Pooling可以表达同一类特征出现多次的情形，即可以表达某类特征的强度；另外，因为这些Top K特征值的相对顺序得以保留，所以应该说其保留了部分位置信息，但是这种位置信息只是特征间的相对顺序，而非绝对位置信息。
    > 
    > |Chunk-Max Pooling
    > 
    > Chunk-MaxPooling的思想是：把某个Filter对应的Convolution层的所有特征向量进行分段，切割成若干段后，在每个分段里面各自取得一个最大特征值，比如将某个Filter的特征向量切成3个Chunk，那么就在每个Chunk里面取一个最大值，于是获得3个特征值。（如图4所示，不同颜色代表不同分段）
    > 
    > ![](https://img-blog.csdn.net/20160922224215779?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
    > 
    > 乍一看Chunk-Max Pooling思路类似于K-Max Pooling，因为它也是从Convolution层取出了K个特征值，但是两者的主要区别是：K-Max Pooling是一种全局取Top K特征的操作方式，而Chunk-Max Pooling则是先分段，在分段内包含特征数据里面取最大值，所以其实是一种局部Top K的特征抽取方式。
    > 
    > 至于这个Chunk怎么划分，可以有不同的做法，比如可以事先设定好段落个数，这是一种静态划分Chunk的思路；也可以根据输入的不同动态地划分Chunk间的边界位置，可以称之为动态Chunk-Max方法（这种称谓是我随手命名的，非正式称谓，请注意）。
    > 
    > Chunk-Max Pooling很明显也是保留了多个局部Max特征值的相对顺序信息，尽管并没有保留绝对位置信息，但是因为是先划分Chunk再分别取Max值的，所以保留了比较粗粒度的模糊的位置信息；当然，如果多次出现强特征，则也可以捕获特征强度。
    > 
    > Event Extraction via Dynamic Multi-Pooling Convolutional Neural Networks这篇论文提出的是一种ChunkPooling的变体，就是上面说的动态Chunk-Max Pooling的思路，实验证明性能有提升。Local Translation Prediction with Global Sentence Representation 这篇论文也用实验证明了静态Chunk-Max性能相对MaxPooling Over Time方法在机器翻译应用中对应用效果有提升。
    > 
    > 如果思考一下，就会发现，如果分类所需要的关键特征的位置信息很重要，那么类似Chunk-Max Pooling这种能够粗粒度保留位置信息的机制应该能够对分类性能有一定程度的提升作用；但是对于很多分类问题，估计Max-Pooling over time就足够了。
    > 
    > 比如我们拿情感分类来说，估计用Chunk-max策略应该有帮助，因为对于这种表达模式:
    > 
    > "Blablabla....表扬了你半天，BUT.....你本质上就是个渣"
    > 
    > 与这种表达模式
    > 
    > "虽然说你是个渣，但是.....Blablabla.....欧巴我还是觉得你最好，因为你最帅"
    > 
    > 明显位置信息对于判别整体情感倾向是有帮助作用的，所以引入位置信息应该有帮助。
    > 
    > 所以，你分析下你手头的问题，看看位置是不是重要特征，如果是，那么套用一下Chunk-Max策略，估计性能会有提升，比如上面举的情感分类问题估计效果会有提升。
    > 
    > **Pooling层的作用：**
    > 
    > **1\. 不变性，更关注是否存在某些特征而不是特征具体的位置。可以看作加了一个很强的先验，让学到的特征要能容忍一些的变化。**
    > 
    > **2\. 减小下一层输入大小，减小计算量和参数个数。\
    > 3\. 获得定长输出。（文本分类的时候输入是不定长的，可以通过池化获得定长输出）\
    > 4\. 防止过拟合或有可能会带来欠拟合。**
    > 

#### 實作

- [FredericGodin/DynamicCNN: Dynamic Convolutional Neural Networks for Theano/Lasagne](https://github.com/FredericGodin/DynamicCNN)

- [CNN与句子分类之动态池化方法DCNN--TensorFlow实现篇 - CSDN博客](https://blog.csdn.net/liuchonge/article/details/67644305)

- [tensorflow - Variable size Convolutional Neural Network Input and Fixed output - Stack Overflow](https://stackoverflow.com/questions/38628014/variable-size-convolutional-neural-network-input-and-fixed-output)

    > I know it's an old thread, but for people who are looking for a solution. It has been implemented in tensorflow 1.4.0
    > 
    > tf.nn.max_pool() now takes 1d tensor as an input as opposed to a list of ints in the older versions. So you can use a placeholder as the argument of ksize.


### Hu’s Paper

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
### He’s Paper

- [卷积神经网络(CNN)在句子建模上的应用 | Jey Zhang](http://www.jeyzhang.com/cnn-apply-on-modelling-sentence.html)

### Yin’s Paper

- [卷积神经网络(CNN)在句子建模上的应用 | Jey Zhang](http://www.jeyzhang.com/cnn-apply-on-modelling-sentence.html)


### Universal Sentence Encoder

- [通用句子語義編碼器，谷歌在語義文本相似性上的探索 - 幫趣](http://bangqu.com/gY7194.html)

    > **語義文本相似度**
    > 
    > 在「Learning Semantic Textual Similarity from Conversations」這篇論文中，我們引入一種新的方式來學習語義文本相似的句子表示。直觀的說，如果句子的回答分佈相似，則它們在語義上是相似的。例如，「你多大了？」以及「你的年齡是多少？」都是關於年齡的問題，可以通過類似的回答，例如「我 20 歲」來回答。相比之下，雖然「你好嗎？」和「你多大了？」包含的單詞幾乎相同，但它們的含義卻大相徑庭，所以對應的回答也相去甚遠。
    > 
    > 論文地址：https://arxiv.org/abs/1804.07754
    > 
    > ![](http://i2.bangqu.com/j/news/20180527/gY719415273972350175UWgr.png)
    > 
    > *如果句子可以通過相同的答案來回答，那麼句子在語義上是相似的。否則，它們在語義上是不同的。*
    > 
    > 這項工作中，我們希望通過給回答分類的方式學習語義相似性：給定一個對話輸入，我們希望從一批隨機選擇的回覆中分類得到正確的答案。但是，任務的最終目標是學習一個可以返回表示各種自然語言關係（包括相似性和相關性）的編碼模型。我們提出了另一預測任務（此處是指 SNLI 蘊含數據集），並通過共享的編碼層同時推進兩項任務。利用這種方式，我們在 STSBenchmark 和 CQA task B 等相似度度量標準上取得了更好的表現，究其原因，是簡單等價關係與邏輯蘊含之間存在巨大不同，後者爲學習複雜語義表示提供了更多可供使用的信息。
    > 
    > ![](http://i2.bangqu.com/j/news/20180527/gY71941527397235681nLm72.png)
    > 
    > *對於給定的輸入，分類可以認爲是一種對所有可能候選答案的排序問題。*
    > 
    > **通用句子編碼器**
    > 
    > 「Universal Sentence Encoder」這篇論文介紹了一種模型，它通過增加更多任務來擴展上述的多任務訓練，並與一個類似 skip-thought 的模型聯合訓練，從而在給定文本片段下預測句子上下文。然而，我們不使用原 skip-thought 模型中的編碼器 - 解碼器架構，而是使用一種只有編碼器的模型，並通過共享編碼器來推進預測任務。利用這種方式，模型訓練時間大大減少，同時還能保證各類遷移學習任務（包括情感和語義相似度分類）的性能。這種模型的目的是爲儘可能多的應用（釋義檢測、相關性、聚類和自定義文本分類）提供一種通用的編碼器。
    > 
    > 論文地址：https://arxiv.org/abs/1803.11175
    > 
    > ![](http://i2.bangqu.com/j/news/20180527/gY71941527397237211r96N9.png)
    > 
    > *成對語義相似性比較，結果爲 TensorFlow Hub 通用句子編碼器模型的輸出。*
    > 
    > 正如文中所說，通用句子編碼器模型的一個變體使用了深度平均網絡（DAN）編碼器，而另一個變體使用了更加複雜的自注意力網絡架構 Transformer。
    > 
    > ![](http://i2.bangqu.com/j/news/20180527/gY71941527397238079233wo.png)
    > 
    > *「Universal Sentence Encoder」一文中提到的多任務訓練。各類任務及結構通過共享的編碼層/參數（灰色框）進行連接。*
    > 
    > 隨着其體系結構的複雜化，Transformer 模型在各種情感和相似度分類任務上的表現都優於簡單的 DAN 模型，且在處理短句子時只稍慢一些。然而，隨着句子長度的增加，使用 Transformer 的計算時間明顯增加，但是 DAN 模型的計算耗時卻幾乎保持不變。
    > 
    > **新模型**
    > 
    > 除了上述的通用句子編碼器模型之外，我們還在 TensorFlow Hub 上共享了兩個新模型：大型通用句型編碼器通和精簡版通用句型編碼器。
    > 
    > -   大型：https://www.tensorflow.org/hub/modules/google/universal-sentence-encoder-large/1
    > 
    > -   精簡：https://www.tensorflow.org/hub/modules/google/universal-sentence-encoder-lite/1
    > 
    >  這些都是預訓練好的 Tensorflow 模型，給定長度不定的文本輸入，返回一個語義編碼。這些編碼可用於語義相似性度量、相關性度量、分類或自然語言文本的聚類。
    > 
    > 大型通用句型編碼器模型是用我們介紹的第二篇文章中提到的 Transformer 編碼器訓練的。它針對需要高精度語義表示的場景，犧牲了速度和體積來獲得最佳的性能。
    > 
    > 精簡版模型使用 Sentence Piece 詞彙庫而非單詞進行訓練，這使得模型大小顯著減小。它針對內存和 CPU 等資源有限的場景（如小型設備或瀏覽器）。
    > 
    > 我們很高興與大家分享這項研究以及這些模型。這只是一個開始，並且仍然還有很多問題亟待解決，如將技術擴展到更多語言上（上述模型目前僅支持英語）。我們也希望進一步地開發這種技術，使其能夠理解段落甚至整個文檔。在實現這些目標的過程中，很有可能會產生出真正的「通用」編碼器。
    > 
    > *原文鏈接：https://ai.googleblog.com/2018/05/advances-in-semantic-textual-similarity.html*


- [《Universal Sentence Encoder》论文分享](https://zhuanlan.zhihu.com/p/35174235)

    > 论文主要是提出了一个统一的句子编码框架，句子级别的encode比Word2vec使用起来会更加的方便，因为可以直接拿来做句子分类等任务。
    > 
    > 本文主要提出了两个句子encode的框架，一个是之前《attention is all you need》里面的一个encode框架，另一个是DAN（deep average network）的encode方式。两个的训练方式较为类似，都是通过多任务学习，将encode用在不同的任务上，包括分类，生成等等，以不同的任务来训练一个编码器，从而实现泛化的目的。
    > 
    > Transformer：
    > 
    > 第一个句子编码模型使用了transformer里面的一个子图，这个子图通过attention来一个句子中词语的context表示，同时考虑所有的词并将其转化为一个fixed length向量。具体了解可以去看那篇论文，这篇论文本身也没有给出具体的图。
    > 
    > ![](https://pic4.zhimg.com/80/v2-540dc62cdb5fe8939c5185a0eeb14c7b_hd.jpg)
    > 
    > DAN：
    > 
    > 第二个句子编码模型使用了较为简单的一个DAN模型（[Mohit Iyyer](https://link.zhihu.com/?target=http%3A//www.aclweb.org/anthology/P/P15/P15-1162.pdf)），通过对embedding求平均后输入到feed-forward network，然后不加softmax即可得到隐层表示，然后把这个向量类似于上面的方法，用多任务来进行训练模型。
    > 
    > ![](https://pic3.zhimg.com/80/v2-bb79f8465693d9834e45a616b6a53631_hd.jpg)
    > 
    > 论文之所以提出两个是考虑到模型的准确度和复杂程度，以及训练的资源消耗。
    > 
    > attention那个encode模型准确率高，但是模型复杂度高，训练时间长，消耗gpu资源多
    > 
    > 而DAN模型虽然准确度低，但是训练快，模型复杂度低。
    > 
    > 文中也给出了样例，有了一个初始训练好的模型，用户可以根据自己的需求再加入一些文本进行再次训练。（[使用地址](https://link.zhihu.com/?target=https%3A//www.tensorflow.org/hub/modules/google/universal-sentence-encoder/1)）
    > 
    > ![](https://pic4.zhimg.com/80/v2-51aac31df9e31c1d907171f20e96fc0f_hd.jpg)
    > 
    > 文中还提出了比较两个句子向量之间的相似度时候不用原生的cos距离，而是转化为弧度之后计算，效果要好于原生的：
    > 
    > ![](https://pic3.zhimg.com/80/v2-cb699c1869f91223cffe3d77cc524f79_hd.jpg)
    > 



