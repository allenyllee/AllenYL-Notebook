# NLP__資料蒐集2-1

[toc]
<!-- toc --> 

## 詞嵌入


### word2Vec

#### 原理

- [類神經網路 -- word2vec (part 1 : Overview) « MARK CHANG'S BLOG](http://cpmarkchang.logdown.com/posts/773062-neural-network-word2vec-part-1-overview)

- [理解 Word2Vec 之 Skip-Gram 模型](https://zhuanlan.zhihu.com/p/27234078)

- [Word2vec (中文)](https://www.slideshare.net/ywchen88/word2vec-70245972)


#### 實作

- [以 gensim 訓練中文詞向量 | 雷德麥的藏書閣](https://zake7749.github.io/2016/08/28/word2vec-with-gensim/)

- [zake7749/word2vec-tutorial: 中文詞向量訓練教學](https://github.com/zake7749/word2vec-tutorial)

- [使用tensorflow实现word2vec中文词向量的训练](https://zhuanlan.zhihu.com/p/28979653)

- [類神經網路 -- word2vec (part 1 : Overview) « MARK CHANG'S BLOG](http://cpmarkchang.logdown.com/posts/773062-neural-network-word2vec-part-1-overview)

- [Alex-CHUN-YU/Word2vec: 訓練中文詞向量 Word2vec, Word2vec was created by a team of researchers led by Tomas Mikolov at Google.](https://github.com/Alex-CHUN-YU/Word2vec)

- [用中文資料測試 word2vec - 翼之都, City of Wings](http://city.shaform.com/blog/2014/11/04/word2vec.html)

- [自然語言處理入門- Word2vec小實作 – PyLadies Taiwan – Medium](https://medium.com/pyladies-taiwan/%E8%87%AA%E7%84%B6%E8%AA%9E%E8%A8%80%E8%99%95%E7%90%86%E5%85%A5%E9%96%80-word2vec%E5%B0%8F%E5%AF%A6%E4%BD%9C-f8832d9677c8)

- [詞向量介紹](https://fgc.stpi.narl.org.tw/activity/videoDetail/4b1141305ddf5522015de5479f4701b1)

### Skip-gram / CBOW

- [Is skip gram (negative sampling) better than CBOW (NS) for word2vec? If so, why? - Quora](https://www.quora.com/Is-skip-gram-negative-sampling-better-than-CBOW-NS-for-word2vec-If-so-why)

    > Please see [Stephan Gouws](https://www.quora.com/profile/Stephan-Gouws) excellent answer here: [How does word2vec work? Can someone walk through a specific example?](https://www.quora.com/How-does-word2vec-work-Can-someone-walk-through-a-specific-example)
    > 
    > >For the skipgram, the direction of the prediction is simply inverted, i.e. now we try to predict P(citizens | X), P(of | X), etc. This turns out to learn finer-grained vectors when one trains over more data. The main reason is that the CBOW smooths over a lot of the distributional statistics by averaging over all context words while the skipgram does not. With little data, this "regularizing" effect of the CBOW turns out to be helpful, but since data is the ultimate regularizer the skipgram is able to extract more information when more data is available.
    > 


### fastText

- [Word vectors for 157 languages · fastText](https://fasttext.cc/docs/en/crawl-vectors.html)

- [fastText，智慧與美貌並重的文本分類及向量化工具 - 幫趣](http://bangqu.com/749a22.html#utm_source=Facebook_PicSee&utm_medium=Social)

    > 簡單介紹一下fastText的主要作者，這位高顏值的Facebook科學家Tomas Mikolov小哥。他2012年到2014年就職於Google，隨後跳到了Facebook至今。
    >  
    > 他名揚天下的，主要是以下三篇重要論文：
    > 
    > 1.Efficient Estimation of WordRepresentation in Vector Space, 2013 —— 這篇是word2vec的開蒙之作；
    > 
    > 2.Distributed Representations ofSentences and Documents, 2014 —— 這篇將詞向量的思想擴展到了段落和文檔上；
    > 
    > 3.Enriching Word Vectors withSubword Information, 2016 —— 這篇和fastText相關，引入了詞內的n-gram信息，豐富了詞向量的語義。
    > 
    > fastText能夠做到效果好，速度快，主要依靠兩個祕密武器：一是利用了詞內的n-gram信息(subword n-gram information)，二是用到了層次化Softmax迴歸(Hierarchical Softmax)的訓練trick。我們分別介紹一下。
    > 
    > 
    > __Subword n-gramlnformation__
    > 
    > 在fastText的工作之前，大部分的文本向量化的工作，都是以詞彙表中的獨立單詞作爲基本單元來進行訓練學習的。這種想法非常自然，但也會帶來如下的問題：
    > 
    > · 低頻詞、罕見詞，由於在語料中本身出現的次數就少，得不到足夠的訓練，效果不佳；
    > 
    > · 未登錄詞，如果出現了一些在詞典中都沒有出現過的詞，或者帶有某些拼寫錯誤的詞，傳統模型更加無能爲力。
    > 
    > fastText引入了subword n-gram的概念來解決詞形變化(morphology)的問題。直觀上，它將一個單詞打散到字符級別，並且利用字符級別的n-gram信息來捕捉字符間的順序關係，希望能夠以此豐富單詞內部更細微的語義。我們知道，西方語言文字常常通過前綴、後綴、字根來構詞，漢語也有單字表義的傳統，所以這樣的做法聽起來還是有一定的道理。
    > 
    > 舉個例子。對於一個單詞「google」，爲了表達單詞前後邊界，我們加入<>兩個字符，即變形爲「 」。假設我們希望抽取所有的tri-gram信息，可以得到如下集合：G = { }。在實踐中，我們往往會同時提取單詞的多種n-gram信息，如2/3/4/5-gram。這樣，原始的一個單詞google，就被一個字符級別的n-gram集合所表達。
    > 
    > 在訓練過程中，每個n-gram都會對應訓練一個向量，而原來完整單詞的詞向量就由它對應的所有n-gram的向量求和得到。所有的單詞向量以及字符級別的n-gram向量會同時相加求平均作爲訓練模型的輸入。
    > 
    > 從實驗效果來看，subword n-gram信息的加入，不但解決了低頻詞未登錄詞的表達的問題，而且對於最終任務精度一般會有幾個百分點的提升。唯一的問題就是由於需要估計的參數多，模型可能會比較膨脹。不過，Facebook也提供了幾點壓縮模型的建議：
    > 
    > · 採用hash-trick。由於n-gram原始的空間太大，可以用某種hash函數將其映射到固定大小的buckets中去，從而實現內存可控；
    > 
    > · 採用quantize命令，對生成的模型進行參數量化和壓縮；
    > 
    > · 減小最終向量的維度。
    > 
    > __Hierarchical Softmax__
    > 
    > 另一個效率優化的點是所謂的層次化Softmax。
    > 
    > Softmax大家都比較熟悉，它是邏輯迴歸(logisticregression)在多分類任務上的推廣，是我們訓練的神經網絡中的最後一層。一般地，Softmax以隱藏層的輸出h爲輸入，經過線性和指數變換後，再進行全局的歸一化處理，找到概率最大的輸出項。當詞彙數量V較大時（一般會到幾十萬量級），Softmax計算代價很大，是O(V)量級。
    > 
    > 層次化的Softmax的思想實質上是將一個全局多分類的問題，轉化成爲了若干個二元分類問題，從而將計算複雜度從O(V)降到O(logV)。
    > 
    > 每個二元分類問題，由一個基本的邏輯迴歸單元來實現。如下圖所示，從根結點開始，每個中間結點（標記成灰色）都是一個邏輯迴歸單元，根據它的輸出來選擇下一步是向左走還是向右走。下圖示例中實際上走了一條「左-左-右」的路線，從而找到單詞w₂。而最終輸出單詞w₂的概率，等於中間若干邏輯迴歸單元輸出概率的連乘積。
    > 
    > ![](http://i2.bangqu.com/j/news/20180606/749a22152825763470852j19.png)
    > 
    >  ![](http://i2.bangqu.com/j/news/20180606/749a221528257635684823ER.png)
    > 
    > 至此，我們還剩下兩個問題，一是如何構造每個邏輯迴歸單元的輸入，另一個是如何建立這棵用於判斷的樹形結構。
    > 
    > __fastText和傳統CBOW模型對比__
    > 
    > 這裏假設你對word2vec的CBOW模型比較熟悉，我們來小結一下CBOW和fastText的訓練過程有什麼不同。下面兩張圖分別對應CBOW和fastText的網絡結構圖。
    > 
    > 兩者的不同主要體現在如下幾個方面：
    > 
    > · 輸入層：CBOW的輸入是目標單詞的上下文並進行one-hot編碼，fastText的輸入是多個單詞embedding向量，並將單詞的字符級別的n-gram向量作爲額外的特徵；
    > 
    > · 從輸入層到隱藏層，CBOW會將上下文單詞向量疊加起來並經過一次矩陣乘法（線性變化）並應用激活函數，而fastText省略了這一過程，直接將embedding過的向量特徵求和取平均；
    > 
    > · 輸出層，一般的CBOW模型會採用Softmax作爲輸出，而fastText則採用了Hierarchical Softmax，大大降低了模型訓練時間；
    > 
    > · CBOW的輸出是目標詞彙，fastText的輸出是文檔對應的類標。
    > 



### ELMo

- [[1802.05365] Deep contextualized word representations](https://arxiv.org/abs/1802.05365)


### Poincaré Embeddings for Learning Hierarchical Representations

- [[1705.08039] Poincar\'e Embeddings for Learning Hierarchical Representations](https://arxiv.org/abs/1705.08039)

- [(2 封私信 / 82 条消息)如何理解闵可夫斯基空间距离公式中的负号？ - 知乎](https://www.zhihu.com/question/22296243/answer/184942906)

    > 
    > 量子力学和狭义相对论都有一些公设，比如说这个光速不变，为什么光速不变？又如量子力学波粒二相性，叠加态，不确定原理，纠缠态里的超距相互作用等等，量子力学告诉你，不要试图理解，它们就是这样，接受了这样的假设，你算出来的东西跟现实世界观测到的一切都符合。但是我们作为学生学习的时候，就变的超级困难。原则上这样的公设需要更底层的理论去解释。最近我看到一本书，牛津大学出的量子力学的多世界解释，感觉理解量子力学一下子变的容易很多。然后发现这种多世界解释，对于理解闵可夫斯基时空的结构也很有帮助。如果你不想看下面的公式，只要接受一个定理，就可以理解我说的为什么闵可夫斯基时空与多世界理论是一致的。
    > 
    > 这个定理就是： **一个层层劈裂的树结构，其连续极限对应着双曲空间（即闵可夫斯基空间）。**
    > 
    > **如果你想知道这个定理哪来的，可以搜索： Poincare Embeddings for Learning Hierarchical Representations (2017 May 26 by Facebook AI Research).**
    > 
    > 我们也来做个假设，显式的世界是1+1维的，只有t - x分量，在一个双曲空间，半径是 s, 双曲圆的圆周是 t = 2 pi sinh s, 双曲圆的面积是 x = 2pi (cosh s - 1), 随着球半径 s 的增加 ds，圆周长和面积呈指数增长，
    > 
    > dt = 2 pi cosh s ds
    > 
    > dx = 2 pi sinh s ds
    > 
    > 则![dt^2 - dx^2 = (2\pi)^2 ds^2 = ds^2](https://www.zhihu.com/equation?tex=dt%5E2+-+dx%5E2+%3D+%282%5Cpi%29%5E2+ds%5E2+%3D+ds%5E2)
    > 
    > 这意味着什么呢？这个定理说明如果我们的宇宙是多世界的，任何时候时空都会劈裂，宇宙就会以指数暴涨，时空的结构是一个层级劈裂的树结构的连续近似，那么时间和空间分量必然会差一个负数。
    > 
    > 刚才在网上搜了下，发现一篇2000年的PRL文章 Tree Structure of a Percolating Universe; 但是那篇文章讲的是宇宙中物质密度分布的树结构，而不是时空劈裂造成的树结构。
    > 
    > （这也是看到了树结构的连续近似是双曲空间时，突然脑洞大开的想到的时空结构与多世界理论之间的关系。不匿了，反正大家猜不出来我是谁，就算贻笑大方也没关系）
    > 

- [(2 封私信 / 82 条消息)什么是双曲空间？与欧式空间的区别是什么呢？一个图结构能映射到双曲空间是怎么回事？ - 知乎](https://www.zhihu.com/question/27302536)

    > 对于嵌入图结构来说，用到的双曲空间性质主要只有一条：双曲空间H^d从一点出发半径为r的邻域，面积/体积为指数阶增长的c*e^{r(d-1)}而不是欧氏空间的多项式阶增长的c*r^{d-1}。因为这一点，能够满足一定条件（roughly isometric）映射到双曲空间的图（比如树和一些Cayley graph）通常是指数阶增长的，自带non-amenable属性，有着非零的edge expansion，进而很多性质跟嵌入欧氏空间的图（一定amenable）有一些区别。具体在概率论里面就是比如随机游走一定非常返，percolation可以有无穷多个infinte cluster等等。
    > 
    > 形象一点理解的话，可以想像树嵌入于双曲空间，就像lattice嵌入于Z^d。
    > 
    > 以上内容来自Lyons, Peres: Probability on trees and networks 第52-55页和第207-212页，里面掺杂了很多概率的东西题主可以选择性看一看。
    > 
    > 出门在外手机翻书不便没有查准确的结论，回头补上。
    > 



- [異空間への埋め込み！Poincare Embeddingsが拓く表現学習の新展開 - ABEJA Arts Blog](https://tech-blog.abeja.asia/entry/poincare-embeddings)

    - [Embedding in a different space! New development of expressive learning that Poincare Embeddings opens- ABEJA Arts Blog](https://translate.google.com.tw/translate?sl=ja&tl=en&js=y&prev=_t&hl=zh-TW&ie=UTF-8&u=https%3A%2F%2Ftech-blog.abeja.asia%2Fentry%2Fpoincare-embeddings&edit-text=)


    > It is Shirakawa who is researcher at ABEJA.
    > 
    > This time we introduce Poincaré Embeddings [1]. I was surprised at the contents, personally examined, implemented, talked about at a study group, recently luckily I had my implementation picked up by reddit, so as long as I could share the amazing content with this I think. To be honest, it is a technology that has not yet been boiled down in myself, so we will share the current situation, but please forgive me that some speculation, prospects, expectations are mixed in every place.
    > 
    > [[D] Any advice for a non computational-linguist trying to recreate 'Poincaré Embeddings for Learning Hierarchical Representations'? : MachineLearning](https://www.reddit.com/r/MachineLearning/comments/6w3oq7/d_any_advice_for_a_non_computationallinguist/?st=j6u54uxr&sh=c8823212)
    > 
    > Roughly speaking, Poincaré Embeddings is a technology to realize word2vec in a different space called Hyperbolic Space, it expresses data in a space different from the usual space which is a familiar Euclide space (the distance of 2 point $x,y$ is measured by $\sqrt{(x_1 - y_1)^2 + (x_2 - y_2) ^ 2 + ... + (x_d - y_d) ^ 2}$. As a result, in the conventional method (the method of embedding in the Euclide space like word2vec), it required a vector representation of about 200 dimensions, and we succeeded in achieving far higher accuracy with **5 dimensions** .
    > 
    > ![f:id:daynap1204:20170827142406p:plain](https://cdn-ak.f.st-hatena.com/images/fotolife/d/daynap1204/20170827/20170827142406.png "f: id: daynap 1204: 20170827142406 p: plain")  Improvement of embedding accuracy by Poincaré Embeddings (cited from [1])
    > 
    > I will list the merits of embedding in Poincaré space.
    > 
    > -   Compared to embedding in Euclide space, space can be efficiently used exponentially
    > -   As a result, sufficiently precise embedding can be realized in low dimensions
    > -   Automatically extract the hierarchical structure of data
    > -   Easy to implement (it only makes minor corrections)
    > -   Easy to understand ideas
    > -   It may be a good idea to learn machine learning on Riemannian manifolds
    > 
    > Although this method and the idea are simple, it feels very possibilities (since machine learning on Riemannian manifolds has a long history, it seems that it finally came to the practical stage). Although reading mathematical background seems necessary at first glance when reading the thesis, since it is simple to do, I think that it is possible to chew and tell the atmosphere in this article.
    > 
    > I am interested in expressing the graph structure with Deep Learning and solving the problem using the graph structure, but I am exploring whether this method can be used successfully in such cases. Anyway, it is a simple idea so many imaginations are bulging and fun!
    > 
    > Below, there are some slides that I used at study group, so please refer together. Contents that are not explained in this article are also included a little.
    > 
    > <iframe src="//www.slideshare.net/slideshow/embed_code/key/yiq14bajD5sQ8O" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/daynap1204/poincare-embeddings-for-learning-hierarchical-representations" title="Poincare embeddings for Learning Hierarchical Representations" target="_blank">Poincare embeddings for Learning Hierarchical Representations</a> </strong> from <strong><a href="https://www.slideshare.net/daynap1204" target="_blank">Tatsuya Shirakawa</a></strong> </div>
    > 
    > 
    > 
    > Also, my implementation is below. Part of the experiments introduced in this article can be reproduced, so please try it if you are interested. Issue and PR are also welcome.
    > 
    > [TatsuyaShirakawa (Tatsuya Shirakawa)](https://github.com/TatsuyaShirakawa)
    > 
    > 
    > 
    > First let's review from word2vec.
    > 
    > Review of word2vec
    > ===================
    > 
    > Those familiar with word2vec and skipgram are OK even if this section is skipped.
    > 
    > word2vec [2] is a tool for finding the expression vector of words in the text, and two models, skipgram and cbow [3, 4], are implemented.
    > 
    > Originally, Yoshua Bengio and colleagues published a paper [5] to ask for expression vectors (distributed expressions) of words using Deep Neural Networks in 2001 (!) In this paper, It was a mechanism to obtain vectors using Deep Neural Networks.
    > 
    > The contribution of Tomas Mikolov's discovery of skipgram / cbow is to demonstrate that it is only necessary to directly optimize the word "expression vector table" without using a complicated and powerful model like Deep Neural Networks (If you think calmly, you can see that optimization of the table is enough).
    > 
    > Furthermore, Tomas Mikolov et al. Introduced a mechanism called Negative Sampling, which also realized overwhelming improvement in calculation efficiency [6]. Here the word2vec festival in the NLP area began. It is wonderful that good models and good implementations are released properly! By the way I love simple and powerful word2vec.
    > 
    > Well, although it is word2vec, here I will only describe the skipgram (SGNS) with Negative Sampling (cbow a bit different model, but Nori is together). SGNS is a very simple model, prepare a vector expression table of words
    > 
    > 1.  Expression vectors of positive samples that appear in close proximity in the sentence have large inner products
    > 2.  Expression vectors of randomly selected words (negative samples) have small inner products
    > 
    > We will optimize it to become. Specifically, when $V_i$ is the expression vector of the word $i$, ($V = {\{v_i\}}_{i \in I}$ is the expression vector table), set the following objective function to Maximize.
    > 
    > $\text{maximize}_{ \{v_i \}_i } \ \ \mathbb{E}_{(i,j) \sim P(i,j)} \Bigl[ \log \sigma ( \langle v_i, v_j \rangle ) \Bigr] + k \ \mathbb{E}_{(i,j) \sim P(i)P(j)} \Bigl[ \log 1-\sigma (\langle v_i, v_j \rangle) \Bigr]$
    > 
    > Where $\langle v_i, v_j \rangle$ is the inner product of the expression vector for the words $i, j$. $P(i, j)$ is the probability distribution in which the word pair $(i, j)$ appears in close proximity (in the case of the figure below, the word appearing within 2 words on the right and left of the word on is a close word ), And $P(i)$ is the frequency distribution (unigram distribution) of the word $i$ alone. $k$ is a nonnegative constant that controls the balance between potive samples and negative samples (theoretically $k = 1$ is ideal, but values ​​such as $k = 5, 10, 20$ are used practically) The function $\sigma(x) = 1 / (1+ \exp (-x))$ is a sigmoid function (there is really fine tuning of $P(i)$ to 3/4 However, since it is not essential, I ignore it).
    > 
    > Without difficulties, we are seeking a word expression vector to increase the probability of occurrence of positive samples and lower the appearance probability of negative samples.
    > 
    > ![f:id:daynap1204:20170827155338p:plain](https://cdn-ak.f.st-hatena.com/images/fotolife/d/daynap1204/20170827/20170827155338.png "f: id: daynap 1204: 20170827155338 p: plain")  SkipGram with Negative Sampling (SGNS)
    > 
    > SGNS is known to be a matrix decomposition that takes pointwise mutual information (PMI) as an element value (it can be easily shown by a discussion similar to the convergence proof of discriminator of original article of GANs).
    > 
    > $$ \langle v_i, v_j \rangle = PMI(i,j) = log \frac{P(i,j)}{P(i)P(j)} $$
    > 
    > The wonderful aspect of SGNS is its computational efficiency. Slide the window (the dotted line window at the upper left of the above figure) above the text data and acquire the noteworthy words (on in the case above) and the surrounding words (same samples cat, sat, the, mat), On the other hand, if you sample words from the frequency distribution of words (negative samples), then you can easily optimize by stochastic gradient descent method. Furthermore, it is experimentally known that the representation vector of words obtained by this has a well-known regularity (linguistic regularity). It is a king-man = queen-woman guy.
    > 
    > ![f:id:daynap1204:20170827161023p:plain](https://cdn-ak.f.st-hatena.com/images/fotolife/d/daynap1204/20170827/20170827161023.png "f: id: daynap 1204: 20170827161023 p: plain")
    > 
    > Quoted from [6]
    > 
    > Although it is SGNS, it applies only to text data. Here, as an application example to a graph structure, we introduce a technique called LINE (Large-scale Information Network Embedding) [7]. In addition, here is my hobby to introduce the application to graphs, but also because poincaré embedding of subject matter is also related to graph structure (actually tree structure). There is also a feeling that we want to improve the situation that word2vec does not see the eyes of the day though it can apply as it is to nothing to the graph structure (I think that there are many people applying commonsense, of course).
    > 
    > LINE - Application of SGNS to graph
    > ===================================
    > 
    > LINE is a technique to apply SGNS to graph. Specifically, it is in correspondence relationship as follows.
    > 
    > | Object | LINE | SGNS |
    > | --- | --- | --- |
    > | To be embedded | node | word |
    > | P (i) | Proportional to the degree of the node | Proportional to the frequency of appearance of words |
    > | P (i, j) | Uniform distribution from the edge of the graph | Uniform sampling from window |
    > 
    > That is, it will be learning as follows.
    > 
    > 1.  Generate word pair by uniformly sampling edges from graph (positve samples)
    > 2.  By sampling two nodes with a probability proportional to the order, node pairs are generated (negative samples)
    > 
    > Optimizing is also the same objective function as SGNS.
    > 
    > $\text{maximize}_{ \{v_i \}_i } \ \ \mathbb{E}_{(i,j) \sim P(i,j)} \Bigl[ \log \sigma (\langle v_i, v_j \rangle ) \Bigr] + k \ \mathbb{E}_{(i,j) \sim P(i)P(j)} \Bigl[ \log 1-\sigma (\langle v_i, v_j \rangle ) \Bigr]$
    > 
    > It is thanks to the simplicity of SGNS that we could apply as it was to the graph.
    > 
    > Poincaré Embeddings
    > ===================
    > 
    > Here is the main issue. SGNS is simple and wonderful. Calculation efficiency is also very good. I thought that there was nothing more to say, but Poincaré Embeddings took a moment to wait there.
    > 
    > **Its embedding, the best?**
    > 
    > SGNS takes the expression vectors $v_i, v_j$ of the two words $i, j$, and the inner product
    > 
    > $$ \langle v_i, v_j \rangle $$
    > 
    > We measured the degree of cooccurrence of these words (the larger one is easier to co-occur).
    > 
    > But is not there a better way to measure it?
    > 
    > Poincaré Embeddings [1] embeds data (nodes and words) into a distorted space called hyperbolic space that is more space efficient than the Euclide space and measures the distance between those data in that space makes it much more efficient We succeeded in acquiring expression vectors.
    > 
    > Inner product $\langle u, v \rangle$ is $$ \langle u,v \rangle = ({\Vert u + v \Vert}^2 - {\Vert u \Vert}^2 - {\Vert v \Vert}^2)/2 $$, so it essentially depends on how to measure the distance in Eulide space. Therefore, SGNS can be thought of as an embedded model in the Euclide space. I think that it is safe to assume that most models handled in Deep Learning are constructed in Euclide space (there are of course exceptions).
    > 
    > In the case of Poincaré Embeddings, we construct an embedding with hyperbolic space instead of Euclide space. In the hyperbolic space, like the Euclide space, each point is represented as a vector, but unlike the Euclide space, there is distortion in the space, and the way to measure the distance between the two points is different. Therefore, by utilizing this distortion, it becomes possible to embed more efficiently and uniquely than the Euclide space (in short the Euclide space was too flat).
    > 
    > I will leave a little hyperbolic space.
    > 
    > Hyperbolic space
    > ----------------
    > 
    > Hyperbolic space is mathematically a very vital space. If you dig deep, the discussion will not run out, so let's eat only delicious places here. For details, please refer to wikipedia [8] or thesis [9]. If it is a book, the following books are written very clearly.
    > 
    > [![双曲幾何 (現代数学への入門)](https://images-fe.ssl-images-amazon.com/images/I/41NJK988YXL._SL160_.jpg)](https://translate.googleusercontent.com/translate_c?depth=1&hl=zh-TW&ie=UTF8&prev=_t&rurl=translate.google.com.tw&sl=ja&sp=nmt4&tl=en&u=http://www.amazon.co.jp/exec/obidos/ASIN/4000068822/hatena-blog-22/&xid=17259,15700021,15700124,15700149,15700186,15700191,15700201&usg=ALkJrhg2D9tj5WUadbqAPtDTFt1yucbMCw)
    > 
    > [Hyperbolic Geometry (Introduction to Modern Mathematics)](https://translate.googleusercontent.com/translate_c?depth=1&hl=zh-TW&ie=UTF8&prev=_t&rurl=translate.google.com.tw&sl=ja&sp=nmt4&tl=en&u=http://www.amazon.co.jp/exec/obidos/ASIN/4000068822/hatena-blog-22/&xid=17259,15700021,15700124,15700149,15700186,15700191,15700201&usg=ALkJrhg2D9tj5WUadbqAPtDTFt1yucbMCw)
    > 
    > -   Author: Kenji Fukaya
    > -   Publisher / manufacturer: Iwanami Shoten
    > -   Release date: 2004/09/07
    > -   Media: Paperback
    > -   Clicks : 6 times
    > -   [View a blog (2 items) containing this product](https://translate.googleusercontent.com/translate_c?depth=1&hl=zh-TW&ie=UTF8&prev=_t&rurl=translate.google.com.tw&sl=ja&sp=nmt4&tl=en&u=http://d.hatena.ne.jp/asin/4000068822/hatena-blog-22&xid=17259,15700021,15700124,15700149,15700186,15700191,15700201&usg=ALkJrhjhFEPXAU4b8WhRRlQg0lrGMRvjKg)
    > 
    > Although I have not read it, in the feeling that I saw at a bookstore, the hyperbolic space was easy to explain in the following book that recently appeared.
    > 
    > [![曲がった空間の幾何学 現代の科学を支える非ユークリッド幾何とは (ブルーバックス)](https://images-fe.ssl-images-amazon.com/images/I/51CITZPDy-L._SL160_.jpg "Geometry of crooked space Non-Euclidean geometry supporting modern science (Blue Bucks)")](https://translate.googleusercontent.com/translate_c?depth=1&hl=zh-TW&ie=UTF8&prev=_t&rurl=translate.google.com.tw&sl=ja&sp=nmt4&tl=en&u=http://www.amazon.co.jp/exec/obidos/ASIN/4065020239/hatena-blog-22/&xid=17259,15700021,15700124,15700149,15700186,15700191,15700201&usg=ALkJrhgRVhjsAtBstU2Py_u2owlxFfb1HA)
    > 
    > [Geometry of crooked space Non-Euclidean geometry supporting modern science (Blue Bucks)](https://translate.googleusercontent.com/translate_c?depth=1&hl=zh-TW&ie=UTF8&prev=_t&rurl=translate.google.com.tw&sl=ja&sp=nmt4&tl=en&u=http://www.amazon.co.jp/exec/obidos/ASIN/4065020239/hatena-blog-22/&xid=17259,15700021,15700124,15700149,15700186,15700191,15700201&usg=ALkJrhgRVhjsAtBstU2Py_u2owlxFfb1HA)
    > 
    > -   Author: Reiko Miyaoka
    > -   Publisher / Manufacturer: Kodansha
    > -   Release date: 2017/07/19
    > -   Media: New book
    > -   [View a blog containing this product (1 item)](https://translate.googleusercontent.com/translate_c?depth=1&hl=zh-TW&ie=UTF8&prev=_t&rurl=translate.google.com.tw&sl=ja&sp=nmt4&tl=en&u=http://d.hatena.ne.jp/asin/4065020239/hatena-blog-22&xid=17259,15700021,15700124,15700149,15700186,15700191,15700201&usg=ALkJrhiiCDoA50bvbLyO0gIiFEB9W6NJNA)
    > 
    > There are several configuration methods (models) in the hyperbolic space, but here we adopt the Poincaré Ball (Poincaré Disk) model according to the original thesis. In the Poincaré Ball model, the data is expressed in the $d$ unit unit ball $\mathbf{B}^d = \{x \in \mathbb{R}^d \ \Vert x \Vert <1 \}$ I will. In the case of the Poincaré Ball model, the resolution gets accelerated as it approaches the perimeter of this unit sphere $\mathbf{B}^d$ ($\Vert x \Vert = 1$) It is an image in which the space spreads explosively the more it goes), this creates the efficiency of expression.
    > 
    > Regarding hyperbolic space, there is drawing by Escher.
    > 
    > ![f:id:daynap1204:20170827165827j:plain](https://cdn-ak.f.st-hatena.com/images/fotolife/d/daynap1204/20170827/20170827165827.jpg "f: id: daynap 1204: 20170827165827 j: plain")
    > 
    > MC Escher, Circle Limit III, 1959
    > 
    > I think you can see that the space gets tightly packed the more you go to the outside (in contrary, the space spreads to the outside).
    > 
    > Mathematically, the increase in the expansion of this space is expressed as follows.
    > 
    > $$ g_x = \Biggl(\frac{2}{1-{\Vert x \Vert }^2 } \Biggr)^2 g^E $$
    > 
    > The meaning of this expression, $g_x$ is a metric on Poincaré Disc, $g^E$ represents a measure in Euclide space. The way of expanding the space at the point $x$ on Poincaré Ball is $2/(1 - {\Vert x \Vert}^2)$ times that of the same point spreading in the Euclide space . As $\Vert x \Vert$ gets closer to 1 the closer it gets, the more it will be, so the more space you go to the periphery of Poincaré Ball, the wider the space will be.
    > 
    > Then, what is the distance between two points $x, y$ in Poincaré Ball? Mathematically, the distance between two points in such a distorted space is defined by the length of the shortest path connecting two points, geodesic. The distance between two points in the Euclide space was defined by the length of the straight line connecting the two points, but the geodesic is an extension of the concept of distance in the Euclide space to a distorted space (manifold).
    > 
    > In Poincaré Ball, the ruler length varies for each place, so the ruler will continue to change on the way from the point $x$ to the point $y$. Therefore, it seems that it is difficult to identify and calculate the length of what the shortest one (geodesic line) among those roads is, but fortunately Poincaré Ball's In case,
    > 
    > 1.  A geodesic line connecting two points $x, y$ always passes through the two points and becomes an arc perpendicular to the unit sphere
    > 2.  The length of the geodesic line can be computed explicitly $d(x,y) = arccosh \Bigl(1 + 2 \frac{{\Vert x - y \Vert}^2}{(1-{\Vert x \Vert}^2)(1-{\Vert y \Vert}^2)} \Bigr)$
    > 
    > It is known to become. Here, $arccosh(\gamma)=\log \bigl(\gamma + \sqrt{\gamma-1}\sqrt{\gamma+1} \bigr)$ is a function called an inverse hyperbolic cosine function.
    > 
    > ![f:id:daynap1204:20170827231134p:plain](https://cdn-ak.f.st-hatena.com/images/fotolife/d/daynap1204/20170827/20170827231134.png "f: id: daynap 1204: 20170827231134 p: plain")
    > 
    > Quoted from [1]
    > 
    > Even this alone is glad, but that alone will not end. A special property that a tree structure can be embedded in a natural form in hyperbolic space is known, and the distance between the nodes making up the tree structure (the first parent in the family tree, the second parent etc .. ), It can be embedded in a bipolar space of the appropriate dimension [9]. To understand only the atmosphere, this embedding places the node closer to the root of the tree near the center of Poincaré Ball and the node closer to the leaf near the periphery of Poincaré Ball ((b) in the upper figure) .
    > 
    > Because of this nature, it is expected that the data placed near the center when embedded in Poncaré Ball is more abstract and the data placed on the periphery is more concrete (as you will see later, It is astonishing point that actually does that).
    > 
    > I put it down because I wrote it with the momentum.
    > 
    > -   The hyperbolic space is mathematically a venerable space
    > -   By using Poincaré Ball model, hyperbolic space can be expressed in unit sphere
    > 
    > Furthermore, the Poincaré Ball model
    > 
    > -   As the distance from the origin of the unit sphere to the peripheral portion increases, the space expands at an accelerated rate and data can be embedded in space efficiently
    > -   The distance between two points can be calculated explicitly
    > -   It is known that the hierarchical structure is embedded naturally so that the hierarchical structure is disposed closer to the periphery at the terminal end.
    > 
    > It has a wonderful nature.
    > 
    > Construction of Poincaré Embeddings
    > -----------------------------------
    > 
    > Poincaré Embeddings is a technique to embed data in Poincaré Ball. Skipgram expressed the similarity between data pairs $(i, j)$ with inner product $\langle v_i, v_j \rangle$, but in the original paper by Poincaré Embeddings, this was compared with the sign of the distance between two points Inverse of $-d(v_i, v_j)$. Because we decided to represent the inner product by distance, strictly speaking, the correspondence between skipgram and Poincaré Embedding has collapsed, but here we keep our eyes closed (as I will mention later, inner product in hyperbolic space Some papers have defined and used equivalent things [10]).
    > 
    > When learning Poincaré Embeddings like skipgram,
    > 
    > -   For co-occurring data pair (positive samples) the distance is small
    > -   For a randomly selected data pair (negative samples) the distance is increased
    > 
    > We will optimize so that. However, because the distance function is nonnegative, $$ \frac{d(v_i, v_j) - r}{t}$$ is used so that the distance $d(v_i, v_j)$ Include correction like ($r, t$ are hyperparameters). I feel a little bit of teething, but I have no way of looking. Let's wait for future works for the definition of better similarity / dissimilarity function.
    > 
    > Optimization is performed by SGD (stochastic gradient descent method) that can be executed in a distorted space called Riemannian SGD, but this explanation will be replaced by the following slide. The main point is simple, only when correcting the length of the ruler is done when descending the gradient.
    > 
    > ![f:id:daynap1204:20170828013331p:plain](https://cdn-ak.f.st-hatena.com/images/fotolife/d/daynap1204/20170828/20170828013331.png "f: id: daynap 1204: 20170828013331 p: plain")
    > 
    > Experimental results on original paper [1]
    > ------------------------------------------
    > 
    > It is an experiment result of waiting. I am doing two kinds of experiments.
    > 
    > 1.  Embedding a hierarchical structure of nouns in WordNet
    > 2.  Graph link prediction
    > 
    > Let's see each one. Since detailed details are omitted, please refer to the original paper [1] if necessary.
    > 
    > ### Embedding a hierarchical structure of nouns in WordNet
    > 
    > This is made so that it can be reproduced by my first implementation. Please see the README for details of the execution method.
    > 
    > WordNet [10] is an English concept dictionary. In the original thesis, only the nouns are extracted from here, and those that enumerate the conceptual upper / lower relation are set as the data set (for example, since the dog is a mammal, the upper concept is a mammal and the lower concept is a dog) . In particular
    > 
    > | Hyponym | Broader term |
    > | --- | --- |
    > | apple_jelly.n.01 | confiture.n.01 |
    > | telephone_system.n.01 | physical_entity.n.01 |
    > | organizer.n.02 | causal_agent.n.01 |
    > | utmost.n.01 | extent.n.02 |
    > | tael.n.01 | abstraction.n.06 |
    > | financial_institution.n.01 | organization.n.01 |
    > | uruguayan.n.01 | whole.n.02 |
    > | holocentrus_ascensionis.n.01 | vertebrate.n.01 |
    > | bell_metal.n.01 | substance.n.01 |
    > | takeoff.n.02 | happening.n.01 |
    > | ... | ... |
    > 
    > It was imagined that it would be the data of the feeling that (I did not write in the paper so I imagined it based on the numerical value of the experiment result ...). This data is arranged in a noun pair, so that the lower word is on the left side and the upper word is on the right side. ".n" indicates that the word is a noun, and the numbers ". 01" and ".02" are attached to distinguish words with the same spelling but different meanings.
    > 
    > This one line is defined as 1 positive sample, and negative samples are generated by randomly selecting 2 words with the probability proportional to the frequency of appearance of words in this data.
    > 
    > For the above data, maximize the function as below.
    > 
    > $$\mathcal{L}(\Theta) = \sum_{(i, j)\in \mathcal{D}} \log \frac{ \exp(-d(v_i, v_j))}{\sum_{j' \in \mathcal{N}(i)} \exp(-d(v_i, v_{j'}))}$$
    > 
    > Here, $\Theta$ represents the whole parameter of this model, $\mathcal{N}(i)$ is the negative samples of $j$ generated for data $i$, basically It is generated with randomness proportional to the frequency of occurrence, but if $(i, j')$ exists in the data set $\mathcal{D}$, regenerate it excluding it. Maximizing the above function is equivalent to maximizing the probability of applying positive samples and negative samples when they are given to mix.
    > 
    > As I showed you first, the results are starting to emphasize the accuracy of embedding in the Euclide space.
    > 
    > ![f:id:daynap1204:20170828015724p:plain](https://cdn-ak.f.st-hatena.com/images/fotolife/d/daynap1204/20170828/20170828015724.png "f: id: daynap 1204: 20170828015724 p: plain")
    > 
    > Accuracy improvement is also amazing, but person who feels very interesting is how to be embedded. Below is a quotation from the original paper, but I think you will find that it is located closer to the center as the broader word. Hierarchical structure has been extracted correctly (although it is a bit surprising because it is strikingly articulated (low-ranking, high-ranking) where to make a data set ...)
    > 
    > ![f:id:daynap1204:20170828015924p:plain](https://cdn-ak.f.st-hatena.com/images/fotolife/d/daynap1204/20170828/20170828015924.png "f: id: daynap 1204: 20170828015924 p: plain")
    > 
    > I can also reproduce the same embedding with my own code (I can reproduce it if you run my code). For ease of viewing, we apply transformation (isometric transformation) that preserves the distance relationship of data, and it is centered around mammal (mammal).
    > 
    > ![f:id:daynap1204:20170828020209p:plain](https://cdn-ak.f.st-hatena.com/images/fotolife/d/daynap1204/20170828/20170828020209.png "f: id: daynap 1204: 20170828020209 p: plain")
    > 
    > ### Graph link prediction
    > 
    > This is a task of predicting whether there is an edge between two given nodes. For this task, we will maximize the cross entropy of the probabilistic model shown below.
    > 
    > $$ P(e(i,j)=1; \Theta) = \frac{1}{1 + \exp((d(i,j)-r)/t)} $$
    > 
    > Here, $i, j$ are graph nodes, $e(i, j)$ is an edge between them, $e(i, j) = 1$, edge exists If not present, $e (i, j) = 0$. $\Theta$ is a model parameter as well, and $(d(i, j) - r)/t$ is a corrected distance function to take the negative value explained earlier. By maximizing this probabilistic model, nodes closer to one another will be placed closer to each other.
    > 
    > Again in this case, we achieved accuracy exceeding embedding in the Euclide space.
    > 
    > ![f:id:daynap1204:20170828021136p:plain](https://cdn-ak.f.st-hatena.com/images/fotolife/d/daynap1204/20170828/20170828021136.png "f: id: daynap 1204: 20170828021136 p: plain")
    > 
    > Aside: "Inner product" in Poincaré Ball
    > ---------------------------------------
    > 
    > Dare not to inner product but dare to say "inner product" because I feel that it is very difficult to define the ideal inner product in Poincaré Ball.
    > 
    > Shortly after the paper by Poincaré Embeddings [1] came out, Poincaré Ball defined "inner product" and replaced the similarity function denoted as $-d(v_i, v_i)$ by Poincaré Embeddings with its "inner product" A paper [11] appeared (At this time, was there a trigger that promotes embedding in hyperbolic space at this time?). It seems that it was announced at the workshop of KDD 2017 which was held the other day.
    > 
    > [13th International Workshop on Mining and Learning with Graphs (MLG 2017)](http://www.mlgworkshop.org/2017/)
    > 
    > In this paper, "inner product" in Poincaré Ball is defined as follows. When expressing "inner product" in Poincaré Ball of two points $u, v$ as $\langle \langle u, v \rangle \rangle$ to distinguish it from the inner product $\langle u, v \rangle$ in Euclide space
    > 
    > $$ \langle\langle u,v \rangle \rangle = d(o,u) \ d(o,v) \ cos \theta .$$
    > 
    > That is the "inner product". Where $o$ is the origin of Poincaré Ball and $\theta$ is the angle of the angle made by the two points u and v about the origin o. In Poincaré Ball, it is known that the geodesic line between the origin and another point is a straight line connecting the two points, $\theta$ is a geodesic line connecting $o$ and $u$ and It can be thought of as an angle formed by a geodesic line connecting $o$ and $v$. From this point of view, this "inner product" can be regarded as an extension of the concept of inner product in Euclide space to Poincaré Ball.
    > 
    > Actually, I was also looking for a function to replace $-d(v_i, v_j)$, and I was thinking of a similar inner product, but recently, from the correspondence relationship below, "inner product" in Poincaré Ball I realized that the definition of Poincaré Ball can not effectively utilize the richness of the space.
    > 
    > $$ \langle \langle u,v \rangle \rangle = <u', v'>, \ \ u' = \frac{d(o,u)}{\Vert u \Vert} u, \ \ v' = \frac{d(o,v)}{\Vert v \Vert} v $$
    > 
    > Corresponding to $u \rightarrow u', v \rightarrow v'$, there is a one-to-one correspondence between Poincaré Ball and Euclide space, and this correspondence maintains the value of "inner product" . So, although I was thinking with Poincaré Ball, I could only acquire the same expression ability as I thought in Euclide space.
    > 
    > Defining appropriate similarity / dissimilarity in hyperbolic space is likely to become a future task.
    > 
    > in conclusion
    > -------------
    > 
    > How was that. I would be pleased if you could tell even a little about the possibilities of Poincaré Embeddings. Although the direction to represent data in a richer space has been conventionally used (kernel method also implicitly does that), the expression in Poincaré Ball may be one of practical optimal solutions .
    > 
    > I have introduced Graph Convlution before, but I think that Graph Convolution works because Graph has locality, recurrence, fractal nature and hierarchical structure. As we consider these properties, I can not help feeling affinity with Poincaré Embeddings. I'd like to end this paper with my heart pounding up in the future where Deep Learning will be deployed in hyperbolic space.
    > 
    > Publicity
    > =========
    > 
    > ABEJA is looking for Researcher who is intentionally aware of advanced technology! Other professionals are also looking for praise! !
    > 
    > **If you are interested in the latest technology from ABEJA, be sure to read the blog!**
    > 
    > **Those who are interested in the company ABEJA are transmitting information on the company, business and people at Wantedly, so please do follow up by all means!** **!** **[About 株式会社ABEJA - Wantedly](https://tw.wantedly.com/companies/abeja)**
    > 
    > **I want to talk with someone in ABEJA!** **Since we are looking forward to see you office at any time, please feel free to ↓ ↓**
    > 
    > References
    > ==========
    > 
    > [1] M. Nickel and D. Kiela, "Poincaré Embeddings for Learning Hierarchical Representations", arXiv: 1705.08039
    > 
    > [2] [https://code.google.com/archive/p/word2vec/](https://code.google.com/archive/p/word2vec/)
    > 
    > [3] T. Mikolov et al., "Linguistic Regularities in Continuous Space Word Representations", NAACL 2013
    > 
    > [4] T. Mikolov et al., "Efficient Estimation of Word Representations in Vector Space", ICLR 2013
    > 
    > [5] Y. Bengio et al., "A Neural Probabilistic Language Model", NIPS'00
    > 
    > [6] T. Mikolov et al., "Distributed Representations of Words and Phrases and Their Compositionality", NIPS 2013
    > 
    > [7] J. Tang et al., "LINE: Large-scale Information Network Embedding", WWW 2015
    > 
    > [8] [https://en.wikipedia.org/wiki/Hyperbolic_space](https://en.wikipedia.org/wiki/Hyperbolic_space)
    > 
    > [9] Krioukov, Dmitri et al., "Hyperbolic geometry of complex networks", Physical Review 2010
    > 
    > [10] [https://wordnet.princeton.edu/](https://wordnet.princeton.edu/)
    > 
    > [11] BP Chamberlain et al., "Neural Embeddings of Graphs in Hyperbolic Space", arXiv: 1705.10359
    > 
    > [12] [http://tech-blog.abeja.asia/entry/2017/04/27/105613](http://tech-blog.abeja.asia/entry/2017/04/27/105613)

