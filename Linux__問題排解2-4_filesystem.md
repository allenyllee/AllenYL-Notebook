# Linux__問題排解2-4_filesystem

[toc]
<!-- toc --> 


# Btrfs



## introduction

- [Btrfs 檔案系統保護你的企業資料 | 群暉科技 Synology Inc.](https://www.synology.com/zh-tw/dsm/Btrfs)

    > Btrfs 檔案系統的好處?
    > --------------
    > 
    > ### 在 Synology NAS 採用 Btrfs 儲存空間能為企業帶來許多好處。
    > 
    > ![](https://www.synology.com/img/dsm/btrfs/benefits_icon_01.png)
    > 
    > #### 中繼資料鏡像，提升資料可用性
    > 
    > 在任何儲存系統確保中繼資料的完整性極為重要，因為其中包含重要的資訊，如檔案架構、名稱、登入權限以及檔案位置。 Btrfs 檔案系統將兩份中繼資料儲存於一個儲存空間，讓檔案即便在硬碟損壞或壞軌的狀況下，亦能進行資料還原。
    > 
    > ![](https://www.synology.com/img/dsm/btrfs/benefits_icon_02.png)
    > 
    > #### Btrfs 檔案自我修復
    > 
    > 傳統的儲存系統可能沒有錯誤回報機制，導致資料損毀時無法獲得任何警告或錯誤通知。為了避免這類的問題，Btrfs 檔案系統提供資料以及中繼資料的總和檢查碼，在讀取資料的過程中進行驗證。一旦發現錯誤比對 (無聲資料損毀)，Btrfs 檔案系統能夠透過鏡像中繼資料自動偵測到損毀的檔案 (無聲資料損毀)，並使用支援的 RAID 儲存空間類型來還原受損的資料，包括 RAID 1、RAID 5、RAID 6、RAID 10 以及 SHR。
    > 
    > ![](https://www.synology.com/img/dsm/btrfs/benefits_icon_03.png)
    > 
    > #### 快照與資料保護
    > 
    > Btrfs 檔案系統提供強大的快照功能，讓你在任意時間點複製整個共用資料夾。因此，若因人為疏失導致資料庫毀損，你可以在短時間內利用快照還原資料。
    > 
    > #### 影響極小，好處極多
    > 
    > 透過 Btrfs 寫入時複製功能，截取快照只占用一點額外的儲存空間，同時不影響系統效能。
    > 
    > #### 頻繁的排程備份
    > 
    > 可自動執行即時資料備份，最高可達每五分鐘一次，在不影響效能的情況下，提供精細備份與還原。
    > 
    > #### 可彈性調整的保留規則
    > 
    > 依照個人需求保留每小時、每天或每週的快照，最多 256 份。智慧保留政策自動刪除不重要的版本。
    > 
    > #### 即時快照
    > 
    > 即時截取快照與備份資料，毋需擔心檔案在備份作業中被更改或被刪除。
    > 
    > #### 自行還原
    > 
    > 使用者可以利用 File Station 或 Windows File Explorer 瀏覽舊的版本並自行還原至先前的時間點。
    > 
    > #### 即時 SMB / AFP 伺服器端複製技術
    > 
    > 傳統伺服器端的檔案複製需要花費一定的作業時間，相較之下，當來源與目的地位於相同的 Btrfs 儲存空間時，Btrfs 的快速複製技術便能在 File Station、SMB 及 AFP 協定中完成即時的檔案複製。
    > 
    > 更多 Btrfs 的優點
    > ------------
    > 
    > ### 於 Synology NAS 上使用 Btrfs 檔案系統可為 DiskStation Manager 和其他 Synology 套件帶來諸多好處。
    > 
    > #### 高效的 Drive 儲存
    > 
    > 相較於 Ext4，Btrfs 檔案系統只需要一半的儲存空間儲存 Drive 的檔案版本以及歷史紀錄。你可以使用 Drive 保留歷史版本，毋須擔心佔據太多的儲存空間。
    > 
    > ![](https://www.synology.com/img/dsm/btrfs/additional_benefits_01.png)
    > 
    > #### 備份資料的一致性
    > 
    > 傳統的備份方法將資料從一處複製到另一處，若備份過程中修改資料，可能導致資料不一致的狀況。Btrfs 檔案系統可在執行備份作業前進行快照並將其複製到備份目的地，毋須擔心資料被修改、移動或刪除。
    > 
    > ![](https://www.synology.com/img/dsm/btrfs/additional_benefits_02.gif)
    > 
    > #### 共用資料夾配額
    > 
    > 為共用資料夾設定特定的儲存空間限制，讓你的儲存空間不被特定的共用資料夾佔據。當多個團隊或部門共同使用一台 Synology NAS 時，你可以透過此機制掌控可用的儲存空間。
    > 
    > ![](https://www.synology.com/img/dsm/btrfs/additional_benefits_03.png)
    > 
    > #### 複製共用資料夾的所有內容
    > 
    > 透過 Btrfs 檔案系統，你可以選擇共用資料夾並即時地複製其所有內容。快速的複製功能讓你可以在網站檢測或資料庫更新時快速地複製內容。
    > 

- [新一代 Linux 文件系统 btrfs 简介](https://www.ibm.com/developerworks/cn/linux/l-cn-btrfs/index.html)

    > Btrfs 简介
    > --------
    > 
    > 文件系统似乎是内核中比较稳定的部分，多年来，人们一直使用 ext2/3，ext 文件系统以其卓越的稳定性成为了事实上的 Linux 标准文件系统。近年来 ext2/3 暴露出了一些扩展性问题，于是便催生了 ext4 。在 2008 年发布的 Linux2.6.19 内核中集成了 ext4 的 dev 版本。 2.6.28 内核发布时，ext4 结束了开发版，开始接受用户的使用。似乎 ext 就将成为 Linux 文件系统的代名词。然而当您阅读很多有关 ext4 的文章时，会发现都不约而同地提到了 btrfs，并认为 ext4 将是一个过渡的文件系统。 ext4 的作者 Theodore Tso 也盛赞 btrfs 并认为 btrfs 将成为下一代 Linux 标准文件系统。 Oracle，IBM， Intel 等厂商也对 btrfs 表现出了极大的关注，投入了资金和人力。为什么 btrfs 如此受人瞩目呢。这便是本文首先想探讨的问题。
    > 
    > Kevin Bowling[1] 有一篇介绍各种文件系统的文章，在他看来，ext2/3 等文件系统属于"古典时期"。文件系统的新时代是 2005 年由 Sun 公司的 ZFS 开创的。 ZFS 代表" last word in file system "，意思是此后再也不需要开发其他的文件系统了。 ZFS 的确带来了很多崭新的观念，对文件系统来讲是一个划时代的作品。
    > 
    > 如果您比较 btrfs 的特性，将会发现 btrfs 和 ZFS 非常类似。也许我们可以认为 btrfs 就是 Linux 社区对 ZFS 所作出的回应。从此往后在 Linux 中也终于有了一个可以和 ZFS 相媲美的文件系统。
    > 
    > btrfs 的特性
    > ---------
    > 
    > 您可以在 btrfs 的主页上 [2] 看到 btrfs 的特性列表。我自作主张，将那张列表分成了四大部分。
    > 
    > 首先是扩展性 (scalability) 相关的特性，btrfs 最重要的设计目标是应对大型机器对文件系统的扩展性要求。 Extent，B-Tree 和动态 inode 创建等特性保证了 btrfs 在大型机器上仍有卓越的表现，其整体性能而不会随着系统容量的增加而降低。
    > 
    > 其次是数据一致性 (data integrity) 相关的特性。系统面临不可预料的硬件故障，Btrfs 采用 COW 事务技术来保证文件系统的一致性。 btrfs 还支持 checksum，避免了 silent corrupt 的出现。而传统文件系统则无法做到这一点。
    > 
    > 第三是和多设备管理相关的特性。 Btrfs 支持创建快照 (snapshot)，和克隆 (clone) 。 btrfs 还能够方便的管理多个物理设备，使得传统的卷管理软件变得多余。
    > 
    > 最后是其他难以归类的特性。这些特性都是比较先进的技术，能够显著提高文件系统的时间 / 空间性能，包括延迟分配，小文件的存储优化，目录索引等。
    > 
    > ### 扩展性相关的特性
    > 
    > B-Tree
    > 
    > btrfs 文件系统中所有的 metadata 都由 BTree 管理。使用 BTree 的主要好处在于查找，插入和删除操作都很高效。可以说 BTree 是 btrfs 的核心。
    > 
    > 一味地夸耀 BTree 很好很高效也许并不能让人信服，但假如稍微花费一点儿时间看看 ext2/3 中元数据管理的实现方式，便可以反衬出 BTree 的优点。
    > 
    > 妨碍 ext2/3 扩展性的一个问题来自其目录的组织方式。目录是一种特殊的文件，在 ext2/3 中其内容是一张线性表格。如图 1-1 所示 [6]：
    > 
    > ##### 图 1. ext2 directory [6]
    > 
    > ![ext2 directory](https://www.ibm.com/developerworks/cn/linux/l-cn-btrfs/image001.jpg)
    > 
    > 图 1 展示了一个 ext2 目录文件的内容，该目录中包含四个文件。分别是 "home1"，"usr"，"oldfile" 和 "sbin" 。如果需要在该目录中查找目录 sbin，ext2 将遍历前三项，直至找到 sbin 这个字符串为止。
    > 
    > 这种结构在文件个数有限的情况下是比较直观的设计，但随着目录下文件数的增加，查找文件的时间将线性增长。 2003 年，ext3 设计者开发了目录索引技术，解决了这个问题。目录索引使用的数据结构就是 BTree 。如果同一目录下的文件数超过 2K，inode 中的 i_data 域指向一个特殊的 block 。在该 block 中存储着目录索引 BTree 。 BTree 的查找效率高于线性表，
    > 
    > 但为同一个元数据设计两种数据结构总是不太优雅。在文件系统中还有很多其他的元数据，用统一的 BTree 管理是非常简单而优美的设计。
    > 
    > Btrfs 内部所有的元数据都采用 BTree 管理，拥有良好的可扩展性。 btrfs 内部不同的元数据由不同的 Tree 管理。在 superblock 中，有指针指向这些 BTree 的根。如图 2 所示：
    > 
    > ##### 图 2. btrfs btree
    > 
    > ![btrfs btree](https://www.ibm.com/developerworks/cn/linux/l-cn-btrfs/image002.jpg)
    > 
    > FS Tree 管理文件相关的元数据，如 inode，dir 等； Chunk tree 管理设备，每一个磁盘设备都在 Chunk Tree 中有一个 item ； Extent Tree 管理磁盘空间分配，btrfs 每分配一段磁盘空间，便将该磁盘空间的信息插入到 Extent tree 。查询 Extent Tree 将得到空闲的磁盘空间信息； Tree of tree root 保存很多 BTree 的根节点。比如用户每建立一个快照，btrfs 便会创建一个 FS Tree 。为了管理所有的树，btrfs 采用 Tree of tree root 来保存所有树的根节点； checksum Tree 保存数据块的校验和。
    > 
    > **基于 Extent 的文件存储**
    > 
    > 现代很多文件系统都采用了 extent 替代 block 来管理磁盘。 Extent 就是一些连续的 block，一个 extent 由起始的 block 加上长度进行定义。
    > 
    > Extent 能有效地减少元数据开销。为了进一步理解这个问题，我们还是看看 ext2 中的反面例子。
    > 
    > ext2/3 以 block 为基本单位，将磁盘划分为多个 block 。为了管理磁盘空间，文件系统需要知道哪些 block 是空闲的。 Ext 使用 bitmap 来达到这个目的。 Bitmap 中的每一个 bit 对应磁盘上的一个 block，当相应 block 被分配后，bitmap 中的相应 bit 被设置为 1 。这是很经典也很清晰的一个设计，但不幸的是当磁盘容量变大时，bitmap 自身所占用的空间也将变大。这就导致了扩展性问题，随着存储设备容量的增加，bitmap 这个元数据所占用的空间也随之增加。而人们希望无论磁盘容量如何增加，元数据不应该随之线形增加，这样的设计才具有可扩展性。
    > 
    > 下图比较了 block 和 extent 的区别：
    > 
    > ##### 图 3. 采用 extent 的 btrfs 和采用 bitmap 的 ext2/3
    > 
    > ![采用extent的btrfs和采用bitmap的ext2/3](https://www.ibm.com/developerworks/cn/linux/l-cn-btrfs/image003.jpg)
    > 
    > 在 ext2/3 中，10 个 block 需要 10 个 bit 来表示；在 btrfs 中则只需要一个元数据。对于大文件，extent 表现出了更加优异的管理性能。
    > 
    > Extent 是 btrfs 管理磁盘空间的最小单位，由 extent tree 管理。 Btrfs 分配 data 或 metadata 都需要查询 extent tree 以便获得空闲空间的信息。
    > 
    > **动态 inode 分配**
    > 
    > 为了理解动态 inode 分配，还是需要借助 ext2/3 。下表列举了 ext2 文件系统的限制：
    > 
    > ##### 表 1. ext2 限制
    > 
    > |  | 限制 |
    > | --- | --- |
    > | **最大文件数量** | 文件系统空间大小 V / 8192 比如 100G 大小的文件系统中，能创建的文件个数最大为 131072 |
    > 
    > 图 4 显示了 ext2 的磁盘布局：
    > 
    > ##### 图 4. ext2 layout
    > 
    > ![ext2 layout](https://www.ibm.com/developerworks/cn/linux/l-cn-btrfs/image004.jpg)
    > 
    > 在 ext2 中 inode 区是被预先固定分配的，且大小固定，比如一个 100G 的分区中，inode table 区中只能存放 131072 个 inode，这就意味着不可能创建超过 131072 个文件，因为每一个文件都必须有一个唯一的 inode 。
    > 
    > 为了解决这个问题，必须动态分配 inode 。每一个 inode 只是 BTree 中的一个节点，用户可以无限制地任意插入新的 inode，其物理存储位置是动态分配的。所以 btrfs 没有对文件个数的限制。
    > 
    > **针对 SSD 的优化支持**
    > 
    > SSD 是固态存储 Solid State Disk 的简称。在过去的几十年中，CPU/RAM 等器件的发展始终遵循着摩尔定律，但硬盘 HDD 的读写速率却始终没有飞跃式的发展。磁盘 IO 始终是系统性能的瓶颈。
    > 
    > SSD 采用 flash memory 技术，内部没有磁盘磁头等机械装置，读写速率大幅度提升。 flash memory 有一些不同于 HDD 的特性。 flash 在写数据之前必须先执行擦除操作；其次，flash 对擦除操作的次数有一定的限制，在目前的技术水平下，对同一个数据单元最多能进行约 100 万次擦除操作，因此，为了延长 flash 的寿命，应该将写操作平均到整个 flash 上。
    > 
    > SSD 在硬件内部的微代码中实现了 wear leveling 等分布写操作的技术，因此系统无须再使用特殊的 MTD 驱动和 FTL 层。虽然 SSD 在硬件层面做了很多努力，但毕竟还是有限。文件系统针对 SSD 的特性做优化不仅能提高 SSD 的使用寿命，而且能提高读写性能。 Btrfs 是少数专门对 SSD 进行优化的文件系统。 btrfs 用户可以使用 mount 参数打开对 SSD 的特殊优化处理。
    > 
    > Btrfs 的 COW 技术从根本上避免了对同一个物理单元的反复写操作。如果用户打开了 SSD 优化选项，btrfs 将在底层的块空间分配策略上进行优化：将多次磁盘空间分配请求聚合成一个大小为 2M 的连续的块。大块连续地址的 IO 能够让固化在 SSD 内部的微代码更好的进行读写优化，从而提高 IO 性能。
    > 
    > ### 数据一致性相关的特性
    > 
    > **COW 事务**
    > 
    > 理解 COW 事务，必须首先理解 COW 和事务这两个术语。
    > 
    > 什么是 COW?
    > 
    > 所谓 COW，即每次写磁盘数据时，先将更新数据写入一个新的 block，当新数据写入成功之后，再更新相关的数据结构指向新 block 。
    > 
    > 什么是事务？
    > 
    > COW 只能保证单一数据更新的原子性。但文件系统中很多操作需要更新多个不同的元数据，比如创建文件需要修改以下这些元数据：
    > 
    > 1.  修改 extent tree，分配一段磁盘空间
    > 2.  创建一个新的 inode，并插入 FS Tree 中
    > 3.  增加一个目录项，插入到 FS Tree 中
    > 
    > 任何一个步骤出错，文件便不能创建成功，因此可以定义为一个事务。
    > 
    > 下面将演示一个 COW 事务。
    > 
    > A 是 FS Tree 的根节点，新的 inode 的信息将被插入节点 C 。首先，btrfs 将 inode 插入一个新分配的 block C '中，并修改上层节点 B，使其指向新的 block C '；修改 B 也将引发 COW，以此类推，引发一个连锁反应，直到最顶层的 Root A 。当整个过程结束后，新节点 A '变成了 FS Tree 的根。但此时事务并未结束，superblock 依然指向 A 。
    > 
    > ##### 图 5. COW transaction 1
    > 
    > ![COW transaction 1](https://www.ibm.com/developerworks/cn/linux/l-cn-btrfs/image005.jpg)
    > 
    > 接下来，修改目录项（E 节点），同样引发这一过程，从而生成新的根节点 A ''。
    > 
    > ##### 图 6. COW transaction 2
    > 
    > ![COW transaction 2](https://www.ibm.com/developerworks/cn/linux/l-cn-btrfs/image006.jpg)
    > 
    > 此时，inode 和目录项都已经写入磁盘，可以认为事务已经结束。 btrfs 修改 superblock，使其指向 A ''，如下图所示：
    > 
    > ##### 图 7. COW transaction 3
    > 
    > ![COW transaction 3](https://www.ibm.com/developerworks/cn/linux/l-cn-btrfs/image007.jpg)
    > 
    > COW 事务能够保证文件系统的一致性，并且系统 Reboot 之后不需要执行 fsck 。因为 superblock 要么指向新的 A ''，要么指向 A，无论哪个都是一致的数据。
    > 
    > **Checksum**
    > 
    > Checksum 技术保证了数据的可靠性，避免 silent corruption 现象。由于硬件原因，从磁盘上读出的数据会出错。比如 block A 中存放的数据为 0x55，但读取出来的数据变是 0x54，因为读取操作并未报错，所以这种错误不能被上层软件所察觉。
    > 
    > 解决这个问题的方法是保存数据的校验和，在读取数据后检查校验和。如果不符合，便知道数据出现了错误。
    > 
    > ext2/3 没有校验和，对磁盘完全信任。而不幸的是，磁盘的错误始终存在，不仅发生在廉价的 IDE 硬盘上，昂贵的 RAID 也存在 silent corruption 问题。而且随着存储网络的发展，即使数据从磁盘读出正确，也很难确保能够安全地穿越网络设备。
    > 
    > btrfs 在读取数据的同时会读取其相应的 checksum 。如果最终从磁盘读取出来的数据和 checksum 不相同，btrfs 会首先尝试读取数据的镜像备份，如果数据没有镜像备份，btrfs 将返回错误。写入磁盘数据之前，btrfs 计算数据的 checksum 。然后将 checksum 和数据同时写入磁盘。
    > 
    > Btrfs 采用单独的 checksum Tree 来管理数据块的校验和，把 checksum 和 checksum 所保护的数据块分离开，从而提供了更严格的保护。假如在每个数据 block 的 header 中加入一个域保存 checksum，那么这个数据 block 就成为一个自己保护自己的结构。这种结构下有一种错误无法检测出来，比如本来文件系统打算从磁盘上读 block A，但返回了 block B，由于 checksum 在 block 内部，因此 checksum 依旧是正确的。 btrfs 采用 checksum tree 来保存数据块的 checksum，避免了上述问题。
    > 
    > Btrfs 采用 crc32 算法计算 checksum，在将来的开发中会支持其他类型的校验算法。为了提高效率，btrfs 将写数据和 checksum 的工作分别用不同的内核线程并行执行。
    > 
    > ### 多设备管理相关的特性
    > 
    > 每个 Unix 管理员都曾面临为用户和各种应用分配磁盘空间的任务。多数情况下，人们无法事先准确地估计一个用户或者应用在未来究竟需要多少磁盘空间。磁盘空间被用尽的情况经常发生，此时人们不得不试图增加文件系统空间。传统的 ext2/3 无法应付这种需求。
    > 
    > 很多卷管理软件被设计出来满足用户对多设备管理的需求，比如 LVM 。 Btrfs 集成了卷管理软件的功能，一方面简化了用户命令；另一方面提高了效率。
    > 
    > **多设备管理**
    > 
    > Btrfs 支持动态添加设备。用户在系统中增加新的磁盘之后，可以使用 btrfs 的命令将该设备添加到文件系统中。
    > 
    > 为了灵活利用设备空间，Btrfs 将磁盘空间划分为多个 chunk 。每个 chunk 可以使用不同的磁盘空间分配策略。比如某些 chunk 只存放 metadata，某些 chunk 只存放数据。一些 chunk 可以配置为 mirror，而另一些 chunk 则可以配置为 stripe 。这为用户提供了非常灵活的配置可能性。
    > 
    > **Subvolume**
    > 
    > Subvolume 是很优雅的一个概念。即把文件系统的一部分配置为一个完整的子文件系统，称之为 subvolume 。
    > 
    > 采用 subvolume，一个大的文件系统可以被划分为多个子文件系统，这些子文件系统共享底层的设备空间，在需要磁盘空间时便从底层设备中分配，类似应用程序调用 malloc() 分配内存一样。可以称之为存储池。这种模型有很多优点，比如可以充分利用 disk 的带宽，可以简化磁盘空间的管理等。
    > 
    > 所谓充分利用 disk 的带宽，指文件系统可以并行读写底层的多个 disk，这是因为每个文件系统都可以访问所有的 disk 。传统的文件系统不能共享底层的 disk 设备，无论是物理的还是逻辑的，因此无法做到并行读写。
    > 
    > 所谓简化管理，是相对于 LVM 等卷管理软件而言。采用存储池模型，每个文件系统的大小都可以自动调节。而使用 LVM，如果一个文件系统的空间不够了，该文件系统并不能自动使用其他磁盘设备上的空闲空间，而必须使用 LVM 的管理命令手动调节。
    > 
    > Subvolume 可以作为根目录挂载到任意 mount 点。 subvolume 是非常有趣的一个特性，有很多应用。
    > 
    > 假如管理员只希望某些用户访问文件系统的一部分，比如希望用户只能访问 /var/test/ 下面的所有内容，而不能访问 /var/ 下面其他的内容。那么便可以将 /var/test 做成一个 subvolume 。 /var/test 这个 subvolume 便是一个完整的文件系统，可以用 mount 命令挂载。比如挂载到 /test 目录下，给用户访问 /test 的权限，那么用户便只能访问 /var/test 下面的内容了。
    > 
    > 快照和克隆
    > 
    > 快照是对文件系统某一时刻的完全备份。建立快照之后，对文件系统的修改不会影响快照中的内容。这是非常有用的一种技术。
    > 
    > 比如数据库备份。假如在时间点 T1，管理员决定对数据库进行备份，那么他必须先停止数据库。备份文件是非常耗时的操作，假如在备份过程中某个应用程序修改了数据库的内容，那么将无法得到一个一致性的备份。因此在备份过程中数据库服务必须停止，对于某些关键应用这是不能允许的。
    > 
    > 利用快照，管理员可以在时间点 T1 将数据库停止，对系统建立一个快照。这个过程一般只需要几秒钟，然后就可以立即重新恢复数据库服务。此后在任何时候，管理员都可以对快照的内容进行备份操作，而此时用户对数据库的修改不会影响快照中的内容。当备份完成，管理员便可以删除快照，释放磁盘空间。
    > 
    > 快照一般是只读的，当系统支持可写快照，那么这种可写快照便被称为克隆。克隆技术也有很多应用。比如在一个系统中安装好基本的软件，然后为不同的用户做不同的克隆，每个用户使用自己的克隆而不会影响其他用户的磁盘空间。非常类似于虚拟机。
    > 
    > Btrfs 支持 snapshot 和 clone 。这个特性极大地增加了 btrfs 的使用范围，用户不需要购买和安装昂贵并且使用复杂的卷管理软件。下面简要介绍一下 btrfs 实现快照的基本原理。
    > 
    > 如前所述 Btrfs 采用 COW 事务技术，从图 1-10 可以看到，COW 事务结束后，如果不删除原来的节点 A,C,E，那么 A,C,E,D,F 依然完整的表示着事务开始之前的文件系统。这就是 snapshot 实现的基本原理。
    > 
    > Btrfs 采用引用计数决定是否在事务 commit 之后删除原有节点。对每一个节点，btrfs 维护一个引用计数。当该节点被别的节点引用时，该计数加一，当该节点不再被别的节点引用时，该计数减一。当引用计数归零时，该节点被删除。对于普通的 Tree Root, 引用计数在创建时被加一，因为 Superblock 会引用这个 Root block 。很明显，初始情况下这棵树中的所有其他节点的引用计数都为一。当 COW 事务 commit 时，superblock 被修改指向新的 Root A ''，原来 Root block A 的引用计数被减一，变为零，因此 A 节点被删除。 A 节点的删除会引发其子孙节点的引用计数也减一，图 1-10 中的 B，C 节点的引用计数因此也变成了 0，从而被删除。 D,E 节点在 COW 时，因为被 A ''所引用，计数器加一，因此计数器这时并未归零，从而没有被删除。
    > 
    > 创建 Snapshot 时，btrfs 将的 Root A 节点复制到 sA，并将 sA 的引用计数设置为 2 。在事务 commit 的时候，sA 节点的引用计数不会归零，从而不会被删除，因此用户可以继续通过 Root sA 访问 snapshot 中的文件。
    > 
    > ##### 图 8. Snapshot
    > 
    > ![Snapshot](https://www.ibm.com/developerworks/cn/linux/l-cn-btrfs/image008.jpg)
    > 
    > **软件 RAID**
    > 
    > RAID 技术有很多非常吸引人的特性，比如用户可以将多个廉价的 IDE 磁盘组合为 RAID0 阵列，从而变成了一个大容量的磁盘； RAID1 和更高级的 RAID 配置还提供了数据冗余保护，从而使得存储在磁盘中的数据更加安全。
    > 
    > Btrfs 很好的支持了软件 RAID，RAID 种类包括 RAID0,RAID1 和 RAID10.
    > 
    > Btrfs 缺省情况下对 metadata 进行 RAID1 保护。前面已经提及 btrfs 将设备空间划分为 chunk，一些 chunk 被配置为 metadata，即只存储 metadata 。对于这类 chunk，btrfs 将 chunk 分成两个条带，写 metadata 的时候，会同时写入两个条带内，从而实现对 metadata 的保护。
    > 
    > ### 其他特性
    > 
    > Btrfs 主页上罗列的其他特性不容易分类，这些特性都是现代文件系统中比较先进的技术，能够提高文件系统的时间或空间效率。
    > 
    > **Delay allocation**
    > 
    > 延迟分配技术能够减少磁盘碎片。在 Linux 内核中，为了提高效率，很多操作都会延迟。
    > 
    > 在文件系统中，小块空间频繁的分配和释放会造成碎片。延迟分配是这样一种技术，当用户需要磁盘空间时，先将数据保存在内存中。并将磁盘分配需求发送给磁盘空间分配器，磁盘空间分配器并不立即分配真正的磁盘空间。只是记录下这个请求便返回。
    > 
    > 磁盘空间分配请求可能很频繁，所以在延迟分配的一段时间内，磁盘分配器可以收到很多的分配请求，一些请求也许可以合并，一些请求在这段延迟期间甚至可能被取消。通过这样的"等待"，往往能够减少不必要的分配，也有可能将多个小的分配请求合并为一个大的请求，从而提高 IO 效率。
    > 
    > **Inline file**
    > 
    > 系统中往往存在大量的小文件，比如几百个字节或者更小。如果为其分配单独的数据 block，便会引起内部碎片，浪费磁盘空间。 btrfs 将小文件的内容保存在元数据中，不再额外分配存放文件数据的磁盘块。改善了内部碎片问题，也增加了文件的访问效率。
    > 
    > ##### 图 9. inline file
    > 
    > ![inline file](https://www.ibm.com/developerworks/cn/linux/l-cn-btrfs/image009.jpg)
    > 
    > 上图显示了一个 BTree 的叶子节点。叶子中有两个 extent data item 元数据，分别用来表示文件 file1 和 file2 所使用的磁盘空间。
    > 
    > 假设 file1 的大小仅为 15 个字节； file2 的大小为 1M 。如图所示，file2 采用普通的 extent 表示方法：extent2 元数据指向一段 extent，大小为 1M，其内容便是 file2 文件的内容。
    > 
    > 而对于 file1， btrfs 会把其文件内容内嵌到元数据 extent1 中。如果不采用 inline file 技术。如虚线所示，extent1 指向一个最小的 extent，即一个 block，但 file1 有 15 个字节，其余的空间便成为了碎片空间。
    > 
    > 采用 inline 技术，读取 file1 时只需要读取元数据 block，而无需先读取 extent1 这个元数据，再读取真正存放文件内容的 block，从而减少了磁盘 IO 。
    > 
    > 得益于 inline file 技术，btrfs 处理小文件的效率非常高，也避免了磁盘碎片问题。
    > 
    > **目录索引 Directory index**
    > 
    > 当一个目录下的文件数目巨大时，目录索引可以显著提高文件搜索时间。 Btrfs 本身采用 BTree 存储目录项，所以在给定目录下搜索文件的效率是非常高的。
    > 
    > 然而，btrfs 使用 BTree 管理目录项的方式无法同时满足 readdir 的需求。 readdir 是 POSIX 标准 API，它要求返回指定目录下的所有文件，并且特别的，这些文件要按照 inode number 排序。而 btrfs 目录项插入 BTree 时的 Key 并不是 Inode number，而是根据文件名计算的一个 hash 值。这种方式在查找一个特定文件时非常高效，但却不适于 readdir 。为此，btrfs 在每次创建新的文件时，除了插入以 hash 值为 Key 的目录项外，还同时插入另外一种目录项索引，该目录项索引的 KEY 以 sequence number 作为 BTree 的键值。这个 sequence number 在每次创建新文件时线性增加。因为 Inode number 也是每次创建新文件时增加的，所以 sequence number 和 inode number 的顺序相同。以这种 sequence number 作为 KEY 在 BTree 中查找便可以方便的得到一个以 inode number 排序的文件列表。
    > 
    > 另外以 sequence number 排序的文件往往在磁盘上的位置也是相邻的，所以以 sequence number 为序访问大量文件会获得更好的 IO 效率。
    > 
    > 压缩
    > 
    > 大家都曾使用过 zip，winrar 等压缩软件，将一个大文件进行压缩可以有效节约磁盘空间。 Btrfs 内置了压缩功能。
    > 
    > 通常人们认为将数据写入磁盘之前进行压缩会占用很多的 CPU 计算时间，必然降低文件系统的读写效率。但随着硬件技术的发展，CPU 处理时间和磁盘 IO 时间的差距不断加大。在某些情况下，花费一定的 CPU 时间和一些内存，但却能大大节约磁盘 IO 的数量，这反而能够增加整体的效率。
    > 
    > 比如一个文件不经过压缩的情况下需要 100 次磁盘 IO 。但花费少量 CPU 时间进行压缩后，只需要 10 次磁盘 IO 就可以将压缩后的文件写入磁盘。在这种情况下，IO 效率反而提高了。当然，这取决于压缩率。目前 btrfs 采用 zlib 提供的 DEFALTE/INFLATE 算法进行压缩和解压。在将来，btrfs 应该可以支持更多的压缩算法，满足不同用户的不同需求。
    > 
    > 目前 btrfs 的压缩特性还存在一些不足，当压缩使能后，整个文件系统下的所有文件都将被压缩，但用户可能需要更细粒度的控制，比如针对不同的目录采用不同的压缩算法，或者禁止压缩。我相信，btrfs 开发团队将在今后的版本中解决这个问题。
    > 
    > 对于某些类型的文件，比如 jpeg 文件，已经无法再进行压缩。尝试对其压缩将纯粹浪费 CPU 。为此，当对某文件的若干个 block 压缩后发现压缩率不佳，btrfs 将不会再对文件的其余部分进行压缩操作。这个特性在某种程度上提高了文件系统的 IO 效率。
    > 
    > 预分配
    > 
    > 很多应用程序有预先分配磁盘空间的需要。他们可以通过 posix_fallocate 接口告诉文件系统在磁盘上预留一部分空间，但暂时并不写入数据。如果底层文件系统不支持 fallocate，那么应用程序只有使用 write 预先写一些无用信息以便为自己预留足够的磁盘空间。
    > 
    > 由文件系统来支持预留空间更加有效，而且能够减少磁盘碎片，因为所有的空间都是一次分配，因而更有可能使用连续的空间。 Btrfs 支持 posix_fallocate 。
    > 
    > ### 总结
    > 
    > 至此，我们对 btrfs 的很多特性进行了较为详细的探讨，但 btrfs 能提供的特性却并不止这些。 btrfs 正处于试验开发阶段，还将有更多的特性。
    > 
    > Btrfs 也有一个重要的缺点，当 BTree 中某个节点出现错误时，文件系统将失去该节点之下的所有的文件信息。而 ext2/3 却避免了这种被称为"错误扩散"的问题。
    > 
    > 但无论怎样，希望您和我一样，开始认同 btrfs 将是 Linux 未来最有希望的文件系统。
    > 
    > BTRFS 使用简介
    > ----------
    > 
    > 了解了 btrfs 的特性，想必您一定想亲身体验一下 btrfs 的使用。本章将简要介绍如何使用 btrfs 。
    > 
    > ### 创建文件系统
    > 
    > mkfs.btrfs 命令建立一个 btrfs 格式的文件系统。可以用如下命令在设备 sda5 上建立一个 btrfs 文件系统，并将其挂载到 /btrfsdisk 目录下：
    > 
    > ```
    > #mkfs.btrfs /dev/sda5
    > 
    > #mkdir /btrfsdisk
    > 
    > #mount -- t btrfs /dev/sda5 /btrfsdisk
    > 
    > ```
    > 
    > 这样一个 Btrfs 就在设备 sda5 上建立好了。值得一提的是在这种缺省情况下，即使只有一个设备，Btrfs 也会对 metadata 进行冗余保护。如果有多个设备，那么您可以在创建文件系统的时候进行 RAID 设置。详细信息请参见后续的介绍。
    > 
    > 这里介绍其他几个 mkfs.btrfs 的参数。
    > 
    > Nodesize 和 leafsize 用来设定 btrfs 内部 BTree 节点的大小，缺省为一个 page 大小。但用户也可以使用更大的节点，以便增加 fanout，减小树的高度，当然这只适合非常大的文件系统。
    > 
    > Alloc-start 参数用来指定文件系统在磁盘设备上的起始地址。这使得用户可以方便的预留磁盘前面的一些特殊空间。
    > 
    > Byte-count 参数设定文件系统的大小，用户可以只使用设备的一部分空间，当空间不足时再增加文件系统大小。
    > 
    > ### 修改文件系统的大小
    > 
    > 当文件系统建立好之后，您可以修改文件系统的大小。 /dev/sda5 挂载到了 /btrfsdisk 下，大小为 800M 。假如您希望只使用其中的 500M，则需要减小当前文件系统的大小，这可以通过如下命令实现：
    > ```
    > #df
    > 
    > Filesystem   1K-blocks     Used      Available   Use%   Mounted on
    > 
    > /dev/sda1    101086        19000       76867         20%     /boot
    > 
    > /dev/sda5    811248         32       811216         1%     /btrfsdisk
    > 
    > #btrfsctl -- r -300M /btrfsdisk
    > 
    > #df
    > 
    > Filesystem  1K-blocks      Used      Available   Use%   Mounted on
    > 
    > /dev/sda1    101086        19000       76867         20%     /boot
    > 
    > /dev/sda5    504148         32       504106         1%     /btrfsdisk
    > ```
    > 
    > 同样的，您可以使用 btrfsctl 命令增加文件系统的大小。
    > 
    > ### 创建 Snapshot
    > 
    > 下面的例子中，创建快照 snap1 时系统存在 2 个文件。创建快照之后，对 test1 的内容进行修改。再回到 snap1，打开 test1 文件，可以看到 test1 的内容依旧是之前的内容。
    > 
    > ```
    > #ls /btrfsdisk
    > 
    > test1 test2
    > 
    > #vi test1
    > 
    > This is a test
    > 
    > #btrfsctl -- s snap1 /btrfsdisk
    > 
    > #vi test1
    > 
    > Test1 is modified
    > 
    > #cd /btrfsdisk/snap1
    > 
    > #cat test1
    > 
    > This is a test
    > ```
    > 
    > 可以从上面的例子看到，快照 snap1 保存的内容不会被后续的写操作所改变。
    > 
    > ### 创建 subvolume
    > 
    > 使用 btrfs 命令，用户可以方便的建立 subvolume 。假设 /btrfsdisk 已经挂载到了 btrfs 文件系统，则用户可以在这个文件系统内创建新的 subvolume 。比如建立一个 /sub1 的 subvolume，并将 sub1 挂载到 /mnt/test 下：
    > 
    > ```
    > #mkdir /mnt/test
    > 
    > #btrfsctl -- S sub1 /btrfsdisk
    > 
    > #mount -- t btrfs -- o subvol=sub1 /dev/sda5 /mnt/test
    > ```
    > 
    > Subvolme 可以方便管理员在文件系统上创建不同用途的子文件系统，并对其进行一些特殊的配置，比如有些目录下的文件关注节约磁盘空间，因此需要打开压缩，或者配置不同的 RAID 策略等。目前 btrfs 尚处于开发阶段，创建的 subvolme 和 snapshot 还无法删除。此外针对 subvolume 的磁盘 quota 功能也未能实现。但随着 btrfs 的不断成熟，这些功能必然将会进一步完善。
    > 
    > ### 创建 RAID
    > 
    > mkfs 的时候，可以指定多个设备，并配置 RAID 。下面的命令演示了如何使用 mkfs.btrfs 配置 RAID1 。 Sda6 和 sda7 可以配置为 RAID1，即 mirror 。用户可以选择将数据配置为 RAID1，也可以选择将元数据配置为 RAID1 。
    > 
    > 将数据配置为 RAID1，可以使用 mkfs.btrfs 的 -d 参数。如下所示：
    > 
    > 
    > 
    > ```
    > #mkfs.btrfs -- d raid1 /dev/sda6 /dev/sda7
    > 
    > #mount -- t btrfs /dev/sda6 /btrfsdisk
    > ```
    > 
    > ### 添加新设备
    > 
    > 当设备的空间快被使用完的时候，用户可以使用 btrfs-vol 命令为文件系统添加新的磁盘设备，从而增加存储空间。下面的命令向 /btrfsdisk 文件系统增加一个设备 /sda8
    > 
    > ```
    > #btrfs-vol -- a /dev/sda8 /btrfsdisk
    > ```
    > 
    > ### SSD 支持
    > 
    > 用户可以使用 mount 参数打开 btrfs 针对 SSD 的优化。命令如下：
    > 
    > ```
    > #mount -- t btrfs -- o SSD /dev/sda5 /btrfsdisk
    > ```
    > 
    > ***开启压缩功能***
    > 
    > 用户可以使用 mount 参数打开压缩功能。命令如下：
    > 
    > ```
    > 
    > #mount -- t btrfs -- o compress /dev/sda5 /btrfsdisk
    > ```
    > 
    > ***同步文件系统***
    > 
    > 为了提高效率，btrfs 的 IO 操作由一些内核线程异步处理。这使得用户对文件的操作并不会立即反应到磁盘上。您可以做一个实验，在 btrfs 上创建一个文件后，稍等 5 到 10 秒将系统电源切断，再次重启后，新建的文件并没有出现。
    > 
    > 对于多数应用这并不是问题，但有些时候用户希望 IO 操作立即执行，此时就需要对文件系统进行同步。下面的 btrfs 命令用来同步文件系统：
    > 
    > ```
    > 
    > #btrfsctl -- c /btrfsdisk
    > ```
    > 
    > ### Debug 功能
    > 
    > Btrfs 提供了一定的 debug 功能，对于想了解 Btrfs 内部实现原理的读者，debug 将是您最喜欢的工具。这里简单介绍一下 debug 功能的命令使用。
    > 
    > 下面的命令将设备 sda5 上的 btrfs 文件系统中的元数据打印到屏幕上。
    > 
    > ```
    > #btrfs-debug-tree /dev/sda5
    > ```
    > 
    > 通过对打印信息的分析，您将能了解 btrfs 内部各个 BTree 的变化情况，从而进一步理解每一个文件系统功能的内部实现细节。
    > 
    > 比如您可以在创建一个文件之前将 BTree 的内容打印出来，创建文件后再次打印。通过比较两次的不同来了解 btrfs 创建一个文件需要修改哪些元数据。进而理解 btrfs 内部的工作原理。
    > 
    > 


### compress

- [Btrfs Zstd Compression Benchmarks On Linux 4.14 - Phoronix](https://www.phoronix.com/scan.php?page=article&item=btrfs-zstd-compress&num=1)

    > Overall, among the Btrfs compression options, Zstd is performing very well. Keep in mind though with I/O benchmarks, the data tends to be easily compressible compared to more real-world and unique data-sets. It will also be interesting to see how the Btrfs compression performance compares on Linux 4.15 where there is configurable Zlib compression levels and also improvements around the overall Btrfs compression heuristics.

- [How to set a non default zstd compression level at btrfs filesystem defragment? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/412480/how-to-set-a-non-default-zstd-compression-level-at-btrfs-filesystem-defragment)

    - [Compression - btrfs Wiki](https://btrfs.wiki.kernel.org/index.php/Compression)

        > The level support of ZLIB has been added in v4.14, LZO does not support levels (the kernel implementation provides only one), ZSTD level support is planned. 

- [BTRFS - caution before using ZSTD compression - boot problems](https://www.kubuntuforums.net/showthread.php/73616-BTRFS-caution-before-using-ZSTD-compression-boot-problems)

    > Until this is addressed (the developers are aware), **only use ZSTD on non-booting file systems.**


- [kernel/git/mason/linux-btrfs.git - Unnamed repository; edit this file 'description' to name the repository.](https://git.kernel.org/pub/scm/linux/kernel/git/mason/linux-btrfs.git/commit/?h=next&id=5c1aab1dd5445ed8bdcdbb575abc1b0d7ee5b2e7)

    > | Method | Tar Ratio | Extract Ratio | Copy (s) | Extract (s)| Read (s) | 
    > |--------|-----------|---------------|----------|------------|----------|
    > | None | 0.97 | 0.78 | 0.981 | 5.501 | 8.807 | | lzo | 2.06 | 1.38 | 1.631 | 8.458 | 8.585 |
    > | zlib | 3.40 | 1.86 | 7.750 | 21.544 | 11.744 |
    > | zstd 1 | 3.57 | 1.85 | 2.579 | 11.479 | 9.389 |
    > 


### enable compress

- [Compression - btrfs Wiki](https://btrfs.wiki.kernel.org/index.php/Compression)

    > How do I enable compression?
    > ============================
    > 
    > Mount with [-o compress](https://btrfs.wiki.kernel.org/index.php/Mount_options#compress "Mount options") or [-o compress-force](https://btrfs.wiki.kernel.org/index.php/Mount_options#compress "Mount options"). Then write (or re-write) files, and they will be transparently compressed. Some files may not compress very well, and these are typically not recompressed but still written uncompressed. See the [What happens to incompressible files?](https://btrfs.wiki.kernel.org/index.php/Compression#incompressible) section, below.
    > 
    > What is the default compression method?
    > ---------------------------------------
    > 
    > ZLIB. The 'default' means if it's specified by the mount option 'compress' or 'compress-force', or via `chattr +c`, or `btrfs filesystem defrag -c`.
    > 
    > Can I set the compression level?
    > --------------------------------
    > 
    > The level support of ZLIB has been added in v4.14, LZO does not support levels (the kernel implementation provides only one), ZSTD level support is planned.
    > 
    > There are 9 levels of ZLIB supported (1 to 9), mapping 1:1 from the mount option to the algorithm defined level. The default is level 3, which provides the highest compression ratio and is still reasonably fast. The difference in compression gain of levels 7, 8 and 9 is comparable but the higher levels take longer. The level can be specified as the mount option, as "compress=zlib:1". Level 0 maps to the default.
    > 
    > What are the differences between compression methods?
    > =====================================================
    > 
    > There's a speed/ratio trade-off:
    > 
    > -   ZLIB -- slower, higher compression ratio (uses zlib level 3 setting, you can see the zlib level difference between 1 and 6 in zlib sources).
    > -   LZO -- faster compression and decompression than zlib, worse compression ratio, designed to be fast
    > -   ZSTD -- *(since v4.14)* compression comparable to zlib with higher compression/decompression speeds and different ratio levels ([details](https://git.kernel.org/pub/scm/linux/kernel/git/mason/linux-btrfs.git/commit/?h=next&id=5c1aab1dd5445ed8bdcdbb575abc1b0d7ee5b2e7))
    > 
    > The differences depend on the actual data set and cannot be expressed by a single number or recommendation. Do your own benchmarks. LZO seems to give satisfying results for general use.
    > 

- [Will btrfs automatically compress existing files when compression is enabled? - Ask Ubuntu](https://askubuntu.com/questions/129063/will-btrfs-automatically-compress-existing-files-when-compression-is-enabled)

    > You will have to run `btrfs fi defragment` to force recompression of existing data. Otherwise, only new data will be compressed.
    > 
    > From [the FAQ](https://btrfs.wiki.kernel.org/index.php/FAQ#if_your_device_is_small):
    > 
    > > ...consider remounting with `-o compress`, and either rewrite particular files in-place, or run `btrfs fi defragment` to recompress everything. This may take a while.

### defragment

- [Manpage/btrfs-filesystem - btrfs Wiki](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs-filesystem)

    > **$ btrfs filesystem defrag -v -r dir/**
    > 
    > Recursively defragment files under *dir/*, print files as they are processed. The file names will be printed in batches, similarly the amount of data triggered by defragmentation will be proportional to last N printed files. The system dirty memory throttling will slow down the defragmentation but there can still be a lot of IO load and the system may stall for a moment.
    > 
    > **$ btrfs filesystem defrag -v -r -f dir/**
    > 
    > Recursively defragment files under *dir/*, be verbose and wait until all blocks are flushed before processing next file. You can note slower progress of the output and lower IO load (proportional to currently defragmented file).
    > 
    > **$ btrfs filesystem defrag -v -r -f -clzo dir/**
    > 
    > Recursively defragment files under *dir/*, be verbose, wait until all blocks are flushed and force file compression.
    > 
    > **$ btrfs filesystem defrag -v -r -t 64M dir/**
    > 
    > Recursively defragment files under *dir/*, be verbose and try to merge extents to be about 64MiB. As stated above, the success rate depends on actual free space fragmentation and the final result is not guaranteed to meet the target even if run repeatedly.
    > 
    > **$ btrfs filesystem resize -1G /path**
    > 
    > **$ btrfs filesystem resize 1:-1G /path**
    > 
    > Shrink size of the filesystem's device id 1 by 1GiB. The first syntax expects a device with id 1 to exist, otherwise fails. The second is equivalent and more explicit. For a single-device filesystem it's typically not necessary to specify the devid though.
    > 
    > **$ btrfs filesystem resize max /path**
    > 
    > **$ btrfs filesystem resize 1:max /path**
    > 
    > Let's assume that devid 1 exists, the filesystem does not occupy the whole block device, eg. it has been enlarged and we wan the grow the filesystem. Simply using *max* as size we will achieve that.
    > 
    > 

- [defragmentation - btrfs — Is it dangerous to defragment subvolume which has readonly snapshots? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/400225/btrfs-is-it-dangerous-to-defragment-subvolume-which-has-readonly-snapshots)

    > ### Btrfs defrag won't break *all* reflinks
    > 
    > Just the particular instances you point it at. So, if you have subvolume `A`, and snapshots `S1` and `S2` of that subvolume `A`, then running defrag on *just* subvolume `A` will break the reflinks between it and the snapshots, but `S1` and `S2` will still share any data they were originally with each other. If you then take a third snapshot of `A`, it will share data with `A`, but not with `S1` or `S2` (because `A` is no longer sharing data with `S1` or `S2`).
    > 
    > Given this behavior, you have in turn three potential cases when talking about persistent snapshots:
    > 
    > 1.  You care about **minimizing space** used, but aren't as worried about performance.\
    >     In this case, the only option is to **not run defrag at all**.
    > 2.  You care about **performance**, but not space usage. In this case, **defragment everything**.
    > 3.  You care about both space usage and performance. In this **balanced** case, I would personally suggest defragmenting only the source subvolume (so only subvolume `A` in the above explanation), and doing so on a schedule that coincides with snapshot rotation. The idea is to `defragment` just before you take a snapshot, and at a frequency that gives a good balance between space usage and performance. As a general rule, if you take this route, start by doing the defrag on either a monthly basis if you're doing daily or weekly snapshots, or with every fourth snapshot if not, and then adjust the interval based on how that impacts your space usage.
    > 
    > Source: [Btrfs mailinglist](https://www.spinics.net/lists/linux-btrfs/msg69099.html), as referenced by Spacedog.
    > 
    > ### Btrfs defragment readonly snapshot
    > 
    > From my trial and error experience, btrfs defragmenting snapshots (to use the new zstd compression) resulted in 100% Exclusive and 0.00 bytes of shared data.
    > 
    > Before `btrfs defragment`:
    > 
    > ```
    > # btrfs filesystem du -s /mnt/btrfs/Backups.backupdb/d2/readonly-snapshot/
    >      Total   Exclusive  Set shared  Filename
    >    1.41GiB     6.27MiB     1.41GiB  /mnt/btrfs/Backups.backupdb/d2/readonly-snapshot/
    > 
    > ```
    > 
    > After `btrfs defragment`:
    > 
    > ```
    > # btrfs filesystem du -s /mnt/btrfs/Backups.backupdb/d2/readonly-snapshot/
    >      Total   Exclusive  Set shared  Filename
    >    1.42GiB     1.42GiB       0.00B  /mnt/btrfs/Backups.backupdb/d2/readonly-snapshot/
    > 
    > ```
    > 
    > ### Shared data goes down to 0.00B


### mount option


- [How to Tune Btrfs Filesystem for Better Performance – The Geek Diary](https://www.thegeekdiary.com/how-to-tune-btrfs-filesystem-for-better-performance/)

    > 1\. Btrfs's performance improves with use of ssd.
    > -------------------------------------------------
    > 
    > Btrfs is SSD-aware and exploits TRIM/Discard to allow the file system to report unused blocks to the storage device for reuse. On SSDs, Btrfs avoids unnecessary seek optimization and aggressively sends writes in clusters, even if they are from unrelated files.
    > 
    > **Note**: You mount with -o ssd to enable the tuning.
    > 
    > 2\. Enable online defragmentaion.
    > ---------------------------------
    > 
    > Btrfs provides a mount option (**-o autodefrag**) that enables an auto-defragmentation helper. When a block is copied and written to disk, the auto-defragmentation helper marks that portion of the file for defragmentation and hands it off to another thread, enabling fragmentation to be reduced automatically in the background. This capability can provide significant benefit to small database workloads, browser caches, and similar workloads. The great thing is that defragmentation can take place while the file system is mounted and actively performing operations.
    > 
    > 3\. Use noatime option instead of relatime.
    > -------------------------------------------
    > 
    > noatime mount option might speed up your file system, especially in case you have lots of snapshots. Each read access to a file is supposed to update its unix access time. COW will happen and will make even more writes. Default is now relatime which updates access times less often.
    > 
    > 4\. Other mount options
    > -----------------------
    > 
    > Below are few other mount option which you can consider with your need and requirements.
    > 
    > -   **space_cache** -- Btrfs stores the free space data ondisk to make the caching of a block group much quicker (Kernel 2.6.37+). It's a persistent change and is safe to boot into old kernels.
    > -   **nodatacow** -- Do not copy-on-write data. datacow is used to ensure the user either has access to the old version of a file, or to the newer version of the file. datacow makes sure we never have partially updated files written to disk. nodatacow gives slight performance boost by directly overwriting data (like ext[234]), at the expense of potentially getting partially updated files on system failures. Performance gain is usually < 5% unless the workload is random writes to large database files, where the difference can become very large
    > -   **compress=zlib** -- Better compression ratio. It's the default and safe for olders kernels.
    > -   **compress=lzo** -- Fastest compression. btrfs-progs 0.19 or olders will fail with this option. The default in the kernel 2.6.39 and newer.
    > -   **autodefrag** -- will detect random writes into existing files and kick off background defragging. It is well suited to bdb or sqlite databases, but not virtualization images or big databases (yet). Once the developers make sure it doesn't defrag files over and over again, they'll move this toward the default. (Kernel 3.0+)
    > -   **inode_cache** -- enable the new free inode cache. This option maybe slowdown your system at first run. (Kernel 3.0+)
    > 

### file copy

- [cp - How to duplicate a file without copying its data with btrfs? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/249772/how-to-duplicate-a-file-without-copying-its-data-with-btrfs)

    > There are two options:
    > 
    > 1.  `cp --reflink=always`
    > 2.  `cp --reflink=auto`
    > 
    > The second is almost always preferable to the first. Using `auto` means it will fallback to doing a true copy if the file system doesn't support reflinking (for instance, ext4 or copying to an NFS share). With the first option, I'm pretty sure it will outright fail and stop copying.
    > 
    > If you are using this as part of a script that needs to be robust in the face of non-ideal conditions, `auto` will serve your better.


### mount image as loop device

- [opensuse - Mounting a btrfs image file - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/219142/mounting-a-btrfs-image-file)


    > Try:
    > 
    > ```
    > losetup /dev/loop0 sda1.img
    > mount /dev/loop0 /mnt
    > 
    > ```
    > 
    > `dd`ing `/dev/sda1` and using gparted against it does not make sense because you have a partition image and not a drive image. `dd`ing `/dev/sda` would be another thing. In that case you should use
    > 
    > ```
    > kpartx -av sda.img
    > 
    > ```
    > 
    > to create the loop devices for the partitions in the disk image and mount like
    > 
    > ```
    > mount /dev/loop0p1 /mnt
    > 
    > ```
    > 
    > ---
    > 
    > You can also force partition table scan with (new enough?) `losetup -P` option. ([man7.org/linux/man-pages/man8/losetup.8.html](http://man7.org/linux/man-pages/man8/losetup.8.html)) -- [XTL](https://unix.stackexchange.com/users/2856/xtl "554 reputation") [Nov 11 '15 at 13:24](https://unix.stackexchange.com/questions/219142/mounting-a-btrfs-image-file#comment415541_219180)
    > 

- [filesystems - Create a file that's treated like a btrfs file system - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/368182/create-a-file-thats-treated-like-a-btrfs-file-system)

    > The loop device is what you need for this. Run these commands as root:
    > 
    > ```
    > truncate -s1G 1GB.img  # Sparse allocation of a 1GB file
    > ld=$(losetup --show --find 1GB.img); echo "$ld"
    > 
    > ```
    > 
    > You will now have a loop device (for example, `/dev/loop0`) that you can treat as a block device.
    > 
    > ```
    > mkfs -t btrfs "$ld"    # Device that was returned from losetup
    > 
    > mkdir -p /mnt/dsk
    > mount "$ld" /mnt/dsk
    > 
    > ```
    > 
    > When you've finished, tidy up again
    > 
    > ```
    > umount /mnt/dsk
    > losetup -d "$ld"
    > rm 1GB.img
    > 
    > ```
    > 
    > If you want to create a partition table on the block device, make sure you always include the `--partscan` flag on the `losetup` command. This will create the associated devices, for example, `/dev/loop0p1`.



### backup

- [btrfs-backup · PyPI](https://pypi.org/project/btrfs-backup/)

    > This project supports incremental backups for *btrfs* using *snapshots* and *send/receive* between filesystems. Think of it as a basic version of Time Machine.


- [Cold storage with Btrfs • JeeLabs](https://jeelabs.org/2017/09/cold-storage-with-btrfs/)

    > ### Getting started
    > 
    > Here are the commands to set this up. Feel free to adapt as needed and season to taste.
    > 
    > Everything below is done as root (use "`sudo -i`" to get a root shell):
    > 
    > Create a RAID1 Btrfs volume of two disks, connected as `/dev/sdb` and `/dev/sdc`:
    > ```shell
    > mkfs.btrfs -f -d raid1 -m raid1 /dev/sdb /dev/sdc
    > ```
    > 
    > Create the mount points:
    > ```shell
    > mkdir /archive /keep
    > ```
    > 
    > Mount the main volume (if it doesn't pick up both drives, run `btrfs device scan`):
    > ```shell
    > mount /dev/sdb /archive
    > ```
    > 
    > Create a subvolume, for snapshotting:
    > ```shell
    > btrfs subvolume create /archive/KEEP
    > ```
    > 
    > Mount that subvolume as well:
    > ```shell
    > mount -o subvol=KEEP /dev/sdb /keep
    > ```
    > 
    > That's it, more or less. You can now place whatever you like on `/keep/`. To create a dated snapshot, use something like:
    > ```shell
    > btrfs subvolume snapshot -r /keep /archive/`date +%Y%m%d-%H%M`
    > ```
    > 
    > One last step is to make all this persistent, i.e. to simplify remounting after a reboot. First, let's label the volume:
    > ```shell
    > btrfs filesystem label /archive KEEP-2T+2T
    > ```
    > Now let's add these lines to "`/etc/fstab`":
    > ```shell
    > LABEL=KEEP-2T+2T  /archive  btrfs  noauto,noatime,user              0 0
    > LABEL=KEEP-2T+2T  /keep     btrfs  noauto,noatime,user,subvol=KEEP  0 0
    > ```
    > 
    > The `noauto` flag prevents the volume from being mounted on startup, and - far more importantly - so it won't break if the drives happen to be disconnected at boot time.
    > 
    > The `noatime` flag disables saving file access times, which improves disk performance (every change, even updating a timestamp, causes COW disk copying).
    > 
    > The `user` flag allows you to mount and unmount these volumes without `sudo`:
    > ```shell
    > mount /keep
    > ...
    > umount /keep
    > ```
    > 
    > You only have to mount the `/archive` area to access or create snapshots. For day-to-day use, "`mount /keep`" is all you'll need.
    > 
    > There's an excellent [17-min video](https://www.youtube.com/watch?v=XwH4N4UEQbs) by Bubba Lichvar, showing how simple Btrfs is to use.
    > 
    > Time will tell how well it performs, but so far I'm *really* pleased with this Btrfs setup. *Safe **and** flexible cold storage - at last!*

    <iframe width="560" height="315" src="https://www.youtube.com/embed/XwH4N4UEQbs" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

- [backup - Btrfs snapshot to non-btrfs disk. Encryption, read acess - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/304889/btrfs-snapshot-to-non-btrfs-disk-encryption-read-acess)

    > I will just add to Gilles' answer by saying that although you may use "`cp`, `rsync`, etc." to transfer your read-only subvolumes / snapshots, you may also send and store the subvolumes as btrfs streams using the `btrfs send` command. [The btrfs Wiki](https://btrfs.wiki.kernel.org/index.php/Incremental_Backup#Initial_Bootstrapping) mentions the following use:
    > 
    > ```
    > # btrfs subvolume snapshot -r / /my/snapshot-YYYY-MM-DD && sync
    > # btrfs send /my/snapshot-YYYY-MM-DD | ssh user@host btrfs receive /my/backups
    > # btrfs subvolume snapshot -r / /my/incremental-snapshot-YYYY-MM-DD && sync
    > # btrfs send -p /my/snapshot-YYYY-MM-DD /my/incremental-snapshot-YYYY-MM-DD |
    >     ssh user@host btrfs receive /backup/home
    > 
    > ```
    > 
    > but you may also just save the streams for future use:
    > 
    > ```
    > # btrfs subvolume snapshot -r / /my/snapshot-YYYY-MM-DD && sync
    > # btrfs send /my/snapshot-YYYY-MM-DD |
    >     ssh user@host 'cat >/backup/home/snapshot-YYYY-MM-DD.btrfs'
    > # btrfs subvolume snapshot -r / /my/incremental-snapshot-YYYY-MM-DD && sync
    > # btrfs send -p /my/snapshot-YYYY-MM-DD /my/incremental-snapshot-YYYY-MM-DD |
    >     ssh user@host 'cat >/backup/home/incremental-snapshot-YYYY-MM-DD.btrfs'
    > 
    > ```
    > 
    > This is useful to store the verbatim btrfs snapshots at arbitrary filesystems. The advantage over, say, `tar` is that `btrfs` snapshots are incremental and only the delta gets sent. The btrfs Wiki claims that this method of incremental backup tends to be even faster than `rsync`.
    > 

- [Incremental Backup - btrfs Wiki](https://btrfs.wiki.kernel.org/index.php/Incremental_Backup)

    > ### Initial Bootstrapping
    > 
    > We will need to create a read-only snapshot of the volume that serves as the reference for the first backup. I will call this subvolume BACKUP. The subvolume is read-only because "btrfs send" requires read-only subvolumes to operate on. **NB**: there is currently an issue that the snapshots to be used with "btrfs send" must be physically on the disk, or you may receive a "stale NFS file handle" error. This is accomplished by "sync" after the snapshot:
    > ```
    >    btrfs subvolume snapshot -r /home /home/BACKUP
    >    sync
    > ```
    > Once created, we can distribute the initial copy into existing directory or subvolume /backup/home. The subvolume appears as /backup/home/BACKUP:
    > ```
    >    btrfs send /home/BACKUP | btrfs receive /backup/home
    > ```
    > Bootstrapping is now done. The subvolume /home/BACKUP is kept around to serve as local reference for the data that has been backed up, and it is needed for constructing the incremental backup for the next step.
    > 
    > ### Incremental Operation
    > 
    > During incremental backup, we make a new snapshot:
    > ```
    >    btrfs subvolume snapshot -r /home /home/BACKUP-new
    >    sync
    > ```
    > We can now send the difference between the old and new backup to the backup volume:
    > ```
    >    btrfs send -p /home/BACKUP /home/BACKUP-new | btrfs receive /backup/home
    > ```
    > Once this command completes, we should have these 4 subvolumes: /home/BACKUP, /home/BACKUP-new, /backup/home/BACKUP and /backup/home/BACKUP-new. We will now need to migrate the new backup as the old one, and do something for the old one. We could keep it around, maybe timestamped with the date of that backup, or just straight out delete it. Here, I am deleting it:
    > ```
    >    btrfs subvolume delete /home/BACKUP
    >    mv /home/BACKUP-new /home/BACKUP
    >    btrfs subvolume delete /backup/home/BACKUP
    >    mv /backup/home/BACKUP-new /backup/home/BACKUP
    > ```
    > But for instance, if you did want to keep a history of backups, perhaps you would snapshot one of the snapshot directories with something like:
    > 
    >    btrfs subvolume snapshot -r /backup/home/BACKUP /backup/home.$(date +%Y-%m-%d)
    > 

- [BTRFS 心得 | richliu's blog](https://blog.richliu.com/2017/01/18/2070/btrfs-%E5%BF%83%E5%BE%97)

    > 首先在講快照之前, 先要提一下 BTRFS 的樹狀架構, 和傳統的檔案系統不太一樣.\
    > BTRFS 比較像是, 建立了 File System 之後, 一個一個 subvolume 切出來使用. 而不是傳統的硬碟有多大就可以用多大. 想像成一個 pool , 可以隨時建立一個新的區塊, 這個區塊可以是 clone 或是全新的參數.
    > 
    > 當一個 BTRFS 用 mkfs.btrfs 建立好之後, 像是一個 pool , 首先最頂級的 volume 目錄是 root, 符號 /, 第一個 subvolume 是 default, 符號 @ .\
    > Ubuntu 預設安裝(我只用過 Ubuntu, 其他的不確定) 會產生二個預設的 subvolume @, @home
    > 
    > 所以看起來就像是這樣
    > ```
    > /dev/sda2
    > +- /
    > +- @
    > +- @home
    > ```
    > 
    > @ 也就是 default subvolume, 第一個 subvolume
    > 
    > 基本的命令, 列出目前 mount 的 btrfs 和相關的訊息
    > ```
    > $ btrfs subvol list /
    > ```
    > 將 /dev/sda2 subvolume @ mount 在 /mnt/disk
    > ```
    > $ mount -o subvol=@ /dev/sda2 /mnt/disk
    > ```
    > 這是一個範例, top level 5 都是 / 下來的第一層 subvolume
    > 
    > 
    > ```shell
    > # btrfs subvol list /
    > ID 257 gen 4383 top level 5 path @
    > ID 258 gen 4388 top level 5 path @home
    > ID 261 gen 4303 top level 5 path 1404
    > ID 289 gen 4297 top level 261 path 1404/1404working
    > ID 290 gen 4364 top level 257 path @/working
    > ID 291 gen 4434 top level 5 path working
    > 
    > ```
    > 
    > 而 1404/1404working 則是指 ID 261 的 clone(snapshot)\
    > @/working 則是指 ID 257 的 clone(snapshot)
    > 
    > 所以有些人問說為什麼不能刪除 top level 5 的 snapshot , 原因就是要 mount -o subvol=/ 之後再用 btrfs subvol delete
    > 
    > 所以如果
    > ```
    > $ mount -o subvol=/ /dev/sda2 /mnt/disk
    > $ btrfs subvolume snapshot /mnt/disk/@ /mnt/disk/working => create snapshot
    > ```
    > working 就會是開在 top level 5
    > 
    > 如果
    > ```
    > $ mount -o subvol=@ /dev/sda2 /mnt/disk
    > $ btrfs subvolume snapshot /mnt/disk/@ /mnt/disk/working => create snapshot
    > ```
    > working 就會是開在 top level 257 (@/working)
    > 
    > 另外講一下 Ubuntu 16.04 可以針對 @ snapshot 之後將 root 開到另一個 subvolume.\
    > 首先修改 grub.d
    > ```
    > vim /etc/grub.d/10_linux
    > ```
    > 找到以下段落, 改成 cat /root/defaultsubvol , 檔名隨你高興\
    > 這一段會取出 /etc/defaultsubvol 內的內容做為 root 的 subvol .
    > 
    > ```bash
    > case x"$GRUB_FS" in
    >     xbtrfs)
    >         rootsubvol="`cat /root/defaultsubvol`"
    >         rootsubvol="${rootsubvol#/}"
    >         if [ "x${rootsubvol}" != x ]; then
    >             GRUB_CMDLINE_LINUX="rootflags=subvol=${rootsubvol} ${GRUB_CMDLINE_LINUX}"
    >         fi;;
    > ```
    > 
    > 所以這樣是切到 working
    > ```shell
    > $ sudo bash -c "echo 'working' >> /root/defaultsubvol"
    > $ sudo update-grub
    > ```
    > 現在可以編輯一下 /boot/grub/grub.conf 產級確認 subvol 都是指向 working
    > 
    > 如果己經在 working 要切到 @ , 比較複雜一點
    > ```shell
    > $ mount -o subvol=@ /mnt/disk
    > $ for i in dev dev/pts sys proc run; do sudo mount --bind /$i /mnt/disk/$i; done
    > $ sudo chroot /mnt/disk bash -c "echo '@' >> /root/defaultsubvol"
    > $ sudo chroot /mnt/disk sudo update-grub
    > $ reboot
    > ```
    > 這樣之後就可以切來切去了\
    > 對於要常常測測從系統重灌設定的人很好用.
    > 



- [Using Btrfs for Easy Backup and Rollback | John Ramsden](https://ramsdenj.com/2016/04/05/using-btrfs-for-easy-backup-and-rollback.html)

    > Installing Linux on Btrfs
    > =========================
    > 
    > During the install process it is definitely clear that Btrfs is not a second-class citizen on Linux. The initial process of getting a system up and running was quite similar to what I am used to with other filesystems. Unlike ZFS having a complicated install process due to having to get the code from an unofficial repository, and deal with kernel modules, Btrfs support is already in the kernel.
    > 
    > ### Setting up Disks for Btrfs
    > 
    > To use the userspace facilities the package [`btrfs-progs`](https://www.archlinux.org/packages/core/x86_64/btrfs-progs/) is needed.
    > 
    > *I did my install on a single ssd but if I wanted to use soft RAID the process would be quite similar and would just involve multiple Btrfs partitions.*
    > 
    > Partition the disk, make the boot partition and a single partition for Btrfs.
    > 
    > ```
    > [root@archiso /] $ lsblk
    > NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    > sdb      8:16   0 238.5G  0 disk
    > ├─sdb1   8:17   0   512M  0 part
    > └─sdb2   8:18   0   238G  0 part
    > ```
    > 
    > Format partitions, I'm using a single disk however multiple disk RAID is as easy as listing multiple devices here.
    > 
    > ```
    > [root@archiso ~] $  mkfs.btrfs -L Butters /dev/sdb2
    > ```
    > 
    > I'm using a UEFI system so I need an additional partition to boot from.
    > 
    > ```
    > [root@archiso ~] mkfs.vfat -F32 /dev/sdb1
    > ```
    > 
    > ### Subvolumes
    > 
    > Subvolumes can be compared to partitions, and although they are not the same, they are used in a similar way to how partitions are used in a regular install.
    > 
    > First mount the Btrfs partition
    > 
    > ```
    > [root@archiso] ~ $ mount -t btrfs /dev/sdb2  /mnt/btrfs
    > ```
    > 
    > Instead of just installing my system to the root of my Btrfs pool I wanted to use subvolumes so that snapshots could be taken. The decision as to how many subvolumes are made is a difficult one. The argument can be made that it is useful to have a separate partition for `var`, `tmp`, and other directories, but for sake of easing the ability of restoring the state of the computer from a snapshot and simplifying backup, I chose to have a single `/` subvolume "`ROOT`", a single `/home` subvolume "`home`" and a subvolume for storing snapshots "`snapshots`".
    > 
    > Create the "`ROOT`", "`home`", and "`snapshots`" subvolumes.
    > 
    > ```
    > [root@archiso /mnt/btrfs] $ btrfs subvolume create /mnt/btrfs/ROOT
    > [root@archiso /mnt/btrfs] $  btrfs subvolume create /mnt/btrfs/home
    > [root@archiso /mnt/btrfs] $  btrfs subvolume create /mnt/btrfs/snapshots
    > ```
    > 
    > Btrfs subvolumes have IDs and parent IDs this lets them keep track of their hierarchy. By default the root node ID is "5". The command `btrfs subvolume list -p ${directory}` shows the three subvolumes, their ID's and their parent ID "5".
    > 
    > ```
    > [root@archiso /mnt/btrfs] $  btrfs subvolume list -p .
    > ID 257 gen 8 parent 5 top level 5 path ROOT
    > ID 258 gen 9 parent 5 top level 5 path home
    > ID 259 gen 10 parent 5 top level 5 path snaps
    > ```
    > 
    > So my hierarchy tree looks like:
    > 
    > ```
    > Butters (ID 5)
    > ├── home
    > ├── ROOT
    > └── snapshots
    > ```
    > 
    > The Btrfs pool at `/mnt/btrfs` can now be unmounted.
    > 
    > ### Install to Subvolumes
    > 
    > In order to install to "`ROOT`" it needs to be mounted in place of the `/` directory. It's important to turn compression on here so that the files are compressed during the install.
    > 
    > Select the subvolume to mount with `subvol=${subvolume}`.
    > 
    > ```
    > [root@archiso /] $ mount -o compress=lzo subvol=ROOT /dev/sdb2 /mnt
    > [root@archiso /] $ mount -o compress=lzo subvol=home /dev/sdb2 /mnt/home
    > [root@archiso /] $ mount /dev/sdb1 /mnt/boot
    > ```
    > 
    > From here on the install is normal until fstab is configured.
    > 
    > ### Configure fstab
    > 
    > Again specify subvolume, mount the Btrfs pool somewhere under `/mnt`.
    > 
    > ```
    > # /etc/fstab: static file system information
    > #
    > # < file system> < dir>   < type>  < options>       < dump>  < pass>
    > # Btrfs pool
    > UUID=${drive-UUID}  /mnt/Butters    btrfs   rw,noatime,discard,ssd,space_cache    0 0
    > 
    > # ROOT
    > UUID=${drive-UUID}  /   btrfs   rw,noatime,ssd,discard,space_cache,subvolid=257,subvol=/ROOT   0 0
    > 
    > # home
    > UUID=${drive-UUID}  /home   btrfs   rw,noatime,ssd,discard,space_cache,subvolid=258,subvol=/home   0 0
    > 
    > # Boot ond other partitions...
    > ```
    > 
    > *NOTE: subvolid may not be necessary and will need to be changed during a rollback*
    > 
    > ### Configure bootloader
    > 
    > Setting up the bootloader is easy with systemd-boot. Similarly to the fstab setup, the "`ROOT`" subvolume needs to be specified.
    > 
    > ```
    > # SYSTEMD-BOOT
    > #  GNU nano 2.5.2             File: /boot/loader/entries/arch.conf                      Modified
    > 
    > title           Arch Linux
    > linux           /vmlinuz-linux
    > initrd          /intel-ucode.img
    > initrd          /initramfs-linux.img         # Intel microcode for if an intel CPU is in use
    > options         root=PARTUUID=68e329cd-01b9-45e7-b516-ba62c516b4e5 rw rootflags=subvol=ROOT
    > ```
    > 
    > Snapshots
    > =========
    > 
    > ### Recurring Snapshots
    > 
    > After finishing up the rest of the install and rebooting, regular snapshots can be setup with [`snapper`](http://snapper.io/), a btrfs snapshot utility made by SUSE which does regular snapshot and cleanup.
    > 
    > This is where the subvolume snapshots can now be made use of.
    > 
    > Under Archlinux, [Snapper is in the Official Repository](https://www.archlinux.org/packages/community/x86_64/snapper/). After installing the package create a default configuration with snapper under `/etc/snapper/configs/`
    > 
    > ```
    > snapper -c ${config-name} create-config ${subvolume-mountpoint}
    > ```
    > 
    > So for subvolumes "`ROOT`" and "`home`", run:
    > 
    > ```
    > snapper -c root create-config /
    > snapper -c home create-config /home
    > ```
    > 
    > This creates a new subvolume "`.snapshots`" at the root of the specified subvolume. Snapper has a utility to help you roll back; however, it is [inherently flawed](https://bbs.archlinux.org/viewtopic.php?id=194491) and can mess up your file system layout due to how it rolls back.
    > 
    > To avoid this issue, delete the new subvolume snapper just made. Instead create a new subvolume under the "`snapshots`" subvolume for whichever subvolumes are being snapshotted by snapper.
    > 
    > Delete snapper subvolumes
    > 
    > ```
    > btrfs subvolume delete /.snapshots
    > btrfs subvolume delete /home/.snapshots
    > ```
    > 
    > Create `snapshots/ROOT_snaps` and `snapshots/home_snaps`.
    > 
    > ```
    > btrfs subvolume create /mnt/Butters/snapshots/ROOT_snaps
    > btrfs subvolume create /mnt/Butters/snapshots/home_snaps
    > ```
    > 
    > Now these subvolumes can be mounted to the mount location snapper expects.
    > 
    > Make the mountpoints as the root user and mount the subvolumes.
    > 
    > ```
    > mkdir /home/.snapshots
    > mkdir /.snapshots
    > ```
    > 
    > ```
    > mount -o compress=lzo subvol=snapshots/home_snaps /dev/sdb2 /home/.snapshots
    > mount -o compress=lzo subvol=snapshots/ROOT_snaps /dev/sdb2 /.snapshots
    > ```
    > 
    > Now that the directories are set up, snapper can be set to run automatic snapshots and clean up. The cleanup removes snapshots based on the config files in `/etc/snapper/configs/` and can be changed.
    > 
    > ```
    > systemctl start snapper-timeline.timer snapper-cleanup.timer
    > systemctl enable snapper-timeline.timer snapper-cleanup.timer
    > ```
    > 
    > The snapper subvolumes should also be added to the fstab
    > 
    > ```
    > # /etc/fstab: static file system information
    > #
    > # <file system> <dir>   <type>  <options>       <dump>  <pass>
    > 
    > # Other drives...
    > 
    > UUID=${drive-UUID}  /.snapshots    btrfs rw,noatime,compress=lzo,ssd,discard,space_cache,subvolid=420,subvol=snapshots/ROOT_snaps   0 0
    > UUID=${drive-UUID}  /home/.snapshots    btrfs rw,noatime,compress=lzo,ssd,discard,space_cache,subvolid=421,subvol=snapshots/home_snaps   0 0
    > ```
    > 
    > ### Rollback Snapshots
    > 
    > To rollback to an old snapshot; boot into a restore medium (like the arch installer) and mount the Btrfs pool.
    > 
    > To rollback "`ROOT`", first delete or move the unwanted subvolume.
    > 
    > ```
    > btrfs subvolume delete /mnt/Butters/ROOT
    > ```
    > 
    > The dates of the snapshot are stored under `${snapshot-number}/info.xml` if the date needs to be checked.
    > 
    > Checking the snapshot info
    > 
    > ```
    > [root@Butters /mnt/Butters]$ cat snapshots/ROOT_snaps/995/info.xml
    > <?xml version="1.0"?>
    > <snapshot>
    >   <type>single</type>
    >   <num>995</num>
    >   <date>2016-04-03 07:00:05</date>
    >   <description>timeline</description>
    >   <cleanup>timeline</cleanup>
    > </snapshot>
    > ```
    > 
    > Snapshots are read only so after selecting the right snapshot, take a read-write snapshot of it under the location of the old subvolume.
    > 
    > ```
    > btrfs subvol snapshot /mnt/Butters/snapshots/ROOT_snaps/${snapshot} /mnt/Butters/ROOT
    > ```
    > 
    > After that the system can be rebooted.
    > 
    > Backups
    > =======
    > 
    > Since snapshots are not backups it's also important a good backup is in place in addition to having snapshots. The backup solution I found is [Btrbk](https://github.com/digint/btrbk), a very configurable backup solution written in perl. Btrbk was an easy install for me as it was in the Arch User Repository, [Btrbk (AUR)](https://aur.archlinux.org/packages/btrbk/). It came with great documentation, as well as systemd timers and services. Btrbk takes snapshots and then backs up the selected snapshot to a variety of backup locations. The snapshots can then be chosen to be kept or deleted based on a set amount of time.
    > 
    > ### Backup Configuration
    > 
    > After installing Btrbk, an example configuration file can be found at `/etc/btrbk/btrbk.conf.example`. Copy the example config to `/etc/btrbk/btrbk.conf`.
    > 
    > The configuration options I changed were
    > 
    > 1.  `snapshot_dir` - The location for the initial snapshot, if left as default it will make the snapshot in the "volume" directory.
    > 2.  `volume` - The pool that the subvolume being backed up is in.
    > 3.  `subvolume` - The subvolume that is going to be backed up.
    > 4.  `target` - Location where the backup will be placed.
    > 5.  `snapshot_preserve_daily, snapshot_preserve_weekly, snapshot_preserve_monthly` - Amount of time to keep snapshots. I already keep snapshots from snapper so I set all my snapshot preserve settings to zero.
    > 6.  `target_preserve_daily, target_preserve_weekly, target_preserve_monthly` - Amount of time to keep backups.
    > 
    > For a basic backup everything else can be left as default.
    > 
    > I chose to create a new subvolume under `snapshots/btrbk_snaps` to keep things organized; however, there should only ever be one snapshot here so this is not really necessary.
    > 
    > Options correspond to the last section encountered so global options must be set before each volume.
    > 
    > My basic configuration ended up as
    > 
    > ```
    > snapshot_preserve_daily    0
    > snapshot_preserve_weekly   0
    > snapshot_preserve_monthly  0
    > 
    > target_preserve_daily      20
    > target_preserve_weekly     10
    > target_preserve_monthly    all
    > 
    > snapshot_dir               snapshots/btrbk_snaps
    > 
    > volume /mnt/Butters
    >   subvolume ROOT
    >     target send-receive    /mnt/ButterBackup/ROOT
    > 
    >   subvolume home
    >     target send-receive    /mnt/ButterBackup/home
    > ```
    > 
    > *Note: Indentation in the config is for readability purposes only , it does not change the results.*
    > 
    > This configuration is for sending backups somewhere else on the same system, in my case to another drive, but it can easily be configured to send backups over SSH to another computer or server.
    > 
    > ### Directory Structure
    > 
    > So this is what my directory structure ended up looking like
    > 
    > ```
    > .
    > ├── ButterBackup [POOL ONE]
    > |   ├── home
    > |   |   └── (btrbk home pool backups...)
    > |   └── ROOT
    > |       └── (btrbk ROOT pool backups...)
    > |
    > └──── Butters [POOL TWO]
    >     ├── home
    >     │   └── (home directories...)
    >     ├── ROOT
    >     │   └── (root directories...)
    >     └── snapshots
    >         ├── btrbk_snaps
    >         |   ├── (btrbk home pool backups...)
    >         |   └── (btrbk ROOT pool backups...)
    >         ├── home_snaps
    >         |   └── (Snapper home pool snapshots....)
    >         └── ROOT_snaps
    >             └── (Snapper ROOT pool snapshots....)
    > ```

### get UUID

- [btrfs incremental snapshots: find UUID in sent data - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/421163/btrfs-incremental-snapshots-find-uuid-in-sent-data)

    > starting from the code from [btrfs-snapshots-diff.py [github.com]](https://github.com/sysnux/btrfs-snapshots-diff/blob/master/btrfs-snapshots-diff.py) is was able to make a script tailored to my needs. i can use it this way to get the `uuid`s:
    > 
    > ```python
    > with BtrfsStream('snapshot_0-1.data') as btrfs_stream:
    >     print(btrfs_stream.get_send_command())
    > # ('BTRFS_SEND_C_SNAPSHOT',
    > #      (UUID('01234567-89ab-cdef-0123-456789abcdef'),
    > #       UUID('fedcba98-7654-3210-fedc-ba9876543210')))
    > 
    > ```
    > 
    > with the class `BtrfsStream` as below.
    > 
    > i made some modifications to the original code:
    > 
    > -   python 3 (instead of python 2)
    > -   iterating over the file instead of reading all of it into the memory
    > -   added `contextmanager` features in order to use it in a `with` satement
    > 
    > the code is used is then:
    > 
    > ```python
    > from struct import unpack
    > import io
    > from uuid import UUID
    > 
    > class BtrfsStream:
    > 
    >     # From btrfs/send.h
    >     send_cmds = (
    >         'BTRFS_SEND_C_UNSPEC BTRFS_SEND_C_SUBVOL BTRFS_SEND_C_SNAPSHOT '
    >         'BTRFS_SEND_C_MKFILE BTRFS_SEND_C_MKDIR BTRFS_SEND_C_MKNOD '
    >         'BTRFS_SEND_C_MKFIFO BTRFS_SEND_C_MKSOCK BTRFS_SEND_C_SYMLINK '
    >         'BTRFS_SEND_C_RENAME BTRFS_SEND_C_LINK BTRFS_SEND_C_UNLINK '
    >         'BTRFS_SEND_C_RMDIR BTRFS_SEND_C_SET_XATTR BTRFS_SEND_C_REMOVE_XATTR '
    >         'BTRFS_SEND_C_WRITE BTRFS_SEND_C_CLONE BTRFS_SEND_C_TRUNCATE '
    >         'BTRFS_SEND_C_CHMOD BTRFS_SEND_C_CHOWN BTRFS_SEND_C_UTIMES '
    >         'BTRFS_SEND_C_END BTRFS_SEND_C_UPDATE_EXTENT').split()
    > 
    >     send_attrs = (
    >         'BTRFS_SEND_A_UNSPEC BTRFS_SEND_A_UUID BTRFS_SEND_A_CTRANSID '
    >         'BTRFS_SEND_A_INO BTRFS_SEND_A_SIZE BTRFS_SEND_A_MODE '
    >         'BTRFS_SEND_A_UID BTRFS_SEND_A_GID BTRFS_SEND_A_RDEV '
    >         'BTRFS_SEND_A_CTIME BTRFS_SEND_A_MTIME BTRFS_SEND_A_ATIME '
    >         'BTRFS_SEND_A_OTIME BTRFS_SEND_A_XATTR_NAME '
    >         'BTRFS_SEND_A_XATTR_DATA BTRFS_SEND_A_PATH BTRFS_SEND_A_PATH_TO '
    >         'BTRFS_SEND_A_PATH_LINK BTRFS_SEND_A_FILE_OFFSET BTRFS_SEND_A_DATA '
    >         'BTRFS_SEND_A_CLONE_UUID BTRFS_SEND_A_CLONE_CTRANSID '
    >         'BTRFS_SEND_A_CLONE_PATH BTRFS_SEND_A_CLONE_OFFSET '
    >         'BTRFS_SEND_A_CLONE_LEN').split()
    > 
    >     # From btrfs/ioctl.h:#define BTRFS_UUID_SIZE 16
    >     BTRFS_UUID_SIZE = 16
    >     HEADER_SIZE = 17
    > 
    >     # Headers length
    >     l_head = 10
    >     l_tlv = 4
    > 
    >     def __init__(self, path):
    >         '''
    >         '''
    > 
    >         self.path = path
    >         self._stream = None
    > 
    >     def __enter__(self):
    >         '''
    >         enter for context manager
    >         '''
    > 
    >         self._stream = open(self.path, 'rb')
    >         self._read_header()
    >         return self
    > 
    >     def __exit__(self, exc_type, exc_val, exc_tb):
    >         '''
    >         exit for context manager
    >         '''
    > 
    >         self._stream.close()
    > 
    >     def _read_header(self):
    >         '''
    >         read the header
    >         '''
    > 
    >         header = self.read(BtrfsStream.HEADER_SIZE, assert_lengh=False)
    > 
    >         if len(header) < BtrfsStream.HEADER_SIZE:
    >             raise IOError('Invalid stream length\n')
    > 
    >         magic, null, self.version = unpack('<12scI', header)
    >         if magic != b'btrfs-stream':
    >             raise IOError('Not a Btrfs stream!')
    > 
    >     def seek(self, offset, whence=io.SEEK_SET):
    >         '''
    >         seek to a given point
    >         '''
    > 
    >         self._stream.seek(offset)
    > 
    >     def tell(self):
    >         '''
    >         tell where we are
    >         '''
    > 
    >         return self._stream.tell()
    > 
    >     def read(self, n_bytes, assert_lengh=True):
    >         '''
    >         try to read n_bytes
    >         '''
    > 
    >         tell_before = self.tell()
    >         btes = self._stream.read(n_bytes)
    > 
    >         if assert_lengh is True and len(btes) != n_bytes:
    >             msg = ('could only read {} instead of {} at offset {}'
    >                    ).format(len(btes), n_bytes, tell_before)
    >             raise IOError(msg)
    >         return btes
    > 
    >     def tlv_get(self, attr_type):
    >         attr, l_attr = unpack('<HH', self.read(BtrfsStream.l_tlv))
    >         if self.send_attrs[attr] != attr_type:
    >             raise ValueError('Unexpected attribute %s' % self.send_attrs[attr])
    >         ret, = unpack('<H', self.read(2))
    >         return ret
    > 
    >     def _tlv_get_string(self, attr_type):
    >         attr, l_attr = unpack('<HH', self.read(BtrfsStream.l_tlv))
    >         if self.send_attrs[attr] != attr_type:
    >             raise ValueError('Unexpected attribute %s' % self.send_attrs[attr])
    >         ret, = unpack('<%ds' % l_attr, self.read(l_attr))
    >         return ret
    > 
    >     def _tlv_get_u64(self, attr_type):
    >         attr, l_attr = unpack('<HH', self.read(BtrfsStream.l_tlv))
    >         if self.send_attrs[attr] != attr_type:
    >             raise ValueError('Unexpected attribute %s' % self.send_attrs[attr])
    >         ret, = unpack('<Q', self.read(l_attr))
    >         return ret
    > 
    >     def _tlv_get_uuid(self, attr_type):
    >         attr, l_attr = unpack('<HH', self.read(BtrfsStream.l_tlv))
    >         if self.send_attrs[attr] != attr_type:
    >             raise ValueError('Unexpected attribute %s' % self.send_attrs[attr])
    >         return UUID(bytes=self.read(l_attr))
    > 
    >     def get_send_command(self):
    >         '''
    >         search uuids only.
    >         '''
    >         # start at the right point in the file
    >         self.seek(BtrfsStream.HEADER_SIZE)
    > 
    >         while True:
    > 
    >             l_cmd, cmd, crc = unpack('<IHI', self.read(BtrfsStream.l_head))
    >             tell_before_cmd = self.tell()
    > 
    >             try:
    >                 command = self.send_cmds[cmd]
    >             except:
    >                 raise ValueError('Unkown command %d' % cmd)
    > 
    >             if command == 'BTRFS_SEND_C_SNAPSHOT':
    >                 self._tlv_get_string('BTRFS_SEND_A_PATH')
    >                 uuid = self._tlv_get_uuid('BTRFS_SEND_A_UUID')
    >                 self._tlv_get_u64('BTRFS_SEND_A_CTRANSID')
    >                 clone_uuid = self._tlv_get_uuid('BTRFS_SEND_A_CLONE_UUID')
    >                 return 'BTRFS_SEND_C_SNAPSHOT', (uuid, clone_uuid)
    > 
    >             elif command == 'BTRFS_SEND_C_SUBVOL':
    >                 self._tlv_get_string('BTRFS_SEND_A_PATH')
    >                 uuid = self._tlv_get_uuid('BTRFS_SEND_A_UUID')
    >                 return 'BTRFS_SEND_C_SUBVOL', (uuid, )
    > 
    >             elif command == 'BTRFS_SEND_C_CLONE':
    >                 self._tlv_get_string('BTRFS_SEND_A_PATH')
    >                 self._tlv_get_u64('BTRFS_SEND_A_FILE_OFFSET')
    >                 self._tlv_get_u64('BTRFS_SEND_A_CLONE_LEN')
    >                 clone_uuid = self._tlv_get_uuid('BTRFS_SEND_A_CLONE_UUID')
    >                 return 'BTRFS_SEND_C_CLONE', (clone_uuid, )
    > 
    >             elif command == 'BTRFS_SEND_C_END':
    >                 return
    > 
    >             self.seek(tell_before_cmd + l_cmd)
    > 
    > ```
    > 


### change UUID

- [Modifying a BTRFS filesystem UUID - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/104067/modifying-a-btrfs-filesystem-uuid)

    > With the program `btrfstune`, which is part of more recent versions of the normal btrfs-tools, the UUID of a offline file system can be changed. If the partition is eg. `/dev/sda1`, use following command to generate a new, random UUID:
    > 
    > ```
    > btrfstune -u /dev/sda1
    > 
    > ```
    > 
    > To specify which value should be used, use an uppercase `-U` followed by a (valid) UUID string, for example:
    > 
    > ```
    > sudo btrfstune -U e0c5b943-1c02-44a2-bbaf-87ebda5e363b /dev/sdaX
    > 
    > ```
    > 


### Exclude hidden directories from subvolume/snapshot

- [btrfs - Exclude hidden directories from subvolume/snapshot - Ask Ubuntu](https://askubuntu.com/questions/421759/exclude-hidden-directories-from-subvolume-snapshot)

    > Dot-files have no special meaning to the filesystem, and `btrfs send` cannot currently (Feb 2014) exclude files or directories from the target subvolume.
    > 
    > However, `btrfs subvolume snapshot` does exclude subvolumes which are contained in the target subvolume (it creates empty directories in the snapshot), so
    > 
    > -   You may replace the directories that you want to exclude with subvolumes.
    > 

- [backup - btrfs - snapshot of a parent subvolume excludes child subvolumes? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/208063/btrfs-snapshot-of-a-parent-subvolume-excludes-child-subvolumes)

    > > Taking snapshots of a subvolume is not a recursive process. If you create a snapshot of a subvolume, every subvolume or snapshot that the subvolume contains is mapped to an empty directory of the same name inside the snapshot. (from <https://docs.oracle.com/cd/E37670_01/E37355/html/ol_use_case3_btrfs.html>)
    > 
    > If your layout fits, making snapshots of subvolumes that you want will naturally exclude subvolumes that you don't want snapshots of. Snapshots are not backups, but this does effectively exclude the logfiles from the snapshot. If you take a backup from the snapshot, the logfiles should also get excluded from the backups.
    > 





### delete a btrfs subvolume

- [(RESOLVED) Why i cannot delete the subvolume of BTRFS? / Newbie Corner / Arch Linux Forums](https://bbs.archlinux.org/viewtopic.php?id=227026)

    > After entering the command **btrfs subvolume list /mnt**
    > 
    > ```sh
    > # btrfs subvolume list /mnt
    > ID 257 gen 1412 top level 5 path root_bad
    > ID 258 gen 2745 top level 5 path home
    > ID 260 gen 1381 top level 257 path root_bad/var/lib/machines
    > ID 262 gen 1399 top level 5 path Only_YADRO
    > ID 263 gen 2745 top level 5 path root
    > ID 272 gen 1416 top level 5 path i3
    > ```
    > 
    > I saw that subvolume with ID 260 belong subvolume with ID 257 and if i will delete subvolume "machines" and after i will can easily delete subvolume "root_bad". DONE, THANKS!!!

### delete a btrfs snapshot

- [4.12.10 Deleting Snapshots of the root File System](https://docs.oracle.com/cd/E37670_01/E37355/html/ol_delsnp_btrfs.html)
    
    > To delete a snapshot:
    > 
    > 1.  Mount the top level of the file system, for example:
    >     ```
    >     # mount -o subvolid=5 /dev/mapper/vg_btrfs-lv_root /mnt
    >     ```
    > 2.  Change directory to the mount point and delete the snapshot.
    >     ```
    >     # cd /mnt
    >     # btrfs subvolume delete install
    >     
    >     Delete subvolume '/mnt/install'
    >     ```
    >     
    > 3.  Change directory to `/` and unmount the top level of the file system.
    >     ```
    >     # cd /
    >     # umount /mnt
    >     ```
    >     
    >     The list of subvolumes now does not include `install`.
    >     ```
    >     # btrfs subvolume list /
    >     ID 260 top level 5 path root_snapshot_1
    >     ```

- [Can't delete a btrfs snapshot - Ask Ubuntu](https://askubuntu.com/questions/441375/cant-delete-a-btrfs-snapshot)

    > Edit3: Solution
    > 
    > ```sh
    > root@cioco:~# mount /dev/sda2 /btrfs-root/
    > root@cioco:~# ls -l /btrfs-root/
    > total 0
    > drwxr-xr-x 1 root root 262 Apr  1 08:31 @
    > drwxr-xr-x 1 root root 230 Oct 16 22:53 @apt-snapshot-release-upgrade-saucy-2013-10-19_00:52:26
    > drwxr-xr-x 1 root root   6 Oct 16 22:13 @home
    > root@cioco:~# btrfs subvolume delete /btrfs-root/@apt-snapshot-release-upgrade-saucy-2013-10-19_00\:52\:26/
    > Delete subvolume '/btrfs-root/@apt-snapshot-release-upgrade-saucy-2013-10-19_00:52:26'
    > root@cioco:~# dmesg
    > [41113.537617] device label cioco-root devid 1 transid 337615 /dev/sda2
    > 
    > ```
    > 
    > ---
    > 
    > The snapshot exists in the real root of the filesystem, which is not what you have mounted in /. You have the /@ subvolume mounted in /, so there is no such file with that name. You have to mount the real root volume somewhere and use that path to reference the snapshot.
    > 
    > Or you can use apt-btrfs-snapshot delete instead.
    > 
    > ---
    > 
    > apt-btrfs-snapshot is just an apt script that automatically runs the normal btrfs snapshot any time you have apt install/upgrade/remove packages.
    > 


- [How can I delete a apt-btrfs-snapshot when the error is "Directory not empty?" - Super User](https://superuser.com/questions/633219/how-can-i-delete-a-apt-btrfs-snapshot-when-the-error-is-directory-not-empty)

    > Problem was there was a subvolume within a subvolume. You need to delete all inner subvols before deleting containing vol.
    > ```sh
    > btrfs subvol delete /tmp/foo/@apt-snapshot-2013-04-XX_1X:3X:XX/@ 
    > btrfs subvol delete /tmp/foo/@apt-snapshot-2013-04-XX_1X:3X:XX
    > ```

## Snapper with Btrfs

### create automated btrfs snapshots with snapper

- [How to create automated btrfs snapshots with snapper - TechRepublic](https://www.techrepublic.com/article/how-to-create-automated-btrfs-snapshots-with-snapper/)

    > Installing snapper
    > ------------------
    > 
    > Because snapper can be found in the standard repositories, there is only one command necessary for installation:
    > 
    > *`sudo apt-get install snapper`*
    > 
    > You now have the necessary tools to create scheduled btrfs snapshots.
    > 
    > Creating the config file
    > ------------------------
    > 
    > The first step is to create a config file for your subvolume. You have to create a config file for every subvolume you want backed up; in other words, if you have multiple sub-volumes, you'll have to do this for each one.
    > 
    > To create the config file, run the snapper command like so:
    > 
    > 1.  Open a terminal window.
    > 2.  Gain administrative access with the command *`sudo su`.*
    > 3.  Issue the command *`snapper -c CONFIG create-config /PATH/TO/SUBVOLUME`.*
    > 
    > *`CONFIG`* will be the name of the new configuration file, and *`/PATH/TO/SUBVOLUME`* is the actual path to your subvolume. You need to issue this command for every subvolume that requires automatic snapshotting.
    > 
    > The above command will create a configuration file based on the included template *`/etc/snapper/config-templates/default`*. You can create your own templates, save them in the same directory, and base a new snapshot on the custom template by following these steps.
    > 
    > 1.  Open a terminal window.
    > 2.  Gain administrative access with the command *`sudo su`.*
    > 3.  Issue the command *`snapper -c CONFIG create-config -t CUSTOM_DEFAULTS /PATH/TO/SUBVOLUME`.*
    > 
    > *`CONFIG`* will be the name of the new configuration file, *`CUSTOM_DEFAULTS`* is the name of your new template, and *`/PATH/TO/SUBVOLUME`* is the actual path to the btrfs subvolume.
    > 
    > Edit your config file
    > ---------------------
    > 
    > The snapper config files are in *`/etc/snapper/configs`*. There are a number of options that can be customized within that file, but there is only one line that must be configured for hourly snapshots. Within the config file, you'll see this line:
    > 
    > *`TIMELINE_CREATE="yes"`*
    > 
    > When that option is set to "yes," it will create hourly snapshots for your subvolume. This will kick off as soon as you issue the snapper command to create the config file. If you want to check to see if your hourly snapshot has been created, issue the command (making sure to have administrator access) *`snapper -c CONFIG list`* (`CONFIG` is the name of the configuration file). When you issue the command, you'll see how many snapshots have been taken, the time they were taken, and a few more bits of information (**Figure A**).
    > 
    > **Figure A**
    > 
    > ![Figure A](https://tr4.cbsistatic.com/hub/i/2016/08/23/9b6f1346-c6c5-408e-9f9b-ce52f282bd2e/snappera.jpg)
    > 
    > Image: Jack Wallen
    > 
    > ###### The config snapshot been taken twice, and the sub2 snapshot has run once.
    > 
    > Each snapshot is retained within a hidden directory inside of the subvolume. So, if you create a snapshot for sub2, the snapshot will be found in sub2/.snapshots.
    > 
    > Reverting to a snapshot
    > -----------------------
    > 
    > Unfortunately, the snapper tool does not have the ability to revert a current subvolume to a snapshot. In order to do that, you have to manually copy that snapshot in place of the subvolume.
    > 
    > This is working only on an external data drive---the process for rolling back a snapshot on a running environment is quite different, and we'll address that process in an upcoming post.


### pre/post diff snapshot

- [21.7.1 Using snapper with Btrfs Subvolumes](https://docs.oracle.com/cd/E52668_01/E54669/html/ol7-snapper-btrfs.html#)

    > There are three types of snapshot that you can create using **snapper**:
    > 
    > `post`
    > 
    > You use a *post snapshot* to record the state of a subvolume after a modification. A post snapshot should always be paired with a *pre snapshot* that you take immediately before you make the modification.
    > 
    > `pre`
    > 
    > You use a *pre snapshot* to record the state of a subvolume before a modification. A pre snapshot should always be paired with a *post snapshot* that you take immediately after you have completed the modification.
    > 
    > `single`
    > 
    > You can use a single snapshot to record the state of a subvolume but it does not have any association with other snapshots of the subvolume.
    > 
    > For example, the following commands create pre and post snapshots of a subvolume:
    > 
    > ```
    > # snapper -c config_name create -t pre -p
    > N
    > ... Modify the subvolume's contents...
    > # snapper -c config_name create -t post --pre-num N -p
    > N'
    > ```
    > 
    > The **-p** option causes **snapper** to display the number of the snapshot so that you can reference it when you create the post snapshot or when you compare the contents of the pre and post snapshots.
    > 
    > To display the files and directories that have been added, removed, or modified between the pre and post snapshots, use the **status** subcommand:
    > ```
    > # snapper -c config_name status N..N'
    > ```
    > 
    > To display the differences between the contents of the files in the pre and post snapshots, use the **diff** subcommand:
    > ```
    > # snapper -c config_name diff N..N'
    > ```
    > 
    > To list the snapshots that exist for a subvolume:
    > ```
    > # snapper -c config_name list
    > ```
    > 
    > To delete a snapshot, specify its number to the **delete** subcommand:
    > ```
    > # snapper -c config_name delete N'
    > ```
    > 
    > To undo the changes in the subvolume from post snapshot *`N'`* to pre snapshot *`N`*:
    > ```
    > # snapper -c config_name undochange N..N'
    > ```

### snapper config settings

- [用 snapper 轻松玩转 Btrfs 的快照功能_Linux教程_Linux公社-Linux系统门户网站](https://www.linuxidc.com/Linux/2018-01/150112.htm)

    > #### 5.6 快照文件的管理
    > 
    > 由 snapper 所产生的快照默认存储在子卷下面的 `.snapshots` 目录中。我们来看一下它的结构：
    > 
    > ```
    > /mnt/btrfs/.snapshots/
    > ├── 1   # 快照 1 目录
    > │   ├── info.xml    # 快照基本信息
    > │   └── snapshot    # 快照内容
    > │       └── 1.txt
    > └── 2   # 快照 2 目录
    >     ├── filelist-1.txt  # 快照差异比较结果
    >     ├── info.xml    # 快照基本信息
    >     └── snapshot    # 快照内容
    >         ├── 1.txt
    >         └── 2.txt
    > 
    > ```
    > 
    > 可以看到，每个快照的基本信息和内容都在其对应编号的目录中，子目录 `snapshot` 的内容就是拍摄快照时子卷的所有内容。
    > 
    > 快照文件默认是只读的，而且只有 root 可以访问。如果需要恢复单一文件，可以把快照里面的内容用 `cp` 命令拷贝回来。
    > 
    > 由于 Btrfs 文件系统具有写时复制的特性，所以如果文件系统中的文件没有经常被替换，快照占用的空间是非常小的。
    > 
    >
    > #### 6.3 修改快照自动清理的参数
    > 
    > 配置文件位置：`/etc/snapper/configs/<配置名称>`。
    > 
    > 常用字段及对应的功能如下：
    > 
    > | 字段名                 | 功能                                         |
    > |------------------------|----------------------------------------------|
    > | NUMBER_CLEANUP         | 开启 number（基于数量） 的清理算法           |
    > | NUMBER_LIMIT           | 最大快照数量                                 |
    > | TIMELINE_CLEANUP       | 开启 timeline（基于时间） 的清理算法         |
    > | TIMELINE_LIMIT_HOURLY  | 每小时快照的保留数目                         |
    > | TIMELINE_LIMIT_DAILY   | 每天快照的保留数目                           |
    > | TIMELINE_LIMIT_WEEKLY  | 每周快照的保留数目                           |
    > | TIMELINE_LIMIT_MONTHLY | 每月快照的保留数目                           |
    > | TIMELINE_LIMIT_YEARLY  | 每年快照的保留数目                           |
    > | EMPTY_PRE_POST_CLEANUP | 开启 empty-pre-post（基于快照对） 的清理算法 |
    > | EMPTY_PRE_POST_CLEANUP | 开启自动清理无变化快照对                     |
    > 




### snapper-gui and apt-btrfs-snapper

- [BTRFS auto snapshots on ubuntu - HackMD](https://hackmd.io/s/S1FqjrEgZ#)


    > Installation
    > ------------
    > 
    > ### snapper
    > 
    > ```
    > # apt install snapper
    > 
    > ```
    > 
    > after installation, you need to create initial configuration for root partition
    > 
    > ```
    > # snapper create-config /
    > 
    > ```
    > 
    > ### snapper-gui
    > 
    > install from [git repository](https://github.com/ricardomv/snapper-gui):
    > 
    > ```
    > $ git clone https://github.com/ricardo-vieira/snapper-gui/
    > $ cd snapper-gui/
    > # python3 setup.py install
    > 
    > ```
    > 
    > ### apt-btrfs-snapper
    > 
    > install from [git repository](https://github.com/agronick/apt-btrfs-snapper):
    > 
    > ```
    > $ git clone https://github.com/agronick/apt-btrfs-snapper/
    > $ cd apt-btrfs-snapper/
    > # python3 setup.py install
    > 
    > ```
    > 
    > ---
    > 
    > Usage
    > -----
    > 
    > ### snapper
    > 
    > a CLI utility for snapshots management. it can list, create, restore, delete snapshots as well as show diff between them.
    > 
    > it is encouraged to read [this tutorial](http://snapper.io/tutorial.html).
    > 
    > #### config
    > 
    > you **need** to create a subvolume configuration for your BTRFS partition(s). there must be at least one - root subvolume:
    > 
    > ```
    > # snapper create-config /
    > 
    > ```
    > 
    > #### create snapshot
    > 
    > ```
    > # snapper create --description "before changes"
    > 
    > ```
    > 
    > #### list snapshots
    > 
    > ```
    > # snapper list
    > 
    > ```
    > 
    > #### diff snapshots
    > 
    > ```
    > # snapper diff 2..3
    > 
    > ```
    > 
    > 2 and 3 are snapshot numbers as shown in the *list* command
    > 
    > #### restore snapshot
    > 
    > ```
    > # snapper undochange 2..3
    > 
    > ```
    > 
    > 2 and 3 are snapshot numbers as shown in the *list* command
    > 
    > ### snapper-gui
    > 
    > a GUI utility in which you can conveniently list snapshots, diffs and configs as well as create them.
    > 
    > ### apt-btrfs-snapper
    > 
    > a CLI utility and a daemon, which hooks into *apt* actions. it automatically creates two snapshots before and after every apt install, update and remove action.
    > 
    > it also has convenient 'shortcut' commmands for creating and restoring snapshots as well as deleting snapshots older than X days.
    > 
    > ```
    > # apt-btrfs-snapper
    > 
    > ```
    > 
    > 


### snapshot performance issue

- [Snapper plus BTRFS : Fedora](https://www.reddit.com/r/Fedora/comments/8eub1m/snapper_plus_btrfs/)

    > Snapshots easily result in a lot of disk space being consumed. You delete a file, but free space doesn't increase because a snapshot still has that file in it. On the root partition this can apply to stuff like downloaded packages in /var.
    > 
    > So suppose you want to clean this up. Turns out, a couple dozen snapshots on BTRFS results in absolutely horrible performance when trying to remove one. Deleting one locked up my laptop for about an hour, and that's with a SSD. It took me about a day to go through 20-ish snapshots that had accumulated. Fortunately, the more you remove, the faster it gets. The worst thing isn't that it's slow, but that you can't do anything useful while a snapshot is being removed.
    > 
    > My company tried using btrfs snapshots for managing large package archive, where a snapshot was taken per release. The people working on that reported that performance was dreadful as well.
    > 
    > TL;DR: A snapshot or two is probably fine, but let them accumulate and it can lead to a lot of annoyance.

- [Snapper and Btrfs for dummies? : openSUSE](https://www.reddit.com/r/openSUSE/comments/904fmp/snapper_and_btrfs_for_dummies/)

    > i am no expert but if i understood correctly..
    > 
    > 1.  deleting snapshots does not free space right away
    > 
    > 2.  the space used by snapshots can not be reported correctly by df -h or other tools. so maybe my root was not full after all.
    > 
    > ---
    > 
    > Yeah, it's not instant. You have to wait for `snapperd` and `btrfs-cleaner` to finish before you check your free space again.



### Fedora BTRFS+Snapper System setup

- [Fedora BTRFS+Snapper PART 1: System Preparation](https://dustymabe.com/2015/07/14/fedora-btrfssnapper-part-1-system-preparation/)

- [Fedora BTRFS+Snapper PART 2: Full System Snapshot/Rollback](https://dustymabe.com/2015/07/19/fedora-btrfssnapper-part-2-full-system-snapshotrollback/)

- [Fedora BTRFS+Snapper - The Fedora 27 Edition](https://dustymabe.com/2017/12/17/fedora-btrfssnapper-the-fedora-27-edition/)



## Boom: boot to snapshot

- [bmr-cymru/boom: Boom Boot Manager](https://github.com/bmr-cymru/boom)

    > Boom allows for flexible boot configuration and simplifies the creation of new or modified boot entries: for example to boot snapshot images of the system created using LVM2 or BTRFS.




