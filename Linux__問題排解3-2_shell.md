# Linux__問題排解3-2_shell

[toc]
<!-- toc --> 

# shell

## heredoc/pipe/redirect


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

### &> and 2>&1 and &>>

- [command line - What is the differences between &> and 2>&1 - Ask Ubuntu](https://askubuntu.com/questions/635065/what-is-the-differences-between-and-21)

    > Bash's man page mentions there's two ways to redirect [stderr and stdout](https://en.wikipedia.org/wiki/Standard_streams): `&> file` and `>& file`. Now, notice that it says both stderr and stdout.
    > 
    > In case of this `>file 2>&1` we are doing redirection of stdout (1) to file, but then also telling stderr(2) to be redirected to the same place as stdout ! So the purpose may be the same, but the idea slightly different. In other words "John, go to school; Suzzie go where John goes".
    > 
    > What about preference ? `&>` is a `bash` thing. So if you're porting a script, that won't do it. But if you're 100% certain your script will be only working on system with bash - then there's no preference
    > 
    > Here's an example with `dash` , the Debian Amquist Shell which is Ubuntu's default.
    > 
    > ```
    > $ grep "YOLO" * &> /dev/null
    > $ grep: Desktop: Is a directory
    > grep: Documents: Is a directory
    > grep: Downloads: Is a directory
    > grep: Music: Is a directory
    > grep: Pictures: Is a directory
    > grep: Public: Is a directory
    > grep: Templates: Is a directory
    > grep: Videos: Is a directory
    > grep: YOLO: Is a directory
    > grep: bin: Is a directory
    > ```
    > 
    > As you can see, stderr is not being redirected
    > 
    > To address your edits in the question, you can use if statement to check $SHELL variable and change redirects accordingly
    > 
    > But for most cases `> file 2>&1` should work
    > 
    > * * * * *
    > 
    > In more technical terms, the form `[integer]>&word` is called [Duplicating Output File Descriptor](http://pubs.opengroup.org/onlinepubs/009695399/utilities/xcu_chap02.html#tag_02_07_06), and is a feature specified by POSIX Shell Command Language standard, which is supported by most POSIX-compliant and Brourne-like shells.
    > 
    > See also [What does & mean exactly in output redirection?](https://askubuntu.com/a/1031663/295286)


- [bash - What is &>> in a shell script - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/170572/what-is-in-a-shell-script)

    > Your book is likely too old, this is something new in Bash version 4.
    > 
    > ```
    > program &>> result.txt
    > ```
    > 
    > is equivalent to
    > 
    > ```
    > program >> result.txt 2>&1
    > ```
    > 
    > Redirect and append both stdout and stderr to file `result.txt`. More about I/O redirection [here](http://www.tldp.org/LDP/abs/html/io-redirection.html).


### What does & mean exactly in output redirection

- [command line - What does & mean exactly in output redirection? - Ask Ubuntu](https://askubuntu.com/questions/959066/what-does-mean-exactly-in-output-redirection/1031663#1031663)

    > The `&` in `2>&1` simply says that the number `1` is a file descriptor and not a file name. In this case the `standard output file descriptor`.
    > 
    > If you use `2>1`, then this would redirect errors to a file called `1` but if you use `2>&1`, then it would send it to the `standard output stream`.
    > 
    > ---
    > 
    > The `[n]>&word` is called **Duplicating Output File Descriptor**(see [section 2.7.6](http://pubs.opengroup.org/onlinepubs/009695399/utilities/xcu_chap02.html) of POSIX Shell Language Standard). This particular behavior is feature of bourne-like shells, including `ksh`, `dash`, and `bash`; in fact, the standard is based around Bourne shell and `ksh`. Looking into [tcsh](https://linux.die.net/man/1/tcsh) and [csh](https://linux.die.net/man/1/csh) manuals, they apparently do not provide capability of duplicating any file descriptor, however from the description of `>&`, this behaves as `&>` in `bash` (that is, redirects errors and normal output to file).
    > 
    > In *nix like systems, including Ubuntu, you often hear that everything is file, or rather a [file descriptor](https://en.wikipedia.org/wiki/File_descriptor). The standard output is constant file descriptor 1 and standard error is file descriptor 2. So, `> FILE 2>&1` technically means duplicate file descriptor 2 onto file descriptor 1. In other words of [this answer](https://stackoverflow.com/a/11636056/3701431) :
    > 
    > > The 2>&1 tells the shell to give the command a file descriptor 2 that is a duplicate of descriptor 1. (i.e stderr & stdout point to same fd).
    > 
    > The key here is to note that descriptor 1 has to be set first. Because shell processes redirections in left to right order, the `command >FILE 2&1` tells shell to rewire stdout for `command` to go into `FILE` first, and only then descriptor 2 can become copy of 1, that is 1 and 2 point to same location - `FILE`.
    > 
    > This of course goes beyond the standard error and standard output. As show in [this answer](https://unix.stackexchange.com/a/248013/85039), by doing `3&>2`
    > 
    > > ...you duplicate (dup2 ) filedescritor 2 onto filedescriptor 3, possibly closing filedescriptor 3 if it's already open
    > 
    > Example of manipulating file descriptors, among many, would be [capturing output of `dialog` command into variable](https://askubuntu.com/q/491509/295286)
    > 


## gnome-terminal

### execute command in a new terminal

- [gnome-terminal技巧 - CSDN博客](https://blog.csdn.net/swust_long/article/details/7285147)

    > [启动后自动执行命令]
    > 有两个参数可以实现这个功能，`-e`和`-x`，这两个区别在于：
    > 
    > `-e` 可以出现多次，如果在所有`--window`前面，表示对所有window和tab起作用，如果在`--window`或者`--tab`后面，表示只针对这个tab执行，要注意-e后面只能有一个参数，也就是说如果有空格，需要用引号，具体见后例
    > 
    > `-x` 只能出现一次，在`-x`后面的所有内容，均认为是要执行的命令，所以可以出现空格
    > 
    >    这些命令是针对所有tab都执行的
    > 比如：
    > ```
    > $ gnome-terminal -e ls
    > $ gnome-terminal -x ls
    > ```
    > 这两个的执行结果都一样，就是新的终端闪一下就没了，有几种办法：
    > 
    > 一种是修改terminal的配置，在terminal点右键，选择`Profiles->Profile Preferences` 然后找到`Title and Command`，里面有一项`When command exits`，后面选择为`Hold the terminal open`，然后就可以了
    > 
    > 第二种是把结果重定向给`less`，这样`less`执行完之前，是不会退出的
    > 
    > ```
    > $ gnome-terminal -x ls|less
    > ```
    > 第三种是在bash里面再启用一个bash
    > 
    > ```sh
    > $ gnome-terminal -x bash -c "ls; exec bash"
    > $ gnome-terminal -e 'bash -c "ls; exec bash"'
    > ```
    > 注意最后一个命令是exec bash，如果直接写bash也行，相当于开了一个子shell，这样有个缺点，就是直接按关闭按钮的话，会提示还有程序在运行
    > 



## eval/expand/interpolate varible(eval, " ", ' ')

- [bash - Evaluating variables in a string - Stack Overflow](https://stackoverflow.com/questions/18219262/evaluating-variables-in-a-string)

    > Let's take things step by step:
    > 
    > When you do this:
    > 
    > ```sh
    > mycmd='cat $myfile'
    > ```
    > 
    > You prevent the shell from interpolating `$myfile`. Thus:
    > 
    > ```sh
    > $ echo $mycmd
    > cat $myfile
    > ```
    > 
    > If you want to allow the interpolation, you can use double quotes:
    > 
    > ```sh
    > $ mycmd="echo $myfile"  #Double quotes!
    > $ echo "$mycmd"
    > cat afile.txt
    > ```
    > 
    > This, of course, *freezes* the interpretation of `$mycmd` when you do an `eval`.
    > 
    > ```sh
    > $ myfile="afile.txt"
    > $ mycmd="echo $myfile"
    > $ echo $mycmd
    > cat afile.txt
    > $ eval $mycmd   #Prints out afile.txt
    > $ myfile=bfile.txt
    > $ eval $mycmd   #Still prints out afile.txt and not bfile.txt
    > ```
    > 
    > Compare this to:
    > 
    > ```sh
    > $ myfile="afile.txt"
    > $ mycmd='cat $myfile'   #Single quotes hide $myfile from the shell
    > echo $mycmd
    > cat $myfile             #Shell didn't change "$myfile", so it prints as a literal
    > $ eval $mycmd           #Prints out afile.txt
    > $ myfile=bfile.txt
    > $ eval $mycmd           #Now prints out bfile.txt
    > ```
    > 
    > What you probably want to do is to evaluate the `$mycmd` in an echo statement when you echo it:
    > 
    > ```sh
    > $ echo $(eval "echo $mycmd")
    > $ cat afile.txt
    > $ myfile=bfile.txt
    > $ echo $(eval "echo $mycmd")
    > cat bfile.txt
    > ```
    > 


### Parameter Substitution / Parameter Expansion (`${#*}`, `${#@}`, `${var#Pattern}`, `${var%Pattern} `)

- [Bash Reference Manual: Shell Parameter Expansion](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)

- [Parameter Substitution](http://www.tldp.org/LDP/abs/html/parameter-substitution.html)

    > **\${parameter}**
    > 
    > Same as `$parameter`, i.e., value of the variable `parameter`. In certain contexts, only the less ambiguous `${parameter}` form works.
    > 
    > May be used for concatenating variables with strings.
    > 
    > ```sh
    > your_id=${USER}-on-${HOSTNAME}
    > echo "$your_id"
    > #
    > echo "Old \$PATH = $PATH"
    > PATH=${PATH}:/opt/bin  # Add /opt/bin to $PATH for duration of script.
    > echo "New \$PATH = $PATH"
    > ```
    > 
    > ---
    > 
    > **\${parameter-default}**, **\${parameter:-default}**
    > 
    > If parameter not set, use default.
    > 
    > ```sh
    > var1=1
    > var2=2
    > # var3 is unset.
    > 
    > echo ${var1-$var2}   # 1
    > echo ${var3-$var2}   # 2
    > #           ^          Note the $ prefix.
    > 
    > 
    > 
    > echo ${username-`whoami`}
    > # Echoes the result of `whoami`, if variable $username is still unset.
    > ```
    > 
    > 
    > ---
    > 
    > **\${parameter=default}**, **\${parameter:=default}**
    > 
    > If parameter not set, set it to default.
    > 
    > Both forms nearly equivalent. The `:` makes a difference only when `$parameter` has been declared and is `null`, [[1]](http://www.tldp.org/LDP/abs/html/parameter-substitution.html#FTN.AEN6310) as above.
    > 
    > ```sh
    > echo ${var=abc}   # abc
    > echo ${var=xyz}   # abc
    > # $var had already been set to abc, so it did not change.
    > ```
    > 
    > ---
    > **Variable length / Substring removal**
    > 
    > - **\${#var}**
    > 
    >     **String length** (number of characters in `$var`). For an [array](http://www.tldp.org/LDP/abs/html/arrays.html#ARRAYREF), `${#array}` is the length of the first element in the array.
    > 
    > 
    >     Exceptions:
    > 
    >     -   `${#*}` and `${#@}` give the *number of positional parameters*.
    > 
    >     -   For an array, `${#array[*]}` and `${#array[@]}` give the number of elements in the array.
    > 
    >  
    > ---
    > - **\${var#Pattern}**, **\${var##Pattern}**
    > 
    >     - **\${var#Pattern}** Remove from `$var` the *shortest* part of `$Pattern` that matches the *front end* of `$var`.
    > 
    >     - **\${var##Pattern}** Remove from `$var` the *longest* part of `$Pattern` that matches the *front end* of `$var`.
    > 
    > ---
    > - **\${var%Pattern}**, **\${var%%Pattern}**
    > 
    >     - **\${var%Pattern}** Remove from `$var` the *shortest* part of `$Pattern` that matches the *back end* of `$var`.
    > 
    >     - **\${var%%Pattern}** Remove from `$var` the *longest* part of `$Pattern` that matches the *back end* of `$var`.
    > 
    > ---
    > **Variable expansion / Substring replacement**
    > 
    > These constructs have been adopted from *ksh*.
    > 
    > - **${var:pos}**
    > 
    >     Variable `var` expanded, starting from offset `pos`.
    > 
    > - **${var:pos:len}**
    > 
    >     Expansion to a max of `len` characters of variable `var`, from offset `pos`. See [Example A-13](http://www.tldp.org/LDP/abs/html/contributed-scripts.html#PW) for an example of the creative use of this operator.
    > 
    > - **${var/Pattern/Replacement}**
    > 
    >     First match of `Pattern`, within `var` replaced with `Replacement`.
    > 
    >     If `Replacement` is omitted, then the first match of `Pattern` is replaced by *nothing*, that is, deleted.
    > 
    > - **${var//Pattern/Replacement}**
    > 
    >     **Global replacement.** All matches of `Pattern`, within `var` replaced with `Replacement`.
    > 
    >     As above, if `Replacement` is omitted, then all occurrences of `Pattern` are replaced by *nothing*, that is, deleted.
    > 
    > ---
    > 
    > - **${var/#Pattern/Replacement}**
    > 
    >     If *prefix* of `var` matches `Pattern`, then substitute `Replacement` for `Pattern`.
    > 
    > - **${var/%Pattern/Replacement}**
    > 
    >     If *suffix* of `var` matches `Pattern`, then substitute `Replacement` for `Pattern`.
    > 
    > <br>
    > 
    > **Example 10-13. Matching patterns at prefix or suffix of string**
    > 
    > ```sh
    > #!/bin/bash
    > # var-match.sh:
    > # Demo of pattern replacement at prefix / suffix of string.
    > 
    > v0=abc1234zip1234abc    # Original variable.
    > echo "v0 = $v0"         # abc1234zip1234abc
    > echo
    > 
    > # Match at prefix (beginning) of string.
    > v1=${v0/#abc/ABCDEF}    # abc1234zip1234abc
    >                         # |-|
    > echo "v1 = $v1"         # ABCDEF1234zip1234abc
    >                         # |----|
    > 
    > # Match at suffix (end) of string.
    > v2=${v0/%abc/ABCDEF}    # abc1234zip123abc
    >                         #              |-|
    > echo "v2 = $v2"         # abc1234zip1234ABCDEF
    >                         #               |----|
    > 
    > echo
    > 
    > #  ----------------------------------------------------
    > #  Must match at beginning / end of string,
    > #+ otherwise no replacement results.
    > #  ----------------------------------------------------
    > v3=${v0/#123/000}       # Matches, but not at beginning.
    > echo "v3 = $v3"         # abc1234zip1234abc
    >                         # NO REPLACEMENT.
    > v4=${v0/%123/000}       # Matches, but not at end.
    > echo "v4 = $v4"         # abc1234zip1234abc
    >                         # NO REPLACEMENT.
    > 
    > exit 0			
    > ```
    > 


### `${parameter:-word}`, `${parameter:+word}`

- [Bash Reference Manual](https://www.gnu.org/software/bash/manual/bashref.html#Shell-Parameter-Expansion)

    > `${parameter:-word}`
    > 
    > If parameter is unset or null, the expansion of word is substituted. Otherwise, the value of parameter is substituted.
    >     
    > `${parameter:+word}`
    > 
    > If *parameter* is null or unset, nothing is substituted, otherwise the expansion of *word* is substituted.

- [bash - how to smart append LD_LIBRARY_PATH in shell when nounset - Stack Overflow](https://stackoverflow.com/questions/9631228/how-to-smart-append-ld-library-path-in-shell-when-nounset)


    > You could use this construct:
    > 
    > ```shell
    > export LD_LIBRARY_PATH=/mypath${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
    > ```
    > 
    > Explanation:
    > 
    > -   If `LD_LIBRARY_PATH` is not set, then `${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}` expands to nothing without evaluating `$LD_LIBRARY_PATH`, thus the result is equivalent to `export LD_LIBRARY_PATH=/mypath` and no error is raised.
    > 
    > -   If `LD_LIBRARY_PATH` is already set, then `${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}` expands to `:$LD_LIBRARY_PATH`, thus the result is equivalent to `export LD_LIBRARY_PATH=/mypath:$LD_LIBRARY_PATH`.
    > 
    > See the [Bash Reference Manual / 3.5.3 Shell Parameter Expansion](http://www.gnu.org/software/bash/manual/bashref.html#Shell-Parameter-Expansion) for more information on these expansions.
    > 
    > This is an important security practice as two adjacent colons or a trailing/leading colon count as adding the **current directory** to `$PATH` or `$LD_LIBRARY_PATH`. See also:
    > 
    > -   [What corner cases must we consider when parsing path on linux](https://stackoverflow.com/questions/7121753/what-corner-cases-must-we-consider-when-parsing-path-on-linux)
    > -   [bash: $PATH ending in colon puts working directory in PATH](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=775704)
    > -   [How Torch broke ls](https://joshumax.github.io/general/2017/06/08/how-torch-broke-ls.html)
    > 



### ${array[*]} versus ${array[@]}

- [A confusion about ${array[*]} versus ${array[@]} in the context of a Bash completion - Stack Overflow](https://stackoverflow.com/questions/3348443/a-confusion-about-array-versus-array-in-the-context-of-a-bash-comple)

    > Your title asks about `${array[@]}` versus `${array[*]}` but then you ask about `$array[*]` versus `$array[@]` which is a bit confusing. I'll answer both:
    > 
    > When you quote an array variable and use `@` as a subscript, each element of the array is expanded to its full content regardless of whitespace (actually, one of `$IFS`) that may be present within that content. When you use the asterisk (`*`) as the subscript (regardless of whether it's quoted or not) it may expand to new content created by breaking up each array element's content at `$IFS`.
    > 
    > Here's the example script:
    > 
    > ```sh
    > #!/bin/sh
    > 
    > myarray[0]="one"
    > myarray[1]="two"
    > myarray[3]="three four"
    > 
    > echo "with quotes around myarray[*]"
    > for x in "${myarray[*]}"; do
    >         echo "ARG[*]: '$x'"
    > done
    > 
    > echo "with quotes around myarray[@]"
    > for x in "${myarray[@]}"; do
    >         echo "ARG[@]: '$x'"
    > done
    > 
    > echo "without quotes around myarray[*]"
    > for x in ${myarray[*]}; do
    >         echo "ARG[*]: '$x'"
    > done
    > 
    > echo "without quotes around myarray[@]"
    > for x in ${myarray[@]}; do
    >         echo "ARG[@]: '$x'"
    > done
    > ```
    > 
    > And here's it's output:
    > 
    > ```
    > with quotes around myarray[*]
    > ARG[*]: 'one two three four'
    > with quotes around myarray[@]
    > ARG[@]: 'one'
    > ARG[@]: 'two'
    > ARG[@]: 'three four'
    > without quotes around myarray[*]
    > ARG[*]: 'one'
    > ARG[*]: 'two'
    > ARG[*]: 'three'
    > ARG[*]: 'four'
    > without quotes around myarray[@]
    > ARG[@]: 'one'
    > ARG[@]: 'two'
    > ARG[@]: 'three'
    > ARG[@]: 'four'
    > ```
    > 
    > I personally usually want `"${myarray[@]}"`. Now, to answer the second part of your question, `${array[@]}` versus `$array[@]`.
    > 
    > ---
    > 
    > In more detail:
    > 
    > ```sh
    > perls=(perl-one perl-two)
    > compgen -W "${perls[*]} /usr/bin/perl" -- ${cur}
    > ```
    > 
    > is equivalent to:
    > 
    > ```sh
    > compgen -W "perl-one perl-two /usr/bin/perl" -- ${cur}
    > ```
    > 
    > ...which does what you want. On the other hand,
    > 
    > ```sh
    > perls=(perl-one perl-two)
    > compgen -W "${perls[@]} /usr/bin/perl" -- ${cur}
    > ```
    > 
    > is equivalent to:
    > 
    > ```sh
    > compgen -W "perl-one" "perl-two /usr/bin/perl" -- ${cur}
    > ```
    > 
    > ...which is complete nonsense: "perl-one" is the only comp-word attached to the -W flag, and the first real argument -- which compgen will take as the string to be completed -- is "perl-two /usr/bin/perl".
    > 





## special parameters

### pass command line argumants ($n, $*, $@)

- [Shell特殊变量：Shell $0, $#, $*, $@, $?, $$和命令行参数_C语言中文网](http://c.biancheng.net/cpp/view/2739.html)

    > | $0 | 当前脚本的文件名                                                                             |
    > |----|----------------------------------------------------------------------------------------------|
    > | $n | 传递给脚本或函数的参数。n 是一个数字，表示第几个参数。例如，第一个参数是$1，第二个参数是$2。 |
    > | $# | 传递给脚本或函数的参数个数。                                                                 |
    > | $* | 传递给脚本或函数的所有参数。                                                                 |
    > | $@ | 传递给脚本或函数的所有参数。被双引号(" ")包含时，与 $* 稍有不同，下面将会讲到。              |
    > | $? | 上个命令的退出状态，或函数的返回值。                                                         |
    > | $$ | 当前Shell进程ID。对于 Shell 脚本，就是这些脚本所在的进程ID。                                 |
    > 
    > $* 和 $@ 的区别
    > -----------
    > 
    > $* 和 $@ 都表示传递给函数或脚本的所有参数，不被双引号(" ")包含时，都以"\$1" "\$2" ... "\$n" 的形式输出所有参数。
    > 
    > 但是当它们被双引号(" ")包含时，"$*" 会将所有的参数作为一个整体，以"\$1 \$2 ... \$n"的形式输出所有参数；"$@" 会将各个参数分开，以"\$1" "\$2" ... "\$n" 的形式输出所有参数。
    > 


- [bash - What do $? $0 $1 $2 mean in shell script? - Stack Overflow](https://stackoverflow.com/questions/29258603/what-do-0-1-2-mean-in-shell-script)

    > These are positional arguments of the script.
    > 
    > Executing
    > 
    > ```sh
    > ./script.sh Hello World
    > ```
    > 
    > Will make
    > 
    > ```sh
    > $0 = script.sh
    > $1 = Hello
    > $2 = World
    > ```
    > 

### exit state($?)

- [What is the $? (dollar question mark) variable in shell scripting? - Stack Overflow](https://stackoverflow.com/questions/6834487/what-is-the-dollar-question-mark-variable-in-shell-scripting/6834512#6834512)

    > `$?` is used to find the return value of the last executed command. Try the following in the shell:
    > 
    > ```sh
    > ls somefile
    > echo $?
    > ```
    > 
    > If `somefile` exists (regardless whether it is a file or directory), you will get the return value thrown by the `ls` command, which should be `0` (default "success" return value). If it doesn't exist, you should get a number other then 0. The exact number depends on the program.
    > 
    > 

### last argument($_)

- [linux - How to have the cp command create any necessary folders for copying a file to a destination - Stack Overflow](https://stackoverflow.com/questions/947954/how-to-have-the-cp-command-create-any-necessary-folders-for-copying-a-file-to-a)

    > To expand upon Christian's answer, the only reliable way to do this would be to combine mkdir and cp:
    > 
    > mkdir -p /foo/bar && cp myfile "$_"


### get Options set using set builtin command($-)

- [Bash Special Parameters Explained with 4 Example Shell Scripts](https://www.thegeekstuff.com/2010/05/bash-shell-special-parameters/#comments)

    > -   **$-** Options set using set builtin command


### other special parameter

- [shell - What is the meaning of the number displayed by echo $$ ? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/186119/what-is-the-meaning-of-the-number-displayed-by-echo)

    > ### $$
    > 
    > > The PID of the current process.\
    > More examples of different uses listed below:
    > 
    > * * * * *
    > 
    > ### $_
    > 
    > > The default parameter for a lot of functions.
    > 
    > ### $.
    > 
    > > Holds the current record or line number of the file handle that was last read. It is read-only and will be reset to 0 when the file handle is closed.
    > 
    > ### $/
    > 
    > > Holds the input record separator. The record separator is usually the newline character. However, if $/ is set to an empty string, two or more newlines in the input file will be treated as one.
    > 
    > ### $,
    > 
    > > The output separator for the print() function. Nor-mally, this variable is an empty string. However, setting $, to a newline might be useful if you need to print each element in the parameter list on a separate line.
    > 
    > ### $
    > 
    > > Added as an invisible last element to the parameters passed to the print() function. Normally, an empty string, but if you want to add a newline or some other suffix to everything that is printed, you can assign the suffix to $.
    > 
    > ### $
    > 
    > > The default format for printed numbers. Normally, it's set to %.20g, but you can use the format specifiers covered in the section "Example: Printing Revisited" in Chapter 9to specify your own default format.
    > 
    > ### $%
    > 
    > > Holds the current page number for the default file handle. If you use select() to change the default file handle, $% will change to reflect the page number of the newly selected file handle.
    > 
    > ### $=
    > 
    > > Holds the current page length for the default file handle. Changing the default file handle will change $= to reflect the page length of the new file handle.
    > 
    > ### $-
    > 
    > > Holds the number of lines left to print for the default file handle. Changing the default file handle will change $- to reflect the number of lines left to print for the new file handle.
    > 
    > ### $~
    > 
    > > Holds the name of the default line format for the default file handle. Normally, it is equal to the file handle's name.
    > 
    > ### $^
    > 
    > > Holds the name of the default heading format for the default file handle. Normally, it is equal to the file handle's name with _TOP appended to it.
    > 
    > ### $|
    > 
    > > If nonzero, will flush the output buffer after every write() or print() function. Normally, it is set to 0.
    > 
    > ### $?
    > 
    > > Holds the status of the last pipe close, back-quote string, or system() function.
    > 
    > ### $&
    > 
    > > Holds the string that was matched by the last successful pattern match.
    > 
    > ### $`
    > 
    > > Holds the string that preceded whatever was matched by the last successful pattern match.
    > 
    > ### $'
    > 
    > > Holds the string that followed whatever was matched by the last successful pattern match.
    > 
    > ### $+
    > 
    > > Holds the string matched by the last bracket in the last successful pattern match. For example, the statement /Fieldname: (.*)|Fldname: (.*)/ && ($fName = $+); will find the name of a field even if you don't know which of the two possible spellings will be used.
    > 
    > ### $*
    > 
    > > Changes the interpretation of the ^ and $ pattern anchors. Setting $* to 1 is the same as using the /m option with the regular expression matching and substitution operators. Normally, $* is equal to 0.
    > 
    > ### $0
    > 
    > > Holds the name of the file containing the Perl script being executed.
    > 
    > ### $
    > 
    > > This group of variables ($1, $2, $3, and so on) holds the regular expression pattern memory. Each set of parentheses in a pattern stores the string that match the components surrounded by the parentheses into one of the $ variables.
    > 
    > ### $[
    > 
    > > Holds the base array index. Normally, it's set to 0. Most Perl authors recommend against changing it without a very good reason.
    > 
    > ### $]
    > 
    > > Holds a string that identifies which version of Perl you are using. When used in a numeric context, it will be equal to the version number plus the patch level divided by 1000.
    > 
    > ### $"
    > 
    > > This is the separator used between list elements when an array variable is interpolated into a double-quoted string. Normally, its value is a space character.
    > 
    > ### $;
    > 
    > > Holds the subscript separator for multidimensional array emulation. Its use is beyond the scope of this book.
    > 
    > ### $!
    > 
    > > When used in a numeric context, holds the current value of errno. If used in a string context, will hold the error string associated with errno.
    > 
    > ### $@
    > 
    > > Holds the syntax error message, if any, from the last eval() function call.
    > 
    > ### $<
    > 
    > > This UNIX-based variable holds the read uid of the current process.
    > 
    > ### $>
    > 
    > > This UNIX-based variable holds the effective uid of the current process.
    > 
    > ### $)
    > 
    > > This UNIX-based variable holds the read gid of the current process. If the process belongs to multiple groups, then $) will hold a string consisting of the group names separated by spaces.
    > 
    > ### $:
    > 
    > > Holds a string that consists of the characters that can be used to end a word when word-wrapping is performed by the ^ report formatting character. Normally, the string consists of the space, newline, and dash characters.
    > 
    > ### $^D
    > 
    > > Holds the current value of the debugging flags. For more information.
    > 
    > ### $^F
    > 
    > > Holds the value of the maximum system file description. Normally, it's set to 2. The use of this variable is beyond the scope of this book.
    > 
    > ### $^I
    > 
    > > Holds the file extension used to create a backup file for the in-place editing specified by the -i command line option. For example, it could be equal to ".bak."
    > 
    > ### $^L
    > 
    > > Holds the string used to eject a page for report printing.
    > 
    > ### $^P
    > 
    > > This variable is an internal flag that the debugger clears so it will not debug itself.
    > 
    > ### $^T
    > 
    > > Holds the time, in seconds, at which the script begins running.
    > 
    > ### $^W
    > 
    > > Holds the current value of the -w command line option.
    > 
    > ### $^X
    > 
    > > Holds the full pathname of the Perl interpreter being used to run the current script.
    > 
    > Source:
    > 
    > -   [http://www.unix.com/302219737-post3.html](http://www.unix.com/302219737-post3.html)
    > 




### history expansion(exclamation mark, !)

- [quoting - Can't use exclamation mark (!) in bash? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/33339/cant-use-exclamation-mark-in-bash)

    > The exclamation mark is part of history expansion in bash. To use it you need it enclosed in single quotes (eg: `'http://example.org/!132'`) or to directly escape it with a backslash (`\`) before the character (eg: `"http://example.org/\!132"`).
    > 
    > Note that in double quotes, a backslash before the exclam prevents history expansion, BUT the backslash is not removed in such a case. So it's better to use single quotes, so you're not passing a literal backslash to `curl` as part of the URL.
    > 
    > ---
    > 
    > For the record: It's not portable to try escaping "!". The best-practices recommendation is to always quote (singe-quotes) "!". Related: "^" (caret), is a non-metacharacter that needs quoting for portability. Finally, "!" should not be used in an if statement; use it as an argument to test instead if possible (again because of Solaris /bin/sh). -- [Nicholas Wilson](https://unix.stackexchange.com/users/16025/nicholas-wilson "663 reputation") [Oct 18 '12 at 10:31](https://unix.stackexchange.com/questions/33339/cant-use-exclamation-mark-in-bash#comment72933_33340)
    > 
    > ---
    > 
    > As well as the answer given by Daniel, you can also simply turn off history expansion altogether if you don't use it with `set +H`.
    > 
    > ---
    > 
    > Turning off history expansion altogether is the best advice I've heard all day! History expansion is dangerous and [byzantine](http://www.thegeekstuff.com/2011/08/bash-history-expansion/) when there are [much better alternatives](http://www.gnu.org/software/bash/manual/html_node/Commands-For-History.html) (incremental history search with `Ctrl-R`) that let you preview & edit your command so you don't blindly fire away with command `!-14` that you though was at `!-12` that, oops, happened to be `rm -rf *`. Be safe. Disable history expansion! Eschew the `!`! -- [aculich](https://unix.stackexchange.com/users/11052/aculich "906 reputation") [Mar 6 '12 at 1:09](https://unix.stackexchange.com/questions/33339/cant-use-exclamation-mark-in-bash#comment45454_33341)
    > 

## function/fork

### fork bumb

- [fork - what does this command does in bash: ,_,( ){ ,_,| ,_,&};,_, - Stack Overflow](https://stackoverflow.com/questions/27197785/what-does-this-command-does-in-bash)

    > It's a [fork bomb](http://en.wikipedia.org/wiki/Fork_bomb); it will spawn a (potentially) infinite number of processes, until your system runs out of resources (and usually becomes inoperable).
    > 
    > It defines the function named `,_,`, which runs itself (recursion), and piping the output to itself. The last `,_,` is needed to start off the thing.
    > 
    > Formatted, and with `,_,` replaced by `fun`, it looks like:
    > 
    > ```
    > fun() {
    >    fun | fun &
    > };
    > fun
    > ```
    > 
    > Every invocation of `fun` will spawn 2 more invocations of `fun`. The `&` starts the processes in the background (rate of process increase is *exponential*).
    > 
    > It's a variant of the [better known](http://tattoospin.com/wp-content/uploads/2013/10/awesome-fork-bomb-tattoo-from-alex-godair-from-north-street-tattoo-in-normal-il-hack-the-planet.jpg) `:() { :|: & };:`
    > 
    > There are ways to prevent your system from crashing, though; for example in Linux you can edit `/etc/security/limit.conf` & set the maximum number of processes for a user. Other systems have other (usually similar) methods.
    > 
    > Running a fork bomb and crashing your system seems to be something of a rite of passage for UNIX users; it teaches you:
    > 
    > 1.  The importance of imposing resource limits of processes;
    > 2.  that copying & executing commands you do not understand from untrusted sources (eg. the internet) is not a good idea




## shell login

### Prevent user from login (/bin/false & /sbin/nologin)

- [Linux /sbin/nologin与/bin/false的对比 - CSDN博客](https://blog.csdn.net/liupeifeng3514/article/details/79054550)

    > #### **/bin/false**
    > 
    > /bin/false是最严格的禁止login选项，一切服务都不能用。将用户的shell设置为/bin/false,用户会无法登录,并且不会有任何提示。
    > 
    > ```
    > usermod -s /bin/false peipei3514
    > ```
    > 
    > 修改用户peipei3514登录时使用的shell文件为**/bin/false**。
    > 
    > #### **/sbin/nologin**
    > 
    > 　　/sbin/nologin只是不允许login系统，即使给了密码也不行。
    > 
    > 　　所谓"无法登陆"指的仅是这个用户无法使用bash或其他shell来登陆系统而已，并不是说这个账号就无法使用系统资源。举例来说，各个系统账号中，打印作业有lp这个账号管理，www服务器有apache这个账号管理，他们都可以进行系统程序的工作，但就是无法登陆主机而已。
    > 
    > 　　有时候有些服务，比如邮件服务，大部分都是用来接收主机的邮件而已，并不需要登陆。假如有账号试图连接我的主机取得shell，我们就可以拒绝。
    > 
    > 　　另外，如果我想要让某个具有 /sbin/nologin 的用户知道，他们不能登陆主机时，可以新建 /etc/nologin.txt 这个文件，在文件内面写上不能登陆的原因，当用户登录时，屏幕上就会出现这个文件里面的内容。
    > 
    > 　　例如：
    > 
    > ```
    >   #vim /etc/nologin.txt
    >   no login........
    >   #su peipei3514
    > ```


### login system user(/bin/false)from root shell(without password)

- [ubuntu - Run command as Linux "system" user (shell = /bin/false) - Server Fault](https://serverfault.com/questions/274738/run-command-as-linux-system-user-shell-bin-false)

    > I use `su - targetuser -s /bin/bash` from a root shell.
    > 
    > For direct command execution use `-c`:
    > 
    > ```sh
    > su - targetuser -s /bin/bash -c "/bin/echo hello world"
    > ```
    > 

### read command from stdin, exit with non-zero state(bash -se)

- [ubuntu - What does bash -s do? - Stack Overflow](https://stackoverflow.com/questions/37224634/what-does-bash-s-do)

    > From [`man bash`](http://linux.die.net/man/1/bash):
    > 
    > > ```
    > > -s   If  the -s option is present, or if no arguments remain after
    > >      option processing, then commands are read from the standard
    > >      input.  This option allows the positional parameters to be
    > >      set when invoking an interactive shell.
    > > ```
    > 
    > From [`help set`](https://www.gnu.org/software/bash/manual/bashref.html#The-Set-Builtin):
    > 
    > > ```
    > >  -e  Exit immediately if a command exits with a non-zero status.
    > > ```
    > 
    > So, this tells bash to read the script to execute from Standard Input, and to exit immediately if any command in the script (from stdin) fails.
    > 
    > 

## Command parameter/varible/respond

### auto respond to prompts

- [How can I respond to prompts in a Linux Bash script automatically? - Stack Overflow](https://stackoverflow.com/questions/40791622/how-can-i-respond-to-prompts-in-a-linux-bash-script-automatically?rq=1)

    > Try this:
    > 
    > ```
    > echo -e "yes\nyes\nno" | /path/to/your/script
    > ```
    > 
    > ---
    > 
    > ```
    > $ printf "%s\n" yes yes no | ./foo.sh
    > yes yes no
    > ```

- [Automatically enter input in command line - Ask Ubuntu](https://askubuntu.com/questions/338857/automatically-enter-input-in-command-line)

    > Use the command `yes`:
    > 
    > ```
    > yes | script
    > 
    > ```



### Pass bash script parameters to sub-process($@, $*)

- [scripting - Pass bash script parameters to sub-process unchanged - Stack Overflow](https://stackoverflow.com/questions/1695819/pass-bash-script-parameters-to-sub-process-unchanged)

    > You have to put the `$@` in quotes:
    > 
    > ```
    > /the/exe "$@"
    > ```
    > 
    > ---
    >
    > experiments:
    > 
    > ./myscript.sh
    > 
    > ```sh
    > for arg in "$@";do
    >     echo $arg
    > done
    > 
    > for arg in $@;do
    >     echo $arg
    > done
    > 
    > 
    > for arg in "$*";do
    >     echo $arg
    > done
    > 
    > for arg in $*;do
    >     echo $arg
    > done
    > ```
    > run
    > 
    > ```
    > ./myscript.sh "one big thing"
    > ```
    > results
    > ```
    > one big thing
    > one
    > big
    > thing
    > one big thing
    > one
    > big
    > thing
    > ```
    > 
    > 
    > and run
    > ```
    > ./myscript.sh one big thing
    > ```
    > results
    > ```
    > one
    > big
    > thing
    > one
    > big
    > thing
    > one big thing
    > one
    > big
    > thing
    > ```
    > [name=Ya-Lun Li]



### send variable to sub-shell

- [How to "send" variable to sub-shell? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/23179/how-to-send-variable-to-sub-shell)

    > Either use `export` to turn it into an environment variable, or pass it directly to the command.
    > 
    > ```sh
    > VAR="Test" sh -c 'echo "Hello $VAR"'
    > 
    > VAR="Test"
    > export VAR
    > sh -c 'echo "Hello $VAR"'
    > ```
    > 
    > Or simply use double quotes to allow interpolation without having to export anything nor pass the var to the command:
    > 
    > ```sh
    > VAR='Test';
    > sh -c " echo 'Hello $VAR' "
    > ```

### pass all arguments except the first one(${@:2})

- [shell - Process all arguments except the first one (in a bash script) - Stack Overflow](https://stackoverflow.com/questions/9057387/process-all-arguments-except-the-first-one-in-a-bash-script)

    > Use this:
    > 
    > ```
    > echo "${@:2}"
    > ```
    > 
    > * * * * *
    > 
    > The following syntax:
    > 
    > ```
    > echo "${*:2}"
    > ```
    > 
    > would work as well, but is not recommended, because as [@Gordon](https://stackoverflow.com/questions/9057387/process-all-arguments-except-the-first-one#comment11369452_9057392) already explained, that using `*`, it runs all of the arguments together as a single argument with spaces, while `@` preserves the breaks between them (even if some of the arguments themselves contain spaces). It doesn't make the difference with `echo`, but it matters for many other commands.
    > 
    > ---
    > 
    > I just realised my shebang was bad: `#!/usr/bin/env sh` That's why I had problems. You example works fine, same as above provided, after I removed that shebang -- [theta](https://stackoverflow.com/users/992005/theta "9,029 reputation") [Jan 29 '12 at 22:36](https://stackoverflow.com/questions/9057387/process-all-arguments-except-the-first-one-in-a-bash-script#comment11366295_9057392)
    > 

## command execution secquence(; || && & true | !)

### run a command after the previous finished

- [shell - Bash - how to run a command after the previous finished? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/184502/bash-how-to-run-a-command-after-the-previous-finished)

    > Yes, you're doing it the right way. Shell scripts will run each command sequentially, waiting for the first to finish before the next one starts. You can either join commands with `;` or have them on separate lines:
    > 
    > ```
    > command1; command2
    > ```
    > 
    > or
    > 
    > ```
    > command1
    > command2
    > ```
    > 
    > There is no need for `;` if the commands are on separate lines. You can also choose to run the second command only if the first exited successfully. To do so, join them with `&&`:
    > 
    > ```
    > command1 && command2
    > ```
    > 
    > or
    > 
    > ```
    > command1 &&
    > command2
    > ```
    > 
    > For more information on the various control operators available to you, see [here](https://unix.stackexchange.com/q/159513/22222).
    > 

### shell's control operators(`||`, `!`, `&&`, `&`, `;`, `;;`, `|`, `|&`, `(`, or `)`)

- [What are the shell's control and redirection operators? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/159513/what-are-the-shells-control-and-redirection-operators)

    > A. Control operators
    > --------------------
    > 
    > These are tokens that perform control functions, one of `||`, `!`, `&&`, `&`, `;`, `;;`, `|`, `|&`, `(`, or `)`.
    > 
    > ### A.1 List terminators
    > 
    > -   `;` : Will run one command after another has finished, irrespective of the outcome of the first.
    > 
    >     ```
    >     command1 ; command2
    >     ```
    > 
    >     First `command1` is run, in the foreground, and once it has finished, `command2` will be run.
    > 
    >     A newline that isn't in a string literal or after certain keywords is *not* equivalent to the semicolon operator. A list of `;` delimited simple commands is still a *list* - as in the shell's parser must still continue to read in the simple commands that follow a `;` delimited simple command before executing, whereas a newline can delimit an entire command list - or list of lists. The difference is subtle, but complicated: given the shell has no previous imperative for reading in data following a newline, the newline marks a point where the shell can begin to evaluate the simple commands it has already read in, whereas a `;` semi-colon does not.
    > 
    > -   `&` : This will run a command in the background, allowing you to continue working in the same shell.
    > 
    >     ```
    >      command1 & command2
    >     ```
    > 
    >     Here, `command1` is launched in the background and `command2` starts running in the foreground immediately, without waiting for `command1` to exit.
    > 
    >     A newline after `command1` is optional.
    > 
    > ### A.2 Logical operators
    > 
    > -   `&&` : Used to build AND lists, it allows you to run one command only if another exited successfully.
    > 
    >     ```
    >      command1 && command2
    >     ```
    > 
    >     Here, `command2` will run after `command1` has finished and *only* if `command1` was successful (if its exit code was 0). Both commands are run in the foreground.
    > 
    >     This command can also be written
    > 
    >     ```
    >     if command1
    >     then command2
    >     else false
    >     fi
    >     ```
    > 
    >     or simply `if command1; then command2; fi` if the return status is ignored.
    > 
    > -   `||` : Used to build OR lists, it allows you to run one command only if another exited unsuccessfully.
    > 
    >     ```
    >      command1 || command2
    >     ```
    > 
    >     Here, `command2` will only run if `command1` failed (if it returned an exit status other than 0). Both commands are run in the foreground.
    > 
    >     This command can also be written
    > 
    >     ```
    >     if command1
    >     then true
    >     else command2
    >     fi
    >     ```
    > 
    >     or in a shorter way `if ! command1; then command2; fi`.
    > 
    >     Note that `&&` and `||` are left-associative; see [Precedence of the shell logical operators &&, ||](https://unix.stackexchange.com/questions/88850/precedence-of-the-shell-logical-operators) for more information.
    > 
    > -   `!`: This is the "not" operator, used to negate the return status of a command --- return 0 if the command returns a nonzero status, return 1 if it returns the status 0.
    > 
    >     ```
    >     ! command1
    >     ```
    > 
    > ### A.3 Pipe operator
    > 
    > -   `|` : The pipe operator, it passes the output of one command as input to another. A command built from the pipe operator is called a [pipeline](http://en.wikipedia.org/wiki/Pipeline_(Unix)).
    > 
    >     ```
    >      command1 | command2
    >     ```
    > 
    >     Any output printed by `command1` is passed as input to `command2`.
    > 
    > -   `|&` : This is a shorthand for `2>&1 |` in bash and zsh. It passes both standard output and standard error of one command as input to another.
    > 
    >     ```
    >     command1 |& command2
    >     ```
    > 
    > ### A.4 Other list punctuation
    > 
    > `;;` is used solely to mark the end of a [case statement](https://www.gnu.org/software/bash/manual/bashref.html#Conditional-Constructs). Ksh, bash and zsh also support `;&` to fall through to the next case and `;;&` (not in ATT ksh) to go on and test subsequent cases.
    > 
    > `(` and `)` are used to [group commands](https://www.gnu.org/software/bash/manual/bashref.html#Command-Grouping) and launch them in a subshell. `{` and `}` also group commands, but do not launch them in a subshell. See [this answer](https://stackoverflow.com/questions/6270440/simple-logical-operators-in-bash/6270803#6270803) for a discussion of the various types of parentheses, brackets and braces in shell syntax.

### always return good exit status

- [linux - Bash: Run an executable giving a good exit status - Server Fault](https://serverfault.com/questions/228281/bash-run-an-executable-giving-a-good-exit-status)

    > Give this a try:
    > 
    > ```
    > command || true
    > ```
    > 
    > From `man bash`:
    > 
    > > The shell does not exit if the command that fails is part of the command list immediately following a while or until keyword, part of the test following the if or elif reserved words, part of any command executed in a && or ⎪⎪ list except the command following the final && or ⎪⎪, any command in a pipeline but the last, or if the command's return value is being inverted with !.
    > > 
    > 


### executing multiple commands in background in same line(detach)

- [shell - Bash executing multiple commands in background in same line - Stack Overflow](https://stackoverflow.com/questions/22298199/bash-executing-multiple-commands-in-background-in-same-line)

    > As per the `bash` manpage:
    > 
    > > A list is a sequence of one or more pipelines separated by one of the operators `;`, `&`, `&&`, or `||`, and optionally terminated by one of `;`, `&`, or `<newline>`.
    > >
    > > If a command is terminated by the control operator `&`, the shell executes the command in the background in a subshell. The shell does not wait for the command to finish, and the return status is 0. Commands separated by a `;` are executed sequentially; the shell waits for each command to terminate in turn. The return status is the exit status of the last command executed.
    > 
    > You can see there that `&` isn't just something that runs a command in the background, it's actually a *separator* as well. Hence, you don't *need* the semicolon following it. In fact, it's actually *invalid* to try that, just the same as if you put two semicolons in sequence, the actual problem being that `bash` does not permit empty commands:
    > 
    > ```bash
    > pax> echo 1 ; echo 2
    > 1
    > 2
    > 
    > pax> echo 1 ; ; echo 2
    > bash: syntax error near unexpected token ';'
    > ```
    > 
    > * * * * *
    > 
    > You can see how this works from the following transcript, where the second and third dates are *not* separated because the `sleep 10` runs in the background:
    > 
    > ```bash
    > pax> date ; sleep 5 ; date ; sleep 10 & date ; wait
    > Thursday 5 April  09:04:07 AWST 2018
    > Thursday 5 April  09:04:12 AWST 2018
    > [1] 28999
    > Thursday 5 April  09:04:12 AWST 2018
    > [1]+  Done                    sleep 10
    > ```




## line-continuation(`\` ``` ` ```))

### put a line comment for a multi-line command(``` ` ```)

- [bash - How to put a line comment for a multi-line command - Stack Overflow](https://stackoverflow.com/questions/9522631/how-to-put-a-line-comment-for-a-multi-line-command)

    > This is how I do it. Essentially by using Bash's backtick [command substitution](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_03_04.html) one can place these comments anywhere along a long command line even if it is split across lines. I have put the echo command in front of your example so that you can execute the example and see how it works:
    > 
    > ```bash
    > echo CommandName InputFiles `#1st comment`\
    >              --option1 arg1 `#2nd comment`\
    >              --option2 arg2 `#3rd comment`
    > ```
    > 
    > Another example where you can put multiple comments at different points on one line:
    > 
    > ```bash
    > some_cmd --opt1 `#1st comment` --opt2 `#2nd comment` --opt3 `#3rd comment`
    > ```

### input `\` start a new line in bash terminal

- [How to input / start a new line in bash terminal? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/80797/how-to-input-start-a-new-line-in-bash-terminal)

    > When you press `Enter` at the end of:
    > 
    > ```
    > for VARIABLE in file1 file2 file3
    > ```
    > 
    > The shell can't execute anything since that `for` loop is not finished. So instead, it will print a different prompt, the `$PS2` prompt (generally `>`), until you enter the closing `done`.
    > 
    > However, after `>` is displayed, you can't go back to edit the first line.
    > 
    > Alternatively, instead of typing `Enter`, you can type `Ctrl-V``Ctrl-J`. That way, the newline character (aka `^J`) is entered without the current buffer being *accepted*, and you can then go back to editing the first line later on.
    > 
    > In `zsh`, you can press `Alt-Enter` or `Esc``Enter` to insert a newline character without accepting the current buffer. To get the same behavior in `bash`, you can add to your `~/.inputrc`:
    > 
    > ```
    > "\e\C-m": "\026\n"
    > ```
    > 
    > (`\026` being the `^V` character).




# sudo

## trobuleshooting

### fix 'sudo: no tty present and no askpass program specified'

- [linux - How to fix 'sudo: no tty present and no askpass program specified' error? - Stack Overflow](https://stackoverflow.com/questions/21659637/how-to-fix-sudo-no-tty-present-and-no-askpass-program-specified-error)

    > *In Jenkins*:
    > 
    > ```
    > echo '<your-password>' | sudo -S command
    > 
    > ```
    > 
    > *Eg*:-
    > 
    > ```
    > echo '******' | sudo -S service nginx restart
    > 
    > ```
    > 
    > You can use [Mask Password Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Mask+Passwords+Plugin) to hide your password
    > 

# file permission

## What is "umask" and how does it work

- [permissions - What is "umask" and how does it work? - Ask Ubuntu](https://askubuntu.com/questions/44542/what-is-umask-and-how-does-it-work)

    > The umask acts as a set of permissions that applications cannot set on files. It's a file mode creation mask for **processes** and cannot be set for directories itself. Most applications would not create files with execute permissions set, so they would have a default of `666`, which is then modified by the umask.
    > 
    > As you have set the umask to remove the read/write bits for the owner and the read bits for others, a default such as `777` in applications would result in the file permissions being `133`. This would mean that you (and others) could execute the file, and others would be able to write to it.
    > 
    > If you want to make files not be read/write/execute by anyone but the owner, you should use a umask like `077` to turn off those permissions for the group & others.
    > 
    > In contrast, a umask of `000` will make newly created directories readable, writable and descendible for everyone (the permissions will be `777`). Such a umask is highly insecure and you should never set the umask to `000`.
    > 
    > The default umask on Ubuntu is `022` which means that newly created files are readable by everyone, but only writable by the owner:
    > 
    > ```
    > user@computer:~$ touch new-file-name
    > user@computer:~$ ls -dl new-file-name
    > -rw-r--r-- 1 user user 0 Apr  1 19:15 new-file-name
    > 
    > ```
    > 
    > ### Viewing and modifying umask
    > 
    > To view your current umask setting, [open a terminal](https://askubuntu.com/q/38162/6969) and run the command:
    > 
    > ```
    > umask
    > 
    > ```
    > 
    > To change the umask setting of the current shell to something else, say 077, run:
    > 
    > ```
    > umask 077
    > 
    > ```
    > 
    > To test whether this setting works or not, you can create a **new** file (file permissions of an existing file won't be affected) and show information about the file, run:
    > 
    > ```
    > user@computer:~$ touch new-file-name
    > user@computer:~$ ls -dl new-file-name
    > -rw------- 1 user user 0 Apr  1 19:14 new-file-name
    > 
    > ```
    > 
    > The umask setting is inherited by processes started from the same shell. For example, start the text editor GEdit by executing `gedit` in the terminal and save a file using gedit. You'll notice that the newly created file is affected by the same umask setting as in the terminal.
    > 
    > ### Use case: multi-user system
    > 
    > If you are on a system that's shared by multiple users, it's desired that others cannot read files in your home directory. For that, a umask is very useful. Edit `~/.profile` and add a new line with:
    > 
    > ```
    > umask 007
    > 
    > ```
    > 
    > You need to re-login for this umask change in `~/.profile` to take effect. Next, you need to change existing file permissions of files in your home directory by removing the read, write and execute bit for the world. [Open a terminal](https://askubuntu.com/q/38162/6969) and execute:
    > 
    > ```
    > chmod -R o-rwx ~
    > 
    > ```
    > 
    > If you want this umask setting be applied to all users on the system, you could edit the system-wide profile file at `/etc/profile`.
    > 