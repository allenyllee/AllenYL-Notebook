# Linux__問題排解2-1_Disk

[toc]
<!-- toc --> 

# Hard disk smart tool

## SSD firmware downloads

- [PLEXTOR 浦科特 | Support | Downloads](http://www.goplextor.com/tw/Support/Downloads?p=2)

## flashing firmware on linux

- [Flashing BIOS from Linux - ArchWiki](https://wiki.archlinux.org/index.php/Flashing_BIOS_from_Linux)




## SSD life span

- [SsdReady: Measure solid-state drive life | SSD life time and measurement tool](https://www.ssdready.com/measure/?value=37.7&msr=Gb&submit=Estimate%21)

- [The life span of an SSD – how long does it last and what can be done to take care? | Computer Memory Blog – hints & tips, know-how, wiki, tutorials, troubleshooting, news, purchasing advices](https://www.compuram.de/blog/en/the-life-span-of-a-ssd-how-long-does-it-last-and-what-can-be-done-to-take-care/)

    > Can I calculate the life span of an SSD drive?
    > ----------------------------------------------
    > 
    > The more storage cells an SSD owns, the longer it will work. By having a huge storage capacity the storage cells can be treated with care for much longer because they aren't rewritten that often. The life span of a modern SSD can be calculated with the help of a formula:
    > 
    > ![General formula for life span](https://www.compuram.de/blog/wp-content/uploads/2016/02/formel1eng.jpg)
    > 
    > Let's take the Samsung 850 PRO  as an example. The 850 PRO is an MLC SSD with 3,000 write cycles. The capacity of the drive differs depending on the model, ranging from 512GB to 2TB. The SSD factor specifies the rate of the real amount of data to the actual data written. For the calculation, one chooses a high value of 5. In addition, the amount of data that is written on the drive per year is estimated. If an estimation is difficult, then we recommend to choose a value between 1,500 and 2,000GB.
    > 
    > The life span of a Samsung 850 PRO with 1TB then results in:
    > 
    > ![usage of formula](https://www.compuram.de/blog/wp-content/uploads/2016/02/formel2eng.jpg)
    > 
    > This SSD will probably last incredible 343 years. This isn't a guarantee, but a good forecast. The warranty for the named SSD is ten years. Also, TLC drives don't have to hide. The 1TB model of the Samsung 850 EVO series, which is equipped with the low-priced TLC storage type, can expect a life span of 114 years.
    > 
    > If your SSD is already in usage for a while, then you can calculate the anticipated remaining life time with the help of special tools. The [tool SSDlife](https://ssd-life.com/eng/download-ssdlife.html) calculates the working time so far, the amount of data already written and gives a rating regarding the life span.

- [hard disk - How to check the life left in SSD or the medium's wear level? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/106678/how-to-check-the-life-left-in-ssd-or-the-mediums-wear-level)

    > In your first example, what I think you are referring to is the "Media Wearout Indicator" on Intel drives, which is attribute 233. Yes, it has a range of 0-100, with 100 being a brand new, unused drive, and 0 being completely worn out. According to your ouptut, this field doesn't seem to exist.
    > 
    > In your second example, please read the [official docs about SSD_Life_Left.](http://sourceforge.net/apps/trac/smartmontools/wiki/FAQ#TheSSD_Life_LeftAttributeofmynewSandForcebasedSSDreportszero) Per that page:
    > 
    > > The RAW value of this attribute is always 0 and has no meaning. Check the normalized VALUE instead. It starts at 100 and indicates the approximate percentage of SDD life left. It typically decreases when Flash blocks are marked as bad, see the RAW value of Retired_Block_Count
    > 
    > It's really important that you fully understand what smartctl(8) is saying, and not making assumptions. Unfortunately, the S.M.A.R.T. tools aren't always up to date with the latest SSDs and their attributes. As such, there isn't always a clean way to tell how many times the chips have been written to. Best you can do, is look at the "Power_On_Hours", which in your case is "6568", determine your average disk utilization, and average it out.
    > 
    > You should be able to lookup your drive specs, and determine the process used to make the chips. 32nm process chips will have a longer write endurance than 24nm process chips. However, it seems that "on average", you could probably expect about 3,000 to 4,000 writes, with a minimum of 1,000 and a max of 6,000. So, if you have a 64GB SSD, then you should expect somewhere in the neighborhood of a total of 192TB to 256TB written to the SSD, assuming wear leveling.
    > 
    > As an example, if you're sustaining a utilization of say 11 KBps to your drive, then you could expect to see about 40 MB written per hour. At 6568 powered on hours, you've written roughly 260 GB to disk. Knowing that you could probably sustain about 200 TB of total writes, before failure, you have about 600 years before failure due to wearing out the chips. Your disk will likely fail due to worn out capacitors or voltage regulation.



## smartmomtools/smartctl/smartd

- [檢測硬碟 SMART 健康狀態 · 完全用 GNU/Linux 工作](https://chusiang.gitbooks.io/working-on-gnu-linux/29.checking-hd-smart.html)

    > [S.M.A.R.T.](http://zh.wikipedia.org/wiki/S.M.A.R.T.) 是個用來檢測硬碟健康狀況的指標，雖然前文 [26\. 使用 Clonezilla 打造不死的作業系統](https://chusiang.gitbooks.io/working-on-gnu-linux/26.clonezilla.html) 提供了軟體層面的備份方式，但硬體總有老舊、損壞的一天。而一台電腦中又以硬碟裡的資料最為重要，這裡凍仁將介紹 GNU/Linux 下檢測、監控的方法。
    > 
    > ![2013-10-16-palimpsest-smart.png](https://chusiang.gitbooks.io/working-on-gnu-linux/imgs/2013-10-16-palimpsest-smart.png "2013-10-16-palimpsest-smart.png")
    > 
    > ▲ 在 GNOME 上我們可使用 [磁碟公用程式 (GNOME Disks)](http://en.wikipedia.org/wiki/GNOME_Disks) ^[1](https://chusiang.gitbooks.io/working-on-gnu-linux/29.checking-hd-smart.html#fn_1)^ 來檢測 SMART。
    > 
    > ### 安裝 smartmontools
    > 
    > 套件 smartmontools 包含了 smartctl, smartd，是個可以監控 ATA, SCSI 硬碟 (storage) SMART (Self-Monitoring, Analysis and Reporting Technology System) 狀態的工具。我們可以透過它來進階設定各種硬碟退化、錯誤警告的回報機制。
    > 
    > 安裝文字介面的檢測工具 smartmontools。
    > 
    > ```
    >    # Debian, Ubuntu
    >    $ sudo aptitude install smartmontools
    > 
    >    # CentOS, RHEL, Fedora
    >    $ sudo yum install smartmontools
    > 
    > ```
    > 
    > ### smartctl
    > 
    > smartctl 主要是用來進行一次性、暫時性的硬碟掃描，以下為常見的使用方法。
    > 
    > 1.  查看該媒體是否支援 SMART 檢測。
    > 
    >     ```
    >     # - 啟用 (Enabled)。
    >     $ sudo smartctl -i /dev/sda
    >     smartctl 5.41 2011-06-09 r3365 [x86_64-linux-3.8.0-31-generic] (local build)
    >     Copyright (C) 2002-11 by Bruce Allen, http://smartmontools.sourceforge.net
    > 
    >     === START OF INFORMATION SECTION ===
    >     Device Model:     ST3500413AS
    >     Serial Number:    Z2AAMWCL
    >     LU WWN Device Id: 5 000c50 035f695b1
    >     Firmware Version: JC45
    >     User Capacity:    500,107,862,016 bytes [500 GB]
    >     Sector Size:      512 bytes logical/physical
    >     Device is:        Not in smartctl database [for details use: -P showall]
    >     ATA Version is:   8
    >     ATA Standard is:  ATA-8-ACS revision 4
    >     Local Time is:    Wed Oct 16 21:04:44 2013 CST
    >     SMART support is: Available - device has SMART capability.
    >     SMART support is: Enabled
    > 
    >     # - 停用 (Disabled)。
    >     $ sudo smartctl -i /dev/sda
    >     smartctl 5.41 2011-06-09 r3365 [x86_64-linux-3.8.0-31-generic] (local build)
    >     Copyright (C) 2002-11 by Bruce Allen, http://smartmontools.sourceforge.net
    > 
    >     === START OF INFORMATION SECTION ===
    >     Device Model:     ST3500413AS
    >     Serial Number:    Z2AAMWCL
    >     LU WWN Device Id: 5 000c50 035f695b1
    >     Firmware Version: JC45
    >     User Capacity:    500,107,862,016 bytes [500 GB]
    >     Sector Size:      512 bytes logical/physical
    >     Device is:        Not in smartctl database [for details use: -P showall]
    >     ATA Version is:   8
    >     ATA Standard is:  ATA-8-ACS revision 4
    >     Local Time is:    Wed Oct 16 21:05:36 2013 CST
    >     SMART support is: Available - device has SMART capability.
    >     SMART support is: Disabled
    > 
    >     ```
    > 
    > 2.  若尚未啟用 SMART，可以使用 *-s* 參數開啟它。
    > 
    >     ```
    >     $ sudo smartctl -s on /dev/sda
    >     smartctl 5.41 2011-06-09 r3365 [x86_64-linux-3.8.0-31-generic] (local build)
    >     Copyright (C) 2002-11 by Bruce Allen, http://smartmontools.sourceforge.net
    > 
    >     === START OF ENABLE/DISABLE COMMANDS SECTION ===
    >     SMART Enabled.
    > 
    >     ```
    > 
    > 3.  支援 SMART 後我們可以使用 *-H* 參數來手動檢查硬碟、隨身硬碟的建康狀態。
    > 
    >     ```
    >     # - 通過 (passed)。
    >     $ sudo smartctl -H /dev/sda
    >     smartctl 5.41 2011-06-09 r3365 [x86_64-linux-3.8.0-31-generic] (local build)
    >     Copyright (C) 2002-11 by Bruce Allen, http://smartmontools.sourceforge.net
    > 
    >     === START OF READ SMART DATA SECTION ===
    >     SMART overall-health self-assessment test result: PASSED
    > 
    >     # - 失敗 (failed)。
    >     $ sudo smartctl -H /dev/sda
    >     smartctl 5.41 2011-06-09 r3365 [x86_64-linux-3.8.0-31-generic] (local build)
    >     Copyright (C) 2002-11 by Bruce Allen, http://smartmontools.sourceforge.net
    > 
    >     === START OF READ SMART DATA SECTION ===
    >     SMART overall-health self-assessment test result: FAILED!
    >     Drive failure expected in less than 24 hours. SAVE ALL DATA.
    >     Failed Attributes:
    >     ID# ATTRIBUTE_NAME          FLAG     VALUE WORST THRESH TYPE      UPDATED  WHEN_FAILED RAW_VALUE
    >     5 Reallocated_Sector_Ct   0x0033   004   004   005    Pre-fail  Always   FAILING_NOW 1887
    > 
    >     ```
    > 
    > ### smartd
    > 
    > smartd 是個可以把 smartmontools 註冊成例行性服務 (Daemon) 並使用排程來監控的程式，以下為凍仁啟用的步驟。
    > 
    > 1.  啟用 smartd。
    > 
    >     ```
    >     $ sudo vim /etc/default/smartmontools
    >     ...
    >     start_smartd=yes
    >     smartd_opts="--interval=1800"
    > 
    >     ```
    > 
    > 2.  備份設定檔。
    > 
    >     ```
    >     $ sudo cp /etc/smartd.conf /etc/smartd.conf.ori
    > 
    >     ```
    > 
    > 3.  編輯設定檔。
    > 
    >     ```
    >     $ sudo vi /etc/smartd.conf
    >     ......
    > 
    >     # 掃描所有的 ATA/SCSI 設備並將報告寄送給 root。
    >     DEVICESCAN -d removable -n standby -m root -M exec /usr/share/smartmontools/smartd-runner
    > 
    >     # 每日 02:00 快速檢查 sda，每週六 03:00 完整檢查 sda。
    >     /dev/sda -a -o on -S on -s (S/../.././02|L/../../6/03)
    > 
    >     # 每日 04:00 快速檢查 sdb，每週六 05:00 完整檢查 sdb。
    >     /dev/sdb -a -o on -S on -s (S/../.././04|L/../../6/05)
    > 
    >     # 監控 SMART 狀態
    >     /dev/sda -H -l error -l selftest -t -I 194
    >     /dev/sdb -H -l error -l selftest -t -I 194
    > 
    >     # 安靜的檢查，並只郵寄建康狀態給 admin@example.tw
    >     /dev/sda -H -C 0 -U 0 -m admin@example.tw
    >     /dev/sdb -H -C 0 -U 0 -m admin@example.tw
    >     ......
    > 
    >     ```
    > 
    > 4.  啟用服務
    > 
    >     ```
    >     $ sudo /etc/init.d/smartmontools start
    > 
    >     ```
    > 
    > 5.  觀看記錄檔 (log)。
    > 
    >     ```
    >     $ less /var/log/syslog
    >     ......
    >     Oct 17 08:59:47 thinkpad-t410 smartd[11523]: smartd 5.41 2011-06-09 r3365 [x86_64-linux-3.2.0-4-amd64] (local build)
    >     Oct 17 08:59:47 thinkpad-t410 smartd[11523]: Copyright (C) 2002-11 by Bruce Allen, http://smartmontools.sourceforge.net
    >     Oct 17 08:59:47 thinkpad-t410 smartd[11523]: Opened configuration file /etc/smartd.conf
    >     Oct 17 08:59:47 thinkpad-t410 smartd[11523]: Drive: DEVICESCAN, implied '-a' Directive on line 21 of file /etc/smartd.conf
    >     Oct 17 08:59:47 thinkpad-t410 smartd[11523]: Configuration file /etc/smartd.conf was parsed, found DEVICESCAN, scanning devices
    >     Oct 17 08:59:47 thinkpad-t410 smartd[11523]: Device: /dev/sda, type changed from 'scsi' to 'sat'
    >     Oct 17 08:59:47 thinkpad-t410 smartd[11523]: Device: /dev/sda [SAT], opened
    >     ......
    >     Oct 17 08:59:47 thinkpad-t410 smartd[11523]: Device: /dev/sda [SAT], found in smartd database.
    >     Oct 17 08:59:48 thinkpad-t410 smartd[11523]: Device: /dev/sda [SAT], is SMART capable. Adding to "monitor" list.
    >     Oct 17 08:59:48 thinkpad-t410 smartd[11523]: Device: /dev/sda [SAT], state read from /var/lib/smartmontools/smartd.ST9320423AS-5VH55XKG.ata.state
    >     ......
    >     Oct 17 08:59:48 thinkpad-t410 smartd[11525]: smartd has fork()ed into background mode. New PID=11525.
    >     Oct 17 08:59:48 thinkpad-t410 smartd[11525]: file /var/run/smartd.pid written containing PID 11525
    > 
    >     ```
    > 
    > ※ 若想讓 smartd 使用 Gmail 寄送通知件，可使用 [sSMTP](https://wiki.debian.org/sSMTP) 來達成。如果能再搭上兩步驗證裡的專屬應用程式密碼會安全些。
    > 
    > 當 SMART 亮起紅燈時，請儘速備份並更換硬碟。這時可以先拿先前淘汰的舊硬碟墊擋，否則就趕緊買顆新的補上了！ (若您的硬碟保固還沒過，那您可以換新硬碟了，恭喜！)

- [Monitor SATA and SSD Health with SMART | Linux.com | The source for Linux information](https://www.linux.com/learn/intro-to-linux/2017/3/monitor-sata-and-ssd-health-smart)

    > Using computers involves a lot of detours. Let's get back on track and look at the basic information that `smartctl` prints, using a non-Samsung drive:
    > ```
    > $ sudo smartctl -i /dev/sdb
    > smartctl 6.5 2016-01-24 r4214 [x86_64-linux-4.4.0-64-generic] (local build)
    > Copyright (C) 2002-16, Bruce Allen, Christian Franke, www.smartmontools.org
    > 
    > === START OF INFORMATION SECTION ===
    > Model Family:     Seagate Barracuda 7200.14 (AF)
    > Device Model:     ST2000DM001-1CH164
    > Serial Number:    Z240S0F3
    > LU WWN Device Id: 5 000c50 05080924c
    > Firmware Version: CC26
    > User Capacity:    2,000,398,934,016 bytes [2.00 TB]
    > Sector Sizes:     512 bytes logical, 4096 bytes physical
    > Rotation Rate:    7200 rpm
    > Form Factor:      3.5 inches
    > Device is:        In smartctl database [for details use: -P show]
    > ATA Version is:   ATA8-ACS T13/1699-D revision 4
    > SATA Version is:  SATA 3.0, 6.0 Gb/s (current: 6.0 Gb/s)
    > Local Time is:    Mon Mar  6 10:56:00 2017 PST
    > SMART support is: Available - device has SMART capability.
    > SMART support is: Enabled
    > ```
    > 
    > This is a nice bundle of useful information, containing everything but the date of manufacture. Sometimes, you can visit the manufacturer's site and use the serial number to learn if the drive is still under warranty, and decode the date information. If SMART support is not enabled then enable it:
    > ```
    > $ sudo smartctl -s on /dev/sdb
    > smartctl 6.5 2016-01-24 r4214 [x86_64-linux-4.4.0-64-generic] (local build)
    > Copyright (C) 2002-16, Bruce Allen, Christian Franke, www.smartmontools.org
    > 
    > === START OF ENABLE/DISABLE COMMANDS SECTION ===
    > SMART Enabled.
    > ```
    > 
    > `smartctl -s off [device]` disables it.
    > 
    > Want to see a complete data dump? Use the `-x` option:
    > ```
    > $ sudo smartctl -x /dev/sdb
    > ```
    > 
    > ### Health Check
    > 
    > Let's run a quick health check:
    > ```
    > $ sudo smartctl -H /dev/sdb
    > smartctl 6.5 2016-01-24 r4214 [x86_64-linux-4.4.0-64-generic] (local build)
    > Copyright (C) 2002-16, Bruce Allen, Christian Franke, www.smartmontools.org
    > 
    > === START OF READ SMART DATA SECTION ===
    > SMART overall-health self-assessment test result: PASSED
    > ```
    > 
    > Hurrah! It passed. Use `-Hc` to see more details. Now, just for fun, check the logfile for errors:
    > ```
    > $ sudo smartctl -l error /dev/sdb
    > smartctl 6.5 2016-01-24 r4214 [x86_64-linux-4.4.0-64-generic] (local build)
    > Copyright (C) 2002-16, Bruce Allen, Christian Franke, www.smartmontools.org
    > 
    > === START OF READ SMART DATA SECTION ===
    > SMART Error Log Version: 1
    > No Errors Logged
    > ```
    > 
    > Well, this sure is turning into a boring exercise. Which is fine with me. Some forms of boredom are good. What do you do if there are errors? Consult the [Smartmontools FAQ](https://www.smartmontools.org/wiki/FAQ) which ones are significant.
    > 
    > ### Running Self-Tests
    > 
    > You can run a short and a long self-test: `smartctl -t short /dev/sdb` and `smartctl -t long /dev/sdb`. `smartctl` tells you how long the test will run. You won't get any notifications when it's finished. Check the results by reading the log:
    > ```
    > $ sudo smartctl -l selftest /dev/sdb
    > smartctl 6.5 2016-01-24 r4214 [x86_64-linux-4.4.0-64-generic] (local build)
    > Copyright (C) 2002-16, Bruce Allen, Christian Franke, www.smartmontools.org
    > 
    > === START OF READ SMART DATA SECTION ===
    > SMART Self-test log structure revision number 1
    > Num  Test_Description Status                Remaining  LifeTime(hours)  LBA_of_first_error
    > # 1  Short offline   Completed without error       00%      5357
    > ```
    > 
    > ### smartd Daemon and Notifications
    > 
    > You can run `smartd`, the SMART daemon, to continually monitor your drives and email you to report possible troubles. On Debian/Ubuntu/etc. you'll edit `/etc/default/smartmontools` to automatically launch `smartd` at startup, and edit `/etc/smartd.conf` to configure monitoring and notifications. Most distros install `/etc/smartd.conf`, and you'll use your distro's method of launching `smartd` at boot.
    > 




## NVMe support

- [smartctl - Smartmontools with NVMe support on CentOS 7 - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/363212/smartmontools-with-nvme-support-on-centos-7)

    > Using the nvme command-line tool
    > ================================
    > 
    > CentOS 7 ships with an `nvme` command (the yum package is named `nvme-cli`).
    > 
    > It can list the NVMe drives:
    > 
    > ```
    > # nvme list
    > 
    > ```
    > 
    > And can read SMART info:
    > 
    > ```
    > # nvme smart-log /dev/nvme0
    > 
    > ```
    > 
    > And *additional* SMART info (not sure why it's split):
    > 
    > ```
    > # nvme smart-log-add /dev/nvme0
    > 
    > ```
    > 

## NVME can't see S.M.A.R.T. in gnome-disk-utility

- [16.04 - NVME can't see S.M.A.R.T. in gnome-disk-utility - Ask Ubuntu](https://askubuntu.com/questions/942365/nvme-cant-see-s-m-a-r-t-in-gnome-disk-utility)

    > First, make sure that you have the latest firmware installed in the Intel 600P. Go to these web sites for the downloads...
    > 
    > <https://www.intel.com/content/www/us/en/support/memory-and-storage/000017245.html>
    > 
    > <https://downloadcenter.intel.com/product/94922/Intel-SSD-600p-Series>
    > 
    > In the `Disks` utility, make sure that you select the SSD in the left pane, then go to the "hamburger" icon and select `SMART Data & Tests`. That should get you where you want to go.
    > 
    > You might install `gsmartcontrol` and see if that sees the SSD SMART.
    > 
    > ```
    > sudo apt-get update
    > sudo apt-get install gsmartcontrol
    > 
    > ```
    > 


# Disk bench mark

## iotop - check disk I/O utilisation per process

- [linux - Howto check disk I/O utilisation per process - Server Fault](https://serverfault.com/questions/169676/howto-check-disk-i-o-utilisation-per-process#_=_)


    > If you are lucky enough to catch the next peak utilization period, you can study per-process I/O stats interactively, using [iotop](http://guichaz.free.fr/iotop/).
    > 

- [linux - What Process is using all of my disk IO - Stack Overflow](https://stackoverflow.com/questions/488826/what-process-is-using-all-of-my-disk-io)


    > You're looking for `iotop` (assuming you've got kernel >2.6.20 and Python 2.5). Failing that, you're looking into hooking into the filesystem. I recommend the former.

## gnome-disks

- [How to check hard disk performance - Ask Ubuntu](https://askubuntu.com/questions/87035/how-to-check-hard-disk-performance)

    > Graphical method
    > ----------------
    > 
    > 1.  Go to System -> Administration -> Disk Utility.
    >     -   Alternatively, launch the Gnome disk utility from the command line by running `gnome-disks`
    > 2.  Select your hard disk at left pane.
    > 3.  Now click "Benchmark -- Measure Drive Performance" button in right pane.
    > 4.  A new window with charts opens.You will find and two buttons. One is for "Start Read Only Benchmark" and another one is "Start Read/Write Benchmark". When you click on anyone button it starts benchmarking of hard disk.
    > 
    > ![test](https://i.stack.imgur.com/0Xtvn.png)
    > 

## fio

- [How to benchmark disk I/O : Binary Lane](https://www.binarylane.com.au/support/solutions/articles/1000055889-how-to-benchmark-disk-i-o)

    > What not to do
    > ==============
    > 
    > Chances are, you have seen this test before; perhaps even used it yourself. It is the obligatory *dd* test - here is one popular variety:
    > 
    > ~~dd if=/dev/zero of=test bs=64k count=16k conv=fdatasync~~
    > 
    > This test is popular because *dd* is pre-installed on almost all Linux servers. While it is a simple way of seeing if something is broken (for example, if you see 10MB/sec than your server is overloaded) it has a number of problems:
    > 
    > -   This is a single-threaded, sequential-write test. If you are running the typical web+database server on your VPS, the number is meaningless because **typical services do not do long-running sequential writes**.
    > -   The amount of data written (1GB) is small; and hence can be strongly influenced by caching on the host server, or the host's RAID controller. (The *conv=fdatasync* only applies to the VPS, not the host).
    > -   It executes for a very short period of time; just a few seconds on faster I/O subsystems. This isn't enough to get a consistant result.
    > -   There's no read performance testing at all.
    > 
    > So if you accept my argument that *dd* is not a great way to benchmark disk performance, let's walk through a few tools that I think are worth using:
    > 
    > Measuring random IOPS with FIO
    > ==============================
    > 
    > When running a website or similar workload, in general the best measurement of the disk subsystem is known as IOPS: Input/Output Operations per Second. In particular, the specific test we want to do is:
    > 
    > 1.  Random reads, random writes, or a combination of both. Databases in particular will pull data from all over your disk - known as random access.
    > 
    > 2.  4 kilobyte blocks. Again, databases and many other programs will read very small chunks of data - 4 kilobytes is a good working estimate.
    > 3.  Multiple threads. If your website has multiple visitors, your website will serve them all at the same time. We want our benchmark to simulate this behaviour of multiple things accessing the disk at once.
    > 
    > FIO is a popular tool for measuring IOPS on a Linux server. Its very configurable (perhaps even to its detriment) but with the following Bash snippets is easy enough to use.  To start with, here is how to download and compile it - just paste straight into the root shell of your CentOS/Debian/Ubuntu server:
    > 
    > ```
    > cd /root
    > yum install -y make gcc libaio-devel || ( apt-get update && apt-get install -y make gcc libaio-dev  </dev/null )
    > wget https://github.com/Crowd9/Benchmark/raw/master/fio-2.0.9.tar.gz ; tar xf fio*
    > cd fio*
    > make
    > ```
    > 
    > With FIO compiled, we can now run some tests.
    > 
    > Random read/write performance
    > -----------------------------
    > 
    > If you simply want a way to compare different provider's disk performance, then this is the test I suggest. Run the following command:
    > 
    > ```
    > ./fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=test --bs=4k --iodepth=64 --size=4G --readwrite=randrw --rwmixread=75
    > ```
    > 
    > This will create a 4 GB file, and perform 4KB reads and writes using a 75%/25% (ie 3 reads are performed for every 1 write) split within the file, with 64 operations running at a time. The 3:1 ratio is a rough approximation of your typical database.
    > 
    > FIO will now tick along printing a summary as it goes, that looks like this:
    > 
    > ```
    > Jobs: 1 (f=1): [m] [6.5% done] [39613K/13099K /s] [9903 /3274  iops] [eta 01m:12s]
    > 
    > ```
    > 
    > And eventually a full result output like this, with the numbers we want highlighted in yellow:
    > 
    > fio-2.0.9
    > 
    > Starting 1 process
    > 
    > Jobs: 1 (f=1): [m] [100.0% done] [43496K/14671K /s] [10.9K/3667 iops] [eta 00m:00s]
    > 
    > test: (groupid=0, jobs=1): err= 0: pid=31214: Fri May 9 16:01:53 2014
    > 
    >   read : io=3071.1MB, bw=39492KB/s, iops=9873 , runt= 79653msec
    > 
    >   write: io=1024.7MB, bw=13165KB/s, iops=3291 , runt= 79653msec
    > 
    >   cpu : usr=16.26%, sys=71.94%, ctx=25916, majf=0, minf=25
    > 
    >   IO depths : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=0.1%, >=64=100.0%
    > 
    >      submit : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
    > 
    >      complete : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
    > 
    >      issued : total=r=786416/w=262160/d=0, short=r=0/w=0/d=0
    > 
    > Run status group 0 (all jobs):
    > 
    >    READ: io=3071.1MB, aggrb=39492KB/s, minb=39492KB/s, maxb=39492KB/s, mint=79653msec, maxt=79653msec
    > 
    >   WRITE: io=1024.7MB, aggrb=13165KB/s, minb=13165KB/s, maxb=13165KB/s, mint=79653msec, maxt=79653msec
    > 
    > Disk stats (read/write):
    > 
    >   vda: ios=786003/262081, merge=0/22, ticks=3883392/667236, in_queue=4550412, util=99.97%
    > 
    > This tests shows:
    > 
    > -   Binary Lane's network SSD performing 9873 read operations per second and 3291 write operations per second. 
    > -   A VPS using local SSD might reach 40,000 and 10,000 respectively if the system is lightly loaded.
    > 
    > -   A VPS using local non-SSD will probably get somewhere around 500 read / 200 write.
    > 
    > If you want to know what contributed to the above numbers, read on -
    > 
    > Random read performance
    > -----------------------
    > 
    > To measure random reads, use slightly altered FIO command:
    > 
    > ```
    > ./fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=test --bs=4k --iodepth=64 --size=4G --readwrite=randread
    > ```
    > 
    > Again, we pull the iops from the result:
    > 
    > fio-2.0.9
    > 
    > Starting 1 process
    > 
    > Jobs: 1 (f=1): [r] [100.0% done] [62135K/0K /s] [15.6K/0 iops] [eta 00m:00s]
    > 
    > test: (groupid=0, jobs=1): err= 0: pid=31181: Fri May 9 15:38:57 2014
    > 
    >   read : io=1024.0MB, bw=62748KB/s, iops=15686 , runt= 16711msec
    > 
    >   cpu : usr=5.94%, sys=90.13%, ctx=1885, majf=0, minf=89
    > 
    >   IO depths : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=0.1%, >=64=100.0%
    > 
    >      submit : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
    > 
    >      complete : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
    > 
    >      issued : total=r=262144/w=0/d=0, short=r=0/w=0/d=0
    > 
    > Run status group 0 (all jobs):
    > 
    >    READ: io=1024.0MB, aggrb=62747KB/s, minb=62747KB/s, maxb=62747KB/s, mint=16711msec, maxt=16711msec
    > 
    > Disk stats (read/write):
    > 
    >   vda: ios=259063/2, merge=0/1, ticks=951356/20, in_queue=951308, util=96.83%
    > 
    > This tests shows Binary Lane's network storage scoring 15686 read operations per second. By comparison, a local SSD may give 50,0000 while a good non-SSD may give around 2000.
    > 
    > Random write performance
    > ------------------------
    > 
    > Again, just modify the FIO command slightly so we perform randwrite instead of randread:
    > 
    > ```
    > ./fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=test --bs=4k --iodepth=64 --size=4G --readwrite=randwrite
    > ```
    > 
    > Again, we pull the iops from the result:
    > 
    > fio-2.0.9
    > 
    > Starting 1 process
    > 
    > Jobs: 1 (f=1): [w] [100.0% done] [0K/26326K /s] [0 /6581 iops] [eta 00m:00s]
    > 
    > test: (groupid=0, jobs=1): err= 0: pid=31235: Fri May 9 16:16:21 2014
    > 
    >   write: io=1024.0MB, bw=29195KB/s, iops=7298 , runt= 35916msec
    > 
    >   cpu : usr=77.42%, sys=13.74%, ctx=2306, majf=0, minf=24
    > 
    >   IO depths : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=0.1%, >=64=100.0%
    > 
    >      submit : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
    > 
    >      complete : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.1%
    > 
    >      issued : total=r=0/w=262144/d=0, short=r=0/w=0/d=0
    > 
    > Run status group 0 (all jobs):
    > 
    >   WRITE: io=1024.0MB, aggrb=29195KB/s, minb=29195KB/s, maxb=29195KB/s, mint=35916msec, maxt=35916msec
    > 
    > Disk stats (read/write):
    > 
    >   vda: ios=0/260938, merge=0/11, ticks=0/2315104, in_queue=2316372, util=98.87%
    > 
    > This tests shows Binary Lane's network storage scoring 7298 write operations per second. By comparison, a local SSD may give 50,0000 while a good non-SSD may give around 2000.
    > 
    > Measuring latency with IOPing
    > =============================
    > 
    > The final aspect of evaluating disk performance is to measure the latency on individual requests. One way to do so is to install ioping using the following command:
    > 
    > ```
    > cd /root
    > yum install -y make gcc libaio-devel || ( apt-get update && apt-get install -y make gcc libaio-dev  </dev/null )
    > wget https://ioping.googlecode.com/files/ioping-0.6.tar.gz ; tar xf ioping*
    > cd ioping*
    > make
    > ```
    > 
    > We can now run ioping to get an idea of the per-request latency:
    > 
    > ```
    > ./ioping -c 10 .
    > ```
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=1 time=0.2 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=2 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=3 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=4 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=5 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=6 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=7 time=0.3 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=8 time=0.2 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=9 time=0.4 ms
    > 
    > 4096 bytes from . (ext3 /dev/vda1): request=10 time=0.3 ms
    > 
    > --- . (ext3 /dev/vda1) ioping statistics ---
    > 
    > 10 requests completed in 9006.8 ms, 3505 iops, 13.7 mb/s
    > 
    > min/avg/max/mdev = 0.2/0.3/0.4/0.1 ms
    > 
    > Here you can see the average was 0.3ms.  On a healthy system, you should see relatively low variation and an average below 1.0 ms.
    > 

## Bonnie++

- [[Linux-文件系统测试] -- Bonnie++测试 - 简书](https://www.jianshu.com/p/2e048e23e9f7)

    > Bonnie\+\+是一个硬盘和文件系统的基准性能测试工具，它通过一系列的简单测试来生成硬盘和文件系统的性能参数。主要对三个方面做基准测试：数据读、写速度，每秒可以完成的磁盘寻道次数和每秒可以完成的文件元数据操作次数。（说明： Bonnie不能支持>2G的文件，因此Russell Coker ([russell@coker.com.au](https://link.jianshu.com?t=mailto:russell@coker.com.au)) 开发了Bonnie++）
    > 
    > Bonnie\+\+的编译与安装：\
    > 下载Bonnie\+\+测试工具(最新的版本是：bonnie\+\+-1.03e) ：
    > [http://www.coker.com.au/bonnie++/](https://link.jianshu.com?t=http://www.coker.com.au/bonnie++/)
    > 下面以在ubuntu16.04操作系统为例:
    > ```
    > $ tar zxvf bonnie++-1.03e.tgz
    > $ cd bonnie++-1.03e
    > $ ./configure
    > $ make && make install
    > ```
    > 安装完成以后会在/usr/local/sbin/目录中生成两个可执行文件，bonnie++（主测试程序）和zcav（裸盘吞吐量测试程序）；同时也会在/usr/local/bin目录下生成两个可执行文件，用于生成可读性强的测试报告，它们是bon_csv2html和bon_csv2txt。
    > 
    > Bonnie++测试选项说明：\
    > 成功安装bonnie++后，查看bonnie++的测试参数\
    > $ bonnie++ help\
    > usage: bonnie++ [-d scratch-dir] [-s size(MiB)[:chunk-size(b)]]\
    > [-n number-to-stat[:max-size[:min-size][:num-directories]]]\
    > [-m machine-name]\
    > [-r ram-size-in-MiB]\
    > [-x number-of-tests] [-u uid-to-use:gid-to-use] [-g gid-to-use]\
    > [-q] [-f] [-b] [-D] [-p processes | -y]\
    > Version: 1.03e\
    > -d : scratch-dir 用于测试的目录，即测试目标位置；\
    > -s : size(MiB) 用于测试IO性能的文件的大小；如果指定的文件大小大于1G，bonnie++会将其分为多个大小为1G的文件；如果你没有加 -s这个option，系统会默认使用2倍内存大小的文件，比如我的内存是2G，那么bonnie会使用4G的文件来测试性能，原因在于减少缓存的影响\
    > -n : ?\
    > -m : 测试目标主机的主机名，仅用于显示测试结果时的主机标识；\
    > -r : 指定测试程度使用的内存大小；bonnie++一般要求指定的测试文件的大小至少为物理内存的2倍；如果测试时指定的文件过小，则可以通过指定所使用的物理内存大小来滞此条件；\
    > -x : 用于指定同时运行的测试数目；\
    > -u : 测试程序运行时关联的uid，如果以root用户的身份做测试，则此项必须明确指定。\
    > -g : 选项则用于指定gid；\
    > -q : 静默模式；\
    > -f : 快速模式，此种模式不进行IO测试；\
    > -b :\
    > -D : 直接IO测试，用于测试大规模IO请求时的性能；open的时候，带上O_DIRECT标志，对应的代码逻辑在bon_io.cpp；\
    > -p :
    > 
    > Bonnie++测试举例：\
    > $ bonnie++ -u <user_name> ------ 直接用默认参数值\
    > 例 1： bonnie++ -u root\
    > 输出如下结果：\
    > Using uid:1000, gid:1000.\
    > Writing with putc()...done\
    > Writing intelligently...done\
    > Rewriting...done\
    > Reading with getc()...done\
    > Reading intelligently...done\
    > start 'em...done...done...done...\
    > Create files in sequential order...done.\
    > Stat files in sequential order...done.\
    > Delete files in sequential order...done.\
    > Create files in random order...done.\
    > Stat files in random order...done.\
    > Delete files in random order...done.\
    > Version 1.03e ------Sequential Output------ --Sequential Input- --Random-\
    > -Per Chr- --Block-- -Rewrite- -Per Chr- --Block-- --Seeks--\
    > Machine Size K/sec %CP K/sec %CP K/sec %CP K/sec %CP K/sec %CP /sec %CP\
    > yzh-desktop 31G 106862 68 103016 3 39518 2 110741 66 106129 2 206.5 0\
    > ------Sequential Create------ --------Random Create--------\
    > -Create-- --Read--- -Delete-- -Create-- --Read--- -Delete--\
    > files /sec %CP /sec %CP /sec %CP /sec %CP /sec %CP /sec %CP\
    > 16 +++++ +++ +++++ +++ +++++ +++ +++++ +++ +++++ +++ +++++ +++\
    > yzh-desktop,31G,106862,68,103016,3,39518,2,110741,66,106129,2,206.5,0,16,+++++,+++,+++++,+++,+++++,+++,+++++,+++,+++++,+++,+++++,+++\
    > 用bon_csv2html工具将最后一行的结果转化为HTML格式输出：\
    > $ echo yzh-desktop,31G,106862,68,103016,3,39518,2,110741,66,106129,2,206.5,0,16,+++++,+++,+++++,+++,+++++,+++,+++++,+++,+++++,+++,+++++,+++ | /usr/local/bin/bon_csv2html >>bon_result.html
    > 
    > ![](//upload-images.jianshu.io/upload_images/4361046-979e007d1180c685.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    > bon_result.png\
    > 说明：\
    > 1、测试结果中显示形如的"++++"的符号表示此项测试时间小于500ms，所以被视作不准确结果不予显示；\
    > 2、每项测试都会显示两个结果，其中的%CP表示此项测试的CPU占用率；\
    > Sequential Output下的 Per Char是值用putc方式写，毫无疑问，因为cache的line总是大于1字节的，所以不停的骚扰CPU执行putc，看到cpu使用率是68%.写的速度是106MB/s\
    > Sequential Output是按照block去写的，明显CPU使用率就下来了，速度也上去了，写的速度是103MB/s。\
    > Sequential Input下的Per Char是指用getc的方式读文件，速度是110MB/s，CPU使用率是66%。\
    > Sequential Input下的block是指按照block去读文件，速度是106MB/s,CPU使用率是2%。
    > 
    > 带具体参数值进行测试\
    > 例2 ：bonnie++ -d <test_path> -u <user_name> -s <size> -m <host_name> -r <mem_size> -g <gid>\
    > $ bonnie++ -d /home/yzh/images/test -u yzh -m yzh-desktop -r 31720 -g 1000\
    > 说明 ：如果指定的文件大小大于1G，bonnie++会将其分为多个大小为1G的文件；如果你没有加 -s这个option，系统会默认使用2倍内存大小的文件，比如我的内存是16G，那么bonnie会使用32G的文件来测试性能 。\
    > 测试结果如下：
    > 
    > ![](//upload-images.jianshu.io/upload_images/4361046-15dd019a7fd286f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    > bon_result2.png
    > 
    > 



# disk image

## create VHD disk image from dd image under linux

- [How to create VHD disk image from a Linux live system? - Super User](https://superuser.com/questions/410940/how-to-create-vhd-disk-image-from-a-linux-live-system)

    > For future reference, here is how I finally proceeded, with a few comments on the various issues or pitfalls encountered:
    > 
    > ### 1\. Boot the machine with a Linux live system
    > 
    > First step was to boot the machine containing the disk to image, using a Linux live system.
    > 
    > > NOTE: My first idea was to use an Ubuntu Live USB disk, but the machine did not support booting from USB, so I found it easier to use an old **Knoppix live CD**.
    > 
    > ### 2\. Image the disk using `dd` and pipe the data through `ssh`
    > 
    > Then, I copied all the disk content to a file image on my local server using `dd` and piping the data through `ssh`:
    > 
    > > $ dd if=/dev/hdX bs=4k conv=noerror,sync | ssh -c blowfish myuser@myserver 'dd of=myfile.dd'
    > 
    > A few comments here: this method will read all the disk contents, so it can take very long (it took me 5hrs for a 80Gb disk). The bottleneck isn't the network, but really the disk read speed. Before launching the copy, I advice to check the BIOS/disk/system parameters to ensure that the disk and the motherboard are working at their highest possible speed (this can be checked using the command `hdparm -i` and by running a test with `hdparm -Tt /dev/hdX`).
    > 
    > NOTE: `dd` does not output progress of the operation, but we can force it to do so by sending the *USR1* signal to the `dd` process PID from another terminal:
    > 
    > > $ kill -USR1 *PIDofdd*
    > 
    > ### 3\. Reclaim the unused space
    > 
    > At this point, the source machine is no longer needed and we will work exclusively on the destination server (running Linux as well). VirtualBox will be used to convert the raw disk image to the VHD format, but before doing so, we can zero out the unused blocks, so that VirtualBox does not allocate space for them in the final file.
    > 
    > In order to do so, I mounted the images as a loopback device:
    > 
    > ```
    > $ mount -o loop,rw,offset=26608813056 -t ntfs-3g /mnt/mydisk/myfile.dd /mnt/tmp_mnt
    > $ cat /dev/zero > zero.file
    > $ rm zero.file
    > 
    > ```
    > 
    > NOTE: The offset indicating the beginning of the partition within the disk image can be obtained by using `parted` on the image file:
    > 
    > ```
    > $ parted /mnt/mydisk/myfile.dd
    > (parted) unit
    > Unit?  [compact]? B
    > (parted) print
    > Model:  (file)
    > Disk /mnt/mydisk/myfile.dd: 80026361856B
    > Sector size (logical/physical): 512B/512B
    > Partition Table: msdos
    > 
    > Number  Start         End           Size          Type      File system  Flags
    >  1      32256B        21936821759B  21936789504B  primary   ntfs         boot
    >  2      21936821760B  80023749119B  58086927360B  extended               lba
    >  5      26608813056B  80023749119B  53414936064B  logical   ntfs
    > 
    > ```
    > 
    > NOTE2: The default Linux kernel NTFS driver provides read-only access, thus it is necessary to install and use the userspace `ntfs-3g` driver or writing to the disk will raise an error!
    > 
    > ### 4\. Create the VHD image using VBoxManage
    > 
    > At this point, we can use the VirtualBox utilities to convert the raw image to a VHD file:
    > 
    > ```
    > VBoxManage convertfromraw myfile.dd myfile.vhd --format VHD
    > 
    > ```
    > 
    > ---
    > 
    > You forgot to cd into the mounted disk before creating the zero file: mount -o loop,rw,offset=26608813056 -t ntfs-3g /mnt/mydisk/myfile.dd /mnt/tmp_mnt ; cd /mnt/tmp_mnt ; cat /dev/zero > zero.file ; rm zero.file ; Also you can use pv instead of dd to show instant progress. -- [Smeterlink](https://superuser.com/users/298707/smeterlink "172 reputation") [Mar 2 '16 at 7:26](https://superuser.com/questions/410940/how-to-create-vhd-disk-image-from-a-linux-live-system#comment1466868_412495)
    > 
    > ---
    > 
    > I was trying to do exactly the same thing as the OP (while rescuing a Windows installation) and ended up creating a new tool for it, [`ntfsclone2vhd`](https://github.com/yirkha/ntfsclone2vhd).
    > 
    > You would then simply do something like this:
    > 
    > ```
    > ntfsclone --save-image -o - /dev/sdXX | ntfsclone2vhd - /mnt/usb/output.vhd
    > 
    > ```
    > 

- [linux - How do I convert an .img file to vhd? - Super User](https://superuser.com/questions/452720/how-do-i-convert-an-img-file-to-vhd/770057)

    > I'm not sure for how long this has been the case, but since this is the #1 search result for this question, I'll answer it currently. VHD is currently supported by qemu-img. The argument for VHD is vpc. This was found here <http://docs.openstack.org/image-guide/content/ch_converting.html>
    > 
    > In case link breaks, here's a copy/past
    > 
    > Converting images from one format to another is generally straightforward. qemu-img convert: raw, qcow2, VDI, VMDK
    > 
    > The qemu-img convert command can do conversion between multiple formats, including raw, qcow2, VDI (VirtualBox), VMDK (VMWare) and VHD (Hyper-V). Table 7.1. qemu-img format strings
    > 
    > ```
    > **Image format**    **Argument to qemu-img**
    > raw                     raw
    > qcow2                   qcow2
    > VDI (VirtualBox)        vdi
    > VMDK (VMWare)           vmdk
    > VHD (Hyper-V)           vpc
    > 
    > ```
    > 
    > This example will convert a raw image file named centos63.dsk to a qcow2 image file.
    > 
    > ```
    > $ qemu-img convert -f raw -O qcow2 centos64.dsk centos64.qcow2
    > 
    > ```
    > 
    > To convert from vmdk to raw, you would do:
    > 
    > ```
    > $ qemu-img convert -f vmdk -O raw centos64.vmdk centos64.img
    > 
    > ```

- [andreiw/vhdtool: Manipulate VHD (Virtual Hard Disk) images the open-source way.](https://github.com/andreiw/vhdtool)

    > VHDtool
    > ==========
    > 
    > A tool to examine and manipulate VHD images. Initially
    > meant as a way to test dynamic VHD support in my
    > Linux kernel loop VHD parser support. Images mount
    > in Win7.
    > 
    > Why would you use this instead of qemu-img? VHDtool
    > lets you tweak more parameters and create funky
    > VHDs (and will support differencing disks soon too!).
    > 
    > One more reason is that qemu-img actually produces
    > corrupt images that don't fit the VHD spec. Unsure
    > if they event mount on Win7.



## use `cat /dev/zero` to reclaim disk image space

- [filesystems - Purpose of /dev/zero? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/63238/purpose-of-dev-zero)

    > `/dev/zero` is a special file (in this case, a pseudo-device) that provides an endless stream of null characters (so hex 0x00)? That's why your `cat` is not outputting anything (but try running it through `od` (octal dump)).
    > 
    > 'blank file with infinite size' is not 100% correct: it's not a regular file, but a special file (more like a 'stream' or a generator). You can read as much from it as you want, for example with `dd` (like `dd if=/dev/zero of=yourfile count=1024 bs=1024`).
    > 
    > It's not really a *blank* file, nor used to create blank files: it's used to create files or memory pages filled with only zeroes. You can also write to it, making it perform like a sinkhole (its more popular brother `/dev/null` is more commonly used for this though).
    > 

# sparse file

## truncate

- [truncate(1) - Linux man page](https://linux.die.net/man/1/truncate)

    > create a 100GB file
    > ```
    > truncate -s100G 100GB.img
    > ```
    > [name=Ya-Lun Li]
    > 
    > ---
    >  
    > **-s**, **--size**=*SIZE*
    > 
    > use this SIZE
    > 
    > 
    > SIZE may be (or may be an integer optionally followed by) one of following: KB 1000, K 1024, MB 1000*1000, M 1024*1024, and so on for G, T, P, E, Z, Y.
    > 
    > SIZE may also be prefixed by one of the following modifying characters: '+' extend by, '-' reduce by, '<' at most, '>' at least, '/' round down to multiple of, '%' round up to multiple of.

## list actual file size

- [command line - Why does ls -l output a different size from ls -s? - Ask Ubuntu](https://askubuntu.com/questions/269480/why-does-ls-l-output-a-different-size-from-ls-s)

    > 
    > **Now, let us look at the directory:**
    > 
    > ```
    > # ls -ls --block-size 1 f_*
    > 1024 -rw-r--r-- 1 user user 128 Mar 18 15:34 f_random.img
    >    0 -rw-r--r-- 1 user user 128 Mar 18 15:32 f_zeroes.img
    >    ^                         ^
    >    |                         |
    > Amount which the           Actual file size
    > files takes on the fs
    > 
    > ```
    > 
    > The first value is given by the `-s --block-size 1` option, it is the *amount of space used by the file on the file system*.
    > 
    > ---
    > 
    > human readable
    > 
    > ```
    > ls -lsh
    > ```
    > [name=Ya-Lun Li]
    > 

# virtual memory

## Check the System for Swap Information

- [8 Useful Commands to Monitor Swap Space Usage in Linux](https://www.tecmint.com/commands-to-monitor-swap-space-usage-in-linux/)

    > To check swap usage information, you can view the **/proc/swaps** file using the [cat utility](https://www.tecmint.com/13-basic-cat-command-examples-in-linux/).
    > ```shell
    > # cat /proc/swaps
    > Filename				Type		Size	Used	Priority
    > /dev/sda10                              partition	8282108	0	-1
    > ```
    >
    > ---
    > 
    > This command is used to display information about virtual memory statistics. To install vmstat on your Linux system, you can read the article below and see more usage examples:
    > 
    > [Linux Performance Monitoring with Vmstat](https://www.tecmint.com/linux-performance-monitoring-with-vmstat-and-iostat-commands/https://www.tecmint.com/linux-performance-monitoring-with-vmstat-and-iostat-commands/)
    > ```
    > # vmstat
    > ```
    > [![VmStat Check Swap Usage](https://www.tecmint.com/wp-content/uploads/2015/10/VmStat-Check-Swap-Usage-620x344.png)](https://www.tecmint.com/wp-content/uploads/2015/10/VmStat-Check-Swap-Usage.png)
    > 
    > VmStat Check Swap Usage
    > 
    > You need to take note of the following in the swap field from the output of this command.
    > 
    > 1.  **si**: Amount of memory swapped in from disk (s).
    > 2.  **so**: Amount of memory swapped to disk (s).



- [How To Add Swap Space on Ubuntu 16.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-16-04)

    > We can see if the system has any configured swap by typing:
    > 
    > ```
    > sudo swapon --show
    > 
    > ```
    > 
    > If you don't get back any output, this means your system does not have swap space available currently.
    > 
    > You can verify that there is no active swap using the `free` utility:
    > 
    > ```
    > free -h
    > 
    > ```
    > 
    > ```
    > Output              total        used        free      shared  buff/cache   available
    > Mem:           488M         36M        104M        652K        348M        426M
    > Swap:            0B          0B          0B
    > 
    > ```
    > 
    > As you can see in the "Swap" row of the output, no swap is active on the system.
    > 
    >
    > ---
    > 
    > ### Adjusting the Swappiness Property
    > 
    > The `swappiness` parameter configures how often your system swaps data out of RAM to the swap space. This is a value between 0 and 100 that represents a percentage.
    > 
    > With values close to zero, the kernel will not swap data to the disk unless absolutely necessary. Remember, interactions with the swap file are "expensive" in that they take a lot longer than interactions with RAM and they can cause a significant reduction in performance. Telling the system not to rely on the swap much will generally make your system faster.
    > 
    > Values that are closer to 100 will try to put more data into swap in an effort to keep more RAM space free. Depending on your applications' memory profile or what you are using your server for, this might be better in some cases.
    > 
    > We can see the current swappiness value by typing:
    > 
    > ```
    > cat /proc/sys/vm/swappiness
    > 
    > ```
    > 
    > ```
    > Output
    > 60
    > 
    > ```
    > 
    > For a Desktop, a swappiness setting of 60 is not a bad value. For a server, you might want to move it closer to 0.
    > 
    > We can set the swappiness to a different value by using the `sysctl` command.
    > 
    > For instance, to set the swappiness to 10, we could type:
    > 
    > ```
    > sudo sysctl vm.swappiness=10
    > 
    > ```
    > 
    > ```
    > Output
    > vm.swappiness = 10
    > 
    > ```
    > 
    > This setting will persist until the next reboot. We can set this value automatically at restart by adding the line to our `/etc/sysctl.conf` file:
    > 
    > ```
    > sudo nano /etc/sysctl.conf
    > 
    > ```
    > 
    > At the bottom, you can add:
    > 
    > /etc/sysctl.conf
    > 
    > ```
    > vm.swappiness=10
    > 
    > ```
    > 
    > Save and close the file when you are finished.
    > 
    > ### Adjusting the Cache Pressure Setting
    > 
    > Another related value that you might want to modify is the `vfs_cache_pressure`. This setting configures how much the system will choose to cache inode and dentry information over other data.
    > 
    > Basically, this is access data about the filesystem. This is generally very costly to look up and very frequently requested, so it's an excellent thing for your system to cache. You can see the current value by querying the `proc` filesystem again:
    > 
    > ```
    > cat /proc/sys/vm/vfs_cache_pressure
    > 
    > ```
    > 
    > ```
    > Output
    > 100
    > 
    > ```
    > 
    > As it is currently configured, our system removes inode information from the cache too quickly. We can set this to a more conservative setting like 50 by typing:
    > 
    > ```
    > sudo sysctl vm.vfs_cache_pressure=50
    > 
    > ```
    > 
    > ```
    > Output
    > vm.vfs_cache_pressure = 50
    > 
    > ```
    > 
    > Again, this is only valid for our current session. We can change that by adding it to our configuration file like we did with our swappiness setting:
    > 
    > ```
    > sudo nano /etc/sysctl.conf
    > 
    > ```
    > 
    > At the bottom, add the line that specifies your new value:
    > 
    > /etc/sysctl.conf
    > 
    > ```
    > vm.vfs_cache_pressure=50
    > 
    > ```
    > 
    > Save and close the file when you are finished.


## How to change swap size
- [How to change swap size on Ubuntu 14.04 ? | DigitalOcean](https://www.digitalocean.com/community/questions/how-to-change-swap-size-on-ubuntu-14-04)

    > Just follow these steps:
    > 
    > 1.  Make all swap off\
    >     sudo swapoff -a
    > 
    > 2.  Resize the swapfile\
    >     sudo dd if=/dev/zero of=/swapfile bs=1M count=1024
    > 
    > 3.  Make swapfile usable\
    >     sudo mkswap /swapfile
    > 
    > 4.  Make swapon again\
    >     sudo swapon /swapfile
    > 
    > ---
    > 
    > I tried to delete my old swap in /etc/fstab and the code which I delete is
    > 
    > ```
    > /swapfile   none    swap    sw    0   0
    > 
    > ```
    > 



# partition

## 不重启的情况下重读分区

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





# disk space

## no enough space

- [How to Fix the 'No Space Left on Device' Error on Linux - Make Tech Easier](https://www.maketecheasier.com/fix-linux-no-space-left-on-device-error/)

    > Possible Causes
    > ---------------
    > 
    > There are a couple of main causes here. If you saw a discrepancy between `du` and `df` you can jump down to the first option here. Otherwise, start at the second one.
    > 
    > ### Deleted File Reserved by Process
    > 
    > Occasionally, a file will be deleted, but a process is still using it. Linux won't release the storage associated with the file while the process is still running. You just need to find the process and restart it.
    > 
    > ![Check processes for deleted files](https://www.maketecheasier.com/assets/uploads/2017/10/no-space-process.jpg "Check processes for deleted files")
    > 
    > Try to locate the process.
    > ```shell
    > sudo lsof / | grep deleted
    > ```
    > The problematic process should be listed, then just restart it.
    > ```shell
    > sudo systemctl restart service_name
    > ```
    > ### Not Enough Inodes
    > 
    > ![Linux check filesystem inodes](https://www.maketecheasier.com/assets/uploads/2017/10/no-space-inode.jpg "Linux check filesystem inodes")
    > 
    > There is a set of metadata on filesystems called "inodes." Inodes track information about files. A lot of filesystems have a fixed amount of inodes, so it's very possible to fill the max allocation of inodes without filling the filesystem itself. You can use `df` to check.
    > ```shell
    > sudo df -i /
    > ```
    > Compare the inodes used with the total inodes. If there's no more available, unfortunately, you can't get more. Delete some useless or out-of-date files to clear up inodes.
    > 
    > ### Bad Blocks
    > 
    > The last common problem is bad filesystem blocks. Filesystems get corrupt and hard drives die. Your operating system will most likely see those blocks as usable unless they're otherwise marked. The best way to find and mark those blocks is by using `fsck` with the `-cc` flag. Remember that you can't use `fsck` from the same filesystem that you're testing. You'll probably need to use a live CD.
    > ```shell
    > sudo fsck -vcck /dev/sda2
    > ```
    > Obviously, replace the drive location with the drive that you want to check. Also, keep in mind that this will probably take a long time.
    > 

- [no space left on device 磁盘空间不足原因及排查方法 - CSDN博客](https://blog.csdn.net/jiedao_liyk/article/details/78497625)

    > **在系统使用中，经常会遇到no space left on device 磁盘空间不足的情况， 下面来详细的介绍一下产生这种情况的几种原因及解决办法：**
    > 
    > **1\. 首先我们要清楚inode 和 block的概念：**
    > 
    > 1.  inode在格式化创建文件系统的时候诞生，用来存放文件的属性信息，存放着block的位置，没有文件名，创建一个非空文件占用一个inode和至少1个block
    > 
    > 2.  block是实际存放数据的位置，block大小 1k 4k 8k centos 6.x(分区大于500M 默认是4k)，文件很大的话占用多个block, 文件非常小的时候1k block剩余的空间不能继续使用，所以系统中block消耗更快
    > 
    > **所以磁盘慢了就分为，inode满了，和block满了，以及一种特殊的情况，下面我们来具体分析，以及对应的解决方案**
    > 
    > -   查看是否是block满了
    > 
    > ```shell
    > [root@test-os testuser]# df -h   ###查看所有block使用情况
    > Filesystem      Size  Used Avail Use% Mounted on
    > /dev/sda3       8.8G  8.8G     0 100% /
    > tmpfs           931M     0  931M   0% /dev/shm
    > /dev/sda1       190M   40M  141M  22% /boot
    > [root@test-os testuser]# du -sh /usr/* |grep G  ###查找大文件
    > 7.3G    /usr/local
    > [root@test-os testuser]# du -sh /usr/local/* |grep G
    > 7.3G    /usr/local/bin
    > [root@test-os testuser]# du -sh /usr/local/bin/* |grep G
    > 7.3G    /usr/local/bin/1g
    > 
    > [root@test-os testuser]# \rm -f /usr/local/bin/1g  ###删除大文件
    > [root@test-os testuser]#
    > [root@test-os testuser]# df -h    ###接着查看发现已经解决
    > Filesystem      Size  Used Avail Use% Mounted on
    > /dev/sda3       8.8G  1.5G  6.9G  18% /
    > tmpfs           931M     0  931M   0% /dev/shm
    > /dev/sda1       190M   40M  141M  22% /boot
    > ```
    > 
    > -   查看是否inode满了（df -h发现还有空间）
    > 
    > ```shell
    > [root@test-os logs]# touch {1..118}.txt
    > [root@test-os logs]# touch {1..118}.txt
    > touch: cannot touch `118.txt': No space left on device
    > [root@test-os logs]# df -i   ###查看inode使用情况
    > Filesystem     Inodes IUsed  IFree IUse% Mounted on
    > /dev/sda3      593344 56998 536346   10% /
    > tmpfs          238282     1 238281    1% /dev/shm
    > /dev/sda1       51200    39  51161    1% /boot
    > /tmp/1m           128   128      0  100% /app/logs
    > [root@test-os logs]# pwd
    > /app/logs
    > [root@test-os logs]# \rm -f *.txt   ###如果小文件太多，采用a*.txt b*.txt 一批一批的删
    > [root@test-os logs]# df -i   ###接着查看
    > Filesystem     Inodes IUsed  IFree IUse% Mounted on
    > /dev/sda3      593344 56998 536346   10% /
    > tmpfs          238282     1 238281    1% /dev/shm
    > /dev/sda1       51200    39  51161    1% /boot
    > /tmp/1m           128    11    117    9% /app/logs
    > ###如果不知道小文件都在哪里怎么查找？
    > ###查找系统中 目录大小大于1M（目录一般大小为4K，所以目录要是大了那么文件必然很多）
    > [root@localhost testuser]# find / -size +4k -type d |xargs ls -ldhi
    >      11 drwx------   2 root root  12K Sep 23 00:49 /boot/lost+found
    >     946 drwxr-xr-x  12 root root 4.1K Sep 22 17:53 /dev
    > 1114113 drwxr-xr-x  88 root root  12K Sep 22 19:55 /etc
    >  262145 drwxr-xr-x  13 root root  12K Sep 22 18:59 /lib
    > ```
    > 
    > -   查看是不是文件被占用一直没被彻底删除（特殊原因），这种情况往往是容易被忽略，也是让人郁闷的，因为你会发现df -h明明已经有空间了，但是就是放不进去东西
    > 
    > ```shell
    > [root@test-os ~]# lsof |grep deleted
    > rsyslogd   1250      root    1w      REG                8,3 4888889358     140789 /var/log/messages (deleted)
    > 
    > [root@test-os ~]# #lsof 显示出系统中被打开的文件
    > [root@test-os ~]# #第一列 软件/服务的名称
    > [root@test-os ~]# #第八列 文件的大小
    > [root@test-os ~]# #第10列 文件的名字
    > [root@test-os ~]# #第11列 标记（硬链接数为0 进程调用数不为零 就会有 delete)
    > 
    > ####重启对应的服务 释放磁盘空间
    > [root@test-os ~]# /etc/init.d/rsyslog restart
    > Shutting down system logger:                               [  OK  ]
    > Starting system logger:                                    [  OK  ]
    > 
    > [root@test-os ~]# df -h
    > Filesystem      Size  Used Avail Use% Mounted on
    > /dev/sda3       8.8G  1.5G  6.9G  18% /
    > tmpfs           931M     0  931M   0% /dev/shm
    > /dev/sda1       190M   40M  141M  22% /boot
    > /tmp/1m        1003K   19K  933K   2% /app/logs
    > ```
    > 


## no enough inodes

- [How To Increase Amount of Disk inodes in Linux](https://ma.ttias.be/how-to-increase-amount-of-disk-inodes-in-linux/)

    > It doesn't happen often, but at times you may run out of inodes on a Linux system.
    > 
    > To find your current inode usage, run `df -i`.
    > 
    > ```shell
    > $ df -i
    > Filesystem                Inodes   IUsed     IFree  IUse%   Mounted on
    > /dev/mapper/centos-root 19374080   19374080  0      100%   /
    > ```
    > 
    > Out of the available 19.374.080 inodes, none were free. This is pretty much the equivalent of a disk full, except it doesn't show in terms of capacity but in terms of inodes.
    > 
    > If you're confused on what an inode exactly is, [Wikipedia](https://en.wikipedia.org/wiki/Inode) has a good description.
    > 
    > > In a Unix-style file system, an index node, informally referred to as an inode, is a data structure used to represent a filesystem object, which can be one of various things including a file or a directory. Each inode stores the attributes and disk block location(s) of the filesystem object's data.\
    > > *[Wikipedia: inode](https://en.wikipedia.org/wiki/Inode)*
    > 
    > A disk with 0 available inodes is probably full of very small files, somewhere in a specific directory (applications, tmp-files, pid files, session files, ...). Each file uses (*at least*) 1 inode. Many million files would use many million inodes.
    > 
    > If your disks' inodes are full, how do you increase it? The tricky answer is, you probably can't.
    > 
    > The amount of inodes available on a system is decided upon creation of the partition. For instance, a default partition of EXT3/EXT4 has a bytes-per-inode ratio of **one inode every 16384 bytes (16 Kb)**.
    > 
    > A 10GB partition would have would have around 622.592 inodes. A 100GB partition has around 5.976.883,2 inodes (taking into account [the reserved space for super-users/journalling](https://ma.ttias.be/changing-the-reserved-blocks-percentage-on-ext3-filesystems-in-linux/)).
    > 
    > Do you want to increase the amount of inodes? **Either increase the capacity of the disk entirely ([Guide: Increase A VMware Disk Size (VMDK) LVM](https://ma.ttias.be/increase-a-vmware-disk-size-vmdk-formatted-as-linux-lvm-without-rebooting/)), or re-format the disk using `mkfs.ext4 -i` to manually overwrite the *bytes-per-inode* ratio**.
    > 
    > As usual, the [Archwiki](https://wiki.archlinux.org/index.php/Ext4) has a good explanation on why we don't just make the default inode number 10x higher.
    > 
    > > For partitions with size in the hundreds or thousands of GB and average file size in the megabyte range, this usually results in a much too large inode number because the number of files created never reaches the number of inodes.
    > >
    > > This results in a waste of disk space, because all those unused inodes each take up 256 bytes on the filesystem (this is also set in /etc/mke2fs.conf but should not be changed). 256 * several millions = quite a few gigabytes wasted in unused inodes.\
    > > *[Archwiki: ext4](https://wiki.archlinux.org/index.php/Ext4)*
    > 
    > You may be able to create a new partition if you have spare disks/space in your LVM and chose a filesystem that's better suited to handle many small files, [like ReiserFS](https://en.wikipedia.org/wiki/ReiserFS).
    > 

- [linux - Is it possible to change Inode count on an ext4 filesystem? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/45107/is-it-possible-to-change-inode-count-on-an-ext4-filesystem)

    > From the [`mke2fs` man page](http://linux.die.net/man/8/mke2fs):
    > 
    > > Be warned that it is not possible to expand the number of inodes on a filesystem after it is created, so be careful deciding the correct value for this parameter.
    > 
    > So the answer is no.
    > 
    > What you could do is shrink the existing ext4 volume (this requires unmounting the filesystem), use the free space to create a new ext4 volume with fewer inodes, copy the data, remove the old volume and extend the new volume to occupy all the space.

- [files - How can I increase the number of inodes in an ext4 filesystem? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/26598/how-can-i-increase-the-number-of-inodes-in-an-ext4-filesystem)

    > It seems that you have a lot more files than normal expectation.
    > 
    > I don't know whether there is a solution to change the inode table size dynamically. I'm afraid that you need to back-up your data, and create new filesystem, and restore your data.
    > 
    > To create new filesystem with such a huge inode table, you need to use '-N' option of mke2fs(8).
    > 
    > I'd recommend to use '-n' option first (which does not create the fs, but display the use-ful information) so that you could get the estimated number of inodes. Then if you need to, use '-N' to create your filesystem with a specific inode numbers.
    > 
    > ---
    > 
    > @Gilles The `-i` options specifies the size of the inode, not how many there are. The `-N` option sets the number inodes. -- [theillien](https://unix.stackexchange.com/users/77650/theillien "546 reputation") [Oct 23 '14 at 20:12](https://unix.stackexchange.com/questions/26598/how-can-i-increase-the-number-of-inodes-in-an-ext4-filesystem#comment268772_26600)
    > 
    > ---
    > 
    > As another workaround I could suggest considering packing huge collections of files into an uncompressed(!) `tar` archive, and then using `archivemount` to mount it as a filesystem. A tar archive is better for sharing than a filesystem image and provides similar performance when backing up to a cloud or another storage.
    > 
    > * * * * *
    > 
    > If the collection is supposed to be read-only, `squashfs` may be an option, but it requires certain options enabled in the kernel, and `xz` compression is available for tar as well with the same performance.
    > 
    > ---
    > 
    > I have an alternate solutions for this situation. Lets say you have 1000 inodes in a **partition** of 10G. But due to inodes limit you are not suppose to use all space of **partition**. But in this solutions you will be able to use the remaining space of the **partition** without **formatting** it.
    > 
    > ```
    > $ df -i  # see list ( I need just one free inode here so move just one file into other PARTITION)
    > /dev/part1  1000 999 1 99.9%     /data
    > 
    > $ dd if=/dev/zero of=/data/new_data
    > $ mkfs.ext4 /data/new_data
    > $ mkdir /data1
    > $ mount /data/new_data /data1
    > 
    > ```
    > 
    > **for permanent mounting**
    > 
    > ```
    > $ echo "/data/new_data /data1 ext4 defaults 0 1" >> /etc/fstab
    > 
    > ```
    > 
    > ---
    > 
    > Recently ran into this issue when using apt or aptitude upgrade.
    > 
    > ```
    > df -h
    > 
    > Filesystem      Size  Used Avail Use% Mounted on
    > /dev/xvda1      7.8G  5.1G  2.3G  70% /
    > 
    > df -i
    > 
    > Filesystem     Inodes  IUsed  IFree IUse% Mounted on
    > /dev/xvda1     524288 521497   2791  100% /
    > 
    > ```
    > 
    > ---
    > 
    > Supposed you want to sort with the number of inodes in the `/usr/` and its first level subdir, based on @kph0x1 and @OttoLeichliter, with `--max-depth=1` flag, try:
    > 
    > ```
    > du --max-depth=1 --inodes /usr/ 2>/dev/null | sort -n
    > 
    > ```
    > 
    > The output may like this:
    > 
    > ```
    > 1   /usr/etc
    > 6   /usr/games
    > 151 /usr/local
    > 238 /usr/sbin
    > 328 /usr/lib64
    > 2203    /usr/bin
    > 3020    /usr/include
    > 32556   /usr/lib
    > 59052   /usr/src
    > 165062  /usr/share
    > 262618  /usr/
    > 
    > ```
    > 
    > As you can see, the most top 2 subdir of consuming inodes is `/usr/share` and `/usr/src`. Then you can dig into it by using that command again:
    > 
    > ```
    > du --max-depth=1 --inodes /usr/share/ 2>/dev/null | sort -n
    > 
    > ```
    > 
    > or
    > 
    > ```
    > du --max-depth=1 --inodes /usr/src/ 2>/dev/null | sort -n
    > 
    > ```
    > 
    > Do this recursively to find the suspicious folder and remove it.


## /var/lib/mlocate.db too big

- [disk usage - Why is /var/lib/mlocate.db almost 800 MB? - Ask Ubuntu](https://askubuntu.com/questions/23692/why-is-var-lib-mlocate-db-almost-800-mb)

    > On one of my systems that acts as a backup server, mlocate.db hit 9GB. The solution was to exclude the backup directories from locate, since I had no need to search them.
    > 
    > I did this by adding the backup directory to `PRUNEPATHS` in `/etc/updatedb.conf`.
    > 
    > Running `sudo updatedb` then reduced it to 1.6MB (and saves a huge amount of time indexing all of those files).


## Check folder size(du)

- [shell - Check folder size in Bash - Stack Overflow](https://stackoverflow.com/questions/16661982/check-folder-size-in-bash)

    > To check the size of all of the directories within a directory, you can use:
    > 
    > `du -h --max-depth=1`
    > 


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

