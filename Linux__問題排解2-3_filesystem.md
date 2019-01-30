# Linux__問題排解2-3_filesystem

[toc]
<!-- toc --> 

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

### handle squashfs in Windows

- [python 2.7 - How to handle squashfs in Windows - Stack Overflow](https://stackoverflow.com/questions/36478351/how-to-handle-squashfs-in-windows)

    > [7-Zip](http://www.7-zip.org/download.html) is capable of opening squashfs images and extracting their files. I tested this on 7-Zip version 15.14 [64-bit] on Windows 10 with a squashfs image which uses xz compression.
    > 
    > 7-Zip does not appear to list squashfs among the archive formats when creating an archive, so you'll need to look elsewhere if you want to generate a squashfs image with modified files. The [Wikipedia page](https://en.wikipedia.org/wiki/SquashFS) for squashfs indicates that mksquashfs and unsquashfs have been ported to some versions of Windows (it also mentions 7-Zip).
    > 
    > [André's answer](https://stackoverflow.com/a/47373036/5384908) suggests Cygwin as a way to compile and run commands from `squashfs-tools`. The [Windows Subsystem for Linux](https://msdn.microsoft.com/en-us/commandline/wsl/install-win10) provides another way to run `mksquashfs` and `unsquashfs`. On my Windows 10 system in which `Ubuntu 14.04.4` is running via WSL, the following command installed `squashfs-tools`, after which `mksquashfs` and `unsquashfs` are available.
    > 
    > ```shell
    > sudo apt install squashfs-tools
    > ```
    > 
    > With either approach to using `squashfs-tools` (Cygwin or WSL), 7-Zip is unnecessary for updating files in a squashfs image.
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




