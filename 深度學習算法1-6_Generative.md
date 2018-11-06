# 深度學習算法1-6_Generative

[toc]
<!-- toc --> 

## 圖片生成

### VAE

- [Variational Autoencoders Explained](http://kvfrans.com/variational-autoencoders-explained/)
    
    - [[1312.6114] Auto-Encoding Variational Bayes](https://arxiv.org/abs/1312.6114)
    
    - [VAE(Variational Autoencoder)的原理 - Shiyu_Huang - 博客园](https://www.cnblogs.com/huangshiyu13/p/6209016.html)

    > In an autoencoder, we add in another component that takes in the original images and encodes them into vectors for us. The deconvolutional layers then "decode" the vectors back to the original images.
    > 
    > ![](http://kvfrans.com/content/images/2016/08/autoenc.jpg)
    > 
    > We've finally reached a stage where our model has some hint of a practical use. We can train our network on as many images as we want. If we save the encoded vector of an image, we can reconstruct it later by passing it into the decoder portion. What we have is the standard autoencoder.
    > 
    > However, we're trying to build a generative model here, not just a fuzzy data structure that can "memorize" images. We can't generate anything yet, since we don't know how to create latent vectors other than encoding them from images.
    >
    > ---
    > 
    > We let the network decide this itself. For our loss term, we sum up two separate losses: the generative loss, which is a mean squared error that measures how accurately the network reconstructed the images, and a latent loss, which is the KL divergence that measures how closely the latent variables match a unit gaussian.
    > 
    > ```
    > generation_loss = mean(square(generated_image - real_image))
    > latent_loss = KL-Divergence(latent_variable, unit_gaussian)
    > loss = generation_loss + latent_loss
    > ```
    > 
    > In order to optimize the KL divergence, we need to apply a simple reparameterization trick: instead of the encoder generating a vector of real values, it will generate a vector of means and a vector of standard deviations.
    > 
    > ---
    > 
    > ![](http://kvfrans.com/content/images/2016/08/vae.jpg)
    > 
    > Let's say you were given a bunch of pairs of real numbers between [0, 10], along with a name. For example, 5.43 means apple, and 5.44 means banana. When someone gives you the number 5.43, you know for sure they are talking about an apple. We can essentially encode infinite information this way, since there's no limit on how many different real numbers we can have between [0, 10].
    > 
    > However, what if there was a gaussian noise of one added every time someone tried to tell you a number? Now when you receive the number 5.43, the original number could have been anywhere around [4.4 ~ 6.4], so the other person could just as well have meant banana (5.44).
    > 
    > The greater standard deviation on the noise added, the less information we can pass using that one variable.
    > 
    > Now we can apply this same logic to the latent variable passed between the encoder and decoder. The more efficiently we can encode the original image, the higher we can raise the standard deviation on our gaussian until it reaches one.



### CVE-GAN

- [漫談生成模型，從AE到CVAE-GAN - 幫趣](http://bangqu.com/7yE1f6.html#utm_source=Facebook_PicSee&utm_medium=Social)
    - [[1703.10155v1] CVAE-GAN: Fine-Grained Image Generation through Asymmetric Training](https://arxiv.org/abs/1703.10155v1)

    > 它有 4 大組件，對應到 4 個神經網絡，互爲補充，互相促進： 
    > 
    > *   E：編碼器（Encoder），輸入圖像 x，輸出編碼 z。
    > 
    >     如果還給定了類別 c，那麼生成的 z 就會質量更高，即更隨機，因爲可移除c中已包含的信息。
    > 
    > -   G：生成器（Generator）。輸入編碼 z，輸出圖像 x。
    > 
    >     如果還給定了類別 c，那麼就會生成屬於類別 c 的圖像。
    > 
    > -   C：分類器（Classifier）。輸入圖像 x，輸出所屬類別 c。這是我們的老朋友。
    > 
    > -   D：辨別器（Discriminator）。輸入圖像 x，判斷它的真實度。
    > 
    > 
    > 我們先看如果只使用部分組件會是怎樣。首先是 CVAE，如下圖所示：
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f615287833141444NYmU.png)
    > 
    > 然後是 CGAN，其中 y 代表對於真實度的判別，如下圖所示： 
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f615287833149608p5TH.png)
    > 
    > 它們的效果如下圖所示。
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f61528783315326X13z5.png)
    > 
    > 可見： 
    > 
    > -   CVAE 生成的圖像中規中矩，但是模糊。
    > 
    > -   CGAN 生成的圖像清晰，但有時會有明顯錯誤。
    > 
    > 所以 AE 和 GAN 的方法剛好是互補。 
    > 
    > CVAE-GAN 的架構如下圖所示：
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f61528783317230u9w9y.png)
    > 
    > 其中的 G 有 3 個主要目標： 
    > 
    > -   對於從 x 生成的 z，G 應能還原出接近 x 的 x'（像素上的接近）。這來自 AE 的思想。
    > 
    > -   G 生成的圖像應可由 D 鑑別爲屬於真實圖像。這來自 GAN 的思想。
    > 
    > -   G 生成的圖像應可由 C 鑑別爲屬於 c 類別。這與 InfoGAN 的思想有些相似。
    > 
    > 最終得到的 z 可相當好地刻畫圖像。例如，同樣的 z 在不同 c 下的效果如下圖所示。
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f61528783317884d633g.png)
    > 
    > 這裏的不同 c，代表不同的明星。相同的 z，代表其他的一切語義特徵（如表情，角度，光照等等）都一模一樣。
    > 
    > 於是，通過保持 z，改變 c，可輕鬆實現真實的換臉效果，如下圖所示。
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f6152878331967516B73.png)
    > 
    > CVAE-GAN 在語義插值上的效果也很出色，如下圖所示。
    > 
    > ![](http://i2.bangqu.com/j/news/20180612/7yE1f6152878332247033Vla.png)
    > 
    > 由於 CVAE-GAN 生成的樣本質量很高，還可用於增強訓練樣本集，使其他模型（如圖像分類網絡）得到更好的效果。


### SAGAN 自注意生成式對抗網絡

- [帶自注意力機制的生成對抗網絡，實現效果怎樣？ - 幫趣](http://bangqu.com/8833oT.html#utm_source=Facebook_PicSee&utm_medium=Social)

    > 在這個實現中，自注意機制會應用到生成器和鑑別器的兩個網絡層。像素級的自注意力會增加 GPU 資源的調度成本，且每個像素有不同的注意力掩碼。Titan X GPU 大概可選擇的批量大小爲 8，你可能需要減少自注意力模塊的數量來減少內存消耗。
    > 
    > ![](http://i2.bangqu.com/j/news/20180606/8833oT1528261215554cR2q2.png)
    > 
    > 


### VQ-VAE (Neural Discrete Representation Learning)

- [[1711.00937] Neural Discrete Representation Learning](https://arxiv.org/abs/1711.00937)

- [優拓 Paper Note ep.16: Neural Discrete Representation Learning](https://blog.yoctol.com/%E5%84%AA%E6%8B%93-paper-note-ep-16-neural-discrete-representation-learning-601d80f7f9ff)

    > 其中最中心的思想為 VQ-VAE (Vector Quantization-Variational Auto-Encoder)，最重要的一部份是 Vector Quantization，這樣的做法主要是為了解決所謂的 Posterior Collapse，避免在 Decoder 太強的情況下導致所得到的 Latents 是無用的，同時也能夠讓 Variance 不要太大。
    > 
    > 整體的模型圖如下：
    > 
    > ![](https://cdn-images-1.medium.com/max/2000/1*qyyhTBejuVXejVnA4BUwtQ.png)
    > 
    > 其中最重要的是 Embedding Space，將整體的 Latent Space 作為 K-way 分類，限定 Embedding Space 中僅有 k 個 Representation Vector。此為 Vector Quatization 的中心思想。
    > 
    > 舉例來說，我們可以將一張圖壓縮為許多的 Latent Class 的組合，像是上圖中下方即為其中一例，過 CNN Encoder 後再比較 Z(x) 與哪類 Embedding 較為接近，就轉換為該類 Embedding，依據則為下列方程式：
    > 
    > ![](https://cdn-images-1.medium.com/max/1600/0*MHdNg7oKXsT6TyYF.png)
    > 
    > ![](https://cdn-images-1.medium.com/max/1600/0*mDH_BkddkGK9WbbN.png)
    > 
    > 而其 Loss Function 為：
    > 
    > ![](https://cdn-images-1.medium.com/max/1600/0*DhHI4JBum108cTwj.png)
    > 
    > 第一項為 Reconstruction Loss，在做 Error Backpropagation 的時候傳到 Decoder Input 時就將其 Gradient 複製到 Encoder output，再繼續做 Back Propagation。
    > 
    > 第二項為 Error Backpropagate on Embedding Space，會將該類型的 Embedding e 拉近 Encoder Output Z(x)。
    > 
    > 第三項為 Commitment Loss，其用意為讓 Z(x) 能夠真正影響 Embedding Space，讓其訓練速度能夠跟上 Encoder Parameter 的訓練速度。
    > 
    > 
    > ---
    > 
    > 註：
    > 1.  在 [論文連結](https://arxiv.org/pdf/1711.00937.pdf) 中有許多圖片的例子可以參考。
    > 2.  在 [範例參考](https://avdnoord.github.io/homepage/vqvae/) 中也有許多人聲的例子，能夠做到不錯的人聲轉換。
    > 

### UNIT

- [UNIT 介紹 — Unsupervised Image-to-Image Translation – xiao sean – Medium](https://medium.com/@xiaosean5408/unit-%E4%BB%8B%E7%B4%B9-unsupervised-image-to-image-translation-1f9dc2a17cdd)

    > 我們可以先看一下 [Two Minute Papers](https://www.youtube.com/watch?v=dqxqbvyOnMY&feature=youtu.be)當中如何的介紹他。
    > 
    > 作者有將程式碼釋出 [Github](https://github.com/mingyuliutw/UNIT)：
    > 
    > > *請注意，目前版本的實作可能會和論文的有出入，要將branch切去version_02*
    > 
    > ### 成果圖
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/1*hCooeJFioz4JDZjOsNppRw.png)
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/1*jrI0vYc9InlvIiAjTdL1sw.png)
    > 
    > ### 簡介
    > 
    > 本文是在說圖片的風格轉換（style transfer），如貓轉成狗，
    > 
    > 這幾年風格轉換（style transfer)在GAN領域中算是很火紅的話題，
    > 
    > 大概從2015年紅到現在，相關的論文不少，有興趣的可以自己理解。
    > 
    > ### 概念
    > 
    > ### Unsupervised
    > 
    > 標題為：Unsupervised Image-to-Image Translation
    > 
    > 這邊的Unsupervised的概念如下
    > 
    > -   將兩個不同的dataset的圖片一起訓練， 例如：貓和狗
    > -   以往都是成對的資料輸入，以手勢來說，就是兩個人都比同樣的手勢，而這篇論文是可以不用成對的輸入。
    > 
    > ### Latent Space
    > 
    > 此paper的核心概念為Latent Space(共同特徵)。
    > 
    > 假如我們輸入的dataset是貓和狗，
    > 
    > 他們其實會有一些共同的特徵，如眼睛、鼻子、嘴巴、耳朵。
    > 
    > 我們的目標是希望可以學會這些特徵，
    > 
    > 如我們輸入大眼睛的狗狗，可以生成出大眼睛的貓咪照片
    > 
    > 架構如下
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/1*M1_BU7alWKfOk_x-Mj8jGQ.png)
    > 
    > 如上圖我們可以看到
    > 
    > -   2個encoder(下方稱作 Encoder-A, Encoder-B)
    > -   latent space(中間灰色部分)
    > -   2個decoder(下方稱作 Decoder-A, Decoder-B)
    > -   2個discriminator
    > 
    > 作者很貼心的幫我們列出每個model的結合，如Encoder + Decoder(Generator) = VAE。
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/1*eRcdtlI_EytNnNGC0UbuRg.png)
    > 
    > 這部分就屬於歷史演進了，有興趣的可以去研究GAN的進展。
    > 
    > 大家都是站在巨人的肩膀上做研究。
    > 


### On Unifying Deep Generative Models

- [[1706.00550] On Unifying Deep Generative Models](https://arxiv.org/abs/1706.00550)

- [(2 封私信 / 82 条消息)如何评价 On Unifying Deep Generative Models 这篇 paper? - 知乎](https://www.zhihu.com/question/60697472)

    > 
    > 回复评论里的提问：关于我们的工作与最近"试图统一VAE和GAN"工作比如 "[Adversarial Variational Bayes: Unifying Variational Autoencoders and Generative Adversarial Networks](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1701.04722.pdf)" 的关系：
    > 
    > [我们的论文（最近做了大的更新）](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1706.00550.pdf)里有讨论这些工作（see section 6）。Generally，这些论文提出了新的结合VAE和GAN的deep generative models (DGMs)，因此这里的"unifying"指combine两种model变成一个joint model。而我们则是试图对这些DGM models and algorithms建立一个统一的视角("unified view")，发现他们之间的关系，而不是设计新的model instance.
    > 
    > Specifically, 这篇Adversarial Variational Bayes主要是用implicit distribution作为VAE的inference model （而标准的VAE是assume 一个explicit inference distribution，比如Gaussian）。为了learn这个implicit distribution, 论文用了adversarial loss (因为implicit distribution不支持likelihood evaluation, 传统的reconstruction loss不适用)。最近类似的工作还有很多，比如我们论文里已经cite的[26,36,49,54], 大体思想都是用implicit distribution作为inference model。这些工作可以看做是我们提出的统一视角的一个特例，具体的说(专有名词太多就用英文写了)：
    > 
    > Briefly, these works are instances of the general idea proposed in our paper, i.e., **symmetric modeling of generation and inference** (section 6) --- we can apply implicit distributions and adversarial loss for *generation* (i.e., GANs). Symmetrically, we can apply implicit distributions and adversarial loss for *inference* with exact the same formulation, which are essentially what these works do. For example, if we let z be the observed data and x the latent code, InfoGAN is exactly a VAE with implicit distribution as its inference model.
    > 
    > The idea of symmetric view of generation and inference is one of the key insights of our work. It helps reveal the connections between GANs and ADA, as well as the resemblance of GANs to variational inference.
    > 
    > ===============分割线以下为原答案===========
    > 
    > 谢谢关注我们的工作。我们会对论文初稿继续改进，对不足之处也欢迎大家指正和交流。
    > 
    > 这个工作里我们的目标不是提出新的模型，而是希望对deep generative model （DGM）的几类基本方法重新formulate，揭示他们间的关系，建立统一的interpretation。统一的框架主要有两个好处：
    > 
    > （1）对已有模型以及种类繁多的变种有更好或者新的理解，把握算法演进的脉络；
    > 
    > （2）促进 后续研究中，各个本来相互独立的DGM研究方向的融合。期待论文提出的分析框架能促进后续更多的DGM算法/模型的提出。
    > 
    > 对于（1），论文的主要结论是: GANs 和 VAEs 大体上是在minimize 不同方向的KL Divergence。 *Roughly speaking*, 对优化generator P来说，GANs 做 min_{P} KL(P||Q)，VAEs 做 min_{P} KL(Q||P)。由此带来一些insights:
    > 
    > 1) GAN 的这个形式和贝叶斯推断的variational inference类似：把P看做inference model，Q看做posterior。因此我们是在用*inference*来解释*generation*。这一点在论文最后的discussion section有更具体的讨论。
    > 
    > 2) 优化两个方向的KL，正好和经典的wake sleep算法的两个phase对应。GAN可以看做sleep phase的extension，VAE可以看做wake phase的extension。
    > 
    > 3) 根据KL的不对称性质，GANs优化的KL(P||Q)决定了GANs倾向于miss mode，而VAEs倾向于cover mode。这点在之前的一些论文 e.g. [1][29],也有涉及。
    > 
    > 对于（2）,我们举了两个例子，来说明各种加强VAEs的方法能直接应用在GANs上来提高GANs，反之，之前用来提高GANs的方法也能用来提高VAEs。前者，我们从importance weighted VAEs出发可以很轻松推导出importance weighted GANs；后者，我们将GANs的对抗机制直接复制到VAEs上。实验基本没调过参数，不过对base model基本都有提高。



### Glow

- [[1807.03039] Glow: Generative Flow with Invertible 1x1 Convolutions](https://arxiv.org/abs/1807.03039)
    - [下一個GAN？OpenAI提出可逆生成模型Glow - 幫趣](http://bangqu.com/nNcD1K.html#utm_source=Facebook_PicSee&utm_medium=Social)
    - [Glow: Better Reversible Generative Models](https://blog.openai.com/glow/)
    - [[D] Glow: Better Reversible Generative Models：MachineLearning](https://www.reddit.com/r/MachineLearning/comments/8xe5lx/d_glow_better_reversible_generative_models/)





## 動作合成

### Synthesizing Images of Humans in Unseen Poses

- [只需一張照片，運動視頻分分鐘僞造出來 | MIT新算法 - 幫趣](http://bangqu.com/o64789.html)

    > 將源圖像和它對應的2D姿勢信息，以及目標姿勢輸入到這個模型中，它就能合成出一張輸出圖像，把源圖像上的人物形象和目標姿勢結合在一起。
    > 
    > ![](http://i2.bangqu.com/liang/news/20180624/v2-610ea5c421549009d23e203874b1cc6c.jpg)
    > 
    > 這個方法的精髓，就在於把這個艱鉅的大任務分成四塊簡單的、模塊化的子任務，大概如下圖所示：
    > 
    > ![](http://i2.bangqu.com/liang/news/20180624/v2-9918a32aa0bd9bf16c94fdc1de943cca.jpg)
    > 
    > 製造新姿勢的流程分五步。
    > 
    > 第一步得**表示姿勢**，研究人員將2D的姿勢Ps和Pt表示成3D形式RH×W×J，其中H代表輸入圖像的高度，W代表寬度，每個J通道都包含一個以不同節點(x,y)爲中心的高斯凸起。這種方法能快速利用姿態輸入的空間特性，而不僅僅是個扁平、密集的表示。
    > 
    > 表示完動作後，就需要對圖像整體大局進行**原圖分割**，爲合成動作做準備了。
    > 
    > 運動時身體每個部分軌跡不同通常會分段仿射運動場出現，通過將原圖Is分割成前景層和背景層，並將前景的身體部位分割成頭、上臂、下臂、大腿、小腿和軀幹等部分，基於UNet-style架構將原圖分割。
    > 
    > 之後進行**前景空間變形**，將這些被拆分的身體重新組合起來。
    > 
    > ![](http://i2.bangqu.com/liang/news/20180624/v2-63974e2c09e6c375cd5974eed97009c8.jpg)
    > 
    > 之後進行**前景合成**，將轉換後的主體部分合並，進一步細化外觀。下圖顯示了這個階段的Mask Mt(第3列)和yfg(第4列)的幾個輸出示例。
    > 
    > ![](http://i2.bangqu.com/liang/news/20180624/v2-7b2ba05c1b01640201dad24b7179af6e.jpg)
    > 
    > 可以看出，即使一開始是很誇張的姿勢，合成出效果看起來也很真實。可惜的是，高爾夫球杆、網球拍等持有物，在合成後不會被保留。
    > 
    > 此時，完事具備，就差背景了。**背景合成**也就是填補前景動作中開始被遮擋的部分，如上圖第五列所示~
    > 



## 風格變換/跨域生成

### Learning to Discover Cross-Domain Relations with Generative Adversarial Networks

- [论文阅读：Learning to Discover Cross-Domain Relations with Generative Adversarial Networks - CSDN博客](https://blog.csdn.net/u010886794/article/details/78141357)


    > 一、目的
    > ====
    > 
    > 
    >    提出一个基于GAN的网络框架来学习发现跨域关系（cross-domain relation），把寻找这种关系变成了用一种风格的图片生成另一种风格。
    > 
    > 
    >    下面是论文列举的手提包生成鞋、鞋生成手提包的示意图。
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/TnLF6wB.jpg)
    > 
    > 二、模型
    > ====
    > 
    > 
    > GAB表示域A到域B的生成器，GBA表示域B到域A的生成器。为了找到有意义的对应关系，需要将这个映射限制成一对一映射，意思就是说，GAB和GBA应该是刚好相反的映射。对于所有的A里面的真实样本xA，GAB(xA)都要在B里面，对于GBA(xB)也一样。
    > 
    > 
    > 
    > 标准的GAN模型
    > --------
    > 
    > ![这里写图片描述](https://i.imgur.com/YveUKp5.jpg)
    > 
    > 
    >   图中xA、xB分别表示A里面和B里面的真实样本，xAB表示真实样本xA经生成器GAB生成的样本。
    > 
    > 
    > 
    > 标准的GAN模型很容易发生模式崩溃。
    > 
    > 带有重建损失的GAN模型
    > ------------
    > 
    > 
    > 基于前面所提出的一对一映射，对于所有的A里面的真实样本xA，GAB(xA)都要在B里面，这相当于要满足GBA(GAB(xA))=xA这个条件，但是这个条件很难优化，于是改为最小化距离d(GBA(GAB(xA)),xA)，这个d可以是L1，L2等等的度量函数。
    > 
    >    于是，标准的GAN模型就被改成了这样：
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/FeNhHMB.jpg)
    > 
    > 
    > 生成器的损失函数如下：
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/ZD7hIsg.jpg)
    > ![这里写图片描述](https://i.imgur.com/VXPONyc.jpg)
    > 
    > 
    > 生成器GAB收到两个损失，一个是重建损失(reconstruction loss),描述经过两个生成器之后的重建效果与原始真实样本的差距，另外一个是原始GAN的生成损失，表示GAB生成的样本来自B的逼真性。
    > 
    > 判别器的损失如下：
    > 
    > 
    > 
    > ![](https://i.imgur.com/OyQEgQE.jpg)
    > D表示相应域的判别器。
    > 
    > 
    > 相对于原始的GAN模型，这里的重建约束虽然迫使重建样本与原始的一样，但是这仍然会导致类似的模式崩溃问题。
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/gSM7ZGa.jpg)
    > 
    > 
    >  (a)是我们理想的映射，一对一的；(b)是原始GAN的结果，A中的多个模式映射到了B中的一个模式，就是模式崩溃的情况；(c)是加入了重建损失的GAN，A中两个模式的数据都映射到了B中的一个模式，而B中一个模式的数据只能映射到A中这两个模式中的一个。重建损失使得模型在(c)中的两个状态之间震荡，而并不能解决模式崩溃问题。
    >  
    >  个人的理解是，当A的数据放进去一起训练，由于不管是放进哪一个模式，GAB都会产生B中对应的一个模式,而GBA再生成的时候，当生成A中的第一个模式，和第二个模式就不像了，于是接下来重建损失会使得GBA再生成的数据往第二个模式靠拢，但是又不像A里面的第一个模式了，于是模型在这两者之间来回震荡，导致无法收敛。
    > 
    > 
    > 
    > DiscoGAN
    > --------
    > 
    > 
    > 为了解决模式崩溃的问题，就要使得不管是GAB还是GBA，不同模式生成出来的就应该是不同的，于是很自然地想到了对称结构，就是再加一个反过来的生成网络，迫使A和B中的数据一一对应。
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/xiyblG8.jpg)
    > 
    > 
    > 模型中包含两个生成器GAB，这两个GAB是一样的，还有两个生成器GBA，这两个也是一样的。这样就实现了一对一的映射。
    > 
    > 
    > 
    > 损失函数如下：
    > ![这里写图片描述](https://i.imgur.com/CkepbyO.jpg)
    > 
    > 记号和结构
    > -----
    > 
    > ![这里写图片描述](https://i.imgur.com/XlhPBAD.jpg)
    > 
    > 三、实验
    > ====
    > 
    > toy实验
    > -----
    > 
    > 
    >  首先为了证明所提出的这种对称模型对于模式崩溃问题的良好性能，做了一个演示实验。A和B中的数据都是二维的，真实样本都取自混合高斯模型。用3个线性层和一个ReLU激活层作为生成器，判别器用5个线性层，每层后面接一个ReLU层，最后再接一个sigmoid层将输出限定在[0,1]之间。
    > 
    > 
    > 
    > ![这里写图片描述](https://i.imgur.com/mPdhwfQ.jpg)
    > 
    > 
    >  彩色背景表示判别器的输出值，"x"表示B种不同的模式。(a)标示了10个目标模式和最初的转换结果；(b)是标准的GAN迭代40000次的结果；(c)是加入重建损失的网络迭代40000次的结果；(d)是文章提出的DiscoGAN迭代40000次后的结果。
    >  
    >  标准GAN的许多不同颜色的转换点都位于B相同的模式下，海蓝和浅蓝色的点离得很近，橙色和绿色的点也在一起，多种颜色的点（A中的多种模式）都映射到B的同一种模式下。带有重建损失的GAN的模式崩溃问题已经不那么严重了，但是海蓝、绿色和浅蓝色的点仍然会在少数几个模式上重叠。
    >  
    >  标准的GAN和带有重建损失的GAN都没有覆盖B中的所有模式，DiscoGAN将A中的样本转换为B中有边界不重叠的区域，避免了模式崩溃，并且产生的B样本覆盖了所有10种模式，因此这个映射是双射，从A转换的样本也把B的鉴别器个骗过了。
    > 
    > 
    > 
    > 转换实验
    > ----
    > 
    > 汽车到汽车\
    > ![这里写图片描述](https://i.imgur.com/iI9Uu90.jpg)
    > 
    > 人脸到人脸\
    > ![这里写图片描述](https://i.imgur.com/IjQXPjS.jpg)
    > 
    > 性别转换\
    > ![这里写图片描述](https://i.imgur.com/QVRQCWT.jpg)
    > 
    > 头发颜色转换\
    > ![这里写图片描述](https://i.imgur.com/mBwgxPl.jpg)
    > 
    > 是否戴眼镜转换\
    > ![这里写图片描述](https://i.imgur.com/4Mo3BtL.jpg)
    > 
    > 先转换性别，再转换头发颜色\
    > ![这里写图片描述](https://i.imgur.com/1fJYHMe.jpg)
    > 
    > 头发颜色、性别来回转\
    > ![这里写图片描述](https://i.imgur.com/kEyJymW.jpg)
    > 
    > 椅子到汽车，汽车到人脸\
    > ![这里写图片描述](https://i.imgur.com/KAGyOXT.jpg)
    > 
    > 轮廓和图像互转\
    > ![这里写图片描述](https://i.imgur.com/bF3shTp.jpg)
    > 
    > 附录
    > ==
    > 
    > 论文链接\
    > <https://arxiv.org/pdf/1703.05192.pdf>\
    > 论文相关博客\
    > <http://blog.csdn.net/u011636567/article/details/72678625>\
    > 代码地址\
    > 官方代码：<https://github.com/SKTBrain/DiscoGAN>\
    > 其他代码：<https://github.com/carpedm20/DiscoGAN-pytorch>\
    > Tensorflow简洁版本：<https://github.com/ChunyuanLI/DiscoGAN>
    > 


### [1808.04537] Learning Linear Transformations for Fast Arbitrary Style Transfer

- [New AI Style Transfer Algorithm Allows Users to Create Millions of Artistic Combinations - NVIDIA Developer News CenterNVIDIA Developer News Center](https://news.developer.nvidia.com/new-ai-style-transfer-algorithm-allows-users-to-create-millions-of-artistic-combinations/)

- [[1808.04537] Learning Linear Transformations for Fast Arbitrary Style Transfer](https://arxiv.org/abs/1808.04537)



## 異常偵測

### [1805.12511] Cyberattack Detection using Deep Generative Models with Variational Inference
- [[1805.12511] Cyberattack Detection using Deep Generative Models with Variational Inference](https://arxiv.org/abs/1805.12511)

    > ![](https://screenshotscdn.firefoxusercontent.com/images/26a3753d-b194-4233-a6ec-9f8df472989b.png) 

### 杜倫大學提出GANomaly：無需負例樣本實現異常檢測 - 掃文資訊

- [杜倫大學提出GANomaly：無需負例樣本實現異常檢測 - 掃文資訊](https://hk.saowen.com/a/60fb44584916b0e9ae3f29c138f878161923e2ae74559cce432b6c1431913864?fbclid=IwAR0T_-rgy_AbvPQZM3N8hIWEdQ6kAIp0xHxEO433yac4QdfCbu4l2uUJqFg)

## 對抗樣本

- [對抗樣本的基本原理 - 幫趣](http://bangqu.com/5292n6.html#utm_source=Facebook_PicSee&utm_medium=Social)

    > 在原理上介紹對抗樣本，以經典的二分類問題爲例，機器學習模型通過在樣本上訓練，學習出一個分割平面，在分割平面的一側的點都被識別爲類別一，在分割平面的另外一側的點都被識別爲類別二。
    > 
    > ![對抗樣本的基本原理](http://i2.bangqu.com/lf1/news/20180601/5b10cf2ee3682.png)
    > 
    > 生成攻擊樣本時，我們通過某種算法，針對指定的樣本計算出一個變化量，該樣本經過修改後，從人類的感覺無法辨識，但是卻可以讓該樣本跨越分割平面，導致機器學習模型的判定結果改變。
    > 
    > ![對抗樣本的基本原理](http://i2.bangqu.com/lf1/news/20180601/5b10cf3a03ee8.png)
    > 
    > 如何高效的生成對抗樣本，且讓人類感官難以察覺，正是對抗樣本生成算法研究領域的熱點。


- [[1612.06299] Simple Black-Box Adversarial Perturbations for Deep Networks](https://arxiv.org/abs/1612.06299)



## GAN

### Mode colapse

- [整體 or 局部？用全新幾何角度構建 GAN 模型 - 幫趣](http://bangqu.com/2bx137.html#utm_source=Facebook_PicSee&utm_medium=Social)

    > ### 從幾何角度研究 Mode collapse 問題
    > 
    > 當然，從幾何和流型參數化的角度還可以給出對 GAN 更深入的理解，比如對 mode collapse 問題。在 GAN 的相關研究中，mode collapse 是一個被廣泛關注的問題。有很多相關的論文在從不同角度來研究和解決這個問題。
    > 
    > 而基於 Localized GAN 所揭示的幾何方法，我們可以從流型局部崩潰的角度來**解釋和避免 GAN 的 mode collapse**。具體來說，給定了一個 z，當 z 發生變化的時候，對應的 G(z) 沒有變化，那麼在這個局部，GAN 就發生了 mode collapse，也就是不能產生不斷連續變化的樣本。這個現象從幾何上來看，就是對應的流型在這個局部點處，沿着不同的切向量方向不再有變化。換言之，所有切向量不再彼此相互獨立--某些切向量要麼消失，要麼相互之間變得線性相關，從而導致流型的維度在局部出現缺陷（dimension deficient）。
    > 
    > 爲了解決這個問題，最直接的是我們可以給流型的切向量加上一個正交約束 (Orthonormal constraint)，從而避免這種局部的維度缺陷。下圖是在 CelebA 數據集上得到的結果。可以看到，通過對不同的切向量加上正交化的約束，我們可以在不同參數方向上成功地得到不同的變化。
    > 
    > ![整體 or 局部？阿里 CVPR 論文用全新幾何角度構建 GAN 模型](http://i2.bangqu.com/lf1/news/20180606/5b0625c47435b.png)
    > 
    > 上圖：在給定輸入圖像的局部座標系下對人臉的不同屬性進行編輯。




## 醫療

- [GAN打一個響指，假牙就設計好了（上臨牀測試ing - 幫趣](http://bangqu.com/9uu241.html)

## Generate Discrete data

- [Boundary-seeking GANs: A new method for adversarial generation of discrete data - Microsoft Research](https://www.microsoft.com/en-us/research/blog/boundary-seeking-gans-new-method-adversarial-generation-discrete-data/)


- [生成式对抗网络GAN有哪些最新的发展，可以实际应用到哪些场景中？ - 知乎](https://www.zhihu.com/question/52602529/answer/155743699)

    > 作者：莫驚蟄\
    > 链接：https://www.zhihu.com/question/52602529/answer/155743699\
    > 来源：知乎\
    > 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
    > 
    > 直接把GAN应用到NLP领域（主要是生成序列），有两方面的问题：
    > 
    > 1\. GAN最开始是设计用于生成连续数据，但是自然语言处理中我们要用来生成离散tokens的序列。因为生成器(Generator，简称G)需要利用从判别器(Discriminator，简称D)得到的梯度进行训练，而G和D都需要完全可微，碰到有离散变量的时候就会有问题，只用BP不能为G提供训练的梯度。在GAN中我们通过对G的参数进行微小的改变，令其生成的数据更加"逼真"。若生成的数据是基于离散的tokens，D给出的信息很多时候都没有意义，因为和图像不同。图像是连续的，微小的改变可以在像素点上面反应出来，但是你对tokens做微小的改变，在对应的dictionary space里面可能根本就没有相应的tokens.
    > 
    > 2.GAN只可以对已经生成的完整序列进行打分，而对一部分生成的序列，如何判断它现在生成的一部分的质量和之后生成整个序列的质量也是一个问题。
    > 
    > 近几篇重要的工作：
    > 
    > 1\. 为了解决这两个问题，比较早的工作是上交的这篇发表在AAAI 2017的文章：**SeqGAN: Sequence Generative Adversarial Nets with Policy Gradient，** 16年9月就放上了Arxiv上面了，而且也公布了源代码。
    > 
    > 利用了强化学习的东西来解决以上问题。如图，针对第一个问题，首先是将D的输出作为Reward，然后用Policy Gradient Method来训练G。针对第二个问题，通过蒙特卡罗搜索，针对部分生成的序列，用一个Roll-Out Policy（也是一个LSTM）来Sampling完整的序列，再交给D打分，最后对得到的Reward求平均值。
    > 
    > ![](https://pic3.zhimg.com/50/v2-4f2d3324ac0a945434860e3432e7c7d1_hd.jpg)
    > 
    > ![](https://pic3.zhimg.com/80/v2-4f2d3324ac0a945434860e3432e7c7d1_hd.jpg)
    > 
    > 完整算法如图：
    > 
    > ![](https://pic1.zhimg.com/50/v2-6008ee3851e7609fe3ab5a4c4cb6394c_hd.jpg)
    > 
    > ![](https://pic1.zhimg.com/80/v2-6008ee3851e7609fe3ab5a4c4cb6394c_hd.jpg)
    > 
    > 原文链接：[https://arxiv.org/pdf/1609.05473v5.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1609.05473v5.pdf)
    > 
    > Github链接：[LantaoYu/SeqGAN](https://link.zhihu.com/?target=https%3A//github.com/LantaoYu/SeqGAN)
    > 
    > 2\. 第二篇是C.Manning组大神Li Jiwei的文章：**Adversarial Learning for Neural Dialogue Generation，**用GAN和强化学习来做对话系统，如果我没有记错，这篇paper是最早引用SeqGAN的，有同学还说这篇是最早将RL用到GAN上的，主要是Jiwei大神名气太大，一放上Arxiv就引起无数关注。
    > 
    > 如图，文章也是用了Policy Gradient Method来对GAN进行训练，和SeqGAN的方法并没有很大的区别，主要是用在了Dialogue Generation这样困难的任务上面。还有两点就是：第一点是除了用蒙特卡罗搜索来解决部分生成序列的问题之外，因为MC Search比较耗费时间，还可以训练一个特殊的D去给部分生成的序列进行打分。但是从实验效果来看，MC Search的表现要更好一点。
    > 
    > 第二点是在训练G的时候同时还用了Teacher-Forcing（MLE）的方法，这点和后面的MaliGAN有异曲同工之处。
    > 
    > 为什么要这样做的原因是在对抗性训练的时候，G不会直接接触到真实的目标序列（gold-standard target sequence），当G生成了质量很差的序列的时候（生成质量很好的序列其实相当困难），而D又训练得很好，G就会通过得到的Reward知道自己生成的序列很糟糕，但却又不知道怎么令自己生成更好的序列， 这样就会导致训练崩溃。所以通过对抗性训练更新G的参数之后，还通过传统的MLE就是用真实的序列来更新G的参数。类似于有一个"老师"来纠正G训练过程中出现的偏差，类似于一个regularizer。
    > 
    > ![](https://pic1.zhimg.com/50/v2-46fa3718cd1bd1504b57d7feb07a97f0_hd.jpg)
    > 
    > ![](https://pic1.zhimg.com/80/v2-46fa3718cd1bd1504b57d7feb07a97f0_hd.jpg)
    > 
    > 原文链接：[https://arxiv.org/pdf/1701.06547.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1701.06547.pdf)
    > 
    > Github链接：[jiweil/Neural-Dialogue-Generation](https://link.zhihu.com/?target=https%3A//github.com/jiweil/Neural-Dialogue-Generation)
    > 
    > 3\. Yoshua Bengio组在二月底连续放了三篇和GAN有关的paper，其中我们最关心的是大神Tong Che和Li yanran的这篇：**Maximum-Likelihood Augmented Discrete Generative Adversarial Networks（MaliGAN），**简称读起来怪怪的。。。
    > 
    > 这篇文章的工作主要是两个方面：
    > 
    > 1.为G构造一个全新的目标函数，用到了Importance Sampling，将其与D的output结合起来，令训练过程更加稳定同时梯度的方差更低。尽管这个目标函数和RL的方法类似，但是相比之下更能狗降低estimator的方差（强烈建议看原文的3.2 Analysis，分析了当D最优以及D经过训练但并没有到最优两种情况下，这个新的目标函数仍然能发挥作用）
    > 
    > 2.生成较长序列的时候需要用到多次random sampling，所以文章还提出了两个降低方差的技巧：第一个是蒙特卡罗树搜索，这个大家都比较熟悉; 第二个文章称之为Mixed MLE-Mali Training，就是从真实数据中进行抽样，若序列长度大于N，则固定住前N个词，然后基于前N个词去freely run G产生M个样本，一直run到序列结束。
    > 
    > 基于前N个词生成后面的词的原因在于条件分布Pd比完整分布要简单，同时能够从真实的样本中得到较强的训练信号。然后逐渐减少N（在实验三中N=30, K=5， K为步长值，训练的时候每次迭代N-K）
    > 
    > ![](https://pic3.zhimg.com/50/v2-423a1050fa9b5636e682d92dd7501136_hd.jpg)
    > 
    > ![](https://pic3.zhimg.com/80/v2-423a1050fa9b5636e682d92dd7501136_hd.jpg)
    > 
    > Mixed MLE训练的MaliGAN完整算法如下：
    > 
    > ![](https://pic2.zhimg.com/50/v2-9c2bcba753585641ce1507802ace64f8_hd.jpg)
    > 
    > ![](https://pic2.zhimg.com/80/v2-9c2bcba753585641ce1507802ace64f8_hd.jpg)
    > 
    > 在12，梯度更新的时候，第二项（highlight的部分）貌似应该是logP![\theta](https://www.zhihu.com/equation?tex=%5Ctheta)（我最崇拜的学长发邮件去问过一作） 。至于第一部分为什么梯度是近似于这种形式，可以参考Bengio组的另一篇文章：**Boundary-Seeking Generative Adversarial Networks**
    > 
    > 这个BGAN的Intuition就是：令G去学习如何生成在D决策边界的样本，所以才叫做boundary-seeking。作者有一个特别的技巧：如图，当D达到最优的时候，满足如下条件，Pdata是真实的分布，Pg是G生成的分布。
    > 
    > ![](https://pic4.zhimg.com/50/v2-2642ebda15e8f1d2b29e497c40197bb9_hd.jpg)
    > 
    > ![](https://pic4.zhimg.com/80/v2-2642ebda15e8f1d2b29e497c40197bb9_hd.jpg)
    > 
    > 我们对它进行一点微小的变换：这个形式厉害之处在于，尽管我们没有完美的G，但是仍然可以通过对Pg赋予权重来得到真实的分布，这个比例就是如图所示，基于该G的最优D和（1-D）之比。当然我们很难得到最优的D，但我们训练的D越接近最优D，bias越低。而训练D（标准二分类器）要比G简单得多，因为G的目标函数是一个会随着D变动而变动的目标。
    > 
    > ![](https://pic3.zhimg.com/50/v2-49ee11359e258c14dfa4c0f787f2b589_hd.jpg)
    > 
    > ![](https://pic3.zhimg.com/80/v2-49ee11359e258c14dfa4c0f787f2b589_hd.jpg)
    > 
    > 文章后面给出了如何求梯度的数学公式，这里就不贴了。
    > 
    > 回到MaliGAN，作者给出了实验数据，比SeqGAN的效果要更好，看BLEU score.
    > 
    > ![](https://pic4.zhimg.com/50/v2-274b3811dc752bd302e50c8b30cc2594_hd.jpg)
    > 
    > ![](https://pic4.zhimg.com/80/v2-274b3811dc752bd302e50c8b30cc2594_hd.jpg)
    > 
    > 原文链接：[https://arxiv.org/pdf/1702.07983v1.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1702.07983v1.pdf)
    > 
    > 4\. 用SeqGAN做机器翻译，中科院自动化所在三月中旬放出了这篇文章：**Improving Neural Machine Translation with Conditional Sequence Generative Adversarial Nets，**这篇文章主要的贡献就是第一次将GAN应用到了NLP的传统任务上面，而且BLEU有2的提升。
    > 
    > 这个模型他们称之为CSGAN-NMT，G用的是传统的attention-based NMT模型，而D有两种方案，一种是CNN based，另一种是RNN based，通过实验比较发现CNN的效果更好。推测的原因是RNN的分类模型在训练早期能够有极高的分类准确率，导致总能识别出G生成的数据和真实的数据，G难以训练（因为总是negative signal）,
    > 
    > 这篇文章的重点我想是4.训练策略，GAN极难训练，他们首先是用MLE来pretrain G，然后再用G生成的样本和真实样本来pretrain D，当D达到某一个准确率的时候，进入对抗性训练的环节，GAN的部分基本和SeqGAN一样，用policy gradient method+MC search，上面已经讲过了不再重复。但是由于在对抗性训练的时候，G没有直接接触到golden target sentence，所以每用policy gradient更新一次G都跑一次professor forcing。这里我比较困惑，我觉得是不是像Jiwei那篇文章，是用D给出的Reward来更新G参数之后，又用MLE来更新一次G的参数（保证G能接触到真实的样本，这里就是目标语言的序列），但这个方法是teacher-forcing不是professor forcing。
    > 
    > 最后就是训练Trick茫茫，这篇文章试了很多超参数，比如D要pretrain到f=0.82的时候效果最好，还有pretrain要用Adam，而对抗性训练要用RMSProp，同时还要和WGAN一样将每次更新D的权重固定在一个范围之内。
    > 
    > 原文链接：[https://arxiv.org/pdf/1703.04887.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1703.04887.pdf)
    > 
    > 5.最后3月31号放到Arxiv上的文章：**Improved Training of Wasserstein GANs,** WGAN发布之后就引起轰动，比如Ian在Reddit上就点评了这篇文章，NYU的又祭出了这篇，令WGAN在NLP上也能发挥威力。
    > 
    > 在WGAN中，他们给出的改进方案是：
    > 
    > -   判别器最后一层去掉sigmoid
    > -   生成器和判别器的loss不取log
    > -   每次更新判别器的参数之后把它们的绝对值截断到不超过一个固定常数c
    > -   不要用基于动量的优化算法（包括momentum和Adam），推荐RMSProp，SGD也行
    > 
    > 这里引用自知乎专栏：[令人拍案叫绝的Wasserstein GAN - 知乎专栏](https://zhuanlan.zhihu.com/p/25071913)
    > 
    > 文章写得深入浅出，强烈推荐。
    > 
    > 其中第三项就是机器翻译文章中也用到的weight clipping，在本文中，他们发现通过weight clipping来对D实施Lipschitz限制（为了逼近难以直接计算的Wasserstein距离），是导致训练不稳定，以及难以捕捉复杂概率分布的元凶。所以文章提出通过梯度惩罚来对Critic（也就是D，WGAN系列都将D称之为Critic）试试Lipschitz限制。
    > 
    > 如图：损失函数有原来的部分+梯度惩罚，现在不需要weight clipping以及基于动量的优化算法都可以使用了，他们在这里就用了Adam。同时可以拿掉Batch Normalization。
    > 
    > ![](https://pic3.zhimg.com/50/v2-f345da0e5c68b1a7a6f2273bb9d3c19b_hd.jpg)
    > 
    > ![](https://pic3.zhimg.com/80/v2-f345da0e5c68b1a7a6f2273bb9d3c19b_hd.jpg)
    > 
    > 如图所示，实验结果很惊人，这种WGAN---GP的结构，训练更加稳定，收敛更快，同时能够生成更高质量的样本，而且可以用于训练不同的GAN架构，甚至是101层的深度残差网络。
    > 
    > ![](https://pic2.zhimg.com/50/v2-79721ebf87289ad49ffe8f3afd4c425e_hd.jpg)
    > 
    > ![](https://pic2.zhimg.com/80/v2-79721ebf87289ad49ffe8f3afd4c425e_hd.jpg)
    > 
    > 同时也能用于NLP中的生成任务，而且是character-level 的language model，而MaliGAN的实验是在Sentence-Level上面的。而且前面几篇提到的文章2,3,4在对抗性训练的时候或多或少都用到了MLE，令G更够接触到Ground Truth，但是WGAN-GP是完全不需要MLE的部分。
    > 
    > ![](https://pic2.zhimg.com/50/v2-59b2e1d2bf0701f02e9e847df1bb56da_hd.jpg)
    > 
    > ![](https://pic2.zhimg.com/80/v2-59b2e1d2bf0701f02e9e847df1bb56da_hd.jpg)
    > 
    > 原文链接：[https://arxiv.org/pdf/1704.00028.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1704.00028.pdf)
    > 
    > github地址：[https://github.com/igul222/improved_wgan_training](https://link.zhihu.com/?target=https%3A//github.com/igul222/improved_wgan_training)
    > 
    > 代码一起放出简直业界良心。
    > 
    > 6.3月31号还谷歌还放出了一篇BEGAN: Boundary Equilibrium Generative
    > 
    > Adversarial Networks，同时代码也有了是carpedm20用pytorch写的，他复现的速度真心快。。。
    > 
    > 最后GAN这一块进展很多，同时以上提到的几篇重要工作的一二作，貌似都在知乎上，对他们致以崇高的敬意。
    > 
    > 以上。
    > 



## Generate Functions 

- [[1807.04106] VFunc: a Deep Generative Model for Functions](https://arxiv.org/abs/1807.04106)




