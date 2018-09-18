# Computer_Vision__資料收集

[toc]
<!-- toc --> 

## CNN heat map/activation maps/visuralizing

- [mrgloom/CNN-heatmap](https://github.com/mrgloom/CNN-heatmap)

- [Class activation maps in Keras for visualizing where deep learning networks pay attention](https://jacobgil.github.io/deeplearning/class-activation-maps)


## U-Net/V-Net

- [[1606.04797] V-Net: Fully Convolutional Neural Networks for Volumetric Medical Image Segmentation](https://arxiv.org/abs/1606.04797)

- [How to easily train a 3D U-Net or any other model for lung cancer segmentation.](https://medium.com/data-analysis-center/how-to-easily-train-a-3d-u-net-or-any-other-model-for-lung-cancer-segmentation-fc88f970d53)

- [「Deep Learning」V-Net - CSDN博客](https://blog.csdn.net/dgyuanshaofeng/article/details/78161987)

### NiftyNet

- [niftynet](http://niftynet.io/)

    >An open source convolutional neural networks platform for medical image analysis and image-guided therapy





## Loc2Vec

- [Loc2Vec: Learning location embeddings with triplet-loss networks | Sentiance](http://www.sentiance.com/2018/05/03/loc2vec-learning-location-embeddings-w-triplet-loss-networks/)

## 圖像分類

### Now anyone can train Imagenet in 18 minutes

- [Now anyone can train Imagenet in 18 minutes · fast.ai](http://www.fast.ai/2018/08/10/fastai-diu-imagenet/)



### 利用特權信息、語義信息和多源信息輔助基於網絡數據的學習

- [利用特權信息、語義信息和多源信息輔助基於網絡數據的學習 - 幫趣](http://bangqu.com/y34m49.html)

    > 傳統的機器學習尤其是深度學習，需要大量的標註數據，但是標註數據的獲取非常費時費力。考慮到每天都有大量的圖片和視頻被上傳到網上可供免費下載，爲了有效地避免由於標註數據不足帶來的對傳統機器學習模型的不利影響，我們利用互聯網上已有的、大量標註得比較粗糙的網絡圖片或視頻來訓練模型，用於物體識別、人體動作識別、視頻事件檢測等應用。
    > 
    > 然而，用網絡圖片或視頻來訓練模型存在諸多問題，比如：
    > 
    > > 1.網絡圖片或視頻標籤是由用戶提供的，非常不準確。有噪聲的訓練集對模型訓練有非常負面的影響；
    > >
    > > 2\. 網絡圖片視頻和測試集的圖片視頻在數據分佈上存在巨大差異，如果用網絡數據訓練模型，得到的模型在數據分佈差別很大的測試集上，效果會很不理想。
    > 
    > 但是，基於網絡數據學習也有一些優勢，比如：
    > 
    > > 1.網絡圖片和視頻通常會配有標籤、標題等文字信息，但測試圖片和視頻沒有這種文字信息。這種只有訓練數據有但測試數據沒有的信息稱爲特權信息 (privileged information)，我們可以利用特權信息來幫助訓練圖片或視頻的分類模型；
    > >
    > > 2\. 網絡上有可以免費獲得的語義信息，比如我們可以從維基百科上獲取每一個類別的語義信息，用來輔助訓練更魯棒的圖片或視頻的分類模型；
    > >
    > > 3\. 網絡數據具有多源性。不論是圖片還是視頻，我們都可以從很多不同的網站下載大量免費的數據，比如從 Google、Bing 上獲取圖片，從 YouTube、Flickr 中獲取視頻。然而，每一個數據源的數據分佈都會有很大的差異，因此如何利用多源網絡數據進行學習也是很重要的研究課題。
    > 
    > 爲了充分利用網絡數據的優勢，解決基於網絡數據學習中存在的關鍵問題，我們提出了一系列**基於網絡數據的學習方法，使得網絡圖片和視頻能被用於訓練更魯棒的模型，在物體識別、人體動作識別、視頻事件識別等應用上取得了很好的效果。**接下來就分別介紹如何利用上述網絡數據的三個優勢（特權信息、語義信息和多源信息）來解決基於網絡數據學習的兩大主要問題（標籤噪音和數據分佈差異）。
    > 
    > ### 一、 利用特權信息輔助基於網絡數據的學習
    > 
    > 爲了解決網絡數據的標籤噪音問題，我們參照多示例學習 (multi-instance learning) 把網絡圖片分成若干個包。對於二分類問題，我們用類名作爲關鍵詞可以搜索得到很多相關樣本，然後用其他關鍵詞搜索得到很多無關樣本。我們把相關樣本分成正包，無關樣本分成負包。我們只知道每個包的標籤，但不知道每個包裏面樣本的真實標籤。因而，我們對樣本的標籤做了如下假設：每個負包裏面的樣本都是負樣本，但對於每個正包，至少有一定比例的樣本是正樣本而其他是負樣本。其中提到的比例屬於先驗信息，可以根據實驗觀察人爲設定。根據以上假設，我們就可以提出多實例學習的模型來解決標籤噪音的問題。
    > 
    > 另外，我們同時使用特權信息來進一步減弱標籤噪音的影響。受 SVM+的啓發，我們用基於特權信息的損失函數 (loss function) 來代替多實例學習模型中的損失變量，從而用特權信息控制損失的大小。一般來說，在特權信息的約束下，噪音樣本的損失函數值較大，也就說我們允許它們的損失比較大；而非噪音樣本的損失函數值比較小，也就是說我們強制要求它們的損失比較小。綜上，我們將特權信息用於多種多示例學習方法，提出一種新的學習框架，如下圖所示。
    > 
    > ![利用特權信息、語義信息和多源信息輔助基於網絡數據的學習](http://i2.bangqu.com/lf1/news/20180718/5b46c6e76f4cc.jpg)
    > 
    > 在上述框架的基礎上，我們進一步解決網絡訓練數據和用戶測試數據的分佈性差異問題。我們給不同的訓練樣本分配不同的權重。具體來說，離測試數據中心比較近的被分配較高的權重，而離測試數據中心較遠的被分配較低的權重，從而拉近加權的訓練數據中心和測試數據中心的距離。經過公式推導，我們有一個有意思的發現：**對於每一個訓練樣本，它和訓練數據中心的相似度減去它和測試數據中心的相似度可以被看成另外一種特權信息。至此，我們將學習框架拓展爲可以同時解決基於網絡數據學習的兩大問題。**在實驗部分，我們用 Flickr 圖片或視頻作爲訓練集，在圖片分類、人體動作識別和視頻事件檢測的標準測試集上做了大量的實驗，結果證明了特權信息的有效性。我們的論文發表在 ECCV 2014 [1]，後來被拓展到 IJCV [2]。
    > 
    > ### 二、利用語義信息輔助基於網絡數據的學習
    > 
    > 在網上我們可以免費獲得每一種類別的語義信息 (semantic information)。比如給定一個類名，我們可以從它的維基主頁上抽取文本信息作爲該類別的語義信息，也可以用類名的詞向量 (word vector) 作爲該類別的語義信息。我們的方法建立在差分自編碼器 (variational auto-encoder (VAE)) 的基礎上，出於以下兩點考慮：**1\. 自編碼器可以用來檢測噪音；2. 自編碼器的隱藏層 (hidden layer) 可以加入語義信息。**
    > 
    > 我們方法的框架見下圖，分成上下兩個子網絡。下面的子網絡是 VAE，輸入是圖片的 CNN 特徵，輸出是重建概率，可以用來指示該圖片是不是噪音。具體來講，噪音的重建概率比較低而非噪音的重建概率比較高。上面的子網絡是分類器，輸入是類別的語義信息和 VAE 的隱藏變量，輸出是類別種類，這也相當於用分類器來約束 VAE 的隱藏層。在這種情況下，分類器和 VAE 可以聯合利用語義信息來抵制噪音。**從我們最終的目標函數可以看出，我們旨在減少加權的分類損失。具體來說，更可能是非噪音的圖片的損失被分配更高的權重，因爲非噪音的圖片對訓練魯棒的模型貢獻更大。**在訓練階段，我們訓練一個端到端的網絡以優化 CNN、VAE 和分類器的參數。在測試階段，我們輸入測試圖片和所有測試類別的語義信息，預測測試圖片的類別。 ![利用特權信息、語義信息和多源信息輔助基於網絡數據的學習](http://i2.bangqu.com/lf1/news/20180718/5b46c6f2af868.jpg)
    > 
    > 在上述網絡結構的基礎上，我們做了兩點改進用來解決網絡訓練數據和用戶測試數據的分佈性差異問題：
    > 
    > > -   首先，我們用 VAE 同時重建網絡訓練數據和無標籤的測試數據，該方法已被之前域遷移 (domain adaptation) 的論文證明有效。
    > >
    > >
    > > -   其次，我們用網絡訓練數據的隱藏變量 (hidden variable) 來重建測試數據的隱藏變量。
    > 
    > 具體來說，我們假設測試數據的隱藏變量可以由網絡訓練數據的隱藏變量線性表示，並且表示矩陣是低秩的。藉助低秩表示 (low-rank representation) 的學習方法，我們可以更新測試數據的隱藏變量並用更新後的數據重新預測。在實驗部分，我們用 Google 圖片作爲訓練集，在三個圖片分類的標準測試集上做測試。結果表明類別的語義信息可以輔助解決基於網絡數據學習的兩大問題。我們的論文發表在 CVPR 2018 [3]。
    > 
    > ### 三、 利用多源信息輔助基於網絡數據的學習
    > 
    > 網絡上的數據多模態且多源。比如圖片可以從 Google, Flickr, Bing 等網站下載，視頻可以從 Flickr, YouTube 等網站下載，並且從網上下載的圖片或視頻都帶有文本信息。從不同網站下載的數據有很大的分佈差異性。如果用網絡數據作爲訓練集，我們希望選取和測試集分佈比較接近的網絡源作爲訓練集，這樣訓練出來的模型在測試集上能取得更好的效果。所以我們想要在不同的網絡源上分配不同的權重，具體來講，給和測試集分佈比較接近的網絡源分配更高的權重。
    > 
    > 我們的流程圖如下，給定若干個網絡源，其中一部分是圖片源，另一部分是視頻源。我們從圖片中抽取 2D 視覺特徵，從視頻中抽取 3D 視覺特徵，從文本信息中抽取文本特徵，輸入到我們的學習模型。同時，我們的方法也需要輸入無標籤的測試視頻，從測試視頻中同時抽取 2D 視覺特徵和 3D 視覺特徵。基於視覺特徵，我們在每個源上訓練一個分類器。給定一個測試樣本，每個分類器會產生一個預測值。我們把所有的預測值加權平均，和測試樣本的標籤作比較。然而，測試樣本的標籤在訓練階段是未知的，所以我們還需要推斷測試樣本的僞標籤。**綜上，在訓練階段，我們需要同時學習每個源的權重，每個源上的分類器以及測試樣本的僞標籤。這樣就可以解決網絡訓練數據和用戶測試數據分佈的差異性問題。**
    > 
    > 在流程圖中，我們還可以看到所有的圖片和視頻都有附帶的文本信息。我們利用附帶的文本信息作爲特權信息來幫助解決網絡數據標籤噪音的問題。如何利用特權信息去噪已經在第一部分講過，技術細節比較相似，在此就不重複了。在實驗部分，我們把 Google 和 Bing 作爲圖片源，把 Flickr 作爲視頻源，在人體動作識別和視頻事件檢測的標準測試集上做了大量的實驗。實驗證明我們的方法可以更好地利用多模態多源的網絡數據。我們的論文發表在 CVPR 2013 [4]，然後拓展到 T-NNLS [5].
    > 
    > ![利用特權信息、語義信息和多源信息輔助基於網絡數據的學習](http://i2.bangqu.com/lf1/news/20180718/5b46c6e8c93b4.jpg)
    > 
    > ### 總結
    > 
    > **基於網絡數據學習存在兩大主要問題：標籤噪音和數據分佈差異性，所以和基於精確標註數據的學習相比在性能上仍有一定的差距。但是考慮到網絡數據的諸多優勢，基於網絡數據學習有着很大的提升空間和廣闊的應用前景。**在這篇文章中，我們結合過去嘗試的方法，講述瞭如何利用特權信息、語義信息和多源信息幫助解決基於網絡數據學習的主要問題。在未來工作中，我們會繼續探索如何充分利用網絡數據的優勢去提升基於網絡數據學習的性能，並把應用擴展到物體檢測，語義分割、文本和圖片的雙向檢索以及其他領域。
    > 


## 圖片相似性

### 使用 Spark, LSH 和 TensorFlow 檢測圖片相似性

- [使用 Spark, LSH 和 TensorFlow 檢測圖片相似性 - 幫趣](http://bangqu.com/io1Atb.html)

    > 按：本文爲 AI 研習社編譯的技術博客，原標題 Detecting image similarity using Spark, LSH and TensorFlow，作者爲 Andrey Gusev（Pinterest 工程師，內容質量分析師）。
    > 
    > 作爲一個視覺數據處理平臺，擁有從海量圖片中學習並理解其內容的能力是非常重要的。爲了檢測幾近重複的相似圖片，我們使用了一套基於 Spark 和 TensorFlow 的數據流處理系統------NearDup。這套系統的核心由一個使用 Spark 實現的批量化 LSH（locality-sensitive hashing，局部敏感哈希）搜索器和一個基於 TensorFlow 的分類器構成。這個數據流處理系統每天能夠比較上億個分析對象，並漸進式地完成各個圖像類別的信息更新。在本文中，我們將講解如何使用這項技術更好地理解海量圖片內容，從而使得我們產品前端界面的推薦內容和搜索結果具有更高的信息準確性、更大的數據密度。  
    > 
    > **簡介**
    > 
    > 我們將我們圖片庫中的所有圖片劃分爲不同的圖片類，每一類都由幾近相同（以人類觀察員的判斷爲標準）的圖片組成。這種分類標準有一定的主觀性，爲了給你一個感性認識，下圖展示了一些按照 NearDup 閾值進行圖片分類的例子。注意，這些相似圖片不一定來自同一圖像源（參見右下圖），也不一定有相同的背景（參見左下圖）。同時，圖像中可能包含一定的幾何扭曲（參見左上圖），或者旋轉、剪切和翻轉變化（見中心圖和右上圖）。
    > 
    > ![使用 Spark, LSH 和 TensorFlow 檢測圖片相似性](http://i2.bangqu.com/lf1/news/20180730/5b5ac432392e7.png)
    > 
    > 爲圖片庫中的所有圖片進行分類與劃分的過程在數學上無法進行嚴格定義與求解，這是因爲在 NearDup 系統中，圖片之間的關係不具有傳遞性和相等性。爲了說明這一點，我們可以想象將一張「貓」的圖片通過 1000 步慢慢地形變爲一張「狗」的圖片的過程。容易推斷，每一步微小形變前後的兩張圖片的相似度都將落入 NearDup 的閾值，從而將它們判斷爲「相似」圖片。然而，究竟該將這一串前後相似的圖片序列劃分爲哪幾類？貓類，狗類，還是貓-狗類？爲了解決這一問題，我們將問題模型轉化爲圖：圖的節點代表圖片，邊代表相應圖片間的相似度。隨後我們結合傳遞閉包法（ transitive closure ）和貪婪 k-cut 算法來最小化圖的 k-cut 劃分，從而近似求解整個圖片庫的最優劃分。
    > 
    > **使用批量化 LSH 進行數據預處理**
    > 
    > **嵌入和 LSH 對象**
    > 
    > 爲了理解圖片內容，我們將圖片轉換到一個嵌入向量空間（embedded vector space）中。這些圖嵌入向量是圖片的一種高維向量表示，能夠抓取圖片的視覺和語義相似性。它們一般通過神經網絡架構如 VGG16 或 Inception 等處理生成。爲了在 NearDup 系統中處理圖片關係並對圖片庫進行分類，我們每天要比較幾千萬張新圖片，並將它們分類到上億個圖片類別中。如果沒有優化措施，如此大規模的近鄰搜索（nearest neighbor search）問題的時間複雜度爲平方（quadratic）複雜度，相應的計算時間將正比於甚至超過 10 個 quadrillion 秒（1 後面 16 個 0！）。爲此，我們通過將圖嵌入向量進一步縮減爲 LSH 對象的方法，顯著縮小了問題規模，降低了處理難度。
    > 
    > LSH 是一種先進的數據降維技術，降維前後數據點之間的距離關係保持不變。原向量空間首先通過隨機投影法（random projection）和位抽樣 LSH（bit sampling LSH）法進行一定的降維。隨後，我們繼續將所得到的向量位分組爲多個 LSH 對象，分組過程有效地權衡了檢測準確率和計算時間這一矛盾體。分組越精細，進行最近鄰搜索的計算複雜度將越高，但檢測準確率也將越高。這裏，我們使用 LSH 對象之間的 Jaccard 重合度來近似表示原向量空間中相應向量間的餘弦相似度。
    > 
    > **批量 LSH 搜索**
    > 
    > 當所有圖片都用一組 LSH 對象表示之後，我們繼續爲它們建立反向索引，並實現對所有圖片的批量查詢與搜索。從頂層看，我們通過函數式轉換法（functional transformation）、壓縮式反向索引與連接法（compressed inverted indexes and joins）等方法的結合，來實現對所有圖片的一次性批量查詢與比較。這個數據流處理過程是用 Spark 實現的，並需要藉助一系列的優化措施來進一步保證這些海量數據能夠轉化到儘量簡單有效地的LSH 對象空間中進行處理。我們所使用到的主要優化措施包括：
    > 
    > -   **字典編碼**（ Dictionary encoding ） 使得所有數據都用具有最短寬度的數值進行表示
    > 
    > -   **可變字節編碼**（ Variable byte encoding ） 被用於所有的反向索引
    > 
    > -   **索引切分**（ Index partitioning ） 提高了反向索引的平衡性
    > 
    > -   **基於代價的優化器**（ Cost-based optimizer ） 能夠檢測嵌入向量空間的密度，並計算最優的運行時參數
    > 
    > -   **原始數據堆排**（ Primitive data packing ） 進一步提高了內存使用率
    > 
    > -   **Jaccard 重合度計數**（ Jaccard overlap counting ） 基於低層次、高性能的數據收集實現
    > 
    > -   **去堆化**（ Off heaping ） 減少了垃圾回收（GC）過載
    > 
    > **使用遷移學習的候選選擇**
    > 
    > 批量化LSH是產生高查全率（召回率）同時又能最小化計算成本的一個很效果的方法。但是，它通常不會對候選項產生最優的查準率（準確率）和排序。我們通過使用一個有監督的分類器去挑選那些NearDups 認爲足夠相似的候選項。這個分類器是一個遷移學習在視覺嵌入上的例子。它使用了Tensorflow 前饋網絡和一個 Adam 優化器 。我們已經在超過包含10億不同對圖像的樣本集中訓練了分類器。訓練集由決策樹分類器在SURF 視覺特徵上的輸出得到，並進行了幾何驗證，然後用於NearDup 系統的先前迭代。爲了提高學習和每一對圖像的收斂性，將 hamming 碼字節進行異或運算後輸入到輸入層。該分類器被調整到很高的準確率並且在人類標記的樣本上達到了 99% 以上準確率。
    > 
    > SparkContext 也可以對訓練過的網絡進行推斷。使用 mapPartitions 和分組範式，我們可以使用預定義好尺寸的大批數據去有效地向量化和減少開銷。在一個擁有1000萬個參數的網絡中，我們在一個r3.8xlarge 的機器集羣上實現了平均2ms進行一個預測的速率。
    > 
    > **結論**
    > 
    > NearDup 檢測需要進行計算代價很高的兩兩比較。通過在Spark 中使用批處理LSH實現，我們通過跳過不太相似的圖像對大大降低了計算的複雜度。Spark-based 的實現結合了高效的工作負載分配和低層次的優化，以最小化內存和CPU佔用。隨後的調優步驟使用了一個有監督的前饋網絡來選擇和排序高於NearDup 相似性閾值的圖相對。Spark 和Tensorflow 的推斷結合使用了分佈式計算和每個內核矢量化的最佳特性，實現了高吞吐量和低延遲的預測。然後，將這兩個步驟的結果用於集羣圖像，每天幫助提供數百億的搜索結果和在Pinterest 上的推薦。
    > 
    > 欲瞭解更多關於這個問題的信息，請看我在 Spark+AI Summit 2018 的演講。<https://vimeo.com/274629687>
    > 
    > **致謝**：感謝以下團隊成員對本項目的所有貢獻：Jiajing Xu, Vitaliy Kulikov, Jooseong Kim, Peter John Daoud, Andrew Zhai, Matthew Fang, Kevin Lau, Jacob Hanger, Zhuoyuan Li and Chao Wang
    > 
    > 原文鏈接：<https://medium.com/@Pinterest_Engineering/detecting-image-similarity-using-spark-lsh-and-tensorflow-618636afc939>




## 圖片壓縮

- [體積減半畫質翻倍，他用TensorFlow實現了這個圖像極度壓縮模型 - 幫趣](http://bangqu.com/u62hD2.html)

    - [[1804.02958] Generative Adversarial Networks for Extreme Learned Image Compression](https://arxiv.org/abs/1804.02958)
    - [Justin-Tan/generative-compression: TensorFlow Implementation of Generative Adversarial Networks for Extreme Learned Image Compression](https://github.com/Justin-Tan/generative-compression)


## 超解析度

- [阿里巴巴Poster論文：處理多種退化類型的卷積超分辨率 | CVPR 2018 - 幫趣](http://bangqu.com/kjzIo2.html#utm_source=Facebook_PicSee&utm_medium=Social)



## 圖片去噪/低亮度

- [無需額外硬件，全卷積網絡讓機器學習學會夜視能力 - 幫趣](http://bangqu.com/l1KYa5.html)

    - [[1805.01934] Learning to See in the Dark](https://arxiv.org/abs/1805.01934)


- [英偉達提出僅使用噪點圖像訓練的圖像增強方法，可去除照片噪點 - 幫趣](http://bangqu.com/318F5u.html#utm_source=Facebook_PicSee&utm_medium=Social)

    - [[1803.04189] Noise2Noise: Learning Image Restoration without Clean Data](https://arxiv.org/abs/1803.04189)

    > ![](http://i2.bangqu.com/j/news/20180711/318F5u153127800767996f71.png)
    > 
    > ![](http://i2.bangqu.com/j/news/20180711/318F5u1531278013816V3CBF.png)

    >看完這篇有種「江湖一點訣，點破不值錢的感覺。」但也提醒我們 Loss function 的重要。特別是，根據data 中noise 的特性可能需要重新設計一個 Loss function。
    > [name=Ya-Lun Li]


## 文字辨識(OCR)

- [Deep Learning based Text Recognition (OCR) using Tesseract and OpenCV | Learn OpenCV](https://www.learnopencv.com/deep-learning-based-text-recognition-ocr-using-tesseract-and-opencv/)

    > In today’s post, we will learn how to recognize text in images using an open source tool called Tesseract and OpenCV. The method of extracting text from images is also called Optical Character Recognition (OCR) or sometimes simply text recognition.
    > 


## 慢動作

### Super SlowMO

- [Super SloMo: High Quality Estimation of Multiple Intermediate Frames for Video Interpolation](https://people.cs.umass.edu/~hzjiang//projects/superslomo/)

    <iframe width="560" height="315" src="https://www.youtube.com/embed/MjViy6kyiqs" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

    <iframe width="560" height="315" src="https://www.youtube.com/embed/LBezOcnNJ68" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe> 




## 語意分割

### Flood-filling-network(FFN) 繪製腦神經

- [[1611.00421] Flood-Filling Networks](https://arxiv.org/abs/1611.00421)

    >  ![](https://screenshotscdn.firefoxusercontent.com/images/739f39fc-90e4-4030-811a-3b9aa0b17e51.png)
    >     

- [High-precision automated reconstruction of neurons with flood-filling networks | Nature Methods](https://www.nature.com/articles/s41592-018-0049-4)

    - [High-Precision Automated Reconstruction of Neurons with Flood-filling Networks | bioRxiv](https://www.biorxiv.org/content/early/2017/10/09/200675)

    - [Google AI Blog: Improving Connectomics by an Order of Magnitude](https://ai.googleblog.com/2018/07/improving-connectomics-by-order-of.html)

    - [谷歌AI腦神經元繪製法登上Nature子刊：速度提升一個數量級 - 幫趣](http://bangqu.com/1UI64u.html#utm_source=Facebook_PicSee&utm_medium=Social)

    > ![](https://1.bp.blogspot.com/-GvN3s9zAd2E/WzQamIoyrMI/AAAAAAAADGU/UqSwCwOw7XQuBkk3iJQEpiHMRmEpt-hvgCLcBGAs/s640/image3.gif)
    > 
    > ![](https://screenshotscdn.firefoxusercontent.com/images/61719d10-4975-4cb3-a340-47810a27920c.png)


### 基於光流法的語義分割

- [[1807.05636] Cross Pixel Optical Flow Similarity for Self-Supervised Learning](https://arxiv.org/abs/1807.05636)

    > In this paper, we consider the case of self-supervision using motion cues to learn  a  Convolutional  Neural  Network  (CNN)  for  static  images.  Here,  a  deep network is trained to predict, from a single video frame, how the image could change over time. Since predicted changes can be verified automatically by looking at the actual video stream, this approach can be used for self-supervision.Furthermore, predicting motion may induce a deep network to learn about objects in images. The reason is that objects are a major cause of motion regularity and hence predictability: pixels that belong to the same object are much more likely to “move together” than pixels that do not.
    > 
    > Besides giving cues about objects, motion has another appealing characteristic compared to other signals for self-supervision. Many other methods are, in fact, based on destroying information in images (e.g. by removing color, scrambling parts) and then tasking a network with undoing such changes. This has the disadvantage of learning the representation on distorted images (e.g. gray scale). On the other hand, extracting a single frame from a video can be thought of as removing information only along the temporal dimension and allows one to learn the network on undistorted images.
    > 
    > There is however a key challenge in using motion for self-supervision: ambiguity. Even if the deep network can correctly identify all objects in an image, this is still not enough to predict the specific direction and intensity of the objects’ motion in the video, given just a single frame. This ambiguity makes the direct  prediction  of  the  appearance  of  future  frames  particularly  challenging, and overall an overkill if the goal is to learn a good general-purpose image representation for image analysis. Instead, the previous most effective method for self-supervision using motion cues [2] is based on first extracting motion tubes from videos (using off-the-shelf optical flow and motion tube segmentation algorithms) and then training the deep network to predict the resulting per-frame segments rather than motion directly. Thus they map a complex self-supervision task into one of classic foreground-background segmentation.
    > 
    > While the approach of [2] sidesteps the difficult problem of motion prediction  ambiguity,  it  comes  at  the  cost  of  pre-processing  videos  using  a  complex handcrafted motion segmentation pipeline, which includes many heuristics and tunable parameters. In this paper, we instead propose a new method that can ingest cues from optical flow directly.
    > 
    > Our method, presented in section 3 and illustrated in fig. 1, is based on a new cross pixel flow similarity loss layer. As noted above, the key challenge is that  specific  details  about  the  motion,  such  as  its  direction  and  velocity,  are usually difficult if not impossible to predict from a single frame. We address this difficulty  in  two  ways.  First,  we  learn  to  embed  pixels  into  vectors  that  cluster together when the model believes that the corresponding pixels are likely to move together. This is obtained by encouraging the inner product of the learned pixel embeddings to correlate with the similarity between their corresponding optical flow vectors. This does not require the model to explicitly estimate specific motion directions or velocities. However, this is still not sufficient to address the ambiguity completely; in fact, while different objects may be able to move independently, they may not do so all the time. For example, often objects stand still, so their velocities are all zero grouping them together in optical flow. We addressed this second challenge by using a robust loss that captures pixel grouping probabilistically
    > rather than deterministically.
    > 
    > In section 4 we extensively validate our model against other self-supervised learning approaches. First, we show that our approach works as well or better than  [2], establishing  a  new  state-of-the-art  method  for  self-supervision  using motion cues. Second, to put this into context, we also compare the results to all recent approaches for self-supervision that use cues other than motion. In this case, we show that our approach has state-of-the-art performance for semantic image segmentation.
    > 
    > The overall conclusion (section 5) is that our method significantly simplifies leveraging motion cues for self-supervision and does better than existing alternatives  for  this  modality;  it  is  also competitive  with  self-supervision  methods that use other cues, making motion a sensible choice for self-supervision by itself or in combination with other cues [1].
    > 
    > 

### 什麼是光流法

- [光流法 - Wikiwand](https://www.wikiwand.com/zh/%E5%85%89%E6%B5%81%E6%B3%95)

    > 光流的测算
    > -----
    > 
    > 光流法实际是通过检测图像像素点的强度随时间的变化进而推断出物体移动速度及方向的方法。
    > 
    > 在 2D+*t* 维的情况下（3D 和更高维度亦然），假设位于 ![{\displaystyle (x,y,t)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/762804ec2b0ecb79e3259d7ce5e8a79fa07ecbf0) 的[体素](https://www.wikiwand.com/zh/%E4%BD%93%E7%B4%A0 "体素")的亮度是 ![{\displaystyle I(x,y,t)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/943e368e17aa82dd32682aa0a2f44fc544c5268d)。该体素在两个图像帧之间移动了 ![\Delta x](https://wikimedia.org/api/rest_v1/media/math/render/svg/f3890eb866b6258d7a304fc34c70ee3fb3a81a70)、![\Delta y](https://wikimedia.org/api/rest_v1/media/math/render/svg/7caae142d915be8ef4d8c423bf91d1f6ea10e8e0)、![\Delta t](https://wikimedia.org/api/rest_v1/media/math/render/svg/8c28867ecd34e2caed12cf38feadf6a81a7ee542)。于是可以得出一个亮度相同的结论：
    > 
    > ![{\displaystyle I(x,y,t)=I(x+\Delta x,y+\Delta y,t+\Delta t)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ddbed7a05ee486795f8df25b6b63814670baed54)
    > 
    > 假设该移动很小，那么可以根据[泰勒级数](https://www.wikiwand.com/zh/%E6%B3%B0%E5%8B%92%E7%BA%A7%E6%95%B0)得出：
    > 
    > ![{\displaystyle I(x+\Delta x,y+\Delta y,t+\Delta t)=I(x,y,t)+{\frac {\partial I}{\partial x))\Delta x+{\frac {\partial I}{\partial y))\Delta y+{\frac {\partial I}{\partial t))\Delta t+}](https://wikimedia.org/api/rest_v1/media/math/render/svg/749d10ea42b4fb5f9955342d8e294bed10b7c8fd)[H.O.T.](https://www.wikiwand.com/zh/%E6%91%84%E5%8A%A8%E7%90%86%E8%AE%BA)
    > 
    > 因此可以推出：
    > 
    > ![{\displaystyle {\frac {\partial I}{\partial x))\Delta x+{\frac {\partial I}{\partial y))\Delta y+{\frac {\partial I}{\partial t))\Delta t=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6fc4d94f9188324981bba2067476e684467e782d)
    > 
    > 或
    > 
    > ![{\displaystyle {\frac {\partial I}{\partial x)){\frac {\Delta x}{\Delta t))+{\frac {\partial I}{\partial y)){\frac {\Delta y}{\Delta t))+{\frac {\partial I}{\partial t)){\frac {\Delta t}{\Delta t))=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bdc292eb494006ef921415bfd9659debcf3b9a05)
    > 
    > 最终可得出结论：
    > 
    > ![{\displaystyle {\frac {\partial I}{\partial x))V_{x}+{\frac {\partial I}{\partial y))V_{y}+{\frac {\partial I}{\partial t))=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dcea639f5b077f0b62fb6b3e80cac328371a197b)
    > 
    > 这里的 ![{\displaystyle V_{x},V_{y))](https://wikimedia.org/api/rest_v1/media/math/render/svg/21998e0b2d26cb691f3f2f19394bc5f5787f3a06) 是 ![x](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) 和 ![y](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) 方向上的速率，或称为 ![{\displaystyle I(x,y,t)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/943e368e17aa82dd32682aa0a2f44fc544c5268d) 的光流。而 ![{\displaystyle {\tfrac {\partial I}{\partial x))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cc9a3135c6f690d3bac59164e7ffdd94a8e134ea), ![{\displaystyle {\tfrac {\partial I}{\partial y))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/824a2c1da4733074d8ce7b1c70882799080d9463) 和 ![{\displaystyle {\tfrac {\partial I}{\partial t))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/64b817827ab67c30ca91a3d7c0049bde9ae00ad6) 则是图像 ![{\displaystyle (x,y,t)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/762804ec2b0ecb79e3259d7ce5e8a79fa07ecbf0) 在对应方向上的[偏导数](https://www.wikiwand.com/zh/%E5%81%8F%E5%AF%BC%E6%95%B0)。![{\displaystyle I_{x))](https://wikimedia.org/api/rest_v1/media/math/render/svg/eed0dfcd8b1ce6eb2e6b7fbc426b895507d53004)、![{\displaystyle I_{y))](https://wikimedia.org/api/rest_v1/media/math/render/svg/6f3eedd0871fd35e1fd8992c53812cd60d1b07c2) 和 ![{\displaystyle I_{t))](https://wikimedia.org/api/rest_v1/media/math/render/svg/fc386d951e8ffae76357542f14e160621e6668b1) 的关系可用下式表述：
    > 
    > ![{\displaystyle I_{x}V_{x}+I_{y}V_{y}=-I_{t))](https://wikimedia.org/api/rest_v1/media/math/render/svg/262f48c446773db9697b0c4e4b025c6688b755e0)
    > 
    > 或
    > 
    > ![{\displaystyle \nabla I^{T}\cdot {\vec {V))=-I_{t))](https://wikimedia.org/api/rest_v1/media/math/render/svg/f462cbf95a9714d36e0801425adea4ea840b3da0)
    > 
    > 




## 熱力圖

- [凭什么相信你，我的CNN模型？（篇一：CAM和Grad-CAM)](https://bindog.github.io/blog/2018/02/10/model-explanation/)

    > ## 0x01 反卷积和导向反向传播
    > 
    > 关于CNN模型的可解释问题，很早就有人开始研究了，姑且称之为CNN可视化吧。比较经典的有两个方法，反卷积(Deconvolution)和导向反向传播(Guided-backpropagation)，通过它们，我们能够一定程度上“看到”CNN模型中较深的卷积层所学习到的一些特征。当然这两个方法也衍生出了其他很多用途，以反卷积为例，它在图像语义分割中有着非常重要的作用。从本质上说，反卷积和导向反向传播的基础都是反向传播，其实说白了就是对输入进行求导，三者唯一的区别在于反向传播过程中经过ReLU层时对梯度的不同处理策略。在这篇[论文](https://arxiv.org/pdf/1412.6806.pdf)中有着非常详细的说明，如下图所示：
    > 
    > ![diff](http://lc-cf2bfs1v.cn-n1.lcfile.com/eec03f3347b4bbfe2c9e.png)
    > 
    > 虽然过程上的区别看起来没有非常微小，但是在最终的效果上却有很大差别。如下图所示：
    > 
    > ![compare_effect](http://lc-cf2bfs1v.cn-n1.lcfile.com/d3a78959f7bd98e45484.png)
    > 
    > 使用普通的反向传播得到的图像噪声较多，基本看不出模型的学到了什么东西。使用反卷积可以大概看清楚猫和狗的轮廓，但是有大量噪声在物体以外的位置上。导向反向传播基本上没有噪声，特征很明显的集中猫和狗的身体部位上。
    > 
    > 虽然借助反卷积和导向反向传播我们“看到”了CNN模型神秘的内部，但是却并不能拿来解释分类的结果，因为它们对类别并不敏感，直接把所有能提取的特征都展示出来了。在刚才的图片中，模型给出的分类结果是猫，但是通过反卷积和导向反向传播展示出来的结果却同时包括了狗的轮廓。换句话说，我们并不知道模型到底是通过哪块区域判断出当前图片是一只猫的。要解决这个问题，我们必须考虑其他办法。
    > 
    > ---
    > 
    > ## 0x02 CAM
    > 
    > 大家在电视上应该都看过热成像仪生成的图像，就像下面这张图片。
    > 
    > ![热成像仪](http://lc-cf2bfs1v.cn-n1.lcfile.com/b1d76465decdfdd82485.jpg)
    > 
    > 图像中动物或人因为散发出热量，所以能够清楚的被看到。接下来要介绍的CAM(Class Activation Mapping)产生的CAM图与之类似，当我们需要模型解释其分类的原因时，它以热力图（Saliency Map，我不知道怎么翻译最适合，叫热力图比较直观一点）的形式展示它的决策依据，如同在黑夜中告诉我们哪有发热的物体。
    > 
    > 对一个深层的卷积神经网络而言，通过多次卷积和池化以后，它的最后一层卷积层包含了最丰富的空间和语义信息，再往下就是全连接层和softmax层了，其中所包含的信息都是人类难以理解的，很难以可视化的方式展示出来。所以说，要让卷积神经网络的对其分类结果给出一个合理解释，必须要充分利用好最后一个卷积层。
    > 
    > ![CNN](http://lc-cf2bfs1v.cn-n1.lcfile.com/75fc645a087a1c3e6548.png)
    > 
    > CAM借鉴了很著名的论文*[Network in Network](https://arxiv.org/abs/1312.4400)*中的思路，利用GAP(Global Average Pooling)替换掉了全连接层。可以把GAP视为一个特殊的average pool层，只不过其pool size和整个特征图一样大，其实说白了就是求每张特征图所有像素的均值。
    > 
    > ![CNN_GAP](http://lc-cf2bfs1v.cn-n1.lcfile.com/e4a636f667f277cedc74.png)
    > 
    > GAP的优点在NIN的论文中说的很明确了：由于没有了全连接层，输入就不用固定大小了，因此可支持任意大小的输入；此外，引入GAP更充分的利用了空间信息，且没有了全连接层的各种参数，鲁棒性强，也不容易产生过拟合；还有很重要的一点是，在最后的 mlpconv层(也就是最后一层卷积层)强制生成了和目标类别数量一致的特征图，经过GAP以后再通过softmax层得到结果，这样做就给每个特征图赋予了很明确的意义，也就是categories confidence maps。如果你当时不理解这个categories confidence maps是个什么东西，结合CAM应该就能很快理解。
    > 
    > 我们重点看下经过GAP之后与输出层的连接关系(暂不考虑softmax层)，实质上也是就是个全连接层，只不过没有了偏置项，如图所示：
    > 
    > ![GAP_output](http://lc-cf2bfs1v.cn-n1.lcfile.com/2173d395c485a58a4b66.png)
    > 
    > 从图中可以看到，经过GAP之后，我们得到了最后一个卷积层每个特征图的均值，通过加权和得到输出(实际中是softmax层的输入)。需要注意的是，对每一个类别C，每个特征图k的均值都有一个对应的w，记为wck。CAM的基本结构就是这样了，下面就是和普通的CNN模型一样训练就可以了。训练完成后才是重头戏：我们如何得到一个用于解释分类结果的热力图呢？其实非常简单，比如说我们要解释为什么分类的结果是羊驼，我们把羊驼这个类别对应的所有wck
    > 
    > 取出来，求出它们与自己对应的特征图的加权和即可。由于这个结果的大小和特征图是一致的，我们需要对它进行上采样，叠加到原图上去，如下所示。
    > 
    > ![heatmap_sum](http://lc-cf2bfs1v.cn-n1.lcfile.com/42e1796d2fab354daf80.png)
    > 
    > 这样，CAM以热力图的形式告诉了我们，模型是重点通过哪些像素确定这个图片是羊驼了。
    > 
    > ---
    > 
    > ## 0x03 Grad-CAM方法
    > 
    > 
    > 前面看到CAM的解释效果已经很不错了，但是它有一个致使伤，就是它要求修改原模型的结构，导致需要重新训练该模型，这大大限制了它的使用场景。如果模型已经上线了，或着训练的成本非常高，我们几乎是不可能为了它重新训练的。于是乎，Grad-CAM横空出世，解决了这个问题。
    > 
    > Grad-CAM的基本思路和CAM是一致的，也是通过得到每对特征图对应的权重，最后求一个加权和。但是它与CAM的主要区别在于求权重wck
    > 
    > 的过程。CAM通过替换全连接层为GAP层，重新训练得到权重，而Grad-CAM另辟蹊径，用梯度的全局平均来计算权重。事实上，经过严格的数学推导，Grad-CAM与CAM计算出来的权重是等价的。为了和CAM的权重做区分，定义Grad-CAM中第k个特征图对类别c的权重为αck
    > 
    > ，可通过下面的公式计算：
    > 
    > αck=1Z∑i∑j∂yc∂Akij
    > 
    > 其中，Z
    > 
    > 为特征图的像素个数，yc是对应类别c的分数（在代码中一般用logits表示，是输入softmax层之前的值），Akij表示第k个特征图中，(i,j)
    > 
    > 位置处的像素值。求得类别对所有特征图的权重后，求其加权和就可以得到热力图。
    > 
    > LcGrad-CAM=ReLU(∑kαckAk)
    > 
    > Grad-CAM的整体结构如下图所示：
    > 
    > ![Grad-CAM结构](http://lc-cf2bfs1v.cn-n1.lcfile.com/531c1d38e0a0ddaf9553.jpg)
    > 
    > 注意这里和CAM的另一个区别是，Grad-CAM对最终的加权和加了一个ReLU，加这么一层ReLU的原因在于我们只关心**对类别c**
    > 
    > **有正影响的那些像素点**，如果不加ReLU层，最终可能会带入一些属于其它类别的像素，从而影响解释的效果。使用Grad-CAM对分类结果进行解释的效果如下图所示：
    > 
    > ![effect1](http://lc-cf2bfs1v.cn-n1.lcfile.com/2318799bf6bcc13e5218.png)
    > 
    > 除了直接生成热力图对分类结果进行解释，Grad-CAM还可以与其他经典的模型解释方法如导向反向传播相结合，得到更细致的解释。
    > 
    > ![effect2](http://lc-cf2bfs1v.cn-n1.lcfile.com/9c1076aee75f1d4a98ef.png)
    > 
    > 这样就很好的解决了反卷积和导向反向传播对类别不敏感的问题。当然，Grad-CAM的神奇之处还不仅仅局限在对图片分类的解释上，任何与图像相关的深度学习任务，只要用到了CNN，就可以用Grad-CAM进行解释，如图像描述(Image Captioning)，视觉问答(Visual Question Answering)等，所需要做的只不过是把yc
    > 
    > 换为对应模型中的那个值即可。限于篇幅，本文就不展开了，更多细节，强烈建议大家去读读[论文](https://arxiv.org/abs/1610.02391)，包括Grad-CAM与CAM权重等价的证明也在论文中。如果你只是想在自己的模型中使用Grad-CAM，可以参考这个[链接](https://github.com/Ankush96/grad-cam.tensorflow)，熟悉tensorflow的话实现起来真的非常简单，一看就明白。
    > 
    > ---
    > 
    > ## 0x04 扩展
    > 
    > 其实无论是CAM还是Grad-CAM，除了用来对模型的预测结果作解释外，还有一个非常重要的功能：就是用于物体检测。大家都知道现在物体检测是一个非常热门的方向，它要求在一张图片中准确的识别出多个物体，同时用方框将其框起来。物体检测对训练数据量的要求是非常高的，目前常被大家使用的有 PASCAL、COCO，如果需要更多数据，或者想要识别的物体在这些数据库中没有话，那就只能人工来进行标注了，工作量可想而知。
    > 
    > 仔细想想我们不难发现，Grad-CAM在给出解释的同时，不正好完成了标注物体位置的工作吗？虽然其标注的位置不一定非常精确，也不一定完整覆盖到物体的每一个像素。但只要有这样一个大致的信息，我们就可以得到物体的位置，更具有诱惑力的是，我们不需要人工标注的方框就可以做到了。
    > 
    > 顺便吐槽下当前比较火的几个物体检测模型如Faster-RCNN、SSD等，无一例外都有一个Region Proposal阶段，相当于“胡乱”在图片中画各种大小的方框，然后再来判断方框中是否有物体存在。虽然效果很好，但是根本就是违背人类直觉的。相比之下，Grad-CAM这种定位方式似乎更符合人类的直觉。当然这些纯属我个人的瞎扯，业务场景中SSD还是非常好用的，肯定要比Grad-CAM这种弱监督条件下的定位要强的多。
    > 
    > 

### Deconvolution

- [[1311.2901] Visualizing and Understanding Convolutional Networks](https://arxiv.org/abs/1311.2901)

### Guided-backpropagation

- [[1412.6806] Striving for Simplicity: The All Convolutional Net](https://arxiv.org/abs/1412.6806)

### CAM

- [[1512.04150] Learning Deep Features for Discriminative Localization](https://arxiv.org/abs/1512.04150)

### Grad-CAM

- [[1610.02391] Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization](https://arxiv.org/abs/1610.02391)

### Grad-CAM++

- [[1710.11063] Grad-CAM++: Generalized Gradient-based Visual Explanations for Deep Convolutional Networks](https://arxiv.org/abs/1710.11063)



