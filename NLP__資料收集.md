# NLP__資料收集

[toc]
<!-- toc --> 


## Reference Book

### CS4650 and CS7650 ("Natural Language") at Georgia Tech

- [gt-nlp-class/notes at master · jacobeisenstein/gt-nlp-class](https://github.com/jacobeisenstein/gt-nlp-class/tree/master/notes)

## Course

### CS224N

- [CS224n: Natural Language Processing with Deep Learning](http://web.stanford.edu/class/cs224n/)

    - [Lecture 1 | Natural Language Processing with Deep Learning - YouTube](https://www.youtube.com/watch?v=OQQ-W_63UgQ&list=PLqdrfNEc5QnuV9RwUAhoJcoQvu4Q46Lja)



## DEMO

### word2vec 小遊戲

- [讓你看見 AI 自然語言處理多強大！Google 發表一款搜尋引擎和兩個文字遊戲 - INSIDE 硬塞的網路趨勢觀察](https://www.inside.com.tw/2018/04/16/google-introducing-semantic-experiences-with-talk-to-book)

    - [Semantris](https://research.google.com/semantris/)





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

- [ysc/cws_evaluation: Java开源项目cws_evaluation：中文分词器分词效果评估对比](https://github.com/ysc/cws_evaluation)

- [竹間智能科技台北 Emotibot Taipei - 貼文](https://www.facebook.com/EmotibotTaipei/posts/1896621840559761:0)

    > 中文斷詞做不好，人機自然語言交互當然難以取得突破
    > 
    > 原創竹間智能科技Emotibot
    > 中文斷詞是中文文本處理的一個基礎步驟，也是中文人機自然語言交互的基礎模組。不同於英文的是，中文句子中沒有詞的界限，因此在進行中文自然語言處理時，通常需要先進行斷詞，斷詞效果將直接影響詞性、句法樹等模組的效果。當然斷詞只是一個工具，場景不同，要求也不同。
    > 
    > 在人機自然語言交互中，成熟的中文斷詞算法能夠達到更好的自然語言處理效果，幫助計算機理解複雜的中文語言。竹間智能在構建中文自然語言對話系統時，結合語言學不斷優化，訓練出了一套具有較好斷詞效果的算法模型，爲機器更好地理解中文自然語言奠定了基礎。
    > 
    > 在此，對於中文斷詞方案、當前斷詞器存在的問題，以及中文斷詞需要考慮的因素及相關資源，竹間智能 自然語言與深度學習小組 做了些整理和總結，希望能爲大家提供一些參考。
    > 
    > 中文斷詞根據實現原理和特點，主要分爲以下2個類別：
    > 
    > 1、基于詞典斷詞算法
    > 
    > 也稱字符串匹配斷詞算法。該算法是按照一定的策略將待匹配的字符串和一個已建立好的“充分大的”詞典中的詞進行匹配，若找到某個詞條，則說明匹配成功，識別了該詞。常見的基于詞典的斷詞算法分爲以下幾種：正向最大匹配法、逆向最大匹配法和雙向匹配斷詞法等。
    > 
    > 基于詞典的斷詞算法是應用最廣泛、斷詞速度最快的。很長一段時間內研究者都在對基于字符串匹配方法進行優化，比如最大長度設定、字符串存儲和查找方式以及對于詞表的組織結構，比如采用TRIE索引樹、哈希索引等。
    > 
    > 2、基于統計的機器學習算法
    > 
    > 這類目前常用的是算法是HMM、CRF、SVM、深度學習等算法，比如stanford、Hanlp斷詞工具是基于CRF算法。以CRF爲例，基本思路是對漢字進行標注訓練，不僅考慮了詞語出現的頻率，還考慮上下文，具備較好的學習能力，因此其對歧義詞和未登錄詞的識別都具有良好的效果。
    > 
    > Nianwen Xue在其論文《Combining Classifiers for Chinese Word Segmentation》中首次提出對每個字符進行標注，通過機器學習算法訓練分類器進行斷詞，在論文《Chinese word segmentation as character tagging》中較爲詳細地闡述了基于字標注的斷詞法。
    > 
    > 常見的斷詞器都是使用機器學習算法和詞典相結合，一方面能夠提高斷詞准確率，另一方面能夠改善領域適應性。
    > 
    > 隨著深度學習的興起，也出現了基于神經網絡的斷詞器，例如有人員嘗試使用雙向LSTM+CRF實現斷詞器，其本質上是序列標注，所以有通用性，命名實體識別等都可以使用該模型，據報道其斷詞器字符准確率可高達97.5%。算法框架的思路與論文《Neural Architectures for Named Entity Recognition》類似，利用該框架可以實現中文斷詞，如下圖所示：
    > 
    > ![](https://scontent-tpe1-1.xx.fbcdn.net/v/t1.0-9/19429638_1896621840559761_8054285384926288490_n.png?_nc_cat=0&oh=8a0ff108dcc2e5c2487c5212b7ac805f&oe=5BB4F470)
    > 
    > 首先對語料進行字符嵌入，將得到的特征輸入給雙向LSTM，然後加一個CRF就得到標注結果。
    > 
    > 斷詞器當前存在問題：
    > 
    > 目前中文斷詞難點主要有三個：
    > 
    > 1、斷詞標准：比如人名，哈工大的標准中姓和名是分開的，但在Hanlp中是合在一起的。這需要根據不同的需求制定不同的斷詞標准。
    > 
    > 2、歧義：對同一個待切分字符串存在多個斷詞結果。
    > 
    > 歧義又分爲組合型歧義、交集型歧義和真歧義三種類型。
    > 
    > 1) 組合型歧義：斷詞是有不同的粒度的，指某個詞條中的一部分也可以切分爲一個獨立的詞條。比如“中華民國”，粗粒度的斷詞就是“中華民國”，細粒度的斷詞可能是“中華/民國”。
    > 
    > 2) 交集型歧義：在“高雄天和服裝廠”中，“天和”是廠名，是一個專有詞，“和服”也是一個詞，它們共用了“和”字。
    > 
    > 3) 真歧義：本身的語法和語義都沒有問題, 即便采用人工切分也會産生同樣的歧義，只有通過上下文的語義環境才能給出正確的切分結果。例如：對于句子“美國會通過對台售武法案”，既可以切分成“美國/會/通過對台軍售法案”，又可以切分成“美/國會/通過對台軍售法案”。
    > 
    > 一般在搜索引擎中，構建索引時和查詢時會使用不同的斷詞算法。常用的方案是，在索引的時候使用細粒度的斷詞以保證召回，在查詢的時候使用粗粒度的斷詞以保證精度。
    > 
    > 3、新詞：也稱未被詞典收錄的詞，該問題的解決依賴于人們對斷詞技術和漢語語言結構的進一步認識。
    > 
    > 另外，我們收集了如下部分斷詞工具，供參考：
    > 
    > 中國科學院計算所NLPIR： http://ictclas.nlpir.org/nlpir/
    > ansj斷詞器：https://github.com/NLPchina/ansj_seg
    > 哈工大的LTP： https://github.com/HIT-SCIR/ltp
    > 北京清華大學THULAC： https://github.com/thunlp/THULAC
    > Stanford斷詞器：https://nlp.stanford.edu/software/segmenter.shtml
    > Hanlp斷詞器：https://github.com/hankcs/HanLP
    > 結巴斷詞：https://github.com/yanyiwu/cppjieba
    > KCWS斷詞器(字嵌入+Bi-LSTM+CRF) ：https://github.com/koth/kcws
    > ZPar：https://github.com/frcchang/zpar/releases
    > IKAnalyzer： https://github.com/wks/ik-analyzer
    > 
    > 以及部分斷詞器的簡單說明：
    > 
    > 哈工大的斷詞器：主頁上給過調用接口，每秒請求的次數有限制。
    > 北京清華大學THULAC：目前已經有Java、Python和C++ 版本，並且代碼開源。
    > Stanford斷詞器：作爲衆多斯坦福自然語言處理中的一個包，目前最新版本3.7.0， Java實現的CRF算法。可以直接使用訓練好的模型，也提供訓練模型接口。
    > Hanlp斷詞：求解的是最短路徑。優點：開源、有人維護、可以解答。原始模型用的訓練語料是人民日報的語料，當然如果你有足夠的語料也可以自己訓練。
    > 結巴斷詞工具：基于前綴詞典實現高效的詞圖掃描，生成句子中漢字所有可能成詞情況所構成的有向無環圖 (DAG)；采用了動態規劃查找最大概率路徑, 找出基于詞頻的最大切分組合；對于未登錄詞，采用了基于漢字成詞能力的 HMM 模型，使用了 Viterbi 算法。
    > 字嵌入+Bi-LSTM+CRF斷詞器：本質上是序列標注，這個斷詞器用人民日報的80萬語料，據說按照字符正確率評估標准能達到97.5%的准確率，各位感興趣可以去看看。
    > ZPar斷詞器：新加坡科技設計大學開發的中文斷詞器，包括斷詞、詞性標注和Parser，支持多語言，據說效果是公開的斷詞器中最好的，C++ 語言編寫。
    > 
    > 關于速度：
    > 
    > 由于斷詞是基礎組件，其性能也是關鍵的考量因素。通常，斷詞速度跟系統的軟硬件環境有相關外，還與詞典的結構設計和算法複雜度相關。比如我們之前跑過字嵌入+Bi-LSTM+CRF斷詞器，其速度相對較慢。另外，開源項目 https://github.com/ysc/cws_evaluation 曾對多款斷詞器速度和效果進行過對比，可供大家參考。
    > 
    > 


### 結巴中文分詞/斷詞

- [fxsjy/jieba: 结巴中文分词](https://github.com/fxsjy/jieba)

### HuhuSeg

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

## 語意向量

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



## 文章向量


### Doc2Vec

#### 原理

- [深度学习笔记——Word2vec和Doc2vec原理理解并结合代码分析 - CSDN博客](https://blog.csdn.net/mpk_no1/article/details/72458003)

- [A gentle introduction to Doc2Vec – ScaleAbout – Medium](https://medium.com/scaleabout/a-gentle-introduction-to-doc2vec-db3e8c0cce5e)

- [How does doc2vec represent feature vector of a document? Can anyone explain mathematically how the process is done? - Quora](https://www.quora.com/How-does-doc2vec-represent-feature-vector-of-a-document-Can-anyone-explain-mathematically-how-the-process-is-done)

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

- Piyush Bhardwaj **Understanding Word2Vec and Document2Vec.** *Unfinished Notes* [[pdf]](https://piyushbhardwaj.github.io/documents/w2v_p2vupdates.pdf)


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

- [How Quid uses deep learning with small data](https://quid.com/feed/how-quid-uses-deep-learning-with-small-data)

- [[1405.4053] Distributed Representations of Sentences and Documents](https://arxiv.org/abs/1405.4053)


- [情感分析的新方法——基于Word2Vec/Doc2Vec/Python - OPEN 开发经验库](http://www.open-open.com/lib/view/open1444351655682.html)

- [doc2vec计算文档相似度 - 程序园](http://www.voidcn.com/article/p-fiwnobtj-dx.html)

- [Doc2Vec tutorial using Gensim – Andreas Klintberg – Medium](https://medium.com/@klintcho/doc2vec-tutorial-using-gensim-ab3ac03d3a1)

- [How does doc2vec represent feature vector of a document? Can anyone explain mathematically how the process is done? - Quora](https://www.quora.com/How-does-doc2vec-represent-feature-vector-of-a-document-Can-anyone-explain-mathematically-how-the-process-is-done)

- [jhlau/doc2vec: Python scripts for training/testing paragraph vectors](https://github.com/jhlau/doc2vec)


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





## Entropy

- [最大熵模型 (MaxEnt) 實踐短字詞分類 – PyLadies Taiwan – Medium](https://medium.com/pyladies-taiwan/%E6%9C%80%E5%A4%A7%E7%86%B5%E6%A8%A1%E5%9E%8B-maxent-%E5%AF%A6%E8%B8%90%E7%9F%AD%E5%AD%97%E8%A9%9E%E5%88%86%E9%A1%9E-b925665d9082)




## Models
- [DeepMind丨深度學習最新生成記憶模型，遠超RNN的GTMM](http://www.bigdatafinance.tw/index.php/tech/557-deepmind-rnn-gtmm)

### RNN+CNN

- [Representing Language with Recurrent and Convolutional Layers: An Authorship Attribution Example](https://hergott.github.io/language-representation-rnn-cnn/)

## 語意解析



### SLING

- [google/sling: SLING - A natural language frame semantics parser](https://github.com/google/sling)

- [自然語言理解技術大進展！免斷詞，Google語意框架剖析器SLING能自動找出語句架構 | iThome](https://www.ithome.com.tw/news/118415)

    > [Google最近開源釋出實驗性的語意框架剖析器（Parsing）SLING，](https://research.googleblog.com/2017/11/sling-natural-language-frame-semantic.html)有別於以往用斷詞的方式，SLING不需要靠人工的方式標註語句，而是可以透過語意框架（Frame Semantic Parsing）的方式自動抽取出文字所要描述的語意結構，再以語意框架圖（Semantic frame graph）的方式呈現，Google研究團隊表示，SLING是透過Tensorflow和Dragnn訓練過的標註語料庫，這是自然語言理解技術的一大進展，語意分析不再靠斷詞，而是從語言意義層面，自動標註出語句的結構。
    > 
    > SLING是採用一個特定用途的遞歸神經網路（Recurrent neural network，RNN）模型，在該框架圖上，透過輸入文字的遞增編輯動作，來計算輸出值，也就是說，該框架圖因為靈活的特性，可以擷取多個語意任務，SLING的語意剖析器只用了輸入詞句來訓練，沒有採用額外的生成的標註，像是語句相依性分析產生的標註。
    > 
    > ![](https://s4.itho.me/sites/default/files/images/sling.png)
    > 
    > 大部分的自然語言理解系統都是採用一種分析流程，從詞性標註 （Part-of-speech tagging），到透過語句相依性分析（Dependency parsing）來計算輸入的文字語意。這種模型較容易將不同的方析階段模組化，但是往往也導致一個問題，一旦產生錯誤將會影響整個模型的預測。
    > 
    > SLING輸出的語意框架圖可以直接擷取使用者感興趣的語意標示（Semantic annotation），也能避免系統流程中的設計缺陷，還能避免不必要的計算。
    > 
    > 舉例來說，傳統的自然語言理解系統會先執行語句相依性分析的工作，最後才會執行指代消解（Coreference resolution），指代消解是將指定代名詞還原為被替換的名詞，來避免重要的字詞因被替換為指定代名詞，而在計算權重時降低的問題，如果語句相依性分析過程若有錯誤，將會連帶影響最終輸出的結果。
    > 
    > ### 語意框架剖析的機制
    > 
    > 語意框架代表語句的意義，也是一個描述，每個描述都被稱為一個框架，該框架可被視為知識或是意義的單元，也包含了與其相關的概念或是框架的相互關係。SLING將每個框架組織成一個Slot的清單，每個Slot都有自己的角色或是名稱，以及代表的值，該代表值可以是個字詞的原意，或是與其他框架的連結。
    > 
    > 例如，Many people now claim to have predicted Black Monday這句話，SLING先辨識語句的實體、測量值和其他概念，實體像是人物、地點，事件，測量值像是時間、距離，其他概念則包含動詞，接著，將這些辨識出來的字詞分類到正確的語意角色，當作輸入值，因此，SLING會先將people視為人物框架、predicted是動詞類別框架、Black Monday是事件框架，predicted這個動詞表示為PREDICT-01框架，PREDICT-01框架與預測的主詞Slot有相互關係，因此，PREDICT-01與PERSON框架連接，除此之外，PREDICT-01框架也與被預測的受詞有相互關係，與Black Monday的EVENT框架連接。
    > 
    > ![](https://s4.itho.me/sites/default/files/images/%E7%AF%84%E4%BE%8B.PNG)
    > 
    > Google研究團隊認為，SLING透過語意框架，來訓練並優化遞歸神經網路。神經網路在隱藏層中學習到的知識，可以取代了人工標註特徵。
    > 
    > 該語意剖析器的輸入是以雙向長短記憶單元（Bi-directional LSTMs）演算法為基礎的轉換語意框架剖析方法，使用Transition Based Recurrent Unit (TBRU)來輸出，結合成一個訓練過的模型，只需要文字標註當作輸入，經過轉換系統，輸出語意框架圖形，不需要中間產生的標註（Intervening symbolic representation）。
    > 
    > 輸出層的文字在輸出後，還會經過轉換系統（Transition system），再重新進入輸入層，其中，轉換系統的一項關鍵機制是採用了固定大小的框架來記錄字詞對上下文預測的重要程度，也就是說，該框架是用來表示最近提及，或是在語句中被增強的關鍵字。Google研究團隊發現，透過這個簡單的機制，在擷取大量語意框架的關聯上，效率提升有非常多。
    > 
    > 目前，Google的研究團隊表示，SLING是研究語意剖析的實驗，Google已在Github將SLING開源釋出，提供開發人員預先訓練完成的語意剖析模型，可應用於知識萃取、解析複雜引用（Resolving complex references），以及對話理解等工作，未來，Google將會持續擴增SLING的功能。




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

### 寫稿機器人

- [百度AI开放平台-全球领先的人工智能服务平台](https://ai.baidu.com/support/news?action=detail&id=140)

- [只好跟著抄了！PTT 創世神的 AI Labs 為「記者快抄」打造寫稿機器人 | TechNews 科技新報](http://technews.tw/2017/08/09/ai-labs-is-using-ai-to-cover-ptt-news/)


## 機器翻譯

### 監督式

#### attention model

- [tensorflow/nmt: TensorFlow Neural Machine Translation Tutorial](https://github.com/tensorflow/nmt)

- [Attention Is All You Need：基於注意力機制的機器翻譯模型 – Youngmi huang – Medium](https://medium.com/@cyeninesky3/attention-is-all-you-need-%E5%9F%BA%E6%96%BC%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%A9%9F%E5%88%B6%E7%9A%84%E6%A9%9F%E5%99%A8%E7%BF%BB%E8%AD%AF%E6%A8%A1%E5%9E%8B-dcc12d251449)

- [[1706.03762] Attention Is All You Need](https://arxiv.org/abs/1706.03762)

- [Kyubyong/transformer: A TensorFlow Implementation of the Transformer: Attention Is All You Need](https://github.com/Kyubyong/transformer)

- [(4 封私信 / 23 条消息)如何理解谷歌团队的机器翻译新作《Attention is all you need》？ - 知乎](https://www.zhihu.com/question/61077555)

- [《Attention is All You Need》浅读（简介+代码） - 科学空间|Scientific Spaces](https://kexue.fm/archives/4765)





#### fastText

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



### 無監督

#### UNSUPERVISED MACHINE TRANSLATION 

- [《UNSUPERVISED MACHINE TRANSLATION USING MONOLINGUAL CORPORA ONLY》阅读笔记](https://zhuanlan.zhihu.com/p/32375955)

- [【Science】無監督式機器翻譯，不需要人類干預和平行文本 - 壹讀](https://read01.com/Rnzx84N.html)

    > 這兩篇使用非常相似的方法的新論文也可以在句子層面進行翻譯。它們都使用兩種訓練策略，稱為反向翻譯和去噪（Back translation and Denoising）。在反向翻譯中，先把一種語言的句子大致翻譯成另一種語言，然後再翻譯回原來的語言。如果翻譯後的句子與最初的句子不一致，則調整神經網絡再次翻譯，直到變得越來越接近。
    > 
    > 去噪與反向翻譯類似，但不是從一種語言到另一種語言然後再回來，而是從一種語言（通過重新排列或刪除單詞）中添加噪聲，並嘗試將其翻譯回最開始的語言。這些方法的組合，能夠教給網絡更深層次的語言結構。
    > 
    > 但是兩種技術之間還是有著細微的差異。 UPV的系統在訓練期間更頻繁地進行反向翻譯。由位於賓夕法尼亞州匹茲堡的 Facebook 計算機科學家Guillaume Lample和合作者創建的另一個系統在翻譯過程中則增加了一個額外的步驟。在將一個語言解碼為另一種語言之前，這兩個系統都將其從一種語言編碼為更抽象的表示，但Facebook系統的研究員認為，其系統的「中間語言」是真正抽象的。 Artetxe和Lample都表示，他們可以通過應用對方論文的技巧來改善結果。
    > 
    > 兩篇論文之間唯一可以直接比較的結果是從以包含了3000萬句子的英法文本資料庫中進行的翻譯，兩個系統都在雙語評估替補評分（用來衡量翻譯的準確性）上的得分都在15分左右 。這個數字還比不上谷歌翻譯。谷歌翻譯使用有監督的方法，在同類測試上的得分是40多左右，人類水平是50分左右。但是，這些方法都比詞對詞的翻譯要好。


#### CipherGAN

- [无平行文本照样破解密码，CipherGAN有望提升机器翻译水平](https://zhuanlan.zhihu.com/p/33672256)

    > 针对CipherGAN可以使用非平行文本作输入的特点，Gomez在接受Newsweek外媒采访的时候，也提到了，“密码破译的模型思路也能迁移到非监督学习的翻译上。”
    > 
    > 因为语言翻译常面临的难题是，缺乏足够的平行语料。
    > 
    > 正好和非配对明文密文的密码破译过程很相似。
    > 
    > 


## 閱讀理解

### SQuAD

- [机器这次击败人之后，争论一直没平息 | SQuAD风云](https://mp.weixin.qq.com/s?__biz=MzIzNjc1NzUzMw==&mid=2247493419&idx=1&sn=73425fec04482f14f6b9b7316e425e63&chksm=e8d05059dfa7d94fc1457a36d4f62cb1b8a057ce18388fbad448aa6b53f4dbb1299cfd697724&scene=21#wechat_redirect)


SQuAD被称为行业公认的机器阅读理解顶级水平测试，可以理解为机器阅读理解领域的ImageNet。它们同样出自斯坦福，同样是一个数据集，搭配一个竞争激烈的竞赛。

这个竞赛基于SQuAD问答数据集，考察两个指标：EM和F1。

EM是指精确匹配，也就是模型给出的答案与标准答案一模一样；F1，是根据模型给出的答案和标准答案之间的重合度计算出来的，也就是结合了召回率和精确率。

目前阿里、微软团队并列第一，其中EM得分微软（r-net+融合模型）更高，F1得分阿里（SLQA+融合模型）更高。但是他们在EM成绩上都击败了“人类表现”。

---

2016年，斯坦福大学从维基百科上随机选取了536篇文章，随后采用众包的方式，由人类阅读这些文章后，提出问题并人工标注出答案，构成了包含10万多个问题的阅读理解数据集SQuAD。

对于这样一个数据集，以色列巴伊兰大学的著名NLP研究者Yoav Goldberg的评价是太局限（restricted）了。


早在好几个月之前，AI在SQuAD上接近人类得分的时候，Goldberg就专门写了个PPT，把SQuAD批判了一番。

![](http://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtD6fFYcb6DzyJFYv9qXbIXrhnSnicBCVRib5QEQ9QvplO5Jb1gicibv4xfnK4VOlxMTBImGVvcnuAlibPQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1)

他列举了SQuAD的三大不足：

-   受限于可以选择span来回答的问题；

-   需要在给定的段落里寻找答案；

-   段落里保证有答案。

对于这些不足，DeepMind前不久发布的[NarrativeQA论文](http://mp.weixin.qq.com/s?__biz=MzIzNjc1NzUzMw==&mid=2247492423&idx=2&sn=c02f90e09a49c5c41d7aac3472573b94&chksm=e8d05435dfa7dd235aeb66aae46bc619f3cb6940d88b5d00b34204c3e38757f48480de2c6f6f&scene=21#wechat_redirect)做了更详细的说明。

---

他们认为，由于SQuAD问题的答案必须是给定段落中的内容，这就导致很多评估阅读理解能力应该用到的合情合理的问题，根本没法问。

同时，这种简单的答案通过文档表面的信号就能提取出来，对于无法用文中短语来回答、或者需要用文中几个不连续短语来回答的问题，SQuAD训练出来的模型无法泛化。

另外，SQuAD虽然问题很多，但其实用到的文章又少又短，这就限制了整个数据集词汇和话题的多样性。

因此，SQuAD上表现不错的模型，如果要用到更复杂的问题上，可扩展性和适用性都很成问题。


## 文章分類器


### 垃圾郵件

- [Spam detection using neural networks in Python – Emergent // Future – Medium](https://medium.com/emergent-future/spam-detection-using-neural-networks-in-python-9b2b2a062272)

#### dataset

- [UCI Machine Learning Repository: Spambase Data Set](https://archive.ics.uci.edu/ml/datasets/Spambase)

## 機器摘要


### 2017


- [Salesforce research](https://einstein.ai/research/your-tldr-by-an-ai-a-deep-reinforced-model-for-abstractive-summarization)

    - [[1705.04304] A Deep Reinforced Model for Abstractive Summarization](https://arxiv.org/abs/1705.04304)


## 法律文件NLP

- [如何找判決 – 一起讀判決](https://casebf.com/2018/01/16/case_search/)

- [裁判書查詢](http://jirs.judicial.gov.tw/FJUD/FJUDQRY01M_1.aspx)

- [lawsnote.com/](https://lawsnote.com/)

- [KWIC 關鍵字](http://www.taiwanlii.ccu.edu.tw/lawstd_keywordspicker/)

- [台灣法律資訊中心 Taiwan Legal Information Institute](http://www.taiwanlii.ccu.edu.tw/Tool.php)

### 判決書 dataset

- [jrf_data - g0v.hackpad.tw](https://g0v.hackpad.tw/jrf_data-BlLdzEsImuv)


