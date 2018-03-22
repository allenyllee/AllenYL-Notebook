# Linux_Shell__快速上手

## bash

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

