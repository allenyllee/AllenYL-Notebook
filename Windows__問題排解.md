# Windows__問題排解

<!-- toc --> 
[toc]


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
