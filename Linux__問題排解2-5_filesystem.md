# Linux__問題排解2-5_filesystem

[toc]
<!-- toc --> 


# ZFS

## ZFS vs BtrFS

- [ZFS vs BtrFS - 網路儲存裝置 - 電腦討論區 - Mobile01](https://www.mobile01.com/topicdetail.php?f=494&t=4683363)

    > 簡單的說
    > ZFS 適合大型的 storage, 而 BtrFS 只適合 1~4 個 HD 的 storage. (目前不建議 RAID5/6) 除非使用 kernel 4.2 的版本 (就目前使用 4.2 kernel的比例是不到 5%, 而且所有市面上的NAS 都還在使用 3.19以下的 Kernel)
    > 
    > 原因如下:
    > BtrFS 只能支援 RAID 1, 1+0, 5 & 6, 其中 Raid 5&6 還算是 Alpha 階段, 下面是 btrfs 官網的說明:
    > 
    > "Parity RAID appeared in 3.9, and was considered experimental until 3.19, when recovery code to deal with bitrot/checksum errors was introduced. See RAID56 for more details. " **experimental = alpha.
    > 
    > BtrFS 強過 ZFS 的地方
    > 
    > 1. BtrFS 可以輕鬆擴充 HD 以及容量, 譬如使用 3TB 的RAID1, 可以輕鬆的擴充到 6TB的RAID1, 而 ZFS 的 vDEV 模式並不適合更換硬碟擴充, 光是要 resilver 的時間就太誇張了, ZFS 是採取增加新的 vDEV (但是舊的 vDEV 是無法移除). 以實際面來說, 如果是大型的 storage 伺服器, 碰到儲存空間不夠時, 大部分的做法是買一台新的來慢慢做資料移轉 (或是舊的成為 second storage, 而新的成為 primary storage 使用), 比較少 storage administrator 心臟夠大顆, 來玩 storage server 的 live migration 擴充 (因為在 rebuild/resiliver 過程是資料 hd 最危險的時候), 但是以家用的 NAS, RAID 1 可以擴充, 或是從 RAID1 變成 RAID5 是很方便以及經濟的模式, 但是以企業的角度來說, 風險還是太大了.
    > 
    > 2. 未來性. btrFS 未來一片光明, 太多大廠全力投入 btrFS 的開發讓它更完整, 穩定以及強大, 相對來說 ZFS 的邪惡繼父 Oracle 很糟糕, 再來就是收留 ZFS 的孤兒院 OpenZFS fundation 目前還沒有閃亮的人才如 bitcoin 的 Satoshi Nakamoto 可以給 ZFS 一個光明的未來在開源軟體群組中發展.
    > 
    > <br>
    > ZFS 強過 BtrFS 的地方
    > 
    > 1. 效能. ZFS 可以使用 SSD cache 但是 btrFS 的 bcache (插件) 目前還是 alpha 階段, 同時官網目前註明這部分是 btrFS 目前需要重點發展的地方 (細節 <https://bcache.evilpiepirate.org/>) 目前是無人負責這個項目, 從官網的角度 <https://btrfs.wiki.kernel.org/index.php/Project_ideas#dm_cache_or_bcache_like_cache_e.g._on_a_SSD>
    > 
    > 2. 壓縮. ZFS 支援 LZ4 壓縮, 這是非常重要的功能, 因為它搭配上 zfs 的 ssd cache 後, 間接把所有的 random write 都變成了 sequential write, 所以也造成 zfs 寫入速度非常快.
    > 
    > 3. 大容量, 適合8顆以上 HD 的 storage, 而且越多顆效能越快, 其 raidZ3(raid7) 或是多個 raid1+0 組合模式, 可以讓 storage administrator 在效能, 容量空間, 以及 穩定安全性抉擇一個最好的平衡模式. 譬如, 如果 storage server 是 12顆 HD, 大部分的 administrator 會做成 6組 RAID 1, 然後以 stripe 模式 (raid 0) 達到最快的性能, 以及資料安全性的平衡, (因為如果使用 RAIDZ2/RAID6 效能會很糟, 同時資料遺失風險偏高, 兩個 HD 就有資料全毀的風險, hot spare 是很糟糕的模式, 因為 rebuild 過程中, 風險更高)
    > 
    > <br>
    > 結論: ZFS 在未來 3~5年的時間內 (以及過去的5年), 還是這個地球上最強大的檔案格式, 它目前面對的競爭對手有 btrFS 以及 reFS (微軟的), 上述的優點就是為什麼 Qnap 這次推出的 伺服器等級的 NAS 是選擇 ZFS 而不是 btrFS, 而 Synology 在 1~4 bay 的家用 NAS 推用 btrFS. (真的還是不要在 btrFS 上面跑 raid5/6 目前)
    > 


## ZFS Is the Best Filesystem (For Now...)

- [ZFS Is the Best Filesystem (For Now...) - Stephen Foskett, Pack Rat](https://blog.fosketts.net/2017/07/10/zfs-best-filesystem-now/#fnref-9412-4)

    > -   ZFS achieves the kind of scalability every modern filesystem should have, with few limits in terms of data or metadata count and volume or file size.
    > -   ZFS includes checksumming of all data and metadata to detect corruption, an absolutely essential feature for long-term large-scale storage.
    > -   When ZFS detects an error, it can automatically reconstruct data from mirrors, parity, or alternate locations.
    > -   Mirroring and multiple-parity "RAID Z" are built in, combining multiple physical media devices seamlessly into a logical volume.
    > -   ZFS includes robust snapshot and mirror capabilities, including the ability to update the data on other volumes incrementally.
    > -   Data can be compressed on the fly and deduplication is supported as well.
    > 
    > ---
    > 
    > ### What's Wrong With ZFS Today
    > 
    > OpenZFS remains little-changed from what we had a decade ago.
    > 
    > Many remain skeptical of deduplication, which hogs expensive RAM in the best-case scenario. And I do mean expensive: Pretty much every ZFS FAQ flatly declares that ECC RAM is a must-have and 8 GB is the bare minimum. In my own experience with FreeNAS, 32 GB is a nice amount for an active small ZFS server, and this costs $200-$300 even at today's prices.
    > 
    > And ZFS never really adapted to today's world of widely-available flash storage: Although flash can be used to support the ZIL and L2ARC caches, these are of dubious value in a system with sufficient RAM, and ZFS has no true hybrid storage capability. It's laughable that the ZFS documentation obsesses over a few GB of SLC flash when multi-TB 3D NAND drives are on the market. And no one is talking about NVMe even though it's everywhere in performance PC's.
    > 
    > Then there's the question of flexibility, or lack thereof. Once you build a ZFS volume, it's pretty much fixed for life. There are only three ways to expand a storage pool:
    > 
    > 1.  Replace each and every drive in the pool with a larger one (which is great but limiting and expensive)
    > 2.  Add a stripe on another set of drives (which can lead to imbalanced performance and redundancy and a whole world of potential stupid stuff)
    > 3.  Build a new pool and "zfs send" your datasets to it (which is what I do, even though it's kind of tricky)
    > 
    > Apart from option 3 above, you can't shrink a ZFS pool. Worse, you can't change the data protection type without rebuilding the pool, and this includes adding a second or third parity drive. The FreeNAS faithful spend an inordinate amount of time trying to talk new users out of using RAID-Z1 ^[1](https://blog.fosketts.net/2017/07/10/zfs-best-filesystem-now/#fn-9412-1)^ and moaning when they choose to use it anyway.
    > 
    > ---
    > 
    > Still, ZFS is way better than legacy storage SOHO filesystems. The lack of integrity checking, redundancy, and error recovery makes NTFS (Windows), HFS+ (macOS), and ext3/4 (Linux) wholly inappropriate for use as a long-term storage platform. And even ReFS and APFS, lacking data integrity checking, [aren't appropriate](http://blog.fosketts.net/2014/12/19/big-disk-drives-require-data-integrity-checking/) where data loss cannot be tolerated.
    > 
    > ---
    > 
    > Sad as it makes me, as of 2017, ZFS is the best filesystem for long-term, large-scale data storage. Although it can be a pain to use (except in FreeBSD, Solaris, and purpose-built appliances), the robust and proven ZFS filesystem is the only trustworthy place for data outside enterprise storage systems. After all, [reliably storing data is the only thing a storage system really has to do](http://blog.fosketts.net/2014/12/12/prime-directive-storage-lose-data/). All my important data goes on ZFS, from photos to music and movies to office files. It's going to be a long time before I trust anything other than ZFS!


## Who Needs Git When You Got ZFS?

- [Who Needs Git When You Got ZFS? – Zef.me](https://zef.me/who-needs-git-when-you-got-zfs-e9cd11aba8ea)

    > #### Who needs Git?
    > 
    > Using ZFS as a replacement of Git for is probably not a good idea, but just to give you a sense of what ZFS supports at the file system level, let me go through a few typical git-like operations:
    > 
    > -   Creating a repository
    > -   Committing or tagging a version
    > -   Branching
    > -   Pushing and pulling changes from other storage pools, possibly on other machines
    > 
    > Notably missing is support for *merging*, which ZFS does not have direct support for as far as I'm aware.
    > 
    > **Creating a repository**
    > 
    > First, let's create a filesystem for our projects, with a specific nested filesystem for our project, which we'll call "zfsgit". Ues, you can nest filesystems as deep as you like. And then we'll chown the root of the filesystem to our current user so that we don't have to sudo for creating, editing and removing files.
    > ```sh
    > $ sudo zfs create mypool/projects
    > $ sudo zfs create mypool/projects/zfsgit
    > $ sudo chown $(whoami) /Volumes/mypool/projects/zfsgit
    > $ cd /Volumes/mypool/projects/zfsgit
    > ```
    > 
    > Alright, we now have the equivalent of a repository, or checkout thereof.
    > 
    > Let's create a file and put some content in it:
    > ```sh
    > $ echo "Hello" > file.txt
    > ```
    > 
    > **"Committing" and "Tagging"**
    > 
    > In order to create a "commit" or "tag", i.e. something that is kept in our project's history and you can revert to, you can use a ZFS *snapshot*. ZFS snapshots have to be explicitly named. Let's create our first one "firstcommit". We do this by adding @ and the snapshot name to our filesystem name.
    > ```sh
    > $ sudo zfs snapshot mypool/projects/zfsgit@firstcommit
    > ```
    > Now, let's change our file slightly:
    > ```sh
    > $ echo "world" >> file.txt
    > ```
    > Let's see what changed:
    > ```sh
    > $ sudo zfs diff mypool/projects/zfsgit@firstcommit
    > M	/Volumes/mypool/projects/zfsgit/file.txt
    > ```
    > 
    > Sadly it won't really get to see a textual diff, but at least it indicates which file changed. We can now create a new commit:
    > ```sh
    > $ sudo zfs snapshot mypool/projects/zfsgit@secondcommit
    > ```
    > 
    > To list our current snapshots:
    > ```sh
    > $ sudo zfs list -t snapshot
    > NAME                                   USED   AVAIL   REFER  MOUNTPOINT
    > mypool/projects/zfsgit@firstcommit    146Ki       -   370Ki  -
    > mypool/projects/zfsgit@secondcommit       0       -   386Ki  -
    > ```
    > 
    > Now, let's make another change:
    > ```sh
    > $ echo "ladies..." >> file.txt
    > ```
    > 
    > That was a bad idea, let's roll back to our previous snapshot:
    > ```sh
    > $ sudo zfs rollback mypool/projects/zfsgit@secondcommit
    > $ cat file.txt
    > Hello
    > world
    > ```
    > 
    > And now we got our previous version back.
    > 
    > **Branching**
    > 
    > Functionality similar to branching can be achieved using zfs clone, which allows you to clone a filesystem based on a particular snapshot:
    > ```sh
    > $ sudo zfs clone mypool/projects/zfsgit@firstcommit mypool/projects/zfsgit_branch
    > ```
    > 
    > This creates a new copy-on-write filesystem, mounted under mypool/projects/zfsgit_branch which is a very light-weight operation because no copying is involved, and initially barely any extra diskspace is consumed.
    > 
    > **Pushing and pulling repositories**
    > 
    > You can send filesystems, even incrementally to other storage pools, both local and remote. To demonstrate, let's say we created another storage pool called "mypool2" locally. We can now "push" any snapshot to our the other storage pool as follows (as root):
    > ```sh
    > $ zfs send mypool/projects/zfsgit@firstcommit | zfs receive mypool2/zfsgit
    > ```
    > 
    > You can imagine, this works just as well via SSH, for instance:
    > ```sh
    > $ zfs send mypool/projects/zfsgit@firstcommit | ssh root@myserver zfs receive mypool/zfsgit
    > ```
    > 
    > This pushes the entire filesystem as it looked at the time of the snapshot. Alternatively, if we already pushed a previous snapshot before, we can also just push the difference between the previous snapshot and the current one using the -i option:
    > ```sh
    > $ zfs send -i mypool/projects/zfsgit@firstcommit mypool/projects/zfsgit@secondcommit | zfs receive mypool2/zfsgit
    > ```
    > 
    > This is useful for incrementally backing up large file systems. Of course, this is just using Unix pipes, so we can also write the result of zfs send to a file and upload it to S3, for instance:
    > ```sh
    > $ zfs send mypool/projects/zfsgit@firstcommit > backup.dump
    > ```
    > 
    > To pull a filesystem, instead of pushing it, you'd do the reverse, over SSH that could look something like this:
    > ```sh
    > ssh root@myserver zfs send mypool/zfsgit@secondcommit | zfs receive mypool/zfsgit
    > ```
    > 
    > **Should you use ZFS?**
    > 
    > ZFS is pretty cool and pretty stable, at least on Solaris and Linux. I'm not sure of the stability on Mac at this time. Using ZFS as a root file system on Linux is still slightly problematic at this moment, but those issues will likely be resolved soon. I don't have extensive experience with its reliability and performance myself, but the Internets has good things to say.
    > 
    > However, ZFS is not the only game in town. There's also [Linux' Btrfs](http://en.wikipedia.org/wiki/Btrfs), which offers many similar features. However, Btrfs is newer and less mature, it may not be as stable yet. Either way, these file systems are a lot of fun to play with. To learn more about ZFS, I'd recommend reading through [Oracle's ZFS Administration Guide](http://docs.oracle.com/cd/E19253-01/819-5461/index.html), which is pretty readable and much of it applies to Linux and Mac as well.



# bcachefs

- [bcachefs](https://bcachefs.org/)

    > Bcachefs is an advanced new filesystem for Linux, with an emphasis on reliability and robustness. It has a long list of features, completed or in progress:
    > 
    > -   Copy on write (COW) - like zfs or btrfs
    > -   Full data and metadata checksumming
    > -   Multiple devices, including replication and other types of RAID
    > -   Caching
    > -   Compression
    > -   Encryption
    > -   Snapshots
    > -   Scalable - has been tested to 50+ TB, will eventually scale far higher
    > -   Already working and stable, with a small community of users