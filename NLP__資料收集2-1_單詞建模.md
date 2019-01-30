# NLP__資料收集2-1_單詞建模

[toc]
<!-- toc --> 

# 預訓練的詞嵌入

## Tencent AI Lab

- [Embedding Dataset -- NLP Center, Tencent AI Lab](https://ai.tencent.com/ailab/nlp/embedding.html?fbclid=IwAR3AtJVJ608RToZ5-S_7z1_raAlF0EvjhSGmXlNDgjgJ2xzmIHrgD194Gdk)

## Chinsese_word_vectors(繁體、簡體)

- [candlewill/Chinsese_word_vectors: Chinsese_word_vectors](https://github.com/candlewill/Chinsese_word_vectors)

## fastText

- [fastText/pretrained-vectors.md at master · facebookresearch/fastText](https://github.com/facebookresearch/fastText/blob/master/pretrained-vectors.md)

- [Word vectors for 157 languages · fastText](https://fasttext.cc/docs/en/crawl-vectors.html)

## Chinese Word Vectors 中文词向量(簡體)

- [Embedding/Chinese-Word-Vectors: 100+ Chinese Word Vectors 上百种预训练中文词向量](https://github.com/Embedding/Chinese-Word-Vectors)


## Bert

- [bert/multilingual.md at master · google-research/bert](https://github.com/google-research/bert/blob/master/multilingual.md)




# 詞嵌入

## CoNLL 2018 | 最佳论文揭晓：词嵌入获得的信息远比我们想象中的要多得多

- [[1809.02094] Uncovering divergent linguistic information in word embeddings with lessons for intrinsic and extrinsic evaluation](https://arxiv.org/abs/1809.02094)

- [CoNLL 2018 | 最佳论文揭晓：词嵌入获得的信息远比我们想象中的要多得多 ](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650751000&idx=3&sn=e52b5c0b67e3a671e97c73fcc2f711c3&chksm=871a8466b06d0d70fabfe043e5bcd8fd1ffb835fa749023d867a2eed05def79b0a0152b4b3df&mpshare=1&scene=24&srcid=#rd)

    > 虽然从理论角度理解这些模型是更加活跃的研究路线，但这些研究背后的基本思路都是为类似的单词分配类似的向量表征。由此，大部分词嵌入模型依赖来自大型单语语料库的共现统计信息（co-occurrence statistics），并遵循分布假设，也就是相似单词倾向于出现在相似语境中。
    > 
    > 然而，上述论点没有定义「相似单词」的含义，且词嵌入模型实际中应该捕捉哪种关系也不完全清楚。因此一些研究者在真正相似度（如 car - automobile）与关联度（如 car - road）之间进行区分。从另一个角度来说，词语相似度可聚焦在语义（如 sing-chant）或者句法（如 sing-singing）上。我们把这两个方面作为相似度的两个坐标轴，且每一个坐标轴的两端为两种性质：语义/句法轴和相似度/关联度轴。
    > 
    > 本论文提出了一种新方法来调整给定的任意嵌入向量集，使其在这些坐标轴中靠近特定端点。该方法受一阶和二阶共现研究的启发，可推广为词嵌入向量线性变换的连续参数，我们称之为相似度阶（similarity order）。虽然业内提出了多种学习特定词嵌入的方法，但之前的研究明确地改变了训练目标，且总是依赖知识库这样的外部资源。而本论文提出的方法可用做任意预训练词嵌入模型的后处理，不需要任何额外资源。同样，该研究表明，标准的词嵌入模型能够编码不同的语言信息，但能够直接应用的信息有限。此外，该研究也分析了该方法与内部评估和下游任务的关系。该论文主要贡献如下：
    > 
    > 1\. 提出了一个具备自由参数的线性变换，能够调整词嵌入在相似度/关联度和语义/句法坐标轴中的性能，并在词汇类推数据集和相似度数据集中进行了测试。
    > 
    > 2\. 展示了当前词嵌入方法的性能受到无法同时显现不同语言信息（例如前面提到的坐标轴）的限制。该研究提出的方法表明，词嵌入能够捕获的信息多于表面显现出的信息。
    > 
    > 3\. 展示了标准的内部评估只能给出一个静态的不完整图景，加上该研究提出的方法能够帮助我们更好地理解词嵌入模型真正编码哪些信息。
    > 
    > 4\. 展示了该方法也能运用到下游任务中，但相比于使用一般词嵌入作为输入特征的监督系统，其效果在直接使用词嵌入相似度的无监督系统上更显著，因为监督系统有足够的表达能力来学习最优变换。
    > 
    > 总之，该研究揭示了词嵌入如何表示不同语言信息，分析了它在内部评估和下游任务中所扮演的角色，为之后的发展开创了新机遇。
    > 
    > **论文：Uncovering divergent linguistic information in word embeddings with lessons for intrinsic and extrinsic evaluation**
    > 
    > 
    > 论文链接：https://arxiv.org/abs/1809.02094


## 訓練 word vector

### wikipedia 训练繁体中文 embedding(word2vec)模型

- [wikipedia 训练繁体中文 embedding(word2vec)模型 - Jasmine_dream - CSDN博客](https://blog.csdn.net/huhehaotechangsha/article/details/81171619)

    > 由于课题任务需要一个繁体中文的word3vec, 折腾经过记录在此。希望以后少掉几个坑。
    > 训练好的embedding放在[网盘](https://pan.baidu.com/s/1DB_Sft8N9XMyDP9cpVMpBw)中， 密码：`2um0`
    > 
    > 后来又按照这个方法训练了简体中文维度分别为50、100、200、300的embedding，一并放出来[网盘链接](https://pan.baidu.com/s/1JgjRBWwwrcJSy4taPFtLhA) 密码：`751d`
    > 
    > > 原文发布于[个人博客(好望角)](http://imbowei.com/2018/07/22/wikipedia-train-traditional-chinese-embedding%EF%BC%88word2vec%EF%BC%89model/#more)，并在博客持续更新。
    > 
    > * * * * *
    > 
    > ##### get wiki
    > 
    > [最新的wiki datas下载地址](https://dumps.wikimedia.org/zhwiki/latest/zhwiki-latest-pages-articles.xml.bz2)，目前有1.6G大小。
    > 
    > 里面的内容以XML格式保存。节点信息如下：
    > 
    > ```
    > <page>
    >   <title></title>
    >   <id></id>
    >   <timestamp></timestamp>
    >   <username></username>
    >   <comment></comment>
    >   <text xml:space="preserve"></text>
    > </page>
    > 
    > ```
    > 
    > ##### 初步处理
    > 
    > 直接解压真的太蠢了。\
    > 为了节省时间，免去自己写代码处理Wiki的烦恼，Wikipedia Extractor先初步处理。（服务器非root用户，安装命令加上`--user`）
    > 
    > ```
    > git clone https://github.com/attardi/wikiextractor.git wikiextractor
    > cd wikiextractor
    > python setup.py install --user
    > python WikiExtractor.py -b 1024M -o extracted zhwiki-latest-pages-articles.xml.bz2
    > 
    > ```
    > 
    > 执行过程如下，可以看到一共处理了1012693篇文章，输出如下所示：
    > 
    > ```
    > INFO: 6205533	手語新聞
    > INFO: 6205536	班傑明-古根海姆
    > INFO: 6205549	同意
    > INFO: 6205556	2018年荷蘭網路監控法公民投票
    > INFO: 6205594	李儒新
    > INFO: 6205610	深圳信息职业技术学院
    > INFO: 6205626	停下來等著你 (2018年電視劇)
    > INFO: 6205642	簡單矩陣的快速演算法設計
    > INFO: 6205644	斯義桂
    > INFO: 6205646	焦耳效应
    > INFO: 6205648	1925年世界大賽
    > INFO: 6205653	True (方力申專輯)
    > INFO: 6205657	华睿2号
    > INFO: 6205664	河內郡 (大阪府)
    > INFO: 6205691	京都寺町三条商店街的福爾摩斯
    > INFO: 6205675	莫莉-比什死亡事件
    > INFO: 6205703	都筑郡
    > INFO: 6205701	皇座法庭所屬分庭庭長
    > INFO: 6205709	冬瓜餅
    > INFO: 6205710	吸血鬼莫比亞斯
    > INFO: 6205712	淘綾郡
    > INFO: 6205714	明石香織
    > INFO: Finished 71-process extraction of 1012693 articles in 1114.1s (909.0 art/s)
    > 
    > ```
    > 
    > 通过以上抽取后得到两个文件`wiki_00`和`wiki_01`。里面的格式类似下面
    > 
    > ```
    > <doc id="5323477" url="https://zh.wikipedia.org/wiki?curid=5323477" title="結構與能動性">
    > 文章内容
    > </doc>
    > 
    > ```
    > 
    > 在上面的基础上，我们在去掉一些不需要的特殊符号。
    > 
    > ```python
    > import re
    > import sys
    > import codecs
    > def filte(input_file):
    >     p5 = re.compile('<doc (.*)>')
    >     p6 = re.compile('</doc>')
    >     outfile = codecs.open('std_' + input_file, 'w', 'utf-8')
    >     with codecs.open(input_file, 'r', 'utf-8') as myfile:
    >         for line in myfile:
    >             line = p5.sub('', line)
    >             line = p6.sub('', line)
    >             outfile.write(line)
    >     outfile.close()
    > if __name__ == '__main__':
    > filte(input_file)
    >     input_file = sys.argv[1]
    > 
    > ```
    > 
    > ##### 繁体转简体
    > 
    > 首先安装[opencc-python](https://github.com/yichen0831/opencc-python.git)\
    > 网上一大堆教程，全是深坑！其实直接按照代码仓库作者的方法安装就好了。
    > 
    > ```
    > git clone https://github.com/yichen0831/opencc-python.git
    > cd opencc-python
    > python setup.py install --user
    > 
    > ```
    > 
    > 但是，如果追求效率，可以安装[opencc C++ 版本](https://github.com/BYVoid/OpenCC)，python代码的效率堪忧。
    > 
    > 看文档不难发现，繁体字也分为香港区和[台湾省](https://www.baidu.com/s?wd=%E5%8F%B0%E6%B9%BE%E7%9C%81&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)，要用怎么样的转换看具体需求就好
    > 
    > ```python
    > from opencc import OpenCC
    > 
    > opencc = OpenCC('s2hk')
    > for filename in ['wiki_01','wiki_00']:
    > 	with open('std_'+filename,'r',encoding='utf-8') as fin, open('hk_'+filename,'w',encoding='utf-8') as fou:
    > 		for index , line in enumerate(fin.readlines()):
    > 			hk = opencc.convert(line)
    > 			if index % 10000 == 0:
    > 				print(index,hk)
    > 			fou.write(hk)
    > 
    > ```
    > 
    > 得到了两个文件分别大小为 `1024M` 和`154M`
    > 
    > ##### jieba Segment
    > 
    > 先把两个wiki文件合并`cat hk_wiki_00 hk_wiki_01 > hk_wiki`
    > 
    > ```
    > python -m jieba -d " " ./hk_wiki > ./SegHk_wiki
    > 
    > ```
    > 
    > ##### train word2vec
    > 
    > 运行下面写好的脚本，
    > 
    > ```python
    > # -*- coding: utf-8 -*-
    > from gensim.models import word2vec
    > from gensim.models import KeyedVectors
    > import logging
    > import os
    > 
    > if not os.path.exists('./word2vec_tradiCN/'):
    > 	os.makedirs('./word2vec_tradiCN/')
    > 
    > logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)
    > sentences = word2vec.LineSentence('./SegHk_wiki')
    > 
    > for number in [50,100,200,300]:
    > 	model = word2vec.Word2Vec(sentences,size=number,window=5,min_count=5,workers=20)
    > 	# min-count 表示设置最低频率，默认为5，如果一个词语在文档中出现的次数小于该阈值，那么该词就会被舍弃; size代表词词向量的维度
    > 	# 为了后续建模读取vector方便，我们的保存格式应该和glove vector 保持一致
    > 	model.wv.save_word2vec_format('./word2vec_tradiCN/Wiki'+str(number)+'.txt', binary=False)
    > 
    > ```
    > 
    > 然而出现了`Intel MKL FATAL ERROR: Cannot load libmkl_avx2.so or libmkl_def.so.`这个错误\
    > 运行`conda install nomkl`安装nomkl，这是anaconda的问题。
    > 
    > ##### test word2vec
    > 
    > 如果用python2，运行下面的测试脚本可能会出现如下错误`KeyError: "word '\xe7\xb8\xbd\xe7\xb5\xb1' not in vocabulary"`\
    > 这个是python2对于中文的支持不太友好造成的，用python3即可表现正常。
    > 
    > ```python
    > # -*- coding: utf-8 -*-
    > from gensim.models.keyedvectors import KeyedVectors
    > for number in [50,100,200,300]:
    >     wv = KeyedVectors.load_word2vec_format('./word2vec_tradiCN/Wiki'+ str(number)+'.txt', binary=False)
    >     print(number, wv.similarity('總統','民國')) #两个词的相关性
    >     print(number, wv.most_similar(['倫敦','中國'],['北京']),'\n\n') # 北京is to中国 as 伦敦is to？
    > 
    > ```
    > 
    > -   注意，繁体中文，测试的时候也要用繁体的
    > -   这里直接测试了四组不同大小的embedding，可以对比效果。以这个简单的测试来说，200d embedding效果比较好。
    > -   当然，在实际中，效果怎么样，还是要实际测试。
    > 
    > ```
    > 50 0.08906988
    > 50 [('美國', 0.8497380614280701), ('英國', 0.8156374096870422), ('荷蘭', 0.7635571956634521), ('加拿大', 0.7618951201438904), ('蘇格蘭', 0.7564111948013306), ('法國', 0.7498287558555603), ('冰島', 0.7447660565376282), ('愛爾蘭', 0.7290477752685547), ('德國', 0.7261558175086975), ('哥倫比亞', 0.715803861618042)]
    > 
    > 100 0.0021609096
    > 100 [('英國', 0.7518529891967773), ('美國', 0.716768741607666), ('蘇格蘭', 0.706271767616272), ('德國', 0.6398693323135376), ('法國', 0.6289862394332886), ('愛爾蘭', 0.6286278963088989), ('荷蘭', 0.6277433633804321), ('英格蘭', 0.625410795211792), ('加拿大', 0.6076068878173828), ('威爾斯', 0.6075741052627563)]
    > 
    > 200 0.044366393
    > 200 [('英國', 0.6959728598594666), ('蘇格蘭', 0.6404226422309875), ('美國', 0.6401909589767456), ('英格蘭', 0.6158463358879089), ('愛爾蘭', 0.5740842223167419), ('德國', 0.5558757781982422), ('威爾斯', 0.5539498925209045), ('法國', 0.5375431776046753), ('荷蘭', 0.5276069641113281), ('威爾士', 0.5051602721214294)]
    > 
    > 300 0.034565542
    > 300 [('英國', 0.6512337923049927), ('蘇格蘭', 0.5884094834327698), ('英格蘭', 0.5666802525520325), ('美國', 0.5420516729354858), ('愛爾蘭', 0.5202239751815796), ('威爾斯', 0.48060378432273865), ('荷蘭', 0.4763559103012085), ('德國', 0.4744102358818054), ('法國', 0.4675533175468445), ('北愛爾蘭', 0.46320733428001404)]
    > 
    > ```
    > 
    > ##### 网盘链接
    > 
    > 训练好的四个embedding包含892594个词，都放到了[网盘](https://pan.baidu.com/s/1DB_Sft8N9XMyDP9cpVMpBw)中，可以按需下载。 密码：`2um0`
    > 
    > ##### 参考文献
    > 
    > [word2vec实战：获取和预处理中文维基百科(Wikipedia)语料库，并训练成word2vec模型](https://blog.csdn.net/qq_32166627/article/details/68942216)
    > 


### 以 gensim 訓練中文詞向量

- [以 gensim 訓練中文詞向量 | 雷德麥的藏書閣](https://zake7749.github.io/2016/08/28/word2vec-with-gensim/)

    > 最近正在嘗試幾種文本分類的算法，卻一直苦於沒有結構化的中文語料，原本是打算先爬下大把大把的部落格文章，再依 tag 將它們分門別類，可惜試了一陣子後，我見識到了理想和現實間的鴻溝。
    > 
    > [![太麻煩的事我不會做](http://i.imgur.com/VnjnW7S.jpg)](http://i.imgur.com/VnjnW7S.jpg)
    > 
    > [儘管後來還是搞定了](https://github.com/zake7749/PTT-Text-Mining)
    > 
    > 所以就找上了基於非監督學習的 word2vec，為了銜接後續的資料處理，這邊採用的是基於 python 的主題模型函式庫 [gensim](https://radimrehurek.com/gensim/)。這篇教學並不會談太多 word2vec 的數學原理，而是考慮如何輕鬆又直覺地訓練中文詞向量，文章裡所有的程式碼都會傳上 [github](https://github.com/zake7749/word2vec_tutorial)，現在，就讓我們進入正題吧。
    > 
    > 取得語料
    > ----
    > 
    > 要訓練詞向量，第一步當然是取得資料集。由於 word2vec 是基於非監督式學習，訓練集一定一定要越大越好，語料涵蓋的越全面，訓練出來的結果也會越漂亮。我所採用的是維基百科於[2016/08/20的備份](https://dumps.wikimedia.org/zhwiki/20160820/zhwiki-20160820-pages-articles.xml.bz2)，文章篇數共有 2822639 篇。因為維基百科會定期更新備份資料，如果 8 月 20 號的備份不幸地被刪除了，也可以前往[維基百科:資料庫下載](https://zh.wikipedia.org/wiki/Wikipedia:%E6%95%B0%E6%8D%AE%E5%BA%93%E4%B8%8B%E8%BD%BD)挑選更近期的資料，不過請特別注意一點，我們要挑選的是以 `pages-articles.xml.bz2` 結尾的備份，而不是以 `pages-articles-multistream.xml.bz2` 結尾的備份唷，否則會在清理上出現一些異常，無法正常解析文章。
    > 
    > 在等待下載的這段時間，我們可以先把這次的主角`gensim`配置好:
    > 
    > ```
    > pip3 install --upgrade gensim
    > ```
    > 
    > 維基百科下載好後，先別急著解壓縮，因為這是一份 xml 文件，裏頭佈滿了各式各樣的標籤，我們得先想辦法送走這群不速之客，不過也別太擔心，gensim 早已看穿了一切，藉由調用 [wikiCorpus](https://radimrehurek.com/gensim/corpora/wikicorpus.html)，我們能很輕鬆的只取出文章的標題和內容。
    > 
    > 初始化`WikiCorpus`後，能藉由`get_texts()`可迭代每一篇文章，它所回傳的是一個tokens list，我以空白符將這些 tokens 串接起來，統一輸出到同一份文字檔裡。這邊要注意一件事，`get_texts()`受`wikicorpus.py`中的變數`ARTICLE_MIN_WORDS`限制，只會回傳內容長度大於 *50* 的文章。
    > 
    > ```python
    > # -*- coding: utf-8 -*-
    > 
    > import logging
    > import sys
    > 
    > from gensim.corpora import WikiCorpus
    > 
    > def main():
    > 
    >     if len(sys.argv) != 2:
    >         print("Usage: python3 " + sys.argv[0] + " wiki_data_path")
    >         exit()
    > 
    >     logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)
    >     wiki_corpus = WikiCorpus(sys.argv[1], dictionary={})
    >     texts_num = 0
    > 
    >     with open("wiki_texts.txt",'w',encoding='utf-8') as output:
    >         for text in wiki_corpus.get_texts():
    >             output.write(' '.join(text) + '\n')
    >             texts_num += 1
    >             if texts_num % 10000 == 0:
    >                 logging.info("已處理 %d 篇文章" % texts_num)
    > 
    > if __name__ == "__main__":
    >     main()
    > ```
    > 
    > 在shell 裡輸入：
    > 
    > ```
    > python3 wiki_to_txt.py zhwiki-20160820-pages-articles.xml.bz2
    > ```
    > 
    > 如果你的資料不是 8 月 20 號的備份，記得把`zhwiki-20160820-pages-articles.xml.bz2`換成你的備份的檔名唷。這約需花費 20 分鐘來處理，就讓我們先看一下接下來還要做些什麼吧~
    > 
    > 開始斷詞
    > ----
    > 
    > 我們有清完標籤的語料了，第二件事就是要把語料中每個句子，進一步拆解成一個一個詞，這個步驟稱為「斷詞」。中文斷詞的工具比比皆是，這裏我採用的是 [jieba](https://github.com/fxsjy/jieba)，儘管它在繁體中文的斷詞上還是有些不如`CKIP`，但他實在太簡單、太方便、太好調用了，足以彌補這一點小缺憾：
    > 
    > 
    > ```
    > 快速安裝結巴
    > pip3 install jieba
    > ```
    > 
    > ```python
    > # 斷詞示例
    > 
    > import jieba
    > 
    > seg_list = jieba.cut("我来到北京清华大学", cut_all=False)\
    > print("Default Mode: " + "/ ".join(seg_list))  # 精确模式
    > 
    > #輸出 Default Mode: 我/ 来到/ 北京/ 清华大学
    > 
    > 
    > ```
    > 
    > 現在，我們上一階段的檔案也差不多出爐了，以vi打開看起來會是這個樣子：
    > 
    > 
    > ```
    > 歐幾里得 西元前三世紀的希臘數學家 現在被認為是幾何之父 此畫為拉斐爾的作品 雅典學院 数学 是利用符号语言研究數量 结构 变化以及空间等概念的一門学科 从某种角度看屬於形式科學的一種 數學透過抽象化和邏輯推理的使用 由計數 計算 數學家們拓展這些概念......
    > ```
    > 
    > 
    > Opps！出了一點狀況，我們發現簡體跟繁體混在一起了，比如「数学」與「數學」會被 word2vec 當成兩個不同的詞，所以我們在斷詞前，還需加上一道繁簡轉換的手續。然而我們的語料集相當龐大，一般的繁簡轉換會有些力不從心，建議採用[OpenCC](https://github.com/BYVoid/OpenCC)，轉換的方式很簡單：
    > 
    > ```
    > opencc -i wiki_texts.txt -o wiki_zh_tw.txt -c s2tw.json
    > ```
    > 
    > 如果是要將繁體轉為簡體，只要將config的參數從`s2tw.json`改成`t2s.json`即可。現在再檢查一次`wiki_zh_tw.txt`，的確只剩下繁體字了，終於能進入斷詞，輸入`python3 segment.py`。
    > 
    > ```python
    > # -*- coding: utf-8 -*-
    > 
    > import jieba
    > import logging
    > 
    > def main():
    > 
    >     logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)
    > 
    >     # jieba custom setting.
    >     jieba.set_dictionary('jieba_dict/dict.txt.big')
    > 
    >     # load stopwords set
    >     stopword_set = set()
    >     with open('jieba_dict/stopwords.txt','r', encoding='utf-8') as stopwords:
    >         for stopword in stopwords:
    >             stopword_set.add(stopword.strip('\n'))
    > 
    >     output = open('wiki_seg.txt', 'w', encoding='utf-8')
    >     with open('wiki_zh_tw.txt', 'r', encoding='utf-8') as content :
    >         for texts_num, line in enumerate(content):
    >             line = line.strip('\n')
    >             words = jieba.cut(line, cut_all=False)
    >             for word in words:
    >                 if word not in stopword_set:
    >                     output.write(word + ' ')
    >             output.write('\n')
    > 
    >             if (texts_num + 1) % 10000 == 0:
    >                 logging.info("已完成前 %d 行的斷詞" % (texts_num + 1))
    >     output.close()
    > 
    > if __name__ == '__main__':
    >     main()
    > ```
    > 
    > 
    > ### Stopwords and Window
    > 
    > 好啦，這個東西大概要跑個 80 分鐘，~~先讓我講些幹話~~，先讓我們看看上頭做了什麼。除了之前演示的斷詞外，這邊還多做了兩件事，一是調整jieba的辭典，讓他對繁體斷詞比較友善，二是引入了[停用詞](https://zh.wikipedia.org/wiki/%E5%81%9C%E7%94%A8%E8%AF%8D)，停用詞就是像英文中的 the,a,this，中文的你我他，與其他詞相比顯得不怎麼重要，對文章主題也無關緊要的，就可以將它視為停用詞。而要排除停用詞的理由，其實與word2vec的實作概念大大相關，由於在開頭講明了不深究概念，就讓我舉個例子替代長篇大論。
    > 
    > 首先，在word2vec有一個概念叫 windows，我習慣叫他窗口，因為它給我的感覺跟TCP 那個會滑來滑去的東東很像。
    > 
    > Word2Vec
    > --------
    > 
    > 很顯然，一個詞的意涵跟他的左右鄰居很有關係，比如「雨越下越大，茶越充越淡」，什麼會「下」？「雨」會下，什麼會「淡」？茶會「淡」，這樣的類比舉不勝舉，那麼，若把思維逆轉過來呢？
    > 
    > [![逆轉](http://i.imgur.com/KR2ISOg.jpg)](http://i.imgur.com/KR2ISOg.jpg)
    > 
    > 顯然，我們或多或少能從左右鄰居是誰，猜出中間的是什麼，這很像我們國高中時天天在練的英文克漏字。那麼問題來了，左右鄰居有誰？能更精確地說，你要往左往右看幾個？假設我們以「孔乙己 一到 店 所有 喝酒 的 人 便都 看著 他 笑」為例，如果往左往右各看一個：
    > 
    > 
    > ```
    > [孔乙己 一到] 店 所有 喝酒 的 人 便 都 看著 他 笑\
    > [孔乙己 一到 店] 所有 喝酒 的 人 便 都 看著 他 笑\
    > 孔乙己 [一到 店 所有] 喝酒 的 人 便 都 看著 他 笑\
    > 孔乙己 一到 [店 所有 喝酒] 的 人 便 都 看著 他 笑\
    > ......
    > ```
    > 
    > 這樣就構成了一個 size=1 的 windows，這個 1 是極端的例子，為了讓我們看看有停用詞跟沒停用詞差在哪，這句話去除了停用詞應該會變成：
    > 
    > ```
    > 孔乙己 一到 店 所有 喝酒 人 看著 笑
    > ```
    > 
    > 我們看看「人」的窗口變化，原本是「的 人 便」，後來是「喝酒 人 看著」，相比原本的情形，去除停用詞後，我們對「人」這個詞有更多認識，比如人會喝酒，人會看東西，當然啦，這是我以口語的表達，機器並不會這麼想，機器知道的是人跟喝酒會有某種關聯，跟看會有某種關聯，但儘管如此，也遠比本來的「的 人 便」好太多太多了。
    > 
    > 就在剛剛，我的斷詞已經跑完了，現在，讓我們進入收尾的階段吧
    > 
    > ```
    > 2016-08-26 22:27:59,480 : INFO : 已處理 260000 個 token
    > ```
    > 
    > 訓練詞向量
    > -----
    > 
    > 這是最簡單的部分，同時也是最困難的部分，簡單的是程式碼，困難的是詞向量效能上的微調與後訓練。對了，如果你已經對詞向量和語言模型有些研究，在輸入`python3 train.py`之前，建議先看一下之後的內文，相信我，你會需要的。
    > 
    > ```python
    > # -*- coding: utf-8 -*-
    > 
    > import logging
    > 
    > from gensim.models import word2vec
    > 
    > def main():
    > 
    >     logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)
    >     sentences = word2vec.LineSentence("wiki_seg.txt")
    >     model = word2vec.Word2Vec(sentences, size=250)
    > 
    >     #保存模型，供日後使用
    >     model.save("word2vec.model")
    > 
    >     #模型讀取方式
    >     # model = word2vec.Word2Vec.load("your_model_name")
    > 
    > if __name__ == "__main__":
    >     main()
    > ```
    > 
    > 扣掉`logging`與註釋就剩下三行，真是精簡的漂亮。上頭通篇的學問在`model = word2vec.Word2Vec(sentences, size=250)`，我們先讓它現出原型：
    > 
    > 
    > ```python
    > class gensim.models.word2vec.Word2Vec(sentences=None, size=100, alpha=0.025, window=5, min_count=5, max_vocab_size=None, sample=0.001, seed=1, workers=3, min_alpha=0.0001, sg=0, hs=0, negative=5, cbow_mean=1, hashfxn=< built-in function hash>, iter=5, null_word=0, trim_rule=None, sorted_vocab=1, batch_words=10000)
    > ```
    > 
    > 這抵得上 train.py 的所有程式碼了。不過也別太擔心，裏頭多是無關緊要的參數，從初學的角度來看，我們會去動到的大概是：
    > 
    > -   sentences:當然了，這是要訓練的句子集，沒有他就不用跑了
    > -   size:這表示的是訓練出的詞向量會有幾維
    > -   alpha:機器學習中的學習率，這東西會逐漸收斂到 `min_alpha`
    > -   sg:這個不是三言兩語能說完的，sg=1表示採用skip-gram,sg=0 表示採用cbow
    > -   window:還記得孔乙己的例子嗎？能往左往右看幾個字的意思
    > -   workers:執行緒數目，除非電腦不錯，不然建議別超過 4
    > -   min_count:若這個詞出現的次數小於`min_count`，那他就不會被視為訓練對象
    > 
    > 等摸清 Word2Vec 背後的原理後，也可以試著調調`hs`、`negative`，看看對效能會有什麼影響。
    > 
    > 詞向量實驗
    > -----
    > 
    > 訓練完成後，讓我們來測試一下模型的效能，運行`python3 demo.py`。由於 gensim 將整個模型讀了進來，所以記憶體會消耗相當多，如果出現了`MemoryError`，可能得調整一下`min_count`或對常用詞作一層快取，這點要注意一下。
    > 
    > 先來試試相似詞排序吧！
    > 
    > ```
    > 飲料
    > 
    > 相似詞前 100 排序
    > 飲品,0.8439314365386963
    > 果汁,0.7858869433403015
    > 罐裝,0.7305712699890137
    > 冰淇淋,0.702262818813324
    > 酸奶,0.7007108926773071
    > 口香糖,0.6987590193748474
    > 酒類,0.6967358589172363
    > 可口可樂,0.6885123252868652
    > 酒精類,0.6843742728233337
    > 含酒精,0.6825539469718933
    > 啤酒,0.6816493272781372
    > 薯片,0.6779764294624329
    > 紅茶,0.6656282544136047
    > 奶茶,0.656740128993988
    > 提神,0.6566425561904907
    > 牛奶,0.6556192636489868
    > 檸檬茶,0.6494661569595337
    > 
    > 籃球
    > 
    > 相似詞前 100 排序
    > 美式足球,0.6463411450386047
    > 橄欖球,0.6382837891578674
    > 男子籃球,0.6187020540237427
    > 冰球,0.6056296825408936
    > 棒球,0.5859025716781616
    > 籃球運動,0.5831792950630188
    > 籃球員,0.5782726407051086
    > 籃球隊,0.576259195804596
    > 排球,0.5743488073348999
    > 黑子,0.5609416961669922
    > 籃球比賽,0.5498511791229248
    > 打球,0.5496408939361572
    > 中國籃球,0.5471529960632324
    > 男籃,0.5460700392723083
    > ncaa,0.543986439704895
    > 投投,0.5439497232437134
    > 曲棍球,0.5435376167297363
    > nba,0.5415610671043396
    > ```
    > 
    > 前100太多了，所以只把前幾個結果貼上來，我們也能調用`model.similarity(word2,word1)`來直接取得兩個詞的相似度：
    > 
    > ```
    > 冰沙 刨冰
    > 計算 Cosine 相似度
    > 0.631961417455
    > 
    > 電腦 飛鏢
    > 計算 Cosine 相似度
    > 0.154503715708
    > 
    > 電腦 程式
    > 計算 Cosine 相似度
    > 0.5021829415
    > 
    > 衛生紙 漫畫
    > 計算 Cosine 相似度
    > 0.167776641495
    > ```
    > 
    > 能稍微區隔出詞與詞之間的主題，整體來說算是可以接受的了。
    > 
    > ### 更上一層樓
    > 
    > 如何優化詞向量的表現？這其實有蠻多方法的，大方向是從應用的角度出發，我們能針對應用特化的語料進行再訓練，除此之外，斷詞器的選擇也很重要，它很大程度的決定什麼詞該在什麼地方出現，如果發現 `jieba` 有些力不能及的，不妨試著採用別的斷詞器，或是試著在 `jieba` 自訂辭典，調一下每個詞的權重。
    > 
    > 應用考慮好了，接著看看模型，我們可以調整 `model()` 的參數，比方窗口大小、維度、學習率，進一步還能比較 skip-gram 與 cbow 的效能差異，什麼，你說不知道 skip-gram 跟 cbow 是什麼？且看下回分解。
    > 
    > 參考資料
    > ----
    > 
    > [Training Word2Vec Model on English Wikipedia by Gensim](http://textminingonline.com/training-word2vec-model-on-english-wikipedia-by-gensim)
    > 

## word2Vec

### 原理

- [類神經網路 -- word2vec (part 1 : Overview) « MARK CHANG'S BLOG](http://cpmarkchang.logdown.com/posts/773062-neural-network-word2vec-part-1-overview)

- [理解 Word2Vec 之 Skip-Gram 模型](https://zhuanlan.zhihu.com/p/27234078)

- [Word2vec (中文)](https://www.slideshare.net/ywchen88/word2vec-70245972)

- [how_does_word2vec_work.pdf](http://www.1-4-5.net/~dmm/ml/how_does_word2vec_work.pdf)


### What is the function that is being optimized in word2vec?

- [What is the function that is being optimized in word2vec? - Cross Validated](https://stats.stackexchange.com/questions/250218/what-is-the-function-that-is-being-optimized-in-word2vec)

    > > How are the words inputted into a Word2Vec model? In other words, what part of the neural network is used to derive the vector representations of the words?
    > 
    > See [Input vector representation vs output vector representation in word2vec](https://stats.stackexchange.com/q/177667/12359)
    > 
    > > What is the objective function which is being minimized?
    > 
    > The original word2vec papers are notoriously unclear on some points pertaining to the training of the neural network ([Why do so many publishing venues limit the length of paper submissions?](https://academia.stackexchange.com/q/57071/452)). I advise you look at {1-3}, which answer this question.
    > 
    > * * * * *
    > 
    > References:
    > 
    > -   {1} Rong, Xin. "word2vec parameter learning explained." arXiv preprint arXiv:1411.2738 (2014). <https://arxiv.org/abs/1411.2738>
    > -   {2} Goldberg, Yoav, and Omer Levy. "word2vec Explained: deriving Mikolov et al.'s negative-sampling word-embedding method." arXiv preprint arXiv:1402.3722 (2014). <https://arxiv.org/abs/1402.3722>
    > -   {3} [TensorFlow's tutorial on Vector Representations of Words](https://www.tensorflow.org/versions/r0.12/tutorials/word2vec/index.html)

### 實作

- [zake7749/word2vec-tutorial: 中文詞向量訓練教學](https://github.com/zake7749/word2vec-tutorial)

- [使用tensorflow实现word2vec中文词向量的训练](https://zhuanlan.zhihu.com/p/28979653)

- [類神經網路 -- word2vec (part 1 : Overview) « MARK CHANG'S BLOG](http://cpmarkchang.logdown.com/posts/773062-neural-network-word2vec-part-1-overview)

- [Alex-CHUN-YU/Word2vec: 訓練中文詞向量 Word2vec, Word2vec was created by a team of researchers led by Tomas Mikolov at Google.](https://github.com/Alex-CHUN-YU/Word2vec)

- [用中文資料測試 word2vec - 翼之都, City of Wings](http://city.shaform.com/blog/2014/11/04/word2vec.html)

- [自然語言處理入門- Word2vec小實作 – PyLadies Taiwan – Medium](https://medium.com/pyladies-taiwan/%E8%87%AA%E7%84%B6%E8%AA%9E%E8%A8%80%E8%99%95%E7%90%86%E5%85%A5%E9%96%80-word2vec%E5%B0%8F%E5%AF%A6%E4%BD%9C-f8832d9677c8)

- [詞向量介紹](https://fgc.stpi.narl.org.tw/activity/videoDetail/4b1141305ddf5522015de5479f4701b1)

### Can word2vec be considered deep learning?

- [Can word2vec be considered deep learning? - Quora](https://www.quora.com/Can-word2vec-be-considered-deep-learning)

    > I've met [Tomas Mikolov](https://research.facebook.com/tomas-mikolov) several months ago in Moscow at some local machine learning-related event and asked him many questions about deep architectures and their application in NLP in particular. The greatest insight about the word2vec-related experiment came from the result that the simplest model gave the most robust and unexpectedly sensible results. They've tried many different architectures, from simple feed-forward with few layers to deep computationally-heavy models, and the one that was both useful and feasible was the simplest.
    > 
    > Needless to say that we were shaking our heads trying to comprehend that. His lecture "A roadmap towards machine intelligence" took that even further, bringing up the questions whether even-deeper architectures are really the right direction to move in.
    > 



### Skip-gram / CBOW

- [Is skip gram (negative sampling) better than CBOW (NS) for word2vec? If so, why? - Quora](https://www.quora.com/Is-skip-gram-negative-sampling-better-than-CBOW-NS-for-word2vec-If-so-why)

    > Please see [Stephan Gouws](https://www.quora.com/profile/Stephan-Gouws) excellent answer here: [How does word2vec work? Can someone walk through a specific example?](https://www.quora.com/How-does-word2vec-work-Can-someone-walk-through-a-specific-example)
    > 
    > >For the skipgram, the direction of the prediction is simply inverted, i.e. now we try to predict P(citizens | X), P(of | X), etc. This turns out to learn finer-grained vectors when one trains over more data. The main reason is that the CBOW smooths over a lot of the distributional statistics by averaging over all context words while the skipgram does not. With little data, this "regularizing" effect of the CBOW turns out to be helpful, but since data is the ultimate regularizer the skipgram is able to extract more information when more data is available.
    > 


## fastText

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


### fastText原理

- [fastText原理及实践](https://mp.weixin.qq.com/s?__biz=MjM5ODkzMzMwMQ==&mid=2650408615&idx=1&sn=3c1d9b44cf757f1d7202ae8498d7534c&chksm=becd80fd89ba09ebf71b61724ee38f89d9a959142e55b833479a74a963345d90ed86ab704932&mpshare=1&scene=24&srcid=#rd)

    > 本文首先会介绍一些预备知识，比如softmax、ngram等，然后简单介绍word2vec原理，之后来讲解fastText的原理，并着手使用keras搭建一个简单的fastText分类器，最后，我们会介绍fastText在达观数据的应用。
    > 
    > NO.1
    > 
    > 预备知识
    > 
    > **1 Softmax回归**
    > 
    > Softmax回归（Softmax Regression）又被称作多项逻辑回归（multinomial logistic regression），它是逻辑回归在处理多类别任务上的推广。
    > 
    > 在逻辑回归中， 我们有m个被标注的样本：![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XekPQozbxUT3ibjDJNLfhbb1P6vATlcgfQkW6RTkv00PEOxYYFppkWgA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")，其中![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0X0ED3tUZf31ZFQpQZn6Wo08N2JvhMOHj6xmqL0LKnjHdiaicUicTic1UdTA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")。因为类标是二元的，所以我们有![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XhyhpDZ95zoCwyeNP8ozsq4NtUiaF16Py0s8ksBhDqKleVs1m9JfGnYw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")。我们的假设（hypothesis）有如下形式：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XWZveabzHfM33JNicByuzSQXKEZiaqPXEeyW7Ky1aPNu0r6SrO4bSeFAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 代价函数（cost function）如下：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XoWSxvfq5a1PYLl5tZUNbmxiaDe1j5Qycz4h2m0JOf9hUNibmHH30hP8w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 在Softmax回归中，类标是大于2的，因此在我们的训练集![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XrLjY64QfJ970hDr7asy2kickWDV4Y1ApaglxY2UfsavCJ4sWcku64cw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 中，![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XIG0q3rwFGTarRUWXOlhhawiaKEtSsy4qSx96icwMT8ddHdRbphC4UDPg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")。给定一个测试输入x，我们的假设应该输出一个K维的向量，向量内每个元素的值表示x属于当前类别的概率。具体地，假设![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0X1Zf9r69LZxMqtJTDMSKbQuGLLRcAictutH7AfeiaDjhYzXxOy8ibciaZwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")形式如下：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XXrBZGicUNodibN5qSbBfFPSVj4ib5bD1ibSpdpQBzWT1icaL9x2icJM3siaHw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 代价函数如下：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XD4dOFsQ5dS96UU21eSYwGjnRQjRuKGia9XAm4yMGSDKSA9Zmho3pW4Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 其中1{-}是指示函数，即1=1,1=0
    > 
    > 既然我们说Softmax回归是逻辑回归的推广，那我们是否能够在代价函数上推导出它们的一致性呢？当然可以，于是：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XZG1ibAld1Uw18onXlLlGMpLVeppqxWBM42phYJRcsyJ9jaqzhhHe2hw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 可以看到，逻辑回归是softmax回归在K=2时的特例。
    > 
    > **2 分层Softmax**
    > 
    > 你可能也发现了，标准的Softmax回归中，要计算y=j时的Softmax概率：![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XdBMtUiaKVNHtz9WSFdyBrWNuKWYzCw74rdITVlMuR6khiatF6xNzHRsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")，我们需要对所有的K个概率做归一化，这在|y|很大时非常耗时。于是，分层Softmax诞生了，它的基本思想是使用树的层级结构替代扁平化的标准Softmax，使得在计算![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XdBMtUiaKVNHtz9WSFdyBrWNuKWYzCw74rdITVlMuR6khiatF6xNzHRsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")时，只需计算一条路径上的所有节点的概率值，无需在意其它的节点。
    > 
    > 下图是一个分层Softmax示例：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XYfVg8Ol6GyRHV3S5Mgsibtd9Iyzk3tQjIUkWSIFOmhPg1HYiaLPuyS7A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
    > 
    > 树的结构是根据类标的频数构造的霍夫曼树。K个不同的类标组成所有的叶子节点，K-1个内部节点作为内部参数，从根节点到某个叶子节点经过的节点和边形成一条路径，路径长度被表示为![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XZlibibWOScBXYB8tdBw7L7vW76XiasXmTiaGyskdCfCqp2MfME8ichibxD9g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")。于是，![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XrqPWJNr4V5OnI8AXrJ82gWXMlByaM8Kben9VZxrexKCgARkUmibddzA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")就可以被写成：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XicLVg5IK8t2dRKhm957ibzF3VbH3sH1n78S8BpL8GSg04FmKXicGJC6Gg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 其中：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XwMm6Qxw9m7XzROw1wmWzRic23uQdZDr9ib1BvJ8kNI0SRrlXdqPyrCiaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")表示sigmoid函数；
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0Xp9nWemnL2hOa9wOiaFn5yZCNa5exhovN2FX9Et9ACnqMhwX8euHYGmQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")表示n节点的左孩子；
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0Xczlmk9jekm1wWOhOScVVFav0ibqyb0icahexsvvib5dRZH9hJhD6EUVgQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")是一个特殊的函数，被定义为：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XD2pgDXEibAtQ9MialH6Q5OTpbN8zjHt7SqIcbwm5q6taxRiaD3xZyFZBQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XIc5lU6xs01VRa0YbJpDOndBdhLGQIhTKE2JBuAhnq0xwXBof8h0D3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")是中间节点![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XQwQ5r7GjZE2dw7JWiaJc8UxXpB5aqaGKt9IUf6aggOyw0vb3ChSqO6Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")的参数；X是Softmax层的输入。
    > 
    > 上图中，高亮的节点和边是从根节点到 ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0X0QgsicCFia24JibhXG8T4604UaA2D0GicI0pzCWQIwcBSfibNd51RiaGVb9g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践") 的路径，路径长度![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XaOMa8QTgFSaIOhmPJmvwm1eUnaHjaqJn97Xr2NRyABurCqjiaCnvF1Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 可以被表示为：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0Xxibn8eBLk0VQ0kPs5Y0HnWCfUOhNML4YYmNWT2yYEbqsibWcnGqnPQlA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 于是，从根节点走到叶子节点![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0X0QgsicCFia24JibhXG8T4604UaA2D0GicI0pzCWQIwcBSfibNd51RiaGVb9g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")，实际上是在做了3次二分类的逻辑回归。
    > 
    > 通过分层的Softmax，计算复杂度一下从|K|降低到log|K|。
    > 
    > **3 n-gram特征**
    > 
    > 在文本特征提取中，常常能看到n-gram的身影。它是一种基于语言模型的算法，基本思想是将文本内容按照字节顺序进行大小为N的滑动窗口操作，最终形成长度为N的字节片段序列。看下面的例子：
    > 
    > **我来到达观数据参观**
    > 
    > **相应的bigram特征为：** 我来 来到 到达 达观 观数 数据 据参 参观
    > 
    > **相应的trigram特征为：** 我来到 来到达 到达观 达观数 观数据 数据参 据参观
    > 
    > **注意一点：** n-gram中的gram根据粒度不同，有不同的含义。它可以是字粒度，也可以是词粒度的。上面所举的例子属于字粒度的n-gram，词粒度的n-gram看下面例子：
    > 
    > **我 来到 达观数据 参观**
    > 
    > **相应的bigram特征为：** 我/来到 来到/达观数据 达观数据/参观
    > 
    > **相应的trigram特征为：** 我/来到/达观数据 来到/达观数据/参观 
    > 
    > n-gram产生的特征只是作为文本特征的候选集，你后面可能会采用信息熵、卡方统计、IDF等文本特征选择方式筛选出比较重要特征。
    > 
    > NO.2
    > 
    > Word2vec
    > 
    > 你可能要问，这篇文章不是介绍fastText的么，怎么开始介绍起了word2vec？
    > 
    > **最主要的原因是word2vec的CBOW模型架构和fastText模型非常相似。** 于是，你看到facebook开源的fastText工具不仅实现了fastText文本分类工具，还实现了快速词向量训练工具。word2vec主要有两种模型：skip-gram 模型和CBOW模型，这里只介绍CBOW模型，有关skip-gram模型的内容请参考达观另一篇技术文章：
    > 
    > [漫谈Word2vec之skip-gram模型](https://mp.weixin.qq.com/s?__biz=MzA5NzY0MDg1NA==&mid=2706953858&idx=1&sn=cb83cb61330cdb77275e846bec6e7433&scene=21#wechat_redirect)
    > 
    > **1 模型架构**
    > 
    > CBOW模型的基本思路是：用上下文预测目标词汇。架构图如下所示：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XmZPLkLByEj95ibUVbEJ65zXa7p9cU2E83odx0Y0yXBaXfVtYZWPHqBg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 输入层由目标词汇y的上下文单词 ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XDHsmISgUMic5o3prkZL3mcV5wDv18JAzyvF4slyNZGcZUxk2glSNodw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践") 组成， ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0X4qEBp9eQzwp27vg7VHmzic78k2A18aRmvLDyrmLBIvW9oZQU7qLMtbQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践") 是被onehot编码过的V维向量，其中V是词汇量；隐含层是N维向量h；输出层是被onehot编码过的目标词y。输入向量通过 ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XiaaohCL00WyPicb9MZXmDDVmBW1KFSYdHwcbiatNcPcuyteRjhDQZDEVw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")维的权重矩阵W连接到隐含层；隐含层通过 ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XVnrticNoibia8ibkvEkXotgUick4DkBYztX3IuBHib2zRvAaXca2PspdicY9Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践") 维的权重矩阵 ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XG88VYPBuzLyicMR3AjL7Vkq0VDr7hBz65lhya3TNPJQKHl1an1MccYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践") 连接到输出层。因为词库V往往非常大，使用标准的softmax计算相当耗时，于是CBOW的输出层采用的正是上文提到过的分层Softmax。
    > 
    > **2 前向传播**
    > 
    > 输入是如何计算而获得输出呢？先假设我们已经获得了权重矩阵![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XruMDaVbL23MibFnP6C5ia6MMQHRE1y36sULEONSLquesQosJGu5wUuNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")和![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XG88VYPBuzLyicMR3AjL7Vkq0VDr7hBz65lhya3TNPJQKHl1an1MccYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")（具体的推导见第3节），隐含层h的输出的计算公式：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XL84IouorgunlMdjMO1z4A5K8Dcq3pvrw0pZeNQ6RocBzvgawuzpOUg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 即：隐含层的输出是C个上下文单词向量的加权平均，权重为*W*。
    > 
    > 接着我们计算输出层的每个节点：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XWdHCQSsu5FS0KBCic9UDWrOuWP8ia2cTe2Sc4icaCTBiadSxV7fbWu8P3A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 这里![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0X6oqjNwm83esqdvtQc1ZuTQlMn35bQmEHUDL27pWTU75NnCCIH9kaibA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")是矩阵![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XG88VYPBuzLyicMR3AjL7Vkq0VDr7hBz65lhya3TNPJQKHl1an1MccYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")的第j列，最后，将![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XkPj3xicU4PlibPPicExW5BG5T1yJf0qNjmjcUu7O1ML0mM27hEJuXM6DA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")作为softmax函数的输入，得到![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XJDfHXFD5chj5cYNDatyt0q5XN2fFFiaTB4Hdenlj2Dia0jCX9CLg52aA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0X6jmOkrDLkkZtsvPHkndZF5S3xp6a8tOQXUufk4HmPIQJccVmQibHuRQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > **3 反向传播学习权重矩阵**
    > 
    > 在学习权重矩阵和过程中，我们首先随机产生初始值，然后feed训练样本到我们的模型，并观测我们期望输出和真实输出的误差。接着，我们计算误差关于权重矩阵的梯度，并在梯度的方向纠正它们。
    > 
    > 首先定义损失函数，objective是最大化给定输入上下文，target单词的条件概率。因此，损失函数为：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XiaqvQp7FhVDBW2bbHKanwiabpb8J8pTGVY419FPfsXUP9MZVFcjfPNDA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 这里，![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XnNSRDUryfIgfZC7kYbIKB8EW5leB0G0TbbRQhWH6YJ3Zve9EjLJG5A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")表示目标单词在词库V中的索引。
    > 
    > 如何更新权重![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XG88VYPBuzLyicMR3AjL7Vkq0VDr7hBz65lhya3TNPJQKHl1an1MccYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")?
    > 
    > 我们先对E关于![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XRVAzcvWeUGXgIWhbccYHufn44wwtgy7qnnM7ZLMtO1X5wxfrFhZrzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")求导：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XpoxMLmJNmD0mPZXfibSZwDlU3lqNJgiaw2su66vXbGZv4yOGfmFAvgCQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XqakHQn5mcP8CfaQBLJXFjmHr5y30IOvt9mfNhWGNTQWnkD6ml0FoCw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")函数表示：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XOhYEjyFN86dljvYHVfszYCric17LiaTVg2ty91FEhooeSGPe9ibic3eXhA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 于是，![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XRVAzcvWeUGXgIWhbccYHufn44wwtgy7qnnM7ZLMtO1X5wxfrFhZrzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")的更新公式：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XpE9UzHg2NL6Fzl8gASReSFT4ich3F1ZsArA8Sk0pXLPmpCx2Dyl4EMQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > **如何更新权重*W*？**
    > 
    > 我们首先计算E关于隐含层节点的导数：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XZyWHIds4FKCL4g1smovIicK387icNxMgGr6CESVhvMlFeEwNhSXq32Sg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 然后，E关于权重的导数为：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0X28iaqFTmiblOKNlWctmU8fYc0iagPsUb6as3Tic2uXhZpEOh8g72DiaHSPg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > 于是，![](https://mmbiz.qpic.cn/mmbiz_png/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0X2fv524mMNIBUlkBMDwRDczpzUSqyxUnib9NzHWr6uNYcccHcIkIdEvw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")的更新公式：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XHD7T23ZibdeHnSWWP6qEzCDqgvgV0f0l285WLWXWiasqbzqxGBrcticdg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > NO.3
    > 
    > fastText分类
    > 
    > 终于到我们的fastText出场了。这里有一点需要特别注意，一般情况下，使用fastText进行文本分类的同时也会产生词的embedding，即embedding是fastText分类的产物。除非你决定使用预训练的embedding来训练fastText分类模型，这另当别论。
    > 
    > **1 字符级别的n-gram**
    > 
    > word2vec把语料库中的每个单词当成原子的，它会为每个单词生成一个向量。这忽略了单词内部的形态特征，比如："apple" 和"apples"，"达观数据"和"达观"，这两个例子中，两个单词都有较多公共字符，即它们的内部形态类似，但是在传统的word2vec中，这种单词内部形态信息因为它们被转换成不同的id丢失了。
    > 
    > **为了克服这个问题，fastText使用了字符级别的n-grams来表示一个单词。**对于单词"apple"，假设n的取值为3，则它的trigram有:
    > 
    > **"<ap",  "app",  "ppl",  "ple", "le>"**
    > 
    > 其中，<表示前缀，>表示后缀。于是，我们可以用这些trigram来表示"apple"这个单词，进一步，我们可以用这5个trigram的向量叠加来表示"apple"的词向量。
    > 
    > **这带来两点好处：**
    > 
    > 1\. 对于低频词生成的词向量效果会更好。因为它们的n-gram可以和其它词共享。
    > 
    > 2\. 对于训练词库之外的单词，仍然可以构建它们的词向量。我们可以叠加它们的字符级n-gram向量。
    > 
    > **2 模型架构**
    > 
    > 之前提到过，fastText模型架构和word2vec的CBOW模型架构非常相似。下面是fastText模型架构图：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XfJAgBu2jFO56Uiabh5r2iaMZmqmzSeepE23kqZ8ZycicOJuWuibK9ddvkA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > **注意：** 此架构图没有展示词向量的训练过程。可以看到，和CBOW一样，fastText模型也只有三层：输入层、隐含层、输出层（Hierarchical Softmax），输入都是多个经向量表示的单词，输出都是一个特定的target，隐含层都是对多个词向量的叠加平均。
    > 
    > **不同的是，** CBOW的输入是目标单词的上下文，fastText的输入是多个单词及其n-gram特征，这些特征用来表示单个文档；CBOW的输入单词被onehot编码过，fastText的输入特征是被embedding过；CBOW的输出是目标词汇，fastText的输出是文档对应的类标。
    > 
    > **值得注意的是，fastText在输入时，将单词的字符级别的n-gram向量作为额外的特征；在输出时，fastText采用了分层Softmax，大大降低了模型训练时间。** 这两个知识点在前文中已经讲过，这里不再赘述。
    > 
    > fastText相关公式的推导和CBOW非常类似，这里也不展开了。
    > 
    > **3 核心思想**
    > 
    > 现在抛开那些不是很讨人喜欢的公式推导，来想一想fastText文本分类的核心思想是什么？
    > 
    > 仔细观察模型的后半部分，即从隐含层输出到输出层输出，会发现它就是一个softmax线性多类别分类器，分类器的输入是一个用来表征当前文档的向量；模型的前半部分，即从输入层输入到隐含层输出部分，主要在做一件事情：生成用来表征文档的向量。那么它是如何做的呢？叠加构成这篇文档的所有词及n-gram的词向量，然后取平均。叠加词向量背后的思想就是传统的词袋法，即将文档看成一个由词构成的集合。
    > 
    > **于是fastText的核心思想就是：将整篇文档的词及n-gram向量叠加平均得到文档向量，然后使用文档向量做softmax多分类。** 这中间涉及到两个技巧：字符级n-gram特征的引入以及分层Softmax分类。
    > 
    > **4 关于分类效果**
    > 
    > 还有个问题，就是为何fastText的分类效果常常不输于传统的非线性分类器？
    > 
    > **假设我们有两段文本：**
    > 
    > 我 来到 达观数据
    > 
    > 俺 去了 达而观信息科技
    > 
    > 这两段文本意思几乎一模一样，如果要分类，肯定要分到同一个类中去。但在传统的分类器中，用来表征这两段文本的向量可能差距非常大。传统的文本分类中，你需要计算出每个词的权重，比如tfidf值， "我"和"俺" 算出的tfidf值相差可能会比较大，其它词类似，于是，VSM（向量空间模型）中用来表征这两段文本的文本向量差别可能比较大。
    > 
    > **但是fastText就不一样了，它是用单词的embedding叠加获得的文档向量，词向量的重要特点就是向量的距离可以用来衡量单词间的语义相似程度** ，于是，在fastText模型中，这两段文本的向量应该是非常相似的，于是，它们很大概率会被分到同一个类中。
    > 
    > 使用词embedding而非词本身作为特征，这是fastText效果好的一个原因；另一个原因就是字符级n-gram特征的引入对分类效果会有一些提升 。
    > 
    > NO.4
    > 
    > 手写一个fastText
    > 
    > keras是一个抽象层次很高的神经网络API，由python编写，底层可以基于Tensorflow、Theano或者CNTK。它的优点在于：用户友好、模块性好、易扩展等。所以下面我会用keras简单搭一个fastText的demo版，生产可用的fastText请移步https://github.com/facebookresearch/fastText。
    > 
    > 如果你弄懂了上面所讲的它的原理，下面的demo对你来讲应该是非常明了的。
    > 
    > 为了简化我们的任务：
    > 
    > 1\. 训练词向量时，我们使用正常的word2vec方法，而真实的fastText还附加了字符级别的n-gram作为特征输入；
    > 
    > 2\. 我们的输出层使用简单的softmax分类，而真实的fastText使用的是Hierarchical Softmax。
    > 
    > 首先定义几个常量：
    > 
    > VOCAB_SIZE = 2000
    > 
    > EMBEDDING_DIM =100
    > 
    > MAX_WORDS = 500
    > 
    > CLASS_NUM = 5
    > 
    > VOCAB_SIZE表示词汇表大小，这里简单设置为2000；
    > 
    > EMBEDDING_DIM表示经过embedding层输出，每个词被分布式表示的向量的维度，这里设置为100。比如对于"达观"这个词，会被一个长度为100的类似于[ 0.97860014, 5.93589592, 0.22342691, -3.83102846, -0.23053935, ...]的实值向量来表示；
    > 
    > MAX_WORDS表示一篇文档最多使用的词个数，因为文档可能长短不一（即词数不同），为了能feed到一个固定维度的神经网络，我们需要设置一个最大词数，对于词数少于这个阈值的文档，我们需要用"未知词"去填充。比如可以设置词汇表中索引为0的词为"未知词"，用0去填充少于阈值的部分；
    > 
    > CLASS_NUM表示类别数，多分类问题，这里简单设置为5。
    > 
    > 模型搭建遵循以下步骤：
    > 
    > 1\. 添加输入层（embedding层）。Embedding层的输入是一批文档，每个文档由一个词汇索引序列构成。例如：[10, 30, 80, 1000] 可能表示"我 昨天 来到 达观数据"这个短文本，其中"我"、"昨天"、"来到"、"达观数据"在词汇表中的索引分别是10、30、80、1000；Embedding层将每个单词映射成EMBEDDING_DIM维的向量。于是：input_shape=(BATCH_SIZE, MAX_WORDS), output_shape=(BATCH_SIZE,MAX_WORDS, EMBEDDING_DIM)；
    > 
    > 2\. 添加隐含层（投影层）。投影层对一个文档中所有单词的向量进行叠加平均。keras提供的GlobalAveragePooling1D类可以帮我们实现这个功能。这层的input_shape是Embedding层的output_shape，这层的output_shape=( BATCH_SIZE, EMBEDDING_DIM)；
    > 
    > 3\. 添加输出层（softmax层）。真实的fastText这层是Hierarchical Softmax，因为keras原生并没有支持Hierarchical Softmax，所以这里用Softmax代替。这层指定了CLASS_NUM，对于一篇文档，输出层会产生CLASS_NUM个概率值，分别表示此文档属于当前类的可能性。这层的output_shape=(BATCH_SIZE, CLASS_NUM)
    > 
    > 4\. 指定损失函数、优化器类型、评价指标，编译模型。损失函数我们设置为categorical_crossentropy，它就是我们上面所说的softmax回归的损失函数；优化器我们设置为SGD，表示随机梯度下降优化器；评价指标选择accuracy，表示精度。
    > 
    > 用训练数据feed模型时，你需要：
    > 
    > 1\. 将文档分好词，构建词汇表。词汇表中每个词用一个整数（索引）来代替，并预留"未知词"索引，假设为0；
    > 
    > 2\. 对类标进行onehot化。假设我们文本数据总共有3个类别，对应的类标分别是1、2、3，那么这三个类标对应的onehot向量分别是[1, 0,\
    > 0]、[0, 1, 0]、[0, 0, 1]；
    > 
    > 3\. 对一批文本，将每个文本转化为词索引序列，每个类标转化为onehot向量。就像之前的例子，"我 昨天 来到 达观数据"可能被转化为[10, 30,\
    > 80, 1000]；它属于类别1，它的类标就是[1, 0, 0]。由于我们设置了MAX_WORDS=500，这个短文本向量后面就需要补496个0，即[10, 30, 80, 1000, 0, 0, 0, ..., 0]。因此，batch_xs的 维度为( BATCH_SIZE,MAX_WORDS)，batch_ys的维度为（BATCH_SIZE, CLASS_NUM）。
    > 
    > 下面是构建模型的代码，数据处理、feed数据到模型的代码比较繁琐，这里不展示。
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/nW2ZPfuYqSKdibtkfPenkY4m4uAhJ0Q0XSLv0TicvYias0X9DM0J9ebibZjuGicutyCFvsCic5ceeGwXLOnYkHhtGznQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1 "技术干货丨fastText原理及实践")
    > 
    > NO.5
    > 
    > fastText原理及实践
    > 
    > fastText在达观数据的应用
    > 
    > fastText作为诞生不久的词向量训练、文本分类工具，在达观得到了比较深入的应用。主要被用在以下两个系统：
    > 
    > **1\. 同近义词挖掘。** Facebook开源的fastText工具也实现了词向量的训练，达观基于各种垂直领域的语料，使用其挖掘出一批同近义词；
    > 
    > **2\. 文本分类系统。** 在类标数、数据量都比较大时，达观会选择fastText 来做文本分类，以实现快速训练预测、节省内存的目的。
    > 





## Poincaré Embeddings for Learning Hierarchical Representations

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


