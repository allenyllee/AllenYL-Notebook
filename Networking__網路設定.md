# Networking__網路設定

[toc]
<!-- toc --> 

## DNS 設定

- [隱私優先、速度最快，公共DNS服務1.1.1.1上線了 | iThome](https://www.ithome.com.tw/news/122215)

    > 1.1.1.1也強調它是網路上最快的DNS目錄，它的查詢速度只有14.01毫秒，快過Cisco OpenDNS的20.6毫秒、Google Public DNS的34.7毫秒，以及一般ISP業者的68.23毫秒。


- [1.1.1.1 — the Internet’s Fastest, Privacy-First DNS Resolver](https://1.1.1.1/)

## 區網設定

- [請問怎麼兩個同時連線(區網、VPN) - PCZONE 討論區](http://www.pczone.com.tw/vbb3/thread/29/148443/)

    > 目前電腦內有兩個網路(區網、VPN)
    > 想要VPN專門連線上遊戲
    > 其他走區網
    > 不管怎麼設定都是全部走VPN，請網友指導一下
    > 
    > 網路環境是 一組浮動IP透過分享器DHCP至兩台電腦，DMZ設我這台
    > 
    > VPN啟用後命令提示字元鍵入下列指令
    > route change 0.0.0.0 mask 0.0.0.0 XXX.XXX.XXX.XXX
    > route add 0.0.0.0 mask 0.0.0.0 10.0.0.1 metric 50
    > route add 61.215.216.38 10.0.0.1
    > 
    > XXXX是我連外的IP
    > 61.215.216.38是線上遊戲的IP
    > 10.0.0.1是VPN的閘道器
    > 
    > route的用法不太清楚，請指導我一下 謝謝
    > 
    > ---
    > 
    > VPN 內容, TCP/IP 內容, 使用遠端閘道, 不勾, 然後只保留以下這行
    > 引用:
    > 作者: mingbot01 觀看文章
    > route add 61.215.216.38 10.0.0.1


## VPN

- [各种翻墙对比 · Fuck GFW](https://darrenliuwei.com/fuck-gfw/vs.html)

- [VPN原理 - VPN簡介與其應用](https://sites.google.com/site/vpnjianjieyuqiyingyong/xian-kuang-miao-shu/vpn-yuan-li)

    > __VPN原理__
    > 
    > VPN的原理技術很簡單，主要採用的原理技術有四個：穿隧技術（Tunneling）、加解密技術（Encryption & Decryption）、金鑰管理技術（Key management）、使用者與設備身分鑑別技術（Authentication）。
    > 
    > 1.    穿隧技術〈Tunneling〉
    >     穿隧技術其實很簡單，其原理就是將你原本的封包(Packet)視為資料(Data)再重新封裝(Encapsulation)，變成新的封包傳輸在公用網路中。
    > ![](https://sites.google.com/site/vpnjianjieyuqiyingyong/_/rsrc/1420282232007/xian-kuang-miao-shu/vpn-yuan-li/Tunneling.png)
    >     Data：你要傳輸的資料內容。
    >     Header1：內含的 IP Address 是區域或虛擬網路的 IP，或是自訂的 Protocol。
    >     Hearder2：內含的 IP Address 是你要傳輸到對方的IP。
    >     
    >          而穿隧技術是由三種不同的協議所組成的：
    >         1.    Carrier Protocol：用來在網際網路上傳遞封包用的協定。[1]
    >         2.    Encapsulation Protocol：用來包裝原本封包資料用的協定，也就是Header2所使用的協議。例如：GRE、IPSec、PPTP、L2TP....等。[1]
    >         3.    Passenger Protocol：原本封包資料所使用的協定，也就是Header1所使用的協議。[1]
    > 
    >         而Encapsulation Protocol裡的協議會在VPN協議裡作介紹。
    > 
    > 2.    加解密技術〈Encryption & Decryption〉
    >     加解密技術是一個很複雜的，在這我只簡單介紹。對於加密的方法分為兩種：
    > 
    >         1. 對稱式金鑰加密（Symmetric-key algorithm）：又稱為對稱加密、私鑰加密、共享密鑰加密，是密碼學中的一類加密演算法。這類演算法在加密和解密時使用相同的密鑰，或是使用兩個可以簡單地相互推算的密鑰。實務上，這組密鑰成為在兩個或多個成員間的共同祕密，以便維持專屬的通訊聯繫。與公開密鑰加密相比，要求雙方取得相同的密鑰是對稱密鑰加密的主要缺點之一。[3]
    >         
    >         2. 公開金鑰加密〈Public-key cryptography〉：也稱為非對稱加密（asymmetric cryptography），一種密碼學演算法類型，在這種密碼學方法中，需要一對金鑰，一是個私人金鑰，另一個則是公開金鑰。這兩個金鑰是數學相關，用某用戶金鑰加密後所得的資訊，只能用該用戶的解密金鑰才能解密。如果知道了其中一個，並不能計算出另外一個。因此如果公開了一對金鑰中的一個，並不會危害到另外一個的秘密性質。稱公開的金鑰為公鑰；不公開的金鑰為私鑰。[4]
    > 
    >         VPN各個節點間是利用3DES或DES這種對稱式金鑰加密，以達到高傳輸效率。而VPN對於身分認證跟金鑰傳輸是利用非對稱加密的方式。
    > 
    > 3.    金鑰管理技術〈Key management〉
    >     現行常用密鑰管理的技術又可分為SKIP(Simple Key management for IP)與ISAKMP/Oakley (又稱為IKE)兩種。SKIP(Simple Key Management for IP) 利用Diffee-Hellman演算法則， 應用在網路上傳輸密鑰的技術，而ISAKMP/Oakley : Oakley定義如何分辨及確認密鑰，ISA KMP定義分配密鑰的方法。將來會整合在IPv6中。[5]
    > 
    > 4.   使用者與設備身分鑑別技術〈Authentication〉
    >     這個部分是為了確認跟你連接或你所連接VPN對方的身分是不是本人所建立起的機制，主要分為兩種：
    > 
    >         1. 使用者身分鑑別部分：使用者名稱跟密碼、IC卡鑑別‧‧‧等。
    >         2. 設備身分鑑別部分：CA的X.509憑證、分享金鑰。
    >     
    > ---
    > 
    > __VPN協議__
    >     在這我要介紹VPN技術，大概可以分為以下這5種VPN：PPTP、L2TP、IPsec、MPLS、SSL VPN。 
    > 1. 點對點隧道協議PPTP〈Point to Point Tunneling Protocol〉：  
    > 
    >     點對點隧道協議 (PPTP) 是由包括微軟和3Com等公司組成的PPTP論壇開發的一種點對點隧道協，基於撥號使用的PPP協議使用PAP或CHAP之類的加密算法，或者使用 Microsoft的點對點加密算法MPPE。其通過跨越基於 TCP/IP 的數據網絡創建 VPN 實現了從遠程客戶端到專用企業服務器之間數據的安全傳輸。PPTP 支持通過公共網絡(例如 Internet)建立按需的、多協議的、虛擬專用網絡。PPTP 允許加密 IP 通訊，然後在要跨越公司 IP 網絡或公共 IP 網絡(如 Internet)發送的 IP 頭中對其進行封裝。[7]
    > 
    > 2. 第二層隧道協議L2TP〈Layer Two Tunneling Protocol〉：
    > 
    >     L2TP第 2 層隧道協議 (L2TP) 是IETF基於L2F (Cisco的第二層轉發協議)開發的PPTP的後續版本。是一種工業標準 Internet 隧道協議，其可以為跨越面向數據包的媒體發送點到點協議 (PPP) 框架提供封裝。PPTP和L2TP都使用PPP協議對數據進行封裝，然後添加附加包頭用於數據在互聯網絡上的傳輸。PPTP只能在兩端點間建立單一隧道。 L2TP支持在兩端點間使用多隧道，用戶可以針對不同的服務質量創建不同的隧道。L2TP可以提供隧道驗證，而PPTP則不支持隧道驗證。但是當L2TP 或PPTP與IPSEC共同使用時，可以由IPSEC提供隧道驗證，不需要在第2層協議上驗證隧道使用L2TP。 PPTP要求互聯網絡為IP網絡。L2TP只要求隧道媒介提供面向數據包的點對點的連接，L2TP可以在IP(使用UDP)，楨中繼永久虛擬電路 (PVCs),X.25虛擬電路(VCs)或ATM VCs網絡上使用。[7]  
    > 
    > 3. 網際網路安全協定IPsec〈Internet Protocol Security〉：
    > 
    >     IPSec 隧道模式隧道是封裝、路由與解封裝的整個 過程。隧道將原始數據包隱藏(或封裝)在新的數據包內部。該新的數據包可能會有新的尋址與路由信息，從而使其能夠通 過網絡傳輸。隧道與數據保密性結合使用時，在網絡上竊聽通訊的人將無法獲取原始數據包數據(以及原始的源和目標)。封裝的數據包到達目的地後，會刪除封裝，原始數據包頭用於將數據包路由到最終目的地。隧道本身是封裝數據經過的邏輯數據路徑，對原始的源和目的端，隧道是不可見的，而只能看到網絡路徑中的點對點連接。連接雙方並不關心隧道起點和終點之間的任何路由器、交換機、代理服務器或其他安全網關。將隧道和數據保密性結合使用時，可用於提供VPN。封裝的數據包在網絡中的隧道內部傳輸。在此示例中，該網絡是 Internet。網關可以是外部 Internet 與專用網絡間的周界網關。周界網關可以是路由器、防火牆、代理服務器或其他安全網關。另外，在專用網絡內部可使用兩個網關來保護網絡中不信任的通訊。當以隧道模式使用 IPSec 時，其只為 IP 通訊提供封裝。使用 IPSec 隧道模式主要是為了與其他不支持 IPSec 上的 L2TP 或 PPTP VPN 隧道技術的路由器、網關或終端系統之間的相互操作。[7]
    > 
    > 4. 多重通訊協定標籤交換傳輸MPLS〈Multi-Protocol Label Switching〉：
    > 
    >     
    >     多重通訊協定標籤交換傳輸(Multi-Protocol Label Switching)是由IETF 所發展出來的Network Standard。它是實現寬頻網際網路最熱門的技術；其目的是要提供一個更具彈性、擴充性及效率更高的IP層交換技術。MPLS 是一種整合了標籤交換架構與網路層的路由機制的技術，最基本的概念是將進入MPLS Network 的封包(Packet)配置一個固定長度的標籤(Label)，在MPLS Network中Packet會根據標籤(Label) 做Forwarding , 由Label來決定Packet在網路上的路徑，不會再看 Layer 3的 IP Header(標頭)。[8]
    > 
    > 5. 安全通訊協定SSL VPN〈Secure Sockets Layer VPN〉：
    > 
    >     SSL協議提供了數據私密性、端點驗證、信息完整性等特性。SSL協議由許多子協議組成，其中兩個主要的子協議是握手協議和記錄協議。握手協議允許服務器 和客戶端在應用協議傳輸第一個數據字節以前，彼此確認，協商一種加密算法和密碼鑰匙。在數據傳輸期間，記錄協議利用握手協議生成的密鑰加密和解密後來交換 的數據。SSL獨立於應用，因此任何一個應用程序都可以享受它的安全性而不必理會執行細節。SSL置身於網絡結構體系的 傳輸層和應用層之間。此外，SSL本身就被幾乎所有的Web瀏覽器支持。這意味著客戶端不需要為了支持SSL連接安裝額外的軟件。這兩個特徵就是SSL能 應用於VPN的關鍵點。[7]
    > 
    > ---
    > 
    > __VPN Gate__
    > 
    > VPN Gate 學術實驗專案是一個線上服務，由日本國立築波大學研究生院為學術研究目的運營。研究的目的是推廣 "全球分散式公共 VPN 中繼伺服器" 的知識。而VPN Gate 的伺服器是由世界各地的志願者所提供的，而它有以下幾個優點：
    > [6]
    > 
    > ![](https://sites.google.com/site/vpnjianjieyuqiyingyong/_/rsrc/1420447599449/vpn-shi-zuo/vpngate/%E5%9C%96%E7%89%871.png)
    > 
    > 1. 任何平台與作業系統都可以使用，包括Window、Mac、Android‧‧‧等。
    > 2. 支援SSL VPN、L2TP/IPsec、Open VPN、Microsoft SSTP 多項協議技術。
    > 3. 無須註冊帳號，直接使用。
    > 
    > 它並不是只有優點，還有幾點要注意的：
    > 
    > 1. 每個VPN伺服器的IP是不固定的，IP地址會不定期更換。
    > 2. 每天的VPN伺服器數量會不一樣，這要看志願者有沒有開放。
    > 3. 使用VPN Gate 盡量不要傳輸信用卡之類的個人機密數據。
    > 4. 使用時盡量不要用太多流量。
    > 
    > 上面第三點的原因是因為不知道你連的VPN伺服器有沒有問題，在使用中盡量不要上網刷卡買東西之類的，VPN雖然安全，但是不能防VPN內部網路出現的問題。而對於第四點，是因為你連的是志願者所提供的伺服器，用的流量是你所連的伺服器的，所以不要用太多流量。接下來我要介紹VPN Gate 要如何使用。
    > 
    > ![](https://sites.google.com/site/vpnjianjieyuqiyingyong/_/rsrc/1420448243702/vpn-shi-zuo/vpngate/123.png)
    > 
    > 這是進到VPN Gate 官網〈[http://www.vpngate.net/ja/](http://www.vpngate.net/ja/)〉後看到的畫面，先選擇你想要連的國家，之後再選擇你要的連接方法即可。下幾篇會介紹如何連接。
    >     
    >     

- [Can I make a computer connecting via VPN visible to computers within the network it is connecting to? - Server Fault](https://serverfault.com/questions/130014/can-i-make-a-computer-connecting-via-vpn-visible-to-computers-within-the-network)

    > By definition, once you set up a VPN you are part of the remote network; if you examine your network interfaces, you'll see you have a new one, which is your VPN interface and has an IP address belonging to the remote network; this is the IP address you must connect to from the remote machine.
    > 
    > If your network is 192.168.1.x and your local IP address is 192.168.1.2, and the remote network is 10.0.0.x and the remote machine is 10.0.0.10, when you establish a VPN connection you will acquire a new virtual network interface, which will have an address like 10.0.0.42; you should connect to this one, not to 192.168.1.2, which just doesn't exist from the remote network's point of view.
    > 
    > So, if from 10.0.0.10 you try to connect to 192.168.1.2, it will not (ordinarily) work; if you instead connect to 10.0.0.42, it should work.
    > 
    > If it doesn't, then either you have a local firewall on your system which doesn't accept connections on the VPN interface, or the VPN server is configured to not let you talk to remote machines and/or not let remote machines talk to you.
    > 


## HTTPS/SSL certificate

- [NGINX 使用 Let’s Encrypt 免費 SSL 憑證設定 HTTPS 安全加密網頁教學 - G. T. Wang](https://blog.gtwang.org/linux/secure-nginx-with-lets-encrypt-ssl-certificate-on-ubuntu-and-debian/)

- [SSL For Free 免費 SSL 憑證申請，使用 Let's Encrypt 最簡單方法教學！](https://free.com.tw/ssl-for-free/)

- [SSL For Free - Free SSL Certificates in Minutes](https://www.sslforfree.com/)

## 分散式 distributed network

- [Are there any Distributed/mesh-like/P2P VPNs? - Server Fault](https://serverfault.com/questions/685820/are-there-any-distributed-mesh-like-p2p-vpns)

    > I'm not sure whether it completely fulfils your needs, but you should probably take a look at tinc: [http://www.tinc-vpn.org/](http://www.tinc-vpn.org/). It quite closely matches the mesh network orchestrated by a central server as you described, but I'm not sure whether it will succeed in discovering peers in your local network.
    > 
    > ---
    > 
    > The easiest mesh vpn I have found and used is PeerVPN ([http://www.peervpn.net/](http://www.peervpn.net/)).
    > 
    > PeerVPN Features
    > 
    > - Ethernet tunneling support using TAP devices.
    > - IPv6 support.
    > - Full mesh network topology.
    > - Automatically builds tunnels through firewalls and NATs without any further setup (for example, port forwarding).
    > - Shared key encryption and authentication support.
    > 
    > Configuration is simple.. one config file you edit and for basic mesh vpn there are only 6 settings you need to specify see the PeerVPN tutorial which is only 1 page: [http://www.peervpn.net/tutorial/](http://www.peervpn.net/tutorial/)
    > 
    > The PSK encryption/authentication key can be upto 512 bits (64 bytes).
    > 
    > I've set peervpn up so far on multiple remote servers and it works very well. Also, there is no requirement for a "super-node" as you may encounter in other mesh vpn implementations.
    > 
    > Nodes in peervpn learn about newly added nodes to the VPN automatically w/no need to change configurations. Node to node traffic is also direct and not thru some central vpn hub.
    > 
    > Note: read the default peervpn.conf file to learn about alot of other options you "can" take advantage of. But for the basic mesh vpn as I stated you only need to set 6 options (name of vpn, PSK, local tunnel end point IP address, interface "name" you want to see/use on your linux system & port number to use for "that" vpn ... note you can use peervpn for multiple independent VPNs on a server)
    > 
    > ---
    > 
    > I had the exact same problem years ago. I had ~30 offices that all needed to be able to directly communicate, but they were set up in a 'hub-and-spoke' configuration. I wrote a tool in Python to automatically generate the n x (n-1)/2 number of connections in OpenVPN between the offices. Later on I added in support for RIP routing between the sites after a bizarre Comcast issue where one office could see all the others, but not the main office. Finally I added the ability to auto-generate reverse DNS for the link IPs and the ability to push the packages out to each router.
    > 
    > Take a look at [OpenMesher](https://github.com/heyaaron/openmesher/). Just this morning I decided to dust it off for an upcoming project. Hopefully it does what you want. If not, feel free to submit an issue and I'll help.
    > 

### IPOP

- [ipop-project/ipop-project.github.io: Current Wiki and Documentation for IPOP](https://github.com/ipop-project/ipop-project.github.io)

- [IPOP (IP-Over-P2P) - IPOP](http://ipop-project.org/)

    > IPOP (IP-Over-P2P) is an open-source user-centric software virtual network allowing end users to define and create their own virtual private networks (VPNs). IPOP virtual networks provide end-to-end tunneling of IP or Ethernet over Tincan links setup and managed through a control API to create various software-defined VPN overlays.
    > Unique Features
    > 
    > - In contrast to typical VPN technologies, which require complex setup, management and a gateway to relay VPN traffic, IPOP is straightforward to configure, because:
    > - It runs on existing Internet infrastructure, without requiring any specialized networking infrastructure (e.g. hardware switches/routers, or virtual routers);
    > - It uses online social network (OSN) infrastructures to allow users to define their own networks;
    > - It seamlessly traverses firewalls, NATs, and create VPN tunnels in a peer-to-peer fashion, avoiding the need for centralized VPN gateways.
    > 

- [IPOP (IP-over-P2P) Virtual Network Tutorial | FutureSystems Portal](https://portal.futuresystems.org/tutorials/ipop1)

- [Tutorial: Deploying Your Own P2P Overlay for IPOP VPNs | FutureSystems Portal](https://portal.futuresystems.org/tutorials/ipop2)


### meshbird

- [meshbird/meshbird: Distributed private networking](https://github.com/meshbird/meshbird)

### n2n

- [Tech黑手 - 工作雜記: n2n - P2P VPN](https://chunchaichang.blogspot.tw/2010/04/n2n-p2p-vpn.html)

    > n2n - 這是一個開源的 P2P VPN 套件，由知名也是開源的網管軟體-ntop 的作者所開發，軟體特色有：
    > 
    > - 開放原始碼的套件
    > - 建立連線時毋需通過第三方的主機認證
    > - 可獨立運作，無須仰賴官方主機的介接， 安全性高。
    > - 可適用 NAT 防火牆環境。
    > - 可建立多個n2n網路組。
    > - 容易安裝及使用。
    > - 如果使用公用的 supernode，則所有的node 都不需要佔用到 public IP。
    > - 不需要建立 central server，各 node 之間即可以作連線。

### ZeroTier

- [在Linux容器中使用ZeroTier P2P VPN | Soul Of Free Loop](https://zohead.com/archives/zerotier-container/)

    > 关于 ZeroTier P2P VPN
    > 
    > P2P VPN 和我们平常使用的 PPTP、OpenVPN 等 VPN 的不同之处在于其只负责将两个或多个主机通过点对点的方式进行连接，不需要中心服务器支持，多个主机之间通过 STUN 打洞或者 TURN 中继等方式进行连接，比较适合不同网络间的多个主机进行直接连接，不像 PPTP 这种在国内用的最多的就是拿来爬墙的。
    > 
    > 目前使用的比较多的包括 n2n、tinc 和本文要介绍的 ZeroTier 等几种免费开源的 P2P VPN 软件。
    > 
    > n2n 由于已经没人继续开发支持了所以不予考虑，我在对比了 tinc 和 ZeroTier 之后发现 ZeroTier 虽然看起来性能比 tinc 略差一点，但其客户端配置步骤非常简单，不需要像 tinc 那样要在多个主机分别手工生成配置文件，而且 ZeroTier 自己也自带了几个不同国家区域的中继服务器方便普通用户使用，另外一点就是本文要介绍的 ZeroTier 支持在 Linux 容器中使用，因此平时我主要使用 ZeroTier，tinc 用作辅助。
    > 


### SoftEther

- [SoftEther VPN Open Source - SoftEther VPN Project](https://www.softether.org/)


### Private Tor Network

- [antitree/private-tor-network: Run an isolated instance of a tor network in Docker containers](https://github.com/antitree/private-tor-network)

### Tinc

- [Tinc VPN](https://www.tinc-vpn.org/)

    > What is tinc?
    > 
    > tinc is a Virtual Private Network (VPN) daemon that uses tunnelling and encryption to create a secure private network between hosts on the Internet. tinc is Free Software and licensed under the GNU General Public License version 2 or later. Because the VPN appears to the IP level network code as a normal network device, there is no need to adapt any existing software. This allows VPN sites to share information with each other over the Internet without exposing any information to others. In addition, tinc has the following features:
    > 
    > - Encryption, authentication and compression
    > All traffic is optionally compressed using zlib or LZO, and LibreSSL or OpenSSL is used to encrypt the traffic and protect it from alteration with message authentication codes and sequence numbers.
    > 
    > - Automatic full mesh routing
    > Regardless of how you set up the tinc daemons to connect to each other, VPN traffic is always (if possible) sent directly to the destination, without going through intermediate hops.
    > 
    > - NAT traversal
    > As long as one node in the VPN allows incoming connections on a public IP address (even if it is a dynamic IP address), tinc will be able to do NAT traversal, allowing direct communication between peers.
    > 
    > - Easily expand your VPN
    > When you want to add nodes to your VPN, all you have to do is add an extra configuration file, there is no need to start new daemons or create and configure new devices or network interfaces.
    > 
    > - Ability to bridge ethernet segments
    > You can link multiple ethernet segments together to work like a single segment, allowing you to run applications and games that normally only work on a LAN over the Internet.
    > 
    > - Runs on many operating systems and supports IPv6
    > Currently Linux, FreeBSD, OpenBSD, NetBSD, OS X, Solaris, Windows 2000, XP, Vista and Windows 7 and 8 platforms are supported. See our section about supported platforms for more information about the state of the ports. tinc has also full support for IPv6, providing both the possibility of tunneling IPv6 traffic over its tunnels and of creating tunnels over existing IPv6 networks.
    > 


## 翻牆

- [cms88168/docker-ShadowsocksR: ShadowsocksR Server (https://github.com/breakwa11/shadowsocks/tree/manyuser) for Docker](https://github.com/cms88168/docker-ShadowsocksR)

- [第一次用 Docker 自架 v2ray + shadowsocks 翻牆伺服器就上手](https://blog.birkhoff.me/use-docker-to-deploy-vmess-and-ss-using-docker/)

- [breakwa11/shadowsocksr - Docker Hub](https://hub.docker.com/r/breakwa11/shadowsocksr/)

### zeronet

- [HelloZeroNet/ZeroNet: ZeroNet - Decentralized websites using Bitcoin crypto and BitTorrent network](https://github.com/HelloZeroNet/ZeroNet)










