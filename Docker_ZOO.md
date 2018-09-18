# Docker_ZOO

[toc]
<!-- toc --> 


## Resilio Sync

- [resilio/sync - Docker Hub](https://hub.docker.com/r/resilio/sync/)

## 百度雲網盤

- [kukki/docker-baidupan - Docker Hub](https://hub.docker.com/r/kukki/docker-baidupan/)
- [XuShaohua/bcloud: 百度网盘的linux桌面客户端](https://github.com/XuShaohua/bcloud)
- [为什么百度云、360云盘等都取消了同步盘功能？ - 知乎](https://www.zhihu.com/question/38596437)

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



## Wine

- [scottyhardy/docker-wine - Docker Hub](https://hub.docker.com/r/scottyhardy/docker-wine/)

- [suchja/wine - Docker Hub](https://hub.docker.com/r/suchja/wine/)

- [yantis/wine - Docker Hub](https://hub.docker.com/r/yantis/wine/)

- [Running Wine within Docker - Ales Nosek - The Software Practitioner](http://alesnosek.com/blog/2015/07/04/running-wine-within-docker/)



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


