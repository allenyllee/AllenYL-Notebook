# Linux__問題排解1-3_Networking

[toc]
<!-- toc --> 


# Network Interface

## Setup WiFi HotSpot

- [[Quick Tip] How to Create WiFi Hotspot in Ubuntu 18.04 LTS](https://www.debugpoint.com/2018/05/create-wifi-hotspot-ubuntu-android-support/)

    > Step1:
    > ------
    > 
    > Open Settings from application menu or from system menu as shown below.
    > 
    > [![Open Settings](https://www.debugpoint.com/blog/wp-content/uploads/2018/05/Open-Settings.png)](https://www.debugpoint.com/blog/wp-content/uploads/2018/05/Open-Settings.png)
    > 
    > Open Settings
    > 
    > Step 2:
    > -------
    > 
    > In the settings window left pane, click on WiFi.
    > 
    > At the top of the window, make sure WiFi is turned ON and then click more icon. From the context menu, click "Turn on WiFi hotspot".
    > 
    > [![Turn On WiFi Hotspot](https://www.debugpoint.com/blog/wp-content/uploads/2018/05/Turn-On-WiFi-Hotspot.png)](https://www.debugpoint.com/blog/wp-content/uploads/2018/05/Turn-On-WiFi-Hotspot.png)
    > 
    > Turn On WiFi Hotspot
    > 
    > Step 3:
    > -------
    > 
    > You will get a confirmation popup asking whether you want to turn it on. Click Turn On.
    > 
    > [![WiFi Turn On Confirmation](https://www.debugpoint.com/blog/wp-content/uploads/2018/05/WiFi-Turn-On-Confirmation.png)](https://www.debugpoint.com/blog/wp-content/uploads/2018/05/WiFi-Turn-On-Confirmation.png)
    > 
    > WiFi Turn On Confirmation
    > 
    > Step 4:
    > -------
    > 
    > WiFi hotspot is created and you can see the Network Name (i.e. Access Point Name) and the password which you can search from your smartphones, other devices and connect.
    > 
    > [![WiFi Turned On](https://www.debugpoint.com/blog/wp-content/uploads/2018/05/WiFi-Turned-On.png)](https://www.debugpoint.com/blog/wp-content/uploads/2018/05/WiFi-Turned-On.png)
    > 
    > WiFi Turned On
    > 
    > Step 5:
    > -------
    > 
    > That's it. You have created a hotspot from Ubuntu.
    > 
- [How to create and configure Wi-Fi Hotspot in Ubuntu 17.10 - FOSS Linux](https://www.fosslinux.com/2576/how-to-create-and-configure-wi-fi-hotspot-in-ubuntu-17-10.htm)

    > Configuring the Wi-Fi Hotspot in Ubuntu 17.10
    > ---------------------------------------------
    > 
    > In the Step (7) we noticed that the system automatically names the Hotspot name as PC name, but not everybody may want exactly that. Here is how you can change the SSID and password.
    > 
    > Step 1) With the Wireless Hotspot active, launch 'Terminal' and enter the following command:
    > 
    > nm-connection-editor
    > 
    > Step 2) In the "Network Connections", select the Wi-Fi name and click on the gear icon at the bottom.
    > 
    > ![Configuring the Connection](https://www.fosslinux.com/wp-content/uploads/2018/01/Workspace-1_036.jpg)
    > 
    > Configuring the Connection
    > 
    > Step 3) Go ahead and change the Hotspot connection parameters including SSID, Password, etc. as desired.
    > 
    > ![Changing Wi-Fi Hotspot Name, Password, and Other Parameters](https://www.fosslinux.com/wp-content/uploads/2018/01/Workspace-1_037.jpg)
    > 


- [networking - Unwanted automatic connection to hotspot - Ask Ubuntu](https://askubuntu.com/questions/896437/unwanted-automatic-connection-to-hotspot)

    > You should be able to delete the MyHotspot from Edit Connections. However, you can also disable the autoconnect by editing the MyHotspot profile, and unchecking the "Automatically connect to this network when it is available".
    > 
    > [![enter image description here](https://i.stack.imgur.com/1jfyt.png)](https://i.stack.imgur.com/1jfyt.png)

## connecting wifi on boot and available to all users

- [autostart - Start ssh server on boot - Ask Ubuntu](https://askubuntu.com/questions/3913/start-ssh-server-on-boot)

    > I think you should right click on the connection icon, select Edit Connections, click on the Wireless tab, double-click your wireless connection and mark both "Connect automatically" and "available to all users". That means your connection will be up and running without logging in graphically. -- [Leon Nardella](https://askubuntu.com/users/1546/leon-nardella "1,490 reputation") [Sep 9 '10 at 13:56](https://askubuntu.com/questions/3913/start-ssh-server-on-boot#comment3915_3913)

- [command line - stay connected to wifi when all users log out - Ask Ubuntu](https://askubuntu.com/questions/1064959/stay-connected-to-wifi-when-all-users-log-out)

    > Edit your preferred connection and check:
    > 
    > -   Automatically connect to this network
    > -   Available to all users
    > 
    > Also give a high priority number for auto-activation (More than all other connections).
    > 
    > Make sure your wifi gets enabled at boot time (otherwise you have to login and enable it).
    > 
    > Now this connection will be activated before login and stay connected after logout.
    > 
    > ### Using CLI and `nmcli`:
    > 
    > ```
    > nmcli connection modify [CONNECTION-NAME] connection.permissions ''
    > nmcli connection modify [CONNECTION-NAME] connection.autoconnect yes
    > nmcli connection modify [CONNECTION-NAME] connection.autoconnect-priority 10
    > 
    > ```
    > 
    > ### Using GUI:
    > 
    > [![enter image description here](https://i.stack.imgur.com/Jn9et.png)](https://i.stack.imgur.com/Jn9et.png)


## Command-line to list DNS servers

- [Command-line to list DNS servers used by my system - Ask Ubuntu](https://askubuntu.com/questions/152593/command-line-to-list-dns-servers-used-by-my-system)

    > resolv.conf isn't really used anymore, unless you implement it yourself. The network manager does it now. I created an alias to list the DNS servers on my system, as I sometimes switch from OpenDNS to Google's open DNS.
    > 
    > **Ubuntu >= 15**
    > 
    > ```sh
    > nmcli device show < interfacename> | grep IP4.DNS
    > 
    > ```
    > 
    > **Ubuntu <= 14**
    > 
    > ```sh
    > nmcli dev list iface < interfacename> | grep IP4
    > 
    > ```
    > 
    > In my case, `<interfacename>` is `eth0`, which is common, but not always the case.
    > 
    > See if this is what you want.
    > 
    > EDIT:
    > 
    > I think resolv.conf is actually used indirectly, because the network manager creates the server that listens on 127.0.0.1, but I was told that this is an implementation detail that should not be counted on. I think that if you enter DNS addresses before this entry, they might get used, but I'm not sure exactly how this works. I think it's best to use the network manager in most cases, when possible.
    > 
    > ---
    > 
    > nmcli version 0.9.10
    > 
    > You can use either of these commands:
    > ```sh
    > nmcli -t -f IP4.DNS device show eth0
    > IP4.DNS[1]:192.168.1.1
    > IP4.DNS[2]:8.8.8.8
    > 
    > nmcli -t -f IP4.DNS connection show conn-name
    > IP4.DNS[1]:192.168.1.1
    > IP4.DNS[2]:8.8.8.8
    > ```



## where are network-manager's config files

- [[ubuntu] where are network-manager's config files?](https://ubuntuforums.org/showthread.php?t=1480826)
    > ```
    > /etc/NetworkManager/system-connections
    > ```


## manage DNS in NetworkManager via console (nmcli)

- [networking - How to manage DNS in NetworkManager via console (nmcli)? - Server Fault](https://serverfault.com/questions/810636/how-to-manage-dns-in-networkmanager-via-console-nmcli)

    > [Useful nmcli manual](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/sec-Using_the_NetworkManager_Command_Line_Tool_nmcli.html)
    > 
    > here is the syntax to modify an existing connection.
    > 
    > ```sh
    > nmcli con mod < connectionName> ipv4.dns "8.8.8.8 8.8.4.4"
    > 
    > ```
    > 
    > `connectionName` can be found by command: `nmcli con`.\
    > In the question case, it will be `"System eth0"`
    > 
    > you should not really edit /etc/resolv.conf manually as it is generated by NetworkManager service.
    > 
    > ---
    > 
    > ```sh
    > nmcli dev mod "$interface" ipv4.dns "$DNS_IP"
    > ```
    > [name=Ya-Lun Li]

- [14.04 - How to Change DNS of network from Terminal? - Ask Ubuntu](https://askubuntu.com/questions/721080/how-to-change-dns-of-network-from-terminal)

    > `nmcli connection show --active` to obtain active connection name\
    > `nmcli connection edit` *double tab to list available connections and chose appropriate*
    > 
    > > ```
    > >    nmcli> remove ipv4.dns
    > >    nmcli> set ipv4.ignore-auto-dns yes
    > >    nmcli> set ipv4.dns 8.8.8.8 8.8.4.4 (or other dns servers)
    > >    nmcli> save
    > >    nmcli> quit
    > >
    > > ```
    > 
    > `nmcli connection down` *your_connection_name*\
    > `nmcli connection up` *your_connection_name*
    > 
    > ---
    > 
    > Careful with nmcli connection down, if you are on a remote ssh session you can lose connection to the node!! I think is better to call /etc/init.d/network restart -- [Carlos Verdes](https://askubuntu.com/users/526802/carlos-verdes "101 reputation") [Jun 12 at 7:03](https://askubuntu.com/questions/721080/how-to-change-dns-of-network-from-terminal#comment1705700_721107)





# samba

## Mount a samba network drive from terminal

- [networking - Mount a samba network drive from terminal without hardcoding a password - Ask Ubuntu](https://askubuntu.com/questions/725440/mount-a-samba-network-drive-from-terminal-without-hardcoding-a-password)

    > Use the `mount.cifs` command instead, as it allows to specify a credentials file or prompts for a password if none given.
    > 
    > **Installation**
    > 
    > First of all, check you have the needed packages installed by issuing the following command:
    > 
    > ```
    > sudo apt-get install cifs-utils
    > 
    > ```
    > 
    > **METHOD 1 - USING A CREDENTIALS FILE**
    > 
    > According to the manual <http://manpages.ubuntu.com/manpages/raring/man8/mount.cifs.8.html> :
    > 
    > > OPTIONS\
    > > [...]\
    > > credentials=filename specifies a file that contains a username and/or password and optionally the name of the workgroup. The format of the file is:
    > >
    > > username=value\
    > > password=value\
    > > domain=value
    > 
    > Usage:
    > 
    > ```
    > mount.cifs //<hostname_or_ip>/<cifs_share> <local_mountpoint> -o user=<user_to_connect_as>,rw,credentials=<path_to_the_credentials_file>
    > 
    > ```
    > 
    > Example:
    > 
    > ```
    > sudo mount.cifs //domain.com/share /mnt/domain_com -o user=admin,rw,credentials=/root/.credentials
    > 
    > ```
    > 
    > It's important to note that the "name_of_the_user_to_connnect_as" can contain also the domain or the workgroup:
    > 
    > ```
    > user=workgroup/user
    > user=domain/user
    > 
    > ```
    > 
    > (Depending on you environment, you will need more or less options)
    > 
    > Regarding security, it should be enough to store the credentials file in the /root directory, but if you want to store it elsewhere, just
    > 
    > -   set the root user as its owner with `sudo chown root <file>`
    > -   set owner-only permissions with `sudo chmod 600
    > 
    > **METHOD 2 - PASSWORD PROMPT**
    > 
    > If as stated, you don't want your password to be visible at all, then just don't provide the "password" option in your `mount.cifs` command.
    > 
    > From the manpage at <http://manpages.ubuntu.com/manpages/hardy/man8/mount.cifs.8.html>
    > 
    > > password=arg
    > >
    > > ```
    > >       specifies  the  CIFS  password. If this option is not given then the
    > >       environment  variable  PASSWD  is  used.  If  the  password  is  not
    > >       specified directly or indirectly via an argument to mount mount.cifs
    > >       will prompt for a password, unless the guest option is specified.
    > >
    > >       Note that a password which contains the delimiter character (i.e.  a
    > >       comma  ',')  will  fail  to be parsed correctly on the command line.
    > >       However,  the  same  password  defined  in  the  PASSWD  environment
    > >       variable  or  via  a  credentials file (see below) or entered at the
    > >       password prompt will be read correctly.
    > >
    > > ```
    > 
    > Accordingly, the following command should prompt for a password:
    > 
    > ```
    > mount.cifs //<hostname_or_ip>/<cifs_share> <local_mountpoint> -o user=<user_to_connect_as>,rw
    > 
    > ```
    > 
    > Tested and working as expected:
    > 
    > [![enter image description here](https://i.stack.imgur.com/zW2x3.png)](https://i.stack.imgur.com/zW2x3.png)
    > 

### cannot create regular file

- [[ubuntu] smbmount - cannot create regular file](https://ubuntuforums.org/showthread.php?t=1127809)

    > Try something like this instead.
    > 
    > ```shell
    > //smbserver/myshare /home/tux/mnt/myshare cifs rw,username=andreas,uid=1000,gid=1000,nounix,rsize=16384,wsize=57344 0 0
    > ```
    > 
    > See man mount and man mount.cifs for more information.
    > 
    > The problem is that you need to disable unix style permissions handling over CIFS because CIFS can't pass them correctly (remember, this is Windows file sharing, not Linux).


## unable to connect to Windows 10 share

- [[SOLVED] unable to connect to Windows 10 share from Ubuntu](https://ubuntuforums.org/showthread.php?t=2293172)

    > In my desktop-pc I have a MS-account (outlook account) like main user: <MyAccout@outlook.com>. My "Domain" is DESK001_PC and my work group is "WORKGROUP" as default.\
    > At first time I tried:
    > ```
    > user: <myaccount@outlook.com>\
    > domain: DESK001_PC\
    > pass: *******
    > ```
    > 
    > But It didn't work. Then at second time I tried:
    > ```
    > user: <myaccount@outlook.com>\
    > domain: WORKGROUP\
    > pass: *******
    > ```
    > 
    > And It didn't work again. So I looked in my laptop (in windows 10 partition) that when I connected to my Desktop, using <myaccout@outlook.com> / ******* It works and IT SAID (DOMAIN OUTLOOK.COM). It looked so stupid but I said to myself; I've got nothing to lose.
    > 
    > At third time I tried:
    > ```
    > user: <myaccount@outlook.com>\
    > domain: outlook.com\
    > pass: *******
    > ```
    > 
    > And IT WORKED PERFECT!


## Stopping and Starting the Samba Daemons

- [Stopping and Starting the Samba Daemons](http://www.linuceum.com/Server/srvSambaDaemons.php)

    > ### Checking if the Samba Daemons are Running
    > 
    > **Samba** runs a couple of processes in the background: notably the **Samba** and **NetBIOS** daemons.
    > 
    > You can check to see if the Samba daemon (**smbd**) is running using the [ps](http://www.linuceum.com/Desktop/Processes.php) command:
    > ```sh
    > $ ps -ef | grep smbd
    > root      3869     1  0 16:41 ?        00:00:00 smbd -F
    > root      3881  3869  0 16:41 ?        00:00:00 smbd -F
    > fredb     3944  3052  0 16:47 pts/0    00:00:00 grep --color=auto smbd
    > $
    > ```
    > 
    > You can also check to see if the **NetBIOS** **name server** daemon (**nmbd**) is running using the ps command:
    > ```sh
    > $ ps -ef | grep nmbd
    > root      1964     1  0 08:59 ?        00:00:00 nmbd -D
    > fredb     8076  4453  0 18:09 pts/0    00:00:00 grep --color=auto nmbd
    > $
    > ```
    > 
    > If any process (-apart from the grep command itself) is returned, then the process is running.
    > 
    > * * * * *
    > 
    > ### Stopping the Samba Daemons
    > 
    > If you need to stop the smbd or nmbd daemon, you can use the following commands:
    > ```sh
    > $ sudo service smbd stop
    > $ sudo service nmbd stop
    > ```
    > 
    > If you need to forcibly stop the smbd or nmbd daemon, you can use the following command (-you'll need to give them some time to shut down):
    > ```sh
    > sudo kill -15 <smbd PID\>
    > sudo kill -15 <nmbd PID\>
    > ```
    > 
    > Note: only use sudo kill -9 as a last resort - as this may leave shared memory in an inconsistent state
    > 
    > * * * * *
    > 
    > ### Starting the Samba Daemons
    > 
    > If you need to start the smbd or nmbd daemon, you can use the following commands:
    > ```sh
    > $ sudo service smbd start
    > $ sudo service nmbd start
    > ```
    > Note: there is also a restart option if you need to restart the daemon after changing the **Samba** configuration files!

## CIFS-over-SSH

- [CIFS-over-SSH for Windows 7](https://www.nikhef.nl/~janjust/CifsOverSSH/Win7Loopback.html)


    > 
    > Introduction
    > ------------
    > 
    > This tutorial is for Windows 7 but contains mostly screenshots from the English version of Windows Vista. Separate instructions for other versions of Windows are also available:
    > 
    > -   [Windows Vista](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaLoopback.html).
    > -   [Windows 8](https://www.nikhef.nl/~janjust/CifsOverSSH/Win8Loopback.html).
    > -   [Windows 10](https://www.nikhef.nl/~janjust/CifsOverSSH/Win10Loopback.html).
    > 
    > The instructions for Windows 2000/XP are also still [available](https://www.nikhef.nl/~janjust/CifsOverSSH/Howto_Loopback.html).\
    > To be able to mount a Windows share over SSH we will need
    > 
    > -   Administrator access to the local computer, including the ability to *elevate* privileges. If you don't know what I am talking about then stop reading right here.
    > -   [PuTTY v0.58+](http://www.chiark.greenend.org.uk/~sgtatham/putty/), which is an excellent and free implementation of SSH for Windows. It is assumed that you are familiar with the PuTTY user interface.
    > -   One real or virtual network adapter, bound to the *Client for Microsoft Networks* driver.\
    >     Normally you should already have such an adapter, as otherwise you would not be able to mount any Windows shares.
    > -   One real or virtual network adapter, **NOT** bound to the *Client for Microsoft Networks* driver.
    > 
    > This part of the tutorial is split into the following steps:
    > 
    > 1.  As most people do not have a spare real network adapter in their computer, we will add an extra virtual network adapter by [installing](https://www.nikhef.nl/~janjust/CifsOverSSH/Win7Loopback.html#Install) the **Microsoft Loopback Adapter**.
    > 2.  After that, the network adapter must be properly [configured](https://www.nikhef.nl/~janjust/CifsOverSSH/Win7Loopback.html#ConfigureAdapter).
    > 3.  Furthermore, a Windows system driver needs to be [tweaked](https://www.nikhef.nl/~janjust/CifsOverSSH/Win7Loopback.html#ConfigureConsole).
    > 4.  Next, reboot Windows to [verify](https://www.nikhef.nl/~janjust/CifsOverSSH/Win7Loopback.html#Verify) that we've been able to grab port 445 and to see if the `smb` and `lanmanserver` drivers are up and running.
    > 5.  If the port was grabbed, but the drivers are not running, then create a task using the [Windows Task Scheduler](https://www.nikhef.nl/~janjust/CifsOverSSH/WinAddTask.html) to start the drivers.
    > 6.  Next, we set up a special [PuTTY](https://www.nikhef.nl/~janjust/CifsOverSSH/Win7Loopback.html#ConfigurePuTTY) session with the right port-forwarding.
    > 7.  Finally, we start PuTTY and [mount](https://www.nikhef.nl/~janjust/CifsOverSSH/Win7Loopback.html#MountHome) our Nikhef home directory.
    > 
    > 9.  For those wishing to [undo](https://www.nikhef.nl/~janjust/CifsOverSSH/Win7Loopback.html#Undo) the above steps follow the instructions at the bottom of this tutorial.
    > 
    > Installing the Loopback Adapter
    > -------------------------------
    > 
    > To install the Loopback adapter follow these steps:
    > 
    > -   Start the **Add Hardware Wizard** by either going **Start->Settings->Control Panel->Add Hardware** or by starting a console window with elevated (Administrator) privileges. In the console window type
    >     ```
    >     hdwwiz.exe
    >     ```
    >     
    >     The Hardware Wizard will come up:\
    >     ![wizardStart](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaAddHWwiz1.png)
    > -   Click **Next** to continue:\
    >     ![manualSelect](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaAddHWwiz2.png)\
    >     Select **Install the hardware that I manually select from a list** and click **Next**.
    > -   Now you'll see:\
    >     ![networkAdapters](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaAddHWwiz3.png)\
    >     Select the entry **Network adapters** and click **Next**.
    > -   In the next screen\
    >     ![msLoopback](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaAddHWwiz4.png)\
    >     first select **Microsoft** from the list of *Manufacturers* and then select **Microsoft Loopback Adapter** from the list of *Network Adapters*. Finally, click **Next** once more.
    > -   Almost finished:\
    >     ![readyToInstall](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaAddHWwiz5.png)\
    >     This is your last chance to abort, otherwise, click **Next**.
    > -   After a while you should see:\
    >     ![finished](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaAddHWwiz6.png)\
    >     Click **Finish** to exit the Hardware Wizard.
    > 
    > You are now ready to configure your newly installed Loopback adapter. Even though Windows might not ask you to, reboot anyways (heey, it's a Microsoft OS ;-)).\
    > From reports I've seen on the Internet a reboot is sometimes required for the loopback adapter to come up properly.
    > 
    > Configuring the Loopback Adapter
    > --------------------------------
    > 
    > Now that your newly installed loopback adapter is up and running we must configure it properly:
    > 
    > -   Go to the **Network Connections Center**:\
    >     ![NetworkConnections](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaNetworkConns.png)
    > 
    > -   Choose the loopback adapter (usually it is named "Local Area Connection #3") and right-click on it.
    > -   Choose **Properties**, after which a new window will appear\
    >     ![loopProperties](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaLoopPropertiesGeneral.png)\
    >     Make sure that
    >     -   the entry **Client for Microsoft Networks** is **NOT** enabled, i.e. does not have a checkmark in front of it.
    >     -   the entry **File and Printer sharing for Microsoft Networks** is **NOT** enabled, i.e. does not have a checkmark in front of it.
    >     -   the entry **Internet Protocol (TCP/IP)** is enabled.
    > -   Select the entry **Internet Protocol (TCP/IP)**, then click on **Properties**.
    > -   A new window will appear:\
    >     ![loopPropertiesTCPIP](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaLoopPropertiesTCPIP.png)\
    >     Select **Use the following IP address** and fill in the 'IP address' and 'Subnet mask' as above.\
    >     It is not necessary to fill in the 'Default gateway' or a 'DNS server'.
    > -   Click on **Advanced** to make the following window appear:\
    >     ![loopPropertiesTCPIPAdv](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaLoopPropertiesTCPIPAdv.png)\
    >     Deselect **Automatic metric** and fill in the value of **9999** as the 'Interface metric' as shown above.
    > -   Click on the **WINS** tab:\
    >     ![loopPropertiesWINS](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaLoopPropertiesWINS.png)\
    >     and select **Disable NetBIOS over TCP/IP**.
    > -   Click on **OK**.
    > -   You are now back in the main 'TCP/IP Properties' screen. Click **OK** again.
    > -   You are now back in the main 'Loopback Properties' screen. Click **Close**.
    > 
    > Tweaking the 'SMB' driver
    > -------------------------
    > 
    > Now we first need to tweak a Windows system driver to overcome the thing that Microsoft broke. The root cause of the problem is that we need to access the file share using TCP port **445**. However, when Windows Vista or 7 boots this port is grabbed by the system `smb` driver for all interfaces. By delaying the startup of the `smb` driver and by installing a `portproxy` rule we can circumvent this. This section explains how to do this:
    > 
    > -   Start a console window with elevated (Administrator) privileges.
    > -   First, we disable the automatic starting of the `smb` driver:
    >     ```
    >     sc config smb start= demand
    >     ```
    > 
    >     **NOTE** the space after the `start=` !
    > -   Next we add a `portproxy` rule to reroute TCP port 445 to a port of our choosing. For this tutorial, I choose **44445**:
    >     ```
    >     netsh interface portproxy add v4tov4 listenaddress=10.255.255.1 listenport=445 connectaddress=10.255.255.1 connectport=44445
    >     ```
    >     
    >     **IMPORTANT NOTES**:
    >     -   The `listenaddress` is the address of the Loopback adapter configured in the section earlier
    >     -   The `connectaddress` must be identical to the `listenaddress`
    >     -   Using `listenaddress=127.0.0.1` does not work. Believe me, I've tried.
    > 
    > If all went well you should see something like\
    > ![ConfigureConsole](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaConsole.png)\
    > The `portproxy` rule is persistent, so there should be no need to repeat this step after a reboot.-   Alex Tymick reported that for Windows 64bit SP1 a different service needs to be reconfigured:
    >     ```
    >     sc config FDResPub start= demand
    >     ```
    >     
    > I have not been able to confirm this, but if disabling automatic startup of the `smb` driver does not work then it's worth trying this one.
    > 
    > Reboot and verify
    > -----------------
    > 
    > **Note** I've verified this tutorial on multiple Windows 7 Professional installations, patched fully at the date of writing (March 1st, 2018), and the above instructions were sufficient to grab TCP port 445 **and** to get the 'smb' and 'lanmanserver' drivers in a running state.
    > 
    > Of course, now that we have disabled the automatic startup of the 'SMB' driver we have to reboot Windows before proceeding.
    > -   Verify that the `portproxy` was applied successfully by checking the open ports on the system. Type in the command console
    >     ```
    >     netstat -an | find ":445 "
    >     ```
    >     
    >     You should see something like
    >     ```
    >     TCP    10.255.255.1:445    0.0.0.0:0       LISTENING
    >     ```
    > 
    >     If you see '`0.0.0.0:445`' instead then the 'portproxy' rule was not applied correctly.
    >     
    > -   After Windows comes up and you have logged in, check the status of the 'SMB' driver. Open a command console (no privilege elevation is required) and type
    >     ```
    >     sc query smb
    >     sc query lanmanserver
    >     ```
    >    
    >     The 'SMB' and 'LanmanServer' drivers should be in the state **Running**. If they are not, then follow [these steps](https://www.nikhef.nl/~janjust/CifsOverSSH/WinAddTask.html) to create a task using the Task Schedule to start them at system startup.This also shows the downside of the `portproxy` method: it is no longer possible to use local shares on the computer while this rule is active.
    > 
    > Configuring PuTTY
    > -----------------
    > 
    > Set up a special PuTTY session with the appropriate `port-forwarding`:
    > 
    > -   Start PuTTY and create a new session or load your existing session for logging in on `login.nikhef.nl`. Choose host **login2.nikhef.nl** and protocol **SSH**.
    > 
    > -   Expand the **Connection->SSH** menu option in the *Category* tree-list and select **Tunnels**.
    > 
    > -   Add a new forwarded port:
    >     ![puttyLoopTunnels1](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaPuTTYConfigLoopTunnels1.png)
    > 
    > -   For the **Source port**, fill in the *IP address* of your loopback adapter, plus the port **44445** (**NOT** 445!). The entry field might seem to small for it, but it will work. If you have configured your loopback adapter exactly as in the previous section, then fill in **10.255.255.1:44445**.
    >             
    > -   For the **Destination**, fill in **beuk.nikhef.nl:445**.
    > 
    > -   Click on **Add**.
    > 
    > -   You should now see:\
    >     ![puttyLoopTunnels2](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaPuTTYConfigLoopTunnels2.png)
    >     
    > -   In the *Category* tree-list on the left, scroll back up and choose **Session** again. Save your session.
    > 
    > Putting it all together
    > -----------------------
    > 
    > Now that we have configured both our loopback adapter and PuTTY we can put it all together and mount our Nikhef home directory as a Windows share:
    > -   Start your newly created Nikhef-PuTTY session and login on `login2.nikhef.nl` as normal.
    > 
    > -   Make sure port-forwarding is working properly by checking the PuTTY event log. Select the Window menu of the PuTTY screen (top left) and select **Event log**. You should see a log similar to:
    >     ![puttyEventLog](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaPuTTYEventLog.png)\
    >     If not, then check your PuTTY session options first.
    > 
    > -   Go to **Start->Run** and type **\\10.255.255.1\user\<Your-nikhef-userid>**
    > 
    > -   You will be prompted to authenticate yourself:
    >     ![networkLogin](https://www.nikhef.nl/~janjust/CifsOverSSH/VistaLoopLogin.png)\
    >     For the *Username*, fill in the domain **NIKHEF\** followed by your Nikhef-Windows userid.\
    >     For the *Password*, fill in your Nikhef-Windows password, which might be different from the password you use to log in on `login2.nikhef.nl` and press **OK**.
    >     
    > -   You should now see your Nikhef home directory in Windows Explorer!
    > 
    > *Congratulations!*
    > 
    > #### Mapping a network drive
    > 
    > To make life even easier it might be handy to map a network drive to your Nikhef home directory:
    > -   Start Windows Explorer and choose **Tools->Map Network Drive**.
    > -   In the next screen, fill in:\
    >     ![Win7MapNetworkDrive](https://www.nikhef.nl/~janjust/CifsOverSSH/Win7MapNetworkDrive.png)
    >     
    > -   Choose an available drive letter.
    > 
    > -   Do **NOT** click on *Browse* but type in as the *Folder* name: **\\10.255.255.1\user\<Your-nikhef-userid>**
    > 
    > -   Enable the checkbox in front of **Connect using different credentials**.
    > 
    > -   Now click on **Finish**.
    > 
    > -   In the next screen, fill in your Nikhef-Windows userid:
    >     ![Win7NetworkCreds](https://www.nikhef.nl/~janjust/CifsOverSSH/Win7NetworkCreds)
    >     For the *User name*, fill in the domain **NIKHEF** followed by your Nikhef-Windows userid.
    >     For the *Password*, fill in your Nikhef-Windows password, which might be different from the password you use to log in on `login.nikhef.nl` and press **OK**.
    >     
    > -   In the next screen, click on **Finish** to complete the network drive mapping.
    > 
    > -   You should now see a new drive letter appear in the *Folders* tree-list in Windows Explorer. Click on it to verify that you are indeed viewing your Nikhef home directory.
    > 
    > 
    > Control+Z! Undo! Undo!
    > ----------------------
    > 
    > For those wishing to undo the CIFS-over-SSH trick follow these steps:
    > 1.  Start a console window with elevated (Administrator) privileges.
    > 2.  Restore the automatic startup of the `smb` driver by typing
    >     ```
    >     sc config smb start= auto
    >     ```
    >     **NOTE** the space after the `start=` !
    > 3.  Remove the `portproxy` rule by typing
    >     ```
    >     netsh interface portproxy delete v4tov4 listenaddress=10.255.255.1 listenport=445
    >     ```
    >     
    > 4.  Start a `Device Manager` by typing
    >     ```
    >     devmgmt.msc
    >     ```
    >     Expand the 'Network Adapters', right-click on **Loopback adapter** and select **Uninstall**.
    > 5.  If necessary, use the 'Task Scheduler' from the 'Administrative Tasks' menu to delete the task 'Start SMB driver'
    > 
    > *That's all, folks!*
    > 
    > * * * * *
    > 
    > Comments to [Jan Just Keijser](mailto:janjust@nikhef.nl) | lastmod = 20/03/2018 11:46| visitors = 301
    
    

# ssh

## ssh tunnel

- [資訊安全 - SSH Tunnel 帶你遨遊 :: 哇哇3C日誌](https://ez3c.tw/907)

    > 朋友困難:
    > 1.似乎只有開放destination為80的連線
    > 2.無法到Yahoo及Google的webmail
    > 3.不能連上MSN
    > 
    > 
    > 真是不知道朋友找我是找對人還是找錯人啊??但是還是幫他試試看囉，需求一台暴露在網路上的主機可以ssh登入，我是以CentOS4.0(A伺服器)來做實驗，該主機有apache服務，因此我總不能把ssh的service port改成80吧。在此狀況之下，要求朋友在公司時利用[whatismyip](http://www.whatismyip.com/)一站查出公司對外連線所帶的IP(為11.12.13.14~16五個IP，虛構)，我來幫他做轉port的動作。在A伺服器的設定(ssh service port 2222，私有192.168.1.80) 設定來源為11.12.13.14~16，目的為service port 80轉向到service port 2222
    > ```
    > iptables -t nat -A PREROUTING -s 11.12.13.14 -d 192.168.1.80 -p tcp -m tcp --dport 80 -j REDIRECT --to-ports 2222
    > iptables -t nat -A PREROUTING -s 11.12.13.15 -d 192.168.1.80 -p tcp -m tcp --dport 80 -j REDIRECT --to-ports 2222
    > iptables -t nat -A PREROUTING -s 11.12.13.16 -d 192.168.1.80 -p tcp -m tcp --dport 80 -j REDIRECT --to-ports 2222
    > ```
    > 開啟ip_forward
    > ```
    > sysctl -w net.ipv4.ip_forward=1
    > ```
    > 主動對外連線都要開
    > ```
    > iptables -P OUTPUT ACCEPT
    > ```
    > 
    > A伺服器的部分設定完成囉，接下來就是朋友電腦pietty的設定囉
    > 1.當然是建立一個連線囉，destination port是80唷!!
    > ![](http://farm1.static.flickr.com/229/514499772_e0230ad2f5_o.gif)
    > 
    > 2.此部分是要透過網域連線的部分，走http的連線出去唷，proxy的設定就取決於環境囉，後面再Key入domain的帳號密碼
    > ![](http://farm1.static.flickr.com/203/514526909_4dbb058bd7_o.gif)
    > 
    > 3.接下來是設定也很重要的tunnel部分，source port隨意，這是要給localhost listen的，
    > type選擇dynamic，，之後點選Add，之後就給他連過去吧~要能登入算正常唷
    > ![](http://farm1.static.flickr.com/237/514499842_d298194d18_o.gif)
    > 
    > 再來設定朋友的FireFox瀏覽器
    > [#M_ more..
    > 再來設定朋友的FireFox瀏覽器
    > [#M_ more.. | less.. |1.開啟選項->連接->網路->設定![](http://farm1.static.flickr.com/217/514527195_a905559d06_o.gif)
    > 
    > 2.填入剛剛所設定的tunnel，方式是利用SOCKS 5，連線是先到localhost的8080 port，
    > ，localhost此時應該早已與A伺服器連線，連到localhost的8080 port的東西都會經過此條加密tunnel到A伺服器哩
    > ![](http://farm1.static.flickr.com/217/514527643_12d1728f95_o.gif)
    > 
    > 3.設定完成應該就可以上網囉，利用currport檢測一下，的確是網本機走沒錯唷
    > [![](http://farm1.static.flickr.com/234/514500044_70177262f5_m.jpg)](http://farm1.static.flickr.com/234/514500044_8729045eb3_o.gif)
    > 
    > 4.再利用上面說到[whatismyip](http://www.whatismyip.com/)檢測自己的IP，此時應該要是A伺服器的對外IP唷!!_M#]
    > 最後設定大多公司都違法的MSM
    > [#M_ more.. | less.. |1.設定MSN，工具->選項->連線->進階設定
    > ![](http://farm1.static.flickr.com/189/514500498_6e37cd0a93_o.gif)
    > 
    > 2.與FireFox一樣選擇SOCKS的方式連線，原理相同
    > ![](http://farm1.static.flickr.com/215/514527705_c437d16bc8_o.gif)
    > 
    > 3.馬上來測試，搞定囉。其實在本機安裝messenger就露餡哩啦，人家都管制哩還安裝就太白目哩，透過web messenger偷偷上就好哩啊
    > ![](http://farm1.static.flickr.com/210/514527747_774c93aa11_o.gif)
    > 
    > 


### forward multiple ports

- [ssh -L forward multiple ports - Stack Overflow](https://stackoverflow.com/questions/29936948/ssh-l-forward-multiple-ports)

    > Exactly what [NaN](https://stackoverflow.com/users/3751845/nan) answered, you specify multiple -L arguments. I do this all the time. Here is an example of multi port forwarding:
    > 
    > ```sh
    > ssh remote-host -L 8822:REMOTE_IP_1:22 -L 9922:REMOTE_IP_2:22
    > 
    > ```



## reverse ssh tunnel

### How does reverse SSH tunneling work?

- [networking - How does reverse SSH tunneling work? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/46235/how-does-reverse-ssh-tunneling-work)

- [ssh(1) - OpenBSD manual pages](https://man.openbsd.org/ssh)


    > > [`-R`](https://man.openbsd.org/ssh#R) [*bind_address*:]*port*:*host*:*hostport*
    > > 
    > > [`-R`](https://man.openbsd.org/ssh#R_2) [*bind_address*:]*port*:*local_socket*
    > > 
    > > [`-R`](https://man.openbsd.org/ssh#R_3) *remote_socket*:*host*:*hostport*
    > > 
    > > [`-R`](https://man.openbsd.org/ssh#R_4) *remote_socket*:*local_socket*
    > > 
    > > [`-R`](https://man.openbsd.org/ssh#R_5) [*bind_address*:]*port*
    > 
    > 
    > By default, TCP listening sockets on the server will be bound to the loopback interface only. This may be overridden by specifying a *bind_address*. An empty *bind_address*, or the address '`*`', indicates that the remote socket should listen on all interfaces. Specifying a remote *bind_address* will only succeed if the server's `GatewayPorts` option is enabled (see [sshd_config(5)](https://man.openbsd.org/sshd_config.5 "Xr")).
    > 
    > If the *port* argument is '`0`', the listen port will be dynamically allocated on the server and reported to the client at run time. When used together with `-O forward` the allocated port will be printed to the standard output.
    > 

- [玩具烏托邦: 鑿一個反向 ssh 隧道， 對朋友或世界展示筆電或家裡的某個服務](https://newtoypia.blogspot.com/2016/08/reverse-ssh-tunneling.html)

    > ![](https://ckhung.github.io/a/m/16/ssh-tunnel.svg)

    > 1.  在筆電上安裝 apache2 網頁伺服器。
    > 2.  在 /var/www/html/index.html 裡面打一些字。
    > 3.  用 `lynx http://localhost/` 指令確認伺服器架設成功。
    > 4.  在桌機 (假設 IP 是 192.168.34.56) 上安裝 openssh-server、 在 /etc/ssh/sshd_config 裡面加上 `GatewayPorts clientspecified`、 用 `service ssh restart` 重新啟動 ssh 服務。
    > 5.  在桌機上執行 `lynx http://localhost:4380/` 當然會連線失敗。
    > 6.  在筆電上鑿反向 ssh 隧道： `ssh -fNR 4380:localhost:80 192.168.34.56`
    > 7.  在桌機上再次執行 `lynx http://localhost:4380/` 看見筆電的網頁!
    > 8.  從筆電看 `lynx http://192.168.34.56:4380/` 連線失敗。
    > 9.  在筆電上用 `ps ax | grep 'ssh.*:.*:'` 以及工人智慧 (肉眼) 找出先前鑿通的隧道並且用 kill 把它砍掉， 或是用這個指令直接砍掉 「本機上目前已鑿通的所有隧道」： `kill $(ps ax | perl -ne 'print "$1\n" if (/(\d+).*\d\s+ssh.*:.*:/)')`
    > 10. 重鑿一個 「對全世界開放」 的隧道： `ssh -fNR *:4380:localhost:80 192.168.34.56`
    > 11. 在筆電上再次執行 `lynx http://192.168.34.56:4380/` 成功!
    > 

- [Reverse SSH Tunnel 反向打洞實錄](https://fred-zone.blogspot.com/2010/08/reverse-ssh-tunnel.html)

    > ```
    > # 首先，在客戶那理的機器下指令連回我們自己的 Server，並設定自己 Server 上的 12345 port 會對應到幾器上的 SSH port
    > ssh -NfR 12345:localhost:22 fred@myhost.com
    > 
    > # 然後在 myhost 的機器上連自己的 12345 port，就可以連回在客戶那的機器
    > ssh localhost -p 12345
    > ```

- [What is Reverse SSH Port Forwarding - The Devolutions Blog](https://blog.devolutions.net/2017/03/what-is-reverse-ssh-port-forwarding)

    > You could also add some options to your command: **ssh -f -N -T -R 2210:localhost:22 username@yourMachine.com**
    > 
    > -   **-f:** tells the SSH to background itself after it authenticates, saving you time by not having to run something on the remote server for the tunnel to remain alive.
    > -   **-N:** if all you need is to create a tunnel without running any remote commands then include this option to save resources.
    > -   **-T:** useful to disable pseudo-tty allocation, which is fitting if you are not trying to create an interactive shell.

- [Reverse SSH Tunnel實際運用，搭配auotssh永不斷線，putty建立反向tunnel :: 哇哇3C日誌](https://ez3c.tw/2043)

    > 懂點網路還有SSH的人就是很吃香，因為懂個幾招就可以突破網管暢行無阻！非常久之前已經介紹過[SSH Tunne](https://ez3c.tw/907)l的使用，前陣子[FACEBOOK](http://www.facebook.com/)爆紅的時候，SSH Tunnel的使用也開始爆紅了起來，因為似乎沒有什麼事情比偷菜更重要了！因此我想若懂得SSH Tunnel的人應該也很熟悉了！（建議先閱讀：[資訊安全 - SSH Tunnel 帶你遨遊](https://ez3c.tw/907)，包含防火牆PREROUTING轉port的技巧）
    > 
    > ![ssh tunnel.gif](https://host.easylife.tw/pics/201003/reverse_tunnel/ssh%20tunnel.gif)
    > 
    > 
    > 就我自己使用ssh tunnel的經驗來看，沒有使用之前光看介紹也是糊里糊塗，唯有使用過後就能更能了解運作原理，使用起來就會很順手！而ssh tunnel其實還有更進階的運用，這條無敵通道打通之後，除了可以單向的從這條通道出去之外，當然也應該可以反向的連回來，之前我對於反向這一塊很不熟悉，但是試了一次就懂了，這也就是說我可以毫無限制的連回到區網，相對的也代表這條tunnel就是一個危機，若是心臟不夠大顆絕對不推薦使用！
    > 
    > ![reverse tunnel.gif](https://host.easylife.tw/pics/201003/reverse_tunnel/reverse%20tunnel.gif)
    > 
    > 【再次警告！這將成為公司內部的大漏洞，很多風險可能不是你可以承擔的】
    > 
    > 就如上圖所表示的一樣，若你已經有能力建立一條ssh tunnel到外面的主機，那麼你就絕對有辦法從外面的主機連回區域網路，這該怎麼做呢？
    > 
    > ssh -NfR 遠端主機listen port:遠端連回時導向的主機:遠端連回本地主機時導向主機的port 帳號@遠端主機
    > 
    > ssh參數解釋：
    > ```
    > -N：不執行任何指令
    > -f：背景執行
    > -R：主要建立reverse tunnel的參數
    > ```
    > 測試的時候其實不建議加上-N與-f的參數^^
    > 
    > 範例環境：
    > 區域網路主機：
    > ```
    > ServerA / Linux / user userA / ip 192.168.0.123 / ssh port 22
    > ServerB / Linux / user userB / ip 192.168.0.125 / ssh port 22
    > PC / Windows / ip 192.168.0.128 / 遠端桌面 port 3389
    > ```
    > 
    > 遠端主機：
    > ```
    > MyServer / Linux / user me / ip 1.2.3.4 / ssh port 22
    > ```
    > 
    > 範例1：從MyServer ssh連回ServerA
    > ```
    > [userA@ServerA] $ ssh -NfR 2222:localhost:22 me@MyServer
    > --------------------------------------------------------------
    > [me@MyServer] $ netstat -tnl | grep 127.0.0.1
    > tcp        0      0 127.0.0.1:2222              0.0.0.0:*                   LISTEN
    > [me@MyServer] $ ssh userA@127.0.0.1 -p 2222
    > MyServer連線到本機2222 port會導向到ServerA的ssh port，成功連線到ServerA
    > ```
    > 範例2：從MyServer ssh連回ServerB
    > ```
    > [userA@ServerA] $ ssh -NfR 2244:192.168.0.125:22 me@MyServer
    > --------------------------------------------------------------
    > [me@MyServer] $ netstat -tnl | grep 127.0.0.1
    > tcp        0      0 127.0.0.1:2244              0.0.0.0:*                   LISTEN
    > [me@MyServer] $ ssh userB@127.0.0.1 -p 2244
    > MyServer連線到本機2244 port會導向到ServerB的ssh port，成功連線到ServerB
    > ```
    > 範例3：從MyServer遠端桌面PC
    > ```
    > [userA@ServerA] $ ssh -NfR 2266:192.168.0.128:3389 me@MyServer
    > --------------------------------------------------------------
    > [me@MyServer] $ netstat -tnl | grep 127.0.0.1
    > tcp        0      0 127.0.0.1:2266              0.0.0.0:*                   LISTEN
    > [me@MyServer] $ rdesktop 127.0.0.1:2266
    > ```
    > 若你在Linux的桌面環境則可以直接display遠端桌面PC的連線，不然就export DISPLAY到其他主機。\
    > 沒有覺得很難懂？自己做一次或許就知道囉！透過Linux連線出去，若是這條tunnel斷了線，就絕對無法再從外部連線了，因此為了要預防ssh tunnel斷線，第一種方式請在.ssh/config內加入「serveraliveinterval 60」保持KeepAlive連線；第二種可以透過[autossh](http://www.harding.motd.ca/autossh/)幫忙維持連線，若有任何斷線會再自動幫忙連線。
    > 
    > autossh 官方網站：<http://www.harding.motd.ca/autossh/>
    > 
    > ![autossh.gif](https://host.easylife.tw/pics/201003/reverse_tunnel/autossh.gif)
    > 
    > 編譯的方式不再多說，簡單的「./configure && make && make install」就可以完成安裝。
    > 
    > **autossh使用方式：**
    > 
    > 套用在上面的範例1：從MyServer ssh連回ServerA\
    > [userA@ServerA] $ autossh -M 12345 -NfR 2222:localhost:22 me@MyServer\
    > 12345是隨機指定的，不管在MyServer或是ServerA都會Listen，連上之後可以測試砍掉MyServer上的ServerA的連線，autossh會自動在ServerA上重新連線，就是透過autossh保持tunnel永遠不斷線。\
    > 不透過ssh的command，直接利用ssh連線工具也可以達到反向tunnel的建立，拿上面的範例3做示範。
    > 
    > putty與pietty的方式\
    > ![putty.gif](https://host.easylife.tw/pics/201003/reverse_tunnel/putty.gif)
    > 
    > [Xshell](https://ez3c.tw/1282)的方式\
    > ![xshell.gif](https://host.easylife.tw/pics/201003/reverse_tunnel/xshell.gif)

### Set GatewayPorts to enable remote port forwardings to bind to the specific address

- [tunnel - Reverse port tunnelling - Ask Ubuntu](https://askubuntu.com/questions/50064/reverse-port-tunnelling)

    > The command for forwarding port 80 from your local machine (`localhost`) to the remote host on port 8000 is:
    > 
    > ```
    > ssh -R 8000:localhost:80 oli@remote-machine
    > 
    > ```
    > 
    > This requires an additional tweak on the SSH server, add the lines to `/etc/ssh/sshd_config`:
    > 
    > ```
    > Match User oli
    >    GatewayPorts yes
    > 
    > ```
    > 
    > Next, reload the configuration by server executing `sudo reload ssh`.
    > 
    > The setting `GatewayPorts yes` causes SSH to bind port 8000 on the wildcard address, so it becomes available to the public address of `remote-machine` (`remote-machine:8000`).
    > 
    > If you need to have the option for not binding everything on the wildcard address, change `GatewayPorts yes` to `GatewayPorts clientspecified`. Because `ssh` binds to the loopback address by default, you need to specify an empty `bind_address` for binding the wildcard address:
    > 
    > ```
    > ssh -R :8000:localhost:80 oli@remote-machine
    > 
    > ```
    > 
    > The `:` before `8000` is mandatory if `GatewayPorts` is set to `clientspecified` and you want to allow public access to `remote-machine:8000`.
    > 
    > Relevant manual excerpts:
    > 
    > [ssh(1)](http://manpages.ubuntu.com/manpages/natty/en/man1/ssh.1.html)
    > 
    > > -R [bind_address:]port:host:hostport\
    > > Specifies that the given port on the remote (server) host is to be forwarded to the given host and port on the local side. This works by allocating a socket to listen to port on the remote side, and whenever a connection is made to this port, the connection is forwarded over the secure channel, and a connection is made to host port hostport from the local machine. **By default, the listening socket on the server will be bound to the loopback interface only.** This may be overridden by specifying a bind_address. **An empty bind_address, or the address '*', indicates that the remote socket should listen on all interfaces.** Specifying a remote bind_address will only succeed if the server's GatewayPorts option is enabled (see sshd_config(5)).
    > 
    > [sshd_config(5)](http://manpages.ubuntu.com/manpages/natty/en/man5/sshd_config.5.html)
    > 
    > > GatewayPorts\
    > > Specifies whether remote hosts are allowed to connect to ports forwarded for the client. GatewayPorts can be used to specify that sshd should allow remote port forwardings to bind to non-loopback addresses, thus allowing other hosts to connect. **The argument may be 'no' to force remote port forwardings to be available to the local host only, 'yes' to force remote port forwardings to bind to the wildcard address, or 'clientspecified' to allow the client to select the address to which the forwarding is bound.** The default is 'no'.
    > 
    > See also:
    > 
    > -   [How to create a restricted SSH user for port forwarding?](https://askubuntu.com/q/48129/6969)
    > 
    > ---
    > 
    > If the server has `GatewayPorts no`, you can achieve the same result by executing `ssh -g -L 8001:localhost:8000 oli@remote-machine` on the server once you have executed `ssh -R` command on the client. This will make loopback port 8000 on the server accessible on all interfaces on port 8001.
    > 


## ssh interactive

### run shell script on a remote machine (heredoc, script file)

- [shell - SSH heredoc: bash prompt - Stack Overflow](https://stackoverflow.com/questions/13934280/ssh-heredoc-bash-prompt)

    > To make it work with a heredoc, it should be sufficient to invoke `bash`, or whatever shell you want to use on the remote server. Like so:
    > 
    > ```sh
    > ssh $SERVER bash <<EOF
    > cd downloads/
    > read -e -p "Enter the path to the file: " FILEPATH
    > echo $FILEPATH
    > eval FILEPATH="$FILEPATH"
    > 
    > echo "Downloading $FILEPATH to $CLIENT"
    > EOF
    > ```
    > 
    > Note that you probably want to escape the `$` on `FILEPATH`, since currently that will be interpolated by the local shell rather than the remote shell.


- [How to use SSH to run a shell script on a remote machine? - Stack Overflow](https://stackoverflow.com/questions/305035/how-to-use-ssh-to-run-a-shell-script-on-a-remote-machine)

    > This is an old question, and Jason's answer works fine, but I would like to add this:
    > 
    > ```sh
    > ssh user@host <<'ENDSSH'
    > #commands to run on remote host
    > ENDSSH
    > ```
    > 
    > This can also be used with su and commands which require user input. (note the `'` escaped heredoc)
    > 
    > Edit: Since this answer keeps getting bits of traffic, i would add even more info to this wonderful use of heredoc:
    > 
    > You can nest commands with this syntax, and thats the only way nesting seems to work (in a sane way)
    > 
    > ```sh
    > ssh user@host <<'ENDSSH'
    > #commands to run on remote host
    > ssh user@host2 <<'END2'
    > # Another bunch of commands on another host
    > wall <<'ENDWALL'
    > Error: Out of cheese
    > ENDWALL
    > ftp ftp.secureftp-test.com <<'ENDFTP'
    > test
    > test
    > ls
    > ENDFTP
    > END2
    > ENDSSH
    > ```
    > 
    > You can actually have a conversation with some services like telnet, ftp, etc. But remember that heredoc just sends the stdin as text, it doesn't wait for response between lines
    > 
    > Edit: I just found out that you can indent the insides if you use `<<-END` !
    > 
    > ```sh
    > ssh user@host <<-'ENDSSH'
    >     #commands to run on remote host
    >     ssh user@host2 <<-'END2'
    >         # Another bunch of commands on another host
    >         wall <<-'ENDWALL'
    >             Error: Out of cheese
    >         ENDWALL
    >         ftp ftp.secureftp-test.com <<-'ENDFTP'
    >             test
    >             test
    >             ls
    >         ENDFTP
    >     END2
    > ENDSSH
    > ```
    > 
    > (I think this should work)
    > 
    > Also see <http://tldp.org/LDP/abs/html/here-docs.html>
    > 
    > ---
    > 
    > If Machine A is a Windows box, you can use Plink (part of [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)) with the -m parameter, and it will execute the local script on the remote server.
    > 
    > ```sh
    > plink root@MachineB -m local_script.sh
    > ```
    > 
    > If Machine A is a Unix-based system, you can use:
    > 
    > ```sh
    > ssh root@MachineB 'bash -s' < local_script.sh
    > ```
    > 
    > You shouldn't have to copy the script to the remote server to run it.
    > 
    > 

- [scripting - how to run a script file remotely using ssh - Stack Overflow](https://stackoverflow.com/questions/1041597/how-to-run-a-script-file-remotely-using-ssh)


    > If you want to execute local script remotely without saving that script remotely you can do it like this:
    > 
    > ```sh
    > cat local_script.sh | ssh user@remotehost 'bash -'
    > 
    > ```





### send/copy file by ssh

- [linux - How to copy a file without using scp inside an ssh session? - Super User](https://superuser.com/questions/291423/how-to-copy-a-file-without-using-scp-inside-an-ssh-session)

    > To send a file:
    > 
    > ```
    > cat file | ssh ajw@dogmatix "cat > remote"
    > ```
    > 
    > Or:
    > 
    > ```
    > ssh ajw@dogmatix "cat > remote" < file
    > ```
    > 
    > To receive a file:
    > 
    > ```
    > ssh ajw@dogmatix "cat remote" > copy
    > ```
    > 
    > ---
    > 
    > `cd /tmp; cat /bin/bash > test; chmod a+x test; diff test /bin/bash; ./test` all works fine.
    > 
    > ---
    > I need something like this, the only exception is, I need to pipe in all jpg from a folder. How could iterate through /storage/sdcard1/*jpg and `>` to files with the same name ?
    > 
    > you'll need to add `tar` into the mix. `tar cvf - /path/*.jpg | ssh foo@bar.com "tar xvf -"`
    > 

### Do NOT pass the commands via stdin(heredoc)

- [linux - Pseudo-terminal will not be allocated because stdin is not a terminal - Stack Overflow](https://stackoverflow.com/questions/7114990/pseudo-terminal-will-not-be-allocated-because-stdin-is-not-a-terminal)


    > Try `ssh -t -t`(or `ssh -tt` for short) to force pseudo-tty allocation even if stdin isn't a terminal.
    > 
    > See also: [Terminating SSH session executed by bash script](https://stackoverflow.com/questions/7085429/terminating-ssh-session-executed-by-bash-script)
    > 
    > From ssh manpage:
    > 
    > ```
    > -T      Disable pseudo-tty allocation.
    > 
    > -t      Force pseudo-tty allocation.  This can be used to execute arbitrary
    >         screen-based programs on a remote machine, which can be very useful,
    >         e.g. when implementing menu services.  Multiple -t options force tty
    >         allocation, even if ssh has no local tty.
    > ```
    > 
    > ---
    > 
    > All relevant information is in the existing answers, but let me attempt a **pragmatic summary**:
    > 
    > **tl;dr:**
    > 
    > -   **DO pass the commands to run using a *command-line argument***:\
    >     `ssh jdoe@server '...'`
    > 
    >     -   `'...'` strings can span multiple lines, so you can keep your code readable even without the use of a here-document:\
    >         `ssh jdoe@server ' ... '`
    > -   **Do NOT pass the commands via *stdin***, as is the case when you use a [here-document](http://mywiki.wooledge.org/HereDocument):\
    >     `ssh jdoe@server <<'EOF' # Do NOT do this ... EOF`
    > 
    > Passing the commands as an argument works as-is, and:
    > 
    > -   **the problem with the pseudo-terminal will not even arise.**
    > -   **you won't need an `exit` statement** at the end of your commands, because the session will automatically exit after the commands have been processed.
    > 
    > In short: passing commands via *stdin* is a mechanism that is at odds with `ssh`'s design and causes problems that must then be worked around.\
    > Read on, if you want to know more.
    > 
    > * * * * *
    > 
    > ### Optional background information:
    > 
    > **`ssh`'s mechanism for accepting commands to execute on the target server is a *command-line argument***: the final operand (non-option argument) accepts a string containing one or more shell commands.
    > 
    > -   By default, these **commands run unattended, in an *non-interactive* shell, without the use of a (pseudo) terminal (option `-T` is implied), and the session automatically ends** when the last command finishes processing.
    > 
    > -   In the event that your commands require *user interaction*, such as responding to an interactive prompt, you can explicitly request the creation of a [pty (pseudo-tty)](https://en.wikipedia.org/wiki/Pseudoterminal), a pseudo terminal, that enables interacting with the remote session, using the `-t` option; e.g.:
    > 
    >     -   `ssh -t jdoe@server 'read -p "Enter something: "; echo "Entered: [$REPLY]"'`
    > 
    >     -   Note that the interactive `read` prompt only works correctly with a pty, so the `-t` option is needed.
    > 
    >     -   Using a pty has a notable side effect: stdout and stderr are *combined* and both reported via *stdout*; in other words: you lose the distinction between regular and error output; e.g.:
    > 
    >         -   `ssh jdoe@server 'echo out; echo err >&2' # OK - stdout and stderr separate`
    > 
    >         -   `ssh -t jdoe@server 'echo out; echo err >&2' # !! stdout + stderr -> stdout`
    > 
    > **In the absence of this argument, `ssh` creates an *interactive* shell** - including when you send commands via *stdin*, which is where the trouble begins:
    > 
    > -   For an *interactive* shell, `ssh` normally allocates a pty (pseudo-terminal) by default, *except* if its stdin is not connected to a (real) terminal.
    > 
    >     -   **Sending commands via stdin means that `ssh`'s stdin is no longer connected to a terminal, so *no* pty is created, and `ssh` *warns* you accordingly**:\
    >         `Pseudo-terminal will not be allocated because stdin is not a terminal.`
    > 
    >     -   **Even the `-t` option, whose express purpose is to *request* creation of a pty, is *not* enough *in this case***: you'll get the same warning.
    > 
    >         -   Somewhat curiously, you must then ***double* the `-t` option** to force creation of a pty: `ssh -t -t ...` or `ssh -tt ...` shows that you *really, really mean it*.
    > 
    >         -   Perhaps the rationale for requiring this very deliberate step is that *things may not work as expected*. For instance, on macOS 10.12, the apparent equivalent of the above command, providing the commands via stdin and using `-tt`, does *not* work properly; the session gets stuck after responding to the `read` prompt:\
    >             `ssh -tt jdoe@server <<<'read -p "Enter something: "; echo "Entered: [$REPLY]"'`
    >             
    >             
    >             
    > ---
    > 
    > There are a variety of syntaxes that can be used. For example, since commands can be piped into `bash` and `sh`, and probably other shells too, the simplest solution is to just combine `ssh` shell invocation with heredocs:
    > 
    > ```sh
    > ssh user@server /bin/bash <<'EOT'
    > echo "These commands will be run on: $( uname -a )"
    > echo "They are executed by: $( whoami )"
    > EOT
    > ```
    > 
    > Note that executing the above *without* `/bin/bash` will result in the warning `Pseudo-terminal will not be allocated because stdin is not a terminal`. Also note that `EOT` is surrounded by single-quotes, so that `bash` recognizes the heredoc as a *nowdoc*, turning off local variable interpolation so that the command text will be passed as-is to `ssh`.
    > 
    > If you are a fan of pipes, you can rewrite the above as follows:
    > 
    > ```sh
    > cat <<'EOT' | ssh user@server /bin/bash
    > echo "These commands will be run on: $( uname -a )"
    > echo "They are executed by: $( whoami )"
    > EOT
    > ```
    > 
    > The same caveat about `/bin/bash` applies to the above.
    > 
    > Another valid approach is to pass the multi-line remote command as a single string, using multiple layers of `bash` variable interpolation as follows:
    > 
    > ```sh
    > ssh user@server "$( cat <<'EOT'
    > echo "These commands will be run on: $( uname -a )"
    > echo "They are executed by: $( whoami )"
    > EOT
    > )"
    > ```
    > 
    > The solution above fixes this problem in the following manner:
    > 
    > 1.  `ssh user@server` is parsed by bash, and is interpreted to be the `ssh` command, followed by an argument `user@server` to be passed to the `ssh` command
    > 
    > 2.  `"` begins an interpolated string, which when completed, will comprise an argument to be passed to the `ssh` command, which in this case will be interpreted by `ssh` to be the remote command to execute as `user@server`
    > 
    > 3.  `$(` begins a command to be executed, with the output being captured by the surrounding interpolated string
    > 
    > 4.  `cat` is a command to output the contents of whatever file follows. The output of `cat` will be passed back into the capturing interpolated string
    > 
    > 5.  `<<` begins a bash *heredoc*
    > 
    > 6.  `'EOT'` specifies that the name of the heredoc is EOT. The single quotes `'` surrounding EOT specifies that the heredoc should be parsed as a *nowdoc*, which is a special form of heredoc in which the contents do not get interpolated by bash, but rather passed on in literal format
    > 
    > 7.  Any content that is encountered between `<<'EOT'` and `<newline>EOT<newline>` will be appended to the nowdoc output
    > 
    > 8.  `EOT` terminates the nowdoc, resulting in a nowdoc temporary file being created and passed back to the calling `cat` command. `cat` outputs the nowdoc and passes the output back to the capturing interpolated string
    > 
    > 9.  `)` concludes the command to be executed
    > 
    > 10. `"` concludes the capturing interpolated string. The contents of the interpolated string will be passed back to `ssh` as a single command line argument, which `ssh` will interpret as the remote command to execute as `user@server`
    > 
    > ---
    > 
    > 

### run commands on ssh login

- [How can I automatically change directory on ssh login? - Server Fault](https://serverfault.com/questions/167416/how-can-i-automatically-change-directory-on-ssh-login)

    > This works:
    > 
    > ```sh
    > ssh server -t "cd /my/remote/directory; bash --login"
    > 
    > ```
    > 
    > To create a directory if it doesn't exist:
    > 
    > ```sh
    > ssh server -t "mkdir -p newfolder; cd ~/newfolder; pwd; bash --login"
    > 
    > ```
    > 
    > If you don't add `bash` to the end of path then you exit after the `cd` comand runs. And If you don't add `--login` then your `~/.profile` isn't sourced.
    > 



## password and ssh-keygen

### auto respond ENTER key press to ssh-keygen prompts

- [linux - How to simulate two consecutive ENTER key presses for a command in a bash script? - Stack Overflow](https://stackoverflow.com/questions/30712126/how-to-simulate-two-consecutive-enter-key-presses-for-a-command-in-a-bash-script)

    > For example, you can use either
    > 
    > ```
    > echo -e "\n"
    > ```
    > 
    > or
    > 
    > ```
    > echo -en "\n\n"
    > ```
    > 
    > The `-e` option tells `echo` to interpret escape characters. `\n` is the newline (enter) character. So the first prints a newline due to `\n`, and then another one since `echo` usually appends a newline.
    > 
    > The `-n` option tells `echo` to suppress adding an implicit newline. To get two newlines, you thus need to specify two `\n`.
    > 
    > **Edit:**
    > 
    > The problem here is that `ssh-keygen` is special. Due to security considerations, the passphrase is not read from standard input but directly from the terminal! To provide a passphrase (even an empty one) you need to use the `-P` option. Since you then only need one ENTER (for the file path prompt), this command should work:
    > 
    > ```
    > echo | ssh-keygen -P ''
    > ```
    > 
    > (note the two `'` with no space in between: they are important!)


### auto enter ssh password

- [linux - Automatically enter SSH password with script - Stack Overflow](https://stackoverflow.com/questions/12202587/automatically-enter-ssh-password-with-script)

    > sshpass combined with autossh
    > =============================
    > 
    > One nice bonus of the already-mentioned `sshpass` is that you can use it with `autossh`, eliminating even more of the interactive inefficiency.
    > 
    > ```
    > sshpass -p mypassword autossh -M0 -t myusername@myserver.mydomain.com
    > ```
    > ---
    > 
    > Note that you can't add option `-f` to autossh in this combination, because `when used with autossh, ssh will be *unable* to ask for passwords or passphrases.` [harding.motd.ca/autossh/README.txt](http://www.harding.motd.ca/autossh/README.txt) also [superuser.com/questions/1278583/...](https://superuser.com/questions/1278583/autossh-not-working-in-background "autossh not working in background") -- [allenyllee](https://stackoverflow.com/users/1851492/allenyllee "81 reputation") [1 min ago](https://stackoverflow.com/questions/12202587/automatically-enter-ssh-password-with-script#comment90928965_48290352)
    > 
    > ---
    > 
    > Variant I
    > 
    > ```
    > sshpass -p PASSWORD ssh USER@SERVER
    > ```
    > 
    > Variant II
    > 
    > ```
    > #!/usr/bin/expect -f
    > spawn ssh USERNAME@SERVER "touch /home/user/ssh_example"
    > expect "assword:"
    > send "PASSWORD\r"
    > interact
    > ```
    > 
    > ---
    > 
    > Use public key authentication: <https://help.ubuntu.com/community/SSH/OpenSSH/Keys>
    > 
    > In the source host run this only once:
    > 
    > ```
    > ssh-keygen -t rsa # ENTER to every field
    > ssh-copy-id myname@somehost
    > ```
    > 
    > That's all, after that you'll be able to do ssh without password.
    > 
    > ---



## autossh

- [SSH tunnelling for fun and profit: Autossh](https://www.everythingcli.org/ssh-tunnelling-for-fun-and-profit-autossh/)

    > AutoSSH and `-M` (monitoring port)
    > ----------------------------------
    > 
    > With `-M` AutoSSH will continuously send data back and forth through the pair of monitoring ports in order to keep track of an established connection. If no data is going through anymore, it will restart the connection. The specified monitoring and the port directly above (+1) must be free. The first one is used to send data and the one above to receive data on.
    > 
    > Unfortunately, this is not too handy, as it must be made sure both ports (the specified one and the one directly above) a free (not used). So in order to overcome this problem, there is a better solution:
    > 
    > `ServerAliveInterval` and `ServerAliveCountMax` -- they cause the SSH client to send traffic through the encrypted link to the server. This will keep the connection alive when there is no other activity and also when it does not receive any alive data, it will tell AutoSSH that the connection is broken and AutoSSH will then restart the connection.
    > 
    > The [AutoSSH man page](http://www.harding.motd.ca/autossh/README) also recommends the second solution:
    > 
    > > -M [:echo_port],\
    > > ...\
    > > In many ways this [ServerAliveInterval and ServerAliveCountMax options] may be a better solution than the monitoring port.
    > 
    > You can disable the built-in AutoSSH monitoring port by giving it a value of 0:
    > 
    > ```
    > autossh -M 0
    > 
    > ```
    > 
    > Additionally you will also have to specify values for `ServerAliveInterval` and `ServerAliveCountMax`
    > 
    > ```
    > autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3"
    > 
    > ```
    > 
    > So now the complete tunnel command will look like this:
    > 
    > ```
    > autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3" -L 5000:localhost:3306 cytopia@everythingcli.org
    > 
    > ```
    > 
    > | Option | Description |
    > | :-- | :-- |
    > | ServerAliveInterval | ServerAliveInterval: number of seconds that the client will wait before sending a null packet to the server (to keep the connection alive).\
    > Default: 30 |
    > | ServerAliveCountMax | Sets the number of server alive messages which may be sent without ssh receiving any messages back from the server. If this threshold is reached while server alive messages are being sent, ssh will disconnect from the server, terminating the session.\
    > Default: 3 |
    > 
    > AutoSSH and `~/.ssh/config`
    > ---------------------------
    > 
    > In the previous article we were able to simplify the tunnel command via `~/.ssh/config`. Luckily autossh is also aware of this file, so we can still keep our configuration there.
    > 
    > This was our very customized configuration for ssh tunnels which had custom ports and custom rsa keys:
    > 
    > ```
    > $ vim ~/.ssh/config
    >  Host cli-mysql-tunnel
    >     HostName      everythingcli.org
    >     User          cytopia
    >     Port          1022
    >     IdentityFile  ~/.ssh/id_rsa-cytopia@everythingcli
    >     LocalForward  5000 localhost:3306
    > 
    > ```
    > 
    > We can also add the `ServerAliveInterval` and `ServerAliveCountMax` options to that file in order to make things even easier.
    > 
    > ```
    > $ vim ~/.ssh/config
    >  Host cli-mysql-tunnel
    >     HostName      everythingcli.org
    >     User          cytopia
    >     Port          1022
    >     IdentityFile  ~/.ssh/id_rsa-cytopia@everythingcli
    >     LocalForward  5000 localhost:3306
    >     ServerAliveInterval 30
    >     ServerAliveCountMax 3
    > 
    > ```
    > 
    > If you recall all the ssh options we had used already, we can now simply start the autossh tunnel like so:
    > 
    > ```
    > autossh -M 0 -f -T -N cli-mysql-tunnel
    > 
    > ```
    > 
    > AutoSSH environment variables
    > -----------------------------
    > 
    > AutoSSH can also be controlled via a couple of environmental variables. Those are useful if you want to run AutoSSH unattended via `cron`, using shell scripts or during boot time with the help of `systemd` services. The most used variable is probably `AUTOSSH_GATETIME`:
    > 
    > > **AUTOSSH_GATETIME**\
    > > How long ssh must be up before we consider it a successful connection. Default is 30 seconds. If set to 0, then this behaviour is disabled, and as well, autossh will retry even on failure of first attempt to run ssh.
    > 
    > Setting `AUTOSSH_GATETIME` to 0 is most useful when running AutoSSH at boot time.
    > 
    > All other environmental variables including the once responsible for logging options can be found in the [AutoSSH Readme](http://www.harding.motd.ca/autossh/README).
    > 
    > AutoSSH during boot with systemd
    > --------------------------------
    > 
    > If you want a permanent SSH tunnel already created during boot time, you will (nowadays) have to create a systemd service and enable it. There is however an important thing to note about systemd and AutoSSH: `-f` (background usage) already implies `AUTOSSH_GATETIME=0`, however `-f` is not supported by systemd.
    > 
    > > <http://www.freedesktop.org/software/systemd/man/systemd.service.html>\
    > > [...] running programs in the background using "&", and other elements of shell syntax are not supported.
    > 
    > So in the case of `systemd` we need to make use of `AUTOSSH_GATETIME`. Let's look at a very basic service:
    > 
    > ```
    > $ vim /etc/systemd/system/autossh-mysql-tunnel.service
    > [Unit]
    > Description=AutoSSH tunnel service everythingcli MySQL on local port 5000
    > After=network.target
    > 
    > [Service]
    > Environment="AUTOSSH_GATETIME=0"
    > ExecStart=/usr/bin/autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3" -NL 5000:localhost:3306 cytopia@everythingcli.org -p 1022
    > 
    > [Install]
    > WantedBy=multi-user.target
    > 
    > ```
    > 
    > Tell systemd that we have added some stuff:
    > 
    > ```
    > systemctl daemon-reload
    > 
    > ```
    > 
    > Start the service
    > 
    > ```
    > systemctl start autossh-mysql-tunnel.service
    > 
    > ```
    > 
    > Enable during boot time
    > 
    > ```
    > systemctl enable autossh-mysql-tunnel.service
    > 
    > ```

### Permanent SSH Tunnels with autossh

- [autossh 斷線自動重連 « Jamyy's Weblog](http://jamyy.us.to/blog/2014/05/6347.html)

    > 將 Public Key 傳遞到遠端機器
    > 
    > ```
    > $ ssh-copy-id -i ~/.ssh/id_rsa.pub username@server
    > ```
    > 

- [Permanent SSH Tunnels with autossh | Linuxaria](https://linuxaria.com/howto/permanent-ssh-tunnels-with-autossh)

    > The use of `autossh` allow you to create an arbitrary number of tunnels in a very safe way, if you do not need to listen on reserved ports (<1024), you can run the program with an unprivileged user , which in our case will be precisely `autossh` .Create that user on both ends of the tunnel with:
    > 
    > 
    > ```
    > useradd -m -s /bin/false autossh
    > ```
    > 
    > 
    > please note as the user has disabled the shell and has not set a password, which will make it impossible to use the user for access to the system (which we do not need since it is only used to create the tunnel) .
    > 
    > The decision to not set the password for the authentication requires the use of keys, which is anyway the best choice and if possible to use exclusively. For this to the start of the tunnel connection you have to create the key for the user, that if you want the tunnel to start automatically at startup, will be without a passphrase, for this you must run the following commands:
    > ```
    > root@hain:~# su -s /bin/bash autossh
    > autossh@mail:/root$ ssh-kegen
    > Generating public/private rsa key pair.
    > Enter file in which to save the key (/home/autossh/.ssh/id_rsa):
    > Enter passphrase (empty for no passphrase):
    > Enter same passphrase again:
    > Your identification has been saved in /home/autossh/.ssh/id_rsa.
    > Your public key has been saved in /home/autossh/.ssh/id_rsa.pub.
    > The key fingerprint is:
    > b6:b7:d5:1e:fd:b0:62:57:b5:77:4c:33:82:78:f7:06 autossh@dodds
    > The key's randomart image is:
    > +--[ RSA 2048]----+
    > |                 |
    > |                 |
    > |          . .    |
    > |         . o E oo|
    > |        S . . +o=|
    > |       . .   . ==|
    > |        . . . =.+|
    > |         . oo..+.|
    > |          .. oo .|
    > +-----------------+
    > ```
    > (you must use `su` with the first command to impersonate the user `autossh` as this has not a shell or a valid password).
    > 
    > Once this is done you should take care to copy the public key on the machine/s and/or destination and install it in the user's home of `autossh` in the file `.ssh /authorized_keys` ; check that this file belongs to the user `autossh` .
    > 
    > Once this is done you can create a tunnel just by running the opportune command on `ssh` through `autossh` . Since you only want to bring up the tunnel you need to use the option `-N` to tell `ssh` to not run any commands, the option `-f to put it in the background, and these options are also important:`
    > ```
    > -o "ServerAliveInterval 60"
    > -o "ServerAliveCountMax 3"
    > ```
    > that activate the monitoring of the existence with the internal connection of `ssh` , the tunnel can then be activated with the usual options `-L` or `-R` depending on the direction of the tunnel.
    > 
    > So for example if you want to create a tunnel to connect to a remote MySQL database on a machine that is accessible via SSH, once created the users, as described, it will be sufficient to run the command:
    > 
    > 
    > ```
    > su -s /bin/sh autossh -c 'autossh -M 0 -q -f -N -o "ServerAliveInterval 60" -o "ServerAliveCountMax 3" -L 3306:localhost:3306 autossh@remotemachine'
    > ```
    > 
    > 
    > and at least the first time you have to accept the validity of the key fingerprint.
    > 
    > To enable the tunnel permanently at boot the easiest thing to do is to put the command in `/etc/rc.local` or similar files that are run at your system startup.
    > 

### autossh with sshpass (without -f)

- [内网穿透系列——SSH反向隧道 （最简单的内网穿透方案） | Senraの小窝](http://www.senra.me/nat-traversal-series-ssh-reverse-tunnel-the-easies-solution/)

    > **如果你使用了sshpass，那么你的autossh不能加-f参数，因为sshpass需要autossh在前台请求密码才能实现输入，这点和expect差不多，而加上-f参数放后台后会无效，所以如果要使用sshpass请务必不要加-f参数，当然，我是推荐你单使用autossh然后配合-i参数来用key认证的**
    > 
    > 如果非要sshpass，那么只能如下了，不带-f
    > ```
    > sshpass -p "ssh密码" autossh -M 5678 -CNR 2222:localhost:22 root@1.2.3.4
    > ```
    > 
    > 然后把这条命令丢到/etc/rc.local中就行了，当然你也可以选择脚本啊或者crontab之类的方法来实现开机启动，这儿我就不多说了
    > 

