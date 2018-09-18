# Networking__網路設定

[toc]
<!-- toc --> 


## Router 設定

### router 當 switch 用

- [把 router 當 switch 用的設定步驟](https://cloudtu.github.io/blog/2014/02/router-switch.html)

    > 在 office 偶爾會遇到要連到同網段機器來做一些事，可是平常我都把自己的終端設備掛在自己帶來的 router 之下，這時臨時要去生個 switch 來用實在有點麻煩。後來 google 了一下，發現只要照下面二個步驟就可以讓 router 變身成 switch，還蠻簡單的，有這需求的人可以參考一下 ... :)
    > 
    > 1. 連進 router 的 web console，把 dhcp server 功能關掉
    > 2. 把原先接在 wan port 的網路線改接到 lan port

### 凱擘小烏龜 password

- [[教學]凱擘大寬頻 wifi 設定 只要花掉你人生的三分鐘 @ 電腦維修初學者 :: 痞客邦 ::](http://dahufoodtravel.pixnet.net/blog/post/220380751-%5B%E6%95%99%E5%AD%B8%5D%E5%87%B1%E6%93%98%E5%A4%A7%E5%AF%AC%E9%A0%BB-wifi-%E8%A8%AD%E5%AE%9A-%E5%8F%AA%E8%A6%81%E8%8A%B1%E6%8E%89%E4%BD%A0%E4%BA%BA%E7%94%9F%E7%9A%84)

    > **凱擘大寬頻 wifi 設定解救步驟**
    > 
    > **第一歨：重新設置凱擘大寬頻分享器**
    > 
    > 重置的按鈕，在分享器的頭上，有一個很小的圈圈，你必須要用小針或牙籤之類的東西，按個10秒，再放開他就會恢復原廠設置了
    > 
    > **第二歨：連上有凱擘大寬頻的網路線或是無線網路**
    > 
    > 不是凱擘的網路狀態，絕對進入不了分享器的內部喔！
    > 
    > **第三歨：在瀏覽器搜尋框輸入凱擘分享器的登入網址**
    > 
    > 凱擘分享器進入設定網址
    > 
    > 192.168.0.1
    > 
    > 192.168.100.1（通常我是輸入這個網址）
    > 
    > ![凱擘大寬頻 wifi 設定1](https://pic.pimg.tw/dahufoodtravel/1473984459-4291475666.png?v=1473984602)
    > 
    > **第四歨：輸入登入密碼**
    > 
    > 帳號：admin\
    > 密碼：password（建議第一次登入之後就修改密碼，免得被有心人士登入）
    > 
    > ![凱擘大寬頻 wifi 設定2](https://pic.pimg.tw/dahufoodtravel/1473984460-91823209.png?v=1473984602)
    > 

### 不同網段，互連問題

- [不同網段，互連問題 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/questions/10112356)

    > ![](https://d1dwq032kyr03c.cloudfront.net/upload/images/20121217/2012121715053650cec440ed8cc_resize.jpg)
    > 
    > 樓主的問題不難很簡單\
    > 你的ROUTER基本上要建立幾個網段\
    > 分別是 192.168.1.X 192.168.2.X 10.10.10.X網段\
    > 遮罩皆可以設定為 255.255.255.0\
    > 所以你在ROUTER上分別設定3個IP\
    > 192.168.1.254 192.168.2.254 10.10.10.254\
    > 接著CLIENT端上如果是 192.168.1.X的網段\
    > 那麼閘道就要設定 192.168.1.254這個IP\
    > 其他2個網段請自行設定\
    > 因為你把這3個網段都設定到ROUTER上\
    > 那麼routing的問題就給router處理就好\
    > 這觀念很基本 解法也很快速

### dlink 無法login

- [cant login to router - D-Link | DSLReports Forums](https://www.dslreports.com/forum/r24893337-cant-login-to-router)


    > You could have a browser problem. Try a different browser and see if that fixes things.


    > If you haven't resolved it yet, it's possible you have something like adblock or noscript that's causing it to not load the image.


    > Always a good idea to go to IE when having to deal with router settings, especially when upgrading the firmware.


## Asuswrt Merlin

### Asus RT-AC66U_B1

- [ASUS RT-AC66U B1 - WikiDevi](https://wikidevi.com/wiki/ASUS_RT-AC66U_B1)

    > - ASUS RT-AC66U B1 H/W Ver.:A1 - BCM4708C0 (@1.0GHz Dual Core)
    > 
    >    Also has one front USB3 port, one USB2 back ports, AMD flash (NAND),
    > 
    >    and can be flashed with Merlin firmware for the RT-AC68U.
    >    




### install Merlin

- [【长期更新】ASUS Merlin 折腾记 + 我的 RT-AC66U B1](https://zhuanlan.zhihu.com/p/34156571)

    > 什么是 Merlin
    > ----------
    > 
    > > AsusWRT-Merlin 是基于华硕路由器固件的一个嵌入式 Linux 系统，它号称是"增强版"的华硕固件。并且它不仅限于安装在华硕设备上，其它路由器也能使用。\
    > > Merlin 固件在国内，很多路由器党都亲切的叫它：梅林。
    > 
    > 你可以在这里下载官方 Merlin：[Download | Asuswrt-Merlin](https://link.zhihu.com/?target=https%3A//asuswrt.lostrealm.ca/download)
    > 
    > 如果你需要一些符合我国国情的功能（去广告、科学上网、DDNS）等的话，可以去下载 Koolshare 论坛修改的固件：[Index of / - KoolShare 固件下载服务器](https://link.zhihu.com/?target=http%3A//firmware.koolshare.cn/)
    > 
    > P.S：AC66U B1 与 AC68U 的固件是一样的，直接下载 AC68U 的即可
    > 
    > 下载后记得检查一下 MD5 / SHA256，然后进入 WEB 页面选择「系统管理」→「固件升级」，上传你的 trx 固件文件，点击升级即可。
    > 
    > ![](https://pic4.zhimg.com/80/v2-f012b582773571b2b3f8b65946e08994_hd.jpg)
    > 
    > 从官方固件升级到 Merlin 固件不需要清除数据，但如果你想从 Merlin 固件刷回官方固件，则需要清除数据和 NVRAM（最好在救援模式下操作），第一次启动可能需要 5 分钟左右，耐心等一会儿。
    > 
    > 安装完 Merlin 后做的一些工作
    > ------------------
    > 
    > -   开启 JFFS 分区
    > 
    > 当你成功登入管理页面后，选择「系统管理」→「系统设置」。在 Persistent JFFS2 partition 栏，Enable JFFS custom scripts and configs 选择「是」，把上面的格式化也选择上，重启路由器即可生效。
    > 
    > -   开启 uPnP 并配置防火墙
    > 
    > ![](https://pic4.zhimg.com/80/v2-c2f2e8423989743dfa553a403bfc129b_hd.jpg)
    > 
    > **重要！配置完成后一定要点击左侧的「防火墙」，在「一般设置」处，将 NAT Loopback 从默认的 ASUS 改为 Merlin，否则你将会碰到明明 uPnP 开启了但是 BT 等下载软件却连接不上公网的情况（即使你有公网 IP）**
    > 
    > ![](https://pic2.zhimg.com/80/v2-3ede5e06be7ce8c316dd99737118c4ed_hd.jpg)
    > 
    > -   开启 SSH（最好只保留内网访问）
    > 
    > ![](https://pic4.zhimg.com/80/v2-c49582c06f1af670e2b759fbd95b3f9f_hd.jpg)
    > 
    > 连接可以使用 PuTTY 或 WinSCP（协议选择 SCP），使用路由器管理的账号和密码登录即可。
    > 
    > Koolshare 论坛的改版 Merlin 固件都有软件中心，这里我就不再赘述了，各取所需安装所需插件即可。
    > 
    > **由于软件中心去除了科学上网，想手动安装的请[点此查看](https://link.zhihu.com/?target=https%3A//www.mianao.info/2017/10/02/asus-merlin-%25E5%259B%25BA%25E4%25BB%25B6-koolshare-%25E6%2594%25B9%25E7%2589%2588%25E7%25A6%25BB%25E7%25BA%25BF%25E5%25AE%2589%25E8%25A3%2585shadowsocks/)**
    > 


### install entware

- [Entware · RMerl/asuswrt-merlin Wiki](https://github.com/RMerl/asuswrt-merlin/wiki/Entware)

    > ### About
    > 
    > [Entware](http://github.com/Entware/entware) is a modern alternative to Optware. Originally designed for OpenWRT, it is also usable by other firmware platforms such as DD-WRT or Tomato. You can also set this up on your Asuswrt-Merlin based router.
    > 
    > For those unfamiliar with Optware: it's a software repository that offers various software programs that can be installed on your router. They allow you to add new functionality to your router (provided you have the know-how to properly configure them). This allows you, for example, to install and run the Asterisk SIP server on your router.
    > 
    > Note that you cannot use both Optware and Entware at the same time.
    > 
    > **Important:** Asus's DownloadMaster is based on Optware, and therefore is NOT compatible with Entware. You will have to uninstall DownloadMaster and look at the alternatives provided by Entware.
    > 
    > After uninstalling, you should make sure "asusware.arm" or "asusware.*" dir on mounted disk partition is deleted. Otherwise, Entware won't work properly.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/Entware#setup)Setup
    > 
    > The installation and configuration process must be done through telnet or SSH. If that part scares you, then forget about Entware already: everything must be installed and configured through telnet/SSH.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/Entware#the-easy-way)The easy way
    > 
    > Starting with v3.0.0.4.270.25 a new script has been introduced to facilitate Entware installation. After installing a [USB drive](https://github.com/RMerl/asuswrt-merlin/wiki/Initialize-OPTWARE), just type in terminal:
    > 
    > ```
    > entware-setup.sh
    > 
    > ```
    > 
    > ```
    > admin@RT-AC66U:/tmp/mnt/sda1/asusware# entware-setup.sh
    >  Info:  This script will guide you through the Entware installation.
    >  Info:  Script modifies only "entware" folder on the chosen drive,
    >  Info:  no other data will be touched. Existing installation will be
    >  Info:  replaced with this one. Also some start scripts will be installed,
    >  Info:  the old ones will be saved to .entwarejffs_scripts_backup.tgz
    > 
    >  Info:  Looking for available partitions...
    > [1] --> /tmp/mnt/sda1
    >  =>  Please enter partition number or 0 to exit
    > 
    > ```
    > 
    > Choose a partition where Entware should be installed, in this case is only [1] --> /tmp/mnt/sda1
    > 
    > ```
    > [0-1]: 1
    >  Info:  /tmp/mnt/sda1 selected.
    > 
    >  Info:  Creating /tmp/mnt/sda1/entware folder...
    >  * Warning:  Deleting old /tmp/opt symlink...
    >  Info:  Creating /tmp/opt symlink...
    >  Info:  Creating /jffs scripts backup...
    > tar: removing leading '/' from member names
    >  Info:  Modifying start scripts...
    >  Info:  Starting Entware deployment....
    > 
    > Info: Creating folders...
    > Info: Deploying opkg package manager...
    > Downloading /opt/bin/opkg... success!
    > Downloading /opt/etc/opkg.conf... success!
    > Downloading /opt/etc/profile... success!
    > Downloading /opt/etc/init.d/rc.func... success!
    > Downloading /opt/etc/init.d/rc.unslung... success!
    > Info: Basic packages installation...
    > Downloading http://pkg.entware.net/binaries/mipsel/Packages.gz.
    > Updated list of available packages in /opt/var/opkg-lists/entware-ng.
    > Installing ldconfig (1.0.12-1) to root...
    > Downloading http://pkg.entware.net/binaries/mipsel/ldconfig_1.0.12-1_mipselsf.ipk.
    > Installing findutils (4.5.14-1) to root...
    > Downloading http://pkg.entware.net/binaries/mipsel/findutils_4.5.14-1_mipselsf.ipk.
    > Installing libc (1.0.12-1) to root...
    > Downloading http://pkg.entware.net/binaries/mipsel/libc_1.0.12-1_mipselsf.ipk.
    > Installing libgcc (4.8.5-1) to root...
    > Downloading http://pkg.entware.net/binaries/mipsel/libgcc_4.8.5-1_mipselsf.ipk.
    > Installing libssp (4.8.5-1) to root...
    > Downloading http://pkg.entware.net/binaries/mipsel/libssp_4.8.5-1_mipselsf.ipk.
    > Configuring ldconfig.
    > Configuring libgcc.
    > Configuring libc.
    > Configuring libssp.
    > Configuring findutils.
    > 
    > Congratulations! If there are no errors above then Entware-ng is successfully initialized.
    > 
    > Found a Bug? Please report at https://github.com/Entware-ng/Entware-ng/issues
    > 
    > Type 'opkg install <pkg_name>' to install necessary package.
    > 
    > ```
    > 
    > The script will create a new directory named "entware" and not "asusware" like in the "old" way, but the result is the same:
    > 
    > ```
    > admin@RT-AC66U:/tmp/home/root/# cd /opt
    > admin@RT-AC66U:/tmp/mnt/sda1/entware#
    > 
    > ```
    > 
    > ---
    > 
    > ### Usage
    > 
    > Entware's management tool is called "opkg". Just type "opkg" to see a list of available commands. the most useful ones would be the following:
    > 
    > ```
    > opkg list
    > opkg install software_name
    > opkg remove software_name
    > 
    > ```
    > 
    > For example, to install nano, a text editor that is much more user-friendly than vi:
    > 
    > ```
    > opkg install nano
    > 
    > ```
    > 
    > See a youtube video [here](http://www.youtube.com/watch?v=WhlzW_Fl1KA&feature=youtu.be)
    > 

### install python, git and add swap

- [玩转路由之 AsusWRT-Merlin 与 Entware - Blog for BlueRain / 蓝雨博客](https://blog.bluerain.io/p/AsusWrt-Merlin.html)

    > ### 安装 Python
    > 
    > 到这一步，Merlin 已经配置好了，Entware 也完成了，基本大功告成了，此时的 Merlin 可以当作一个自由的嵌入式 Linux 使用了。那么，我首先推荐安装支持最为完美的脚本语言 Python 的环境：
    > 
    > 安装 python（默认 2.7 版本）：
    > 
    > ```
    > opkg install python
    > ```
    > 
    > 安装 pip
    > 
    > ```
    > opkg install python-pip
    > ```
    > 
    > 此时别急，这时候的 pip 是有问题的，几乎安装不上任何包，但是并不是硬件架构的原因，是因为 setuptools 版本太旧了。需要：
    > 
    > ```
    > pip install --upgrade setuptools
    > ```
    > 
    > 升级 setuptools 即可。你以为这样就能用了？
    > 
    > 慢，如果你就此打住的话，会发现许多包含 native code 的包编译不了，原因当然是没有 python-dev 了。但是你直接安装 python-dev 又会出现这样的错误：
    > 
    > ```
    > Collected errors:
    > 
    >  * check_data_file_clashes: Package python-dev wants to install file /opt/lib/libpython2.7.so
    > 
    >         But that file is already provided by package  * python-base
    > 
    >  * check_data_file_clashes: Package python-dev wants to install file /opt/lib/libpython2.7.so.1.0
    > 
    >         But that file is already provided by package  * python-base
    > 
    >  * opkg_install_cmd: Cannot install package python-dev.
    > ```
    > 
    > 原因和 python-base 包的文件冲突了。需要这样（覆盖掉）：
    > 
    > ```
    > opkg install python-dev --force-overwrite
    > ```
    > 
    > 执行完上面的命令后，此时 Python 才能完美使用。
    > 
    > ### 有关 Git
    > 
    > Git 其实没有啥问题，但是，你很有可能装错包了。如果你是直接 opkg install git 安装的话，你将无法拉取 HTTPS 协议的 git 地址。也就是说，这么大的 github 克隆不下来任何仓库。你需要安装它：
    > 
    > ```
    > opkg remove git
    > ```
    > 
    > ```
    > opkg install git-http
    > ```
    > 
    > 此时的 git 才能正常克隆 https 协议的仓库。
    > 
    > ### 给系统设置虚拟内存
    > 
    > 依次执行：
    > 
    > ```
    > dd if=/dev/zero of=/tmp/mnt/sda1/swapfile bs=1024 count=512000
    > mkswap /tmp/mnt/sda1/swapfile
    > swapon /tmp/mnt/sda1/swapfile
    > ```
    > 
    > 然后，创建启动脚本：
    > 
    > ```
    > echo '
    > #!/bin/sh
    > # Turn On Usage Of Swapfile
    > 
    > if [ -f "/tmp/mnt/sda1/swapfile" ];then
    > swapon /tmp/mnt/sda1/swapfile
    > echo "Turning Swapfile On"
    > fi
    > ' >> /jffs/scripts/post-mount
    > ```
    > 
    > 给执行权限：
    > 
    > ```
    > chmod a+rx /jffs/scripts/*
    > ```
    > 
    > 大功告成。如果你对 swap 大小不满意请自行修改（注意 U 盘路径）。
    > 
    > ### 附加
    > 
    > 1.  关于为什么 R7000 不能使用 OpenWRT？
    > 
    >     OpenWRT 是支持 R7000 的，并且我也用过。我指的是无法正常使用路由器的功能，最重要的无线功能是无法启用的。原因是 R7000 的相关硬件的驱动是闭源的。如果你完全将其作为有线路由器来使用，OpenWRT 也未尝不可。
    > 
    > 2.  为什么 Merlin 可以让 R7000 使用无线？
    > 
    >     因为华硕的一些路由器跟 R7000 用了同样的硬件，Merlin 有对应驱动的内核。但也因为如此，R7000 的 Merlin 内核一直处在 2.6 版本，这对于一个常更新的系统是一个很大的弊端。
    > 
    > 3.  为什么华硕不更新驱动支持新内核？
    > 
    >     貌似很多人都有这个想法。但其实，驱动是对应厂商提供的，华硕也无能为力。在硬件不开源以及厂商不更新的情况下，可能只能把这个 2.6 内核使用下去。
    > 
    > 4.  2.6 这么旧的内核有什么短板？
    > 
    >     目前很多公司生产环境 RH 系列的系统都是用的 2.6 内核，对于大多数情况而言是没有影响的。但是不排除有例如一些新元素不对旧内核进行支持的情况（例如高版本的 Docker、TCP-BBR 算法等）。当然，这种情况在嵌入式系统上概率会更小。
    > 
    > ### 关于内核版本
    > 
    > 在后续的了解中，我知道了原来 DD-WRT 是能在高版本内核（最新版已经是 4.4）中使用无线功能的。原因是 DD-WRT 和厂商有商业关系，所以解决了驱动问题。\
    > 于是我兴奋的去尝试了 DD-WRT，不得不说它是个非常优秀的路由器系统，有庞大的配置项。但可惜的是，我一直无法成功配置 Optware 或者 Entware 的环境。并且是由于一些莫名其妙的问题导致的，让人匪夷所思。例如，在 DD-WRT 的系统上，我无法执行生成的任何一个二进制可执行文件，这导致所有东西无法安装或者安装以后无法运行。
    > 
    > 经过长时间的资料搜索，仍然无法解决。后来就刷回 Merlin 了，这也是我强烈推荐 Merlin 的原因。DD-WRT 可以一试，希望你们没有或者能解决我当时没能解决的问题。
    > 
    > UPDATE：DD 的所有问题已经解决，详情[点击这里](http://blog.bluerain.io/p/DD-WRT.html)。
    > 




### entware package list

- [Packages list (armv7sf-k2.6)](http://bin.entware.net/armv7sf-k2.6/Packages.html)

### add user

- [ubuntu - How to add an user in OpenWrt using command or python? - Stack Overflow](https://stackoverflow.com/questions/50060219/how-to-add-an-user-in-openwrt-using-command-or-python)
    > 
    > You should install the `shadow-useradd` package:
    > 
    > ```
    > opkg update
    > opkg install shadow-useradd
    > ```
    > 
    > Documentation : [Secure your router's access](https://wiki.openwrt.org/doc/howto/secure.access)
    > 

- [Secure your router's access [OpenWrt Wiki]](https://wiki.openwrt.org/doc/howto/secure.access)

    > Create a non-privileged user in OpenWrt
    > ---------------------------------------
    > 
    > Example that adds a user called nicolaus:
    > ```
    > opkg update
    > opkg install shadow-useradd
    > useradd nicolaus
    > ```
    > 
    > Or add the user by hand (Take care that **uid/gid** (e.g.=1000) are not already in use!)
    > ```
    > /etc/passwd: USER:x:1000:1000:GROUP:/mnt/usb:/bin/false
    > /etc/group: GROUP:x:1000:
    > /etc/shadow: USER:RANDOMSTUFWillBeUpdatedWithPasswd:16666:0:99999:7:::
    > passwd USER
    > ```
    > 
    > However, you can't ssh to this user yet. To enable ssh access, you should make a password for that user, create his home folder and most importantly **indicate the shell** of that user:
    > ```
    > passwd nicolaus
    > mkdir /home
    > mkdir /home/nicolaus
    > chown nicolaus /home/nicolaus
    > vi /etc/passwd
    >    nicolaus:x:1000:1000:nicolaus:/home/nicolaus:/bin/ash
    > ```
    > 
    > ### Allow temporary privileged access using sudo
    > 
    > First, you should install `sudo`:
    > ```
    > opkg install sudo
    > ```
    > 
    > Additionally, you must allow your desired user by manipulating `'/etc/sudoers`' by tool `visudo`. Now you can follow **ONE** of the methods below to choose how the user should be able to run commands as `root`:
    > 
    > #### Method 1: 'sudo'ing by any user with root password (more secure)
    > 
    > In this method any user can temporarily run commands as root only if he knows the root password. This way when the user runs a command with `sudo` he should enter root's password instead of his password.
    > 
    > For enabling this method you should open the file `'/etc/sudoers`' by entering the command
    > ```
    > visudo
    > ```
    > 
    > Then uncomment the 2 lines below in that file and then save
    > ```
    > ## Uncomment to allow any user to run sudo if they know the password
    > ## of the user they are running the command as (root by default).
    > Defaults targetpw  # Ask for the password of the target user
    > ALL ALL=(ALL) ALL  # WARNING: only use this together with 'Defaults targetpw'
    > ```
    > 
    > This method is more secure because you don't need to protect both root and privileged (sudoer) users to keep the whole system safe.
    > 
    > One usecase can be allowing remote ssh with password from WAN: For more security (still less than RSA key) you can only allow users other than root to ssh with their password (optionally on a custom port) from WAN. And for even more security you can request root's password after running `sudo`. Therefor in this scenario a hacker should find 3 different strings **user's username**, **user's password** and **root's password** to get full access to the system. Even if the user's account get compromised, then the intruder still can't damage your system because he doesn't have root password yet.
    > 
    > #### Method 2: 'sudo'ing with the user's password
    > 
    > In this method, after logging in by the desired user, when you enter `sudo` you should enter the user's password again. The end result is similar to how you use `sudo` in Ubuntu or other popular Linux disros, but this method doesn't utilize group 'sudo' for this purpose.
    > 
    > For enabling this method you should also enter the command
    > ```
    > visudo
    > ```
    > And then add a line allowing your user, under comment "## User privilege specification":
    > ```
    > ##
    > ## User privilege specification
    > ##
    > root ALL=(ALL) ALL
    > nicolaus ALL=(ALL) ALL
    > ```
    > 
    > #### Method 3: 'sudo'ing with the user's password if he is member of group 'sudo' (needs installing some packages)
    > 
    > This method is very similar to Method 2, except that it allows any member of group 'sudo' to use `sudo` with their own password. This method is exactly the same one used in Ubuntu and other popular Linux distros to allow `'sudo`' access for a user.
    > 
    > For activating this method first you should allow group 'sudo' to use command `sudo` by entering
    > ```
    > visudo
    > ```
    > And then uncomment the line below:
    > ```
    > ## Uncomment to allow members of group sudo to execute any command
    > %sudo ALL=(ALL) ALL
    > ```
    > Second you should create group 'sudo'. You can do it by manually editing `'/etc/group`' but it's more standard to install and use tools for this purpose:
    > ```
    > opkg install shadow-groupadd
    > groupadd --system sudo
    > ```
    > 
    > And finally add your current user to the group 'sudo'. You can directly append your user to `'/etc/group`' but again it's better to use `usermod`:
    > ```
    > opkg install shadow-usermod
    > usermod -a -G sudo nicolaus
    > ```
    > 
    > This method is more convenient because you can simply allow `sudo` access for any user you want, just by *`usermod -a -G sudo <USER>`* but takes more space (for installing new packages) than method 2 which may be more suitable for systems with very limited space.
    > 
    > 
    > 

- [How to create user without useradd command in OpenWRT | Vladimir Ivanov](https://vladimir-ivanov.net/create-user-without-useradd-command-openwrt/)

    > There is no useradd command in OpenWRT. Instead, shadow user package is available but I found it overkill. Anyway, if you are interested in using it -- check out [this tutorial](http://wiki.openwrt.org/doc/howto/secure.access),\
    > Follow these steps to create a user without using **useradd** command in OpenWRT.
    > 
    > **Step 1**
    > 
    > Traditionally, the /etc/passwd file is used to keep track of every registered user that has  access to a system.\
    > Each line is an entry for one user, and fields on each line are separated by a colon.  The fields are:
    > 
    > -   User name
    > -   Encrypted password
    > -   User ID number (UID)
    > -   User's group ID number (GID)
    > -   Full name of the user (GECOS)
    > -   User home directory
    > -   Login shell
    > 
    > To add a new user by hand, add a new line at the end of the file, filling in the appropriate information. The information you add needs to meet some requirements, or your new user may have problems logging in. First, make sure that both the user name and user ID is unique. Assign the user a group, either 100 (the "users" group in OpenWRT) or your default group (use its number, not its name). Give the user a valid home directory (which you'll create later) and shell (set shell to /bin/false if you want the user to be able to use FTP but not SSH).
    > 
    > So, open the file for editing and add an entry of user details in /etc/passwd file.
    > 
    > 
    > ```
    > $ vi /etc/passwd
    > ```
    > 
    > Example entry:
    > 
    > ```
    > testuser:x:501:501:test user:/home/user:/bin/ash
    > ```
    > 
    > **Step 2**
    > 
    > Assign a password to the user you just created.
    > 
    > 
    > ```
    > $ passwd testuser
    > ```
    > 
    > 
    > passwd will prompt you for a password. You will see output like this
    > 
    > 
    > ```
    > Changing password for user testuser.
    > 
    > New password:
    > 
    > Retype new password:
    > 
    > passwd: all authentication tokens updated successfully.
    > ```
    > 
    > 
    > **Step 3**
    > 
    > All normal users are members of the "users" group on a typical Linux system. However, if you want to create a new group, or add the new user to additional groups, you'll need to modify the /etc/group file. Here is a typical entry:
    > 
    > 
    > ```
    > cvs::102:chris,logan,david,root
    > ```
    > 
    > 
    > The fields are group name, group password, group ID, and group members, separated by commas. Creating a new group is a simple matter of adding a new line with a unique group ID, and listing all the users you want to be in the group. Any users that are in this new group and are logged in will have to log out and log back in for those changes to take effect.
    > 
    > **Step 4**
    > 
    > Use mkdir to create the new user's home directory in the location you entered into the /etc/passwd file, and use chown to change the owner of the new directory to the new user.
    > 
    > 
    > ```
    > $ mkdir /home/testuser
    > 
    > $ chown testuser /home/testuser
    > ```
    > 
    > 
    > **NB**: Removing a user is a simple matter of deleting all of the entries that exist for that user. Remove the user's entry from /etc/passwd and remove the login name from any groups in the /etc/group file. If you wish, delete the user's home directory, too.
    > 
    > This tutorial is based on [Slackware Linux Essentials](http://www.slackbook.org/html/essential-sysadmin-hardusers.html) book.
    > 
    > 

### user script

- [User scripts · RMerl/asuswrt-merlin Wiki](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts)

    > About user scripts
    > ------------------
    > 
    > While Asuswrt-Merlin only adds a limited number of new features over the original firmware, a lot of customizations can be achieved through the use of user scripts. These will allow you to set up custom firewall rules, create jobs that can be run at scheduled intervals, or start new services.
    > 
    > Those scripts are stored in the internal non-volatile flash in the [JFFS](https://github.com/RMerl/asuswrt-merlin/wiki/JFFS) partition. Support for these scripts must be enabled, under Administration -> System on the webui.
    > 
    > [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#available-scripts)Available scripts:
    > -------------------------------------------------------------------------------------------------
    > 
    > These shell scripts will be run when certain events occur. They must be saved in `/jffs/scripts/`.
    > 
    > These scripts will usually run in parallel to the event itself, except when explicitly documented as being a blocking script. In that case, the script will prevent the execution of the event itself until either the script completes, or it times out (current default timeout value is 120 seconds).
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#services-start)services-start
    > 
    > Called after all other system services have been started at boot. This is the best place to stop one of these services and restart it with a different configuration, for example. (But be aware that anytime the service gets manually restarted it will revert back to the original setup.)
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#services-stop)services-stop
    > 
    > Called before all system services are stopped, usually on a reboot.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#service-event)service-event
    > 
    > Called before a service event is called (i.e. restart_httpd, restart_wireless, etc...). First argument is the event (typically *stop*, *start* or *restart*), second argument is the target (*wireless*, *httpd*, etc...). This is a blocking script, meaning that it will prevent the execution of the event itself until the script either completes or times out.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#wan-start)wan-start
    > 
    > Called after the WAN interface came up. Good place to put scripts that depend on the WAN interface (e.g. to update an IPv6 tunnel or a dynamic DNS service). The Internet connection is unlikely to be active when this script is run. Add a `sleep` line to delay running until the connection is complete, or loop until your command succeeds.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#firewall-start)firewall-start
    > 
    > Called after the firewall got started and filtering rules have been applied. This is where you will usually put your own custom rules in the filter table (but *not* the NAT table). The script receives the WAN interface name (e.g. `ppp0`) as an argument which can be used in the script using `$1`.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#nat-start)nat-start
    > 
    > Called after NAT rules (i.e. port forwards and such) have been applied to the NAT table. This is where you will want to put your own NAT table custom rules (e.g. a port forward that only allows connections coming from a specific IP).
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#init-start)init-start
    > 
    > Called right after JFFS got mounted, and before any of the services get started. This is the earliest part of the boot process where you can insert something.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#pre-mount)pre-mount
    > 
    > Called just before a partition gets mounted. This is run in a blocking call and will block the mounting of the partition for which it is invoked until its execution is complete or it times out. This is done so that it can be used for things like running `e2fsck` on the partition before mounting. This script is passed the device path being mounted (e.g. `/dev/sda1`) as an argument which can be used in the script using `$1`.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#post-mount)post-mount
    > 
    > Called just after a partition got mounted. The script is passed the mount point (the filesystem path where the partition was mounted, e.g. `/tmp/mnt/OPT`) as an argument which can be used in the script using `$1`.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#unmount)unmount
    > 
    > Called just before unmounting a partition. Like pre-mount, this is a blocking script, so be careful with it. The script is passed the mount point as an argument which can be used in the script using `$1`.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#dhcpc-event)dhcpc-event
    > 
    > Called whenever a DHCP event occurs on the WAN interface. The type of event is passed as an argument which can be used in the script using `$1`; possible event types in the version of `udhcpc` in ASUSWRT are `deconfig` (when udhcpc starts and when a lease is lost), `bound` (when a lease and new IP address are acquired), and `renew` (when a lease is renewed, but the IP did not change).
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#openvpn-event)openvpn-event
    > 
    > Called whenever an OpenVPN server gets started/stopped, or an OpenVPN client connects to a remote server. Uses the same syntax/parameters as the "up" and "down" scripts in OpenVPN.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#ddns-start)ddns-start
    > 
    > Called at the end of a DDNS update process. This script is also called when setting the DDNS type to "Custom". The script gets passed the WAN IP as an argument, which can be used in the script using `$1`. When handling a "Custom" DDNS, this script is also responsible for reporting the success or failure of the update process. See the [Custom DDNS](https://github.com/RMerl/asuswrt-merlin/wiki/Custom-DDNS) section for more information.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#update-notification)update-notification
    > 
    > Called when the scheduled new firmware version availability check detects there's a new firmware available for download. See [update notification example](https://github.com/RMerl/asuswrt-merlin/wiki/update-notification-example) for more info.
    > 
    > [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#postconf-scripts)Postconf scripts
    > ----------------------------------------------------------------------------------------------
    > 
    > Note that in addition to these, you can also use the numerous postconf scripts supported by the firmware, which allow you to execute a script between the moment a service's config file is generated and the service is about to be executed. See the [Postconf scripts](https://github.com/RMerl/asuswrt-merlin/wiki/Custom-config-files#postconf-scripts) section for more information.
    > 
    > [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#creating-scripts)Creating scripts
    > ----------------------------------------------------------------------------------------------
    > 
    > Don't forget to set any script you create as being executable:
    > 
    > ```
    > chmod a+rx /jffs/scripts/*
    > 
    > ```
    > 
    > And like any UNIX script, they need to start with a shebang:
    > 
    > ```
    > #!/bin/sh
    > 
    > ```
    > 
    > Also, you must save files with UNIX line endings. Note that Windows's Notepad cannot save with UNIX line endings; use Notepad++ instead. You can also directly edit them on the router through SSH, by using `vi` or `nano`, both included in the firmware; they will create files with the proper line endings.
    > 
    > [](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts#troubleshooting-scripts)Troubleshooting scripts:
    > -------------------------------------------------------------------------------------------------------------
    > 
    > Try running your script manually at first to make sure there is no syntax error in it. You can also insert some code near the top to be able to easily determine whether or not your script ran. For example:
    > 
    > ```
    > touch /tmp/000wanstarted
    > 
    > ```
    > 
    > You can then easily tell that the script did run by looking for the presence of 000wanstarted in the `/tmp` directory.
    > 
    > A useful command for debugging user scripts is `logger`, which will log messages to the system log, visible in the Web UI.
    > 

### Custom DDNS

- [Custom DDNS · RMerl/asuswrt-merlin Wiki](https://github.com/RMerl/asuswrt-merlin/wiki/Custom-DDNS)

    > ### Introduction
    > 
    > If you set the DDNS (dynamic DNS) service to "Custom", then you can fully control the update process through a `ddns-start` user script (which could launch a custom update client, or run a simple "wget" on a provider's update URL). The ddns-start script is passed the WAN IP as an argument.
    > 
    > Note that your custom script is responsible for notifying the firmware on the success or failure of the process. To do this your script must execute:
    > 
    > ```
    > /sbin/ddns_custom_updated 0 or 1
    > 
    > ```
    > 
    > (where 0 = failure, 1 = successful update)
    > 
    > If you can't determine the success or failure, then report it as a success to ensure that the firmware won't continuously try to force an update.
    > 
    > Finally, like all [user scripts](https://github.com/RMerl/asuswrt-merlin/wiki/User-scripts), the option to support custom scripts and config files must be enabled under Administration -> System.
    > 
    > After enabling custom scripts, place the contents of your update script in `/jffs/scripts/ddns-start` and Enable the DDNS Client in WAN -> DDNS and use `Custom` as Server.
    > 
    > [](https://github.com/RMerl/asuswrt-merlin/wiki/Custom-DDNS#using-a-ddns-with-double-nat)Using a DDNS with Double NAT
    > =====================================================================================================================
    > 
    > If your ASUS router is double NATed behind your ISP's router, you may need to retrieve your external IP rather than using the one passed to it from the Custom DDNS settings. Find the line in your update script where the IP is used
    > 
    > ```
    > IP=${1}
    > 
    > ```
    > 
    > and change it to get the IP from an external source
    > 
    > ```
    > IP=$(wget -O - -q http://myip.dnsomatic.com/)
    > 
    > ```
    > 
    > The above uses dnsomatic, but it can be modified to work with any source. The OpenWrt wiki provides a list [here](https://wiki.openwrt.org/doc/howto/ddns.client#detecting_local_ip).
    > 




### get public ip

- [ipify - A Simple Public IP Address API](https://www.ipify.org/)

    > ```sh
    > #!/bin/bash
    > 
    > ip=$(curl -s https://api.ipify.org)
    > echo "My public IP address is: $ip"
    > ```

### update a dyndns host entry 

- [Simple bash script to update a dyndns host entry](https://gist.github.com/allenyllee/01ef0908f56c47eea6f41c05d2209de7)

    > ```sh
    > #!/bin/bash
    > HOST=foo.example.com
    > USER=
    > PASS=
    > IPADDR=$(curl -s https://api.ipify.org)
    > RESULT=$(wget -q -O- "https://$USER:$PASS@members.dyndns.org/nic/update?hostname=$HOST&myip=$IPADDR&wildcard=NOCHG&mx=NOCHG&backmx=NOCHG")
    > ```

###  Setup SSL using nginx and Let's Encrypt 

- [Using Let's Encrypt · Entware/Entware-ng Wiki](https://github.com/Entware/Entware-ng/wiki/Using-Let%27s-Encrypt)

    > Introduction
    > ------------
    > 
    > This How-To helps to configure A+ SSL protected web server, using [nginx](http://nginx.org/) and [Let's Encrypt](https://letsencrypt.org/) as a certificate issuer right on router.
    > 
    > ![](https://camo.githubusercontent.com/8d5c5a72120b93553d011d1f70dc8959988ac798/68747470733a2f2f686162726173746f726167652e6f72672f66696c65732f6533352f3865662f6661632f65333538656666616338323334383663626132313865313535663238363962322e6a7067)
    > 
    > [](https://github.com/Entware/Entware-ng/wiki/Using-Let%27s-Encrypt#requirements)Requirements
    > ---------------------------------------------------------------------------------------------
    > 
    > -   You need domain name (**my.domain.ru** as example below) which is resolved to router IP address,
    > -   You need TCP80 and TCP443 ports open on router.
    > 
    > [](https://github.com/Entware/Entware-ng/wiki/Using-Let%27s-Encrypt#installation)Installation
    > ---------------------------------------------------------------------------------------------
    > 
    > Install necessary packages:
    > 
    > ```
    > opkg install bash ca-certificates coreutils-mktemp curl diffutils grep nginx openssl-util
    > 
    > ```
    > 
    > Download helper script to get/renew Let's Encrypt certificates:
    > 
    > ```
    > cd /opt/etc/nginx
    > curl -O https://raw.githubusercontent.com/lukas2511/dehydrated/master/dehydrated
    > 
    > ```
    > 
    > Edit two sections at `/opt/etc/nginx/nginx.conf`:
    > 
    > -   in `server` section:
    > 
    > `server_name "my.domain.ru";`
    > 
    > -   in `location` section:
    > 
    > `root /opt/share/nginx/html;`
    > 
    > Now start web server and make sure it's available from internet as <http://my.domain.ru>
    > 
    > `/opt/etc/init.d/S80nginx start`
    > 
    > Prepare folder, which will be used by Let's Encrypt service to make sure this web server belongs to you:
    > 
    > ```
    > echo WELLKNOWN="/opt/share/nginx/html/.well-known/acme-challenge" > config
    > mkdir -p /opt/share/nginx/html/.well-known/acme-challenge
    > 
    > ```
    > 
    > and start script to get new SSL sertificate:
    > 
    > ```
    > bash ./dehydrated --domain my.domain.ru --cron
    > 
    > ```
    > 
    > You'll get following answer if all goes fine:
    > 
    > ```
    > /opt/etc/nginx # bash ./dehydrated --domain my.domain.ru --cron
    > # INFO: Using main config file /opt/etc/nginx/config.sh
    > Processing my.domain.ru
    >  + Signing domains...
    >  + Generating private key...
    >  + Generating signing request...
    >  + Requesting challenge for my.domain.ru...
    >  + Responding to challenge for my.domain.ru...
    >  + Challenge is valid!
    >  + Requesting certificate...
    >  + Checking certificate...
    >  + Done!
    >  + Creating fullchain.pem...
    >  + Done!
    > 
    > ```
    > 
    > > **Note**: You may encounter errors here depending on your settings. Many people have found it necessary to add the following to their server block for their configuration
    > 
    > ```
    > location ^~ /.well-known {
    > 	allow all;
    > }
    > 
    > ```
    > 
    > The next step can take from five minutes (on Asus RT-N66U) to one hour (on Asus RT-N14U). If you've got Linux PC, you can run following command on PC then transfer **dhparams.pem** to router:
    > 
    > ```
    > openssl dhparam -out dhparams.pem 2048
    > 
    > ```
    > 
    > Now, configure HTTPS on nginx by adding following strings to `server` section of `/opt/etc/nginx/nginx.conf`:
    > 
    > ```
    > listen 443 ssl;
    > include ssl.conf;
    > 
    > ```
    > 
    > and put following content to `/opt/etc/nginx/ssl.conf`:
    > 
    > ```
    > ssl_certificate /opt/etc/nginx/certs/my.domain.ru/fullchain.pem;
    > ssl_certificate_key /opt/etc/nginx/certs/my.domain.ru/privkey.pem;
    > ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
    > ssl_prefer_server_ciphers on;
    > ssl_dhparam /opt/etc/nginx/dhparams.pem;
    > 
    > ssl_session_cache shared:SSL:10m;
    > ssl_session_timeout 5m;
    > # ssl_stapling on;
    > 
    > add_header Strict-Transport-Security "max-age=31536000; includeSubDomains";
    > 
    > ```
    > 
    > Restart web server and make sure <https://my.domain.ru> is available from internet:
    > 
    > ```
    > /opt/etc/init.d/S80nginx restart
    > 
    > ```
    > 
    > [](https://github.com/Entware/Entware-ng/wiki/Using-Let%27s-Encrypt#renewing-of-ssl-certificates)Renewing of SSL certificates
    > -----------------------------------------------------------------------------------------------------------------------------
    > 
    > By default, the Let's Encrypt SSL certificate is valid for 3 months. You can renew it from cron automatically:
    > 
    > ```
    > opkg install cron
    > 
    > ```
    > 
    > Create cron job by placing following script to **/opt/etc/cron.monthly/renew_certs.sh**:
    > 
    > ```
    > #!/bin/sh
    > cd /opt/etc/nginx
    > bash ./dehydrated --domain my.domain.ru --cron
    > nginx -s reload
    > 
    > ```
    > 
    > and make it executable:
    > 
    > ```
    > chmod +x /opt/etc/cron.monthly/renew_certs.sh
    > 
    > ```
    > 
    > Don't forget to start cron:
    > 
    > ```
    > /opt/etc/init.d/S10cron start
    > 
    > ```
    > 
    > 

### Store custom SSL certificates

- [Custom SSL certificates · RMerl/asuswrt-merlin Wiki](https://github.com/RMerl/asuswrt-merlin/wiki/Custom-SSL-certificates)

    > ### Web interface (HTTPS support)
    > 
    > Starting with 380.67, Asuswrt-Merlin can now use your own SSL certificate for securing the management webui. This can be useful if you generate your certificate using your own CA which you have stored in your client devices, or if you obtain a valid certificate from a known CA.
    > 
    > To do so, you must first enable persistent certificate support, on the Administration -> System page. Under the Web Interface section make sure that the *Authentication Method* is set to either *HTTPS* or *Both*. Then, set *Use persistent certificate* to *Yes*, then press *Apply*.
    > 
    > Now, your router is going to use a self-signed certificate, and store it on the JFFS partition. The next step is to connect to your router over SSH or SCP, then store your own key and certificate files into the */jffs/ssl/* directory. There should already be a key.pem and cert.pem file there, which are the key and self-signed certificate generated by your router. Replace these two with yours. They must be in PEM format, which looks something like this:
    > 
    > ```
    > -----BEGIN CERTIFICATE-----
    > a series of random characters
    > on multiple lines
    > -----END CERTIFICATE-----
    > 
    > ```
    > 
    > Then, restart the router's web server to make it use the new provided certificate. Run the following command over SSH:
    > 
    > ```
    > service restart_httpd
    > 
    > ```
    > 
    > After that, if you access your router over HTTPS (don't forget to specify the port, which by default will be 8443), it should be using your new certificate.
    > 
    > ### [](https://github.com/RMerl/asuswrt-merlin/wiki/Custom-SSL-certificates#ftp-server-tls-support)FTP server (TLS support)
    > 
    > You can also provide your own key/cert for the FTP server. They must also be stored under */jffs/ssl/* and named ftp.key and ftp.crt.
    > 

## OpenWRT

### packages table

- [OpenWrt Project: Package table](https://openwrt.org/packages/table/start)



### Run Docker containers on OpenWrt?

- [Packaging Docker on OpenWrt - Stack Overflow](https://stackoverflow.com/questions/42221803/packaging-docker-on-openwrt)

- [Run Docker containers on OpenWrt?](https://forum.archive.openwrt.org/viewtopic.php?id=50326&p=2)

    > I also interesting in trying Docker on OpenWRT if this will be possible.
    > 
    > There is already solution for LXC if anyone want to give it a try: [https://forum.openwrt.org/viewtopic.php ... 64#p275064](https://forum.openwrt.org/viewtopic.php?pid=275064#p275064)
    > 
    > ---
    > 
    > Has there been any progress on this?\
    > I'm trying to get an instance of docker running on openWRT myself.\
    > So far I've tried to run a prebuilt Docker on my ARM Platform.
    > 
    > An attemp to run "dockerd &" gave me:
    > 
    > > root@lede:~# WARN[0000] could not change group /var/run/docker.sock to docker: group docker not found\
    > >     INFO[0000] libcontainerd: new containerd process, pid: 2902\
    > >     WARN[0000] containerd: low RLIMIT_NOFILE changing to max  current=1024 max=4096\
    > >     WARN[0001] unable to modify root key limit, number of containers could be limited by this quota: open /proc/sys/kernel/keys/root_maxkeys: no such file or directory\
    > >     Error starting daemon: error while opening volume store metadata database: madvise: function not implemented
    > 
    > this doesn't look too bad, right?\
    > The Docker Installation guide points out that I need to have "a properly mounted cgroupfs hierarchy"\
    > As my error output says something about groups, my guess is that I need to set up a cgroup hierarchy.
    > 
    > ---
    > 
    > This is made possible on Chaos Calmer built for x86-64 platform, however building from source code is required.
    > 
    > First add these to targets/linux/x86/config-3.18(i don't remember the actual path but seems so):
    > 
    > ```
    > CONFIG_ADVISE_SYSCALLS=y
    > CONFIG_KEYS=y
    > CONFIG_EXT4_FS_POSIX_ACL=y
    > CONFIG_EXT4_FS_SECURITY=y
    > CONFIG_KEYS_DEBUG_PROC_KEYS=y
    > CONFIG_AUDIT=y
    > CONFIG_AUDITSYSCALL=y
    > CONFIG_SCHED_AUTOGROUP=y
    > CONFIG_TMPFS_POSIX_ACL=y
    > CONFIG_PROC_KCORE=y
    > CONFIG_JFFS2_FS_POSIX_ACL=y
    > CONFIG_JFFS2_FS_SECURITY=y
    > CONFIG_X86_DECODER_SELFTEST=y
    > ```
    > 
    > Then in Global Build settings select everything related to namespace, cgroup and lxc, select kmod-veth in Network Support, select everything related to ebtables(just use search) and kmod-nf-nathelper kmod-nf-nathelper-extra in Netfilter Extensions.
    > 
    > Also select iptables-mod-conntrack-extra iptables-mod-extra iptables-mod-ipsec iptables-mod-nat-extra in iptables, and procps xz-utils in Utiltites.
    > 
    > Start the build now and you'll get what you want.
    > 
    > I'm not allowed to post image or links here, if possible I'm willing to share my prebuilt image and buildroot environment(a docker image).
    > 
    > ---
    > 
    > here is my full kernel config that I used to get it running: bit.ly/2wIvKSs
    > 
    > ---
    > 
    > **Which applications do you have in mind?**\
    > E.g. I implemented a smart desktop lamp which used the currently connected devices in the network as a feature. If my ereader was connected (which it is only when in use) this would give the lamp a hint that it should turn on. I didn't use docker to broadcast that information to the lamp.
    > 
    > **Where is the requierement for docker?**\
    > I gave these arguments to support the idea of using the Router as a computing platform in general. Not related to docker.
    > 
    > The benefit of using docker is that it makes the provisioning of applications across different routers/servers/Raspberrys easy. Think of a mobile user. He may run his application on different routers as he moves through the city. Those routers might all be part of a docker swarm, and we can dynamically move the application in form of a container between the routers.
    > 

- [packaging Docker on OpenWrt - Google 網上論壇](https://groups.google.com/forum/#!searchin/docker-dev/openwrt/docker-dev/tR6Mx3pVKf4/6dI_Mi7YS6cJ)

    > Hi,
    > 
    > I'd like Docker to be packaged on [OpenWrt](https://openwrt.org/) so I've [stirred the waters on the OpenWrt forum](https://www.google.com/url?q=https%3A%2F%2Fforum.openwrt.org%2Fviewtopic.php%3Fpid%3D232175%23p232175&sa=D&sntz=1&usg=AFQjCNFjL1RI3qZA9j0hwvasLvRK4cPtzw).  I've got them interested and am seeing what I can do to help the process along.
    > 
    > The first step, I imagine, is to cross compile Docker for ARM.  I've downloaded the Docker build environment and see a target in the Makefile called "cross" but when I tried it I got the following error message:
    > 
    > > $ make cross
    > >
    > > docker build -t "docker:master" .
    > >
    > > Uploading context 38.63 MB
    > >
    > > Uploading context 
    > >
    > > Step 0 : docker-version 0.6.1
    > >
    > > # Skipping unknown instruction DOCKER-VERSION
    > >
    > > Step 1 : FROM ubuntu:13.10
    > >
    > >  ---> 5e019ab7bf6d
    > 
    > > ...
    > 
    > > Step 24 : ADD . /go/src/[github.com/dotcloud/docker](http://github.com/dotcloud/docker)
    > >
    > >  ---> Using cache
    > >
    > >  ---> 326fbd19bdd0
    > >
    > > Successfully built 326fbd19bdd0
    > >
    > > docker run --rm -it --privileged -e TESTFLAGS -e TESTDIRS -e DOCKER_GRAPHDRIVER -e DOCKER_EXECDRIVER -v "/Users/david/Documents/projects/docker/bundles:/go/src/[github.com/dotcloud/docker/bundles](http://github.com/dotcloud/docker/bundles)" "docker:master" hack/make.sh binary cross
    > >
    > >\
    > >
    > > ---> Making bundle: binary (in bundles/0.10.0-dev/binary)
    > >
    > > # [github.com/dotcloud/docker/docker](http://github.com/dotcloud/docker/docker)
    > >
    > > /usr/local/go/pkg/tool/linux_amd64/6l: running gcc failed: Cannot allocate memory
    > >
    > > make: *** [cross] Error 2
    > 
    > Instructions for creating packages on OpenWrt are here:  <http://kamikaze.openwrt.org/docs/openwrt.html#x1-460002.1.2>
    > 
    > Any suggestions for the next step along the path?
    > 
    > Thanks,
    > 
    > David
    > 
    > ---
    > 
    > Ah, thank you!  This didn't occur to me because I'm compiling on a MacBook Pro with 8 GB of memory but of course it's not the host---the host is an Ubuntu Vagrant box with only 512 MB.  Too many abstractions!  :-)  I upped the virtual host's RAM to 4 GB and it worked.
    > 
    > 
    > 



### run OpenWRT on Docker
- [Docker OpenWrt Image [OpenWrt Wiki]](https://wiki.openwrt.org/doc/howto/docker_openwrt_image)


### run LXD on OpenWRT

- [LXD - success on OpenWRT (privileged containers) - but problems with unprivileged - LXD - Linux Containers Forum](https://discuss.linuxcontainers.org/t/lxd-success-on-openwrt-privileged-containers-but-problems-with-unprivileged/1729/13)

    > hi there,
    > 
    > i have been quite busy the last weeks, besides LXD, but now i am finished with what i wanted, my last tests regarding "machine learning" even on mipsel concluded today...\
    > besides LXD i got quite a lot of other GO packages for openwrt to compile (also on mips(el)), like terraform, kubernetes, prometheus, influx stack, syncthing, docker (altough i am not a docker fan), and so on... for all of them i have written openwrt package makefiles with necessary patches and so on, as they can easily be compiled by selecting the packages in the configuration (make menuconfig)...
    > 
    > what took me a little longer was the "find3" location service...\
    > therefore i needed "openblas" (with lapack - required fortran), numpy, scipy and scikit... they now all compile on arm and mipsel with openwrt (netgear r7800 - and mt7621 based "D-Link DIR-860L rev B1" and "Ubiquiti Networks EdgeRouter X")...\
    > an btw LXD containers for testing were really helpful during that time... ![:slight_smile:](https://discuss.linuxcontainers.org/images/emoji/google/slight_smile.png?v=5 ":slight_smile:")
    > 
    > i will upload the repositories (different branches for each feature patch - e.g. separate ones for containers. btrfs, etc) to gitlab tomorrow or even later today... also with the custom repositories for GO packages, python, and some additional custom packages (tfshark from wireshark, openblas)...
    > 
    > after uploading the repos i will post the links...\
    > and after that i will write some short documentation for it ![:wink:](https://discuss.linuxcontainers.org/images/emoji/google/wink.png?v=5 ":wink:")
    > 
    > bye,
    > 
    > manfred
    > 
    > ps: the time is near ![:smiley:](https://discuss.linuxcontainers.org/images/emoji/google/smiley.png?v=5 ":smiley:")
    > 
    > ---
    > 
    > i have created a gitlab account and uploaded the repository.
    > 
    > ### [Manni](https://gitlab.com/users/mgschweidl/projects)
    > 
    > 
    > it's "openwrt-dev"
    > i have rebased all my branches on current master / 18.06 version from today morning.\
    > the patches for procd are in the branches with the extension "container".
    > 
    > normally every branch for itself should be usable by it's own. although i always combined them when i was building images / packages.
    > 
    > the "golang" branches include the necessary patches to build the go toolchain as part of the normal toolchain. but it need's to be selected within "Advanced configuration options (for developers)" -> "Toolchain Options" -> "*** Go compiler ***" and enable "Build go"
    > 
    > I have also two versions 1.10 and 1.8 as i started with the go compiler in openwrt with inoffical patches for mips (soft-float) with 1.8. all current packages from my gitlab repo "openwrt_custom_packages_golang" are only tested with the 1.10 version of go.\
    > all other settings should be by default ok. binaries will be installed within "/usr/lib/golang-packages" by default, but could be changed by modifications of the compiler options.
    > 
    > the only package including more than the binary is LXD, which includes modifications (setup) and procd init script. so simple install of the package should be enough. then proceed with "lxd init" and so on... for LXD you need the patches from "container" branches for the version of your choice (18.06 or master).
    > 
    > the "btrfs" branch includes patches for using btrfs on raid as extroot on startup and patches for configuration of subvolumes to mount in "/etc/config/fstab"
    > example:
    > 
    > ```
    > config 'global'
    > option anon_swap '0'
    > option anon_mount '0'
    > option auto_swap '1'
    > option auto_mount '1'
    > option delay_root '5'
    > option check_fs '0'
    > 
    > config 'mount'
    > option target '/overlay'
    > option uuid 'b8c76bbb-e1e3-4b01-9a6a-608077d8c89a'
    > option fstype 'btrfs'
    > option btrfs_raid '1'
    > option options 'subvol=@r7800_overlay_current'
    > option enabled '1'
    > 
    > config 'mount'
    > option target '/data'
    > option uuid '694f6730-682f-41b3-9e81-21b86b17ae43'
    > option fstype 'btrfs'
    > option options 'subvol=@r7800_data_current'
    > option enabled '1'
    > 
    > config 'mount'
    > option target '/data/lxd_container'
    > option uuid '694f6730-682f-41b3-9e81-21b86b17ae43'
    > option fstype 'btrfs'
    > option options 'subvol=@lxd_container'
    > option enabled '1'
    > ```
    > 
    > the "kernel" branch includes new kernel modules as some minor modifications.
    > 
    > the "container" branch includes patches for mouting of "cgroup hierarchy and cgroup v2" as container detection for lxd / lxc.
    > 
    > the "host-variants" brnach includes patches for building of "host packages" in variants, e.g. build a python host package only for python3 or python2. but as it is a simple implementation it could be used as well for other purposes. i was tired of compiling "numpy", "scipy" or "scikit" always for both python versions on the host, as this always takes some time. ![:wink:](https://discuss.linuxcontainers.org/images/emoji/google/wink.png?v=5 ":wink:")
    > 
    > i thinkt that's the most important informations. if you use my package feeds, add them as described in the openwrt documentation. IMPORTANT: install at first my feeds than "/scripts/install -p custom... -a" as otherwise i have encountered strange results. after that run the normal feeds package installation.
    > 
    > hopefully it works for you as well as for me. ![:slight_smile:](https://discuss.linuxcontainers.org/images/emoji/google/slight_smile.png?v=5 ":slight_smile:")\
    > at the weekend we have a big birthday party within the family, so i will not be available for most of the time.
    > 
    > bye,
    > 
    > manfred
    > 
    > ps: i hope i have not forgotten something important which is "normal" to me?!? ![:wink:](https://discuss.linuxcontainers.org/images/emoji/google/wink.png?v=5)
    > 
    > ---
    > 
    > PPS: i have forgotten... if you need openwrt images for LXD, you have two options: you can generate an rootfs tarball from the openwrt configuration menu or you use binwalk, etc to extract it from the generated image file.
    > 
    > here is a simple "metadata.yaml" file and the tempaltes i used. it's normal LXD stuff ![:slight_smile:](https://discuss.linuxcontainers.org/images/emoji/google/slight_smile.png?v=5 ":slight_smile:")
    > 
    > ```yaml
    > creation_date: 1525762351
    > expiry_date: 1528354351
    > properties:
    > architecture: mipsel
    > description: openwrt snapshot mipsel (20180516_06:19)
    > name: openwrt-snapshot-mipsel-default-20180516_06:19
    > os: openwrt
    > release: snapshot
    > serial: "20180516_06:19"
    > variant: default
    > templates:
    > /etc/config/system:
    > when:
    > - create
    > - copy
    > create_only: false
    > template: system.tpl
    > properties: {}
    > /etc/hosts:
    > when:
    > - create
    > - copy
    > create_only: false
    > template: hosts.tpl
    > properties: {}
    > 
    > hosts.tpl
    > 127.0.1.1 {{ container.name }}
    > 127.0.0.1 localhost
    > ::1 localhost ip6-localhost ip6-loopback
    > ff02::1 ip6-allnodes
    > ff02::2 ip6-allrouters
    > 
    > system.tpl
    > config system
    > option hostname {{ container.name }}
    > option zonename 'Europe/Vienna'
    > option timezone 'CET-1CEST,M3.5.0,M10.5.0/3'
    > option ttylogin '0'
    > option log_size '64'
    > option urandom_seed '0'
    > ```
    > 
    > ---
    > 
    > Please note, that I managed to track down the failure to mount `/proc`. The root cause of this is that the `atime` flags (`MS_NOATIME`, `MS_RELATIME`, ...) are locked in user namespaces. By default `/proc` will be mounted with `noatime` on `openWRT` but `LXC` will mount `/proc` with `default` options which means that it will be mounted with `relatime`. The kernel will refuse this for aforementioned reasons.\
    > `LXC` now carries a [patch 2](https://github.com/lxc/lxc/commit/69eadddb37352ff29fd785577b9d89c23f522657) upstream that copies the `atime` flags which you can try and backport to your distro.\
    > As a workaround for now you can set:
    > 
    > ```
    > lxc config set <container-name> raw.lxc "lxc.mount.entry = proc proc proc rw,remount,nodev,nosuid,noexec,noatime 0 0"
    > 
    > ```
    > 

### build a openwrt image with kernel LXC enabled

- [LXC on OpenWRT – GNUton's Blog](http://www.gnuton.org/blog/2016/02/lxc-on-openwrt/)

    > **Intro**
    > 
    > LXC stands for LinuX Container. Those containers are some kind of chroot images but on steroids. But you can find a more appropriate definition and info on the internet! ![😀](https://s.w.org/images/core/emoji/11/svg/1f600.svg)
    > 
    > The popular Docker, under the hood, makes use of this technology in order to work and that is what makes this technology so popular nowadays.
    > 
    > LXC is lightweight and it can run on openwrt without any problem. To get it working, btw, you have to enable it in the kernel. In this article i will show you how to build a openwrt image with LXC enabled.
    > 
    > * * * * *
    > 
    > **Let's getting started!**
    > 
    > The documentation availabe at [wiki.openwrt.org](https://wiki.openwrt.org/doc/howto/buildroot.exigence) explains to you how to download the source code from git of the current openwrt release ("Caos Calmer" as for now) . Avoid to download the packages, so **skip** the step:
    > 
    > ```sh
    > ./scripts/feeds install -a
    > ```
    > 
    > That will make the compilation a lot faster. Since you are building the current release, you can always get the packages you need from the official repo.
    > 
    > Once cloned the git repository, you can proceed getting the diff config file from the official repository and add your changes to it.
    > 
    > The diff config file contains all the configuration settings needed to build openwrt for your target board (RPi in my case).
    > 
    > For a raspberry pi this step would look like this:
    > 
    > ```sh
    > wget http://downloads.openwrt.org/chaos_calmer/15.05/brcm2708/bcm2708/config.diff
    > cp config.diff .config
    > cat LXC_PATCH >> .config
    > make defconfig
    > make menuconfig
    > ```
    > 
    > Make menuconfig is optional and it can be used to validate the configuration.
    > 
    > LXC_PATCH files contains the following lines, which add lxc support to the openwrt kernel.
    > 
    > ```sh
    > CONFIG_KERNEL_BLK_CGROUP=y
    > # CONFIG_KERNEL_CC_STACKPROTECTOR_NONE is not set
    > CONFIG_KERNEL_CC_STACKPROTECTOR_REGULAR=y
    > CONFIG_KERNEL_CFQ_GROUP_IOSCHED=y
    > CONFIG_KERNEL_CGROUPS=y
    > CONFIG_KERNEL_CGROUP_CPUACCT=y
    > CONFIG_KERNEL_CGROUP_DEVICE=y
    > CONFIG_KERNEL_CGROUP_FREEZER=y
    > CONFIG_KERNEL_CGROUP_SCHED=y
    > CONFIG_KERNEL_CPUSETS=y
    > CONFIG_KERNEL_DEVPTS_MULTIPLE_INSTANCES=y
    > CONFIG_KERNEL_FREEZER=y
    > CONFIG_KERNEL_IOSCHED_DEADLINE=m
    > CONFIG_KERNEL_IPC_NS=y
    > # CONFIG_KERNEL_KALLSYMS is not set
    > CONFIG_KERNEL_LXC_MISC=y
    > CONFIG_KERNEL_MEMCG=y
    > CONFIG_KERNEL_MEMCG_SWAP=y
    > CONFIG_KERNEL_MM_OWNER=y
    > CONFIG_KERNEL_NAMESPACES=y
    > CONFIG_KERNEL_NETPRIO_CGROUP=y
    > CONFIG_KERNEL_NET_CLS_CGROUP=y
    > CONFIG_KERNEL_NET_NS=y
    > CONFIG_KERNEL_PID_NS=y
    > CONFIG_KERNEL_POSIX_MQUEUE=y
    > CONFIG_KERNEL_RESOURCE_COUNTERS=y
    > CONFIG_KERNEL_USER_NS=y
    > CONFIG_KERNEL_UTS_NS=y
    > ```
    > 
    > The configuation is now in good shape and you can run "make world" ti build a flash able image which can be found in the bin directory
    > 
    > In case you need to re-compile everything from scratch, please make use of *make dirclean* and *make clean*.
    > 
    > If you wanna purge the config too, then run *make distclean*.
    > 
    > The compilation will take a while. Once done you can flash it to your device or SD card in my case according to
    > 
    > the instructions related to your target board.
    > 
    > After flashing the image to the device, SSH onto the device and  install the following package:
    > 
    > ```sh
    > sudo -s
    > 
    > opkg update
    > opkg install iptables-mod-extra kmod-ipt-extra lxc-start lxc-execute lxc-info getopt xz lxc lxc-attach lxc-autostart lxc-cgroup lxc-checkconfig lxc-clone lxc-common lxc-config lxc-configs lxc-console lxc-create lxc-destroy lxc-execute lxc-freeze lxc-hookslxc-info lxc-init lxc-ls lxc-lua lxc-monitor lxc-monitord lxc-snapshot lxc-start lxc-stop lxc-templates lxc-unfreeze lxc-unsharelxc-user-nic lxc-usernsexec lxc-wait lxc-unshare bash debootstrap
    > ```
    > 
    > Bash is needed by all lxc-templates. Debootstrap is needed by some Debian based distribution templates.
    > 
    > Once you have the lxc userspace tools installed, you should check that lxc support in the kernel is fine by running the following command:
    > 
    > ```sh
    > root@opwenrt:/usr/lib/lua/luci# lxc-checkconfig
    > — Namespaces —
    > Namespaces: enabled
    > Utsname namespace: enabled
    > Ipc namespace: enabled
    > Pid namespace: enabled
    > User namespace: enabled
    > Network namespace: enabled
    > Multiple /dev/pts instances: enabled
    > 
    > — Control groups —
    > Cgroup: enabled
    > Cgroup clone_children flag: enabled
    > Cgroup device: enabled
    > Cgroup sched: enabled
    > Cgroup cpu account: enabled
    > Cgroup memory controller: enabled
    > 
    > — Misc —
    > Veth pair device: enabled
    > Macvlan: enabled
    > Vlan: enabled
    > File capabilities: enabled
    > 
    > Note : Before booting a new kernel, you can check its configuration
    > usage : CONFIG=/path/to/config /usr/bin/lxc-checkconfig
    > ```
    > 
    > If you get all options enabled they you get make use of all functionalities that LXC has to offer and you can then proceed  creating your first container:
    > 
    > ```sh
    > lxc-create -t cirros –name mycontainer
    > ```
    > 
    > Remember that the containers are saved in /var/cache/lxc/
    > 
    > Please note that the lxc community package currently comes with a wide set of almost broken templates
    > 

    > ```sh
    > root@Honeypot:/usr/lib/lua/luci# opkg files lxc-templates
    > Package lxc-templates (1.1.1-1) is installed on root and has the following files:
    > /usr/share/lxc/templates/lxc-oracle <– BAD ARCHITECTURE. NO ARM??
    > /usr/share/lxc/templates/lxc-plamo <– depends on “flock”. It may work. I got “Failed to download”
    > /usr/share/lxc/templates/lxc-busybox <– creates the containers, but doesn’t start (busybox no statically linked)
    > /usr/share/lxc/templates/lxc-fedora <– fails to download /releases/20/Fedora/armhfp/os
    > /usr/share/lxc/templates/lxc-sshd <— requires ssh-keygen.
    > /usr/share/lxc/templates/lxc-ubuntu-cloud <– no idea what’s broken
    > /usr/share/lxc/templates/lxc-openmandriva
    > /usr/share/lxc/templates/lxc-gentoo <– requires tar. maybe works >220MB. Ran out of disk on /tmp
    > /usr/share/lxc/templates/lxc-download <– no idea what’s wrong. broken?
    > /usr/share/lxc/templates/lxc-archlinux <– fails require pacman. not available?
    > /usr/share/lxc/templates/lxc-cirros <– WORKS
    > /usr/share/lxc/templates/lxc-debian <– requires debootstrap. maybe broken?
    > /usr/share/lxc/templates/lxc-ubuntu <– requires debootstrap. maybe broken?
    > /usr/share/lxc/templates/lxc-centos <– requires yum. fails container creation
    > /usr/share/lxc/templates/lxc-altlinux <– requires apt-get. fails container creation
    > /usr/share/lxc/templates/lxc-alpine <– requires sha256sum.
    > /usr/share/lxc/templates/lxc-opensuse <– requires zipper. not available?
    > ```
    > 
    > Feel free to check overtime if any of those templates have been fixed, but for the time being only the smallest distro work for me and maybe some of you would prefer to create containers elsewhere and get openwrt download them.
    > 
    > For sure it would be nice to have a openwrt specific containers hub.
    > 
    > Beside those CLI tools,  OpenWRT community repo offers a LuCI web interface package.
    > 
    > This interface offers two main options:
    > 
    > 1.  Management of the current images available. (start, stop, info, config editor)
    > 2.  Download new images from the internet if you have a repository from where you can download images.
    > 
    > For me 1 works as a charme, but I have not managed to get 2 working yet.




### docker binaries for Armhf(armv7l,armv6,...)

- [Install Docker CE from binaries | Docker Documentation](https://docs.docker.com/install/linux/docker-ce/binaries/)

    > ### Install static binaries
    > 
    > 1.  Download the static binary archive. Go to [https://download.docker.com/linux/static/stable/](https://download.docker.com/linux/static/stable/x86_64/) (or change `stable` to `edge` or `test`), choose your hardware platform, and download the `.tgz` file relating to the version of Docker CE you want to install.
    > 
    > 2.  Extract the archive using the `tar` utility. The `dockerd` and `docker` binaries are extracted.
    > 
    >     ```
    >     $ tar xzvf /path/to/\<FILE\>.tar.gz
    > 
    >     ```
    > 
    > 3.  **Optional**: Move the binaries to a directory on your executable path, such as `/usr/bin/`. If you skip this step, you must provide the path to the executable when you invoke `docker` or `dockerd` commands.
    > 
    >     ```
    >     $ sudo cp docker/* /usr/bin/
    > 
    >     ```
    > 
    > 4.  Start the Docker daemon:
    > 
    >     ```
    >     $ sudo dockerd &
    > 
    >     ```
    > 
    >     If you need to start the daemon with additional options, modify the above command accordingly or create and edit the file `/etc/docker/daemon.json` to add the custom configuration options.
    > 
    > 5.  Verify that Docker is installed correctly by running the `hello-world` image.
    > 
    >     ```
    >     $ sudo docker run hello-world
    > 
    >     ```
    > 
    >     This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.
    
    
### Installing, running, using docker on armhf (ARMv7) devices

- [Installing, running, using docker on armhf (ARMv7) devices · umiddelb/armhf Wiki](https://github.com/umiddelb/armhf/wiki/Installing,-running,-using-docker-on-armhf-%28ARMv7%29-devices)




## DNS 設定

- [隱私優先、速度最快，公共DNS服務1.1.1.1上線了 | iThome](https://www.ithome.com.tw/news/122215)

    > 1.1.1.1也強調它是網路上最快的DNS目錄，它的查詢速度只有14.01毫秒，快過Cisco OpenDNS的20.6毫秒、Google Public DNS的34.7毫秒，以及一般ISP業者的68.23毫秒。


- [1.1.1.1 — the Internet’s Fastest, Privacy-First DNS Resolver](https://1.1.1.1/)

## 區網設定

- [請問怎麼兩個同時連線(區網、VPN) - PCZONE 討論區](http://www.pczone.com.tw/vbb3/thread/29/148443/)

    > 目前電腦內有兩個網路(區網、VPN)
    > 想要VPN專門連線上遊戲
    > 其他走區網
    > 不管怎麼設定都是全部走VPN，請網友指導一下
    > 
    > 網路環境是 一組浮動IP透過分享器DHCP至兩台電腦，DMZ設我這台
    > 
    > VPN啟用後命令提示字元鍵入下列指令
    > route change 0.0.0.0 mask 0.0.0.0 XXX.XXX.XXX.XXX
    > route add 0.0.0.0 mask 0.0.0.0 10.0.0.1 metric 50
    > route add 61.215.216.38 10.0.0.1
    > 
    > XXXX是我連外的IP
    > 61.215.216.38是線上遊戲的IP
    > 10.0.0.1是VPN的閘道器
    > 
    > route的用法不太清楚，請指導我一下 謝謝
    > 
    > ---
    > 
    > VPN 內容, TCP/IP 內容, 使用遠端閘道, 不勾, 然後只保留以下這行
    > 引用:
    > 作者: mingbot01 觀看文章
    > route add 61.215.216.38 10.0.0.1


## VPN

- [各种翻墙对比 · Fuck GFW](https://darrenliuwei.com/fuck-gfw/vs.html)

- [VPN原理 - VPN簡介與其應用](https://sites.google.com/site/vpnjianjieyuqiyingyong/xian-kuang-miao-shu/vpn-yuan-li)

    > __VPN原理__
    > 
    > VPN的原理技術很簡單，主要採用的原理技術有四個：穿隧技術（Tunneling）、加解密技術（Encryption & Decryption）、金鑰管理技術（Key management）、使用者與設備身分鑑別技術（Authentication）。
    > 
    > 1.    穿隧技術〈Tunneling〉
    >     穿隧技術其實很簡單，其原理就是將你原本的封包(Packet)視為資料(Data)再重新封裝(Encapsulation)，變成新的封包傳輸在公用網路中。
    > ![](https://sites.google.com/site/vpnjianjieyuqiyingyong/_/rsrc/1420282232007/xian-kuang-miao-shu/vpn-yuan-li/Tunneling.png)
    >     Data：你要傳輸的資料內容。
    >     Header1：內含的 IP Address 是區域或虛擬網路的 IP，或是自訂的 Protocol。
    >     Hearder2：內含的 IP Address 是你要傳輸到對方的IP。
    >     
    >          而穿隧技術是由三種不同的協議所組成的：
    >         1.    Carrier Protocol：用來在網際網路上傳遞封包用的協定。[1]
    >         2.    Encapsulation Protocol：用來包裝原本封包資料用的協定，也就是Header2所使用的協議。例如：GRE、IPSec、PPTP、L2TP....等。[1]
    >         3.    Passenger Protocol：原本封包資料所使用的協定，也就是Header1所使用的協議。[1]
    > 
    >         而Encapsulation Protocol裡的協議會在VPN協議裡作介紹。
    > 
    > 2.    加解密技術〈Encryption & Decryption〉
    >     加解密技術是一個很複雜的，在這我只簡單介紹。對於加密的方法分為兩種：
    > 
    >         1. 對稱式金鑰加密（Symmetric-key algorithm）：又稱為對稱加密、私鑰加密、共享密鑰加密，是密碼學中的一類加密演算法。這類演算法在加密和解密時使用相同的密鑰，或是使用兩個可以簡單地相互推算的密鑰。實務上，這組密鑰成為在兩個或多個成員間的共同祕密，以便維持專屬的通訊聯繫。與公開密鑰加密相比，要求雙方取得相同的密鑰是對稱密鑰加密的主要缺點之一。[3]
    >         
    >         2. 公開金鑰加密〈Public-key cryptography〉：也稱為非對稱加密（asymmetric cryptography），一種密碼學演算法類型，在這種密碼學方法中，需要一對金鑰，一是個私人金鑰，另一個則是公開金鑰。這兩個金鑰是數學相關，用某用戶金鑰加密後所得的資訊，只能用該用戶的解密金鑰才能解密。如果知道了其中一個，並不能計算出另外一個。因此如果公開了一對金鑰中的一個，並不會危害到另外一個的秘密性質。稱公開的金鑰為公鑰；不公開的金鑰為私鑰。[4]
    > 
    >         VPN各個節點間是利用3DES或DES這種對稱式金鑰加密，以達到高傳輸效率。而VPN對於身分認證跟金鑰傳輸是利用非對稱加密的方式。
    > 
    > 3.    金鑰管理技術〈Key management〉
    >     現行常用密鑰管理的技術又可分為SKIP(Simple Key management for IP)與ISAKMP/Oakley (又稱為IKE)兩種。SKIP(Simple Key Management for IP) 利用Diffee-Hellman演算法則， 應用在網路上傳輸密鑰的技術，而ISAKMP/Oakley : Oakley定義如何分辨及確認密鑰，ISA KMP定義分配密鑰的方法。將來會整合在IPv6中。[5]
    > 
    > 4.   使用者與設備身分鑑別技術〈Authentication〉
    >     這個部分是為了確認跟你連接或你所連接VPN對方的身分是不是本人所建立起的機制，主要分為兩種：
    > 
    >         1. 使用者身分鑑別部分：使用者名稱跟密碼、IC卡鑑別‧‧‧等。
    >         2. 設備身分鑑別部分：CA的X.509憑證、分享金鑰。
    >     
    > ---
    > 
    > __VPN協議__
    >     在這我要介紹VPN技術，大概可以分為以下這5種VPN：PPTP、L2TP、IPsec、MPLS、SSL VPN。 
    > 1. 點對點隧道協議PPTP〈Point to Point Tunneling Protocol〉：  
    > 
    >     點對點隧道協議 (PPTP) 是由包括微軟和3Com等公司組成的PPTP論壇開發的一種點對點隧道協，基於撥號使用的PPP協議使用PAP或CHAP之類的加密算法，或者使用 Microsoft的點對點加密算法MPPE。其通過跨越基於 TCP/IP 的數據網絡創建 VPN 實現了從遠程客戶端到專用企業服務器之間數據的安全傳輸。PPTP 支持通過公共網絡(例如 Internet)建立按需的、多協議的、虛擬專用網絡。PPTP 允許加密 IP 通訊，然後在要跨越公司 IP 網絡或公共 IP 網絡(如 Internet)發送的 IP 頭中對其進行封裝。[7]
    > 
    > 2. 第二層隧道協議L2TP〈Layer Two Tunneling Protocol〉：
    > 
    >     L2TP第 2 層隧道協議 (L2TP) 是IETF基於L2F (Cisco的第二層轉發協議)開發的PPTP的後續版本。是一種工業標準 Internet 隧道協議，其可以為跨越面向數據包的媒體發送點到點協議 (PPP) 框架提供封裝。PPTP和L2TP都使用PPP協議對數據進行封裝，然後添加附加包頭用於數據在互聯網絡上的傳輸。PPTP只能在兩端點間建立單一隧道。 L2TP支持在兩端點間使用多隧道，用戶可以針對不同的服務質量創建不同的隧道。L2TP可以提供隧道驗證，而PPTP則不支持隧道驗證。但是當L2TP 或PPTP與IPSEC共同使用時，可以由IPSEC提供隧道驗證，不需要在第2層協議上驗證隧道使用L2TP。 PPTP要求互聯網絡為IP網絡。L2TP只要求隧道媒介提供面向數據包的點對點的連接，L2TP可以在IP(使用UDP)，楨中繼永久虛擬電路 (PVCs),X.25虛擬電路(VCs)或ATM VCs網絡上使用。[7]  
    > 
    > 3. 網際網路安全協定IPsec〈Internet Protocol Security〉：
    > 
    >     IPSec 隧道模式隧道是封裝、路由與解封裝的整個 過程。隧道將原始數據包隱藏(或封裝)在新的數據包內部。該新的數據包可能會有新的尋址與路由信息，從而使其能夠通 過網絡傳輸。隧道與數據保密性結合使用時，在網絡上竊聽通訊的人將無法獲取原始數據包數據(以及原始的源和目標)。封裝的數據包到達目的地後，會刪除封裝，原始數據包頭用於將數據包路由到最終目的地。隧道本身是封裝數據經過的邏輯數據路徑，對原始的源和目的端，隧道是不可見的，而只能看到網絡路徑中的點對點連接。連接雙方並不關心隧道起點和終點之間的任何路由器、交換機、代理服務器或其他安全網關。將隧道和數據保密性結合使用時，可用於提供VPN。封裝的數據包在網絡中的隧道內部傳輸。在此示例中，該網絡是 Internet。網關可以是外部 Internet 與專用網絡間的周界網關。周界網關可以是路由器、防火牆、代理服務器或其他安全網關。另外，在專用網絡內部可使用兩個網關來保護網絡中不信任的通訊。當以隧道模式使用 IPSec 時，其只為 IP 通訊提供封裝。使用 IPSec 隧道模式主要是為了與其他不支持 IPSec 上的 L2TP 或 PPTP VPN 隧道技術的路由器、網關或終端系統之間的相互操作。[7]
    > 
    > 4. 多重通訊協定標籤交換傳輸MPLS〈Multi-Protocol Label Switching〉：
    > 
    >     
    >     多重通訊協定標籤交換傳輸(Multi-Protocol Label Switching)是由IETF 所發展出來的Network Standard。它是實現寬頻網際網路最熱門的技術；其目的是要提供一個更具彈性、擴充性及效率更高的IP層交換技術。MPLS 是一種整合了標籤交換架構與網路層的路由機制的技術，最基本的概念是將進入MPLS Network 的封包(Packet)配置一個固定長度的標籤(Label)，在MPLS Network中Packet會根據標籤(Label) 做Forwarding , 由Label來決定Packet在網路上的路徑，不會再看 Layer 3的 IP Header(標頭)。[8]
    > 
    > 5. 安全通訊協定SSL VPN〈Secure Sockets Layer VPN〉：
    > 
    >     SSL協議提供了數據私密性、端點驗證、信息完整性等特性。SSL協議由許多子協議組成，其中兩個主要的子協議是握手協議和記錄協議。握手協議允許服務器 和客戶端在應用協議傳輸第一個數據字節以前，彼此確認，協商一種加密算法和密碼鑰匙。在數據傳輸期間，記錄協議利用握手協議生成的密鑰加密和解密後來交換 的數據。SSL獨立於應用，因此任何一個應用程序都可以享受它的安全性而不必理會執行細節。SSL置身於網絡結構體系的 傳輸層和應用層之間。此外，SSL本身就被幾乎所有的Web瀏覽器支持。這意味著客戶端不需要為了支持SSL連接安裝額外的軟件。這兩個特徵就是SSL能 應用於VPN的關鍵點。[7]
    > 
    > ---
    > 
    > __VPN Gate__
    > 
    > VPN Gate 學術實驗專案是一個線上服務，由日本國立築波大學研究生院為學術研究目的運營。研究的目的是推廣 "全球分散式公共 VPN 中繼伺服器" 的知識。而VPN Gate 的伺服器是由世界各地的志願者所提供的，而它有以下幾個優點：
    > [6]
    > 
    > ![](https://sites.google.com/site/vpnjianjieyuqiyingyong/_/rsrc/1420447599449/vpn-shi-zuo/vpngate/%E5%9C%96%E7%89%871.png)
    > 
    > 1. 任何平台與作業系統都可以使用，包括Window、Mac、Android‧‧‧等。
    > 2. 支援SSL VPN、L2TP/IPsec、Open VPN、Microsoft SSTP 多項協議技術。
    > 3. 無須註冊帳號，直接使用。
    > 
    > 它並不是只有優點，還有幾點要注意的：
    > 
    > 1. 每個VPN伺服器的IP是不固定的，IP地址會不定期更換。
    > 2. 每天的VPN伺服器數量會不一樣，這要看志願者有沒有開放。
    > 3. 使用VPN Gate 盡量不要傳輸信用卡之類的個人機密數據。
    > 4. 使用時盡量不要用太多流量。
    > 
    > 上面第三點的原因是因為不知道你連的VPN伺服器有沒有問題，在使用中盡量不要上網刷卡買東西之類的，VPN雖然安全，但是不能防VPN內部網路出現的問題。而對於第四點，是因為你連的是志願者所提供的伺服器，用的流量是你所連的伺服器的，所以不要用太多流量。接下來我要介紹VPN Gate 要如何使用。
    > 
    > ![](https://sites.google.com/site/vpnjianjieyuqiyingyong/_/rsrc/1420448243702/vpn-shi-zuo/vpngate/123.png)
    > 
    > 這是進到VPN Gate 官網〈[http://www.vpngate.net/ja/](http://www.vpngate.net/ja/)〉後看到的畫面，先選擇你想要連的國家，之後再選擇你要的連接方法即可。下幾篇會介紹如何連接。
    >     
    >     

- [Can I make a computer connecting via VPN visible to computers within the network it is connecting to? - Server Fault](https://serverfault.com/questions/130014/can-i-make-a-computer-connecting-via-vpn-visible-to-computers-within-the-network)

    > By definition, once you set up a VPN you are part of the remote network; if you examine your network interfaces, you'll see you have a new one, which is your VPN interface and has an IP address belonging to the remote network; this is the IP address you must connect to from the remote machine.
    > 
    > If your network is 192.168.1.x and your local IP address is 192.168.1.2, and the remote network is 10.0.0.x and the remote machine is 10.0.0.10, when you establish a VPN connection you will acquire a new virtual network interface, which will have an address like 10.0.0.42; you should connect to this one, not to 192.168.1.2, which just doesn't exist from the remote network's point of view.
    > 
    > So, if from 10.0.0.10 you try to connect to 192.168.1.2, it will not (ordinarily) work; if you instead connect to 10.0.0.42, it should work.
    > 
    > If it doesn't, then either you have a local firewall on your system which doesn't accept connections on the VPN interface, or the VPN server is configured to not let you talk to remote machines and/or not let remote machines talk to you.
    > 


## HTTPS/SSL certificate

- [NGINX 使用 Let’s Encrypt 免費 SSL 憑證設定 HTTPS 安全加密網頁教學 - G. T. Wang](https://blog.gtwang.org/linux/secure-nginx-with-lets-encrypt-ssl-certificate-on-ubuntu-and-debian/)

- [SSL For Free 免費 SSL 憑證申請，使用 Let's Encrypt 最簡單方法教學！](https://free.com.tw/ssl-for-free/)

- [SSL For Free - Free SSL Certificates in Minutes](https://www.sslforfree.com/)

## 分散式 distributed network

- [Are there any Distributed/mesh-like/P2P VPNs? - Server Fault](https://serverfault.com/questions/685820/are-there-any-distributed-mesh-like-p2p-vpns)

    > I'm not sure whether it completely fulfils your needs, but you should probably take a look at tinc: [http://www.tinc-vpn.org/](http://www.tinc-vpn.org/). It quite closely matches the mesh network orchestrated by a central server as you described, but I'm not sure whether it will succeed in discovering peers in your local network.
    > 
    > ---
    > 
    > The easiest mesh vpn I have found and used is PeerVPN ([http://www.peervpn.net/](http://www.peervpn.net/)).
    > 
    > PeerVPN Features
    > 
    > - Ethernet tunneling support using TAP devices.
    > - IPv6 support.
    > - Full mesh network topology.
    > - Automatically builds tunnels through firewalls and NATs without any further setup (for example, port forwarding).
    > - Shared key encryption and authentication support.
    > 
    > Configuration is simple.. one config file you edit and for basic mesh vpn there are only 6 settings you need to specify see the PeerVPN tutorial which is only 1 page: [http://www.peervpn.net/tutorial/](http://www.peervpn.net/tutorial/)
    > 
    > The PSK encryption/authentication key can be upto 512 bits (64 bytes).
    > 
    > I've set peervpn up so far on multiple remote servers and it works very well. Also, there is no requirement for a "super-node" as you may encounter in other mesh vpn implementations.
    > 
    > Nodes in peervpn learn about newly added nodes to the VPN automatically w/no need to change configurations. Node to node traffic is also direct and not thru some central vpn hub.
    > 
    > Note: read the default peervpn.conf file to learn about alot of other options you "can" take advantage of. But for the basic mesh vpn as I stated you only need to set 6 options (name of vpn, PSK, local tunnel end point IP address, interface "name" you want to see/use on your linux system & port number to use for "that" vpn ... note you can use peervpn for multiple independent VPNs on a server)
    > 
    > ---
    > 
    > I had the exact same problem years ago. I had ~30 offices that all needed to be able to directly communicate, but they were set up in a 'hub-and-spoke' configuration. I wrote a tool in Python to automatically generate the n x (n-1)/2 number of connections in OpenVPN between the offices. Later on I added in support for RIP routing between the sites after a bizarre Comcast issue where one office could see all the others, but not the main office. Finally I added the ability to auto-generate reverse DNS for the link IPs and the ability to push the packages out to each router.
    > 
    > Take a look at [OpenMesher](https://github.com/heyaaron/openmesher/). Just this morning I decided to dust it off for an upcoming project. Hopefully it does what you want. If not, feel free to submit an issue and I'll help.
    > 

### IPOP

- [ipop-project/ipop-project.github.io: Current Wiki and Documentation for IPOP](https://github.com/ipop-project/ipop-project.github.io)

- [IPOP (IP-Over-P2P) - IPOP](http://ipop-project.org/)

    > IPOP (IP-Over-P2P) is an open-source user-centric software virtual network allowing end users to define and create their own virtual private networks (VPNs). IPOP virtual networks provide end-to-end tunneling of IP or Ethernet over Tincan links setup and managed through a control API to create various software-defined VPN overlays.
    > Unique Features
    > 
    > - In contrast to typical VPN technologies, which require complex setup, management and a gateway to relay VPN traffic, IPOP is straightforward to configure, because:
    > - It runs on existing Internet infrastructure, without requiring any specialized networking infrastructure (e.g. hardware switches/routers, or virtual routers);
    > - It uses online social network (OSN) infrastructures to allow users to define their own networks;
    > - It seamlessly traverses firewalls, NATs, and create VPN tunnels in a peer-to-peer fashion, avoiding the need for centralized VPN gateways.
    > 

- [IPOP (IP-over-P2P) Virtual Network Tutorial | FutureSystems Portal](https://portal.futuresystems.org/tutorials/ipop1)

- [Tutorial: Deploying Your Own P2P Overlay for IPOP VPNs | FutureSystems Portal](https://portal.futuresystems.org/tutorials/ipop2)


### meshbird

- [meshbird/meshbird: Distributed private networking](https://github.com/meshbird/meshbird)

### n2n

- [Tech黑手 - 工作雜記: n2n - P2P VPN](https://chunchaichang.blogspot.tw/2010/04/n2n-p2p-vpn.html)

    > n2n - 這是一個開源的 P2P VPN 套件，由知名也是開源的網管軟體-ntop 的作者所開發，軟體特色有：
    > 
    > - 開放原始碼的套件
    > - 建立連線時毋需通過第三方的主機認證
    > - 可獨立運作，無須仰賴官方主機的介接， 安全性高。
    > - 可適用 NAT 防火牆環境。
    > - 可建立多個n2n網路組。
    > - 容易安裝及使用。
    > - 如果使用公用的 supernode，則所有的node 都不需要佔用到 public IP。
    > - 不需要建立 central server，各 node 之間即可以作連線。

### ZeroTier

- [在Linux容器中使用ZeroTier P2P VPN | Soul Of Free Loop](https://zohead.com/archives/zerotier-container/)

    > 关于 ZeroTier P2P VPN
    > 
    > P2P VPN 和我们平常使用的 PPTP、OpenVPN 等 VPN 的不同之处在于其只负责将两个或多个主机通过点对点的方式进行连接，不需要中心服务器支持，多个主机之间通过 STUN 打洞或者 TURN 中继等方式进行连接，比较适合不同网络间的多个主机进行直接连接，不像 PPTP 这种在国内用的最多的就是拿来爬墙的。
    > 
    > 目前使用的比较多的包括 n2n、tinc 和本文要介绍的 ZeroTier 等几种免费开源的 P2P VPN 软件。
    > 
    > n2n 由于已经没人继续开发支持了所以不予考虑，我在对比了 tinc 和 ZeroTier 之后发现 ZeroTier 虽然看起来性能比 tinc 略差一点，但其客户端配置步骤非常简单，不需要像 tinc 那样要在多个主机分别手工生成配置文件，而且 ZeroTier 自己也自带了几个不同国家区域的中继服务器方便普通用户使用，另外一点就是本文要介绍的 ZeroTier 支持在 Linux 容器中使用，因此平时我主要使用 ZeroTier，tinc 用作辅助。
    > 


### SoftEther

- [SoftEther VPN Open Source - SoftEther VPN Project](https://www.softether.org/)


### Private Tor Network

- [antitree/private-tor-network: Run an isolated instance of a tor network in Docker containers](https://github.com/antitree/private-tor-network)

### Tinc

- [Tinc VPN](https://www.tinc-vpn.org/)

    > What is tinc?
    > 
    > tinc is a Virtual Private Network (VPN) daemon that uses tunnelling and encryption to create a secure private network between hosts on the Internet. tinc is Free Software and licensed under the GNU General Public License version 2 or later. Because the VPN appears to the IP level network code as a normal network device, there is no need to adapt any existing software. This allows VPN sites to share information with each other over the Internet without exposing any information to others. In addition, tinc has the following features:
    > 
    > - Encryption, authentication and compression
    > All traffic is optionally compressed using zlib or LZO, and LibreSSL or OpenSSL is used to encrypt the traffic and protect it from alteration with message authentication codes and sequence numbers.
    > 
    > - Automatic full mesh routing
    > Regardless of how you set up the tinc daemons to connect to each other, VPN traffic is always (if possible) sent directly to the destination, without going through intermediate hops.
    > 
    > - NAT traversal
    > As long as one node in the VPN allows incoming connections on a public IP address (even if it is a dynamic IP address), tinc will be able to do NAT traversal, allowing direct communication between peers.
    > 
    > - Easily expand your VPN
    > When you want to add nodes to your VPN, all you have to do is add an extra configuration file, there is no need to start new daemons or create and configure new devices or network interfaces.
    > 
    > - Ability to bridge ethernet segments
    > You can link multiple ethernet segments together to work like a single segment, allowing you to run applications and games that normally only work on a LAN over the Internet.
    > 
    > - Runs on many operating systems and supports IPv6
    > Currently Linux, FreeBSD, OpenBSD, NetBSD, OS X, Solaris, Windows 2000, XP, Vista and Windows 7 and 8 platforms are supported. See our section about supported platforms for more information about the state of the ports. tinc has also full support for IPv6, providing both the possibility of tunneling IPv6 traffic over its tunnels and of creating tunnels over existing IPv6 networks.
    > 


## 翻牆

- [cms88168/docker-ShadowsocksR: ShadowsocksR Server (https://github.com/breakwa11/shadowsocks/tree/manyuser) for Docker](https://github.com/cms88168/docker-ShadowsocksR)

- [第一次用 Docker 自架 v2ray + shadowsocks 翻牆伺服器就上手](https://blog.birkhoff.me/use-docker-to-deploy-vmess-and-ss-using-docker/)

- [breakwa11/shadowsocksr - Docker Hub](https://hub.docker.com/r/breakwa11/shadowsocksr/)

### zeronet

- [HelloZeroNet/ZeroNet: ZeroNet - Decentralized websites using Bitcoin crypto and BitTorrent network](https://github.com/HelloZeroNet/ZeroNet)










