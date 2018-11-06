# Application__筆記3

[toc]
<!-- toc --> 

# Docker Zoo

## GUI in docker

- [docker-baseimage-gui/README.md at master · jlesage/docker-baseimage-gui](https://github.com/jlesage/docker-baseimage-gui/blob/master/README.md#environment-variables)

## 設定中文GUI


- [postgresql - Change Ubuntu locale in Docker - Stack Overflow](https://stackoverflow.com/questions/26473819/change-ubuntu-locale-in-docker)

- [Docker Python set utf-8 locale - Stack Overflow](https://stackoverflow.com/questions/43356982/docker-python-set-utf-8-locale)

- [ubuntu - Can't configure locale in Docker image - Stack Overflow](https://stackoverflow.com/questions/32333650/cant-configure-locale-in-docker-image)

- [Docker container 無法輸入中文 « 少年沒帶腦](http://gaga5lala.logdown.com/posts/2016/10/14/docker-container-cannot-type-in-chinese)

### Set the locale

- [How to set the locale inside a Ubuntu Docker container? - Stack Overflow](https://stackoverflow.com/questions/28405902/how-to-set-the-locale-inside-a-ubuntu-docker-container)

    > ```
    > # install locales packages
    > RUN apt-get -y install locales
    > 
    > # Set the locale
    > RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    >     locale-gen
    > ```

### Set locale env

- [docker 学习 - 解决ubuntu镜像中文乱码问题 - 简书](https://www.jianshu.com/p/43a3468362aa?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)

    > 先输入`locale -a`，查看一下现在已安装的语言，已经有`C.UTF-8`字符集
    > 
    > ![](https://upload-images.jianshu.io/upload_images/2729580-f6ca6ad20a8599cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/362)
    > 
    > 
    > 输入`locale`查看下语言情况，显示语言不正确。
    > 
    > ![](https://upload-images.jianshu.io/upload_images/2729580-3a029a07a822585d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/372)
    > 

    > 通常设置`LANG、LANGUAGE、LC_ALL`这三个就行了。 关于他们三的关系简言之： LANG默认设置，LC_*没设值的时候就拿LANG；LANGUAGE是程序语言设置；LC_ALL强制设置所有LC_* 详细传送门： [https://blog.csdn.net/nick357/article/details/8513699]


- [CoreOS那些事之：再谈Docker运行中文GUI软件（上）](http://www.infoq.com/cn/articles/talk-about-docker-running-the-chinese-gui-software)

    > ```
    > ENV LANGUAGE zh_TW.UTF-8
    > ENV LANG zh_TW.UTF-8
    > ENV LC_ALL zh_TW.UTF-8
    > ```



### install chinese fonts

- [在 x64 Linux 桌面利用 Docker 技術進行「稅額試算服務線上登錄」作業 « Jamyy's Weblog](http://jamyy.us.to/blog/2015/05/7408.html)

    > ```
    > apt-get -y install ttf-wqy-microhei
    > ```



### set timezone

- [Docker容器时区设置与中文字符支持 - 倚楼听风雨 - SegmentFault 思否](https://segmentfault.com/a/1190000005026503)

    > 
    > ```
    > ENV TZ=Asia/Taipei
    > RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
    > 
    > ```

### set chinese fonts in wine app

- [Chinese fonts are not visible in programs installed in Wine - Ask Ubuntu](https://askubuntu.com/questions/1019530/chinese-fonts-are-not-visible-in-programs-installed-in-wine)

    > First u must download wqy-microhei.ttc font online (<https://github.com/anthonyfok/fonts-wqy-microhei/blob/master/wqy-microhei.ttc>)
    > 
    > After save this Regedit file on pc (<https://gist.github.com/swordfeng/c3fd6b6fcf6dc7d7fa8a>)
    > 
    > Font file copy to wine folder under C: drive folder, under Windows folder, under Font (/home/YOURUSERNAME/.wine/drive_c/windows/Fonts)
    > 
    > If you cant see .wine folder, enter anyfolder and push keyboard Ctrl+H (show/hide hidden folder)
    > 
    > And last one you have downloaded regedit file. Steps: 1) Download winetricks (sudo apt-get install winetricks) 2) Open wine tricks app 3) First screen select 'Select the default wineprefix' and click OK (go to next) 4) Select option to 'Run regedit'. You will see windows registry editor screen. 5) Click on bar 'Registry > Import Registry File' 6）Select downloaded registry file and import. 7）Finish!
    > 
    > I hope it help you. I also use some software have chinese font. Wine don't support some distro maybe.


## Resilio Sync

- [resilio/sync - Docker Hub](https://hub.docker.com/r/resilio/sync/)

## 百度雲網盤

- [kukki/docker-baidupan - Docker Hub](https://hub.docker.com/r/kukki/docker-baidupan/)
- [XuShaohua/bcloud: 百度网盘的linux桌面客户端](https://github.com/XuShaohua/bcloud)
- [为什么百度云、360云盘等都取消了同步盘功能？ - 知乎](https://www.zhihu.com/question/38596437)

### 用Wine安装百度云

- [Ubuntu13.04(64bit)下用Wine安装百度云、360云、微云 - tomheaven的专栏 - CSDN博客](https://blog.csdn.net/hanlin_tan/article/details/40226009)

2.其次安装百度云、360云需要的 wininet 网络组件（不进行此步骤百度云或微云进登陆界面时直接崩溃，360云不能联网），终端运行：
```
winetricks wininet
```


## Dropbox

- [janeczku/dropbox - Docker Hub](https://hub.docker.com/r/janeczku/dropbox/)

### inotify.max_user_watches

- [inotify.max_user_watches on synology · Issue #18 · janeczku/docker-dropbox](https://github.com/janeczku/docker-dropbox/issues/18)

    > I don't know if you found a solution for this, but I basically added the following line to the run file below `chmod 755 /dbox/Drobox` <https://github.com/janeczku/docker-dropbox/blob/master/run#L31>
    > 
    > `echo fs.inotify.max_user_watches=100000 | tee -a /etc/sysctl.config && sysctl -p` Once this is done you then have to build the docker image. However you do have to add the `--privileged` flag to the docker run statement

- [Dropbox fs.inotify error - Stack Overflow](https://stackoverflow.com/questions/35711897/dropbox-fs-inotify-error)

    > If I type `apropos inotify` in a shell to see which manpage are about "inotify" I get these results:
    > 
    > ```
    > $ apropos inotify
    > inotify (7)          - monitoring filesystem events
    > inotify_add_watch (2) - add a watch to an initialized inotify instance
    > inotify_init (2)     - initialize an inotify instance
    > inotify_init1 (2)    - initialize an inotify instance
    > inotify_rm_watch (2) - remove an existing watch from an inotify instance
    > upstart-file-bridge (8) - Bridge between Upstart and inotify
    > 
    > ```
    > 
    > `apropos` finds manpages. `apropos` is your friend. Remember `apropos`.
    > 
    > The first one looks promising, so lets try opening that with `man inotify`. You should now get the documentation of `ifnotify`. It says:
    > 
    > ```
    > NAME
    >     inotify - monitoring filesystem events
    > 
    > DESCRIPTION
    >     The  inotify API provides a mechanism for monitoring filesystem events.
    >     Inotify can be used to monitor individual files, or to monitor directo‐
    >     ries.   When  a  directory is monitored, inotify will return events for
    >     the directory itself, and for files inside the directory.
    > 
    > ```
    > 
    > So now we've learned what `inotify` roughly does. Let's see if it also has something useful to say about your error.
    > 
    > We can search in manpages by pressing `/<term><enter>`. So lets try: `/max_user_watches<enter>` That brings us to this section:
    > 
    > ```
    >    /proc/sys/fs/inotify/max_user_watches
    >           This specifies an upper limit on the number of watches that  can
    >           be created per real user ID.
    > 
    > ```
    > 
    > The `/proc/sys/fs/inotify/max_user_watches` file is the same as the `fs.inotify.max_user_watches` setting in `/etc/sysctl.conf`. They're just two different ways to access the same Linux kernel parameter.
    > 
    > You can press `q` to exit.
    > 
    > I can see what the *current* value is by using:
    > 
    > ```
    > $ cat /proc/sys/fs/inotify/max_user_watches
    > 524288
    > 
    > ```
    > 
    > or:
    > 
    > ```
    > $ sysctl fs.inotify.max_user_watches
    > fs.inotify.max_user_watches = 524288
    > 
    > ```
    > 
    > They both use the same underlying value in the Linux kernel.
    > 
    > Note that this value is actually five times *larger* than what Dropbox recommends! This is on my Ubuntu 15.10 system.
    > 
    > So now we have learned that:
    > 
    > 1.  `inotify` is a Linux system to monitor changes to files and directories.
    > 2.  That we can set how many files or directories a user is allowed to watch simultaneously.
    > 3.  That Dropbox gives the error "Unable to monitor entire Dropbox folder hierarchy".
    > 
    > From this information, It seems to be the case that Dropbox is unable to watch enough files and directories for changes because the `fs.inotify.max_user_watches` is too low.
    > 
    > What I recommend is:
    > 
    > 1.  Check the `/etc/sysctl.conf` with any text editor as root. Make sure there are no `fs.inotify.max_user_watches=100000` lines here. If there are, remove them.
    > 2.  Reboot the system to restore the default value.
    > 3.  Check what the value of `fs.inotify.max_user_watches` is as described above.
    > 4.  Double that by running `sudo echo 'fs.inotify.max_user_watches=XXX' >> /etc/sysctl.conf && sudo sysctl -p /etc/sysctl.conf`. You don't need to reboot after this change.
    > 5.  Hope this error is now fixed. Time will tell. If not, try doubling the value again.
    >     -   If that doesn't fix it, there *may* be another problem, or maybe you just need to increase it *even more*. It depends a bit on what the default value is for your system.
    > 
    > **Note**: Newer versions of systemd no longer load the `/etc/sysctl.conf` file, it will only load files from the `/etc/sysctl.d/` directory. Using a file in the `/etc/sysctl.d` directory *should* already be supported by most Linux distros, so I recommend you use that for future-proofing.
    > 
    > * * * * *
    > 
    > If you're wondering "why is there a limit in the first place?" then consider what would happen if a program would watch a million files. Would that still work? And what about a billion? 10 billion? 10 trillion? etc.
    > 
    > At some point, your system will run out of resources and crash. [See here](https://stackoverflow.com/q/27197785/660921) on some "fun" ways to do that ;-)

- [Changing /proc/sys/fs/inotify/max_user_watches · Issue #24 · JrCs/docker-crashplan](https://github.com/JrCs/docker-crashplan/issues/24)

    > You need to increase the `fs.inotify.max_user_watches`parameter on the host. For example you can create a configuration file in `/etc/sysctl.d`. Example `/etc/sysctl.d/crashplan.conf` with content:
    > 
    > ```
    > fs.inotify.max_user_watches = 1048576
    > 
    > ```


- [13.04 - How to change value of /proc/sys/fs/inotify/max_user_watches - Ask Ubuntu](https://askubuntu.com/questions/353041/how-to-change-value-of-proc-sys-fs-inotify-max-user-watches)

    > For permanent configuration:
    > 
    > ```
    > echo 'fs.inotify.max_user_watches = 1524288' | sudo tee /etc/sysctl.d/99-whatever.conf
    > sudo sysctl -p --system
    > 
    > ```
    > 
    > then restart the application you've been using.
    > 


## OneDrive

- [oznu/onedrive - Docker Hub](https://hub.docker.com/r/oznu/onedrive/)

- [skilion/onedrive: Free Client for OneDrive on Linux](https://github.com/skilion/onedrive)


- [How to sync your Microsoft OneDrive cloud storage with Linux | ModMy](https://www.modmy.com/how-sync-onedrive-linux)



## Google Drive

- [Top 12 Best Google Drive Linux Client Software | UbuntuPIT](https://www.ubuntupit.com/top-12-best-google-drive-linux-client-software/)

### google-drive-ocamlfuse

- [How does google-drive-ocamlfuse work? · Issue #167 · astrada/google-drive-ocamlfuse](https://github.com/astrada/google-drive-ocamlfuse/issues/167)

    > Does it creates a local copy and sync it with the remote copy in Google Drive? In other words, does it work like Dropbox? I want the files available offline, and then backup/sync the files with Google Drive, when I am online. Is google-drive-ocamlfuse suitable for this purpose? I am using Ubuntu.
    > 
    > ---
    > 
    > No, it does not work like the Dropbox client, so you cannot access your files offline. Please check out another client (e.g. [this one](https://github.com/odeke-em/drive)).
    > 


- [mitcdh/google-drive-ocamlfuse - Docker Hub](https://hub.docker.com/r/mitcdh/google-drive-ocamlfuse/)

- [retrohunter/docker-google-drive-ocamlfuse - Docker Hub](https://hub.docker.com/r/retrohunter/docker-google-drive-ocamlfuse/)

- [Google Drive API 憑證 - Scripts](https://console.developers.google.com/apis/credentials?project=project-id-4148804015066406542)

- [Google-drive as Docker container | allskyee](https://allskyee.blogspot.com/2017/03/google-drive-as-docker-container.html)

    > 1\. Get Google API permission
    > -----------------------------
    > 
    > The steps to do this is very well documented in [this](https://github.com/ruo91/docker-google-drive) github repository which itself is another Docker application. The instructions seem to be a bit outdated, however, so I will update them with what I see at the time of this writing.
    > 
    > You will need to visit [console.developers.google.com/iam-admin/projects](https://console.developers.google.com/) and create a project. After deciding on a name, click "Ok" and you will be taken to the API Manager site. Under "Google Apps API", click on "Drive API". This will take you to another page that looks like below,
    > 
    > [![](https://1.bp.blogspot.com/-_o5jMvr4p2Y/WLbKJVnpscI/AAAAAAAAB80/rHj0jgiA4y4Vs2XWDNvm826k5tjb_uSdgCLcB/s640/gdriveapi.png)](https://1.bp.blogspot.com/-_o5jMvr4p2Y/WLbKJVnpscI/AAAAAAAAB80/rHj0jgiA4y4Vs2XWDNvm826k5tjb_uSdgCLcB/s1600/gdriveapi.png)\
    > Click on "**enable**" in the top-middle spot which turns to "**disable**" upon click, then the "**Create credentials**" button on the top-right thereafter to create a set of keys to access Google Drive via API. You can create about more details on that at [developers.google.com/identity/protocols/OAuth2](https://developers.google.com/identity/protocols/OAuth2). Follow the four steps to create the necessary credentials and download the credentials at the last step.
    > 
    > This is a JSON file named client_id.json that has two fields which you will require later on. This is the **client_id** and the **client_secret** fields. Open these files and keep a copy of these two fields so that you may reference them later on.
    > 
    > ---
    > 
    > The run command doesn't mount the Google Drive yet as the config file is missing. Remember the client ID and secret ID (**client_id** and **client_secret** in  client_id.json file) I told you about earlier. It's time to use them to generate a config file and save it into the home directory of user abc. Assuming the former is X and the latter is Y, the command would be,
    > 
    > docker exec -i -t -u abc:abc google-drive\
    > google-drive-ocamlfuse -f -headless\
    > -id "**X**.apps.googleusercontent.com" -secret "**Y**"
    > 
    > This command will produce a link and ask you for a verification key. Open the link on your browser and click on "allow" button. This will generate a verification key and you should copy then paste this content onto the command and press enter.

- [Google drive : redirect_uri_mismatch - Stack Overflow](https://stackoverflow.com/questions/12710262/google-drive-redirect-uri-mismatch)

    > The URI
    > 
    > ```
    > urn:ietf:wg:oauth:2.0:oob
    > 
    > ```
    > 
    > is only applicable to those Google client IDs that have been generated for "installed applications".
    > 
    > So to solve your problem you have to create a new Client ID and set Application Type as "***Installed application***". There you can get ClientId and ClientSecret which you will need.
    > 
    > 1.  Create a new Project [Here](https://console.developers.google.com)
    > 
    > 2.  Select APIs from the left side bar and make sure Drive SDK is ON
    > 
    > 3.  Go to Credientials below APIs ,tap on "CREATE NEW CLIENT ID"
    > 
    > 4.  Select Installed application and type as iOS and provide Bundle ID (or simply choose "Other")
    > 
    > 5.  Copy Client ID & Client secret to use that in your application.
    > 
    > The redirect URI is automatically generated and should prevent the error you are getting.
    > 

### drive

- [dmlb2000/gdrive-backups - Docker Hub](https://hub.docker.com/r/dmlb2000/gdrive-backups/)

- [odeke-em/drive: Google Drive client for the commandline](https://github.com/odeke-em/drive#why-another-google-drive-client)

    > .desktop Files
    > --------------
    > 
    > As previously mentioned, Google Docs, Drawings, Presentations, Sheets etc and all files affiliated with docs.google.com cannot be downloaded raw but only exported. Due to popular demand, Linux users desire the ability to have *.desktop files that enable the file to be opened appropriately by an external opener. Thus by default on Linux, drive will create *.desktop files for files that fall into this category.
    > 
    > To turn off this behavior, you can set flag `-desktop-links` to false e.g
    > 
    > ```source-shell
    > drive pull -desktop-links=false
    > ```
    > 
    > ---
    > 
    > `drive` is not a sync daemon, it provides:
    > 
    > -   Upstreaming and downstreaming. Unlike a sync command, we provide pull and push actions. The user has the opportunity to decide what to do with their local copy and when they decide to. Make some changes, either push the file remotely or revert it to the remote version. You can perform these actions with user prompt:
    > 
    >     ```
    >       echo "hello" > hello.txt
    >       drive push # pushes hello.txt to Google Drive
    >       echo "more text" >> hello.txt
    >       drive pull # overwrites the local changes with the remote version
    > 
    >     ```
    > 
    > -   Allowing to work with a specific file or directory, optionally not recursively. If you recently uploaded a large VM image to Google Drive, yet only a few text files are required for you to work, simply only push/pull the exact files you'd like to worth with:
    > 
    >     ```
    >       echo "hello" > hello.txt
    >       drive push hello.txt # pushes only the specified file
    >       drive pull path/to/a/b path2/to/c/d/e # pulls the remote directory recursively
    > 
    >     ```
    > 
    > -   Better I/O scheduling. One of the major goals is to provide better scheduling to improve upload/download times.
    > 
    > -   Possibility to support multiple accounts. Pull from or push to multiple Google Drive remotes. Possibility to support multiple backends. Why not to push to Dropbox or Box as well?


### gdrive


- [vovimayhem/gdrive - Docker Hub](https://hub.docker.com/r/vovimayhem/gdrive/)

- [prasmussen/gdrive: Google Drive CLI Client](https://github.com/prasmussen/gdrive)

- [Writing .gdoc files from a web browser · lmmx/devnotes Wiki](https://github.com/lmmx/devnotes/wiki/Writing-.gdoc-files-from-a-web-browser)

- [Custom application to open .gdoc extensions · lmmx/devnotes Wiki](https://github.com/lmmx/devnotes/wiki/Custom-application-to-open-.gdoc-extensions)

- [Google drive gdoc download conversion workaround · lmmx/devnotes Wiki](https://github.com/lmmx/devnotes/wiki/Google-drive-gdoc-download-conversion-workaround)

- [gdrive doesn't show Google Docs · Issue #36 · prasmussen/gdrive](https://github.com/prasmussen/gdrive/issues/36)







## Asus Webstorage

- [[SOLVED] ASUS Webstorage 12.04](https://ubuntuforums.org/showthread.php?t=2217645)

    > First Install mono-complete\
    > apt-get install mono-complete
    > 
    > Then change the icon executable\
    > edit the following file
    > 
    > /usr/share/applications/aws-autostart.desktop
    > 
    > update the "Exec=" command to use the following command instead\
    > mono --runtime=v4.0 /usr/lib/ASUSWebStorage/ASUSWebStorage.exe


- [Fix 64bit Ubuntu](http://forum.asuswebstorage.com/showtopic.aspx?topicid=1270)

    > First put ia32-libs and some 32bit dependencies- use this command
    > ```sh
    > $ sudo apt-get install ia32-libs ia32-libs-gtk libxss1 libqt4-core libqt4-gui libxss1 libxss1-dbg libxss-dev libglib2.0-dev libc6 libfreetype6 libjpeg62 libpng12-0 zlib1g libnotify0.4-cil libmono-winforms2.0-cil
    > ```
    > 
    > Second download linux software and (cd ./) to location or use this command
    > ```sh
    > $ wget http://content.asuswebstorage.com/asuswebstorage/ASUSWebStorage.deb
    > ```
    > 
    > Finally install asus webstorage- use this command
    > ```sh
    > $ sudo dpkg -i --force-architecture ASUSWebStorage.deb
    > ```
    > 
    > That should do it.  You probably will get dependency not met and maybe error.  Does not mean not installed and working properly.  Check your menu.  Should have Asus WebStorage icon.
    > 


- [32bit/ubuntu - Docker Hub](https://hub.docker.com/r/32bit/ubuntu/)

- [docker-32bit/ubuntu: Build a docker image for ubuntu i386.](https://github.com/docker-32bit/ubuntu)




## BT(deluge)


### webui

- [Deluge Web UI start @ Amin's Note :: 痞客邦 ::](http://lagunawang.pixnet.net/blog/post/25802110-deluge-web-ui-start)

    > Deluge 真的是很好用的東西，之前就說要寫起來，結果拖到現在才寫:p
    > 
    > 而且還有提供webui 的介面，所以真的很方便。
    > 
    > 1.啟動 Deluge Server
    > 
    > #deluged &
    > 
    > 2.將Deluge 啟動成 Web介面(不啟動 GUI)
    > 
    > #deluge -u web &
    > 
    > 或是
    > 
    > #deluge -u webui &
    > 
    > 啟動好以後，開瀏覽器連接 http://localhost:8112 就可以連線到Deluge的web介面了
    > 
    > 預設密碼：deluge

### settings

- [Queue Settings FAQ? - Deluge Forum](https://forum.deluge-torrent.org/viewtopic.php?t=33263)

    > ![](https://forum.deluge-torrent.org/download/file.php?id=2951)

    > The first 3 setting affect rotation as another user stated. However, I felt more clarification is needed, as it didn't really answer for me what each one setting actually means. At the end I also have a further question that I still need further clarification on, and hope someone can help. So here goes:
    > 
    > Under the Seeding section in the Queue Category:
    > 
    > The first 3 settings are basically if/or statements to decide on whether or not to have a torrent active or queued, by:
    > 
    > **Share Ratio Limit:** *This one is straightforward for most people, but is basically states if the ratio of seeding/downloaded in size reaches this then place torrent into queued status*
    > 
    > **Seed Time Ratio:** *This one was not originally very clear to me, but I found out from another forum it basically means, if time seeding/time downloaded >= this amount, then set torrent to queued status Example, if it takes 10 minutes to download a torrent, and you have this set at 7.00, then the torrent will seed for roughly 70 minutes (70/10 = 7) before going to queued status.*
    > 
    > **Seed Time (m):** *This is also pretty straight forward, and means if a torrent has seeded for x minutes, then place to queued status.*
    > 
    > Setting any of these of course to -1 bypasses that test on the torrent.
    > 
    > **Stop seeding when share ratio reaches:** Means the torrent will stop altogether after it has reached this limit.
    > 
    > **Remove Torrent when share ratio reached** -- *This is the one I need more help on. Does it remove the torrent from Deluge, or from Deluge and the computer? If it's the latter is their a way to stop it from doing that?*


### ThinClient

- [UserGuide/ThinClient – Deluge](https://dev.deluge-torrent.org/wiki/UserGuide/ThinClient)

    > Client Setup
    > ------------
    > 
    > ### Accessing deluged service with local UI Client
    > 
    > When attempting to access a daemon `deluged` on the same machine but running as a different user e.g. your login user is `user` and `deluged` is running as `deluge`, you may be unable access to `deluged`. This is due to the client automatically authorising using the localhost line in the auth file, which is assumed to be at the same config location as `deluged`.
    > 
    > The workaround is to replace the `localclient` line in your user config auth file (`~/.config/deluge/auth`) with the `localclient` line from the `deluged` config `auth` file e.g. `/var/lib/deluge/auth`.
    > 
    > ### GTK UI
    > 
    > The Deluge GTK UI setup require switching the GTK UI from Classic mode to Thin-client mode, then adding and connecting to the remote daemon on the server.
    > 
    > 1.  In `Preferences -> Interface` and disable (untick) `Classic Mode`
    > 2.  Restart `deluge` and you should see the `Connection Manager`.
    >     -   If it is not needed you can remove the `localhost` daemon.
    >     -   If SSH Tunnelling, before continuing [Create SSH Tunnel](https://dev.deluge-torrent.org/wiki/UserGuide/ThinClient#CreateSSHTunnel), and for `Hostname`, below, `127.0.0.2` *must* be used.
    > 3.  Create a new entry with `Add` button:
    >     -   `Hostname` is your server's IP.
    >     -   `Port` should be default `58846`.
    >     -   `Username` and `Password` are those added to the `deluged` config `auth` file.
    > 
    > If this was successful a green tick should now appear as the status for the daemon you just added.
    > 
    > Click on `Connect` and the Connection Manager should disappear.
    > 
    > *Optional step:* Expand `Options` and select '`Automatically connect to selected host on startup`' and '`Do not show this dialog on start-up`'.
    > 
    > Congratulations! You can now access the Deluge daemon, `deluged`, on the server via the GTK UI.
    > 


- [Windows deluge to deluged daemon ubuntu cannot connect - Deluge Forum](https://forum.deluge-torrent.org/viewtopic.php?t=48947)

    > UPDATE: Got it to finally work! after many installs! It was something so simple I was adding username and password to `/.config/deluge/auth` like in the guides but the username,password and level needed to be added to `/var/lib/deluge/auth`.


- [How to control Deluge remotely with a thin client](https://www.rapidseedbox.com/kb/deluge-thin-client)

    > Next step is to set a password:
    > ```
    > echo "user:MyPassword:10" >> ~/.config/deluge/auth
    > ```

- [Configure Deluge ThinClient on Ubuntu + Windows •](https://www.htpcguides.com/configure-deluge-thinclient-ubuntu-windows/)

    > Next step is to enable and allow remote connection for the Deluge daemon
    > 
    > ```
    > sudo nano /home/vpn/.config/deluge/core.conf
    > ```
    > 
    > Find the line
    > 
    > ```
    > "allow_remote": false,
    > ```
    > 
    > and change it to
    > 
    > ```
    > "allow_remote": true,
    > ```
    > 


### change language

- [Interface language - Deluge Forum](https://forum.deluge-torrent.org/viewtopic.php?t=54283)

    > In short, change your $LANG var to a US one, like "en_US.UTF-8". You can also make a shell script running deluge preceded with setting the lang var, if you only want it changed for deluge.

### plugins

- [Plugins – Deluge](https://dev.deluge-torrent.org/wiki/Plugins)

    > #### Client-Server Setups
    > 
    > When running the Deluge daemon, `deluged` and Deluge client on a separate computers, the plugin must be installed on both machines. Installing a plugin egg through the GTK client will copy the egg to both the local plugins directory, as well as the remote daemon's. However if the Python versions on the local machine and remote server do not match, you will have to copy the egg to the remote server manually.

#### uTorrent Import Plugin
- [uTorrent Import Plugin: Painlessly Migrate to Deluge! - Deluge Forum](https://forum.deluge-torrent.org/viewtopic.php?f=9&t=52145)

#### SeedTime

- [[Plugin] SeedTime - Stop seed after time (v0.5) - Deluge Forum](https://forum.deluge-torrent.org/viewtopic.php?f=9&t=39767)


#### MyScheduler v0.3.6 (Forced Start)

- [[Plugin] MyScheduler v0.3.6 (Forced Start) - Deluge Forum](https://forum.deluge-torrent.org/viewtopic.php?f=9&t=54025)



### linuxserver/deluge

- [linuxserver/deluge - Docker Hub](https://hub.docker.com/r/linuxserver/deluge/)




## Wine

- [scottyhardy/docker-wine - Docker Hub](https://hub.docker.com/r/scottyhardy/docker-wine/)

- [suchja/wine - Docker Hub](https://hub.docker.com/r/suchja/wine/)

- [yantis/wine - Docker Hub](https://hub.docker.com/r/yantis/wine/)

- [Running Wine within Docker - Ales Nosek - The Software Practitioner](http://alesnosek.com/blog/2015/07/04/running-wine-within-docker/)


### install .NET Framework

- [WineHQ - .NET Framework 2.0](https://appdb.winehq.org/objectManager.php?sClass=version&iId=3754)

    > .NET Framework 2.0 installation
    > 
    > Make sure you operate on a **clean 32-bit [WINEPREFIX](http://wiki.winehq.org/FAQ#32_bit_wineprefix "WINEPREFIX")** (~/.wine)!
    > 
    > * * * * *
    > 
    > **Installation by using 'winetricks' script**
    > 
    > Use this option for easy installation of .NET 2.0 Framework. [Winetricks](http://wiki.winehq.org/winetricks "Winetricks") will take care of all needed installation prerequisites and work around some problems.
    > 
    > ```
    > $ export WINEARCH=win32
    > 
    > $ wget https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks
    > 
    > $ bash winetricks dotnet20
    > ```


## twister p2p 微網誌

- [miguelfreitas/twister - Docker Hub](https://hub.docker.com/r/miguelfreitas/twister/)

- [twister | P2P microblogging platform](http://twister.net.co/)

- [[1312.7152] twister - a P2P microblogging platform](https://arxiv.org/abs/1312.7152)

## Blog system

- [library/ghost - Docker Hub](https://hub.docker.com/_/ghost/)

- [Ghost 第 100 个版本 1.0 发布，新增编辑器、默认主题等 - 开源中国社区](https://www.oschina.net/news/87169/ghost-1-0?from=20170730)

## fastdfs

- [luhuiguo/fastdfs - Docker Hub](https://hub.docker.com/r/luhuiguo/fastdfs/)

- [happyfish100/fastdfs: FastDFS is an open source high performance distributed file system (DFS). It's major functions include: file storing, file syncing and file accessing, and design for high capacity and load balance.](https://github.com/happyfish100/fastdfs)

- [分布式文件系统 - FastDFS 简单了解一下 - Mafly - 博客园](https://www.cnblogs.com/mafly/p/fastdfs.html)


## IPsec VPN Server

- [在 Docker 上搭建 IPsec VPN 服务器](https://liuliqiang.info/post/build-ipsec-vpn-server-with-docker/)

- [hwdsl2/ipsec-vpn-server - Docker Hub](https://hub.docker.com/r/hwdsl2/ipsec-vpn-server/)



## OpenVPN

- [How To Run OpenVPN in a Docker Container on Ubuntu 14.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-run-openvpn-in-a-docker-container-on-ubuntu-14-04)

- [kylemanna/openvpn - Docker Hub](https://hub.docker.com/r/kylemanna/openvpn/)


## Socks Proxy

### Squid
- [Squid as Socks5 Proxy server - Server Fault](https://serverfault.com/questions/352485/squid-as-socks5-proxy-server/352525)

    > Squid is an HTTP proxy, not a SOCKS proxy. It expects to talk HTTP and nothing else.
    > 
    > Have a look at Dante. I find this to be an easy and reliable SOCKS proxy server.

### Dante

- [Dante - A free SOCKS server](http://www.inet.no/dante/)

- [wernight/dante - Docker Hub](https://hub.docker.com/r/wernight/dante/)

- [vimagick/dante - Docker Hub](https://hub.docker.com/r/vimagick/dante/)



## Virtualbox

- [jazzdd/phpvirtualbox - Docker Hub](https://hub.docker.com/r/jazzdd/phpvirtualbox/)

- [wood1986/virtualbox - Docker Hub](https://hub.docker.com/r/wood1986/virtualbox/)

- [docker-library/virtualbox.vboxwebsrv.phpvirtualbox at master · wood1986/docker-library](https://github.com/wood1986/docker-library/tree/master/virtualbox.vboxwebsrv.phpvirtualbox)

- [d4kr/virtualbox - Docker Hub](https://hub.docker.com/r/d4kr/virtualbox/)

- [jencryzthers/vboxinsidedocker - Docker Hub](https://hub.docker.com/r/jencryzthers/vboxinsidedocker/)


