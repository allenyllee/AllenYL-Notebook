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

## Allow or Prevent Devices to Wake Computer in Windows 10

- [Allow or Prevent Devices to Wake Computer in Windows 10 | Windows 10 Tutorials](https://www.tenforums.com/tutorials/63148-allow-prevent-devices-wake-computer-windows-10-a.html)

    > To Prevent Device to Wake the Computer\
    > A) Type the command below into the command prompt, and press Enter. (see screenshot below)
    > 
    > ![Note](https://www.tenforums.com/images/notesmall10.png "Note")   Note
    > 
    > This will give you a list of all [**devices that are able to wake the computer**](https://www.tenforums.com/tutorials/63142-devices-able-wake-computer-see-windows-10-a.html#option1).
    > 
    > Make note of the device name (ex: "HID Keyboard Device") you want to prevent to wake the computer.
    > 
    > ![](https://www.tenforums.com/images/smilies/arrow.png "Arrow") **powercfg -devicequery wake_armed**
    > 
    > ![Name:  Devices_allowed_to_wake_computer.png
    > Views: 26061
    > Size:  15.9 KB](https://www.tenforums.com/attachments/tutorials/100645d1485971642-allow-prevent-devices-wake-computer-windows-10-a-devices_allowed_to_wake_computer.png?s=8106f81ac5702d12839bbad7aa1a3ee7 )\
    > B) Type the command below into the command prompt, and press Enter. You can close the command prompt when finished. (see screenshot below)\
    > ![](https://www.tenforums.com/images/smilies/arrow.png "Arrow") **powercfg -devicedisablewake "Device Name"**
    > 
    > ![Note](https://www.tenforums.com/images/notesmall10.png "Note")   Note
    > 
    > Substitute **Device Name** in the command above with the actual name of the device.
    > 
    > For example: **powercfg -devicedisablewake "HID Keyboard Device"**
    > 
    > ![Click image for larger version. Name:	Disable_device_to_wake_computer.png 
    > Views:	274 
    > Size:	12.5 KB 
    > ID:	100646](https://www.tenforums.com/attachments/tutorials/100646d1485971642t-allow-prevent-devices-wake-computer-windows-10--disable_device_to_wake_computer.png?s=8106f81ac5702d12839bbad7aa1a3ee7) 
    > 

## 因為應用程式的並列設定不正確，所以無法啟動。 "The application has failed to start because the application configuration is incorrect." 

- [【攻略】【轉貼】「因為應用程式的並列設定不正確，所以無法啟動。」解決方法 @小朋友齊打交 系列 哈啦板 - 巴哈姆特](https://forum.gamer.com.tw/C.php?bsn=7648&snA=3390)

    > Win Vista,7,8,10常遇到的問題
    > 
    > 無法執行之問題\
    > 顯示訊息「因為應用程式的並列設定不正確，所以無法啟動。」等字樣\
    > 請先安裝[Microsoft VC++ 2005 redistributable package](http://ref.gamer.com.tw/redir.php?url=http%3A%2F%2Fwww.microsoft.com%2Fzh-tw%2Fdownload%2Fdetails.aspx%3Fid%3D3387)
    > 
    > 若仍然不能執行，請再安裝[Microsoft VC++ 2005 SP1 redistributable package](http://ref.gamer.com.tw/redir.php?url=http%3A%2F%2Fwww.microsoft.com%2Fzh-tw%2Fdownload%2Fdetails.aspx%3Fid%3D5638)
    > 
    > 還是沒辦法執行請依序安裝以下套件
    > 
    > [Microsoft VC++ 2008 redistributable package](http://ref.gamer.com.tw/redir.php?url=http%3A%2F%2Fwww.microsoft.com%2Fzh-tw%2Fdownload%2Fdetails.aspx%3Fid%3D29)\
    > [Microsoft VC++ 2008 SP1 redistributable package](http://ref.gamer.com.tw/redir.php?url=http%3A%2F%2Fwww.microsoft.com%2Fzh-tw%2Fdownload%2Fdetails.aspx%3Fid%3D5582)\
    > [Microsoft VC++ 2010 redistributable package](http://ref.gamer.com.tw/redir.php?url=http%3A%2F%2Fwww.microsoft.com%2Fzh-tw%2Fdownload%2Fdetails.aspx%3Fid%3D5555)\
    > [Microsoft VC++ 2010 SP1 redistributable package](http://ref.gamer.com.tw/redir.php?url=http%3A%2F%2Fwww.microsoft.com%2Fzh-tw%2Fdownload%2Fdetails.aspx%3Fid%3D8328)
    > 
    > 安裝完仍然不能執行就請檢查是否有這兩個檔案
    > 
    > C:\WINDOWS\WinSxS\x86_Microsoft.VC80.CRT_1fc8b3b9a1e18e3b_8.0.50727.4053_x-ww_e6967989\MSVCR80.dll
    > 
    > C:\WINDOWS\WinSxS\x86_Microsoft.VC80.CRT_1fc8b3b9a1e18e3b_8.0.50727.4053_x-ww_e6967989\MSVCP80.dll
    > 
    > 若沒有這兩個檔案的話請全部移除後重新安裝。
    > 
    > ※如果不能安裝或是安裝失敗，可以建立新使用者帳號並登入該使用者進行安裝。\
    > ※可能會有安裝不完全的情況發生，重新移除套件後重新開機再安裝一次。
    > 
    > 如果真的還是不行就去「事件檢視器」找應用程式錯誤紀錄，若找不到我也沒辦法了。
    > 

## 彻底删除alibabaprotect

- [alibabaprotect是什么,如何彻底删除alibabaprotect](http://www.dnpz.net/diannaozhishi/2360.html)

    > **彻底删除Alibabaprotect的方法：**
    > 
    >    1、首先要卸载优酷客户端然后再进行以下操作。
    > 
    >    2、在系统对应的目录下建立一个名为AlibabaProtect 的文件夹。32位系统，在C:\Program Files 目录（64位系统，在C:\Program Files （x86）目录），如下图。
    > 
    > ![alibabaprotect是什么,如何彻底删除alibabaprotect](http://www.dnpz.net/uploads/allimg/180211/983-1P21110195K04.jpg)
    > 
    >    3、在AlibabaProtect文件夹上单击右键，选择属性；
    > 
    > ![alibabaprotect是什么,如何彻底删除alibabaprotect](http://www.dnpz.net/uploads/allimg/180211/983-1P211102005N3.jpg)
    > 
    >    4、打开AlibabaProtect属性界面后切换到 安全选卡，点击【编辑】，然后把每一个账户的权限全部修改成拒绝，点击应用 确定 保存设置即可，如下图。
    > 
    > ![alibabaprotect是什么,如何彻底删除alibabaprotect](http://www.dnpz.net/uploads/allimg/180211/983-1P211102014G3.jpg)
    > 
    > ![alibabaprotect是什么,如何彻底删除alibabaprotect](http://www.dnpz.net/uploads/allimg/180211/983-1P2111020241P.jpg)
    > 
    >    5、重新安装优酷客户端，这样就不会被强制安装AlibabaProtect了。
    >    
    >        


## You need Administrator Permission To Delete This Folder *FIX*

<iframe width="560" height="315" src="https://www.youtube.com/embed/RE3dYzH1CgI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## disable reopening programs after restart/startup

- [Windows 10 - disable reopening programs after restart/startup - Super User](https://superuser.com/questions/1229963/windows-10-disable-reopening-programs-after-restart-startup)

    > **Settings** > **Accounts** > **Sign-In Options**
    > 
    > Scroll down to **Privacy** on the right and then set the following to **Off**:
    > 
    > ```
    > Use my sign-in info to automatically finish setting up my device after an update or restart.
    > 
    > ```
    > 
    > [![Privacy Settings](https://i.stack.imgur.com/GHjOq.jpg)](https://i.stack.imgur.com/GHjOq.jpg)
    > 
    > I was skeptical, because that doesn't seem like it has much to do with reopening my Google Chrome upon restart, but I tested and it *(finally)* works!
    > 
    > * * * * *
    > 
    > **Update**: with the release of Windows 10 version 1803 (the April 2018 Update), Microsoft modified the wording within that Privacy option to emphasize that it will *"reopen my apps"* if it is configured to be **On**.
    > 
    > ```
    > Use my sign-in info to automatically finish setting up my device and reopen my apps after an update or restart.
    > 
    > ```
    > 
    > [![Disable Reopen My Apps](https://i.stack.imgur.com/rVgzn.jpg)](https://i.stack.imgur.com/rVgzn.jpg)
    > 



## ssh

### enable ssh

- [How to enable, login to, or disable Microsoft SSH Server in Windows 10 - Ctrl blog](https://www.ctrl.blog/entry/how-to-win10-ssh-service)

    > ### Enabling the SSH Server service
    > 
    > 1.  Open the Windows Settings app and go to Update and Security: For developers.
    > 2.  Switch to Developer mode and wait for it to finish downloading any packages.
    > 3.  If you're asked to reboot after the previous step, do so now.
    > 4.  Turn on the Device discovery option.
    > 5.  Turn off the Device discovery option again, unless you want this feature (which adds mDNS support to Windows and allows for remote debugging).
    > 
    > This will enable the SSH Server Broker (SshBroker.dll) and SSH Server Proxy (SshProxy.dll) background services which will handle incoming connections to TCP port 22. The Windows Firewall on your device is automatically configured to allow the service to **listen for incoming connections from both private and public networks.** Read on to learn how to restrict access from trusted networks and block connections from the public internet.
    > 
    > ### Logging in to the SSH Server
    > 
    > You can use any standard SSH client to log in to your device.
    > 
    > Advertisement
    > 
    > You log in using your Windows Account name and either your Microsoft Account password or your local Windows Account password. Please note that your Windows Account name is not the same as your Microsoft Account or domain email address.
    > 
    > You can connect to your device's IPv4 or IPv6 address, or use the device's given NetBIOS name. You can find your device's given name as well as your Windows Account name by executing the "`whoami`" command in PowerShell or Command Prompt. The first part is your NetBIOS name followed by a forward slash, and then your Windows Account name.
    > 
    > Note that you're logged in to the Command Prompt by default and not the Bash shell for Windows. You can type in one of `bash` or `powershell` after logging to switch to either the Bash shell or PowerShell.
    > 
    > ### Protecting the SSH Server
    > 
    > There are currently no brute-force login protection mechanism built into the SSH Server, and Group Policies for rate-limiting login attempts are bypassed for the SSH Server service. This means a remote attacker can make as many guesses of your login credentials as they can possibly push through the network.
    > 
    > Linux and macOS utilities for thwarting brute-force login attempts like SSHGuard and Fail2Ban are not available on Windows. Although they both run in the Windows Subsystem for Linux, they don't have access to nor parsers for the Windows Event Log nor backends for the Windows Firewall.
    > 
    > Without any brute-force login ~~mechanism~~ protections, you're left with depending on a strong account password that you change regularly. You can limit the risk of a brute force attack by disabling login from remote networks. This will limit the service to only accept logins from what is identified in Windows as a local and private network source.
    > 
    > To disable remote network logins, follow the following instructions:
    > 
    > 1.  Open the Start menu and search for "`allow firewall`". Open `Allow an app through the Windows Firewall`.
    > 2.  Authenticate yourself to modify the firewall rules by clicking the `Change settings` button.
    > 3.  Locate "Ssh Server" in the list and disable the checkbox in the Public column.
    > 4.  Click the `OK` button to apply the changes.
    > 
    > This does depend on having the correct trust levels configured for the networks your computer connects to. Explore the Network section of the Windows Settings app to see the currently configured level of trust in the various networks your device is connected to.
    > 
    > ### Disabling the SSH Server service
    > 
    > There is no on or off switch for the SSH server itself. As you might have guessed from the above section on how to enable the service, it was clearly a bit of an afterthought. To properly disable the service, follow these steps:
    > 
    > 1.  Open the Windows Settings app and go to Update and Security: For developers.
    > 2.  Turn off the Device discovery option if it was previously enabled.
    > 3.  Switch to Windows Store apps mode.
    > 4.  Switch back to Developer mode, if desired.
    > 


