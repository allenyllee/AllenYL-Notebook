# Python__機器學習3-1_自然語言

[toc]
<!-- toc --> 

# jieba 結巴 中文斷詞

- [Python中文分词 jieba 十五分钟入门与进阶 - CSDN博客](https://blog.csdn.net/fontthrone/article/details/72782499)
- [结巴中文分词的用法 - 简书](https://www.jianshu.com/p/e8b5d01ca073)

- [fxsjy/jieba: 结巴中文分词](https://github.com/fxsjy/jieba)

    ```python
    >>> import jieba.posseg as pseg
    >>> words = pseg.cut("我爱北京天安门")
    >>> for word, flag in words:
    ...    print('%s %s' % (word, flag))
    ...
    我 r
    爱 v
    北京 ns
    天安门 ns
    ```
    
- [jieba（结巴）分词种词性简介 - CSDN博客](http://blog.csdn.net/suibianshen2012/article/details/53487157)

    |代號|詞性|解釋|
    |------------------|---------------------|---------------------|
    | Ag | 形语素 | 形容词性语素。形容词代码为 a，语素代码ｇ前面置以A。 |
    | a | 形容词 | 取英语形容词 adjective的第1个字母。 |
    | ad | 副形词 | 直接作状语的形容词。形容词代码 a和副词代码d并在一起。 |
    | an | 名形词 | 具有名词功能的形容词。形容词代码 a和名词代码n并在一起。 |
    | b | 区别词 | 取汉字“别”的声母。 |
    | c | 连词 | 取英语连词 conjunction的第1个字母。 |
    | dg | 副语素 | 副词性语素。副词代码为 d，语素代码ｇ前面置以D。 |
    | d | 副词 | 取 adverb的第2个字母，因其第1个字母已用于形容词。 |
    | e | 叹词 | 取英语叹词 exclamation的第1个字母。 |
    | f | 方位词 | 取汉字“方” |
    | g | 语素 | 绝大多数语素都能作为合成词的“词根”，取汉字“根”的声母。 |
    | h | 前接成分 | 取英语 head的第1个字母。|
    | i | 成语 | 取英语成语 idiom的第1个字母。|
    | j | 简称略语 | 取汉字“简”的声母。 |
    | k | 后接成分 |   |
    | l | 习用语 | 习用语尚未成为成语，有点“临时性”，取“临”的声母。 |
    | m | 数词 | 取英语 numeral的第3个字母，n，u已有他用。 |
    | Ng | 名语素 | 名词性语素。名词代码为 n，语素代码ｇ前面置以N。 |
    | n | 名词 | 取英语名词 noun的第1个字母。|
    | nr | 人名 | 名词代码 n和“人(ren)”的声母并在一起。 |
    | ns | 地名 | 名词代码 n和处所词代码s并在一起。 |
    | nt | 机构团体 | “团”的声母为 t，名词代码n和t并在一起。 |
    | nz | 其他专名 | “专”的声母的第 1个字母为z，名词代码n和z并在一起。 |
    | o | 拟声词 | 取英语拟声词 onomatopoeia的第1个字母。 |
    | p | 介词 | 取英语介词 prepositional的第1个字母。 |
    | q | 量词 | 取英语 quantity的第1个字母。|
    | r | 代词 | 取英语代词 pronoun的第2个字母,因p已用于介词。 |
    | s | 处所词 | 取英语 space的第1个字母。 |
    | tg | 时语素 | 时间词性语素。时间词代码为 t,在语素的代码g前面置以T。 |
    | t | 时间词 | 取英语 time的第1个字母。 |
    | u | 助词 | 取英语助词 auxiliary |
    | vg | 动语素 | 动词性语素。动词代码为 v。在语素的代码g前面置以V。 |
    | v | 动词 | 取英语动词 verb的第一个字母。 |
    | vd | 副动词 | 直接作状语的动词。动词和副词的代码并在一起。 |
    | vn | 名动词 | 指具有名词功能的动词。动词和名词的代码并在一起。 |
    | w | 标点符号 |   |
    | x | 非语素字 | 非语素字只是一个符号，字母 x通常用于代表未知数、符号。 |
    | y | 语气词 | 取汉字“语”的声母。 |
    | z | 状态词 | 取汉字“状”的声母的前一个字母。 |
    | un | 未知词 | 不可识别词及用户自定义词组。取英文Unkonwn首两个字母。(非北大标准，CSW分词中定义) |

## 自定義詞帶特殊符號

- [jieba分词支持关键词带空格和特殊字符 - 王佩的CSDN博客 - CSDN博客](https://blog.csdn.net/wangpei1949/article/details/57077007)

    > 中英文中存在大量这样的专有名词。这种方式有时并不符合我们的需求。我们可以通过改jieba包 **`init.py`** 中几个正则表达式来解决这个问题。用户词典中词词性用`@@`分隔。
    > 
    > 1. 搜索
    >     ```
    >     re_han_default = re.compile("([\u4E00-\u9FD5a-zA-Z0-9+#&._]+)", re.U)
    >     ```
    >     改成
    >     ```
    >     re_han_default = re.compile("(.+)", re.U)
    >     ```
    > 
    > 2. 搜索
    >     ```
    >     re_userdict = re.compile('^(.+?)( [0-9]+)?( [a-z]+)?＄', re.U)
    >     ```
    >     改成
    >     ```
    >     re_userdict = re.compile('^(.+?)(\u0040\u0040[0-9]+)?(\u0040\u0040[a-z]+)?$', re.U)
    >     ```
    > 
    > 3. 搜索
    >     ```
    >     word, freq = line.split(' ')[:2]
    >     ```
    >     改成
    >     ```
    >     word, freq = line.split('\u0040\u0040')[:2]
    >     ```
    > 
    > 4. 补充：若用全模式继续改。
    >     搜索
    >     ```
    >     re_han_cut_all = re.compile("([\u4E00-\u9FD5]+)", re.U)
    >     ```
    >     改成
    >     ```
    >     re_han_cut_all = re.compile("(.+)", re.U)
    >     ```
    > 
    > ```
    > #修改后测试
    > userDict：
    > 中华人民共和国@@n
    > People's Republic of China@@n
    > World Economic Forum@@n
    > 世界经济论坛@@n
    > 
    > 结果：
    > People's Republic of China     is     the     only     legitimate     government     in     China  .
    > World Economic Forum
    > Edu Trust认证
    > ```
    > 

    > -   [promisejia：](https://my.csdn.net/promisejia) 用你的方法修改了init.py.还是仅对中文有效，对特殊字符无效，博主知道怎么回事吗？(3个月前#1楼)收起回复
    > 
    >     -   [promisejia](https://my.csdn.net/promisejia)回复 promisejia： 软件重启一下就可以了，感谢博主(3个月前)举报回复
    > 




# gensim

## API

- [gensim: models.word2vec – Deep learning with word2vec](https://radimrehurek.com/gensim/models/word2vec.html)


    > Parameters:	
    > 
    > - __sg (int {1, 0})__ – Defines the training algorithm. If 1, skip-gram is employed; otherwise, CBOW is used.
    > - __size (int)__ – Dimensionality of the feature vectors.
    > - __window (int)__ – The maximum distance between the current and predicted word within a sentence.
    > - __alpha (float)__ – The initial learning rate.
    > - __min_alpha (float)__ – Learning rate will linearly drop to min_alpha as training progresses.
    > - __seed (int)__ – Seed for the random number generator. Initial vectors for each word are seeded with a hash of the concatenation of word + str(seed). Note that for a fully deterministically-reproducible run, you must also limit the model to a single worker thread (workers=1), to eliminate ordering jitter from OS thread scheduling. (In Python 3, reproducibility between interpreter launches also requires use of the PYTHONHASHSEED environment variable to control hash randomization).
    > - __min_count (int)__ – Ignores all words with total frequency lower than this.
    > - __max_vocab_size (int)__ – Limits the RAM during vocabulary building; if there are more unique words than this, then prune the infrequent ones. Every 10 million word types need about 1GB of RAM. Set to None for no limit.
    > - __sample (float)__ – The threshold for configuring which higher-frequency words are randomly downsampled, useful range is (0, 1e-5).
    > - __workers (int)__ – Use these many worker threads to train the model (=faster training with multicore machines).
    > - __hs (int {1,0})__ – If 1, hierarchical softmax will be used for model training. If set to 0, and negative is non-zero, negative sampling will be used.
    > - __negative (int)__ – If > 0, negative sampling will be used, the int for negative specifies how many “noise words” should be drawn (usually between 5-20). If set to 0, no negative sampling is used.
    > - __cbow_mean (int {1,0})__ – If 0, use the sum of the context word vectors. If 1, use the mean, only applies when cbow is used.
    > - __hashfxn (function)__ – Hash function to use to randomly initialize weights, for increased training reproducibility.
    > - __iter (int)__ – Number of iterations (epochs) over the corpus.
    > - __trim_rule (function)__ – Vocabulary trimming rule, specifies whether certain words should remain in the vocabulary, be trimmed away, or handled using the default (discard if word count < min_count). Can be None (min_count will be used, look to keep_vocab_item()), or a callable that accepts parameters (word, count, min_count) and returns either gensim.utils.RULE_DISCARD, gensim.utils.RULE_KEEP or gensim.utils.RULE_DEFAULT. Note: The rule, if given, is only used to prune vocabulary during build_vocab() and is not stored as part of the model.
    > - __sorted_vocab (int {1,0})__ – If 1, sort the vocabulary by descending frequency before assigning word indexes.
    > - __batch_words (int)__ – Target size (in words) for batches of examples passed to worker threads (and thus cython routines).(Larger batches will be passed if individual texts are longer than 10000 words, but the standard cython code truncates to that maximum.)
    > - __compute_loss (bool)__ – If True, computes and stores loss value which can be retrieved using model.get_latest_training_loss().
    > - __callbacks__ – List of callbacks that need to be executed/run at specific stages during training.
    > 
    > 

## filter out words with low tf-idf in a corpus

- [python - How to filter out words with low tf-idf in a corpus with gensim? - Stack Overflow](https://stackoverflow.com/questions/24688116/how-to-filter-out-words-with-low-tf-idf-in-a-corpus-with-gensim)

    > Say you have a document `tfidf_doc` which generated by gensim's `TfidfModel()` with the corresponding bag of words document `bow_doc`, and you want to filter words that have tfidf value lower then `cut_percent`% of words in this document, you can call `tfidf_filter(tfidf_doc, cut_percent)`, then it will return a cut version of `tfidf_doc`:
    > 
    > ```python
    > def tfidf_filter(tfidf_doc, cut_percent):
    > 
    >     sorted_by_tfidf = sorted(tfidf_doc, key=lambda tup: tup[1])
    >     cut_value = sorted_by_tfidf[int(len(sorted_by_tfidf)*cut_percent)][1]
    > 
    >     #print('before cut:',len(tfidf_doc))
    > 
    >     #print('cut value:', cut_value)
    >     for i in range(len(tfidf_doc)-1, -1, -1):
    >         if tfidf_doc[i][1] < cut_value:
    >             tfidf_doc.pop(i)
    > 
    >     #print('after cut:',len(tfidf_doc))
    > 
    >     return tfidf_doc
    > ```
    > 
    > Then you want to filter the document `bow_doc` by the resulting `tfidf_doc`, jsut call `filter_bow_by_tfidf(bow_doc, tfidf_doc)`, it will return cut version of `bow_doc`:
    > 
    > ```python
    > def filter_bow_by_tfidf(bow_doc, tfidf_doc):
    >     bow_idx = len(bow_doc)-1
    >     tfidf_idx = len(tfidf_doc)-1
    > 
    >     #print('before :', len(bow_doc))
    > 
    >     while True:
    >         if bow_idx < 0: break
    > 
    >         if tfidf_idx < 0:
    >             #print('pop2 :', bow_doc.pop(bow_idx))
    >             bow_doc.pop(bow_idx)
    >             bow_idx -= 1
    >         if bow_doc[bow_idx][0] > tfidf_doc[tfidf_idx][0]:
    >             #print('pop1 :', bow_doc.pop(bow_idx))
    >             bow_doc.pop(bow_idx)
    >             bow_idx -= 1
    >         if bow_doc[bow_idx][0] == tfidf_doc[tfidf_idx][0]:
    >             #print('keep :', bow_doc[bow_idx])
    >             bow_idx -= 1
    >             tfidf_idx -= 1
    > 
    >     #print('after :', len(bow_doc))
    > 
    >     return bow_doc
    > ```
