# NLP__資料收集2-2_單詞建模

[toc]
<!-- toc --> 


# ULMFiT

- [[1801.06146] Universal Language Model Fine-tuning for Text Classification](https://arxiv.org/abs/1801.06146)



# ELMo

- [[1802.05365] Deep contextualized word representations](https://arxiv.org/abs/1802.05365)



# Bert

- [[1810.04805] BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/abs/1810.04805)

- [google-research/bert: TensorFlow code and pre-trained models for BERT](https://github.com/google-research/bert)

## 从Word Embedding到Bert模型—自然语言处理中的预训练技术发展史

- [从Word Embedding到Bert模型—自然语言处理中的预训练技术发展史 - 知乎](https://zhuanlan.zhihu.com/p/49271699)

    > Bert最近很火，应该是最近最火爆的AI进展，网上的评价很高，那么Bert值得这么高的评价吗？我个人判断是值得。那为什么会有这么高的评价呢？是因为它有重大的理论或者模型创新吗？其实并没有，从模型创新角度看一般，创新不算大。但是架不住效果太好了，基本刷新了很多NLP的任务的最好性能，有些任务还被刷爆了，这个才是关键。另外一点是Bert具备广泛的通用性，就是说绝大部分NLP任务都可以采用类似的两阶段模式直接去提升效果，这个第二关键。客观的说，把Bert当做最近两年NLP重大进展的集大成者更符合事实。
    > 
    > 本文的主题是自然语言处理中的预训练过程，会大致说下NLP中的预训练技术是一步一步如何发展到Bert模型的，从中可以很自然地看到Bert的思路是如何逐渐形成的，Bert的历史沿革是什么，继承了什么，创新了什么，为什么效果那么好，主要原因是什么，以及为何说模型创新不算太大，为何说Bert是近年来NLP重大进展的集大成者。我们一步一步来讲，而串起来这个故事的脉络就是自然语言的预训练过程，但是落脚点还是在Bert身上。要讲自然语言的预训练，得先从图像领域的预训练说起。
    > 
    > ***图像领域的预训练***
    > --------------
    > 
    > 自从深度学习火起来后，预训练过程就是做图像或者视频领域的一种比较常规的做法，有比较长的历史了，而且这种做法很有效，能明显促进应用的效果。
    > 
    > ![](https://pic3.zhimg.com/80/v2-4c27ee0ff1fb87f27d55b007cb4ceb06_hd.jpg)
    > 
    > 那么图像领域怎么做预训练呢，上图展示了这个过程，我们设计好网络结构以后，对于图像来说一般是CNN的多层叠加网络结构，可以先用某个训练集合比如训练集合A或者训练集合B对这个网络进行预先训练，在A任务上或者B任务上学会网络参数，然后存起来以备后用。假设我们面临第三个任务C，网络结构采取相同的网络结构，在比较浅的几层CNN结构，网络参数初始化的时候可以加载A任务或者B任务学习好的参数，其它CNN高层参数仍然随机初始化。之后我们用C任务的训练数据来训练网络，此时有两种做法，一种是浅层加载的参数在训练C任务过程中不动，这种方法被称为"Frozen";另外一种是底层网络参数尽管被初始化了，在C任务训练过程中仍然随着训练的进程不断改变，这种一般叫"Fine-Tuning"，顾名思义，就是更好地把参数进行调整使得更适应当前的C任务。一般图像或者视频领域要做预训练一般都这么做。
    > 
    > 这么做有几个好处，首先，如果手头任务C的训练集合数据量较少的话，现阶段的好用的CNN比如Resnet/Densenet/Inception等网络结构层数很深，几百万上千万参数量算起步价，上亿参数的也很常见，训练数据少很难很好地训练这么复杂的网络，但是如果其中大量参数通过大的训练集合比如ImageNet预先训练好直接拿来初始化大部分网络结构参数，然后再用C任务手头比较可怜的数据量上Fine-tuning过程去调整参数让它们更适合解决C任务，那事情就好办多了。这样原先训练不了的任务就能解决了，即使手头任务训练数据也不少，加个预训练过程也能极大加快任务训练的收敛速度，所以这种预训练方式是老少皆宜的解决方案，另外疗效又好，所以在做图像处理领域很快就流行开来。
    > 
    > 那么新的问题来了，为什么这种预训练的思路是可行的？
    > 
    > ![](https://pic2.zhimg.com/80/v2-7cf372d37ea124baf56450dd6935e605_hd.jpg)
    > 
    > 目前我们已经知道，对于层级的CNN结构来说，不同层级的神经元学习到了不同类型的图像特征，由底向上特征形成层级结构，如上图所示，如果我们手头是个人脸识别任务，训练好网络后，把每层神经元学习到的特征可视化肉眼看一看每层学到了啥特征，你会看到最底层的神经元学到的是线段等特征，图示的第二个隐层学到的是人脸五官的轮廓，第三层学到的是人脸的轮廓，通过三步形成了特征的层级结构，越是底层的特征越是所有不论什么领域的图像都会具备的比如边角线弧线等底层基础特征，越往上抽取出的特征越与手头任务相关。正因为此，所以预训练好的网络参数，尤其是底层的网络参数抽取出特征跟具体任务越无关，越具备任务的通用性，所以这是为何一般用底层预训练好的参数初始化新任务网络参数的原因。而高层特征跟任务关联较大，实际可以不用使用，或者采用Fine-tuning用新数据集合清洗掉高层无关的特征抽取器。
    > 
    > ![](https://pic4.zhimg.com/80/v2-a30936681c07b850ebbad390c7cef7f3_hd.jpg)
    > 
    > 一般我们喜欢用ImageNet来做网络的预训练，主要有两点，一方面ImageNet是图像领域里有超多事先标注好训练数据的数据集合，分量足是个很大的优势，量越大训练出的参数越靠谱；另外一方面因为ImageNet有1000类，类别多，算是通用的图像数据，跟领域没太大关系，所以通用性好，预训练完后哪哪都能用，是个万金油。分量足的万金油当然老少通吃，人人喜爱。
    > 
    > 听完上述话，如果你是具备研究素质的人，也就是说具备好奇心，你一定会问下面这个问题："既然图像领域预训练这么好用，那干嘛自然语言处理不做这个事情呢？是不是搞NLP的人比搞CV的傻啊？就算你傻，你看见人家这么做，有样学样不就行了吗？这不就是创新吗，也许能成，万一成了，你看，你的成功来得就是这么突然!"
    > 
    > 嗯，好问题，其实搞NLP的人一点都不比你傻，早就有人尝试过了，不过总体而言不太成功而已。听说过word embedding吗？2003年出品，陈年技术，馥郁芳香。word embedding其实就是NLP里的早期预训练技术。当然也不能说word embedding不成功，一般加到下游任务里，都能有1到2个点的性能提升，只是没有那么耀眼的成功而已。
    > 
    > 没听过？那下面就把这段陈年老账讲给你听听。
    > 
    > ***Word Embedding考古史***
    > -----------------------
    > 
    > 这块大致讲讲Word Embedding的故事，很粗略，因为网上关于这个技术讲的文章太多了，汗牛冲动，我不属牛，此刻更没有流汗，所以其实丝毫没有想讲Word Embedding的冲动和激情，但是要说预训练又得从这开始，那就粗略地讲讲，主要是引出后面更精彩的部分。在说Word Embedding之前，先更粗略地说下语言模型，因为一般NLP里面做预训练一般的选择是用语言模型任务来做。
    > 
    > ![](https://pic2.zhimg.com/80/v2-64323e651f56edb618b70b229543d555_hd.jpg)
    > 
    > 什么是语言模型？其实看上面这张PPT上扣下来的图就明白了，为了能够量化地衡量哪个句子更像一句人话，可以设计如上图所示函数，核心函数P的思想是根据句子里面前面的一系列前导单词预测后面跟哪个单词的概率大小（理论上除了上文之外，也可以引入单词的下文联合起来预测单词出现概率）。句子里面每个单词都有个根据上文预测自己的过程，把所有这些单词的产生概率乘起来，数值越大代表这越像一句人话。语言模型压下暂且不表，我隐约预感到我这么讲你可能还是不太会明白，但是大概这个意思，不懂的可以去网上找，资料多得一样地汗牛冲动。
    > 
    > 假设现在让你设计一个神经网络结构，去做这个语言模型的任务，就是说给你很多语料做这个事情，训练好一个神经网络，训练好之后，以后输入一句话的前面几个单词，要求这个网络输出后面紧跟的单词应该是哪个，你会怎么做？
    > 
    > ![](https://pic2.zhimg.com/80/v2-e2842dd9bc442893bd53dd9fa32d6c9d_hd.jpg)
    > 
    > 你可以像上图这么设计这个网络结构，这其实就是大名鼎鼎的中文人称"神经网络语言模型"，英文小名NNLM的网络结构，用来做语言模型。这个工作有年头了，是个陈年老工作，是Bengio 在2003年发表在JMLR上的论文。它生于2003，火于2013，以后是否会不朽暂且不知，但是不幸的是出生后应该没有引起太大反响，沉寂十年终于时来运转沉冤得雪，在2013年又被NLP考古工作者从海底湿淋淋地捞出来了祭入神殿。为什么会发生这种技术奇遇记？你要想想2013年是什么年头，是深度学习开始渗透NLP领域的光辉时刻，万里长征第一步，而NNLM可以算是南昌起义第一枪。在深度学习火起来之前，极少有人用神经网络做NLP问题，如果你10年前坚持用神经网络做NLP，估计别人会认为你这人神经有问题。所谓红尘滚滚，谁也挡不住历史发展趋势的车轮，这就是个很好的例子。
    > 
    > 上面是闲话，闲言碎语不要讲，我们回来讲一讲NNLM的思路。先说训练过程，现在看其实很简单，见过RNN、LSTM、CNN后的你们回头再看这个网络甚至显得有些简陋。学习任务是输入某个句中单词 ![W_t="Bert"](http://www.zhihu.com/equation?tex=W_t%3D%E2%80%9CBert%E2%80%9D) 前面句子的t-1个单词，要求网络正确预测单词Bert，即最大化：
    > 
    > ![  P(W_t="Bert"|W_1,W_2,...W_(t-1);θ)](http://www.zhihu.com/equation?tex=++P%28W_t%3D%E2%80%9CBert%E2%80%9D%7CW_1%2CW_2%2C%E2%80%A6W_%28t-1%29%3B%CE%B8%29)
    > 
    > 前面任意单词 ![W_i](http://www.zhihu.com/equation?tex=W_i) 用Onehot编码（比如：0001000）作为原始单词输入，之后乘以矩阵Q后获得向量 ![C(W_i )](http://www.zhihu.com/equation?tex=C%28W_i+%29) ，每个单词的 ![C(W_i )](http://www.zhihu.com/equation?tex=C%28W_i+%29) 拼接，上接隐层，然后接softmax去预测后面应该后续接哪个单词。这个 ![C(W_i )](http://www.zhihu.com/equation?tex=C%28W_i+%29) 是什么？这其实就是单词对应的Word Embedding值，那个矩阵Q包含V行，V代表词典大小，每一行内容代表对应单词的Word embedding值。只不过Q的内容也是网络参数，需要学习获得，训练刚开始用随机值初始化矩阵Q，当这个网络训练好之后，矩阵Q的内容被正确赋值，每一行代表一个单词对应的Word embedding值。所以你看，通过这个网络学习语言模型任务，这个网络不仅自己能够根据上文预测后接单词是什么，同时获得一个副产品，就是那个矩阵Q，这就是单词的Word Embedding是被如何学会的。
    > 
    > 2013年最火的用语言模型做Word Embedding的工具是Word2Vec，后来又出了Glove，Word2Vec是怎么工作的呢？看下图。
    > 
    > ![](https://pic1.zhimg.com/80/v2-eadc8776d24d3050468907b35c79f274_hd.jpg)
    > 
    > Word2Vec的网络结构其实和NNLM是基本类似的，只是这个图长得清晰度差了点，看上去不像，其实它们是亲兄弟。不过这里需要指出：尽管网络结构相近，而且也是做语言模型任务，但是其训练方法不太一样。Word2Vec有两种训练方法，一种叫CBOW，核心思想是从一个句子里面把一个词抠掉，用这个词的上文和下文去预测被抠掉的这个词；第二种叫做Skip-gram，和CBOW正好反过来，输入某个单词，要求网络预测它的上下文单词。而你回头看看，NNLM是怎么训练的？是输入一个单词的上文，去预测这个单词。这是有显著差异的。为什么Word2Vec这么处理？原因很简单，因为Word2Vec和NNLM不一样，NNLM的主要任务是要学习一个解决语言模型任务的网络结构，语言模型就是要看到上文预测下文，而word embedding只是无心插柳的一个副产品。但是Word2Vec目标不一样，它单纯就是要word embedding的，这是主产品，所以它完全可以随性地这么去训练网络。
    > 
    > 为什么要讲Word2Vec呢？这里主要是要引出CBOW的训练方法，BERT其实跟它有关系，后面会讲它们之间是如何的关系，当然它们的关系BERT作者没说，是我猜的，至于我猜的对不对，后面你看后自己判断。
    > 
    > ![](https://pic3.zhimg.com/80/v2-ffc7595cf4d9548d59a7fd90241f151e_hd.jpg)
    > 
    > 使用Word2Vec或者Glove，通过做语言模型任务，就可以获得每个单词的Word Embedding，那么这种方法的效果如何呢？上图给了网上找的几个例子，可以看出有些例子效果还是很不错的，一个单词表达成Word Embedding后，很容易找出语义相近的其它词汇。
    > 
    > 我们的主题是预训练，那么问题是Word Embedding这种做法能算是预训练吗？这其实就是标准的预训练过程。要理解这一点要看看学会Word Embedding后下游任务是怎么用它的。
    > 
    > ![](https://pic3.zhimg.com/80/v2-5875b516b8b3d4bad083fc2280d095fa_hd.jpg)
    > 
    > 假设如上图所示，我们有个NLP的下游任务，比如QA，就是问答问题，所谓问答问题，指的是给定一个问题X，给定另外一个句子Y,要判断句子Y是否是问题X的正确答案。问答问题假设设计的网络结构如上图所示，这里不展开讲了，懂得自然懂，不懂的也没关系，因为这点对于本文主旨来说不关键，关键是网络如何使用训练好的Word Embedding的。它的使用方法其实和前面讲的NNLM是一样的，句子中每个单词以Onehot形式作为输入，然后乘以学好的Word Embedding矩阵Q，就直接取出单词对应的Word Embedding了。这乍看上去好像是个查表操作，不像是预训练的做法是吧？其实不然，那个Word Embedding矩阵Q其实就是网络Onehot层到embedding层映射的网络参数矩阵。所以你看到了，使用Word Embedding等价于什么？等价于把Onehot层到embedding层的网络用预训练好的参数矩阵Q初始化了。这跟前面讲的图像领域的低层预训练过程其实是一样的，区别无非Word Embedding只能初始化第一层网络参数，再高层的参数就无能为力了。下游NLP任务在使用Word Embedding的时候也类似图像有两种做法，一种是Frozen，就是Word Embedding那层网络参数固定不动；另外一种是Fine-Tuning，就是Word Embedding这层参数使用新的训练集合训练也需要跟着训练过程更新掉。
    > 
    > 上面这种做法就是18年之前NLP领域里面采用预训练的典型做法，之前说过，Word Embedding其实对于很多下游NLP任务是有帮助的，只是帮助没有大到闪瞎忘记戴墨镜的围观群众的双眼而已。那么新问题来了，为什么这样训练及使用Word Embedding的效果没有期待中那么好呢？答案很简单，因为Word Embedding有问题呗。这貌似是个比较弱智的答案，关键是Word Embedding存在什么问题？这其实是个好问题。
    > 
    > ![](https://pic3.zhimg.com/80/v2-43671d49b40c4b8fffec102e5051809e_hd.jpg)
    > 
    > 这片在Word Embedding头上笼罩了好几年的乌云是什么？是多义词问题。我们知道，多义词是自然语言中经常出现的现象，也是语言灵活性和高效性的一种体现。多义词对Word Embedding来说有什么负面影响？如上图所示，比如多义词Bank，有两个常用含义，但是Word Embedding在对bank这个单词进行编码的时候，是区分不开这两个含义的，因为它们尽管上下文环境中出现的单词不同，但是在用语言模型训练的时候，不论什么上下文的句子经过word2vec，都是预测相同的单词bank，而同一个单词占的是同一行的参数空间，这导致两种不同的上下文信息都会编码到相同的word embedding空间里去。所以word embedding无法区分多义词的不同语义，这就是它的一个比较严重的问题。
    > 
    > 你可能觉得自己很聪明，说这可以解决啊，确实也有很多研究人员提出很多方法试图解决这个问题，但是从今天往回看，这些方法看上去都成本太高或者太繁琐了，有没有简单优美的解决方案呢？
    > 
    > ELMO提供了一种简洁优雅的解决方案。
    > 
    > ***从Word Embedding到ELMO***
    > --------------------------
    > 
    > ELMO是"Embedding from Language Models"的简称，其实这个名字并没有反应它的本质思想，提出ELMO的论文题目："Deep contextualized word representation"更能体现其精髓，而精髓在哪里？在deep contextualized这个短语，一个是deep，一个是context，其中context更关键。在此之前的Word Embedding本质上是个静态的方式，所谓静态指的是训练好之后每个单词的表达就固定住了，以后使用的时候，不论新句子上下文单词是什么，这个单词的Word Embedding不会跟着上下文场景的变化而改变，所以对于比如Bank这个词，它事先学好的Word Embedding中混合了几种语义 ，在应用中来了个新句子，即使从上下文中（比如句子包含money等词）明显可以看出它代表的是"银行"的含义，但是对应的Word Embedding内容也不会变，它还是混合了多种语义。这是为何说它是静态的，这也是问题所在。ELMO的本质思想是：我事先用语言模型学好一个单词的Word Embedding，此时多义词无法区分，不过这没关系。在我实际使用Word Embedding的时候，单词已经具备了特定的上下文了，这个时候我可以根据上下文单词的语义去调整单词的Word Embedding表示，这样经过调整后的Word Embedding更能表达在这个上下文中的具体含义，自然也就解决了多义词的问题了。所以ELMO本身是个根据当前上下文对Word Embedding动态调整的思路。
    > 
    > ![](https://pic4.zhimg.com/80/v2-fe335ea9fdcd6e0e5ec4a9ac0e2290db_hd.jpg)
    > 
    > ELMO采用了典型的两阶段过程，第一个阶段是利用语言模型进行预训练；第二个阶段是在做下游任务时，从预训练网络中提取对应单词的网络各层的Word Embedding作为新特征补充到下游任务中。上图展示的是其预训练过程，它的网络结构采用了双层双向LSTM，目前语言模型训练的任务目标是根据单词 ![W_i](http://www.zhihu.com/equation?tex=W_i) 的上下文去正确预测单词 ![W_i](http://www.zhihu.com/equation?tex=W_i) ， ![W_i](http://www.zhihu.com/equation?tex=W_i) 之前的单词序列Context-before称为上文，之后的单词序列Context-after称为下文。图中左端的前向双层LSTM代表正方向编码器，输入的是从左到右顺序的除了预测单词外 ![W_i](http://www.zhihu.com/equation?tex=W_i) 的上文Context-before和下文Context-after；右端的逆向双层LSTM代表反方向编码器，输入的是从右到左的逆序的句子上文和下文；每个编码器的深度都是两层LSTM叠加，而每一层的正向和逆向单词编码会拼接到一起。这个网络结构其实在NLP中是很常用的。使用这个网络结构利用大量语料做语言模型任务就能预先训练好这个网络，如果训练好这个网络后，输入一个新句子 ![Snew](http://www.zhihu.com/equation?tex=Snew) ，句子中每个单词都能得到对应的三个Embedding:最底层是单词的Word Embedding，往上走是第一层双向LSTM中对应单词位置的Embedding，这层编码单词的句法信息更多一些；再往上走是第二层LSTM中对应单词位置的Embedding，这层编码单词的语义信息更多一些。也就是说，ELMO的预训练过程不仅仅学会单词的Word Embedding，还学会了一个双层双向的LSTM网络结构，而这两者后面都有用。
    > 
    > ![](https://pic2.zhimg.com/80/v2-ef6513ff29e3234011221e4be2e97615_hd.jpg)
    > 
    > 上面介绍的是ELMO的第一阶段：预训练阶段。那么预训练好网络结构后，如何给下游任务使用呢？上图展示了下游任务的使用过程，比如我们的下游任务仍然是QA问题，此时对于问句X，我们可以先将句子X作为预训练好的ELMO网络的输入，这样句子X中每个单词在ELMO网络中都能获得对应的三个Embedding，之后给予这三个Embedding中的每一个Embedding一个权重a，这个权重可以学习得来，根据各自权重累加求和，将三个Embedding整合成一个。然后将整合后的这个Embedding作为X句在自己任务的那个网络结构中对应单词的输入，以此作为补充的新特征给下游任务使用。对于上图所示下游任务QA中的回答句子Y来说也是如此处理。因为ELMO给下游提供的是每个单词的特征形式，所以这一类预训练的方法被称为"Feature-based Pre-Training"。至于为何这么做能够达到区分多义词的效果，你可以想一想，其实比较容易想明白原因。
    > 
    > ![](https://pic4.zhimg.com/80/v2-3d058e0f20bfd598898f38e0cefc2b5f_hd.jpg)
    > 
    > 上面这个图是TagLM采用类似ELMO的思路做命名实体识别任务的过程，其步骤基本如上述ELMO的思路，所以此处不展开说了。TagLM的论文发表在2017年的ACL会议上，作者就是AllenAI里做ELMO的那些人，所以可以将TagLM看做ELMO的一个前导工作。前几天这个PPT发出去后有人质疑说FastAI的在18年4月提出的ULMFiT才是抛弃传统Word Embedding引入新模式的开山之作，我深不以为然。首先TagLM出现的更早而且模式基本就是ELMO的思路；另外ULMFiT使用的是三阶段模式，在通用语言模型训练之后，加入了一个领域语言模型预训练过程，而且论文重点工作在这块，方法还相对比较繁杂，这并不是一个特别好的主意，因为领域语言模型的限制是它的规模往往不可能特别大，精力放在这里不太合适，放在通用语言模型上感觉更合理；再者，尽管ULFMiT实验做了6个任务，但是都集中在分类问题相对比较窄，不如ELMO验证的问题领域广，我觉得这就是因为第二步那个领域语言模型带来的限制。所以综合看，尽管ULFMiT也是个不错的工作，但是重要性跟ELMO比还是差一档，当然这是我个人看法。
    > 
    > ![](https://pic2.zhimg.com/80/v2-9ebad261ecc7be832553e4320aefa745_hd.jpg)
    > 
    > 前面我们提到静态Word Embedding无法解决多义词的问题，那么ELMO引入上下文动态调整单词的embedding后多义词问题解决了吗？解决了，而且比我们期待的解决得还要好。上图给了个例子，对于Glove训练出的Word Embedding来说，多义词比如play，根据它的embedding找出的最接近的其它单词大多数集中在体育领域，这很明显是因为训练数据中包含play的句子中体育领域的数量明显占优导致；而使用ELMO，根据上下文动态调整后的embedding不仅能够找出对应的"演出"的相同语义的句子，而且还可以保证找出的句子中的play对应的词性也是相同的，这是超出期待之处。之所以会这样，是因为我们上面提到过，第一层LSTM编码了很多句法信息，这在这里起到了重要作用。
    > 
    > ![](https://pic3.zhimg.com/80/v2-360d10468d7a8878627c68780fe6d502_hd.jpg)
    > 
    > ELMO经过这般操作，效果如何呢？实验效果见上图，6个NLP任务中性能都有幅度不同的提升，最高的提升达到25%左右，而且这6个任务的覆盖范围比较广，包含句子语义关系判断，分类任务，阅读理解等多个领域，这说明其适用范围是非常广的，普适性强，这是一个非常好的优点。
    > 
    > ![](https://pic4.zhimg.com/80/v2-50c143b95e2d566d99d97be02834c447_hd.jpg)
    > 
    > 那么站在现在这个时间节点看，ELMO有什么值得改进的缺点呢？首先，一个非常明显的缺点在特征抽取器选择方面，ELMO使用了LSTM而不是新贵Transformer，Transformer是谷歌在17年做机器翻译任务的"Attention is all you need"的论文中提出的，引起了相当大的反响，很多研究已经证明了Transformer提取特征的能力是要远强于LSTM的。如果ELMO采取Transformer作为特征提取器，那么估计Bert的反响远不如现在的这种火爆场面。另外一点，ELMO采取双向拼接这种融合特征的能力可能比Bert一体化的融合特征方式弱，但是，这只是一种从道理推断产生的怀疑，目前并没有具体实验说明这一点。
    > 
    > 我们如果把ELMO这种预训练方法和图像领域的预训练方法对比，发现两者模式看上去还是有很大差异的。除了以ELMO为代表的这种基于特征融合的预训练方法外，NLP里还有一种典型做法，这种做法和图像领域的方式就是看上去一致的了，一般将这种方法称为"基于Fine-tuning的模式"，而GPT就是这一模式的典型开创者。
    > 
    > ***从Word Embedding到GPT***
    > -------------------------
    > 
    > ![](https://pic1.zhimg.com/80/v2-5028b1de8fb50e6630cc9839f0b16568_hd.jpg)
    > 
    > GPT是"Generative Pre-Training"的简称，从名字看其含义是指的通用的预训练，核心在通用上。GPT也采用两阶段过程，第一个阶段是利用语言模型进行预训练，第二阶段通过Fine-tuning的模式解决下游任务。上图展示了GPT的预训练过程，其实和ELMO是类似的，主要不同在于两点：首先，特征抽取器不是用的RNN，而是用的Transformer，上面提到过它的特征抽取能力要强于RNN，这个选择很明显是很明智的；其次，GPT的预训练虽然仍然是以语言模型作为目标任务，但是采用的是单向的语言模型，所谓"单向"的含义是指：语言模型训练的任务目标是根据 ![W_i](http://www.zhihu.com/equation?tex=W_i) 单词的上下文去正确预测单词 ![W_i](http://www.zhihu.com/equation?tex=W_i) ， ![W_i](http://www.zhihu.com/equation?tex=W_i) 之前的单词序列Context-before称为上文，之后的单词序列Context-after称为下文。ELMO在做语言模型预训练的时候，预测单词 ![W_i](http://www.zhihu.com/equation?tex=W_i) 同时使用了上文和下文，而GPT则只采用Context-before这个单词的上文来进行预测，而抛开了下文。这个选择现在看不是个太好的选择，原因很简单，它没有把单词的下文融合进来，这限制了其在更多应用场景的效果，比如阅读理解这种任务，在做任务的时候是可以允许同时看到上文和下文一起做决策的。如果预训练时候不把单词的下文嵌入到Word Embedding中，是很吃亏的，白白丢掉了很多信息。
    > 
    > 这里强行插入一段简单提下Transformer，尽管上面提到了，但是说的还不完整，补充两句。首先，Transformer是个叠加的"自注意力机制（Self Attention）"构成的深度网络，是目前NLP里最强的特征提取器，注意力这个机制在此被发扬光大，从任务的配角不断抢戏，直到Transformer一跃成为踢开RNN和CNN传统特征提取器，荣升头牌，大红大紫。你问了：什么是注意力机制？这里再插个广告，对注意力不了解的可以参考鄙人16年出品17年修正的下文："[深度学习中的注意力模型](https://zhuanlan.zhihu.com/p/37601161)"，补充下相关基础知识，如果不了解注意力机制你肯定会落后时代的发展。而介绍Transformer比较好的文章可以参考"[The Annotated Transformer.](http://link.zhihu.com/?target=http%3A//nlp.seas.harvard.edu/2018/04/03/attention.html) "这里不展开介绍。
    > 
    > 其次，我的判断是Transformer在未来会逐渐替代掉RNN成为主流的NLP工具，RNN一直受困于其并行计算能力，这是因为它本身结构的序列性依赖导致的，尽管很多人在试图通过修正RNN结构来修正这一点，但是我不看好这种模式，因为给马车换轮胎不如把它升级到汽车，这个道理很好懂，更何况目前汽车的雏形已经出现了，干嘛还要执着在换轮胎这个事情呢？是吧？再说CNN，CNN在NLP里一直没有形成主流，CNN的最大优点是易于做并行计算，所以速度快，但是在捕获NLP的序列关系尤其是长距离特征方面天然有缺陷，不是做不到而是做不好，目前也有很多改进模型，但是特别成功的不多。综合各方面情况，很明显Transformer同时具备并行性好，又适合捕获长距离特征，没有理由不在赛跑比赛中跑不过RNN和CNN。
    > 
    > 好了，题外话结束，我们再回到主题，接着说GPT。上面讲的是GPT如何进行第一阶段的预训练，那么假设预训练好了网络模型，后面下游任务怎么用？它有自己的个性，和ELMO的方式大有不同。
    > 
    > ![](https://pic3.zhimg.com/80/v2-587528a22eff055b6f479dae67f7c1aa_hd.jpg)
    > 
    > 上图展示了GPT在第二阶段如何使用。首先，对于不同的下游任务来说，本来你可以任意设计自己的网络结构，现在不行了，你要向GPT的网络结构看齐，把任务的网络结构改造成和GPT的网络结构是一样的。然后，在做下游任务的时候，利用第一步预训练好的参数初始化GPT的网络结构，这样通过预训练学到的语言学知识就被引入到你手头的任务里来了，这是个非常好的事情。再次，你可以用手头的任务去训练这个网络，对网络参数进行Fine-tuning，使得这个网络更适合解决手头的问题。就是这样。看到了么？这有没有让你想起最开始提到的图像领域如何做预训练的过程（请参考上图那句非常容易暴露年龄的歌词）？对，这跟那个模式是一模一样的。
    > 
    > 这里引入了一个新问题：对于NLP各种花样的不同任务，怎么改造才能靠近GPT的网络结构呢？
    > 
    > ![](https://pic1.zhimg.com/80/v2-4c1dbed34a8f8469dc0fefe44b860edc_hd.jpg)
    > 
    > GPT论文给了一个改造施工图如上，其实也很简单：对于分类问题，不用怎么动，加上一个起始和终结符号即可；对于句子关系判断问题，比如Entailment，两个句子中间再加个分隔符即可；对文本相似性判断问题，把两个句子顺序颠倒下做出两个输入即可，这是为了告诉模型句子顺序不重要；对于多项选择问题，则多路输入，每一路把文章和答案选项拼接作为输入即可。从上图可看出，这种改造还是很方便的，不同任务只需要在输入部分施工即可。
    > 
    > ![](https://pic3.zhimg.com/80/v2-bd58acbb2096e01ee322c0b9b2ed05fe_hd.jpg)
    > 
    > GPT的效果是非常令人惊艳的，在12个任务里，9个达到了最好的效果，有些任务性能提升非常明显。
    > 
    > ![](https://pic3.zhimg.com/80/v2-98bf16ea0d734ffae0989dec55df9bca_hd.jpg)
    > 
    > 那么站在现在的时间节点看，GPT有什么值得改进的地方呢？其实最主要的就是那个单向语言模型，如果改造成双向的语言模型任务估计也没有Bert太多事了。当然，即使如此GPT也是非常非常好的一个工作，跟Bert比，其作者炒作能力亟待提升。
    > 
    > ***Bert的诞生***
    > -------------
    > 
    > ![](https://pic2.zhimg.com/80/v2-477b738008eb2b5650577bbd220bc58d_hd.jpg)
    > 
    > 我们经过跋山涉水，终于到了目的地Bert模型了。
    > 
    > Bert采用和GPT完全相同的两阶段模型，首先是语言模型预训练；其次是使用Fine-Tuning模式解决下游任务。和GPT的最主要不同在于在预训练阶段采用了类似ELMO的双向语言模型，当然另外一点是语言模型的数据规模要比GPT大。所以这里Bert的预训练过程不必多讲了。
    > 
    > ![](https://pic1.zhimg.com/80/v2-7aa8d891632fdd522499f96e7f14cac4_hd.jpg)
    > 
    > 第二阶段，Fine-Tuning阶段，这个阶段的做法和GPT是一样的。当然，它也面临着下游任务网络结构改造的问题，在改造任务方面Bert和GPT有些不同，下面简单介绍一下。
    > 
    > ![](https://pic4.zhimg.com/80/v2-a0d3d439fe45cb03f7bd8a4936992a6b_hd.jpg)
    > 
    > 在介绍Bert如何改造下游任务之前，先大致说下NLP的几类问题，说这个是为了强调Bert的普适性有多强。通常而言，绝大部分NLP问题可以归入上图所示的四类任务中：一类是序列标注，这是最典型的NLP任务，比如中文分词，词性标注，命名实体识别，语义角色标注等都可以归入这一类问题，它的特点是句子中每个单词要求模型根据上下文都要给出一个分类类别。第二类是分类任务，比如我们常见的文本分类，情感计算等都可以归入这一类。它的特点是不管文章有多长，总体给出一个分类类别即可。第三类任务是句子关系判断，比如Entailment，QA，语义改写，自然语言推理等任务都是这个模式，它的特点是给定两个句子，模型判断出两个句子是否具备某种语义关系；第四类是生成式任务，比如机器翻译，文本摘要，写诗造句，看图说话等都属于这一类。它的特点是输入文本内容后，需要自主生成另外一段文字。
    > 
    > ![](https://pic3.zhimg.com/80/v2-0245d07d9e227d1cb1091d96bf499032_hd.jpg)
    > 
    > 对于种类如此繁多而且各具特点的下游NLP任务，Bert如何改造输入输出部分使得大部分NLP任务都可以使用Bert预训练好的模型参数呢？上图给出示例，对于句子关系类任务，很简单，和GPT类似，加上一个起始和终结符号，句子之间加个分隔符即可。对于输出来说，把第一个起始符号对应的Transformer最后一层位置上面串接一个softmax分类层即可。对于分类问题，与GPT一样，只需要增加起始和终结符号，输出部分和句子关系判断任务类似改造；对于序列标注问题，输入部分和单句分类是一样的，只需要输出部分Transformer最后一层每个单词对应位置都进行分类即可。从这里可以看出，上面列出的NLP四大任务里面，除了生成类任务外，Bert其它都覆盖到了，而且改造起来很简单直观。尽管Bert论文没有提，但是稍微动动脑子就可以想到，其实对于机器翻译或者文本摘要，聊天机器人这种生成式任务，同样可以稍作改造即可引入Bert的预训练成果。只需要附着在S2S结构上，encoder部分是个深度Transformer结构，decoder部分也是个深度Transformer结构。根据任务选择不同的预训练数据初始化encoder和decoder即可。这是相当直观的一种改造方法。当然，也可以更简单一点，比如直接在单个Transformer结构上加装隐层产生输出也是可以的。不论如何，从这里可以看出，NLP四大类任务都可以比较方便地改造成Bert能够接受的方式。这其实是Bert的非常大的优点，这意味着它几乎可以做任何NLP的下游任务，具备普适性，这是很强的。
    > 
    > ![](https://pic1.zhimg.com/80/v2-e9e7f70582e63fae44c1e97d70fcca24_hd.jpg)
    > 
    > Bert采用这种两阶段方式解决各种NLP任务效果如何？在11个各种类型的NLP任务中达到目前最好的效果，某些任务性能有极大的提升。一个新模型好不好，效果才是王道。
    > 
    > ![](https://pic3.zhimg.com/80/v2-330788d33e39396db17655e42c7f6afa_hd.jpg)
    > 
    > 到这里我们可以再梳理下几个模型之间的演进关系。从上图可见，Bert其实和ELMO及GPT存在千丝万缕的关系，比如如果我们把GPT预训练阶段换成双向语言模型，那么就得到了Bert；而如果我们把ELMO的特征抽取器换成Transformer，那么我们也会得到Bert。所以你可以看出：Bert最关键两点，一点是特征抽取器采用Transformer；第二点是预训练的时候采用双向语言模型。
    > 
    > 那么新问题来了：对于Transformer来说，怎么才能在这个结构上做双向语言模型任务呢？乍一看上去好像不太好搞。我觉得吧，其实有一种很直观的思路，怎么办？看看ELMO的网络结构图，只需要把两个LSTM替换成两个Transformer，一个负责正向，一个负责反向特征提取，其实应该就可以。当然这是我自己的改造，Bert没这么做。那么Bert是怎么做的呢？我们前面不是提过Word2Vec吗？我前面肯定不是漫无目的地提到它，提它是为了在这里引出那个CBOW训练方法，所谓写作时候埋伏笔的"草蛇灰线，伏脉千里"，大概就是这个意思吧？前面提到了CBOW方法，它的核心思想是：在做语言模型任务的时候，我把要预测的单词抠掉，然后根据它的上文Context-Before和下文Context-after去预测单词。其实Bert怎么做的？Bert就是这么做的。从这里可以看到方法间的继承关系。当然Bert作者没提Word2Vec及CBOW方法，这是我的判断，Bert作者说是受到完形填空任务的启发，这也很可能，但是我觉得他们要是没想到过CBOW估计是不太可能的。
    > 
    > 从这里可以看出，在文章开始我说过Bert在模型方面其实没有太大创新，更像一个最近几年NLP重要技术的集大成者，原因在于此，当然我不确定你怎么看，是否认同这种看法，而且我也不关心你怎么看。其实Bert本身的效果好和普适性强才是最大的亮点。
    > 
    > ![](https://pic1.zhimg.com/80/v2-146b89cf7ec3eceb349c0d39f8aea228_hd.jpg)
    > 
    > 那么Bert本身在模型和方法角度有什么创新呢？就是论文中指出的Masked 语言模型和Next Sentence Prediction。而Masked语言模型上面讲了，本质思想其实是CBOW，但是细节方面有改进。
    > 
    > ![](https://pic1.zhimg.com/80/v2-5893870247eedd20b9cb43507d065150_hd.jpg)
    > 
    > Masked双向语言模型向上图展示这么做：随机选择语料中15%的单词，把它抠掉，也就是用[Mask]掩码代替原始单词，然后要求模型去正确预测被抠掉的单词。但是这里有个问题：训练过程大量看到[mask]标记，但是真正后面用的时候是不会有这个标记的，这会引导模型认为输出是针对[mask]这个标记的，但是实际使用又见不到这个标记，这自然会有问题。为了避免这个问题，Bert改造了一下，15%的被上天选中要执行[mask]替身这项光荣任务的单词中，只有80%真正被替换成[mask]标记，10%被狸猫换太子随机替换成另外一个单词，10%情况这个单词还待在原地不做改动。这就是Masked双向语音模型的具体做法。
    > 
    > ![](https://pic1.zhimg.com/80/v2-5a51a24c706135ddb9515791715be9bc_hd.jpg)
    > 
    > 至于说"Next Sentence Prediction"，指的是做语言模型预训练的时候，分两种情况选择两个句子，一种是选择语料中真正顺序相连的两个句子；另外一种是第二个句子从语料库中抛色子，随机选择一个拼到第一个句子后面。我们要求模型除了做上述的Masked语言模型任务外，附带再做个句子关系预测，判断第二个句子是不是真的是第一个句子的后续句子。之所以这么做，是考虑到很多NLP任务是句子关系判断任务，单词预测粒度的训练到不了句子关系这个层级，增加这个任务有助于下游句子关系判断任务。所以可以看到，它的预训练是个多任务过程。这也是Bert的一个创新。
    > 
    > ![](https://pic3.zhimg.com/80/v2-6cf98bd136d57b04067077c1c189f6c2_hd.jpg)
    > 
    > 上面这个图给出了一个中文训练实例，从中可以体会下上面讲的masked语言模型和下句预测任务。训练数据就长这种样子。
    > 
    > ![](https://pic3.zhimg.com/80/v2-3898b02c6b71662a1076b6621a6661a2_hd.jpg)
    > 
    > 顺带讲解下Bert的输入部分，也算是有些特色。它的输入部分是个线性序列，两个句子通过分隔符分割，最前面和最后增加两个标识符号。每个单词有三个embedding:位置信息embedding，这是因为NLP中单词顺序是很重要的特征，需要在这里对位置信息进行编码；单词embedding,这个就是我们之前一直提到的单词embedding；第三个是句子embedding，因为前面提到训练数据都是由两个句子构成的，那么每个句子有个句子整体的embedding项对应给每个单词。把单词对应的三个embedding叠加，就形成了Bert的输入。
    > 
    > ![](https://pic3.zhimg.com/80/v2-f7227ae6232e45150c1912d2940a7206_hd.jpg)
    > 
    > 至于Bert在预训练的输出部分如何组织，可以参考上图的注释。
    > 
    > ![](https://pic3.zhimg.com/80/v2-3b53d187704109dc3c68533551ee62fa_hd.jpg)
    > 
    > 我们说过Bert效果特别好，那么到底是什么因素起作用呢？如上图所示，对比试验可以证明，跟GPT相比，双向语言模型起到了最主要的作用，对于那些需要看到下文的任务来说尤其如此。而预测下个句子来说对整体性能来说影响不算太大，跟具体任务关联度比较高。
    > 
    > ![](https://pic4.zhimg.com/80/v2-b8a2679bd6dfdae09abb53a0fdf972db_hd.jpg)
    > 
    > 最后，我讲讲我对Bert的评价和看法，我觉得Bert是NLP里里程碑式的工作，对于后面NLP的研究和工业应用会产生长久的影响，这点毫无疑问。但是从上文介绍也可以看出，从模型或者方法角度看，Bert借鉴了ELMO，GPT及CBOW，主要提出了Masked 语言模型及Next Sentence Prediction，但是这里Next Sentence Prediction基本不影响大局，而Masked LM明显借鉴了CBOW的思想。所以说Bert的模型没什么大的创新，更像最近几年NLP重要进展的集大成者，这点如果你看懂了上文估计也没有太大异议，如果你有大的异议，杠精这个大帽子我随时准备戴给你。如果归纳一下这些进展就是：首先是两阶段模型，第一阶段双向语言模型预训练，这里注意要用双向而不是单向，第二阶段采用具体任务Fine-tuning或者做特征集成；第二是特征抽取要用Transformer作为特征提取器而不是RNN或者CNN；第三，双向语言模型可以采取CBOW的方法去做（当然我觉得这个是个细节问题，不算太关键，前两个因素比较关键）。Bert最大的亮点在于效果好及普适性强，几乎所有NLP任务都可以套用Bert这种两阶段解决思路，而且效果应该会有明显提升。可以预见的是，未来一段时间在NLP应用领域，Transformer将占据主导地位，而且这种两阶段预训练方法也会主导各种应用。
    > 
    > 另外，我们应该弄清楚预训练这个过程本质上是在做什么事情，本质上预训练是通过设计好一个网络结构来做语言模型任务，然后把大量甚至是无穷尽的无标注的自然语言文本利用起来，预训练任务把大量语言学知识抽取出来编码到网络结构中，当手头任务带有标注信息的数据有限时，这些先验的语言学特征当然会对手头任务有极大的特征补充作用，因为当数据有限的时候，很多语言学现象是覆盖不到的，泛化能力就弱，集成尽量通用的语言学知识自然会加强模型的泛化能力。如何引入先验的语言学知识其实一直是NLP尤其是深度学习场景下的NLP的主要目标之一，不过一直没有太好的解决办法，而ELMO/GPT/Bert的这种两阶段模式看起来无疑是解决这个问题自然又简洁的方法，这也是这些方法的主要价值所在。
    > 
    > 对于当前NLP的发展方向，我个人觉得有两点非常重要，一个是需要更强的特征抽取器，目前看Transformer会逐渐担当大任，但是肯定还是不够强的，需要发展更强的特征抽取器；第二个就是如何优雅地引入大量无监督数据中包含的语言学知识，目前看预训练这种两阶段方法还是很有效的，当然后面肯定还会有更好的模型出现。
    > 
    > 完了，这就是自然语言模型预训练的发展史。
    >
    > 注：本文可以任意转载，转载时请标明作者和出处。
    > 

## 谷歌终于开源BERT代码：3 亿参数量，机器之心全面解读 

- [谷歌终于开源BERT代码：3 亿参数量，机器之心全面解读 ](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650751075&idx=2&sn=0a3ecd1af5f8549051760775e34db342&chksm=871a841db06d0d0bcf3cc4e620bb384e050ba6e92224d338a8ddc1543add97a4a4e7919ebf15&mpshare=1&scene=24&srcid=#rd)

    > BERT 的核心过程非常简洁，它会先从数据集抽取两个句子，其中第二句是第一句的下一句的概率是 50%，这样就能学习句子之间的关系。其次随机去除两个句子中的一些词，并要求模型预测这些词是什么，这样就能学习句子内部的关系。最后再将经过处理的句子传入大型 Transformer 模型，并通过两个损失函数同时学习上面两个目标就能完成训练。
    > 
    > 业界广泛认为谷歌新提出来的 BERT 预训练模型主要在三方面会启发今后的研究，即对预训练 NLP 模型的贡献、计算力对研究的重要性、以及研究团队和工程能力。
    > 
    > 
    > **预训练 NLP 模型**
    > 
    > 其实预训练模型或迁移学习很早就有人研究，但真正广受关注还是在近几年。清华大学刘知远表示：「大概在前几年，可能很多人都认为预训练的意义不是特别大，当时感觉直接在特定任务上做训练可能效果会更好。我认为 BERT 相当于在改变大家的观念，即在极大数据集上进行预训练对于不同的 NLP 任务都会有帮助。」
    > 
    > 虽然 CV 领域的预训练模型展现出强大的能力，但 NLP 领域也一直探讨实现无监督预训练的方法，复旦大学邱锡鹏说：「其实早在 16 年的时候，我们在知乎上讨论过 NLP 的发展方向。我记得当初回答 NLP 有两个问题，其中第一个就是怎么充分挖掘无标注数据，而 BERT 这篇论文提供了两个很好的方向来挖掘无标注数据的潜力。虽然这两个方法本身并不新颖，但它相当于做得非常极致。另外一个问题是 Transformer，它当时在机器翻译中已经展示出非常强的能力，其实越大的数据量就越能显示出这个结构的优点，因为它可以叠加非常深的层级。」
    > 
    > 深度好奇创始人兼 CTO 吕正东博士最后总结道：「通用的 composition architecture + 大量数据 + 好的 unsupervised 损失函数，带来的好的 sentence model, 可以走很远。它的架构以及它作为 pre-trained model 的使用方式，都非常类似视觉领域的好的深度分类模型，如 AlexNet 和 Residual Net。」
    > 
    > **计算力**
    > 
    > 尽管 BERT 效果惊人，但它需要的计算量非常大，原作者在论文中也表示每次只能预测 15% 的词，因此模型收敛得非常慢。BERT 的作者在 Reddit 上也表示预训练的计算量非常大，Jacob 说：「OpenAI 的 Transformer 有 12 层、768 个隐藏单元，他们使用 8 块 P100 在 8 亿词量的数据集上训练 40 个 Epoch 需要一个月，而 BERT-Large 模型有 24 层、2014 个隐藏单元，它们在有 33 亿词量的数据集上需要训练 40 个 Epoch，因此在 8 块 P100 上可能需要 1 年？16 Cloud TPU 已经是非常大的计算力了。」
    > 
    > 吕正东表示：「BERT 是一个 google 风格的暴力模型，暴力模型的好处是验证概念上简单模型的有效性，从而粉碎大家对于奇技淫巧的迷恋； 但暴力模型通常出现的一个坏处是'there is no new physics'，我相信不少人对 BERT 都有那种『我也曾经多多少少想过类似的事情』的感觉，虽然也仅仅是想过而已。」
    > 
    > **研究团队**
    > 
    > 最后对于 BERT 的研究团队，微软全球技术院士黄学东说：「包括一作 Jacob 在内，BERT 四个作者有三个是微软前员工。这个研究其实改变了自然语言处理今后的方向，他们的贡献应该和当年微软在计算机视觉中用 ResNet 所造就的贡献是一样的。可惜 Jacob 不是在我们团队做的，我们本来可以多一项光荣的任务。我非常喜欢 Jacob 的东西，他以前也是微软的优秀员工。」
    > 
    > **BERT 官方预训练模型**
    > 
    > 在众多研究者的关注下，谷歌发布了 BERT 的实现代码与预训练模型。其中代码比较简单，基本上是标准的 Transformer 实现，但是发布的预训练模型非常重要，因为它需要的计算力太多。总体而言，谷歌开放了预训练的 BERT-Base 和 BERT-Large 模型，且每一种模型都有 Uncased 和 Cased 两种版本。
    > 
    > 其中 Uncased 在使用 WordPiece 分词之前都转换为小写格式，并剔除所有 Accent Marker，而 Cased 会保留它们。项目作者表示一般使用 Uncased 模型就可以了，除非大小写对于任务很重要才会使用 Cased 版本。所有预训练模型及其地址如下：
    > 
    > -   BERT-Base, Uncased：12-layer, 768-hidden, 12-heads, 110M parameters
    > 
    > -   地址：https://storage.googleapis.com/bert_models/2018_10_18/uncased_L-12_H-768_A-12.zip
    > 
    > -   BERT-Large, Uncased：24-layer, 1024-hidden, 16-heads, 340M parameters
    > 
    > -   地址：https://storage.googleapis.com/bert_models/2018_10_18/uncased_L-24_H-1024_A-16.zip
    > 
    > -   BERT-Base, Cased：12-layer, 768-hidden, 12-heads , 110M parameters
    > 
    > -   地址：https://storage.googleapis.com/bert_models/2018_10_18/cased_L-12_H-768_A-12.zip
    > 
    > -   BERT-Large, Cased：24-layer, 1024-hidden, 16-heads, 340M parameters（目前无法使用，需要重新生成）。
    > 
    > 每一个 ZIP 文件都包含了三部分，即保存预训练模型与权重的 ckpt 文件、将 WordPiece 映射到单词 id 的 vocab 文件，以及指定模型超参数的 json 文件。除此之外，谷歌还发布了原论文中将预训练模型应用于各种 NLP 任务的源代码，感兴趣的读者可以查看 GitHub 项目复现论文结果。
    > 
    > BERT 官方项目地址：https://github.com/google-research/bert
    > 
    > 最后，这个项目可以在 CPU、GPU 和 TPU 上运行，但是在有 12GB 到 16GB 显存的 GPU 上，很可能模型会发生显存不足的问题。因此读者也可以在 Colab 先试着使用 BERT，如下展示了在 Colab 上使用免费 TPU 微调 BERT 的 Notebook：
    > 
    > BERT Colab 地址：https://colab.sandbox.google.com/github/tensorflow/tpu/blob/master/tools/colab/bert_finetuning_with_cloud_tpus.ipynb
    > 
    > **2 Transformer 概览**
    > 
    > 在整个 Transformer 架构中，它只使用了注意力机制和全连接层来处理文本，因此 Transformer 确实没使用循环神经网络或卷积神经网络实现「特征抽取」这一功能。此外，Transformer 中最重要的就是自注意力机制，这种在序列内部执行 Attention 的方法可以视为搜索序列内部的隐藏关系，这种内部关系对于翻译以及序列任务的性能有显著提升。
    > 
    > 如 Seq2Seq 一样，原版 Transformer 也采用了编码器-解码器框架，但它们会使用多个 Multi-Head Attention、前馈网络、层级归一化和残差连接等。下图从左到右展示了原论文所提出的 Transformer 架构、Multi-Head Attention 和点乘注意力。本文只简要介绍这三部分的基本概念与结构，更详细的 Transformer 解释与实现请查看机器之心的 GitHub 项目：[基于注意力机制，机器之心带你理解与训练神经机器翻译系统 。](http://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650742155&idx=1&sn=137825a13a4c31fffb6b2347c0304366&chksm=871ad9f5b06d50e31e2857a08a4a9ae9f57fd0191be580952d80f1518779594670cccc903fbe&scene=21#wechat_redirect)
    > 
    > 其中点乘注意力是注意力机制的一般表达形式，将多个点乘注意力叠加在一起可以组成 Transformer 中最重要的 Multi-Head Attention 模块，多个 Multi-Head Attention 模块堆叠在一起就组成了 Transformer 的主体结构，并借此抽取文本中的信息。
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_jpg/KmXPKA19gWic47IIJQyYPAkhp2zklbF30RD6uEtb4zf9VZn9zug4Fm54m9v4mlgCNB8HdgficHTsxHkwxk6svA5g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
    > 
    > *改编自论文《Attention is all your need》。*
    > 
    > 上图右边的点乘注意力其实就是标准 Seq2Seq 模型中的注意力机制。其中 Query 向量与 Value 向量在 NMT 中相当于目标语输入序列与源语输入序列，Query 与 Key 向量的点乘相当于余弦相似性，经过 SoftMax 函数后可得出一组归一化的概率。这些概率相当于给源语输入序列做加权平均，即表示在生成一个目标语单词时源语序列中哪些词是重要的。
    > 
    > 上图中间的 Multi-head Attention 其实就是多个点乘注意力并行处理并将最后的结果拼接在一起。这种注意力允许模型联合关注不同位置的不同表征子空间信息，我们可以理解为在参数不共享的情况下，多次执行点乘注意力。
    > 
    > 最后上图左侧为 Transformer 的整体架构。输入序列首先会转换为词嵌入向量，在与位置编码向量相加后可作为 Multi-Head 自注意力模块的输入，自注意力模块表示 Q、V、K 三个矩阵都是相同的。该模块的输出再经过一个全连接层就可以作为编码器模块的输出。
    > 
    > 原版 Transformer 的解码器与编码器结构基本一致，只不过在根据前面译文预测当前译文时会用到编码器输出的原语信息。在 BERT 论文中，研究者表示他们只需要使用编码器抽取文本信息，因此相对于原版架构只需要使用编码器模块。
    > 
    > 在模型架构上，BERT 使用了非常深的网络，原版 Transformer 只堆叠了 6 个编码器解码器模块，即上图的 N=6。而 BERT 基础模型使用了 12 个编码器模块（N=12），BERT 大模型堆叠了 24 个编码器模块（N=24）。其中堆叠了 6 个模块的 BERT 基础模型主要是为了和 OpenAI GPT 进行对比。
    > 
    > **3 BERT 论文解读**
    > 
    > BERT 的全称是基于 Transformer 的双向编码器表征，其中「双向」表示模型在处理某一个词时，它能同时利用前面的词和后面的词两部分信息。这种「双向」的来源在于 BERT 与传统语言模型不同，它不是在给定所有前面词的条件下预测最可能的当前词，而是随机遮掩一些词，并利用所有没被遮掩的词进行预测。下图展示了三种预训练模型，其中 BERT 和 ELMo 都使用双向信息，OpenAI GPT 使用单向信息。
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWic47IIJQyYPAkhp2zklbF30NgPDic9o1xJyCkEK7Vs1yUcelBYggG1oSeLqdNYOq7dtqaT3LJlvMPA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
    > 
    > *图：选自《BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding》。*
    > 
    > 如上所示为不同预训练模型的架构，BERT 可以视为结合了 OpenAI GPT 和 ELMo 优势的新模型。其中 ELMo 使用两条独立训练的 LSTM 获取双向信息，而 OpenAI GPT 使用新型的 Transformer 和经典语言模型只能获取单向信息。BERT 的主要目标是在 OpenAI GPT 的基础上对预训练任务做一些改进，以同时利用 Transformer 深度模型与双向信息的优势。
    > 
    > **输入表征**
    > 
    > 前面已经了解过 BERT 最核心的过程就是同时预测加了 MASK 的缺失词与 A/B 句之间的二元关系，而这些首先都需要体现在模型的输入中，在 Jacob 等研究者的原论文中，有一张图很好地展示了模型输入的结构。
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWic47IIJQyYPAkhp2zklbF30RrGWuQfzVnm7tTOffZ933ES4cCz7FSZ9CJtlHPYxDGQg853oAPtkaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
    > 
    > *图：选自《BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding》。*
    > 
    > 如上所示，输入有 A 句「my dog is cute」和 B 句「he likes playing」这两个自然句，我们首先需要将每个单词及特殊符号都转化为词嵌入向量，因为神经网络只能进行数值计算。其中特殊符 [SEP] 是用于分割两个句子的符号，前面半句会加上分割编码 A，后半句会加上分割编码 B。
    > 
    > 因为要建模句子之间的关系，BERT 有一个任务是预测 B 句是不是 A 句后面的一句话，而这个分类任务会借助 A/B 句最前面的特殊符 [CLS] 实现，该特殊符可以视为汇集了整个输入序列的表征。
    > 
    > 最后的位置编码是 Transformer 架构本身决定的，因为基于完全注意力的方法并不能像 CNN 或 RNN 那样编码词与词之间的位置关系，但是正因为这种属性才能无视距离长短建模两个词之间的关系。因此为了令 Transformer 感知词与词之间的位置关系，我们需要使用位置编码给每个词加上位置信息。
    > 
    > **预训练过程**
    > 
    > BERT 最核心的就是预训练过程，这也是该论文的亮点所在。简单而言，模型会从数据集抽取两句话，其中 B 句有 50% 的概率是 A 句的下一句，然后将这两句话转化前面所示的输入表征。现在我们随机遮掩（Mask 掉）输入序列中 15% 的词，并要求 Transformer 预测这些被遮掩的词，以及 B 句是 A 句下一句的概率这两个任务。
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWic47IIJQyYPAkhp2zklbF30gRuiamvYHK1D8x3Y9I9O9reUfnPArLlgfIpYibTeukvBqYOG5osEVRHw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
    > 
    > 首先谷歌使用了 BooksCorpus（8 亿词量）和他们自己抽取的 Wikipedia（25 亿词量）数据集，每次迭代会抽取 256 个序列（A+B），一个序列的长度为小于等于 512 个「词」。因此 A 句加 B 句大概是 512 个词，每一个「句子」都是非常长的一段话，这和一般我们所说的句子是不一样的。这样算来，每次迭代模型都会处理 12.8 万词。
    > 
    > 对于二分类任务，在抽取一个序列（A+B）中，B 有 50% 的概率是 A 的下一句。如果是的话就会生成标注「IsNext」，不是的话就会生成标注「NotNext」，这些标注可以作为二元分类任务判断模型预测的凭证。
    > 
    > 对于 Mask 预测任务，首先整个序列会随机 Mask 掉 15% 的词，这里的 Mask 不只是简单地用「[MASK]」符号代替某些词，因为这会引起预训练与微调两阶段不是太匹配。所以谷歌在确定需要 Mask 掉的词后，80% 的情况下会直接替代为「[MASK]」，10% 的情况会替代为其它任意的词，最后 10% 的情况会保留原词。
    > 
    > -   原句：my dog is hairy
    > 
    > -   80%：my dog is [MASK]
    > 
    > -   10%：my dog is apple
    > 
    > -   10%：my dog is hairy
    > 
    > 注意最后 10% 保留原句是为了将表征偏向真实观察值，而另外 10% 用其它词替代原词并不会影响模型对语言的理解能力，因为它只占所有词的 1.5%（0.1 × 0.15）。此外，作者在论文中还表示因为每次只能预测 15% 的词，因此模型收敛比较慢。
    > 
    > **微调过程**
    > 
    > 最后预训练完模型，就要尝试把它们应用到各种 NLP 任务中，并进行简单的微调。不同的任务在微调上有一些差别，但 BERT 已经强大到能为大多数 NLP 任务提供高效的信息抽取功能。对于分类问题而言，例如预测 A/B 句是不是问答对、预测单句是不是语法正确等，它们可以直接利用特殊符 [CLS] 所输出的向量 C，即 P = softmax(C * W)，新任务只需要微调权重矩阵 W 就可以了。
    > 
    > 对于其它序列标注或生成任务，我们也可以使用 BERT 对应的输出信息作出预测，例如每一个时间步输出一个标注或词等。下图展示了 BERT 在 11 种任务中的微调方法，它们都只添加了一个额外的输出层。在下图中，Tok 表示不同的词、E 表示输入的嵌入向量、T_i 表示第 i 个词在经过 BERT 处理后输出的上下文向量。
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWic47IIJQyYPAkhp2zklbF30rQgSbll9SHCM5pcuuCdPvy1seFBkZMy3c531OuzNJAC0BnibLKgr1JQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
    > 
    > *图：选自《BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding》。*
    > 
    > 如上图所示，句子级的分类问题只需要使用对应 [CLS] 的 C 向量，例如（a）中判断问答对是不是包含正确回答的 QNLI、判断两句话有多少相似性的 STS-B 等，它们都用于处理句子之间的关系。句子级的分类还包含（b）中判语句中断情感趋向的 SST-2 和判断语法正确性的 CoLA 任务，它们都是处理句子内部的关系。
    > 
    > 在 SQuAD v1.1 问答数据集中，研究者将问题和包含回答的段落分别作为 A 句与 B 句，并输入到 BERT 中。通过 B 句的输出向量，模型能预测出正确答案的位置与长度。最后在命名实体识别数据集 CoNLL 中，每一个 Tok 对应的输出向量 T 都会预测它的标注是什么，例如人物或地点等。
    > 
    > **4 官方模型详情**
    > 
    > 前面我们已经介绍过谷歌官方发布的 BERT 项目，这一部分主要会讨论如何在不同的 NLP 任务中微调预训练模型，以及怎样使用预训练 BERT 抽取文本的语义特征。此外，原项目还展示了 BERT 的预训练过程，但由于它需要的计算力太大，因此这里并不做介绍，读者可详细阅读原项目的说明文件。
    > 
    > 项目地址：https://github.com/google-research/bert
    > 
    > **微调预训练 BERT**
    > 
    > 该项目表示原论文中 11 项 NLP 任务的微调都是在单块 Cloud TPU（64GB RAM）上进行的，目前无法使用 12GB - 16GB 内存的 GPU 复现论文中 BERT-Large 模型的大部分结果，因为内存匹配的最大批大小仍然太小。但是基于给定的超参数，BERT-Base 模型在不同任务上的微调应该能够在一块 GPU（显存至少 12GB）上运行。
    > 
    > 这里主要介绍如何在句子级的分类任务以及标准问答数据集（SQuAD）微调 BERT-Base 模型，其中微调过程主要使用一块 GPU。而 BERT-Large 模型的微调读者可以参考原项目。
    > 
    > 
    > 
    > 
    > 以下为原项目中展示的句子级分类任务的微调，在运行该示例之前，你必须运行一个脚本下载GLUE data，并将它放置到目录\$GLUE_DIR。然后，下载预训练BERT-Base模型，解压缩后存储到目录\$BERT_BASE_DIR。
    > 
    > GLUE data 脚本地址：https://gist.github.com/W4ngatang/60c2bdb54d156a41194446737ce03e2e
    > 
    > 该示例代码在Microsoft Research Paraphrase Corpus（MRPC）上对BERT-Base进行微调，该语料库仅包含3600个样本，在大多数GPU上该微调过程仅需几分钟。
    > 
    > ```shell
    > export BERT_BASE_DIR=/path/to/bert/uncased_L-12_H-768_A-12
    > export GLUE_DIR=/path/to/glue
    > python run_classifier.py \  
    >     --task_name=MRPC \  
    >     --do_train=true \  
    >     --do_eval=true \  
    >     --data_dir=$GLUE_DIR/MRPC \  
    >     --vocab_file=$BERT_BASE_DIR/vocab.txt \  
    >     --bert_config_file=$BERT_BASE_DIR/bert_config.json \  
    >     --init_checkpoint=$BERT_BASE_DIR/bert_model.ckpt \  
    >     --max_seq_length=128 \  
    >     --train_batch_size=32 \  
    >     --learning_rate=2e-5 \  
    >     --num_train_epochs=3.0 \  
    >     --output_dir=/tmp/mrpc_output/
    > ```
    > 
    > 
    > 输出如下：
    > 
    > ```shell
    > ***** Eval results *****  
    > eval_accuracy = 0.845588  
    > eval_loss = 0.505248  
    > global_step = 343  
    > loss = 0.505248
    > ```
    > 
    > 
    > 
    > 
    > 可以看到，开发集准确率是84.55%。类似MRPC这样的较小数据集在开发集准确率上方差较高，即使是从同样的预训练检查点开始运行。如果你重新运行多次（确保使用不同的output_dir），结果将在84%和88%之间。注意：你或许会看到信息"Running train on CPU."这只是表示模型不是运行在Cloud TPU上而已。
    > 
    > **通过预训练BERT抽取语义特征**
    > 
    > 对于原论文11项任务之外的试验，我们也可以通过预训练BERT抽取定长的语义特征向量。因为在特定案例中，与其端到端微调整个预训练模型，直接获取预训练上下文嵌入向量会更有效果，并且也可以缓解大多数内存不足问题。在这个过程中，每个输入token的上下文嵌入向量指预训练模型隐藏层生成的定长上下文表征。
    > 
    > 例如，我们可以使用脚本extract_features.py 抽取语义特征：
    > 
    > ```shell
    > # Sentence A and Sentence B are separated by the ||| delimiter.# For single sentence inputs, don't use the delimiter.echo 'Who was Jim Henson ? ||| Jim Henson was a puppeteer' > /tmp/input.txt
    > python extract_features.py \  
    >     --input_file=/tmp/input.txt \  
    >     --output_file=/tmp/output.jsonl \  
    >     --vocab_file=$BERT_BASE_DIR/vocab.txt \  
    >     --bert_config_file=$BERT_BASE_DIR/bert_config.json \  
    >     --init_checkpoint=$BERT_BASE_DIR/bert_model.ckpt \  
    >     --layers=-1,-2,-3,-4 \  
    >     --max_seq_length=128 \  
    >     --batch_size=8
    > ```
    > 
    > 上面的脚本会创建一个JSON文件（每行输入占一行），JSON文件包含layers指定的每个Transformer层的BERT激活值（-1是Transformer的最后一个隐藏层）。注意这个脚本将生成非常大的输出文件，默认情况下每个输入token 会占据 15kb 左右的空间。
    > 
    > 最后，项目作者表示它们近期会解决GPU显存占用太多的问题，并且会发布多语言版的BERT预训练模型。他们表示只要在维基百科有比较大型的数据，那么他们就能提供预训练模型，因此我们还能期待下次谷歌发布基于中文语料的BERT预训练模型。


## 谷歌最强NLP模型BERT如约开源，12小时GitHub标星破1500，即将支持中文 

- [谷歌最强NLP模型BERT如约开源，12小时GitHub标星破1500，即将支持中文](https://mp.weixin.qq.com/s?__biz=MzIzNjc1NzUzMw==&mid=2247507210&idx=3&sn=ee69c35f118a1768ac04aa832b3e6186&chksm=e8d06a78dfa7e36e92ba4e14263389a76415a9e900a041ccf82c21655ed466e71a8353f519c7&mpshare=1&scene=24&srcid=#rd)

    > **使用BERT分为两步：预训练和微调。**
    > 
    > 预训练的代价非常高昂（需要4到16个云TPU训练4天），但是每种语言都是训练一次就够了。谷歌大脑团队发布了一些预训练的模型，目前仅限英语，但不久后也会发布多语言模型。大多数NLP研究人员根本不需要从头开始训练他们自己的模型。
    > 
    > 与预训练不同，微调则比较容易。从完全相同的预训练模型开始，本文中的所有结果只需最多在单个云TPU上运行1小时，或者在GPU上运行几小时。例如，目前最先进的单系统SQuAD，在单个云TPU上训练大约30分钟，就能获得91.0％的Dev F1分数。
    > 
    > BERT的另一个重要特性是，它能适应许多类型的NLP任务。它的论文里就展示了句子级别（如SST-2），句对级别（如MultiNLI），单词级别（如NER）和小段级别（如SQuAD）的最新结果，几乎没有针对特定任务进行修改。
    > 
    > 支持汉语吗？
    > ======
    > 
    > 目前放出的预训练模型是英语的，不过，谷歌大脑团队打算11月底之前放出经更多语言预训练的多语种模型。
    > 
    > 更多语言究竟包括哪些？官方没有给出准确信息，不过BERT一作Jacob Devlin回应排队求中日韩德甚至马其顿语版本的群众们时说，他正在用维基百科规模最大的60种语言训练模型，汉语、韩语、日语、德语、西班牙语等等都包含在其中。
    > 
    > 就是这里列出的1-60号语言：
    > 
    > https://meta.wikimedia.org/wiki/List_of_Wikipedias#All_Wikipedias_ordered_by_number_of_articles
    > 
    > 另外，他们对中文做了一点比较特殊的处理，就是把CJK Unicode字符集里的所有字符token化。
    > 
    > 项目库中发布了哪些内容？
    > ============
    > 
    > -   用于BERT模型架构的TensorFlow代码（主要是标准的Transformer架构）。
    > 
    > -   BERT-Base和BERT-Large模型小写和Cased版本的预训练检查点。
    > 
    > -   论文里微调试验的TensorFlow代码，比如SQuAD，MultiNLI和MRPC。\
    >     此项目库中的所有代码都可以直接用在CPU，GPU和云TPU上。
    > 
    > 预训练模型
    > =====
    > 
    > 这里发布的是论文中的BERT-Base和BERT-Large模型。\
    > 其中，Uncased的意思是，文本在经过WordPiece token化之前，全部会调整成小写，比如"John Smith"会变成"john smith"。Uncased模型也会剔除任何的重音标记。Cased意味着，文本的真实情况和重音标记都会保留下来。
    > 
    > 通常情况下，Uncased模型更好，除非文本的原始信息会对你的任务来说非常重要。比如说，识别命名实体或对部分语音标记。
    > 
    > 这些模型与源代码（Apache 2.0）的授权相同。
    > 
    > 在下面的模型介绍中，沿袭论文中的简称：层数（即 Transformer 块）表示为L，将隐藏尺寸表示为H，将自注意力头（self-attention heads）的数量表示为A。
    > 
    > 复制下方链接到浏览器中即可下载
    > 
    > BERT-Base, Uncased：L=12，H=768，A=12，总参数=110M\
    > https://storage.googleapis.com/bert_models/2018_10_18/uncased_L-12_H-768_A-12.zip
    > 
    > BERT-Large, Uncased：L=24, H=1024, A=16, 总参数=340M\
    > https://storage.googleapis.com/bert_models/2018_10_18/uncased_L-24_H-1024_A-16.zip
    > 
    > BERT-Base, Cased：L=12，H=768，A=12，总参数=110M\
    > https://storage.googleapis.com/bert_models/2018_10_18/cased_L-12_H-768_A-12.zip
    > 
    > BERT-Large, Cased：L=24, H=1024, A=16, 总参数=340M\
    > https://storage.googleapis.com/bert_models/2018_10_18/cased_L-12_H-768_A-12.zip
    > 
    > 每个.zip文件，都包含3个东西：
    > 
    > 一个 TensorFlow检查点（bert_model.ckpt），一个vocab文件（vocab.txt）和一个配置文件（bert_config.json）。
    > 
    > 如果你想对这些预训练模型进行端到端的微调，参见这份具体操作：\
    > https://github.com/google-research/bert/blob/master/README.md#fine-tuning-with-bert
    > 
    > 使用 BERT 提取固定特征向量(如 ELMo)
    > ========================
    > 
    > 有时候，与对整个预训练模型进行端到端的微调相比，直接获得预训练模型的语境嵌入会更好一些。
    > 
    > 预训练模型的语境嵌入，是由预训练模型的隐藏层生成的每个token的固定语境表示。这应该能够减轻大部分内存不足的问题。
    > 
    > 比如，脚本extract_features.py，可以这样使用：
    > 
    > ```
    > # Sentence A and Sentence B are separated by the ||| delimiter.# For single sentence inputs, don't use the delimiter.echo 'Who was Jim Henson ? ||| Jim Henson was a puppeteer' > /tmp/input.txt
    > python extract_features.py \  
    >     --input_file=/tmp/input.txt \  
    >     --output_file=/tmp/output.jsonl \  
    >     --vocab_file=$BERT_BASE_DIR/vocab.txt \  
    >     --bert_config_file=$BERT_BASE_DIR/bert_config.json \  
    >     --init_checkpoint=$BERT_BASE_DIR/bert_model.ckpt \  
    >     --layers=-1,-2,-3,-4 \  
    >     --max_seq_length=128 \  
    >     --batch_size=8
    > ```
    > 
    > 这将创建一个 JSON 文件（每行输入一行），包含由layers指定的每个Transformer层的BERT 激活（-1是Transformer的最后隐藏层，等等）\
    > 请注意，这个脚本将产生非常大的输出文件，默认情况下，每个输入token产生大约15kb输出。
    > 
    > 如果你预测训练标签，需要保持原始词汇和token词之间的一致性。具体请参阅下面的Token化部分。
    > 
    > Token化
    > ------
    > 
    > 对于句子层级的任务，token化非常简单。按照run_classifier.py和extract_features.py中的代码运行就行了。句子层级任务的基本流程是：
    > 
    > 1.  实例化。tokenizer = tokenization.FullTokenizer
    > 
    > 2.  将原始文本token化。tokens = tokenizer.tokenize(raw_text).
    > 
    > 3.  截断句子长度。（最大序列你最多可以使用512，但因为内存和速度的原因，短一点可能会更好）
    > 
    > 4.  在正确的位置添加[ CLS ]和[ SEP ]token。
    > 
    > [ CLS ]是分类输出的特殊符号，[ SEP ]是分离非连续token序列的特殊符号。
    > 
    > 单词级别和跨度级别的任务（例如SQuAD 和 NER）更为复杂，因为你需要保证输入文本和输出文本之间对齐，以便你能够映射训练标签。
    > 
    > SQuAD是一个非常复杂的例子，因为输入的标签是基于字符的，而且段落的长度也经常会超过默认的最大序列。查看run_squad.py中的代码， 可以看到Google是如何处理这个问题的。
    > 
    > 在介绍处理单词级别任务的通用方法之前，了解分词器（tokenizers）到底在做什么非常重要。它主要有三个步骤：
    > 
    > 1.  文本标准化：将所有的空白字符转换为空格，在Uncased模型中，要将所有字母小写，并剔除重音标记。例如：John Johanson's, → john johanson's,
    > 
    > 2.  标点符号分离：把标点符号分为两个部分，也就是说，在所有的标点符号字符周围添加空格。标点符号的定义是： (a)任何具有 p * Unicode 类的东西，(b)任何非字母 / 数字 / 空格 ASCII 字符，例如 $这样的字符，技术上不是标点符号。例如：john johanson's, → john johanson ' s ,
    > 
    > 3.  WordPiece token化：将空白token化，应用到上述过程的输出中，并对每个token分别应用WordPiece。（这个实现直接基于 tensor2tensor）。例如：john johanson ' s , → john johan ##son ' s ,
    > 
    > 这个方案的优点在于，它与大多数英语分词器兼容。例如，假设你有一个类似这样的标记部分语音任务：
    > 
    > ```
    > Input: John Johanson 's houseLabels: NNP NNP POS NN
    > ```
    > 
    > 所有的token化输出都是这样的：
    > 
    > ```
    > Tokens: john johan ##son ' s house
    > ```
    > 
    > 至关重要的是，这与输入John Johanson's house的输出是一样的，在'之前也没有空格。
    > 
    > 如果你有一个带有单词级别注释的预token化表示，你可以独立地对每个输入单词进行简单的分析，并确保原始文本到token化文本之间是对齐的：
    > 
    > ```python
    > ### Input
    > orig_tokens = ["John", "Johanson", "'s",  "house"]
    > labels      = ["NNP",  "NNP",      "POS", "NN"]
    > ### Output
    > bert_tokens = []
    > # Token map will be an int -> int mapping between the `orig_tokens` index and
    > # the `bert_tokens` index.
    > orig_to_tok_map = []
    > tokenizer = tokenization.FullTokenizer(    
    >     vocab_file=vocab_file, do_lower_case=True)
    > bert_tokens.append("[CLS]")
    > for orig_token in orig_tokens:  
    >     orig_to_tok_map.append(len(bert_tokens))  
    >     bert_tokens.extend(tokenizer.tokenize(orig_token))
    > bert_tokens.append("[SEP]")
    > # bert_tokens == ["[CLS]", "john", "johan", "##son", "'", "s", "house", "[SEP]"]
    > # orig_to_tok_map == [1, 2, 4, 6]
    > ```
    > 
    > 现在，orig_to_tok_map能用来将labels映射到token化表示上。
    > 
    > 有一些常见的英语训练方案，会导致BERT的训练方式之间出现轻微的不匹配。
    > 
    > 例如，如果你输入的是缩写单词而且又分离开了，比如do n't，将会出现错误匹配。如果可能的话，你应该预先处理数据，将其转换为原始的文本。如果不处理，这种错误匹配也不是什么大问题。
    > 
    > 预训练BERT
    > =======
    > 
    > 如果你想自己预训练BERT，可以看看这份资源中在任意文本语料库上完成"masked LM"和"预测下一句"任务的代码。
    > 
    > 注意：这不是论文中的原始代码，但是同样能生成论文中所描述的预训练数据。原始代码是C++写成的，更复杂。
    > 
    > 首先是数据生成环节：输入每句一行的纯文本文件，用空行分隔文件，会得到一组TFRecord文件格式的tf.train.Example。
    > 
    > ```python
    > python create_pretraining_data.py \  
    >     --input_file=./sample_text.txt \  
    >     --output_file=/tmp/tf_examples.tfrecord \  
    >     --vocab_file=$BERT_BASE_DIR/vocab.txt \  
    >     --do_lower_case=True \  
    >     --max_seq_length=128 \  
    >     --max_predictions_per_seq=20 \  
    >     --masked_lm_prob=0.15 \  
    >     --random_seed=12345 \  
    >     --dupe_factor=5
    > ```
    > 
    > 这段脚本能把整个输入文件中的所有样例存储到内存，所以，如果输入文件比较大，你要把它分割开，多次调用这个脚本。
    > 
    > max_predictions_per_seq是每个序列能获得masked LM预测的最大值，应该设置到和max_seq_length乘masked_lm_prob差不多。
    > 
    > 数据生成之后就可以运行预训练了。
    > 
    > ```
    > python run_pretraining.py \  
    >     --input_file=/tmp/tf_examples.tfrecord \  
    >     --output_dir=/tmp/pretraining_output \  
    >     --do_train=True \  
    >     --do_eval=True \  
    >     --bert_config_file=$BERT_BASE_DIR/bert_config.json \  
    >     --init_checkpoint=$BERT_BASE_DIR/bert_model.ckpt \  
    >     --train_batch_size=32 \  
    >     --max_seq_length=128 \  
    >     --max_predictions_per_seq=20 \  
    >     --num_train_steps=20 \  
    >     --num_warmup_steps=10 \  
    >     --learning_rate=2e-5
    > ```
    > 
    > 注意，如果你要从头开始预训练的话，就去掉代码里的init_checkpoint。模型的设置在bert_config_file里。
    > 
    > 这段代码只能预训练20步左右，但实际使用中，你可能需要训练10000步以上，在num_train_steps这里设置数字就可以。
    > 
    > 另外，max_seq_length和max_predictions_per_seq传递给run_pretraining.py的参数，必须和create_pretraining_data.py.一样。
    > 
    > 得到的输出会是这样的：
    > 
    > ```
    > ***** Eval results *****  
    > global_step = 20  
    > loss = 0.0979674  
    > masked_lm_accuracy = 0.985479  
    > masked_lm_loss = 0.0979328  
    > next_sentence_accuracy = 1.0  
    > next_sentence_loss = 3.45724e-05
    > ```
    > 
    > **这里还有一些预训练注意事项：**
    > 
    > 如果你的任务有大型特定域语料库可用，比如电影评论、科研论文等等，则从BERT检查点开始，对语料库执行额外的预训练步骤可能会有用。
    > 
    > 论文中使用的学习率是1e-4。但是，如果你从现有BERT检查点开始执行额外的预训练步骤，则应使用较小的学习率（例如，2e-5）。
    > 
    > 现在BERT模型只支持英语，但是Google打算在"不久的将来"发布经过多种语言预训练的多语种模型。这个不久，他们希望是11月底之前。
    > 
    > 注意力是序列长度的平方，所以长序列非常昂贵（耗费计算力）。一批64个长度为512的序列，比一批256个长度为128的序列要昂贵的多，它们的全连接、卷积成本相同，但是512长度的序列注意力成本要高很多。
    > 
    > 不过有时候确实需要长序列，比如要学习位置嵌入的时候，用长序列就学得非常快。这时候，可以先用短序列（比如长度128）训练90000步，再用长序列（比如长度512）训练10000步。注意，这需要用不同的max_seq_length值生成两次数据。
    > 
    > 如果从头开始预训练，请注意：成本很高，在GPU上成本尤其高。Google推荐先用单个可抢占（preemptible）的云TPU v2，预训练BERT-Base。这需要两周时间，500美元，还需要缩小批次大小。
    > 
    > **预训练数据：**
    > 
    > 论文用的预处理数据集......Sorry，Google说不公布了。不过他们提供了一些让你自己搞定数据集的途径。
    > 
    > 如果想用维基百科，从这里下载：\
    > https://dumps.wikimedia.org/enwiki/latest/enwiki-latest-pages-articles.xml.bz2
    > 
    > 然后用WikiExtractor.py提取文本：\
    > https://github.com/attardi/wikiextractor
    > 
    > 然后进行必要的清理，转换成纯文本。
    > 
    > 如果想用BookCorpus数据集，它已经不提供开放下载了，可以用比较小的Project Guttenberg数据集替代：\
    > https://web.eecs.umich.edu/~lahiri/gutenberg_dataset.html
    > 
    > 还有一个大型文本资源，叫Common Crawl，也可以清理一下提取出预训练BERT要用的语料库：\
    > http://commoncrawl.org/
    > 
    > 在Colab里使用BERT
    > =============
    > 
    > Google还提供了更贴心的使用方式：在他们的Colab（全称Colaboratory）里，打开这个名叫"BERT FineTuning with Cloud TPUs"的笔记本，就可以开工了：\
    > https://colab.research.google.com/github/tensorflow/tpu/blob/master/tools/colab/bert_finetuning_with_cloud_tpus.ipynb
    > 
    > 如果你想免费薅一把谷歌云TPU资源，现在Colab是个不错的途径。

## Bert 原理

- [【NLP】Google BERT详解 - 知乎](https://zhuanlan.zhihu.com/p/46652512)


    > Attention和Transformer还不熟悉的请移步之前的文章：
    > 
    > 1.  [【NLP】Attention原理和源码解析](https://zhuanlan.zhihu.com/p/43493999)
    > 
    > 2. [【NLP】Transformer详解](https://zhuanlan.zhihu.com/p/44121378)
    > 
    > NLP迁移学习中的三个state of the art模型可以参考前面的文章：
    > 
    > [【NLP】语言模型和迁移学习](https://zhuanlan.zhihu.com/p/42618178)
    > 
    > 正文分割线
    > 
    > **1.BERT模型**
    > ------------
    > 
    > BERT的全称是Bidirectional Encoder Representation from Transformers，即双向Transformer的Encoder，因为decoder是不能获要预测的信息的。模型的主要创新点都在pre-train方法上，即用了Masked LM和Next Sentence Prediction两种方法分别捕捉词语和句子级别的representation。
    > 
    > **1.1 模型结构**
    > ------------
    > 
    > 由于模型的构成元素Transformer已经解析过，就不多说了，BERT模型的结构如下图最左：
    > 
    > ![](https://pic1.zhimg.com/80/v2-d942b566bde7c44704b7d03a1b596c0c_hd.jpg)
    > 
    > 对比OpenAI GPT(Generative pre-trained transformer)，BERT是双向的Transformer block连接；就像单向rnn和双向rnn的区别，直觉上来讲效果会好一些。
    > 
    > 对比ELMo，虽然都是"双向"，但目标函数其实是不同的。ELMo是分别以![P(w_i| w_1, ...w_{i-1})](http://www.zhihu.com/equation?tex=P%28w_i%7C+w_1%2C+...w_%7Bi-1%7D%29) 和 ![P(w_i|w_{i+1}, ...w_n)](http://www.zhihu.com/equation?tex=P%28w_i%7Cw_%7Bi%2B1%7D%2C+...w_n%29) 作为目标函数，独立训练处两个representation然后拼接，而BERT则是以 ![P(w_i|w_1,  ...,w_{i-1}, w_{i+1},...,w_n)](http://www.zhihu.com/equation?tex=P%28w_i%7Cw_1%2C++...%2Cw_%7Bi-1%7D%2C+w_%7Bi%2B1%7D%2C...%2Cw_n%29) 作为目标函数训练LM。
    > 
    > **1.2 Embedding**
    > -----------------
    > 
    > 这里的Embedding由三种Embedding求和而成：
    > 
    > ![](https://pic2.zhimg.com/80/v2-11505b394299037e999d12997e9d1789_hd.jpg)
    > 
    > 其中：
    > 
    > -   Token Embeddings是词向量，第一个单词是CLS标志，可以用于之后的分类任务
    > -   Segment Embeddings用来区别两种句子，因为预训练不光做LM还要做以两个句子为输入的分类任务
    > -   Position Embeddings和之前文章中的Transformer不一样，不是三角函数而是学习出来的
    > 
    > **1.3 Pre-training Task 1#: Masked LM**
    > ---------------------------------------
    > 
    > 第一步预训练的目标就是做语言模型，从上文模型结构中看到了这个模型的不同，即bidirectional。**关于为什么要如此的bidirectional**，作者在[reddit](http://link.zhihu.com/?target=http%3A//www.reddit.com/r/MachineLearning/comments/9nfqxz/r_bert_pretraining_of_deep_bidirectional/)上做了解释，意思就是如果使用预训练模型处理其他任务，那人们想要的肯定不止某个词左边的信息，而是左右两边的信息。而考虑到这点的模型ELMo只是将left-to-right和right-to-left分别训练拼接起来。直觉上来讲我们其实想要一个deeply bidirectional的模型，但是普通的LM又无法做到，因为在训练时可能会"穿越"（**关于这点我不是很认同，之后会发文章讲一下如何做bidirectional LM**）。所以作者用了一个加mask的trick。
    > 
    > 在训练过程中作者随机mask 15%的token，而不是把像cbow一样把每个词都预测一遍。**关于为什么这样做，我觉得可能是模型结构本身的原因，从结构上看输入输出是长度一样的sequence，这样模型实际上在做sequence-level的LM。**
    > 
    > Mask如何做也是有技巧的，如果一直用标记[MASK]代替（在实际预测时是碰不到这个标记的）会影响模型，所以随机mask的时候10%的单词会被替代成其他单词，10%的单词不替换，剩下80%才被替换为[MASK]。具体为什么这么分配，作者没有说。。。要注意的是Masked LM预训练阶段模型是不知道真正被mask的是哪个词，所以模型每个词都要关注。
    > 
    > **1.4 Pre-training Task 2#: Next Sentence Prediction**
    > ------------------------------------------------------
    > 
    > 因为涉及到QA和NLI之类的任务，增加了第二个预训练任务，目的是让模型理解两个句子之间的联系。训练的输入是句子A和B，B有一半的几率是A的下一句，输入这两个句子，模型预测B是不是A的下一句。预训练的时候可以达到97-98%的准确度。
    > 
    > **1.5 Fine-tunning**
    > --------------------
    > 
    > 分类：对于sequence-level的分类任务，BERT直接取第一个[CLS]token的final hidden state ![C\in\Re^H](http://www.zhihu.com/equation?tex=C%5Cin%5CRe%5EH) ，加一层权重 ![W\in\Re^{K\times H}](http://www.zhihu.com/equation?tex=W%5Cin%5CRe%5E%7BK%5Ctimes+H%7D) 后softmax预测label proba： ![P=softmax(CW^T) \\](http://www.zhihu.com/equation?tex=P%3Dsoftmax%28CW%5ET%29+%5C%5C)
    > 
    > 其他预测任务需要进行一些调整，如图：
    > 
    > ![](https://pic2.zhimg.com/80/v2-b054e303cdafa0ce41ad761d5d0314e1_hd.jpg)
    > 
    > 因为大部分参数都和预训练时一样，精调会快一些，所以作者推荐多试一些参数。
    > 
    > **2\. 优缺点**
    > -----------
    > 
    > **2.1 优点**
    > ----------
    > 
    > BERT是截至2018年10月的最新state of the art模型，通过预训练和精调横扫了11项NLP任务，这首先就是最大的优点了。而且它还用的是Transformer，也就是相对rnn更加高效、能捕捉更长距离的依赖。对比起之前的预训练模型，它捕捉到的是真正意义上的bidirectional context信息。
    > 
    > **2.2 缺点**
    > ----------
    > 
    > 作者在文中主要提到的就是MLM预训练时的mask问题：
    > 
    > 1.  [MASK]标记在实际预测中不会出现，训练时用过多[MASK]影响模型表现
    > 2.  每个batch只有15%的token被预测，所以BERT收敛得比left-to-right模型要慢（它们会预测每个token）
    > 
    > **3\. 总结**
    > ----------
    > 
    > 一遍读下来，感觉用到的都是现有的东西，可没想到效果会这么好，而别人又没想到。不过文章中没有具体解释的很多点可以看出这样出色的结果也是通过不断地实验得出的，而且训练的数据也比差不多结构的OpenAI GPT多，所以数据、模型结构，都是不可或缺的东西。
    > 
    > 以上。
    > 
    > 【参考资料】：
    > 
    > 1.  [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](http://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1810.04805.pdf)
    > 2.  [全面超越人类！Google称霸SQuAD，BERT横扫11大NLP测试](https://zhuanlan.zhihu.com/p/46648916)
    > 3.  [知乎：如何评价BERT模型？](https://www.zhihu.com/question/298203515?from=timeline&isappinstalled=0&utm_medium=social&utm_source=wechat_session)
    > 

## Attention 原理

- [【NLP】Attention原理和源码解析 - 知乎](https://zhuanlan.zhihu.com/p/43493999)


    > 1\. 核心思想
    > --------
    > 
    > Attention的思想理解起来比较容易，就是在decoding阶段对input中的信息赋予不同权重。在nlp中就是针对sequence的每个time step input，在cv中就是针对每个pixel。
    > 
    > 2\. 原理解析
    > --------
    > 
    > 针对Seq2seq翻译来说，rnn-based model差不多是图1的样子：
    > 
    > ![](https://pic1.zhimg.com/80/v2-e258d6cd046c0567ad72a8fe930807cc_hd.jpg)
    > 
    > 图1 传统rnn-based model
    > 
    > 而比较基础的加入attention与rnn结合的model是下面的样子（也叫soft attention）：
    > 
    > ![](https://pic4.zhimg.com/80/v2-5a509cc5d422b5d83006f41738dd7b43_hd.jpg)
    > 
    > ![](https://pic4.zhimg.com/80/v2-f0a7c907fca9301a628ac3a5bfe04ac7_hd.jpg)
    > 
    > 其中 ![\alpha_{0}^1](http://www.zhihu.com/equation?tex=%5Calpha_%7B0%7D%5E1) 是 ![h_{0}^1](http://www.zhihu.com/equation?tex=h_%7B0%7D%5E1) 对应的权重，算出所有权重后会进行softmax和加权，得到 ![c^0](http://www.zhihu.com/equation?tex=c%5E0) 。
    > 
    > 可以看到Encoding和decoding阶段仍然是rnn，但是decoding阶使用attention的输出结果 ![c^0, c^1](http://www.zhihu.com/equation?tex=c%5E0%2C+c%5E1) 作为rnn的输入。
    > 
    > **那么重点来了， 权重 ![\alpha](http://www.zhihu.com/equation?tex=%5Calpha) 是怎么来的呢？常见有三种方法：**
    > 
    > -   ![\alpha_{0}^1=cos\_sim(z_0, h_1)](http://www.zhihu.com/equation?tex=%5Calpha_%7B0%7D%5E1%3Dcos%5C_sim%28z_0%2C+h_1%29)
    > -   ![\alpha_0 =neural\_network(z_0, h)](http://www.zhihu.com/equation?tex=%5Calpha_0+%3Dneural%5C_network%28z_0%2C+h%29)
    > -   ![\alpha_0 = h^TWz_0](http://www.zhihu.com/equation?tex=%5Calpha_0+%3D+h%5ETWz_0)
    > 
    > 思想就是根据当前解码"状态"判断输入序列的权重分布。
    > 
    > 如果把attention剥离出来去看的话，其实是以下的机制：
    > 
    > ![](https://pic3.zhimg.com/80/v2-99839119705a82a807409d104f63e88a_hd.jpg)
    > 
    > 输入是query(Q), key(K), value(V)，输出是attention value。如果与之前的模型对应起来的话，query就是 ![z_0, z_1](http://www.zhihu.com/equation?tex=z_0%2C+z_1) ，key就是 ![h_1, h_2, h_3, h_4](http://www.zhihu.com/equation?tex=h_1%2C+h_2%2C+h_3%2C+h_4) ，value也是![h_1, h_2, h_3, h_4](http://www.zhihu.com/equation?tex=h_1%2C+h_2%2C+h_3%2C+h_4)。模型通过Q和K的匹配计算出权重，再结合V得到输出：
    > 
    > ![Attention(Q, K, V) = softmax(sim(Q, K))V \\](http://www.zhihu.com/equation?tex=Attention%28Q%2C+K%2C+V%29+%3D+softmax%28sim%28Q%2C+K%29%29V+%5C%5C)
    > 
    > 再深入理解下去，这种机制其实做的是寻址（addressing），也就是模仿中央处理器与存储交互的方式将存储的内容读出来，可以看一下[李宏毅老师的课程](http://link.zhihu.com/?target=http%3A//speech.ee.ntu.edu.tw/%7Etlkagk/courses_MLSD15_2.html)。
    > 
    > 3\. 模型分类
    > --------
    > 
    > 3.1 Soft/Hard Attention
    > 
    > soft attention：传统attention，可被嵌入到模型中去进行训练并传播梯度
    > 
    > hard attention：不计算所有输出，依据概率对encoder的输出采样，在反向传播时需采用蒙特卡洛进行梯度估计
    > 
    > 3.2 Global/Local Attention
    > 
    > global attention：传统attention，对所有encoder输出进行计算
    > 
    > local attention：介于soft和hard之间，会预测一个位置并选取一个窗口进行计算
    > 
    > 3.3 Self Attention
    > 
    > 传统attention是计算Q和K之间的依赖关系，而self attention则分别计算Q和K自身的依赖关系。具体的详解会在下篇文章给出~
    > 
    > 4\. 优缺点
    > -------
    > 
    > 优点：
    > 
    > -   在输出序列与输入序列"顺序"不同的情况下表现较好，如翻译、阅读理解
    > -   相比RNN可以编码更长的序列信息
    > 
    > 缺点：
    > 
    > -   对序列顺序不敏感
    > -   通常和RNN结合使用，不能并行化
    > 
    > 5\. TF源码解析
    > ----------
    > 
    > 发现已经有人解析得很明白了，即使TF代码有更新，原理应该还是差不多的，直接放上来吧：
    > 
    > [顾秀森：Tensorflow源码解读（一）：AttentionSeq2Seq模型​](https://zhuanlan.zhihu.com/p/27769667)[zhuanlan.zhihu.com![图标](https://pic3.zhimg.com/v2-2716e5d0b5024a7de923191e440421d6_180x120.jpg)](https://zhuanlan.zhihu.com/p/27769667)
    > 
    > 【参考资料】：
    > 
    > 1.  [李宏毅老师的课程](http://link.zhihu.com/?target=http%3A//speech.ee.ntu.edu.tw/%7Etlkagk/courses_MLSD15_2.html)
    > 2.  [知乎：目前主流的attention方法都有哪些？](https://www.zhihu.com/question/68482809/answer/268266647)
    > 3.  [模型汇总24 - 深度学习中Attention Mechanism详细介绍：原理、分类及应用](https://zhuanlan.zhihu.com/p/31547842)
    > 
    > 

## Attention 實作

- [Tensorflow源码解读（一）：Attention Seq2Seq模型 - 知乎](https://zhuanlan.zhihu.com/p/27769667)

    > Seq2Seq模型是机器翻译，对话生成等任务里经典的模型，attention机制也是在2016年刷爆了各种NLP任务，这两者都是很值得深入研究掌握的模型。本文要分享的是Tensorflow官方例子，翻译模型里的embedding_attention_seq2seq函数源码解读。文章参考了另一篇博客[1]和官方github源码，attention部分的公式和推导涉及了源码参考的论文[2]。
    > 
    > **tf.nn.seq2seq**文件共实现了5个seq2seq函数，因为本文重点讲解最后一个，所以前4个简要介绍一下。
    > 
    > -   basic_rnn_seq2seq：最简单版本，输入和输出都是embedding的形式；最后一步的state vector作为decoder的initial state；encoder和decoder用相同的RNN cell， 但不共享权值参数；
    > -   tied_rnn_seq2seq：同1，但是encoder和decoder共享权值参数
    > -   embedding_rnn_seq2seq：同1，但输入和输出改为id的形式，函数会在内部创建分别用于encoder和decoder的embedding matrix
    > -   embedding_tied_rnn_seq2seq：同2，但输入和输出改为id形式，函数会在内部创建分别用于encoder和decoder的embedding matrix
    > -   embedding_attention_seq2seq：同3，但多了attention机制
    > 
    > 下面进入正题！
    > 
    > **tf.nn.seq2seq.embedding_attention_seq2seq**
    > ---------------------------------------------
    > 
    > ```
    > # T代表time_steps, 时序长度
    > def embedding_attention_seq2seq(encoder_inputs,  # [T, batch_size]
    >                                 decoder_inputs,  # [T, batch_size]
    >                                 cell,
    >                                 num_encoder_symbols,
    >                                 num_decoder_symbols,
    >                                 embedding_size,
    >                                 num_heads=1,      # attention的抽头数量
    >                                 output_projection=None, #decoder的投影矩阵
    >                                 feed_previous=False,
    >                                 dtype=None,
    >                                 scope=None,
    >                                 initial_state_attention=False):
    > 
    > ```
    > 
    > 参数
    > --
    > 
    > **Input**
    > 
    > -   encoder_inputs：encoder的输入，int32型 id tensor list
    > -   decoder_inputs：decoder的输入，int32型id tensor list
    > -   cell： RNN_Cell的实例
    > -   num_encoder_symbols, num_decoder_symbols： 分别是编码和解码的符号数，即词表大小
    > -   embedding_size： 词向量的维度
    > -   num_heads：attention的抽头数量，一个抽头算一种加权求和方式，后面会进一步介绍
    > -   output_projection：decoder的output向量投影到词表空间时，用到的投影矩阵和偏置项(W, B)；W的shape是[output_size, num_decoder_symbols]，B的shape是[num_decoder_symbols]；若此参数存在且feed_previous=True，上一个decoder的输出先乘W再加上B作为下一个decoder的输入
    > -   feed_previous：若为True, 只有第一个decoder的输入（"GO"符号）有用，所有的decoder输入都依赖于上一步的输出；一般在测试时用（当然源码也提到，可以在训练时用于模拟测试的环境，比如**Scheduled Sampling**）
    > -   initial_state_attention: 默认为False, 初始的attention是零；若为True，将从initial state和attention states开始attention
    > 
    > **Output**
    > 
    > -   (outputs, state) tuple pair，outputs是 2D Tensors list, 每个Tensor的shape是[batch_size, cell.state_size]；state是 最后一个时间步，decoder cell的state，shape是[batch_size, cell.state_size]
    > 
    > **Encoder**
    > 
    > -   创建了一个embedding matrix.
    > -   计算encoder的output和state
    > -   生成attention states，用于计算attention
    > 
    > ```
    > encoder_cell = rnn_cell.EmbeddingWrapper(
    >         cell, embedding_classes=num_encoder_symbols,
    >         embedding_size=embedding_size)
    >     encoder_outputs, encoder_state = rnn.rnn(
    >         encoder_cell, encoder_inputs, dtype=dtype) #  [T，batch_size，size]
    > 
    >     top_states = [array_ops.reshape(e, [-1, 1, cell.output_size])
    >                   for e in encoder_outputs]    # T * [batch_size, 1, size]
    >     attention_states = array_ops.concat(1, top_states) # [batch_size,T,size]
    > 
    > ```
    > 
    > 上面的**EmbeddingWrapper**, 是RNNCell的前面加一层embedding，作为encoder_cell, input就可以是word的id。
    > 
    > ```
    > class EmbeddingWrapper(RNNCell):
    >   def __init__(self, cell, embedding_classes, embedding_size, initializer=None):
    >   def __call__(self, inputs, state, scope=None):
    >   #生成embedding矩阵[embedding_classes,embedding_size]
    >   #inputs: [batch_size, 1]
    >   #return : (output, state)
    > 
    > ```
    > 
    > **Decoder**
    > 
    > -   生成decoder的cell，通过OutputProjectionWrapper类对输入参数中的cell实例包装实现
    > 
    > ```
    > # Decoder.
    >     output_size = None
    >     if output_projection is None:
    >       cell = rnn_cell.OutputProjectionWrapper(cell, num_decoder_symbols)
    >       output_size = num_decoder_symbols
    >     if isinstance(feed_previous, bool):
    >       return embedding_attention_decoder(
    >           ...
    >       )
    > 
    > ```
    > 
    > 上面的**OutputProjectionWrapper**将输出映射成想要的维度
    > 
    > ```
    > class OutputProjectionWrapper(RNNCell):
    >   def __init__(self, cell, output_size): # output_size:映射后的size
    >   def __call__(self, inputs, state, scope=None):
    >   #init 返回一个带output projection的 rnn_cell
    > 
    > ```
    > 
    > 接着对embedding_attention_decoder一探究竟：
    > 
    > ```
    > def embedding_attention_decoder(decoder_inputs,
    >                                 initial_state,
    >                                 attention_states,
    >                                 cell,
    >                                 num_symbols,
    >                                 embedding_size,
    >                                 num_heads=1,
    >                                 output_size=None,
    >                                 output_projection=None,
    >                                 feed_previous=False,
    >                                 update_embedding_for_previous=True,
    >                                 dtype=None,
    >                                 scope=None,
    >                                 initial_state_attention=False):
    > # 核心代码
    >     embedding = variable_scope.get_variable("embedding",
    >                                             [num_symbols, embedding_size])
    >     loop_function = _extract_argmax_and_embed(
    >         embedding, output_projection,
    >         update_embedding_for_previous) if feed_previous else None
    >     emb_inp = [
    >         embedding_ops.embedding_lookup(embedding, i) for i in decoder_inputs]
    >     # T * [batch_size, embedding_size]
    >     return attention_decoder(
    >         emb_inp,
    >         initial_state,
    >         attention_states,
    >         cell,
    >         output_size=output_size,
    >         num_heads=num_heads,
    >         loop_function=loop_function,
    >         initial_state_attention=initial_state_attention)
    > 
    > ```
    > 
    > 简要的说，embedding_attention_decoder的代码，第一步创建了解码用的embedding； 第二步创建了一个循环函数loop_function，用于将上一步的输出映射到词表空间，输出一个word embedding作为下一步的输入；最后是我们最关注的**attention_decoder**部分完成解码工作！
    > 
    > tf.nn.attention_decoder
    > -----------------------
    > 
    > 论文涉及三个公式：
    > 
    > ![](https://pic2.zhimg.com/80/v2-118c6e2c3b28a4ae3d0b9bf2cd42a49d_hd.png)
    > 
    > encoder输出的隐层状态![(h_{1},...,h_{T_{A}})](http://www.zhihu.com/equation?tex=%28h_%7B1%7D%2C...%2Ch_%7BT_%7BA%7D%7D%29)，decoder的隐层状态![(d_{1},...,d_{T_{B}})](http://www.zhihu.com/equation?tex=%28d_%7B1%7D%2C...%2Cd_%7BT_%7BB%7D%7D%29)。![v^{T}](http://www.zhihu.com/equation?tex=v%5E%7BT%7D)，![W^{'}_{1}](http://www.zhihu.com/equation?tex=W%5E%7B%27%7D_%7B1%7D)，![W^{'}_{2}](http://www.zhihu.com/equation?tex=W%5E%7B%27%7D_%7B2%7D)是模型要学的参数。**所谓的attention，就是在每个解码的时间步，对encoder的隐层状态进行加权求和，针对不同信息进行不同程度的注意力。**那么我们的重点就是求出不同隐层状态对应的权重。源码中的attention机制里是最常见的一种，可以分为三步走：（1）通过当前隐层状态(![d_{t}](http://www.zhihu.com/equation?tex=d_%7Bt%7D))和关注的隐层状态(![h_{i}](http://www.zhihu.com/equation?tex=h_%7Bi%7D))求出对应权重![u^{t}_{i}](http://www.zhihu.com/equation?tex=u%5E%7Bt%7D_%7Bi%7D)；（2）softmax归一化为概率；（3）作为加权系数对不同隐层状态求和，得到一个的信息向量![d^{'}_{t}](http://www.zhihu.com/equation?tex=d%5E%7B%27%7D_%7Bt%7D)。后续的![d^{'}_{t}](http://www.zhihu.com/equation?tex=d%5E%7B%27%7D_%7Bt%7D)使用会因为具体任务有所差别。
    > 
    > 上面的![a^{t}_{i}](http://www.zhihu.com/equation?tex=a%5E%7Bt%7D_%7Bi%7D)含义是第t个时间步，对![h_{i}](http://www.zhihu.com/equation?tex=h_%7Bi%7D)的加权系数。
    > 
    > 下面上代码的时刻！
    > 
    > ```
    > def attention_decoder(decoder_inputs,  #T * [batch_size, input_size]
    >                       initial_state,   #[batch_size, cell.states]
    >                       attention_states,#[batch_size, attn_length , attn_size]
    >                       cell,
    >                       output_size=None,
    >                       num_heads=1,
    >                       loop_function=None,
    >                       dtype=None,
    >                       scope=None,
    >                       initial_state_attention=False):
    > 
    > ```
    > 
    > 对于num_heads参数，还记得当初留的坑么：) 我们知道，attention就是对信息的加权求和，一个attention head对应了一种加权求和方式，这个参数定义了用多少个attention head去加权求和，所以公式三可以进一步表述为![\sum^{num\_heads}_{j=1}\sum^{T_{A}}_{i=1}a_{i,j}h_{i}](http://www.zhihu.com/equation?tex=%5Csum%5E%7Bnum%5C_heads%7D_%7Bj%3D1%7D%5Csum%5E%7BT_%7BA%7D%7D_%7Bi%3D1%7Da_%7Bi%2Cj%7Dh_%7Bi%7D)。
    > 
    > -   ![W_{1}*h_{i}](http://www.zhihu.com/equation?tex=W_%7B1%7D%2Ah_%7Bi%7D)用的是卷积的方式实现，返回的tensor的形状是[batch_size, attn_length, 1, attention_vec_size]
    > 
    > ```
    > # To calculate W1 * h_t we use a 1-by-1 convolution
    >     hidden = array_ops.reshape(
    >         attention_states, [-1, attn_length, 1, attn_size])
    >     hidden_features = []
    >     v = []
    >     attention_vec_size = attn_size  # Size of query vectors for attention.
    >     for a in xrange(num_heads):
    >       k = variable_scope.get_variable("AttnW_%d" % a,
    >                                       [1, 1, attn_size, attention_vec_size])
    >       hidden_features.append(nn_ops.conv2d(hidden, k, [1, 1, 1, 1], "SAME"))
    >       v.append(
    >           variable_scope.get_variable("AttnV_%d" % a, [attention_vec_size]))
    > 
    > ```
    > 
    > -   ![W_{2}*d_{t}](http://www.zhihu.com/equation?tex=W_%7B2%7D%2Ad_%7Bt%7D)，此项是通过下面的线性映射函数linear实现
    > 
    > ```
    > for a in xrange(num_heads):
    >         with variable_scope.variable_scope("Attention_%d" % a):
    >           # query对应当前隐层状态d_t
    >           y = linear(query, attention_vec_size, True)
    >           y = array_ops.reshape(y, [-1, 1, 1, attention_vec_size])
    >           # 计算u_t
    >           s = math_ops.reduce_sum(
    >               v[a] * math_ops.tanh(hidden_features[a] + y), [2, 3])
    >           a = nn_ops.softmax(s)
    >           # 计算 attention-weighted vector d.
    >           d = math_ops.reduce_sum(
    >               array_ops.reshape(a, [-1, attn_length, 1, 1]) * hidden,
    >               [1, 2])
    >           ds.append(array_ops.reshape(d, [-1, attn_size]))
    > 
    > ```
    > 
    > 到这里，embedding_attention_seq2seq的核心代码都已经解读完毕了。在实际的运用，可以根据需求灵活使用各个函数，特别是attention_decoder函数。相信坚持阅读下来的小伙伴们，能对这个API有更深刻的认识：)
    > 
    > 参考文献：
    > 
    > [1] [tensorflow学习笔记（十一）：seq2seq Model相关接口介绍](http://link.zhihu.com/?target=http%3A//blog.csdn.net/u012436149/article/details/52976413)
    > 
    > [2] Grammar as a Foreign Language


## Transformer 原理

- [【NLP】Transformer详解 - 知乎](https://zhuanlan.zhihu.com/p/44121378)

    > 传送门：[【NLP】Attention原理和源码解析](https://zhuanlan.zhihu.com/p/43493999)
    > 
    > 自Attention机制提出后，加入attention的Seq2seq模型在各个任务上都有了提升，所以现在的seq2seq模型指的都是结合rnn和attention的模型，具体原理可以参考传送门的文章。之后google又提出了解决sequence to sequence问题的transformer模型，用全attention的结构代替了lstm，在翻译任务上取得了更好的成绩。本文主要介绍《Attention is all you need》这篇文章，自己在最初阅读的时候还是有些不懂，希望可以在自己的解读下让大家更快地理解这个模型^ ^
    > 
    > **1\. 模型结构**
    > ------------
    > 
    > 模型结构如下图：
    > 
    > ![](https://pic1.zhimg.com/80/v2-4b53b731a961ee467928619d14a5fd44_hd.jpg)
    > 
    > 和大多数seq2seq模型一样，transformer的结构也是由encoder和decoder组成。
    > 
    > **1.1 Encoder**
    > ---------------
    > 
    > Encoder由N=6个相同的layer组成，layer指的就是上图左侧的单元，最左边有个"Nx"，这里是x6个。每个Layer由两个sub-layer组成，分别是multi-head self-attention mechanism和fully connected feed-forward network。其中每个sub-layer都加了residual connection和normalisation，因此可以将sub-layer的输出表示为：
    > 
    > ![sub\_layer\_output = LayerNorm(x+(SubLayer(x))) \\](http://www.zhihu.com/equation?tex=sub%5C_layer%5C_output+%3D+LayerNorm%28x%2B%28SubLayer%28x%29%29%29+%5C%5C)
    > 
    > 接下来按顺序解释一下这两个sub-layer：
    > 
    > -   **Multi-head self-attention**
    > 
    > 熟悉attention原理的童鞋都知道，attention可由以下形式表示：
    > 
    > ![attention\_output = Attention(Q, K, V) \\](http://www.zhihu.com/equation?tex=attention%5C_output+%3D+Attention%28Q%2C+K%2C+V%29+%5C%5C)
    > 
    > multi-head attention则是通过h个不同的**线性变换**对Q，K，V进行投影，最后将不同的attention结果拼接起来：
    > 
    > ![MultiHead(Q, K, V) = Concat(head_1, ..., head_h)W^O \\](http://www.zhihu.com/equation?tex=MultiHead%28Q%2C+K%2C+V%29+%3D+Concat%28head_1%2C+...%2C+head_h%29W%5EO+%5C%5C)
    > 
    > ![head_i = Attention(QW_i^Q, KW_i^K, VW_i^V) \\](http://www.zhihu.com/equation?tex=head_i+%3D+Attention%28QW_i%5EQ%2C+KW_i%5EK%2C+VW_i%5EV%29+%5C%5C)
    > 
    > self-attention则是取Q，K，V相同。
    > 
    > 另外，文章中attention的计算采用了scaled dot-product，即：
    > 
    > ![Attention(Q, K, V) = softmax(\frac{QK^T}{\sqrt{d_k}})V \\](http://www.zhihu.com/equation?tex=Attention%28Q%2C+K%2C+V%29+%3D+softmax%28%5Cfrac%7BQK%5ET%7D%7B%5Csqrt%7Bd_k%7D%7D%29V+%5C%5C)
    > 
    > 作者同样提到了另一种复杂度相似但计算方法additive attention，在 ![d_k](http://www.zhihu.com/equation?tex=d_k) 很小的时候和dot-product结果相似，![d_k](http://www.zhihu.com/equation?tex=d_k)大的时候，如果不进行缩放则表现更好，但dot-product的计算速度更快，进行缩放后可减少影响（由于softmax使梯度过小，具体可见论文中的引用）。
    > 
    > -   **Position-wise feed-forward networks**
    > 
    > 第二个sub-layer是个全连接层，之所以是position-wise是因为处理的attention输出是某一个位置i的attention输出。
    > 
    > **1.2 Decoder**
    > ---------------
    > 
    > Decoder和Encoder的结构差不多，但是多了一个attention的sub-layer，这里先明确一下decoder的输入输出和解码过程：
    > 
    > -   输出：对应i位置的输出词的概率分布
    > -   输入：encoder的输出 & 对应i-1位置decoder的输出。所以中间的attention不是self-attention，它的K，V来自encoder，Q来自上一位置decoder的输出
    > -   解码：**这里要特别注意一下，编码可以并行计算，一次性全部encoding出来，但解码不是一次把所有序列解出来的，而是像rnn一样一个一个解出来的**，因为要用上一个位置的输入当作attention的query
    > 
    > 明确了解码过程之后最上面的图就很好懂了，这里主要的不同就是新加的另外要说一下新加的attention多加了一个mask，因为训练时的output都是ground truth，这样可以确保预测第i个位置时不会接触到未来的信息。
    > 
    > 加了mask的attention原理如图（另附multi-head attention）：
    > 
    > ![](https://pic3.zhimg.com/80/v2-df2ca1b7a60d829245b7b7c37f80a3aa_hd.jpg)
    > 
    > **1.3 Positional Encoding**
    > ---------------------------
    > 
    > 除了主要的Encoder和Decoder，还有数据预处理的部分。Transformer抛弃了RNN，而RNN最大的优点就是在时间序列上对数据的抽象，所以文章中作者提出两种Positional Encoding的方法，将encoding后的数据与embedding数据求和，加入了相对位置信息。
    > 
    > 这里作者提到了两种方法：
    > 
    > 1.  用不同频率的sine和cosine函数直接计算
    > 2.  学习出一份positional embedding（[参考文献](http://link.zhihu.com/?target=https%3A//arxiv.org/abs/1705.03122)）
    > 
    > 经过实验发现两者的结果一样，所以最后选择了第一种方法，公式如下：
    > 
    > ![PE_{(pos, 2i)} = sin(pos/10000^{2i/d_{model}}) \\](http://www.zhihu.com/equation?tex=PE_%7B%28pos%2C+2i%29%7D+%3D+sin%28pos%2F10000%5E%7B2i%2Fd_%7Bmodel%7D%7D%29+%5C%5C)
    > 
    > ![PE_{(pos, 2i+1)} = cos(pos/10000^{2i/d_{model}}) \\](http://www.zhihu.com/equation?tex=PE_%7B%28pos%2C+2i%2B1%29%7D+%3D+cos%28pos%2F10000%5E%7B2i%2Fd_%7Bmodel%7D%7D%29+%5C%5C)
    > 
    > 作者提到，方法1的好处有两点：
    > 
    > 1.  任意位置的 ![PE_{pos+k}](http://www.zhihu.com/equation?tex=PE_%7Bpos%2Bk%7D) 都可以被 ![PE_{pos}](http://www.zhihu.com/equation?tex=PE_%7Bpos%7D) 的线性函数表示，三角函数特性复习下：
    > 
    > ![cos(\alpha+\beta) = cos(\alpha)cos(\beta)-sin(\alpha)sin(\beta) \\](http://www.zhihu.com/equation?tex=cos%28%5Calpha%2B%5Cbeta%29+%3D+cos%28%5Calpha%29cos%28%5Cbeta%29-sin%28%5Calpha%29sin%28%5Cbeta%29+%5C%5C)
    > 
    > ![sin(\alpha+\beta) = sin(\alpha)cos(\beta) + cos(\alpha)sins(\beta) \\](http://www.zhihu.com/equation?tex=sin%28%5Calpha%2B%5Cbeta%29+%3D+sin%28%5Calpha%29cos%28%5Cbeta%29+%2B+cos%28%5Calpha%29sins%28%5Cbeta%29+%5C%5C)
    > 
    > 2. 如果是学习到的positional embedding，（个人认为，没看论文）会像词向量一样受限于词典大小。也就是只能学习到"位置2对应的向量是(1,1,1,2)"这样的表示。所以用三角公式明显不受序列长度的限制，也就是可以对 比所遇到序列的更长的序列 进行表示。
    > 
    > **2\. 优点**
    > ----------
    > 
    > 作者主要讲了以下三点：
    > 
    > ![](https://pic4.zhimg.com/80/v2-a36b4e3924ef8864716736f8f1e77233_hd.jpg)
    > 
    > 1.  Total computational complexity per layer （每层计算复杂度）
    > 
    > 2\. Amount of computation that can be parallelized, as mesured by the minimum number of sequential operations required
    > 
    > 作者用最小的序列化运算来测量可以被并行化的计算。也就是说对于某个序列![x_1, x_2, ..., x_n](http://www.zhihu.com/equation?tex=x_1%2C+x_2%2C+...%2C+x_n) ，self-attention可以直接计算 ![x_i, x_j](http://www.zhihu.com/equation?tex=x_i%2C+x_j) 的点乘结果，而rnn就必须按照顺序从 ![x_1](http://www.zhihu.com/equation?tex=x_1) 计算到 ![x_n](http://www.zhihu.com/equation?tex=x_n)
    > 
    > 3\. Path length between long-range dependencies in the network
    > 
    > 这里Path length指的是要计算一个序列长度为n的信息要经过的路径长度。cnn需要增加卷积层数来扩大视野，rnn需要从1到n逐个进行计算，而self-attention只需要一步矩阵计算就可以。所以也可以看出，self-attention可以比rnn更好地解决长时依赖问题。当然如果计算量太大，比如序列长度n>序列维度d这种情况，也可以用窗口限制self-attention的计算数量
    > 
    > 4\. 另外，从作者在附录中给出的栗子可以看出，self-attention模型更可解释，attention结果的分布表明了该模型学习到了一些语法和语义信息
    > 
    > ![](https://pic3.zhimg.com/80/v2-d69547987a6510f22171b35c6e3f7e7e_hd.jpg)
    > 
    > **3\. 缺点**
    > ----------
    > 
    > 缺点在原文中没有提到，是后来在Universal Transformers中指出的，在这里加一下吧，主要是两点：
    > 
    > 1.  实践上：有些rnn轻易可以解决的问题transformer没做到，比如复制string，尤其是碰到比训练时的sequence更长的时
    > 2.  理论上：transformers非computationally universal（[图灵完备](https://www.zhihu.com/question/20115374/answer/288346717)），（我认为）因为无法实现"while"循环
    > 
    > **4\. 总结**
    > ----------
    > 
    > Transformer是第一个用纯attention搭建的模型，不仅计算速度更快，在翻译任务上也获得了更好的结果。Google现在的翻译应该是在此基础上做的，但是请教了一两个朋友，得到的答案是主要看数据量，数据量大可能用transformer好一些，小的话还是继续用rnn-based model
    > 
    > 以上。\
    > 【参考资料】：
    > 
    > 1.  [Attention is all you need](http://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1706.03762.pdf)
    > 2.  [知乎：谷歌论文《Attention is all you need》里Transformer模型的一些疑问？](https://www.zhihu.com/question/269481411)
    > 3.  [Stackoverflow: positional embedding](http://link.zhihu.com/?target=https%3A//stackoverflow.com/questions/46452020/sinusoidal-embedding-attention-is-all-you-need)
    > 



## 语言模型和迁移学习

- [【NLP】语言模型和迁移学习 - 知乎](https://zhuanlan.zhihu.com/p/42618178)

    > **1\. 简介**
    > ----------
    > 
    > 长期以来，词向量一直是NLP任务中的主要表征技术。随着2017年底以及2018年初的一系列技术突破，研究证实预训练的语言表征经过精调后可以在众多NLP任务中达到更好的表现。目前预训练有两种方法：
    > 
    > 1.  Feature-based：将训练出的representation作为feature用于任务，从词向量、句向量、段向量、文本向量都是这样的。新的ELMo也属于这类，但迁移后需要重新计算出输入的表征。
    > 2.  Fine-tuning：这个主要借鉴于CV，就是在预训练好的模型上加些针对任务的层，再对后几层进行精调。新的ULMFit和OpenAI GPT属于这一类。
    > 
    > 本文主要对ELMo、ULMFiT以及OpenAI GPT三种预训练语言模型作简要介绍。
    > 
    > **2\. ELMo**
    > ------------
    > 
    > **2.1 模型原理与架构**
    > ---------------
    > 
    > 原文链接：[Deep contextualized word representations](http://link.zhihu.com/?target=https%3A//arxiv.org/abs/1802.05365)
    > 
    > ELMo是从双向语言模型（BiLM）中提取出的Embedding。训练时使用BiLSTM，给定N个tokens (t1, t2,...,tN), 目标为最大化：
    > 
    > ![ \sum^N_{k=1}(\log p(t_k| t_1, ...,t_{k-1};\Theta x, \overrightarrow{\Theta}{LSTM}, \Theta s) + \log p(t_k\vert t{k+1}, ...,t_{N}; \Theta x, \overleftarrow{\Theta}{LSTM}, \Theta _s))  \\](http://www.zhihu.com/equation?tex=+%5Csum%5EN_%7Bk%3D1%7D%28%5Clog+p%28t_k%7C+t_1%2C+...%2Ct_%7Bk-1%7D%3B%5CTheta+x%2C+%5Coverrightarrow%7B%5CTheta%7D%7BLSTM%7D%2C+%5CTheta+s%29+%2B+%5Clog+p%28t_k%5Cvert+t%7Bk%2B1%7D%2C+...%2Ct_%7BN%7D%3B+%5CTheta+x%2C+%5Coverleftarrow%7B%5CTheta%7D%7BLSTM%7D%2C+%5CTheta+_s%29%29++%5C%5C)
    > 
    > ELMo对于每个token ![t_k](http://www.zhihu.com/equation?tex=t_k) , 通过一个L层的biLM计算出2L+1个表示：
    > 
    > ![R_k = {x_k^{LM}, \overrightarrow{h}{k,j}^{LM}, \overleftarrow{h}{k, j}^{LM} \vert j=1, ..., L} = {h_{k,j}^{LM} \vert j=0,..., L} \\](http://www.zhihu.com/equation?tex=R_k+%3D+%7Bx_k%5E%7BLM%7D%2C+%5Coverrightarrow%7Bh%7D%7Bk%2Cj%7D%5E%7BLM%7D%2C+%5Coverleftarrow%7Bh%7D%7Bk%2C+j%7D%5E%7BLM%7D+%5Cvert+j%3D1%2C+...%2C+L%7D+%3D+%7Bh_%7Bk%2Cj%7D%5E%7BLM%7D+%5Cvert+j%3D0%2C...%2C+L%7D+%5C%5C)
    > 
    > 其中 ![h_{k,0}^{LM}](http://www.zhihu.com/equation?tex=h_%7Bk%2C0%7D%5E%7BLM%7D) 是对token进行直接编码的结果(这里是字符通过CNN编码)， ![h_{k,j}^{LM} = [\overrightarrow{h}{k,j}^{LM}; \overleftarrow{h}{k, j}^{LM}]](http://www.zhihu.com/equation?tex=h_%7Bk%2Cj%7D%5E%7BLM%7D+%3D+%5B%5Coverrightarrow%7Bh%7D%7Bk%2Cj%7D%5E%7BLM%7D%3B+%5Coverleftarrow%7Bh%7D%7Bk%2C+j%7D%5E%7BLM%7D%5D) 是每个biLSTM层输出的结果。
    > 
    > 应用中将ELMo中所有层的输出R压缩为单个向量, ![ELMo_k = E(R_k;\Theta \epsilon)](http://www.zhihu.com/equation?tex=ELMo_k+%3D+E%28R_k%3B%5CTheta+%5Cepsilon%29) , 最简单的压缩方法是取最上层的结果做为token的表示: ![E(R_k) = h_{k,L}^{LM} ](http://www.zhihu.com/equation?tex=E%28R_k%29+%3D+h_%7Bk%2CL%7D%5E%7BLM%7D+) , 更通用的做法是通过一些参数来联合所有层的信息：
    > 
    > ![ELMo_k^{task} = E(R_k;\Theta ^{task}) = \gamma ^{task} \sum_{j=0}^L s_j^{task}h_{k,j}^{LM}  \\](http://www.zhihu.com/equation?tex=ELMo_k%5E%7Btask%7D+%3D+E%28R_k%3B%5CTheta+%5E%7Btask%7D%29+%3D+%5Cgamma+%5E%7Btask%7D+%5Csum_%7Bj%3D0%7D%5EL+s_j%5E%7Btask%7Dh_%7Bk%2Cj%7D%5E%7BLM%7D++%5C%5C)
    > 
    > 其中 ![s_j ](http://www.zhihu.com/equation?tex=s_j+) 是softmax出来的权重,![\gamma](http://www.zhihu.com/equation?tex=%5Cgamma) 是一个任务相关的scale参数，在优化过程中很重要，同时因为每层BiLM的输出分布不同， ![\gamma](http://www.zhihu.com/equation?tex=%5Cgamma) 可以对层起到normalisation的作用。
    > 
    > 论文中使用的预训练BiLM在[Jozefowicz et al.](http://link.zhihu.com/?target=https%3A//arxiv.org/abs/1602.02410)中的**CNN-BIG-LSTM**基础上做了修改，最终模型为**2**层biLSTM（4096 units, 512 dimension projections），并在第一层和第二层之间增加了残差连接。同时使用CNN和两层Highway对token进行字符级的上下文无关编码。使得模型最终对每个token输出三层向量表示。
    > 
    > **2.2 模型训练注意事项**
    > ----------------
    > 
    > **- 正则化**：
    > 
    > 1\. Dropout
    > 
    > 2\. 在loss中添加权重的惩罚项 ![\lambda||w||^{2}_{2} ](http://www.zhihu.com/equation?tex=%5Clambda%7C%7Cw%7C%7C%5E%7B2%7D_%7B2%7D+) (实验结果显示ELMo适合较小的 ![\lambda](http://www.zhihu.com/equation?tex=%5Clambda) )
    > 
    > **- [TF版源码](http://link.zhihu.com/?target=https%3A//github.com/allenai/bilm-tf)解析**：
    > 
    > 1\. 模型架构的代码主要在training模块的LanguageModel类中，分为两步：第一步创建word或character的Embedding层（CNN+Highway）；第二步创建BiLSTM层。
    > 
    > 2\. 加载所需的预训练模型为model模块中的BidirectionalLanguageModel类。
    > 
    > **2.3 模型的使用**
    > -------------
    > 
    > 1.  将ELMo向量 ![ELMo_k^{task}](http://www.zhihu.com/equation?tex=ELMo_k%5E%7Btask%7D) 与传统的词向量 ![x_{k}](http://www.zhihu.com/equation?tex=x_%7Bk%7D) 拼接成 ![[x_{k};ELMo_k^{task}] ](http://www.zhihu.com/equation?tex=%5Bx_%7Bk%7D%3BELMo_k%5E%7Btask%7D%5D+) 后，输入到对应具体任务的RNN中。
    > 2.  将ELMo向量放到模型输出部分，与具体任务RNN输出的 ![h_{k}](http://www.zhihu.com/equation?tex=h_%7Bk%7D) 拼接成 ![[h_{k};ELMo_k^{task}]](http://www.zhihu.com/equation?tex=%5Bh_%7Bk%7D%3BELMo_k%5E%7Btask%7D%5D) 。
    > 3.  [Keras代码示例](http://link.zhihu.com/?target=https%3A//github.com/strongio/keras-elmo)
    > 
    > ```
    > import tensorflow as tf
    > from keras import backend as K
    > import keras.layers as layers
    > from keras.models import Model
    > 
    > # Initialize session
    > sess = tf.Session()
    > K.set_session(sess)
    > 
    > # Instantiate the elmo model
    > elmo_model = hub.Module("https://tfhub.dev/google/elmo/1", trainable=True)
    > sess.run(tf.global_variables_initializer())
    > sess.run(tf.tables_initializer())
    > 
    > # We create a function to integrate the tensorflow model with a Keras model
    > # This requires explicitly casting the tensor to a string, because of a Keras quirk
    > def ElmoEmbedding(x):
    >     return elmo_model(tf.squeeze(tf.cast(x, tf.string)), signature="default", as_dict=True)["default"]
    > 
    > input_text = layers.Input(shape=(1,), dtype=tf.string)
    > embedding = layers.Lambda(ElmoEmbedding, output_shape=(1024,))(input_text)
    > dense = layers.Dense(256, activation='relu')(embedding)
    > pred = layers.Dense(1, activation='sigmoid')(dense)
    > 
    > model = Model(inputs=[input_text], outputs=pred)
    > 
    > model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
    > model.summary()
    > 
    > ```
    > 
    > **2.4 模型的优缺点**
    > --------------
    > 
    > **优点**：
    > 
    > 1.  效果好，在大部分任务上都较传统模型有提升。实验正式ELMo相比于词向量，可以更好地捕捉到语法和语义层面的信息。
    > 2.  传统的预训练词向量只能提供一层表征，而且词汇量受到限制。ELMo所提供的是character-level的表征，对词汇量没有限制。
    > 
    > **缺点**：
    > 
    > 速度较慢，对每个token编码都要通过language model计算得出。
    > 
    > **2.5 适用任务**
    > ------------
    > 
    > -   Question Answering
    > -   Textual entailment
    > -   Semantic role labeling
    > -   Coreference resolution
    > -   Named entity extraction
    > -   Sentiment analysis
    > 
    > **3\. ULMFiT**
    > --------------
    > 
    > **3.1 模型原理与架构**
    > ---------------
    > 
    > 原文链接：[Universal Language Model Fine-tuning for Text Classification](http://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1801.06146.pdf)
    > 
    > ULMFiT是一种有效的NLP迁移学习方法，核心思想是通过精调预训练的语言模型完成其他NLP任务。文中所用的语言模型参考了[Merity et al. 2017a](http://link.zhihu.com/?target=https%3A//arxiv.org/abs/1708.02182)的**AWD-LSTM**模型，即没有attention或shortcut的三层LSTM模型。
    > 
    > ULMFiT的过程分为三步：
    > 
    > ![](https://pic3.zhimg.com/80/v2-757fc68dcb577afacc6d8a7f635c12ee_hd.jpg)
    > 
    > **1\. General-domain LM pre-train**
    > 
    > -   在Wikitext-103上进行语言模型的预训练。
    > -   预训练的语料要求：large & capture general properties of language
    > 
    > -   预训练对小数据集十分有效，之后仅有少量样本就可以使模型泛化。
    > 
    > **2\. Target task LM fine-tuning**
    > 
    > 文中介绍了两种fine-tuning方法：
    > 
    > -   Discriminative fine-tuning
    > 
    > 因为网络中不同层可以捕获不同类型的信息，因此在精调时也应该使用不同的learning rate。作者为每一层赋予一个学习率 ![\eta^{l}](http://www.zhihu.com/equation?tex=%5Ceta%5E%7Bl%7D) ，实验后发现，首先通过精调模型的最后一层L确定学习率 ![\eta^{L}](http://www.zhihu.com/equation?tex=%5Ceta%5E%7BL%7D) ，再递推地选择上一层学习率进行精调的效果最好，递推公式为: ![\eta^{l-1} = \eta^{l}/2.6](http://www.zhihu.com/equation?tex=%5Ceta%5E%7Bl-1%7D+%3D+%5Ceta%5E%7Bl%7D%2F2.6)
    > 
    > -   Slanted triangular learning rates (STLR)
    > 
    > 为了针对特定任务选择参数，理想情况下需要在训练开始时让参数快速收敛到一个合适的区域，之后进行精调。为了达到这种效果，作者提出STLR方法，即让LR在训练初期短暂递增，在之后下降。如图b的右上角所示。具体的公式为：
    > 
    > ![ cut = floor{(T * cut_frac)} \\](http://www.zhihu.com/equation?tex=+cut+%3D+floor%7B%28T+%2A+cut_frac%29%7D+%5C%5C)
    > 
    > ![f(x)= \begin{cases} t/cut & \text{t < cut}\\ 1 - \frac{t-cut}{cut*(1/cut\_frac - 1)} & \text{otherwise} \end{cases} \\](http://www.zhihu.com/equation?tex=f%28x%29%3D+%5Cbegin%7Bcases%7D+t%2Fcut+%26+%5Ctext%7Bt+%3C+cut%7D%5C%5C+1+-+%5Cfrac%7Bt-cut%7D%7Bcut%2A%281%2Fcut%5C_frac+-+1%29%7D+%26+%5Ctext%7Botherwise%7D+%5Cend%7Bcases%7D+%5C%5C)
    > 
    > ![ \eta_{t} = \eta_{max} \frac{1+p(ratio -1)}{ratio} \\](http://www.zhihu.com/equation?tex=+%5Ceta_%7Bt%7D+%3D+%5Ceta_%7Bmax%7D+%5Cfrac%7B1%2Bp%28ratio+-1%29%7D%7Bratio%7D+%5C%5C)
    > 
    > -   T: number of training iterations
    > -   cut_frac: fraction of iterations we increase the LR
    > -   cut: the iteration when we switch from increasing to decreasing the LR
    > -   p: the fraction of the number of iterations we have increased or will decrease the LR respectively
    > -   ratio: specifies how much smaller the lowest LR is from thr max LR ![\eta_{max}](http://www.zhihu.com/equation?tex=%5Ceta_%7Bmax%7D)
    > -   ![ \eta_{t} ](http://www.zhihu.com/equation?tex=+%5Ceta_%7Bt%7D+) : the LR at iteration t
    > 
    > 文中作者使用的 ![ cut\_frac=1, ration=32, \eta_{max} = 0.01 ](http://www.zhihu.com/equation?tex=+cut%5C_frac%3D1%2C+ration%3D32%2C+%5Ceta_%7Bmax%7D+%3D+0.01+)
    > 
    > **3\. Target task classifier fine-tuning**
    > 
    > 为了完成分类任务的精调，作者在最后一层添加了两个线性block，每个都有batch-norm和dropout，使用ReLU作为中间层激活函数，最后经过softmax输出分类的概率分布。最后的精调涉及的环节如下：
    > 
    > -   Concat pooling\
    >     第一个线性层的输入是最后一个隐层状态的池化。因为文本分类的关键信息可能在文本的任何地方，所以只是用最后时间步的输出是不够的。作者将最后时间步 ![ h_{T}](http://www.zhihu.com/equation?tex=+h_%7BT%7D) 与尽可能多的时间步 ![H= {h_{1},... , h_{T}}](http://www.zhihu.com/equation?tex=H%3D+%7Bh_%7B1%7D%2C...+%2C+h_%7BT%7D%7D) 池化后拼接起来，以 ![h_{c} = [h_{T}, maxpool(H), meanpool(H)] ](http://www.zhihu.com/equation?tex=h_%7Bc%7D+%3D+%5Bh_%7BT%7D%2C+maxpool%28H%29%2C+meanpool%28H%29%5D+) 作为输入。
    > 
    > -   Gradual unfreezing\
    >     由于过度精调会导致模型遗忘之前预训练得到的信息，作者提出逐渐unfreez网络层的方法，从最后一层开始unfreez和精调，由后向前地unfreez并精调所有层。
    > 
    > -   BPTT for Text Classification (BPT3C)\
    >     为了在large documents上进行模型精调，作者将文档分为固定长度为b的batches，并在每个batch训练时记录mean和max池化，梯度会被反向传播到对最终预测有贡献的batches。
    > 
    > -   Bidirectional language model\
    >     在作者的实验中，分别独立地对前向和后向LM做了精调，并将两者的预测结果平均。两者结合后结果有0.5-0.7的提升。
    > 
    > **3.2 模型训练注意事项**
    > ----------------
    > 
    > **- [PyTorch版源码](http://link.zhihu.com/?target=https%3A//github.com/fastai/fastai)解析** (FastAI第10课)
    > 
    > ```
    > # location: fastai/lm_rnn.py
    > 
    > def get_language_model(n_tok, emb_sz, n_hid, n_layers, pad_token,
    >                  dropout=0.4, dropouth=0.3, dropouti=0.5, dropoute=0.1, wdrop=0.5, tie_weights=True, qrnn=False, bias=False):
    >     """Returns a SequentialRNN model.
    > 
    >     A RNN_Encoder layer is instantiated using the parameters provided.
    > 
    >     This is followed by the creation of a LinearDecoder layer.
    > 
    >     Also by default (i.e. tie_weights = True), the embedding matrix used in the RNN_Encoder
    >     is used to  instantiate the weights for the LinearDecoder layer.
    > 
    >     The SequentialRNN layer is the native torch's Sequential wrapper that puts the RNN_Encoder and
    >     LinearDecoder layers sequentially in the model.
    > 
    >     Args:
    >         n_tok (int): number of unique vocabulary words (or tokens) in the source dataset
    >         emb_sz (int): the embedding size to use to encode each token
    >         n_hid (int): number of hidden activation per LSTM layer
    >         n_layers (int): number of LSTM layers to use in the architecture
    >         pad_token (int): the int value used for padding text.
    >         dropouth (float): dropout to apply to the activations going from one LSTM layer to another
    >         dropouti (float): dropout to apply to the input layer.
    >         dropoute (float): dropout to apply to the embedding layer.
    >         wdrop (float): dropout used for a LSTM's internal (or hidden) recurrent weights.
    >         tie_weights (bool): decide if the weights of the embedding matrix in the RNN encoder should be tied to the
    >             weights of the LinearDecoder layer.
    >         qrnn (bool): decide if the model is composed of LSTMS (False) or QRNNs (True).
    >         bias (bool): decide if the decoder should have a bias layer or not.
    >     Returns:
    >         A SequentialRNN model
    >     """
    >     rnn_enc = RNN_Encoder(n_tok, emb_sz, n_hid=n_hid, n_layers=n_layers, pad_token=pad_token,
    >                  dropouth=dropouth, dropouti=dropouti, dropoute=dropoute, wdrop=wdrop, qrnn=qrnn)
    >     enc = rnn_enc.encoder if tie_weights else None
    >     return SequentialRNN(rnn_enc, LinearDecoder(n_tok, emb_sz, dropout, tie_encoder=enc, bias=bias))
    > 
    > def get_rnn_classifier(bptt, max_seq, n_class, n_tok, emb_sz, n_hid, n_layers, pad_token, layers, drops, bidir=False,
    >                       dropouth=0.3, dropouti=0.5, dropoute=0.1, wdrop=0.5, qrnn=False):
    >     rnn_enc = MultiBatchRNN(bptt, max_seq, n_tok, emb_sz, n_hid, n_layers, pad_token=pad_token, bidir=bidir,
    >                       dropouth=dropouth, dropouti=dropouti, dropoute=dropoute, wdrop=wdrop, qrnn=qrnn)
    >     return SequentialRNN(rnn_enc, PoolingLinearClassifier(layers, drops))
    > 
    > ```
    > 
    > **3.3 模型的优缺点**
    > --------------
    > 
    > **优点**：
    > 
    > 对比其他迁移学习方法（ELMo）更适合以下任务：
    > 
    > - 非英语语言，有标签训练数据很少
    > 
    > - 没有state-of-the-art模型的新NLP任务
    > 
    > - 只有部分有标签数据的任务
    > 
    > **缺点**：
    > 
    > 对于分类和序列标注任务比较容易迁移，对于复杂任务（问答等）需要新的精调方法。
    > 
    > **3.4 适用任务**
    > ------------
    > 
    > -   Classification
    > -   Sequence labeling
    > 
    > **4\. OpenAI GPT**
    > ------------------
    > 
    > **4.1 模型原理与架构**
    > ---------------
    > 
    > 原文链接：[Improving Language Understanding by Generative Pre-Training](http://link.zhihu.com/?target=https%3A//s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf) (未出版)
    > 
    > OpenAI Transformer是一类可迁移到多种NLP任务的，基于Transformer的语言模型。它的基本思想同ULMFiT相同，都是在尽量不改变模型结构的情况下将预训练的语言模型应用到各种任务。不同的是，OpenAI Transformer主张用Transformer结构，而ULMFiT中使用的是基于RNN的语言模型。文中所用的网络结构如下：
    > 
    > ![](https://pic3.zhimg.com/80/v2-8a4cbead57525234c6a33b23c96d18c6_hd.jpg)
    > 
    > 模型的训练过程分为两步：
    > 
    > **1\. Unsupervised pre-training**
    > 
    > 第一阶段的目标是预训练语言模型，给定tokens的语料 ![U = {u_{1}, ..., u_{n}}](http://www.zhihu.com/equation?tex=U+%3D+%7Bu_%7B1%7D%2C+...%2C+u_%7Bn%7D%7D) ，目标函数为最大化似然函数：
    > 
    > ![L_{1}(U) = \sum_{i}logP(u_{i}|u_{i-k}, ..., u_{i-1};\theta) \\](http://www.zhihu.com/equation?tex=L_%7B1%7D%28U%29+%3D+%5Csum_%7Bi%7DlogP%28u_%7Bi%7D%7Cu_%7Bi-k%7D%2C+...%2C+u_%7Bi-1%7D%3B%5Ctheta%29+%5C%5C)
    > 
    > 该模型中应用multi-headed self-attention，并在之后增加position-wise的前向传播层，最后输出一个分布：
    > 
    > ![h_{0}=UW_{e}+W_{p} \\](http://www.zhihu.com/equation?tex=h_%7B0%7D%3DUW_%7Be%7D%2BW_%7Bp%7D+%5C%5C)
    > 
    > ![h_{l} = transformer_block(h_{l-1})  \\](http://www.zhihu.com/equation?tex=h_%7Bl%7D+%3D+transformer_block%28h_%7Bl-1%7D%29++%5C%5C)
    > 
    > ![P(u) = softmax(h_{n}W_{e}^{T}) \\](http://www.zhihu.com/equation?tex=P%28u%29+%3D+softmax%28h_%7Bn%7DW_%7Be%7D%5E%7BT%7D%29+%5C%5C)
    > 
    > **2\. Supervised fine-tuning**
    > 
    > 有了预训练的语言模型之后，对于有标签的训练集 ![C](http://www.zhihu.com/equation?tex=C) ，给定输入序列 ![x^{1}, ..., x^{m}](http://www.zhihu.com/equation?tex=x%5E%7B1%7D%2C+...%2C+x%5E%7Bm%7D) 和标签 ![y](http://www.zhihu.com/equation?tex=y)，可以通过语言模型得到 ![h_{l}^{m}](http://www.zhihu.com/equation?tex=h_%7Bl%7D%5E%7Bm%7D) ，经过输出层后对 ![y ](http://www.zhihu.com/equation?tex=y+) 进行预测：
    > 
    > ![P(y|x^{1},...,x^{m})=softmax(h_{l}^{m}W_{y})  \\](http://www.zhihu.com/equation?tex=P%28y%7Cx%5E%7B1%7D%2C...%2Cx%5E%7Bm%7D%29%3Dsoftmax%28h_%7Bl%7D%5E%7Bm%7DW_%7By%7D%29++%5C%5C)
    > 
    > 则目标函数为：
    > 
    > ![L_{2}(C)= \sum_{(x,y)}logP(y|x^{1}...,x^{m}) \\](http://www.zhihu.com/equation?tex=L_%7B2%7D%28C%29%3D+%5Csum_%7B%28x%2Cy%29%7DlogP%28y%7Cx%5E%7B1%7D...%2Cx%5E%7Bm%7D%29+%5C%5C)
    > 
    > 整个任务的目标函数为：
    > 
    > ![L_{3}(C)= L_{2}(C)+\lambda * L_{1}(C) \\](http://www.zhihu.com/equation?tex=L_%7B3%7D%28C%29%3D+L_%7B2%7D%28C%29%2B%5Clambda+%2A+L_%7B1%7D%28C%29+%5C%5C)
    > 
    > **4.2 模型训练注意事项**
    > ----------------
    > 
    > **- [TF版源码](http://link.zhihu.com/?target=https%3A//github.com/openai/finetune-transformer-lm)解析**
    > 
    > ```
    > # location: finetune-transformer-lm/train.py
    > 
    > def model(X, M, Y, train=False, reuse=False):
    >     with tf.variable_scope('model', reuse=reuse):
    >         # n_special=3，作者把数据集分为三份
    >         # n_ctx 应该是 n_context
    >         we = tf.get_variable("we", [n_vocab+n_special+n_ctx, n_embd], initializer=tf.random_normal_initializer(stddev=0.02))
    >         we = dropout(we, embd_pdrop, train)
    > 
    >         X = tf.reshape(X, [-1, n_ctx, 2])
    >         M = tf.reshape(M, [-1, n_ctx])
    > 
    >         # 1. Embedding
    >         h = embed(X, we)
    > 
    >         # 2. transformer block
    >         for layer in range(n_layer):
    >             h = block(h, 'h%d'%layer, train=train, scale=True)
    > 
    >         # 3. 计算语言模型loss
    >         lm_h = tf.reshape(h[:, :-1], [-1, n_embd])
    >         lm_logits = tf.matmul(lm_h, we, transpose_b=True)
    >         lm_losses = tf.nn.sparse_softmax_cross_entropy_with_logits(logits=lm_logits, labels=tf.reshape(X[:, 1:, 0], [-1]))
    >         lm_losses = tf.reshape(lm_losses, [shape_list(X)[0], shape_list(X)[1]-1])
    >         lm_losses = tf.reduce_sum(lm_losses*M[:, 1:], 1)/tf.reduce_sum(M[:, 1:], 1)
    > 
    >         # 4. 计算classifier loss
    >         clf_h = tf.reshape(h, [-1, n_embd])
    >         pool_idx = tf.cast(tf.argmax(tf.cast(tf.equal(X[:, :, 0], clf_token), tf.float32), 1), tf.int32)
    >         clf_h = tf.gather(clf_h, tf.range(shape_list(X)[0], dtype=tf.int32)*n_ctx+pool_idx)
    > 
    >         clf_h = tf.reshape(clf_h, [-1, 2, n_embd])
    >         if train and clf_pdrop > 0:
    >             shape = shape_list(clf_h)
    >             shape[1] = 1
    >             clf_h = tf.nn.dropout(clf_h, 1-clf_pdrop, shape)
    >         clf_h = tf.reshape(clf_h, [-1, n_embd])
    >         clf_logits = clf(clf_h, 1, train=train)
    >         clf_logits = tf.reshape(clf_logits, [-1, 2])
    > 
    >         clf_losses = tf.nn.sparse_softmax_cross_entropy_with_logits(logits=clf_logits, labels=Y)
    >         return clf_logits, clf_losses, lm_losses
    > 
    > ```
    > 
    > **4.3 模型的优缺点**
    > --------------
    > 
    > **优点**：
    > 
    > 1.  循环神经网络所捕捉到的信息较少，而Transformer可以捕捉到更长范围的信息。
    > 2.  计算速度比循环神经网络更快，易于并行化
    > 3.  实验结果显示Transformer的效果比ELMo和LSTM网络更好
    > 
    > **缺点**：
    > 
    > 对于某些类型的任务需要对输入数据的结构作调整
    > 
    > **4.4 适用任务**
    > ------------
    > 
    > -   Natural Language Inference
    > -   Question Answering and commonsense reasoning
    > -   Classification
    > -   Semantic Similarity
    > 
    > **5\. 总结**
    > ----------
    > 
    > 从Wrod Embedding到OpenAI Transformer，NLP中的迁移学习从最初使用word2vec、GLoVe进行字词的向量表示，到ELMo可以提供前几层的权重共享，再到ULMFiT和OpenAI Transformer的整个预训练模型的精调，大大提高了NLP基本任务的效果。同时，多项研究也表明，以语言模型作为预训练模型，不仅可以捕捉到文字间的语法信息，更可以捕捉到语义信息，为后续的网络层提供高层次的抽象信息。另外，基于Transformer的模型在一些方面也展现出了优于RNN模型的效果。
    > 
    > 最后，关于具体任务还是要进行多种尝试，可以使用以上方法做出模型baseline，再调整网络结构提升效果。