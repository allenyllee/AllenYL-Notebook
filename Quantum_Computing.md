# Quantum_Computing

[toc]
<!-- toc --> 

## Quantum Programming

- [搶先Google、IBM一步，微軟推出秘密武器「Q#」，要讓量子電腦遍地開花｜數位時代](https://www.bnext.com.tw/article/47393/microsoft-releases-quantum-computing-development-kit-preview)

    > 量子運算程式語言「Q#」誕生
    > --------------
    > 
    > 達成九月在Ignite開發者大會上的目標，微軟在本周宣布推出量子運算程式語言的Preview （預覽版）開發包，號稱可以降低商用量子計算技術的出錯率、增加穩定性，並加快量子運算走向商業化的速度。
    > 
    > 這款開發包，有一個叫「Q#」的程式語言，可以協助開發者為量子電腦開發軟體，以及一台整合在微軟開發工具套件系列Visual Studio中的量子電腦模擬器「Q# library」，個人用戶最多可以模擬30個邏輯量子位能問題、企業客戶則可以模擬超過40個量子位能的計算問題，讓開發人員可以在一般電腦上利用Azure雲端服務測試量子電腦軟體，提供全套式的解決方案。



### Microsoft Q#

- [Quantum Development Kit | Microsoft](https://www.microsoft.com/en-us/quantum/development-kit)

- [Write a quantum program | Microsoft Docs](https://docs.microsoft.com/zh-tw/quantum/quantum-writeaquantumprogram?view=qsharp-preview&tabs=tabid-vs2017)








## Quantum Chip

- [CES 2018: Intel's 49-Qubit Chip Shoots for Quantum Supremacy - IEEE Spectrum](https://spectrum.ieee.org/tech-talk/computing/hardware/intels-49qubit-chip-aims-for-quantum-supremacy)

    > ![Intel's 49-qubit superconducting quantum test chip, Tangle Lake.](https://spectrum.ieee.org/image/MzAwMjc3Mg.jpeg)
    > 
    > Photo: Intel
    > 
    > Intel's new 49-qubit superconducting quantum test chip is named Tangle Lake.
    > 

    > It’s still going to be a long road before anyone will realize the commercial promise of quantum computing, which leverages the idea of quantum bits (qubits) that can represent more than one information state at the same time. Intel’s roadmap suggests researchers could achieve 1,000-qubit systems within 5 to 7 years. That sounds like a lot until you realize that many experts believe quantum computers will need at least one million qubits to become useful from a commercial standpoint.

- [继续向量子霸权迈进，谷歌开发72位量子芯片](https://zhuanlan.zhihu.com/p/34273525)

    > 在3月5日的美国物理学会的一次会议上，科学家们报告，谷歌正在测试一台72位量子位的量子计算机，与该公司之前的9位比特芯片相比，将是一次巨大的飞跃。
    > 
    > 来自谷歌的物理学家Julian Kelly表示，该小组希望使用具有更多量子位的芯片来首次实现量子霸权，即达到所有传统计算机无法实现的计算能力。
    > 
    > 与采用0或1为比特的传统计算机不同，归功于量子叠加效应，一个量子位可以是0，1或两者的混合体。实现量子霸权则需要一台超过50量子位的计算机，目前科学家们仍在努力实现控制这么多精细的量子体。
    > 
    > ![](https://pic2.zhimg.com/80/v2-1b7f0d0824355a398f75fc76b91c9978_hd.jpg)
    > 
    > 图 | 谷歌的72位量子芯片的计算能力可能会首次实现超越传统计算机
    > 
    > 由于芯片中的量子比特排列成类似松果鳞片的图案，因而谷歌的72位量子比特的计算机也得到了一个形象的绰号：“狐尾松”（Bristlecone），目前该计算机还在测试中。
    > 
    > 来自加州大学圣巴巴拉分校的谷歌物理学家John Martinis表示,他们刚开始进行该计算机的测试，并且目前的测试情况非常乐观。另外，他补充到，如果一切顺利的话，量子霸权的演示可能在几个月内实现。
    > 
    > 谷歌是目前致力于将量子计算机成为现实的几家公司之一。在2017年11月，IBM也宣布测试一台50位量子计算机，随后英特尔在今年1月宣布测试具有49位量子比特的芯片。
    > 

- [冷静冷静！谷歌发布72量子比特芯片，却还未实现量子霸权](https://zhuanlan.zhihu.com/p/34278702)

    > 美国时间3月5日，谷歌研究博客（Google Research Blog）丢出一个深水炸弹——Bristlecone，这是一个72量子比特的量子芯片。
    > 
    > 谷歌Google此次公布的Bristlecone的量子芯片使用了一种新的架构，允许单个阵列上的72个量子比特具有重叠设计，将两个不同的网格放在一起。
    > 
    >   
    > 
    > ![](https://pic1.zhimg.com/80/v2-f6b03b4ab973f90a08569e27fbd48cd5_hd.jpg)
    > 
    >   
    > 
    > ▲左边是谷歌最新的72量子比特量子处理器Bristlecone|右边是图示：每个“X”代表一个量子比特，量子比特之间以线性阵列方式相连
    > 
    > Google利用称为量子纠错（Quantum Error Correction）的专门流程对Bristlecone进行了优化，以尽可能降低错误率。正是谷歌这样的设计，让Bristlecone量子芯片在达到72量子比特的同时也实现了1%的错误率。
    > 
    > 一时间，科技圈炸开了锅，因为这意味着，在实现量子计算这条赛道上，目前谷歌可能成为了领跑的那一个（关于量子计算机更通俗易懂的报道可以参看：量子计算机有多可怕一秒破译全世界所有密码！）。
    > 
    > 
    > 二、**谷歌的量子霸权之路**
    > ---------------
    > 
    > 谷歌宣布研制出低错误率、72量子比特的量子芯片Bristlecone，并且正在往实现72量子比特的量子计算机的方向上推进，虽然72量子比特非常令人兴奋，但是从量子芯片到量子计算机，谷歌要做的工作还有很多。
    > 
    > 2017年12月，来自德国Jülich超级计算中心（Jülich Supercomputing Centre），中国武汉大学和荷兰格罗宁根大学（the University of Groningen）的研究人员宣布，他们打破了在经典超级计算机上可以模拟量子比特数量的世界纪录。
    > 
    > 该团队能够在超级计算机上模拟46个量子位，打破了之前45个量子位的记录。尽管45和46量子比特之间的差别可能看起来很小，但是，每增加一个量子比特，其对于各方面的要求都是指数性增加的。通常情况下，如果其他条件相同，每个额外量子比特的内存需求会翻倍。
    > 
    > 因此目前，最强大的超级计算机只能模拟46个量子比特，并且对于需要模拟的每个新量子比特而言，其存储需求通常会增加一倍。
    > 
    > 因此，要模拟一个72量子比特的量子计算机，我们需要数百万倍的RAM（Random-Access Memory，随机存取存储），也就是2的（72-46）次方倍数。外媒Tom’ Hardware认为我们很可能无法在超级计算机中达到这样体量的RAM。
    > 
    > 如果谷歌正在研究的72量子比特的量子计算机能够比我们最强大的超级计算机更快地运行任何算法，那么量子霸权时代将会到来。对此，谷歌也表示：“我们乐观但同时也是谨慎地认为，利用Bristlecone可以实现量子霸权”。


## Topological quantum computer

- [【重磅】微软量子计算重大突破：量子系统或存在天使粒子，一个稳定的量子比特强过 1 万个](https://zhuanlan.zhihu.com/p/35065555)

    - [Quantized Majorana conductance | Nature](https://www.nature.com/articles/nature26142)

- [發現馬約拉納費米子存在證據，微軟在構建量子電腦上又邁出一步 | TechNews 科技新報](https://technews.tw/2018/03/30/microsoft-and-majorana-fermion/)







## Quantum Computing for Machine Learning

- [How quantum effects could improve artificial intelligence](https://via.hypothes.is/https://phys.org/news/2016-10-quantum-effects-artificial-intelligence.html#annotations:Wpq38PRXEeecQMeKKj0UMQ)

    > ![](https://3c1703fe8d.site.internapcdn.net/newman/gfx/news/hires/2016/quantummachi.jpg)

    > In the new study, the researchers' main result is that quantum effects can help improve [reinforcement learning](https://via.hypothes.is/https://phys.org/tags/reinforcement+learning/), which is one of the three main branches of machine learning. They showed that quantum effects have the potential to provide quadratic improvements in learning efficiency, as well as exponential improvements in performance for short periods of time when compared to classical techniques for a wide class of learning problems.  
    > 
    > 
    > While other research groups have previously shown that quantum effects can offer improvements for the other two main branches of machine learning (supervised and unsupervised learning), reinforcement learning has not been as widely investigated from a quantum perspective.  
  

- [Quantum algorithm could help AI think faster](https://phys.org/news/2018-02-quantum-algorithm-ai-faster.html)

    - [超越传统算法！全新量子算法可以帮助 AI 更快思考](https://zhuanlan.zhihu.com/p/33725833)

        > 第一个量子线性系统算法是在 2009 年由另外一组研究人员提出的，该算法是研究机器学习或人工智能的量子形式的鼻祖。
        > 
        > **这套线性系统算法适用于大型数据矩阵。** 例如，交易者可以尝试预测未来的商品价格，该矩阵可以获取关于价格随时间变化的历史数据和关于可能影响这些价格的特征数据，比如货币汇率。该算法通过“反转”矩阵来计算每个特征之间的关联性，这些信息可以用来推断未来趋势。
        > 
        > Zhao 解释道：“在分析矩阵时需要进行大量的计算，比方说当输入超过 10000×10000 个元素时，这对于普通的计算机就变得很困难了。这是因为随着矩阵中元素数量的增加，计算的步骤也会急速增长——矩阵的大小每增加一倍，计算的长度就会增加 8 倍。”
        > 
        > 2009 年提出的算法可以更好地处理更大的矩阵，但必须是稀疏矩阵。在这些情况下，元素之间的关系是有限的，而现实世界中的数据通常不是这样。Zhao 和研究小组提出了一个新的算法，比经典和以前的量子算法版本都快，也没有限制它所计算的数据的种类。
        > 
        > **简单来说，该算法依靠一种被称为量子奇异值估算的技术。** 对于一个 10000 平方的矩阵，经典算法大约花费数万亿量级计算步骤，第一个量子算法需要几万步，而新量子算法只需要几百步。
        > 


- [Quantum computers could greatly accelerate machine learning](https://via.hypothes.is/https://phys.org/news/2015-03-quantum-greatly-machine.html#annotations:LSyXOvRbEeeM6CehLAH9Yg)

    > For the first time, physicists have performed machine learning on a photonic quantum computer, demonstrating that quantum computers may be able to exponentially speed up the rate at which certain machine learning tasks are performed—in some cases, reducing the time from hundreds of thousands of years to mere seconds. The new method takes advantage of quantum entanglement, in which two or more objects are so strongly related that paradoxical effects often arise since a measurement on one object instantaneously affects the other. Here, quantum entanglement provides a very fast way to classify vectors into one of two categories, a task that is at the core of machine learning.  

    > ![](https://3c1703fe8d.site.internapcdn.net/newman/gfx/news/hires/2015/1-quantummachi.jpg)

    > In the new paper, the physicists addressed this challenge by representing vectors with quantum states, and then entangling the states before comparing the distance between them. As they explain, quantum computers are naturally good at manipulating vectors. So to do this, they used a small-scale quantum computer that manipulates optical qubits, or photons.
    > 
    > In the optical setup, one photon acts as an ancillary qubit, and is used to entangle another photon that encodes both the reference vector and the new vector. The resulting two-photon entangled state is used to classify two-dimensional vectors, whereas three- and four-photon entangled states can classify four- and eight-dimensional vectors, respectively. In general, different vector dimensions are needed to describe the properties of different real-world objects.

- [Quantum Machine Learning: An Overview](https://www.kdnuggets.com/2018/01/quantum-machine-learning-overview.html)

    <iframe width="560" height="315" src="https://www.youtube.com/embed/g_IaVepNDT4?start=82" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

    - [量子机器学习入门科普：解读量子力学和机器学习的共生关系](https://zhuanlan.zhihu.com/p/33173860)

        > **量子计算**
        > --------
        > 
        > **量子（Quantum）**
        > ---------------
        > 
        > 量子是任何物理实体（比如能量和质量等）的最小可能单位。1900年，德国物理学家、量子力学创始人马克斯·普朗克（Max Planck）提出，在原子和亚原子水平，一个物体的能量被包含在叫做量子（quanta）的离散数据包中。
        > 
        > 波粒二象性（Wave-particle duality）是量子粒子的特征，它是指微观粒子基于不同的环境，有时会表现出波动性，而有时表现出粒子性。
        > 
        > 量子理论的特点是找到给定点x在空间中存在的概率，而不是它的确切位置。
        > 
        >   
        > 
        > ![](https://pic3.zhimg.com/80/v2-f0ad1f3883ce9f64473cb8cf58901036_hd.jpg)
        > 
        >   
        > 
        > **△** 光具有例子和波的双重性质
        > 
        > **量子位（Qubit）**
        > --------------
        > 
        > 经典计算机通过经典的“位（bit）”执行操作，这些位不是0就是1，而量子计算机借住的是“量子位（qubits）”。
        > 
        > 量子位可被表示为绕核旋转的电子和光子。光子的偏振态和电子的自旋态可用|1>和|0>分别表示。
        > 
        > **叠加（Superposition）**
        > ---------------------
        > 
        > 量子位同时以0和1的形式存在，这种现象被称为“叠加”。
        > 
        > 虽然粒子能存在于多个量子态中，一旦我们确定了粒子的能量或位置，叠加就至此消失，它只能存在一个状态。
        > 
        >   
        > 
        > ![](https://pic1.zhimg.com/80/v2-1d4b8ecf1cd3d940ac1ca29190bde112_hd.jpg)
        > 
        > **△** 量子位被定义为一对指向单位球面中一个点的复杂向量。一般来说，直指上方（正轴）的量子位表示为列向量|0>，指向下方（负轴）的量子位为行向量|1>。
        > 
        > **纠缠（Entanglement）**
        > --------------------
        > 
        > “量子纠缠”指的是量子粒子之间的相互作用。即使粒子间相隔甚远，它们依然相互作用、相互参照，而不是独立的。
        > 
        > 在测量时，如果一对纠缠的量子被决定处于箭头向下的自旋态（能量最低状态），则当电子与它的磁场保持一致时，这个状态就会被传递到另一个相关的箭头向上的相对自旋态的例子上。
        > 
        > 量子纠缠允许相隔很远的量子位彼此之间及时相互作用。
        > 
        > 讲完这四个基本概念，可能会有个疑问，**量子计算是怎样释放出巨大的并行性的？**
        > 
        > 两个相互作用的经典位有四种状态，即00、01、10或11。每个信息的两个组成成分（第一个位和第二个位）组合起来仅表示给定时间内的二进制结构。向普通计算机添加更多的位仍表示二进制结构。
        > 
        >   
        > 
        > ![](https://pic1.zhimg.com/80/v2-100dbe8604c8a01a3358daf68795e2bd_hd.jpg)
        > 
        >   
        > 
        > **△** 在测量前的叠加中的量子位具有“自旋向上”和“自旋向下”的概率
        > 
        > 一个量子位可同时存在0和1这两种状态。因此，两个相互作用的量子位可被同时存储为4个二进制结构。一般来说，‘n’ 量子位可同时代表 ‘2^n’个经典二进制结构。
        > 
        > 因此，一个300量子位的量子计算机能同时探索2^300种可能的结果，因此带来了巨大的并行性。所以，在量子计算机中加入更多的量子位会成倍增加计算能力。
        > 
        > 目前，我们的技术还无法实现真正意义上的量子计算机，因为添加更多的量子位和处理亚原子需要低于-452华氏度的低温环境。
        > 
        > 因此，微软通过量子模拟器LIQUi|>模拟40量子位的操作，通过微软Azure云计算资源扩展。
        > 
        > 量子计算可解决专业的科学问题，如分子建模、高温超导体的产生、药物建模和测试、分子的选择以及有机电池的制造。对于看视频或写Word文档等一般用途的任务，它并不是最佳选择。

## Quantum Memory

- [How can you tell if a quantum memory is really quantum?](https://phys.org/news/2018-05-quantum-memory.html)

    > Conventional protocols for testing for space-like correlations often use two characters, Alice as the sender and Bob as the receiver of quantum states. But since quantum memories involve time-like correlations, the protocol needs only a single character, whom the researchers call Abby, to act as both the sender and receiver at different times. In the test proposed in the new study, by comparing the relative frequencies of the signals that Abby sends and receives, it is possible to estimate the time-like entanglement and therefore certify that a quantum memory can store quantum information.
    > 
    > 

## Quantum computation

- [New quantum computer design to predict molecule properties](https://phys.org/news/2018-05-quantum-molecule-properties.html)

## Quantum imformation transfer

- [Transferring quantum information using sound](https://phys.org/news/2018-06-quantum_1.html)

    > As the research team has now been able to show using simulation calculations, any number of these quanta can be linked together in the diamond rod via phonons. The individual silicon atoms are switched on and off using microwaves. During this process, they emit or absorb phonons. This creates a quantum entanglement of the silicon defects, thus allowing quantum information to be transferred.

## Quantum Physics

### Hardy's Paradox

- [Classical Physics and Quantum Physics Can't Come to Terms on Hardy's Paradox](https://edgylabs.com/new-quantum-probability-rule-offers-novel-perspective-of-wave-function-collapse)

    > This experiment was first known as Hardy’s paradox. Some argue that it’s not a paradox per se, like say the Einstein-Podolsky-Rosen paradox. In many ways, it’s more of a theorem.
    > 
    > In the Universe, when matter and antimatter meet, particles and antiparticles annihilate one another through a flow of energy in the form of gamma radiation.
    > 
    > Hardy, however, showed that it’s theoretically possible that sometimes (in 6 to 9 percent of cases) when there’s no observer, matter and antimatter can interact and survive the encounter – classical physics cannot allow this.

    - [[1709.09812] Generalized Hardy's Paradox](https://arxiv.org/abs/1709.09812
    
    