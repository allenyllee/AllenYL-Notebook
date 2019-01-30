# Linux__問題排解5-1_Docker

[toc]
<!-- toc --> 

# docker

## tutorials

- [什麼是 Docker · 《Docker —— 從入門到實踐》正體中文版](https://philipzheng.gitbooks.io/docker_practice/content/introduction/what.html)

- [什么是 Docker · Docker —— 从入门到实践](https://yeasy.gitbooks.io/docker_practice/content/introduction/what.html)

## 操作容器

-   docker run ubuntu:14.04 /bin/echo 'Hello world'
    
-   docker run -t -i ubuntu:14.04 /bin/bash #交互模式
    
-   docker run ubuntu:17.10 /bin/sh -c "while true; do echo hello world; sleep 1; done" #後台模式
    
-   docker container ls #列出容器
    
-   docker container stop \[container_id\] #終止容器
    
-   docker container rm \[container_name\] #刪除容器
    

### see the file size of your containers

- [linux - Docker - How to analyze a container's disk usage? - Stack Overflow](https://stackoverflow.com/questions/26753087/docker-how-to-analyze-a-containers-disk-usage)

    > To see the file size of your containers, you can use the `-s` argument of `docker ps`:
    > 
    > ```
    > docker ps -s
    > 
    > ```
    > 
    > ---
    > 
    > After **1.13.0, Docker** includes a new command `docker system df` to show docker disk usage.
    > 
    > ```
    > $ docker system df
    > TYPE            TOTAL        ACTIVE     SIZE        RECLAIMABLE
    > Images          5            1          2.777 GB    2.647 GB (95%)
    > Containers      1            1          0 B         0B
    > Local Volumes   4            1          3.207 GB    2.261 (70%)
    > 
    > ```
    > 
    > To show more detailed information on space usage
    > 
    > ```
    > $ docker system df -v
    > 
    > ```



## 進入容器

```shell
docker exec -ti [container_id] bash #進入容器
```
### Exploring Docker container's file system

- [linux - Exploring Docker container's file system - Stack Overflow](https://stackoverflow.com/questions/20813486/exploring-docker-containers-file-system)

    > **Method 1: snapshoting**
    > 
    > You can evaluate container filesystem this way:
    > 
    > ```
    > # find ID of your running container:
    > docker ps
    > 
    > # create image (snapshot) from container filesystem
    > docker commit 12345678904b5 mysnapshot
    > 
    > # explore this filesystem using bash (for example)
    > docker run -t -i mysnapshot /bin/bash
    > 
    > ```
    > 
    > This way, you can evaluate filesystem of the running container in the precise time moment. Container is still running, no future changes are included.
    > 
    > You can later delete snapshot using (filesystem of the running container is not affected!):
    > 
    > ```
    > docker rmi mysnapshot
    > 
    > ```
    > 
    > **Method 2: ssh**
    > 
    > If you need continuous access, you can install sshd to your container and run the sshd daemon:
    > 
    > ```
    >  docker run -d -p 22 mysnapshot /usr/sbin/sshd -D
    > 
    >  # you need to find out which port to connect:
    >  docker ps
    > 
    > ```
    > 
    > This way, you can run your app using ssh (connect and execute what you want).
    > 
    > **UPDATE - Method 3: nsenter**
    > 
    > Use `nsenter`, see <http://blog.docker.com/2014/06/why-you-dont-need-to-run-sshd-in-docker/>
    > 
    > > *The short version is: with nsenter, you can get a shell into an existing container, even if that container doesn't run SSH or any kind of special-purpose daemon*
    > 
    > **UPDATE - Method 4: docker exec**
    > 
    > Docker version 1.3 (latest, you might need to use docker apt repo to install latest version as of Nov 2014) supports new command `exec` that behave similar to `nsenter`. This command can run new process in already running container (container must have PID 1 process running already). You can run `/bin/bash` to explore container state:
    > 
    > ```
    > docker exec -t -i mycontainer /bin/bash
    > 
    > ```
    > 
    > see [Docker command line documentation](https://docs.docker.com/v1.3/reference/commandline/cli/#exec)
    > 
    > 
    > ---
    > 
    > The most voted answer is good except if your container isn't an actual Linux system.
    > 
    > Many containers (especially the go based ones) don't have any standard binary (no /bin/bash, /bin/sh). In that case, you will need to access the actual containers file directly:
    > 
    > Works like a charm:
    > 
    > ```
    > name=< name>
    > dockerId=$(docker inspect -f {{.Id}} $name)
    > mountId=$(cat /var/lib/docker/image/aufs/layerdb/mounts/$dockerId/mount-id)
    > cd /var/lib/docker/aufs/mnt/$mountId
    > 
    > ```
    > 
    > Note: You need to run it as root.
    > 



## 操作鏡像
    
-   在 Dockerfile 文件所在目录执行：docker build -t \[image_name\]:\[tag\] . #製作鏡像
    
-   docker pull \[image\]:\[tag\] #從Dockerhub拉取鏡像

## dockerfile

- [Compose file version 2 reference | Docker Documentation](https://docs.docker.com/compose/compose-file/compose-file-v2/#cpu-and-other-resources)

    > **Note:** The following options were added in [version 2.2](https://docs.docker.com/compose/compose-file/compose-versioning/#version-22): `cpu_count`, `cpu_percent`, `cpus`. The following options were added in [version 2.1](https://docs.docker.com/compose/compose-file/compose-versioning/#version-21): `oom_kill_disable`, `cpu_period`

### multi-stage builds

- [Use multi-stage builds | Docker Documentation](https://docs.docker.com/develop/develop-images/multistage-build/)

    > Name your build stages
    > ----------------------
    > 
    > By default, the stages are not named, and you refer to them by their integer number, starting with 0 for the first `FROM` instruction. However, you can name your stages, by adding an `as <NAME>` to the `FROM` instruction. This example improves the previous one by naming the stages and using the name in the `COPY` instruction. This means that even if the instructions in your Dockerfile are re-ordered later, the `COPY` doesn't break.
    > 
    > ```sh
    > FROM golang:1.7.3 as builder
    > WORKDIR /go/src/github.com/alexellis/href-counter/
    > RUN go get -d -v golang.org/x/net/html
    > COPY app.go    .
    > RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .
    > 
    > FROM alpine:latest
    > RUN apk --no-cache add ca-certificates
    > WORKDIR /root/
    > COPY --from=builder /go/src/github.com/alexellis/href-counter/app .
    > CMD ["./app"]
    > 
    > ```
    > 
    > Stop at a specific build stage
    > ------------------------------
    > 
    > When you build your image, you don't necessarily need to build the entire Dockerfile including every stage. You can specify a target build stage. The following command assumes you are using the previous `Dockerfile` but stops at the stage named `builder`:
    > 
    > ```sh
    > $ docker build --target builder -t alexellis2/href-counter:latest .
    > 
    > ```
    > 
    > A few scenarios where this might be very powerful are:
    > 
    > -   Debugging a specific build stage
    > -   Using a `debug` stage with all debugging symbols or tools enabled, and a lean `production` stage
    > -   Using a `testing` stage in which your app gets populated with test data, but building for production using a different stage which uses real data
    > 
    > Use an external image as a "stage"
    > ----------------------------------
    > 
    > When using multi-stage builds, you are not limited to copying from stages you created earlier in your Dockerfile. You can use the `COPY --from` instruction to copy from a separate image, either using the local image name, a tag available locally or on a Docker registry, or a tag ID. The Docker client pulls the image if necessary and copies the artifact from there. The syntax is:
    > 
    > ```sh
    > COPY --from=nginx:latest /etc/nginx/nginx.conf /nginx.conf
    > 
    > ```



### CMD as parameters of ENTRYPOINT

- [Docker difference between run, cmd, entrypoint commands](https://til.codes/docker-run-vs-cmd-vs-entrypoint/)

    > ###### Exec form
    > 
    > Exec form of ENTRYPOINT allows you to set commands and parameters and then use either form of CMD to set additional parameters that are more likely to be changed. ENTRYPOINT arguments are always used while CMD ones can be overwritten by command line arguments provided when Docker container runs. For example, the following snippet in Dockerfile
    > 
    > ```
    > ENTRYPOINT ["/bin/echo", "Hello"]
    > CMD ["world"]
    > 
    > ```
    > 
    > when container runs as `docker run -it <image>` will produce output
    > 
    > ```
    > Hello world
    > 
    > ```
    > 
    > 

### limit Docker container logs size

- [logging - Docker container logs taking all my disk space - Stack Overflow](https://stackoverflow.com/questions/31829587/docker-container-logs-taking-all-my-disk-space#_=_)

    > CAUTION: This is for docker-compose version 2 only
    > 
    > Example:
    > 
    > ```
    > version: '2'
    > services:
    >   db:
    >     container_name: db
    >     image: mysql:5.7
    >     ports:
    >       - 3306:3306
    >     logging:
    >       options:
    >         max-size: 50m
    > 
    > ```

### clear the logs properly for a Docker container

- [How to clear the logs properly for a Docker container? - Stack Overflow](https://stackoverflow.com/questions/42510002/how-to-clear-the-logs-properly-for-a-docker-container)

    > From [this question](https://serverfault.com/q/637996/351549) there's a one-liner that you can run:
    > 
    > ```
    > echo "" > $(docker inspect --format='{{.LogPath}}' <container_name_or_id>)
    > 
    > ```
    > 
    > I'm not a big fan of modifying Docker's files directly. You can have Docker automatically rotate the logs for you. This is done with additional flags to dockerd if you are using the default [JSON logging driver](https://docs.docker.com/config/containers/logging/json-file/):
    > 
    > ```
    > dockerd ... --log-opt max-size=10m --log-opt max-file=3
    > 
    > ```
    > 
    > You can also set this as part of your [daemon.json](https://docs.docker.com/engine/reference/commandline/dockerd/#on-linux) file instead of modifying your startup scripts:
    > 
    > ```
    > {
    >   "log-driver": "json-file",
    >   "log-opts": {"max-size": "10m", "max-file": "3"}
    > }
    > 
    > ```
    > 
    > Make sure to run a `systemctl reload docker` after changing this file to have the settings applied.
    > 

## nvidia docker OpenGL support

- [nvidia/cudagl - Docker Hub](https://hub.docker.com/r/nvidia/cudagl/)

- [nvidia/opengl - Docker Hub](https://hub.docker.com/r/nvidia/opengl/)

- [nvidia-docker 1 can run OpenGL applications; nvidia-docker 2 can't · Issue #534 · NVIDIA/nvidia-docker](https://github.com/NVIDIA/nvidia-docker/issues/534)


- [ros-indigo-desktop-full-nvidia/Dockerfile at master · lindwaltz/ros-indigo-desktop-full-nvidia](https://github.com/lindwaltz/ros-indigo-desktop-full-nvidia/blob/master/Dockerfile)

    > 
    > **below sourced from https://gitlab.com/nvidia/opengl/blob/ubuntu14.04/1.0-glvnd/runtime/Dockerfile**
    > 
    > ```dockerfile
    > RUN apt-get update && apt-get install -y --no-install-recommends \
    >         git \
    >         ca-certificates \
    >         make \
    >         automake \
    >         autoconf \
    >         libtool \
    >         pkg-config \
    >         python \
    >         libxext-dev \
    >         libx11-dev \
    >         x11proto-gl-dev && \
    >     rm -rf /var/lib/apt/lists/*
    > 
    > WORKDIR /opt/libglvnd
    > 
    > RUN git clone --branch=v1.0.0 https://github.com/NVIDIA/libglvnd.git . && \
    >     ./autogen.sh && \
    >     ./configure --prefix=/usr/local --libdir=/usr/local/lib/x86_64-linux-gnu && \
    >     make -j"$(nproc)" install-strip && \
    >     find /usr/local/lib/x86_64-linux-gnu -type f -name 'lib*.la' -delete
    > 
    > RUN dpkg --add-architecture i386 && \
    >     apt-get update && apt-get install -y --no-install-recommends \
    >         gcc-multilib \
    >         libxext-dev:i386 \
    >         libx11-dev:i386 && \
    >     rm -rf /var/lib/apt/lists/*
    > 
    > # 32-bit libraries
    > RUN make distclean && \
    >     ./autogen.sh && \
    >     ./configure --prefix=/usr/local --libdir=/usr/local/lib/i386-linux-gnu --host=i386-linux-gnu "CFLAGS=-m32" "CXXFLAGS=-m32" "LDFLAGS=-m32" && \
    >     make -j"$(nproc)" install-strip && \
    >     find /usr/local/lib/i386-linux-gnu -type f -name 'lib*.la' -delete
    > 
    > #COPY --from=glvnd /usr/local/lib/x86_64-linux-gnu /usr/local/lib/x86_64-linux-gnu
    > #COPY --from=glvnd /usr/local/lib/i386-linux-gnu /usr/local/lib/i386-linux-gnu
    > 
    > COPY 10_nvidia.json /usr/local/share/glvnd/egl_vendor.d/10_nvidia.json
    > 
    > RUN echo '/usr/local/lib/x86_64-linux-gnu' >> /etc/ld.so.conf.d/glvnd.conf && \
    >     echo '/usr/local/lib/i386-linux-gnu' >> /etc/ld.so.conf.d/glvnd.conf && \
    >     ldconfig
    > 
    > ENV LD_LIBRARY_PATH /usr/local/lib/x86_64-linux-gnu:/usr/local/lib/i386-linux-gnu${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
    > ```
    > 


## install docker in bash on windows

- [Running Docker containers on Bash on Windows - Jayway](https://blog.jayway.com/2017/04/19/running-docker-on-bash-on-windows/)

- [Installing the Docker client on Windows Subsystem for Linux (Ubuntu)](https://medium.com/@sebagomez/installing-the-docker-client-on-ubuntus-windows-subsystem-for-linux-612b392a44c4)

- [Can you run Docker natively on the new Windows 10 (Ubuntu) bash userspace? - Server Fault](https://serverfault.com/questions/767994/can-you-run-docker-natively-on-the-new-windows-10-ubuntu-bash-userspace#_=_)

## debconf: delaying package configuration, since apt-utils is not installed

- [出现 debconf: delaying package configuration, sin... - 简书](https://www.jianshu.com/p/99fd61e6aa29)


    > 在使用Dockerfile构建镜像时，在安装软件包的过程中，出现了一个问题：
    > 
    > ```
    > debconf: delaying package configuration, since apt-utils is not installed
    > 
    > ```
    > 
    > 我的目标镜像是ubuntu的latest
    > 
    > 在寻找答案的过程中，我在一个github项目的issue中找到了一些解释：
    > 
    > 翻译后大致如下：
    > 
    > > 没有安装这个包会造成什么危害（警告除外）吗？
    > 
    > 不，它还没有停止任何运行的软件。只是一个警告，没有别的。
    > 
    > > 它只对交互式安装很重要。
    > 
    > 所以在我们如果不必要给予某些软件包相应的配置信息时，可以采用`apt-get`的一个选项`--assume-yes`,即忽略掉警告信息。
    > 
    > 所以当前最好的解决方案是:
    > 
    > ```
    > ARG DEBIAN_FRONTEND=noninteractive
    > RUN apt-get update && apt-get install --assume-yes apt-utils
    > 
    > ```
    > 
    > 作用就是忽略掉相应的警告信息。
    > 
    > 但是 如果某些软件包需要进行相应的配置。那么这种做法也不可取。\
    > 还在找寻原因...................
    > 
    > 参考资料:\
    > 上文中所看到的[issue](https://link.jianshu.com?t=https://github.com/tianon/docker-brew-ubuntu-core/issues/59)
    > 

## apt gives “Unstable CLI Interface” warning

- [command line - apt gives “Unstable CLI Interface” warning - Ask Ubuntu](https://askubuntu.com/questions/990823/apt-gives-unstable-cli-interface-warning)

    > That's quite simple: `apt` is for the terminal and gives beautiful output while `apt-get` and `apt-cache` are for scripts and give stable, parseable output.

## mount

### 技术|Docker背后的内核知识：命名空间资源隔离

- [技术|Docker背后的内核知识：命名空间资源隔离](https://linux.cn/article-5057-5.html)



### mounted inside the container, expose it to the host

- [docker - s3 mounted inside the container. how to expose it to the host? - Stack Overflow](https://stackoverflow.com/questions/43687025/s3-mounted-inside-the-container-how-to-expose-it-to-the-host)

    > I do similar thing with glusterFS it requires higher permissions for the container but it's doable. In short docker command would be:
    > 
    > ```sh
    > docker run --cap-add SYS_ADMIN --device fuse -v host_mount_dir:container_mount_dir:shared IMAGE COMMAND
    > 
    > ```
    > 
    > If you get error like "Path /foo is mounted on /foo but it is not a shared mount ..." then your docker daemon runs in different mount namespace than systemd. There is an easy way to make it in same namespace:
    > 
    > ```sh
    > mkdir -p /etc/systemd/system/docker.service.d/
    > cat << EOF > /etc/systemd/system/docker.service.d/clear_mount_propagation_flags.conf
    > [Service]
    > MountFlags=shared
    > EOF
    > 
    > ```
    > 
    > And restart docker daemon. TL;DR: mount will be visible on host if you mount it into dir binded by -v. Watch out for dragons ;)
    > 
    > ---
    > 
    > This works with other mount types. The key is `:shared` flag on the volume (bind) when running container. -- [Artur Bodera](https://stackoverflow.com/users/181664/artur-bodera "1,489 reputation") [Sep 12 '17 at 9:37](https://stackoverflow.com/questions/43687025/s3-mounted-inside-the-container-how-to-expose-it-to-the-host#comment79307959_43687970)

## logs

- [docker logs | Docker Documentation](https://docs.docker.com/engine/reference/commandline/logs/)





# LXC

## run most armv7 binaries directly on x86 by LXC and qemu-user-static

- [LXC 1.0: Some more advanced container usage [4/10] | Stéphane Graber's website](https://stgraber.org/2013/12/23/lxc-1-0-some-more-advanced-container-usage/)

    > Running foreign architectures
    > =============================
    > 
    > By default LXC will only let you run containers of one of the architectures supported by the host. That makes sense since after all, your CPU doesn't know what to do with anything else.
    > 
    > Except that we have this convenient package called "qemu-user-static" which contains a whole bunch of emulators for quite a few interesting architectures. The most common and useful of those is qemu-arm-static which will let you run most armv7 binaries directly on x86.
    > 
    > The "ubuntu" template knows how to make use of qemu-user-static, so you can simply check that you have the "qemu-user-static" package installed, then run:
    > 
    > ```sh
    > sudo lxc-create -t ubuntu -n p3 -- -a armhf
    > ``` 
    > 
    > After a rather long bootstrap, you'll get a new p3 container which will be mostly running Ubuntu armhf. I'm saying mostly because the qemu emulation comes with a few limitations, the biggest of which is that any piece of software using the ptrace() syscall will fail and so will anything using netlink. As a result, LXC will install the host architecture version of upstart and a few of the networking tools so that the containers can boot properly.
    > 
    > ```sh
    > stgraber@castiana:~$ file /bin/ls
    > /bin/ls: ELF 64-bit LSB  executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, """BuildID[sha1]""" =e50e0a5dadb8a7f4eaa2fd715cacb9842e157dc7, stripped
    > stgraber@castiana:~$ sudo lxc-start -n p3 -d
    > stgraber@castiana:~$ sudo lxc-attach -n p3
    > root@p3:/# file /bin/ls
    > /bin/ls: ELF 32-bit LSB  executable, ARM, EABI5 version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, """BuildID[sha1]""" =88ff013a8fd9389747fb1fea1c898547fb0f650a, stripped
    > root@p3:/# exit
    > stgraber@castiana:~$ sudo lxc-stop -n p3
    > stgraber@castiana:~$
    > ```
    > 
    > Hooks
    > =====
    > 
    > As we know people like to script their containers and that our configuration can't always accommodate every single use case, we've introduced a set of hooks which you may use.
    > 
    > Those hooks are simple paths to an executable file which LXC will run at some specific time in the lifetime of the container. Those executables will also be passed a set of useful environment variables so they can easily know what container invoked them and what to do.
    > 
    > The currently available hooks are (details in [lxc.conf(5)](http://qa.linuxcontainers.org/master/current/doc/man/lxc.conf.5.html "lxc.conf(5) manpage")):
    > 
    > -   lxc.hook.pre-start (called before any initialization is done)
    > -   lxc.hook.pre-mount (called after creating the mount namespace but before mounting anything)
    > -   lxc.hook.mount (called after the mounts but before pivot_root)
    > -   lxc.hook.autodev (identical to mount but only called if using autodev)
    > -   lxc.hook.start (called in the container right before /sbin/init)
    > -   lxc.hook.post-stop (run after the container has been shutdown)
    > -   lxc.hook.clone (called when cloning a container into a new one)
    > 
    > Additionally each network section may also define two additional hooks:
    > 
    > -   lxc.network.script.up (called in the network namespace after the interface was created)
    > -   lxc.network.script.down (called in the network namespace before destroying the interface)
    > 
    > All of those hooks may be specified as many times as you want in the configuration so you can use each hooking point multiple times.
    > 
    > As a simple example, let's add the following to our "p1" container:
    > ```sh
    > lxc.hook.pre-start = /var/lib/lxc/p1/pre-start.sh
    > ```
    > 
    > And create the hook itself at /var/lib/lxc/p1/pre-start.sh:
    > 
    > ```sh
    > #!/bin/sh
    > echo "arguments: $*" > /tmp/test
    > echo "environment:" >> /tmp/test
    > env | grep LXC >> /tmp/test
    > ```
    > 
    > Make it executable (chmod 755) and then start the container.\
    > Checking /tmp/test you should see:
    > 
    > ```sh
    > arguments: p1 lxc pre-start
    > environment:
    > LXC_ROOTFS_MOUNT=/usr/lib/x86_64-linux-gnu/lxc
    > LXC_CONFIG_FILE=/var/lib/lxc/p1/config
    > LXC_ROOTFS_PATH=/var/lib/lxc/p1/rootfs
    > LXC_NAME=p1
    > ```
    > 
    > Android containers
    > ==================
    > 
    > I've often been asked whether it was possible to run Android in an LXC container. Well, the short answer is yes. However it's not very simple and it really depends on what you want to do with it.
    > 
    > The first thing you'll need if you want to do this is get your machine to run an Android kernel, you'll need to have any modules needed by Android built and loaded before you can start the container.
    > 
    > Once you have that, you'll need to create a new container by hand.\
    > Let's put it in "/var/lib/lxc/android/", in there, you need a configuration file similar to this one:
    > 
    > ```sh
    > lxc.rootfs = /var/lib/lxc/android/rootfs
    > lxc.utsname = armhf
    > 
    > lxc.network.type = none
    > 
    > lxc.devttydir = lxc
    > lxc.tty = 4
    > lxc.pts = 1024
    > lxc.arch = armhf
    > lxc.cap.drop = mac_admin mac_override
    > lxc.pivotdir = lxc_putold
    > 
    > lxc.hook.pre-start = /var/lib/lxc/android/pre-start.sh
    > 
    > lxc.aa_profile = unconfined
    > ```
    > 
    > /var/lib/lxc/android/pre-start.sh is where the interesting bits happen. It needs to be an executable shell script, containing something along the lines of:
    > 
    > ```sh
    > #!/bin/sh
    > mkdir -p $LXC_ROOTFS_PATH
    > mount -n -t tmpfs tmpfs $LXC_ROOTFS_PATH
    > 
    > cd $LXC_ROOTFS_PATH
    > cat /var/lib/lxc/android/initrd.gz | gzip -d | cpio -i
    > 
    > # Create /dev/pts if missing
    > mkdir -p $LXC_ROOTFS_PATH/dev/pts
    > ```
    > 
    > Then get the initrd for your device and place it in /var/lib/lxc/android/initrd.gz.
    > 
    > At that point, when starting the LXC container, the Android initrd will be unpacked on a tmpfs (similar to Android's ramfs) and Android's init will be started which in turn should mount any partition that Android requires and then start all of the usual services.
    > 
    > Because there are no apparmor, cgroup or even network configuration applied to it, the container will have a lot of rights and will typically completely crash the machine. You unfortunately have to be familiar with the way Android works and not be afraid to modify its init scripts if not even its init process to only start the bits you actually want.
    > 
    > I can't provide a generic recipe there as it completely depends on what you're interested on, what version of Android and what device you're using. But it's clearly possible to do and you may want to look at Ubuntu Touch to see how we're doing it by default there.
    > 
    > One last note, Android's init script isn't in /sbin/init, so you need to tell LXC where to load it with:
    > ```sh
    > lxc-start -n android -- /init
    > ```
    > 
    > LXC on Android devices
    > ======================
    > 
    > So now that we've seen how to run Android in LXC, let's talk about running Ubuntu on Android in LXC.
    > 
    > LXC has been ported to bionic (Android's C library) and while not feature-equivalent with its glibc build, it's still good enough to be used.
    > 
    > Unfortunately due to the kind of low level access LXC requires and the fact that our primary focus isn't Android, installation could be easier...You won't be finding LXC on the Google PlayStore and we won't provide you with a .apk that you can install.
    > 
    > Instead every time something changes in the upstream git branch, we produce a new tarball which can be downloaded here: <https://jenkins.linuxcontainers.org/view/LXC/view/LXC%20builds/job/lxc-build-android/lastSuccessfulBuild/artifact/lxc-android.tar.gz>
    > 
    > This build is known to work with Android >= 4.2 but will quite likely work on older versions too.
    > 
    > For this to work, you'll need to grab your device's kernel configuration and run lxc-checkconfig against it to see whether it's compatible with LXC or not. Unfortunately it's very likely that it won't be... In that case, you'll need to go hunt for the kernel source for your device, add the missing feature flags, rebuild it and update your device to boot your updated kernel.
    > 
    > As scary as this may sound, it's usually not that difficult as long as your device is unlocked and you're already using an alternate ROM like Cyanogen which usually make their kernel git tree easily available.
    > 
    > Once your device has a working kernel, all you need to do is unpack our tarball as root in your device's / directory, copy an arm container to /data/lxc/containers/<container name>, get into /data/lxc and run "./run-lxc lxc-start -n <container name>".\
    > A few seconds later you'll be greeted by a login prompt.

