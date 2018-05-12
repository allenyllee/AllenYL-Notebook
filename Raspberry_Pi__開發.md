# Raspberry_Pi__開發

[toc]
<!-- toc --> 

## 連線到 Rpi

### 透過網路卡

1. Connect Raspberry Pi Directly with an Ethernet Cable

    - [1.How to Connect Raspberry Pi Directly with an Ethernet Cable - YouTube](https://www.youtube.com/watch?v=WBlXvGwkZa8)

    用 RJ45 網路線將Rpi接到筆電，之後打開putty，位址輸入 raspberry.local 就能連線到Rpi
    ![](https://screenshotscdn.firefoxusercontent.com/images/b82ee438-9436-4627-97a2-ab33f6774822.png)

    在cmd 下`ping raspberry.local` 就能得到 Rpi 的ip

    ![](https://screenshotscdn.firefoxusercontent.com/images/78357195-b3d3-433d-881c-2cd605562a75.png)


2. 設定固定ip

    將SD 卡插入電腦，在boot 分區中找到cmdline.txt，將ip 加在第一行最後面

    Origin:
    ```
    dwc_otg.lpm_enable=0 console=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait 
    ```

    Modify:
    ```
    dwc_otg.lpm_enable=0 console=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait ip=169.254.0.2
    ```

    ip格式如下:

    ```
    ip=192.168.1.200::192.168.1.1:255.255.255.0:rpi:eth0:off
    ip=<client-ip>:<server-ip>:<gw-ip>:<netmask>:<hostname>:<device>:<autoconf>
    ```

    如果筆電的乙太網卡沒有設固定ip，預設就會是169.254.x.x 開頭，因此Rpi 的固定ip也必須設為 169.254.x.x 開頭
    
    如果想要Rpi 固定網址為192.168.100.x，就要將比電的乙太網卡設定為固定ip192.168.100.1，如下
    
    ![](https://screenshotscdn.firefoxusercontent.com/images/e6d4f091-3f19-472f-9b2d-ae7a5c2eed9d.png)
    
    並且在 cmdline.txt 加上 `ip=192.168.100.2::192.168.100.1` 
    第一個ip表示 Rpi的ip，第二個表示 Gate Way 的ip，也就是筆電網卡的ip，如下：
    
    ```
    dwc_otg.lpm_enable=0 console=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait ip=192.168.100.2::192.168.100.1
    ```

    
    
    ---

    參考資料:

    - [SSH over direct ethernet connection - Raspberry Pi Forums](https://www.raspberrypi.org/forums/viewtopic.php?t=24993)

    - [RPi cmdline.txt - eLinux.org](https://elinux.org/RPi_cmdline.txt)

    - [How can I edit a Raspbian SD card image to use a static IP address within Windows? - Raspberry Pi Stack Exchange](https://raspberrypi.stackexchange.com/questions/13464/how-can-i-edit-a-raspbian-sd-card-image-to-use-a-static-ip-address-within-window?newreg=200e0b6265554a78b592443024071495)

    - [1.6 直接 連接到 另外一部電腦(用網路線) - 學習樹莓派--Raspberry Pi](https://sites.google.com/site/raspberypishare0918/home/di-yi-ci-qi-dong/zhi-jie-lian-bi-dian)

    - [IP Address - Raspberry Pi Documentation](https://www.raspberrypi.org/documentation/remote-access/ip-address.md)


### 透過Serial Port

- [[基礎] 從序列埠登入到 Raspberry Pi](https://www.raspberrypi.com.tw/1999/connect-to-raspberry-pi-via-serial/)

    ![](https://www.raspberrypi.com.tw/wp-content/uploads/2014/09/connect-serial-to-raspberry-pi-model-b-plus.png)


    插入USB 轉TTL 傳輸線後，打開裝置管理員，看是在哪個COM port
    ![](https://screenshotscdn.firefoxusercontent.com/images/0cc65927-47b6-4f85-ae18-5cfef414def8.png)

    在 Connection type 先選擇 Serial，再根據剛剛的連接埠依序填入 Serial line、Speed的值。由於剛剛裝置管理員是看到 COM5，因此在 Serial line 也填入 COM5，Speed 填入 115200。

    ![](https://screenshotscdn.firefoxusercontent.com/images/5d2ecf01-9d44-4474-aa53-a9cd1fdf01ba.png)


    相關的參數填完後，按 “Open” 就能連上 Raspberry Pi 如下圖。如果等了幾秒還是沒有畫面，可將 Raspberry Pi 重開(電源重插拔)，應該就可以順利看到登入訊息。


## Container OS

- [Ubuntu MATE for the Raspberry Pi 2 and Raspberry Pi 3 | Ubuntu MATE](https://ubuntu-mate.org/raspberry-pi/)

- [Ubuntu Core | Ubuntu](https://www.ubuntu.com/core)

- [Alpine Linux 挑戰最小 docker image OS | 小惡魔 - 電腦技術 - 工作筆記 - AppleBOY](https://blog.wu-boy.com/2015/12/a-super-small-docker-image-based-on-alpine-linux/)

- [6大Container OS介紹 | iThome](http://www.ithome.com.tw/news/95756)

- [RancherOS：一个运行Docker容器的最小Linux操作系统](http://www.infoq.com/cn/news/2015/03/rancheros-docker-linux)

- [IT Robotics Lab: Raspberry Pi 移植即時作業系統FreeRTOS](http://blog.ittraining.com.tw/2016/03/freertos.html)

- [用樹莓派架設SSL VPN 最低成本打造窮人翻牆梯 - 技術專欄 - 網管人NetAdmin](http://www.netadmin.com.tw/article_content.aspx?sn=1507030005)

- [Raspberry Pi 的基礎 - 40 套作業系統任你選之 2017 威力加強版 | IT 技術家](http://blog.itist.tw/2016/12/34-best-operating-systems-for-raspberry-pi.html)

- [Raspberry Pi 的基礎 - 24 套作業系統大集合，我該選誰？ | IT 技術家](http://blog.itist.tw/2015/11/how-to-choosing-operating-system-for-raspberry-pi.html)

- [一片Raspberry Pi能跑多少個Container？答案驚人 | iThome](http://www.ithome.com.tw/news/99447)


