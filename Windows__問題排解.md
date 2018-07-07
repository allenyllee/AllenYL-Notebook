# Windows__問題排解

[toc]
<!-- toc --> 

## 常用連結

- [FileHippo.com - Download Free Software](https://filehippo.com/zh/)

## 磁碟空間清理

- [清理Windows.edb文件释放C盘空间(原创) - 瑞恩多芬 - 博客园](https://www.cnblogs.com/bison1989/archive/2011/11/09/2243703.html)

    > 经过对C盘的整体盘查，找到了下面这个文件：C:\\ProgramData\\Microsoft\\Search\\Data\\Applications\\Windows\\Windows.edb，如果你没找到的话可以通过搜索文件的方式收搜索Windows.edb。你会发现这个文件巨大，有的机子有1G多，有的机子有2G多，更有甚者达到7至8G！这个文件是用来对你整个机子的所有文件进行索引用的，这样你使用windows键+F键搜索文件的时候可以比较快速地搜索出你想要的文件。
    > 
    > 如果你不想继续使用索引技术，可以进行如下操作（我的是win7，xp的具体查看其他文档资料）：开始--->附件--->运行--->输入services.msc--->确定--->找到“Windows Search”服务--->右键--->关闭，想用的时候再开启。

- [Windows.edb 檔將會以在 Windows 8 或 Windows Server 2012 非常大](https://support.microsoft.com/zh-tw/help/2838018/the-windows-edb-file-grows-very-large-in-windows-8-or-windows-server-2)

    __如何刪除並重建索引__

    -   在 \[搜尋\] 方塊中，鍵入**索引選項**。  

    -   點選或按一下 \[**索引選項**。
    -   請點選或按一下 \[**進階**\]。
    -   點選或按一下 \[**索引設定**\] 索引標籤中的 \[**重建**\]。
    -   點選或按一下\[**確定**\]以確認。

## 軟體安裝問題

- [Can't Update Evernote, Evernote.msi missing - Evernote for Windows - Evernote User Forum](https://discussion.evernote.com/topic/100267-cant-update-evernote-evernotemsi-missing/)

    >  I have the same problem every time I try to update Evernote—**update will crash because of msi file missing.** For the last update I searched the forums and eventually made it work.
    > 
    > For this one, the problem was still there. I tired uninstalling it only to find out I have now Evernote 6.2.4 and Evernote 6.1.2 both installed. I was able to uninstall the newer version, but the old version is still there, **can not be uninstalled due to missing MSI**, I can not install or run Evernote because of the same MSI that seems to be corrupt. Can you plese give me a solution that would fix this permanently? 
    > 
    > ---
    > Hi. It's been suggested before that the way out of that corner is to reinstall 6.1.2 so as to 'correct' the installation,  then uninstall it completely and install the current version.  [Evernote 6.1.2 installer](http://filehippo.com/download_evernote/68286/)
    > 

## Realtek HD Audio Manager missing

- [Realtek HD Audio Manager missing. - Realtek - Apps General Discussion](http://www.tomsguide.com/answers/id-3486617/realtek-audio-manager-missing.html)

    > You have to download drivers from your motherboards manufacturer. "several sources" means several drivers and they are probably conflicting to take control of the audio device. Uninstall current drivers first before installing new ones. Also under device manager, click "show hidden devices" under view and uninstall duplicate audio devices.

## Disable Flashing Taskbar buttons or icons on Windows taskbar

- [Disable Flashing Taskbar buttons or icons in Windows 10/8/7](https://www.thewindowsclub.com/disable-flashing-taskbar-buttons-windows)

    > Notifications in Windows are present to draw your attention to programs or areas that require your immediate attention. While this helps in resolving issues quickly it can annoy some. Especially the taskbar icons or buttons which flash, once the program is opened or there is a change in the program. Its icon shows up on the taskbar and begin flashing, becoming golden yellow. It will flash **7 times**, after which it will continue to throb gently. In this post, we will see how you can **disable the flashing of taskbar buttons or icons** or **change the count** for the number of times it can flash.
    > 
    > Disable Flashing Taskbar buttons
    > --------------------------------
    > 
    > Open the Windows Registry, by typing *regedit* in Run box. It's the [Windows Registry](https://www.thewindowsclub.com/windows-registry-basics) that stores configuration information about many important parts of Windows operating system. By editing it, you can tune Windows to behave the way you want it. However, modifying the Windows Registry can cause serious problems to your system, so make sure you know what you're doing and create a system restore point first before proceeding further.
    > 
    > ![regedit](https://thewindowsclub-thewindowsclubco.netdna-ssl.com/wp-content/uploads/2015/06/regedit1.png)
    > 
    > Locate and then click the subkey that holds the registry item or items that you want to change. For this, browse the following path:
    > 
    > HKEY_CURRENT_USER\Control Panel\Desktop
    > 
    > ![Desktop](https://thewindowsclub-thewindowsclubco.netdna-ssl.com/wp-content/uploads/2015/06/Desktop-600x344.png)
    > 
    > Double-click the **ForegroundFlashCount** entry and change the Value data field to **0**. The default on my Windows 8.1 computer is 7 in Hexadecimal.
    > 
    > ![value](https://thewindowsclub-thewindowsclubco.netdna-ssl.com/wp-content/uploads/2015/06/value.png)
    > 
    > > ForegroundFlashCount specifies the number of times the taskbar button flashes to notify the user that the system has activated a background window. ForegroundLockTimeout specifies the time, following user input, during which the system keeps applications from moving into the foreground. If the time elapsed since the last user input exceeds the value of the ForegroundLockTimeout entry, the window will automatically be brought to the foreground.
    > 
    > So, you may want to also ensure that value of **ForegroundLockTimeout** is set to **0**. The default on my Windows 8.1 computer is 30d40 in Hexadecimal.
    > 
    > ![Disable Flashing Taskbar buttons](https://thewindowsclub-thewindowsclubco.netdna-ssl.com/wp-content/uploads/2015/06/foreground-flashcount1-600x326.png "Disable Flashing Taskbar buttons")
    > 
    > After having done this, restart Windows and you should no longer see any flashing icon in the taskbar on your Windows 8.1 computer.
    > 
    > ### Change the number of time Taskbar button flashes
    > 
    > If you want to Change the number of time Taskbar button flashes, then you can change the value of ForegroundFlashCount from the default 7, to a number **between 1 and 6**, and restart your computer.
    > 

