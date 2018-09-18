# Linux__問題排解1-1

[toc]
<!-- toc --> 

## Ubuntu

### Codename
- [Releases - Ubuntu Wiki](https://wiki.ubuntu.com/Releases)




### iPhone無法充電

- [[ubuntu] 17.10 doesn't charge/recognize iPhone when plugged in](https://ubuntuforums.org/showthread.php?t=2376741)

    > 在ACTION=="add" 那一行最後加上RUN+="/usr/sbin/usbmuxd" 讓它每次插入iPhone時都會啟動usbmuxd 服務
    > 
    > Code:
    > 
    > ```shell
    > $ cat /lib/udev/rules.d/39-usbmuxd.rules
    > # usbmuxd (Apple Mobile Device Muxer listening on /var/run/usbmuxd)
    > 
    > # Initialize iOS devices into "deactivated" USB configuration state and activate usbmuxd
    > ACTION=="add", SUBSYSTEM=="usb", ATTR{idVendor}=="05ac", ATTR{idProduct}=="12[9a][0-9a-f]", ENV{USBMUX_SUPPORTED}="1", ATTR{bConfigurationValue}="0", OWNER="usbmux", TAG+="systemd", ENV{SYSTEMD_WANTS}="usbmuxd.service", RUN+="/usr/sbin/usbmuxd"
    > 
    > # Exit usbmuxd when the last device is removed
    > ACTION=="remove", SUBSYSTEM=="usb", ENV{PRODUCT}=="5ac/12[9a][0-9a-f]/*", ENV{INTERFACE}=="255/*", RUN+="/usr/sbin/usbmuxd -x"
    > ```
    > 


### change hard drive name

- [rename - How to change hard drive name - Ask Ubuntu](https://askubuntu.com/questions/904561/how-to-change-hard-drive-name/904564#_=_)

    > The easiest way to do this would be to do it with GUI
    > 
    > -   Go to **disk app** (through Unity Dash or terminal with `gnome-disks` command)
    > -   Choose your **partition**
    > -   Click the little **gear** icon [![Gear icon](https://i.stack.imgur.com/LqMJB.png)](https://i.stack.imgur.com/LqMJB.png)
    > -   Select **Edit mount options**
    > -   Toggle **Automatic Mount Option** to *Off*
    > -   Edit mount point to `/media/ronin_cunningham/StorageDevice`
    > 
    > On a side note, this will also enable your partition to be mounted automatically on start up, **If** you don't want that to happen then make sure to
    > 
    > -   Un-mark **Mount at Startup**
    > 
    > You'd want to do this if your **Bootup times** are slow
    > 
    > * * * * *
    > 
    > [![screenshot of gnome-disk app](https://i.stack.imgur.com/9q6am.png)](https://i.stack.imgur.com/9q6am.png) *Theme might not look exactly like this*

### rc.local systemd 設置

- [Ubuntu 18.04 rc.local systemd设置 - CSDN博客](https://blog.csdn.net/zhengchaooo/article/details/80202599)

    > ###### ubuntu18.04不再使用initd管理系统，改用systemd。
    > 
    > ###### 然而systemd很难用，改变太大，跟之前的完全不同。
    > 使用systemd设置开机启动\
    > 为了像以前一样，在/etc/rc.local中设置开机启动程序，需要以下几步：\
    > 1、systemd默认读取/etc/systemd/system下的配置文件，该目录下的文件会链接/lib/systemd/system/下的文件。一般系统安装完/lib/systemd/system/下会有rc-local.service文件，即我们需要的配置文件。
    > 
    > 链接过来：
    > 
    > ```shell
    > ln -fs /lib/systemd/system/rc-local.service /etc/systemd/system/rc.local.service
    > ```
    > 
    > ```shell
    > cd /etc/systemd/system/
    > cat rc.local.service
    > ```
    > 
    > rc.local.service内容
    > 
    > ```shell
    > #  SPDX-License-Identifier: LGPL-2.1+
    > #
    > #  This file is part of systemd.
    > #
    > #  systemd is free software; you can redistribute it and/or modify it
    > #  under the terms of the GNU Lesser General Public License as published by#  the Free Software Foundation; either version 2.1 of the License, or
    > #  (at your option) any later version. 
    > 
    > # This unit gets pulled automatically into multi-user.target by
    > # systemd-rc-local-generator if /etc/rc.local is executable.
    > [Unit]
    > Description=/etc/rc.local Compatibility
    > Documentation=man:systemd-rc-local-generator(8)
    > ConditionFileIsExecutable=/etc/rc.local
    > After=network.target 
    > 
    > [Service]
    > Type=forking
    > ExecStart=/etc/rc.local start
    > TimeoutSec=0
    > RemainAfterExit=yes
    > GuessMainPID=no 
    > 
    > [Install]
    > WantedBy=multi-user.target
    > Alias=rc.local.service
    > ```
    > 
    > 1) [Unit] 区块：启动顺序与依赖关系。 
    > 
    > 2) [Service] 区块：启动行为,如何启动，启动类型。 
    > 
    > 3) [Install] 区块，定义如何安装这个配置文件，即怎样做到开机启动。
    > 
    > 
    > 2、创建/etc/rc.local文件
    > 
    > ```shell
    > touch /etc/rc.local
    > ```
    > 
    > 3、赋可执行权限
    > 
    > ```shell
    > chmod 755 /etc/rc.local
    > ```
    > 
    > 4、编辑rc.local，添加需要开机启动的任务
    > 
    > ```shell
    > #!/bin/bash
    > 
    > echo "test rc " > /var/test.log
    > ```
    > 
    > 5、执行reboot重启系统，然后查看test.log
    > 

### Set default application

- [Set default application using `xdg-mime` | Guy Rutenberg](https://www.guyrutenberg.com/2018/01/20/set-default-application-using-xdg-mime/)

    > You can use the `xdg-mime` utility to query the default mime-type associations and change them.
    > 
    > ```
    > xdg-mime query default video/mp4
    > ```
    > 
    > Will return the `.desktop` file associated with the default app to open mp4 files. To change the default association:
    > 
    > ```
    > xdg-mime default vlc.desktop video/mp4
    > ```
    > 
    > you need to specify the `desktop` file to open files of the specified mime type. To check the mime-type of a given file, use
    > 
    > ```
    > file -ib filename
    > ```
    > 

### where to store default application

- [xdg - Open a directory in the default file manager and select a file - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/364997/open-a-directory-in-the-default-file-manager-and-select-a-file)
    > 
    > `xdg-mime` uses `mimeapps.list` to determine the default application to use.
    > 
    > 
    > `mimeapps.list` lists default applications for a given mimetype under [Default Applications] section. It allows to list multiple default applications in their decreasing order of preference. For example :
    > 
    > ```
    > [Default Applications]
    > mimetype1 = default1.desktop;default2.desktop;
    > ```

- Find location of `mimeapps.list`

    > ```shell
    > sudo find . -name mimeapps.list
    > ```
    > 
    > returns:
    > 
    > ```shell
    > ./usr/share/gdm/greeter/applications/mimeapps.list
    > ./home/allenyl/.config/mimeapps.list
    > ```
    > 
    > the `/home/allenyl/.config/mimeapps.list` is where to store the user value
    > 
    > [name=Ya-Lun Li]



### Ubuntu 18.04 hangs on booting with message "started user manager for uid 120"

- [boot - Ubuntu 18.04 hangs on booting with message "started user manager for uid 120" on Asus 1015PX - Ask Ubuntu](https://askubuntu.com/questions/1037922/ubuntu-18-04-hangs-on-booting-with-message-started-user-manager-for-uid-120-on)

    > Enter Ubuntu by recovery mode, from the main menu choose the first option, the one about the restart, give always ok and you should arrive to the desktop; once in, update and upghrade everithing and after that open a terminal and type "sudo nano /etc/gdm3/custom.conf" , once the file is opened, in the [daemon] section uncoment "WaylandEnable=false" , save and restart, problem fixed ;-) .


- [17.10 to 18.04 upgrade freezes during boot - Ask Ubuntu](https://askubuntu.com/questions/1036242/17-10-to-18-04-upgrade-freezes-during-boot#1037192)

    > **Update #7:**
    > 
    > Turns out that the problem isn't a gdm3 vs lightdm problem. It's a gdm3/wayland problem with older Intel GPU's. To fix...
    > 
    > In `terminal`...
    > 
    > -   `cd /etc/gdm3` # change directory
    > -   `sudo pico custom.conf` # edit this file
    > 
    > Find and change:
    > 
    > `#WaylandEnable=false`
    > 
    > To this:
    > 
    > `WaylandEnable=false`
    > 
    > Save the file.
    > 
    > -   `sudo dpkg-reconfigure gdm3` # select gdm3 DM
    > 
    > Select gdm3 and OK.
    > 
    > -   `reboot` # reboot the computer
    > 
    > 

### Kworker consuming too many resource

- [linux - How interpret kworker threads names? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/152819/how-interpret-kworker-threads-names)

    > According to [kernel.org](https://www.kernel.org/doc/Documentation/kernel-per-CPU-kthreads.txt), the syntax is `kworker/%u:%d%s (cpu, id, priority)`. The `u` designates a special CPU, the unbound cpu, meaning that the kthread is currently unbound.
    > 
    > The workqueue workers which have negative nice value have 'H' postfixed to their names. ([source](https://lkml.org/lkml/2013/3/19/661))
    > 

- [Kworker, what is it and why is it hogging so much CPU? - Ask Ubuntu](https://askubuntu.com/questions/33640/kworker-what-is-it-and-why-is-it-hogging-so-much-cpu)

    > "kworker" is a placeholder process for kernel worker threads, which perform most of the actual processing for the kernel, especially in cases where there are interrupts, timers, I/O, etc. These typically correspond to the vast majority of any allocated "system" time to running processes. It is not something that can be safely removed from the system in any way, and is completely unrelated to nepomuk or KDE (except in that these programs may make system calls, which may require the kernel to do something).
    > 
    > There were some reports of excessive kworker activity for relatively idle systems starting during 2.6.36 development ([example discussion](https://lkml.org/lkml/2011/3/29/2)), and wide reports of confusion and problems with 2.6.38 (although many of these reports include the word "Natty", so I presume these people not to have used any kernel between 2.6.35 (distributed in Ubuntu 10.10) and 2.6.38 (distributed in Ubuntu 11.04).
    > 
    > I've found many reports of something that "fixed" this for one or another user. Most "fixes" seem to be related to updates of the kernel of various sorts. Where the update can be tracked to a specific issue, it seems to often be some driver or kernel service that has been patched to not misbehave: I have the impression that there are a very large number of things in the kernel that can cause a behaviour which is observed as excessive kworker usage.
    > 
    > If you find the system unusable due to excessive kworker activity, I would recommend trying to do fewer things. If you think you're not doing anything, try shutting down long-running services or timers (RSS readers, mail readers, file indexers, activity trackers, etc.). If this doesn't work, try restarting. If your system allows you to enable or disable hardware in a pre-boot environment, try turning off hardware you aren't using. If it happens on every restart before you do anything, you could try uninstalling things, but at this point you'll want to be running syscall profiling tools to track down specific applications that seem to be causing this overload.
    > 
    > It is to be hoped that your specific system will stop expressing this behaviour with a future kernel upgrade (and many of the most common causes of this have been solved).
    > 
    > ---
    > 
    > **What is kworker?** `kworker` means a Linux kernel process doing "work" (processing system calls). You can have several of them in your process list: `kworker/0:1` is the one on your first CPU core, `kworker/1:1` the one on your second etc..
    > 
    > **Why does kworker hog your CPU?** To find out why a kworker is wasting your CPU, you can create CPU backtraces: watch your processor load (with `top` or something) and in moments of high load through `kworker`, execute `echo l > /proc/sysrq-trigger` to create a backtrace. (On Ubuntu, this needs you to login with `sudo -s`). Do this several times, then watch the backtraces at the end of `dmesg` output. See what happens frequently in the CPU backtraces, it hopefully points you to the source of your problem.
    > 
    > **Example: e1000e.** In my case, I found a backtrace like this nearly every time:
    > 
    > ```
    > Call Trace:
    >  delay_tsc+0x4a/0x80
    >  __const_udelay+0x2c/0x30
    >  e1000_acquire_swflag_ich8lan+0xa2/0x240 [e1000e]
    >  e1000e_read_phy_reg_igp+0x29/0x80 [e1000e]
    >  e1000e_phy_has_link_generic+0x85/0x120 [e1000e]
    >  e1000_check_for_copper_link_ich8lan+0x48/0x930 [e1000e]
    >  e1000e_has_link+0x55/0xd0 [e1000e]
    >  e1000_watchdog_task+0x5e/0x960 [e1000e]
    > 
    > ```
    > 
    > It hinted me to a problem in the `e1000e` Ethernet card module, and indeed a `sudo rmmod e1000e` made the high CPU load go away immediately [[e1000e bug #26](http://sourceforge.net/p/e1000/bugs/26/)].
    > 
    > ---
    > 
    > -   `echo l > /proc/sysrq-trigger` seems to not work on proxmox saying `sysrq: SysRq : This sysrq operation is disabled.` sadly. -- [hak8or](https://askubuntu.com/users/184175/hak8or "101 reputation") [Jan 29 at 0:51](https://askubuntu.com/questions/33640/kworker-what-is-it-and-why-is-it-hogging-so-much-cpu#comment1618295_421916)
    > 
    > -   sysrq need to be reenabled with sysctl -w kernel.sysrq=1 see [askubuntu.com/questions/911522/...](https://askubuntu.com/questions/911522/how-can-i-enable-the-magic-sysrq-key-on-ubuntu-desktop "how can i enable the magic sysrq key on ubuntu desktop") -- [Sebastien](https://askubuntu.com/users/325483/sebastien "101 reputation") [Apr 6 at 6:36](https://askubuntu.com/questions/33640/kworker-what-is-it-and-why-is-it-hogging-so-much-cpu#comment1660494_421916)
    > 
    > ---
    > 
    > Why does kworker hog your CPU (cont.)? As an alternative to my other answer here, Perf is a more professional way to analyse what kernel tasks are hogging your CPU:
    > 
    >     Install perf:
    > 
    >     sudo apt-get install linux-tools-common linux-tools-3.11.0-15-generic
    > 
    >     (The second package must match your kernel version. You can first install just linux-tools-common and call perf to let it tell you which package it needs.)
    > 
    >     Record some 10 seconds of backtraces on all your CPUs:
    > 
    >     sudo perf record -g -a sleep 10
    > 
    >     Analyse your recording:
    > 
    >     sudo perf report
    > 
    >     (Navigate the call graph with ←, →, ↑, ↓ and Enter.)
    > 
    > 

### enable the "magic sysrq key"

- [How can I enable the "magic sysrq key" on ubuntu desktop? - Ask Ubuntu](https://askubuntu.com/questions/911522/how-can-i-enable-the-magic-sysrq-key-on-ubuntu-desktop)

    > To enable sysrq magic keys temporarily:
    > 
    > `# echo "1" > /proc/sys/kernel/sysrq`
    > 
    > or `# sysctl -w kernel.sysrq=1`
    > 
    > This enables sysrq magic keys for the current user session. You can disable it again by exchanging 1 with 0 in the above commands. Or go back to the standard value of **176**.
    > 
    > To enable these changes at boot time one has to create config file in the sysctl.d directory (e.g. /etc/sysctl.d/90-sysrq.conf) with this line:
    > 
    > ```
    > kernel.sysrq=1
    > 
    > ```
    > 
    > So setting /proc/sys/kernel/sysrq to **1** enables the sysrq magic keys, setting it to **0** disables it.


- [linux - What does "sudo -s" actually do? - Super User](https://superuser.com/questions/306923/what-does-sudo-s-actually-do)

    > 
    > `sudo -s` runs the shell specified in your `$SHELL` environment variable as the superuser/root. You can specify another user using `-u`.
    > 
    > The `$SHELL` environment variable contains the path to the user's default login shell. The actual setting for the default shell program is usually in `etc/passwd`. Depending on what you've done in your current session, the $SHELL variable may not contain the shell program you're currently using. If you login automatically with zsh for instance, but then invoke bash, $SHELL won't change from `/bin/zsh`.
    > 
    > Show the current user and shell program: `echo $(whoami) is logged in and shell is $0`
    > 
    > -   `whoami` prints out the username the user is working under.
    > -   `$0` contains the name/path of the currently running program (shell program in this case).
    > 
    > ---
    > 
    > The major difference between sudo -i and sudo -s is:
    > 
    >     sudo -i gives you the root environment, i.e. your ~/.bashrc is ignored.
    >     sudo -s gives you the user's environment, so your ~/.bashrc is respected.
    > 




### can't set Launch at session startup

> Check the owner of `~/.config/autostart/` is current user or not. If not, `chown user:user -R ~/.config/autostart/` 
> [name=Ya-Lun Li]


### Can't add Custom .desktop files to Ubuntu dock

- [17.10 - Can't add Custom .desktop files to Ubuntu dock - Ask Ubuntu](https://askubuntu.com/questions/967409/cant-add-custom-desktop-files-to-ubuntu-dock)

    > 1.  Create a `.desktop` file in `~/.local/share/applications`.
    > 2.  Add the following lines in it
    > 
    >     ```
    >     [Desktop Entry]
    >     Comment=Chrome my profile
    >     Terminal=false
    >     Name=My Chrome
    >     Exec=google-chrome --profile-directory=Default
    >     Type=Application
    >     Icon=google-chrome
    > 
    >     ```
    > 
    >     (I'm naming it "My Chrome" to avoid confusion with the already existing Google Chrome launcher. You can use any other name.)
    > 
    > 3.  Make it executable.
    > 
    > 4.  Click on *Activities* or *Show Applications* and search for "My Chrome". It should appear.
    > 
    > 5.  Right click on it and mark as favourite.
    > 
    >     When right clicking on application icon in dock doesn't show "*Add to favourites*" option, search for the application in *Activities* screen, and then **drag it across to the dock** (suggested by [Legolas](https://askubuntu.com/users/611441/legolas)).
    > 
    > If nothing works, see this Q&A: [Cannot add custom launcher to Dock (*Add to Favorites*)](https://askubuntu.com/questions/990833/cannot-add-custom-launcher-to-dock-add-to-favorites)
    > 
    > ---
    > 
    > 
    > Yes, of course, you can't put ~ in the .desktop file, you'll have to put the full path (there is no ~ in the content of the sample .desktop file though). – pomsky May 28 at 18:01
    > 
    > ---
    > 
    > For anyone if the application is not appearing in Activities, make sure you dote have "NoDisplay=true" in the .desktop file for your application.







### Duplicate Icons in the dock of GNOME Shell

- [Duplicate Icons in the dock of GNOME Shell, Ubuntu 17.10 - Ask Ubuntu](https://askubuntu.com/questions/975178/duplicate-icons-in-the-dock-of-gnome-shell-ubuntu-17-10#975230)

    > 1.  Open Files and go to your `/usr/share/applications` folder. Look for the "Nightly" file and copy it.
    > 2.  Paste the file in `~/.local/share/applications`. It should look like a file with the name `<filename>.desktop`.
    > 3.  Right click on this `.desktop` file and open with Text Editor.
    > 4.  Launch "Nightly" from "*Activities*".
    > 5.  Run `xprop WM_CLASS` in Terminal.
    > 6.  Place the cursor over the opened "Nightly" window. The cursor should turn into a crosshair already. Click. You should get a `WM_CLASS` string for "Nightly" in Terminal.
    > 7.  In the `.desktop` file opened in Text Editor and add the following line
    > 
    >     ```
    >     StartupWMClass=OBTAINED-VALUE
    > 
    >     ```
    > 
    >     In place of `OBTAINED-VALUE` put a value you got from step 6 without any quotes.
    > 
    > 8.  Save the `.desktop` file.
    > 
    > ---
    > 
    > I am trying to do the same with PyCharm. Got "sun-awt-X11-XFramePeer", "jetbrains-pycharm-ce" as the output for step 6. I used StartupWMClass=jetbrains-pycharm-ce and it works. – d4nyll
    > 
    > ---
    > 
    > 9. Rename .desktop file to OBTAINED-VALUE.desktop (e.g. jetbrains-phpstorm.desktop instead phpstorm.desktop), works in Ubuntu 18.04 – Aleksey Deryagin


### Add menu option to favoured app launcher in Ubuntu dock

- [18.04 - Add menu option to favoured app launcher in Ubuntu dock - Ask Ubuntu](https://askubuntu.com/questions/1031780/add-menu-option-to-favoured-app-launcher-in-ubuntu-dock)

    > Follow the steps below.
    > 
    > 1.  Copy `.desktop` file associated to your preferred application, say `app-name.desktop` from `/usr/share/applications/` to `~/.local/share/applications/`. You can do this by running the following command in Terminal
    > 
    >     ```
    >     cp /usr/share/applications/app-name.desktop ~/.local/share/applications/
    > 
    >     ```
    > 
    > 2.  Open the `.desktop` file using a text-editor, for example by running
    > 
    >     ```
    >     gedit ~/.local/share/applications/app-name.desktop
    > 
    >     ```
    > 
    > 3.  Look for a line beginning with `Actions=`. If there is one, append `My-Custom-Action;` to it. Otherwise add the following line
    > 
    >     ```
    >     Actions=My-Custom-Action;
    > 
    >     ```
    > 
    > 4.  Write the following lines at end of the file:
    > 
    >     ```
    >     [Desktop Action My-Custom-Action]
    >     Name=Name of the Option
    >     Exec=command-you-want-ro-run
    > 
    >     ```
    > 
    >     For example if you want to open Text editor, put `gedit` in place of `command-you-want-ro-run`.
    > 
    > 5.  Save the file.
    > 
    > 6.  Click on "*Activities*" and search for the application.
    > 
    > 7.  Right click on the application icon and select "Add to Favourites". It should be added to the Ubuntu dock.
    > 
    > Now if you right click on the newly added application icon in the dock, you should see a "Name of the Option" entry in the context menu which should work as expected.
    > 
    > Similarly you can other options by adding new `Desktop Action`s and adding the name of the action to the `Actions=` line. For more info see [this](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#extra-actions).


## package management

### search for available packages

- [apt - How do I search for available packages from the command-line? - Ask Ubuntu](https://askubuntu.com/questions/160897/how-do-i-search-for-available-packages-from-the-command-line)

    > ### To search for a particular package by name or description:
    > 
    > From the command-line, use:
    > 
    > ```
    > apt-cache search keyword
    > ```
    > 


### install/remove/reconfigure .deb file

- [software installation - How do I install a .deb file via the command line? - Ask Ubuntu](https://askubuntu.com/questions/40779/how-do-i-install-a-deb-file-via-the-command-line)

    > ### Install a package
    > 
    > ```
    > sudo dpkg -i DEB_PACKAGE
    > 
    > ```
    > 
    > For example if the package file is called `askubuntu_2.0.deb` then you should do `sudo dpkg -i askubuntu_2.0.deb`. If `dpkg` reports an error due to dependency problems, you can run `sudo apt-get install -f` to download the missing dependencies and configure everything. If that reports an error, you'll have to sort out the dependencies yourself by following for example [How do I resolve unmet dependencies after adding a PPA?](https://askubuntu.com/questions/140246/how-do-i-resolve-unmet-dependencies).
    > 
    > ### Remove a package
    > 
    > ```
    > sudo dpkg -r PACKAGE_NAME
    > 
    > ```
    > 
    > For example if the package is called `askubuntu` then you should do `sudo dpkg -r askubuntu`.
    > 
    > ### Reconfigure an existing package
    > 
    > ```
    > sudo dpkg-reconfigure PACKAGE_NAME
    > 
    > ```
    > 
    > This is useful when you need to reconfigure something related to said package. Some useful examples it the `keyboard-configuration` when you want to enable the `Ctrl`+`Alt`+`Backspace` in order to reset the X server, so you would the following:
    > 
    > ```
    > sudo dpkg-reconfigure keyboard-configuration
    > 
    > ```
    > 
    > Another great one is when you need to set the Timezone for a server or your local testing computer, so you use use the `tzdata` package:
    > 
    > ```
    > sudo dpkg-reconfigure tzdata
    > 
    > ```
    > 

### install ip/ifconfig/ping/lsb_release/add-apt-repository/sudo

- [ubuntu 一些命令安装 - 简书](https://www.jianshu.com/p/d5d42b4a77fc)

    > ### ip 命令
    > ```
    > apt install iproute2
    > ```
    > ### ifconfig 命令
    > ```
    > apt install net-tools
    > ```
    > ### ping 命令
    > ```
    > apt install iputils-ping
    > ```
    > ### lsb_release 命令
    > ```
    > apt install lsb-release
    > ```
    > ### add-apt-repository 命令
    > ```
    > sudo apt-get install software-properties-common python-software-properties
    > ```
    > ### sudo 命令
    > ```
    > apt install sudo
    > ```
    > 

### install Vulkan

- [Install And Test Vulkan On Linux - LinuxConfig.org](https://linuxconfig.org/install-and-test-vulkan-on-linux)

    > **AMD** It's best to enable a PPA for the latest Mesa drivers. There is a PPA that packages and releases the latest changes straight from Mesa's Git. Add the PPA to your system and update. Then, upgrade your system. It will automatically upgrade your existing Mesa packages.
    > 
    > ```
    > $ sudo add-apt-repository ppa:oibaf/graphics-drivers
    > $ sudo apt update
    > $ sudo apt upgrade
    > ```
    > 
    > When it's done, install the Vulkan packages.
    > ```
    > $ apt install libvulkan1 mesa-vulkan-drivers vulkan-utils
    > ```
    > ---
    > 
    > 
    > **NVIDIA** Ubuntu also has a great repository for the NVIDIA proprietary drivers. Add it to your system, and update Apt.
    > 
    > ```
    > $ sudo add-apt-repository ppa:graphics-drivers/ppa
    > $ sudo apt upgrade
    > ```
    > 
    > Now, install your drivers and Vulkan.
    > ```
    > $ sudo apt install nvidia-graphics-drivers-396 nvidia-settings vulkan vulkan-utils
    > ```
    > 
    > ---
    > 
    > Vulkan Info
    > -----------
    > 
    > [![Vulkan Info](https://linuxconfig.org/images/vulkan-info.jpg)](https://linuxconfig.org/images/vulkan-info.jpg "Vulkan Info")
    > 
    > Vulkan Info
    > 
    > The first ting that you can do to ensure that you have Vulkan installed and working on your system is run the `vulkaninfo` command to pull up relevant information about your system. If you get info about your graphics card, you'll know that Vulkan is working.
    > ```
    > $ vulkaninfo | less
    > ```
    > 

### install without dependencies

- [Ubuntu 18.04 Unable to install Viber - Ask Ubuntu](https://askubuntu.com/questions/1030479/ubuntu-18-04-unable-to-install-viber])

    > The problem is not only with the `viber.deb` file but also with the `libcurl3` requirement of `viber.deb`.
    > 
    > In Ubuntu 18.04 `libcurl3` cannot coexist with `libcurl4` so you are going to face problems with other applications. In my case Viber and Steam could not coexist.
    > 
    > After some search I found the following solution which is to deb-package, fix the dependency and then build a new viber file.
    > 
    > The steps are:
    > 
    > 1.  Save the `viber.deb` file in a folder
    > 2.  Open the folder in a terminal
    > 3.  execute the following commands
    > 4.  `dpkg-deb -x viber.deb viber`
    > 5.  `dpkg-deb --control viber.deb viber/DEBIAN`
    > 6.  Edit `viber/DEBIAN/control` and replace "libcurl3" with "libcurl4" (also delete the last blank line from the file or you will get an error afterwards)
    > 7.  `dpkg -b viber viberlibcurl4.deb`
    > 8.  `sudo dpkg -i viberlibcurl4.deb` or install the `.deb` file with `gdebi`
    > 
    > Viber seems to work ok with `libcurl4` atleast for me until now.
    > 
    > I found the solution here, in a comment...
    > 
    > <https://linuxconfig.org/how-to-install-viber-on-ubuntu-18-04-bionic-beaver-linux>
    > 
    > ---
    > 
    > ```
    > sudo dpkg -i --ignore-depends=libcurl3 viber.deb
    > 
    > ```
    > 
    > Works perfectly for me.
    > 
    > ---
    > 
    > Download the rpm package with:
    > 
    > ```
    > wget https://download.cdn.viber.com/desktop/Linux/viber.rpm
    > 
    > ```
    > 
    > Install alien, convert the rpm package and install the newly created deb package:
    > 
    > ```
    > sudo apt-get install alien
    > sudo alien --to-deb --scripts viber.rpm
    > sudo dpkg -i viber_7.0.0.1035-3_amd64.deb
    > 
    > ```
    > 
    > The conversion will take about 5 minutes. Be patient!
    > 


## screen resolution

### change the screen resolution for the GDM login screen

- [10.04 - How to change the screen resolution for the GDM login screen? - Ask Ubuntu](https://askubuntu.com/questions/12998/how-to-change-the-screen-resolution-for-the-gdm-login-screen)

    > On newer systems, you will want to place your monitors.xml file into the gdm configuration directory, the resolution will be picked up there:
    > 
    > This, of course, assumes that you have gon into Settings > Displays, and have selected the resolution you want, click 'Apply', this will create a monitors.xml in .config of your home dir.
    > 
    > ```
    > sudo cp ~/.config/monitors.xml /var/lib/gdm3/.config/monitors.xml
    > ```
    > 
    > I got this from below blog, it is about 2 CentOS, but it works on debian-based systems (such as debian & ubuntu) as well, slightly different path ... provided you have gnome 3.x, cannot wait until Gnome 3 reaches Beta ;-)
    > 
    > <https://mrkmg.com/posts/2015/03/changing-the-login-screen-resolution-in-centos-7-for-gnome-3/>

    > Thanks, this worked! I additionally ran `sudo chown gdm:gdm /var/lib/gdm3/.config/monitors.xml`


### generate xorg.conf

- [intel graphics - /etc/X11/xorg.conf doesn't exist? - Ask Ubuntu](https://askubuntu.com/questions/25746/etc-x11-xorg-conf-doesnt-exist)

    > You COULD create your own xorg.conf by typing in a tty (not running gdm) the following:
    > 
    > `X -configure`
    > 
    > That will create a file called **xorg.conf.new**
    > 
    > To test the file type `X -config xorg.conf.new`
    > 
    > If you can load X and see the mouse and a good resolution then you can press CTRL+ALT+BACKSPACE to quit.
    > 
    > Copy then xorg.conf.new to the new location
    > 
    > `cp xorg.conf.new /etc/X11/xorg.conf`
    > 
    > Run `startx` to test.
    > 
    > Also the file does not exist since X.org does not needed anymore for some video cards (as i understand) only some Video cards have xorg.conf because of specific configurations (Like Nvidia and Ati). The rest of the X.org configuration options are in **/usr/share/X11** like synaptics.
    > 
    > Now to test out if you have Direct Rendering do this:
    > 
    > `glxinfo | grep -i "Direct Rendering"` If it says YES then you can run several games. If it says NO then you might need more configuration. Also run `glxgears` to see how many FPS you have. If the glx commands are not there run `sudo apt-get install mesa-utils`
    > 
    > I can not guarantee that it will make it work for starcraft 2 (Remember you also need to have wine installed)
    > 


### check direct render

- [display - Ubuntu's max resolution is 1024x768 (unknown monitor) - Super User](https://superuser.com/questions/679923/ubuntus-max-resolution-is-1024x768-unknown-monitor)

    > Try installing mesa-utils using `sudo apt-get install mesa-utils`.
    > 
    > Once you have this installed reboot your machine. After rebooting the machine open a terminal and type `glxinfo | grep render` and `glxgears`
    > 
    > That should fix it.



## recover mode

### boot in recovery mode with read write

- [[lubuntu] boot in recovery mode with read write](https://ubuntuforums.org/showthread.php?t=2114086)

    > The following command will remount the root partition with read/write access...
    > 
    > ```shell
    > mount -o rw,remount /
    > ```


## virtual memory

### Check the System for Swap Information

- [8 Useful Commands to Monitor Swap Space Usage in Linux](https://www.tecmint.com/commands-to-monitor-swap-space-usage-in-linux/)

    > To check swap usage information, you can view the **/proc/swaps** file using the [cat utility](https://www.tecmint.com/13-basic-cat-command-examples-in-linux/).
    > ```shell
    > # cat /proc/swaps
    > Filename				Type		Size	Used	Priority
    > /dev/sda10                              partition	8282108	0	-1
    > ```
    >
    > ---
    > 
    > This command is used to display information about virtual memory statistics. To install vmstat on your Linux system, you can read the article below and see more usage examples:
    > 
    > [Linux Performance Monitoring with Vmstat](https://www.tecmint.com/linux-performance-monitoring-with-vmstat-and-iostat-commands/https://www.tecmint.com/linux-performance-monitoring-with-vmstat-and-iostat-commands/)
    > ```
    > # vmstat
    > ```
    > [![VmStat Check Swap Usage](https://www.tecmint.com/wp-content/uploads/2015/10/VmStat-Check-Swap-Usage-620x344.png)](https://www.tecmint.com/wp-content/uploads/2015/10/VmStat-Check-Swap-Usage.png)
    > 
    > VmStat Check Swap Usage
    > 
    > You need to take note of the following in the swap field from the output of this command.
    > 
    > 1.  **si**: Amount of memory swapped in from disk (s).
    > 2.  **so**: Amount of memory swapped to disk (s).



- [How To Add Swap Space on Ubuntu 16.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-16-04)

    > We can see if the system has any configured swap by typing:
    > 
    > ```
    > sudo swapon --show
    > 
    > ```
    > 
    > If you don't get back any output, this means your system does not have swap space available currently.
    > 
    > You can verify that there is no active swap using the `free` utility:
    > 
    > ```
    > free -h
    > 
    > ```
    > 
    > ```
    > Output              total        used        free      shared  buff/cache   available
    > Mem:           488M         36M        104M        652K        348M        426M
    > Swap:            0B          0B          0B
    > 
    > ```
    > 
    > As you can see in the "Swap" row of the output, no swap is active on the system.
    > 
    >
    > ---
    > 
    > ### Adjusting the Swappiness Property
    > 
    > The `swappiness` parameter configures how often your system swaps data out of RAM to the swap space. This is a value between 0 and 100 that represents a percentage.
    > 
    > With values close to zero, the kernel will not swap data to the disk unless absolutely necessary. Remember, interactions with the swap file are "expensive" in that they take a lot longer than interactions with RAM and they can cause a significant reduction in performance. Telling the system not to rely on the swap much will generally make your system faster.
    > 
    > Values that are closer to 100 will try to put more data into swap in an effort to keep more RAM space free. Depending on your applications' memory profile or what you are using your server for, this might be better in some cases.
    > 
    > We can see the current swappiness value by typing:
    > 
    > ```
    > cat /proc/sys/vm/swappiness
    > 
    > ```
    > 
    > ```
    > Output
    > 60
    > 
    > ```
    > 
    > For a Desktop, a swappiness setting of 60 is not a bad value. For a server, you might want to move it closer to 0.
    > 
    > We can set the swappiness to a different value by using the `sysctl` command.
    > 
    > For instance, to set the swappiness to 10, we could type:
    > 
    > ```
    > sudo sysctl vm.swappiness=10
    > 
    > ```
    > 
    > ```
    > Output
    > vm.swappiness = 10
    > 
    > ```
    > 
    > This setting will persist until the next reboot. We can set this value automatically at restart by adding the line to our `/etc/sysctl.conf` file:
    > 
    > ```
    > sudo nano /etc/sysctl.conf
    > 
    > ```
    > 
    > At the bottom, you can add:
    > 
    > /etc/sysctl.conf
    > 
    > ```
    > vm.swappiness=10
    > 
    > ```
    > 
    > Save and close the file when you are finished.
    > 
    > ### Adjusting the Cache Pressure Setting
    > 
    > Another related value that you might want to modify is the `vfs_cache_pressure`. This setting configures how much the system will choose to cache inode and dentry information over other data.
    > 
    > Basically, this is access data about the filesystem. This is generally very costly to look up and very frequently requested, so it's an excellent thing for your system to cache. You can see the current value by querying the `proc` filesystem again:
    > 
    > ```
    > cat /proc/sys/vm/vfs_cache_pressure
    > 
    > ```
    > 
    > ```
    > Output
    > 100
    > 
    > ```
    > 
    > As it is currently configured, our system removes inode information from the cache too quickly. We can set this to a more conservative setting like 50 by typing:
    > 
    > ```
    > sudo sysctl vm.vfs_cache_pressure=50
    > 
    > ```
    > 
    > ```
    > Output
    > vm.vfs_cache_pressure = 50
    > 
    > ```
    > 
    > Again, this is only valid for our current session. We can change that by adding it to our configuration file like we did with our swappiness setting:
    > 
    > ```
    > sudo nano /etc/sysctl.conf
    > 
    > ```
    > 
    > At the bottom, add the line that specifies your new value:
    > 
    > /etc/sysctl.conf
    > 
    > ```
    > vm.vfs_cache_pressure=50
    > 
    > ```
    > 
    > Save and close the file when you are finished.


### How to change swap size
- [How to change swap size on Ubuntu 14.04 ? | DigitalOcean](https://www.digitalocean.com/community/questions/how-to-change-swap-size-on-ubuntu-14-04)

    > Just follow these steps:
    > 
    > 1.  Make all swap off\
    >     sudo swapoff -a
    > 
    > 2.  Resize the swapfile\
    >     sudo dd if=/dev/zero of=/swapfile bs=1M count=1024
    > 
    > 3.  Make swapfile usable\
    >     sudo mkswap /swapfile
    > 
    > 4.  Make swapon again\
    >     sudo swapon /swapfile
    > 
    > ---
    > 
    > I tried to delete my old swap in /etc/fstab and the code which I delete is
    > 
    > ```
    > /swapfile   none    swap    sw    0   0
    > 
    > ```
    > 


## Disk bench mark

### iotop - check disk I/O utilisation per process

- [linux - Howto check disk I/O utilisation per process - Server Fault](https://serverfault.com/questions/169676/howto-check-disk-i-o-utilisation-per-process#_=_)


    > If you are lucky enough to catch the next peak utilization period, you can study per-process I/O stats interactively, using [iotop](http://guichaz.free.fr/iotop/).
    > 

- [linux - What Process is using all of my disk IO - Stack Overflow](https://stackoverflow.com/questions/488826/what-process-is-using-all-of-my-disk-io)


    > You're looking for `iotop` (assuming you've got kernel >2.6.20 and Python 2.5). Failing that, you're looking into hooking into the filesystem. I recommend the former.

### gnome-disks

- [How to check hard disk performance - Ask Ubuntu](https://askubuntu.com/questions/87035/how-to-check-hard-disk-performance)

    > Graphical method
    > ----------------
    > 
    > 1.  Go to System -> Administration -> Disk Utility.
    >     -   Alternatively, launch the Gnome disk utility from the command line by running `gnome-disks`
    > 2.  Select your hard disk at left pane.
    > 3.  Now click "Benchmark -- Measure Drive Performance" button in right pane.
    > 4.  A new window with charts opens.You will find and two buttons. One is for "Start Read Only Benchmark" and another one is "Start Read/Write Benchmark". When you click on anyone button it starts benchmarking of hard disk.
    > 
    > ![test](https://i.stack.imgur.com/0Xtvn.png)
    > 

### fio

- [How to benchmark disk I/O : Binary Lane](https://www.binarylane.com.au/support/solutions/articles/1000055889-how-to-benchmark-disk-i-o)

    > What not to do
    > ==============
    > 
    > Chances are, you have seen this test before; perhaps even used it yourself. It is the obligatory *dd* test - here is one popular variety:
    > 
    > ~~dd if=/dev/zero of=test bs=64k count=16k conv=fdatasync~~
    > 
    > This test is popular because *dd* is pre-installed on almost all Linux servers. While it is a simple way of seeing if something is broken (for example, if you see 10MB/sec than your server is overloaded) it has a number of problems:
    > 
    > -   This is a single-threaded, sequential-write test. If you are running the typical web+database server on your VPS, the number is meaningless because **typical services do not do long-running sequential writes**.
    > -   The amount of data written (1GB) is small; and hence can be strongly influenced by caching on the host server, or the host's RAID controller. (The *conv=fdatasync* only applies to the VPS, not the host).
    > -   It executes for a very short period of time; just a few seconds on faster I/O subsystems. This isn't enough to get a consistant result.
    > -   There's no read performance testing at all.
    > 
    > So if you accept my argument that *dd* is not a great way to benchmark disk performance, let's walk through a few tools that I think are worth using:
    > 
    > Measuring random IOPS with FIO
    > ==============================
    > 
    > When running a website or similar workload, in general the best measurement of the disk subsystem is known as IOPS: Input/Output Operations per Second. In particular, the specific test we want to do is:
    > 
    > 1.  Random reads, random writes, or a combination of both. Databases in particular will pull data from all over your disk - known as random access.
    > 
    > 2.  4 kilobyte blocks. Again, databases and many other programs will read very small chunks of data - 4 kilobytes is a good working estimate.
    > 3.  Multiple threads. If your website has multiple visitors, your website will serve them all at the same time. We want our benchmark to simulate this behaviour of multiple things accessing the disk at once.
    > 
    > FIO is a popular tool for measuring IOPS on a Linux server. Its very configurable (perhaps even to its detriment) but with the following Bash snippets is easy enough to use.  To start with, here is how to download and compile it - just paste straight into the root shell of your CentOS/Debian/Ubuntu server:
    > 
    > ```
    > cd /root
    > yum install -y make gcc libaio-devel || ( apt-get update && apt-get install -y make gcc libaio-dev  </dev/null )
    > wget https://github.com/Crowd9/Benchmark/raw/master/fio-2.0.9.tar.gz ; tar xf fio*
    > cd fio*
    > make
    > ```
    > 
    > With FIO compiled, we can now run some tests.
    > 
    > Random read/write performance
    > -----------------------------
    > 
    > If you simply want a way to compare different provider's disk performance, then this is the test I suggest. Run the following command:
    > 
    > ```
    > ./fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=test --bs=4k --iodepth=64 --size=4G --readwrite=randrw --rwmixread=75
    > ```
    > 
    > This will create a 4 GB file, and perform 4KB reads and writes using a 75%/25% (ie 3 reads are performed for every 1 write) split within the file, with 64 operations running at a time. The 3:1 ratio is a rough approximation of your typical database.
    > 
    > FIO will now tick along printing a summary as it goes, that looks like this:
    > 
    > ```
    > Jobs: 1 (f=1): [m] [6.5% done] [39613K/13099K /s] [9903 /3274  iops] [eta 01m:12s]
    > 
    > ```
    > 
    > And eventually a full result output like this, with the numbers we want highlighted in yellow:
    > 
    > fio-2.0.9
    > 
    > Starting 1 process
    > 
    > Jobs: 1 (f=1): [m] [100.0% done] [43496K/14671K /s] [10.9K/3667 iops] [eta 00m:00s]
    > 
    > test: (groupid=0, jobs=1): err= 0: pid=31214: Fri May 9 16:01:53 2014
    > 
    >   read : io=3071.1MB, bw=39492KB/s, iops=9873 , runt= 79653msec
    > 
    >   write: io=1024.7MB, bw=13165KB/s, iops=3291 , runt= 79653msec
    > 
    >   cpu : usr=16.26%, sys=71.94%, ctx=25916, majf=0, minf=25
    > 
    >   IO depths : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=0.1%, >=64=100.0%
    > 
    >      submit : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
    > 
    >      complete : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
    > 
    >      issued : total=r=786416/w=262160/d=0, short=r=0/w=0/d=0
    > 
    > Run status group 0 (all jobs):
    > 
    >    READ: io=3071.1MB, aggrb=39492KB/s, minb=39492KB/s, maxb=39492KB/s, mint=79653msec, maxt=79653msec
    > 
    >   WRITE: io=1024.7MB, aggrb=13165KB/s, minb=13165KB/s, maxb=13165KB/s, mint=79653msec, maxt=79653msec
    > 
    > Disk stats (read/write):
    > 
    >   vda: ios=786003/262081, merge=0/22, ticks=3883392/667236, in_queue=4550412, util=99.97%
    > 
    > This tests shows:
    > 
    > -   Binary Lane's network SSD performing 9873 read operations per second and 3291 write operations per second. 
    > -   A VPS using local SSD might reach 40,000 and 10,000 respectively if the system is lightly loaded.
    > 
    > -   A VPS using local non-SSD will probably get somewhere around 500 read / 200 write.
    > 
    > If you want to know what contributed to the above numbers, read on -
    > 
    > Random read performance
    > -----------------------
    > 
    > To measure random reads, use slightly altered FIO command:
    > 
    > ```
    > ./fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=test --bs=4k --iodepth=64 --size=4G --readwrite=randread
    > ```
    > 
    > Again, we pull the iops from the result:
    > 
    > fio-2.0.9
    > 
    > Starting 1 process
    > 
    > Jobs: 1 (f=1): [r] [100.0% done] [62135K/0K /s] [15.6K/0 iops] [eta 00m:00s]
    > 
    > test: (groupid=0, jobs=1): err= 0: pid=31181: Fri May 9 15:38:57 2014
    > 
    >   read : io=1024.0MB, bw=62748KB/s, iops=15686 , runt= 16711msec
    > 
    >   cpu : usr=5.94%, sys=90.13%, ctx=1885, majf=0, minf=89
    > 
    >   IO depths : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=0.1%, >=64=100.0%
    > 
    >      submit : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
    > 
    >      complete : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
    > 
    >      issued : total=r=262144/w=0/d=0, short=r=0/w=0/d=0
    > 
    > Run status group 0 (all jobs):
    > 
    >    READ: io=1024.0MB, aggrb=62747KB/s, minb=62747KB/s, maxb=62747KB/s, mint=16711msec, maxt=16711msec
    > 
    > Disk stats (read/write):
    > 
    >   vda: ios=259063/2, merge=0/1, ticks=951356/20, in_queue=951308, util=96.83%
    > 
    > This tests shows Binary Lane's network storage scoring 15686 read operations per second. By comparison, a local SSD may give 50,0000 while a good non-SSD may give around 2000.
    > 
    > Random write performance
    > ------------------------
    > 
    > Again, just modify the FIO command slightly so we perform randwrite instead of randread:
    > 
    > ```
    > ./fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=test --bs=4k --iodepth=64 --size=4G --readwrite=randwrite
    > ```
    > 
    > Again, we pull the iops from the result:
    > 
    > fio-2.0.9
    > 
    > Starting 1 process
    > 
    > Jobs: 1 (f=1): [w] [100.0% done] [0K/26326K /s] [0 /6581 iops] [eta 00m:00s]
    > 
    > test: (groupid=0, jobs=1): err= 0: pid=31235: Fri May 9 16:16:21 2014
    > 
    >   write: io=1024.0MB, bw=29195KB/s, iops=7298 , runt= 35916msec
    > 
    >   cpu : usr=77.42%, sys=13.74%, ctx=2306, majf=0, minf=24
    > 
    >   IO depths : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=0.1%, >=64=100.0%
    > 
    >      submit : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
    > 
    >      complete : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.1%
    > 
    >      issued : total=r=0/w=262144/d=0, short=r=0/w=0/d=0
    > 
    > Run status group 0 (all jobs):
    > 
    >   WRITE: io=1024.0MB, aggrb=29195KB/s, minb=29195KB/s, maxb=29195KB/s, mint=35916msec, maxt=35916msec
    > 
    > Disk stats (read/write):
    > 
    >   vda: ios=0/260938, merge=0/11, ticks=0/2315104, in_queue=2316372, util=98.87%
    > 
    > This tests shows Binary Lane's network storage scoring 7298 write operations per second. By comparison, a local SSD may give 50,0000 while a good non-SSD may give around 2000.
    > 
    > Measuring latency with IOPing
    > =============================
    > 
    > The final aspect of evaluating disk performance is to measure the latency on individual requests. One way to do so is to install ioping using the following command:
    > 
    > ```
    > cd /root
    > yum install -y make gcc libaio-devel || ( apt-get update && apt-get install -y make gcc libaio-dev  </dev/null )
    > wget https://ioping.googlecode.com/files/ioping-0.6.tar.gz ; tar xf ioping*
    > cd ioping*
    > make
    > ```
    > 
    > We can now run ioping to get an idea of the per-request latency:
    > 
    > ```
    > ./ioping -c 10 .
    > ```
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=1 time=0.2 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=2 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=3 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=4 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=5 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=6 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=7 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=8 time=0.2 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=9 time=0.4 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=10 time=0.3 ms
    > 
    > --- . (ext3 /dev/vda1) ioping statistics ---
    > 
    > 10 requests completed in 9006.8 ms, 3505 iops, 13.7 mb/s
    > 
    > min/avg/max/mdev = 0.2/0.3/0.4/0.1 ms
    > 
    > Here you can see the average was 0.3ms.  On a healthy system, you should see relatively low variation and an average below 1.0 ms.
    > 

### Bonnie++

- [[Linux-文件系统测试] -- Bonnie++测试 - 简书](https://www.jianshu.com/p/2e048e23e9f7)

    > Bonnie\+\+是一个硬盘和文件系统的基准性能测试工具，它通过一系列的简单测试来生成硬盘和文件系统的性能参数。主要对三个方面做基准测试：数据读、写速度，每秒可以完成的磁盘寻道次数和每秒可以完成的文件元数据操作次数。（说明： Bonnie不能支持>2G的文件，因此Russell Coker ([russell@coker.com.au](https://link.jianshu.com?t=mailto:russell@coker.com.au)) 开发了Bonnie++）
    > 
    > Bonnie\+\+的编译与安装：\
    > 下载Bonnie\+\+测试工具(最新的版本是：bonnie\+\+-1.03e) ：
    > [http://www.coker.com.au/bonnie++/](https://link.jianshu.com?t=http://www.coker.com.au/bonnie++/)
    > 下面以在ubuntu16.04操作系统为例:
    > ```
    > $ tar zxvf bonnie++-1.03e.tgz
    > $ cd bonnie++-1.03e
    > $ ./configure
    > $ make && make install
    > ```
    > 安装完成以后会在/usr/local/sbin/目录中生成两个可执行文件，bonnie++（主测试程序）和zcav（裸盘吞吐量测试程序）；同时也会在/usr/local/bin目录下生成两个可执行文件，用于生成可读性强的测试报告，它们是bon_csv2html和bon_csv2txt。
    > 
    > Bonnie++测试选项说明：\
    > 成功安装bonnie++后，查看bonnie++的测试参数\
    > $ bonnie++ help\
    > usage: bonnie++ [-d scratch-dir] [-s size(MiB)[:chunk-size(b)]]\
    > [-n number-to-stat[:max-size[:min-size][:num-directories]]]\
    > [-m machine-name]\
    > [-r ram-size-in-MiB]\
    > [-x number-of-tests] [-u uid-to-use:gid-to-use] [-g gid-to-use]\
    > [-q] [-f] [-b] [-D] [-p processes | -y]\
    > Version: 1.03e\
    > -d : scratch-dir 用于测试的目录，即测试目标位置；\
    > -s : size(MiB) 用于测试IO性能的文件的大小；如果指定的文件大小大于1G，bonnie++会将其分为多个大小为1G的文件；如果你没有加 -s这个option，系统会默认使用2倍内存大小的文件，比如我的内存是2G，那么bonnie会使用4G的文件来测试性能，原因在于减少缓存的影响\
    > -n : ?\
    > -m : 测试目标主机的主机名，仅用于显示测试结果时的主机标识；\
    > -r : 指定测试程度使用的内存大小；bonnie++一般要求指定的测试文件的大小至少为物理内存的2倍；如果测试时指定的文件过小，则可以通过指定所使用的物理内存大小来滞此条件；\
    > -x : 用于指定同时运行的测试数目；\
    > -u : 测试程序运行时关联的uid，如果以root用户的身份做测试，则此项必须明确指定。\
    > -g : 选项则用于指定gid；\
    > -q : 静默模式；\
    > -f : 快速模式，此种模式不进行IO测试；\
    > -b :\
    > -D : 直接IO测试，用于测试大规模IO请求时的性能；open的时候，带上O_DIRECT标志，对应的代码逻辑在bon_io.cpp；\
    > -p :
    > 
    > Bonnie++测试举例：\
    > $ bonnie++ -u <user_name> ------ 直接用默认参数值\
    > 例 1： bonnie++ -u root\
    > 输出如下结果：\
    > Using uid:1000, gid:1000.\
    > Writing with putc()...done\
    > Writing intelligently...done\
    > Rewriting...done\
    > Reading with getc()...done\
    > Reading intelligently...done\
    > start 'em...done...done...done...\
    > Create files in sequential order...done.\
    > Stat files in sequential order...done.\
    > Delete files in sequential order...done.\
    > Create files in random order...done.\
    > Stat files in random order...done.\
    > Delete files in random order...done.\
    > Version 1.03e ------Sequential Output------ --Sequential Input- --Random-\
    > -Per Chr- --Block-- -Rewrite- -Per Chr- --Block-- --Seeks--\
    > Machine Size K/sec %CP K/sec %CP K/sec %CP K/sec %CP K/sec %CP /sec %CP\
    > yzh-desktop 31G 106862 68 103016 3 39518 2 110741 66 106129 2 206.5 0\
    > ------Sequential Create------ --------Random Create--------\
    > -Create-- --Read--- -Delete-- -Create-- --Read--- -Delete--\
    > files /sec %CP /sec %CP /sec %CP /sec %CP /sec %CP /sec %CP\
    > 16 +++++ +++ +++++ +++ +++++ +++ +++++ +++ +++++ +++ +++++ +++\
    > yzh-desktop,31G,106862,68,103016,3,39518,2,110741,66,106129,2,206.5,0,16,+++++,+++,+++++,+++,+++++,+++,+++++,+++,+++++,+++,+++++,+++\
    > 用bon_csv2html工具将最后一行的结果转化为HTML格式输出：\
    > $ echo yzh-desktop,31G,106862,68,103016,3,39518,2,110741,66,106129,2,206.5,0,16,+++++,+++,+++++,+++,+++++,+++,+++++,+++,+++++,+++,+++++,+++ | /usr/local/bin/bon_csv2html >>bon_result.html
    > 
    > ![](//upload-images.jianshu.io/upload_images/4361046-979e007d1180c685.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    > bon_result.png\
    > 说明：\
    > 1、测试结果中显示形如的"++++"的符号表示此项测试时间小于500ms，所以被视作不准确结果不予显示；\
    > 2、每项测试都会显示两个结果，其中的%CP表示此项测试的CPU占用率；\
    > Sequential Output下的 Per Char是值用putc方式写，毫无疑问，因为cache的line总是大于1字节的，所以不停的骚扰CPU执行putc，看到cpu使用率是68%.写的速度是106MB/s\
    > Sequential Output是按照block去写的，明显CPU使用率就下来了，速度也上去了，写的速度是103MB/s。\
    > Sequential Input下的Per Char是指用getc的方式读文件，速度是110MB/s，CPU使用率是66%。\
    > Sequential Input下的block是指按照block去读文件，速度是106MB/s,CPU使用率是2%。
    > 
    > 带具体参数值进行测试\
    > 例2 ：bonnie++ -d <test_path> -u <user_name> -s <size> -m <host_name> -r <mem_size> -g <gid>\
    > $ bonnie++ -d /home/yzh/images/test -u yzh -m yzh-desktop -r 31720 -g 1000\
    > 说明 ：如果指定的文件大小大于1G，bonnie++会将其分为多个大小为1G的文件；如果你没有加 -s这个option，系统会默认使用2倍内存大小的文件，比如我的内存是16G，那么bonnie会使用32G的文件来测试性能 。\
    > 测试结果如下：
    > 
    > ![](//upload-images.jianshu.io/upload_images/4361046-15dd019a7fd286f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    > bon_result2.png
    > 
    > 


## sparse file

### truncate

- [truncate(1) - Linux man page](https://linux.die.net/man/1/truncate)

    > create a 100GB file
    > ```
    > truncate -s100G 100GB.img
    > ```
    > [name=Ya-Lun Li]
    > 
    > ---
    >  
    > **-s**, **--size**=*SIZE*
    > 
    > use this SIZE
    > 
    > 
    > SIZE may be (or may be an integer optionally followed by) one of following: KB 1000, K 1024, MB 1000*1000, M 1024*1024, and so on for G, T, P, E, Z, Y.
    > 
    > SIZE may also be prefixed by one of the following modifying characters: '+' extend by, '-' reduce by, '<' at most, '>' at least, '/' round down to multiple of, '%' round up to multiple of.

### ls

- [command line - Why does ls -l output a different size from ls -s? - Ask Ubuntu](https://askubuntu.com/questions/269480/why-does-ls-l-output-a-different-size-from-ls-s)

    > 
    > **Now, let us look at the directory:**
    > 
    > ```
    > # ls -ls --block-size 1 f_*
    > 1024 -rw-r--r-- 1 user user 128 Mar 18 15:34 f_random.img
    >    0 -rw-r--r-- 1 user user 128 Mar 18 15:32 f_zeroes.img
    >    ^                         ^
    >    |                         |
    > Amount which the           Actual file size
    > files takes on the fs
    > 
    > ```
    > 
    > The first value is given by the `-s --block-size 1` option, it is the *amount of space used by the file on the file system*.
    > 
    > ---
    > 
    > human readable
    > 
    > ```
    > ls -lsh
    > ```
    > [name=Ya-Lun Li]
    > 

## disk space

### no enough space

- [How to Fix the 'No Space Left on Device' Error on Linux - Make Tech Easier](https://www.maketecheasier.com/fix-linux-no-space-left-on-device-error/)

    > Possible Causes
    > ---------------
    > 
    > There are a couple of main causes here. If you saw a discrepancy between `du` and `df` you can jump down to the first option here. Otherwise, start at the second one.
    > 
    > ### Deleted File Reserved by Process
    > 
    > Occasionally, a file will be deleted, but a process is still using it. Linux won't release the storage associated with the file while the process is still running. You just need to find the process and restart it.
    > 
    > ![Check processes for deleted files](https://www.maketecheasier.com/assets/uploads/2017/10/no-space-process.jpg "Check processes for deleted files")
    > 
    > Try to locate the process.
    > ```shell
    > sudo lsof / | grep deleted
    > ```
    > The problematic process should be listed, then just restart it.
    > ```shell
    > sudo systemctl restart service_name
    > ```
    > ### Not Enough Inodes
    > 
    > ![Linux check filesystem inodes](https://www.maketecheasier.com/assets/uploads/2017/10/no-space-inode.jpg "Linux check filesystem inodes")
    > 
    > There is a set of metadata on filesystems called "inodes." Inodes track information about files. A lot of filesystems have a fixed amount of inodes, so it's very possible to fill the max allocation of inodes without filling the filesystem itself. You can use `df` to check.
    > ```shell
    > sudo df -i /
    > ```
    > Compare the inodes used with the total inodes. If there's no more available, unfortunately, you can't get more. Delete some useless or out-of-date files to clear up inodes.
    > 
    > ### Bad Blocks
    > 
    > The last common problem is bad filesystem blocks. Filesystems get corrupt and hard drives die. Your operating system will most likely see those blocks as usable unless they're otherwise marked. The best way to find and mark those blocks is by using `fsck` with the `-cc` flag. Remember that you can't use `fsck` from the same filesystem that you're testing. You'll probably need to use a live CD.
    > ```shell
    > sudo fsck -vcck /dev/sda2
    > ```
    > Obviously, replace the drive location with the drive that you want to check. Also, keep in mind that this will probably take a long time.
    > 

- [no space left on device 磁盘空间不足原因及排查方法 - CSDN博客](https://blog.csdn.net/jiedao_liyk/article/details/78497625)

    > **在系统使用中，经常会遇到no space left on device 磁盘空间不足的情况， 下面来详细的介绍一下产生这种情况的几种原因及解决办法：**
    > 
    > **1\. 首先我们要清楚inode 和 block的概念：**
    > 
    > 1.  inode在格式化创建文件系统的时候诞生，用来存放文件的属性信息，存放着block的位置，没有文件名，创建一个非空文件占用一个inode和至少1个block
    > 
    > 2.  block是实际存放数据的位置，block大小 1k 4k 8k centos 6.x(分区大于500M 默认是4k)，文件很大的话占用多个block, 文件非常小的时候1k block剩余的空间不能继续使用，所以系统中block消耗更快
    > 
    > **所以磁盘慢了就分为，inode满了，和block满了，以及一种特殊的情况，下面我们来具体分析，以及对应的解决方案**
    > 
    > -   查看是否是block满了
    > 
    > ```shell
    > [root@test-os testuser]# df -h   ###查看所有block使用情况
    > Filesystem      Size  Used Avail Use% Mounted on
    > /dev/sda3       8.8G  8.8G     0 100% /
    > tmpfs           931M     0  931M   0% /dev/shm
    > /dev/sda1       190M   40M  141M  22% /boot
    > [root@test-os testuser]# du -sh /usr/* |grep G  ###查找大文件
    > 7.3G    /usr/local
    > [root@test-os testuser]# du -sh /usr/local/* |grep G
    > 7.3G    /usr/local/bin
    > [root@test-os testuser]# du -sh /usr/local/bin/* |grep G
    > 7.3G    /usr/local/bin/1g
    > 
    > [root@test-os testuser]# \rm -f /usr/local/bin/1g  ###删除大文件
    > [root@test-os testuser]#
    > [root@test-os testuser]# df -h    ###接着查看发现已经解决
    > Filesystem      Size  Used Avail Use% Mounted on
    > /dev/sda3       8.8G  1.5G  6.9G  18% /
    > tmpfs           931M     0  931M   0% /dev/shm
    > /dev/sda1       190M   40M  141M  22% /boot
    > ```
    > 
    > -   查看是否inode满了（df -h发现还有空间）
    > 
    > ```shell
    > [root@test-os logs]# touch {1..118}.txt
    > [root@test-os logs]# touch {1..118}.txt
    > touch: cannot touch `118.txt': No space left on device
    > [root@test-os logs]# df -i   ###查看inode使用情况
    > Filesystem     Inodes IUsed  IFree IUse% Mounted on
    > /dev/sda3      593344 56998 536346   10% /
    > tmpfs          238282     1 238281    1% /dev/shm
    > /dev/sda1       51200    39  51161    1% /boot
    > /tmp/1m           128   128      0  100% /app/logs
    > [root@test-os logs]# pwd
    > /app/logs
    > [root@test-os logs]# \rm -f *.txt   ###如果小文件太多，采用a*.txt b*.txt 一批一批的删
    > [root@test-os logs]# df -i   ###接着查看
    > Filesystem     Inodes IUsed  IFree IUse% Mounted on
    > /dev/sda3      593344 56998 536346   10% /
    > tmpfs          238282     1 238281    1% /dev/shm
    > /dev/sda1       51200    39  51161    1% /boot
    > /tmp/1m           128    11    117    9% /app/logs
    > ###如果不知道小文件都在哪里怎么查找？
    > ###查找系统中 目录大小大于1M（目录一般大小为4K，所以目录要是大了那么文件必然很多）
    > [root@localhost testuser]# find / -size +4k -type d |xargs ls -ldhi
    >      11 drwx------   2 root root  12K Sep 23 00:49 /boot/lost+found
    >     946 drwxr-xr-x  12 root root 4.1K Sep 22 17:53 /dev
    > 1114113 drwxr-xr-x  88 root root  12K Sep 22 19:55 /etc
    >  262145 drwxr-xr-x  13 root root  12K Sep 22 18:59 /lib
    > ```
    > 
    > -   查看是不是文件被占用一直没被彻底删除（特殊原因），这种情况往往是容易被忽略，也是让人郁闷的，因为你会发现df -h明明已经有空间了，但是就是放不进去东西
    > 
    > ```shell
    > [root@test-os ~]# lsof |grep deleted
    > rsyslogd   1250      root    1w      REG                8,3 4888889358     140789 /var/log/messages (deleted)
    > 
    > [root@test-os ~]# #lsof 显示出系统中被打开的文件
    > [root@test-os ~]# #第一列 软件/服务的名称
    > [root@test-os ~]# #第八列 文件的大小
    > [root@test-os ~]# #第10列 文件的名字
    > [root@test-os ~]# #第11列 标记（硬链接数为0 进程调用数不为零 就会有 delete)
    > 
    > ####重启对应的服务 释放磁盘空间
    > [root@test-os ~]# /etc/init.d/rsyslog restart
    > Shutting down system logger:                               [  OK  ]
    > Starting system logger:                                    [  OK  ]
    > 
    > [root@test-os ~]# df -h
    > Filesystem      Size  Used Avail Use% Mounted on
    > /dev/sda3       8.8G  1.5G  6.9G  18% /
    > tmpfs           931M     0  931M   0% /dev/shm
    > /dev/sda1       190M   40M  141M  22% /boot
    > /tmp/1m        1003K   19K  933K   2% /app/logs
    > ```
    > 


### no enough inodes

- [How To Increase Amount of Disk inodes in Linux](https://ma.ttias.be/how-to-increase-amount-of-disk-inodes-in-linux/)

    > It doesn't happen often, but at times you may run out of inodes on a Linux system.
    > 
    > To find your current inode usage, run `df -i`.
    > 
    > ```shell
    > $ df -i
    > Filesystem                Inodes   IUsed     IFree  IUse%   Mounted on
    > /dev/mapper/centos-root 19374080   19374080  0      100%   /
    > ```
    > 
    > Out of the available 19.374.080 inodes, none were free. This is pretty much the equivalent of a disk full, except it doesn't show in terms of capacity but in terms of inodes.
    > 
    > If you're confused on what an inode exactly is, [Wikipedia](https://en.wikipedia.org/wiki/Inode) has a good description.
    > 
    > > In a Unix-style file system, an index node, informally referred to as an inode, is a data structure used to represent a filesystem object, which can be one of various things including a file or a directory. Each inode stores the attributes and disk block location(s) of the filesystem object's data.\
    > > *[Wikipedia: inode](https://en.wikipedia.org/wiki/Inode)*
    > 
    > A disk with 0 available inodes is probably full of very small files, somewhere in a specific directory (applications, tmp-files, pid files, session files, ...). Each file uses (*at least*) 1 inode. Many million files would use many million inodes.
    > 
    > If your disks' inodes are full, how do you increase it? The tricky answer is, you probably can't.
    > 
    > The amount of inodes available on a system is decided upon creation of the partition. For instance, a default partition of EXT3/EXT4 has a bytes-per-inode ratio of **one inode every 16384 bytes (16 Kb)**.
    > 
    > A 10GB partition would have would have around 622.592 inodes. A 100GB partition has around 5.976.883,2 inodes (taking into account [the reserved space for super-users/journalling](https://ma.ttias.be/changing-the-reserved-blocks-percentage-on-ext3-filesystems-in-linux/)).
    > 
    > Do you want to increase the amount of inodes? **Either increase the capacity of the disk entirely ([Guide: Increase A VMware Disk Size (VMDK) LVM](https://ma.ttias.be/increase-a-vmware-disk-size-vmdk-formatted-as-linux-lvm-without-rebooting/)), or re-format the disk using `mkfs.ext4 -i` to manually overwrite the *bytes-per-inode* ratio**.
    > 
    > As usual, the [Archwiki](https://wiki.archlinux.org/index.php/Ext4) has a good explanation on why we don't just make the default inode number 10x higher.
    > 
    > > For partitions with size in the hundreds or thousands of GB and average file size in the megabyte range, this usually results in a much too large inode number because the number of files created never reaches the number of inodes.
    > >
    > > This results in a waste of disk space, because all those unused inodes each take up 256 bytes on the filesystem (this is also set in /etc/mke2fs.conf but should not be changed). 256 * several millions = quite a few gigabytes wasted in unused inodes.\
    > > *[Archwiki: ext4](https://wiki.archlinux.org/index.php/Ext4)*
    > 
    > You may be able to create a new partition if you have spare disks/space in your LVM and chose a filesystem that's better suited to handle many small files, [like ReiserFS](https://en.wikipedia.org/wiki/ReiserFS).
    > 

- [linux - Is it possible to change Inode count on an ext4 filesystem? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/45107/is-it-possible-to-change-inode-count-on-an-ext4-filesystem)

    > From the [`mke2fs` man page](http://linux.die.net/man/8/mke2fs):
    > 
    > > Be warned that it is not possible to expand the number of inodes on a filesystem after it is created, so be careful deciding the correct value for this parameter.
    > 
    > So the answer is no.
    > 
    > What you could do is shrink the existing ext4 volume (this requires unmounting the filesystem), use the free space to create a new ext4 volume with fewer inodes, copy the data, remove the old volume and extend the new volume to occupy all the space.

- [files - How can I increase the number of inodes in an ext4 filesystem? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/26598/how-can-i-increase-the-number-of-inodes-in-an-ext4-filesystem)

    > It seems that you have a lot more files than normal expectation.
    > 
    > I don't know whether there is a solution to change the inode table size dynamically. I'm afraid that you need to back-up your data, and create new filesystem, and restore your data.
    > 
    > To create new filesystem with such a huge inode table, you need to use '-N' option of mke2fs(8).
    > 
    > I'd recommend to use '-n' option first (which does not create the fs, but display the use-ful information) so that you could get the estimated number of inodes. Then if you need to, use '-N' to create your filesystem with a specific inode numbers.
    > 
    > ---
    > 
    > @Gilles The `-i` options specifies the size of the inode, not how many there are. The `-N` option sets the number inodes. -- [theillien](https://unix.stackexchange.com/users/77650/theillien "546 reputation") [Oct 23 '14 at 20:12](https://unix.stackexchange.com/questions/26598/how-can-i-increase-the-number-of-inodes-in-an-ext4-filesystem#comment268772_26600)
    > 
    > ---
    > 
    > As another workaround I could suggest considering packing huge collections of files into an uncompressed(!) `tar` archive, and then using `archivemount` to mount it as a filesystem. A tar archive is better for sharing than a filesystem image and provides similar performance when backing up to a cloud or another storage.
    > 
    > * * * * *
    > 
    > If the collection is supposed to be read-only, `squashfs` may be an option, but it requires certain options enabled in the kernel, and `xz` compression is available for tar as well with the same performance.
    > 
    > ---
    > 
    > I have an alternate solutions for this situation. Lets say you have 1000 inodes in a **partition** of 10G. But due to inodes limit you are not suppose to use all space of **partition**. But in this solutions you will be able to use the remaining space of the **partition** without **formatting** it.
    > 
    > ```
    > $ df -i  # see list ( I need just one free inode here so move just one file into other PARTITION)
    > /dev/part1  1000 999 1 99.9%     /data
    > 
    > $ dd if=/dev/zero of=/data/new_data
    > $ mkfs.ext4 /data/new_data
    > $ mkdir /data1
    > $ mount /data/new_data /data1
    > 
    > ```
    > 
    > **for permanent mounting**
    > 
    > ```
    > $ echo "/data/new_data /data1 ext4 defaults 0 1" >> /etc/fstab
    > 
    > ```
    > 
    > ---
    > 
    > Recently ran into this issue when using apt or aptitude upgrade.
    > 
    > ```
    > df -h
    > 
    > Filesystem      Size  Used Avail Use% Mounted on
    > /dev/xvda1      7.8G  5.1G  2.3G  70% /
    > 
    > df -i
    > 
    > Filesystem     Inodes  IUsed  IFree IUse% Mounted on
    > /dev/xvda1     524288 521497   2791  100% /
    > 
    > ```
    > 
    > ---
    > 
    > Supposed you want to sort with the number of inodes in the `/usr/` and its first level subdir, based on @kph0x1 and @OttoLeichliter, with `--max-depth=1` flag, try:
    > 
    > ```
    > du --max-depth=1 --inodes /usr/ 2>/dev/null | sort -n
    > 
    > ```
    > 
    > The output may like this:
    > 
    > ```
    > 1   /usr/etc
    > 6   /usr/games
    > 151 /usr/local
    > 238 /usr/sbin
    > 328 /usr/lib64
    > 2203    /usr/bin
    > 3020    /usr/include
    > 32556   /usr/lib
    > 59052   /usr/src
    > 165062  /usr/share
    > 262618  /usr/
    > 
    > ```
    > 
    > As you can see, the most top 2 subdir of consuming inodes is `/usr/share` and `/usr/src`. Then you can dig into it by using that command again:
    > 
    > ```
    > du --max-depth=1 --inodes /usr/share/ 2>/dev/null | sort -n
    > 
    > ```
    > 
    > or
    > 
    > ```
    > du --max-depth=1 --inodes /usr/src/ 2>/dev/null | sort -n
    > 
    > ```
    > 
    > Do this recursively to find the suspicious folder and remove it.

