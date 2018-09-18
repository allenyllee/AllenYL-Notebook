# Linux__問題排解1-2

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

## mount/umount

### mount option

- [mount(8): mount filesystem - Linux man page](https://linux.die.net/man/8/mount)

    > **atime**
    > 
    > Do not use noatime feature, then the inode access time is controlled by kernel defaults. See also the description for **strictatime** and **relatime** mount options.
    > 
    > **noatime**
    > 
    > Do not update inode access times on this filesystem (e.g, for faster access on the news spool to speed up news servers).
    > 
    > **auto**
    > 
    > Can be mounted with the **-a** option.
    > 
    > **noauto**
    > 
    > Can only be mounted explicitly (i.e., the **-a** option will not cause the filesystem to be mounted).
    > 
    > **defaults**
    > 
    > Use default options: **rw**, **suid**, **dev**, **exec**, **auto**, **nouser**, **async**, and **relatime.**
    > 
    > **dev**
    > 
    > Interpret character or block special devices on the filesystem.
    > 
    > **nodev**
    > 
    > Do not interpret character or block special devices on the file system.
    > 
    > **exec**
    > 
    > Permit execution of binaries.
    > 
    > **noexec**
    > 
    > Do not allow direct execution of any binaries on the mounted filesystem. (Until recently it was possible to run binaries anyway using a command like /lib/ld*.so /mnt/binary. This trick fails since Linux 2.4.25 / 2.6.0.)
    > 
    > **suid**
    > 
    > Allow set-user-identifier or set-group-identifier bits to take effect.
    > 
    > **nosuid**
    > 
    > Do not allow set-user-identifier or set-group-identifier bits to take effect. (This seems safe, but is in fact rather unsafe if you have **suidperl**(1) installed.)
    > 
    > **remount**
    > 
    > Attempt to remount an already-mounted filesystem. This is commonly used to change the mount flags for a filesystem, especially to make a readonly filesystem writeable. It does not change device or mount point.
    > 
    > The remount functionality follows the standard way how the mount command works with options from fstab. It means the mount command doesn't read fstab (or mtab) only when a *device* and *dir* are fully specified.
    > ```
    > mount -o remount,rw /dev/foo /dir
    > ```
    > After this call all old mount options are replaced and arbitrary stuff from fstab is ignored, except the loop= option which is internally generated and maintained by the mount command.
    > ```
    > mount -o remount,rw /dir
    > ```
    > After this call mount reads fstab (or mtab) and merges these options with options from command line ( **-o** ).
    > 
    > **user**
    > 
    > Allow an ordinary user to mount the filesystem. The name of the mounting user is written to mtab so that he can unmount the filesystem again. This option implies the options **noexec**, **nosuid**, and **nodev** (unless overridden by subsequent options, as in the option line **user,exec,dev,suid**).
    > 
    > **nouser**
    > 
    > Forbid an ordinary (i.e., non-root) user to mount the filesystem. This is the default.
    > 

- [mount - Can't execute a file with execute permission bit set - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/102812/cant-execute-a-file-with-execute-permission-bit-set)

    > If you use `user` and want to have executable files, use `user,exec`.


### bind mount

- [14.04 - How to make mount --bind permanent? - Ask Ubuntu](https://askubuntu.com/questions/550348/how-to-make-mount-bind-permanent)

    > The easiest way is to *mount --bind* what you need like
    > 
    > ```
    > mount --bind /home/sda1/Windows/Users/Me/Dropbox ~/Dropbox
    > 
    > ```
    > 
    > Then open *mtab*
    > 
    > ```
    > sudo nano /etc/mtab
    > 
    > ```
    > 
    > Copy your line like
    > 
    > ```
    > /home/sda1/Windows/Users/Me/Dropbox /home/me/Dropbox none rw,bind 0 0
    > 
    > ```
    > 
    > and paste it in *fstab* so it would mount on reboot
    > 
    > ```
    > sudo nano /etc/fstab
    > 
    > ```
    > 
    > If you folder is on mounted disk make sure your binding line comes after disk mount



- [filesystems - What is a bind mount? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/198590/what-is-a-bind-mount/198591)

    > What is a bind mount?
    > ---------------------
    > 
    > A *bind mount* is an alternate view of a directory tree. Classically, mounting creates a view of a storage device as a directory tree. A bind mount instead takes an existing directory tree and replicates it under a different point. The directories and files in the bind mount are the same as the original. Any modification on one side is immediately reflected on the other side, since the two views show the same data.
    > 
    > 
    > Unlike a hard link or symbolic link, a bind mount doesn't affect what is stored on the filesystem. It's a property of the live system.
    > 
    > ---
    > 
    > How do I create a bind mount?
    > -----------------------------
    > 
    > ### bindfs
    > 
    > The [`bindfs`](http://bindfs.org/) filesystem is a [FUSE](http://en.wikipedia.org/wiki/Filesystem_in_Userspace) filesystem which creates a view of a directory tree. For example, the command
    > 
    > ```
    > bindfs /some/where /else/where
    > 
    > ```
    > 
    > makes `/else/where` a mount point under which the contents of `/some/where` are visible.
    > 
    > Since bindfs is a separate filesystem, the files `/some/where/foo` and `/else/where/foo` appear as different files to applications (the bindfs filesystem has its own `st_dev` value). Any change on one side is "magically" reflected on the other side, but the fact that the files are the same is only apparent when one knows how bindfs operates.
    > 
    > Bindfs has no knowledge of mount points, so if there is a mount point under `/some/where`, it appears as just another directory under `/else/where`. Mounting or unmounting a filesystem underneath `/some/where` appears under `/else/where` as a change of the corresponding directory.
    > 
    > ---
    > 
    > ### Linux bind mount
    > 
    > Under Linux, bind mounts are available as a kernel feature. You can create one with the [`mount`](http://man7.org/linux/man-pages/man8/mount.8.html) command, by passing either the `--bind` command line option or the `bind` mount option. The following two commands are equivalent:
    > 
    > ```
    > mount --bind /some/where /else/where
    > mount -o bind /some/where /else/where
    > 
    > ```
    > 
    > Here, the "device" `/some/where` is not a disk partition like in the case of an on-disk filesystem, but an existing directory. The mount point `/else/where` must be an existing directory as usual. Note that no filesystem type is specified either way: making a bind mount doesn't involve a filesystem driver, it copies the kernel data structures from the original mount.
    > 
    > ---
    > 
    > If there are mount points under `/some/where`, their contents are not visible under `/else/where`. Instead of `bind`, you can use `rbind`, also replicate mount points underneath `/some/where`. For example, if `/some/where/mnt` is a mount point then
    > 
    > ```
    > mount --rbind /some/where /else/where
    > 
    > ```
    > 
    > is equivalent to
    > 
    > ```
    > mount --bind /some/where /else/where
    > mount --bind /some/where/mnt /else/where/mnt
    > 
    > ```
    > 
    > ---
    > 
    > It is possible to have different mount options in two bind-mounted directories. There is a quirk, however: making the bind mount and setting the mount options cannot be done atomically, they have to be two successive operations. (Older kernels did not allow this.) For example, the following commands create a read-only view, but there is a small window of time during which `/else/where` is read-write:
    > 
    > ```
    > mount --bind /some/where /else/where
    > mount -o remount,ro,bind /else/where
    > 
    > ```
    > 
    > ---
    > 
    > ### Read-only view
    > 
    > It can be useful to create a read-only view of a filesystem, either for security reasons or just as a layer of safety to ensure that you won't accidentally modify it.
    > 
    > With bindfs:
    > 
    > ```
    > bindfs -r /some/where /mnt/readonly
    > 
    > ```
    > 
    > With Linux, the simple way:
    > 
    > ```
    > mount --bind /some/where /mnt/readonly
    > mount -o remount,ro,bind /mnt/readonly
    > 
    > ```
    > 
    > This leaves a short interval of time during which `/mnt/readonly` is read-write. If this is a security concern, first create the bind mount in a directory that only root can access, make it read-only, then move it to a public mount point. In the snippet below, note that it's important that `/root/private` (the directory above the mount point) is private; the original permissions on `/root/private/mnt` are irrelevant since they are hidden behind the mount point.
    > 
    > ```
    > mkdir -p /root/private/mnt
    > chmod 700 /root/private
    > mount --bind /some/where /root/private/mnt
    > mount -o remount,ro,bind /root/private/mnt
    > mount --move /root/private/mnt /mnt/readonly
    > 
    > ```
    > 
    > ---
    > 
    > ### Mounting in a jail
    > 
    > A [chroot jail](http://en.wikipedia.org/wiki/Chroot) runs a process in a subtree of the system's directory tree. This can be useful to run a program with restricted access, e.g. run a network server with access to only its own files and the files that it serves, but not to other data stored on the same computer). A limitation of chroot is that the program is confined to one subtree: it can't access independent subtrees. Bind mounts allow grafting other subtrees onto that main tree.
    > 
    > For example, suppose that a machine runs a service `/usr/sbin/somethingd` which should only have access to data under `/var/lib/something`. The smallest directory tree that contains both of these files is the root. How can the service be confined? One possibility is to make hard links to all the files that the service needs (at least `/usr/sbin/somethingd` and several shared libraries) under `/var/lib/something`. But this is cumbersome (the hard links need to be updated whenever a file is upgraded), and doesn't work if `/var/lib/something` and `/usr` are on different filesystems. A better solution is to create an ad hoc root and populate it with using mounts:
    > 
    > ```
    > mkdir /run/something
    > cd /run/something
    > mkdir -p etc/something lib usr/lib usr/sbin var/lib/something
    > mount --bind /etc/something etc/something
    > mount --bind /lib lib
    > mount --bind /usr/lib usr/lib
    > mount --bind /usr/sbin usr/sbin
    > mount --bind /var/lib/something var/lib/something
    > mount -o remount,ro,bind etc/something
    > mount -o remount,ro,bind lib
    > mount -o remount,ro,bind usr/lib
    > mount -o remount,ro,bind usr/sbin
    > chroot . /usr/sbin/somethingd &
    > 
    > ```
    > 
    > Linux's [mount namespaces](http://lwn.net/2001/0301/a/namespaces.php3) generalize chroots. Bind mounts are how namespaces can be populated in flexible ways. See [Making a process read a different file for the same filename](https://unix.stackexchange.com/questions/81003/making-a-process-read-a-different-file-for-the-same-filename) for an example.
    > 
    > ---
    > 
    > ### Running a different distribution
    > 
    > Another use of chroots is to install a different distribution in a directory and run programs from it, even when they require files at hard-coded paths that are not present or have different content on the base system. This can be useful, for example, to install a 32-bit distribution on a 64-bit system that doesn't support mixed packages, to install older releases of a distribution or other distributions to test compatibility, to install a newer release to test the latest features while maintaining a stable base system, etc. See [How do I run 32-bit programs on a 64-bit Debian/Ubuntu?](https://unix.stackexchange.com/questions/12956/how-do-i-run-32-bit-programs-on-a-64-bit-debian-ubuntu) for an example on Debian/Ubuntu.
    > 
    > Suppose that you have an installation of your distribution's latest packages under the directory `/f/unstable`, where you run programs by switching to that directory with `chroot /f/unstable`. To make home directories available from this installations, bind mount them into the chroot:
    > 
    > ```
    > mount --bind /home /f/unstable/home
    > 
    > ```
    > 
    > The program [schroot](https://packages.debian.org/jessie/schroot) does this automatically.
    > 
    > ---
    > 
    > ### Accessing files hidden behind a mount point
    > 
    > When you mount a filesystem on a directory, this hides what is behind the directory. The files in that directory become inaccessible until the directory is unmounted. Because BSD nullfs and Linux bind mounts operate at a lower level than the mount infrastructure, a nullfs mount or a bind mount of a filesystem exposes directories that were hidden behind submounts in the original.
    > 
    > For example, suppose that you have a tmpfs filesystem mounted at `/tmp`. If there were files under `/tmp` when the tmpfs filesystem was created, these files may still remain, effectively inaccessible but taking up disk space. Run
    > 
    > ```
    > mount --bind / /mnt
    > 
    > ```
    > 
    > (Linux) or
    > 
    > ```
    > mount -t nullfs / /mnt
    > 
    > ```
    > 
    > (FreeBSD) to create a view of the root filesystem at `/mnt`. The directory `/mnt/tmp` is the one from the root filesystem.
    > 
    > ---
    > 
    > Side effects of bind mounts
    > ---------------------------
    > 
    > ### Recursive directory traversals
    > 
    > If you use bind mounts, you need to take care of applications that traverse the filesystem tree recursively, such as backups and indexing (e.g. to build a [locate](http://en.wikipedia.org/wiki/Locate_(Unix)) database).
    > 
    > Usually, bind mounts should be excluded from recursive directory traversals, so that each directory tree is only traversed once, at the original location. With bindfs and nullfs, configure the traversal tool to ignore these filesystem types, if possible. Linux bind mounts cannot be recognized as such: the new location is equivalent to the original. With Linux bind mounts, or with tools that can only exclude paths and not filesystem types, you need to exclude the mount points for the bind mounts.
    > 
    > Traversals that stop at filesystem boundaries (e.g. `find -xdev`, `rsync -x`, `du -x`, ...) will automatically stop when they encounter a bindfs or nullfs mount point, because that mount point is a different filesystem. With Linux bind mounts, the situation is a bit more complicated: there is a filesystem boundary only if the bind mount is grafting a different filesystem, not if it is grafting another part of the same filesystem.
    > 
    > 



### loop device

- [loop device介绍及losetup使用-秋天的童话-51CTO博客](http://blog.51cto.com/wushank/1212647)

    > 一、**loop 设备介绍**\
    > 1、 在类 UNIX 系统里，loop设备是一种伪设备(pseudo-device)，或者也可以说是仿真设备。它能使我们像块设备一样访问一个文件。在使用之前，一个 loop设备必须要和一个文件进行连接。这种结合方式给用户提供了一个替代块特殊文件的接口。因此，如果这个文件包含有一个完整的文件系统，那么这个文件就可以像一个磁盘设备一样被mount 起来。
    > 
    >   上面说的文件格式，我们经常见到的是 CD 或 DVD 的 ISO 光盘镜像文件或者是软盘(硬盘)的 *.img镜像文件。通过这种 loop mount (回环mount)的方式，这些镜像文件就可以被 mount到当前文件系统的一个目录下。\
    >   
    >    至 此，顺便可以再理解一下 loop之含义：对于第一层文件系统，它直接安装在我们计算机的物理设备之上；而对于这种被 mount起来的镜像文件(它也包含有文件系统)，它是建立在第一层文件系统之上，这样看来，它就像是在第一层文件系统之上再绕了一圈的文件系统，所以称为loop。
    > 
    >  2、在 Linux 里，loop 设备的设备名形如：
    >  
    > ```
    >      ls /dev/loop*
    > 
    >           /dev/loop0  /dev/loop2 /dev/loop4  /dev/loop6
    > 
    >           /dev/loop1  /dev/loop3 /dev/loop5  /dev/loop7
    > 
    >               ... ...
    > ```
    > 例如，要在一个目录下 mount 一个包含有磁盘镜像的文件，需要分 2 步走：
    > 
    > losetup /dev/loop0  disk.img #使磁盘镜像文件与循环设备连结起来
    > 
    > mount /dev/loop0   /home/groad/disk_test #将循环设备 mount 到目录 disk_test下\
    > 
    >    经过上面的两个命令后，镜像文件就如同一个文件系统挂载在 disk_test目录下，当然我们也可以往镜像里面添加文件。其实上面的两个步骤可以写成一个步骤：
    > 
    >    mount -t minix -o loop./disk.img ./disk_test\
    >       其 中，加了 -o loop 指定后，那么也就相当于执行了第一行的 losetup 命令。
    > 
    >   最后，要卸载的话，就直接 umount /dev/loop0 即可。
    > 
    > 二、**完整测试实例**
    > 
    > **     1. 首先创建一个 1G 大小的空文件**：
    > 
    >            # dd if=/dev/zeroof=loopfile.img bs=1G count=1
    > 
    >               1+0 records in
    > 
    >               1+0 records out
    > 
    >               1073741824 bytes (1.1 GB) copied, 69.3471 s, 15.5 MB/s
    > 
    >  **2\. 对该文件格式化为 ext4 格式**：
    > ```shell
    > # mkfs.ext4    loopfile.img
    > ```
    > > mke2fs 1.41.11 (14-Mar-2010)\
    > > loopfile.img is not a block special device.\
    > > Proceed anyway? (y,n) y\
    > > Filesystem label=\
    > > OS type: Linux\
    > > Block size=4096 (log=2)\
    > > Fragment size=4096 (log=2)\
    > > Stride=0 blocks, Stripe width=0 blocks\
    > > 65536 inodes, 262144 blocks\
    > > 13107 blocks (5.00%) reserved for the super user\
    > > First data block=0\
    > > Maximum filesystem blocks=268435456\
    > > 8 block groups\
    > > 32768 blocks per group, 32768 fragments per group\
    > > 8192 inodes per group\
    > > Superblock backups stored on blocks:\
    > > 32768,98304, 163840, 229376\
    > >\
    > > Writing inode tables:done\
    > > Creating journal (8192 blocks): done\
    > > Writing superblocks and filesystem accounting information:done\
    > >\
    > > This filesystem will be automatically checked every 38 mountsor\
    > > 180 days, whichever comesfirst. Use tune2fs -c or -i tooverride.
    > 
    >    **3\. 用 file 命令查看下格式化后的文件类型**：
    > 
    >          # file loopfile.img
    > 
    >              loopfile.img: Linux rev 1.0 ext4 filesystem data,UUID=a9dfb4a0-6653-4407-ae05-7044d92c1159 (extents) (large files)(huge files)
    > 
    >  **4\. 准备将上面的文件挂载起来**：
    > 
    >              # mkdir /mnt/loopback
    > 
    >              # mount -o loop loopfile.img /mnt/loopback\
    >       mount 命令的 -o loop 选项可以将任意一个 loopback 文件系统挂载。上面的 mount 命令实际等价于下面两条命令：
    > 
    >              # losetup /dev/loop0   loopfile.img
    > 
    >              # mount /dev/loop0    /mnt/loopback\
    >       因此实际上，mount -o loop 在内部已经默认的将文件和 /dev/loop0 挂载起来了。
    > 
    >        然而对于第一种方法(mount -oloop)并不能适用于所有的场景。比如，我们想创建一个硬盘文件，然后对该文件进行分区，接着挂载其中一个子分区，这时就不能用 -oloop 这种方法了。因此必须如下做：
    > 
    >          # losetup /dev/loop1   loopfile.img
    > 
    >          # fdisk /dev/loop1
    > 
    >  **6\. 卸载挂载点**
    > 
    >       # umount/mnt/loopback
    > 
    > **三、losetup介绍：**
    > 
    > losetup [ -e encryption ] [ -o offset ] loop_device file losetup [ -d ] loop_device\
    > 描 述：losetup 用 来 将 loop device 与 档 案 或 block device 联 结 、 分 离 . 以 及 查 询 loop device 目 前 的 状 况 , 如 只 给 定 loop_device 的 参 数 . 则 秀 出 loop device 目 前 的 状 况 .\
    > 选 项 ：\
    > -d  将某个档案或装制与loop装置分离\
    > -e encryption\
    > 启 动 资 料 编 码 . 下 列 为 可 用 的 选 项 参 数 :\
    > NONE  不 编 码 ( 定 义 值 ) .\
    > XOR  使 用 简 易 的 XOR 编 码\
    > DES 编 码 须 在 kernel 上 加 上 DES 编 码 功 能 . DES 编 码 是 利 用 启 始 值 做 为 密 码 保 护 来 防 止 他 人 用 字 典 功 击 法 破 解 .\
    > -o offset  资 料 开 启 时 资 料 平移(offset) 几 个 bytes 来 与 档 案 或 装 置 联 接 .
    > 
    > 举例：\
    >       If  you  are  using the loadable module you must have the module loaded\
    >       first with the command\
    >              # modprobe loop\
    >       Maybe also encryption modules are needed.\
    >              # modprobe des # modprobe cryptoloop\
    >       The following commands can be used as an  example  of  using  the  loop\
    >       device.\
    >              # dd if=/dev/zero of=/file bs=1k count=100\
    >              # losetup -e des /dev/loop0 /file\
    >              Password:\
    >              Init (up to 16 hex digits):\
    >              # mkfs -t ext2 /dev/loop0 100\
    >              # mount -t ext2 /dev/loop0 /mnt\
    >               ...\
    >              # umount /dev/loop0\
    >              # losetup -d /dev/loop0
    > 
    > **四、loop设备的参数调整：**
    > 
    > 如果需要超过8个loopdevice，那么使用losetup命令的时候可能会遇到类似的错误 'no suchdevice',这是因为超过了可用loopdevice设备的最大限制，依据你的Linux系统，可以通过修改
    > 
    > /etc/modprobe.conf
    > 
    > 配置文件，增加如下参数的方式进行扩展
    > 
    > options loopmax_loop=20 --比如我增加到20个
    > 
    > 保存退出，如果要了马上生效的话，可以通过
    > 
    > modprobe -vloop
    > 
    > 命令立即加载该模块。
    > ```
    > [root@vm11g dev]# cat /etc/modprobe.conf|greploop\
    > options loop max_loop=20
    > 
    > [root@vm11g dev]# modprobe -v loop\
    > insmod/lib/modules/2.6.9-42.0.0.0.1.ELsmp/kernel/drivers/block/loop.komax_loop=20\
    > 
    > [root@vm11g dev]# ls -ltr/dev/loop*\
    > brw-rw---- 1 root disk 7, 8 Jul 19 07:44 /dev/loop8\
    > brw-rw---- 1 root disk 7, 9 Jul 19 07:44 /dev/loop9\
    > brw-rw---- 1 root disk 7, 10 Jul 19 07:44 /dev/loop10\
    > brw-rw---- 1 root disk 7, 11 Jul 19 07:44 /dev/loop11\
    > brw-rw---- 1 root disk 7, 12 Jul 19 07:44 /dev/loop12\
    > brw-rw---- 1 root disk 7, 13 Jul 19 07:44 /dev/loop13\
    > brw-rw---- 1 root disk 7, 14 Jul 19 07:44 /dev/loop14\
    > brw-rw---- 1 root disk 7, 15 Jul 19 07:44 /dev/loop15\
    > brw-rw---- 1 root disk 7, 16 Jul 19 07:44 /dev/loop16\
    > brw-rw---- 1 root disk 7, 17 Jul 19 07:44 /dev/loop17\
    > brw-rw---- 1 root disk 7, 18 Jul 19 07:44 /dev/loop18\
    > brw-rw---- 1 root disk 7, 19 Jul 19 07:44 /dev/loop19\
    > brw-rw---- 1 root disk 7, 0 Jul 19 2009 /dev/loop0\
    > brw-rw---- 1 root disk 7, 1 Jul 19 2009 /dev/loop1\
    > brw-rw---- 1 root disk 7, 2 Jul 19 2009 /dev/loop2\
    > brw-rw---- 1 root disk 7, 3 Jul 19 2009 /dev/loop3\
    > brw-rw---- 1 root disk 7, 4 Jul 19 2009 /dev/loop4\
    > brw-rw---- 1 root disk 7, 5 Jul 19 2009 /dev/loop5\
    > brw-rw---- 1 root disk 7, 6 Jul 19 2009 /dev/loop6\
    > brw-rw---- 1 root disk 7, 7 Jul 19 2009/dev/loop7
    > ```
    > 有了这个东西,在Linux下就可以借助file来测试学习ASM了。
    > 


### umount when the device is busy

- [linux - Can't unmount a loop backed file but there's no open files? - Server Fault](https://serverfault.com/questions/58991/cant-unmount-a-loop-backed-file-but-theres-no-open-files)

    > I believe this is what [fuser](http://linux.die.net/man/1/fuser) is for. Specifically, `fuser -km /path/to/mount/point` - note that the `-k` flag kills processes with files open on this filesystem. You can omit this flag to see a list first.


- [How to umount when the device is busy | Something Odd!](https://odd.blog/2008/02/13/how-to-umount-when-the-device-is-busy/)

    > ```shell
    > # umount /media/disk/
    > umount: /media/disk: device is busy
    > umount: /media/disk: device is busy
    > ```
    > 
    > First thing you'll do will probably be to close down all your terminals and xterms but here's a better way. You can use the fuser command to find out which process was keeping the device busy:
    > 
    > ```shell
    > # fuser -m /dev/sdc1
    > /dev/sdc1: 538
    > # ps auxw|grep 538
    > donncha 538 0.4 2.7 219212 56792 ? SLl Feb11 11:25 rhythmbox
    > ```
    > 
    > Rhythmbox is the culprit! Close that down and umount the drive. Problem solved!
    > 

### mount VHD/VHDX by qemu

- [[ubuntu] How do you mount a VHD image](https://ubuntuforums.org/showthread.php?t=2299701)

    > Sorry about that simply install qemu-utils
    > 
    > ```sh
    > sudo apt-get install qemu-utils
    > ```
    > 
    > Now it says to Load the nbd kernel module. Yes, I'm serious, the network block device module! (Note: All of the following commands require superuser permissions, so escalate your privileges in whatever way makes you most comfortable.)
    > 
    > So that is done by
    > 
    > ```sh
    > sudo rmmod nbd sudo modprobe nbd max_part=16
    > ```
    > 
    > Then run qemu-nbd, which is a user space loopback block device server for QEMU-supported disk images. Basically, it knows all about weird disk image formats, and presents them to the kernel via nbd, and ultimately to the rest of the system as if they were a normal disk.
    > 
    > ```sh
    > qemu-nbd -c /dev/nbd0 <vdi-file>
    > ```
    > 
    > Of course you will need to replace <vdi-file> with your vdi name.
    > 
    > Then That command will expose the entire image as a block device named /dev/nbd0, and the partitions within it as subdevices. For example, the first partition in the image will appear as **/dev/nbd0p1.**
    > 
    > Now you could, for instance, run cfdisk on the block device, but **you will most likely want to mount an individual partition**.
    > 
    > 
    > ```sh
    > mount /dev/nbd0p1 /mnt
    > ```
    > 
    > Again changing if needed.
    > 
    > Now you should be able to move things in and out as he states.
    > 
    > And in his own words
    > 
    > Gadzooks! Now you can muck around inside the filesystem to your heart's content. Go ahead and copy stuff in or out, or if you're feeling fruity, have some chrooty: chroot /mnt.
    > And when you're done, unmount the filesystem and shut down the qemu-nbd service.
    > 
    > By way of
    > 
    > 
    > ```sh
    > umount /mnt
    > qemu-nbd -d /dev/nbd0
    > ```
    > 
    > ---
    > 
    > You can then mount the image with:
    > ```sh
    > sudo modprobe nbd max_part=16
    > sudo qemu-nbd -c /dev/nbd0 /path/to/vhdfile
    > sudo partprobe /dev/nbd0
    > sudo mount /dev/nbd0p1 /mnt/image
    > ```
    > 
    > Obviously you need to replace the path in red with the actual path to where the VHD image is located. Don't forget to unmount the image like you would as normal after you're done.
    > 
    > sudo umount /mnt/image
    > 




### mount vdi/vmdk/ova by qemu

- [How to mount a virtual hard disk? - Ask Ubuntu](https://askubuntu.com/questions/202571/how-to-mount-a-virtual-hard-disk)

    > You can also use qemu:
    > 
    > For `.vdi`
    > ----------
    > 
    > ```
    > sudo modprobe nbd
    > sudo qemu-nbd -c /dev/nbd1 ./linux_box/VM/image.vdi
    > 
    > ```
    > 
    > if they are not installe you can install them (on Ubuntu is this comand)
    > 
    > ```
    > sudo apt install qemu-utils
    > 
    > ```
    > 
    > and then mount it
    > 
    > ```
    > mount /dev/nbd1p1 /mnt
    > 
    > ```
    > 
    > For `.vmdk`
    > -----------
    > 
    > ```
    > sudo modprobe nbd
    > sudo qemu-nbd -r -c /dev/nbd1 ./linux_box/VM/image.vmdk
    > 
    > ```
    > 
    > notice tha I use the option `-r` that's because **VMDK version 3 must be read only** to be able to be mounted by qemu
    > 
    > and then I mount it
    > 
    > ```
    > mount /dev/nbd1p1 /mnt
    > 
    > ```
    > 
    > I use `nbd1` because `nbd0` sometimes gives 'mount: special device /dev/nbd0p1 does not exist'
    > 
    > For .ova
    > --------
    > 
    > ```
    > tar -tf image.ova
    > tar -xvf image.ova
    > 
    > ```
    > 
    > The above will extract the `.vmdk` disk and then mount that.

### Unable to mount NTFS partition

- [Unable to mount NTFS partition (no hibernation) - Ask Ubuntu](https://askubuntu.com/questions/748163/unable-to-mount-ntfs-partition-no-hibernation)

    > Run `sudo ntfsfix /dev/sda2` and you will be able to mount the partition.

- [Unable to mount Windows (NTFS) filesystem due to hibernation - Ask Ubuntu](https://askubuntu.com/questions/145902/unable-to-mount-windows-ntfs-filesystem-due-to-hibernation)

    > EDIT: **DOING THIS *MIGHT* HAVE DANGEROUS CONSEQUENCES** and Windows might fail to boot or corrupt the filesystem upon booting.
    > 
    > * * * * *
    > 
    > Use [ntfsfix](http://linux.die.net/man/8/ntfsfix) in the terminal, even if you can't access Windows
    > 
    > ```
    > sudo ntfsfix /dev/sdXY
    > 
    > ```
    > 
    > where XY is the partition, e.g. `a2` (`/dev/sda2`) or `b1` (`/dev/sdb1`)
    > 
    > ntfsfix repairs some fundamental NTFS inconsistencies, resets the NTFS journal file and schedules an NTFS consistency check for the first boot into Windows.



## partition

### 不重启的情况下重读分区

- [partprobe命令_Linux partprobe 命令用法详解：不重启的情况下重读分区](http://man.linuxde.net/partprobe)

    > **partprobe命令**用于重读分区表，当出现删除文件后，出现仍然占用空间。可以partprobe在不重启的情况下重读分区。
    > 
    > ### 语法
    > 
    > partprobe(选项)(参数)
    > 
    > ### 选项
    > 
    > -d：不更新内核；
    > -s：显示摘要和分区；
    > -h：显示帮助信息；
    > -v：显示版本信息。
    > 
    > ### 参数
    > 
    > 设备：指定需要确认分区表改变的硬盘对应的设备文件。
    > 
    > ### 实例
    > 
    > 使用partprobe不重启系统添加新的磁盘分区，主机自带硬盘超过300GB，目前只划分使用了3个主分区，不到70GB，如下：
    > ```sh
    > [root@localhost ~]# [df](http://man.linuxde.net/df "df命令") -h
    > Filesystem Size Used Avail Use% Mounted on
    > /dev/sda1 29G 3.7G  24G 14% /
    > /dev/sda2 29G  22G 5.2G 81% /oracle
    > tmpfs    2.0G    0 2.0G  0% /dev/shm
    > 
    > [root@localhost ~]# [cat](http://man.linuxde.net/cat "cat命令") /proc/partitions
    > major minor  #blocks  name
    > 
    >    8     0  311427072 sda
    >    8     1   30716248 sda1
    >    8     2   30716280 sda2
    >    8     3    8193150 sda3
    >    8    16     976896 sdb
    >    8    32     976896 sdc
    > 
    > ...省略其他
    > ```
    > 
    > 现在需要给系统添加1个100GB的空间存放数据文件，而又不影响现有系统上业务的运行，使用[fdisk](http://man.linuxde.net/fdisk "fdisk命令")结合partprobe命令不重启系统添加一块新的磁盘分区。操作步骤如下：
    > 
    > **第1步 添加新的磁盘分区**：
    > ```sh
    > [root@localhost ~]# fdisk /dev/sda
    > The number of cylinders for this disk is [set](http://man.linuxde.net/set "set命令") to 38770.
    > There is nothing wrong with that, but this is larger than 1024,
    > and could in certain setups cause problems with:
    > 1) software that runs [at](http://man.linuxde.net/at "at命令") boot [time](http://man.linuxde.net/time "time命令") (e.g., old versions of [lilo](http://man.linuxde.net/lilo "lilo命令"))
    > 2) booting and partitioning software from other OSs
    >    (e.g., DOS FDISK, OS/2 FDISK)
    > 
    > [command](http://man.linuxde.net/command "command命令") (m for [help](http://man.linuxde.net/help "help命令")): p
    > 
    > Disk /dev/sda: 318.9 GB, 318901321728 bytes
    > 255 heads, 63 sectors/track, 38770 cylinders
    > Units = cylinders of 16065 * 512 = 8225280 bytes
    > 
    >    Device Boot      Start         End      Blocks   [id](http://man.linuxde.net/id "id命令")  System
    > /dev/sda1   *           1        3824    30716248+  83  Linux
    > /dev/sda2            3825        7648    30716280   83  Linux
    > /dev/sda3            7649        8668     8193150   82  Linux swap / Solaris
    > 
    > Command (m for help): n
    > Command action
    >    e   extended
    >    p   primary partition (1-4)
    > p
    > Selected partition 4
    > First cylinder (8669-38770, default 8669):
    > Using default value 8669
    > [last](http://man.linuxde.net/last "last命令") cylinder or +size or +sizeM or +sizeK (8669-38770, default 38770): +100G
    > Command (m for help): [w](http://man.linuxde.net/w "w命令")
    > The partition table has been altered!
    > 
    > Calling ioctl() to re-[read](http://man.linuxde.net/read "read命令") partition table.
    > 
    > WARNING: Re-reading the partition table failed with error 16:
    > 
    > Device or resource busy.
    > The kernel still uses the old table.
    > The new table will be used at the next [reboot](http://man.linuxde.net/reboot "reboot命令").
    > Syncing disks.
    > ```
    > 
    > **第2步 使用工具partprobe让kernel读取分区信息：**
    > ```sh
    > [root@localhost ~]# partprobe
    > ```
    > 
    > 使用fdisk工具只是将分区信息写到磁盘，如果需要[mkfs](http://man.linuxde.net/mkfs "mkfs命令")磁盘分区则需要重启系统，而使用partprobe则可以使kernel重新读取分区信息，从而避免重启系统。
    > 
    > **第3步 格式化文件系统：**
    > ```
    > [root@localhost ~]# mkfs.ext3 /dev/sda4
    > [mke2fs](http://man.linuxde.net/mke2fs "mke2fs命令") 1.39 (29-May-2006)
    > Filesystem label=
    > OS [type](http://man.linuxde.net/type "type命令"): Linux
    > Block size=4096 (log=2)
    > Fragment size=4096 (log=2)
    > 12222464 inodes, 24416791 blocks
    > 1220839 blocks (5.00%) reserved for the super user
    > First data block=0
    > Maximum filesystem blocks=4294967296
    > 746 block [groups](http://man.linuxde.net/groups "groups命令")
    > 32768 blocks per group, 32768 fragments per group
    > 16384 inodes per group
    > Superblock backups stored on blocks:
    >         32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632,
    > 　　　　2654208, 4096000, 7962624, 11239424, 20480000, 23887872
    > 
    > Writing inode tables: done
    > Creating journal (32768 blocks): done
    > Writing superblocks and filesystem accounting information:
    > 
    > done
    > 
    > This filesystem will be automatically checked every 26 mounts or
    > 180 days, whichever comes first.  Use [tune2fs](http://man.linuxde.net/tune2fs "tune2fs命令") -c or -i to override.
    > [root@localhost ~]#
    > ```
    > 
    > **第4步 [mount](http://man.linuxde.net/mount "mount命令")新的分区`/dev/sda4`：**
    > ```sh
    > [root@localhost ~]# [e2label](http://man.linuxde.net/e2label "e2label命令")  /dev/sda4 /data
    > [root@localhost ~]# [mkdir](http://man.linuxde.net/mkdir "mkdir命令") /data
    > [root@localhost ~]# mount /dev/sda4 /data
    > [root@localhost ~]# df
    > Filesystem           1K-blocks      Used Available Use% Mounted on
    > /dev/sda1             29753556   3810844  24406900  14% /
    > /dev/sda2             29753588  11304616  16913160  41% /oracle
    > tmpfs                  2023936         0   2023936   0% /dev/shm
    > /dev/sda4             96132968    192312  91057300   1% /data
    > ```
    > 
    > 使用partprobe可以不用重启系统即可配合fdisk工具创建新的分区。



## system init

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








