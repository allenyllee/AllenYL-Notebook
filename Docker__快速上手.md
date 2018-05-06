# Docker__快速上手

[toc]
<!-- toc --> 

## What is docker

-   Docker 是一種輕量級的作業系統虛擬化解決方案，其所創造出的虛擬環境又稱為容器(container)。
    
-   傳統的虛擬化技術，如VirtureBox等，主要是用軟體虛擬出一整套硬體，然後在其上運行一套完整的OS。可想而知，運行效率相當低落。
    
-   Docker的創新在於想到: 既然原本就有OS 了，為何不好好利用呢？由於Linux OS 不同版本間的 kernel 是可以共用的，只要在上面實作一層虛擬 API，應用程式看起來就好像跑在不同機器上了呢！

![](https://screenshotscdn.firefoxusercontent.com/images/d6bb2271-9180-449a-960f-c14bd3c0adcc.png)


### docker command

- [什麼是 Docker · 《Docker —— 從入門到實踐》正體中文版](https://philipzheng.gitbooks.io/docker_practice/content/introduction/what.html)

- [什么是 Docker · Docker —— 从入门到实践](https://yeasy.gitbooks.io/docker_practice/content/introduction/what.html)

#### 操作容器
    
-   docker run ubuntu:14.04 /bin/echo 'Hello world'
    
-   docker run -t -i ubuntu:14.04 /bin/bash #交互模式
    
-   docker run ubuntu:17.10 /bin/sh -c "while true; do echo hello world; sleep 1; done" #後台模式
    
-   docker container ls #列出容器
    
-   docker exec -i \[container_id\] bash #進入容器
    
-   docker container stop \[container_id\] #終止容器
    
-   docker container rm \[container_name\] #刪除容器
    

#### 操作鏡像
    
-   在 Dockerfile 文件所在目录执行：docker build -t \[image_name\]:\[tag\] . #製作鏡像
    
-   docker pull \[image\]:\[tag\] #從Dockerhub拉取鏡像


### Container Architecture

- [Architecting Containers Part 1: Why Understanding User Space vs. Kernel Space Matters – Red Hat Enterprise Linux Blog](https://rhelblog.redhat.com/2015/07/29/architecting-containers-part-1-user-space-vs-kernel-space/)

    > before diving head-first into a discussion about the architecture and deployment of containers in a production environment, there are three important things that developers, architects, and systems administrators, need to know :
    > 
    > 1.  All applications, inclusive of containerized applications, rely on the underlying kernel
    > 2.  The kernel provides an API to these applications via system calls
    > 3.  Versioning of this API matters as it’s the “glue” that ensures deterministic communication between the user space and kernel space
    > 
    > While containers are sometimes treated like virtual machines, it is important to note, unlike virtual machines, the kernel is the only layer of abstraction between programs and the resources they need access to. Let’s see why.
    > 
    > All processes make system calls:
    > 
    > [![User Space vs. Kernel Space - Simple User Space](https://rhelblog.files.wordpress.com/2015/07/user-space-vs-kernel-space-simple-user-space.png?w=640&h=253)](https://rhelblog.files.wordpress.com/2015/07/user-space-vs-kernel-space-simple-user-space.png) As containers are processes, they also make system calls:
    > 
    > [![User Space vs. Kernel Space - Simple Container](https://rhelblog.files.wordpress.com/2015/07/user-space-vs-kernel-space-simple-container.png?w=640&h=253)](https://rhelblog.files.wordpress.com/2015/07/user-space-vs-kernel-space-simple-container.png)
    > 
    > OK, so you understand what a process is, and that containers are processes, but what about the files and programs that live inside a container image? These files and programs make up what is known as [user space](http://www.linfo.org/user_space.html). When a container is started, a program is loaded into memory from the container image. Once the program in the container is running, it still needs to make system calls into [kernel space](http://www.linfo.org/kernel_space.html). The ability for the user space and kernel space to communicate in a deterministic fashion is critical.

### Container Perfomance

- [What is the runtime performance cost of a Docker container - Stack Overflow](https://stackoverflow.com/questions/21889053/what-is-the-runtime-performance-cost-of-a-docker-container)

    > [Here](http://domino.research.ibm.com/library/cyberdig.nsf/papers/0929052195DD819C85257D2300681E7B/$File/rc25482.pdf) is an excellent 2014 IBM research paper titled "An Updated Performance Comparison of Virtual Machines and Linux Containers" by Felter et al. that provides a comparison between bare metal, KVM, and Docker containers. **The general result is that Docker is nearly identical to Native performance and faster than KVM in every category.**
    > 
    > The exception to this is Docker's NAT - if you use port mapping (e.g. `docker run -p 8080:8080`) then you can expect a minor hit in latency, as shown below. However, you can now use the host network stack (e.g. `docker run --net=host`) when launching a Docker container, which will perform identically to the `Native` column (as shown in the Redis latency results lower down).
    > 
    > ![Docker NAT overhead](https://i.stack.imgur.com/4yRh1m.png)
    > 
    > 
    > 
    > Taking a look at Disk IO:
    > 
    > ![IO docker vs kvm vs native](https://i.stack.imgur.com/2Ftytm.png)
    > 
    > Now looking at CPU overhead:
    > 
    > ![docker cpu overhead](https://i.stack.imgur.com/wZZH6m.png)
    > 
    > Now some examples of memory (read the paper for details, memory can be extra tricky)
    > 
    > ![docker memory comparison](https://i.stack.imgur.com/aHPVkm.png)
    > 


## install docker


### install docker in bash on windows

- [Running Docker containers on Bash on Windows - Jayway](https://blog.jayway.com/2017/04/19/running-docker-on-bash-on-windows/)

- [Installing the Docker client on Windows Subsystem for Linux (Ubuntu)](https://medium.com/@sebagomez/installing-the-docker-client-on-ubuntus-windows-subsystem-for-linux-612b392a44c4)

- [Can you run Docker natively on the new Windows 10 (Ubuntu) bash userspace? - Server Fault](https://serverfault.com/questions/767994/can-you-run-docker-natively-on-the-new-windows-10-ubuntu-bash-userspace#_=_)


## Docker swarm vs. Kubernetes vs. Mesos vs. Amazon ECS


- [Kubernetes Vs Docker Swarm - A Comparison of Containerization Platform](https://vexxhost.com/blog/kubernetes-vs-docker-swarm/)

    > **Benefits & drawbacks of Kubernetes**
    > 
    > **_Benefits of Kubernetes:_**
    > 
    > -   Kubernetes is backed by the Cloud Native Computing Foundation (CNCF).
    > -   Kubernetes have an impressively huge community among container orchestration tools. Over 50,000 commits and 1200 contributors.
    > -   Kubernetes is an open source and modular tool that works with any OS.
    > -   Kubernetes provides easy service organization with pods
    > 
    > **_Drawbacks of Kubernetes_**
    > 
    > -   When doing it yourself, Kubernetes installation can be quite complex with steep learning curve. An option to solve this issue is to opt for a managed [Kubernetes-as-a-service](https://vexxhost.com/public-cloud/container-services/kubernetes/) such as ours.
    > -   In Kubernetes, it is required to have a separate set of tools for management, including kubectl CLI.
    > -   It is Incompatible with existing Docker CLI and Compose tools
    > 
    > **Benefits & drawbacks of Docker Swarm**
    > 
    > **_Benefits of Docker Swarm_**
    > 
    > -   Docker Swarm is easy to install with a fast setup
    > -   Docker Swarm is a lightweight installation. It is simpler to deploy and Swarm mode is included in the Docker engine.
    > -   Docker Swarm has an easier learning curve.
    > -   Docker Swarm smoothly integrates with Docker Compose and Docker CLI. That’s because these are native Docker tools. Most of the Docker CLI commands will work with Swarm.
    > 
    > **_Drawbacks of Docker Swarm_**
    > 
    > -   Docker Swarm provides limited functionality.
    > -   Docker Swarm has limited fault tolerance.
    > -   Docker Swarm have smaller community and project as compared to Kubernetes community
    > -   In Docker Swarm, services can be scaled manually.
    > 

    > Docker Swarm is preferred in environments where simplicity and fast development is favored. Whereas Kubernetes is suitable for environments where medium to large clusters are running complex applications.

- [巅峰对决之Swarm、Kubernetes、Mesos - DockOne.io](http://dockone.io/article/1138)

    > ### Apache Mesos & Mesosphere Marathon
    > 
    > Mesos的目的就是建立一个高效可扩展的系统，并且这个系统能够支持很多各种各样的框架，不管是现在的还是未来的框架，它都能支持。这也是现今一个比较大的问题：类似Hadoop和MPI这些框架都是独立开的，这导致想要在框架之间做一些细粒度的分享是不可能的。\[35\]  
    >   
    > 因此Mesos的提出就是为了在底部添加一个轻量的资源共享层（resource-sharing layer），这个层使得各个框架能够适用一个统一的接口来访问集群资源。Mesos并不负责调度而是负责委派授权，毕竟很多框架都已经实现了复杂的调度。  
    >   
    > 取决于用户想要在集群上运行的作业类型，共有四种类型的框架可供使用\[52\]。其中有一些支持原生的Docker，比如说Marathon\[39\]。Docker容器的支持自从Mesos 0.20.0就已经被加入到Mesos中了\[51\]。  
    >   
    > 我们接下来将会重点关注如何在让Mesos和Marathon一起工作，毕竟Marathon主要是由Mesosphere维护\[41\]，并且提供了很多关于调度的功能，比如说约束（constraints）\[38\]，健康检查（health checks）\[40\]，服务发现（service discovery）和负载均衡（load balancing）\[42\]。  
    > 
    > [![04.png](http://dockone.io/uploads/article/20160320/bba30f8f454ec423e10e10d080c5d581.png "04.png")](http://dockone.io/uploads/article/20160320/bba30f8f454ec423e10e10d080c5d581.png)
    > 
    >   
    > Apache Mesos architecture using Marathon, © Adrian Mouat \[49\]  
    >   
    > 我们可以从图上看到，集群中一共出现了4个模块。ZooKeeper帮助Marathon查找Mesos master的地址\[53\]，同时它具有多个实例可用，以此应付故障的发生。Marathon负责启动，监控，扩展容器。Mesos maser则给节点分配任务，同时如果某一个节点有空闲的CPU/RAM，它就会通知Marathon。Mesos slave运行容器，并且报告当前可用的资源。  
    > 
    > #### 约束（Constraints）
    > 
    > 约束使得操作人员能够操控应用在哪些节点上运行，它主要由三个部分组成：一个字段名（field name）（可以是slavve的hostname或者任何Mesos slave属性），一个操作符和一个可选的值。5个操作符如下：  
    >   
    > 操作符：角色（role）  
    > 
    > -   UNIQUE：使得属性唯一，比如说越苏\[“hostname”,”UNIQUE”\]使得每个host上只有一个应用在运行。
    > -   CLUSTER：使得运行应用的slaves必须共享同一个特定属性。比如说约束 \[“rack id”, “CLUSTER”, “rack-1”\] 强制应用必须运行在rack-1上，或者处于挂起状态知道rack-1有了空余的CPU/RAM。
    > -   GROUP_BY：根据某个特性的属性，将应用平均分配到节点上，比如说特定的host或者rack。
    > -   LIKE：使得应用只运行在拥有特定属性的slaves上。尽管只有CLUSTER可用，但由于参数是一个正则表达式，因此很多的值都能够被匹配到。
    > -   UNLIKE：和LIKE相反。
    > 
    >   
    > 
    > #### 健康检查（Health checks）
    > 
    > 健康检查是应用依赖的，需要被手动实现。这是因为只有开发者知道他们自己的应用如何判断健康状态。（这是一个Swarm和Mesos之间的不同点）  
    >   
    > Mesos提供了很多选项来声明每个健康检查之间需要等待多少秒，或者多少次连续的健康检查失败后，这个不健康的任务需要被终结。  
    > 
    > #### 服务发现和负载均衡（Service discovery and load balancing）
    > 
    > 为了能够发送数据到正在运行的应用，我们需要服务发现。Apache Mesos提供了基于DNS的服务发现，称之为Mesos-DNS\[44\]，它能够在多个框架（不仅仅是Marathon）组成的集群中很好的工作。  
    >   
    > 如果一个集群只由运行容器的节点组成，Marathon足以承当起管理的任务。在这种情况下，主机可以运行一个TCP的代理，将静态服务端口的连接转发到独立的应用实例上。Marathon确保所有动态分配的服务端口都是唯一的，这种方式比手动来做好的多，毕竟多个拥有同样镜像的容器需要同一个端口，而这些容器可以运行在同一个主机上。  
    >   
    > Marathon提供了两个TCP/HTTP代理。一个简单的shell脚本\[37\]还有一个更复杂的脚本，称之为marathon-ld，它拥有更多的功能\[43\]。
    > 

- [Container Wars: Kubernetes vs. Docker Swarm vs. Amazon ECS | Caylent](https://caylent.com/containers-kubernetes-docker-swarm-amazon-ecs/)

    > Elastic Container Service (Amazon ECS)
    > --------------------------------------
    > 
    > AWS’s own container management service, [Amazon ECS](https://aws.amazon.com/ecs/) is a Docker-compatible service which allows you to run containerized applications on EC2 instances and is an alternative to both Kube and Swarm.
    > 
    > While Docker has won everyone over with its simplicity, Amazon ECS is a comparatively complex tool as you have to learn a whole new platform. Components within ECS consist of:
    > 
    > -   **ECS clusters:** Groups of EC2 instances which run tasks.
    > -   **Task Definition:** A text file, in JSON format, which includes much the same information as a ‘docker run’ command. Plus, details including which containers should run on on one host.
    > -   **Service:** Your tool for running and maintaining specified numbers of task definition instances across your cluster.
    > -   **Service Scheduler:** Keeps watch over running tasks and makes sure that the correct number is up. Plus, the feature reschedules tasks if they have failed.
    > -   **Container Agents:** This feature allows you to connect your cluster instances to your container.
    > 
    > Amazon ECS provides maximum value for those looking for seamless integration between containers and other AWS services. It’s a fully managed service which offers high availability, scalability, and security. On top of that, your AWS support plan includes it as standard.
    > 
    > Plus, if you are already on AWS, there is no need to install any extra software to operate your cluster.
    > 

- [Docker vs. Kubernetes vs. Apache Mesos: Why What You Think You Know is Probably Wrong - Mesosphere](https://mesosphere.com/blog/docker-vs-kubernetes-vs-apache-mesos/?utm_source=twitter&utm_medium=organic)

    > Let’s start with Docker…
    > ------------------------
    > 
    > Docker Inc., today started as a Platform-as-a-Service startup named dotCloud. The dotCloud team found that managing dependencies and binaries across many applications and customers required significant effort. So they combined some of the capabilities of Linux [cgroups](https://en.wikipedia.org/wiki/Cgroups) and namespaces into a single and easy to use package so that applications can consistently run on any infrastructure. This package is [the Docker image](https://docs.docker.com/engine/docker-overview/), which provides the following capabilities:
    > 
    > -   **Packages the application and the libraries in a single package** (the Docker Image), so applications can consistently be deployed across many environments;
    > -   **Provides Git-like semantics**, such as “docker push”, “docker commit” to make it easy for application developers to quickly adopt the new technology and incorporate it in their existing workflows;
    > -   **Define Docker images as immutable layers**, enabling immutable infrastructure. Committed changes are stored as an individual read-only layers, making it easy to re-use images and track changes. Layers also save disk space and network traffic by only transporting the updates instead of entire images;
    > -   **Run Docker containers by instantiating the immutable image** with a writable layer that can temporarily store runtime changes, making it easy to deploy and scale multiple instances of the applications quickly.
    > ![](https://mesosphere.com/wp-content/uploads/2017/07/docker-host.png)
    > 
    > Enter Kubernetes
    > ----------------
    > 
    > Google recognized the potential of the Docker image early on and sought to deliver container orchestration “as-a-service” on the Google Cloud Platform. Google had tremendous experience with containers (they introduced cgroups in Linux) but existing internal container and distributed computing tools like Borg were directly coupled to their infrastructure. So, instead of using any code from their existing systems, Google designed Kubernetes from scratch to orchestrate Docker containers. Kubernetes was released in February 2015 with the following goals and considerations:
    > 
    > -   **Empower application developers** with a powerful tool for Docker container orchestration without having to interact with the underlying infrastructure;
    > -   **Provide standard deployment interface** and primitives for a consistent app deployment experience and APIs across clouds;
    > -   **Build on a Modular API core** that allows vendors to integrate systems around the core Kubernetes technology.
    > 
    > ![](https://mesosphere.com/wp-content/uploads/2017/07/kubernetes-architecture.png)
    > 
    > 
    > 
    > Apache Mesos
    > ------------
    > 
    > Apache Mesos started as a UC Berkeley project to create a next-generation cluster manager, and apply the lessons learned from cloud-scale, distributed computing infrastructures such as [Google’s Borg](https://research.google.com/pubs/pub43438.html) and [Facebook’s Tupperware](https://www.youtube.com/watch?v=C_WuUgTqgOc). While Borg and Tupperware had a monolithic architecture and were closed-source proprietary technologies tied to physical infrastructure, Mesos introduced a modular architecture, an open source development approach, and was designed to be completely independent from the underlying infrastructure. Mesos was quickly adopted by [Twitter](https://youtu.be/F1-UEIG7u5g), [Apple(Siri)](http://www.businessinsider.com/apple-siri-uses-apache-mesos-2015-8), [Yelp](https://engineeringblog.yelp.com/2015/11/introducing-paasta-an-open-platform-as-a-service.html), [Uber](http://highscalability.com/blog/2016/9/28/how-uber-manages-a-million-writes-per-second-using-mesos-and.html), [Netflix](https://medium.com/netflix-techblog/distributed-resource-scheduling-with-apache-mesos-32bd9eb4ca38), and many leading technology companies to support everything from microservices, big data and real time analytics, to elastic scaling.
    > 
    > As a cluster manager, Mesos was architected to solve for a very different set of challenges:
    > 
    > -   **Abstract data center resources** into a single pool to simplify resource allocation while providing a consistent application and operational experience across private or public clouds;
    > -   **Colocate diverse workloads** on the same infrastructure such analytics, stateless microservices, distributed data services and traditional apps to improve utilization and reduce cost and footprint;
    > -   **Automate day-two operations** for application-specific tasks such as deployment, self healing, scaling, and upgrades; providing a highly available fault tolerant infrastructure;
    > -   **Provide evergreen extensibility** to run new application and technologies without modifying the cluster manager or any of the existing applications built on top of it;
    > -   **Elastically scale** the application and the underlying infrastructure from a handful, to tens, to tens of thousands of nodes.
    > 
    > ![](https://mesosphere.com/wp-content/uploads/2017/07/mesos-two-level-scheduler.png)
    > 




## Docker swarm

- [twtrubiks/docker-swarm-tutorial: Docker Swarm 基本教學 - 從無到有 Docker-Swarm-Beginners-Guide📝](https://github.com/twtrubiks/docker-swarm-tutorial)

## Mesos

- [Mesosphere釋出開源資料中心作業系統DC/OS，誓言讓資料中心管理像使用個人電腦 | iThome](https://www.ithome.com.tw/news/105437)

- [用30天來建構和操作Apache Mesos 系列文章列表 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/users/20103456/ironman/1063)

- [mesos 原理与架构 · Docker —— 从入门到实践](https://yeasy.gitbooks.io/docker_practice/content/mesos/architecture.html)

    > ### 架构
    > 
    > 下面这张基本架构图来自 Mesos 官方。
    > 
    > ![mesos 的基本架构](https://yeasy.gitbooks.io/docker_practice/content/mesos/_images/mesos-architecture.png)
    > 
    > 图 1.22.3.1 - mesos 的基本架构
    > 
    > 可以看出，Mesos 采用了经典的主-从（master-slave）架构，其中主节点（管理节点）可以使用 zookeeper 来做 HA。
    > 
    > Mesos master 服务将运行在主节点上，Mesos slave 服务则需要运行在各个计算任务节点上。
    > 
    > 负责完成具体任务的应用框架们，跟 Mesos master 进行交互，来申请资源。
    > 
    > ### 基本单元
    > 
    > Mesos 中有三个基本的组件：管理服务（master）、任务服务（slave）以及应用框架（framework）。
    > 
    > #### 管理服务 \- master
    > 
    > 跟大部分分布式系统中类似，主节点起到管理作用，将看到全局的信息，负责不同应用框架之间的资源调度和逻辑控制。应用框架需要注册到管理服务上才能被使用。
    > 
    > 用户和应用需要通过主节点提供的 API 来获取集群状态和操作集群资源。
    > 
    > #### 任务服务 \- slave
    > 
    > 负责汇报本从节点上的资源状态（空闲资源、运行状态等等）给主节点，并负责隔离本地资源来执行主节点分配的具体任务。
    > 
    > 隔离机制目前包括各种容器机制，包括 LXC、Docker 等。
    > 
    > #### 应用框架 \- framework
    > 
    > 应用框架是实际干活的，包括两个主要组件：
    > 
    > -   调度器（scheduler）：注册到主节点，等待分配资源；
    > -   执行器（executor）：在从节点上执行框架指定的任务（框架也可以使用 Mesos 自带的执行器，包括 shell 脚本执行器和 Docker 执行器）。
    > 
    > 应用框架可以分两种：一种是对资源的需求是会扩展的（比如 Hadoop、Spark 等），申请后还可能调整；一种是对资源需求大小是固定的（MPI 等），一次申请即可。
    > 

- [Apache Mesos: The True OS For The Software Defined Data Center? – Cloud Architect Musings](https://cloudarchitectmusings.com/2015/03/23/apache-mesos-the-true-os-for-the-software-defined-data-center/)

- [DCOS到底是啥？看完这篇你就懂了~ - 51CTO.COM](http://cloud.51cto.com/art/201603/506805.htm)

    > 下面介绍三种基于Mesos衍生的生态系统： Mesosphere DCOS 从Mesosphere官网了解到，Mesosphere DCOS是以 Mesos为“核心”，与其周边服务及功能组件所组成的一个生态系统。它跨越数据中心或云环境中的所有主机，将所有主机的资源放入一个资源池，使所有主机的行为整体上像一个大计算机。 Mesosphere DCOS内部架构图
    > 
    > ![](http://s5.51cto.com/wyfs02/M00/7C/CD/wKiom1bYCDzxFp3EAACDVAFWONA866.jpg)
    > 
    > 由图可见，Mesosphere DCOS除了内核Mesos，还有两个关键组件Marathon和Chronos。其中，Marathon(名分布式的init)是一个用于启动长时间运行应用程序和服务的框架，Chronos(又名分布式的cron)是一个在Mesos上运行和管理计划任务的框架。此外，Mesosphere DCOS还有Mesos-DNS这样的插件模块，它类似一个CLI，一个GUI又或者是提供你想运行的所有的包的仓库等工具。 Mesosphere DCOS 可以运行在任意的现代Linux环境，公有或私有云，虚拟机甚至是裸机环境，当前支持的平台有亚马逊AWS，谷歌GCE，微软Azure，Openstack等等。据Mesosphere官网显示，Mesosphere DCOS在其公有仓库上已提供了40多种服务组件，比如Hadoop，Spark，Cassandra, Jenkins, Kafka, MemSQL等等。 浙江移动与天玑联合研发的DCOS 下图为该DCOS内部架构示意
    > 
    > ![](http://s3.51cto.com/wyfs02/M00/7C/CC/wKioL1bYCLbAFMh4AAB6tbAFsOs988.jpg)
    > 
    > 由图可见，“核心”Mesos负责集群中所有节点资源的动态调度与管理。其上还包括DCOS管控平台，容器应用框架等重要功能组件。该运营商表示，上述DCOS平台不仅具备灵活弹性的伸缩能力，为系统提供高效的平行扩展来应对突发的业务高峰，而且Mesos与Docker的结合极大简化业务运维复杂度，实现自动化部署与应用程序升级，Mesos还可为资源管理提供高容错性，自动辨别服务器、机架或网络出现的故障等。
    > 

- [談談Apache Mesos和Mesosphere DCOS：歷史、架構、發展和應用 - 壹讀](https://read01.com/xA44K.html)

    > Mesos 的設計宗旨在於嘗試和提高集群的利用效率和性能，他們認為對於數據中心資源的單純靜態劃分和使用的這樣一個方式是值得重新考量的，舉個例子來說：  
    >   
    > 我們假設你的數據中心裡擁有9個主機：
    > 
    > ![](https://i1.read01.com/SIG=2hrde6o/3041705658323030.jpg)
    > 
    > 如果把它靜態的劃分開來，並且指定每三個主機承載一個應用，這樣一來總共是3個應用（這裡是Hadoop、Spark 和 Ruby on Rails）。
    > 
    > ![](https://i2.read01.com/SIG=2tar2cp/3041705658323031.jpg)
    > 
    > 顯而易見的一個問題是這些主機的資源利用率並不會很高；
    > 
    > ![](https://i3.read01.com/SIG=28o1miq/3041705658323032.jpg)
    > 
    > 因此如果你想使用全部的資源，即這裡例子中的全部9台主機，那麼就需要將其抽象成一個共享資源池，而你可以按需計劃配置，這樣的話，利用率自然可以得到相應的提升；
    > 
    > ![](https://i1.read01.com/SIG=249nqor/3041705658323033.jpg)
    > 
    > Mesos團隊的第二個觀點在於他們覺得需要為分布式系統量身定製一套新的系統，換句話說，他們覺得MapReduce並不是適用於所有的場景（這也導致了Spark的誕生，而它又是另外一個故事了），而我們需要一個新的更簡單和更具有通用性的專為分布式系統提供服務的這樣一個框架。
    > 
    > #### Mesos 框架（分布式系統）到底是什麼?
    > 
    > 一般來說，一個分布式系統你需要有一個Coordinator（調度器）和 多個Worker（執行任務）。調度器以同步（分布式）的方式運行進程/任務，處理程序錯誤（容錯），並且負責優化性能（即彈性伸縮）。換句話說，它負責協調在數據中心去實際執行你想要運行的代碼（不需要是一個完整的程序，它也可以是某些種類的運算）。正如之前所提到的那樣，Mesos將其稱之為聯合調度。
    > 
    > ![](https://i2.read01.com/SIG=33tkves/3041705658323034.jpg)
    > 
    > 或者也可以這麼說，Mesos是一個帶有調度器的分布式系統。
    > 
    > ![](https://i3.read01.com/SIG=3fc2j4t/3041705658323035.jpg)
    > 
    > 那麼Mesos的真正定位是什麼呢? 當你嘗試去執行它的任務時你可以理解為它實際上就是機器和調度器之間的一層抽象。  
    >   
    > 因此在Mesos里，調度器是和Mesos層（通過API等）通信，而不是直接跟物理機器打交道。Mesos這裡通過這樣的方式嘗試解決的即是資源的靜態劃分問題，這意味著你不再需要針對每個特定的運行時分配一個對應的調度器去決定實際去執行它的workers，而取而代之的是，你有一個調度器去和Mesos通信，而它會反過來依據整個資源池的剩餘資源做調度。
    > 
    > ![](https://i1.read01.com/SIG=3quo7qu/3041705658323036.jpg)
    > 
    > 這樣做帶來的最顯而易見的好處就是你可以在一批機器上運行多個不同的分布式系統並且更有效的（不再是靜態劃分）動態劃分和共享這些資源。
    > 
    > ![](https://i2.read01.com/SIG=3mfebgv/3041705658323037.jpg)
    > 
    > 其次，之所以這樣抽象設計的另外一個重要原因在於它能夠提供一個通用功能集（故障檢測、分布式任務、任務啟動、任務監控、結束任務、清理任務等），這樣一來就無需每個分布式系統都各自重複的去實現這樣一套邏輯。
    > 
    > #### Mesos 適合作為數據中心的哪一層的抽象?
    > 
    > Mesos 這一層抽象實現的目的即是想要嘗試通過使用並更好的調度資源使得運行在其之上的這些框架變得更加易於構建和運行。
    > 
    > ![](https://i3.read01.com/SIG=1lmucmg/3041705658323038.jpg)
    > 
    > IaaS的抽象的是機器，例如你給它指定一個數字，它便會生成一堆的機器而這也可以看作是Mesos概念模型更底層化的一個抽象。PaaS則考慮的更多是部署和管理應用/服務，它並不關心底層的那些基礎架構，而你可以把它看作是Mesos概念模型的一個更高層面的抽象。在交互方面，PaaS可能是和開發者直接交互，而Mesos則是以API的形式和軟體程序交互。  
    >   
    > 換句話說，你可以基於Mesos之上構建一個Paas系統（例如像Marathon - 它好像任何地方都比一個真正的Paas系統更像PaaS），同時你可以在一個IaaS上運行Mesos（例如OpenStack）。  
    >   
    > 如果你將你的Mesos運行在一個組合系統（例如就像Openstack + 物理硬體 + 虛擬機）之上，那麼你可以很直觀的再次體會到動態劃分資源的好處，那便是你能夠跨越這些底層組件而直接的去管理和計劃你的工作負載，某種意義上來說，你可以認為Mesos類似於是一個數據中心的內核，即它負責將物理機器抽象成資源，從而使得你能夠忽略底層組件的存在，通過消費Mesos的抽象資源來構建分布式系統。  
    >   
    > 因此我們可以說，Apache Mesos是為構建和運行其它分布式系統（例如像Spark）提供服務的分布式系統。
    > 
    > #### Mesos架構內幕
    > 
    > 在 Mesos 里，一個框架程序（或者說分布式系統）發起的一次請求會在被接收到的那個時刻由調度器承接和分配。這跟傳統分布式系統一般人為發起請求的方式不太一樣（再強調一下，Mesos將會讓框架程序發起請求，而不是人工操作），傳統的方式即需要在人為發起請求時設定好需要分配的特定資源，然後再去真正請求和獲取這些資源，這類情況中最典型的莫過於需求場景的變換（設想在Map/Reduce的場景下，比如在Map和Reduce階段切換之際產生的一個需求資源的變化）
    > 
    > ![](https://i1.read01.com/SIG=1p780sh/3041705658323039.jpg)
    > 
    > 與傳統分布式系統不一樣的是，Mesos 將會立馬為其分配所能分配的最大資源，而不是傻傻的在那等到滿足該請求的資源完成/完全到位（在這裡它想要實現的便是在絕大多數情況下十分奏效的無阻塞式資源分配策略，即你無須立馬消費預期請求的全量資源的這樣的情景）。  
    >   
    > 當然，現在框架類應用（分布式系統）也可以使用Mesos提供的資源完成他們自己的調度，這便是所謂的 「二次資源調度」。
    > 
    > ![](https://i3.read01.com/SIG=2vu57os/3041705658323041.jpg)
    > 
    > 最終達到的效果即是你下發的一個任務可以在整個數據中心的任意一個地方提交並且運行。  
    >   
    > 構建這樣的「二次資源調度」系統的原因在於它可以在同一時間內支持多個分布式系統。同樣以上面的例子來解釋，Mesos為Spark提供和分配所需的資源。而這裡，Spark則負責決策和分配這些可用資源去運行實際任務（即因為可用的資源得以滿足需求，所以我才能夠實際去運行這些map任務）。
    > 
    > ![](https://i1.read01.com/SIG=2acvj6v/3041705658323042.jpg)
    > 
    > 所以一旦一個任務被框架應用提交到Mesos，那麼這些任務就必須被實際執行。Mesos master 負責指派任務給每個slave，而每個slave通過上面跑著的agent來管理和運行這些任務。（這即是說如果這個任務是對應的一個命令，那麼它會去執行它，如果它需要一些特定的資源來完成這個任務，比如像jar包，那麼它會先獲取所需的資源，然後在一個沙盒裡執行它，最後才發起這個任務）  
    >   
    > 或者說你也可以這樣，框架應用可以通過一個執行器（框架應用需要一個中間層，這個中間層可以用來多線程執行任務）來靈活的決定它想要執行的任務。
    > 
    > ![](https://i2.read01.com/SIG=26t9vcu/3041705658323043.jpg)
    > 
    > 為了保證資源的相對隔離性，Mesos 對 Kernel的cgroups和namespaces 提供了內置的原生支持，當然你也可以將一個Docker容器當做一個任務去運行。這樣一來，它便給你提供了一個多租戶的（框架）資源池的訪問機制（跨主機和主機內部的進程間通信）。  
    >   
    > 你可以預請求你所需的資源，當然這樣你也就回到了資源固定劃分的時代。如果你有一些有狀態的應用，那麼你需要預定一些資源（這類任務通常需要在同一台主機上運行）並且需要一些持久化的存儲卷（數據需要能夠支持故障遷移和恢復），而這類需求Mesos同樣能夠支持。DCOS（數據中心作業系統）即是Mesos的「核心」與其周邊的服務及功能組件所組成的一個生態系統。例如像mesos-dns這樣的插件模塊，類似一個CLI，一個GUI又或者是提供你想運行的所有的包的倉庫等工具，以及像Marathon（又名分布式的init）、Chronos（又名分布式的cron）這樣的框架等等。  
    > 
    > 

### Install Mesos

- [安装与使用 · Docker —— 从入门到实践](https://yeasy.gitbooks.io/docker_practice/content/mesos/installation.html#)

- [通过Docker来部署Mesos集群 - DockOne.io](http://dockone.io/article/136)

    > 通过Docker来部署Mesos集群
    > ==================
    > 
    > 【编者的话】Apache Mesos系统是一套资源管理调度集群系统，可以用来管理Docker集群，换个思路，本文介绍了如何通过Docker容器来部署一个单节点和多节点的Mesos集群，整个过程非常简单，只需要七个命令即可完成，整个步骤作者也记录到了GitHub，推荐学习。  
    >   
    > 这篇文章将教你如何使用Docker容器部署一个单节点的[Mesos](http://mesosphere.com/)集群，整个部署过程非常简单，只需要七个命令。在部署之前你需要准备一个装有Docker的环境，这个非常简单，我不赘述。我们总共需要启动四个容器，分别是：  
    > 
    > -   ZooKeeper
    > -   Meso Master
    > -   Marathon
    > -   Mesos Slave Container
    > 
    >   
    > 如上面提到的，我们只需要一个可以运行的Docker Server，你可以通过任何你喜欢的方式来获得Docker，比如在[本地的Vagrant中安装Docker](https://docs.vagrantup.com/v2/provisioning/docker.html)、使用[Boot2Docker](http://boot2docker.io/)、使用[CoreOS](https://coreos.com/)或者在AWS安装。整个的部署过程我都放到了[GitHub](https://github.com/sekka1/mesosphere-docker)上了，包括所有的容器构建的Dockerfile文件， 你可以本地去构建这些镜像， 或者从Docker Hub上下载已经构建好的镜像。我们所使用的是Docker Hub上的镜像是：  
    > 
    > -   [ZooKeeper](https://registry.hub.docker.com/u/garland/zookeeper/)
    > -   [Meso Master](https://registry.hub.docker.com/u/garland/mesosphere-docker-mesos-master/)
    > -   [Marathon](https://registry.hub.docker.com/u/garland/mesosphere-docker-marathon/)
    > 
    >   
    > 
    > #### 部署步骤
    > 
    > **第一步：**获取Docker Server的IP，并赋值到HOST_IP变量中，在接下来的步骤中我们还会用到。  
    > 
    > root@docker-server:/# HOST_IP=10.11.31.7
    > 
    >   
    > **第二步：**启动ZooKeeper容器。  
    > 
    > docker run -d \
    > -p 2181:2181 \
    > -p 2888:2888 \
    > -p 3888:3888 \
    > garland/zookeeper
    > 
    >   
    > **第三步：** 启动Mesos Master。  
    > 
    > docker run --net="host" \
    > -p 5050:5050 \
    > -e "MESOS\_HOSTNAME=${HOST\_IP}" \
    > -e "MESOS\_IP=${HOST\_IP}" \
    > -e "MESOS\_ZK=zk://${HOST\_IP}:2181/mesos" \
    > -e "MESOS_PORT=5050" \
    > -e "MESOS\_LOG\_DIR=/var/log/mesos" \
    > -e "MESOS_QUORUM=1" \
    > -e "MESOS\_REGISTRY=in\_memory" \
    > -e "MESOS\_WORK\_DIR=/var/lib/mesos" \
    > -d \
    > garland/mesosphere-docker-mesos-master
    > 
    >   
    > **第四步：** 启动Marathon。  
    > 
    > docker run -d \
    > -p 8080:8080 \
    > garland/mesosphere-docker-marathon --master zk://${HOST_IP}:2181/mesos \
    > --zk zk://${HOST_IP}:2181/marathon
    > 
    >   
    > **第五步：** 启动Mesos Slave。  
    > 
    > docker run -d \
    > --name mesos\_slave\_1 \
    > --entrypoint="mesos-slave" \
    > -e "MESOS\_MASTER=zk://${HOST\_IP}:2181/mesos" \
    > -e "MESOS\_LOG\_DIR=/var/log/mesos" \
    > -e "MESOS\_LOGGING\_LEVEL=INFO" \
    > garland/mesosphere-docker-mesos-master:latest
    > 
    >   
    > **第六步：** 访问 Mesos 页面。  
    > Mesos Web 页面地址是：  
    > 
    > http://${HOST_IP}:5050
    > 
    >   
    > 
    > [![mesos.png](http://dockone.io/uploads/article/20150112/8b66e0df677cdaea0990511ebbf940eb.png)](http://dockone.io/uploads/article/20150112/8b66e0df677cdaea0990511ebbf940eb.png)
    > 
    >   
    > **第七步：** 通过Marathon的Web页面启动一个Job。Marathon Web页面地址是：http://${HOST_IP}:8080。  
    >   
    > Marathon 可以让你部署长期运行的Job到Mesos Slave容器上， 这个可以帮助你去检查你的集群是否启动，并且处于running的状态， 打开上面的地址后你会看到下面的页面：  
    > 
    > [![marathon1.png](http://dockone.io/uploads/article/20150112/96a351240ed6bdddc7570710e65c8025.png)](http://dockone.io/uploads/article/20150112/96a351240ed6bdddc7570710e65c8025.png)
    > 
    >   
    > 点击右上角的“New App”按钮，创建一个新的Job/Task， 我们这里只是输出一个”hello“到文件"/tmp/output.txt"里面，然后我们可以到容器中查看文件是否创建，并检查下这个Job是不是一直在运行。  
    > 
    > [![marathon2.png](http://dockone.io/uploads/article/20150112/4fbac4e14542397efd8a12018e7e90af.png "marathon2.png")](http://dockone.io/uploads/article/20150112/4fbac4e14542397efd8a12018e7e90af.png)
    > 
    >   
    > **第八步：** 检查Job/Task是不是在运行  
    > 接下来让我们检查下Job/Task是不是一直在Mesos Slave上面运行。  
    > 在Docker Server上运行下面的命令， 这个命令会让你进到Mesos Slave 容器中，然后再使用`tail`命令查看/tmp/output.txt文件里面的内容。  
    > 
    > docker exec -it mesos\_slave\_1 /bin/bash
    > root@ca83bf0ea76a:/# tail -f /tmp/output.txt
    > 
    >   
    > 你会看到每隔一秒钟“hello”就会被追加到这个文件中。  
    >   
    > 注意：多节点的Mesos环境部署步骤请参考[这里](https://github.com/sekka1/mesosphere-docker#multi-node-setup)。  
    >   
    > **原文链接：[Deploy a Mesos Cluster with 7 Commands Using Docker](https://medium.com/@gargar454/deploy-a-mesos-cluster-with-7-commands-using-docker-57951e020586)（翻译：左伟 校对：李颖杰）**
    > 



### Using Mesos with nvidia-docker for GPU cluster
    
- [Apache Mesos - Nvidia GPU Support](https://mesos.apache.org/documentation/latest/gpu-support/)

    > Overview
    > --------
    > 
    > Mesos exposes GPUs as a simple `SCALAR` resource in the same way it always has for CPUs, memory, and disk. That is, a resource offer such as the following is now possible:
    > 
    > ```
    > cpus:8; mem:1024; disk:65536; gpus:4;
    > 
    > ```
    > 
    > However, unlike CPUs, memory, and disk, _only_ whole numbers of GPUs can be selected. If a fractional amount is selected, launching the task will result in a `TASK_ERROR`.
    > 

    > Agent Flags
    > -------------------------------------------------------------------------------------
    > 
    > The following isolation flags are required to enable Nvidia GPU support on an agent.
    > 
    > ```
    > --isolation="filesystem/linux,cgroups/devices,gpu/nvidia"
    > 
    > ```
    > 
    > The `filesystem/linux` flag tells the agent to use Linux-specific commands to prepare the root filesystem and volumes (e.g., persistent volumes) for containers that require them.
    > 
    > The `cgroups/devices` flag tells the agent to restrict access to a specific set of devices for each task that it launches (i.e., a subset of all devices listed in `/dev`). When used in conjunction with the `gpu/nvidia` flag, the `cgroups/devices` flag allows us to grant / revoke access to specific GPUs on a per-task basis.
    > 



    > if you want to exclude a specific GPU device because an unwanted Nvidia graphics card is listed alongside a more powerful set of GPUs. When this is required, the following additional agent flags can be used to accomplish this:
    > 
    > ```
    > --nvidia_gpu_devices="<list_of_gpu_ids>"
    > 
    > --resources="gpus:<num_gpus>"
    > 
    > ```
    > 
    > For the `--nvidia_gpu_devices` flag, you need to provide a comma separated list of GPUs, as determined by running `nvidia-smi` on the host where the agent is to be launched ([see below](https://mesos.apache.org/documentation/latest/gpu-support/#external-dependencies) for instructions on what external dependencies must be installed on these hosts to run this command). Example output from running `nvidia-smi` on a machine with four GPUs can be seen below:
    > 
    > ```
    > +------------------------------------------------------+
    > | NVIDIA-SMI 352.79     Driver Version: 352.79         |
    > |-------------------------------+----------------------+----------------------+
    > | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
    > | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
    > |===============================+======================+======================|
    > |   0  Tesla M60           Off  | 0000:04:00.0     Off |                    0 |
    > | N/A   34C    P0    39W / 150W |     34MiB /  7679MiB |      0%      Default |
    > +-------------------------------+----------------------+----------------------+
    > |   1  Tesla M60           Off  | 0000:05:00.0     Off |                    0 |
    > | N/A   35C    P0    39W / 150W |     34MiB /  7679MiB |      0%      Default |
    > +-------------------------------+----------------------+----------------------+
    > |   2  Tesla M60           Off  | 0000:83:00.0     Off |                    0 |
    > | N/A   38C    P0    40W / 150W |     34MiB /  7679MiB |      0%      Default |
    > +-------------------------------+----------------------+----------------------+
    > |   3  Tesla M60           Off  | 0000:84:00.0     Off |                    0 |
    > | N/A   34C    P0    39W / 150W |     34MiB /  7679MiB |     97%      Default |
    > +-------------------------------+----------------------+----------------------+
    > 
    > ```
    > 
    > The GPU `id` to choose can be seen in the far left of each row. Any subset of these `ids` can be listed in the `--nvidia_gpu_devices` flag (i.e., all of the following values of this flag are valid):
    > 
    > ```
    > --nvidia_gpu_devices="0"
    > --nvidia_gpu_devices="0,1"
    > --nvidia_gpu_devices="0,1,2"
    > --nvidia_gpu_devices="0,1,2,3"
    > --nvidia_gpu_devices="0,2,3"
    > --nvidia_gpu_devices="3,1"
    > etc...
    > 
    > ```
    > 
    > For the `--resources=gpus:<num_gpus>` flag, the value passed to `<num_gpus>` must equal the number of GPUs listed in `--nvidia_gpu_devices`. If these numbers do not match, launching the agent will fail.
    > 


    > ### Minimal Setup With Support for Docker Containers[](https://mesos.apache.org/documentation/latest/gpu-support/#minimal-setup-with-support-for-docker-containers)
    > 
    > The commands below show a minimal example of bringing up a GPU-capable Mesos cluster on `localhost` and running a docker container on it. The required agent flags are set as described above, and the `mesos-execute` command has been told to enable the `GPU_RESOURCES` framework capability so it can receive offers containing GPU resources. Additionally, the required flags to enable support for docker containers (as described [here](https://mesos.apache.org/documentation/latest/container-image/)) have been set up as well.
    > 
    > ```
    > $ mesos-master \
    >       --ip=127.0.0.1 \
    >       --work_dir=/var/lib/mesos
    > 
    > $ mesos-agent \
    >       --master=127.0.0.1:5050 \
    >       --work_dir=/var/lib/mesos \
    >       --image_providers=docker \
    >       --executor_environment_variables="{}" \
    >       --isolation="docker/runtime,filesystem/linux,cgroups/devices,gpu/nvidia"
    > 
    > $ mesos-execute \
    >       --master=127.0.0.1:5050 \
    >       --name=gpu-test \
    >       --docker_image=nvidia/cuda \
    >       --command="nvidia-smi" \
    >       --framework_capabilities="GPU_RESOURCES" \
    >       --resources="gpus:1"
    > 
    > ```
    > 
    > If all goes well, you should see something like the following in the `stdout` out of your task.
    > 
    > ```
    > +------------------------------------------------------+
    > | NVIDIA-SMI 352.79     Driver Version: 352.79         |
    > |-------------------------------+----------------------+----------------------+
    > | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
    > | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
    > |===============================+======================+======================|
    > |   0  Tesla M60           Off  | 0000:04:00.0     Off |                    0 |
    > | N/A   34C    P0    39W / 150W |     34MiB /  7679MiB |      0%      Default |
    > +-------------------------------+----------------------+----------------------+
    > 
    > ```
    > 


- [基于 Mesos、Docker 和 Nvidia GPU 的深度学习平台实践-DockerInfo](http://www.dockerinfo.net/3697.html)

    > NVIDIA GPU 可以大大加快 Deep Learning 任务的运行速度；同时，GPU资源又是十分昂贵的，需要尽可能提高 GPU 资源的利用率。为了解决上述问题，我们利用 [Mesos](http://www.dockerinfo.net/docker/mesos "更多关于 Mesos 的文章") 将 GPU 资源汇聚成资源池来实现资源共享，并借用 Docker 交付深度学习的 runtime 环境，很好的解决了上述问题。
    > 
    > 平台架构
    > ----
    > 
    > 这里从节点内部和集群两层介绍平台的架构。
    > 
    > 在节点内部，我们利用nvidia-docker ( https://github.com/NVIDIA/nvidia-docker ) 来帮助容器内部的程序调用外面主机上的CUDA driver。如下图一所示，CUDA Driver 及GPU Driver安装在外部Host 上；CUDA Toolkit、其它深度学习组件及用户应用程序运行在Docker 容器中。这样既能快速配置环境，又保证了HOST不受用户应用程序污染。
    > 
    > ![20161115160457](http://img.dockerinfo.net/2016/11/20161115160457.jpg)
    > 
    > 
    > 在整个集群层面，利用Mesos将资源池化，用户可通过Marathon统一入口部署自己的深度学习Docker Package。如下图二所示，集群包括3个Mesos 管理（Master）节点和多个工作（slave）节点，任务分发到slave后，slave通过 executor 与 Docker daemon 通信，Docker daemon 按需从内部镜像仓库拉取并加载Docker image。对应到真实应用场景，带有深度学习依赖组件的 Docker image 将被pull&run，用户可以通过ssh或者jupyter的web入口与组件进行交互。
    > 
    > ![20161115160511](http://img.dockerinfo.net/2016/11/20161115160511.jpg)

- [klueska-mesosphere/mesos-gpu-docker](https://github.com/klueska-mesosphere/mesos-gpu-docker)
    
    > Clone this repo on an Nvidia GPU equipped machine with at least 2 GPUs (g2.8xlarge instances will do nicely).
    > 
    > Then run:
    > 
    > ```
    > ./build.sh
    > ./run.sh
    > ./deploy-tasks.sh
    > 
    > ```
    > 
    > This will launch 2 marathon applications. The first application runs `nvidia-smi` every 60 seconds without a docker container, and the second one runs `nvidia-smi` every 60 seconds inside an `nvidia/cuda` container.

- [Tutorial: Deep learning with TensorFlow, Nvidia and Apache Mesos (DC/OS), Part 1 - Mesosphere](https://mesosphere.com/blog/tutorial-deep-learning-with-tensorflow-nvidia-and-apache-mesos-dcos-part-1/)

    [Part 1: Deep Learning w/ TensorFlow, Nvidia & DC/OS (Apache Mesos) - YouTube](https://www.youtube.com/watch?v=hrXiqKGb7OQ&feature=youtu.be)

    > -   Tutorial #1: Run a Tensor flow Docker image on your laptop and run a machine learning model with and without GPUs.
    >     
    > -   Tutorial #2: Run a Tensoflow Docker image on a DC/OS cluster with and without GPUs. See GPU isolation and Jupyter in action.
    >     
    > -   Tutorial #3: Deploy a dynamic, distributed TensorFlow on DC/OS from the Universe. See how TensorFlow on DC/OS dynamically consumes and releases resources on the cluster when done. Run multiple TensorFlows on the same cluster with different resource requirements.


- [Docker on Mesos - Mesosphere](https://mesosphere.com/blog/docker-on-mesos/)

- [Tutorial: Deep learning with TensorFlow, Nvidia and Apache Mesos (DC/OS), Part 2 - Mesosphere](https://mesosphere.com/blog/tutorial-deep-learning-with-tensorflow-nvidia-and-apache-mesos-dcos-part-2/)

    [Part 2: Deep Learning w/ TensorFlow, Nvidia & DC/OS (Apache Mesos) - YouTube](https://www.youtube.com/watch?v=VzHVM0SCF44)
    
    > ### Run TensorFlow on DC/OS with GPUs
    > 
    > #### Deploy the TensorFlow service with GPUs
    > 
    > Now that you’ve got TensorFlow examples running on your cluster, let’s see how performance compares when you configure your service to use GPUs.
    > 
    > 1.  Go to the Services tab of the DC/OS UI.
    > 2.  Click **+** to add a service.
    > 3.  Choose **Single Container**.
    > 4.  Toggle to the **JSON Editor** and paste the following [application definition](https://docs.mesosphere.com/1.9/deploying-services/creating-services/) into the editor.
    >     
    >     {
    >       "id": "tensorflow-gpus-1",
    >       "acceptedResourceRoles": \["slave_public"\],
    >       "cpus": 4,
    >       "gpus": 4,
    >       "mem": 2048,
    >       "disk": 0,
    >       "instances": 1,
    >       "container": {
    >         "type": "MESOS",
    >         "docker": {
    >           "image": "tensorflow/tensorflow:latest-gpu"
    >         }
    >       }
    >     }
    >     
    >     This application definition is largely the same as the last one, except, here, you’re requesting 4 GPUs and specifying the TensorFlow Docker image that’s configured for GPUs.
    >     
    > 5.  Click **Review and Run**, then **Run Service**.
    > 
    > #### Verify access to GPUs
    > 
    > You’ll recall that we created a cluster with a public agent that has 8 GPUs, but only requested access to 4. Let’s verify that the node has 8 GPUs, and that our service has access to only 4 of them.
    > 
    > 1.  First, use `dcos task exec` to run a command inside of the container to get the public IP address of the agent node the container is running on.
    >     
    >     dcos task exec tensorflow-gpus-1 curl -s ifconfig.co
    >     
    > 2.  Now, use that public IP to SSH into the node and run `nvidia-smi` to verify the number of GPUs the node has.
    >     
    >     ssh <public-ip> nvida-smi
    >     
    >     You should see 8 GPUs installed and running on the machine. The container for your service, however, should only be able to see 4 of those GPUs.
    >     
    > 3.  Run `dcos task exec` with the `bash` option to get a shell inside of your service’s container.
    >     
    >     dcos task exec -it tensorflow-gpus-1 bash
    >     
    > 4.  Set up environment variables so you can run `nvida-smi` from within this shell.
    >     
    >     export LD\_LIBRARY\_PATH=/usr/local/nvidia/lib64 export PATH=$PATH:/usr/local/nvidia/bin
    >     
    > 5.  Run `nvidia-smi` to verify that even though you have 8 GPUs installed on the _machine_, you only have access to four of them inside this container.
    >     
    >     nvidia-smi
    >     
    > 
    > #### Run a TensorFlow example with GPUs
    > 
    > Now that you’ve installed TensorFlow and verified your access to 4 GPUs, let’s run the same example as before.
    > 
    > 1.  If you exited the `tensorflow-gpus-1` container, reenter it and set up the environment variables by following the steps in the last section.
    > 2.  Install git and clone the TensorFlow-Examples repository.
    >     
    >     apt-get update; apt-get install -y git git clone https://github.com/aymericdamien/TensorFlow-Examples
    >     
    > 3.  Run and time the same example you ran earlier, the convolutional network example.
    >     
    >     cd TensorFlow-Examples/examples/3\_NeuralNetworks time python convolutional\_network.py
    >     
    > 4.  Watch the code find the GPUs and execute.
    > 
    > This took my DC/OS cluster about 2 minutes: about 5 times faster than before!
    > 
    > #### Launch Two TensorFlow Instances
    > 
    > You’ll recall that we have a cluster with _8_ GPUs, but we only requested access to 4 of them. Now, let’s launch a second TensorFlow instance that will consume the remaining 4 GPUs in parallel with the first.
    > 
    > Running more than one TensorFlow instance in parallel shows that you can have multiple users on the same cluster with _isolated access_ to the GPUs on it.
    > 
    > 1.  Add a third service to your DC/OS cluster with the following application definition, which is similar to the first application definition with GPUs.
    >     
    >     {
    >       "id": "tensorflow-gpus-2",
    >       "acceptedResourceRoles": \["slave_public"\],
    >       "cpus": 4,
    >       "gpus": 4,
    >       "mem": 2048,
    >       "disk": 0,
    >       "instances": 1,
    >       "container": {
    >         "type": "MESOS",
    >         "docker": {
    >           "image": "tensorflow/tensorflow:latest-gpu"
    >         }
    >       }
    >     }
    >     
    > 2.  Verify that your second TensorFlow instance is running by accessing the Jupyter notebook that runs by default on the TensorFlow Docker image. In the application definition above, the `acceptedResourceRoles` parameter is set to `slave_public`, which gives us access to the public IP of the agents where the containers are running.
    >     1.  Get the public IP of the agent where the task has been launched.
    >         
    >         dcos task exec tensorflow-gpus-2 curl -s ifconfig.co
    >         
    >     2.  Go to the STDERR log of the service to get the Jupyter URL. **Services** \> **tensorflow-gpus-2** \> **task-id** \> **paper icon** \> **ERROR (STDERR)**. You will see this a message similar to the following.
    >         
    >          Copy/paste this URL into your browser when you connect for the first time, to login with a token: http://localhost:10144/?token=d4f3d8f80eb97299e74b5254d1600c480c3f042d548e51f5        
    >         
    >     3.  Replace `localhost` with the public IP you found earlier to see the Jupyter notebook.
    >     4.  Click the `Getting Started` notebook and run some commands.
    > 
    > Thanks for playing along at home!


- [douban/tfmesos: Tensorflow in Docker on Mesos #tfmesos #tensorflow #mesos](https://github.com/douban/tfmesos)


- [Training Your Custom Model with the DC/OS TensorFlow package - Mesosphere](https://mesosphere.com/blog/tensorflow-custom-model/)

- [Distributed TensorFlow with GPU Support on Mesosphere DC/OS](https://mesosphere.com/blog/tensorflow-gpu-support-deep-learning/)

    <iframe width="560" height="315" src="https://www.youtube.com/embed/vsyU9R3y7VA" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

    > ### Benefits of running Distributed TensorFlow on DC/OS
    > 
    > The new beta release of TensorFlow on DC/OS helps solve each of the problems outlined above and more. Specifically it helps to:
    > 
    > 1.  **Simplify the deployment of distributed TensorFlow:** Deploying a distributed TensorFlow cluster with all of its components on any infrastructure, whether it’s baremetal, virtual or public cloud is as simple as passing a JSON file to a single CLI command. Updating and tweaking parameters to fine-tune and optimize becomes trivial.
    > 2.  **Share infrastructure across teams:** DC/OS allows multiple teams to share the infrastructure and launch multiple TensorFlow jobs while maintaining complete resource isolation. Once a TensorFlow job is done, capacity is released and made available to other teams.
    > 3.  **Deploy different TensorFlow versions on the same cluster:** As with many DC/OS services, you can easily deploy multiple instances of a services, each with a different version, on the same cluster. This means that when a new version of TensorFlow is released, one team can take advantage of the latest features and capabilities without running the risk of breaking another team’s code.
    > 4.  **Allocate GPUs dynamically:** GPUs greatly increase the speed of deep learning models, especially during training. However, GPUs are precious resources that must be efficiently utilized. Since DC/OS automatically detects all GPUs on a cluster, [GPU-based scheduling](https://mesosphere.com/blog/accelerating-machine-learning-with-gpus-and-dcos/) can be used to allow TensorFlow to request all or some of the GPU resources on a per job basis (similar to requesting CPU, memory, and disk resources). Once the job is complete, the GPU resources are released and made available to other jobs.
    > 5.  **Focus on model development, not deployment:** DC/OS separates the model development from the cluster configuration by eliminating the need to manually introduce a ClusterSpec in the model code. Instead, the person deploying the TensorFlow package specifies the properties of the various workers and parameter servers they would like their model to run with, and the package generates a unique ClusterSpec for it at deploy-time. Under the hood the package finds a set of machines to run each worker / parameter server on, populates a ClusterSpec with the appropriate values, starts each parameter server and worker task, and passes it the generated ClusterSpec. The developer simply writes his code expecting this object to be populated, and the package takes care of the rest.The figure below shows a JSON snippet that can be used to deploy a TensorFlow package from the DC/OS CLI with a mix of CPU and GPU workers.![It's easy to deploy distributed TensorFlow on DC/OS using the CLI.](https://mesosphere.com/wp-content/uploads/2017/10/tensorflow-dcos-7.png?v2)
    >     
    >     The command to launch TensorFlow with this config would be:
    >     
    >     dcos package install beta-tensorflow --options=<path/to/config.json>
    >     
    >     The package can also be deployed from the DC/OS service catalog by specifying these parameters in the UI.
    >     
    > 6.  **Automate failure recovery:** The TensorFlow package is written using the DC/OS SDK and leverages built-in resiliency features including automatic restart so that failed tasks effectively self-heal.
    > 7.  **Deploy job configuration parameters securely at runtime:** The DC/OS secrets service dynamically deploys credentials and confidential configuration options to each TensorFlow instance at runtime. Operators can easily add credentials to access confidential information or specific configuration URLs without exposing them in the model code.
    > 
    > 


- [Day1: 使用Apache Mesos的目的為何？ - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10184643)

    > **它能幫助我們做到哪些事情？**
    > 
    > ![http://ithelp.ithome.com.tw/upload/images/20161201/20103456RrxGTPlpbk.png](http://ithelp.ithome.com.tw/upload/images/20161201/20103456RrxGTPlpbk.png)
    > 
    > 上圖是一個在傳統部署service最簡單的架構，如有四台機器有2台是部署Tomcat Service另外2台是Jetty Service，在部署這些service上系統管理者必須要清礎的知道哪些server上有哪些Service，並且要了解到每台server上的資源，如果這時有新的需求如要在加入一台新的Jetty Service，這時系統管理員會在這四台機器中選擇一台資源使用率較低的server進行部署。之後host1有可能因為硬體故障導致Tomcat Service無法啟動，而大家只能連到host2有可能導致流量過大而造成host2記憶體不夠而當機，一連串的惡性循環而造成系統管理員過累工作效率降低，而下圖改用Apache Mesos的架構來解決此問題：  
    > ![http://ithelp.ithome.com.tw/upload/images/20161201/20103456XODssn8JE9.png](http://ithelp.ithome.com.tw/upload/images/20161201/20103456XODssn8JE9.png)
    > 
    > 改成Apache Mesos架構會如上圖，Mesos詳細的架構在未來還會繼續介紹，以上圖來說在建構Tomcat Service和Jetty Service的操作是透過Mesos Framework如Marathon的方式，我們只要透過restful的方式把寫好的json設定傳到Marathon就可以執行啟動service，json的設定檔內容如下，Marathon Framework也在未來會做介紹，現在只是簡單demo mesos對我們使用上的方便性。
    > 
    > **能夠使我們得到哪些好處呢？**
    > 
    > ![http://ithelp.ithome.com.tw/upload/images/20161201/20103456lZY8QVdJ2Q.png](http://ithelp.ithome.com.tw/upload/images/20161201/20103456lZY8QVdJ2Q.png)
    > 
    > 執行restful的指令如下：
    > 
    > ```
    > curl -X POST -H "Content-type: application/json" http://172.17.0.4:8080/v2/apps -d @Tomcat.json
    > ```
    > 
    > 上面的json設定可以設定tomcat service要執行在2台的server上，如果有一台的service被砍掉或當掉會在其它的server上啟動service、可以設定要在哪幾台特定的server上執行service、另外也可以去指定service需要多少的資源(如：CPU core數、記憶體大小)…等等的功能，這些在未來都會做介紹，在部署server上只要把設定檔寫好就可以快速的把service啟動起來，讓我們的工作效率增加也期望讓我們在部署service和管理整個cluster的資源更加的自動化。
    > 



## HyperPilot
- [容器叢集效能成新議題，HyperPilot開源釋出，要靠機器學習自動優化容器叢集 | iThome](https://www.ithome.com.tw/news/121876)

    > 藉助容器叢集，來支援大數據或機器學習分析所需的大型叢集，已是資料科學家常用的方法之一，但想要自己在雲端部署Docker容器叢集，第一個挑戰就是，要怎麼租用VM，才能省錢又能符合需要的效能？得同時考量VM規格、容器配置和應用程式的配置需求等多項複雜變因，來衡量成本，往往得靠資深的雲端架構師才有能力拿捏得當。
    > 
    > 前Mesosphere分散式系統首席工程師Timothy Chen[近日開源釋出](https://medium.com/@tnachen/hyperpilot-open-sourced-100-of-its-products-18d0e018fe45)了一套容器叢集配置自動化工具Hyperpilot，這是利用機器學習技術中的Bayesian Optimization最佳化技術，依據使用者提供的條件，來找出最佳的容器叢集所需要的VM架構配置，目前只能針對AWS上的VM規格為優化對象。
    > 
    > 這套工具還提供了一個資源瓶頸分析工具HyperPath，可以從CPU、記憶體、網路、I/O的來評估資源瓶頸，開發者已配置的單一容器或單一節點的效能上限，方便開發者來衡量應用程式在這樣規格的容器或節點上的執行效能。
    > 
    > Timothy Chen率領的團隊也開發了新的Heracles 效能評估演算法，可供容器叢集控制器使用，來動態調整配置給應用程式的資源，根據Timothy Chen釋出的測試例子，可將一個Spark分析叢集的效能利用率提高2～3倍。

- [Hyperpilot open sourced 100% of its products – Timothy Chen – Medium](https://medium.com/@tnachen/hyperpilot-open-sourced-100-of-its-products-18d0e018fe45)

