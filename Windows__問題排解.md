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

## Prevent Hard Disk from going to Sleep

- [NoSleepHD v2.0 by Ashutosh Agarwal](https://archive.codeplex.com/?p=nosleephd)

- [Prevent Hard Disk from going to Sleep in Windows 10/8/7](https://www.thewindowsclub.com/prevent-hard-drive-going-sleep-windows)




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


# disk and filesystem

## List Drives using Command Prompt and PowerShell

- [List Drives using Command Prompt and PowerShell](https://www.thewindowsclub.com/list-drives-using-command-prompt-powershell-windows)

    > ### List Drives using Command Prompt
    > 
    > If you need to simply list the drives, you may use **[WMIC](https://www.thewindowsclub.com/wmi-commands-on-windows-7)**.  Windows Management Instrumentation (WMI) is the infrastructure for management data and operations on Windows-based operating systems.
    > 
    > Open a command prompt, and type the following command:
    > 
    > wmic logicaldisk get name
    > 
    > Press Enter and you will see the list of Drives.
    > 
    > You can also use the following parameter:
    > 
    > wmic logicaldisk get caption
    > 
    > ![List Drives in Command Prompt 2](https://thewindowsclub-thewindowsclubco.netdna-ssl.com/wp-content/uploads/2015/08/List-Drives-in-Command-Prompt-2-600x384.jpg)
    > 
    > Using the following will display Device ID and volume name as well:
    > 
    > wmic logicaldisk get deviceid, volumename, description
    > 
    > Windows also includes an additional command-line tool for file, system and disk management, called **[Fsutil](https://www.thewindowsclub.com/disk-management-tool-windows)**. This utility helps you lits files, change the short name of a file, find files by SID's (Security Identifier) and perform other complex tasks.  You can also use *fsutil* to display drives. Use the following command:
    > 
    > fsutil fsinfo drives
    > 
    > It will show mapped drives too.
    > 
    > You can also use [**diskpart**](https://www.thewindowsclub.com/disk-management-tool-windows) to get a list of drives along with some more details. The  Diskpart utility can do everything that the Disk Management console can do, and more! It's invaluable for script writers or anyone who simply prefers working at a command prompt.
    > 
    > Open CMD and type *diskpart*. Next use the following command:
    > 
    > list volume
    > 
    > ![List Drives in Command Prompt](https://thewindowsclub-thewindowsclubco.netdna-ssl.com/wp-content/uploads/2015/08/List-Drives-in-Command-Prompt-1-600x318.jpg)
    > 
    > You will see that the console display the Volume number and letter, label, formatting type, partition type, size, status and other information.
    > 
    > ### List Drives using PowerShell
    > 
    > To display drives using PowerShell, type *powershell* in the same CMD windows and hit Enter. This will open a PowerShell window.
    > 
    > Now use the following command:
    > 
    > get-psdrive -psprovider filesystem
    > 
    > ![List Drives in powershell](https://thewindowsclub-thewindowsclubco.netdna-ssl.com/wp-content/uploads/2015/08/List-Drives-in-powershell-3-600x318.jpg)
    > 

- [windows - List every \Device\Harddiskvolume.? - Super User](https://superuser.com/questions/1058217/list-every-device-harddiskvolume)


    > Found a powershell script that lists the mounted volumes:
    > 
    > ```powershell
    > # Biuild System Assembly in order to call Kernel32:QueryDosDevice.
    >    $DynAssembly = New-Object System.Reflection.AssemblyName('SysUtils')
    >    $AssemblyBuilder = [AppDomain]::CurrentDomain.DefineDynamicAssembly($DynAssembly, [Reflection.Emit.AssemblyBuilderAccess]::Run)
    >    $ModuleBuilder = $AssemblyBuilder.DefineDynamicModule('SysUtils', $False)
    > 
    >    # Define [Kernel32]::QueryDosDevice method
    >    $TypeBuilder = $ModuleBuilder.DefineType('Kernel32', 'Public, Class')
    >    $PInvokeMethod = $TypeBuilder.DefinePInvokeMethod('QueryDosDevice', 'kernel32.dll', ([Reflection.MethodAttributes]::Public -bor [Reflection.MethodAttributes]::Static), [Reflection.CallingConventions]::Standard, [UInt32], [Type[]]@([String], [Text.StringBuilder], [UInt32]), [Runtime.InteropServices.CallingConvention]::Winapi, [Runtime.InteropServices.CharSet]::Auto)
    >    $DllImportConstructor = [Runtime.InteropServices.DllImportAttribute].GetConstructor(@([String]))
    >    $SetLastError = [Runtime.InteropServices.DllImportAttribute].GetField('SetLastError')
    >    $SetLastErrorCustomAttribute = New-Object Reflection.Emit.CustomAttributeBuilder($DllImportConstructor, @('kernel32.dll'), [Reflection.FieldInfo[]]@($SetLastError), @($true))
    >    $PInvokeMethod.SetCustomAttribute($SetLastErrorCustomAttribute)
    >    $Kernel32 = $TypeBuilder.CreateType()
    > 
    >    $Max = 65536
    >    $StringBuilder = New-Object System.Text.StringBuilder($Max)
    > 
    >    Get-WmiObject Win32_Volume | ? { $_.DriveLetter } | % {
    >        $ReturnLength = $Kernel32::QueryDosDevice($_.DriveLetter, $StringBuilder, $Max)
    > 
    >        if ($ReturnLength)
    >        {
    >            $DriveMapping = @{
    >                DriveLetter = $_.DriveLetter
    >                DevicePath = $StringBuilder.ToString()
    >            }
    > 
    >            New-Object PSObject -Property $DriveMapping
    >        }
    >    }
    > 
    > ```
    > 
    > Source: <http://www.morgantechspace.com/2014/11/Get-Volume-Path-from-Drive-Name-using-Powershell.html>
    > 
    > Output looks like this:
    > 
    > ```
    > DevicePath               DriveLetter
    > ----------               -----------
    > \Device\HarddiskVolume2  F:
    > \Device\HarddiskVolume7  J:
    > \Device\HarddiskVolume10 D:
    > \Device\HarddiskVolume12 E:
    > \Device\HarddiskVolume5  C:
    > 
    > ```
    > 

- [Get Volume Path from Drive Name using Powershell script](https://www.morgantechspace.com/2014/11/Get-Volume-Path-from-Drive-Name-using-Powershell.html)

    > Get Device Path from Device Name (Drive Letter) using Powershell script
    > =======================================================================
    > 
    > The below script displays **Device Path** for the given **Device Name**(Derive letter). The device name(drive letter) cannot have a trailing backslash; for example, use "**C:**", not "**C:\**". Follow the below steps to get volume path from drive letter.
    > 
    >    1. Copy the below [Powershell](http://www.morgantechspace.com/search/label/Powershell) script and paste in Notepad file.\
    >    2. Save As the Notepad file with the extension **.ps1** like **Get-DevicePath-from-DeviceName.ps1**
    > 
    > **Powershell Script**: [Download Get-DevicePath-from-DeviceName.ps1](http://sourceforge.net/projects/morgansource/files/Powershell/SystemInfo/Get-DevicePath-from-DeviceName.ps1/download)
    > ```powershell
    > $driveLetter = Read-Host "Enter Drive Letter:"
    > Write-Host " "
    > $DynAssembly = New-Object System.Reflection.AssemblyName('SysUtils')
    > $AssemblyBuilder = [AppDomain]::CurrentDomain.DefineDynamicAssembly($DynAssembly, [Reflection.Emit.AssemblyBuilderAccess]::Run)
    > $ModuleBuilder = $AssemblyBuilder.DefineDynamicModule('SysUtils', $False)
    >  
    > # Define [Kernel32]::QueryDosDevice method
    > $TypeBuilder = $ModuleBuilder.DefineType('Kernel32', 'Public, Class')
    > $PInvokeMethod = $TypeBuilder.DefinePInvokeMethod('QueryDosDevice', 'kernel32.dll', ([Reflection.MethodAttributes]::Public -bor [Reflection.MethodAttributes]::Static), [Reflection.CallingConventions]::Standard, [UInt32], [Type[]]@([String], [Text.StringBuilder], [UInt32]), [Runtime.InteropServices.CallingConvention]::Winapi, [Runtime.InteropServices.CharSet]::Auto)
    > $DllImportConstructor = [Runtime.InteropServices.DllImportAttribute].GetConstructor(@([String]))
    > $SetLastError = [Runtime.InteropServices.DllImportAttribute].GetField('SetLastError')
    > $SetLastErrorCustomAttribute = New-Object Reflection.Emit.CustomAttributeBuilder($DllImportConstructor, @('kernel32.dll'), [Reflection.FieldInfo[]]@($SetLastError), @($true))
    > $PInvokeMethod.SetCustomAttribute($SetLastErrorCustomAttribute)
    > $Kernel32 = $TypeBuilder.CreateType()
    >  
    > $Max = 65536
    > $StringBuilder = New-Object System.Text.StringBuilder($Max)
    > $ReturnLength = $Kernel32::QueryDosDevice($driveLetter, $StringBuilder, $Max)
    >  
    >  if ($ReturnLength)
    >  {
    >      Write-Host "Device Path: "$StringBuilder.ToString()
    >   }
    >   else
    >   {
    >       Write-Host "Device Path: not found"
    >   }
    > Write-Host " "
    > ```
    > 
    >    3. Now run the script file **Get-DevicePath-from-DeviceName.ps1** from [Powershell](http://www.morgantechspace.com/search/label/Powershell), and give the Drive letter as argument which you want to get device path.
    > 
    > [![Get Volume Path from Drive Name using Powershell script](https://1.bp.blogspot.com/-eMioNnOMwXM/VGJdsGSjUzI/AAAAAAAABXo/RV0jAmSOjrc/s320/Get-Device-Path-from-Device-Name.png)](https://1.bp.blogspot.com/-eMioNnOMwXM/VGJdsGSjUzI/AAAAAAAABXo/RV0jAmSOjrc/s1600/Get-Device-Path-from-Device-Name.png)
    > 


## create 1G zeroed sparse file in windows

- [fsutil - How to create 1G zeroed sparse file in windows? - Super User](https://superuser.com/questions/314310/how-to-create-1g-zeroed-sparse-file-in-windows)


    > ```
    > FSUtil File CreateNew temp 0x100000
    > FSUtil Sparse SetFlag temp
    > FSUtil Sparse SetRange temp 0 0x100000
    > ```

## mount raw(dd) HDD image on Windows

- [3 Ways to Mount a RAW Image in Windows](http://www.hackingarticles.in/3-ways-mount-raw-image-windows/)

    > In Forensic, to investigate a hard drive or disks we always make a forensic image. A Forensic Image is a forensically sound and complete copy of a hard drive or other digital media, generally intended for use as evidence. Copies include unallocated space, slack space, and boot record.  Many computer forensic programs, especially the all-in-one suites, use their own file formats to store information. These images are stored in a format of RAW file or AFF or E01.
    > 
    > **RAW Image Format: This** format is a RAW bit-by-bit copy of the original. It is often accompanied by Meta data stored in separate formats. This Image Format is most common used and is read by every Forensic tool in the industry.
    > 
    > Once the RAW image is created, it can't be read unless it is mounted by a tool. Mount is the process that will take the raw logical image and mount it onto a specified directory of choice to be able to examine the contents of that image. The image has to include be a recognizable file system as a partition. This makes invocation of the command interesting as the raw image is a physical disk image and not a specific partition of a file system.
    > 
    > Mount an image for a read-only view that leverages to see the content of the image exactly as the user saw it on the original drive.
    > 
    > There are various methods to mount a RAW file. But before we learn how to mount our RAW files, just have look on your my computer so that you can have a idea about how many drives you have before mounting a RAW file. For instance, following is the image of my computer of my PC:
    > 
    > ![](https://i2.wp.com/3.bp.blogspot.com/-CcidtOfCSao/V7M07hECrQI/AAAAAAAANIQ/2-fgVh1LqE4c4ViITXe0lec4VlJuLkuEQCLcB/s1600/1.png?w=687&ssl=1)
    > 
    > Now, Let us have a look on these methods :
    > 
    > **Forensic Tool Kit Imager**
    > 
    > FTK Imager (version -- 3.4.2) is tool introduced by Access Data which is used to preview data. It is also an imaging tool that lets us acquire in a forensically sound way. FTK helps us to create forensic images, Mount an image for a read-only view, Create hashes of files, etc and right now we will focus on its Mount function. To mount a RAW image file via FTK, first of all download FTK from --> <http://accessdata.com/product-download/digital-forensics/ftk-imager-version-3.4.2>
    > 
    > Now that FTK is downloaded and installed, open it and click on **Files** on the menu bar. A drop down menu will appear, from this menu click on **Image Mounting**.
    > 
    > ![](https://i1.wp.com/4.bp.blogspot.com/-QRNIWQB07QA/V7M08xbHx-I/AAAAAAAANIs/4Vj5USPeIfgIMWf9LPI_mgcHOj8uMfjBACLcB/s1600/3.png?w=687&ssl=1)
    > 
    > A dialogue box will open now. Give the path of RAW file in Image File option and click on **Mount button**.
    > 
    > ![](https://i1.wp.com/1.bp.blogspot.com/-65jXAGU8tAo/V7M087VDMEI/AAAAAAAANIo/FIA-zq4DbXUdA79vEG6Xxc_6brtK0YbkgCLcB/s1600/2.png?w=687&ssl=1)
    > 
    > Once you click on Mount button your image will be mounted and you can see result in Mapped images:
    > 
    > ![](https://i2.wp.com/1.bp.blogspot.com/-_LRnNH951rw/V7M09aC0XTI/AAAAAAAANIw/FlnyZZIUc6ALdlzOHRA6CLySR3h8LJwlgCLcB/s1600/4.png?w=687&ssl=1)
    > 
    > **OSFMount**
    > 
    > OSFMount (version -- 1.5.1015) is software by PassMark Software's. It helps you mount your image files even your hard disk image file in windows with a drive letter. You can then analyze the disk image files further. For your original files not to be altered, the image files are mounted as read only by default. Download this software from --> **<http://www.osforensics.com/tools/mount-disk-images.html>**
    > 
    > Open OSFMount after the instalation is completed open it:
    > 
    > ![](https://i2.wp.com/1.bp.blogspot.com/-2l7IZV4YpQw/V7M09a7h-GI/AAAAAAAANI0/k7a65eWdclIFw0mHIZvwxVPzlnlPY_c-wCLcB/s1600/5.png?w=687&ssl=1)
    > 
    > Go to File menu and select **Mount new virtual disk** option.
    > 
    > ![](https://i0.wp.com/2.bp.blogspot.com/-e7Ai0AI4IVE/V7M09ik-_PI/AAAAAAAANI4/fudQXgLWmRwRl4dzmpdSxbJ4H-4Vb3LowCLcB/s1600/6.png?w=687&ssl=1)
    > 
    > Dialogues will open; here give the path of your image file under the heading Image file and click on **OK**.
    > 
    > ![](https://i1.wp.com/2.bp.blogspot.com/-piBHZcyCaBY/V7M09_HGKOI/AAAAAAAANI8/lRRC_mzgUi4i9vbTbInZPEfEvxT_koAaQCLcB/s1600/7.png?w=687&ssl=1)
    > 
    > You can see in the following image that your RAW image will be mounted as a result:
    > 
    > ![](https://i0.wp.com/3.bp.blogspot.com/--QMejVsVO3Y/V7M09_HfNsI/AAAAAAAANJA/wVLr5VWlxvA2xAMwMtWUTX46_E4_JRzkACLcB/s1600/8.png?w=687&ssl=1)
    > 
    > **Mount Image Pro**
    > 
    > Get Data is a software development company that has launched Mount Image Pro (version -- 6). It is a computer forensic tool which enables us to mount an image for forensic purpose. You can download this software from **<http://www.mountimage.com/>**
    > 
    > Open the software after its installation.
    > 
    > ![](https://i2.wp.com/1.bp.blogspot.com/-0IldbOfFMbU/V7M0-Noi6NI/AAAAAAAANJE/shzG-Gs6XT4yQCprWpOAI7YL4qYa9h58ACLcB/s1600/9.png?w=687&ssl=1)
    > 
    > Go to **File menu** and click on **Mount Image File.**
    > 
    > ![](https://i2.wp.com/1.bp.blogspot.com/-iUahPG4BJlw/V7M07gjYgoI/AAAAAAAANIM/XxzOaGfSVcA7hukaJywhVluwykWVsNrMACLcB/s1600/10.png?w=687&ssl=1)
    > 
    > A dialogue box will open and select your image file from it.
    > 
    > ![](https://i1.wp.com/3.bp.blogspot.com/-XIqAPeW4HuY/V7M07qLousI/AAAAAAAANIU/r9tUGEQTFBwwHDvt9r0h1Q3-Isp82p_wQCLcB/s1600/11.png?w=687&ssl=1)
    > 
    > And then another dialogue box will open informing you with all the details. Click on OK.
    > 
    > ![](https://i1.wp.com/2.bp.blogspot.com/-Xs_yNahPXps/V7M08BH3aZI/AAAAAAAANIY/pAB9P1P_P6M5cEKkncbHxhG_gBtuw7jXgCLcB/s1600/12.png?w=687&ssl=1)
    > 
    > It will further show you the progress in another dialogue box.
    > 
    > ![](https://i1.wp.com/2.bp.blogspot.com/-MZHHfqt-fc4/V7M08NMOnWI/AAAAAAAANIc/Z4vYu4FdPUUXk82189wHUMe5955difzPgCLcB/s1600/13.png?w=687&ssl=1)
    > 
    > And as the outcome you can see that your image file will mount as shown in following image:
    > 
    > ![](https://i2.wp.com/2.bp.blogspot.com/-dsj_hWiERVQ/V7M08XMVB_I/AAAAAAAANIg/OUNf74vho18mcNDiiTdxmlR6jNwyJeszQCLcB/s1600/14.png?w=687&ssl=1)
    > 
    > Now, as i had asked you to check you're my computer before mounting the image, similarly, you can again check my computer and you will an extra drive as shown below:
    > 
    > ![](https://i1.wp.com/4.bp.blogspot.com/-bMGiI8Y-PXk/V7M08jn5V-I/AAAAAAAANIk/boAdLlk6FQMlQVIh5KBFllc7-yH9tEjKACLcB/s1600/15.png?w=687&ssl=1)
    > 
    > **Author**: **Yashika Dhir** is a passionate Researcher and Technical Writer at Hacking Articles. She is a hacking enthusiast. contact **[here](https://www.linkedin.com/in/yashika-dhir-b94722a3?trk=pulse-det-athr_prof-art_hdr)**
    > 
    > 



- [How to mount raw HDD image on Windows? - Software Recommendations Stack Exchange](https://softwarerecs.stackexchange.com/questions/18966/how-to-mount-raw-hdd-image-on-windows?newreg=2d14ea277b3a41b0aec2f1e34e325f86)

    > You can convert a raw image into a VHD basically it just needs some extra headers.
    > 
    > Microsoft created a tool called vhdtool.exe which can convert the raw image. A technet post here lists all the tools for hyper-v <http://social.technet.microsoft.com/wiki/contents/articles/121.hyper-v-tools.aspx>.
    > 
    > Please note as Microsoft has terminated technet things are getting hard to find.
    > 
    > As an alternative you can use [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and its VBoxManage tool to convert a raw disk dump into a VHD-file:
    > 
    > ```
    > VBoxManage.exe convertdd disk.raw disk.vhd --format VHD
    > 
    > ```
    > 
    > You can then mount the VHD (windows 7 and above only though)
    > 
    > To do this:
    > 
    > -   Open Computer Management (In admin tools control panel)
    > -   Click Disk Management
    > -   Click Action -> Mount VHD (If greyed out click on the list of drives)
    > 
    > **EDIT**
    > 
    > **Make sure you work on a copy of the image file as the vhdtool.exe tool writes directly to the file specified!!**
    > 
    > **Also you will need to rename the file to .vhd manually after**
    > 

### VhdTool/VhdxTool

- [VhdTool Is Dead, Long Live VhdxTool!](https://www.systola.com/blog/14.01.2015/VhdTool-Is-Dead-Long-Live-VhdxTool/)

- [vhd修复工具vhdtool,资源比较难找 - CSDN博客](https://blog.csdn.net/gogcc/article/details/51144701)

    > ### 1小时
    > 
    > 如果使用vhd中一不小心断电了,vhd就报错.
    > 
    > 提示无法装载,文件或目录损坏! 
    > 
    > gogo好久找到一个死链:
    > 
    >    <http://code.msdn.microsoft.com/vhdtool>
    > 
    > 受不了![大哭](http://static.blog.csdn.net/xheditor/xheditor_emot/default/wail.gif)
    > 
    > ### 2小时
    > 
    > 然后又找到了:vhdxtool
    > 
    >     http://systola.com/support/KB100005
    > 
    > 结果都没有修复功能.
    > 
    > ### 3小时
    > 
    > 又找到一个:
    > 
    >  https://web.archive.org/web/20130504064711/http://archive.msdn.microsoft.com/vhdtool/Release/ProjectReleases.aspx?ReleaseId=5344
    > 
    > 结果不能下载.
    > 
    > ### 4小时
    > 
    > 还找到了这个:
    > 
    > https://blog.workinghardinit.work/tag/vhd-tool/
    > 
    > 结果没有修复功能
    > 
    > 5小时:
    > 
    > 又上github
    > 
    > https://github.com/andreiw/vhdtool
    > 
    > 可惜根本不是我需要的哪个版本.只是同名而已
    > 
    > .
    > 
    > 6小时:
    > 
    > 最后终于找到了:
    > 
    > http://www.mediafire.com/download/f96bmsvjz4qdvbu/VhdTool.zip
    > 
    > 版本为2.0,大小为58K(gogo: vhdtool 2.0 )
    > 
    > ```
    > Create: Creates a new fixed format VHD of size <Size>.
    >         WARNING - this function is admin only and bypasses
    >         file system security.  The resulting VHD file will
    >         contain data which currently exists on the physical disk.
    > Convert: Converts an existing file to a fixed-format VHD.
    >          The existing file length, rounded up, will contain block data
    >          A VHD footer is appended to the current end of file.
    > Extend: Extends an existing fixed format VHD to a larger size <Size>.
    >         WARNING - this function is admin only and bypasses
    >         file system security.  The resulting VHD file will
    >         contain data which currently exists on the physical disk.
    > Repair: Repairs a broken Hyper-V snapshot chain where an administrator
    >         has expanded the size of the root VHD.  The base VHD will be
    >         returned to its original size. THIS MAY CAUSE DATA LOSS if the
    >         contents of the base VHD were changed after expansion.
    > ```
    > 
    > 然后 repair
    > 
    > 然后我还上传了百度盘,有需要的哪去,可惜没有找到源代码:
    > 
    > http://pan.baidu.com/s/1qY25NrQ
    > 
    > 由于我没有avhd(备份文件所以这个办法行不通)
    > 
    > 7 结果
    > 
    >     研究了好久,发现损坏的vhd可以用diskgenius打开,可以读出文件!  
    > 
    > 说明vhd只是ntfs系统不完整.
    > 
    > 其实只要chkdsk一下就可以了.但是chkdsk不支持虚拟磁盘!!![哭](http://static.blog.csdn.net/xheditor/xheditor_emot/default/cry.gif)
    > 
    > 猜想：
    > 
    > 还可以上终极大法! 
    > 
    > 安装virtualBox,把vhd文件当硬盘镜像!然后进入虚拟机chkdsk!  
    > 
    > 可惜它读取vhd不像虚拟光驱一样直接读取的,会报错.不能加载.
    > 
    > 还可以用hyper-v方式来处理,参考:
    > 
    > http://www.techieshelp.com/hyper-v-vhd-the-file-or-directory-is-corrupted-and-unreadable/
    > 
    > 8 另外的
    > 
    > 还有通过程序来解决
    > 
    > vb和C#/vbs都可以连接系统硬件挂载服务
    > 
    > 如下连接：
    > 
    > https://msdn.microsoft.com/zh-cn/library/cc136982(v=vs.85).aspx
    > 
    > 9 用脚本来解决
    > 
    > 比较方便的是用脚本来解决： （powsershell)
    > ```
    > $VHDName = "V:\serverx.vhd"
    > #Get the MSVM_ImageManagementService
    > $VHDService = get-wmiobject -class "Msvm_ImageManagementService" -namespace "root\virtualization" -computername "."
    > #Now we mount the VHD
    > $Result = $VHDService.Mount($VHDName)
    > 
    > chkdsk
    > ```
    > 
    > 只能在windows server 2008上这样操作.(要安装 hyper-V管理工具:关闭或打开windows功能 )
    > 
    > 注：windows sever 2008以后 namespace有v2  (win10上成功, win7 没有hyper-v管理工具)
    > 
    > 相应的命令要改成： `Get-WmiObject -computername "." -namespace "root\virtualization\v2" -class "Msvm_ImageManagementService"`
    > 
    > 还是万能的stackoverflow强大.
    > 
    > http://stackoverflow.com/questions/tagged/vhd
    > 
    > 10 回到起点
    > 
    > windows系统支持虚拟硬盘. 所以" 虚拟硬盘软件工具"很少,不像虚拟光驱一大把.
    > 
    > https://social.technet.microsoft.com/Forums/windowsserver/en-US/a08ad18f-4b6a-46a0-bd1f-274fbbc5b737/attach-a-vhd-in-windows-7
    > 
    > 用diskpart  attach abc.vhd
    > 
    > 然后 chkdsk
    > 
    > 


### Hyper-V .vhdx 格式磁盘镜像转换为VirtualBox可用的.vhd格式

- [Hyper-V .vhdx 格式磁盘镜像转换为VirtualBox可用的.vhd格式](https://gist.github.com/WesleyBlancoYuan/1f3236bf006f97161a2df31bd1e97190)

    > Hyper-V 默认创建 **.vhdx** 格式的虚拟磁盘。
    > 
    > 根据SuperUser上的这个问题：
    > http://superuser.com/questions/723381/how-to-open-vhdx-files-in-virtualbox
    > 
    > 尽管第三个答案指出，
    > 
    > > VirtualBox since 4.2 changelog says support added for VHDX "Storage: added readonly support for VHDX images".
    > 
    > 但这种格式在VirtualBox中是不支持的，要使用它建立新的镜像，会出现错误。具体信息为：
    > ```
    > Could not open the medium 'D:\desarrollo\Hyper-V\Ubuntu2\Virtual Hard Disks\Ubuntu2.vhdx'.
    > VD: error VERR_NOT_SUPPORTED opening image file 'D:\desarrollo\Hyper-V\Ubuntu2\Virtual Hard Disks\Ubuntu2.vhdx' (VERR_NOT_SUPPORTED).
    > 
    > 
    > Código Resultado: 
    > E_FAIL (0x80004005)
    > Componente: 
    > MediumWrap
    > Interfaz: 
    > IMedium {4afe423b-43e0-e9d0-82e8-ceb307940dda}
    > Receptor: 
    > IVirtualBox {0169423f-46b4-cde9-91af-1e9d5b6cd945}
    > Receptor RC: 
    > VBOX_E_OBJECT_NOT_FOUND (0x80BB0001)
    > ```
    > 
    > 根据搜索之后的信息，可以在启用Hyper-V后，使用PowerShell把.vmhk镜像转换为Virtualbox支持的VHD镜像。详情见以下答案： 
    > 
    > http://superuser.com/questions/751954/how-to-convert-a-vhdx-file-to-vhd#answer-751957
    > 
    > 具体操作步骤为：
    > 
    >  - Windows + R打开“运行”对话框，键入cmd，在command窗口中键入PowerShell来使用PowerShell窗口。或者直接打开PowerShell。
    >  - 在PS提示符后，使用以下命令：
    >     ```
    >     Convert-VHD –Path YOUR VHDX PATH –DestinationPath YOUR DESTINATION PATH
    >     ```
    >     例如：
    >     ```
    >     Convert-VHD -Path c:\myDisk\Ubuntu.vhdx -DestinationPath d:\Ubuntu_vhd.vhd
    >     ```
    >     注意两个路径都要带后缀。
    > 
    >  - 等待处理完成，用VirtualBox加载生成的镜像，完成。
    >  
    > 


## btrfs for windows

- [maharmstone/btrfs: WinBtrfs](https://github.com/maharmstone/btrfs)

    > -   How do I format a partition as Btrfs?
    > 
    > Use the included command line program mkbtrfs.exe. We can't add Btrfs to Windows' own dialog box, unfortunately, as its list of filesystems has been hardcoded. You can also run `format /fs:btrfs`, if you don't need to set any Btrfs-specific options.


### delete subvolume

- [How to delete subvolume? · Issue #50 · maharmstone/btrfs](https://github.com/maharmstone/btrfs/issues/50)

    > Unlike on Linux, you can delete subvolumes on Windows as if they were any other directory.

