# Neural_Attention__資料蒐集

- [Reasoning, Attention, Memory (RAM) NIPS Workshop 2015](http://www.thespermwhale.com/jaseweston/ram/)



## Neural Turing Machines

- [[1410.5401v2] Neural Turing Machines](https://arxiv.org/abs/1410.5401v2)

- [類神經網路 -- Neural Turing Machine « MARK CHANG'S BLOG](http://cpmarkchang.logdown.com/posts/279710-neural-network-neural-turing-machine)

    > ### Introduction
    > 
    > *Recurrent Neural Network* 在進行 *Gradient Descent* 的時候，會遇到所謂的 *Vanishing Gradient Problem* ，也就是說，在後面時間點的所算出的修正量，要回傳去修正較前面時間的參數值，此修正量會隨著時間傳遞而衰減。
    > 
    > 為了改善此問題，可以用類神經網路模擬記憶體的構造，把前面神經元所算出的值，儲存起來。例如： *Long Short-term Memory (LSTM)* 即是模擬記憶體讀寫的構造，將某個時間點算出的值給儲存起來，等需要用它的時候再讀出來。
    > 
    > 除了模擬單一記憶體的儲存與讀寫功能之外，也可以用類神經網路的構造來模擬 *Turing Machine* ，也就是說，有個 *Controller* ，可以更精確地控制，要將什麼值寫入哪一個記憶體區塊，或讀取哪一個記憶體區塊的值，這種類神經網路模型，稱為 *Neural Turing Machine* 。
    > 
    > 如果可以模擬 *Turing Machine* ，即表示可以學會電腦能做的事。也就是說，這種機器學習模型可以學會電腦程式的邏輯控制與運算。
    > 
    > ### Neural Turing Machine
    > 
    > *Neural Turing Machine* 的架構如下：
    > 
    > ![](http://lh3.googleusercontent.com/-Q0ZMlPrbLkU/ViucASG4HrI/AAAAAAAABk4/-ZL4sny1-g0/s532-Ic42/ntm1.jpeg)
    > 
    > 可分為幾個部分：\
    > **Input:** 從外部輸入的值。\
    > **Output:** 輸出到外部的值。\
    > **Controller:** 相當於電腦的IO和CPU，可以從外部輸入值，或從記憶體讀取值，經過運算，再將算出的結果輸出去，或寫入記憶體， *Controller* 可以用 *feed forward neural network* 或者 *recurrent neural network* （相當於有register的CPU）來模擬。\
    > **Read/Write Head:** 記憶體的讀寫頭，相當於pointer ，是要被讀取或被寫入的記憶體的address。\
    > **Memory:** 記憶體，相當於電腦的RAM，同一個地址可對應到一整排的記憶體單位，就像電腦一樣，用8個bit組成的一個byte，具有同一個memory address。
    > 
    > 以下細講每一部份的數學模型。
    > 
    > #### Memory
    > 
    > *memory* 是一個二維陣列。如下圖，一個 *memory block* 是由數個 *memory cell* 所構成。同一個 *block* 中的 *cell* 有相同的 *address* 。如下圖中，共有 $n$ 個 *block* ， 每個 *block* 有 $m$  個 *cell* 。
    > 
    > ![](http://lh3.googleusercontent.com/-uULs3_cBN7s/Vi5LNFwPs7I/AAAAAAAABrI/5noEAzgaRL8/s465-Ic42/nndl10.jpeg)
    > 
    > 操作 *Memory* 的動作有三種：即 *Read* ， *Erase* 和 *Add* 。
    > 
    > ##### Read
    > 
    > *Read* 是將記憶體裡面的值，讀出來，並傳給 *controller* 。由於記憶體有很多個 *memory block* ，至於要讀取哪個，由讀寫頭（ *Read/Write Head* ）來控制，讀寫頭為一個向量 $\textbf{w}$  ，其數值表示要讀取記憶體位置的權重，滿足以下條件：
    > 
    > $$
    > \sum_{i}w(i) = 1 \\
    > 0 \leq w(i) \leq 1, \forall i
    > $$
    > 
    > 讀寫頭內部各元素 $w_{i}$  的值介於 0 到 1 之間，且加起來的和為 1 ，這可解釋為，讀寫頭存在的位置，是用機率來表示。而讀出來的值，為記憶體區塊所儲存的值，乘上讀寫頭在此區塊 $i$  的機率 $w(i)$  ，所得出之期望值，如下：
    > 
    > $$
    > \textbf{r} \leftarrow \sum_{i}w(i)\textbf{M}(i) \mspace{40mu} \text{(1)}
    > $$
    > 
    > 其中，$\textbf{r}$  為 *Read vector* ，即從記憶體讀出來的值， $\textbf{M(i)}$  為記憶體 $i$  區塊的值， 而 $w(i)$  為讀寫頭 $w$  在區塊 $i$  的機率。
    > 
    > 例如下圖中， $w(0) = 0.9$ ， $w(1) = 0.1$ ，即表示，讀寫頭在位置 0 的機率為 0.9，在位置 1 的機率為 0.1 。
    > 
    > ![](http://lh3.googleusercontent.com/-zD7Q1XQ-D1U/Vi5IS5dDyeI/AAAAAAAABqs/OS4quQeUygI/s648-Ic42/ntm3.jpeg)
    > 
    > 將上圖中記憶體內部的值 $\textbf{M(i)}$  ，以及讀寫頭位置的值 $w(i)$  ，代入公式(1)，即可得出
    > 
    > $$
    > \begin{bmatrix}
    >       r_{0}  \\[0.3em]
    >       r_{1}  \\[0.3em]
    >       r_{2}  \\[0.3em]
    >     \end{bmatrix}
    > =\begin{bmatrix}
    >       1*0.9+2*0.1  \\[0.3em]
    >       1*0.9+1*0.1  \\[0.3em]
    >       2*0.9+4*0.1  \\[0.3em]
    >     \end{bmatrix}
    > =\begin{bmatrix}
    >       1.1  \\[0.3em]
    >       1.0  \\[0.3em]
    >       2.2  \\[0.3em]
    >     \end{bmatrix}
    > $$
    > 
    > ##### Erase
    > 
    > 如果要刪除記憶體內部的值，則要進行 *Erase* ，過程跟 *Read* 類似，都需要用讀寫頭 *w* 來控制。但刪除的動作，需要控制去刪除掉哪個 *memory cell* 的值，而不是一次就把整個 *memory block* 的值都刪除。所以需要另一個 *erase vector* $\textbf{e}$ 來選擇要被刪除的 *cell* 。 *erase vector* 為一向量，如下：
    > 
    > $$
    > 0 \leq e(j) \leq 1,  \mspace{10mu} 0 \leq j \leq m-1 , \mspace{10mu} \forall j
    > $$ 
    > 
    > 其中， $j$  為一個介於 0~m-1 之間的數， m 為 *block size* 。向量元素的值 $e(j)$  介於 0~1 之間。如果值為1，則表示要清空這個 *cell* 的值，若為 0 則表示保留 *cell* 原本的值， *erase* 的公式如下：
    > 
    > $$
    > \textbf{M}(i) \leftarrow (1-w(i) \textbf{e} ) \textbf{M}(i) \mspace{40mu} \text{(2)}
    > $$ 
    > 
    > 其中， $\textbf{w}$  是用來控制要清除哪個 *memory block* 而 $\textbf{e}$  是要控制清除這個 *block* 裡面的哪些 *cell* ，如下圖所示：
    > 
    > ![](http://lh3.googleusercontent.com/-6Kfryh9jcw0/Vi5ISyqYodI/AAAAAAAABqw/6nZYBUStn0M/s686-Ic42/ntm4.jpeg)
    > 
    > 上圖中，根據 $\textbf{w}$  和 $\textbf{e}$  這兩個向量所選擇的結果， 在 $\textbf{M}$  中，共有四個 *cell* 的值被削減了，分別位於左上角和左下角，用較明亮的背景色表示其位置。\
    > 將上圖中 $\textbf{w}$  、 $\textbf{e}$  和 $\textbf{M}$  中的值，代入公式(2) ，可得出此結果，如下：
    > 
    > $$
    > M= 
    > \begin{bmatrix}
    >       1(1-0.9) & 2(1-0.1) & 3 & ...  \\[0.3em]
    >       1 & 1 & 2 & ...  \\[0.3em]
    >       2(1-0.9) & 4(1-0.1) & 1 & ...  \\[0.3em]
    >     \end{bmatrix}
    > =\begin{bmatrix}
    >       0.1 & 1.8 & 3 & ...  \\[0.3em]
    >       1 & 1 & 2 & ...  \\[0.3em]
    >       0.2 & 3.6 & 1 & ...  \\[0.3em]
    >     \end{bmatrix}
    > $$
    > 
    > ##### Add
    > 
    > 將新的值寫入記憶體的動作為 *add* 。之所以稱為 *add* （而非 *write* ）因為這個動作是會把記憶體內原本的值，再「加上」要寫入的值。至於要把哪些值加到記憶體，則需要有一個 *add vector* ，其維度和 *memory block* 的大小 $m$  相同。 *Add* 的公式如下：
    > 
    > $$
    > \textbf{M}(i) \leftarrow  \textbf{M}(i)  + w(i) \textbf{a} \mspace{40mu} \text{(3)}
    > $$ 
    > 
    > 過程如下圖所示：
    > 
    > ![](http://lh3.googleusercontent.com/-Df2y47FgNGw/Vi5ITQnW7VI/AAAAAAAABq4/ULxq-vJWhfk/s697-Ic42/ntm5.jpeg)
    > 
    > 上圖中，位於 $\textbf{M}$  的左上角，共有四個 *cell* 的值被增加了。\
    > 將上圖中 $\textbf{w}$  、 $\textbf{a}$  和 $\textbf{M}$  中的值，代入公式(3) ，可得出此結果，如下：
    > 
    > $$
    > M= 
    > \begin{bmatrix}
    >       0.1+0.9 & 1.8+0.1 & 3 & ...  \\[0.3em]
    >       1.0+0.9 & 1.0+0.1 & 2 & ...  \\[0.3em]
    >       0.2 & 3.6 & 1 & ...  \\[0.3em]
    >     \end{bmatrix}
    > =\begin{bmatrix}
    >       1.0 & 1.9 & 3 & ...  \\[0.3em]
    >       1.9 & 1.1 & 2 & ...  \\[0.3em]
    >       0.2 & 3.6 & 1 & ...  \\[0.3em]
    >     \end{bmatrix}
    > $$
    > 
    > #### Controller
    > 
    > *Controller* 為控制器，它可以用類神經網路之類的機器學習模型來代替，但其實可以把它當成是黑盒子，只要可以符合下圖中所要求的 *input* 、 *output* 以及各種參數的值，就可以當 *controller* 。
    > 
    > ![](http://lh3.googleusercontent.com/-GBeNZB5gv2M/ViugOjalF2I/AAAAAAAABm4/AaTnvc5aQNI/s685-Ic42/ntm6.jpeg)
    > 
    > 上圖中， *controller* 根據外部環境的輸入值 *input*，以及 *read vector* $\textbf{r}$  ，經過其內部運算，會輸出 *output* 值到外在環境，還有 *erase vector* $\textbf{e}$  和 *add vector* $\textbf{a}$  ，來控制記憶體的清除與寫入。但還缺少了讀寫頭向量 $\textbf{w}$  。
    > 
    > 如果要產生讀寫頭向量 $\textbf{w}$  ， 需要透過一連串的 *Addressing Mechanisms* 的運算，最後即可得出讀寫頭位置。而 *controller* 則負責產生出 *Addressing Mechanisms* 所需的參數。
    > 
    > #### Addressing Mechanism
    > 
    > *controller* 會產生五個參數來進行 *addressing mechanisms* ，這些參數分別為： $\textbf{k}, \beta, g , \textbf{s}, \gamma$  。其中， $\textbf{k}$  和 $\textbf{s}$  為向量，其餘參數為純量，這些參數的意義，在以下篇章會解釋，整個 *addressing mechanisms* 的過程如下圖所示。
    > 
    > ![](http://lh3.googleusercontent.com/-F8lg0Kwasf8/Vium3fOAddI/AAAAAAAABoQ/Oi2uyfWz8kY/s687-Ic42/ntm30.jpeg)
    > 
    > 上圖中，總共有四個步驟，這四個步驟共需要用到這五種參數，經過了這一連串的過程之後，最後所產生出的 $\textbf{w}$  即為讀寫頭位置，如上圖左下角所示。以下細講每個步驟在做什麼。
    > 
    > ##### Content Addressing
    > 
    > 首先，是找出記憶體中跟參數 *memory key* $\textbf{k}$  值最相近的記憶體區塊。
    > 
    > 讀寫頭的位置 $\textbf{w}$ ，就先根據記憶體區塊中，跟 $\textbf{k}$  的相似度來決定，公示如下：
    > 
    > $$
    > w(i) \leftarrow \frac{e^{\beta K[\textbf{k},\textbf{M}(i)] } }{ \sum_{j} e^{ \beta K[\textbf{k},\textbf{M}(j)] } }
    > $$
    > 
    > 其中， $K[\textbf{k},\textbf{M}(i)]$  表示 *memory key* $k$  跟記憶體區塊 $M(i)$  的 *cosine similarity* ，即兩向量的夾角，如果 $\textbf{k}$  跟 $M(i)$  的內容越接近的話，則 $K[\textbf{k},\textbf{M}(i)]$  算出來的值會越大。 最後算出來的值 $w(i)$  ，即是 $\textbf{k}$  跟 $M(i)$  的相似度，除以記憶體內所有區塊相似度，標準化的結果。\
    > *cosine similarity* 的公式如下：
    > 
    > $$
    > K[\textbf{u},\textbf{v} ] = \frac{ \textbf{u} \cdot \textbf{v} }{ |\textbf{u}| \cdot |\textbf{v}| }
    > $$
    > 
    > 經過了 *cosine similarity* 後，越相似的向量，值會越大，而參數 $\beta$  是個大於0的參數，可用來控制 $\textbf{w}$  內的元素值，集中與分散程度，如下圖所示：
    > 
    > ![](https://lh3.googleusercontent.com/-c0nIcH--Mlg/ViujE8ycsvI/AAAAAAAABns/pUg5Vu7jHQk/s655-Ic42/ntm21.jpeg)
    > 
    > 上圖中，向量 $\textbf{k}$  中的值，與記憶體中第三行區塊的值最相似（用較淺色的背景表示）。但如果 $\beta$  很大（例如： $\beta=50$ ），算出來的 $\textbf{w}$  值會集中在第三個位置，也就是說，只有第三個位置的值是1，其他都是0（用較淺色的背景表示），如上圖的左下方。如果 $\beta$  很小（例如： $\beta=0$ ），則算出來的 $\textbf{w}$  值會平均分散到每個元素之中，如上圖的右下方。
    > 
    > ##### Interpolation
    > 
    > 讀寫頭其實也是有「記憶」的，也就是說，目前時間點的 $\textbf{w}_{t}$   ，也可能會受到上個時間點 $\textbf{w}_{t-1}$   的影響，要達到這樣的效果，就是用 *content addressing* 所算出的值 $\textbf{w}_{t}$   ，和上個時間點的讀寫頭位置 $\textbf{w}_{t-1}$   做 *interpolation* ，公式如下：
    > 
    > $$
    > \textbf{w}_{t} \leftarrow g \textbf{w}_{t} + (1-g) \textbf{w}_{t-1}
    > $$
    > 
    > 其中，參數 $g$  用來表示 $\textbf{w}$  有多少比例是這個時間點 *content addressing* 所算出的值，還是上個時間點的值。如下圖所示：
    > 
    > ![](http://lh3.googleusercontent.com/-lQ1ptkUtJp0/ViujE3uNTRI/AAAAAAAABnw/T6cGWHp724c/s630-Ic42/ntm22.jpeg)
    > 
    > 如果 $g=1$  ，則 $\textbf{w}$  的值會完全取決於這個時間點 *content addressing* 所算出的值，如上圖的左下方，若 $g=0$  ， $\textbf{w}$  會完全取決於上個時間點的值，如上圖的右下方。
    > 
    > ##### Convolutional Shift
    > 
    > 如果要讓讀寫頭的位置可以稍微往左或往右移動，這就要用 *Convolutional Shift* 來做調整。 參數 $\textbf{s}$  是一個向量，用 *convolutional shift* ，來將 $\textbf{w}$  的值往左或往右平移，公式如下：
    > 
    > $$
    > w(i) \leftarrow \sum_{j} w(j) s(i-j)
    > $$ 
    > 
    > 舉個例子，如果 $\textbf{s}$  中有三個元素：$s_{-1}, s_{0}, s_{1}$   ，則 $w(i)$  經過了以上公式後，結果如下：
    > 
    > $$
    > w(i) \leftarrow w(i+1) s(-1) + w(i)s(0) + w(i-1)s(1)
    > $$ 
    > 
    > 根據此公式， $w(i)$  的值，如下圖所示：
    > 
    > ![](http://lh3.googleusercontent.com/--G27BIV4OwM/ViuoNOb7eXI/AAAAAAAABo8/mHoSBYow0d4/s228-Ic42/ntm231.jpeg)
    > 
    > 也就是說， $s_{-1}=1$  時，可讓原本的 $w_{i+1}$   往左移一格，移到 $w_{i}$  ，若 $s_{1}=1$  時，可讓原本的 $w_{i-1}$   往右移一格，移到 $w_{i}$   。
    > 
    > 舉個例子，如果 $s_{-1} = 1, s_{0}=0, s_{1} = 0$  ，則 $w$  中的值，全部往左移動一格，若碰到邊界則再循環到最右邊，如下圖左方所示。 如果 $s_{-1} = 0, s_{0}=0, s_{1} = 1$  ，則 $w$  中的值，全部往右移動一格。若 $s_{-1} = 0.5, s_{0}=0, s_{1} = 0.5$  ，則 $w$  為往左和往右移動後的平均，如下圖右方所示。
    > 
    > ![](http://lh3.googleusercontent.com/-IWyC4L0Tvys/ViujE_Wu9DI/AAAAAAAABno/gWkTYygp9p4/s675-Ic42/ntm23.jpeg)
    > 
    > ##### Sharpening
    > 
    > 此過程是再一次調整 $w$  的集中與分散程度，公示如下：
    > 
    > $$
    > w(i) \leftarrow \frac{w(i)^{\gamma}}{\sum_{j}w(j)^{\gamma}}
    > $$
    > 
    > 其中， $\gamma$  的功能和 *Content Addressing* 中的 $\beta$  是一樣的，但是經過了接下來的 *Interpolation* 跟 *Convolutional Shift* 之後，$w$  裡面的集中度又會改變，所以要再重新調整一次。
    > 
    > ![](http://lh3.googleusercontent.com/-weBeNSLG80Y/ViujFvEcA-I/AAAAAAAABn4/bTTGIqL3fhE/s666-Ic42/ntm24.jpeg)
    > 
    > ### Experiment: Repeat Copy
    > 
    > 關於 *Neural Turing Machine* 的學習能力，可以參考以下例子。
    > 
    > 在訓練資料中，給定一個區塊的 *data* （如下圖左上角紅色區塊）做為 *input data* ，將這個區塊複製成七份，做為 *output data* 。則 *Neural Turing Machine* 有辦法學會這個「複製」過程所需的運算程序，也就是重複跑七次輸出一樣的東西。
    > 
    > ![](http://lh3.googleusercontent.com/-5z_sGMUPFco/Vi5U2g77jPI/AAAAAAAABrg/kzJDk0uX5jM/s596-Ic42/repeatcopy7_h1.png)
    > 
    > ![](http://lh3.googleusercontent.com/-5xG74uII2Yk/Vi5U2poqyeI/AAAAAAAABrc/qFlVYt-ccrk/s575-Ic42/repeatcopy7_h2.png)
    > 
    > 從上圖中，可看到讀寫頭的移動，重複走了相同的路徑，走了七次，依序將記憶體中儲存的 *input data* 的值，讀出來並輸出到 *output* 。
    > 
    > 有個完整的 *Neural Turing Machine* 套件，以及此實驗的相關程式碼於：<https://github.com/fumin/ntm>
    > 
    > ### Reference
    > 
    > [Alex Graves, Greg Wayne, Ivo Danihelka. Neural Turing Machines. 2014](http://arxiv.org/abs/1410.5401)
    > 

## Memory Networks



- [[1410.3916] Memory Networks](https://arxiv.org/abs/1410.3916)
    - [记忆网络-Memory Network](https://zhuanlan.zhihu.com/c_129532277)


- [[1503.08895] End-To-End Memory Networks](https://arxiv.org/abs/1503.08895)
    - [记忆网络之End-To-End Memory Networks](https://zhuanlan.zhihu.com/p/29679742)

- [End-to-End Memory Networks · ZMonster's Blog](http://www.zmonster.me/notes/end-to-end-memory-networks.html)

    > 这篇论文是在看 [Hierarchical Memory Networks for Answer Selection on Unknown Words](http://www.zmonster.me/notes/hmn_for_qa.html) 时追过去的 ------ 这篇论文里有些东西讲的不明不白，还好它里面说明一些思想来自哪里。
    > 
    > 论文标题为 "End-to-End Memory Networks" ，很显然这篇论文是基于 Memory Networks 来做了一些工作，按照惯例，论文在开头说了一些原始的 Memory Networks 的缺点:
    > 
    > 1.  Memory Networks 难以进行 BP 训练
    > 2.  Memory Networks 需要更多的 supervision(这个没太懂，回头把 Memory Networks 再看一下)
    > 
    > 模型的基本结构如下图所示。
    > 
    > ![memn2n_single_layer.png](http://www.zmonster.me/assets/img/memn2n_single_layer.png)
    > 
    > 模型的输入包含两部分，一个是图左端那个「Sentences」，即由多个句子组成的内容，这些句子会被输入到网络中并储存为「memory」，可以认为是在检索/问答时的历史信息或者说上下文；另一部分是 query 或说 question，就是图中下端那个 q，也是一个句子。模型最后的输出也是一个句子。
    > 
    > 模型的输出，按照我对这张图的理解，应该是一个经过 softmax 的 d 维向量(d 是 vocabulary 的大小)，但是这样的话就只能输出一个词了？从后面的实验部分来看确实是这样的，总感觉这样的话并不是很适用于常规的 QA 任务了。
    > 
    > 输入的 Sentences，首先通过 embedding 矩阵 A 得到 input memory。其实就是将每一个句子 encode 成一个向量，也就是图上的 mi
    > 
    > ，这些 mi
    > 
    > 组合起来就得到 input memory，也就是涂上标为 **Input** 的那块矩形 M。问题 q 同样通过 embedding 矩阵 B 来 encode 成一个向量 u，然后用 u 和 M 內积得到一个权值向量:
    > 
    > $$
    > p=softmax(u^{T}M)
    > $$
    > 
    > 接着，输入的 Sentences 通过另外一个 embedding 矩阵 C 得到另外一个 memory 表示，也就是图上标为 **Output** 的那块矩形 C，然后用上一步得到的权值向量来对 C 进行加权求和:
    > 
    > $$
    > o=\sum_{i}p_{i}c_{i}
    > $$
    > 
    > 对于这部分，我的理解是，u 和 M 的內积相当于一个 attention，得到 attention 后，就用来在用于输出的 memory 也就是 C 中进行检索得到输出结果。不过还是有些地方不太明白，比如说反映在网络结构上，u 和 M 的內积是怎么体现的？输入连接两个 embedding 矩阵又是怎么体现的？
    > 
    > 在得到输出向量 o 后，按理来说直接 softmax 就可以得到结果吧，但是这里却和 question 的向量 u 做了一个加法才进行 softmax，不是很懂，也许和 ResNet 的那个 residual connection 是同样的思想？但是 2015 年 3 月份(这篇论文的发表时间)的时候 ResNet 还没有正式发表吧。
    > 
    > 以上就是单层时的情况，多层的时候就用前一层的(未经过 softmax 的)输出作为本层的输入向量 u，即
    > 
    > $$
    > u^{k+1} = o^{k}+u^{k}
    > $$
    > 
    > 一图胜千言:
    > 
    > ![memn2n_multi_layer.png](http://www.zmonster.me/assets/img/memn2n_multi_layer.png)
    > 
    > 在多层结构的时候，作者又对 "weight typing" 做了不同的尝试 ------ 不知道「weight typing」该怎么翻译，且看下文吧。
    > 
    > 可以看到，在上面的多层网络结构中，每一层都有一个 A 和 C，对 A 和 C 的处理，有两种方式:
    > 
    > 1.  Adjacent: 将前一层的输出 embedding 矩阵 C 作为本层的输入 embedding 矩阵 A: $A^{k+1}=C^{k}$ 
    > 2.   Layer-wise: 像 RNN 一样，所有输入 embedding 矩阵 A 共享参数: $A^{1}=A^{2}=...=A^{K}$ ，输出矩阵 C 同理
    > 
    > 在对句子的 encode 上，也有两种不同的处理方式:
    > 
    > 1.  BoW: 简单的将句子中每个词的 embedding 累加起来: $m_{i}=\sum_{j}Ax_{ij}$，u 和 $c_{i}$   的计算同理
    > 2.  position encoding: $m_{i}=\sum_{j}l_{j}\cdot Ax_{ij}$，这里的 $l_{j}$ 就是所谓的反映了词序的 position encoding，它和后面的值进行 element-wise 的乘法而不是內积，而这个 position encoding 的计算方法是: $l_{kj}=(1-j/J)-(k/d)(1-2j/J)$，其中 j 是词在句子中的位置，J 是句子的长度，k 是这个词的 vocabulary id，d 是 vocabulary 的大小。
    > 
    > 此外就是 Sentences 中的句子之间也是有次序的，为了反映这个次序，又在计算 $m_{i}$ 和 $c_{i}$ 时加了一个额外的叫做 temporal encoding 的东西，分别记为 $T_{A}(i)$ 和 $T_{C}(i)$ :
    > 
    > $$
    > m_{i}=\sum_{j}Axij + T_{A}(i)
    > $$
    > 
    > 但是并没有说 $T_{A}(i)$ 和 $T_{C}(i)$ 是如何表现的，只是带了一句: Both $T_{A}$ and $T_{C}$ are learnd during training。另外，在模型中，句子的次序对真实的次序而言是倒序的。
    > 
    > 作者提出这个模型除了用在 QA 上外，还在语言模型上做了实验。在做语言模型时，是没有 question/query 的，所以 u 被设置为一个常量的向量(值都为 0.1)；然后每个 $m_{i}$ 和 $c_{i}$ 都是对应一个词而不是一个句子了，因为 LM 是 word-level 的问题嘛。
    > 
    > 最后总结一下，本文的主要贡献是增强了原始的 Memory Networks，让其称为一个端到端的模型，能更方便地使用 BP 方法进行训练。
    > 
    > 就酱！