# Linux__問題排解4-1_lib

[toc]
<!-- toc --> 

## gcc g++ 

### Check glibc version

- [c - Check glibc version for a particular gcc compiler - Stack Overflow](https://stackoverflow.com/questions/9705660/check-glibc-version-for-a-particular-gcc-compiler)

    > use ldd --version
    > 
    > This should return the glibc version being used i.e.
    > 
    > ```
    > $ ldd --version
    > 
    > ldd (GNU libc) 2.17
    > Copyright (C) 2012 Free Software Foundation, Inc.
    > This is free software; see the source for copying conditions.  There is NO
    > ```
    > 
    > 
    > which is the same result as running my libc library
    > 
    > ```
    > $ /lib/libc.so.6
    > 
    > GNU C Library (GNU libc) stable release version 2.17, by Roland McGrath et al.
    > Copyright (C) 2012 Free Software Foundation, Inc.
    > This is free software; see the source for copying conditions.
    > ```
    > 
    > ---
    > 
    > Use `-print-file-name` `gcc` option:
    > 
    > ```
    > $ gcc -print-file-name=libc.so
    > /usr/lib/gcc/x86_64-redhat-linux/4.5.1/../../../../lib64/libc.so
    > ```
    > 
    > That gives the path. Now:
    > 
    > ```
    > $ file /usr/lib/gcc/x86_64-redhat-linux/4.5.1/../../../../lib64/libc.so
    > /usr/lib/gcc/x86_64-redhat-linux/4.5.1/../../../../lib64/libc.so: ASCII C program text
    > 
    > $ cat /usr/lib/gcc/x86_64-redhat-linux/4.5.1/../../../../lib64/libc.so
    > /* GNU ld script
    >    Use the shared library, but some functions are only in
    >    the static library, so try that secondarily.  */
    > OUTPUT_FORMAT(elf64-x86-64)
    > GROUP ( /lib64/libc.so.6 /usr/lib64/libc_nonshared.a  AS_NEEDED ( /lib64/ld-linux-x86-64.so.2 ) )
    > ```
    > 
    > Looks like a linker script. `libc` is special on Linux in that it can be executed:
    > 
    > ```
    > $ /lib64/libc.so.6
    > GNU C Library stable release version 2.13, by Roland McGrath et al.
    > Copyright (C) 2011 Free Software Foundation, Inc.
    > This is free software; see the source for copying conditions.
    > There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A
    > PARTICULAR PURPOSE.
    > Compiled by GNU CC version 4.5.1 20100924 (Red Hat 4.5.1-4).
    > Compiled on a Linux 2.6.35 system on 2011-08-05.
    > Available extensions:
    >     Support for some architectures added on, not maintained in glibc core.
    >     The C stubs add-on version 2.1.2.
    >     crypt add-on version 2.1 by Michael Glad and others
    >     GNU Libidn by Simon Josefsson
    >     Native POSIX Threads Library by Ulrich Drepper et al
    >     BIND-8.2.3-T5B
    >     RT using linux kernel aio
    > libc ABIs: UNIQUE IFUNC
    > For bug reporting instructions, please see:
    > <http://www.gnu.org/software/libc/bugs.html>.
    > ```
    > 
    > ---
    > 
    > Write a test program (name it for example `glibc-version.c`):
    > 
    > ```
    > #include <stdio.h>
    > #include <stdlib.h>
    > #include <gnu/libc-version.h>
    > 
    > int main(int argc, char *argv[]) {
    >   printf("GNU libc version: %s\n", gnu_get_libc_version());
    >   exit(EXIT_SUCCESS);
    > }
    > ```
    > 
    > and compile it with the gcc-4.4 compiler:
    > 
    > ```
    > gcc-4.4 glibc-version.c -o glibc-version
    > ```
    > 
    > When you execute `./glibc-version` the used glibc version is shown.
    > 
    > ---
    > 
    > `gnu_get_libc_version` identifies the *runtime* version of the GNU C Library.
    > 
    > If what you care about is the *compile-time* version (that is, the version that provided the headers in `/usr/include`), you should look at the macros `__GLIBC__` and `__GLIBC_MINOR__`. These expand to positive integers, and will be defined as a side-effect of including *any* header file provided by the GNU C Library; this means you can include a standard header, and then use `#ifdef __GLIBC__` to decide whether you can include a nonstandard header like `gnu/libc-version.h`.
    > 
    > Expanding the test program from the accepted answer:
    > 
    > ```
    > #include <stdio.h>
    > #ifdef __GLIBC__
    > #include <gnu/libc-version.h>
    > #endif
    > 
    > int
    > main(void)
    > {
    > #ifdef __GLIBC__
    >   printf("GNU libc compile-time version: %u.%u\n", __GLIBC__, __GLIBC_MINOR__);
    >   printf("GNU libc runtime version:      %s\n", gnu_get_libc_version());
    >   return 0;
    > #else
    >   puts("Not the GNU C Library");
    >   return 1;
    > #endif
    > }
    > ```
    > 
    > When I compile and run this program on the computer I'm typing this answer on (which is a Mac) it prints
    > 
    > ```
    > Not the GNU C Library
    > ```
    > 
    > but when compiled and run on a nearby Linux box it prints
    > 
    > ```
    > GNU libc compile-time version: 2.24
    > GNU libc runtime version:      2.24
    > ```
    > 
    > Under normal circumstances, the "runtime" version could be bigger than the "compile-time" version, but never smaller. The major version number is unlikely ever to change again (the last time it changed was the "libc6 transition" in 1997).
    > 
    > If you would prefer a shell 'one-liner' to dump these macros, use:
    > 
    > ```
    > echo '#include <errno.h>' | gcc -xc - -E -dM |
    >     grep -E '^#define __GLIBC(|_MINOR)__ ' | sort
    > ```
    > 
    > The `grep` pattern is chosen to match only the two macros that are relevant, because there are dozens of internal macros named `__GLIBC_somethingorother` that you don't want to have to read through.



### libstdc++.so.6: version `GLIBCXX_3.4.20' not found

- [ubuntu 16.04 - libstdc++.so.6: version `GLIBCXX_3.4.20' not found - Stack Overflow](https://stackoverflow.com/questions/44773296/libstdc-so-6-version-glibcxx-3-4-20-not-found)

    > This is table of versions of `gcc` and versions of appropriate `libstdc++`:
    > 
    > > ```
    > > GCC 4.9.0: libstdc++.so.6.0.20
    > > GCC 5.1.0: libstdc++.so.6.0.21
    > > GCC 6.1.0: libstdc++.so.6.0.22
    > > GCC 7.1.0: libstdc++.so.6.0.23
    > > GCC 7.2.0: libstdc++.so.6.0.24
    > > GCC 8.0.0: libstdc++.so.6.0.25
    > >
    > > ```
    > 
    > ( full list of versions is [here](https://gcc.gnu.org/onlinedocs/libstdc++/manual/abi.html) )
    > 
    > It is not dependent from how to install gcc - it may be installed from package or compiled and installed from sources.
    > 
    > It is possible that system gcc libraries is available instead of newely installed. So need to specify environment variable where to find libraries for example in command line like this:
    > 
    > ```
    > $ LD_LIBRARY_PATH=/usr/local/lib64 command args ...
    > 
    > ```
    > 
    > ---
    > 
    > You can check if you get GLIBCXX desired version like this:
    > 
    > ```
    > strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBCXX
    > 
    > ```


### install latest gcc on Ubuntu

- [How to install latest gcc on Ubuntu LTS (12.04, 14.04, 16.04)](https://gist.github.com/application2000/73fd6f4bf1be6600a2cf9f56315a2d91)

    > **GCC 7.1** on Ubuntu 14.04 & 16.04:
    > 
    > ```
    > sudo apt-get update -y &&\
    > sudo apt-get upgrade -y &&\
    > sudo apt-get dist-upgrade -y &&\
    > sudo apt-get install build-essential software-properties-common -y &&\
    > sudo add-apt-repository ppa:ubuntu-toolchain-r/test -y &&\
    > sudo apt-get update -y &&\
    > sudo apt-get install gcc-7 g++-7 -y &&\
    > sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 60 --slave /usr/bin/g++ g++ /usr/bin/g++-7 &&\
    > sudo update-alternatives --config gcc
    > 
    > ```

    > **GCC 8.1.0** on Ubuntu 14.04 & 16.04 & 18.04:
    > ```
    > sudo apt-get update -y &&\
    > sudo apt-get upgrade -y &&\
    > sudo apt-get dist-upgrade -y &&\
    > sudo apt-get install build-essential software-properties-common -y &&\
    > sudo add-apt-repository ppa:ubuntu-toolchain-r/test -y &&\
    > sudo apt-get update -y &&\
    > sudo apt-get install gcc-8 g++-8 -y &&\
    > sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 60 --slave /usr/bin/g++ g++ /usr/bin/g++-8 &&\
    > sudo update-alternatives --config gcc
    > ```
    > 
    > ---
    > 
    > ```
    > gcc --version
    > gcc (Ubuntu 8-20180424-0ubuntu1~16.04.1) 8.0.1 20180424 (experimental) [trunk revision 259590]
    > ```
    > 

- [Install gcc-8 only on Ubuntu 18.04? - Ask Ubuntu](https://askubuntu.com/questions/1028601/install-gcc-8-only-on-ubuntu-18-04)

    > Use [`update-alternatives`](https://linux.die.net/man/8/update-alternatives) for having `gcc` redirected automatically to `gcc-8`:
    > 
    > ```
    > sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 700 --slave /usr/bin/g++ g++ /usr/bin/g++-7
    > sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 800 --slave /usr/bin/g++ g++ /usr/bin/g++-8
    > 
    > ```
    > 
    > This will give you the convenience of gcc being at the latest version, and still you will be able to invoke `gcc-7` or `gcc-8` directly.
    > 
    > If you'll wish to change the default gcc version later on, run `sudo update-alternatives --config gcc`. It will bring a prompt similar to this, which lets you pick the version to be used:
    > 
    > ```
    > There are 2 choices for the alternative gcc (providing /usr/bin/gcc).
    > 
    >   Selection    Path            Priority   Status
    > ------------------------------------------------------------
    > * 0            /usr/bin/gcc-8   800       auto mode
    >   1            /usr/bin/gcc-7   700       manual mode
    >   2            /usr/bin/gcc-8   800       manual mode
    > 
    > Press <enter> to keep the current choice[*], or type selection number:
    > 
    > ```
    > 
    > The higher priority is the one that is picked automatically by `update-alternatives`.
    > 

### Segmentation Fault

- [c++ - Segmentation Fault before main() when using glut, and std::string? - Stack Overflow](https://stackoverflow.com/questions/31579243/segmentation-fault-before-main-when-using-glut-and-stdstring)

    > By the way you can try also
    > 
    > ```
    > LD_PRELOAD=/lib64/libpthread.so.0 ./main
    > ```
    > 
    > in order to make sure that `pthread_key_create` is loaded before other symbols.
    > 
    > ---
    > 
    > I met a similar problem, but `LD_PRELOAD=/lib/x86_64-linux-gnu/libpthread.so.0 ./main` not allways worked. This problem happened on NVIDIA GPU, OpenGL is linked to `/usr/lib/nvidia-352/libGL.so.1`,after tested on different computers, I find changing g++ version to g++-5 works, or linking to 'mesa/libGL.so', another OpenGL implementation, by `g++ main.cpp -o main -Wl, --rpath /usr/lib/x86_64-linux-gnu/mesa -lGLU -lGL -lglut`.
    > 
    > ---
    > 
    > You could see what dependencies both your program and libGL have by running `ldd` - this shows compile-time dependencies.
    > 

### Segmentation Fault: how to debug 

- [【已解决】Linux下出现Segmentation Fault（core dump）错误 - CSDN博客](https://blog.csdn.net/YSBJ123/article/details/50035169)

    > 今天被这个问题搞了半个小时，后来通过添加printf(...)语句的方法找到了错误原因，是因为在程序中错误的输出一个为空的字符串导致。。。
    > 
    > 博客地址：<http://www.cnblogs.com/panfeng412/archive/2011/11/06/segmentation-fault-in-linux.html>
    > 
    > 1\. 段错误是什么
    > ==========
    > 
    > 一句话来说，段错误是指访问的内存超出了系统给这个程序所设定的内存空间，例如访问了不存在的内存地址、访问了系统保护的内存地址、访问了只读的内存地址等等情况。这里贴一个对于"段错误"的准确定义（参考Answers.com）：
    > 
    > 
    > 
    > A segmentation fault (often shortened to segfault) is a particular error condition that can occur during the operation of computer software. In short, a segmentation fault occurs when a program attempts to access a memory location that it is not allowed to access, or attempts to access a memory location in a way that is not allowed (e.g., attempts to write to a read-only location, or to overwrite part of the operating system). Systems based on processors like the Motorola 68000 tend to refer to these events as Address or Bus errors.
    > 
    > Segmentation is one approach to memory management and protection in the operating system. It has been superseded by paging for most purposes, but much of the terminology of segmentation is still used, "segmentation fault" being an example. Some operating systems still have segmentation at some logical level although paging is used as the main memory management policy.
    > 
    > On Unix-like operating systems, a process that accesses invalid memory receives the SIGSEGV signal. On Microsoft Windows, a process that accesses invalid memory receives the STATUS_ACCESS_VIOLATION exception.
    > 
    > 
    > 
    > 2\. 段错误产生的原因
    > ============
    > 
    > 2.1 访问不存在的内存地址
    > --------------
    > 
    > 
    > ```c
    > #include<stdio.h>
    > #include<stdlib.h>
    > void main()
    > {
    >         int *ptr = NULL;
    >         *ptr = 0;
    > }
    > ```
    > 
    > 
    > 2.2 访问系统保护的内存地址
    > ---------------
    > 
    > 
    > ```c
    > #include<stdio.h>
    > #include<stdlib.h>
    > void main()
    > {
    >         int *ptr = (int *)0;
    >         *ptr = 100;
    > }
    > ```
    > 
    > 
    > 2.3 访问只读的内存地址
    > -------------
    > 
    > 
    > ```c
    > #include<stdio.h>
    > #include<stdlib.h>
    > #include<string.h>
    > void main()
    > {
    >         char *ptr = "test";
    >         strcpy(ptr, "TEST");
    > }
    > ```
    > 
    > 
    > 2.4 栈溢出
    > -------
    > 
    > 
    > ```c
    > #include<stdio.h>
    > #include<stdlib.h>
    > void main()
    > {
    >         main();
    > }
    > ```
    > 
    > 
    > 等等其他原因。
    > 
    > 3\. 段错误信息的获取
    > ============
    > 
    > 程序发生段错误时，提示信息很少，下面有几种查看段错误的发生信息的途径。
    > 
    > 3.1 dmesg
    > ---------
    > 
    > dmesg可以在应用程序crash掉时，显示内核中保存的相关信息。如下所示，通过dmesg命令可以查看发生段错误的程序名称、引起段错误发生的内存地址、指令指针地址、堆栈指针地址、错误代码、错误原因等。以程序2.3为例：
    > ```
    > panfeng@ubuntu:~/segfault$ dmesg
    > [ 2329.479037] segfault3[2700]: segfault at 80484e0 ip 00d2906a sp bfbbec3c error 7 in libc-2.10.1.so[cb4000+13e000]
    > ```
    > 3.2 -g
    > ------
    > 
    > 使用gcc编译程序的源码时，加上-g参数，这样可以使得生成的二进制文件中加入可以用于gdb调试的有用信息。以程序2.3为例：
    > ```
    > panfeng@ubuntu:~/segfault$ gcc -g -o segfault3 segfault3.c
    > ```
    > 3.3 nm
    > ------
    > 
    > 使用nm命令列出二进制文件中的符号表，包括符号地址、符号类型、符号名等，这样可以帮助定位在哪里发生了段错误。以程序2.3为例：
    > 
    > 
    > ```asm
    > panfeng@ubuntu:~/segfault$ nm segfault3
    > 08049f20 d _DYNAMIC
    > 08049ff4 d _GLOBAL_OFFSET_TABLE_
    > 080484dc R _IO_stdin_used
    >          w _Jv_RegisterClasses
    > 08049f10 d __CTOR_END__
    > 08049f0c d __CTOR_LIST__
    > 08049f18 D __DTOR_END__
    > 08049f14 d __DTOR_LIST__
    > 080484ec r __FRAME_END__
    > 08049f1c d __JCR_END__
    > 08049f1c d __JCR_LIST__
    > 0804a014 A __bss_start
    > 0804a00c D __data_start
    > 08048490 t __do_global_ctors_aux
    > 08048360 t __do_global_dtors_aux
    > 0804a010 D __dso_handle
    >          w __gmon_start__
    > 0804848a T __i686.get_pc_thunk.bx
    > 08049f0c d __init_array_end
    > 08049f0c d __init_array_start
    > 08048420 T __libc_csu_fini
    > 08048430 T __libc_csu_init
    >          U __libc_start_main@@GLIBC_2.0
    > 0804a014 A _edata
    > 0804a01c A _end
    > 080484bc T _fini
    > 080484d8 R _fp_hw
    > 080482bc T _init
    > 08048330 T _start
    > 0804a014 b completed.6990
    > 0804a00c W data_start
    > 0804a018 b dtor_idx.6992
    > 080483c0 t frame_dummy
    > 080483e4 T main
    >          U memcpy@@GLIBC_2.0
    > ```
    > 
    > 
    > 3.4 ldd
    > -------
    > 
    > 使用ldd命令查看二进制程序的共享链接库依赖，包括库的名称、起始地址，这样可以确定段错误到底是发生在了自己的程序中还是依赖的共享库中。以程序2.3为例：
    > ```
    > panfeng@ubuntu:~/segfault$ ldd ./segfault3
    >     linux-gate.so.1 =>  (0x00e08000)
    >     libc.so.6 => /lib/tls/i686/cmov/libc.so.6 (0x00675000)
    >     /lib/ld-linux.so.2 (0x00482000)
    > ```
    > 4\. 段错误的调试方法
    > ============
    > 
    > 4.1 使用printf输出信息
    > ----------------
    > 
    > 这个是看似最简单但往往很多情况下十分有效的调试方式，也许可以说是程序员用的最多的调试方式。简单来说，就是在程序的重要代码附近加上像printf这类输出信息，这样可以跟踪并打印出段错误在代码中可能出现的位置。
    > 
    > 为了方便使用这种方法，可以使用条件编译指令#ifdef DEBUG和#endif把printf函数包起来。这样在程序编译时，如果加上-DDEBUG参数就能查看调试信息；否则不加该参数就不会显示调试信息。
    > 
    > 4.2 使用gcc和gdb
    > -------------
    > 
    > ### 4.2.1 调试步骤
    > 
    >  1、为了能够使用gdb调试程序，在编译阶段加上-g参数，以程序2.3为例：
    > 
    > panfeng@ubuntu:~/segfault$ gcc -g -o segfault3 segfault3.c
    > 
    > 2、使用gdb命令调试程序：
    > 
    > 
    > ```
    > panfeng@ubuntu:~/segfault$ gdb ./segfault3
    > GNU gdb (GDB) 7.0-ubuntu
    > Copyright (C) 2009 Free Software Foundation, Inc.
    > License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
    > This is free software: you are free to change and redistribute it.
    > There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
    > and "show warranty" for details.
    > This GDB was configured as "i486-linux-gnu".
    > For bug reporting instructions, please see:
    > <http://www.gnu.org/software/gdb/bugs/>...
    > Reading symbols from /home/panfeng/segfault/segfault3...done.
    > (gdb)
    > ```
    > 
    > 
    > 3、进入gdb后，运行程序：
    > 
    > 
    > ```
    > (gdb) run
    > Starting program: /home/panfeng/segfault/segfault3
    > 
    > Program received signal SIGSEGV, Segmentation fault.
    > 0x001a306a in memcpy () from /lib/tls/i686/cmov/libc.so.6
    > (gdb)
    > ```
    > 
    > 
    > 从输出看出，程序2.3收到SIGSEGV信号，触发段错误，并提示地址0x001a306a、调用memcpy报的错，位于/lib/tls/i686/cmov/libc.so.6库中。
    > 
    > 4、完成调试后，输入quit命令退出gdb：
    > 
    > 
    > ```
    > (gdb) quit
    > A debugging session is active.
    > 
    >     Inferior 1 [process 3207] will be killed.
    > 
    > Quit anyway? (y or n) y
    > ```
    > 
    > 
    > ### 4.2.2 适用场景
    > 
    > 1、仅当能确定程序一定会发生段错误的情况下使用。
    > 
    > 2、当程序的源码可以获得的情况下，使用-g参数编译程序。
    > 
    > 3、一般用于测试阶段，生产环境下gdb会有副作用：使程序运行减慢，运行不够稳定，等等。
    > 
    > 4、即使在测试阶段，如果程序过于复杂，gdb也不能处理。
    > 
    > 4.3 使用core文件和gdb
    > ----------------
    > 
    > 在4.2节中提到段错误会触发SIGSEGV信号，通过man 7 signal，可以看到SIGSEGV默认的handler会打印段错误出错信息，并产生core文件，由此我们可以借助于程序异常退出时生成的core文件中的调试信息，使用gdb工具来调试程序中的段错误。
    > 
    > ### 4.3.1 调试步骤
    > 
    > 1、在一些Linux版本下，默认是不产生core文件的，首先可以查看一下系统core文件的大小限制：
    > ```
    > panfeng@ubuntu:~/segfault$ ulimit -c
    > 0
    > ```
    > 2、可以看到默认设置情况下，本机Linux环境下发生段错误时不会自动生成core文件，下面设置下core文件的大小限制（单位为KB）：
    > ```
    > panfeng@ubuntu:~/segfault$ ulimit -c 1024
    > panfeng@ubuntu:~/segfault$ ulimit -c
    > 1024
    > ```
    > 3、运行程序2.3，发生段错误生成core文件：
    > ```
    > panfeng@ubuntu:~/segfault$ ./segfault3
    > 段错误 (core dumped)
    > ```
    > 4、加载core文件，使用gdb工具进行调试：
    > 
    > 
    > ```
    > panfeng@ubuntu:~/segfault$ gdb ./segfault3 ./core
    > GNU gdb (GDB) 7.0-ubuntu
    > Copyright (C) 2009 Free Software Foundation, Inc.
    > License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
    > This is free software: you are free to change and redistribute it.
    > There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
    > and "show warranty" for details.
    > This GDB was configured as "i486-linux-gnu".
    > For bug reporting instructions, please see:
    > <http://www.gnu.org/software/gdb/bugs/>...
    > Reading symbols from /home/panfeng/segfault/segfault3...done.
    > 
    > warning: Can't read pathname for load map: 输入/输出错误.
    > Reading symbols from /lib/tls/i686/cmov/libc.so.6...(no debugging symbols found)...done.
    > Loaded symbols for /lib/tls/i686/cmov/libc.so.6
    > Reading symbols from /lib/ld-linux.so.2...(no debugging symbols found)...done.
    > Loaded symbols for /lib/ld-linux.so.2
    > Core was generated by `./segfault3'.
    > Program terminated with signal 11, Segmentation fault.
    > #0  0x0018506a in memcpy () from /lib/tls/i686/cmov/libc.6
    > ```
    > 
    > 
    > 从输出看出，同4.2.1中一样的段错误信息。
    > 
    > 5、完成调试后，输入quit命令退出gdb：
    > ```
    > (gdb) quit
    > ```
    > ### 4.3.2 适用场景
    > 
    > 1、适合于在实际生成环境下调试程序的段错误（即在不用重新发生段错误的情况下重现段错误）。
    > 
    > 2、当程序很复杂，core文件相当大时，该方法不可用。
    > 
    > 4.4 使用objdump
    > -------------
    > 
    > ### 4.4.1 调试步骤
    > 
    > 1、使用dmesg命令，找到最近发生的段错误输出信息：
    > ```
    > panfeng@ubuntu:~/segfault$ dmesg
    > ... ...
    > [17257.502808] segfault3[3320]: segfault at 80484e0 ip 0018506a sp bfc1cd6c error 7 in libc-2.10.1.so[110000+13e000]
    > ```
    > 其中，对我们接下来的调试过程有用的是发生段错误的地址：80484e0和指令指针地址：0018506a。
    > 
    > 2、使用objdump生成二进制的相关信息，重定向到文件中：
    > ```
    > panfeng@ubuntu:~/segfault$ objdump -d ./segfault3 > segfault3Dump
    > ```
    > 其中，生成的segfault3Dump文件中包含了二进制文件的segfault3的汇编代码。
    > 
    > 3、在segfault3Dump文件中查找发生段错误的地址：
    > 
    > 
    > ```asm
    > panfeng@ubuntu:~/segfault$ grep -n -A 10 -B 10 "80484e0" ./segfault3Dump
    > 121- 80483df:    ff d0                    call   *%eax
    > 122- 80483e1:    c9                       leave
    > 123- 80483e2:    c3                       ret
    > 124- 80483e3:    90                       nop
    > 125-
    > 126-080483e4 <main>:
    > 127- 80483e4:    55                       push   %ebp
    > 128- 80483e5:    89 e5                    mov    %esp,%ebp
    > 129- 80483e7:    83 e4 f0                 and    $0xfffffff0,%esp
    > 130- 80483ea:    83 ec 20                 sub    $0x20,%esp
    > 131: 80483ed:    c7 44 24 1c e0 84 04     movl   $0x80484e0,0x1c(%esp)
    > 132- 80483f4:    08
    > 133- 80483f5:    b8 e5 84 04 08           mov    $0x80484e5,%eax
    > 134- 80483fa:    c7 44 24 08 05 00 00     movl   $0x5,0x8(%esp)
    > 135- 8048401:    00
    > 136- 8048402:    89 44 24 04              mov    %eax,0x4(%esp)
    > 137- 8048406:    8b 44 24 1c              mov    0x1c(%esp),%eax
    > 138- 804840a:    89 04 24                 mov    %eax,(%esp)
    > 139- 804840d:    e8 0a ff ff ff           call   804831c <memcpy@plt>
    > 140- 8048412:    c9                       leave
    > 141- 8048413:    c3                       ret
    > ```
    > 
    > 
    > 通过对以上汇编代码分析，得知段错误发生main函数，对应的汇编指令是movl $0x80484e0,0x1c(%esp)，接下来打开程序的源码，找到汇编指令对应的源码，也就定位到段错误了。
    > 
    > ### 4.4.2 适用场景
    > 
    > 1、不需要-g参数编译，不需要借助于core文件，但需要有一定的汇编语言基础。
    > 
    > 2、如果使用了gcc编译优化参数（-O1，-O2，-O3）的话，生成的汇编指令将会被优化，使得调试过程有些难度。
    > 
    > 4.5 使用catchsegv
    > ---------------
    > 
    > catchsegv命令专门用来扑获段错误，它通过动态加载器（ld-linux.so）的预加载机制（PRELOAD）把一个事先写好的库（/lib/libSegFault.so）加载上，用于捕捉断错误的出错信息。
    > 
    > 
    > ```asm
    > panfeng@ubuntu:~/segfault$ catchsegv ./segfault3
    > Segmentation fault (core dumped)
    > *** Segmentation fault
    > Register dump:
    > 
    >  EAX: 00000000   EBX: 00fb3ff4   ECX: 00000002   EDX: 00000000
    >  ESI: 080484e5   EDI: 080484e0   EBP: bfb7ad38   ESP: bfb7ad0c
    > 
    >  EIP: 00ee806a   EFLAGS: 00010203
    > 
    >  CS: 0073   DS: 007b   ES: 007b   FS: 0000   GS: 0033   SS: 007b
    > 
    >  Trap: 0000000e   Error: 00000007   OldMask: 00000000
    >  ESP/signal: bfb7ad0c   CR2: 080484e0
    > 
    > Backtrace:
    > /lib/libSegFault.so[0x3b606f]
    > ??:0(??)[0xc76400]
    > /lib/tls/i686/cmov/libc.so.6(__libc_start_main+0xe6)[0xe89b56]
    > /build/buildd/eglibc-2.10.1/csu/../sysdeps/i386/elf/start.S:122(_start)[0x8048351]
    > 
    > Memory map:
    > 
    > 00258000-00273000 r-xp 00000000 08:01 157 /lib/ld-2.10.1.so
    > 00273000-00274000 r--p 0001a000 08:01 157 /lib/ld-2.10.1.so
    > 00274000-00275000 rw-p 0001b000 08:01 157 /lib/ld-2.10.1.so
    > 003b4000-003b7000 r-xp 00000000 08:01 13105 /lib/libSegFault.so
    > 003b7000-003b8000 r--p 00002000 08:01 13105 /lib/libSegFault.so
    > 003b8000-003b9000 rw-p 00003000 08:01 13105 /lib/libSegFault.so
    > 00c76000-00c77000 r-xp 00000000 00:00 0 [vdso]
    > 00e0d000-00e29000 r-xp 00000000 08:01 4817 /lib/libgcc_s.so.1
    > 00e29000-00e2a000 r--p 0001b000 08:01 4817 /lib/libgcc_s.so.1
    > 00e2a000-00e2b000 rw-p 0001c000 08:01 4817 /lib/libgcc_s.so.1
    > 00e73000-00fb1000 r-xp 00000000 08:01 1800 /lib/tls/i686/cmov/libc-2.10.1.so
    > 00fb1000-00fb2000 ---p 0013e000 08:01 1800 /lib/tls/i686/cmov/libc-2.10.1.so
    > 00fb2000-00fb4000 r--p 0013e000 08:01 1800 /lib/tls/i686/cmov/libc-2.10.1.so
    > 00fb4000-00fb5000 rw-p 00140000 08:01 1800 /lib/tls/i686/cmov/libc-2.10.1.so
    > 00fb5000-00fb8000 rw-p 00000000 00:00 0
    > 08048000-08049000 r-xp 00000000 08:01 303895 /home/panfeng/segfault/segfault3
    > 08049000-0804a000 r--p 00000000 08:01 303895 /home/panfeng/segfault/segfault3
    > 0804a000-0804b000 rw-p 00001000 08:01 303895 /home/panfeng/segfault/segfault3
    > 09432000-09457000 rw-p 00000000 00:00 0 [heap]
    > b78cf000-b78d1000 rw-p 00000000 00:00 0
    > b78df000-b78e1000 rw-p 00000000 00:00 0
    > bfb67000-bfb7c000 rw-p 00000000 00:00 0 [stack]
    > ```
    > 
    > 
    > 5\. 一些注意事项
    > ==========
    > 
    > 1、出现段错误时，首先应该想到段错误的定义，从它出发考虑引发错误的原因。
    > 
    > 2、在使用指针时，定义了指针后记得初始化指针，在使用的时候记得判断是否为NULL。
    > 
    > 3、在使用数组时，注意数组是否被初始化，数组下标是否越界，数组元素是否存在等。
    > 
    > 4、在访问变量时，注意变量所占地址空间是否已经被程序释放掉。
    > 
    > 5、在处理变量时，注意变量的格式控制是否合理等。
    > 
    > 6\. 参考资料列表
    > ==========
    > 
    > 1、http://www.docin.com/p-105923877.html
    > 
    > 2、http://blog.chinaunix.net/space.php?uid=317451&do=blog&id=92412


## GUI app

### BadDrawable (invalid Pixmap or Window parameter)/X Error: BadAccess (attempt to access private resource denied)/X Error: BadShmSeg (invalid shared segment parameter)

- [attempt to access private resource denied · Issue #21 · osrf/docker_images](https://github.com/osrf/docker_images/issues/21)

    > alternative solution is to pass `--ipc host` and take advantage of MIT-SHM performance
    > 
    > ---
    > 
    > > The MIT-SHM is an extension to the X server which allows faster transactions by using shared memory.
    > 
    > docker's --ipc setting: <https://docs.docker.com/engine/reference/run/#/ipc-settings-ipc> allows accessing shared memory between x11 and application running in container. But I'm no expert on it either.
    > 
    > It could open security holes though ( I made SO question, hopefully will someone answer <http://stackoverflow.com/questions/38907708/docker-ipc-host-and-security> ), I don't know enough to say for sure. But if you trust application inside (which is this case I suspect) and use docker more for convinience than security, you could just allow it.
    > 
    > PS: GPU benchmark (with `--ipc host`) showed identical performance in container and on host system (well technically the container was .5 FPS faster :) ).




- [BadDrawable (invalid Pixmap or Window parameter) · Issue #53 · P0cL4bs/WiFi-Pumpkin](https://github.com/P0cL4bs/WiFi-Pumpkin/issues/53)

    > add this line `QT_X11_NO_MITSHM=1` in ~/.profile file. or (ie: system env var).
    > 
    > ```source-shell
    > export QT_X11_NO_MITSHM=1
    > ```

- [ubuntu 16.10 xserver bad access · Issue #66 · unetbootin/unetbootin](https://github.com/unetbootin/unetbootin/issues/66)

    > a temporary workaround is to run it with
    > ```
    > sudo QT_X11_NO_MITSHM=1 unetbootin
    > ```
    > 




### vulkan smoketest black screen

- [Installing nvidia vulkan drivers for 16.04 - Ask Ubuntu](https://askubuntu.com/questions/774131/installing-nvidia-vulkan-drivers-for-16-04)

    > I had the same issue, until I uninstalled `mesa-vulkan-drivers`. DOTA2 then immediately started with the `-vulkan` option. Also `vulkaninfo` gives me a lot more output now, without the error.
    > 
    > ---
    > 
    > Downlad the sdk <https://lunarg.com/vulkan-sdk/>
    > 
    > Run the sdk, copy the extracted folder to some location and add the following path variables
    > 
    > ```
    > export LD_LIBRARY_PATH=$HOME/VulkanSDK/1.0.21.1/x86_64/lib
    > export VK_LAYER_PATH=$HOME/VulkanSDK/1.0.21.1/x86_64/etc/explicit_layer.d
    > 
    > ```
    > 
    > You may need to adjust the path.
    > 
    > That is all you need to do.
    > 
    > The sdk is completely optional, but this should get you get started.
    > 
    > 


### install vulkan SDK

- [pmathia0/gcc-cmake-vulkan - Docker Hub](https://hub.docker.com/r/pmathia0/gcc-cmake-vulkan/~/dockerfile/)

    > ```
    > RUN wget -O VulkanSDK.run https://sdk.lunarg.com/sdk/download/1.0.61.0/linux/vulkansdk-linux-x86_64-1.0.61.0.run?u= && \
    >     chmod ugo+x VulkanSDK.run
    > 
    > RUN ./VulkanSDK.run
    > RUN cd VulkanSDK/1.0.61.0
    > ENV VULKAN_SDK="/VulkanSDK/1.0.61.0/x86_64:${VULKAN_SDK}"
    > ENV PATH="${VULKAN_SDK}/bin:${PATH}"
    > ENV LD_LIBRARY_PATH="${VULKAN_SDK}/lib:${LD_LIBRARY_PATH}"
    > ENV VK_LAYER_PATH="${VULKAN_SDK}/etc/explicit_layer.d:${VK_LAYER_PATH}"
    > ```
    > 


### OpenGL test

- [How to benchmark your GPU on Linux](https://www.howtoforge.com/tutorial/linux-gpu-benchmark/)

    > GLX-Gears
    > ---------
    > 
    > GLX gears is a popular OpenGL test that is part of the "mesa-utils" package. Install the package on Ubuntu with this command:
    > ```
    > sudo apt-get install mesa-utils
    > ```
    > You can invoke it by typing "glxgears" on a terminal.
    > ```
    > glxgears
    > ```
    > ---
    > 
    > GL Mark 2
    > ---------
    > 
    > GL mark is a much richer benchmarking tool developed by the kind people behind the Linaro distribution. Contrary to glxgears, glmark offers a rich set of tests that concern different aspects of your graphics unit performance (buffering, building, lighting, texturing etc), allowing for a much more comprehensive and meaningful test. Each test is conducted for 10 seconds and the frame rate is counted individually. In the end, users get a performance score based on all previous tests. I like this tool for its simplicity and flawless operation. You can find it as a pre-built package in most distributions under the name "glmark2". Install it with:
    > ```
    > sudo apt-get install glmark2
    > ```
    > on Ubuntu.
    > 
    > After installing it, you may run it by typing "glmark2" on a terminal.
    > ```
    > glmark2
    > ```
    > ---
    > 
    > Unigine Benchmark Products
    > --------------------------
    > 
    > Finally, for users that seek something more advanced that the previous two tools, there are four benchmark tools that use the Unigine 3D engine. These are the Valley, Heaven, Tropics and Sanctuary which offer free versions that can be [downloaded](https://unigine.com/products/heaven/download/) from the Unigine website. These benchmarking tools boast real-time ambient occlusion, interplaying lights from different sources, HDR renderings, realistic water and a dynamic sky with atmospheric light scattering. Users may also set the anti-aliasing levels, texture quality and filtering, anisotropy and shader quality. Besides hitting that "benchmark" button that will test your hardware in 10 steps, you may also wander around freely, change the time of day (which changes the lighting of the world) and accurately determine the conditions that "bend" your hardware the most.
    > 
    > 


### install nvidia-docker v1 on ubuntu 18.04

- [NVIDIA/nvidia-docker at 1.0](https://github.com/NVIDIA/nvidia-docker/tree/1.0)

- [Cannot install on Ubuntu 16.10 Yakkety - dependency issues · Issue #234 · NVIDIA/nvidia-docker](https://github.com/NVIDIA/nvidia-docker/issues/234)


    > I followed your suggestion, built and installed successfully in my ubuntu desktop 16.10 box.
    > 
    > I zipped my file and uploaded it here, hope it can help others from clone&edit&docker&make works. :)
    > 
    > [nvidia-docker_1.0.1-yakkety_amd64.deb.zip](https://github.com/NVIDIA/nvidia-docker/files/818401/nvidia-docker_1.0.1-yakkety_amd64.deb.zip)
    > 
    > 
    > Download above then:
    > ```
    > sudo apt-get install ./nvidia-docker_1.0.1-yakkety_amd64.deb
    > ```
    > or
    > 
    > ```
    > sudo dpkg -i ./nvidia-docker_1.0.1-yakkety_amd64.deb
    > ```
    > 
    > 

- [Error looking up volume plugin nvidia-docker: legacy plugin: plugin not found... · Issue #437 · NVIDIA/nvidia-docker](https://github.com/NVIDIA/nvidia-docker/issues/437)

    > 
    > Try `sudo service nvidia-docker start` first.
    > 
    > Try `sudo nvidia-docker-plugin` first.
    > 

## OpenGL issue

### libGL: OpenDriver: trying /usr/lib/x86_64-linux-gnu/dri/tls/swrast_dri.so

- [nividia libGL.so lookup problem · Issue #2 · badlogic/jglfw](https://github.com/badlogic/jglfw/issues/2)

    > show linked library
    > 
    > ```
    > #ldconfig --verbose  | grep libGL.so
    > ```


### libGL error: No matching fbConfigs or visuals found

- [nvidia - Steam: libGL error: No matching fbConfigs or visuals found libGL error: failed to load driver: swrast - Ask Ubuntu](https://askubuntu.com/questions/834254/steam-libgl-error-no-matching-fbconfigs-or-visuals-found-libgl-error-failed-t)

    > **Ubuntu 16.04+** For anyone still getting same error, if you are using nvidia driver, sometimes you will see that libGL.so.1 points to ambiguous libGL provided by both mesa and nvidia. To test this, you can run this command
    > 
    > ```
    > $ sudo ldconfig -p | grep -i gl.so
    > 
    > ```
    > 



## audio app

### Can't initialize OpenAL wrapper. Install latest OpenAL.

- [installation - Unable to locate package openAL - Ask Ubuntu](https://askubuntu.com/questions/122939/unable-to-locate-package-openal)

    > Use the following command in a terminal:
    > 
    > ```
    > sudo apt-get install libalut-dev
    > 
    > ```

### AL lib: (WW) alc_initconfig: Failed to initialize backend "pulse"

- [add audio support in docker container for gazebo simulation · Issue #7 · jacknlliu/ros-docker-images](https://github.com/jacknlliu/ros-docker-images/issues/7)

    > Solution:
    > 
    > ```source-shell
    > docker run --device /dev/snd\
    > 	          -e PULSE_SERVER=unix:${XDG_RUNTIME_DIR}/pulse/native\
    > 	          -v ${XDG_RUNTIME_DIR}/pulse/native:${XDG_RUNTIME_DIR}/pulse/native\
    > 	          --group-add $(getent group audio | cut -d: -f3)
    > ```
    > 
    > In container, we also need the following command to make sure the access to `/dev/snd/*`, if your user in container is not created by `docker run` option `--user` or `USER` in Dockerfile
    > 
    > ```source-shell
    > sudo usermod -aG audio <your_user>
    > 
    > # or directly change the permission of /dev/snd/*
    > # sudo chmod a+rwx /dev/snd/*
    > # this will take effect directly, without restarting your container.
    > ```
    > 
    > And then **restart** your container.
    > 
    > ---
    > 
    > Pulseaudio vs. ALSA
    > ===================
    > 
    > > Pulseaudio is a sound server which allows multiple sound sources to be fed through to one or more sinks. AFAIK Alsa only works with one source at a time.... Actually I think that is wrong and Alsa does support multiple concurrent sources.
    > >
    > > Found this diagram showing what it does:
    > 
    > [![pulseaudio-alsa](https://user-images.githubusercontent.com/6220143/37566280-f1966bec-2af1-11e8-8d17-04a392242422.png)](https://user-images.githubusercontent.com/6220143/37566280-f1966bec-2af1-11e8-8d17-04a392242422.png)
    > 
    > > PulseAudio basically sits atop ALSA, and use it internally. ALSA is unable by itself to be used by multiple applications, so PulseAudio provides this functionality among others.
    > > 
    > 


