# AI__硬體介紹與環境設定

<!-- toc --> 
[toc]

## 我的深度學習專用機 My Deep Learning Box

- [原價屋估價](http://www.coolpc.com.tw/evaluate.php)

- 主機：ASRock DeskMini250 GTX (__~\$46400__) [time=Oct 07, 2017]
    - 空機 (主機板+網卡) (__~\$13900__)
    - GPU：NVIDIA GTX1070 (MXM介面) (__~\$22500__)
    - CPU：Intel Pentium G4600 (3.6Ghz) (效能近i3-7100) (__~\$2150__)
    - RAM：Crucial DDR4-2400 16G (__~\$4400__)
    - SSD：Plextor M8PeG 256G NVMe  (__~\$3450__)
    - HDD：Seagate 2T SATA (2.5inch) (__~\$3450__)
- 螢幕：LG 22MP58VQ-P 22型AH-IPS寬螢幕 (__~\$2588__)

- ASRock DeskMini250 介紹
    - [Computex 2017：看ASRock把GTX 1080塞到小鋼砲電腦裡 (124873) - 癮科技](https://www.cool3c.com/article/124873)
    - [ASRock > DeskMini GTX/RX](http://www.asrock.com/nettop/Intel/DeskMini%20GTXRX/index.tw.asp#Specification)

- 筆電MXM顯卡介紹
    - [制霸筆電 NVIDIA GTX 1080 / 1070 / 1060 GPU 直上電競筆電 性能大勝 今非昔比 - 電腦DIY](https://www.computerdiy.com.tw/nvidia-gtx-10-series-notebooks/)

- G4600 與 i3 7100 效能規格差不多，只有差在AVX 指令集(dlib 有 AVX 支援編譯版)
    [G4600 vs i3 7100 - BENCHMARKS / GAMING TESTS REVIEW AND COMPARISON / Kaby Lake vs Kaby Lake - YouTube](https://www.youtube.com/watch?v=frrn0tzNJWA)


## Hardware suggestion

- [A Full Hardware Guide to Deep Learning - Tim Dettmers](http://timdettmers.com/2015/03/09/deep-learning-hardware-guide/)

- [Deep Confusion: Misadventures In Building A Deep Learning Machine - TOPBOTS](https://www.topbots.com/deep-confusion-misadventures-in-building-a-machine-learning-server/)

- [Tim Dettmers's answer to Why are GPUs well-suited to deep learning? - Quora](https://www.quora.com/Why-are-GPUs-well-suited-to-deep-learning/answer/Tim-Dettmers-1)

- [System Builder - Core i5-7500 3.4GHz Quad-Core, GeForce GTX 1080 Ti 11GB Founder Edition - PCPartPicker](https://pcpartpicker.com/list/T6wHjc)

- [I: Building a Deep Learning (Dream) Machine – Machine Ponderings](https://graphific.github.io/posts/building-a-deep-learning-dream-machine/)

- [Kaggle: Your Home for Data Science](https://www.kaggle.com/general/23519)

- [Optimizing a Starter CUDA Machine Learning / AI / Deep Learning Build](https://www.servethehome.com/optimizing-a-starter-cuda-machine-learning-ai-deep-learning-build/)

- [What laptop is best for deep learning experiments? - Quora](https://www.quora.com/What-laptop-is-best-for-deep-learning-experiments)


### Cost vs Performance

- [The \$1700 great Deep Learning box: Assembly, setup and benchmarks](https://blog.slavv.com/the-1700-great-deep-learning-box-assembly-setup-and-benchmarks-148c5ebe6415)
- [Build a Deep Learning Rig for \$800 – Towards Data Science](https://towardsdatascience.com/build-a-deep-learning-rig-for-800-4434e21a424f)

- [Early Experiences with Deep Learning on a Laptop with Nvidia GTX 1070 GPU – part 1 – Amund Tveit's Blog](https://amundtveit.com/2017/02/28/deep-learning-on-a-laptop-with-nvidia-gtx-1070-gpu-part-1/)

    **1\. Choice of GPU**  
    I decided on the GTX 1070 GPU since it had

    1.  Same amount of GPU RAM as GTX 1080 – 8 GB – enough to develop or test a large range of CNN and GAN models
    2.  Was cheaper and used less energy than GTX 1080
    3.  High performance

    **2\. Choice of Laptop and Configuration**

    I first installed Ubuntu 14.04 with Cuda (8.0), cuDNN, Nvidia drivers, nvidia-docker and then later upgraded to Ubuntu 16.04 – check out the blog post (by Donald Kinghorn) [Install Ubuntu 16.04 or 14.04 and CUDA 8 and 7.5 for NVIDIA Pascal GPU](https://www.pugetsystems.com/labs/hpc/Install-Ubuntu-16-04-or-14-04-and-CUDA-8-and-7-5-for-NVIDIA-Pascal-GPU-825/). Then I [installed TensorFlow](https://www.tensorflow.org/install/install_linux) and [Pytorch](http://pytorch.org/), got some issues with GPU support for Pytorch but I assume it is just finger trouble on my side, but Tensorflow worked nicely on the GPU as you can see in the section below.

    **3\. Example training the Pix2Pix Conditional Adversarial Network in TensorFlow on the Laptop**

    To test Deep Learning on the laptop I chose the [pix2pix-tensorflow](https://github.com/yenchenlin/pix2pix-tensorflow) project, see examples below followed by a gif of actual training on the laptop.

    **Appendix – Deep Learning benchmark of Nvidia GTX 1070**

    _The benchmark in the table below – from [github.com/tobigithub/tensorflow-deep-learning/wiki/tf-benchmarks](https://github.com/tobigithub/tensorflow-deep-learning/wiki/tf-benchmarks) – was very favorable in the direction of 1070 (note that this compares 1080 and 1070 to older generation GPUs)_

    ![](https://amundtveit.com/wp-content/uploads/2017/02/gpuperf.png)

### GPU Choose

- just considering...
    1. floting point precision
    2. memory size

- [Which GPU(s) to Get for Deep Learning - Tim Dettmers](http://timdettmers.com/2017/04/09/which-gpu-for-deep-learning/)

    **Best GPU overall (by a small margin)**: Titan Xp  
    **Cost efficient but expensive**: GTX 1080 Ti, GTX 1070, GTX 1080  
    **Cost efficient and cheap**:  GTX 1060 (6GB)  
    **I work with data sets > 250GB**: GTX Titan X (Maxwell), NVIDIA Titan X Pascal, or NVIDIA Titan Xp  
    **I have little money**: GTX 1060 (6GB)  
    **I have almost no money**: GTX 1050 Ti (4GB)  
    **I do Kaggle**: GTX 1060 (6GB) for any "normal" competition, or GTX 1080 Ti for "deep learning competitions"  
    **I am a competitive computer vision researcher**: NVIDIA Titan Xp; do not upgrade from existing Titan X (Pascal or Maxwell)  
    **I am a researcher**: GTX 1080 Ti. In some cases, like natural language processing, a GTX 1070 or GTX 1080 might also be a solid choice — check the memory requirements of your current models  
    **I want to build a GPU cluster**: This is really complicated, you can get some ideas [here](http://timdettmers.com/2014/09/21/how-to-build-and-use-a-multi-gpu-system-for-deep-learning/)  
    **I started deep learning and I am serious about it**: Start with a GTX 1060 (6GB). Depending of what area you choose next (startup, Kaggle, research, applied deep learning) sell your GTX 1060 and buy something more appropriate  
    **I want to try deep learning, but I am not serious about it**: GTX 1050 Ti (4 or 2GB)



- [Choosing between GeForce or Quadro GPUs to do machine learning via TensorFlow - Stack Overflow](https://stackoverflow.com/questions/34715055/choosing-between-geforce-or-quadro-gpus-to-do-machine-learning-via-tensorflow)  

    I think GeForce TITAN is great and is widely used in Machine Learning (ML). In ML, single precision is enough in most of cases.

    More detail on the performance of the GTX line (currently GeForce 10) can be found in Wikipedia, [here](https://en.wikipedia.org/wiki/GeForce_10_series).

    Other sources around the web support this claim. Here is a quote [from doc-ok in 2013](http://doc-ok.org/?p=304) ([permalink](https://perma.cc/GH7A-8UUX)).

    > For comparison, an "entry-level" \$700 Quadro 4000 is significantly slower than a \$530 high-end GeForce GTX 680, at least according to my measurements using several Vrui applications, and the closest performance-equivalent to a GeForce GTX 680 I could find was a Quadro 6000 for a whopping \$3660.

    Specific to ML, including deep learning, there is a [Kaggle forum discussion dedicated to this subject](https://www.kaggle.com/general/11332) (Dec 2014, [permalink](https://perma.cc/RBZ6-YX9F)), which goes over comparisons between the Quadro, GeForce, and Tesla series:

    > Quadro GPUs aren't for scientific computation, Tesla GPUs are. Quadro cards are designed for accelerating CAD, so they won't help you to train neural nets. They can probably be used for that purpose just fine, but it's a waste of money.
    > 
    > Tesla cards are for scientific computation, but they tend to be pretty expensive. The good news is that many of the features offered by Tesla cards over GeForce cards are not necessary to train neural networks.
    > 
    > For example, Tesla cards usually have ECC memory, which is nice to have but not a requirement. They also have much better support for double precision computations, but single precision is plenty for neural network training, and they perform about the same as GeForce cards for that.
    > 
    > One useful feature of Tesla cards is that they tend to have is a lot more RAM than comparable GeForce cards. More RAM is always welcome if you're planning to train bigger models (or use RAM-intensive computations like FFT-based convolutions).
    > 
    > If you're choosing between Quadro and GeForce, definitely pick GeForce. If you're choosing between Tesla and GeForce, pick GeForce, unless you have a lot of money and could really use the extra RAM.

    **NOTE:** Be careful what platform you are working on and what the default precision is in it. For example, [here in the CUDA forums](https://devtalk.nvidia.com/default/topic/959375/cuda-programming-and-performance/performance-issues-with-cuda-and-python-r/1) (August 2016), one developer owns two Titan X's (GeForce series) and doesn't see a performance gain in any of their R or Python scripts. This is diagnosed as a result of R being defaulted to double precision, and has a worse performance on new GPU than their CPU (a Xeon processor). Tesla GPUs are cited as the best performance for double precision. In this case, converting all numbers to float32 increases performance from 12.437s with nvBLAS 0.324s with gmatrix+float32s on one TITAN X (see first benchmark). Quoting from this forum discussion:

    > Double precision performance of Titan X is pretty low.



- [Performance Issues with CUDA and Python/R - NVIDIA Developer Forums](https://devtalk.nvidia.com/default/topic/959375/cuda-programming-and-performance/performance-issues-with-cuda-and-python-r/1)

    > If R is using double precision data, Titan X is not the right card to use. Double precision performance of Titan X is pretty low. [name=mfatica]
    
    > The best **double precision** performance per dollar is, by far, found with a Kepler based Titan or Titan Black, not a Maxwell or Pascal Titan X.  
    >
    >　A Titan Black is about \$500 on eBay (used) and gives you about 1700 DP gigaflops. A Titan is about \$350 and gives about 1400 DP gigaflops.  
    >
    > Your Maxwell Titan X is only about 192 DP gigaflops, but has a tremendous single precision throughput of 6000 gigaflops. Pascal Titan X is 300 DP, 10000 SP.  
    >
    > If you want the most powerful double precision option, a DGX-1 is a totally different class and gives you 37600 DP gigaflops for $129,000. [name=SPWorley]

- [Which GPU to use for deep learning? | LinkedIn](https://www.linkedin.com/pulse/20141013042457-89310056-which-gpu-to-use-for-deep-learning/)

    > "Another important factor to consider however, is that the Fermi architecture (400 and 500 series) is quite a bit faster than the newer Kepler architecture (600 and 700 series)"
    >
    > However, Alex’s [CudaConvnet2](https://code.google.com/p/cuda-convnet2/) package has done some optimization for Kepler cards, compared to previous version which is more suitable to run on a Fermi card. So I am not sure whether this statement would still be true or not.

    > GTX titan serials have much better double float computing performance than GTX 780/780Ti, but it is said in Eric Battenberg’s post that train deep learning model does not require double float computing.
    > 
    > GTX 780Ti is much more powerful than GTX 780 (look for specs in the [wiki table](http://en.wikipedia.org/wiki/GeForce_700_series#GeForce_700_.287xx.29_series)), with only a little bit more expensive than GTX 780, so sounds like GTX 780Ti is the best w.r.t performance/price ratio.

- [What are the downsides of the NVIDIA's GTX 1080 vs Titan X when used for deep learning? - Quora](https://www.quora.com/What-are-the-downsides-of-the-NVIDIAs-GTX-1080-vs-Titan-X-when-used-for-deep-learning)

    > The Nvidia’s GTX 1080 has 8GB of RAM vs 12GB for the TitanX. This limits the amount of data (mini-batch size or how deep your network can be) although from a speed perspective pascal architecture is much faster. However leading deep learning platforms including Caffe will soon support 16 bit floating point (instead of 32bit). With 16bit precision (FP16), you can load more data for training equivalent to 16GB of FP32 (either bigger batch sizes or more layers).
    > 
    > Update (6/7/2016): It appears that FP16 is working way slower than FP32 in NVIDIA’s 1080. You can read more here: [https://devtalk.nvidia.com/defau...](https://devtalk.nvidia.com/default/topic/934562/cuda-programming-and-performance/nvidia-pascal-geforce-gtx-1080-amp-gtx-1070/post/4889687/) [name=Siddharth Mohan]

    > The 1080 has indeed the 16-bit support but these instructions are 1/64th slower than the 32-bits’s
    > [name=Djébril Mokaddem]

    > Nvidia's marketing material claims that GTX 1080 has 10TFlops performance as compared to GTX 980 Ti at 7TFlops performance. Titan X is equivalent to a GTX 980 Ti however with 12GB of memory instead of 4-6GB of memory. So, in comparison, GTX 1080 has higher compute capability but with less memory (i.e. 8GB). The price however for a GTX 1080 (~6oo USD) is much lower than a Titan X (~1,000 USD). The Titan X prices however could drop when the GTX 1080 is released.
    > 
    > In general, it is best to favor more memory for a Deep Learning application. So if we make the assumption that both are selling for the same price, then a Titan X is a better deal than a GTX 1080.
    > 
    > Update: Nvida just released info on [The New NVIDIA TITAN X: The Ultimate. Period. | The Official NVIDIA Blog](https://blogs.nvidia.com/blog/2016/07/21/titan-x/) It has 12GB of memory and 11TFlops performance. The above comment refers to the OLD Titan X. [name=Carlos E. Perez]

### HDD vs SSD

- [incubator-mxnet/example/image-classification at master · apache/incubator-mxnet](https://github.com/apache/incubator-mxnet/tree/master/example/image-classification)

    -   SSD is much faster than HDD when dealing with a large number of small files. (but HDD is good enough to read `rec` files).
        -   We can use a cloud storage instance to prepare the data. For example, AWS `i2.4xlarge` provides 4 x 800 GB SSDs.

        -   We can make a software RAID over multiple disks. For example, the following command create a RAID0 on 4 disks:

            ```shell
            sudo mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 \
              /dev/nvme0n1 /dev/nvme1n1 /dev/nvme2n1 /dev/nvme3n1
            sudo mkfs /dev/md0
            ```

    -   Check `*.sh` scripts in the `data/` folder for more examples
    -   Use `im2rec.py --help` to see more options.

- [Training Deep Net on 14 Million Images by Using A Single Machine](http://dmlc.ml/mxnet/2015/10/27/training-deep-net-on-14-million-images.html)

    Data Preprocessing
    ------------------

    The raw full ImageNet dataset is more than 1TB. Before training the network, we need to shuffle these images then load batch of images to feed the neural network. Before we describe how we solve it, let’s do some calculation first:

    Assume we have two good storage device \[2\]:

    | Device | 4K Random Seek | Sequential Seek |
    | --- | --- | --- |
    | WD Black (HDD) | 0.43 MB /s (110 IOPS) | 170 MB/s |
    | Samsung 850 PRO (SSD) | 40 MB/s (10,000 IOPS) | 550 MB/s |

    A very naive approach is loading from a list by random seeking. If use this approach, we will spend 677 hours with HDD or 6.7 hours with SSD respectively. This is only about read. Although SSD looks not bad, but 1TB SSD is not affordable for everyone.

    But we notice sequential seek is much faster than random seek. Also, loading batch by batch is a sequential action. Can we make a change? The answer is we can’t do sequential seek directly. We need random shuffle the training data first, then pack them into a sequential binary package.

    This is the normal solution used by most deep learning packages. However, unlike ImageNet 1K dataset, where we **_cannot_** store the images in raw pixels format. Because otherwise we will need more than 1TB space. Instead, we need to pack the images in compressed format.

    **_The key ingredients are_**

    -   Store the images in jpeg format, and pack them into binary record.
    -   Split the list, and pack several record files, instead of one file.
        -   This allows us to pack the images in distributed fashion, because we will be eventually bounded by the IO cost during packing.
        -   We need to make the package being able to read from several record files, which is not too hard. This will allow us to store the entire imagenet dataset in around 250G space.

    After packing, together with threaded buffer iterator, we can simply achieve an IO speed of around 3,000 images/sec on a normal HDD.


### Benchmark
- [Benchmarks  |  TensorFlow](https://www.tensorflow.org/performance/benchmarks)

- [DeepMark/deepmark: THE Deep Learning Benchmarks](https://github.com/DeepMark/deepmark)

- [soumith/convnet-benchmarks: Easy benchmarking of all publicly accessible implementations of convnets](https://github.com/soumith/convnet-benchmarks)

- [baidu-research/DeepBench: Benchmarking Deep Learning operations on different hardware](https://github.com/baidu-research/DeepBench)

- [cnn-benchmarks/README.md at master · jcjohnson/cnn-benchmarks](https://github.com/jcjohnson/cnn-benchmarks/blob/master/README.md)

    Benchmarks for popular convolutional neural network models on CPU and different GPUs, with and without cuDNN.

    Some general conclusions from this benchmarking:

    -   **Pascal Titan X > GTX 1080**: Across all models, the Pascal Titan X is **1.31x to 1.43x** faster than the GTX 1080 and **1.47x to 1.60x** faster than the Maxwell Titan X. This is without a doubt the best card you can get for deep learning right now.
    -   **GTX 1080 > Maxwell Titan X**: Across all models, the GTX 1080 is **1.10x to 1.15x** faster than the Maxwell Titan X.
    -   **ResNet > VGG**: ResNet-50 is faster than VGG-16 and more accurate than VGG-19 (7.02 vs 9.0); ResNet-101 is about the same speed as VGG-19 but much more accurate than VGG-16 (6.21 vs 9.0).
    -   **Always use cuDNN**: On the Pascal Titan X, cuDNN is **2.2x to 3.0x** faster than nn; on the GTX 1080, cuDNN is **2.0x to 2.8x** faster than nn; on the Maxwell Titan X, cuDNN is **2.2x to 3.0x** faster than nn.
    -   **GPUs are critical**: The Pascal Titan X with cuDNN is **49x to 74x** faster than dual Xeon E5-2630 v3 CPUs.




## Software/Hardware Architecture

- [Tutorial on Hardware Architectures for Deep Neural Networks](http://eyeriss.mit.edu/tutorial.html)

### GPU architecture

- [GPU: nvidia architecture comparison(1. Fermi 2.Kepler 3. Maxwell 4. Pascal 5. Tesla) | LinkedIn](https://www.linkedin.com/pulse/gpu-nvidia-architecture-comparison1-fermi-2kepler-3-maxwell-chi/)

    > ### Fermi GPU:
    > 
    > Released in 2010, NVIDIA engineers set out to design a new GPU architecture. The architecture defines a GPU's building blocks, how they're connected, and how they work.
    > 
    > Named after the Italian nuclear physicist Enrico Fermi, Fermi is to incorporate full geometry processing to the GPU, enabling a key DirectX 11 technique called tessellation with displacement mapping.
    > 
    > ### Kepler GPU:
    > 
    > Released in 2012, NVIDIA unveiled its plans to join the cloud gaming space. They’re developed specifically for the GRID and efficient in HPC setup. It has Graphics Processing Clusters (or GPCs), each of which contained a raster engine and four Streaming Multiprocessor (or SM) units. GPU Boost for automatic overclocking.
    > 
    > ### Maxwell GPU:
    > 
    > Released in 2014, Maxwell-based GPU has new Dynamic Super Resolution (or DSR) that’s designed to put 4K-quality content on lower-resolution screens. Maximum Ram will 12gb (Titan X or Quadro M6000) whereas Pascal 32GB of video memory. Quad SLI in Maxwell upto 4 Graphics card whereas Pascal upto 8 Graphics Card.
    > 
    > ### Pascal GPU:
    > 
    > Released in 2016, Pascal is designed for the best scalability and Pascal will be priced at a premium because it is a more expensive product as HBM2 and NVLink included.
    > 
    > HBM2 for Bandwidth and NVLink to improve unified virtual addressing scheme across the GPUs and between CPUs and GPUs. So it has capable of allowing data to move 5% to 12% faster across CPUs and GPUs compared to PCI-Express.
    > 
    > ### Conclusion:
    > 
    > Even after a new technology is introduced, sometimes the old one can be had at a much cheaper price and therefore continues to be a good price/performer since there is no end of life.
    > 
    > 25 Times More Performance from Fermi to Kepler GPU
    > 
    > 35 Times More Performance from Kepler to Maxwell GPU
    > 
    > 10 Times More performance from Maxwell to Pascal GPU
    > 
    > Also, when compare the three generations of Graphics card on their raw performance alone, the Pascal does better than the Kepler or Maxwell cards .
    > 
    > 
    >| Architecture | Fermi | Kepler |  Maxwell | Pascal  | Volta |
    >|--            |--     |--      |--        |--       |--     |
    >| GPU Design   | SM    | SMX    | SMM      | SMP Max ||
    >|VRAM|1.5GB GDDR5|6GB GDDR5|12 GB GDDR5|16/32 GB HBM2|12GB HBM2|
    >|Max Bandwidth|192 GB/s|336 GB/s|336 GB/s|1 TB/s|652.8GB/s|
    > 
    > 
    > NVIDIA Volta GPUs, successors to Pascal Architecture.

- [Inside Volta: The World’s Most Advanced Data Center GPU | NVIDIA Developer Blog](https://devblogs.nvidia.com/inside-volta/?ncid=so-lin-vt-13919)

- [FP16 Throughput on GP104: Good for Compatibility (and Not Much Else) - The NVIDIA GeForce GTX 1080 & GTX 1070 Founders Editions Review: Kicking Off the FinFET Generation](https://www.anandtech.com/show/10325/the-nvidia-geforce-gtx-1080-and-1070-founders-edition-review/5)

    > Pascal introduces a new type of FP32 CUDA core that supports a form of FP16 execution where two FP16 operations are run through the CUDA core at once (vec2). This core, which for clarity I’m going to call an FP16x2 core, allows the GPU to process 1 FP32 or 2 FP16 operations per clock cycle, essentially doubling FP16 performance relative to an identically configured Maxwell or Kepler GPU.
    > 
    > 
    > ![](https://images.anandtech.com/doci/10325/FP16x2_575px.png)
    > 
    > Now there are several special cases here due to the use of vec2 – packing together operations is not the same as having native FP16 CUDA cores – but in a nutshell NVIDIA can pack together FP16 operations as long as they’re the same operation, e.g. both FP16s are undergoing addition, multiplication, etc.
    > 
    > Pascal isn’t just faster than Maxwell overall, but when it comes to FP16 operations on the FP16x2 core, Pascal is a **lot** faster, with theoretical throughput over similar Maxwell GPUs increasing by over three-fold thanks to the combination of overall speed improvements and double speed FP16 execution.
    > 
    > GeForce GTX 1080, on the other hand, is **not** faster at FP16. In fact it’s downright slow. For their consumer cards, NVIDIA has severely limited FP16 CUDA performance. GTX 1080’s FP16 instruction rate is 1/128th its FP32 instruction rate, or after you factor in vec2 packing, the resulting theoretical performance (in FLOPs) is 1/64th the FP32 rate, or about 138 GFLOPs.
    > 
    > As it turns out, when it comes to FP16 NVIDIA has made another significant divergence between the HPC-focused GP100, and the consumer-focused GP104. On GP100, these FP16x2 cores are used throughout the GPU as both the GPU’s primarily FP32 core and primary FP16 core. However on GP104, NVIDIA has retained the old FP32 cores.
    > 
    > The lack of a significant number of FP16x2 cores is why GP104’s FP16 CUDA performance is so low as listed above. There is only 1 FP16x2 core for every 128 FP32 cores.
    > 
    > FP64 has been treated as a Tesla feature since the beginning, and consumer parts have either shipped with a very small number of FP64 CUDA cores for binary compatibility purposes, or when a GeForce card uses an HPC-class GPU, FP64 performance is artificially restricted.
    > 
    > However in the case of FP64, performance has never been slower than 1/32, whereas with FP16 we’re looking at a much slower 1/128 instruction rate.
    > 
    > ![](https://screenshotscdn.firefoxusercontent.com/images/2a3517ba-a92f-4a90-b312-5b88bee58d1a.png)
    > 
    > Overall I’m not surprised that NVIDIA limited the FP16 performance of the GTX 1080 – albeit by a new record – as they clearly consider faster FP16 performance a feature that can be monetized under Tesla.
    > 
    > At the same time NVIDIA has still yet to disclose the dGPUs used with the DRIVE PX 2 module, where again fast FP16 support is useful for neural network inference.
    > 
    > 



### NVLink

- [NVLink - Wikiwand](https://www.wikiwand.com/en/NVLink)

    > Performance[](https://en.wikipedia.org/w/index.php?title=NVLink&action=edit&section=2)
    > --------------------------------------------------------------------------------------
    > 
    > The following table shows a comparison of relevant bus parameters for real world semiconductors that all offer NVLink as one of their options:
    > 
    > | Semiconductor | Interconnect | Transmission  Technology  Rate (per lane) | Lanes per  Sub-Link  (out + in) | Sub-Link Data Rate  (per data direction) | Sub-Link  Count | Total Data Rate  (out + in) | Total  Lanes  (out + in) | Total  Data Rate  (out + in) |
    > | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    > | Nvidia P100[\[3\]](https://www.wikiwand.com/en/NVLink#citenote3) | PCIe 3.0 |  8 GT/s | 16 + 16 **Ⓑ** | 128 Gbit/s = 16 GByte/s | 1 |  16 +  16 GByte/s[\[4\]](https://www.wikiwand.com/en/NVLink#citenote4) | 32 **Ⓒ** |  32 GByte/s |
    > | [IBM Power9](https://www.wikiwand.com/en/POWER9#I.2FO "POWER9")[\[5\]](https://www.wikiwand.com/en/NVLink#citenote5) | PCIe 4.0 | 16 GT/s | 16 + 16 **Ⓑ** | 256 Gbit/s = 32 GByte/s | 3 |  96 +  96 GByte/s | 48 | 192 GByte/s |
    > | Nvidia P100 | NVLink 1.0 | 20 GT/s |  8 +  8 **Ⓐ** | 160 Gbit/s = 20 GByte/s | 4 |  80 +  80 GByte/s | 64 | 160 GByte/s |
    > | [IBM Power8+](https://www.wikiwand.com/en/POWER8#POWER8_with_NVLink "POWER8") | NVLink 1.0 | 20 GT/s |  8 +  8 **Ⓐ** | 160 Gbit/s = 20 GByte/s | 4 |  80 +  80 GByte/s | 64 | 160 GByte/s |
    > | Nvidia V100 | NVLink 2.0 | 25 GT/s |  8 +  8 **Ⓐ** | 200 Gbit/s = 25 GByte/s | 6[\[6\]](https://www.wikiwand.com/en/NVLink#citenote6) | 150 + 150 GByte/s | 96 | 300 GByte/s |
    > | [IBM Power9](https://www.wikiwand.com/en/POWER9#I.2FO "POWER9")[\[7\]](https://www.wikiwand.com/en/NVLink#citenote7) | NVLink 2.0  (BlueLink ports) | 25 GT/s |  8 +  8 **Ⓐ** | 200 Gbit/s = 25 GByte/s | 6 | 150 + 150 GByte/s | 96 | 300 GByte/s |
    > 
    > 

- [GTC2018：Nvidia全面升級AI軟硬體 - EE Times Taiwan 電子工程專輯網](https://www.eettaiwan.com/news/article/20180328NT01-Nvidia-Taps-Memory-Switch-for-AI?utm_source=EETT%20Article%20Alert&utm_medium=Email&utm_campaign=2018-03-29)

    > 為了超越Nvidia，英特爾計劃在明年量產支援12組100Gbit/s鏈路的Nervana晶片，而Nvidia Volta則支援6個25Gbit/s NVLinks。Nervana晶片支援非同相記憶體，可在打造加速器叢集(包括環狀網路)時提供更大的靈活性，但在編程時將會更加困難。
    > 
    > 為了簡化編碼作業，英特爾宣佈開放其Ngraph編譯器，目的在於來自第三方AI架構(如Google TensorFlow)的軟體轉變為可在英特爾Xeon、Nervana及其FPGA晶片上執行的程式碼。


### VRAM

- [memory - How do I calculate video RAM requirements? - Super User](https://superuser.com/questions/256932/how-do-i-calculate-video-ram-requirements)

    > A graphics card actually requires relatively little memory to function as a simple framebuffer (2D graphics) device:
    > 
    > For example - the framebuffer requirements for 1920x1080 in 32 bit colour would be:
    > 
    > -   1920 x 1080 = 2073600 pixels
    > -   2073600 x 32 = 66355200 bits
    > -   66355200 / 8 = 8294400 bytes
    > -   8294400 / 1024 = 8100 kilobytes
    > -   8100 / 1024 = 7.91015625 megabytes
    > 
    > So even at that high resolution an 8MB card would be able to display an image.
    > 
    > You can double, or even triple that amount if you are using double or triple buffering (display one image while rendering another then switch to that new image while you render a third, etc).
    > 
    > All the rest of the memory is used when the card is working with 3D graphics to store internal copies (and transformed copies) of textures for rendering. The more memory you have the more and higher resolution textures the card can hold internally, so it won't need to be repeatedly sent the same textures over and over again by the gaming engine.
    > 
    > So basically the more memory you have the better it will be for 3D gaming.
    > 

- [How much VRAM do you really need at 1080p, 1440p and 4K?](https://www.tweaktown.com/tweakipedia/89/much-vram-need-1080p-1440p-4k/index.html)

    > Results
    > ---------
    > 
    > **1080p**: At 1920x1080, we're seeing an average of around 1.5GB to 2GB of VRAM being used, with GTA V blowing all the way out to 3.7GB, and Shadow of Mordor getting there with 3.3GB. Still, 1080p is quite tame on the framebuffer.
    > 
    > **1440p**: Moving up to 2560x1440, we see GTA V consume 3.9GB of VRAM while Shadow of Mordor uses 3.5GB. Thief begins to crawl up there with 2.9GB of VRAM, while Battlefield 4 on the Ultra preset (minus AA) is only consuming 2.2GB of VRAM and is one of the best looking games out right now.
    > 
    > **4K**: As for what games or tests use the most VRAM, we see that it's a tie between Thief and GTA V, both using 4.3GB of VRAM, while Shadow of Mordor isn't far behind with 3.9GB being used - all at 4K. Battlefield 4 only uses 3GB of VRAM, which is quite surprising.
    > 
    > Final Thoughts
    > --------------
    > 
    > Surprised? Probably. 4GB of VRAM is more than enough for most video cards today, even at 4K. We haven't taken into account any anti-aliasing, as we're going to follow through with another article that looks at 1080p, 1440p and 4K with 4xAA enabled to see how much AA strains the framebuffer in these titles. But in all my years of using PCs, I barely use AA. AA is a personal preference. I'd rather have high framerates on my 120-144Hz screens, but anti-aliasing really helps at 1080p and below.
    > 


- [How much VRAM do you need at 1080p, 1440p and 4K with AA enabled?](https://www.tweaktown.com/tweakipedia/90/much-vram-need-1080p-1440p-4k-aa-enabled/index.html)

    > Results
    > ---------
    > 
    > **1080p**: Far Cry 4 actually doesn't perform too badly at all at 1080p, but with AA enabled you're going to need 3GB+. When it comes to The Witcher 3, HBAO+ doesn't do too much at all to VRAM consumption. Battlefield 4 consumes another 20% VRAM or so at 1080p with AA enabled while Metro: Last Light uses another 30% or so - up to 1.3GB of VRAM.
    > 
    > Shadow of Mordor really loves its VRAM, with 4.7GB of VRAM being used at just 1080p with AA enabled, up from the 3.3GB used without AA. GTA V doesn't use much more VRAM with AA enabled at 1080p, while Tomb Raider uses another 180MB of VRAM for a total of 1.5GB at 1080p.
    > 
    > **1440p**: 2560x1440 is where the VRAM begins to get stressed out, starting with Heaven using 1.6GB compared to 819MB - a 100% increase in VRAM consumption. But Far Cry 4 is where the fun starts, with 3.7GB used, up from 2.8GB without AA. The Witcher 3 again doesn't consume much more at all, you don't notice any difference between 2168MB and 2197MB being used.
    > 
    > Battlefield 4 jumps up from 1.9GB to nearly 2.3GB at 1440p with AA applied, while Metro: Last Light uses another 200MB+ of VRAM at 1440p with AA enabled. Shadow of Mordor uses just under 5GB of VRAM at 1440p with AO enabled. Grand Theft Auto V uses much more VRAM at 1440p with AA enabled, jumping up from 3.9GB to nearly 4.6GB of VRAM.
    > 
    > **4K**: This is why you're here once again, to see 4K results with AA enabled. Starting with Heaven, which leaps from 1.3GB to a huge 3GB of VRAM consumption with AA enabled. Far Cry 4 uses a huge 5.7GB at 4K with AA enabled, a large jump from the 3.7GB without AA enabled.
    > 
    > Ambient Occlusion enabled in The Witcher 3 sees the game using another 200MB of VRAM, while Battlefield 4 uses nearly 3GB of VRAM with AA enabled versus 2.3GB without AA. Metro: Last Light consumes just over 2GB of VRAM with AA enabled, versus the 1.6GB used without AA.
    > 
    > Shadow of Mordor really enjoys the VRAM at 4K with AO enabled, jumping from 3.9GB to 5.4GB while GTA V absolutely leaps up from its 4.3GB to a huge 6.4GB of VRAM consumption with AA enabled at 4K.
    > 
    > **8K**: Bonus round! I ran Shadow of Mordor at 4K with 200% super sampling, which renders the game at 7680x4320, or 8K. At 8K, Shadow of Mordor consumes a mammoth, VRAM-busting 8.4GB of VRAM.
    > 
    > Battlefield 4 on the other hand, I could run with AA enabled, and disabled. At 7680x4320 without AA, Battlefield 4 was using 5.2GB of VRAM, while 4xAA enabled saw this skyrocket to a huge 7.5GB of VRAM.
    > 
    > Final Thoughts
    > --------------
    > 
    > Our first article really gave us a great look at just how much VRAM you need in games, where we honestly weren't surprised that you don't really need 4GB of VRAM or more. With AA applied - and some people really do love using AA - those numbers really start to climb above 6GB in some games, like Shadow of Mordor, or GTA V.
    > 
    > We aren't even maxing out the anti-aliasing settings, as you can force NVIDIA or AMD settings to much higher settings, but that is overkill, isn't it? For some it won't be, so if that's something you want to see us do, please do let us know. For now, we've shown you just how much the maxed out in-game settings can do with AA (or AO in SoM) can cause games to consume much more VRAM.
    > 
    > One of the more interesting tests was quickly running Middle-earth: Shadow of Mordor at 8K, which consumes a gigantic 8.4GB of VRAM. 8K is the future of gaming, and while it is many years away, if today's games are using 8GB of VRAM, what will the games of tomorrow consume?
    > 
    > You might think that VRAM consumption isn't something to worry about, or "I don't need more than 4-6GB" - and while that applies to most of the games today - it will definitely change in the future. 8K will use 8GB+ of VRAM in the future, but by next year I think we'll begin to see video cards with 24GB of VRAM (Titan 2, I'm looking at you).

- [Hardware choices: VRAM and PCIe bandwidth：deeplearning](https://www.reddit.com/r/deeplearning/comments/5fohlp/hardware_choices_vram_and_pcie_bandwidth/)

    > Generally 8gb will be enough for vision tasks because reducing the batch size on a CNN reduces the memory requirements ~linearly. That means you can use a small batch size and train large networks and get good results (though you might have to reduce your learning rate for small batch sizes). I believe the memory requirements for RNN's aren't affected much by the batch size (parameters take the most ram here) so the more VRAM the better.
    > 
    > Tim's blog post claims that CPU power doesn't really matter, but in my experience that's not really true at all. You're going to do a lot of data processing, maybe even online while training. Depending on how complex this processing is, it might make the CPU the bottleneck.
    > 
    > The other option is to add a third GPU to run your monitors. This will cause you to have an 8x, 4x, 4x pcie lane split, and I think that could hurt you.

- [caffe-yolo/multigpu.md at master · yeahkun/caffe-yolo](https://github.com/yeahkun/caffe-yolo/blob/master/docs/multigpu.md)

    > Performance is **heavily** dependent on the PCIe topology of the system, the configuration of the neural network you are training, and the speed of each of the layers. 
    > 
    > In general, scaling on 2 GPUs tends to be ~1.8X on average for networks like AlexNet, CaffeNet, VGG, GoogleNet. 4 GPUs begins to have falloff in scaling.


### GPU to SSD DMA

- [NVIDIA GPUDirect | NVIDIA Developer](https://developer.nvidia.com/gpudirect)

    > ![](https://developer.nvidia.com/sites/default/files/akamai/cuda/images/GPUDirect_v2.0_p2p_coms.png)
    > 
    > Using GPUDirect, multiple GPUs, third party network adapters, solid-state drives (SSDs) and other devices can directly read and write CUDA host and device memory, eliminating unnecessary memory copies, dramatically lowering CPU overhead, and reducing latency, resulting in significant performance improvements in data transfer times for applications running on NVIDIA Tesla™ and Quadro™ products

- [GPUDirect RDMA :: CUDA Toolkit Documentation](http://docs.nvidia.com/cuda/gpudirect-rdma/index.html)

    > ![](http://docs.nvidia.com/cuda/gpudirect-rdma/graphics/gpudirect-rdma-within-linux-device-driver-model.png)


- [PostgreSQL 上，直接將 SSD 的內容送到 GPU 上，加速讀取速度 – Gea-Suan Lin's BLOG](https://blog.gslin.org/archives/2016/09/23/6863/postgresql-%E4%B8%8A%EF%BC%8C%E7%9B%B4%E6%8E%A5%E5%B0%87-ssd-%E7%9A%84%E5%85%A7%E5%AE%B9%E9%80%81%E5%88%B0-gpu-%E4%B8%8A%EF%BC%8C%E5%8A%A0%E9%80%9F%E8%AE%80%E5%8F%96%E9%80%9F%E5%BA%A6/)
    -  [GpuScan and SSD-To-GPU Direct DMA | Hacker News](https://news.ycombinator.com/item?id=12524405)
    - [(EN) GpuScan + SSD-to-GPU Direct DMA - KaiGaiの俺メモ](http://kaigai.hatenablog.com/entry/2016/09/08/003556)
    - [heterodb/pg-strom: PG-Strom - Master development repository](https://github.com/heterodb/pg-strom)

- [kaigai/nvme-kmod: A kernel module to support SSD-to-GPU direct DMA](https://github.com/kaigai/nvme-kmod)

- [enfiskutensykkel/ssd-gpu-dma: Build userspace NVMe drivers and storage applications with CUDA support](https://github.com/enfiskutensykkel/ssd-gpu-dma)
    This library is a userspace API implemented in C for writing custom NVM Express ([NVMe](http://nvmexpress.org/wp-content/uploads/NVM-Express-1_3a-20171024_ratified.pdf)) drivers and high-performance storage applications. The API provides simple semantics and functions which a userspace program can use to control or manage one or more NVMe disk controllers.



- [cuda - Is it possible to access hard disk directly from gpu? - Stack Overflow](https://stackoverflow.com/questions/27282273/is-it-possible-to-access-hard-disk-directly-from-gpu)

    > It's not possible without host intervention. The host owns the disk drive. GPUDirect is for transferring data between PCIE devices, fundamentally. If you had your own PCIE HDD controller, on the same PCIE fabric as the GPU, and access to the device driver source code, you could conceivably write a GPUDirect RDMA driver that would allow for direct transfer from GPU to disk. (It will still require host intervention to set up.) In practice, nobody assumes that this is the level of effort that you want to take on. – [name=Robert Crovella]

    >@Siddharth You may want to take a look at [this GTC 2014 presentation](http://on-demand.gputechconf.com/gtc/2014/presentations/S4265-rdma-gpu-direct-for-fusion-io-iodrive.pdf) that discusses GPUdirect RDMA access to SSD-like storage. – [name=njuffa]

    > For anyone else looking for this, 'lazy unpinning' did more or less what I want.
    > 
    > Go through the following to see if this can be helpful for you.
    > 
    > > The most straightforward implementation using RDMA for GPUDirect would pin memory before each transfer and unpin it right after the transfer is complete. Unfortunately, this would perform poorly in general, as pinning and unpinning memory are expensive operations. The rest of the steps required to perform an RDMA transfer, however, can be performed quickly without entering the kernel (the DMA list can be cached and replayed using MMIO registers/command lists).
    > > 
    > > Hence, lazily unpinning memory is key to a high performance RDMA implementation. What it implies, is keeping the memory pinned even after the transfer has finished. This takes advantage of the fact that it is likely that the same memory region will be used for future DMA transfers thus lazy unpinning saves pin/unpin operations.
    > > 
    > > An example implementation of lazy unpinning would keep a set of pinned memory regions and only unpin some of them (for example the least recently used one) if the total size of the regions reached some threshold, or if pinning a new region failed because of BAR space exhaustion (see PCI BAR sizes).
    > 
    > Here is a link to an [application guide](http://developer.download.nvidia.com/compute/cuda/5_0/rc/docs/GPUDirect_RDMA.pdf) and to [nvidia docs](http://docs.nvidia.com/cuda/gpudirect-rdma/#lazy-unpinning-optimization).[name=L Lawliet]

    > Trying to use this feature, I wrote a small example on Windows x64 to implement this. In this example, kernel "directly" accesses disk space. Actually, as @RobertCrovella mentioned previously, the operating system is doing the job, with probably some CPU work; but no supplemental coding.
    > 
    > ```c
    > __global__ void kernel(int4* ptr)
    > {
    >     int4 val ; val.x = threadIdx.x ; val.y = blockDim.x ; val.z = blockIdx.x ; val.w = gridDim.x ;
    >     ptr[threadIdx.x + blockDim.x * blockIdx.x] = val ;
    >     ptr[160*1024*1024 + threadIdx.x + blockDim.x * blockIdx.x] = val ;
    > }
    > 
    > #include "Windows.h"
    > 
    > int main()
    > {
    >     // 4GB - larger than installed GPU memory
    >     size_t size = 256 * 1024 * 1024 * sizeof(int4) ;
    > 
    >     HANDLE hFile = ::CreateFile ("GPU.dump", (GENERIC_READ | GENERIC_WRITE), 0, 0, CREATE_ALWAYS, FILE_ATTRIBUTE_NORMAL, NULL) ;
    > 
    >     HANDLE hFileMapping = ::CreateFileMapping (hFile, 0, PAGE_READWRITE, (size >> 32), (int)size, 0) ;
    > 
    >     void* ptr = ::MapViewOfFile (hFileMapping, FILE_MAP_ALL_ACCESS, 0, 0, size) ;
    > 
    >     ::cudaSetDeviceFlags (cudaDeviceMapHost) ;
    > 
    >     cudaError_t er = ::cudaHostRegister (ptr, size, cudaHostRegisterMapped) ;
    >     if (cudaSuccess != er)
    >     {
    >         printf ("could not register\n") ;
    >         return 1 ;
    >     }
    > 
    >     void* d_ptr ;
    >     er = ::cudaHostGetDevicePointer (&d_ptr, ptr, 0) ;
    >     if (cudaSuccess != er)
    >     {
    >         printf ("could not get device pointer\n") ;
    >         return 1 ;
    >     }
    > 
    >     kernel<<<256,256>>> ((int4*)d_ptr) ;
    > 
    >     if (cudaSuccess != ::cudaDeviceSynchronize())
    >     {
    >         printf ("error in kernel\n") ;
    >         return 1 ;
    >     }
    > 
    >     if (cudaSuccess != ::cudaHostUnregister (ptr))
    >     {
    >         printf ("could not unregister\n") ;
    >         return 1 ;
    >     }
    > 
    >     ::UnmapViewOfFile (ptr) ;
    > 
    >     ::CloseHandle (hFileMapping) ;
    >     ::CloseHandle (hFile) ; 
    > 
    >     ::cudaDeviceReset() ;
    > 
    >     printf ("DONE\n");
    > 
    >     return 0 ;
    > }
    > ```
    > [name=Florent DUGUET]


### GPU on Embedded system

- [csarron/emdl: Embedded and mobile deep learning research resources](https://github.com/csarron/emdl)

- [Deep Learning on ARM Platforms - SFO17-509](https://www.slideshare.net/linaroorg/deep-learning-on-arm-platforms-sfo17509)

- [Tegra - Wikiwand](https://www.wikiwand.com/en/Tegra)

- [極度強悍的 SoC 處理器，NVIDIA Tegra X1 內部功能與架構預覽 | TechNews 科技新報](http://technews.tw/2015/01/06/nvidia-tegra-x1-soc-architecture-preview/)

### 開發版

- [Nvidia Jetson - Wikiwand](https://www.wikiwand.com/en/Nvidia_Jetson)

- [Everything You Need To Know About The NVIDIA Jetson TX1 Performance - Phoronix](https://www.phoronix.com/scan.php?page=article&item=nvidia-jtx1-perf&num=1)

### GPGPU

- [一窩瘋「人工智慧晶片」前，你需要知道的幾件關於 GPGPU 的事 | TechNews 科技新報](https://technews.tw/2017/09/12/what-you-need-to-know-about-gpgpu/)

### FPGA

- [IT Robotics Lab: SoC FPGA 嵌入式系統晶片?](http://blog.ittraining.com.tw/2017/09/soc-fpga.html)

    > __Why SoC FPGA?__
    > 
    > 目前嵌入式系統晶片開發人員必須面對激烈的市場挑戰，被要求更高的單位功耗性能/運算效能、更低的時延以及更短的開發週期來滿足各種的市場需求，因此基於FPGA的SoC已成為最流行且可行的解決方案。簡單來說,就是在FPGA可程式邏輯晶片嵌入了一個「硬核」處理器系統-- SoC (包含了ARM處理器、記憶體控制器、I/O週邊)，在Intel (Altera)把這個SoC稱作是HPS (Hard Processor System) 。  
    > 
    > 在SoC FPGA 架構下可以彈性的設計，單純使用ARM SoC、僅單獨使用FPGA或兩者一起使用。當兩者一起用時, FPGA可以作為ARM週邊的角色，針對大量且須經複雜運算的資料,如數據資料、影像訊號、聲音訊號等，可利用FPGA 硬體並行運算能力設計演算法追求最佳效能。因此，利用SoC FPGA 架構所設計的嵌入式平台，不僅可以突顯了產品優勢，在價格和性能上都可以達到最優，更重要的是產品能夠及時上市。  
    > 
    > HPS是屬於hard core 方式, 也可以選擇使用 soft core 的方式. 就是用Intel 自己的CPU--NiosII, 但用Soft core的方式, 就會消秏到原本FPGA的邏輯匣。
    > 
    > HPS 和 FPGA 有自己的Bus系統, HPS 的ARM 是 AXI Bus , FPGA 是 Avalon Bus, , 故需要設計一個Bridge 讓兩邊系統能夠溝通。 
    > 
    > 
    > [![](https://2.bp.blogspot.com/-fymgzrA3_cw/Wb0soE0nadI/AAAAAAAAFt4/oWsMGb96pskUICJnLjazLA4Nqi_Zpv3ggCLcBGAs/s640/DE0-Nano1.png)](https://2.bp.blogspot.com/-fymgzrA3_cw/Wb0soE0nadI/AAAAAAAAFt4/oWsMGb96pskUICJnLjazLA4Nqi_Zpv3ggCLcBGAs/s1600/DE0-Nano1.png)
    > 


### Google TPU

- [Google’s AI Processor’s (TPU) Heart Throbbing Inspiration](https://medium.com/intuitionmachine/googles-ai-processor-is-inspired-by-the-heart-d0f01b72defe)

    > ![](https://cdn-images-1.medium.com/max/1200/1*mvGhZQdd91h21ZCG7DMqVg.png)

    > 256 x 256 8bit multiply-add computational units. That’s a grand total of 65,536 processors capable of cranking out 92 trillion operations per second!

    > ![](https://cdn-images-1.medium.com/max/1200/1*249Jc-YR3s_QqUtSsDTjQw.png)


- [An in-depth look at Google’s first Tensor Processing Unit (TPU) | Google Cloud Big Data and Machine Learning Blog  |  Google Cloud](https://cloud.google.com/blog/big-data/2017/05/an-in-depth-look-at-googles-first-tensor-processing-unit-tpu)

    > TPU delivered 15–30X higher performance and 30–80X higher performance-per-watt than contemporary CPUs and GPUs.


    > The TPU ASIC is built on a 28nm process, runs at 700MHz and consumes 40W when running. Because we needed to deploy the TPU to Google's existing servers as fast as possible, we chose to package the processor as an external accelerator card that fits into an SATA hard disk slot for drop-in installation. The TPU is connected to its host via a PCIe Gen3 x16 bus that provides 12.5GB/s of effective bandwidth.




- [【Hot Chips 29】淺談 Google 的 TPU | TechNews 科技新報](https://technews.tw/2018/01/02/about-google-tpu/)

- [詳解Google第二代TPU，既能推理又能訓練，性能霸道 | Google I/O 2017 - 每日頭條](https://kknews.cc/tech/p55no6j.html)

    > 首先開發出新的晶片並不能保證Google成功，要使用TPU 2.0，開發者要學習一種構建和運行神經網絡的新方法。它不僅僅是一個新的晶片，TPU 2.0也是專門為TensorFlow設計。雖然Tensorflow是開源軟體，但也有許多研究人員使用Torch和Caffe等類似的軟體。新硬體需要新的軟體優化，這需要不少時間。
    > 
    > 在Google推出TPU 2.0的幾周之前，Facebook的AI研究主管Yann LeCun質疑稱，市場可能不需要新的AI專用晶片，因為研究者已經對使用GPU所需的工具非常熟悉了。新的硬體意味著新的生態系統。
    > 
    > 另外，Google雲服務的成功不僅取決於晶片的速度，以及使用的容易程度，還要考慮成本。所以，如果Google以比現有GPU服務更低的成本提供TPU服務，會得到更廣泛的用戶基礎。
    > 
    > Google自己當然會使用新TPU系統，但也會將它的能力開放給其它公司使用。Google表示，不會將晶片直接出售，而是會通過其新的雲服務（年底前公布）提供，任何開發者都可以使用新處理器帶來的計算能力。
    > 
    > Google也重申了其對開源模式的承諾，表示會向同意發布研究結果的研究人員提供TPU資源，甚至可能開原始碼。他甚至呼籲開發者加入TensorFlow Research Cloud計劃，它會免費提供一組1000台TPU。
    > 
    > 新TPU的速度優勢肯定會吸引到不少研究人員，畢竟AI研究要在大量硬體上廣泛試錯。就此而言，Google願意免費提供計算資源對全世界的AI研究者來說都是有好處的，當然，這對Google來說也是有好處的。

- [dean-nips17.pdf](http://learningsys.org/nips17/assets/slides/dean-nips17.pdf)




###### tags: `systolic`
- [download;jsessionid=EA259B539AA3B7DCB8D2C11D1397C767 - 1982-kung-why-systolic-architecture.pdf](http://www.eecs.harvard.edu/~htk/publication/1982-kung-why-systolic-architecture.pdf)

- [Should We All Embrace Systolic Arrays? | LinkedIn](https://www.linkedin.com/pulse/should-we-all-embrace-systolic-arrays-chien-ping-lu/?trk=mp-reader-card)

- [Instruction systolic array (ISA) - Matrix multiplication](http://www.iti.fh-flensburg.de/lang/papers/isa/isa2.htm)

    ![](https://media.giphy.com/media/8vZUh9LrkN4llUUxaN/giphy.gif)

    <iframe width="560" height="315" src="https://www.youtube.com/embed/sJltBQ4MOHA" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>


### compiler
- [nGraph: A New Open Source Compiler for Deep Learning Systems - Intel AI](https://ai.intel.com/ngraph-a-new-open-source-compiler-for-deep-learning-systems/?)

    > We are pleased to announce the open sourcing of nGraph, a framework-neutral Deep Neural Network (DNN) model compiler that can target a variety of devices. With nGraph, data scientists can focus on data science rather than worrying about how to adapt their DNN models to train and run efficiently on different devices. Continue reading below for highlights of our engineering challenges and design decisions, and see [GitHub](https://github.com/NervanaSystems/ngraph), our [documentation](http://ngraph.nervanasys.com/index.html/), and our [SysML paper](https://arxiv.org/abs/1801.08058) for additional details.
    > 
    > ![](http://simplecore.intel.com/nervana/wp-content/uploads/sites/53/2018/03/Picture1-2-300x168.png)
    > 
    > _Figure 1 –_ nGraph ecosystem_._
    > 
    > We currently support TensorFlow*, MXNet*, and neon directly through nGraph. CNTK*, PyTorch*, and Caffe2* are supported indirectly through ONNX. Users can run these frameworks on several devices: Intel Architecture, GPU, and Intel Nervana Neural Network Processor (NNP). Support for future devices/frameworks in our roadmap is faded.


## Environment Setup

### Linux or Windows?

### Nvidia Driver install

### Jupyter Notebook/Lab setup

#### for Linux

##### system information

- cpu info
    - [8 commands to check cpu information on Linux – BinaryTides](https://www.binarytides.com/linux-cpu-information/)
    - top
    - cat /proc/cpuinfo
    - lscpu

- memory info
    - [5 commands to check memory usage on Linux – BinaryTides](https://www.binarytides.com/linux-command-check-memory-usage/)
    - cat /proc/meminfo
    - free -g (in GB)
    - free -m (in MB)
    - 

- gpu info
    - watch nvidia-smi



#### for Windows

- [How to Install Tensorflow-GPU version with Jupyter (Windows 10) in 8 easy steps.](https://medium.com/@viveksingh.heritage/how-to-install-tensorflow-gpu-version-with-jupyter-windows-10-in-8-easy-steps-8797547028a4)


##### Library
- [Unofficial Windows Binaries for Python Extension Packages](https://www.lfd.uci.edu/~gohlke/pythonlibs/)

- [aleju/imgaug: Image augmentation for machine learning experiments.](https://github.com/aleju/imgaug)


##### Troubleshooting

- [python - DLL load failed error when importing cv2 - Stack Overflow](https://stackoverflow.com/questions/43184887/dll-load-failed-error-when-importing-cv2)

    > You can download the latest OpenCV 3.2.0 for Python 3.6 on Windows 32-bit or 64-bit machine, look for file starts with`opencv_python‑3.2.0‑cp36‑cp36m`, from this [unofficial site](http://www.lfd.uci.edu/~gohlke/pythonlibs/#opencv). Then type below command to install it:
    > 
    > -   `pip install opencv_python‑3.2.0‑cp36‑cp36m‑win32.whl` (32-bit version)
    > -   `pip install opencv_python‑3.2.0‑cp36‑cp36m‑win_amd64.whl` (64-bit version)
    > 
    > I think it would be easier.

- [python - Tensorflow GPU application crashes Jupyter notebook kernel - Stack Overflow](https://stackoverflow.com/questions/44851188/tensorflow-gpu-application-crashes-jupyter-notebook-kernel)

    > One suggestion is to place the following snippet before you import tensorflow:
    > 
    > ```
    > import os
    > os.environ["CUDA_VISIBLE_DEVICES"]="-1"
    > ```
    > 
    > **Added after @ Nicolas comment**
    > 
    > Yes this disables GPU! Which is not what is wanted.

- [python - Error with pip install scikit-image - Stack Overflow](https://stackoverflow.com/questions/38608698/error-with-pip-install-scikit-image)

    > install numpy first
    > 
    > ```
    > pip install numpy
    > ```
    > 
    > If you face installation issues for numpy, get the pre-built windows installers from [http://www.lfd.uci.edu/~gohlke/pythonlibs/](http://www.lfd.uci.edu/~gohlke/pythonlibs/) for your python version (python version is different from windows version).
    > 
    > numpy 32-bit: numpy-1.11.1+mkl-cp27-cp27m-win32.whl
    > 
    > numpy 64-bit: numpy-1.11.1+mkl-cp27-cp27m-win_amd64.whl
    > 
    > Later you require VC++ 9.0, then please get it from below link Microsoft Visual C++ 9.0 is required. Get it from [http://aka.ms/vcpython27](http://aka.ms/vcpython27)
    > 
    > Then install
    > 
    > ```
    > pip install scikit-image
    > ```
    > 
    > It will install below list before installing scikit-image
    > 
    > pyparsing, six, python-dateutil, pytz, cycler, matplotlib, scipy, decorator, networkx, pillow, toolz, dask
    > 
    > If it fails at installation of scipy, follow below steps: get the pre-built windows installers from [http://www.lfd.uci.edu/~gohlke/pythonlibs/](http://www.lfd.uci.edu/~gohlke/pythonlibs/) for your python version (python version is different from windows version).
    > 
    > Scipy 32-bit: scipy-0.18.0-cp27-cp27m-win32.whl
    > 
    > Scipy 64-bit: scipy-0.18.0-cp27-cp27m-win_amd64.whl
    > 
    > If it fails saying **whl is not supported wheel on this platform** , then upgrade pip using **python -m pip install --upgrade pip** and try installing scipy
    > 
    > Now try
    > 
    > ```
    > pip install scikit-image
    > ```
    > 
    > It should work like a charm.



### Docker for Deep Learning

- [floydhub/dl-docker: An all-in-one Docker image for deep learning. Contains all the popular DL frameworks (TensorFlow, Theano, Torch, Caffe, etc.)](https://github.com/floydhub/dl-docker)
- [ufoym/deepo: A series of Docker images (and their generator) that allows you to quickly set up your deep learning research environment.](https://github.com/ufoym/deepo)

### How about TPU?

- [谷歌这个大杀器要让英伟达慌了，实战评测：TPU相比GPU简直又快又省](https://zhuanlan.zhihu.com/p/33972503)
- [脈動陣列- 因Google TPU獲得新生 - 幫趣](http://bangqu.com/1SD42k.html)

### How about mobile/Embedded system

- [嵌入式系統開發人員套件與模組 | NVIDIA Jetson|NVIDIA](http://www.nvidia.com.tw/object/embedded-systems-dev-kits-modules-tw.html)
- [開發你的酷炫裝備 Jetson TX1使用指南 - 壹讀](https://read01.com/RR86nM.html)
- [Nvidia Brings Computer Vision and Deep Learning to the Embedded World | Hackaday](https://hackaday.com/2015/11/10/nvidia-brings-computer-vision-and-deep-learning-to-the-embedded-world/)
- [Arm會是AI進入尋常百姓家的關鍵推手？ - EE Times Taiwan 電子工程專輯網](https://www.eettaiwan.com/news/article/20180222NT03-Arm-Extends-AI-to-the-Masses?utm_source=EETT%20Article%20Alert&utm_medium=Email&utm_campaign=2018-02-23)
- [高通首次推出AI引擎，打包所有軟硬件算力 - 幫趣](http://bangqu.com/zu312j.html)
- [發掘 ARM GPU 的全部深度學習性能，TVM 優化帶來高達2倍性能提升 - 幫趣](http://bangqu.com/o9r51a.html)
- [Machine learning on mobile: on the device or in the cloud?](http://machinethink.net/blog/machine-learning-device-or-cloud/)



## 雲端服務

- [Compute Pricing Comparison: AWS vs Azure vs Google Cloud](https://www.simform.com/compute-pricing-comparison-aws-azure-googlecloud/)

- [AWS vs Paperspace vs FloydHub : Choosing your cloud GPU partner](https://medium.com/@rupak.thakur/aws-vs-paperspace-vs-floydhub-choosing-your-cloud-gpu-partner-350150606b39)
- [FloydHub - Deep Learning Platform - Cloud GPU](https://www.floydhub.com/)
- [Is it a good idea to use FloydHub or other cloud services to train deep models? - Quora](https://www.quora.com/Is-it-a-good-idea-to-use-FloydHub-or-other-cloud-services-to-train-deep-models)

- [How much does a GPU instance cost?：MLQuestions](https://www.reddit.com/r/MLQuestions/comments/5s0jnc/how_much_does_a_gpu_instance_cost/)


- [GPU訓練機器學習模型哪家強？AWS、谷歌雲、IBM等6大平台對比 - iFuun](http://www.ifuun.com/a201802109938558/)
    - [Machine learning mega-benchmark: GPU providers (part 2) | RaRe Technologies](https://rare-technologies.com/machine-learning-benchmarks-hardware-providers-gpu-part-2/)

    > ![Imgur](https://i.imgur.com/KVFNlFq.png)


    > -   Paperspace appears to be one step ahead with regards to performance and costs. This is especially true for occasional/infrequent users who just wish to experiment with deep learning techniques (similar conclusion in [another benchmark](https://medium.com/initialized-capital/benchmarking-tensorflow-performance-and-cost-across-different-gpu-options-69bd85fe5d58)).
    > -   Dedicated servers (like the ones provided by LeaderGPU) and bare metal servers (such as Hetzner) are suitable for users considering heavy-duty long term employment of these resources (doh). Note though that since they are less flexible in the matter of customizing the servers, make sure that your task is highly CPU/GPU intensive to truly benefit from the pricing.
    > -   Newer players like Paperspace and LeaderGPU shouldn’t be dismissed, as they can aid in cutting a major chunk of the costs. Enterprises can be averse to switching providers because of the associated inertia and switching costs, but these smaller platforms are definitely worth considering.
    > -   AWS and GCE can be terrific options for someone looking for integration with their other services (AI integrations – Amazon’s Rekognition, Google’s Cloud AI).
    > -   Unless you plan to run a task that will take days to complete, sticking to a lower end single-GPU instance is the best bargain (see also [here](http://minimaxir.com/2017/11/benchmark-gpus/)).
    > -   Higher-end GPUs are significantly faster but actually have worse ROI. You should opt for these only when a short training time (lower R&D cycle latency) is more important than the hardware costs.
    > 




### Preempted vs On-demand


### Amazon AWS

- [open-guides/og-aws: 📙 Amazon Web Services — a practical guide](https://github.com/open-guides/og-aws#why-an-open-guide)

- [Learning Machine Learning on the cheap: Persistent AWS Spot Instances](https://blog.slavv.com/learning-machine-learning-on-the-cheap-persistent-aws-spot-instances-668e7294b6d8)



### Microsoft Azure

### Google Colaboratory

- [Google Colab Free GPU Tutorial – Deep Learning Turkey – Medium](https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d)

    ### Setting Free GPU

    It is so simple to alter default hardware **(CPU to GPU or vice versa)**; just follow **Edit > Notebook settings** or **Runtime>Change runtime type** and **select GPU** as **Hardware accelerator**.

    ![](https://cdn-images-1.medium.com/max/1000/1*WNovJnpGMOys8Rv7YIsZzA.png)


    ### Running or Importing .py Files with Google Colab

    Run these codes first in order to install the necessary libraries and perform authorization.

    ```shell=
    !apt-get install -y -qq software-properties-common python-software-properties module-init-tools  
    !add-apt-repository -y ppa:alessandro-strada/ppa 2>&1 > /dev/null  
    !apt-get update -qq 2>&1 > /dev/null  
    !apt-get -y install -qq google-drive-ocamlfuse fuse  
    from google.colab import auth  
    auth.authenticate_user()  
    from oauth2client.client import GoogleCredentials  
    creds = GoogleCredentials.get\_application\_default()  
    import getpass  
    !google-drive-ocamlfuse -headless -id={creds.client\_id} -secret={creds.client\_secret} < /dev/null 2>&1 | grep URL  
    vcode = getpass.getpass()  
    !echo {vcode} | google-drive-ocamlfuse -headless -id={creds.client\_id} -secret={creds.client\_secret}
    ```

    When you run the code above, you should see a result like this:

    ![](https://cdn-images-1.medium.com/max/1000/1*Tdf4sfvctlQbCpxekMI9LQ.png)

    **Click** the link, **copy** verification code and **paste** it to text box.

    After completion of the authorization process,

    mount your **Google Drive**:

    ```shell=
    !mkdir -p drive  
    !google-drive-ocamlfuse drive
    ```

    install **Keras:**

    `!pip install -q keras`

    upload [mnist_cnn.py](https://github.com/keras-team/keras/blob/master/examples/mnist_cnn.py) file to **app** folder which is located on your **Google Drive**.

    ![](https://cdn-images-1.medium.com/max/1000/1*9y7lbgBmG99ZVkGr5b7arQ.png)

    **mnist_cnn.py** file

    run the code below to train a simple convnet on the [MNIST dataset](http://yann.lecun.com/exdb/mnist/).

    `!python3 "drive/Colab Notebooks/mnist_cnn.py"`

    #### 2\. Is GPU Working?

    To see if you are currently using the GPU in Colab, you can run the following code in order to cross-check:

    ```python=
    import tensorflow as tf
    tf.test.gpu_device_name()
    ```

    ![](https://cdn-images-1.medium.com/max/1000/1*rHxgzJWoos7f4AYF90PkzQ.jpeg)

    #### 3\. Which GPU Am I Using?

    ```python=
    from tensorflow.python.client import device_lib  
    device_lib.list_local_devices()
    ```

    Currently, **Colab only provides Tesla K80**.

    ![](https://cdn-images-1.medium.com/max/1000/1*D-xR_CzTP3_MMt_8UqIj4Q.png)

    #### 4\. What about RAM?

    `!cat /proc/meminfo`

    ![](https://cdn-images-1.medium.com/max/1000/1*EPbmqr--SxC0crhMxoaS9Q.png)

    #### 5\. What about CPU?

    `!cat /proc/cpuinfo`

    ![](https://cdn-images-1.medium.com/max/1250/1*keRD5wndUyzoxgNUwfWfsQ.png)

    #### 6\. Changing Working Directory

    Normally when you run this code:

    `!ls`

    You probably see **datalab and drive** folders.

    Therefore you must add **drive/app** before defining each filename.

    To get rid of this problem, you can simply change the working directory. (In this tutorial I changed to **app folder**) with this simple code:

    ```python=
    import os  
    os.chdir("drive/app")
    ```

    After running code above, if you run again

    `!ls`

    You would see **app folder content** and don’t need to add **drive/app** all the time anymore.

    __11. How to Restart Google Colab?__

    In order to restart (or reset) your virtual machine, simply run:

    `!kill -9 -1`

    __12. How to Add Form to Google Colab?__

    In order not to change hyperparameters every time in your code, you can simply add form to Google Colab.

    ![](https://cdn-images-1.medium.com/max/1000/1*Cy19qeGZzgllJrtAqOH4OQ.png)

    For instance, I added form which contain learning_rate variable and optimizer string.
 
    ![](https://cdn-images-1.medium.com/max/1000/1*kGvfrNrRHwfv1jWtguufkg.png)


- [sys.path different in Jupyter and Python - how to import own modules in Jupyter? - Stack Overflow](https://stackoverflow.com/questions/34976803/sys-path-different-in-jupyter-and-python-how-to-import-own-modules-in-jupyter)

    Here is what I do on my projects in jupyter notebook,

    ```python=
    import sys
    sys.path.append("../") # go to parent dir
    from customFunctions import *
    ```

    Then, to affect changes in `customFunctions.py`,

    ```python=
    %load_ext autoreload
    %autoreload 2
    ```

- [python - How can access Uploaded File in Google colab - Stack Overflow](https://stackoverflow.com/questions/48485255/how-can-access-uploaded-file-in-google-colab)

    > Here's an adjustment to your snippet that will save any uploaded file in the current directory using the uploaded file name.
    > ```python
    > from google.colab import files
    > uploaded = files.upload()
    > 
    > for name, data in uploaded.items():
    >   with open(name, 'wb') as f:
    >     f.write(data)
    >     print ('saved file', name)
    > ```
    > 

- [External data: Drive, Sheets, and Cloud Storage - Colaboratory](https://colab.research.google.com/notebook#fileId=/v2/external/notebooks/io.ipynb&scrollTo=s6nDq8Nk7aPN)




- [python - from ... import OR import ... as for modules - Stack Overflow](https://stackoverflow.com/questions/22245711/from-import-or-import-as-for-modules)

    You can use **as** to rename modules suppose you have two apps that have views and you want to import them

    ```python=
    form app1 import views as views1
    from app2 import views as views2
    ```

    if you want multiple import use comma separation

    ```python=
    >>> from datetime import date as d, time as t
    >>> d
    <type 'datetime.date'>
    >>> t
    <type 'datetime.time'>
    ```


- [machine learning - Google Colaboratory: misleading information about its GPU (only 5% RAM available) - Stack Overflow](https://stackoverflow.com/questions/48750199/google-colaboratory-misleading-information-about-its-gpu-only-5-ram-available)

    Here is little debug function I scraped together:

    ```python=
    # memory footprint support libraries/code
    !ln -sf /opt/bin/nvidia-smi /usr/bin/nvidia-smi
    !pip install gputil
    !pip install psutil
    !pip install humanize
    import psutil
    import humanize
    import os
    import GPUtil as GPU
    GPUs = GPU.getGPUs()
    # XXX: only one GPU on Colab and isn’t guaranteed
    gpu = GPUs[0]
    def printm():
     process = psutil.Process(os.getpid())
     print("Gen RAM Free: " + humanize.naturalsize( psutil.virtual_memory().available ), " | Proc size: " + humanize.naturalsize( process.memory_info().rss))
     print("GPU RAM Free: {0:.0f}MB | Used: {1:.0f}MB | Util {2:3.0f}% | Total {3:.0f}MB".format(gpu.memoryFree, gpu.memoryUsed, gpu.memoryUtil*100, gpu.memoryTotal))
    printm()
    ```

    Executing it in the notebook without running any other code gives me:

    ```shell=
    Gen RAM Free: 11.6 GB  | Proc size: 666.0 MB
    GPU RAM Free: 566MB | Used: 10873MB | Util  95% | Total 11439MB
    ```

- [Google Colaboratory gets disconnected after 10-15 minutes.：learnmachinelearning](https://www.reddit.com/r/learnmachinelearning/comments/88ywbo/google_colaboratory_gets_disconnected_after_1015/)

    > 1. Yeah.. that environment definitely looks like the reason of your problem
    > 2. Here are some useful things I used in my last colabs: https://colab.research.google.com/drive/1P2AmVHPmDccstO0BiGu2uGAG0vTx444b
    > 
    > About how to reload your saved checkpoint, there are lot of documentation about it around, I use something similar to this:
    > 
    > ```python
    > saver = tf.train.Saver() ckpt = tf.train.latest_checkpoint('./MODEL/encoder/') if (ckpt): print (ckpt) saver.restore(sess, ckpt) start_step = int(ckpt.split('-')[1])
    > ```
    > 

- [Does Google Colab stay connected when I close my browser? - Stack Overflow](https://stackoverflow.com/questions/49062628/does-google-colab-stay-connected-when-i-close-my-browser)

    > 1. The current cell will continue executing once you close your browser, but the outputs will not end up in the notebook in Drive. (If you were to reconnect before your VM were considered idle and deleted, any values you'd computed would still be available in your kernel.)
    > 
    > 2. Distinct users are always assigned to distinct backends, so they'd have to install the libraries themselves. (This is one reason we encourage keeping library setup/config in the notebook.)

- [amazon redshift - Can I run Google colaboratory locally? - Stack Overflow](https://stackoverflow.com/questions/47316383/can-i-run-google-colaboratory-locally)

    > Colab now supports execution with local backends! You can get started by following these instructions: https://research.google.com/colaboratory/local-runtimes.html
    > 
    > By default, Colab stores all code cell outputs in Google Drive. If your local connection will access sensitive data and you would like to omit these, you can select "Omit code cell output when saving this notebook" when connecting to your local runtime.

- [python - Answer "yes" to terminal on Google Colaboratory - Stack Overflow](https://stackoverflow.com/questions/48709520/answer-yes-to-terminal-on-google-colaboratory)

    >Or script typing "yes" using something like https://pexpect.readthedocs.io/en/stable/

### How about Decentrlized Frog Computing?

- [Fog Computing Can Beat Amazon’s Cloud Computing Services On Price, Speed, And Convenience](https://blog.sonm.io/fog-computing-can-beat-amazons-cloud-computing-services-on-price-speed-and-convenience-5904d1dd14e8)
- 

## 該自己架還是使用雲端？

- [GPU servers for machine learning startups: Cloud vs On-premise?](https://medium.com/@thereibel/gpu-servers-for-machine-learning-startups-cloud-vs-on-premise-9a9dedfcadc9)

    ### Cloud vs on-premise: Performance

    When we initially benchmarked cloud-GPUs I was actually surprised to discover that **in general cloud-based GPUs are very slow.**

    If you were to buy one of these cards it would set you back about 5K\$ — so if you live by the "if it’s expensive it must be good"-rule you would figure they would be awesome for deep learning, right?

    Well.. They’re not. **A Titan X Pascal which you can get for 1K\$ will beat a Tesla K40/K80 any day!** What’s the deal with that?

    > Titan: 15 seconds pr. batchsize 64   
    > Tesla: 45 seconds pr. batchsize 32

    Based on our experience there’s no doubt. On-Premise Titan-based GPU servers are way faster than cloud Tesla-based GPU servers.

    > On-premise: 1. Cloud: 0.

    ### Cloud vs on-premise: Cost

    One of our GPU servers costs approximately 8.5K\$ which includes 4x Titan X Pascals. An Amazon P2.xlarge instance with 1x Tesla K80 costs 0.9\$/hr. To compare on a GPU-basis let’s bump that up to 3.6\$/hr to get 4x Tesla K80.

    This means that **I could get 2361 computing hours (or approximately 100days of training) on the P2 instances before I reach the price of my on-premise GPU server.**

    > After <100 days of training your on-premise GPU server will be cheaper.

    But let’s not forget that the **Tesla K80s are 6x slower than the Titan’s**. This means that I need to wait 6x longer for the K80s to finish training the same job as the Titans.

    Let’s say that we need to train a job that would take one week (168hours) to train on the on-premise server. Because the K80s have 6x lower computing efficiency this would take the K80s 1008 hours (168*6) resulting in a cost of 3.6K\$ or **almost half the price of my on-premise server.**

    > On-premise: 2. Cloud: 0

    ### Cloud vs on-premise: Operations
    
    Having your own servers at your office inherently comes with more operational issues:
    
    -   Do we have the right drivers installed?
    -   Coordinating updates
    -   Network breakdowns
    -   Wifi connectivity problems
    -   Unscheduled reboots
    -   Power outages
    -   Equipment failure
    -   Why doesn’t it respond?
    -   No more disk space
    -   Cable nightmares
    -   etc..

    If you’re using Amazon’s GPU servers you don’t need to worry about unscheduled reboots because Ubuntu decided to perform automatic updates, thereby killing all jobs on the machine.

    Still, Cloud wins this one.

    > On-premise: 2. Cloud: 1

    ### Conclusion

    If it’s your job to make sure the machine learning team stays effective you would want to keep training times as low as possible and I would say that in the 1.5 years we’ve been running on-premise GPU servers we might have had a total of 1–2 days downtime.

- [What is best cloud solution for deep learning? - Quora](https://www.quora.com/What-is-best-cloud-solution-for-deep-learning)

    > Using a cloud service is a good choice for getting started. But note that building a local deep learning rig does become cost effective if you need to train models for 1500+ hours. See [Andrej Karpathy’s setup](https://twitter.com/karpathy/status/648256662554341377) if you want to give it a try.[name=Vedant Misra]

- [The \$1700 great Deep Learning box: Assembly, setup and benchmarks](https://blog.slavv.com/the-1700-great-deep-learning-box-assembly-setup-and-benchmarks-148c5ebe6415)

    However, as time passed, the AWS bills steadily grew larger, even as I switched to [10x cheaper Spot instances](https://medium.com/slavv/learning-machine-learning-on-the-cheap-persistent-aws-spot-instances-668e7294b6d8). Also, I didn’t find myself training more than one model at a time. Instead, I’d go to lunch/workout/etc. while the model was training, and come back later with a clear head to check on it.

    But eventually the model complexity grew and took longer to train. I’d often forget what I did differently on the model that had just completed its 2-day training. Nudged by the great experiences of the other folks on the [Fast.AI Forum](http://forums.fast.ai/), I decided to settle down and to get a dedicated DL box at home.

    __The most important reason was saving time while prototyping models — if they trained faster, the feedback time would be shorter.__ Thus it would be easier for my brain to connect the dots between the assumptions I had for the model and its results.

    __Then I wanted to save money — I was using Amazon Web Services (AWS), which offered P2 instances with Nvidia K80 GPUs. Lately, the AWS bills were around \$60–70/month with a tendency to get larger. Also, it is expensive to store large datasets, like ImageNet.__

    __A sensible budget for me would be about 2 years worth of my current compute spending. At \$70/month for AWS, this put it at around \$1700 for the whole thing.__
    
    

