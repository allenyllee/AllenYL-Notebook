# Computer_Graphics__電腦圖學

[toc]
<!-- toc --> 

## Raytracing

- [Microsoft 發表 DirectX 12 Raytracing API 功能集 DXR，標準化光追蹤步驟 | T客邦 - 我只推薦好東西](https://www.techbang.com/posts/57408-microsoft-publishes-the-directx-raytracing-api-feature-set-dxr-standard-light-tracing-steps)

    > 若要瞭解光追蹤的成像原理，我們先來理解目前絕大部分 3D 遊戲畫面是如何繪製的。由於即時遊戲畫面需要每秒提供 30 張～60 張以上的畫面更新速率，因而需要 1 種相當有效率且易於平行運算的作業方式，Rasterization 光柵化就是目前 3D 遊戲的基礎。
    > 
    > 光柵化簡而言之就是把 3D 虛擬空間裡的所有物件，剃除視角以外的物件，也把被其它物件遮擋，物件背面部分全部刪除減少實際運算量（Z-buffer Culling），再壓縮至 1 張平面，而這平面就是你我所能看見的螢幕，接著再依據每個像素進行相關的貼圖、上色、打光作業。雖然這種方式能夠大量減少運算工作，同時產生不錯的畫面品質，卻也因為少了一些物件以及光線之間的交互作用，看起來與真實世界總有不小的差距。
    > 
    > 之後加入許多增進畫面品質的運算技巧，譬如 Bump Mapping 凹圖貼圖、Normal Mapping 法線貼圖、Parallax Mapping 視差貼圖、Global Illumination 全域照明、Ambient Occlusion 環境遮蔽等，都是為了加強畫面的品質與真實性。
    > 
    > ![](https://cdn0-techbang.pixfs.net/system/images/433803/original/29969e87bdc0ede4cb638c8cefc892e6.png?1521497551)  
    > ▲光柵化逐步剃除物件的步驟，由上而下分別為無剃除、剔除視錐以外物件、刪去視角以外部分、刪去背部看不見部分、刪去被其它物件遮蔽部分。
    > 
    > ![](https://cdn2-techbang.pixfs.net/system/images/433801/original/a59f717c9536fa56df1f77e5b266dd2d.png?1521497395)  
    > ▲三角形光柵化的效果。
    > 
    > Raytracing 光追蹤則是模擬真實世界光線運作方式，包含光在物體表面的折射、散射、繞射，或是穿過物體的透射，同時考慮到光在各個物體之間的交互作用，也就是計算場景的光場，最終以平面方式呈現在螢幕。為了減少運算量，實際上運算步驟並不從光源開始，而是由攝影機視角反向射出數條虛擬光線，追蹤這些虛擬光線的路徑。
    > 
    > ![](https://cdn2-techbang.pixfs.net/system/images/433804/original/e6f6301fb1078457ec0b633ca3280d37.png?1521497585)  
    > ▲光追蹤可以計算物件與物件之間的光線交互作用。
    > 
    > 因為內部原理與實際環境相當類似，光追蹤可以產生相當逼真的畫面效果，無需其它特殊的運算技巧。但是相對於光柵化還是需要相當大的運算資源，因此 3D 遊戲絕大部分依然選用光柵作為產生畫面的手段，光追蹤則是應用在動畫、電影特效等沒有時間限制的領域。部分遊戲貼圖材質也會先行以光追蹤技法處理，預先改變顏色後再貼上物件，產生較為逼真的結果。
    > 
    - [Announcing Microsoft DirectX Raytracing! – DirectX Developer Blog](https://blogs.msdn.microsoft.com/directx/2018/03/19/announcing-microsoft-directx-raytracing/)

- [What's the Difference Between Ray Tracing, Rasterization? | NVIDIA Blog](https://blogs.nvidia.com/blog/2018/03/19/whats-difference-between-ray-tracing-rasterization/)




## GPU Rendering process

- [graphics card - Why are videos rendered by the cpu instead of the gpu? - Super User](https://superuser.com/questions/790418/why-are-videos-rendered-by-the-cpu-instead-of-the-gpu)

    > Before HD was a thing, CPUs could handle video decoding easily. When HD became popular about 8 years ago, GPU manufacturers started to implement accelerated video decoding in their chips. You could easily find graphics cards marketed as supporting HD videos and some other slogans. Today any GPU supports accelerated video, even integrated GPUs like Intel HD Graphics or their predecessors, Intel GMA. Without that addition your CPU would have a hard time trying to digest 1080p video with acceptable framerate, not to mention increased energy consumption. So you're already using accelerated video everyday.
    > 
    > Now when GPUs have more and more general use computational power, they are widely used to accelerate video processing too. This trend started around the same time when accelerated decoding was introduced. Programs like Badaboom started to gain popularity as it turned out that GPUs are much better at (re)encoding video than CPUs. It couldn't be done before, though, because GPUs lacked generic computational abilities.
    > 
    > But GPUs could already scale, rotate and transform pictures since middle ages, so why weren't we able to use these features for video processing? Well, these features were never implemented to be used in such way, so they were suboptimal for various reasons.
    > 
    > When you program a game, you first upload all graphics, effects etc. to the GPU and then you just render polygons and map appropriate objects to them. You don't have to send textures each time they are needed, you can load them and reuse them. **When it comes to video processing, you have to constantly feed frames to the GPU, process them and fetch them back to reencode them on CPU (remember, we're talking about pre-computational-GPU times)**. This wasn't how GPUs were supposed to work, so performance wasn't great.
    > 
    > Another thing is, **GPUs aren't quality-oriented when it comes to image transformations**. When you're playing a game at 40+ fps, you won't really notice slight pixel misrepresentations. Even if you would, game graphics weren't detailed enough for people to care. There are various hacks and tricks used to speed up rendering that can slightly affect quality. **Videos are played at rather high framerates too, so scaling them dynamically at playback is acceptable, but reencoding or rendering has to produce results that are pixel-perfect or at least as close as possible at reasonable cost.** You can't achieve that without proper features implemented directly in GPU.
    > 
    > Nowadays using GPUs to process videos is quite common because we have required technology in place. Why it's not the default choice is rather a question to program's publisher, not us - it's their choice. Maybe they believe that their clients have hardware oriented to process videos on CPU, so switching to GPU will negatively affect performance, but that's just my guess. Another possibility is that they still treat GPU rendering as experimental feature that's not stable enough to set it as a default yet. You don't want to waste hours rendering your video just to realize something is screwed up due to GPU rendering bug. If you decide to use it anyway, then you can't blame the software publisher - it was your decision.
    > 

- [How a GPU Works](https://www.cs.cmu.edu/afs/cs/academic/class/15462-f11/www/lec_slides/lec19.pdf)

    ![](https://screenshotscdn.firefoxusercontent.com/images/66d590a0-f112-4f68-9e6b-0a5840ef6025.png)

## 3D 建模

### GQN Neural rendering

<iframe width="560" height="315" src="https://www.youtube.com/embed/gnctSz2ofU4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

- [Neural scene representation and rendering | DeepMind](https://deepmind.com/blog/neural-scene-representation-and-rendering/)

- [自动「脑补」3D环境！DeepMind最新Science论文提出生成查询网络GQN | 机器之心](https://www.jiqizhixin.com/articles/Science-Neural-scene-representation-and-rendering)


    > 在这项发表在 Science 的研究中，DeepMind 引入了生成查询网络（Generative Query Network/GQN）的框架，其中机器通过到处走动并仅在由它们自己获取的数据中训练来感知周围环境。该行为和婴儿、动物很相似，GQN 通过尝试观察周围的世界并进行理解来学习。以此，GQN 得以学习合理的场景以及它们的几何性质，而不需要任何场景内容的人类标记。
    > 
    > GQN 模型由两部分构成：一个表征网络以及一个生成网络。表征网络将智能体的观察作为输入，并生成一个描述潜在场景的表征（向量）。然后生成网络从之前未观察过的视角来预测（想象）该场景。
    > 
    > 表征网络不知道生成网络将被要求预测哪些视角，因此必须找到尽可能准确描述场景真实布局的有效方法。表征网络能通过简明的分布式表示捕获最重要的元素，例如目标位置、颜色和房间布局。在训练过程中，生成器学习环境中的典型目标、特征、关系和规律。这组共享的「概念」使表征网络能够以高度压缩、抽象的方式来描述场景，让生成网络在必要时填写细节。例如，表征网络将把「蓝色立方体」简洁地表示为一个小的数值集合，生成网络将知道从特定的角度来看，这是如何以像素的形式表现出来的。
    > 
    > 我们在模拟 3D 世界里一组由程序生成的环境中对 GQN 进行了受控实验，这些环境包含随机位置、颜色、形状和纹理的多个目标，还有随机光源和严重遮挡。在这些环境下训练后，我们使用 GQN 的表征网络来生成新的、以前未见过的视角下的场景表征。我们在实验中表明，GQN 具有几个重要的特性：
    > 
    > -   GQN 的生成网络可以从新的视角非常精确地「想象」以前未见过视角下的场景。当给定场景表征和新视角时，它会生成清晰的图像，而不需要预先规定角度、遮挡或照明的规律。因此，生成网络是从数据中学习的近似渲染器（renderer）：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW8ymzWBzccLf3HS5gOQrALlns7f5ax0aicgiaJSVrSI6we8kgQcjPCiaWAJfBa82CoNtCfdl493WibwJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)
    > 
    > -   GQN 的表征网络可以学习计数、定位和分类目标，并且不需要任何目标级的标注。即使它的表征可能是很小的，GQN 在查询视角的预测也能达到很高的准确率，几乎和真实场景无法分辨。这意味着该表征网络可以准确地感知，例如识别积木块的精确配置：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_gif/KmXPKA19gW8ymzWBzccLf3HS5gOQrALl3gxSZnKh4STsRmTq3GicPAj8oxwXLz2WGFzdLH6nuGn9ic8clc64rNvw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)
    > 
    > -   GQN 可以表征、测量和减少不确定性。它可以计算关于场景可信度的不确定度，即使其内容不是完全可见的，并且它可以组合一个场景的多个部分视角来构建一致的整体。下图中展示了它的第一人称视角和自顶向下视角的预测。该模型通过预测的易变性来表达不确定度，并随着它在迷宫中移动而逐渐减小（灰色椎体表示观察位置，黄色椎体表示查询位置）。
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW8ymzWBzccLf3HS5gOQrALlmibDblbAZ3cmm6ydBMUQbe7e3MeDDK93lHDZiaacIKvVvJQ52XW96YKQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1)
    > 
    > -   GQN 的表征允许实现鲁棒性的、数据效率高的强化学习。当给定 GQN 的紧凑型表征时，如下所示，当前最优的深度强化学习智能体相比于 model-free 的基线智能体在学习完成任务上有更高的数据效率。对于这些智能体，通用网络中编码的信息能被视为环境的先验知识：
    > 
    > ![](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gW8ymzWBzccLf3HS5gOQrALlI5ZDO1ZvEqELkqwU2TJ1IeItRXBKXwHfDyiag37Niaql5GSIxr7Q2TMQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1)
    > 
    > *相比于使用原像素的标准方法，使用 GQN 迭代次数少了 4 倍，但收敛表现一致且有更加数据高效的策略学习。*
    > 
    > GQN 建立在最近大量多视角的几何研究、生成式建模、无监督学习和预测学习的基础上，它展示了一种学习物理场景的紧凑、直观表征的全新方式。重要的是，提出的这种方法不需要特定域的工程以及消耗时间对场景内容打标签，使得同一模型能够应用到大量不同的环境。它也学习了一种强大的神经渲染器，能够产生准确的、全新视角的场景图像。
    > 
    > DeepMind 认为，相比于更多传统的计算机视觉技术，他们的方法还有许多缺陷，目前也只在合成场景下训练工作的。然而，随着新数据资源的产生、硬件能力的发展，DeepMind 希望探索 GQN 框架应用到更高分辨率真实场景图像的研究。未来，探索 GQN 应用到更广泛的场景理解的工作也非常重要，例如通过跨空间和时间的查询来学习物理和移动等常识概念，还有应用到虚拟和增强现实等。
    > 


### Photo realistic Neural rendering

- [Gaussian Material Synthesis – new! ACM Transactions on Graphics (SIGGRAPH 2018) Károly Zsolnai-Fehér, Peter Wonka, Michael Wimmer – Károly Zsolnai-Fehér – Research Scientist](https://users.cg.tuwien.ac.at/zsolnai/gfx/gaussian-material-synthesis/)

    <iframe width="560" height="315" src="https://www.youtube.com/embed/6FzVhIV_t3s" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

    > In this paper, we teach an AI the concept of metallic, translucent materials and more. The newly synthesized materials can be visualized in real-time via neural rendering and we also propose an intuitive variant generation technique to enable the user to fine-tune these recommended materials. This project took more than 3000 work hours to complete – I hope you’ll enjoy the result!
    > 

### 共面性3D重建

- [ECCV 2018 | 國防科大&普林斯頓提出共面性檢測網絡：助力三維場景重建 - 幫趣](http://bangqu.com/611o8q.html)

    > 在此之前，傳統方法往往通過檢測不同圖片中的共同特徵點來實現圖片配準。但是由於圖片曝光不統一、相機運動太快導致圖像模糊等因素，關鍵點的檢測和特徵計算差強人意，基於特徵點的配准算法有很強的侷限性。
    > 
    > 爲了解決這一問題，人們開始嘗試利用較特徵點更大的幾何體來提高三維場景重建的精度。過去的五年裏，這方面的研究工作大多集中於利用平面的共面性對配準結果進行優化矯正。以 CVPR 2017 文章 [1] 中的方法爲例，該方法首先利用 SIFT 特徵點實現初步配準，然後通過將近似共面平面矯正成完全共面平面來優化相機位置。這種遞進式的優化方法雖然能夠在一定程度上提高三維場景重建精度，但是卻嚴重依賴於對相機位姿的初始估計。當初始位姿誤差很大的時候，該方法無法正確檢測幀間的共面平面，從而帶來巨大的重建誤差。那麼，如何才能更好地利用平面提高三維重建精度呢？
    > 
    > ![](http://i2.bangqu.com/j/news/20180810/611o8q1533877229321f2U6o.png)*圖 2 平面共面性預測*
    > 
    > 「我們注意到，人類在判斷兩個平面是否共面時並不需要估計相機的位姿。爲了解決上述問題，一個很直接的想法是讓機器具有像人類一樣對共面性進行判斷的能力。我們提出使用深度網絡預測不同幀中的兩個平面是否共面，這在三維重建領域尚屬首次。」論文的第一作者施逸飛這樣介紹這項工作。「人類在做這種判斷時，既會觀察兩個平面的紋理顏色是否一致，也會考慮平面的語義信息。例如，假設我知道兩個平面都是地面，那麼它們極有可能是共面的。」
    > 
    > ![](http://i2.bangqu.com/j/news/20180810/611o8q1533877230596C1m1D.png)*圖 3 PlaneMatch 算法流程圖*

