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

## show the filesystem type(df, mount, fuseblk, stat, blkid, file, lsblk)

- [How do I find out what filesystem my partitions are using? - Ask Ubuntu](https://askubuntu.com/questions/309047/how-do-i-find-out-what-filesystem-my-partitions-are-using)

    > The command `df -T` will print your filesystem types, as follows:
    > 
    > ```
    > ~$ df -T
    > Filesystem     Type      1K-blocks       Used Available Use% Mounted on
    > /dev/sda1      ext4      190230236  102672812  77894244  57% /
    > udev           devtmpfs    1021128         12   1021116   1% /dev
    > tmpfs          tmpfs        412884        816    412068   1% /run
    > none           tmpfs          5120          0      5120   0% /run/lock
    > none           tmpfs       1032208       2584   1029624   1% /run/shm
    > cgroup         tmpfs       1032208          0   1032208   0% /sys/fs/cgroup
    > /dev/sdb1      fuseblk  1953480700 1141530424 811950276  59% /home/user/storage
    > 
    > ```
    > 
    > [This article](http://www.thegeekstuff.com/2011/04/identify-file-system-type/) sums up several other methods of obtaining this information.
    > 
    > Here are a couple of other examples that I use occasionally:
    > 
    > ```
    > ~$ mount | grep "^/dev"
    > /dev/sda1 on / type ext4 (rw,errors=remount-ro)
    > /dev/sdb1 on /home/user/storage type fuseblk (rw,nosuid,nodev,allow_other,blksize=4096)
    > 
    > ~$ sudo file -sL /dev/sda1
    > /dev/sda1: Linux rev 1.0 ext4 filesystem data, UUID=b53ecdf7-5247-4d65-91a6-be9264c84dea (extents) (large files) (huge files)
    > 
    > ```
    > 
    > ---
    > 
    > You can also use the `lsblk` command like this:
    > 
    > ```
    > $ sudo lsblk -f
    > 
    > NAME        FSTYPE LABEL      MOUNTPOINT
    > sda
    > ├─sda1      ntfs   OS
    > ├─sda2      ntfs   Data
    > ├─sda3
    > ├─sda5      ext4              /
    > └─sda6      swap              [SWAP]
    > 
    > ```
    > 
    > ---
    > 
    > Try `sudo blkid -o list > ~/myFileSytems` on a terminal to found out. Then open the file `myFileSystems` with a text editor (the file should be in your home folder). But I consider that is not your main issue, you might want to provide more info in your question. -- [edwin](https://askubuntu.com/users/159545/edwin "3,280 reputation") [Jun 17 '13 at 1:44](https://askubuntu.com/questions/309047/how-do-i-find-out-what-filesystem-my-partitions-are-using#comment389556_309047)



- [linux - How to show the filesystem type via the terminal? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/53313/how-to-show-the-filesystem-type-via-the-terminal)

    > Yes, according to man `df` you can:
    > 
    > > ```
    > > -T, --print-type      print file system type
    > >
    > > ```
    > 
    > Another way is to use the `mount` command. Without parameters it lists the currently mounted devices, including their file systems.
    > 
    > In case you need to find out only one certain file system, is easier to use the `stat` command's `-f` option instead of parsing out one value from the above mentioned commands' output.
    > 
    > ---
    > 
    > `mount` won't show the file system mounted by fuse, just that it's a `fuseblk` -- [Evan Carroll](https://unix.stackexchange.com/users/3285/evan-carroll "4,826 reputation") [Dec 25 '16 at 21:46](https://unix.stackexchange.com/questions/53313/how-to-show-the-filesystem-type-via-the-terminal#comment585669_53314)
    > 
    > -   `stat -f /var`, for example. -- [CivFan](https://unix.stackexchange.com/users/84008/civfan "242 reputation") [Apr 12 '17 at 16:09](https://unix.stackexchange.com/questions/53313/how-to-show-the-filesystem-type-via-the-terminal#comment634810_53314)
    > 
    > ---
    > 
    > If the filesystem is not mounted (but if it is as well):
    > 
    > ```
    > blkid -o value -s TYPE /dev/block/device
    > 
    > ```
    > 
    > or:
    > 
    > ```
    > file -Ls /dev/block/device
    > 
    > ```
    > 
    > You'll generally need read access to the block device. However, in the case of `blkid`, if it can't read the device, it will try to get that information as cached in `/run/blkid/blkid.tab` or `/etc/blkid.tab`.
    > 
    > ```
    > lsblk -no FSTYPE /dev/block/device
    > 
    > ```
    > 
    > will also give you that information, this time by querying the `udev` data (something like `/run/udev/data/b$major:$minor`).


## find on which physical device a folder is located(df, lvs, mdadm)

- [filesystems - How do I find on which physical device a folder is located? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/11311/how-do-i-find-on-which-physical-device-a-folder-is-located)

    > The `df(1)` command will tell you the device that a file or directory is on:
    > 
    > ```
    > df /work
    > 
    > ```
    > 
    > The first field has the device that the file or directory is on.
    > 
    > e.g.
    > 
    > ```
    > $ df /root
    > Filesystem           1K-blocks      Used Available Use% Mounted on
    > /dev/sda1              1043289    194300    795977  20% /
    > 
    > ```
    > 
    > If the device is a logical volume, you will need to determine which block device(s) the logical volume is on. For this, you can use the `lvs(8)` command:
    > 
    > ```
    > # df /usr
    > Filesystem           1K-blocks      Used Available Use% Mounted on
    > /dev/mapper/orthanc-usr
    >                        8256952   4578000   3259524  59% /usr
    > # lvs -o +devices /dev/mapper/orthanc-usr
    >   LV   VG      Attr   LSize Origin Snap%  Move Log Copy%  Convert Devices
    >   usr  orthanc -wi-ao 8.00g                                       /dev/sda3(0)
    > 
    > ```
    > 
    > The last column tells you that the logical volume `usr` in the volume group `orthanc` (`/dev/mapper/orthanc-usr`) is on the device `/dev/sda3`. Since a volume group can span multiple physical volumes, you may find that you have multiple devices listed.
    > 
    > Another type of logical block device is a md (Multiple Devices, and used to be called meta-disk I think) device, such as `/dev/md2`. To look at the components of a md device, you can use `mdadm --detail` or look in `/proc/mdstat`
    > 
    > ```
    > # df /srv
    > Filesystem           1K-blocks      Used Available Use% Mounted on
    > /dev/md2             956626436 199340344 757286092  21% /srv
    > # mdadm --detail /dev/md2
    > ...details elided...
    >     Number   Major   Minor   RaidDevice State
    >        0       8        3        0      active sync   /dev/sda3
    >        1       8       19        1      active sync   /dev/sdb3
    > 
    > ```
    > 
    > You can see that `/dev/md2` is on the `/dev/sda3` and `/dev/sdb3` devices.
    > 
    > There are other methods that block devices can be nested (fuse, loopback filesystems) that will have their own methods for determining the underlying block device, and you can even nest multiple layers so you have to work your way down. You'll have to take each case as it comes.
    > 
    > ---
    > 
    > I was so impressed with this answer that I used it as the basis for a command, "rawdev", that returns the underlying device(s) of a path or partition, even in cases where LVM and/or MD are nested. It's available on Github: [github.com/BMDan/rawdev](https://github.com/BMDan/rawdev) . -- [BMDan](https://unix.stackexchange.com/users/106108/bmdan "101 reputation") [Mar 10 '15 at 19:02](https://unix.stackexchange.com/questions/11311/how-do-i-find-on-which-physical-device-a-folder-is-located#comment316138_11312)
    > 




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


## fsck on next reboot(tune2fs / fsck.mode=force / fsck.repair / FSCKFIX=yes)

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


