# DevOps__開發維運

[toc]
<!-- toc --> 

# Continueous Integration/Deploy(CI, CD)

- [Turbo Charge Agile Processes with Deep Learning – Intuition Machine – Medium](https://medium.com/intuitionmachine/deep-learning-enables-agile-processes-6cfc353fa9b2)

- [Continuous Integration on your Machine/Deep Learning models with Moven – SSIX](https://ssix-project.eu/continuous-integration-with-moven/)

- [Moven, Machine/Deep Learning models distribution relying on the Maven infrastructure – SSIX](https://ssix-project.eu/moven-machinedeep-learning-models-distribution-relying-on-the-maven-infrastructure/)

- [Test-Driven Development for Data Science · Pivotal Engineering Journal](http://engineering.pivotal.io/post/test-driven-development-for-data-science/)

- [Continuous Integration for Data Science · Pivotal Engineering Journal](http://engineering.pivotal.io/post/continuous-integration-for-data-science/)

- [Continuous delivery for machine learning](https://www.slideshare.net/RajeshMuppalla/continuous-delivery-for-machine-learning-82257558)

## Tools

### Jenkins

Jenkins 的設定截圖，參考一下

1.  到管理Jenkins>系統設定>新增雲>Yet Another Docker
2.  在 Yet Another Docker 面板輸入Docker 所在URL ([localhost:4243](http://localhost:4243)) (這部份需要設定啟動 Docker API) 參考以下script  
    
    ```shell
    ######################
    # enable docker api for jenkins CI use
    # Enabling Docker Remote API on Ubuntu 16.04 – The Blog of Ivan Krizsan
    # [https://www.ivankrizsan.se/2016/05/18/enabling-docker-remote-api-on-ubuntu-16-04/](https://www.ivankrizsan.se/2016/05/18/enabling-docker-remote-api-on-ubuntu-16-04/)
    # test: curl [http://localhost:4243/version](http://localhost:4243/version)
    # test2: curl -X GET [http://192.168.5.5:4243/images/json](http://192.168.5.5:4243/images/json)
    ######################
    sudo sed -i '/ExecStart=\\/usr\\/bin\\/docker*/ c\\ExecStart=\\/usr\\/bin\\/dockerd\\/ -H fd:\\/\\/ -H tcp:\\/\\/[0.0.0.0:4243](http://0.0.0.0:4243)\\/' /lib/systemd/system/docker.service
    systemctl daemon-reload
    sudo service docker restart
    ```
      
    
3.  Image name 填上 `evarga/jenkins-slave` (目前只有測過這個image是可用的，但這個image裡面是ubuntu，所以要參考一下他的dockerfile，改寫成其他OS對應的套件，再build一個新的image出來)
    
    [evarga/jenkins-slave - Docker Hub](https://hub.docker.com/r/evarga/jenkins-slave/~/dockerfile/)
    
4.  label 可隨便填，之後會用到(這裡填another-docker) 
    
5.  launch method 選 Docker SSH computer launcher，credential 填登入image的帳號密碼(那個image的設定是 jenkins:jenkins) 

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.2&disp=emb&attbid=ANGjdJ9rsKN_9N3hW7g5MN-9np8GukKBUyKJ9dT5QUi4wK94C8ezHy6MsWy6EkFhQCUn0w9Ds8_BO0BuJxjz6eEgP6bGnG2UGdjKCQqYa67uoDynmQUjN8WtkobHayc&sz=s0-l75-ft&ats=1521905790349&rm=15f2df6dd368d970&zw&atsh=1)  
  

6. 主畫面選擇 新增作業  

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.3&disp=emb&attbid=ANGjdJ9OgjFcZoMxsbZmCX2uEdC7nTf5YdK6RN3EtJV8j-tvfsH5xjsysDGjgPeyVPRdJK7Sp5JkwIXonxrRIxhMKI4_Ekxsw_fJiJ1GzdPjVNh8YGaMVuvcQobZ5K0&sz=s0-l75-ft&ats=1521905790349&rm=15f2df6dd368d970&zw&atsh=1)  

  

7. 輸入專案名稱，選擇建置Free-Style 軟體專案，按ok  

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.4&disp=emb&attbid=ANGjdJ_HbTb4MbBTIVeig6Of7x5NpxvzCfLulRMYSrv4TBn0UHGZq9YGqi1RyEgFE4D3lShM3mAraDA1QuhcYM_hqPqxc5ttmzZkSKDVXO7VHA-qB5jWPJTzcaPzoHo&sz=s0-l75-ft&ats=1521905790349&rm=15f2df6dd368d970&zw&atsh=1)  
  

8. 限制執行節點 填入 another-docker，在執行shell 中填入`echo hello world`


    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.1&disp=emb&attbid=ANGjdJ8rlMHD6OIDDXVZlomz_BCWoF57ldGGkkybqpwKfiuouDzkcUogGaO9yui12GX9-bZK-4FD8dhxTsLXwgVYDbyu-9gzlsYLJ01WVyIBsDKuOpd6UYrq-FQqr2Q&sz=s0-l75-ft&ats=1521905790349&rm=15f2df6dd368d970&zw&atsh=1)  

  

  

9. 按下 馬上建置，過一陣子建置歷程中會出現一條紀錄，點進去可以看見內容  

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.5&disp=emb&attbid=ANGjdJ_3ReJfVYImessuDwtaJU9BJLtzkkxpu8r_F70Mb_HP5x5xcoByvUWWk_h5wxmYOZuaxItp7il4xvyYXUWuXKgku_x4Up75zCEnMnBWQYjF8JS_yi9gmQQYQyc&sz=s0-l75-ft&ats=1521905790350&rm=15f2df6dd368d970&zw&atsh=1)  

  

  

10. 點入Console Output 可以看見 執行結果，這個結果表示在該docker image 中執行echo hello world 成功

    這表示可以執行任何command，可以執行git clone XXX 把 code 抓下來，也可以透過 gitlab-plugin 作到這件事

    [jenkinsci/gitlab-plugin: A Jenkins plugin for interfacing with GitLab](https://github.com/jenkinsci/gitlab-plugin)

    如果失敗的話就會return error code，這裡的狀態就會顯示錯誤  

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.6&disp=emb&attbid=ANGjdJ-3Ig78Cn2zrrscPkOjRpr1ty3mXK-4Wc0p01u1pjCmORKmu-NDSUedyV3yacCyU1SkhljUwBwMjRBl_KXJ3wqPO8LM_GkMoEgPwHRFf9pg7H9s5ZLhFrLM9no&sz=s0-l75-ft&ats=1521905790350&rm=15f2df6dd368d970&zw&atsh=1)  
  

  

11. 如果需要build 完可以直接燒到機台上的話，可能要修改docker run 的設定，加上 `--privileged` 參數 應該就可以access NVMe device

    這樣就可以執行燒錄，或其他的測試 script，中間如果發生任何意外中斷的話，就會直接 return failed

    (可以在所有的測試機台上安裝docker client，在 Yet Another Docker 的地方選擇 Add Docker Template，輸入測試機台的url，就可在所有機台上進行自動測試，但windows 可能還沒辦法，主要原因是windows 的docker client 是跑在虛擬機中，沒有辦法access real HW，也許未來會支援吧，可以關注一下) 

    ![](https://mail.google.com/mail/u/0/?ui=2&ik=d8d4e58d88&view=fimg&th=15f2df6dd368d970&attid=0.7&disp=emb&attbid=ANGjdJ-sefQKTrCCwrBcx66uumuhJfghe8Rx_dF8wnjj13WlEuTlZWfYNiMGeA7Ey4yYzWHcIN7lQyBnSqUTrhZajluscddnKDdXIWKSnvj-Uw5jmMuzEt79ULlo1vo&sz=s0-l75-ft&ats=1521905790350&rm=15f2df6dd368d970&zw&atsh=1)

### TeamCity

- [持续集成：TeamCity 的安装和使用 - 简书](https://www.jianshu.com/p/255a484555d9)


    > 同类工具
    > ----
    > 
    > -   Jenkins：[http://jenkins-ci.org/](https://link.jianshu.com?t=http://jenkins-ci.org/)
    > -   Travis CI：[http://travis-ci.org/](https://link.jianshu.com?t=http://travis-ci.org/)
    > -   Bamboo：[http://www.atlassian.com/software/bamboo](https://link.jianshu.com?t=http://www.atlassian.com/software/bamboo)
    > -   Hudson：[http://hudson-ci.org/](https://link.jianshu.com?t=http://hudson-ci.org/)
    > -   QuickBuild：[http://www.pmease.com/](https://link.jianshu.com?t=http://www.pmease.com/)
    > -   其他：[http://www.oschina.net/project/tag/344/ci?lang=0&os=0&sort=view&p=1](https://link.jianshu.com?t=http://www.oschina.net/project/tag/344/ci?lang=0&os=0&sort=view&p=1)
    > -   好的网络文章介绍：
    >     -   [持续集成工具的选择](https://link.jianshu.com?t=http://cristal.iteye.com/blog/482658)
    > 
    > TeamCity 入门
    > -----------
    > 
    > -   先来看一段官网的介绍视频
    > -   这个视频其实已经很清楚地说明了一个整理流程是怎样的，我今天只是做一个更加清晰的细节讲解而已
    > -   你需要穿越：[https://www.youtube.com/watch?v=J-iYMMG6jmc#action=share](https://link.jianshu.com?t=https://www.youtube.com/watch?v=J-iYMMG6jmc#action=share)
    > 
    > ### TeamCity 安装部署（Linux 环境）
    > 
    > -   在我讲之前，如果你英文还可以，就到官网这里看下：
    > -   [Installation Quick Start](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/Installation+Quick+Start#InstallationQuickStart-onLinuxandOSX)
    > -   安装环境要求：
    >     -   JDK 1.7 以上，如果你要使用的是 2016 最新的 TeamCity 9.1 的话，JDK 官网推荐的 1.8
    > -   安装包下载：[https://www.jetbrains.com/teamcity/download/#section=linux-version](https://link.jianshu.com?t=https://www.jetbrains.com/teamcity/download/#section=linux-version)
    > -   开始安装（eg：TeamCity-9.1.6.tar.gz）：
    >     -   解压压缩包（解压速度有点慢）：`tar zxf TeamCity-9.1.6.tar.gz`
    >     -   解压完的目录结构讲解：[https://confluence.jetbrains.com/display/TCD9/TeamCity+Home+Directory](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/TeamCity+Home+Directory)
    >     -   下载的 tar.gz 的本质是已经里面捆绑了一个 Tomcat，所以如果你会 Tomcat 的话，有些东西你可以自己改的。
    >     -   按我个人习惯，把解压缩的目录放在 usr 目录下：`mv TeamCity/ /usr/program/`
    >     -   进入解压目录：`cd /usr/program/TeamCity/`
    >     -   启动程序：`/usr/program/TeamCity/bin/runAll.sh start`
    >     -   停止程序：`/usr/program/TeamCity/bin/runAll.sh stop`
    >     -   启动需要点时间，最好能给它一两分钟吧
    > 
    > ### 首次进入
    > 
    > -   假设我们已经启动了 TeamCity
    > -   访问（TeamCity 默认端口是：8111）：[http://192.168.1.113:8111/](https://link.jianshu.com?t=http://192.168.1.113:8111/)
    > -   如果访问不了，请先关闭防火墙：`service iptables stop`
    > -   你也可以选择把端口加入白名单中：
    >     -   `sudo iptables -I INPUT -p tcp -m tcp --dport 8111 -j ACCEPT`
    >     -   `sudo /etc/rc.d/init.d/iptables save`
    >     -   `sudo service iptables restart`
    > -   如果你要改变端口，找到下面这个 8111 位置：`vim /usr/program/TeamCity/conf/server.xml`
    > 
    > ```
    > <Connector port="8111" ...
    > 
    > ```
    > 
    > -   在假设你已经可以访问的情况，我们开始进入 TeamCity 的设置向导：
    > -   ![](//upload-images.jianshu.io/upload_images/12159-eef693c16006891c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图英文所示，TeamCity 的一些软件安装的配置、服务的配置默认都会放在：`/root/.BuildServer`
    >     -   如果你要了解更多 TeamCity Data Directory 目录，你可以看：[https://confluence.jetbrains.com/display/TCD9/TeamCity+Data+Directory](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/TeamCity+Data+Directory)
    > -   ![](//upload-images.jianshu.io/upload_images/12159-085f9195ebf6d67c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图英文所示，TeamCity 的一些构建历史、用户信息、构建结果等这类数据是需要放在关系型数据库上的，而默认它给我们内置了一个。
    >     -   如果你要了解更多 TeamCity External Database，你可以看：[https://confluence.jetbrains.com/display/TCD9/Setting+up+an+External+Database](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/Setting+up+an+External+Database)
    >     -   首次使用，官网是建议使用默认的：`Internal(HSQLDB)`，这样我们无需在一开始使用的就考虑数据库迁移或安装的问题，我们只要好好感受 TeamCity 给我们的，等我们决定要使用了，后续再更换数据也是可以的。但是内置的有一个注意点：'TeamCity with the native MSSQL external database driver is not compatible with Oracle Java 6 Update 29, due to a bug in Java itself. You can use earlier or later versions of Oracle Java.'
    >     -   假设我们就选 `Internal(HSQLDB)` ，则在创建初始化数据库的过程稍微需要点时间，我这边是几分钟。
    > -   ![](//upload-images.jianshu.io/upload_images/12159-c5553269a058698e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图所示，接受下协议
    > -   ![](//upload-images.jianshu.io/upload_images/12159-f00cec34cc240263.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图所示，我们要创建一个顶级管理员账号，我个人习惯测试的账号是：`admin`，`123456`
    > -   ![](//upload-images.jianshu.io/upload_images/12159-9c5dc64753ab6b5c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图所示，安装完首次进来地址：[http://192.168.1.113:8111/profile.html?tab=userGeneralSettings](https://link.jianshu.com?t=http://192.168.1.113:8111/profile.html?tab=userGeneralSettings)
    >     -   我们可以完善一些管理员信息和基础配置信息，这些配置不配置都无所谓了，只是完善了可以更加好用而已
    >     -   如果你有 SMTP 的邮箱，你可以来这里开启邮件通知功能：[http://192.168.1.113:8111/admin/admin.html?item=email](https://link.jianshu.com?t=http://192.168.1.113:8111/admin/admin.html?item=email)
    >     -   如果你要开启通知功能那肯定下一步就是考虑通知内容的模板要如何设定：[https://confluence.jetbrains.com/display/TCD9//Customizing+Notifications](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9//Customizing+Notifications)
    >     -   模板存放路径在：`/root/.BuildServer/config/_notifications`，用的是 FreeMarker 的语法
    > 
    > ### 项目的构建、管理
    > 
    > -   建议可以看下官网：[https://confluence.jetbrains.com/display/TCD9/Configure+and+Run+Your+First+Build](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/Configure+and+Run+Your+First+Build)
    > -   现在让我们开始创建一个项目进行构建
    > -   项目管理地址：[http://192.168.1.113:8111/admin/admin.html?item=projects](https://link.jianshu.com?t=http://192.168.1.113:8111/admin/admin.html?item=projects)
    > -   假设我现在有一个项目的结构是这样的：
    > 
    > ```
    > - Youshop-Parent，输出是 pom
    >     - Youshop-manage，输出是 pom
    >         - Youshop-pojo，输出 jar
    > 
    > ```
    > 
    > -   我们现在以 Youshop-pojo 为例，让它自动构建并发布到 Nexus 中，其他项目道理是一样的，这里就不多说。
    > -   ![](//upload-images.jianshu.io/upload_images/12159-9b7011ede04768a7.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    > -   如上图，由于目前只要是公司的项目都应该是在版本控制的，所以这里我们选择：**Create project from URL**
    > -   ![](//upload-images.jianshu.io/upload_images/12159-797389cad89b851a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    > -   如上图，我们可以看出 TeamCity 也支持 HTTP、SVN、Git 等链接方式。
    > -   ![](//upload-images.jianshu.io/upload_images/12159-cbf0825bae391241.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    > -   输入你项目托管商的账号密码，我这里用的是 oschina 的。
    > -   ![](//upload-images.jianshu.io/upload_images/12159-6db995399c8a30c8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    > -   账号、密码验证通过，现在可以给这个项目配置一个项目基本信息。
    > -   ![](//upload-images.jianshu.io/upload_images/12159-7c16133dee0c9733.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    > -   在从版本控制中下载文件和扫描文件
    > -   ![](//upload-images.jianshu.io/upload_images/12159-30a662b62e0094a2.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    > -   TeamCity 自动扫描到我是用 Maven 构建的项目，所以把 POM 文件找出来了，如果你一个项目有多种构建方式，有对应的配置文件的话，这里都会显示出来的。
    > -   我们勾选 Maven 前面的复选框，点击：`Use Selected`
    > -   ![](//upload-images.jianshu.io/upload_images/12159-9672cbc538ca5ac5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    > -   由于我们的目标是构建完自动发布到 Nexus，所以我们的 **Maven Goals** 应该是：`clean install deploy`，这里我们应该点击：`Edit`，进行编辑。
    > -   如果你不懂 **Maven Goals**，那你需要学习下，这个很重要。
    >     -   官网：[http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html](https://link.jianshu.com?t=http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)
    > -   ![](//upload-images.jianshu.io/upload_images/12159-f093c5fd45245c3b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，这台服务器必须装有 Maven、JDK
    >     -   如上图，`Goals` 我们的目标是 `clean install deploy`
    >     -   如上图，`Maven Home` 我建议是自己自定义路径，这样肯定不会有问题。所以你服务器上的 Maven 安装路径是什么你就在这里填写上去。Maven 目前支持的最高版本是：3.2.5
    >         -   下载 Maven 3.2.5：[http://archive.apache.org/dist/maven/maven-3/3.2.5/binaries/](https://link.jianshu.com?t=http://archive.apache.org/dist/maven/maven-3/3.2.5/binaries/)
    >     -   如上图，`Java Parameters` 我建议也是自己自定义路径，别选择其他选项。
    > -   ![](//upload-images.jianshu.io/upload_images/12159-73efbf55f00c40cd.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，点击 `run`，开始手动构建该项目
    > -   ![](//upload-images.jianshu.io/upload_images/12159-9752a0ceef12dd66.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，我们看到简略的构建日志
    > -   ![](//upload-images.jianshu.io/upload_images/12159-ea94e2a7e8f71255.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    > -   ![](//upload-images.jianshu.io/upload_images/12159-3e81c357ae6ba6bf.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上 2 张图，我们看到详细的构建内容
    > -   ![](//upload-images.jianshu.io/upload_images/12159-ae4d8a263011163a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，当我们版本控制中有提交的时候，TeamCity 会识别到记录
    > -   ![](//upload-images.jianshu.io/upload_images/12159-4d42a184082dbfa7.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，我们可以看到提交的 Commit Message 信息。
    >     -   如上图，右边红圈的三个按钮是用来处理这次提交的，常用的是第一次按钮，点击对此次版本进行构建
    > -   ![](//upload-images.jianshu.io/upload_images/12159-028a3933f49716cc.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，如果你要看所有的提交记录，可以在 Change Log 看到并且指定版本构建
    > -   ![](//upload-images.jianshu.io/upload_images/12159-1b35005bfb3cc68c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，如果在你不想要这个项目的时候可以进行删除
    > -   ![](//upload-images.jianshu.io/upload_images/12159-dc9d726fc6911e50.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，因为 Goals 里面有 deploy 命令，所以构建完成会发布到 Nexus 中，这样团队的人就可以用到最新的代码了
    > -   ![](//upload-images.jianshu.io/upload_images/12159-55801b4e2e9c98f5.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上 gif 图演示，项目常去的几个配置地方就是这样些了
    > 
    > ### 配置自动构建触发行为
    > 
    > -   官网提供的触发行为有：[https://confluence.jetbrains.com/display/TCD9/Configuring+Build+Triggers](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/Configuring+Build+Triggers)
    > -   下面我们举例说常见的：`VCS Trigger`、`Schedule Trigger`
    > -   ![](//upload-images.jianshu.io/upload_images/12159-1bf4408f74954836.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，点击 `Add new trigger` 添加触发器
    > -   ![](//upload-images.jianshu.io/upload_images/12159-53f50fe6d1452e25.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，常见的触发器就这些了
    > -   ![](//upload-images.jianshu.io/upload_images/12159-07c36dd4cee4570f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，配置好 `VCS Trigger` 效果是，当我们有代码提交的时候，TeamCity 检查到新版本之后自动构建，这个最常用
    > -   ![](//upload-images.jianshu.io/upload_images/12159-92f098fa029d158e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，`Schedule Trigger` 的作用就是定时构建，除了常用的几个输入框设置定时外，TeamCity 还可以使用 Cron 语法进行设置
    >     -   TeamCity 采用的 Cron 语法是 Quartz，具体你可以看：[Quartz CronTrigger Tutorial](https://link.jianshu.com?t=http://www.quartz-scheduler.org/documentation/quartz-1.x/tutorials/crontrigger#CronTriggersTutorial-Specialcharacters)
    >     -   如果你不懂 Cron 语法那就算了，但是我想做 Java 这个应该要会的
    > 
    > ### 集成 IntelliJ IDEA
    > 
    > -   安装 IntelliJ IDEA：[https://confluence.jetbrains.com/display/TCD9/IntelliJ+Platform+Plugin](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/IntelliJ+Platform+Plugin)
    > -   ![](//upload-images.jianshu.io/upload_images/12159-b0b7e9b7256df1a0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，我们可以直接连上 TeamCity 服务器，这里的用户名密码是 TeamCity 的账号系统。
    > -   ![](//upload-images.jianshu.io/upload_images/12159-3f37daffdbcc5dc0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/647)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，连上去的效果是这里会打钩
    > -   ![](//upload-images.jianshu.io/upload_images/12159-59a8ff0b6a73ccc6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
    > 
    >     TeamCity 向导
    > 
    >     -   如上图，我们可以直接把别人提交的内容做 patch 直接用 IntelliJ IDEA 进行整合
    >     -   还有其他很多结合玩法大家可以自己去尝试下
    > 
    > ### 其他
    > 
    > -   TeamCity 的插件列表：[https://confluence.jetbrains.com/display/TW/TeamCity+Plugins](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TW/TeamCity+Plugins)
    > -   使用外部数据库：
    >     -   使用外部数据库：[https://confluence.jetbrains.com/display/TCD9/Setting+up+an+External+Database](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/Setting+up+an+External+Database)
    >     -   迁移到外部数据库：[https://confluence.jetbrains.com/display/TCD9/Migrating+to+an+External+Database](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/Migrating+to+an+External+Database)
    > -   数据备份：[https://confluence.jetbrains.com/display/TCD9/TeamCity+Data+Backup](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/TeamCity+Data+Backup)
    > -   代码检查功能：
    >     -   [https://confluence.jetbrains.com/display/TCD9/Code+Quality+Tools](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/Code+Quality+Tools)
    >     -   [https://confluence.jetbrains.com/display/TCD9/Code+Quality+Tools#CodeQualityTools-IntelliJIDEA-poweredCodeAnalysisTools](https://link.jianshu.com?t=https://confluence.jetbrains.com/display/TCD9/Code+Quality+Tools#CodeQualityTools-IntelliJIDEA-poweredCodeAnalysisTools)
    >     -   [https://confluence.jetbrains.com/pages/viewpage.action?pageId=74847276](https://link.jianshu.com?t=https://confluence.jetbrains.com/pages/viewpage.action?pageId=74847276)
    > 


## Smoke test

- [Smoke test for a Docker image – ngeor.wordpress.com](https://ngeor.wordpress.com/2017/12/28/smoke-test-for-a-docker-image/)

    > According to [Wikipedia](https://en.wikipedia.org/wiki/Smoke_testing_(software)), a smoke test is *a preliminary test that reveals simple failures severe enough to (for example) reject a prospective software release*. *The process of smoke testing aims to determine whether the application is so badly broken as to make further immediate testing unnecessary.* If we consider our dockerized blog-helm web application, a possible smoke test can be: can we pull the image from the registry? If we run the image, does the container stay alive or does it crash immediately? In this post, I'll implement this in an extra build configuration in TeamCity with a generic bash script doing the actual work.
    > 
    > First we need to create the new build configuration:
    > 
    > ![2017-12-28 08_21_44-Create Build Configuration --- TeamCity.png](https://ngeor.files.wordpress.com/2017/12/2017-12-28-08_21_44-create-build-configuration-e28094-teamcity.png?w=660)
    > 
    > Adding a new build configuration for the Smoke Test
    > 
    > Just like in the previous post, we need to make it part of the [build chain](https://ngeor.wordpress.com/2017/12/27/build-chains-in-teamcity/), so it needs the VCS root:
    > 
    > ![2017-12-28 08_22_48-Smoke Test Configuration --- TeamCity.png](https://ngeor.files.wordpress.com/2017/12/2017-12-28-08_22_48-smoke-test-configuration-e28094-teamcity.png?w=660)
    > 
    > Attaching VCS root
    > 
    > and the snapshot dependency. Note that the only artifact needed is the `image-tag.txt` file that contains the Docker image tag name.
    > 
    > ![2017-12-28 08_24_40-Smoke Test Configuration --- TeamCity.png](https://ngeor.files.wordpress.com/2017/12/2017-12-28-08_24_40-smoke-test-configuration-e28094-teamcity.png?w=660)
    > 
    > Configuring dependencies
    > 
    > I'd like to smoke test all feature branches automatically on every commit, so I configure a Finished Build trigger:
    > 
    > ![2017-12-28 08_26_31-Smoke Test Configuration --- TeamCity.png](https://ngeor.files.wordpress.com/2017/12/2017-12-28-08_26_31-smoke-test-configuration-e28094-teamcity.png?w=660)
    > 
    > Automatically smoke test all green Commit Stage builds
    > 
    > and I don't want to be able to deploy to the test environment unless the smoke test has passed, so I add another snapshot dependency to the Deploy to Test build configuration:
    > 
    > ![2017-12-28 08_29_16-Deploy To Test Configuration --- TeamCity.png](https://ngeor.files.wordpress.com/2017/12/2017-12-28-08_29_16-deploy-to-test-configuration-e28094-teamcity.png?w=660)
    > 
    > Only deploy when smoke test passes
    > 
    > With these changes we have a new build chain with the Smoke Test build configuration in between Commit Stage and Deploy to Test:
    > 
    > ![2017-12-28 08_52_34-Blog Helm __ Commit Stage _ Build Chains --- TeamCity.png](https://ngeor.files.wordpress.com/2017/12/2017-12-28-08_52_34-blog-helm-__-commit-stage-_-build-chains-e28094-teamcity.png?w=660)
    > 
    > The new build chain
    > 
    > Now the build pipeline is configured and we just need to write the script that performs the smoke test. The script is a bit long at 98 lines of Bash, so I'll just [link to it](https://github.com/ngeor/blog-helm/blob/v1.5.1/ci-scripts/smoke-test-docker-image.sh) if you want to read it. Its logic is roughly as follows:
    > 
    > -   Pull the image from the custom docker registry
    > -   Start a container with this image in the background (so that the script can continue)
    > -   Wait until the container starts (it retries 5 times with 5 seconds sleep between each retry). If the container can't start at all, either it's completely wrong, or the host is too slow, or something else weird is going on.
    > -   Wait to verify that the container stays up (same retry rules as before). This is the actual substance of this smoke test. The container starts, but does it stay up? This is supposed to be a web application, so it should stay up to serve incoming HTTP requests.
    > -   Cleanup: stop the container, print its logs (useful for troubleshooting), remove the container.
    > 
    > Let's see an example build log of a successful smoke test:
    > 
    > ![2017-12-28 09_15_19-Blog Helm __ Smoke Test _ #1.5.0-smoke-test.2 (28 Dec 17 08_09) _ Build Log --- Te.png](https://ngeor.files.wordpress.com/2017/12/2017-12-28-09_15_19-blog-helm-__-smoke-test-_-1-5-0-smoke-test-2-28-dec-17-08_09-_-build-log-e28094-te.png?w=660)
    > 
    > Build log of a passed smoke test
    > 
    > You can see that the container starts and stays up. The script tried 5 times and the container didn't die inexplicably in between, so that's good enough as far this smoke test is concerned.
    > 
    > To get a red build out of this smoke test, I modified the `CMD` instruction in the `Dockerfile` so that it references a non-existing JavaScript file (`indexx.js` instead of `index.js`). This is the resulting build log:
    > 
    > ![2017-12-28 09_22_22-Blog Helm __ Smoke Test _ #1.5.0-smoke-test.3 (28 Dec 17 08_21) _ Build Log --- Te.png](https://ngeor.files.wordpress.com/2017/12/2017-12-28-09_22_22-blog-helm-__-smoke-test-_-1-5-0-smoke-test-3-28-dec-17-08_21-_-build-log-e28094-te.png?w=660)
    > 
    > Build log of a failed smoke test
    > 
    > The container starts successfully, but a few seconds later it dies. The smoke test script prints the container logs, so we can clearly see that nodeJS exited because it couldn't find the file `/app/indexx.js`.
    > 
    > This smoke test costs a bit more than 30" when it is green and less when it is red. Including some overhead for preparing and starting the build, this means that, on the happy flow, we have almost an entire minute to wait before we can deploy our application. What are we buying with this minute to justify spending it?
    > 
    > The checks we're doing (Can we pull the image? Does the container stay up?) would be implicit in an integration test, because you have to start the container in order to do the integration test against the running application. The advantage with a separate smoke test is that it's easier to troubleshoot what went wrong. If you see a failed smoke test, you understand that there's nothing wrong with your integration tests but something more fundamental has gone wrong.


# CI for Machine Learning Project

- [Continuous Integration for ML Projects – Onfido Tech – Medium](https://medium.com/onfido-tech/continuous-integration-for-ml-projects-e11bc1a4d34f)

    > Jenkins is our continuous integration system of choice and we use it for building and deploying applications. All of our repos contain a Jenkinsfile which defines the pipeline that Jenkins will execute. Most common steps of the pipeline are:
    > 
    > -   Build a Docker image
    > -   Run our unit/integration test (within a instance of that Docker image)
    > -   Run acceptance tests (end-to-end, may require some orchestration)
    > -   Deploy to staging and production
    > 
    > Every time developer pushes their code to remote git server, Jenkins reads the pipeline file and follows the appropriate steps. Having this pipeline define for each repository has proven to give us a lot of flexibility to each service steps.
    > 
    > Here is a visualization of these processes:

    > ![](https://cdn-images-1.medium.com/max/1200/1*b1N4Scplrl0SPIkPfIU4wA.png)


    > #### **Testing models before deploying**
    > 
    > As we do with all other software, before we release changes to ML models we want to have a certain degree of confidence that our changes have not negatively impacted how our system behaves (at least in unexpected ways). But how can we be confident that our models perform as we expect them?
    > 
    > The solution we found is to introduce a new type of test in our test suite: **accuracy tests**.
    > 
    > An accuracy test exercises the inference code for a test data sample for a model to verify that the output is above an expected threshold.
    > 
    > If you remember our CI lifecycle above, we made the following changes:
    > 
    > -   Allow docker image building step to resolve the model dependencies
    > -   Run unit/integration tests (fast to fail)
    > -   Run acceptance test (usually slower than the previous set)
    > -   Download the test dataset (currently using S3 to store this information)
    > -   Trigger the accuracy tests (speed can vary greatly depending on hardware, sample size, etc.)
    > 
    > With this setup, we have a high degree of confidence when making changes in our services that the performance of models have been unaffected — enabling us to move a lot faster.
    > 
    > As this runs inside a container, we can also run these tests locally.
    > 
    > In some scenarios, we have had to make different compromises:
    > 
    > -   For services using small and fast inference models, we can use small (but still statistically significant) test datasets which — with some parallelising — can run on every build and finish in seconds/minutes
    > -   For other services using models with higher resource needs/slower inference time, we chose to run them on a scheduled basis on integration branches. This balances time for feedback with certainty that we’ll still catch regressions before they reach production
    > 
    > At this point we have a system that allows us to add new models, make change with confidence and deploy to production in a streamlined way. The pipeline looks similar to before:
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/1*N6L8T495ii4EZFEzgZZbow.png)
    > 
    > Pipeline after the introduction of ML models


- [Don’t be afraid of the big bad blob! – Onfido Tech – Medium](https://medium.com/onfido-tech/dont-be-afraid-of-the-big-bad-blob-3da567f7a67b)

    > If you’re familiar with machine learning, you probably know that these trained models can sometimes get pretty big, up to multiple GBs per model.
    > 
    > Now, think of these models stored in your Git repository. Every change in these large files causes the repository to grow by the size of the file. You can then easily get a repository that weights dozens of GBs, which is much harder to maintain — and not really what Git was built for.

    > After spending quite some time in researching and brainstorming, we came up with the following architecture
    >
    > ![](https://cdn-images-1.medium.com/max/1200/1*dnUxUa1uBUoy7TgJU1eWIA.jpeg)
    >
    > We have our code repository. Part of that repository is the Dockerfile which includes a specific instruction to resolve all the dependencies of the project as described in the dependencies.json file.
    > 
    > Each dependency is provided with its path of where it can be found, and the version required for it.
    > 
    > All of the dependencies are stored in S3 which is a fast, reliable, scalable and robust remote file storage.
    > 
    > #### Architecture in depth
    > 
    > Our models are being stored and versioned in an S3 bucket by our machine learning engineers. This architecture scales easily to help us industrialise our machine learning pipelines.
    > 
    > This led us to develop and recently open-source the [s3-uploader](https://github.com/onfido/s3-uploader) command line tool. This command line tool is written in Python, and its purpose is to upload any resource to S3 while taking care of the versioning for you.
    > 
    > To use it, one just simply needs to run the following command:
    > ```shell
    > s3-uploader -b s3-bucket -f /path/to/large_blob -l project/blobs/data/
    > ```
    > Where you only need to provide the **name of your bucket**, the **path to the blob** and **the location in which the blob should be placed in your project**. After that, you’ll get the json output to add to the dependencies.json file.
    > 
    > Inside the code repository, we have the dependencies.json file which is a configuration file that provides all of the project’s dependencies that are not stored in git. The file content is as follows:
    > 
    > ```json
    > { 
    >   "dependencies": [ 
    >     { 
    >       "location": "project/models/data/", 
    >       "name": "trained_model", 
    >       "version": "2017-03-27-15-22-20" 
    >     }, 
    >     { 
    >       "location": "project/blobs/data/", 
    >       "name": "large_blob", 
    >       "version": "latest" 
    >     } 
    >   ], 
    >   "repository": "s3://s3-bucket" 
    > }
    > ```
    > 
    > In addition, we have the Dockerfile which contains all the instructions to build a docker container with all the code and the trained models that later will be deployed and run on Kubernetes.
    > 
    > The part of the Dockerfile that is in charge of resolving all the project’s dependencies is this one-liner:
    > ```dockerfile
    > # Resolve project's dependencies
    > 
    > RUN dependencies-resolver -c dependencies.json
    > ```
    > 
    > This led us to develop and recently open-source the [dependencies-resolver](https://github.com/onfido/dependencies-resolver) command line tool. The command line tool is written in Python and handles all the project’s S3 dependencies for you. In our use-case, the resolver use defined in the Dockerfile. While building the container, the resolver downloads all the dependencies and places them in their specified location. The tool is not required to run as part of the Dockerfile and can be used outside of that context.
    > 


# 文字 DevOpts (Literate DevOps)

- [Literate DevOps](http://howardism.org/Technical/Emacs/literate-devops.html)

    > Maintaining servers falls into two phases:
    > 
    > 1.  Bang head until server works
    > 2.  Capture effort into some automation tool like Puppet or Chef.
    > 
    > Recently, I’ve been playing around with making the first phase closer to the second. For lack of a better word, I’m calling it _literate devops_.

## 使用 Jupyter Notebook 實現文字 DevOpts (Literate DevOps)

- 範例:
    - [literate-ops/10k-single-jupyterhub.ipynb at master · allenyllee/literate-ops](https://github.com/allenyllee/literate-ops/blob/master/10k-single-jupyterhub.ipynb)

