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


### test.test_doc2vec.ConcatenatedDoc2Vec

- [test.test_doc2vec — gensim 3.2.0 documentation](https://www.pydoc.io/pypi/gensim-3.2.0/autoapi/test/test_doc2vec/index.html#test.test_doc2vec.ConcatenatedDoc2Vec)




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

## LDA

### model

- [gensim: models.ldamodel – Latent Dirichlet Allocation](https://radimrehurek.com/gensim/models/ldamodel.html#gensim.models.ldamodel.LdaModel.update)

    > id2word ({dict of (int, str), gensim.corpora.dictionary.Dictionary}) – Mapping from word IDs to words. It is used to determine the vocabulary size, as well as for debugging and topic printing.



### update with unseen words (hash trick)

- [gensim lda model - calling update on a corpus with unseen words - Stack Overflow](https://stackoverflow.com/questions/22196248/gensim-lda-model-calling-update-on-a-corpus-with-unseen-words)

    > No, you must use the same dictionary (mapping between words and their integer ids) for both training, updates and inference.
    > 
    > Which means you can update the model with new documents, but not with new word types.
    > 
    > Check out the [HashDictionary](http://radimrehurek.com/gensim/corpora/hashdictionary.html) class which uses the "hashing trick" to work around this limitation (but the hashing trick comes with its own caveats).



- [gensim: corpora.hashdictionary – Construct word<->id mappings](https://radimrehurek.com/gensim/corpora/hashdictionary.html)

    > **debug** (*bool**,* *optional*) -- Store which tokens have mapped to a given id? **Will use a lot of RAM**. If you find yourself running out of memory (or not sure that you really need raw tokens), keep *debug=False*.
    > 

- [corpora.hashdictionary — gensim 3.2.0 documentation](https://www.pydoc.io/pypi/gensim-3.2.0/autoapi/corpora/hashdictionary/index.html)

    > `restricted_hash`(*token*)
    > 
    > Calculate id of the given token. Also keep track of what words were mapped to what ids, for debugging reasons.

- [gensim: corpora.dictionary – Construct word<->id mappings](https://radimrehurek.com/gensim/corpora/dictionary.html#gensim.corpora.dictionary.Dictionary)

    > `token2id`
    > 
    > *dict of (str, int)* -- token -> tokenId.
    > 
    > `id2token`
    > 
    > *dict of (int, str)* -- Reverse mapping for token2id, initialized in a lazy manner to save memory (not created until needed).
    > 

### update with unseen words (filter out vocabulary by VocabTransform)

- [update LdaMulticore/lda model with new document - Google 網上論壇](https://groups.google.com/forum/#!msg/gensim/2KzJNYQSJxA/QiLYdfnGCgAJ)

    > You can update the model by calling `lda_model.update`. Please note that once the model is trained there is no way to increase the vocabulary, so you need to filter out the new out-of-vocabulary(OOV) words using [VocabTransform](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2FRaRe-Technologies%2Fgensim%2Fwiki%2FRecipes-%26-FAQ%23q8-how-can-i-filter-a-saved-corpus-and-its-corresponding-dictionary&sa=D&sntz=1&usg=AFQjCNGIGWhUaZLyPFJ1KrmUF5GG5m3AjA).
    > 


- [Recipes & FAQ · RaRe-Technologies/gensim Wiki](https://github.com/RaRe-Technologies/gensim/wiki/Recipes-&-FAQ#q8-how-can-i-filter-a-saved-corpus-and-its-corresponding-dictionary)

    > ### Q8: How can I filter a saved corpus and its corresponding dictionary?
    > 
    > **Answer:** (by [Yaser Martinez](https://github.com/elyase))
    > 
    > The function `dictionary.filter_extremes` changes the original IDs so we need to reread and (optionally) rewrite the old corpus using a transformation:
    > 
    > ```source-python
    > import copy
    > from gensim.models import VocabTransform
    > 
    > # filter the dictionary
    > old_dict = corpora.Dictionary.load('old.dict')
    > new_dict = copy.deepcopy(old_dict)
    > new_dict.filter_extremes(keep_n=100000)
    > new_dict.save('filtered.dict')
    > 
    > # now transform the corpus
    > corpus = corpora.MmCorpus('corpus.mm')
    > old2new = {old_dict.token2id[token]:new_id for new_id, token in new_dict.iteritems()}
    > vt = VocabTransform(old2new)
    > corpora.MmCorpus.serialize('filtered_corpus.mm', vt[corpus], id2word=new_dict)
    > 
    > ```
    > 
    > 

## Troubleshooting

### AttributeError: 'Doc2Vec' object has no attribute 'syn1'

- [Doc2Vec.infer_vector: AttributeError: 'Doc2Vec' object has no attribute 'syn1' · Issue #483 · RaRe-Technologies/gensim](https://github.com/RaRe-Technologies/gensim/issues/483)

    > I think it's clear now. `model.infer_vectors` trains the new documents with the neural weights of the actual model (<https://github.com/piskvorky/gensim/blob/develop/gensim/models/doc2vec.py#L684>).
    > As `model.init_sims(replace=True)` is deleting them for memory save reasons, the method `model.infer_vectors` can not work. It's the same reason why `model.train` is not working after `model.init_sims(replace=True)`.

### infer most similar vector from ConcatenatedDocvecs

- [python - Doc2Vec: infer most similar vector from ConcatenatedDocvecs - Stack Overflow](https://stackoverflow.com/questions/54186233/doc2vec-infer-most-similar-vector-from-concatenateddocvecs)

    > The `ConcatenatedDocvecs` is a simple utility wrapper class that lets you access the concatenation of a tag's vectors in multiple underlying `Doc2Vec` models. It exists to make it a little easier to reproduce some of the analysis in the original 'ParagraphVector' paper.
    > 
    > It doesn't reproduce all the functionality of a `Doc2Vec` model (or set of keyed-vectors), so can't directly hep you with the `most_similar()` you want to perform.
    > 
    > You could instead do a most-similar operation within each of the constituent models, then combine the two similarity measures (per neighbor) -- such as by averaging them -- to get a usable similarity-like value for the combined model (and then re-sort on that). I suspect, but am not sure, such a value from the two 100d models would behave very much like a a true cosine-similarity from the concatenated 200d model.
    > 
    > Alternatively, instead of using `ConcatenatedDoc2Vec` wrapper class (which only creates and returns the concatenated 200d vectors when requested), you could look at the various `KeyedVectors` class in gensim, and use (or adapt) one to be filled with all the concatenated 200d vectors from the two constituent models. Then, its `most_similar()` would work.
    > 

# pytext

- [PyText | Deep Learning Framework | Facebook AI](https://facebook.ai/developers/tools/pytext?fbclid=IwAR0PBLPOf5jZ8xvEIerFMWZbdkDFAp5DOoJ5Fwqfwp-p1B20NnBllANqMlo)

- [PyText Documentation — PyText documentation](https://pytext-pytext.readthedocs-hosted.com/en/latest/)

    > **Core PyText Features:**
    > 
    > -   Production ready models for various NLP/NLU tasks:
    >     -   Text classifiers
    >         -   [Yoon Kim (2014): Convolutional Neural Networks for Sentence Classification](https://arxiv.org/abs/1408.5882)
    >         -   [Lin et al. (2017): A Structured Self-attentive Sentence Embedding](https://arxiv.org/abs/1703.03130)
    >     -   Sequence taggers
    >         -   [Lample et al. (2016): Neural Architectures for Named Entity Recognition](https://www.aclweb.org/anthology/N16-1030)
    >     -   Joint intent-slot model
    >         -   [Zhang et al. (2016): A Joint Model of Intent Determination and Slot Filling for Spoken Language Understanding](https://www.ijcai.org/Proceedings/16/Papers/425.pdf)
    >     -   Contextual intent-slot models
    > -   Extensible components that allow easy creation of new models and tasks
    > -   Ensemble training support
    > -   Distributed-training support (using the new C10d backend in PyTorch 1.0)
    > -   Reference implementation and a pre-trained model for the paper: [Gupta et al. (2018): Semantic Parsing for Task Oriented Dialog using Hierarchical Representations](http://aclweb.org/anthology/D18-1300)
    > 
- [Pytext: A natural language modeling framework based on PyTorch | Hacker News](https://news.ycombinator.com/item?id=18682627)

    > Could you guys elaborate on the relationship between PyText, torchtext, and AllenNLP? I've briefly used the latter two, but with how quickly things are moving it'd be nice to have a quick answer from the devs themselves.
    > 
    > 
    > [ahhegazy77](https://news.ycombinator.com/user?id=ahhegazy77 "User profile") ![](moz-extension://669356ce-356f-4477-af7f-b5e5ef151d5a/images/tag.svg "Tag user")    [5 days ago](https://news.ycombinator.com/item?id=18687690)
    > 
    > PyText dev here, Torchtext provides a set of data-abstractions that helps reading and processing raw text data into PyTorch tensors, at the moment we use Torchtext in PyText for training-time data reading and preprocessing.
    > 
    > AllenNLP is a great NLP modeling library that is aimed at providing reference implementations and prebuilt state-of-the-art models, and make it easy to iterate on and research with models for different NLP tasks.
    > 
    > We've built PyText to be a rich NLP modeling library (along the lines of AllenNLP) but with production capabilities baked in the design from day 1.
    > 
    > Examples are: - We provide interfaces to make sure data preprocessing can be consistent between training and runtime - The model interfaces are compatible with ONNX and torch.jit - A core goal for us in the next few month is to be able to run models trained in PyText on mobile.
    > 
    > Among other differences like supporting distributed training and multi-task learning.
    > 
    > That being said, so far our library of models has been mostly influenced by our current production use-cases, we are actively working on enriching this library with more models and tasks while keeping production capabilities and inference speed in mind.
    > 
    > ---
    > 
    > 
    > [bethebunny](https://news.ycombinator.com/user?id=bethebunny "User profile") ![](moz-extension://669356ce-356f-4477-af7f-b5e5ef151d5a/images/tag.svg "Tag user")    [6 days ago](https://news.ycombinator.com/item?id=18683506)
    > 
    > AllenNLP is great, and influenced the design of PyText in several ways. There are some central design decisions of AllenNLP that make it incompatible with PyTorch's jit tracing and so make productionizing models require much more manual work. It also generally leaves preprocessing up to the user, so preprocessing consistently between training and inference is outside the scope of what AllenNLP does.
    > 

# AllenNLP

- [AllenNLP](https://allennlp.org/)

    > AllenNLP makes it easy to design and evaluate new deep learning models for nearly any NLP problem, along with the infrastructure to easily run them in the cloud or on your laptop.
    > 




## Building a fancy model for text classification

- [Deep Learning for text made easy with AllenNLP – The Startup – Medium](https://medium.com/swlh/deep-learning-for-text-made-easy-with-allennlp-62bc79d41f31)

    - [都说AllenNLP好用，我们跑一遍看看究竟多好用 | 雷锋网](https://www.leiphone.com/news/201804/i7qpRI9oYHVMfGCm.html)


## Training a Sentiment Analyzer using AllenNLP

- [Training a Sentiment Analyzer using AllenNLP (in less than 100 lines of Python code) – Real-World Natural Language Processing](http://www.realworldnlpbook.com/blog/training-sentiment-analyzer-using-allennlp.html)

## ELMo: Deep contextualized word representations

- [ELMo: Deep contextualized word representations](https://allennlp.org/elmo)

    > ELMo representations are:
    > 
    > -   *Contextual*: The representation for each word depends on the entire context in which it is used.
    > -   *Deep*: The word representations combine all layers of a deep pre-trained neural network.
    > -   *Character based*: ELMo representations are purely character based, allowing the network to use morphological clues to form robust representations for out-of-vocabulary tokens unseen in training.