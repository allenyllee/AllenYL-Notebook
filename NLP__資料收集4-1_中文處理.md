# NLP__資料收集4-1_中文處理

[toc]
<!-- toc --> 

# 中文自然語言處理

- [如何斷開中文峰峰相連的詞彙鎖鍊，讓電腦能讀懂字裡行間的語意？ - PanSci 泛科學](https://pansci.asia/archives/144346)

- [線上系統展示 | CKIP Lab 中文詞知識庫小組](http://ckip.iis.sinica.edu.tw:8080/demo/)

- [認識中文字元碼](http://idv.sinica.edu.tw/bear/charcodes/Section05.htm)


# 常用中文規則

## 中日韓 Unicode table

- [CJK Unified Ideographs - Unicode® character table](https://unicode-table.com/en/blocks/cjk-unified-ideographs/)

## 標點符號

- [关于标点符号 · Issue #169 · fxsjy/jieba](https://github.com/fxsjy/jieba/issues/169)

    > ```
    > :!),.:;?]}¢'"、。〉》」』】〕〗〞︰︱︳﹐､﹒
    > ﹔﹕﹖﹗﹚﹜﹞！），．：；？｜｝︴︶︸︺︼︾﹀﹂﹄﹏､～￠
    > 々‖•·ˇˉ―--′’”([{£¥'"‵〈《「『【〔〖（［｛￡￥〝︵︷︹︻
    > ︽︿﹁﹃﹙﹛﹝（｛“‘-—_…
    > ```

## 文言文字典

- [可以处理文言文吗？ · Issue #639 · fxsjy/jieba](https://github.com/fxsjy/jieba/issues/639)

- [nlputils/jiebazhc at master · The-Orizon/nlputils](https://github.com/The-Orizon/nlputils/tree/master/jiebazhc)



## 千家姓

- [中華民族萬家姓: 中華民國注音姓氏排行榜（民國96年版）](https://chab88.blogspot.com/2009/07/blog-post_10.html)

- https://regex101.com/r/jvUKrP/15/

    > |陳|林|黃|張|李|王|吳|劉|蔡|楊|許|鄭|謝|郭|洪|邱|曾|廖|賴|徐|周|葉|蘇|莊|呂|江|何|蕭|羅|高|潘|簡|朱|鍾|彭|游|詹|胡|施|沈|余|盧|趙|梁|顏|柯|翁|魏|孫|戴|方|宋|范|鄧|杜|傅|侯|曹|薛|丁|卓|馬|董|唐|藍|蔣|石|温|古|紀|姚|黄|連|馮|歐|程|湯|康|田|姜|汪|白|鄒|尤|巫|鐘|涂|阮|龔|黎|韓|嚴|袁|金|童|陸|夏|柳|凃|邵|錢|溫|伍|倪|于|譚|駱|熊|任|顧|甘|秦|毛|史|章|萬|俞|官|雷|饒|粘|張簡|闕|崔|尹|凌|孔|歐陽|辛|辜|易|陶|段|龍|葛|韋|池|孟|殷|褚|賈|賀|麥|管|莫|文|關|向|包|武|丘|范姜|華|梅|樊|利|房|左|佘|魯|安|鮑|花|郝|全|穆|邢|塗|蒲|成|常|谷|耿|盛|練|鄔|聶|祝|曲|解|繆|齊|申|閻|岳|符|龎|應|籃|裴|陽|單|舒|牛|喬|畢|翟|鄞|季|留|卜|塗|覃|喻|項|滕|焦|商|買|車|苗|戚|虞|牟|臧|力|樂|雲|樓|艾|費|巴|司|屈|宗|尚|靳|桂|諶|衛|宮|祁|欒|髙|沙|路|幸|刁|時|柴|瞿|閻|談|隋|柏|竇|鄺|查|霍|閔|吉|冉|遲|仲|鄂|仇|儲|松|龎|湛|東|風|榮|匡|婁|冷|甯|卞|裘|昌|晏|桑|顏|席|初|岑|邊|叢|禇|郁|姬|偕|蘭|蒙|兵|區|勞|郎|甄|奚|屠|聞|景|鞠|明|佟|釋|周黃|米|伊|荊|厲|茆|机|盤|原|封|干|才|錡|粟|江謝|容|標|平|皮|宜|宣|竺|茅|藺|鄢|司徒|蓋|敖|張廖|芮|黨|冼|寇|苑|候|惠|貝|栢|危|狄|於|南|禹|胥|嵇|杞|枋|烏|逄|諸|師|岩|楚|鹿|修|農|浦|哀|欉|城|來|戎|翁林|月|豐|那|甯|強|忻|滿|覺|関|姜林|都|支|帥|闞|戰|宇|晁|濮|元|郜|燕|井|朱陳|雍|寧|廉|束|相|鈕|絲|上官|酆|森|鞏|永|揭|慕|計|薄|麻|栗|杭|富|壽|卿|斯|羊|戈|印|居|邴|班|陳李|哈|張陳|普|權|門|張李|邱黃|賓|林吳|亓|日|陳黃|漆|冀|王李|李陳|端木|衣|祖|爐|綦|卯|酈|根|閆|葉劉|乃|步|矯|國|姬|念|招|臺|資|李林|仝|苟|璩|寸|秋|達|薩|尉|展|栁|水|陳吳|諸葛|經|索|扈|山|嘪|宓|甯|鳳|扶|勵|豆|和|海|邰|墜|角|劉黃|衡|肖|昝|隆|伏|貢|同|英|過|茹|味|銀|曠|邸|豊|公|眭|糠|宿|沃|字|但|楓|閩|出|盂|信|紅|赫|湖|巖|陳許|敬|蒯|闗|習|漳|操|廣|褚|侍|晋|堯|邜|阮呂|皇甫|霜|滑|劉張|生|朴|洗洗|晉|况|李黃|張許|巢|周|登|書|勤|依|陣|掌|黑|玉|由|廉|藩|宛|郗|三|法|洋|承|禚|磨|閉|唐|丹|哖|延|禤|亢|巧|阿|翼|邦|虎|陰|靖|沐|訾|鮮|歸|桞|剛|望|李王|王吳|別|衷|奉|青|保|毒|母|渠|刀|勾|郭李|蘇陳|毋|律|慈|巨|呼|番|鎖|徐陳|冒|徐辜|歐李|階|糜|焉|么|世|冬|雙|鐵|布|年|逯|言|玲|咸|須|王劉|仰|稅|張楊|蔡黃|位|壯|從|刑|庄|謝林|木|芶|秘|漢|軒|博|尋|開|蟻|續|曾林|郇|申屠|陳呂|記|檀|鬆|鄭黃|完|隗|寶|尉遲|老|埕|惲|台|庾|后|拾|俸|植|蒼|芎|咼|淡|党|團|卡|戢|懷|庹|陵|撤|多|荀|郟|示|考|定|瑪|蔚|職|郭黃|員|遊|慶|弓|郤|笪|蹇|罕|陀|送|欽|遇|果|長|學|乜|牙|宦|种|閃|倫|西|亞|拉|拓|豹|鴻|倉|財|智|儀|墨|隨|籍|火|業|縱|吳鄭|汝|猶|兆|伯|首|泰|魚|暢|賽|方鄒|波|堵|脩|淩|線|譙|司馬|洪許|岡|蚋|賁|雅|詩|銅|潛|蓮|繩|壬|牧|莎|祿|潭|闇|川|杲|振|央|竹|行|乳|凍|及|以|可|仵|拱|部|越|陳彭|乙|付|光|佐|昂|春|樟|祈|菰|幹|所|河|速|繞|黃沈|余楊|廖蔡|甫|府|思|崇|新|德|劉許|問|密|接|尼|瓦|乾|釧|淦|勝|貴|澎|類|夏侯|軒轅|劉范|莊吳|仁|吾|底|巷|是|旋|疏|僧|暴|賢|閭|蘆|代|先|院|吳游|介|化|仉|殳|把|里|呼|怯|迮|零|鍾張|劉郭|因|香|理|脫|圍|斐|萇|嘉|察|霄|汲|納|慎|遠|襲|弋|甲|回|洛|革|郅|宰|校|裔|樸|鎮|鮮于|曾江|後|娜|家|停|傳|槐|增|澹|隴|徐謝|正|局|勇|弭|揚|虢|糴|陳辜|朿|克|帖|度|要|茶|逢|弼|福|肇|雒|雛|索南|張趙|千|占|格|荷|答|補|粱|道|諾|穰|淳于|李梁|郭洪|孫林|百|順|運|端|蒿|蕢|優|籠|玄|杻|柑|眉|神|桃|浮|剡|喜|楮|電|睢|暨|賞|靜|令狐|胡周|朱吳|顓孫|加|希|飛|酒|菅|塘|義|藏|耀|戴楊|大|佃|拜|秧|寒|敦|樹|機|興|嶺|鎦|鐔|札西|康張|江周|張朱|小|比|令|妙|具|彼|旺|皋|益|教|紫|萊|奧|節|緒|輝|翦|獨|鑑|沈游|東方|王顏|朱翁|列|合|治|奕|威|星|皇|苫|浣|斜|腰|嘎|憨|讓|札|名|夷|如|次|姒|泣|俎|偉|務|梨|犁|彪|提|塔|源|鉉|滾|磊|麗|露|邏|濮陽|一|攸|拔|桐|浩|豈|偶|敏|頓|嘺|彌|營|孫劉|陸費|連林|孑|天|心|旦|托|旮|佛|卲|受|固|板|況|者|雨|卻|洒|庫|茬|基|雪|凱|復|愛|碧|舞|劇|緱|鑾|土登|第五|凡|北|抄|枉|姥|省|美|胖|荒|荐|釗|旃|排|紹|傘|尊|善|聖|頊|監|維|緞|闖|騰|旦增|格桑|簡蕭|黃路|尢|丑|朮|臣|君|求|佡|羋|肯|芭|降|珠|紐|耕|陝|得|淳|清|莉|傑|棘|棗|猴|媽|歲|溥|圖|爾|銓|閰|審|稽|範|噶|舉|默|螘|禮|蕾|王易|薛林|士|中|守|有|姑|油|泊|娃|若|拿拿|真|假|啜|莘|筆|菲|閑|煙|貊|樵|積|縣|錫|鐘簡|白瑪|嚴林|上|扎|仕|句|弗|吏|汗|伋|宏|村|社|帕|拖|昆|沓|妲|厚|咪|彥|祕|茍|衍衍|迪|苖|邾|厙|恭|恩|扆|崗|淑|野|偰|揣|換|淵|琪|超|鄉|飽|筱|雎|漫|種|翡|潤|駒|薜|霞|甕|雞|繳|繼|鬱|袞桑|褚阮|益西|延陵|了|八|今|少|必|矢|立|朵|努|志|改|見|赤|制|奇|委|妮|朋|芙|邯|俄|係|珍|約|恒|埃|庭|效|起|剪|勒|將|渚|細|透|晴|逸|寋|督|號|賃|載|雋|竭|韶|禢|摩|潼|潮|嬴|澤|鄶|濱|濟|環|總|鍊|藤|騫|囊|靈|朱田|貢佈|扎西|丌|內|太|斗|本|目|旭|自|优|呈|吼|坊|坎|秀|伭|汶|奔|泥|知|芳|表|軋|非|俐|哇|恪|曷|柔|泉|祗|耐|苦|茂|迦|俉|奎|倚|島|徒|悅|桓|珮|珞|啊|堅|專|您|措|笛|第|荻|堀|閈|堪|湘|琴|結|意|椿|殿|瑞|群|誠|鉛|溤|演|睡|酸|遷|頡|養|撖|戲|黛|齋|瀨|璽|瓊|簫|證|礦|籐|辯|班森|于林|入|也|兀|勺|丐|允|刈|友|丙|且|叭|它|打|汀|卌|亦|伙|吁|佑|兌|呀|夾|妣|孝|孜|尾|每|玖|良|汴|刺|協|取|坤|岱|庚|性|或|舍|衫|邳|勃|契|姻|屋|恆|染|某|柒|呰|姞|昶|昜|訇|哲|娘|娟|娥|息|悟|扇|挪|烘|素|能|荏|迴|陜|鬥|袓|匙|參|曼|唱|圈|培|庶|晚|梵|梭|欸|淨|笙|軟|通|堤|壹|嵐|棠|琪|琺|琵|甦|硯|策|菜|跋|鈔|喏|羡|塞|廈|會|瑁|睦|肅|裟|該|詳|靶|葳|豋|僮|撤|歌|閥|閤|箂|鄚|蔤|儉|寬|憂|澄|潔|瑾|賡|褟|儒|導|憑|歷|璣|錦|霓|頭|錒|縮|霙|織|舊|黟|廬|簿|繡|霧|繨|羆|贇|藹|鐃|躍|曩|蘜|蘧|讀|曬|鸞|棋|于廖|旦巴|鍾巴|公羊|文樂|伊西|江田|班澤|



# 中文詞/字嵌入

## Chinese Character Embeddings

- [干货|NLP领域中文vs英文有什么异同点，中文NLP有什么独特的地方?_搜狐科技_搜狐网](http://www.sohu.com/a/138840703_642762)

- [Leonard-Xu/CWE](https://github.com/Leonard-Xu/CWE)


# 中文摘要

- [zkwi/textSummary: 文本智能摘要提取](https://github.com/zkwi/textSummary)


# 漢語語言推理

- [讓計算機明白「天天」代表「每一天」之後，如何避免讓它認爲「爸爸」代表「每個爸」 - 幫趣](http://bangqu.com/J414WY.html)

    > 類比推理可以很好地刻畫語言規則，舉例說明，「人」等價於person，「人人」則等價於英文的 every person，那麼如果「天」代表 day，我們就可以類比推理「天天」代表 every day。目前類比推理也是評估詞嵌入的一個可靠方法。類比推理還可以用於詞形轉換、語義關係探測和翻譯未知詞等任務。但是不同語言之間擁有很大的形態差異，類比推理針對各個語言的研究也不盡相同。以漢語來說，漢語是公認的缺乏詞形變化的分析性語言。目前漢語類比推理的相關工作也屈指可數，僅有的中文類比數據集也只是英文數據集的部分翻譯，且數據規模較小，只包含 134個 中文詞，並且不涉及到任何語法知識。因此，作者團隊決定深入研究漢語類比推理，並且發佈了一個標準 benchmark 用以評估中文詞嵌入（[附帶 100 多個開源預訓練嵌入](https://github.com/Embedding/Chinese-Word-Vectors)）。
    > 
    > 在詞法關係方面，作者主要研究了兩個內容，一是重疊（Reduplication），二是半詞綴（Semi-affixation）。所謂重疊就是詞語中的部分漢字以一定的形式發生重疊，從而引起語法或語義差異，作者總結出六種重疊模式，如下圖所示。
    > 
    > ![讓計算機明白「天天」代表「每一天」之後，如何避免讓它認爲「爸爸」代表「每個爸」](http://i2.bangqu.com/lf1/news/20180803/5b598309ccb95.png)
    > 
    > 以 A-A 爲例，對於漢語中的名詞來說，這種結構可以表示「親屬關係」（爸->爸爸）或者表示「每一個」（天->天天），對於動詞來說，這種結構可以表示動作時間短暫或嘗試（看->看看），這種結構還能將形容詞轉爲副詞（深->深深）。
    > 
    > 由於漢語缺乏典型的詞綴，一些成分既發揮了類似詞綴的作用同時又能當作獨立使用的語素，這些成分按劉月華老師的觀點稱之爲半詞綴。目前作者團隊總結了 21 個半前綴，和 41 個半後綴。例如，半前綴可以將數詞變爲序數詞，如「第」（一->第一），半後綴還有將形容詞名詞化的能力，如「子」（胖->胖子）
    > 
    > 在語義關係方面，作者團隊從地理、歷史、自然和人物四個方面提出了 28 種語義關係。舉個地域方面的例子，「浙江」是省名，「浙」是「浙江」簡稱，「杭州」是「浙江」省會，「越劇」是「浙江」代表戲劇，這就是他們之間的語義關係。通過語義關係可以形成類比問題（如「皖」是「安徽」的省會，那麼「浙」是哪個省的省會？）。
    > 
    > 爲了滿足漢語類比推理任務的要求，作者團隊自建了 CA8 數據集（共17813 個問題），包含大量的類比問題，對語法和語義都有涉及。CA8 相較於之前翻譯自英文數據集的 CA_translated 有很大改進。如下圖所示。
    > 
    > ![讓計算機明白「天天」代表「每一天」之後，如何避免讓它認爲「爸爸」代表「每個爸」](http://i2.bangqu.com/lf1/news/20180803/5b598cee17c91.png)
    > 
    > 最後，作者的實驗基於 68 種形態關係和 28 種語義關係，他們採用基於詞向量的計算方法來挑戰這個任務。實驗結果表明，向量表示模型、上下文特徵和訓練語料庫都對漢語類比推理有重要影響。同時實驗也證明了 CA8 的確是評價漢語詞嵌入的可靠 benchmark。 CA8 和同期發佈的上百種中文詞向量資源將成爲漢語 NLP 任務的堅實基礎。論文相關資源和代碼在Github發佈以來，已獲得超過2000星，是今年NLP領域最受歡迎的項目之一。
    > 
    > 以上就是對於這篇論文的全部介紹。
    > 
    > 詳情請查看論文：[http://aclweb.org/anthology/P18-2023 ](http://aclweb.org/anthology/P18-2023)
    > 
    > Github項目：<https://github.com/Embedding/Chinese-Word-Vectors>

# 文言文翻譯

## 基于 Moses 的文言文统计机器翻译系统

- [Moses - Main/HomePage](http://www.statmt.org/moses/)

- [文言文線上翻譯](https://app.gumble.pw/wenyan/)

- [基于 Moses 的文言文统计机器翻译系统 - GumboGumble](https://gumble.pw/classical-chinese-translation.html)


    > 这是一份参加学校办的科技竞赛写的论文。既然没得奖，就直接放出来供大家参考吧。本文内容参见之前发布的 [《文言文机器翻译》](https://gumble.pw/wenyan-translate.html)。点击使用 [在线演示](https://app.gumble.pw/wenyan/)。
    > 
    > 为了更清楚地列出所采用的资源和工具，在发布时另外标注了链接和符号角标。
    > 
    > **摘要**：本项目制作了一种文言文机器翻译系统，使用了基于词组的统计翻译模型。通过收集整理大量平行语料、训练针对文言文的分词系统并应用统计机器翻译中的先进技术，在控制了模型大小和内存占用的情况下，使本系统的翻译结果质量超过了现有系统的水平。本系统拥有较为友好的用户交互界面，能根据文本特征自动确定翻译方向并在结果中显示原文和译文中词语的对应关系，最终本系统可以为用户提供了一个新的文言文辅助阅读方法。
    > 
    > **关键词**：文言文，统计机器翻译，自然语言处理
    > 
    > 
    > [1   概述](https://gumble.pw/classical-chinese-translation.html#id90)
    > -------------------------------------------------------------------
    > 
    > 文言文是古汉语的书面语言，具有文字简练的特点，与现代白话文有较大区别。要读懂文言文需要有对应的训练并积累一定的阅读量，这导致大多数人较难读懂古代典籍。为了帮助阅读和理解文言文，本项目实现了一种文言文翻译系统。
    > 
    > 统计机器翻译是广泛采用的一种机器翻译的模式，其通过对大量平行语料进行分析，构造统计模型，从而使用该模型生成翻译。寻找最佳翻译的过程就是找到根据模型的参数产生概率最高的句子。[Moses](http://www.statmt.org/moses/) [[1]](https://gumble.pw/classical-chinese-translation.html#id77) 是一套成熟完善的统计机器翻译系统，可以训练产生能够翻译任意语言对的翻译模型，并通过高效的搜索算法找到最有可能的翻译结果。
    > 
    > 本项目采用基于词组的统计翻译模型 [[2]](https://gumble.pw/classical-chinese-translation.html#id78)，通过收集大量平行语料，并根据文言文和现代汉语的特点进行了相应处理和优化，得到了质量较高的翻译结果。本项目同时设计了一个基于网页的用户交互界面。
    > 
    > [2   语料收集与处理](https://gumble.pw/classical-chinese-translation.html#id91)
    > ------------------------------------------------------------------------
    > 
    > 语料的收集处理是统计机器翻译的重要组成部分。由于统计机器翻译的原理和特点，需要有大量平行语料并进行相对应的处理，才能训练得到较好的翻译结果。
    > 
    > ### [2.1   平行语料](https://gumble.pw/classical-chinese-translation.html#id92)
    > 
    > 本项目使用了大量网络上可获得的平行语料，包括各个文言文翻译网站以及古代书籍的译注版本。对于这些来源，都分别按照其格式特点进行了半自动半人工的处理，从而丰富了平行语料的来源，减少了大量无效数据。根据处理后平行语料的质量和对齐程度不同，可分为极少量的按句对齐、一些按段落对齐和其他大部分按篇章对齐的语料。Moses 统计机器翻译系统主要针对的是按句翻译，也就需要将平行语料按句对齐。
    > 
    > 已按句对齐的语料无需处理即可直接使用。按段落对齐和按篇章对齐的处理步骤相似，首先都要将其进行断句处理。断句规则为，在分号、句号、感叹号、问号后断句；如果有下引号，则在其之后断句；在冒号和上引号之间断句。在实际翻译时也必须采用相同的断句规则。之后，采用[机器翻译辅助句对齐](https://github.com/rsennrich/Bleualign)的方法 [[3]](https://gumble.pw/classical-chinese-translation.html#id79)，使用之前的训练的模型粗略翻译一遍原文，保证原文和机翻译文能按句对齐，以修改后的 BLEU 得分比较机翻译文和参考译文的相似度，最后使原文和参考译文能按句对齐。最后，统一过滤无效句对并去重，得到按句对齐、可供 Moses 直接使用的平行语料，称为训练集，约有八十五万句对；从上述平行语料中另外人工抽取并校对一千对左右翻译质量较高的句子作为调优集和评估集。
    > 
    > ### [2.2   单一语言语料](https://gumble.pw/classical-chinese-translation.html#id93)
    > 
    > 除了平行语料，单一语言语料的作用在统计机器翻译中也是十分重要的。现代白话文语料除了上述平行语料之外，主要包括新闻 [[*]](https://gumble.pw/classical-chinese-translation.html#id14)、小说、字幕 [[†]](https://gumble.pw/classical-chinese-translation.html#id15)和维基媒体项目 [[‡]](https://gumble.pw/classical-chinese-translation.html#id16) [[§]](https://gumble.pw/classical-chinese-translation.html#id17) （除中文维基文库）等 [[¶]](https://gumble.pw/classical-chinese-translation.html#id18)。文言文语料除了平行语料之外，主要包括中文维基文库中筛选出的古代和近代的文献。最终得到的单一语言语料数量较大，约为上述平行语料的二十倍，作为语言模型的训练材料，能更好地保证输出语言的通顺流畅。
    > 
    > | [[*]](https://gumble.pw/classical-chinese-translation.html#id9) | 可参考 [搜狗全网新闻数据](https://www.sogou.com/labs/dl/ca.html)，本项目未使用 |
    > 
    > | [[†]](https://gumble.pw/classical-chinese-translation.html#id10) | [Web Inventory of Transcribed and Translated Talks](https://wit3.fbk.eu/) |
    > 
    > | [[‡]](https://gumble.pw/classical-chinese-translation.html#id11) | [维基媒体项目数据库](https://dumps.wikimedia.org/) |
    > 
    > | [[§]](https://gumble.pw/classical-chinese-translation.html#id12) | [维基媒体项目导出数据转文本](https://github.com/attardi/wikiextractor) |
    > 
    > | [[¶]](https://gumble.pw/classical-chinese-translation.html#id13) | 还有 [OPUS: the open parallel corpus](http://opus.lingfil.uu.se/)，未标注参考文献 |
    > 
    > ### [2.3   文字的选择](https://gumble.pw/classical-chinese-translation.html#id94)
    > 
    > 本项目对于上述所有语料，统一转换成简化字 [[#]](https://gumble.pw/classical-chinese-translation.html#id24)，即训练的模型使用的文字为简体字。中华人民共和国自 1956 年后施行汉字简化制度，所以在此之前的文献应以传统汉字（繁体字）保存。然而，由于网络上使用繁体中文的平行语料资源严重缺乏；繁体中文语料来源质量参差不齐，有些是使用机器从简体简单转换而来，鱼龙混杂 [[♠]](https://gumble.pw/classical-chinese-translation.html#id25)；校对原文需要极大的人力；而且无法确保能将用户输入的简体中文输入正确转换为对应繁体，正确处理文言文的简繁转换比对白话文的简繁转换更为困难 [[♥]](https://gumble.pw/classical-chinese-translation.html#id26)，所以经过考虑，语料和用户输入将统一转换为简化字之后再进行处理。 [[♦]](https://gumble.pw/classical-chinese-translation.html#id27)
    > 
    > | [[#]](https://gumble.pw/classical-chinese-translation.html#id20) | 这里采用 [OpenCC](https://github.com/BYVoid/OpenCC) |
    > 
    > | [[♠]](https://gumble.pw/classical-chinese-translation.html#id21) | 指维基文库。 |
    > 
    > | [[♥]](https://gumble.pw/classical-chinese-translation.html#id22) | 可以尝试再来一份用于简繁转换的统计机器翻译模型。 |
    > 
    > | [[♦]](https://gumble.pw/classical-chinese-translation.html#id23) | 在线上采用「[简易中文简繁转换](https://github.com/gumblex/zhconv)」 |
    > 
    > [3   模型训练](https://gumble.pw/classical-chinese-translation.html#id95)
    > ---------------------------------------------------------------------
    > 
    > 这个翻译系统使用的特征包括短语翻译模型、语言模型、调序模型以及一些稀疏特征。翻译模型（短语翻译表）使源语言和目标语言的词汇能互相对应，语言模型确保输出的是通顺的目标语言，调序模型可以适当改变输入语句的顺序，附加的稀疏特征能给输出评分更多参考，可较大程度提高翻译质量。
    > 
    > ### [3.1   中文分词](https://gumble.pw/classical-chinese-translation.html#id96)
    > 
    > 在训练翻译模型和语言模型之前，需要先对文言文和白话文进行针对性的分词处理以提高翻译质量。[[4]](https://gumble.pw/classical-chinese-translation.html#id80) 对于现代白话文，使用了 ["结巴"中文分词软件](https://github.com/fxsjy/jieba)，禁用了默认的隐马尔可夫新词发现模型，防止产生模型外词汇。
    > 
    > 对于文言文，不能简单使用白话文的分词模型，所以首先构建了文言文分词所需要使用的词汇表。词汇表来源有"结巴"包含的默认词典（按词性筛选出部分实词），台湾教育部《重编国语词典修订本》（按词汇类别筛选） [[♣]](https://gumble.pw/classical-chinese-translation.html#id34) 以及各种关于历史人物、地名、朝代、官职等输入法词库 [[**]](https://gumble.pw/classical-chinese-translation.html#id35)，再加上用程序生成的数字、方位、干支等词汇，共计约三万八千条。 [[††]](https://gumble.pw/classical-chinese-translation.html#id36)
    > 
    > 鉴于文言文大部分为单音节词汇，少有分词歧义，所以在训练分词模型时简单采用了首先进行最大正向匹配，再统计每个词汇出现次数的方法，即最大似然估计，最后筛选掉极低频词汇。在文言文分词时，运用此字典即可获得较好的分词效果。
    > 
    > | [[♣]](https://gumble.pw/classical-chinese-translation.html#id31) | 《[萌典](https://www.moedict.tw/)》 [数据](https://github.com/g0v/moedict-process) |
    > 
    > | [[**]](https://gumble.pw/classical-chinese-translation.html#id32) | 主要是搜狗、百度和 QQ 拼音词库。 |
    > 
    > | [[††]](https://gumble.pw/classical-chinese-translation.html#id33) | 下载：[简体](https://gumble.pw/static/zhcdict-s.txt.gz)、[繁体](https://gumble.pw/static/zhcdict-t.txt.gz) |
    > 
    > ### [3.2   语言模型](https://gumble.pw/classical-chinese-translation.html#id97)
    > 
    > 在训练语言模型时采用上述在数量上更多的单一语言语料。语言模型采用 [KenLM](http://kheafield.com/code/kenlm/) 语言模型工具估算生成四元语言模型，其使用 Modified Kneser-Ney 算法 [[5]](https://gumble.pw/classical-chinese-translation.html#id81) 平滑 n 元组数据。生成 ARPA 文本格式的语言模型之后，转换成 KenLM [[6]](https://gumble.pw/classical-chinese-translation.html#id82) 的 Trie 数据结构二进制文件。使用这种数据结构的文件相比其实现的另外一种 Probing（散列表）数据结构，文件更小、占用内存更少，但速度稍慢。因为这些语言模型所用的语料更新次数相对较少且模型生成速度慢，所以不在下述"实验管理系统"中生成。
    > 
    > ### [3.3   实验管理系统](https://gumble.pw/classical-chinese-translation.html#id98)
    > 
    > 通过使用 Moses 附带的"实验管理系统"[[7]](https://gumble.pw/classical-chinese-translation.html#id83) [[‡‡]](https://gumble.pw/classical-chinese-translation.html#id50)，编写一个配置文件，就可自动完成模型训练的各个过程。训练步骤为：分词、过滤、词对齐、建立翻译及调序模型、过滤模型、权重调优、评估。
    > 
    > ![Experiment Management System](https://gumble.pw/img/lzht-ems.png)
    > 
    > **图 1** 实验管理系统生成的模型训练步骤
    > 
    > 首先系统按照配置，将训练集、调优集和评估集使用上述分词方法进行分词，并筛选掉超过 100 词的句子，因为长句通常可靠性不高，而且会减慢词对齐速度。然后，系统将分词后的平行语料进行预处理，准备进行词对齐。在本项目中，使用基于 IBM Model 2 的 [fast_align](https://github.com/clab/fast_align) [[8]](https://gumble.pw/classical-chinese-translation.html#id84) 工具进行词对齐。该工具比常用的基于 IBM Model 4 的词对齐工具约快十倍，且在源语言和目标语言语序相似的情况下质量相当。
    > 
    > 词对齐之后，系统提取词组表，合并预先准备的文言文词典的释义作为附加词组表，限定词组的最大长度为 4，并同时生成词汇调序表。按照对词组在平行语料中共同出现的显著性检验，可以删减掉大部分词组表而不影响、甚至提高翻译得分 [[9]](https://gumble.pw/classical-chinese-translation.html#id85)，从而节省大量空间。同时，使用压缩词汇表和调序表技术 [[10]](https://gumble.pw/classical-chinese-translation.html#id86) 能进一步减少磁盘占用而不影响翻译速度。
    > 
    > 在调优时不仅考虑翻译模型、语言模型等特征，还加入了目标词汇插入、源词汇删除、词汇直接翻译、词汇长度四种稀疏特征，这可以使 BLEU 得分提高约 20%。因为特征数目较多，调优采用 k-best MIRA 算法 [[11]](https://gumble.pw/classical-chinese-translation.html#id87)。得到最佳特征参数后，对模型进行整体评估，计算 BLEU [[12]](https://gumble.pw/classical-chinese-translation.html#id88) 评分，从而可以对翻译质量进行量化比较。上述过程所产生的最终模型文件较小 [[§§]](https://gumble.pw/classical-chinese-translation.html#id51)，翻译时内存占用适中 [[¶¶]](https://gumble.pw/classical-chinese-translation.html#id52)，适合在云端服务部署。
    > 
    > 因为将文言文和白话对调再训练模型即可获得反向翻译功能，所以每次均进行双向训练，得到文言文到白话文和白话文到文言文两个翻译模型。这两个模型互相独立，因此不能保证它们有相同的翻译质量。
    > 
    > | [[‡‡]](https://gumble.pw/classical-chinese-translation.html#id42) | [Experiment Management System](http://www.statmt.org/moses/?n=FactoredTraining.EMS). 此部分涉及内容参见 Moses 文档。 |
    > 
    > | [[§§]](https://gumble.pw/classical-chinese-translation.html#id48) | 两个模型总计约 0.5G。 |
    > 
    > | [[¶¶]](https://gumble.pw/classical-chinese-translation.html#id49) | 服务端内存占用总计约 0.5G。 |
    > 
    > ### [3.4   语言判定](https://gumble.pw/classical-chinese-translation.html#id99)
    > 
    > 在设计用户界面过程中，自动判定翻译方向可以简化用户操作。通过建立朴素贝叶斯分类器，可以比较准确地判断出源语言。该模型使用 Unicode"中日韩统一表意文字"U+4E00 到 U+9FCC 区段共 20941 个汉字作为识别文本的特征，并认为白话文和文言文出现概率相同。忽略 Unicode 中其他汉字区段是因为其中绝大部分汉字过于生僻，在实际文本中几乎不会出现。
    > 
    > 训练语料采用前述白话文和文言文两个单一语言语料库。在训练模型时使用最大似然估计，并使用 Simple Good-Turing [[13]](https://gumble.pw/classical-chinese-translation.html#id89) 算法平滑数据，防止有零概率出现。计算之后将概率值取对数储存为 JSON 数据文件。
    > 
    > 该模型的数据文件比较大，为了在网页客户端脚本中使用，将每个值量化，用 ASCII 中的可打印字符表示成字符串。计算时可直接取字符编码相加，比较结果。如果计算结果为零，则说明其中不包含模型中的汉字，无法确定翻译方向。
    > 
    > [4   软件设计](https://gumble.pw/classical-chinese-translation.html#id100) [[##]](https://gumble.pw/classical-chinese-translation.html#id60)
    > ----------------------------------------------------------------------------------------------------------------------------------------
    > 
    > ### [4.1   软件结构](https://gumble.pw/classical-chinese-translation.html#id101)
    > 
    > 软件获得的用户输入为待翻译字符串和翻译方向。如果前端没有指定翻译方向，则在服务器端由上述朴素贝叶斯分类器进行自动选择。如果无法确定翻译方向，例如输入文本为其他语言，认为该文本无法翻译，所以按原样输出。之后服务端判断，如果用户短时间内请求太多，则生成验证码验证是否为人工操作；如果文本太长，则要求用户切分文本再提交，防止服务过载。
    > 
    > 网页服务器将收到的文本通过 TCP 接口提交给后台翻译服务进程。该服务进程可以响应包括翻译、分词、简繁转换等命令，通过将这些服务集中在一个服务进程，可以提高稳定性，避免网页服务器重复加载词典。该服务进程同时管理两个后台 Moses 进程，分别负责两个方向的翻译。
    > 
    > 在收到翻译请求后，先去除特殊字符，分行并按标点分句。其中在分句时，如果一句太长，则按逗号等标点切分，若还是太长，则直接按字数切分，防止一句翻译产生过多候选，占用内存过多或耗时过长。对于切分后的每一句话，检查是否包含上述"语言判定"中所使用区段范围内的汉字，如果没有则直接进入输出队列；将输入规范标点、统一转换为简体后，如果该句包含在缓存中，也直接输出。之后，程序为待翻译语句进行分词、XML 转义并在标点符号前后添加调序限制，通过标准输入调用 Moses 进程翻译。当 Moses 结束翻译，翻译服务进程解析其标准输出，XML 反向转义、解析词对齐，将结果加入输出队列，并加入缓存。最后，程序收集上述翻译结果，并按照调用参数格式化输出。网页服务器收到其回应后，按照用户浏览器设定中偏好的语言（简体或繁体） [[♠♠]](https://gumble.pw/classical-chinese-translation.html#id61) 转换输出文字，最后生成网页呈现给用户。
    > 
    > ![Flow chart](https://gumble.pw/img/lzht-flowchart.png)
    > 
    > **图 2** 软件结构和翻译过程
    > 
    > 在之后的开发中，该服务后端将实现翻译应用程序接口，从而实现即时翻译功能，并为相关开发者提供更简便的服务。
    > 
    > ### [4.2   用户界面](https://gumble.pw/classical-chinese-translation.html#id102)
    > 
    > 本项目实现了基于网页的用户界面，使该文言文翻译系统成为一个网络服务。
    > 
    > ![Web interface](https://gumble.pw/img/lzht-web.png)
    > 
    > **图 3** 基于网页的用户界面
    > 
    > 该界面除实现了基本的输入、输出功能之外，还可以自动判别翻译方向，并可在结果中显示原文和译文中词语的对应关系。翻译方向的判别由上述语言判定模型完成，如果判定错误，用户可按"切换"按钮更正。鼠标移动，或触摸屏触摸到译文上的词汇时，在相应位置会高亮标出词汇的对应关系，用户从而能更好地评估翻译结果。在屏幕小的设备上，网页会自动适配为上下排版，方便用户操作。
    > 
    > | [[##]](https://gumble.pw/classical-chinese-translation.html#id55) | 「语言判定」部分以及该部分源码包含在 <https://github.com/gumblex/pywebapps> |
    > 
    > | [[♠♠]](https://gumble.pw/classical-chinese-translation.html#id58) | 即 `Accept-Language` 头。 |
    > 
    > [5   相关研究对比](https://gumble.pw/classical-chinese-translation.html#id103)
    > ------------------------------------------------------------------------
    > 
    > 在网络上能找到的最早的文言文翻译软件是"文言之星" [[♥♥]](https://gumble.pw/classical-chinese-translation.html#id68)，更新日期为 2001 年。该软件采用简单按照词汇表替换的方式进行翻译，且只能将文言文翻译为白话文。由于其边翻译边更新图形界面，所以速度较慢。[[♦♦]](https://gumble.pw/classical-chinese-translation.html#id69) 该软件翻译效果一般，没有考虑到分词和歧义问题，对上下文的处理能力较弱。 [[♣♣]](https://gumble.pw/classical-chinese-translation.html#id70)
    > 
    > 在 2014 年 4 月百度翻译推出了文言文翻译功能 [[***]](https://gumble.pw/classical-chinese-translation.html#id71)，能较好地完成文言文和白话文互译任务，对于未知文言文语句，其翻译结果会输出较多原文。通过本项目的几次失败实验，可以推测，百度翻译较本项目不足之处可能在于其模型为二元，或者在文言文分词方面有缺陷。百度翻译会对名句段进行直接匹配，而在匹配后再进行简繁转换，所以繁体和简体输入得到的结果可能略有不同。
    > 
    > 例如：
    > 
    > 1.  孔子适郑，与弟子相失，孔子独立郭东门。（《史记・孔子世家》）
    > 
    > > **文言之星**：孔你适郑，和弟你相失，孔你单独确定郭东门。
    > >
    > > **百度翻译**：孔子到郑国，与学生相互失去，孔子独自站在郭东门。
    > >
    > > **本项目**：孔子到了郑国，与弟子们失散了，孔子独自站在外城的东门。
    > 
    > 1.  少焉，月出于东山之上，徘徊于斗牛之间，白露横江，水光接天；纵一苇之所如，陵万顷之茫然。（《前赤壁赋》）
    > 
    > > **文言之星**：少呢，月出在东山的向上，徘徊在争胜负牛的参与，白露横江，水光接天；纵一苇的处所象，陵很多一会儿茫然而。
    > >
    > > **百度翻译**（原文为繁体）：少了，月出于东山之上，徘徊在斗宿、牛宿之间，白露横江，水光和天际连结成一片；即使一苇之所如，陵万顷的茫然。
    > >
    > > **百度翻译**（原文为简体）：少了，月亮从东山的上空升起，在斗宿和牛宿两星座之间徘徊，白漾漾的雾气笼罩江面，水光和天际连结成一片；任凭苇叶似的小船飘向何处，陵万顷的茫然。
    > >
    > > **本项目**：不多时，明月从东山后升起的上边，徘徊在斗星与牛的时候，白露横江，水光接上天；即使一叶小舟的地方，而去，李陵万顷的茫然。
    > 
    > 可见上述例文均不同程度地出现在百度翻译和本项目的训练集中。文言之星完全缺乏合适的分词和歧义处理。百度翻译对名句的直接匹配可以在一定程度上弥补机器翻译的不足。本项目没有进行直接匹配，会尽量尝试进行翻译而不是直接输出难以确定的词组，并且能更好地反馈训练集的内容，即召回率较高。
    > 
    > 使用相同的测试集、分词方法和 BLEU 算法对上述系统进行翻译质量评估，得到评分如下表。如表所示，本项目在翻译质量上能可见地超过上述研究。
    > 
    > **表 1** 各文言文翻译系统的 BLEU 得分比较
    > | 系统 | 文言文到白话文 | 白话文到文言文 |
    > | --- | --- | --- |
    > | 文言之星 | 6.12 | N/A |
    > | 百度翻译 | 20.41 | 34.11 |
    > | 本项目 | **30.48** | **48.19** |
    > 
    > 本项目为独立项目，与上述研究完全无关。上述例文和评估数据均为测试当时所产生 [[†††]](https://gumble.pw/classical-chinese-translation.html#id72)，会因各系统模型、参数或算法等更新而变化。
    > 
    > | [[♥♥]](https://gumble.pw/classical-chinese-translation.html#id63) | 自行搜索下载。 |
    > 
    > | [[♦♦]](https://gumble.pw/classical-chinese-translation.html#id64) | 17537 字测试集，文言之星用时约 51 分钟，百度翻译用时约半分钟（包括网络延迟），本项目用时约三分钟。 |
    > 
    > | [[♣♣]](https://gumble.pw/classical-chinese-translation.html#id65) | 在测试中采用了[重新实现的 Python 版本](https://github.com/The-Orizon/nlputils/blob/master/WWStarClone.py)以提高速度。 |
    > 
    > | [[***]](https://gumble.pw/classical-chinese-translation.html#id66) | 在「百度翻译」 [网页](http://fanyi.baidu.com/#wyw/zh/)或客户端中选择 |
    > 
    > | [[†††]](https://gumble.pw/classical-chinese-translation.html#id67) | 测试时使用的模型为 2016 年 3 月生成的模型，代号「陈振栋」。 |
    > 
    > [6   结论与展望](https://gumble.pw/classical-chinese-translation.html#id104)
    > -----------------------------------------------------------------------
    > 
    > 本项目实现了一个基于统计模型的文言文机器翻译系统。该系统能对文言文和白话文进行较准确的互译，有比现有系统更高的翻译质量。本项目也实现了一个图形用户界面，方便用户进行翻译操作。本项目不仅使用了现有机器翻译框架，还针对文言文分词进行了优化、建立了用于识别文言文和现代文的模型并编写了整合功能较多、更适合中文的 Moses 前端服务，提供了一个新的文言文辅助阅读方法。
    > 
    > 未来可以在这个基础上增添平行语料、加入词汇参数或句法模型，并改善语言模型，使翻译结果更精确；在翻译服务后端增加负载平衡等措施，提高翻译服务在云端部署的可扩展性。同时，用户界面可以加入即时翻译和字典等功能，使该系统能更适合于辅助文言文阅读和学习。由于本项目最终使用的模型文件总体大小较小，可以考虑进一步缩小模型文件并制作成手机应用，使用户在离线时也可以翻译文言文。 [[‡‡‡]](https://gumble.pw/classical-chinese-translation.html#id75)
    > 
    > | [[‡‡‡]](https://gumble.pw/classical-chinese-translation.html#id74) | 除非有资助或其他贡献者，这些展望很难实现。 |
    > 
    > [7   参考文献](https://gumble.pw/classical-chinese-translation.html#id105)
    > ----------------------------------------------------------------------
    > 
    > | [[1]](https://gumble.pw/classical-chinese-translation.html#id3) | Philipp Koehn, Hieu Hoang, Alexandra Birch, Chris Callison-Burch, Marcello Federico, Nicola Bertoldi, Brooke Cowan, Wade Shen, Christine Moran, Richard Zens, Chris Dyer, Ondrej Bojar, Alexandra Constantin, Evan Herbst, "Moses: Open Source Toolkit for Statistical Machine Translation", In *Proceedings of the 45th Annual Meeting of the ACL on Interactive Poster and Demonstration Sessions*, pages 177--180, 2007. |
    > 
    > | [[2]](https://gumble.pw/classical-chinese-translation.html#id4) | Philipp Koehn, Franz Josef Och, Daniel Marcu, "Statistical phrase-based translation", *Proceedings of the 2003 Conference of the North American Chapter of the Association for Computational Linguistics on Human Language Technology*, p.48-54, May 27-June 01, 2003, Edmonton, Canada |
    > 
    > | [[3]](https://gumble.pw/classical-chinese-translation.html#id7) | Rico Sennrich, Martin Volk, "MT-based Sentence Alignment for OCR-generated Parallel Texts". In *Proceedings of AMTA 2010*, Denver, Colorado, 2010 |
    > 
    > | [[4]](https://gumble.pw/classical-chinese-translation.html#id30) | Pi-Chuan Chang, Michel Galley and Christopher D. Manning, "Optimizing Chinese word segmentation for machine translation performance", *Proceedings of the Third Workshop on Statistical Machine Translation*, p.224-232, June 19-19, 2008, Columbus, Ohio |
    > 
    > | [[5]](https://gumble.pw/classical-chinese-translation.html#id38) | Kenneth Heafield, Ivan Pouzyrevsky, Jonathan H. Clark, and Philipp Koehn. "Scalable modified Kneser-Ney language model estimation". In *Proceedings of the 51st Annual Meeting of the Association for Computational Linguistics*, Sofia, Bulgaria, 4---9 August, 2013. |
    > 
    > | [[6]](https://gumble.pw/classical-chinese-translation.html#id39) | Kenneth Heafield, "KenLM: Faster and Smaller Language Model Queries." WMT at EMNLP, Edinburgh, Scotland, United Kingdom, 30---31 July, 2011. |
    > 
    > | [[7]](https://gumble.pw/classical-chinese-translation.html#id41) | Philipp Koehn, "An Experimental Management System.", Proceedings of the Machine Translation Marathon 2010, *The Prague Bulletin of Mathematical Linguistics*, vol. 94, pp. 86-96, 2010. |
    > 
    > | [[8]](https://gumble.pw/classical-chinese-translation.html#id43) | Chris Dyer, Victor Chahuneau, and Noah A. Smith. "A Simple, Fast, and Effective Reparameterization of IBM Model 2". In Proc. of NAACL, 2013. |
    > 
    > | [[9]](https://gumble.pw/classical-chinese-translation.html#id44) | Howard Johnson, Joel Martin, George Foster, and Roland Kuhn. "Improving translation quality by discarding most of the phrasetable". In *Proceedings of EMNLP-CoNLL*. 967--975. 2007. |
    > 
    > | [[10]](https://gumble.pw/classical-chinese-translation.html#id45) | Marcin Junczys-Dowmunt. "Phrasal Rank-Encoding: Exploiting Phrase Redundancy and Translational Relations for Phrase Table Compression", Proceedings of the Machine Translation Marathon 2012, *The Prague Bulletin of Mathematical Linguistics*, vol. 98, pp. 63-74, 2012. |
    > 
    > | [[11]](https://gumble.pw/classical-chinese-translation.html#id46) | Colin Cherry and George Foster, "Batch tuning strategies for statistical machine translation", In *Proceedings of the 2012 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies*, pages 427--436, 2012. |
    > 
    > | [[12]](https://gumble.pw/classical-chinese-translation.html#id47) | Papineni, Kishore, Salim Roukos, Todd Ward, and Wei-Jing Zhu. "BLEU: A Method for Automatic Evaluation of Machine Translation.", *Proceedings of the 40th Annual Meeting on Association for Computational Linguistics*, pp. 311--318, 2002. |
    > 
    > [[13]](https://gumble.pw/classical-chinese-translation.html#id54)Gale, William A., and Geoffrey Sampson. "Good‐turing Frequency Estimation without Tears." *Journal of Quantitative Linguistics* 2.3 (1995): 217-37.


# 中文處理流程



## python文字探勘，資料前處理流程介紹

- [python文字探勘，資料前處理流程介紹 @ DannyPhoebe's 鼴鼠豬 ~ miscellaneous](https://dannypheobe.blogspot.com/2016/07/python.html)

    > **●讀取文本資料**\
    > 在處理文件時，最好是希望能批次性的處理。因此在抓取資料時，最好就預先注意輸出的格式，以及排除錯誤的資料，這都將會使後續的步驟更加地順利省事。
    > 
    > 程式碼實作，利用**python內建的 os.listdir**，就可以列出所有包含在某資料夾內的檔案。再配合上 startswith或是 endswith來限定檔名，就可以進一步縮小列出的範圍。接著，就可以依照自己資料的格式，撰寫一個讀檔的 function，將文本資料一一的讀進程式中。
    > ```py
    > import os
    > rootdir = os.path.join(os.getcwd(),'your_directory')
    > your_files = [os.path.join(rootdir,item) for item in os.listdir(rootdir) if item.endswith('.txt')] #舉例找出檔名結尾為.txt的檔案
    > 
    > corpus = []
    > 
    > def load_text(file):
    >     with open(file,'r') as I:
    >         return I.readlines
    > 
    > for file in your_files:
    >     corpus += load_text(file)
    > ```
    > 
    > **●將雜訊轉換為單一標籤**
    > 進行機器學習時，一般會希望盡量減少分析目標外的干擾，以達到更高的準確率。例如分析中文資料時，就可以統一利用 NUM及 ENG來將資料中包含的數字以及英文給取代掉。
    > 
    > 程式碼實作的部份，像這種關於字串特徵的處理，一般都是應用 **正則表示式(regular expression)** 的方式來解決。所謂的正則表示式，就是利用一些符號來找出文字中特定的特徵，推薦看這篇[**部落格文章**](http://blog.csdn.net/pleasecallmewhy/article/details/8929576)來作瞭解以及後續的查詢。
    > ```py
    > import re
    > for sentence in corpus:
    >     sentence = re.sub(r'[A-Za-z]+', ' ENG ', sentence)
    >     sentence = re.sub(r'\d+', ' NUM ',  sentence)
    > ```
    > python有內建相當強大的正則表示式模組re，可以利用**re.sub (substitute)的功能**來將符合特徵的文字作替換。大家可以搭配上面的連結來看看程式碼中的 \d+、[A-Za-z]+等等是什麼意思，肯定更能體會正則表示式的用途。
    > 
    > **●中文斷詞**
    > 由於中文的詞與詞之間並不像英文存在空格隔開，因此如何適當地將成串的文字斷開成詞的組合一直是中文自然語言處理(natural language processing, NLP)中重要的問題。
    > 
    > 在斷詞處理上，python最廣為使用的套件當屬 **結巴斷詞 (jieba)** 了。僅管結巴斷詞的正確率不是最優秀的，但它方便擴充自訂辭典的設計以及簡單的操作方式讓使用者可以快速上手。
    > 
    > 程式碼實作，我認為這篇[**部落格文章**](http://blog.fukuball.com/ru-he-shi-yong-jieba-jie-ba-zhong-wen-fen-ci-cheng-shi/)舉例說明的相當清楚，推薦大家參考看看，這邊就不再贅述。
    > 
    > **●去除停止詞**
    > 在斷完詞之後，若你去進行詞頻分析時一定會發現，許多無法突顯主題的冗字出現的頻率總是名列前矛，例如：的、我、你、嗎，以及標點符號等等。對於這些字，這個領域中就稱之為 **停止詞 (stopword)** ，而一般在進行文字探勘時都會預先將這些字詞剔除。
    > 
    > 網路上可以搜尋到不少人家準備好的[**停止詞詞庫**](http://www.cnblogs.com/ibook360/archive/2011/11/23/2260397.html)，但大多都是簡體中文的資源。不用擔心，利用 Google網頁翻譯或是[**線上簡轉繁的服務**](http://38time.artjoey.com/link/trans_ts.htm)大家就可以建立好繁體的停止詞詞庫了。當然，在使用過程中也可以依照自己的需要去增減它。
    > 
    > 程式碼實作，最方便的作法是先以 with open將停止詞詞庫讀入一個 list後，再利用個 for迴圈檢查句子中的每一個詞是否包含在停止詞詞庫中。
    > 
    > ```py
    > with open('stopword.txt','r') as f:
    >     stopwords = f.readlines()
    > 
    > your_words = segmented_sentence #已經斷詞好的語料
    > words_filtered = ' '.join([word for word in your_words if word not in stopwords]) #將停止詞濾掉
    > ```
    > 題外話，若今天是想檢查整個文本而非一個單詞是否含有停止詞時，可以利用python中 **內建的 function：any()** ，詳細可參考[**這篇 stackoverflow的回答**](http://stackoverflow.com/questions/3271478/check-list-of-words-in-another-string)。
    > 




## 計算詞頻

- [好玩的分詞——python jieba分詞模組的基本用法 - 掃文資訊](https://tw.saowen.com/a/4145f47a12884f749ce11a4b15ac990cab092c260232ab09ee0d76ce48158ebd)

    > > 獲取出現頻率Top n的詞
    > =============
    > 
    > 還是以上面的三體全集文字為例，假如想要獲取分詞結果中出現頻率前20的詞列表，可以這樣獲取：
    > 
    > ```py
    > from collections import Counter
    > c = Counter(santi_words).most_common(20)
    > print c
    > 
    > ```
    > 


## 移除停用詞/產生文字雲

- [中文自然語言處理基礎 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10192043)

    > Import
    > ======
    > 
    > ```py
    > import jieba
    > jieba.set_dictionary('dict.txt.big')  # 如果是使用繁體文字，請記得去下載繁體字典來使用
    > with open('stops.txt', 'r', encoding='utf8') as f:  # 中文的停用字，我也忘記從哪裡拿到的，效果還可以，繁體字的資源真的比較少，大家將就一下吧
    >     stops = f.read().split('\n')
    > 
    > ```
    > 
    > ---
    > 
    > 1. Import套件並把以上文章輸入
    > 
    >     ```py
    >     from collections import Counter
    >     from wordcloud import WordCloud
    >     from matplotlib import pyplot as plt
    > 
    >     testStr = """
    >     前言
    >     中文自然語言處理，與英文最大的差別就在斷詞，但是說實話，這個部分至今仍然沒有一個套件可以做好很好。目前而言，繁體中文有兩個套件可以使用，一個是中研院開發的斷詞系統，但是經過多方打聽，使用上並不是特別方便。因此我個人打選擇使用第二套系統jieba，中文叫做結巴，很幸運地這個套件有python的介面，使用上非常容易，只是這是大陸人開發的系統，必須自行輸入繁體字典，這篇文章的繁體字典出處在這邊。順帶一提，這篇文章寫得很好，對於jieba如果有想要有更深的認識，可以好好拜讀。
    >     另外，由於這篇文章有使用到許多外部資源，所以若有需要巡長文章中出現的其他檔案，請參考這個repo
    > 
    >     斷詞
    >     結巴的斷詞分成兩個模式，精準模式只找到系統演算出最精準的斷詞可能，全斷詞模式則是把所有可能的斷詞模式列出來，如果你想要用來做文本分析，句子又沒有很長的的時候，建議你可以使用全斷詞模式，可以增加文跟文章之間的可比性，我曾經因為把斷詞模式改掉，在預測準確率上面就從96%變成99%，大家可以參考一下。
    > 
    >     去除停用字
    >     這個部分跟英文沒什麼差別啦，只是中文的停用字並沒有被內建在nltk當中，要自己找檔案，上面Import是我找到的檔案，大家覺得不夠好也可以自己再去找。不過因為實在太長的，我就不全部列出來了。
    > 
    >     詞性標注
    >     雖然jieba也有提供詞性標注功能，不過實在做得還不到能用的程度，實務上我也沒什麼在用，所以大家就先略過這個部分吧。
    > 
    >     其他
    >     由於這邊文章實在太短了，又有很大部分與昨天的文章重複，所以我們就拿上面我已經打好的文字來做分析吧。
    >     """
    >     ```
    > 
    > 2.  斷詞並去除停用字
    > 
    >     ```py
    >     stops.append('\n')  ## 我發現我的文章中有許多分行符號，這邊加入停用字中，可以把它拿掉
    >     stops.append('\n\n')
    >     terms = [t for t in jieba.cut(testStr, cut_all=True) if t not in stops]
    >     sorted(Counter(terms).items(), key=lambda x:x[1], reverse=True)  ## 這個寫法很常出現在Ｃounter中，他可以排序，list每個item出現的次數。
    >     ```
    > 
    >     ![https://ithelp.ithome.com.tw/upload/images/20171219/20107576HfU19b7hGg.png](https://ithelp.ithome.com.tw/upload/images/20171219/20107576HfU19b7hGg.png)
    > 
    > 3.  產生文字雲（請特別注意要加上字形檔，否則會產生亂碼）
    > 
    >     ```py
    >     wordcloud = WordCloud(font_path="simsun.ttf")  ##做中文時務必加上字形檔
    >     wordcloud.generate_from_frequencies(frequencies=Counter(terms))
    >     plt.figure(figsize=(15,15))
    >     plt.imshow(wordcloud, interpolation="bilinear")
    >     plt.axis("off")
    >     plt.show()
    >     ```
    > 
    >     ![https://ithelp.ithome.com.tw/upload/images/20171219/20107576LXAdzuZue5.png](https://ithelp.ithome.com.tw/upload/images/20171219/20107576LXAdzuZue5.png)
    > 
    > 4.  如果你喜歡一些有圖片遮罩的文字雲\
    >     如果你想要做到一樣的事情，只是用不同的遮罩，或是不同的文字，以下會叼寄出你要改的部分。
    >     
    > 
    >     ```py
    >     from PIL import Image
    > 
    >     alice_mask = np.array(Image.open("cloud_mask7.png"))  ## 請更改cloud_mask7.png路徑
    >     wc = WordCloud(background_color="white", max_words=2000, mask=alice_mask, font_path="simsun.ttf")
    >     wc.generate_from_frequencies(Counter(terms))  ## 請更改Counter(terms)
    > 
    >     # wc.to_file(path.join(d, "cloud.png"))  ##如果要存檔，可以使用
    > 
    >     plt.imshow(wc, interpolation='bilinear')
    >     plt.axis("off")
    >     plt.figure()
    >     plt.imshow(alice_mask, cmap=plt.cm.gray, interpolation='bilinear')
    >     plt.axis("off")
    >     plt.show()
    >     ```
    > 
    >     ![https://ithelp.ithome.com.tw/upload/images/20171219/20107576A1mEswQR5z.png](https://ithelp.ithome.com.tw/upload/images/20171219/20107576A1mEswQR5z.png)


## 停用詞列表

- [Python-in-5-days/10-2 中文斷詞-移除停用詞.md at master · allenyllee/Python-in-5-days](https://github.com/allenyllee/Python-in-5-days/blob/master/10-2%20%E4%B8%AD%E6%96%87%E6%96%B7%E8%A9%9E-%E7%A7%BB%E9%99%A4%E5%81%9C%E7%94%A8%E8%A9%9E.md)

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
