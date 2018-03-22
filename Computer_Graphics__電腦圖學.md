# Computer_Graphics__電腦圖學

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

