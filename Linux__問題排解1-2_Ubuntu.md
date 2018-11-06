# Linux__問題排解1-2_Ubuntu

[toc]
<!-- toc --> 

## super user

### gksu alternatives

- [gksu Alternatives in Ubuntu 18.04 - Make Tech Easier](https://www.maketecheasier.com/gksu-alternatives-ubuntu-bionic/)

    > Using GVFS -- Recommended
    > ------------------------
    > 
    > ![Use gedit gvfs](https://www.maketecheasier.com/assets/uploads/2018/06/gksu-gvfs-file.jpg "Use gedit gvfs")
    > 
    > The recommended method for launching a graphical application now is to use functionality already built in to gvfs, the utility used for managing and mounting filesystems. This will require you to launch your graphical application from the terminal, much like gksu did.
    > 
    > Unlike gksu, this is already built in to GNOME and will simply require that you alter your file path to specify that you're opening it as an administrator. Opening a file with gedit looks something like this:
    > ```shell
    > gedit admin:///path/to/file.txt
    > ```
    > This will work with any utility that needs to access a file with root privileges. As long as your program takes the path to a file when it's launched, you can launch it with admin privileges this way.
    > 
    > Using Su
    > --------
    > 
    > ![Use Su for applications](https://www.maketecheasier.com/assets/uploads/2018/06/gksu-su.jpg "Use Su for applications")
    > 
    > This next option isn't exactly recommended, and it can be a security risk if used improperly. That said, it's the most direct way to launch a program as root. Keep in mind, this will launch things **as root**, not just with root privileges. You should also keep in mind that GNOME and other desktop environments will handle the privileges for you when you launch a utility like gParted through your desktop launcher. This method isn't strictly necessary for that. In any case, this is still an option.
    > 
    > Start by switching your user to root in the terminal. Make note of the `-` at the end. That bit makes launching graphical applications possible in most cases.
    > ```shell
    > sudo su -
    > ```
    > Now, launch your application.
    > ```shell
    > gparted
    > ```

- [gksudo - Why is gksu no longer installed by default? - Ask Ubuntu](https://askubuntu.com/questions/284306/why-is-gksu-no-longer-installed-by-default)

    > However gksu is not recommended any more and it may be removed entirely from future issues of Ubuntu. In general the development team would prefer us not to use GUI applications as root but to use **sudo** and the command line instead.
    > 
    > In the long term pkexec is preferred however it's not very easy to use at the moment.
    > 
    > **pkexec** allows an authorized user to execute PROGRAM as another user. If username is not specified, then the program will be executed as the administrative super user, root.
    > 
    > see the [man page](http://manpages.ubuntu.com/manpages/raring/en/man1/pkexec.1.html) `man pkexec` for more information.
    > 
    > In the mean time you can open a terminal `CTRL`+`ALT`+`T` or search for terminal in dash.
    > 
    > **Do not close the terminal until you have finished this is important** as the GUI program is a child of the terminal and if you close it the GUI program will also close.
    > 
    > Enter `sudo -i`
    > 
    > You are now logged on as root so can make the changes you want for example
    > 
    > ```
    > gedit path_to_file
    > 
    > ```
    > 
    > to edit a configuration file, or
    > 
    > ```
    > nautilus
    > 
    > ```
    > 
    > to run the file manager
    > 
    > When you are finished close the GUI application then in the terminal
    > 
    > ```
    > exit
    > 
    > ```
    > 
    > You can now close the terminal.


- [sudo - I need an equivalent of gksu in 18.04 - Ask Ubuntu](https://askubuntu.com/questions/1042344/i-need-an-equivalent-of-gksu-in-18-04)

    > Nautilus Admin (*nautilus-admin*) is a simple Python extension for the Nautilus file manager that adds some administrative actions to the right-click menu:
    > 
    > -   Open as Administrator: opens a folder in a new Nautilus window running with administrator (root) privileges.
    > -   Edit as Administrator: opens a file in a Gedit window running with administrator (root) privileges.
    > 
    > To install Nautilus Admin in all currently supported versions of Ubuntu open the terminal and type:
    > 
    > ```
    > sudo apt install nautilus-admin
    > 
    > ```
    > 
    > I've tested all the alternatives to gksu in 18.04 for other applications besides files and Gedit, and the one that seems to work the most consistently is:
    > ```shell
    > sudo -H appname &>/dev/null
    > ```
    > `pkexec` is the best replacement for gksu when it works because it provides higher security, but it is very inconsistent across different apps and can cause crashing with some apps. `sudo -i` is unnecessarily difficult to manage because it elevates your privileges to root for an extended period of time when you only need to be root to run a single command.

- [How do I start Nautilus as root? - Ask Ubuntu](https://askubuntu.com/questions/156998/how-do-i-start-nautilus-as-root)

    > 
    > 
    > If you are using Ubuntu 17.10
    > -----------------------------
    > 
    > The following method does not work with Wayland by default. There are some workarounds. The easiest one is not to use Wayland. [How do you switch from Wayland back to Xorg in Ubuntu 17.10?](https://askubuntu.com/questions/961304/how-do-you-switch-from-wayland-back-to-xorg-in-ubuntu-17-10) Other alternatives are described in [Why don't gksu/gksudo or launching a graphical application with sudo work with Wayland?](https://askubuntu.com/questions/961967/why-dont-gksu-gksudo-or-launching-a-graphical-application-with-sudo-work-with-w)
    > 
    > Ubuntu will switch back to Xorg by default in 18.04 LTS and the workarounds will not be needed then.
    > 
    > Original answer
    > ---------------
    > 
    > Source: [WebUpd8](http://www.webupd8.org/2015/03/how-to-run-gedit-and-nautilus-as-root.html)
    > 
    > `gksu` hasn't been updated since 2009 and is [not recommended](https://askubuntu.com/a/284717/662) any more. In fact, Ubuntu no longer ships with gksu by default (though it may be installed for many of you, because some apps still depend on it) and it may even be completely removed at some point.
    > 
    > **`Nautilus admin` adds PolicyKit files for both Nautilus and Gedit** and it allows opening a file or folder from Nautilus as root, via PolicyKit:
    > 
    > To install `Nautilus Admin` in Ubuntu, open a terminal by pressing `Ctrl`+`Alt`+`T` and use the following command:
    > 
    > ```
    > sudo apt-get install nautilus-admin
    > 
    > ```
    > 
    > And to [restart Nautilus](https://askubuntu.com/questions/19979/how-to-restart-nautilus-without-logging-out) use either of the following commands:
    > 
    > `nautilus -q` or `killall nautilus`
    > 
    > After this when you right click on a folder you will see:
    > 
    > [![enter image description here](https://i.stack.imgur.com/waGLf.png)](https://i.stack.imgur.com/waGLf.png)
    > 
    > If you right click on a text file editable by Gedit you will see:
    > 
    > [![enter image description here](https://i.stack.imgur.com/1YiZf.png)](https://i.stack.imgur.com/1YiZf.png)
    > 
    > Then you will be prompted for password:
    > 
    > [![enter image description here](https://i.stack.imgur.com/H4koz.png)](https://i.stack.imgur.com/H4koz.png)
    > 
    > Related question: ["Open in terminal" not working on nautilus as root](https://askubuntu.com/questions/833139/open-in-terminal-not-working-on-nautilus-as-root)
    > 
    > Finally, installing `nautilus-admin` also allows opening nautilus as root from the command line. Use the following command instead of `gksu` or `gksudo`:
    > 
    > ```
    > pkexec nautilus
    > 
    > ```
    > 
    > to open nautilus as root.
    > 
    > Hope this helps

### switch from Wayland back to Xorg

- [How do you switch from Wayland back to Xorg in Ubuntu 17.10? - Ask Ubuntu](https://askubuntu.com/questions/961304/how-do-you-switch-from-wayland-back-to-xorg-in-ubuntu-17-10)

    > When you boot your system and get to the GDM login screen you should find a cogwheel (⚙️) next to the sign in button. If you click on the cogwheel you should find an **Ubuntu on Xorg** option which will start an Xorg session instead of a Wayland session.
    > 
    > [![enter image description here](https://i.stack.imgur.com/6FtxL.jpg)](https://i.stack.imgur.com/6FtxL.jpg)
    > 
    > ---
    > 
    > If you wish to do it permanently, edit
    > 
    > `/etc/gdm3/custom.conf` and uncomment the line
    > 
    > `#WaylandEnable=false` by removing the `#` in front.
    > 
    > Save the file and then on reboot you will never see the cog asking for which session to use.
    > 

### launching a graphical application with sudo work with Wayland

- [root - Why don't gksu/gksudo or launching a graphical application with sudo work with Wayland? - Ask Ubuntu](https://askubuntu.com/questions/961967/why-dont-gksu-gksudo-or-launching-a-graphical-application-with-sudo-work-with-w)

    > Solutions
    > =========
    > 
    > In Wayland it is often difficult to run GUI application programs with elevated (sudo -H, gksu ...) permissions. It is a good idea to do such tasks with command line tools.
    > 
    > But there are workarounds, if you have a GUI tool, that works well for you and needs elevated permissions. (I use two such standard tools: the Synaptic Package Manager, **`synaptic`** and the partitioning tool Gparted, **`gparted`**. I use MakeUSB to create USB boot drives, **`mkusb`**, too, but it can run the parts that need elevated permissions without graphics.)
    > 
    > ### `xhost` and `sudo -H`
    > 
    > 1.  There is a workaround to allow graphical application programs owned by other users than the logged in user in Wayland,
    > 
    >     ```
    >     xhost +si:localuser:root
    > 
    >     ```
    > 
    > 2.  `gksu` and `gksudo` are not bundled with standard Ubuntu and do not work here, but they work in Xorg.
    > 
    >     Instead you can use
    > 
    >     ```
    >     sudo -H
    > 
    >     ```
    > 
    > 3.  It is a good idea to prevent graphical application programs owned by other users than the logged in user afterwards,
    > 
    >     ```
    >     xhost -si:localuser:root
    > 
    >     ```
    > 
    > ### gvfs admin backend
    > 
    > In Ubuntu 17.10 (gvfs >= 1.29.4) you can use the gvfs admin backend. Notice that you need the full path,
    > 
    > ```
    > gedit admin:///path/to/file
    > 
    > ```
    > 
    > In theory, the gvfs admin backend method (which uses polkit) is better and safer (than `xhost` and `xudo -H`), regardless of the UI you use.
    > 
    > You don't run the whole application as root. Privilege escalation happens only when strictly necessary. See the following link and links from it,
    > 
    > -   [sisco311's reply in the Ubuntu Forums thread 'Which best practice for using gedit as root?'](https://ubuntuforums.org/showthread.php?t=2385818&p=13743162#post13743162)
    > 
    >     This is post #4. See also post #6 in the same thread.
    > 
    > ### nautilus-admin
    > 
    > It is also possible to use `nautilus-admin` for file operations with elevated permissions and to use `gedit` with elevated permissions. This is described in the following AskUbuntu answer,
    > 
    > -   [How do I start Nautilus as root?](https://askubuntu.com/questions/156998/how-do-i-start-nautilus-as-root/868882#868882)
    > 
    > Temporary access for root to the Wayland desktop via function `gks`
    > -------------------------------------------------------------------
    > 
    > Please avoid `sudo GUI-program`. It can cause the system to overwrite the configuration files for your regular user ID with `root`'s configuration and set ownership and permissions to fit `root` and lock out your regular user ID. You should run GUI applications with `sudo -H`, which writes the configuration files in `root`'s home directory `/root`. Example:
    > 
    > ```
    > sudo -H gedit myfile.txt
    > 
    > ```
    > 
    > But there is a risk that you forget `-H`. Instead you can create a function, for example `gks`
    > 
    > ```
    > gks () { xhost +si:localuser:root; sudo -H "$@"; xhost -si:localuser:root; }
    > 
    > ```
    > 
    > and store it in your `~/.bashrc` near the aliases. Then you can run
    > 
    > ```
    > gks gedit myfile.txt
    > 
    > ```
    > 
    > in a way similar to how you used `gksudo` before.
    > 
    > Testing
    > -------
    > 
    > You can check how `sudo`, `sudo -H` and `gks` work with the following commands
    > 
    > ```
    > sudodus@xenial32 ~ $ sudo bash -c "echo ~"
    > /home/sudodus
    > sudodus@xenial32 ~ $ sudo -H bash -c "echo ~"
    > /root
    > sudodus@xenial32 ~ $ gks () { xhost +si:localuser:root; sudo -H "$@"; xhost -si:localuser:root; }
    > sudodus@xenial32 ~ $ gks bash -c "echo ~"
    > localuser:root being added to access control list
    > /root
    > localuser:root being removed from access control list
    > sudodus@xenial32 ~ $
    > 
    > ```
    > 
    > and of course
    > 
    > ```
    > gks gedit myfile.txt
    > 
    > ```
    > 
    > according to the example in the previous section.
    > 
    > Method that works via Alt-F2 and Gnome Shell menu
    > -------------------------------------------------
    > 
    > Instead of adding a simple one-line function to `~/.bashrc`, you can make a system, that works also without bash. It may be convenient to use, but is more complicated to set up. Please notice that you should install only one of the alternatives, because the one-line function will disturb using this more complicated system.
    > 
    > Three files
    > -----------
    > 
    > The shellscript **`gks`**:
    > 
    > ```shell
    > #!/bin/bash
    > 
    > xhost +si:localuser:root
    > 
    > if [ $# -eq 0 ]
    > then
    >   xterm -T "gks console - enter command and password"\
    >   -fa default -fs 14 -geometry 60x4\
    >   -e bash -c 'echo "gks lets you run command lines with GUI programs
    > with temporary elevated permissions in Wayland.";\
    > read -p "Enter command: " cmd;\
    > cmdfile=$(mktemp); echo "$cmd" > "$cmdfile";\
    > sudo -H bash "$cmdfile"; rm "$cmdfile"'
    > else
    >  xterm -T "gks console - enter password" -fa default -fs 14 -geometry 60x4 -e sudo -H "$@"
    > fi
    > 
    > xhost -si:localuser:root;
    > 
    > ```
    > 
    > The desktop file **`gks.desktop`**:
    > 
    > ```
    > [Desktop Entry]
    > Version=1.0
    > Categories=Application;System;
    > Type=Application
    > Name=gks
    > Description=Run program with temporary elevated permissions in Wayland
    > Comment=Run program with temporary elevated permissions in Wayland
    > Exec=gks %f
    > Icon=/usr/share/icons/gks.svg
    > Terminal=false
    > StartupNotify=false
    > GenericName[en_US.UTF-8]=Run program with temporary elevated permissions in Wayland
    > 
    > ```
    > 
    > The icon file **`gks.svg`** looks like this:
    > 
    > [![enter image description here](https://i.stack.imgur.com/tpOxW.png)](https://i.stack.imgur.com/tpOxW.png)
    > 
    > You can download the icon file or a tarball with all three files from this link,
    > 
    > [wiki.ubuntu.com/Wayland/gks](https://wiki.ubuntu.com/Wayland/gks)
    > 
    > Copy the [extracted or copied & pasted] files to the following locations,
    > 
    > ```
    > sudo cp gks /usr/bin
    > sudo cp gks.desktop /usr/share/applications/
    > sudo cp gks.svg /usr/share/icons
    > 
    > ```
    > 
    > Logout/login or reboot, and there should be a working desktop icon. It will work from a terminal window like with the simple solution with the function.
    > 
    > **`Alt F2`** box:
    > 
    > [![enter image description here](https://i.stack.imgur.com/39Jam.png)](https://i.stack.imgur.com/39Jam.png)
    > 
    > Gnome Shell menu:
    > 
    > [![enter image description here](https://i.stack.imgur.com/NKPQp.png)](https://i.stack.imgur.com/NKPQp.png)
    > 
    > gks console and gparted:
    > 
    > [![enter image description here](https://i.stack.imgur.com/8VvWt.png)](https://i.stack.imgur.com/8VvWt.png)
    > 
    > Custom script and desktop file
    > ------------------------------
    > 
    > If you have only a few GUI applications, that need elevated permissions, you could make custom scripts and desktop files for them and avoid entering the command (application name). You would only enter the password, which is not more difficult compared to the previous versions of Ubuntu (you should enter the password anyway).
    > 
    > Example with the simple GUI program `xlogo` that comes with the program package `x11-apps`:
    > 
    > The shellscript **`gkslogo`** (simplified compared to `gks`),
    > 
    > ```
    > #!/bin/bash
    > 
    > xhost +si:localuser:root
    > 
    > xterm -T "gks console - enter password" -fa default -fs 14 -geometry 60x4 -e sudo -H xlogo
    > 
    > xhost -si:localuser:root;
    > 
    > ```
    > 
    > The desktop file **`gkslogo.desktop`**:
    > 
    > ```
    > [Desktop Entry]
    > Version=1.0
    > Categories=Application;System;
    > Type=Application
    > Name=gkslogo
    > Description=Run program with temporary elevated permissions in Wayland
    > Comment=Run program with temporary elevated permissions in Wayland
    > Exec=gkslogo
    > Icon=/usr/share/icons/gks.svg
    > Terminal=false
    > StartupNotify=false
    > GenericName[en_US.UTF-8]=Run program with temporary elevated permissions in Wayland
    > 
    > ```
    > 
    > I was lazy and used the same icon file **`gks.svg`**
    > 
    > Copy the [copied & pasted] files to the following locations,
    > 
    > ```
    > sudo cp gkslogo /usr/bin
    > sudo cp gkslogo.desktop /usr/share/applications/
    > 
    > ```
    > 
    > gks[logo] console and xlogo:
    > 
    > [![enter image description here](https://i.stack.imgur.com/XnL7s.png)](https://i.stack.imgur.com/XnL7s.png)
    > 
    > 


## font rendering

### infinality

- [Better Font Rendering In Linux With Infinality ~ Web Upd8: Ubuntu / Linux blog](http://www.webupd8.org/2013/06/better-font-rendering-in-linux-with.html)

    > **[Infinality](http://www.infinality.net/) is a set of Freetype patches that try to provide an improved font rendering for Linux and also, to allow easy customization** so the users can adjust the settings to their taste. Using it, **you can easily set the font style to emulate OSX, OSX2, Windows 98, WIndows XP or Windows 7** or you can use the **"Linux" or "Infinality" (default) styles**.
    > 
    > ---
    > 
    > Install and configure Infinality for better font rendering in Linux
    > -------------------------------------------------------------------
    > 
    > **Ubuntu:** Freetype with the Infinality patches can be installed in Ubuntu by using a PPA. **To add the PPA and install the required packages in Ubuntu 16.04, 15.10, 15.04, 14.04, or 12.04 / Linux Mint 18, 17 or 13 use the following commands:**
    > 
    > ```
    > sudo add-apt-repository ppa:no1wantdthisname/ppa
    > sudo apt-get update
    > sudo apt-get upgrade
    > sudo apt-get install fontconfig-infinality
    > ```
    > 
    > **Once installed, log out and log back in.**
    > 
    > 
    > ---
    > 
    > **Once you install Infinality, it's time to configure it. To set the style you want to use, run the following command:**
    > 
    > ```
    > sudo bash /etc/fonts/infinality/infctl.sh setstyle
    > ```
    > 
    > And select the style you want to use. Available options are: debug, infinality, linux, osx, osx2, win7, win98 and winxp (I recommend using the **"linux" style**, obviously, but you can try any style, then remember to log out and log back in - you can easily select a different style later on by using the same command). **To use the Windows or OSX style you'll also need to use the Windows or OSX fonts**.\
    > **Optional:** next, open */etc/profile.d/infinality-settings.sh* with a text editor as root - I'll use Gedit below:
    > 
    > ```
    > sudo -H gedit /etc/profile.d/infinality-settings.sh
    > ```
    > 
    > And in this file, search for ***USE_STYLE*** (it should be USE_STYLE="DEFAULT" by default) and change it to one of the following styles (I recommend using "UBUNTU" here but you should also try the default to see which one you like better):
    > 
    > -   DEFAULT - A compromise that should please most people;
    > -   OSX - Simulate OSX rendering;
    > -   IPAD - Simulate iPad rendering;
    > -   UBUNTU - Simulate Ubuntu rendering;
    > -   LINUX - Generic "Linux" style - no snapping or certain other tweaks;
    > -   WINDOWS - Simulate Windows rendering;
    > -   WINDOWS7 - Simulate Windows rendering with normal glyphs;
    > -   WINDOWS7LIGHT- Simulate Windows 7 rendering with lighter glyphs;
    > -   WINDOWS - Simulate Windows rendering;
    > -   VANILLA - Just subpixel hinting;
    > -   CUSTOM - Your own choice;
    > -   Infinality styles:
    > 
    > -   CLASSIC - Infinality rendering circa 2010. No snapping;
    > -   NUDGE - CLASSIC with lightly stem snapping and tweaks;
    > -   PUSH - CLASSIC with medium stem snapping and tweaks;
    > -   SHOVE - Full stem snapping and tweaks without sharpening;
    > -   SHARPENED - Full stem snapping, tweaks, and Windows-style sharpening;
    > -   INFINALITY - Settings used by the Infinality developer;
    > -   DISABLED - Act as though running without the extra infinality enhancements (just subpixel hinting).
    > 
    > In this file you can change many other settings but if you don't know what they do, only change the style. Then, save the file, log out and log back in to see the changes.
    > 

- [How to install Infinality on 17.10? fontconfig-infinality not found in Ubuntu 17.10](https://ubuntuforums.org/showthread.php?t=2385152)

    > You can install it via .deb package
    > 
    > cd /tmp\
    > wget [https://launchpad.net/~no1wantdthisn...u0ppa1_all.deb](https://launchpad.net/~no1wantdthisname/+archive/ubuntu/ppa/+files/fontconfig-infinality_20130104-0ubuntu0ppa1_all.deb)\
    > sudo dpkg -i fontconfig-infinality_20130104-0ubuntu0ppa1_all.deb\
    > sudo bash /etc/fonts/infinality/infctl.sh setstyle
    > 
    > Tested in Ubuntu 18.


## dconf-editor and gsettings 

- [unity - Shouldn't dconf-editor and gsettings access the same database? - Ask Ubuntu](https://askubuntu.com/questions/416556/shouldnt-dconf-editor-and-gsettings-access-the-same-database)

    > -   `dconf-editor` uses `schema path` to show settings data tree. Same structure used to store data in GVariant database.
    > 
    > -   `gsettings` (from glib-2.0) uses `schema id` to show/get settings data. Same way as any other application should do which uses GSetttings API.
    > 
    > -   It's up to the application developer to set both as he/she would like. (with some restriction for canonical naming). So `path` could be different than `id` but most application developers prefer to use identical word series/combination. Some don't preserve same capitalization. Example [Tracker project from Gnome](https://git.gnome.org/browse/tracker/tree/data/gschemas)
    > 
    >     ```
    >     <schema id="org.freedesktop.Tracker.Miner" path="/org/freedesktop/tracker/miner/" />
    > 
    >     ```
    > 
    >     In addition to that, some alternative applications share same settings which belong to the Gnome desktop. Example: `input-sources`
    > 
    > * * * * *
    > 
    > -   First, **Apps should not mess with `dconf`**
    > 
    >     Introduction from [dconf](https://wiki.gnome.org/Projects/dconf) project page:
    > 
    >     `dconf` is a low-level configuration system. Its main purpose is to provide a backend to GSettings on platforms that don't already have configuration storage systems.
    > 
    > -   **Where's the data stored?** (Ref: <https://wiki.gnome.org/Projects/dconf/SystemAdministrators>)
    > 
    >     A profile is a list of configuration databases. What it seems that Gnome & Unity use same profile.
    > 
    >     ```
    >     $ cat /etc/dconf/profile/gdm
    >     user-db:user
    >     system-db:gdm
    > 
    >     ```
    > 
    >     1.  `user-db:user`: First database in the profile is read-write `rw` and it is created in the user's home directory.
    > 
    >         ```
    >         $ file ~/.config/dconf/user
    >         /home/sneetsher/.config/dconf/user: GVariant Database file, version 0
    > 
    >         ```
    > 
    >     2.  `system-db:gdm`: read-only
    > 
    >         ```
    >         $ file /etc/dconf/db/gdm
    >         /etc/dconf/db/gdm: GVariant Database file, version 0
    > 
    >         ```
    > 
    >         `dconf` could bind a text style store in addition to GVariant Database from `db.d/*` folder. Example (Notice file path, so it is a part of `system-db:gdm`):
    > 
    >         ```
    >          $ cat /etc/dconf/db/gdm.d/00-upstream-settings
    > 
    >          # This file is part of the GDM packaging and should not be changed.
    >          #
    >          # Instead create your own file next to it with a higher numbered prefix,
    >          # and run
    >          #
    >          #       dconf update
    >          #
    > 
    >          [org/gnome/desktop/a11y/keyboard]
    >          enable=true
    > 
    >          [org/gnome/desktop/background]
    >          show-desktop-icons=false
    >          ...
    > 
    >         ```
    > 
    > -   **Schema Files: Relation between `schema id` & `schema path`** (`*.gschema.xml`)
    > 
    >     [What is the schema XML file in the data/glib-2.0 folder of my Quickly application?](https://askubuntu.com/questions/165890/what-is-the-schema-xml-file-in-the-data-glib-2-0-folder-of-my-quickly-applicatio) by [trent](https://askubuntu.com/users/50523/trent) shows a nice example of using GSettings API in a Quickly application, and his conclusion based on his experience.
    > 
    >     Back to Vino. Each application that uses GSsettings should define its schema's and should store/install them in `/usr/share/glib-2.0/schemas/` (It's a glib directory):
    > 
    >     ```
    >     $ dpkg -L vino | grep -i glib-2.0
    >     /usr/share/glib-2.0
    >     /usr/share/glib-2.0/schemas
    >     /usr/share/glib-2.0/schemas/org.gnome.Vino.enums.xml
    >     /usr/share/glib-2.0/schemas/org.gnome.Vino.gschema.xml
    > 
    >     $ more /usr/share/glib-2.0/schemas/org.gnome.Vino.gschema.xml
    >     <schemalist>
    >       <schema id='org.gnome.Vino' path='/org/gnome/desktop/remote-access/'>
    >         <key name='enabled' type='b'>
    >           <summary>Enable remote access to the desktop</summary>
    >           <description>
    >             If true, allows remote access to the desktop via the RFB
    >             protocol. Users on remote machines may then connect to the
    >             desktop using a VNC viewer.
    >           </description>
    >           <default>false</default>
    >         </key>
    > 
    >         <key name='prompt-enabled' type='b'>
    >           <summary>Prompt the user before completing a connection</summary>
    >           <description>
    >             If true, remote users accessing the desktop are not allowed
    >             access until the user on the host machine approves the
    >             connection. Recommended especially when access is not password
    >             protected.
    >           </description>
    >           <default>true</default>
    >         </key>
    >     ...
    > 
    >     ```
    > 
    >     If you noticed, The schema is defined with an `id` and a `path`. The schema file name follows the `id` value.
    > 
    >     ```
    >     <schema id='org.gnome.Vino' path='/org/gnome/desktop/remote-access/'>
    > 
    >     ```
    > 
    > -   `*.enums.xml` files are for custom enumeration declaration, to be used as new data types in `*.gschema.xml` with same `schema id`.
    > 
    >     ```
    >     $ cat /usr/share/glib-2.0/schemas/org.gnome.Vino.enums.xml
    >     <!-- Generated data (by glib-mkenums) -->
    > 
    >     <schemalist>
    >       <enum id='org.gnome.Vino.VinoIconVisibility'>
    >         <value nick='never' value='0'/>
    >         <value nick='always' value='1'/>
    >         <value nick='client' value='2'/>
    >       </enum>
    >     </schemalist>
    > 
    >     <!-- Generated data ends here -->
    > 
    >     $ gsettings range org.gnome.Vino icon-visibility
    >     enum
    >     'never'
    >     'always'
    >     'client'
    > 
    >     $ gsettings get org.gnome.Vino icon-visibility
    >     'client'
    > 
    >     ```
    > 
    > -   **Compiling Schema's** (Ref: [Playing with dconf and gnome-tweak-tool](https://lleksah.wordpress.com/2012/04/04/playing-with-dconf-and-gnome-tweak-tool/))
    > 
    >     As part of the installation process (it has a dpkg trigger), schema's are compiled with `glib-compile-schemas` tool (from glib)
    > 
    >     ```
    >     sudo glib-compile-schemas /usr/share/glib-2.0/schemas
    > 
    >     ```
    > 
    >     `*.gschema.xml` will be compiled to a binary file `/usr/share/glib-2.0/schemas/gschemas.compiled`
    > 
    > -   **Vendor Override Files** (`*.gschema.override`)
    > 
    >     In addition to schema files, `glib-compile-schemas` reads *vendor override* files, which are key files that can override default values for keys in the schemas (Ref: [`man glib-compile-schemas`](http://manpages.ubuntu.com/manpages/trusty/en/man1/glib-compile-schemas.1.html)). They contain the changes done by Ubuntu distribution to override upstream schema defaults.
    > 
    >     ```
    >     $ ls /usr/share/glib-2.0/schemas/*.gschema.override
    >     /usr/share/glib-2.0/schemas/10_compiz-gnome.gschema.override
    >     /usr/share/glib-2.0/schemas/10_desktop-base.gschema.override
    >     /usr/share/glib-2.0/schemas/10_evolution-common.gschema.override
    >     /usr/share/glib-2.0/schemas/10_gnome-settings-daemon.gschema.override
    >     /usr/share/glib-2.0/schemas/10_gnome-shell.gschema.override
    >     /usr/share/glib-2.0/schemas/10_gnome-system-log.gschema.override
    >     /usr/share/glib-2.0/schemas/10_gsettings-desktop-schemas.gschema.override
    >     /usr/share/glib-2.0/schemas/10_libgtk-3-common.gschema.override
    >     /usr/share/glib-2.0/schemas/10_ubuntu-settings.gschema.override
    >     /usr/share/glib-2.0/schemas/20_ubuntu-gnome-default-settings.gschema.override
    > 
    >     $ cat /usr/share/glib-2.0/schemas/10_gnome-settings-daemon.gschema.override
    >     [org.gnome.desktop.wm.keybindings]
    >     switch-input-source=['<Super>space']
    >     switch-input-source-backward=['<Shift><Super>space']
    > 
    >     ```
    > 
    >     Example of override files use, See [How to customize the Ubuntu Live CD?](https://askubuntu.com/questions/48535/how-to-customize-the-ubuntu-live-cd/157562#157562) (5. Customization 2: Backgrounds and Themes).
    > 
    > -   **Lock files**
    > 
    >     Currently, dconf supports only per-key locking, no sub-path lock. User defined values will still be stored in `user-db` but will have no effect on applications. dconf/gsettings returns default values instead for those locked keys. Lock files are stored in `db.d/locks/`. Example:
    > 
    >     ```
    >     $ cat /etc/dconf/db/gdm.d/locks/00-upstream-settings-locks
    >     /org/gnome/desktop/a11y/keyboard/enable
    >     /org/gnome/desktop/background/show-desktop-icons
    >     /org/gnome/desktop/lockdown/disable-application-handlers
    >     /org/gnome/desktop/lockdown/disable-command-line
    >     /org/gnome/desktop/lockdown/disable-lock-screen
    >     /org/gnome/desktop/lockdown/disable-log-out
    >     /org/gnome/desktop/lockdown/disable-printing
    >     /org/gnome/desktop/lockdown/disable-print-setup
    >     /org/gnome/desktop/lockdown/disable-save-to-disk
    >     /org/gnome/desktop/lockdown/disable-user-switching
    >     ...
    > 
    >     ```
    > 
    >     After locks modification, to be effective run:
    > 
    >     ```
    >     sudo dconf update
    > 
    >     ```
    > 
    >     A good showcase: [dconf Settings: defaults and locks](http://www.mattfischer.com/blog/?p=431)
    > 
    > -   **Changing Global Settings**
    > 
    >     The default for `gsettings`/`dconf-editor` is to edit the `user-db`. To change `system-db`, write a new override file and recompile schema's.
    > 
    >     I couldn't get this to work:
    > 
    >     ```
    >     sudo su gdm -c 'gsettings ...'
    > 
    >     ```
    > 
    >     neither the other answers here [Set Default/Global Gnome Preferences (Gnome 3)](https://unix.stackexchange.com/questions/27484/set-default-global-gnome-preferences-gnome-3), may be that was for an old release.
    >     
    >     


### Remove key or path of schema tree 

- [maintenance - How do I clean up my dconf database? - Ask Ubuntu](https://askubuntu.com/questions/45535/how-do-i-clean-up-my-dconf-database/85755#85755)

    > This is possible using the `dconf reset` command, though it's not clear if that's a side-effect of a bug.
    > 
    > -   For a single key:
    > 
    >     ```
    >     dconf reset "/path/to/the/key"
    > 
    >     ```
    > 
    >     **Must not** end with a `/`.
    > 
    > -   For a whole path:
    > 
    >     ```
    >     dconf reset -f "/path/to/the/path/"
    > 
    >     ```
    > 
    >     **Must** end with a `/`.
    > 
    > If you do this while having `dconf-editor` opened, it will likely crash.



### Change Dock behavior: on click minimize

- [安装 Ubuntu 18.04 LTS 后要做的 11 件事情 - 开源中国社区](https://www.oschina.net/news/95593/things-to-do-after-installing-ubuntu-18-04?from=20180429)

    > 你只需在 Terminal 应用程序中运行此命令，就可以轻松地为 Ubuntu Dock 启用最小化操作：
    > 
    > ```bash
    > gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'
    > ```
    > 

- [gnome shell - How to turn off on click minimize on dock option on Ubuntu 18.04? - Ask Ubuntu](https://askubuntu.com/questions/1030531/how-to-turn-off-on-click-minimize-on-dock-option-on-ubuntu-18-04)

    > You can revert to the default option by running
    > 
    > ```
    > gsettings reset org.gnome.shell.extensions.dash-to-dock click-action
    > 
    > ```
    > 
    > Also try running
    > 
    > ```
    > gsettings range org.gnome.shell.extensions.dash-to-dock click-action
    > 
    > ```
    > 
    > then you'll get all possible values that can be set. See if you find another option preferable.
    > 



### Cannot add custom launcher to Dock (*Add to Favorites*)

- [gnome - Cannot add custom launcher to Dock (*Add to Favorites*) - Ask Ubuntu](https://askubuntu.com/questions/990833/cannot-add-custom-launcher-to-dock-add-to-favorites)

    > Open Terminal and run
    > 
    > ```
    > gsettings get org.gnome.shell favorite-apps
    > 
    > ```
    > 
    > You should get the list of `.desktop` files associated to the apps pinned to Ubuntu dock in order, something like the following:
    > 
    > ```
    > ['appname-1.desktop', 'appname-2.desktop', 'appname-3.desktop', 'appname-4.desktop', 'appname-5.desktop']
    > 
    > ```
    > 
    > Suppose you want to pin the app associated to the `intellij.desktop` file as the second item in the dock. In that case, run
    > 
    > ```
    > gsettings set org.gnome.shell favorite-apps "['appname-1.desktop', 'intellij.desktop', 'appname-2.desktop', 'appname-3.desktop', 'appname-4.desktop', 'appname-5.desktop']"
    > 
    > ```

### Hide Removable Drive Icons from Desktop

- [Hide Removable Drive Icons from Your Ubuntu Desktop](https://www.howtogeek.com/howto/ubuntu/hide-removable-drive-icons-from-your-ubuntu-desktop/)

    > I prefer a clean desktop with no icons cluttering it up, but by default Ubuntu adds icons to the desktop for every single removable drive that you attach to your system.
    > 
    > ![](https://www.howtogeek.com/wp-content/uploads/2007/05/WindowsLiveWriter/HideRemoveableDriveIconsfromYourUbuntuDe_F982/010520071178055829266974714.png)
    > 
    > Having recently transitioned to using Ubuntu full-time at home (instead of just part-time), this was one of the first things I wanted to disable. Sadly there's no option in the default configuration screens, so we'll have to use the "registry editor" for Ubuntu, called gconf-editor.
    > 
    > Just type in *gconf-editor* into the Alt+F2 run dialog to open the app. 
    > 
    >  ![](https://www.howtogeek.com/wp-content/uploads/2007/05/WindowsLiveWriter/HideRemoveableDriveIconsfromYourUbuntuDe_F982/010520071178057478449516320.png)
    > 
    > Now browse down to the following key:
    > 
    > > apps \ nautilus \ desktop
    > 
    > ![](https://www.howtogeek.com/wp-content/uploads/2007/05/WindowsLiveWriter/HideRemoveableDriveIconsfromYourUbuntuDe_F982/010520071178057409601492898.png)
    > 
    > You should see a key in the right-hand pane called *volumes_visible*. Remove the checkbox from it, and the icons will instantly disappear from the desktop. Remember that you can always access the drives from the "Computer" icon, or easily in the file browser.


### ctrl+shift to change language

- [18.04 ctrl+shift to change language - Ask Ubuntu](https://askubuntu.com/questions/1029588/18-04-ctrlshift-to-change-language)

    > You can set such keyboard shortcut as follows:
    > 
    > On Ubuntu 18.04 LTS with GNOME desktop from GNOME Tweaks.
    > 
    > 1.  Install it
    > 
    >     ```
    >     sudo apt-get install gnome-tweaks
    > 
    >     ```
    > 
    > 2.  Then open GNOME Tweaks (`gnome-tweaks`).
    > 
    > 3.  Select *Keyboard & Mouse* tab
    > 4.  Click *Additional Layout Options* button
    > 5.  Expand *Switching to another layout*
    > 6.  Select `Ctrl` + `Shift` here
    > 
    > See screenshot below:
    > 
    > [![GNOME Tweaks - set <Ctrl+Shift>](https://i.stack.imgur.com/6eUtV.png)](https://i.stack.imgur.com/6eUtV.png)
    > 
    > Or simply:
    > 
    > ```
    > gsettings set org.gnome.desktop.input-sources xkb-options\
    > "['grp:ctrl_shift_toggle']"
    > 
    > ```
    > 
    > If you do not like `Super` + `Space` and `Shift`+`Super`+`Space` you can disable them with
    > 
    > ```
    > gsettings set org.gnome.desktop.wm.keybindings switch-input-source "['']"
    > gsettings set org.gnome.desktop.wm.keybindings switch-input-source-backward  "['']"
    > gsettings set org.freedesktop.ibus.general.hotkey triggers "['']"
    > 
    > ```

### GLib-GIO-Message: Using the 'memory' GSettings backend. Your settings will not be saved or shared with other applications.

- [ubuntu16.4 修改菜單到下方 錯誤：GLib-GIO-Message: Using the 'memory' GSettings backend. Your settings will not be saved or shared with other applications. - 掃文資訊](https://hk.saowen.com/a/ebbd364855b4987bcf2718a46b5045fb246b6ef0f5b72c5c8278e63bc09dd959)

    > 1.修改命令
    > 
    > #在終端輸入
    > gsettings set com.canonical.Unity.Launcher launcher-position Bottom
    > 
    > 2.如果遇錯
    > 
    > GLib-GIO-Message: Using the 'memory' GSettings backend.  Your settings will not be saved or shared with other applications.
    > 
    > 3.輸入命令，再執行上一步
    > 
    > export GIO_EXTRA_MODULES=/usr/lib/x86_64-linux-gnu/gio/modules/

### Switching between windows with scroll wheel on Ubuntu Dock

- [17.10 - Switching between windows with scroll wheel on Ubuntu Dock - Ask Ubuntu](https://askubuntu.com/questions/966887/switching-between-windows-with-scroll-wheel-on-ubuntu-dock)

    > Open Terminal and run
    > 
    > ```
    > gsettings set org.gnome.shell.extensions.dash-to-dock scroll-action 'cycle-windows'
    > 
    > ```

### show preview if multiple windows are opened and minimize if single window open.

- [How do I enable 'minimize on click' on Ubuntu dock in Ubuntu 17.10 and 18.04? - Ask Ubuntu](https://askubuntu.com/questions/960074/how-do-i-enable-minimize-on-click-on-ubuntu-dock-in-ubuntu-17-10-and-18-04)

    > use this command. it will show preview if multiple windows are opened and minimize if single window open.
    > 
    > ```
    > gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize-or-overview'
    > 
    > ```





## system init/systemd

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



### Upstart(new) vs System V initialization(old)

- [ubuntu 下为何没有/etc/inittab文件 linux下程序的启动流程 - CSDN博客](https://blog.csdn.net/yusiguyuan/article/details/9928139)

    > Linux 内核启动 init ，init进程ID是1，是所有进程的父进程，所有进程由它控制。
    > 
    > Ubuntu 的启动由upstart控制，自9.10后不再使用`/etc/event.d`目录的配置文件，改为`/etc/init`。
    > 
    > 查看当前的运行级别，Ubuntu 桌面默认是2。
    > 
    > 
    > 
    > ```sh
    > runlevel
    > ```
    > 
    > Ubuntu 的系统运行级别：
    > 
    > 
    > 
    > ```sh
    > 0       系统停机状态
    > 
    > 1       单用户或系统维护状态
    > 
    > 2~5     多用户状态
    > 
    > 6       重新启动
    > 
    > S
    > ```
    > 
    > 切换运行级别，执行命令：
    > 
    > 
    > 
    > ```sh
    > init [0123456Ss]
    > ```
    > 
    > 即在 init 命令后跟一个参数，此参数是要切换到的运行级的运行级代号，如：用 init 0 命令关机；用 init 6 命令重新启动。
    > 
    > 这就是我们的关机命令之一 $ sudo init 0  的由来:
    > 
    > 
    > 
    > ```sh
    > $ sudo init 0
    > ```
    > 
    > 查看系统当前运行等级：
    > 
    > 
    > 
    > ```sh
    > runlevel
    > ```
    > 
    > **查看系统在什么地方设置这个初始值，打开文件： （后面详细介绍为什么**
    > 
    > 
    > 
    > 
    > ```sh
    > $ nano /etc/init/rc-sysinit.conf
    > ```
    > 
    > **你会发现这么一句：**  
    > 
    > 
    > 
    > 
    > ```sh
    > # Default runlevel, this may be overriden on the kernel command-line
    > 
    > # or by faking an old /etc/inittab entry
    > 
    > env DEFAULT_RUNLEVEL=2
    > ```
    > 
    > Ubuntu init启动流程分析:
    > ==================
    > 
    > 现行的Linux distros主流的有两种init方式：一种是广为流传的System V initialization，它来源于Unix并且至今仍被各种Linux distros所采用；另一种是近几年提出的Upstart方式，基于事件机制，系统的所有服务，任务都是由事件驱动的。据我所知，采用后一种方式的目前有Ubuntu（6.10 and later），Fedora（9.10 and later），Debian（optional）。虽然采用Upstart的发行版并不多，但它旨在取代旧式的System V initialization。
    > 
    > 作为知识梳理，我现在就先在这里总结一下这两种方式各自的初始化流程，这也是为了方便整理思路：
    > 
    > 之前在查找Linux系统init流程的相关资料时总是能够看到inittab的身影，但是在我的Ubuntu上是没有这个文件的，到后来才知道采用 Upstart方式的Ubuntu上是没有inittab这个文件的。在旧式的System V initialization中，`/etc/inittab`可是个相当重要的文件。init进程启动后第一时间找的就是它！inittab负责初始化系统，设置系统runlevel及进 入各runlevel对应要执行的命令。假设当前inittab中设置的默认runlevle是5，则init会运行`/etc/init.d/rc 5`命令，该命令会依据系统服务的依赖关系遍历执行`/etc/rc5.d/中的脚本/`程序。进入`/etc/rc5.d`目录可以发现里面的文件都是到`/etc/init.d/下对应的脚本/`程序的软链接。以S开头的为启动的意思，以K开头的为停止。并且S/K后面的两位数数字代表了服务的启动顺序（由服务依赖关系决定）。
    > 
    > 【注】   网上查了一下， .d 文件的作用 ： .d代表目录即文件夹的意思。/etc是存放配置文件的目录，配置文件有的是单独的，有的是一类，通常单独的配置文件后缀是.conf，一类的配置文件放在一个目录中，目录名就叫XX.d，XX指的是哪方面的配置文件，比如init.d就存放有关linux启动的配置文件。
    > 
    > 那么Upstart job是怎么样的呢？我们知道，System V initializaiton是以runlevel为核心，依据服务间依赖关系的init方式，但在Upstart job，runlevel虽说对于服务的启动也有影响但已不是关键所在。Upstart job是事件驱动的，系统服务的启动、停止等等均是由事件决定的，反过来，系统服务的启动、停止也可以作为事件源触发其他服务。并且事件并不一定得由系统内部产生，用户可以手工的键入start/stop [Service]产生事件来启动/终止服务。`man upstart-evnets`查看upstart job所定义的事件，可以发现，runlevel也被当作事件来对待（因runlevel的改变而产生的事件），诸如此类还有其他如 startup，started，filesystem等等。那么系统服务又是如何知道自己应该什么时候启动，什么时候终止的呢？答案就在于`/etc /init`中（有的distros可能是在`/etc/event.d`）。进入`/etc/init`目录下一看，均是系统服务的配置文件，或者说，是job definition files。（实际上Upstart init只需要`/etc/init`这么一个目录，不像System V init，"拐弯抹脚"转好多圈才到达目的地，在性能上不如前者）。随便打开一个文件，比如`cron.conf`：
    > 
    > 
    > 
    > ```sh
    > # cron - regular background program processing daemon
    > 
    > #
    > 
    > # cron is a standard UNIX program that runs user-specified programs at
    > 
    > # periodic scheduled times
    > 
    > description "regular background program processing daemon"
    > 
    > start on runlevel [2345]
    > 
    > stop on runlevel [!2345]
    > 
    > expect fork
    > 
    > respawn
    > 
    > exec cron
    > ```
    > 
    > 相信敏锐的程序猿们都发现了：start on runlevel [2345]；stop on runlevel [！2345]
    > 
    > 没错，配置文件就是通过这个来设置服务何时启动，何时终止的。
    > 
    > 实际上并不仅仅在系统启动初期，在系统运转的任何时期都可以通过发送事件来启动或终止服务。这便是Upstart job的优点之一，除了用于系统初始化，还可以在系统运行阶段发挥作用。相比之下System V initialization方式下的配置文件一般只用于系统初始化阶段，当然系统运行阶段我们可以通过`/etc/init.d/Service start/stop/otherCommand`来操作服务，但很明显不如Upstart方式简洁明白。(如果你是linux 用户，你一定不陌生这些，一定很清楚。)
    > 
    > 好，介绍完System V initialization和Upstart，那么现在就能介绍Ubuntu init系统初始化流程。前面提过Ubuntu使用的是Upstart方式的initialization，其实不全然，考虑到6.10之前的版本采用的System V init及某些服务的需要，Ubuntu采用的是兼容模式，即：系统中既有System V-style启动的服务，也有Upstart启动的服务。如果你使用的是Ubuntu11.04（我目前PC上的系统），那么你可以看到系统中有这么几个目录：
    > 
    > 
    > 
    > ```sh
    > /etc/init
    > 
    > /etc/init.d
    > 
    > /etc/rc${runlevel}.d
    > ```
    > 
    > 作为两种init方式各自特征的`/etc/init.d`，`/etc/rc${runlevel}.d/`目录和`/etc/init`目录在Ubuntu中都有了，那么Ubuntu是如何实现兼容的？实际上，Ubuntu中并没有直接采用System V-style启动服务，要知道，Ubuntu中的init已被替换为Upstart init，而System V-style的服务是存放于`/etc/rc${runlevel}.d/`目录中的，（而`/etc/rc${runlevle}.d/`下的文件是到`/etc/init.d`的软链接）可Upstart init并不会直接跑到这里面去启动服务。它是通过间接调用来启动这类服务的。换句话说，Ubuntu中的init并不会直接奔着`/etc/init.d`或者`/etc/rc${runlevel}.d/`而去，它采用了折衷的办法，通过`/etc/init`下的某些配置文件调用`/etc/rc${runlevel}.d/`中的脚本以启动采用旧式System V-style的服务。（这是精髓）唉，说的我自己都觉得好绕，还是见实例吧，看下面。
    > 
    > 进入`/etc/init`目录（Upstart init会到该目录下读取配置文件），会发现几个跟rc有关的配置文件：
    > 
    > 
    > 
    > ```sh
    > rc.conf
    > 
    > rc-sysinit.conf
    > 
    > rcS.conf
    > ```
    > 
    > `rc-sysinit`在startup事件发生时被启动，rc在系统runlevel变化时被启动，rcS在系统runlevel为S时启动。在配置文件的注释中说明了，这几个文件，正是Upstart init处理System V-style服务的关键。
    > 
    > `rc-sysinit`在startup事件发生时被启动，即，Upstart init会首先读取`rc-sysinit.conf`并执行相关配置和脚本。`rc-sysinit.conf`的主要工作是设置系统默认runlevel，检测是否存在`/etc/inittab`或内核命令行，若存在，则按内核命令行>`/etc/inittab`>默认runlevel的顺序设置系统 runlevel。最后，调用`telinit`进入设置的runlevel。
    > 
    > 由于调用了`telinit`进入了设定的runlevel，runlevel改变的事件发生，此时rc服务启动（当然其他服务也会）。那么，我们就有必要来看看`rc.conf`中到底有什么东西。打开`rc.conf`，注意到最后一行：
    > 
    > 
    > 
    > ```sh
    > exec /etc/init.d/rc $RUNLEVEL
    > ```
    > 
    > 是不是感觉`/etc/init.d/rc`很熟悉，没错，在System V initialization中，`/etc/inittab`中的各runlevel对应的命令行就是通过这种形式设置的。
    > 
    > 很明显，`/etc/init.d/rc`被调用了，并且传入了早前设置好的系统runlevel作为参数。而`/etc/init.d/rc`会根据传入 的runlevel参数调用`/etc/rc${runlevel}.d/`下的脚本（以S开头）以启动服务，终止在前次runlevel启动而当前在 runlevel需要终止的服务。至此，Ubuntu处理System V-style服务的流程是不是渐渐明朗了。通过rc-sysinit和rc间接的调用`/etc/init.d/rc`从而启动System V-style服务，Ubuntu在采用新式Upstart init照顾了旧式的System V init。
    > 
    > 采用Upstart方式启动的服务则在`/etc/init/`目录中有属于自己的一份配置文件，终端下键入：`initctl list`，看看列出的服务是否同`/etc/init/`下的服务完全一致！

### start a Docker container with systemd

- [How to start a Docker container at boot time | Luis Toubes](https://toub.es/2017/08/08/how-to-start-a-docker-container-at-boot-time/)

    > Init system
    > -----------
    > 
    > There maybe times when other services depend on your Docker containers, in these cases it's much better to use the init system from your operating system. Steps below are **useful for Linux users** using `systemd` as their init system. Nowadays [systemd](https://en.wikipedia.org/wiki/Systemd) is one of the most popular init systems; Debian, Ubuntu, Raspbian, Arch, Red Hat and many other distributions are using it.
    > 
    > I will try not to go into much detail, since there are many articles describing how to use `systemd`, I'm just going to document a couple examples about how you can boot a Docker container using `systemd`.
    > 
    > For more information about `systemd` I suggest you check out these links:
    > 
    > -   [Managing services with Systemd](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/chap-Managing_Services_with_systemd.html)
    > -   [How to use systemctl to Manage Systemd services and units](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)
    > 
    > ### Step 1 - Create file rpi-agario.service
    > 
    > Assuming that we want **to start** previous **Agario container** using `systemd` and this container **already exists** in your host and is called `my-agario-server`, create a file named `rpi-agario.service` and include following code:
    > 
    > 
    > ```sh
    > [Unit]
    > Description=My Agario Server
    > Requires=docker.service
    > After=docker.service
    > 
    > [Service]
    > #Restart=always
    > ExecStart=/usr/bin/docker start -a my-agario-server
    > ExecStop=/usr/bin/docker stop -t 2 my-agario-server
    > 
    > [Install]
    > WantedBy=default.target
    > ```
    > 
    > 
    > It looks straightforward, isn't it?. `ExecStart` (Line 8) and `ExecStop` (Line 9) are the directives in charge to start and stop the container.
    > 
    > Line 7 is commented out, because I don't want `systemd` restart the service in any case but you could pass values like "always", "on-success", "on-failure", "on-abnormal", "on-abort", or "on-watchdog" and these will trigger a restart according to the way that the service was stopped.
    > 
    > ### Step 2 - Make systemd see your service
    > 
    > Copy file from step 1 in `/etc/systemd/system/` and give execution rights to the file.
    > 
    > Now you are going to be able of:
    > 
    > -   Enable the service on boot
    > 
    > 
    > ```sh
    > sudo systemctl enable rpi-agario
    > ```
    > 
    > 
    > -   Check current status
    > 
    > 
    > ```sh
    > sudo systemctl status rpi-agario
    > ```
    > 
    > 
    > -   Disable the service from boot
    > 
    > 
    > ```sh
    > sudo systemctl disable rpi-agario
    > ```
    > 
    > 
    > ### Aha Moment
    > 
    > An important point to notice from previous init file is the `-a flag` in `ExecStart` directive, it took me a few hours to realize what was the problem before the Aha Moment.
    > 
    > According to Docker help, `-a` or `--attach` will attach STDOUT/STDERR and forward signals, if you don't include this flag Docker is going to start the container through `ExecStart` and it will send a success signal, then `systemd` will interpret this signal as the process has successfully completed and it will proceed to call `ExecStop` and maybe your face will be like mine face during some minutes.
    > 
    > [![systemd beauty](https://toub.es/assets/memes/confused.jpg)](https://toub.es/assets/memes/confused.jpg)
    > 
    > So be aware, always remember to attach consoles and forward signals on the `ExecStart` directive.
    > 
    > ### Scripts at start up
    > 
    > As a final note, if you want to execute scripts instead of docker containers it would be useful directives **`type=oneshot`** and **`remainafterexit=yes`**.
    > 
    > These directives will inform to systemd that the script shall be considered active even when all its processes exited. For instance, I have configured a script to mount some encrypted folders and turn on a nextcloud container, this is how it looks the service descriptor.
    > 
    > 
    > ```sh
    > [Unit]
    > Description=NextCloud Secure Drive mount
    > Requires=docker.service
    > After=network-online.target docker.service
    > 
    > [Service]
    > Type=oneshot
    > ExecStart=/home/pi/laboratory/geheim/secure-mount.sh
    > RemainAfterExit=yes
    > ExecStop=/home/pi/laboratory/geheim/secure-unmount.sh
    > 
    > [Install]
    > WantedBy=multi-user.target
    > ```
    > 
    > 
    > I hope these notes are useful to someone in the world!


## cron job

### Cronjob for rebooting everyday

- [scheduled - How can I schedule a nightly reboot? - Ask Ubuntu](https://askubuntu.com/questions/13730/how-can-i-schedule-a-nightly-reboot)

    > I'd use cron (should already be installed):
    > 
    > Edit crontab:
    > 
    > ```
    > sudo crontab -e
    > 
    > ```
    > 
    > The first time you might have to choose your preferred editor (like nano)
    > 
    > Insert a line like
    > 
    > ```
    > 0 4   *   *   *    /sbin/shutdown -r +5
    > 
    > ```
    > 
    > at the bottom. Explanation:
    > 
    > ```
    > m      h    dom        mon   dow       command
    > minute hour dayOfMonth Month dayOfWeek commandToRun
    > 
    > ```
    > 
    > so the line
    > 
    > ```
    >   0 4   *   *   *    /sbin/shutdown -r +5
    > 
    > ```
    > 
    > would reboot your system every day at 4:05am. *(4:00am + 5 minutes)*
    > 
    > `Ctrl`+`X`, `Y`, `Enter` should get you out of crontab (if using nano)
    > 
    > Note: you might have to run `crontab -e` as root, because shutdown needs root.



### Can I set fsck as a cron job

- [Can I set fsck as a cron job? : linux4noobs](https://www.reddit.com/r/linux4noobs/comments/13m50t/can_i_set_fsck_as_a_cron_job/)


    > Running fsck on a mounted filesystem isn't a good idea; it can report false positives, miss actual problems and, worst of all, actually cause corruption. So you'd have to unmount your filesystems, run fsck, then re-mount them, which would be quite troublesome for /. You could force a fsck on next reboot (touch /forcefsck) and reboot in your cron job.
    > 
    > Instead, consider using a proper, mature journalled filesystem, like xfs, which never requires a fsck.
    > 
    > Anyway, what are you trying to accomplish? There are servers out there that have years of uptime, never run fsck and are quite happy. Running fsck pro-actively is never justified, it just increases hard-disk wear.
    > 
    > If you feel that your file system is corrupting while under normal operation, then you've got a serious problem with your system, be it hardware or software; fsck isn't going to help.
    > 
    > ---
    > 
    > What you've got there is a failing disk drive. Re-mapping the bad blocks is fine and dandy but doesn't cure the problem, just side-steps it. That drive needs to be replaced.


