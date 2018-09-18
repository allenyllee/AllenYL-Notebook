# Linux__問題排解3-2

[toc]
<!-- toc --> 

# shell

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

## shell scripting

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