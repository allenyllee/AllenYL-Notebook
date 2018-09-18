# Linux__問題排解3-1

[toc]
<!-- toc --> 


## bash

### remove file with progress bar

- [Is it possible to determine the progress of an rm command? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/255190/is-it-possible-to-determine-the-progress-of-an-rm-command)

    > This is the command
    > 
    > ```shell
    > rm -rv DIR_OR_FILE_NAME | pv -l -s $( du -a DIR_OR_FILE_NAME | wc -l ) > /dev/null
    > ```
    > 
    > If you need root permissions for the dir or file to delete,
    > 
    > ```shell
    > sudo rm -rv DIR_OR_FILE_NAME | pv -l -s $( sudo du -a DIR_OR_FILE_NAME | wc -l ) > /dev/null
    > ```
    > 
    > -   `rm -rv`: `-r` to recursively remove DIRs and files. `-v` verbose it lists all the files and directories that is removing.
    > 
    > -   `pv -l -s`: `-l` to count lines instead of bytes. `-s` set the total lines to be removed.
    > 
    > -   `$( du -a <dir_or_file> | wc -l )`: `du -a` returns a list all files and directories from the dir specified. `wc -l` returns the count of lines outputted by `du -a`.
    > 
    > -   `> /dev/null`: send the output of `rm -rv` to nowhere.
    > 
    > ---
    > 
    > Good idea.  This may give an incorrect file/directory count if any names contain newlines; `find {dir} -printf . | wc -c` would be safer (but `-printf` is a GNU extension).
    > 
    > ---
    > 
    > Also you can add `pv` between `du -a` and `wc -l` to get the progress of cunting files
    > ```shell
    > sudo rm -rv DIR_OR_FILE_NAME | pv -l -s $( sudo du -a DIR_OR_FILE_NAME | pv | wc -l ) > /dev/null
    > ```
    > 
    > [name=Ya-Lun Li]




### du

- [【系統】使用 du 來看磁碟的使用空間 @ My Life :: 隨意窩 Xuite日誌](http://blog.xuite.net/chingwei/blog/32566618-%E3%80%90%E7%B3%BB%E7%B5%B1%E3%80%91%E4%BD%BF%E7%94%A8+du+%E4%BE%86%E7%9C%8B%E7%A3%81%E7%A2%9F%E7%9A%84%E4%BD%BF%E7%94%A8%E7%A9%BA%E9%96%93)

    > 下圖是直接執行 du ，資料很多，而且子目錄下的所有檔案都會列出來，看得很累~~不好用
    > 
    > **du**\
    > ![](http://3.blog.xuite.net/3/8/3/1/11851958/blog_1028365/txt/32566618/1.png)
    > 
    > 所以我們設定，最多只顯示一層，清楚多了。但 Size 預設是 K ，有點小
    > 
    > **du --max-depth=1**\
    > ![](http://3.blog.xuite.net/3/8/3/1/11851958/blog_1028365/txt/32566618/2.png)
    > 
    > 加上 -B M ，表示使用 MB來顯示，如果是加 G ，就是  GB 了。
    > 
    > **du --max-depth=1 -B M**\
    > ![](http://3.blog.xuite.net/3/8/3/1/11851958/blog_1028365/txt/32566618/3.png)
    > 
    > 但如果很多，我還要特地看是那個檔占最多空間，麻煩，加上 sort -g 來排序
    > 
    > **du --max-depth=1 -B M | sort -g**\
    > ![](http://3.blog.xuite.net/3/8/3/1/11851958/blog_1028365/txt/32566618/4.png)
    > 
    > 上面就可以看的很清楚，那個東西占最多的空間了。
    > 如果要針對某個目錄的話。就直接加在後面就好了。
    > 
    > **du --max-depth=1 -B M php-5.2.5/ | sort -g**\
    > ![](http://3.blog.xuite.net/3/8/3/1/11851958/blog_1028365/txt/32566618/0.png)
    > 
    > 總結：就是使用 **du --max-depth=1 -B M | sort -g** 就對了啦
    > 

- [Linux du command help and examples](https://www.computerhope.com/unix/udu.htm)

    > -s: summarize
    > 
    > ```
    > $ du -s /usr/
    > 
    > 6533388	/usr/
    > ```
    > 
    > -h: Print sizes in human readable format, rounding values and using abbreviations. For example, "1K", "234M", "2G", etc.
    > 
    > ```
    > $ du -sh /usr/
    > 
    > 6.3G	/usr/
    > ```

### lsof

- [3. lsof 一切皆文件 — Linux Tools Quick Tutorial](https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/lsof.html)

    > ```shell
    > $ lsof | more
    > COMMAND     PID      USER   FD      TYPE             DEVICE SIZE/OFF       NODE NAME
    > init          1      root  cwd       DIR              253,0     4096          2 /
    > init          1      root  rtd       DIR              253,0     4096          2 /
    > init          1      root  txt       REG              253,0   150352    1310795 /sbin/init
    > init          1      root  mem       REG              253,0    65928    5505054 /lib64/libnss_files-2.12.so
    > init          1      root  mem       REG              253,0  1918016    5521405 /lib64/libc-2.12.so
    > init          1      root  mem       REG              253,0    93224    5521440 /lib64/libgcc_s-4.4.6-20120305.so.1
    > init          1      root  mem       REG              253,0    47064    5521407 /lib64/librt-2.12.so
    > init          1      root  mem       REG              253,0   145720    5521406 /lib64/libpthread-2.12.so
    > ...
    > ```
    > 


### cd to previous dir

- [unix - How can I change to the previous directory instead of going up? - Super User](https://superuser.com/questions/324512/how-can-i-change-to-the-previous-directory-instead-of-going-up)

    > The command
    > 
    > ```
    > cd -
    > 
    > ```
    > 
    > will perform the swap you need on most of the mainstream shells, the older longer variant is
    > 
    > ```
    > cd "$OLDPWD"
    > 
    > ```
    > 
    > which will use the environment variable that contains the previous working directory.
    > 




### cut

- [How to define 'tab' delimiter with 'cut' in BASH? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/35369/how-to-define-tab-delimiter-with-cut-in-bash)

    > Two ways:
    > 
    > Press `Ctrl-v + Tab`
    > 
    > ```shell
    > cut -f2 -d'   ' infile
    > ```
    > 
    > or write it like this:
    > 
    > ```shell
    > cut -f2 -d$'\t' infile
    > ```


### tee

- [How to append tee to a file in Bash? - Ask Ubuntu](https://askubuntu.com/questions/808539/how-to-append-tee-to-a-file-in-bash)

    > ```
    > echo -e "First Line" | tee ~/output.log
    > echo -e "Second Line" | tee -a ~/output.log
    >                             ^^
    > ```
    > 
    > From [man tee](http://man7.org/linux/man-pages/man1/tee.1.html):
    > 
    > ```
    >    Copy standard input to each FILE, and also to standard output.
    > 
    >    -a, --append
    >           append to the given FILEs, do not overwrite
    > ```
    > 
    > Note: Using `-a` still creates the file mentioned.
    > 



### echo/printf

- [Echo newline in Bash prints literal \n - Stack Overflow](https://stackoverflow.com/questions/8467424/echo-newline-in-bash-prints-literal-n)

    > You could use `printf` instead:
    > 
    > ```
    > printf "hello\nworld\n"
    > ```
    > 
    > `printf` has more consistent behavior than `echo`. The behavior of `echo` varies greatly between different versions.

### get origin user name in sudo

- [linux - How do you find the original user through multiple sudo and su commands? - Stack Overflow](https://stackoverflow.com/questions/4598001/how-do-you-find-the-original-user-through-multiple-sudo-and-su-commands)

    > Results:
    > 
    > Use `who am i | awk '{print $1}'` OR `logname` as no other methods are guaranteed.
    > 
    > Logged in as self:
    > 
    > ```
    > evan> echo $USER
    > evan
    > evan> echo $SUDO_USER
    > 
    > evan> echo $LOGNAME
    > evan
    > evan> whoami
    > evan
    > evan> who am i | awk '{print $1}'
    > evan
    > evan> logname
    > evan
    > evan>
    > ```
    > 
    > Normal sudo:
    > 
    > ```
    > evan> sudo -s
    > root> echo $USER
    > root
    > root> echo $SUDO_USER
    > evan
    > root> echo $LOGNAME
    > root
    > root> whoami
    > root
    > root> who am i | awk '{print $1}'
    > evan
    > root> logname
    > evan
    > root>
    > ```
    > 
    > sudo su - :
    > 
    > ```
    > evan> sudo su -
    > [root ]# echo $USER
    > root
    > [root ]# echo $SUDO_USER
    > 
    > [root ]# echo $LOGNAME
    > root
    > [root ]# whoami
    > root
    > [root ]# who am i | awk '{print $1}'
    > evan
    > [root ]# logname
    > evan
    > [root ]#
    > ```
    > 
    > sudo su -; su tom :
    > 
    > ```
    > evan> sudo su -
    > [root ]# su tom
    > tom$ echo $USER
    > tom
    > tom$ echo $SUDO_USER
    > 
    > tom$ echo $LOGNAME
    > tom
    > tom$ whoami
    > tom
    > tom$ who am i | awk '{print $1}'
    > evan
    > tom$ logname
    > evan
    > tom$
    > ```



### chmod

- [linux - Chmod recursively - Stack Overflow](https://stackoverflow.com/questions/13377606/chmod-recursively)

    > You need read access, in addition to execute access, to list a directory. If you only have execute access, then you can find out the names of entries in the directory, but no other information (not even types, so you don't know which of the entries are subdirectories). This works for me:
    > 
    > ```
    > find . -type d -exec chmod +rx {} \;
    > ```
    > 
    > ---
    > 
    > You can use chmod with the `X` mode letter (the capital X) to set the executable flag only for directories.
    > 
    > In the example below the executable flag is cleared and then set for all directories recursively:
    > 
    > ```
    > ~$ mkdir foo
    > ~$ mkdir foo/bar
    > ~$ mkdir foo/baz
    > ~$ touch foo/x
    > ~$ touch foo/y
    > 
    > ~$ chmod -R go-X foo
    > ~$ ls -l foo
    > total 8
    > drwxrw-r-- 2 wq wq 4096 Nov 14 15:31 bar
    > drwxrw-r-- 2 wq wq 4096 Nov 14 15:31 baz
    > -rw-rw-r-- 1 wq wq    0 Nov 14 15:31 x
    > -rw-rw-r-- 1 wq wq    0 Nov 14 15:31 y
    > 
    > ~$ chmod -R go+X foo
    > ~$ ls -l foo
    > total 8
    > drwxrwxr-x 2 wq wq 4096 Nov 14 15:31 bar
    > drwxrwxr-x 2 wq wq 4096 Nov 14 15:31 baz
    > -rw-rw-r-- 1 wq wq    0 Nov 14 15:31 x
    > -rw-rw-r-- 1 wq wq    0 Nov 14 15:31 y
    > ```
    > 
    > A bit of explaination:
    > 
    > -   `chmod -x foo` - clear the *eXecutable* flag for `foo`
    > -   `chmod +x foo` - set the *eXecutable* flag for `foo`
    > -   `chmod go+x foo` - same as above, but set the flag only for *Group* and *Other* users, don't touch the *User* (owner) permission
    > -   `chmod go+X foo` - same as above, but apply only to directories, don't touch files
    > -   `chmod -R go+X foo` - same as above, but do this *Recursively* for all subdirectories of `foo`
    > 

- [linux - How do I set chmod for a folder and all of its subfolders and files? - Stack Overflow](https://stackoverflow.com/questions/3740152/how-do-i-set-chmod-for-a-folder-and-all-of-its-subfolders-and-files)

    > I suspect what you really want to do is set the directories to 755 and either leave the files alone or set them to 644. For this, you can use the `find` command. For example:
    > 
    > To change all the directories to 755 (`drwxr-xr-x`):
    > 
    > ```
    > find /opt/lampp/htdocs -type d -exec chmod 755 {} \;
    > 
    > ```
    > 
    > To change all the files to 644 (`-rw-r--r--`):
    > 
    > ```
    > find /opt/lampp/htdocs -type f -exec chmod 644 {} \;
    > 
    > ```


### sort

- [linux - Sorting in bash - Stack Overflow](https://stackoverflow.com/questions/3510275/sorting-in-bash)

    __question__
    > I have been trying to get the unique values in each column of a tab delimited file in bash. So, I used the following command.
    > 
    > ```shell
    > cut -f <column_number> <filename> | sort | uniq -c
    > ```
    > 
    > It works fine and I can get the unique values in a column and its count like
    > 
    > ```shell
    > 105 Linux
    > 55  MacOS
    > 500 Windows
    > ```
    > 
    > What I want to do is instead of sorting by the column value names (which in this example are OS names) I want to sort them by count and possibly have the count in the second column in this output format. So It will have to look like:
    > 
    > ```
    > Windows 500
    > MacOS   105
    > Linux   55
    > ```
    > 
    > How do I do this?
    > 
    __solution__
    > Use:
    > 
    > ```shell
    > cut -f <col_num> <filename>
    >     | sort 
    >     | uniq -c
    >     | sort -r -k1 -n
    >     | awk '{print $2" "$1}'
    > ```
    > 
    > The `sort -r -k1 -n` sorts in reverse order, using the first field as a numeric value. The `awk` simply reverses the order of the columns. You can test the added pipeline commands thus (with nicer formatting):
    > 
    > ```shell
    > pax> echo '105 Linux
    > 55  MacOS
    > 500 Windows' | sort -r -k1 -n | awk '{printf "%-10s %5d\n",$2,$1}'
    > Windows      500
    > Linux        105
    > MacOS         55
    > ```


## if else not


### Operators

- [If Statements - Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/bash-if-statements.php)

    > | Operator              | Description                                                           |
    > |-----------------------|-----------------------------------------------------------------------|
    > | ! EXPRESSION          | The EXPRESSION is false.                                              |
    > | -n STRING             | The length of STRING is greater than zero.                            |
    > | -z STRING             | The lengh of STRING is zero (ie it is empty).                         |
    > | STRING1 = STRING2     | STRING1 is equal to STRING2                                           |
    > | STRING1 != STRING2    | STRING1 is not equal to STRING2                                       |
    > | INTEGER1 -eq INTEGER2 | INTEGER1 is numerically equal to INTEGER2                             |
    > | INTEGER1 -gt INTEGER2 | INTEGER1 is numerically greater than INTEGER2                         |
    > | INTEGER1 -lt INTEGER2 | INTEGER1 is numerically less than INTEGER2                            |
    > | -d FILE               | FILE exists and is a directory.                                       |
    > | -e FILE               | FILE exists.                                                          |
    > | -r FILE               | FILE exists and the read permission is granted.                       |
    > | -s FILE               | FILE exists and it's size is greater than zero (ie. it is not empty). |
    > | -w FILE               | FILE exists and the write permission is granted.                      |
    > | -x FILE               | FILE exists and the execute permission is granted.                    |
    > 

    > ```shell
    > #!/bin/bash
    > # elif statements
    > 
    > if [ $1 -ge 18 ]
    > then
    >   echo You may go to the party.
    > elif [ $2 == 'yes' ]
    > then
    >   echo You may go to the party but be back before midnight.
    > else
    >   echo You may not go to the party.
    > fi
    > ```

### test if a file does not exist

- [How do I tell if a regular file does not exist in Bash? - Stack Overflow](https://stackoverflow.com/questions/638975/how-do-i-tell-if-a-regular-file-does-not-exist-in-bash)

    > The [test](http://man7.org/linux/man-pages/man1/test.1.html) command (`[` here) has a "not" logical operator which is the exclamation point (similar to many other languages). Try this:
    > 
    > ```sh
    > if [ ! -f /tmp/foo.txt ]; then
    >     echo "File not found!"
    > fi
    > ```




## Terminal Keyboard Shortcut

### copy/paste

- [Why does Ctrl + V not paste in Bash (Linux shell)? - Super User](https://superuser.com/questions/421463/why-does-ctrl-v-not-paste-in-bash-linux-shell)


    > most modern terminal programs, like GNOME Terminal, use `Ctrl` `Shift` `C` and `Ctrl` `Shift` `V`.
    > 
    > (Earlier Windows versions (1.x and 2.x), as well as IBM OS/2, only supported the IBM CUA keys CtrlIns to copy and ShiftIns to paste; these shortcuts remain supported by all Windows versions.)
    > 
    > (Most X11 toolkits also support the CUA "copy" and "paste" keys, which do not conflict with terminal programs. Unfortunately, the implementations are rather inconsistent -- `Ctrl` `Ins` copies to the "clipboard" in most programs (GTK, Qt4, but ignored by Xaw); however, `Shift` `Ins` pastes from the "primary selection" in most GTK and Qt4 programs, but from "clipboard" in Firefox, and from the now-obsolete cut-buffers in the now-obsolete Xaw.)
    > 
    > `Ctrl+Ins` to copy and `Shift+Ins` to paste



## linux version/architecture

### show kernel & distribution version

- [Linux Command: Show Linux Version - nixCraft](https://www.cyberciti.biz/faq/command-to-show-linux-version/)

    > To print all information, enter:
    > ```
    > $ uname -a
    > ```
    > Sample outputs:
    > ```
    > Linux vivek-laptop 2.6.32-23-generic-pae #37-Ubuntu SMP Fri Jun 11 09:26:55 UTC 2010 i686 GNU/Linux
    > ```
    > Where,
    > 
    > -   **2.6.32-23** -- Linux kernel version number
    > -   **pae** -- pae kernel type indicate that I'm accssing more than 4GB ram using 32 bit kernel.
    > -   **SMP** -- Kernel that supports multi core and multiple cpus.
    > 
    > ---
    > 
    > ### /proc/version file
    > 
    > Type the following command to see Linux version info:
    > ```
    > $ cat /proc/version
    > ```
    > Sample outputs:
    > ```
    > Linux version 3.2.0-0.bpo.1-amd64 (Debian 3.2.4-1~bpo60+1) (ben@decadent.org.uk) (gcc version 4.4.5 (Debian 4.4.5-8) ) #1 SMP Sat Feb 11 08:41:32 UTC 2012
    > ```
    > The above output identifies the kernel version that is currently running. It includes the contents of `/proc/sys/kernel/ostype`, `/proc/sys/kernel/osrelease`, and `/proc/sys/kernel/version` files. For example:
    > ```
    > $ cat /proc/sys/kernel/{ostype,osrelease,version}
    > ```
    > Sample outputs:
    > ```
    > Linux
    > 3.2.0-0.bpo.1-amd64
    > #1 SMP Sat Feb 11 08:41:32 UTC 2012
    > ```
    > 
    > ---
    > 
    > Find Distribution Version
    > -------------------------
    > 
    > Type the following command:
    > ```
    > $ cat /etc/*release
    > ```
    > OR
    > ```
    > $ lsb_release -a
    > ```
    > 

### lsb_release

- [shell - How to check OS and version using a Linux command - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/88644/how-to-check-os-and-version-using-a-linux-command)

    > Kernel Version
    > --------------
    > 
    > If you want kernel version information, use uname(1). For example:
    > 
    > ```
    > $ uname -a
    > Linux localhost 3.11.0-3-generic #8-Ubuntu SMP Fri Aug 23 16:49:15 UTC 2013 x86_64 x86_64 x86_64 GNU/Linux
    > ```
    > 
    > Distribution Information
    > ------------------------
    > 
    > If you want distribution information, it will vary depending on your distribution and whether your system supports the [Linux Standard Base](http://en.wikipedia.org/wiki/Linux_Standard_Base). Some ways to check, and some example output, are immediately below.
    > 
    > ```
    > $ lsb_release -a
    > No LSB modules are available.
    > Distributor ID: Ubuntu
    > Description:    Ubuntu Saucy Salamander (development branch)
    > Release:    13.10
    > Codename:   saucy
    > 
    > $ cat /etc/lsb-release
    > DISTRIB_ID=Ubuntu
    > DISTRIB_RELEASE=13.10
    > DISTRIB_CODENAME=saucy
    > DISTRIB_DESCRIPTION="Ubuntu Saucy Salamander (development branch)"
    > 
    > $ cat /etc/issue.net
    > Ubuntu Saucy Salamander (development branch)
    > 
    > $ cat /etc/debian_version
    > wheezy/sid
    > ```


### check if 32-bit or a 64-bit OS

- [architecture - How do I check if I have a 32-bit or a 64-bit OS? - Ask Ubuntu](https://askubuntu.com/questions/41332/how-do-i-check-if-i-have-a-32-bit-or-a-64-bit-os)

    > I know at least 2 ways. Open a terminal(`Ctrl`+`Alt`+`T`) and type:
    > 
    > 1.  `uname -a`
    > 
    >     Result for 32-bit Ubuntu:
    >     
    >     > Linux discworld 2.6.38-8-generic #42-Ubuntu SMP Mon Apr 11 03:31:50 UTC 2011 i686 i686 **i386** GNU/Linux
    > 
    >     whereas the 64-bit Ubuntu will show:
    > 
    >     > Linux discworld 2.6.38-8-generic #42-Ubuntu SMP Mon Apr 11 03:31:50 UTC 2011 x86_64 x86_64 **x86_64** GNU/Linux
    > 
    >     Shorter version:
    > 
    >     ```
    >     $ uname -i
    >     x86_64
    > 
    >     ```
    > 
    >     or
    > 
    > 2.  `file /sbin/init`
    > 
    >     Result for 32-bit Ubuntu:
    >     
    >     > /sbin/init: ELF **32-bit** LSB shared object, **Intel 80386**, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.15, stripped
    >     
    >     
    >     whereas for the 64-bit version it would look like:
    >     
    >     > /sbin/init: ELF **64-bit** LSB shared object, **x86-64**, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.15, stripped
    >     
    >     
    >     Same for systems using systemd (16.04):
    > 
    >     `file /lib/systemd/systemd`
    > 
    >     Result for 64-bit:
    >     
    >     > /lib/systemd/systemd: ELF **64-bit** LSB shared object, **x86-64**, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=54cc7ae53727d3ab67d7ff5d66620c0c589d62f9, stripped
    >     
    
    
### cpu/chipset version

- [raspbian - How do I tell which version arm cpu on my Pi? - Raspberry Pi Stack Exchange](https://raspberrypi.stackexchange.com/questions/9912/how-do-i-tell-which-version-arm-cpu-on-my-pi)

    > At a command prompt, type
    > 
    > ```
    > cat /proc/cpuinfo
    > 
    > ```
    > 
    > to view CPU information.
    > 
    > The ARM11 chips use version 6 of the ARM instruction set, ARMv6. More recent chips from the ARM Cortex range like the Cortex A7, A8 etc all use the ARMv7 instruction set.
    > 
    > All Pi boards are shipped with an ARM11. The options on the second line look like a better fit for building software for the Pi. The first set of options appears to be for a newer generation of ARM chip.
    > 



## kill

### force kill process(-9)

- [command line - "kill <PID>" not really killing the process, why? - Ask Ubuntu](https://askubuntu.com/questions/59811/kill-pid-not-really-killing-the-process-why)

    > Processes can ignore some signals. If you send SIGKILL it will not be able to ignore it (and neither catch it to do cleanups). Try:
    > 
    > ```
    > kill -9 {PID}
    > ```
    > 
    > ---
    > 
    > If `kill` is invoked without any parameter, it sends the signal number 15 (`SIGTERM`). This signal can be ignored by the process. This signal notifies the process to clean his things up and then end correctly by himself. *That's the nice way.*
    > 
    > You can also "send" the signal number 9 (`SIGKILL`) that cannot be ignored by the process. The process will even not recognize it, because the kernel ends the process, not the process itself. *That's the evil way.*
    > 
    > One says `kill -9 <pid>` always works. That's a **misbelief**. There are situations where even `kill -9` does not kill the process. For example when a process has the state `D` (uninterruptable sleep). A process comes into this state everytime it waits for I/O (normally not very long). So, if a process waits for I/O (on a defect harddisk for example) and it is not programmed properly (with a timeout), then you simply **cannot kill the process**. No matter what you do. You just can try to make the file accessible that the process continues.
    > 


### Prevent process from killing itself

- [linux - Prevent process from killing itself using pkill - Stack Overflow](https://stackoverflow.com/questions/15740481/prevent-process-from-killing-itself-using-pkill)

    > You can explicitly filter out the current PID from the results:
    > 
    > ```
    > kill $(pgrep -f $DAEMON | grep -v ^$$\$)
    > ```
    > 
    > To correctly use the `-f` flag, be sure to supply the whole path to the daemon rather than just a substring. That will prevent you from killing the script (and eliminate the need for the above `grep`) and also from killing all other system processes that happen to share the daemon's name.
    > 

### Kill process by command name

- [linux - Kill process by command name - Server Fault](https://serverfault.com/questions/406094/kill-process-by-command-name)

    > Simples, use `pkill`
    > 
    > `pgrep, pkill - look up or signal processes based on name and other attributes`
    > 
    > ---
    > 
    > Use the "-f" option in pgrep/pkill to match on the full command line, rather than just the process name (which will likely be just "java", so there may be an issue if there are other java processes running).
    > 

### Check precess alive(-0)

- [bash - What does `kill -0 $pid` in a shell script do? - Stack Overflow](https://stackoverflow.com/questions/11012527/what-does-kill-0-pid-in-a-shell-script-do)

    > sending the signal `0` to a given `PID` just checks if any process with the given `PID` is running and you have the permission to send a signal to it.
    > 
    > For more information see the following manpages:
    > 
    > *kill(1)*
    > 
    > ```
    > $ man 1 kill
    > ...
    > If sig is 0, then no signal is sent, but error checking is still performed.
    > ...
    > ```
    > 
    > *kill(2)*
    > 
    > ```
    > $ man 2 kill
    > ...
    > If sig is 0, then no signal is sent, but error checking is still performed; this
    > can be used to check for the existence of a process ID or process group ID.
    > ...
    > ```
    > 

### wait for any process

- [bash - WAIT for "any process" to finish - Stack Overflow](https://stackoverflow.com/questions/1058047/wait-for-any-process-to-finish/10407912#10407912)

    > I found "kill -0" does not work if the process is owned by root (or other), so I used pgrep and came up with:
    > 
    > ```
    > while pgrep -u root process_name > /dev/null; do sleep 1; done
    > ```
    > 
    > This would have the disadvantage of probably matching zombie processes.
    > 
    > ---
    > 
    > ### To wait for any process to finish
    > 
    > Linux:
    > 
    > ```
    > tail --pid=$pid -f /dev/null
    > ```
    > 
    > Darwin (requires that `$pid` has open files):
    > 
    > ```
    > lsof -p $pid +r 1 &>/dev/null
    > ```
    > 
    > ### With timeout (seconds)
    > 
    > Linux:
    > 
    > ```
    > timeout $timeout tail --pid=$pid -f /dev/null
    > ```
    > 
    > Darwin (requires that `$pid` has open files):
    > 
    > ```
    > lsof -p $pid +r 1m%s -t | grep -qm1 $(date -v+${timeout}S +%s 2>/dev/null || echo INF)
    > ```
    > 

## process

### adjust process prority(nice)

- [nice Man Page - Bash - SS64.com](https://ss64.com/bash/nice.html)

    > **Examples**
    > 
    > Run an echo command with low priority:
    > ```
    > sudo nice -n 10 echo Hello
    > ```
    > Run an echo command with high priority:
    > ```
    > sudo nice -n -10 echo Hello
    > ```

### Prevent process from killed by oom killer

- [Prevent Linux From Automatically Killing a Process - Ars Technica OpenForum](https://arstechnica.com/civis/viewtopic.php?f=16&t=59183)

    > `echo -17 > /proc/PID/oom_adj` will prevent a given process from being killed. That just means a different process will be killed instead, so it isn't really a solution.
    > 


## user/group/password

### get user/group id

- [command line - How can I find my User ID (UID) from terminal? - Ask Ubuntu](https://askubuntu.com/questions/468236/how-can-i-find-my-user-id-uid-from-terminal#_=_)

    > Try also :
    > 
    > ```
    > getent passwd username
    > 
    > ```
    > 
    > This will display user id , group id and home directory .
    > 
    > Or:
    > 
    > ```
    > grep username /etc/passwd
    > 
    > ```
    > 
    > ---
    > 
    > 1.  Using the [id](http://www.manpagez.com/man/1/id/) command you can get the real and effective user and group IDs.
    > 
    >     UID:
    >     ```
    >     id -u <username>
    > 
    >     ```
    > 
    >     GID:
    >     ```
    >      id -g <username> 
    >     ```
    > 
    >     If no username is supplied to `id`, it will default to the current user.
    > 
    > 2.  Using the enviroment variable.
    > 
    >     ```
    >     echo $UID
    > 
    >     ```
    
### Get Current User Name

- [Linux / Unix Shell Script: Get Current User Name - nixCraft](https://www.cyberciti.biz/faq/appleosx-bsd-shell-script-get-current-user/)

    > ```sh
    > echo "$USER"
    > ```
    > ```sh
    > id -u -n
    > ```
    > 
    > The following script reads user name and store to a variable called _user _uid:
    > ```sh
    > #!/bin/bash
    > _user="$(id -u -n)"
    > _uid="$(id -u)"
    > echo "User name : $_user"
    > echo "User name ID (UID) : $_uid"
    > ```
    > 
    > ### A note about $EUID
    > 
    > This variable EUID is readonly. It expands to the effective user ID of the current user, initialized at shell startup. You can use $EUID to find out if user is root or not with the following syntax:
    > ```sh
    > # Find out if you are root or not for admin tasks.
    > (( EUID )) && { echo 'Run this script with root priviliges.'; exit 1; } || echo 'Running as root, starting service...'
    > ```
    > 


## heredoc/pipe


### execute the rest scripts with different user

- [permissions - How do I use su to execute the rest of the bash script as that user? - Stack Overflow](https://stackoverflow.com/questions/1988249/how-do-i-use-su-to-execute-the-rest-of-the-bash-script-as-that-user)

    > Much simpler: use `sudo` to run a shell and use a [heredoc](https://en.wikipedia.org/wiki/Here_document) to feed it commands.
    > 
    > ```
    > #!/bin/bash
    > whoami
    > sudo -u someuser bash << EOF
    > echo "In"
    > whoami
    > EOF
    > echo "Out"
    > whoami
    > ```
    > 
    > (answer [originally on SuperUser](https://superuser.com/a/468163/33589))
    > 


### avoid variable expantion

- [command line - How to enclose in quotes if both single and double quotes are already used? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/52775/how-to-enclose-in-quotes-if-both-single-and-double-quotes-are-already-used)

    > You can entirely avoid the need to quote using here documents. Note that setting the label in single/double quotes(as in "EOF" in the example below) disables variable and command evaluation within the text.
    > 
    > ```sh
    > cat <<"EOF" >>~/globalLog.txt
    > cat file2.txt  | sed 's/"//g' > file3.txt ## Step 2
    > EOF
    > 
    > ```
    > 

### setting variables inside subshell when using <<

- [shell script - setting variables inside subshell when using << - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/95988/setting-variables-inside-subshell-when-using)

    > To stop the shell from expanding variables in the here document as it is being read, you can either single-quote the tag or backslash *every* use of *every* variable:
    > 
    > ```
    > $ bash <<'EOF'
    > > a=foo
    > > echo "$a"
    > > EOF
    > foo
    > 
    > $ bash <<EOF
    > > a=foo
    > > echo "\$a"
    > > EOF
    > foo
    > ```

### heredoc with tab indented

- [bash - Can't indent heredoc to match nesting's indent - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/76481/cant-indent-heredoc-to-match-nestings-indent/76483)

    > You can change the here-doc operator to `<<-`. You can then indent both the here-doc *and the delimiter* with tabs:
    > 
    > ```sh
    > #! /bin/bash
    > cat <<-EOF
    >     indented
    >     EOF
    > echo Done
    > ```
    > 
    > Note that **you must use tabs**, not spaces to indent the here-doc. This means the above example won't work copied (Stack Exchange replaces tabs with spaces). There can not be any quotes around the first `EOF` delimiter, else parameter expansion, command substitution, and arithmetic expansion are not in effect.
    > 
    > 

### Here-document without interpreting escape sequences, but with interpolation

- [quoting - Here-document without interpreting escape sequences, but with interpolation - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/376103/here-document-without-interpreting-escape-sequences-but-with-interpolation)

    > No, you are out of luck. The manual states:
    > 
    > > and \ **must** be used to quote the characters \, $, and `
    > 
    > There is a workaround, use several here-docs:
    > 
    > ```sh
    > cat <<\EOF > file.tex
    > \documentclass[varwidth=true,border=5pt]{standalone}
    > \usepackage[utf8]{inputenc}
    > \usepackage{amsmath}
    > 
    > \begin{document}
    > EOF
    > cat <<EOF >> file.tex
    > $1
    > EOF
    > cat <<\EOF >> file.tex
    > \end{document}
    > EOF
    > 
    > ```
    > 
    > Or better, once a variable contains a backlash, it is not changed on expansion:
    > 
    > ```sh
    > doc1='\documentclass[varwidth=true,border=5pt]{standalone}
    > \usepackage[utf8]{inputenc}
    > \usepackage{amsmath}
    > 
    > \begin{document}
    > '
    > doc2="$1"
    > doc3='\end{document}
    > '
    > cat <<EOF > file.tex
    > $doc1
    > $doc2
    > $doc3
    > EOF
    > 
    > ```
    > 
    > Which is a convoluted way of writing:
    > 
    > ```sh
    > doc='\documentclass[varwidth=true,border=5pt]{standalone}
    > \usepackage[utf8]{inputenc}
    > \usepackage{amsmath}
    > 
    > \begin{document}
    > '"$1"'
    > \end{document}
    > '
    > printf '%s' "$doc" > file.tex
    > 
    > ```
    > 

### assign a heredoc value to a variable

- [How to assign a heredoc value to a variable in Bash? - Stack Overflow](https://stackoverflow.com/questions/1167746/how-to-assign-a-heredoc-value-to-a-variable-in-bash)

    > **Use $() to assign the output of `cat` to your variable like this:**
    > 
    > ```sh
    > VAR=$(cat <<'END_HEREDOC'
    > abc'asdf"
    > $(dont-execute-this)
    > foo"bar"''
    > END_HEREDOC
    > )
    > 
    > # this will echo variable with new lines intact
    > echo "$VAR"
    > # this will echo variable without new lines (changed to space character)
    > echo $VAR
    > ```


## counting files

### counting files in tar

- [file count in tar](https://www.unix.com/shell-programming-and-scripting/125877-file-count-tar.html)
    > 
    > the -t option lists files in an archive, so this might be what you want
    > 
    > ```shell
    > tar -tf myarchive.tar | wc -l
    > ```
    > 
    > The only downside is that if there are lots of directories in the archive they will inflate the count.
    > 
    > ---
    > 
    > I suppose to that end, you could replace **wc -l** with
    > 
    > ```
    > tar -tf judgements.tar | grep -vc "/$"
    > ```
    > 

### wc (word count)

- [wc 計算檔案的行數、字數、位元組數 @ Altohorn-linux :: 隨意窩 Xuite日誌](http://blog.xuite.net/altohorn/linux/17259885-wc+%E8%A8%88%E7%AE%97%E6%AA%94%E6%A1%88%E7%9A%84%E8%A1%8C%E6%95%B8%E3%80%81%E5%AD%97%E6%95%B8%E3%80%81%E4%BD%8D%E5%85%83%E7%B5%84%E6%95%B8)

    > 指令名稱：wc
    > 功能說明：wc指令可以計算檔案的列數、字數、及位元數。
    > 語法：wc [options] file
    > 
    > [options]
    > -c：--bytes 顯示位元數統計。
    > -m：--chars 顯示字母數統計。
    > -l：--lines 顯示行數統計。
    > -L：--max-line-length 印出最長一行的字數。
    > -w：--words 顯示單字數(word)統計。
    > 
    > 範例：
    > 1.計算fileA文字檔的列數、字數及byte數
    > ```shell
    > wc fileA
    > ```
    > 2.計算fileA的列數
    > ```shell
    > wc -l fileA
    > ```
    > 


## find

### basic usage

- [Bash's find command - Math2001's blog](https://math2001.github.io/post/bashs-find-command/)

    > ### Tests (filters)
    > 
    > Some of `find`'s power comes from it's ability to *filter* which files and folder it "selects". They are called *tests*. So, here are some of them:
    > 
    > #### `-type`
    > 
    > ```
    > $ find -type f
    > ./app/app.js
    > ./app/index.html
    > ./app/style.css
    > ./dist/app.js
    > ./dist/index.html
    > ./dist/style.css
    > $ find -type d
    > .
    > ./app
    > ./dist
    > ```
    > 
    > Here, the filter is `-type`. You guessed it, `-type f` selects files, and `-type d` selects directories. [More about `-type`](https://www.gnu.org/software/findutils/manual/html_mono/find.html#Type)
    > 
    > #### `-name`
    > 
    > ```
    > $ find -name "*.js"
    > ./app/app.js
    > ./dist/app.js
    > $ find -name "*.JS"
    > $ find -iname "*.JS"
    > ./app/app.js
    > ./dist/app.js
    > ```
    > 
    > `-name` takes a glob. The `-iname` variant is case insensitive. [More about `-name`](https://www.gnu.org/software/findutils/manual/html_mono/find.html#Base-Name-Patterns)
    > 
    > #### `-path`
    > 
    > This is the exact same as name, except that it doesn't only apply on the filename, but the whole path (the path that would be outputted). Unlike `-path` though, `*` will match both `/` and leading dots in filename
    > 
    > Same, you have `-ipath` for a case *insensitive* version of it. [More about `-path`](https://www.gnu.org/software/findutils/manual/html_mono/find.html#Full-Name-Patterns)
    > 
    > Note: `-wholename` is the same as `-path`, but `-path` is more portable.
    > 
    > ---
    > 
    > ### Combining test -- operators
    > 
    > Every expression returns a value except operators. A test returns true if it matches the current file (`-name "*.js"` returns true for `app.js`, but not `index.html`). You can conjugate everything with operators.
    > 
    > Every operators only applies to the next expression. So, `expr1 or expr2 and expr3` is the same as `(expr1 or expr2) and expr3`.
    > 
    > #### `-and`
    > 
    > ```
    > $ find -name "*.js" -type f
    > ./app/app.js
    > ./dist/app.js
    > ```
    > 
    > Pretty straight forward, right? You select items that finish with `.js` *and* that are file. You can guess the operator `-and` is the default one. Therefore `find -name "*.js" -and -type f` is the exact same!
    > 
    > #### `-or`
    > 
    > What if you want `.js` and `.css` files? You can use the `-or` operator:
    > 
    > ```
    > $ find -name "*.js" -or -name "*.css" -type f
    > ./app/app.js
    > ./app/style.css
    > ./dist/app.js
    > ./dist/style.css
    > ```
    > 
    > Again, this is the same as `find -name "*.js" -or -name "*.css" -and -type f`.
    > 
    > #### `-not`
    > 
    > If you want every files that do *not* end with `.js`, you can do:
    > 
    > ```
    > $ find -not -name "*.js" -type f
    > ./app/index.html
    > ./app/style.css
    > ./dist/index.html
    > ./dist/style.css
    > ```
    > 
    > ---
    > 
    > ### Actions
    > 
    > Now, printing out the filenames if fun, doing some stuff with them is even better! And guess why it actually prints out the filenames: because the default action is `-print`!
    > 
    > ```
    > $ find -type f -print
    > ./app/app.js
    > ./app/index.html
    > ./app/style.css
    > ./dist/app.js
    > ./dist/index.html
    > ./dist/style.css
    > ```
    > 
    > It's exactly what you'd expect, right?
    > 
    > Note: Just as the tests, actions **return a value** too. Remember this.
    > 
    > #### `-delete`
    > 
    > `-delete` is a pretty useful action. Guess what it does: deletes files (watch out though: it doesn't throw what it deletes to the bin, it *actually* deletes them, like `rm`).
    > 
    > If you want to delete every temporary file created by vim (files that end with `~`), you can just run this:
    > 
    > ```
    > $ find -name "*~" -delete
    > ```
    > 
    > Gone! Every temp files are gone!
    > 
    > What I recommend you do before this is run just `find -name "*~"` so that you see which file are going to be deleted.
    > 
    > #### `-exec`
    > 
    > If you want to do some more complex things though, you might want to use the action `-exec`.
    > 
    > This action takes an undefined number of parameters representing a command that it's going to run on *every* selected files. It stops "consuming" arguments as soon as it sees a `;`. Note that `{}` will be replace with file's path. So,
    > 
    > ```
    > $ find -name "*~" -delete
    > $ # does the same thing as
    > $ find -name "*~" -exec rm {} \;
    > ```
    > 
    > Note: as you can see, we need to escape the `;` to prevent bash from interpreting it.
    > 
    > `-delete` is more efficient though, and more secure. Use it when you can.
    > 
    > ##### Optimizing
    > 
    > It's better to run one command on multiple files than multiple commands on one file each time. For example, the first one is better:
    > 
    > ```
    > $ rm 1.jpg 2.jpg 3.jpg
    > ```
    > 
    > ```
    > $ rm 1.jpg
    > $ rm 2.jpg
    > $ rm 3.jpg
    > ```
    > 
    > Of course, the ability to do that depends on the command, but `find` gives you the possibility of doing that in your `-exec` actions.
    > 
    > Note: It'll automatically adapt to the maximum command line length of your system.
    > 
    > In order to do that, you have to use `{} +`, like so:
    > 
    > ```
    > $ find -name "*~" -exec rm {} +
    > ```
    > 
    > In this case `{} +` will be replaced by as many paths as the maximum command line length of your system allows.
    > 
    > Note that `{} +` has to be at the *end* of the command. [More about optimizing](https://www.gnu.org/software/findutils/manual/html_mono/find.html#Multiple-Files)
    > 


### exclude dir

- [linux - How to exclude a directory in find . command - Stack Overflow](https://stackoverflow.com/questions/4210042/how-to-exclude-a-directory-in-find-command)

    > Use the prune switch, for example if you want to exclude the `misc` directory just add a `-path ./misc -prune -o` to your find command:
    > 
    > ```
    > find . -path ./misc -prune -o -name '*.txt' -print
    > ```
    > 
    > Here is an example with multiple directories:
    > 
    > ```
    > find . -type d \( -path dir1 -o -path dir2 -o -path dir3 \) -prune -o -print
    > ```
    > 
    > Here we exclude dir1, dir2 and dir3, since in `find` expressions it is an action, that acts on the criteria `-path dir1 -o -path dir2 -o -path dir3` (if dir1 or dir2 or dir3), ANDed with `type -d`. Further action is `-o print`, just print.
    > 

### regex support

- [bash - find command with regex quantifier e.g. {1,2} - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/67192/find-command-with-regex-quantifier-e-g-1-2)

    > ```
    > find . -regex '.*myfile[0-9][0-9]?'
    > ```
    > 
    > or
    > 
    > If you have GNU find, you can use another regular expression type:
    > 
    > ```
    > find . -regextype sed -regex '.*myfile[0-9]\{1,2\}'
    > ```

### [fast] find folders which contain files which contain a string

- [grep to display folders which contain files which contain a string - Server Fault](https://serverfault.com/questions/290915/grep-to-display-folders-which-contain-files-which-contain-a-string)

    > This would be my approach:
    > 
    > ```sh
    > find dev -type f -print0 | \          # find all files
    > xargs -0 grep 'extends MY_Output' | \ # search for your string
    > cut -d/ -f2  | \                      # extract web folder name
    > sort | uniq                           # eliminate duplicates
    > 
    > ```
    > 
    > Note use of the `print0` parameter to `find` and the `-0` (zero) flag to `xargs`, which prevents problems if your filenames have embedded spaces in them.


## xargs

### Argument list too long

- [【Linux小筆記】用xargs處理Argument list too long的錯誤以及其原理 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10183432)

    > 在 [你真的了解xargs命令吗](http://blog.csdn.net/voidccc/article/details/8624696) 這篇文章中，深入去討論 xargs 的運作方式，他作對上面 DESCRIPTION中:
    > 
    > > > executes the command (default is /bin/echo) one or more times
    > 
    > 這段話，實際去驗證究竟會執行幾次，發現 xargs 使用的 命令一次會被調用 2000~ 4000次左右，因此，如果列出的log有一萬筆的話，可能就會被分成 3到 5次左右來執行，因而避開了 `Argument list too long` 的錯誤。
    > 

### xargs -0 and find -print0 and grep --null

- [find中的-print0和xargs中-0的奥妙_改变自己_新浪博客](http://blog.sina.com.cn/s/blog_5611597901019nye.html)

    > xargs 默认是以空白字符 (空格, TAB, 换行符) 来分割记录的, 因此文件名 ./file 1.log 被解释成了两个记录 ./file 和 1.log, 不幸的是 rm 找不到这两个文件.
    > 
    > 为了解决此类问题, 聪明的人想出了一个办法, 让 find 在打印出一个文件名之后接着输出一个 NULL 字符 ('\0') 而不是换行符, 然后再告诉 xargs 也用 NULL 字符来作为记录的分隔符. 这就是 find 的 -print0 和 xargs 的 -0 的来历吧.
    > 
    > 
    > 你可能要问了, 为什么要选 '\0' 而不是其他字符做分隔符呢? 这个也容易理解: 一般的编程语言中都用 '\0' 来作为字符串的结束标志, 文件的路径名中不可能包含 '\0' 字符.

- [bash - Is there a grep equivalent for find's -print0 and xargs's -0 switches? - Stack Overflow](https://stackoverflow.com/questions/15976570/is-there-a-grep-equivalent-for-finds-print0-and-xargss-0-switches)

    > Use GNU Grep's `--null` Flag
    > ----------------------------
    > 
    > According to the [GNU Grep documentation](http://www.gnu.org/software/grep/manual/grep.html#Output-Line-Prefix-Control), you can use Output Line Prefix Control to handle ASCII NUL characters the same way as *find* and *xargs*.
    > 
    > > -Z\
    > > --null\
    > > Output a zero byte (the ASCII NUL character) instead of the character that normally follows a file name. For example, 'grep -lZ' outputs a zero byte after each file name instead of the usual newline. This option makes the output unambiguous, even in the presence of file names containing unusual characters like newlines. This option can be used with commands like 'find -print0', 'perl -0', 'sort -z', and 'xargs -0' to process arbitrary file names, even those that contain newline characters.
    > 
    > Use `tr` from GNU Coreutils
    > ---------------------------
    > 
    > As the OP correctly points out, this flag is most useful when handling filenames on input or output. In order to actually convert grep output to use NUL characters as line endings, you'd need to use a tool like *sed* or *tr* to transform each line of output. For example:
    > 
    > ```
    > find /etc/passwd -print0 |
    >     xargs -0 egrep -Z 'root|www' |
    >     tr "\n" "\0" |
    >     xargs -0 -n1
    > ```
    > 
    > This pipeline will use NULs to separate filenames from *find*, and then convert newlines to NULs in the strings returned by *egrep*. This will pass NUL-terminated strings to the next command in the pipeline, which in this case is just *xargs* turning the output back into normal strings, but it could be anything you want.
    > 


## grep

### exclude and count 

- [10+ useful grep command options with examples - Unix/Linux](https://www.crybit.com/grep-command-string-options/)

    > 
    > #### **5\. Checking for full-words not for substring**
    > ```
    > # grep -w "word" file_name
    > ```
    > ---
    > 
    > #### **7\. Exclude pattern match**
    > 
    > If you wish to exclude the pattern match, then you can use -v option
    > ```
    > # grep -v "string" file_name
    > ```
    > ---
    > 
    > #### **8\. Counting the number of matches**
    > 
    > For counting the number of matches, we can use the option -c
    > ```
    > # grep -c "string" file_name
    > ```
    > ---
    > #### **9\. To display the file names that matches the pattern**
    > ```
    > # grep -l "string" file_pattern
    > ```
    > ---
    > 
    > #### **10\. Show only matched string**
    > 
    > It might not be useful if you are starightly giving the string, but it will be useful if you want to show out only the matched string of the pattern
    > ```
    > # grep -o "regexp" file_name
    > ```
    > ---
    > 
    > #### **11\. Shows line number while displaying the output**
    > ```
    > # grep -n "string" file_name
    > ```
    > 
    > 


### search for Fixed string(same as fgrep)

- [bash search for string in each line of file - Stack Overflow](https://stackoverflow.com/questions/5695916/bash-search-for-string-in-each-line-of-file)

    > Don't use bash, use grep.
    > 
    > ```shell
    > grep -F "$cnty" wheatvrice.csv >> wr_imp.csv
    > ```


### Search file2 the fixed string which listed in the file1

- [*grep -F/f的作用* - CSDN博客](https://blog.csdn.net/zhuying_linux/article/details/7019132)

    > **grep -F -f  file1 file2**
    > 
    > **功能：可以把文件2中存在文件1的行输出**
    > 
    > ```sh
    > [root@SOR_SYS hahah]# cat file1
    > 11111
    > 22222
    > 11111
    > 22222
    > 33333
    > 44444
    > 55555
    > ```
    > ```sh
    > [root@SOR_SYS hahah]# cat file2
    > 11111 bj
    > 22222 hb
    > 33333 hn
    > 44444 nm
    > 55555 xm
    > 66666 mk
    > ```
    > 
    > ```sh
    > [root@SOR_SYS hahah]# grep -F -f file1 file2
    > 11111 bj
    > 22222 hb
    > 33333 hn
    > 44444 nm
    > 55555 xm
    > [root@SOR_SYS hahah]#
    > ```
    > 
    > 另一種作法，用join:
    > 
    > 將file1 做sort 後再做 uniq -c 去除重複並輸出重複計數。join 指定要合併的欄位 -1 2 為 file1 的第2欄， -2 1為 file2 第1欄
    > 
    > ```sh
    > [root@SOR_SYS hahah]# join -1 2 -2 1 <(sort file1|uniq -c) <(sort file2)
    > 11111 2 bj
    > 22222 2 hb
    > 33333 1 hn
    > 44444 1 nm
    > 55555 1 xm
    > ```
    > 


### and/or/not

- [grep 指令 - Jex’s Note](http://blog.jex.tw/blog/2013/11/26/grep/)

    > 一般用法
    > ====
    > 
    > ```
    > grep -R '時間' *
    > 
    > ```
    > 
    > -   -r, --recursive like --directories=recurse
    > -   -R, --dereference-recursive likewise, but follow all symlinks
    > -   --include=FILE_PATTERN search only files that match FILE_PATTERN
    > -   --exclude=FILE_PATTERN skip files and directories matching FILE_PATTERN
    > -   --exclude-from=FILE skip files matching any file pattern from FILE
    > -   --exclude-dir=PATTERN directories that match PATTERN will be skipped.
    > -   -i, --ignore-case ignore case distinctions
    > -   -P, --perl-regexp
    > -   -o, --only-matching
    > 
    > `grep ^d`：過濾出資料夾
    > 
    > OR
    > ==
    > 
    > 沒有任何 option, 必須使用 `\|` 來分隔 pattern :
    > 
    > ```
    > grep 'pattern1\|pattern2' filename
    > grep 'Tech\|Sales' employee.txt
    > 
    > ```
    > 
    > 使用 option `-E` (extended regexp), 使用 `|` 分隔 pattern :
    > 
    > ```
    > grep -E 'pattern1|pattern2' filename
    > grep -E 'Tech|Sales' employee.txt
    > 
    > ```
    > 
    > 使用 `egrep` 指令, 相當於使用 `grep -E` :
    > 
    > ```
    > egrep 'pattern1|pattern2' filename
    > egrep 'Tech|Sales' employee.txt
    > 
    > ```
    > 
    > 使用 option `-e`, 但 pattern 必須分開寫
    > 
    > ```
    > grep -e pattern1 -e pattern2 filename
    > grep -e Tech -e Sales employee.txt
    > 
    > ```
    > 
    > AND
    > ===
    > 
    > AND 在 grep 沒有操作符, 可以使用 `-E` 達成 :
    > 
    > ```
    > grep -E 'pattern1.*pattern2' filename
    > grep -E 'pattern1.*pattern2|pattern2.*pattern1' filename
    > grep -E 'Dev.*Tech' employee.txt
    > grep -E 'Manager.*Sales|Sales.*Manager' employee.txt
    > 
    > ```
    > 
    > 使用 linux 原生指令 `|` 來達成 :
    > 
    > ```
    > grep -E 'pattern1' filename | grep -E 'pattern2'
    > grep Manager employee.txt | grep Sales
    > 
    > ```
    > 
    > NOT
    > ===
    > 
    > 使用 `-v` (invert match) 達成, 它會顯示除了符合 pattern 以外的搜尋結果
    > 
    > ```
    > grep -v 'pattern1' filename
    > grep -v Sales employee.txt
    > egrep 'Manager|Developer' employee.txt | grep -v Sales
    > 
    > ```
    > 
    > Others
    > ======
    > 
    > ### 只過濾出符合的部份
    > 
    > ```
    > echo 'hello world' | grep -oP 'hello \K(world)'
    > 
    > ```
    > 
    > ref : <http://www.thegeekstuff.com/2011/10/grep-or-and-not-operators/>

### stop at first match

- [How to stop grep at first match - Shell - Linux Tips](https://linux-tips.com/t/how-to-stop-grep-at-first-match/355)

    > You can use `-m` option, see the descriptions from manpage below:
    > 
    > ```sh
    > -m NUM, --max-count=NUM
    >     Stop reading a file after NUM matching lines.
    > 
    > ```
    > 
    > If you know that there will be only one matching, you should use the grep like that:
    > 
    > ```sh
    > $ grep -m 1 pattern file.txt
    > 
    > ```

### Extended regex: grouping/quantifiers

- [Using Grep + Regex (Regular Expressions) to Search Text in Linux | DigitalOcean](https://www.digitalocean.com/community/tutorials/using-grep-regular-expressions-to-search-for-text-patterns-in-linux)

    > Grouping
    > 
    > ```sh
    > grep "\(grouping\)" file.txt
    > 
    > grep -E "(grouping)" file.txt
    > 
    > egrep "(grouping)" file.txt
    > ```
    > 
    > Alternation
    > ```sh
    > grep -E "(GPL|General Public License)" GPL-3
    > ```
    > 
    > Quantifiers
    > ```sh
    > grep -E "(copy)?right" GPL-3
    > ```
    > 
    > Specifying Match Repetition
    > 
    > ```sh
    > grep -E "[[:alpha:]]{16,20}" GPL-3
    > ```
    > 

### exclude character

- [regex - Making sure a file path is complete in grep - Stack Overflow](https://stackoverflow.com/questions/7563345/making-sure-a-file-path-is-complete-in-grep)

    > Assuming there's only one per line, you could start with something like:
    > 
    > ```
    > grep '\.html' | grep -v '/app/.*\.html'
    > ```
    > 
    > The first will deliver all those that have `.html`. The second will strip from that list all those that have the `app` variant, leaving only those that violate your check.
    > 
    > Obviously, this may need to be adjusted depending on how tricky your lines are (more than one per line, other stuff on the line and so forth) but this "give me a list of all possible violations then remove those that aren't violations" is a tried and tested method.
    > 
    > For example (as Kent suggests), you may want to ensure that the HTML files are all *directly* in the `app` directories instead of possibly `app/something/xyzzy.html`. In that case, you could simply adjust your second filter to ensure this:
    > 
    > ```
    > grep '\.html' | grep -v '/app/[^/]*\.html'
    > ```
    > 
    > Using `[^/]*` (any number of non-`/` characters) instead of `.*` (any number of characters, including `/`) will leave in those that don't have the HTML file directly in the `app` directory.
    > 


## read/while/for

### use pipe/command grouping/ProcessSubstitution/Here strings

- [I set variables in a loop that's in a pipeline. Why do they disappear after the loop terminates? Or, why can't I pipe data to read?](http://mywiki.wooledge.org/BashFAQ/024)


- [shell script - Use bash's read builtin without a while loop - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/162211/use-bashs-read-builtin-without-a-while-loop)

    > It's often said that the next two statements do the same:
    > 
    > ```
    > head somefile | read A B C D E FOO
    > read A B C D E FOO < <(head somefile)
    > ```
    > 
    > Well, not exactly. The first one is a pipe from `head` to `bash`'s `read` builtin. One process's stdout to another process's stdin.
    > 
    > The second statement is redirection and process substitution. It is handled by `bash` itself. It creates a FIFO (named pipe, `<(...)`) that `head`'s output is connected to, and redirects (`<`) it to the `read` process.
    > 
    > So far these seem equivalent. But when working with variables it can matter. In the first one the variables are not set after executing. In the second one they are available in the current environment.
    > 
    > Every shell has another behavior in this situation. See [that link](http://mywiki.wooledge.org/BashFAQ/024) for which they are. In `bash` you can work around that behavior with command grouping `{}`, process substitution (`< <()`) or Here strings (`<<<`).
    > 


### use file descriptor

- [linux - How to read using "read" from file descriptor 3 in bash script? - Stack Overflow](https://stackoverflow.com/questions/2087188/how-to-read-using-read-from-file-descriptor-3-in-bash-script)

    > It's also possible to get bash to assign a file descriptor to a variable; The next free descriptor number will be allocated starting from 10. For example:
    > 
    > ```sh
    > #!/bin/bash
    > FILENAME="my_file.txt"
    > exec {FD}<${FILENAME}     # open file for read, assign descriptor
    > echo "Opened ${FILENAME} for read using descriptor ${FD}"
    > while read -u ${FD} LINE
    > do
    >     # do something with ${LINE}
    >     echo ${LINE}
    > done
    > exec {FD}<&-    # close file
    > ```

### use `while read` replace `for` loop when there are slashes or spaces in loop items

- [branch - How to fetch all git branches? - Stack Overflow](https://stackoverflow.com/questions/10312521/how-to-fetch-all-git-branches#_=_)

    > The solution of @kim3er worked for me. The problem with all snippets is that they don't work when you have slashes or spaces in the branch names. When you need to write bulletproof bash scripts you should use the `while read` trick as this `git branch -r | while read remote; do git branch --track "${remote#origin/}" "$remote"; d` and quote the variable expansions! -- [pinkeen](https://stackoverflow.com/users/242496/pinkeen "399 reputation") [Nov 6 '14 at 13:30](https://stackoverflow.com/questions/10312521/how-to-fetch-all-git-branches#comment42138879_10312587)
    > 


### Pipe a list of strings to for loop (pipe to `cat`; expansion `"${a[@]}"`; `while read` )

- [bash - Pipe a list of strings to for loop - Stack Overflow](https://stackoverflow.com/questions/29560198/pipe-a-list-of-strings-to-for-loop)

    > This might work but I don't recommend it:
    > 
    > ```sh
    > echo "some
    > different
    > lines
    > " | for i in $(cat) ; do
    >     ...
    > done
    > ```
    > 
    > `$(cat)` will expand everything on `stdin` but if one of the lines of the `echo` contains spaces, `for` will think that's two words. So it might eventually break.
    > 
    > If you want to process a list of words in a loop, this is better:
    > 
    > ```sh
    > a=($(echo "some
    > different
    > lines
    > "))
    > for i in "${a[@]}"; do
    >     ...
    > done
    > ```
    > 
    > Explanation: `a=(...)` declares an array. `$(cmd...)` expands to the output of the command. It's still vulnerable for white space but if you quote properly, this can be fixed.
    > 
    > `"${a[@]}"` expands to a correctly quoted list of elements in the array.
    > 
    > Note: `for` is a built-in command. Use `help for` (in bash) instead.
    > 
    > ---
    > 
    > Actually, you should use `a=("word" "a b" "foo")` (3 elements) and then `for i in "${a[@]}"; do ...`; that would iterate three times. You would get 4 iterations. -- [Aaron Digulla](https://stackoverflow.com/users/34088/aaron-digulla "238,928 reputation") [Apr 10 '15 at 12:29](https://stackoverflow.com/questions/29560198/pipe-a-list-of-strings-to-for-loop#comment47272638_29561161)
    > 
    > ---
    > 
    > `for` iterates over a list of words, like this:
    > 
    > ```sh
    > for i in word1 word2 word3; do echo "$i"; done
    > ```
    > 
    > use a `while read` loop to iterate over lines:
    > 
    > ```sh
    > echo "some
    > different
    > lines" | while read -r line; do echo "$line"; done
    > ```
    > 
    > Here is [some useful reading](http://mywiki.wooledge.org/DontReadLinesWithFor) on reading lines in bash.





## sed/head/tail/awk

### delete first n lines

- [linux - How to use sed to remove the last n lines of a file - Stack Overflow](https://stackoverflow.com/questions/13380607/how-to-use-sed-to-remove-the-last-n-lines-of-a-file)

    > I don't know about `sed`, but it can be done with `head`:
    > 
    > ```
    > head -n -2 myfile.txt
    > ```

- [bash - How do I delete the first n lines of an ascii file using shell commands? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/37790/how-do-i-delete-the-first-n-lines-of-an-ascii-file-using-shell-commands)

    > As long as the file is not a symlink or hardlink, you can use sed, tail, or awk. Example below.
    > 
    > ```
    > $ cat t.txt
    > 12
    > 34
    > 56
    > 78
    > 90
    > ```
    > 
    > sed
    > ---
    > 
    > ```
    > $ sed -e '1,3d' < t.txt
    > 78
    > 90
    > ```
    > 
    > You can also use sed in-place without a temp file: `sed -i -e 1,3d yourfile`. This won't echo anything, it will just modify the file in-place. If you don't need to pipe the result to another command, this is easier.
    > 
    > tail
    > ----
    > 
    > ```
    > $ tail -n +4 t.txt
    > 78
    > 90
    > ```
    > 
    > awk
    > ---
    > 
    > ```
    > $ awk 'NR > 3 { print }' < t.txt
    > 78
    > 90
    > ```


### replace a newline (\n)

- [How can I replace a newline (\n) using sed? - Stack Overflow](https://stackoverflow.com/questions/1251999/how-can-i-replace-a-newline-n-using-sed)

    > Use `tr` instead?
    > 
    > ```
    > tr '\n' ' ' < input_filename
    > 
    > ```
    > 
    > or remove the newline characters entirely:
    > 
    > ```
    > tr -d '\n' < input.txt > output.txt
    > 
    > ```
    > 
    > or if you have the GNU version (with its long options)
    > 
    > ```
    > tr --delete '\n' < input.txt > output.txt
    > 
    > ```
    > 

### Add a line to a specific position

- [Add a line to a specific position in a file using Linux sed](https://www.garron.me/en/linux/add-line-to-specific-position-in-file-linux.html)

    > Consider this file:
    > 
    > line 1
    > line 2
    > line 4
    > 
    > As you can see we missed *line 3*, so to add it just execute this command:
    > 
    > ```shell
    > sed '3iline 3' filename.txt
    > 
    > ```
    > 
    > *Parts of the command*
    > 
    > -   sed: is the command itself
    > -   3: is the line where you want the new line inserted
    > -   i: is the parameter that says sed to insert the line.
    > -   line 3: is the text to be added in that position.
    > -   filename: is the file where sed is going to act.
    > 
    > That will just put the result in the screen but the file will remain the same, you can redirect the output to a new file:
    > 
    > ```shell
    > sed '3iline 3' input.txt > output.txt
    > 
    > ```

### Replace all/k-th/first k/after k-th occurance words

- [text processing - Sed -- Replace first k instances of a word in the file - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/155805/sed-replace-first-k-instances-of-a-word-in-the-file)

    > Line-oriented solution
    > ----------------------
    > 
    > With standard sed, there is a command to replace the k-th occurrance of a word on a line. If `k` is 3, for example:
    > 
    > ```
    > sed 's/old/new/3'
    > ```
    > 
    > Or, one can replace all occurrences with:
    > 
    > ```
    > sed 's/old/new/g'
    > ```
    > 
    > Neither of these is what you want.
    > 
    > GNU `sed` offers an extension that will change the k-th occurrance and all after that. If k is 3, for example:
    > 
    > ```
    > sed 's/old/new/g3'
    > ```
    > 
    > These can be combined to do what you want. To change the first 3 occurrences:
    > 
    > ```
    > $ echo old old old old old | sed -E 's/\<old\>/\n/g4; s/\<old\>/new/g; s/\n/old/g'
    > new new new old old
    > ```
    > 
    > where `\n` is useful here because we can be sure that it never occurs on a line.
    > 
    > ### Explanation:
    > 
    > We use three `sed` substitution commands:
    > 
    > -   `s/\<old\>/\n/g4`
    > 
    >     This the GNU extension to replace the fourth and all subsequent occurrences of `old` with `\n`.
    > 
    >     The extended regex feature `\<` is used to match the beginning of a word and `\>` to match the end of a word. This assures that only complete words are matched. Extended regex requires the `-E` option to `sed`.
    > 
    > -   `s/\<old\>/new/g`
    > 
    >     Only the first three occurrences of `old` remain and this replaces them all with `new`.
    > 
    > -   `s/\n/old/g`
    > 
    >     The fourth and all remaining occurrences of `old` were replaced with `\n` in the first step. This returns them back to their original state.
    > 
    > ### Non-GNU solution
    > 
    > If GNU sed is not available and you want to change the first 3 occurrences of `old` to `new`, then use three `s` commands:
    > 
    > ```
    > $ echo old old old old old | sed -E -e 's/\<old\>/new/' -e 's/\<old\>/new/' -e 's/\<old\>/new/'
    > new new new old old
    > ```
    > 
    > This works well when `k` is a small number but scales poorly to large `k`.
    > 
    > Since some non-GNU seds do not support combining commands with semicolons, each command here is introduced with its own `-e` option. It may also be necessary to verify that your `sed` supports the word boundary symbols, `\<` and `\>`.
    > 
    > File-oriented solution
    > ----------------------
    > 
    > We can tell sed to read the whole file in and then perform the substitutions. For example, to replace the first three occurrences of `old` using a BSD-style sed:
    > 
    > ```
    > sed -E -e 'H;1h;$!d;x' -e 's/\<old\>/new/' -e 's/\<old\>/new/' -e 's/\<old\>/new/'
    > ```
    > 
    > The sed commands `H;1h;$!d;x` read the whole file in.
    > 
    > Because the above does not use any GNU extension, it should work on BSD (OSX) sed. Note, thought, that this approach requires a `sed` that can handle long lines. GNU `sed` should be fine. Those using a non-GNU version of `sed` should test its ability to handle long lines.
    > 
    > With a GNU sed, we can further use the `g` trick described above, but with `\n` replaced with `\x00`, to replace the first three occurrences:
    > 
    > ```
    > sed -E -e 'H;1h;$!d;x; s/\<old\>/\x00/g4; s/\<old\>/new/g; s/\x00/old/g'
    > ```
    > 
    > This approach scales well as `k` becomes large. This assumes, though, that `\x00` is not in your original string. Since it is impossible to put the character `\x00` in a bash string, this is usually a safe assumption.
    > 
    > 


### Read multiline (H;1h;$!d;x)

- [linux - sed not finding '0A' control character - Stack Overflow](https://stackoverflow.com/questions/37645067/sed-not-finding-0a-control-character)

    > In `sed`, unlike say python, the newline character `\n` is considered a *line separator* and *not* part of any line. If you want to modify the newline characters, read the whole file in at once and then do your substitutions:
    > 
    > ```
    > sed 'H;1h;$!d;x; s/something\n/somethingelse/g'
    > 
    > ```
    > 
    > ### How it works
    > 
    > `sed` has both a pattern space (where newly-read lines go) and a hold space. These commands append the newly-read lines to the hold space until we reach the last line. Then the whole of the file is transferred to the pattern space and you can do whatever commands on it that you wish. In detail:
    > 
    > -   `H` - Append current line to hold space
    > -   `1h` - If this is the first line, overwrite the hold space with it
    > -   `$!d` - If this is not the last line, delete pattern space and jump to the next line.
    > -   `x` - Exchange hold and pattern space to put whole file in pattern space
    > 
    > ### Example
    > 
    > Let's consider this sample file:
    > 
    > ```
    > $ cat file
    > Try to av-
    > oid word
    > splits.
    > 
    > ```
    > 
    > Now, let's merge any line that ends with a hyphen with the line that follows:
    > 
    > ```
    > $ sed 'H;1h;$!d;x; s/-\n//g' file
    > Try to avoid word
    > splits.
    > 
    > ```
    > 
    > Or, if you prefer the hex form:
    > 
    > ```
    > $ sed 'H;1h;$!d;x; s/-\x0a//g' file2
    > Try to avoid word
    > splits.
    > 
    > ```

### Deal with each line after Read multiline (H;1h;$!d;x)

- [sed - Simple significant usage of '/M' multi-line address suffix? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/298670/simple-significant-usage-of-m-multi-line-address-suffix)

    > As Stéphane pointed out, this modifier is useful when the pattern space contains more then one line. Here are a few more examples using `'H;1h;$!d;x` which accumulates all lines in the hold buffer and then on last line it exchanges buffers so the whole input is in the pattern space. So with this input:
    > 
    > ```
    > printf %s\\n 'onetwo' 'four' 'fivetwo' | sed 'H;1h;$!d;x;l;d'
    > 
    > ```
    > 
    > this is what the pattern space looks like:
    > 
    > ```
    > onetwo\nfour\nfivetwo$
    > 
    > ```
    > 
    > `M` might come in handy
    > 
    > -   if you need to match the beginning or/and the end of *some or all lines in the pattern space*:
    > 
    >     ```
    >     printf %s\\n 'onetwo' 'four' 'fivetwo' | sed 'H;1h;$!d;x;s/^/DO/M2;s/$/END/Mg'
    > 
    >     onetwoEND
    >     DOfourEND
    >     fivetwoEND
    > 
    >     ```
    > 
    > -   if you're trying to find a match that does not span over multiple lines:
    > 
    >     ```
    >     printf %s\\n 'onetwo' 'four' 'fivetwo' | sed 'H;1h;$!d;x;s/one.*two/MATCH/M'
    > 
    >     MATCH
    >     four
    >     fivetwo
    > 
    >     ```
    > 
    > -   if you want to manipulate the pattern space on condition that some line in the pattern space starts or ends with a certain pattern (this is an example where it's not used in conjunction with `s`: delete pattern space if one line ends in `ur`):
    > 
    >     ```
    >     printf %s\\n 'onetwo' 'four' 'fivetwo' | sed 'H;1h;$!d;x;/ur$/Md'
    > 
    >     ```
    > 
    > In all these examples, if you remove `M` the result will be quite different. However, this doesn't mean the above can't be done without `M`, it's just more convenient:
    > 
    > ```
    > s/one.*two/MATCH/M'
    > 
    > ```
    > 
    > vs
    > 
    > ```
    > s/one[^\n]*two/MATCH/'
    > 
    > ```
    > 
    > or
    > 
    > ```
    > /ur$/Md'
    > 
    > ```
    > 
    > vs
    > 
    > ```
    > /ur$\|ur\n/d'
    > 
    > ```
    > 
    > 


### change delimiter(\|#@,)

- [bash - How do I escape double and single quotes in sed? - Stack Overflow](https://stackoverflow.com/questions/7517632/how-do-i-escape-double-and-single-quotes-in-sed)

    > The `sed` command allows you to use other characters instead of `/`:
    > 
    > ```
    > sed 's#"http://www.fubar.com"#URL_FUBAR#g'
    > ```

### Using varibles in pattern

- [bash - How do I use variables in a sed command? - Ask Ubuntu](https://askubuntu.com/questions/76808/how-do-i-use-variables-in-a-sed-command)

    > The shell is responsible for expanding variables. When you use single quotes for strings, its contents will be treated literally, so `sed` now tries to replace every occurrence of the literal `$var1` by `ZZ`.
    > 
    > ### Using double quotes
    > 
    > Use double quotes to make the shell expand variables while preserving whitespace:
    > 
    > ```
    > sed -i "s/$var1/ZZ/g" "$file"
    > ```
    > 
    > When you require the quote character in the replacement string, you have to precede it with a backslash which will be interpreted by the shell. In the following example, the string `quote me` will be replaced by `"quote me"` (the character `&` is interpreted by `sed`):
    > 
    > ```
    > sed -i "s/quote me/\"&\"/" "$file"
    > ```
    > 
    > ### Using single quotes
    > 
    > If you've a lot shell meta-characters, consider using single quotes for the pattern, and double quotes for the variable:
    > 
    > ```
    > sed -i 's,'"$pattern"',Say hurrah to &: \\0/,' "$file"
    > ```
    > 
    > Notice how I use `s,pattern,replacement,` instead of `s/pattern/replacement/`, I did it to avoid interference with the `/` in `\\0/`.
    > 
    > ### Example
    > 
    > The shell then runs the above command `sed` with the next arguments (assuming `pattern=bert` and `file=text.txt`):
    > 
    > ```
    > -i
    > s,bert,Say hurrah to &: \\0/,
    > text.txt
    > ```
    > 
    > If `file.txt` contains `bert`, the output will be:
    > 
    > ```
    > Say hurrah to bert: \0/
    > ```

## tar

- [How to create and extract zip, tar, tar.gz and tar.bz2 files in Linux](https://www.simplehelp.net/2008/12/15/how-to-create-and-extract-zip-tar-targz-and-tarbz2-files-in-linux/)


    > TAR
    > ---
    > 
    > Tar is a very commonly used archiving format on Linux systems. The advantage with tar is that it consumes very little time and CPU to compress files, but the compression isn't very much either. Tar is probably the Linux/UNIX version of zip -- quick and dirty. Here's how you compress a directory:
    > 
    > ```shell
    > tar -cvf archive_name.tar directory_to_compress
    > ```
    > 
    > And to extract the archive:
    > 
    > ```shell
    > tar -xvf archive_name.tar.gz
    > ```
    > 
    > This will extract the files in the archive_name.tar archive in the current directory. Like with the tar format you can optionally extract the files to a different directory:
    > 
    > ```shell
    > tar -xvf archive_name.tar -C /tmp/extract_here/
    > ```


- [tar 指令的常用語法 | Vixual](http://www.vixual.net/blog/archives/127)

    > ### 常用參數
    > 
    > -   *-c* 打包一個 tar 檔案
    > -   *-x* 解開一個 tar 檔案
    > -   *-t* 檢視 tar 檔案的內容
    > -   *-z* 使用 gzip 壓縮
    > -   *-v* 顯示建立 tar 檔案的過程
    > -   *-P* 使用絕對路徑
    > -   *-f* 指定 tar 檔案的檔案名稱。此參數的後面要接檔案名稱，因此要注意參數的順序 (通常是把 f 參數寫在最後一個，或者是與其它參數拆開使用)

- [How can I build a tar from stdin? - Stack Overflow](https://stackoverflow.com/questions/2597875/how-can-i-build-a-tar-from-stdin)

    > Extending [geekosaur answer](https://stackoverflow.com/a/5200173/471376):
    > 
    > ```
    > find /directory | tar -cf archive.tar -T -
    > 
    > ```
    > 
    > You can use stdin with the `-T` option.
    > 
    > Note that if you filter files using some condition (e.g. `-name` option) in general you need to **exclude directories** in the pipe, otherwise tar will process all their content, that is not what you want. So, use:
    > 
    > ```
    > find /directory -type f -name "mypattern" | tar -cf archive.tar -T -
    > 
    > ```
    > 
    > If you don't use `-type`, all the content of directories matching `"mypattern"` will be added !
    > 

### create backup from symbolic links

- [tar - How to create backup from symbolic links? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/32633/how-to-create-backup-from-symbolic-links)


    > 
    > Use the `-h` tar option. From the man page:
    > 
    > ```
    > -h, --dereference
    >     don't archive symlinks; archive the files they point to
    > 
    > ```
    > 
    > ---
    > 
    > 
    > -   If I have /sym1 points to /backups and /sym2 points to /backups, then I run `tar -hcf file.tar /sym1 /sym2` will I get /backups twice? -- [Felipe Alvarez](https://unix.stackexchange.com/users/11437/felipe-alvarez "379 reputation") [Jan 28 '15 at 23:55](https://unix.stackexchange.com/questions/32633/how-to-create-backup-from-symbolic-links#comment302487_32636)
    > 
    > -   @FelipeAlvarez `-L` counts files once, `-l` multiple times. See [here](https://unix.stackexchange.com/a/82477/105615). -- [Suuuehgi](https://unix.stackexchange.com/users/105615/suuuehgi "299 reputation") [Apr 11 at 22:02](https://unix.stackexchange.com/questions/32633/how-to-create-backup-from-symbolic-links#comment789960_32636)
    > 
    > 


### copy files faster and safer than cp

- [- How to copy files in linux faster and safer than cp - zylk](https://www.zylk.net/en/web-2-0/blog/-/blogs/how-to-copy-files-in-linux-faster-and-safer-than-cp)

    > In fact, cp -a is a quite slow process that sometimes is faster (and safer) implemented by tar, for example:
    > ```shell
    > $ tar cf - . | (cd /dst; tar xvf -)
    > ```
    > Usually faster, and more verbose. Another commands such as pv can help you too, to monitor the progress of a copy between two directories, for example:
    > ```shell
    > $ tar cf - . | pv | (cd /dst; tar xf -)
    > 2,06GB 0:00:09 [ 194MB/s] [  <=>                     ]
    > ```


### zip, rar, 7z, tar...

- [GNU / Linux 各種壓縮與解壓縮指令 | 凍仁的筆記](http://note.drx.tw/2008/04/command.html)

    > ### .tar (僅打包，無壓縮)
    > 
    > -   套件名稱：[tar](apt://tar "使用 AptURL 安裝。")。
    > -   打包：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar cvf _FileName.tar DirName_
    >     ```
    > -   解包：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar xvf _FileName.tar_
    >     ```
    > 
    >   
    > 
    > ### .gz
    > 
    > -   套件名稱：[gzip](apt://gzip "使用 AptURL 安裝。")。
    > -   壓縮  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ gzip _FileName_
    >     ```
    > -   解壓縮 1：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ gunzip _FileName.gz_
    >     ```
    > -   解壓縮 2：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ gzip -d _FileName.gz_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .tar.gz
    > 
    > -   套件名稱：[gzip](apt://gzip "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar zcvf _FileName.tar.gz DirName_
    >     ```
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar zxvf _FileName.tar.gz_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### bz
    > 
    > -   壓縮：unkown。
    > -   解壓縮 1：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ bzip2 -d _FileName.bz_
    >     ```
    > -   解壓縮 2：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ bunzip2 _FileName.bz_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .tar.bz
    > 
    > -   壓縮：unkown。
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar jxvf _FileName.tar.bz_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .bz2
    > 
    > -   套件名稱：[bzip2](apt://bzip2 "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ bzip2 -z _FileName_
    >     ```
    > -   解壓縮 1：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ bzip2 -d _FileName.bz2_
    >     ```
    > -   解壓縮 2：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ bunzip2 _FileName.bz2_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .tar.bz2
    > 
    > -   套件名稱：[bzip2](apt://bzip2 "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar jcvf _FileName.tar.bz2 DirName_
    >     ```
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar jxvf _FileName.tar.bz2_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .xz
    > 
    > -   套件名稱：[xz-utils](apt://xz-utils,xz-lzma "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ xz -z _FileName_
    >     ```
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ xz -d _FileName.xz_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .tar.xz
    > 
    > -   套件名稱：[xz-utils](apt://xz-utils,xz-lzma "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar Jcvf _FileName.tar.xz DirName_
    >     ```
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar Jxvf _FileName.tar.xz_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .Z
    > 
    > -   壓縮：compress _FileName_
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ uncompress _FileName.Z_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .tar.Z
    > 
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar Zcvf _FileName.tar.Z DirName_
    >     ```
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar Zxvf _FileName.tar.Z_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .tgz
    > 
    > -   套件名稱：[gzip](apt://gzip "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar zcvf _FileName.tgz FileName_
    >     ```
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar zxvf _FileName.tgz_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .tar.tgz
    > 
    > -   套件名稱：[gzip](apt://gzip "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar zcvf _FileName.tar.tgz FileName_
    >     ```
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ tar zxvf _FileName.tar.tgz_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .7z
    > 
    > -   套件名稱：[p7zip-full](apt://p7zip-full "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ 7z a _FileName.7z FileName_
    >     ```
    > -   使用密碼 (PASSWORD) 壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ 7z a _FileName.7z FileName_ -p_PASSWORD_
    >     ```
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ 7z x _FileName.7z_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .zip
    > 
    > -   套件名稱：[zip](apt://zip "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ zip _FileName.zip DirName_
    >     ```
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ unzip _FileName.zip_
    >     ```
    > 
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .rar
    > 
    > -   套件名稱：[rar](apt://rar "使用 AptURL 安裝。"), [unrar](apt://unrar "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ rar a _FileName.rar DirName_
    >     ```
    > -   解壓縮 1：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ rar e _FileName.rar_
    >     ```
    > -   解壓縮 2：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ unrar e _FileName.rar_
    >     ```
    > -   解壓縮 3：在指定目錄內解壓縮。  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ rar x _FileName.rar DirName_
    >     ```
    > -   解壓縮 4：解壓縮完整路徑
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ unrar x _FileName.rar
    >     ```
    >   
    > [](http://note.drx.tw/2008/04/command.html)  
    > 
    > ### .lha
    > 
    > -   套件名稱：[lha](apt://lha "使用 AptURL 安裝。")。
    > -   壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ lha -a _FileName.lha FileName_
    >     ```
    > -   解壓縮：  
    >     ```shell
    >     > [ jonny@linux ~ ]  
    >     > $ lha -e _FileName.lha_
    >     ```
    > 



## pv (pipe viewer)

- [pv 指令顯示 Linux 程式執行進度，管線 Pipe 資料監看指令 - G. T. Wang](https://blog.gtwang.org/linux/pv-pipe-viewer-progress-monitor-linux-command/)


    > Linux 的 `pv` 指令可以讓使用者即時監看通過管線（pipe）的資料量。
    > 
    > 一個 Linux 系統管理者通常都會花許多時間在終端機上管理系統，例如使用各種指令進行安裝或移除系統套件、查看系統負載狀況、複製與搬移等檔案操作，還有其他各式各樣的動作都可以在終端機中達成。
    > 
    > 有一些指令在執行時不會特別輸出一些進度的相關資訊，如果執行的時間比較常時，使用者無從得知指令的執行狀況，常會懷疑指令是否已經當掉了。  
    > 
    > 
    >   
    > 大部分的 Linux 指令都不會提供執行進度的輸出訊息，但是執行進度是使用者常常會想要看的東西，遇到這樣的狀況我們可以使用 `pv` 指令來產生有用的進度訊息，讓一般的指令加上進度顯示的功能，以下是 `pv` 指令的使用方式與範例。
    > 
    > ## 安裝
    > 
    > 在 Ubuntu Linux 上若要安裝 `pv`，可以使用 apt：
    > 
    > ```shell
    > sudo apt-get install pv
    > ```
    > 
    > 若在 Red Hat 系列的 Linux 上安裝 `pv`，則使用 `yum`：
    > 
    > ```shell
    > yum install pv
    > ```
    > 
    > FreeBSD 的使用者可以透過 port 安裝：
    > 
    > ```shell
    > cd /usr/ports/sysutils/pv/
    > make install clean
    > ```
    > 
    > 或是直接安裝編譯好的版本：
    > 
    > ```shell
    > pkg_add -r pv
    > ```
    > 
    > 
    > ## 使用 `pv` 顯示程式執行進度
    > 
    > `pv` 的角色就跟 `cat` 類似，一般 `cat` 可以將資料從檔案或是標準輸入（stdin）讀取進來，然後從標準輸出（stdout）輸出，而 `pv` 也是一樣，只是它在輸入與輸出中間會自動將進度顯示在終端機上。
    > 
    > 舉例來說，假設我們要將一個檔案內容導向另外一個檔案，可以這樣寫：
    > 
    > ```shell
    > cat file > other_file
    > ```
    > 
    > 如果 `file` 這個檔案很大的時候（例如一個 iso 影像檔），這種指令會需要等待一段時間，沒有任何輸出，這時候就可以改用 `pv`，變成這樣：
    > 
    > ```shell
    > pv file > other_file
    > ```
    > 
    > 將 `cat` 的位置替換為 `pv` 之後，就會顯示資料的處理進度。我拿 Ubuntu Linux 16.04 的 iso 檔作為示範，將其導入 `/dev/null`：
    > 
    > ```shell
    > pv ubuntu-16.04-desktop-amd64.iso > /dev/null
    > ```
    > 
    > 在導向資料的過程中，`pv` 就會產生這樣的進度輸出：
    > 
    > [![pv-pipe-viewer-progress-monitor-linux-command-01](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-01.png "<code>pv</code> 進度輸出")](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-01.png)
    > 
    > `pv` 進度輸出
    > 
    > `pv` 的基本使用方式就是這樣，實際運用上可以結合 Linux 中其它的指令一起使用，以下是一些常用的範例。
    > 
    > 
    > ## `pv` 使用範例
    > 
    > 使用 `gzip` 壓縮資料時不會有任何進度指示，我們可以藉由 `pv` 來顯示進度：
    > 
    > ```shell
    > pv file | gzip > file.gz
    > ```
    > 
    > [![pv-pipe-viewer-progress-monitor-linux-command-02](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-02.png "<code>pv</code> 進度輸出")](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-02.png)
    > 
    > `pv` 進度輸出
    > 
    > 如果要從其他的行程（process）讀取資料來傳送，也可以用管線（pipe）的方式將 `pv` 串在中間：
    > 
    > ```shell
    > cat file | pv | gzip > file.gz
    > ```
    > 
    > [![pv-pipe-viewer-progress-monitor-linux-command-03](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-03.png "<code>pv</code> 進度輸出")](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-03.png)
    > 
    > `pv` 進度輸出
    > 
    > 不過在這種情況下 `pv` 就無法判斷整個完整資料的大小，所以無法計算整體進度，只會顯示經過的時間以及資料處理的速度。如果完整的資料大小是已知的，可以使用 `-s` 指定資料大小，這樣 `pv` 就會計算整體的進度（以百分比表示）：
    > 
    > ```shell
    > cat file | pv -s 1513308160 | gzip > file.gz
    > ```
    > 
    > [![pv-pipe-viewer-progress-monitor-linux-command-04](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-04.png "<code>pv</code> 進度輸出")](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-04.png)
    > 
    > `pv` 進度輸出
    > 
    > `pv` 若配合 `dialog` 這個小工具就可以製作出文字介面的進度視窗：
    > 
    > ```shell
    > (pv -n file | gzip > file) 2>&1 | dialog --gauge "Please wait..." 10 70 0
    > ```
    > 
    > 這裡的 `-n` 參數是可以讓 `pv` 直接輸出單純的百分比數字，因為 `pv` 的訊息預設會輸出至標準錯誤（stderr），所以我們要加上 `2>&1` 讓標準錯誤導向標準輸出，然後將標準輸出導向 `dialog` 產生文字的進度視窗。
    > 
    > [![pv-pipe-viewer-progress-monitor-linux-command-05](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-05.png "<code>pv</code> 配合 <code>dialog</code>")](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-05.png)
    > 
    > `pv` 配合 `dialog`
    > 
    > 如果有許多的處理動作串在一起，可以加上多個 `pv` 監看不同處理步驟的狀況：
    > 
    > ```shell
    > pv -cN raw file | gzip | pv -cN gzip > file.gz
    > ```
    > 
    > [![pv-pipe-viewer-progress-monitor-linux-command-06](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-06.png "多個 <code>pv</code> 進度輸出")](https://blog.gtwang.org/wp-content/uploads/2016/10/pv-pipe-viewer-progress-monitor-linux-command-06.png)
    > 
    > 多個 `pv` 進度輸出
    > 
    > 使用 [netcat](https://blog.gtwang.org/linux/linux-utility-netcat-examples/) 傳送資料時也不會有任何進度指示，一樣可以藉由 `pv` 來顯示進度：
    > 
    > ```shell
    > pv file | nc 192.168.0.1 3000
    > cat file | pv | nc 192.168.0.1 3000
    > cat file | pv -s 12345 | nc 192.168.0.1 3000
    > (pv -n file | nc 192.168.0.1 3000) 2>&1 | dialog --gauge "Please wait..." 10 70 0
    > ```
    > 
    > 計算 [MD5 與 SHA1 校驗碼](https://blog.gtwang.org/linux/generate-verify-check-files-md5-sha1-checksum-linux/)：
    > 
    > ```shell
    > pv file | md5sum
    > pv file | sha1sum
    > ```
    > 
    > 備份 `/dev/sda` 磁碟，跳過錯誤：
    > 
    > ```shell
    > pv -EE /dev/sda > disk-image.img
    > ```
    > 
    > 將映像檔寫回磁碟：
    > 
    > ```shell
    > pv disk-image.img > /dev/sda
    > ```
    > 
    > 抹除磁碟上所有的資料，這個主要用於丟棄硬碟之前，把資料徹底清除，避免資料外洩：
    > 
    > ```shell
    > pv < /dev/zero > /dev/sda
    > ```


### show the transfer progress and speed when copying files

- [command line - How to show the transfer progress and speed when copying files with cp? - Ask Ubuntu](https://askubuntu.com/questions/17275/how-to-show-the-transfer-progress-and-speed-when-copying-files-with-cp)

    > While `cp` hasn't got this functionality, you can use `pv` to do this:
    > 
    > ```
    > pv my_big_file > backup/my_big_file
    > 
    > ```
    > 
    > Note: this method will lose the file's permissions and ownership. Files copied this way will have the same permissions as if you'd created them yourself and will belong to you.
    > 
    > In this example, `pv` basically just outputs the file to stdout*, which you redirect to a file using the `>` operator. Simultaneously, it prints information about the progress to the terminal when you do that.
    > 
    > This is what it looks like:
    > 
    > ```
    > stefano@ubuntu:~/Data$ pv my_big_file > backup/my_big_file
    >  138MB 0:00:01 [73.3MB/s] [=================================>] 100%
    > 
    > ```
    > 
    > ---
    > 
    > Like `cat`, `pv` is not a good tool for copying sparse files since [it will expand them by filling in any gaps with zero-bytes](http://unix.stackexchange.com/a/30382/48446). This means that the new file can take up considerably more disk space despite having the same content as the original. -- [ali_m](https://askubuntu.com/users/185188/ali-m "165 reputation") [Nov 18 '15 at 15:26](https://askubuntu.com/questions/17275/how-to-show-the-transfer-progress-and-speed-when-copying-files-with-cp#comment1025319_17279)

### cp vs. cat to copy a file

- [bash - cp vs. cat to copy a file - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/30295/cp-vs-cat-to-copy-a-file/30382#30382)

    > One more issue comes to my mind where `cat` vs. `cp` makes a significant difference:
    > 
    > By definition, cat will expand sparse files, filling in the gaps with "real" zero bytes, while cp at least can be told to preserve the holes.
    > 
    > Sparse files are files where sequences of zero bytes have been replaced by metadata to preserve space. You can test by creating one with dd, and duplicate it with the tools of your choice.
    > 
    > 1.  Create a sparse file (changing to /tmp beforehand to avoid trouble - see final note):
    > 
    >     ```
    >     15> cd /tmp
    >     16> dd if=/dev/null of=sparsetest bs=512b seek=5
    >     0+0 records in
    >     0+0 records out
    >     0 bytes (0 B) copied, 5.9256e-05 s, 0.0 kB/s
    >     ```
    > 
    > 2.  size it - it should not take any space.
    > 
    >     ```
    >     17> du -sh sparsetest
    >     0       sparsetest
    >     ```
    > 
    > 3.  copy it with cp and check size
    > 
    >     ```
    >     18> cp sparsetest sparsecp
    >     19> du -sh sparsecp
    >     0       sparsecp
    >     ```
    > 
    > 4.  now copy it with cat and check size
    > 
    >     ```
    >     20> cat sparsetest > sparsecat
    >     21> du -sh sparsecat
    >     1.3M    sparsecat
    >     ```
    > 
    > 5.  try your preferred tools to check on their behaviour
    > 
    > 6.  don't forget to clean up.

## tee

### redirect output to a location I don't have permission to write to

- [linux - How do I use sudo to redirect output to a location I don't have permission to write to? - Stack Overflow](https://stackoverflow.com/questions/82256/how-do-i-use-sudo-to-redirect-output-to-a-location-i-dont-have-permission-to-wr)

    > Your command does not work because the redirection is performed by your shell which does not have the permission to write to `/root/test.out`. The redirection of the output **is not** performed by sudo.
    > 
    > There are multiple solutions:
    > 
    > -   Run a shell with sudo and give the command to it by using the `-c` option:
    > 
    >     ```
    >     sudo sh -c 'ls -hal /root/ > /root/test.out'
    > 
    >     ```
    > 
    > -   Create a script with your commands and run that script with sudo:
    > 
    >     ```
    >     #!/bin/sh
    >     ls -hal /root/ > /root/test.out
    > 
    >     ```
    > 
    >     Run `sudo ls.sh`. See Steve Bennett's [answer](https://stackoverflow.com/a/16514624/12892) if you don't want to create a temporary file.
    > 
    > -   Launch a shell with `sudo -s` then run your commands:
    > 
    >     ```
    >     [nobody@so]$ sudo -s
    >     [root@so]# ls -hal /root/ > /root/test.out
    >     [root@so]# ^D
    >     [nobody@so]$
    > 
    >     ```
    > 
    > -   Use `sudo tee` (if you have to escape a lot when using the `-c` option):
    > 
    >     ```
    >     sudo ls -hal /root/ | sudo tee /root/test.out > /dev/null
    > 
    >     ```
    > 
    >     The redirect to `/dev/null` is needed to stop [**tee**](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/tee.html) from outputting to the screen. To *append* instead of overwriting the output file (`>>`), use `tee -a` or `tee --append` (the last one is specific to [GNU coreutils](https://www.gnu.org/software/coreutils/manual/html_node/tee-invocation.html)).
    


## vi

- [Basic vi Commands](https://www.cs.colostate.edu/helpdocs/vi.html)

### Searching Text

> A common occurrence in text editing is to replace one word or phase by another. To locate instances of particular sets of characters (or strings), use the following commands.
> 
> |   | /string | search forward for occurrence of string in text                |
> |---|---------|----------------------------------------------------------------|
> |   | ?string | search backward for occurrence of string in text               |
> |   | n       | move to next occurrence of search string                       |
> |   | N       | move to next occurrence of search string in opposite direction |
> 

