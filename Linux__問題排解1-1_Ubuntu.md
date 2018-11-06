# Linux__問題排解1-1_Ubuntu

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













## app launcher/default app/startup app

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

### can't set Launch at session startup

> Check the owner of `~/.config/autostart/` is current user or not. If not, `chown user:user -R ~/.config/autostart/` 
> [name=Ya-Lun Li]
> 


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




