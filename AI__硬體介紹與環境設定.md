# AI__硬體介紹與環境設定





## 我的深度學習專用機

- [原價屋估價](http://www.coolpc.com.tw/evaluate.php)

- 主機：ASRock DeskMini250 GTX (__~$46400__) [time=Oct 07, 2018]
    - 空機 (主機板+網卡) (__~$13900__)
    - GPU：NVIDIA GTX1070 (MXM介面) (__~$22500__)
    - CPU：Intel Pentium G4600 (3.6Ghz) (效能近i3-7100) (__~$2150__)
    - RAM：Crucial DDR4-2400 16G (__~$4400__)
    - SSD：Plextor M8PeG 256G NVMe  (__~$3450__)
    - HDD：Seagate 2T SATA (2.5inch) (__~$3450__)
- 螢幕：LG 22MP58VQ-P 22型AH-IPS寬螢幕 (__~$2588__)

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

    > For comparison, an "entry-level" $700 Quadro 4000 is significantly slower than a $530 high-end GeForce GTX 680, at least according to my measurements using several Vrui applications, and the closest performance-equivalent to a GeForce GTX 680 I could find was a Quadro 6000 for a whopping $3660.

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
    >　A Titan Black is about $500 on eBay (used) and gives you about 1700 DP gigaflops. A Titan is about $350 and gives about 1400 DP gigaflops.  
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

### GPU to SSD DMA

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



## 雲端服務

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


