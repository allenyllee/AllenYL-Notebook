# Linux_Shell__快速上手

<!-- toc --> 
[toc]

## bash

### Keyboard Shortcut

- [Why does Ctrl + V not paste in Bash (Linux shell)? - Super User](https://superuser.com/questions/421463/why-does-ctrl-v-not-paste-in-bash-linux-shell)

    > `Ctrl+Ins` to copy and `Shift+Ins` to paste



### zip, unzip

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
    > 
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

### line remove

- [linux - How to use sed to remove the last n lines of a file - Stack Overflow](https://stackoverflow.com/questions/13380607/how-to-use-sed-to-remove-the-last-n-lines-of-a-file)

    > I don't know about `sed`, but it can be done with `head`:
    > 
    > ```
    > head -n -2 myfile.txt
    > ```

- [bash - How do I delete the first n lines of an ascii file using shell commands? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/37790/how-do-i-delete-the-first-n-lines-of-an-ascii-file-using-shell-commands)

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



## Ubuntu

- [apt - How do I search for available packages from the command-line? - Ask Ubuntu](https://askubuntu.com/questions/160897/how-do-i-search-for-available-packages-from-the-command-line)

    > ### To search for a particular package by name or description:
    > 
    > From the command-line, use:
    > 
    > ```
    > apt-cache search keyword
    > ```
    > 

