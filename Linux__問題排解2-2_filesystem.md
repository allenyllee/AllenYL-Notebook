# Linux__問題排解2-2_filesystem

[toc]
<!-- toc --> 

# mount/umount

## mount option

- [mount(8): mount filesystem - Linux man page](https://linux.die.net/man/8/mount)

    > **atime**
    > 
    > Do not use noatime feature, then the inode access time is controlled by kernel defaults. See also the description for **strictatime** and **relatime** mount options.
    > 
    > **noatime**
    > 
    > Do not update inode access times on this filesystem (e.g, for faster access on the news spool to speed up news servers).
    > 
    > **auto**
    > 
    > Can be mounted with the **-a** option.
    > 
    > **noauto**
    > 
    > Can only be mounted explicitly (i.e., the **-a** option will not cause the filesystem to be mounted).
    > 
    > **defaults**
    > 
    > Use default options: **rw**, **suid**, **dev**, **exec**, **auto**, **nouser**, **async**, and **relatime.**
    > 
    > **dev**
    > 
    > Interpret character or block special devices on the filesystem.
    > 
    > **nodev**
    > 
    > Do not interpret character or block special devices on the file system.
    > 
    > **exec**
    > 
    > Permit execution of binaries.
    > 
    > **noexec**
    > 
    > Do not allow direct execution of any binaries on the mounted filesystem. (Until recently it was possible to run binaries anyway using a command like /lib/ld*.so /mnt/binary. This trick fails since Linux 2.4.25 / 2.6.0.)
    > 
    > **suid**
    > 
    > Allow set-user-identifier or set-group-identifier bits to take effect.
    > 
    > **nosuid**
    > 
    > Do not allow set-user-identifier or set-group-identifier bits to take effect. (This seems safe, but is in fact rather unsafe if you have **suidperl**(1) installed.)
    > 
    > **remount**
    > 
    > Attempt to remount an already-mounted filesystem. This is commonly used to change the mount flags for a filesystem, especially to make a readonly filesystem writeable. It does not change device or mount point.
    > 
    > The remount functionality follows the standard way how the mount command works with options from fstab. It means the mount command doesn't read fstab (or mtab) only when a *device* and *dir* are fully specified.
    > ```
    > mount -o remount,rw /dev/foo /dir
    > ```
    > After this call all old mount options are replaced and arbitrary stuff from fstab is ignored, except the loop= option which is internally generated and maintained by the mount command.
    > ```
    > mount -o remount,rw /dir
    > ```
    > After this call mount reads fstab (or mtab) and merges these options with options from command line ( **-o** ).
    > 
    > **user**
    > 
    > Allow an ordinary user to mount the filesystem. The name of the mounting user is written to mtab so that he can unmount the filesystem again. This option implies the options **noexec**, **nosuid**, and **nodev** (unless overridden by subsequent options, as in the option line **user,exec,dev,suid**).
    > 
    > **nouser**
    > 
    > Forbid an ordinary (i.e., non-root) user to mount the filesystem. This is the default.
    > 

- [mount - Can't execute a file with execute permission bit set - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/102812/cant-execute-a-file-with-execute-permission-bit-set)

    > If you use `user` and want to have executable files, use `user,exec`.


## bind mount

- [14.04 - How to make mount --bind permanent? - Ask Ubuntu](https://askubuntu.com/questions/550348/how-to-make-mount-bind-permanent)

    > The easiest way is to *mount --bind* what you need like
    > 
    > ```
    > mount --bind /home/sda1/Windows/Users/Me/Dropbox ~/Dropbox
    > 
    > ```
    > 
    > Then open *mtab*
    > 
    > ```
    > sudo nano /etc/mtab
    > 
    > ```
    > 
    > Copy your line like
    > 
    > ```
    > /home/sda1/Windows/Users/Me/Dropbox /home/me/Dropbox none rw,bind 0 0
    > 
    > ```
    > 
    > and paste it in *fstab* so it would mount on reboot
    > 
    > ```
    > sudo nano /etc/fstab
    > 
    > ```
    > 
    > If you folder is on mounted disk make sure your binding line comes after disk mount



- [filesystems - What is a bind mount? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/198590/what-is-a-bind-mount/198591)

    > What is a bind mount?
    > ---------------------
    > 
    > A *bind mount* is an alternate view of a directory tree. Classically, mounting creates a view of a storage device as a directory tree. A bind mount instead takes an existing directory tree and replicates it under a different point. The directories and files in the bind mount are the same as the original. Any modification on one side is immediately reflected on the other side, since the two views show the same data.
    > 
    > 
    > Unlike a hard link or symbolic link, a bind mount doesn't affect what is stored on the filesystem. It's a property of the live system.
    > 
    > ---
    > 
    > How do I create a bind mount?
    > -----------------------------
    > 
    > ### bindfs
    > 
    > The [`bindfs`](http://bindfs.org/) filesystem is a [FUSE](http://en.wikipedia.org/wiki/Filesystem_in_Userspace) filesystem which creates a view of a directory tree. For example, the command
    > 
    > ```
    > bindfs /some/where /else/where
    > 
    > ```
    > 
    > makes `/else/where` a mount point under which the contents of `/some/where` are visible.
    > 
    > Since bindfs is a separate filesystem, the files `/some/where/foo` and `/else/where/foo` appear as different files to applications (the bindfs filesystem has its own `st_dev` value). Any change on one side is "magically" reflected on the other side, but the fact that the files are the same is only apparent when one knows how bindfs operates.
    > 
    > Bindfs has no knowledge of mount points, so if there is a mount point under `/some/where`, it appears as just another directory under `/else/where`. Mounting or unmounting a filesystem underneath `/some/where` appears under `/else/where` as a change of the corresponding directory.
    > 
    > ---
    > 
    > ### Linux bind mount
    > 
    > Under Linux, bind mounts are available as a kernel feature. You can create one with the [`mount`](http://man7.org/linux/man-pages/man8/mount.8.html) command, by passing either the `--bind` command line option or the `bind` mount option. The following two commands are equivalent:
    > 
    > ```
    > mount --bind /some/where /else/where
    > mount -o bind /some/where /else/where
    > 
    > ```
    > 
    > Here, the "device" `/some/where` is not a disk partition like in the case of an on-disk filesystem, but an existing directory. The mount point `/else/where` must be an existing directory as usual. Note that no filesystem type is specified either way: making a bind mount doesn't involve a filesystem driver, it copies the kernel data structures from the original mount.
    > 
    > ---
    > 
    > If there are mount points under `/some/where`, their contents are not visible under `/else/where`. Instead of `bind`, you can use `rbind`, also replicate mount points underneath `/some/where`. For example, if `/some/where/mnt` is a mount point then
    > 
    > ```
    > mount --rbind /some/where /else/where
    > 
    > ```
    > 
    > is equivalent to
    > 
    > ```
    > mount --bind /some/where /else/where
    > mount --bind /some/where/mnt /else/where/mnt
    > 
    > ```
    > 
    > ---
    > 
    > It is possible to have different mount options in two bind-mounted directories. There is a quirk, however: making the bind mount and setting the mount options cannot be done atomically, they have to be two successive operations. (Older kernels did not allow this.) For example, the following commands create a read-only view, but there is a small window of time during which `/else/where` is read-write:
    > 
    > ```
    > mount --bind /some/where /else/where
    > mount -o remount,ro,bind /else/where
    > 
    > ```
    > 
    > ---
    > 
    > ### Read-only view
    > 
    > It can be useful to create a read-only view of a filesystem, either for security reasons or just as a layer of safety to ensure that you won't accidentally modify it.
    > 
    > With bindfs:
    > 
    > ```
    > bindfs -r /some/where /mnt/readonly
    > 
    > ```
    > 
    > With Linux, the simple way:
    > 
    > ```
    > mount --bind /some/where /mnt/readonly
    > mount -o remount,ro,bind /mnt/readonly
    > 
    > ```
    > 
    > This leaves a short interval of time during which `/mnt/readonly` is read-write. If this is a security concern, first create the bind mount in a directory that only root can access, make it read-only, then move it to a public mount point. In the snippet below, note that it's important that `/root/private` (the directory above the mount point) is private; the original permissions on `/root/private/mnt` are irrelevant since they are hidden behind the mount point.
    > 
    > ```
    > mkdir -p /root/private/mnt
    > chmod 700 /root/private
    > mount --bind /some/where /root/private/mnt
    > mount -o remount,ro,bind /root/private/mnt
    > mount --move /root/private/mnt /mnt/readonly
    > 
    > ```
    > 
    > ---
    > 
    > ### Mounting in a jail
    > 
    > A [chroot jail](http://en.wikipedia.org/wiki/Chroot) runs a process in a subtree of the system's directory tree. This can be useful to run a program with restricted access, e.g. run a network server with access to only its own files and the files that it serves, but not to other data stored on the same computer). A limitation of chroot is that the program is confined to one subtree: it can't access independent subtrees. Bind mounts allow grafting other subtrees onto that main tree.
    > 
    > For example, suppose that a machine runs a service `/usr/sbin/somethingd` which should only have access to data under `/var/lib/something`. The smallest directory tree that contains both of these files is the root. How can the service be confined? One possibility is to make hard links to all the files that the service needs (at least `/usr/sbin/somethingd` and several shared libraries) under `/var/lib/something`. But this is cumbersome (the hard links need to be updated whenever a file is upgraded), and doesn't work if `/var/lib/something` and `/usr` are on different filesystems. A better solution is to create an ad hoc root and populate it with using mounts:
    > 
    > ```
    > mkdir /run/something
    > cd /run/something
    > mkdir -p etc/something lib usr/lib usr/sbin var/lib/something
    > mount --bind /etc/something etc/something
    > mount --bind /lib lib
    > mount --bind /usr/lib usr/lib
    > mount --bind /usr/sbin usr/sbin
    > mount --bind /var/lib/something var/lib/something
    > mount -o remount,ro,bind etc/something
    > mount -o remount,ro,bind lib
    > mount -o remount,ro,bind usr/lib
    > mount -o remount,ro,bind usr/sbin
    > chroot . /usr/sbin/somethingd &
    > 
    > ```
    > 
    > Linux's [mount namespaces](http://lwn.net/2001/0301/a/namespaces.php3) generalize chroots. Bind mounts are how namespaces can be populated in flexible ways. See [Making a process read a different file for the same filename](https://unix.stackexchange.com/questions/81003/making-a-process-read-a-different-file-for-the-same-filename) for an example.
    > 
    > ---
    > 
    > ### Running a different distribution
    > 
    > Another use of chroots is to install a different distribution in a directory and run programs from it, even when they require files at hard-coded paths that are not present or have different content on the base system. This can be useful, for example, to install a 32-bit distribution on a 64-bit system that doesn't support mixed packages, to install older releases of a distribution or other distributions to test compatibility, to install a newer release to test the latest features while maintaining a stable base system, etc. See [How do I run 32-bit programs on a 64-bit Debian/Ubuntu?](https://unix.stackexchange.com/questions/12956/how-do-i-run-32-bit-programs-on-a-64-bit-debian-ubuntu) for an example on Debian/Ubuntu.
    > 
    > Suppose that you have an installation of your distribution's latest packages under the directory `/f/unstable`, where you run programs by switching to that directory with `chroot /f/unstable`. To make home directories available from this installations, bind mount them into the chroot:
    > 
    > ```
    > mount --bind /home /f/unstable/home
    > 
    > ```
    > 
    > The program [schroot](https://packages.debian.org/jessie/schroot) does this automatically.
    > 
    > ---
    > 
    > ### Accessing files hidden behind a mount point
    > 
    > When you mount a filesystem on a directory, this hides what is behind the directory. The files in that directory become inaccessible until the directory is unmounted. Because BSD nullfs and Linux bind mounts operate at a lower level than the mount infrastructure, a nullfs mount or a bind mount of a filesystem exposes directories that were hidden behind submounts in the original.
    > 
    > For example, suppose that you have a tmpfs filesystem mounted at `/tmp`. If there were files under `/tmp` when the tmpfs filesystem was created, these files may still remain, effectively inaccessible but taking up disk space. Run
    > 
    > ```
    > mount --bind / /mnt
    > 
    > ```
    > 
    > (Linux) or
    > 
    > ```
    > mount -t nullfs / /mnt
    > 
    > ```
    > 
    > (FreeBSD) to create a view of the root filesystem at `/mnt`. The directory `/mnt/tmp` is the one from the root filesystem.
    > 
    > ---
    > 
    > Side effects of bind mounts
    > ---------------------------
    > 
    > ### Recursive directory traversals
    > 
    > If you use bind mounts, you need to take care of applications that traverse the filesystem tree recursively, such as backups and indexing (e.g. to build a [locate](http://en.wikipedia.org/wiki/Locate_(Unix)) database).
    > 
    > Usually, bind mounts should be excluded from recursive directory traversals, so that each directory tree is only traversed once, at the original location. With bindfs and nullfs, configure the traversal tool to ignore these filesystem types, if possible. Linux bind mounts cannot be recognized as such: the new location is equivalent to the original. With Linux bind mounts, or with tools that can only exclude paths and not filesystem types, you need to exclude the mount points for the bind mounts.
    > 
    > Traversals that stop at filesystem boundaries (e.g. `find -xdev`, `rsync -x`, `du -x`, ...) will automatically stop when they encounter a bindfs or nullfs mount point, because that mount point is a different filesystem. With Linux bind mounts, the situation is a bit more complicated: there is a filesystem boundary only if the bind mount is grafting a different filesystem, not if it is grafting another part of the same filesystem.
    > 
    > 



## loop device

- [loop device介绍及losetup使用-秋天的童话-51CTO博客](http://blog.51cto.com/wushank/1212647)

    > 一、**loop 设备介绍**\
    > 1、 在类 UNIX 系统里，loop设备是一种伪设备(pseudo-device)，或者也可以说是仿真设备。它能使我们像块设备一样访问一个文件。在使用之前，一个 loop设备必须要和一个文件进行连接。这种结合方式给用户提供了一个替代块特殊文件的接口。因此，如果这个文件包含有一个完整的文件系统，那么这个文件就可以像一个磁盘设备一样被mount 起来。
    > 
    >   上面说的文件格式，我们经常见到的是 CD 或 DVD 的 ISO 光盘镜像文件或者是软盘(硬盘)的 *.img镜像文件。通过这种 loop mount (回环mount)的方式，这些镜像文件就可以被 mount到当前文件系统的一个目录下。\
    >   
    >    至 此，顺便可以再理解一下 loop之含义：对于第一层文件系统，它直接安装在我们计算机的物理设备之上；而对于这种被 mount起来的镜像文件(它也包含有文件系统)，它是建立在第一层文件系统之上，这样看来，它就像是在第一层文件系统之上再绕了一圈的文件系统，所以称为loop。
    > 
    >  2、在 Linux 里，loop 设备的设备名形如：
    >  
    > ```
    >      ls /dev/loop*
    > 
    >           /dev/loop0  /dev/loop2 /dev/loop4  /dev/loop6
    > 
    >           /dev/loop1  /dev/loop3 /dev/loop5  /dev/loop7
    > 
    >               ... ...
    > ```
    > 例如，要在一个目录下 mount 一个包含有磁盘镜像的文件，需要分 2 步走：
    > 
    > losetup /dev/loop0  disk.img #使磁盘镜像文件与循环设备连结起来
    > 
    > mount /dev/loop0   /home/groad/disk_test #将循环设备 mount 到目录 disk_test下\
    > 
    >    经过上面的两个命令后，镜像文件就如同一个文件系统挂载在 disk_test目录下，当然我们也可以往镜像里面添加文件。其实上面的两个步骤可以写成一个步骤：
    > 
    >    mount -t minix -o loop./disk.img ./disk_test\
    >       其 中，加了 -o loop 指定后，那么也就相当于执行了第一行的 losetup 命令。
    > 
    >   最后，要卸载的话，就直接 umount /dev/loop0 即可。
    > 
    > 二、**完整测试实例**
    > 
    > **     1. 首先创建一个 1G 大小的空文件**：
    > 
    >            # dd if=/dev/zeroof=loopfile.img bs=1G count=1
    > 
    >               1+0 records in
    > 
    >               1+0 records out
    > 
    >               1073741824 bytes (1.1 GB) copied, 69.3471 s, 15.5 MB/s
    > 
    >  **2\. 对该文件格式化为 ext4 格式**：
    > ```shell
    > # mkfs.ext4    loopfile.img
    > ```
    > > mke2fs 1.41.11 (14-Mar-2010)\
    > > loopfile.img is not a block special device.\
    > > Proceed anyway? (y,n) y\
    > > Filesystem label=\
    > > OS type: Linux\
    > > Block size=4096 (log=2)\
    > > Fragment size=4096 (log=2)\
    > > Stride=0 blocks, Stripe width=0 blocks\
    > > 65536 inodes, 262144 blocks\
    > > 13107 blocks (5.00%) reserved for the super user\
    > > First data block=0\
    > > Maximum filesystem blocks=268435456\
    > > 8 block groups\
    > > 32768 blocks per group, 32768 fragments per group\
    > > 8192 inodes per group\
    > > Superblock backups stored on blocks:\
    > > 32768,98304, 163840, 229376\
    > >\
    > > Writing inode tables:done\
    > > Creating journal (8192 blocks): done\
    > > Writing superblocks and filesystem accounting information:done\
    > >\
    > > This filesystem will be automatically checked every 38 mountsor\
    > > 180 days, whichever comesfirst. Use tune2fs -c or -i tooverride.
    > 
    >    **3\. 用 file 命令查看下格式化后的文件类型**：
    > 
    >          # file loopfile.img
    > 
    >              loopfile.img: Linux rev 1.0 ext4 filesystem data,UUID=a9dfb4a0-6653-4407-ae05-7044d92c1159 (extents) (large files)(huge files)
    > 
    >  **4\. 准备将上面的文件挂载起来**：
    > 
    >              # mkdir /mnt/loopback
    > 
    >              # mount -o loop loopfile.img /mnt/loopback\
    >       mount 命令的 -o loop 选项可以将任意一个 loopback 文件系统挂载。上面的 mount 命令实际等价于下面两条命令：
    > 
    >              # losetup /dev/loop0   loopfile.img
    > 
    >              # mount /dev/loop0    /mnt/loopback\
    >       因此实际上，mount -o loop 在内部已经默认的将文件和 /dev/loop0 挂载起来了。
    > 
    >        然而对于第一种方法(mount -oloop)并不能适用于所有的场景。比如，我们想创建一个硬盘文件，然后对该文件进行分区，接着挂载其中一个子分区，这时就不能用 -oloop 这种方法了。因此必须如下做：
    > 
    >          # losetup /dev/loop1   loopfile.img
    > 
    >          # fdisk /dev/loop1
    > 
    >  **6\. 卸载挂载点**
    > 
    >       # umount/mnt/loopback
    > 
    > **三、losetup介绍：**
    > 
    > losetup [ -e encryption ] [ -o offset ] loop_device file losetup [ -d ] loop_device\
    > 描 述：losetup 用 来 将 loop device 与 档 案 或 block device 联 结 、 分 离 . 以 及 查 询 loop device 目 前 的 状 况 , 如 只 给 定 loop_device 的 参 数 . 则 秀 出 loop device 目 前 的 状 况 .\
    > 选 项 ：\
    > -d  将某个档案或装制与loop装置分离\
    > -e encryption\
    > 启 动 资 料 编 码 . 下 列 为 可 用 的 选 项 参 数 :\
    > NONE  不 编 码 ( 定 义 值 ) .\
    > XOR  使 用 简 易 的 XOR 编 码\
    > DES 编 码 须 在 kernel 上 加 上 DES 编 码 功 能 . DES 编 码 是 利 用 启 始 值 做 为 密 码 保 护 来 防 止 他 人 用 字 典 功 击 法 破 解 .\
    > -o offset  资 料 开 启 时 资 料 平移(offset) 几 个 bytes 来 与 档 案 或 装 置 联 接 .
    > 
    > 举例：\
    >       If  you  are  using the loadable module you must have the module loaded\
    >       first with the command\
    >              # modprobe loop\
    >       Maybe also encryption modules are needed.\
    >              # modprobe des # modprobe cryptoloop\
    >       The following commands can be used as an  example  of  using  the  loop\
    >       device.\
    >              # dd if=/dev/zero of=/file bs=1k count=100\
    >              # losetup -e des /dev/loop0 /file\
    >              Password:\
    >              Init (up to 16 hex digits):\
    >              # mkfs -t ext2 /dev/loop0 100\
    >              # mount -t ext2 /dev/loop0 /mnt\
    >               ...\
    >              # umount /dev/loop0\
    >              # losetup -d /dev/loop0
    > 
    > **四、loop设备的参数调整：**
    > 
    > 如果需要超过8个loopdevice，那么使用losetup命令的时候可能会遇到类似的错误 'no suchdevice',这是因为超过了可用loopdevice设备的最大限制，依据你的Linux系统，可以通过修改
    > 
    > /etc/modprobe.conf
    > 
    > 配置文件，增加如下参数的方式进行扩展
    > 
    > options loopmax_loop=20 --比如我增加到20个
    > 
    > 保存退出，如果要了马上生效的话，可以通过
    > 
    > modprobe -vloop
    > 
    > 命令立即加载该模块。
    > ```
    > [root@vm11g dev]# cat /etc/modprobe.conf|greploop\
    > options loop max_loop=20
    > 
    > [root@vm11g dev]# modprobe -v loop\
    > insmod/lib/modules/2.6.9-42.0.0.0.1.ELsmp/kernel/drivers/block/loop.komax_loop=20\
    > 
    > [root@vm11g dev]# ls -ltr/dev/loop*\
    > brw-rw---- 1 root disk 7, 8 Jul 19 07:44 /dev/loop8\
    > brw-rw---- 1 root disk 7, 9 Jul 19 07:44 /dev/loop9\
    > brw-rw---- 1 root disk 7, 10 Jul 19 07:44 /dev/loop10\
    > brw-rw---- 1 root disk 7, 11 Jul 19 07:44 /dev/loop11\
    > brw-rw---- 1 root disk 7, 12 Jul 19 07:44 /dev/loop12\
    > brw-rw---- 1 root disk 7, 13 Jul 19 07:44 /dev/loop13\
    > brw-rw---- 1 root disk 7, 14 Jul 19 07:44 /dev/loop14\
    > brw-rw---- 1 root disk 7, 15 Jul 19 07:44 /dev/loop15\
    > brw-rw---- 1 root disk 7, 16 Jul 19 07:44 /dev/loop16\
    > brw-rw---- 1 root disk 7, 17 Jul 19 07:44 /dev/loop17\
    > brw-rw---- 1 root disk 7, 18 Jul 19 07:44 /dev/loop18\
    > brw-rw---- 1 root disk 7, 19 Jul 19 07:44 /dev/loop19\
    > brw-rw---- 1 root disk 7, 0 Jul 19 2009 /dev/loop0\
    > brw-rw---- 1 root disk 7, 1 Jul 19 2009 /dev/loop1\
    > brw-rw---- 1 root disk 7, 2 Jul 19 2009 /dev/loop2\
    > brw-rw---- 1 root disk 7, 3 Jul 19 2009 /dev/loop3\
    > brw-rw---- 1 root disk 7, 4 Jul 19 2009 /dev/loop4\
    > brw-rw---- 1 root disk 7, 5 Jul 19 2009 /dev/loop5\
    > brw-rw---- 1 root disk 7, 6 Jul 19 2009 /dev/loop6\
    > brw-rw---- 1 root disk 7, 7 Jul 19 2009/dev/loop7
    > ```
    > 有了这个东西,在Linux下就可以借助file来测试学习ASM了。
    > 

### find which images belong to which /dev/loop(losetup -l)

- [How to find which images belong to which /dev/loop? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/172382/how-to-find-which-images-belong-to-which-dev-loop)

    > `losetup` (the command normally used to set them up) will tell you:
    > 
    > ```
    > $ /sbin/losetup --list
    > NAME       SIZELIMIT OFFSET AUTOCLEAR RO BACK-FILE
    > /dev/loop0         0      0         0  0 /var/tmp/jigdo/debian-7.6.0-amd64-CD-1.iso
    > 
    > ```
    > 
    > Note that with older versions you may hat to use use `-a` instead of `--list`, and this outputs in a different and now deprecated format.
    > 
    > The information comes from `/sys`:
    > 
    > ```
    > $ cat /sys/class/block/loop0/loop/backing_file
    > /var/tmp/jigdo/debian-7.6.0-amd64-CD-1.iso
    > 
    > ```
    > 
    > Another, possibly more portable, option is to get it from udisks:
    > 
    > ```
    > $ udisksctl info -b /dev/loop0
    > /org/freedesktop/UDisks2/block_devices/loop0:
    > ⋮
    >   org.freedesktop.UDisks2.Loop:
    >     Autoclear:          false
    >     BackingFile:        /var/tmp/jigdo/debian-7.6.0-amd64-CD-1.iso
    >     SetupByUID:         1000
    > ⋮
    > 
    > ```
    > 
    > `losetup` will also happily remove them for you, using the `-d` option. That just requires the loop device as a parameter; it doesn't care about the backing file/device.

### mount multiple partitions from disk image simultaneously (losetup -P/kpartx)

- [loop device - How to mount multiple partitions from disk image simultaneously? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/342463/how-to-mount-multiple-partitions-from-disk-image-simultaneously)

    > **losetup 2.21 -P option**
    > 
    > ```
    > losetup -P -f --show my.img
    > 
    > ```
    > 
    > Creates one `/dev/loopXpY` per partition.
    > 
    > Advantage: executable pre-installed in many distros (util-linux package).
    > 
    > Disadvantage: quite recent option, not present in Ubuntu 14.04, before that just use kpartx: <https://unix.stackexchange.com/a/405639/32558>
    > 
    > **`losetup -P` automation**
    > 
    > Usage:
    > 
    > ```
    > $ los my.img
    > /dev/loop0
    > /mnt/loop0p1
    > /mnt/loop0p2
    > 
    > $ ls /mnt/loop0p1
    > /whatever
    > /files
    > /youhave
    > /there
    > 
    > $ sudo losetup -l
    > NAME       SIZELIMIT OFFSET AUTOCLEAR RO BACK-FILE                                                                                      DIO
    > /dev/loop1         0      0         0  0 /full/path/to/my.img
    > 
    > $ # Cleanup.
    > $ losd 0
    > $ ls /mnt/loop0p1
    > $ ls /dev | grep loop0
    > loop0
    > 
    > ```
    > 
    > Source:
    > 
    > ```
    > los() (
    >   img="$1"
    >   dev="$(sudo losetup --show -f -P "$img")"
    >   echo "$dev"
    >   for part in "$dev"?*; do
    >     if [ "$part" = "${dev}p*" ]; then
    >       part="${dev}"
    >     fi
    >     dst="/mnt/$(basename "$part")"
    >     echo "$dst"
    >     sudo mkdir -p "$dst"
    >     sudo mount "$part" "$dst"
    >   done
    > )
    > losd() (
    >   dev="/dev/loop$1"
    >   for part in "$dev"?*; do
    >     if [ "$part" = "${dev}p*" ]; then
    >       part="${dev}"
    >     fi
    >     dst="/mnt/$(basename "$part")"
    >     sudo umount "$dst"
    >   done
    >   sudo losetup -d "$dev"
    > )
    > 
    > ```

    > ---
    > 
    > Use `kpartx` tool. It will map image partitions using `/dev/mapper` which you can mount directly.
    > 
    > ```
    > $ sudo kpartx -a disk.img
    > $ sudo mount -o loop /dev/mapper/loop0p2 /mnt
    > 
    > ```
    > 
    > PS. Do not forget to remove mappings after you are done: `sudo kpartx -d disk.img`


## umount when the device is busy

- [linux - Can't unmount a loop backed file but there's no open files? - Server Fault](https://serverfault.com/questions/58991/cant-unmount-a-loop-backed-file-but-theres-no-open-files)

    > I believe this is what [fuser](http://linux.die.net/man/1/fuser) is for. Specifically, `fuser -km /path/to/mount/point` - note that the `-k` flag kills processes with files open on this filesystem. You can omit this flag to see a list first.


- [How to umount when the device is busy | Something Odd!](https://odd.blog/2008/02/13/how-to-umount-when-the-device-is-busy/)

    > ```shell
    > # umount /media/disk/
    > umount: /media/disk: device is busy
    > umount: /media/disk: device is busy
    > ```
    > 
    > First thing you'll do will probably be to close down all your terminals and xterms but here's a better way. You can use the fuser command to find out which process was keeping the device busy:
    > 
    > ```shell
    > # fuser -m /dev/sdc1
    > /dev/sdc1: 538
    > # ps auxw|grep 538
    > donncha 538 0.4 2.7 219212 56792 ? SLl Feb11 11:25 rhythmbox
    > ```
    > 
    > Rhythmbox is the culprit! Close that down and umount the drive. Problem solved!
    > 

## mount VHD/VHDX by qemu

- [[ubuntu] How do you mount a VHD image](https://ubuntuforums.org/showthread.php?t=2299701)

    > Sorry about that simply install qemu-utils
    > 
    > ```sh
    > sudo apt-get install qemu-utils
    > ```
    > 
    > Now it says to Load the nbd kernel module. Yes, I'm serious, the network block device module! (Note: All of the following commands require superuser permissions, so escalate your privileges in whatever way makes you most comfortable.)
    > 
    > So that is done by
    > 
    > ```sh
    > sudo rmmod nbd 
    > sudo modprobe nbd max_part=16
    > ```
    > 
    > Then run qemu-nbd, which is a user space loopback block device server for QEMU-supported disk images. Basically, it knows all about weird disk image formats, and presents them to the kernel via nbd, and ultimately to the rest of the system as if they were a normal disk.
    > 
    > ```sh
    > qemu-nbd -c /dev/nbd0 <vdi-file>
    > ```
    > 
    > Of course you will need to replace <vdi-file> with your vdi name.
    > 
    > Then That command will expose the entire image as a block device named /dev/nbd0, and the partitions within it as subdevices. For example, the first partition in the image will appear as **/dev/nbd0p1.**
    > 
    > Now you could, for instance, run cfdisk on the block device, but **you will most likely want to mount an individual partition**.
    > 
    > 
    > ```sh
    > mount /dev/nbd0p1 /mnt
    > ```
    > 
    > Again changing if needed.
    > 
    > Now you should be able to move things in and out as he states.
    > 
    > And in his own words
    > 
    > Gadzooks! Now you can muck around inside the filesystem to your heart's content. Go ahead and copy stuff in or out, or if you're feeling fruity, have some chrooty: chroot /mnt.
    > And when you're done, unmount the filesystem and shut down the qemu-nbd service.
    > 
    > By way of
    > 
    > 
    > ```sh
    > umount /mnt
    > qemu-nbd -d /dev/nbd0
    > ```
    > 
    > ---
    > 
    > You can then mount the image with:
    > ```sh
    > sudo modprobe nbd max_part=16
    > sudo qemu-nbd -c /dev/nbd0 /path/to/vhdfile
    > sudo partprobe /dev/nbd0
    > sudo mount /dev/nbd0p1 /mnt/image
    > ```
    > 
    > Obviously you need to replace the path in red with the actual path to where the VHD image is located. Don't forget to unmount the image like you would as normal after you're done.
    > 
    > sudo umount /mnt/image
    > 




## mount vdi/vmdk/ova by qemu

- [How to mount a virtual hard disk? - Ask Ubuntu](https://askubuntu.com/questions/202571/how-to-mount-a-virtual-hard-disk)

    > You can also use qemu:
    > 
    > For `.vdi`
    > ----------
    > 
    > ```
    > sudo modprobe nbd
    > sudo qemu-nbd -c /dev/nbd1 ./linux_box/VM/image.vdi
    > 
    > ```
    > 
    > if they are not installe you can install them (on Ubuntu is this comand)
    > 
    > ```
    > sudo apt install qemu-utils
    > 
    > ```
    > 
    > and then mount it
    > 
    > ```
    > mount /dev/nbd1p1 /mnt
    > 
    > ```
    > 
    > For `.vmdk`
    > -----------
    > 
    > ```
    > sudo modprobe nbd
    > sudo qemu-nbd -r -c /dev/nbd1 ./linux_box/VM/image.vmdk
    > 
    > ```
    > 
    > notice tha I use the option `-r` that's because **VMDK version 3 must be read only** to be able to be mounted by qemu
    > 
    > and then I mount it
    > 
    > ```
    > mount /dev/nbd1p1 /mnt
    > 
    > ```
    > 
    > I use `nbd1` because `nbd0` sometimes gives 'mount: special device /dev/nbd0p1 does not exist'
    > 
    > For .ova
    > --------
    > 
    > ```
    > tar -tf image.ova
    > tar -xvf image.ova
    > 
    > ```
    > 
    > The above will extract the `.vmdk` disk and then mount that.

## Unable to mount NTFS partition

- [Unable to mount NTFS partition (no hibernation) - Ask Ubuntu](https://askubuntu.com/questions/748163/unable-to-mount-ntfs-partition-no-hibernation)

    > Run `sudo ntfsfix /dev/sda2` and you will be able to mount the partition.

- [Unable to mount Windows (NTFS) filesystem due to hibernation - Ask Ubuntu](https://askubuntu.com/questions/145902/unable-to-mount-windows-ntfs-filesystem-due-to-hibernation)

    > EDIT: **DOING THIS *MIGHT* HAVE DANGEROUS CONSEQUENCES** and Windows might fail to boot or corrupt the filesystem upon booting.
    > 
    > * * * * *
    > 
    > Use [ntfsfix](http://linux.die.net/man/8/ntfsfix) in the terminal, even if you can't access Windows
    > 
    > ```
    > sudo ntfsfix /dev/sdXY
    > 
    > ```
    > 
    > where XY is the partition, e.g. `a2` (`/dev/sda2`) or `b1` (`/dev/sdb1`)
    > 
    > ntfsfix repairs some fundamental NTFS inconsistencies, resets the NTFS journal file and schedules an NTFS consistency check for the first boot into Windows.


# filesystem check

## fsck commands

- [10 Linux Fsck Command Examples to Check and Repair Filesystem](https://www.thegeekstuff.com/2012/08/fsck-command-examples/comment-page-1/)

    > Linux fsck utility is used to check and repair Linux filesystems ([ext2, ext3, ext4](https://www.thegeekstuff.com/2011/05/ext2-ext3-ext4/), etc.).
    > 
    > Depending on when was the last time a file system was checked, the system runs the fsck during boot time to check whether the filesystem is in consistent state. System administrator could also run it manually when there is a problem with the filesystems.
    > 
    > Make sure to execute the fsck on an unmounted file systems to avoid any data corruption issues.
    > 
    > This article explains 10 practical examples on how to execute fsck command to troubleshoot and fix any filesystem errors.
    > 
    > ### 1\. Filesystem Check on a Disk Partition
    > 
    > First, view all the available partitions on your system using [parted command](https://www.thegeekstuff.com/2011/09/parted-command-examples/) as shown below.
    > ```
    > # parted /dev/sda 'print'
    > 
    > Number  Start   End     Size    Type      File system  Flags
    >  1      1049kB  106MB   105MB   primary   fat16        diag
    >  2      106MB   15.8GB  15.7GB  primary   ntfs         boot
    >  3      15.8GB  266GB   251GB   primary   ntfs
    >  4      266GB   500GB   234GB   extended
    >  5      266GB   466GB   200GB   logical   ext4
    >  6      467GB   486GB   18.3GB  logical   ext2
    >  7      487GB   499GB   12.0GB  logical   fat32        lba
    > ```
    > 
    > You can check a specific filesystem (for example: /dev/sda6) as shown below.
    > ```
    > # fsck /dev/sda6
    > fsck from util-linux 2.20.1
    > e2fsck 1.42 (29-Nov-2011)
    > /dev/sda6: clean, 95/2240224 files, 3793506/4476416 blocks
    > ```
    > 
    > The following are the possible [exit codes](https://www.thegeekstuff.com/2010/03/bash-shell-exit-status/) for fsck command.
    > 
    > -   0 -- No errors
    > -   1 -- Filesystem errors corrected
    > -   2 -- System should be rebooted
    > -   4 -- Filesystem errors left uncorrected
    > -   8 -- Operational error
    > -   16 -- Usage or syntax error
    > -   32 -- Fsck canceled by user request
    > -   128 -- Shared-library error
    > 
    > ### 2\. Fsck Command Specific to a Filesystem Type
    > 
    > fsck internally uses the respective filesystem checker command for a filesystem check operation. These fsck checker commands are typically located under /sbin.
    > 
    > The following example show the various possible fsck checker commands (for example: fsck.ext2, fsck.ext3, fsck.ext4, etc.)
    > ```
    > # cd /sbin
    > # ls fsck*
    > fsck  fsck.cramfs  fsck.ext2  fsck.ext3  fsck.ext4  fsck.ext4dev  fsck.minix  fsck.msdos  fsck.nfs  fsck.vfat
    > ```
    > 
    > fsck command will give you an error when it doesn't find a filesystem checker for the filesystem that is being checked.
    > 
    > For example, if you execute fsck over a ntfs partition, you'll get the following error message. There is no fsck.ntfs under /sbin. So, this gives the following error message.
    > ```
    > # fsck /dev/sda2
    > fsck from util-linux 2.20.1
    > fsck: fsck.ntfs: not found
    > fsck: error 2 while executing fsck.ntfs for /dev/sda2
    > ```
    > 
    > ### 3\. Check All Filesystems in One Run using Option -A
    > 
    > You can check all the filesystems in a single run of fsck using this option. This checks the file system in the order given by the fs_passno mentioned for each filesystem in /etc/fstab.
    > 
    > Please note that the filesystem with a fs_passno value of 0 are skipped, and greater than 0 are checked in the order.
    > 
    > The /etc/fstab contains the entries as listed below,
    > ```
    > # cat /etc/fstab
    > 
    > ##
    > proc            /proc           proc    nodev,noexec,nosuid 0       0
    > ## / was on /dev/sda5 during installation
    > /dev/sda5 /               ext4    errors=remount-ro 0       1
    > ## /mydata was on /dev/sda6 during installation
    > /dev/sda6 /mydata         ext2    defaults        0       2
    > ## /backup was on /dev/sda7 during installation
    > /dev/sda7 /backup         vfat    defaults        0       3
    > ```
    > 
    > Here, the filesystem with the same fs_passno are checked in parallel in your system.
    > ```
    > # fsck -A
    > ```
    > 
    > It is recommended that you exclude the root filesystem during this global check by adding -R option as shown below.
    > ```
    > # fsck -AR -y
    > fsck from util-linux 2.20.1
    > e2fsck 1.42 (29-Nov-2011)
    > /dev/sda6: clean, 95/2240224 files, 3793506/4476416 blocks
    > dosfsck 3.0.12, 29 Oct 2011, FAT32, LFN
    > /dev/sda7: 8 files, 50/1463400 clusters
    > ```
    > 
    > Note: Option -y is explained in one of the examples below.
    > 
    > ### 4\. Check Only a Specific Filesystem Type using Option -t
    > 
    > Using fsck -t option, you can specify the list of filesystem to be checked. When you are using with option -A, the fsck will check only the filesystem mentioned with this option -t. Note that fslist is a comma separated values.
    > 
    > Now, pass ext2 as the fslist value to -t option as shown below:
    > ```
    > # fsck -AR -t ext2 -y
    > fsck from util-linux 2.20.1
    > e2fsck 1.42 (29-Nov-2011)
    > /dev/sda6: clean, 11/2240224 files, 70327/4476416 blocks
    > ```
    > 
    > In this example, /dev/sda6 is the only partition created with the filesystem ext2, thus it get checked accordingly.
    > 
    > Using the keyword 'no' in front of filesystem, you can check all other filesystem types except a particular filesystem.
    > 
    > In the following example, ext2 filesystem is excluded from the check.
    > ```
    > # fsck -AR -t noext2 -y
    > fsck from util-linux 2.20.1
    > dosfsck 3.0.12, 29 Oct 2011, FAT32, LFN
    > /dev/sda7: 0 files, 1/1463400 clusters
    > ```
    > 
    > ### 5\. Don't execute Fsck on Mounted Filesystem using Option -M
    > 
    > It is a good idea to use this option as default with all your fsck operation. This prevents you from running fsck accidentally on a filesystem that is mounted.
    > ```
    > # mount | grep "/dev/sd*"
    > /dev/sda5 on / type ext4 (rw,errors=remount-ro)
    > /dev/sda6 on /mydata type ext2 (rw)
    > /dev/sda7 on /backup type vfat (rw)
    > ```
    > 
    > As shown above, /dev/sda7 is mounted. If you try to execute fsck on this /dev/sda7 mounted filesystem (along with the -M option), fsck will simply exit with the exit code 0 as shown below.
    > ```
    > # fsck -M /dev/sda7
    > # echo $?
    > 0
    > ```
    > 
    > ### 6\. Skip the Display Title using Option -T
    > 
    > Using option -T, you can skip the title get displayed in the beginning of fsck command output.
    > ```
    > # fsck -TAR
    > e2fsck 1.42 (29-Nov-2011)
    > /dev/sda6 is mounted.  e2fsck: Cannot continue, aborting.
    > dosfsck 3.0.12, 29 Oct 2011, FAT32, LFN
    > /dev/sda7: 8 files, 50/1463400 clusters
    > ```
    > 
    > Note that the title is something like "fsck from util-linux 2.20.1".
    > 
    > ### 7\. Force a Filesystem Check Even if it's Clean using Option -f
    > 
    > By default fsck tries to skip the clean file system to do a quicker job.
    > ```
    > # fsck /dev/sda6
    > fsck from util-linux 2.20.1
    > e2fsck 1.42 (29-Nov-2011)
    > /dev/sda6: clean, 95/2240224 files, 3793503/4476416 blocks
    > ```
    > 
    > You can force it to check the file system using -f as shown below.
    > ```
    > # fsck /dev/sda6 -f
    > fsck from util-linux 2.20.1
    > e2fsck 1.42 (29-Nov-2011)
    > Pass 1: Checking inodes, blocks, and sizes
    > Pass 2: Checking directory structure
    > Pass 3: Checking directory connectivity
    > Pass 4: Checking reference counts
    > Pass 5: Checking group summary information
    > /dev/sda6: 95/2240224 files (7.4% non-contiguous), 3793503/4476416 blocks
    > ```
    > 
    > ### 8\. Attempt to Fix Detected Problems Automatically using Option -y
    > 
    > In the following example, /dev/sda6 partition is corrupted as shown below.
    > ```
    > # mount /dev/sda6 /mydata
    > # cd /mydata
    > # ls -li
    > ls: cannot access test: Input/output error
    > total 72
    >   49061 -rw-r--r--  1 root root     8 Aug 21 21:50 1
    >   49058 -rw-r--r--  1 root root 36864 Aug 21 21:24 file_with_holes
    >   49057 -rw-r--r--  1 root root  8192 Aug 21 21:23 fwh
    >      11 drwxr-xr-x  2 root root 49152 Aug 19 00:29 lost+found
    > 2060353 ?rwSr-S-wT 16 root root  4096 Aug 21 21:11 Movies
    >       ? -?????????  ? ?    ?        ?            ? test
    > ```
    > As seen above, the directory **Movies** and a file **test** attributes are invalid.
    > 
    > In the following example, -y will pass "yes" to all the questions to fix the detected corruption automatically.
    > ```
    > # fsck -y /dev/sda6
    > fsck from util-linux 2.20.1
    > e2fsck 1.42 (29-Nov-2011)
    > /dev/sda6 contains a file system with errors, check forced.
    > Pass 1: Checking inodes, blocks, and sizes
    > Inode 2060353 is a unknown file type with mode 0137642 but it looks
    > like it is really a directory.
    > Fix? yes
    > 
    > Pass 2: Checking directory structure
    > Entry 'test' in / (2) has deleted/unused inode 49059.  Clear? yes
    > 
    > Pass 3: Checking directory connectivity
    > Pass 4: Checking reference counts
    > Pass 5: Checking group summary information
    > 
    > /dev/sda6: ***** FILE SYSTEM WAS MODIFIED *****
    > /dev/sda6: 96/2240224 files (7.3% non-contiguous), 3793508/4476416 blocks
    > ```
    > 
    > ### 9\. Avoid Repair, but Report Problems to Stdout using Option -n
    > 
    > It is possible to print such detected problems into stdout without repairing the filesystem using fsck -n option.
    > 
    > First, you could notice/see the problem in partition /dev/sda6 that the Movies directory (and fwh file) doesn't have valid attribute details.
    > ```
    > # mount /dev/sda6 /mydata
    > # cd /mydata
    > # ls -lrt
    > total 64
    > drwxr-xr-x  2 root root 49152 Aug 19 00:29 lost+found
    > ?--xrwx-wx 16 root root  4096 Aug 21 21:11 Movies
    > ?-----x-wx  1 root root  8192 Aug 21 21:23 fwh
    > -rw-r--r--  1 root root 36864 Aug 21 21:24 file_with_holes
    > -rw-r--r--  1 root root     8 Aug 21 21:50 1
    > ```
    > 
    > The above problem in the specific partition displayed in stdout without doing any fix on it as follows,
    > 
    > The following fsck example displays the problem in the stdout without fixing it. (partial output is shown below).
    > ```
    > # fsck -n /dev/sda6
    > fsck from util-linux 2.20.1
    > e2fsck 1.42 (29-Nov-2011)
    > /dev/sda6 contains a file system with errors, check forced.
    > Pass 1: Checking inodes, blocks, and sizes
    > Inode 2060353 is a unknown file type with mode 0173 but it looks
    > like it is really a directory.
    > Fix? no
    > Inode 2060353, i_blocks is 8, should be 0.  Fix? no
    > 
    > Pass 2: Checking directory structure
    > Inode 2060353 (/Movies) has invalid mode (0173).
    > Clear? no
    > 
    > Inode 49057 (/fwh) has invalid mode (013).
    > Clear? no
    > 
    > Entry 'fwh' in / (2) has an incorrect filetype (was 1, should be 0).
    > Fix? no
    > 
    > Pass 3: Checking directory connectivity
    > Unconnected directory inode 65409 (???)
    > Connect to /lost+found? no
    > 
    > '..' in ... (65409) is ??? (2060353), should be  (0).
    > Fix? no
    > 
    > Unconnected directory inode 2076736 (???)
    > Connect to /lost+found? no
    > 
    > Pass 4: Checking reference counts
    > Inode 2 ref count is 4, should be 3.  Fix? no
    > 
    > Inode 65409 ref count is 3, should be 2.  Fix? no
    > 
    > Inode 2060353 ref count is 16, should be 15.  Fix? no
    > 
    > Unattached inode 2060354
    > Connect to /lost+found? no
    > 
    > Pass 5: Checking group summary information
    > Block bitmap differences:  -(164356--164357) -4149248
    > Fix? no
    > 
    > Directories count wrong for group #126 (1, counted=0).
    > Fix? no
    > 
    > /dev/sda6: ********** WARNING: Filesystem still has errors **********
    > 
    > /dev/sda6: 96/2240224 files (7.3% non-contiguous), 3793508/4476416 blocks
    > ```
    > 
    > ### 10\. Automatically Repair the Damaged Portions using Option -a
    > 
    > In order to repair the damaged portion automatically ( without any user interaction ), use the option -a as shown below.
    > ```
    > # fsck -a -AR
    > ```
    > 
    > The option -a is same as -p in e2fsck utility. It cause e2fsck to fix any detected problems that has to be safely fixed without user interaction.
    > 
    > In case when fsck requires administrator's attention, it simply exits with error code 4 before printing the description of the problem.
    > ```
    > # fsck -a /dev/sda6
    > fsck from util-linux 2.20.1
    > /dev/sda6 contains a file system with errors, check forced.
    > /dev/sda6: Inode 2060353 is a unknown file type with mode 0173 but it looks
    > like it is really a directory.
    > 
    > /dev/sda6: UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY.
    > 	(i.e., without -a or -p options)
    > 
    > # echo $?
    > 4
    > ```
    > 
    > As you remember, fsck -y option can be used here to fix the above issue automatically.
    > ```
    > # fsck -y /dev/sda6
    > fsck from util-linux 2.20.1
    > e2fsck 1.42 (29-Nov-2011)
    > /dev/sda6 contains a file system with errors, check forced.
    > Pass 1: Checking inodes, blocks, and sizes
    > Inode 2060353 is a unknown file type with mode 0173 but it looks
    > like it is really a directory.
    > Fix? yes
    > 
    > Pass 2: Checking directory structure
    > Inode 49057 (/fwh) has invalid mode (013).
    > Clear? yes
    > 
    > Pass 3: Checking directory connectivity
    > Pass 4: Checking reference counts
    > Pass 5: Checking group summary information
    > Block bitmap differences:  -(164356--164357)
    > Fix? yes
    > 
    > Free blocks count wrong for group #5 (0, counted=2).
    > Fix? yes
    > 
    > Free blocks count wrong (682908, counted=682910).
    > Fix? yes
    > 
    > /dev/sda6: ***** FILE SYSTEM WAS MODIFIED *****
    > /dev/sda6: 95/2240224 files (7.4% non-contiguous), 3793506/4476416 blocks
    > ```
    > 




## fsck with autocorrect

- [10.04 - Force fsck.ext4 on reboot, but really "forceful" - Ask Ubuntu](https://askubuntu.com/questions/14740/force-fsck-ext4-on-reboot-but-really-forceful)

    > I know this is a really old thread, but I recently had to solve this problem so I wanted to post how to force the OS to fix problems found with fsck during bootup (for 12.04).
    > 
    > You do need to run the command `sudo touch /forcefsck`. This will cause it to perform an fsck on the next boot. You can see the results of the fsck in /var/log/boot.log.
    > 
    > However, you are not guaranteed that fsck will fix anything it finds. To do this, you would need to edit the file /etc/default/rcS. There is a line at the end of that file:
    > 
    > ```
    > FSCKFIX=no
    > 
    > ```
    > 
    > This needs to be changed to the following:
    > 
    > ```
    > FSCKFIX=yes
    > 
    > ```
    > 
    > This will have the same effect as running the fsck with the -y option which will force all fixes that are possible to be implemented and it will not ask for user interaction.
    > 
    > This will allow you to run the fsck like the OP was asking to without having to resort to booting from a live disk which isn't always possible especially if you are on a remote system.

- [init - How can I make fsck run non-interactively at boot time? - Ask Ubuntu](https://askubuntu.com/questions/151025/how-can-i-make-fsck-run-non-interactively-at-boot-time)

    > The setting I am looking for is in [/etc/default/rcS](http://manpages.ubuntu.com/manpages/precise/man5/rcS.5.html), `FSCKFIX=yes`. This means "automatically repair filesystems with inconsistencies during boot" and causes fsck to run with the `-y` flag. It was set to `no` in both of my Ubuntu systems.
    > 
    > Even when set to `no`, the boot time fsck is still somewhat noninteractive. mountall runs fsck with `-a`, a synonym for `-p`, which means "automatically fix any filesystem problems that can be safely fixed without human intervention". Apparently `-p` drops to interactive mode if there are unsafe fixes to be made. To run fully automatically, you need `-y` or `FSCKFIX=yes`.
    > 
    > ---
    > 
    > For Ubuntu 15,16,17+ the FSCKFIX value setting is located in `/lib/init/vars.sh`
    > 
    > Can use command `grep -r FSCKFIX * 2>/dev/null` to find it.


- [Pi3: /etc/default/rcS --> FSCKFIX=yes? - Raspberry Pi Forums](https://www.raspberrypi.org/forums/viewtopic.php?t=144279)

    > Nothing can repair data corruption if it has happened. fsck simply makes filesystem metadata consistent. (So, directories cannot be their own parent, no two files have the same name, all space either belongs to exactly one file or is free; things like that.) You may still lose data, including stuff that is needed for boot.
    > 
    > FSCKFIX does not control whether fsck runs, but whether it "fixes" *everything* without user interaction. With "no", it will abort and give you a root shell if the errors are too serious. If your goal is to manually recover as much data as possible, you might want that. If you have backups, you might prefer to let fsck try its best.
    > 
    > In the Foundation's spindle-era images, FSCKFIX=yes was actually the default. In recent images, /boot/cmdline.txt has "fsck.repair=yes". I believe that takes precedence and is basically equivalent. If you want "no", remove the stanza from /boot/cmdline.txt as well.
    > 


## fsck on next reboot(tunefs/fsck.mode=force/fsck.repair/FSCKFIX=yes)

- [Bug #513644 “Does not log fsck invocations in /var/log/fsck/” : Bugs : mountall package : Ubuntu](https://bugs.launchpad.net/ubuntu/+source/mountall/+bug/513644)

    > Also as per Adam, on 16.04 the /forcefsck functionality is not available, so the recommended method of triggering a filesystem check on boot is to use tune2fs, as this method will work on 12.04, 14.04 and 16.04:
    > ```
    > sudo tune2fs -CCOUNT DEVICE
    > ```
    > 
    > Setting the count to 1 will cause an fsck on each reboot, while -1 disables the scan.


- [linux - What should I do to force the root filesystem check (and optionally a fix) at boot? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/400851/what-should-i-do-to-force-the-root-filesystem-check-and-optionally-a-fix-at-bo/400927#400927)

    > `ext4` filesystem check during boot
    > ===================================
    > 
    > Tested on OS: Linux Mint 18.x in a Virtual Machine
    > 
    > Basic information
    > =================
    > 
    > `/etc/fstab` has the `fsck` order as the last (6th) column, for instance:
    > 
    > ```
    > <file system>    <mount point>    <type>    <options>    <dump>    <fsck>
    > UUID=2fbcf5e7-1234-abcd-88e8-a72d15580c99 / ext4 errors=remount-ro 0 1
    > 
    > ```
    > 
    > * * * * *
    > 
    > `FSCKFIX=yes` variable in `/etc/default/rcS`
    > 
    > This will change the fsck to auto fix, but *not* force a fsck check.
    > 
    > From `man rcS`:
    > 
    > > ```
    > > FSCKFIX
    > >     When  the  root  and all other file systems are checked, fsck is
    > >     invoked with the -a option which means "autorepair".   If  there
    > >     are  major  inconsistencies then the fsck process will bail out.
    > >     The system will print a  message  asking  the  administrator  to
    > >     repair  the  file  system manually and will present a root shell
    > >     prompt (actually a sulogin prompt) on the console.  Setting this
    > >     option  to  yes  causes  the fsck commands to be run with the -y
    > >     option instead of the -a option.  This will tell fsck always  to
    > >     repair the file systems without asking for permission.
    > >
    > > ```
    > 
    > * * * * *
    > 
    > From `man tune2fs`
    > 
    > > ```
    > > If you are using journaling on your filesystem, your filesystem
    > > will never be marked dirty, so it will not normally be checked.
    > >
    > > ```
    > 
    > * * * * *
    > 
    > Start with
    > ==========
    > 
    > Setting the following
    > 
    > > ```
    > > FSCKFIX=yes
    > >
    > > ```
    > 
    > in the file
    > 
    > ```
    > /etc/default/rcS
    > 
    > ```
    > 
    > Check and note last time fs was checked:
    > 
    > ```
    > sudo tune2fs -l /dev/sda1 | grep "Last checked"
    > 
    > ```
    > 
    > * * * * *
    > 
    > These two options did NOT work
    > ==============================
    > 
    > 1.  **Passing `-F` (force `fsck` on reboot) argument to `shutdown`:**
    > 
    >     ```
    >     shutdown -rF now
    > 
    >     ```
    > 
    >     Nope; see: `man shutdown`.
    > 
    > 2.  **Adding the `/forcefsck` empty file with:**
    > 
    >     ```
    >     touch /forcefsck
    > 
    >     ```
    > 
    >     These scripts seem to use this:
    > 
    >     ```
    >     /etc/init.d/checkfs.sh
    >     /etc/init.d/checkroot.sh
    > 
    >     ```
    > 
    >     did **NOT** work on reboot, but the file was deleted.
    > 
    >     *Verified by:*
    > 
    >     ```
    >     sudo tune2fs -l /dev/sda1 | grep "Last checked"
    >     sudo less /var/log/fsck/checkfs
    >     sudo less /var/log/fsck/checkroot
    > 
    >     ```
    > 
    >     These seem to be the logs for the `init` scripts.
    > 
    > **I repeat, these two options did NOT work!**
    > 
    > * * * * *
    > 
    > Both of these methods DID work
    > ==============================
    > 
    > 1.  **[systemd-fsck](https://www.freedesktop.org/software/systemd/man/systemd-fsck@.service.html) kernel boot switches**
    > 
    >     Editing the main `grub` configuration file:
    > 
    >     ```
    >     sudoedit /etc/default/grub
    > 
    >     ```
    > 
    >     > ```
    >     > GRUB_CMDLINE_LINUX="fsck.mode=force"
    >     >
    >     > ```
    > 
    >     ```
    >     sudo update-grub
    >     sudo reboot
    > 
    >     ```
    > 
    >     This did do a file system check as verified with:
    > 
    >     ```
    >     sudo tune2fs -l /dev/sda1 | grep "Last checked"
    > 
    >     ```
    > 
    >     Note: This **DID** a check, but to force a fix too, you need to specify `fsck.repair="preen"`, or `fsck.repair="yes"`.
    > 
    > 2.  **Using `tune2fs` to set the number of file system mounts before doing a `fsck`, `man tune2fs`**
    > 
    >     > ```
    >     > tune2fs' info is kept in the file system superblock
    >     >
    >     > ```
    > 
    >     `-c` switch sets the number of times to mount the fs before checking the fs.
    > 
    >     ```
    >     sudo tune2fs -c 1 /dev/sda1
    > 
    >     ```
    > 
    >     Verify with:
    > 
    >     ```
    >     sudo tune2fs -l /dev/sda1
    > 
    >     ```
    > 
    >     This **DID** work as verified with:
    > 
    >     ```
    >     sudo tune2fs -l /dev/sda1 | grep "Last checked"
    > 
    >     ```
    > 
    > * * * * *
    > 
    > Summary
    > =======
    > 
    > To force a `fsck` on every boot on Linux Mint 18.x, use either `tune2fs`, or `fsck.mode=force`, with optional `fsck.repair=preen` / `fsck.repair=yes`, the kernel command line switches.


- [Linux Force fsck on the Next Reboot or Boot Sequence - nixCraft](https://www.cyberciti.biz/faq/linux-force-fsck-on-the-next-reboot-or-boot-sequence/)

    > A note about systemd based systems
    > ----------------------------------
    > 
    > The above mentioned solution only works with the old SysVinit and early versions of Upstart. It won't work with systemd. [systemd-fsck understands](https://www.freedesktop.org/software/systemd/man/systemd-fsck@.service.html) one kernel command line parameter:
    > 
    > > **fsck.mode=**\
    > > One of "auto", "force", "skip". Controls the mode of operation. The default is "auto", and ensures that file system checks are done when the file system checker deems them necessary. "force" unconditionally results in full file system checks. "skip" skips any file system checks.
    > >
    > > **fsck.repair=**\
    > > One of "preen", "yes", "no". Controls the mode of operation. The default is " preen", and will automatically repair problems that can be safely fixed. "yes " will answer yes to all questions by fsck and "no" will answer no to all questions.

- [[all variants] How to implement automatic disk check on next reboot on dirty shutdown](https://ubuntuforums.org/showthread.php?t=2367175)

    > /forcefsck no longer works as it was a SysV thing (and early upstart) - ubuntu is Systemd these days.
    > 
    > If you add
    > 
    > ```
    > fsck.mode=auto
    > ```
    > to your kernel line the system will fsck as and when required - no other scripting required.

- [How to automatically force fsck disks after crash in `systemd`? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/50762/how-to-automatically-force-fsck-disks-after-crash-in-systemd)

    > For example with Grub: edit `/etc/default/grub`, then append `fsck.mode=force` to the value of `GRUB_CMDLINE_LINUX_DEFAULT`. Then run `update-grub` and `reboot`. -- [Yvan](https://unix.stackexchange.com/users/113214/yvan "101 reputation") [Sep 6 '16 at 8:38](https://unix.stackexchange.com/questions/50762/how-to-automatically-force-fsck-disks-after-crash-in-systemd#comment541716_50772)

- [boot - Automatically force fsck -fy when encountering "UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY." - Ask Ubuntu](https://askubuntu.com/questions/1006417/automatically-force-fsck-fy-when-encountering-unexpected-inconsistency-run-fs)

    > *Let me preface this with a disclaimer that if you have regular issues with unclean filesystems, even though you shutdown your system cleanly, you have grave underlying problems and its possible [fsck can do more harm than good](https://serverfault.com/a/786659/291077) !*
    > 
    > AFAIK there is no mechanism for an automatic fsck only if inconsistencies are found.
    > 
    > However, you do an fsck at *every boot* with some kernel parameters.
    > 
    > ```
    > sudo nano /etc/default/grub
    > 
    > ```
    > 
    > find the line that says
    > 
    > ```
    > GRUB_CMDLINE_LINUX_DEFAULT
    > 
    > ```
    > 
    > and add
    > 
    > ```
    > fsck.mode=force  fsck.repair=yes
    > 
    > ```
    > 
    > to the existing things there.
    > 
    > *yes* here should do the same as your `FSCKFIX=yes` in `/etc/default/rcS` or a manual `fsck -fy`. Personally I think `preen` would be safer, but then again it would hang on startup if the disk needs some more fixes that `fsck` does not deem "*safe* " and wants user interaction.
    > 
    > run
    > 
    > ```
    > sudo update-grub
    > 
    > ```
    > 
    > to update grup and verify it with
    > 
    > ```
    > grep fsck /boot/grub/grub.cfg
    > 
    > ```
    > 
    > or have a look with an editor in `/boot/grub/grub.cfg`
    > 
    > If you then reboot, the filesystem should be checked, you can verify the last time it was checked (should be your boot time) with
    > 
    > ```
    > sudo dumpe2fs -h /dev/your/device | grep checked
    > dumpe2fs 1.43.5 (04-Aug-2017)
    > Last checked:             Sun Feb 18 08:53:31 2018
    > 
    > ```
    > 

## Where are fsck results logged at boot time

- [logging - Where are fsck results logged at boot time, after /forcefsck? - Ask Ubuntu](https://askubuntu.com/questions/112907/where-are-fsck-results-logged-at-boot-time-after-forcefsck/603027#603027)

    > **For Ubuntu 16.04**
    > 
    > The command `journalctl -b --no-pager | grep systemd-fsck`
    > 
    > reports non root partition file system checks.similar to this:
    > 
    > ```
    > Mar 22 15:06:26 64bitUbuntu systemd-fsck[750]: /dev/sdb1: clean, 146223/121454592 files, 356711795/485818368 blocks
    > 
    > ```
    > 
    > For root partition checks at boot issue the command `more /var/log/boot.log`
    > 
    > Provides results similar to this:
    > 
    > ```
    > /dev/sda2: clean, 349091/1954064 files, 2379983/7814912 blocks
    > 
    > ```
    > 
    > ---
    > 
    > find nvme partition:
    > ```
    > sudo grep nvme /var/log/boot.log
    > ```
    > 
    > results:
    > ```
    > /dev/nvme0n1p2 has been mounted 1 times without being checked, check forced.
    > /dev/nvme0n1p2: Inode 9971 extent tree (at level 1) could be shorter.  IGNORED.
    > Inode 5768686 extent tree (at level 2) could be narrower.  IGNORED.                             
    > /dev/nvme0n1p2: 1009579/15597568 files (0.4% non-contiguous), 47917105/62383360 blocks
    > 
    > ```
    > [name=Ya-Lun Li]

- [16.04 - Where are the logs of fsck done via the recovery mode at? - Ask Ubuntu](https://askubuntu.com/questions/781154/where-are-the-logs-of-fsck-done-via-the-recovery-mode-at)

    > There won't be any, if there is filesystem damage at boot, there won't be any filesystem mounted to write the log in yet. Writing a log can make any damage worse.
    > 


## When is fsck dangerous

- [linux - When is fsck dangerous? - Server Fault](https://serverfault.com/questions/786648/when-is-fsck-dangerous/786659#786659)

    > `fsck` definitely causes more harm than good if the underlying hardware is somehow damaged; bad CPU, bad RAM, a dying hard drive, disk controller gone bad... in those cases more corruption is inevitable.
    > 
    > If in doubt, it's a good idea to just to take an image of the corrupted disk with `dd_rescue` or some other tool, and then see if you can successfully fix that image. That way you still have the original setup available.
    > 
    > ---
    > 
    > First of all, you need to understand that with modern (journalized) filesystems, a system crash will not corrupt the filesystem and no fsck will be required at boot time.
    > 
    > Ext3, Ext4, ZFS, btrfs, xfs and all modern FS are 100% consistent after a crash or system reset.
    > 
    > Non journalized FS like ext2 or vfat are a big NOGO for a system rootfs.
    > 
    > Now, if your system requires a fsck at boot time, you should ask yourself: what was the reason for this in the first place?
    > 
    > You should investigate your kernel logs afterwards to find out, when and what did happen. You should also go back in time in the logs to find since when the error did start. You should check your disks with smartctl. Etc... If you need a fsck on a journalized fs, it is virtually certain that your hardware is failing, assuming the fs was not damaged by an admin (with block-level tools like dd) or by a bug.
    > 
    > So it is silly to use fsck to "fix" the problem without investigating and fixing the root cause (by replacing/upgrading the faulty hardware/firmware/software).
    > 
    > Doing a fsck, completing the boot and being happy is naive to say the least. Stating "I've had fsck work a greater percentage of the time than what you quote" is making me wondering what you mean with "fsck work". fsck may have brought back your fs to a consistent state by loosing some files and data in the process... Did you compare with a backup? Many people loose files or get file data corruption without noticing...




## fix "sudo: unable to open ... Read-only file system"

- [filesystem - How to fix "sudo: unable to open ... Read-only file system"? - Ask Ubuntu](https://askubuntu.com/questions/197459/how-to-fix-sudo-unable-to-open-read-only-file-system/1073542#1073542)


    > The answer by hexafraction didn't work for me. Every time I tried executing `sudo fsck -Af -M` it just showed
    > 
    > ```sh
    > $ sudo fsck -Af -M
    > fsck from util-linux 2.20.1
    > 
    > ```
    > 
    > and nothing else. No error or anything. For me, booting into a live disc and executing this worked -
    > 
    > ```sh
    > sudo fsck.ext4 -f /dev/sda1
    > 
    > ```
    > 
    > Provided the partition in question `/dev/sda1` was an ext4 filesystem.
    > 
    > ---
    > 
    > If you were in situations that can not use live disc, e.g. you are remotely ssh into your system, you can still using the command that @Bibhas had answered:
    > 
    > ```sh
    > sudo fsck.ext4 -f /current/filesystem/mount/point
    > 
    > ```
    > for example:
    > ```
    > sudo fsck.ext4 -f /dev/nvme0n1p2
    > ```
    > 
    > It will prompt for fixing your filesystem error. You also need to reboot your system remotely.
    > [name=Ya-Lun Li]


# list of filesystems

- [filesystems - What is a bind mount? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/198590/what-is-a-bind-mount/198591)

    > Going beyond bind mounts
    > ------------------------
    > 
    > Bind mounts provide a view of a directory tree at a different location. They expose the same files, possibly with different mount options and (with bindfs) different ownership and permissions. Filesystems that present an altered view of a directory tree are called *overlay filesystems* or *stackable filesystems*. There are many other overlay filesystems that perform more advanced transformations. Here are a few common ones. If your desired use case is not covered here, check the [repository of FUSE filesystems](http://sourceforge.net/p/fuse/wiki/FileSystems/).
    > 
    > -   [loggedfs](http://sourceforge.net/projects/loggedfs/) --- log all filesystem access for debugging or monitoring purposes ([configuration file syntax](https://unix.stackexchange.com/questions/13794/loggedfs-configuration-file-syntax/13797#13797), [Is it possible to find out what program or script created a given file?](https://unix.stackexchange.com/questions/6068/is-it-possible-to-find-out-what-program-or-script-created-a-given-file/6080#6080), [List the files accessed by a program](https://unix.stackexchange.com/questions/18844/list-the-files-accessed-by-a-program/18872#18872))
    > 
    > ### Filter visible files
    > 
    > -   [clamfs](http://clamfs.sourceforge.net/) --- run files through a virus scanner when they are read
    > -   [filterfs](http://filterfs.sourceforge.net/) --- hide parts of a filesystem
    > -   [rofs](https://github.com/cognusion/fuse-rofs) --- a read-only view. Similar to `bindfs -r`, just a little more lightweight.
    > -   [Union mounts](http://en.wikipedia.org/wiki/Union_mount) --- present multiple filesystems (called *branches*) under a single directory: if `tree1` contains `foo` and `tree2` contains `bar` then their union view contains both `foo` and `bar`. New files are written to a specific branch, or to a branch chosen according to more complex rules. There are several implementations of this concept, including:
    > 
    >     -   [aufs](http://aufs.sourceforge.net/) --- Linux kernel implementation
    >     -   [funionfs](http://funionfs.apiou.org/?lng=en) --- FUSE implementation
    >     -   [mhddfs](http://svn.uvw.ru/mhddfs/trunk/README) --- FUSE, write files to a branch based on free space
    >     -   [overlay](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/filesystems/overlayfs.txt) --- Linux kernel implementation
    >     -   [unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) --- FUSE, with caching and copy-on-write features
    > 
    > ### Modify file names and metadata
    > 
    > -   [ciopfs](http://brain-dump.org/projects/ciopfs/) --- case-insensitive filenames (can be useful to mount Windows filesystems)
    > -   [convmvfs](http://fuse-convmvfs.sourceforge.net/) --- convert filenames between character sets ([example](https://unix.stackexchange.com/questions/67232/same-file-different-filename-due-to-encoding-problem/67273#67273))
    > -   [posixovl](http://sourceforge.net/projects/posixovl/) --- store Unix filenames and other metadata (permissions, ownership, ...) on more restricted filesystems such as VFAT ([example](https://unix.stackexchange.com/questions/108890/what-is-the-best-way-to-synchronize-files-to-a-vfat-partition/108937#108937))
    > 
    > ### View altered file contents
    > 
    > -   [avfs](http://avf.sourceforge.net/) --- for each archive file, present a directory with the content of the archive ([example](https://unix.stackexchange.com/questions/13749/how-do-i-recursively-grep-through-compressed-archives/13798#13798), [more examples](https://unix.stackexchange.com/search?tab=votes&q=avfs%20is%3aanswer)). There are also many [FUSE filesystems that expose specific archives as directories](http://sourceforge.net/p/fuse/wiki/ArchiveFileSystems/).
    > -   [fuseflt](http://users.softlab.ntua.gr/~thkala/projects/fuseflt/) --- run files through a pipeline when reading them, e.g. to recode text files or media files ([example](https://unix.stackexchange.com/questions/33574/how-to-use-grep-ack-with-files-in-arbitrary-encoding/33580#33580))
    > -   [lzopfs](https://github.com/vasi/lzopfs) --- transparent decompression of compressed files
    > -   [mp3fs](http://khenriks.github.io/mp3fs/) --- transcode FLAC files to MP3 when they are read ([example](https://unix.stackexchange.com/questions/37701/how-to-encode-huge-flac-files-into-mp3-and-other-files-like-aac/115695#115695))
    > -   [scriptfs](https://code.google.com/p/scriptfs/) --- execute scripts to serve content (a sort of local CGI) ([example](https://unix.stackexchange.com/questions/181673/using-process-substitution-to-trick-programs-expecting-files-with-specific-exte/181680#181680))
    > 
    > ### Modify the way content is stored
    > 
    > -   [chironfs](https://code.google.com/p/chironfs/) --- replicate files onto multiple underlying storage ([RAID-1 at the directory tree level](https://unix.stackexchange.com/questions/14544/raid-1-lvm-at-the-level-of-directories-aka-mknodding-a-directory))
    > -   [copyfs](http://n0x.org/copyfs) --- keep copies of all versions of the files
    > -   [encfs](http://www.arg0.net/encfs) --- encrypt files
    > -   [pcachefs](https://code.google.com/p/pcachefs/) --- on-disk cache layer for slow remote filesystems
    > -   [simplecowfs](https://github.com/vi/simplecowfs) --- store changes via the provided view in memory, leaving the original files intact
    > -   [wayback](http://wayback.sourceforge.net/) --- keep copies of all versions of the files
    > 


## ext4

- [defragment - Do ext4 filesystems need to be defragmented? - Super User](https://superuser.com/questions/536788/do-ext4-filesystems-need-to-be-defragmented)

    > > Do `ext4` filesystems need to be defragmented?
    > 
    > Yes (but very rarely).
    > 
    > > If so, how do I defragment them?
    > 
    > Copy all the files off the partition, erase the files from the partition, then copy the files back onto the partition. The file system will intelligently allocate the files as you copy them back onto the disk.
    > 
    > > If not, could you post a simple explanation of why they do not need to be defragmented?
    > 
    > `ext4` acts in a more intelligent way than merely adding new files into the next available space. Instead of placing multiple files near each other on the hard disk, Linux file systems scatter different files all over the disk, leaving a large amount of free space between them. When a file is edited and needs to grow, there's usually plenty of free space for the file to grow into. If fragmentation does occur, the file system will attempt to move the files around to reduce fragmentation in normal use, without the need for a defragmentation utility.
    > 
    > Thanks to a Comment by @Green Reaper my attention has been drawn to [e4defrag](https://askubuntu.com/questions/265932/is-it-safe-to-defrag-ext4-file-system-using-e4defrag).
    > 
    > ---
    > 
    > If you have an ext4 file system created with the `extent` option (it's the default in most recent distros), you can check fragmentation on it with `e4defrag -c /path/to/check`, and defragment it without umounting with `e4defrag /path/to/check`. But if you have enough free space you won't need to do so. -- [gerlos](https://superuser.com/users/85364/gerlos "403 reputation")



## archivemount

- [unix - Is it possible to mount a .tar file? - Super User](https://superuser.com/questions/265772/is-it-possible-to-mount-a-tar-file)

    > In fact, it seems that at least with newer Ubuntu^1^ versions it is possible to simply `apt-get install archivemount`. Then you can mount your archive as
    > 
    > ```
    > archivemount [archive file] [mount point]
    > 
    > ```

## squashfs

- [falconindy/SquashFu: A backup program employing the use of SquashFS, Aufs and Rsync](https://github.com/falconindy/SquashFu)

- [squashfs wo compression = speed up?](https://forums.fedoraforum.org/showthread.php?284366-squashfs-wo-compression-speed-up)

    > mksquashfs has several parameters to compress/not-compress various parts of the filesystem.
    > 
    > **-noI do not compress inode table\
    > -noD do not compress data blocks\
    > -noF do not compress fragment blocks\
    > -noX do not compress extended attributes**\
    > There are also several compression algorithms to choose from.
    > 
    > There is of course no advantage in using squashfs w/o compression, but yes it works as expected.
    > 
    > Btrfs supports compression too, fyi.
    > 
    > When you compress files, this reduces the amount of block I/O and increases the amount of data that appears in memory buffers, so it can make the disk I/O much less and therefore faster. However the negative side is that you must use CPU resource to uncompress on reads and compress on writes and that takes some time. Whether this is a net plus of minus depends on the application, the disk speed, the CPU performance and such.
    > 

- [mount - Faster alternative to ArchiveMount? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/24032/faster-alternative-to-archivemount/83994)

    > You could also create a compressed squashfs image
    > 
    > ```
    > mksquashfs /etc squashfs.img -comp xz
    > mkdir img
    > mount -o squashfs,ro squashfs.img img
    > 
    > ```
    > 
    > ---
    > 
    > To get random access to a compressed file, you could also use pixz.


- [SquashFS HOWTO](http://www.tldp.org/HOWTO/html_single/SquashFS-HOWTO/)

    > 4.4. Making it writeble
    > -----------------------
    > 
    > As mentioned, another interesting use for **SquashFS** is with **Unionfs** filesystem, which provides *copy-on-write* semantics for the read-only file systems, enahancing the possibilities. (For unionfs you can look at <http://www.filesystems.org/project-unionfs.html>)
    > 
    > Just to make an example, you may want to make your /home/user squashed, to compress and backup your files without losing the possibility to apply changes or writing new files.
    > 
    > Create the `ro.fs` squashed file system and the `rw.fs` dir.
    > 
    > 
    > ```shell
    > bash# mksquashfs /home/user1 ro.fs
    > bash# mkdir /home/rw.fs
    > ```
    > 
    > 
    > Mount the squashed ro.fs file system using the loopback device
    > 
    > 
    > ```shell
    > bash# mount -t squashfs ro.fs /mnt -o loop
    > ```
    > 
    > mount the unionfs file system, that makes `/mnt` and `/home/rw.fs` apparently merged under `/home/user1` location.
    > 
    > 
    > ```shell
    > bash# cd /home
    > bash# mount -t unionfs -o dirs=rw.fs=rw:/mnt=ro unionfs user1
    > ```
    > 
    > As you can see, now you can create new files in /home/user1.
    > 
    > 
    > ```shell
    > bash# cd /home/user1
    > bash# touch file1
    > bash# ls
    > ```
    > 
    > umount the unionfs and the squashfs file systems and list the content of /home/user1 and /home/rw.fs dir
    > 
    > 
    > ```shell
    > bash# cd ..
    > bash# umount /home/user1
    > bash# umount /mnt
    > 
    > bash# ls /home/user1
    > bash# ls /home/rw.fs
    > ```
    > 
    > You can see that the new `file1` was created in `/home/rw.fs`
    > 
    > When you want to add the new created files to the *stable* and *compressed* squashed file system, you have to add them to the exsisting one.
    > 
    > 
    > ```shell
    > bash# mksquashfs /home/rw.fs /home/ro.fs
    > ```
    > 
    > 
    > Now, to mount your squashed user home directory at system startup, you can do as follow:
    > 
    > Make squashfs and unionfs modules loaded at boot time.
    > 
    > 
    > ```shell
    > bash# echo squashfs >> /etc/modules
    > bash# echo unionfs >> /etc/modules
    > ```
    > 
    > 
    > Change the owner of the writeble branch to match user1.
    > 
    > 
    > ```shell
    > chown user1 /home/rw.fs
    > ```
    > 
    > 
    > Add these lines to /etc/fstab file to mount squashfs and unionfs at boot time.
    > 
    > 
    > ```shell
    > ...
    > /home/ro.fs  /mnt squashfs loop 0 0
    > unionfs /home/user1 unionfs dirs=/home/rw.fs=rw:/mnt=ro 0 0
    > ```
    > 
    >  
 

- [Embedded Linux: Using Compressed File Systems [LWN.net]](https://lwn.net/Articles/219827/)

    > ### SquashFS
    > 
    > A more recent (and more actively supported, the last updates coming in mid January 2007) compressed file system is [SquashFS](http://squashfs.sourceforge.net/). SquashFS is a kind of successor to CramFS because it aims at the same target audience while providing a similar process for creation and use of the file system. What makes SquashFS an improvement over CramFS is best [stated by Phillip Lougher](http://www.uwsg.iu.edu/hypermail/linux/kernel/0210.3/1550.html) in a linux-kernel mailing list post: "SquashFS basically gives better compression, bigger files/file system support, and more inode information."
    > 
    > Both SquashFS and CramFS use zlib compression. However, CramFS uses a fixed size 4KB block while SquashFS supports from 0.5KB to 64KB. This variable block size allows for much larger file systems under SquashFS, something desirable for complex embedded systems like digital video recorders. Also SquashFS supports compression of both the metadata and block fragments while CramFS does not. And, while CramFS is integrated with the kernel source, SquashFS is not. It comes as a set of kernel patches and the driver module. The CELinux Forum provides [some comparisons of SquashFS against other file systems](http://tree.celinuxforum.org/CelfPubWiki/SquashFsComparisons) (compressed and uncompressed).
    > 
    > ### JFFS2
    > 
    > Another compressed file system is [JFFS2](http://sources.redhat.com/jffs2/), the Journaling Flash file system, version 2. It was designed specifically for use with both NOR and NAND flash devices, and recently received an update via David Woodhouse for the NAND flash memory being used in the OLPC project. JFFS2 is actually a bit more sophisticated than SquashFS because it provides [mechanisms for plugging in different compression algorithms](http://sourceware.org/jffs2/jffs2-html/node3.html), including not using any compression at all. But unlike SquashFS, JFFS2 is integrated into the kernel.
    > 
    > So if you're building an embedded system with flash storage, wouldn't you be better with JFFS2? Not necessarily.
    > 
    > [According to the OpenWRT project](http://wiki.openwrt.org/OpenWrtDocs/Installing#head-3d6480403b294d4c261f360ab9efc82f388a8790), which uses both SquashFS and JFFS2, SquashFS provides better performance than JFFS2. Additionally, at least in the case of the few files that need to be updated for a production version of the project, there is little advantage to using a read/write JFFS2 compressed root file system with respect to the performance hit it incurs vs a read-only SquashFS root file system used with a writable JFFS2 file system for stored files.
    > 
    > JFFS2 is a read/write file system while SquashFS is a read-only file system. A runtime system very often needs to write to its root file system. Imagine making updates to `/etc/hosts`, for example, as you might with a embedded video recorder client trying to access a server backend on a local network. If writing to the file system is required for an embedded system, how could you use SquashFS at all?
    > 
    > Some projects, like OpenWRT, use a hybrid system that uses a read-only root file system mixed with a read/write file system for saving files. In such a hybrid you might use special configurations or modified applications to access read/write file systems, but that doesn't help if you need write access to `/etc/hosts` on a read-only file system. What you need is a method of having parts of the directory structure writable while other parts are read-only. What you need is a stackable file system like UnionFS.
    > 
    > ### Using UnionFS: BusyBox and SquashFS together
    > 
    > UnionFS is a mechanism for mounting two directories from different file systems under the same name. For example, I could have a read-only SquashFS file system and a read/write JFFS2 file system mounted together under the root directory so that the JFFS2 would be `/tmp` and `/etc` while the SquashFS might be everything else.
    > 
    > So how might you use this with a compressed file system and our BusyBox based utilities we created in the last article? First, we build our kernel with SquashFS patches and then build the UnionFS driver as a loadable module. Next, we build BusyBox with all the runtime utilities we need and install the result to a local directory on the build machine, let's call it "`/tmp/busybox`". Next, we package those files into a compressed SquashFS file system:
    > ```
    >     mksquashfs /tmp/busybox /tmp/busybox.sqfs -info
    > ```
    > This command takes the contents of /tmp/busybox and compresses it into a file system image in `/tmp` called `busybox.sqfs`. The `-info` option increases verbosity, printing the filenames, original size and compression ratio as they are processed.
    > 
    > We then create an initramfs with another build of BusyBox that has only minimal utilities - enough to do mounting of the loopback device and loading kernel modules, plus the UnionFS module we built previously (which we manually copy into the directory after we rebuild BusyBox). We might add support for other devices like a CDROM if we store the SquashFS file there or JFFS2 and support for flash memory if we store the SquashFS file there.
    > 
    > At runtime, I need a writable file system to go with my read-only SquashFS file system. I'll use the tmpfs file system which puts all the files I'll write at runtime in virtual memory. In my init script for my initramfs, I add:
    > ```
    >     mkdir /.tmpfs
    >     mount -w -t tmpfs -o size=90% tmpfs /.tmpfs
    >     mkdir /.tmpfs/.overlay
    > ```
    > The overlay directory will be used to store data written by my embedded system.
    > 
    > When you boot your 2.6 kernel, you'll have a BusyBox based initramfs with an init script and your SquashFS file system (or a way to get to that file system via commands in your init script). I'm mounting the `busybox.sqfs` file from the root directory of a CD over the loopback device onto a directory in my initramfs, so I add the following to the init script:
    > ```
    > 	mkdir /.tmpfs/.cdrom
    > 	mount -r -t iso9660 /dev/cdrom /.tmpfs/.cdrom
    > 	losetup /dev/loop0 /.tmpfs/.cdrom/root.sqfs
    > ```
    > Then I can mount the loopback device as a SquashFS file system to another directory I've created in my tmpfs:
    > ```
    > 	mkdir /.tmpfs/.sqfs
    > 	mount -r -t squashfs /dev/loop0 /.tmpfs/.sqfs
    > ```
    > UnionFS mounts multiple directories, in either read-only or read-write mode, onto a single directory. In the init script, I place three directories side by side under a single UnionFS directory:
    > ```
    > 	mount -w -t unionfs -o\
    > 		dirs=/.tmpfs/.overlay=rw:/.tmpfs/.cdrom=ro:/.tmpfs/.sqfs=ro\
    > 		unionfs /.union
    > ```
    > What this does is place all three directory structures, which are referred to as branches under UnionFS, under `/.union`; any conflicting directory names are resolved by taking the first one found, searching the branches left to right. So if there is an `/.tmpfs/.overlay/etc/hosts` (a file we've created at runtime, for example), it takes precedence over `/.tmpfs/.sqfs/etc/hosts`.
    > 
    > With this command, when you write to `/.union` (which later becomes the root directory due to a switch_root in the init script), the writes go to the read/write directory which is on the tmpfs file system. But this writable space is in memory and won't survive reboots. If you need to save data between boots, you could mount a compact flash drive under `/.tmpfs/cf` and use that instead of `/.tmpfs/.overlay` in the previous mount command.
    > 
    > Which directory gets the write if there are two read-write branches? UnionFS uses "copy-up", which causes any attempt to write to a read-only branch to be written to the next read-write branch on its left. Imagine creating a SquashFS for `/etc`, one for `/var` and one for everything else in your root partition. Then if you had 2 compact flashes you could use one for writes to `/etc` and one for writes to `/var` simply by ordering these correctly when you mounted them under the UnionFS file system.

- [mount - Mounting a squashfs filesystem in read-write - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/80305/mounting-a-squashfs-filesystem-in-read-write)

    > Using overlayfs as shown is the best way to have pseudo "squashfs rw" ; It requires however to run on > 4.x kernel (or ubuntu >14.x trusty ).
    > 
    > An alternative solution when one is sitting on older live cd without any overlayfs/aufs/unionfs is to make use of squashfs'own capabilities
    > 
    > important:
    > 
    > ```
    >  without unsquashfs, so this can be done on low storage system
    > 
    > ```
    > 
    > example:
    > 
    > modify squashfs's "usr" directory
    > 
    > ```
    > 1    mount squashfs_file /mnt
    > 
    > 2    cp -a /mnt/usr $HOME  ##modify whatever $HOME/usr as needed
    > 
    > 3    mksquashfs /mnt new_squashfs_file -wildcards -e usr
    > 
    > 4    mksquashfs $HOME/usr new_squashfs_file -keep-as-directory
    > 
    > 5    umount /mnt  # cleanup
    > 
    > ```
    > 
    > line 3 builds temporarily squashfsfile excluding olddir_usr
    > 
    > line 4 appends modified-usr-dir into new_squashfsfile
    > 
    > "
    > 
    > Hope that help
    > 
    > wangj
    > 
    > see here append squashfs [Append to sub-directory inside squashfs file](https://unix.stackexchange.com/questions/375191/append-to-sub-directory-inside-squashfs-file?rq=1)
    > 
    > 

## overlayfs

- [Explaining OverlayFS – What it Does and How it Works | Datalight](https://www.datalight.com/blog/2016/01/27/explaining-overlayfs-%E2%80%93-what-it-does-and-how-it-works/)

    > The simplest case (image below) involves two directories, each containing files and folders. We can think of them as "upper" and "lower," with the rest of Linux and applications positioned above that. The "lower" directory is read-only. File access through the OverlayFS retrieves data from the "upper" directory first, and then defaults to the "lower" directory if a file doesn't exist.
    > 
    > ![Linux OverlayFS allows you to overlay the contents of one directory onto another](https://www.datalight.com/assets/blog-images/OverlayFS_Image.png)
    > 
    > Note that the two original directories ("upper" and "lower") are still directly accessible to the Linux kernel, but this access could be limited by the application.
    > 
    > Modifications to files in the "upper" directory will take place as usual. Any modification to a file from the "lower" folder will create a copy in the upper directory, and that file will be the one modified. This leaves the base files untouched and available through direct access to the "lower" folder.
    > 
    > Interestingly, a second task could copy modified files from the "upper" folder to the "lower" when modifications are complete. In this way, an OverlayFS setup could simulate some of the functionality of transaction points within the Reliance Nitro file system.
    > 
    > A file removed from the OverlayFS directory would directly remove a file from the "upper" directory, and simulate that removal from the "lower" directory by creating what is called a "whiteout" file. This file exists only within the OverlayFS directory, without physically appearing in either the "upper" or "lower" directories. When the OverlayFS is dismounted, this state information will be lost, so care should be taken to reflect any necessary changes to the "lower" directory.
    > 
    > A subdirectory can also be deleted from the "lower" directory, which creates what is known as an "opaque directory" in the OverlayFS directory. Behind the scenes, OverlayFS uses the "trusted" extended attribute class or namespace to record "whiteouts" and "opaque directories." Linux file systems that support the "trusted" namespace can be used for either, and Reliance Nitro is among that set.


- [Linux source code: Documentation/filesystems/overlayfs.txt (v3.18) - Bootlin](https://elixir.bootlin.com/linux/v3.18/source/Documentation/filesystems/overlayfs.txt#L92)

    > whiteouts and opaque directories
    > --------------------------------
    > 
    > In order to support rm and rmdir without changing the lower
    > filesystem, an overlay filesystem needs to record in the upper filesystem
    > that files have been removed.  This is done using whiteouts and opaque
    > directories (non-directories are always opaque).
    > 
    > A whiteout is created as a character device with 0/0 device number.
    > When a whiteout is found in the upper level of a merged directory, any
    > matching name in the lower level is ignored, and the whiteout itself
    > is also hidden.
    > 
    > A directory is made opaque by setting the xattr "trusted.overlay.opaque"
    > to "y".  Where the upper filesystem contains an opaque directory, any
    > directory in the lower filesystem with the same name is ignored.
    > 
    > Non-directories
    > ---------------
    > 
    > Objects that are not directories (files, symlinks, device-special
    > files etc.) are presented either from the upper or lower filesystem as
    > appropriate.  When a file in the lower filesystem is accessed in a way
    > the requires write-access, such as opening for write access, changing
    > some metadata etc., the file is first copied from the lower filesystem
    > to the upper filesystem (copy_up).  Note that creating a hard-link
    > also requires copy_up, though of course creation of a symlink does
    > not.



- [filesystem - How do I use OverlayFS? - Ask Ubuntu](https://askubuntu.com/questions/109413/how-do-i-use-overlayfs)

    > `mount -t overlayfs -o [mount options] overlayfs [mountpoint for merged system]`
    > 
    > Where [mount options] can be:
    > 
    > -   lowerdir=somedir: lowerdir is the directory you're going to lay your new filesystem over, if there are duplicates these get overwritten by (actually, hidden in favor of) upperdir's version
    > -   upperdir=somedir: upperdir is the directory you want to overlay lowerdir with. If duplicate filenames exist in lowerdir and upperdir, upperdir's version takes precedence.
    > -   standard mount options. The only one I've seen from code is ro/rw, but you can experiment.
    > 
    > One thing that confused me at first, so I should probably clarify, is that mounting an overlayfs does not actually mount a filesystem. I was trying to mount a squashfs filesystem using an overlayfs mount, but that's not how it works. You must first mount the (in my case squashfs) filesystem to an arbitrary directory, then use overlayfs to merge the mount point (a directory) and another directory onto a tertiary directory (the overlayfs mount point)(edit: this "tertiary" directory can actually be the upperdir= directory). The tertiary directory is where you will see the merged filesystems (or directory trees - it's flexible).
    > 
    > ### Example 1, overlaying the root filesystem
    > 
    > I've been working on an Ubuntu hybrid boot disk where the base Ubuntu system exists as filesystem.squashfs and I have files called ubuntu.overlay kubuntu.overlay xubuntu.overlay and lubuntu.overlay. The .overlay files are base installs of said systems with the contents of filesystem.squashfs pruned (to save space). Then I modified the init scripts to overlay the correct distro's .overlay file (from a boot parameter) using overlayfs and the above options and it works like a charm!
    > 
    > These are the lines that I used in my init scripts (once all variables are translated):
    > 
    > ```
    > mkdir -p /overlay
    > mount -t squashfs /cdrom/casper/ubuntu.overlay /overlay
    > mount -t overlayfs -o lowerdir=/filesystem.squashfs,upperdir=/overlay overlayfs /
    > 
    > ```
    > 
    > Note that filesystem.squashfs above is a *directory* created by casper, not a file.
    > 
    > These three statements create an `/overlay` directory, mount a squashfs filesystem on the `/overlay` directory and then use OverlayFS to essentially merge the contents of `/overlay` over `/`.
    > 
    > ### Example 2, transparent merging of two directories
    > 
    > In the process of re-building my live USB for each release, I use OverlayFS to save a bunch of time. I start off with a directory called ubuntu-base which contains the contents of the ubuntu-core image which is the most basic install. I will then create directories called ubuntu, kubuntu, lubuntu, and xubuntu.
    > 
    > Then, I use OverlayFS to make the files from the ubuntu-base show up in the individual directories. I would use something like this:
    > 
    > ```
    > mount -t overlayfs -o lowerdir=ubuntu-base,upperdir=kubuntu overlayfs kubuntu
    > 
    > ```
    > 
    > This makes the files from ubuntu-base show up in the kubuntu folder. Then, I can `chroot` to the kubuntu folder and do something like `apt-get install kubuntu-desktop`. Any changes that are made while in this OverlayFS mount will remain in the upper directory, in this case the kubuntu folder. Then, once I unmount the OverlayFS mount the files that really exist in ubuntu-base but are "mirrored" into the kubuntu folder vanish unless they have been changed. This keeps me from having to have multiple copies of the files in ubuntu-base while still being able to use them as if they physically exist in each location.
    > 

## pixz

- [vasi/pixz: Parallel, indexed xz compressor](https://github.com/vasi/pixz)




