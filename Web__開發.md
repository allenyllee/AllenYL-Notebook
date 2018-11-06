# Web__開發

[toc]
<!-- toc --> 


## 前後端 tutorial


- [Half-Stack Developer 養成計畫 系列文章列表 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/users/20091346/ironman/1150?page=1)

### 簡單留言板(無資料庫)

- [想～簡簡單單愛：超簡單留言板 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10187442)

### 一般留言板(有資料庫)

- [沒那麼簡單～的留言板 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10187673)



## utf8 解編碼

- [URL編碼 | URL解碼](https://www.ifreesite.com/urldecoderencoder.htm)



## Content Management Framework

- [Strapi - Node.js REST API Framework with extensible Admin Panel.](https://strapi.io/)


# 前端

## ReactJS vs Angular5 vs Vue.js

- [ReactJS vs Angular5 vs Vue.js — What to choose in 2018?](https://medium.com/@TechMagic/reactjs-vs-angular5-vs-vue-js-what-to-choose-in-2018-b91e028fa91d)




# webserver

## apache

### run different website in a same domain with HTTP and HTTPS

- [VirtualHost Examples - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/vhosts/examples.html)

- [wordpress - How to run different website in a same domain with HTTP and HTTPS - Stack Overflow](https://stackoverflow.com/questions/47119307/how-to-run-different-website-in-a-same-domain-with-http-and-https)

    > You can do this in your [virtual host configuration](https://httpd.apache.org/docs/2.4/vhosts/examples.html):
    > 
    > ```
    > Listen 80
    > Listen 443
    > 
    > <VirtualHost *:80>
    >     ServerName example.com
    >     DocumentRoot "/path/to/wordpress"
    > </VirtualHost>
    > 
    > <VirtualHost *:443>
    >     ServerName example.com
    >     DocumentRoot "/path/to/laravel/public"
    > </VirtualHost>
    > ```
    > 
    > You may also need to define directories if the sources are not under your default http root. For example:
    > 
    > ```
    > <VirtualHost *:443>
    >     ServerName example.com
    >     DocumentRoot "/path/to/laravel"
    >     <Directory /path/to/laravel>
    >           AllowOverride All
    >     </Directory>
    > </VirtualHost>
    > ```
    > 
    > This will also allow Apache to serve that directory and use any .htaccess files (if it wasn't allowed already).
    > 
    > ---
    > 
    > What you set as a server name in each configuration is up to you. The webserver will respond to requests on that port requesting the specific server name. -- [apokryfos](https://stackoverflow.com/users/487813/apokryfos "16,579 reputation") [Nov 5 '17 at 11:21](https://stackoverflow.com/questions/47119307/how-to-run-different-website-in-a-same-domain-with-http-and-https#comment81191510_47120431)
    > 




## nginx

### 設定 https 連線

- [XYZ的筆記本: Nginx 設定 https 連線](https://xyz.cinc.biz/2017/06/nginx-https-ssl.html)

    > 假設要自己發憑證給網站。
    > 
    > 先建立放SSL憑證的資料夾
    > ```sh
    > $ mkdir /etc/nginx/ssl
    > ```
    > 
    > 產生網站的私鑰、證書。\
    > example.com.key：私鑰(private key)\
    > example.com.crt：證書(certificate)\
    > (其中 -nodes 參數，表示不對 private key 加密，避免每次啟動 nginx 需要輸入密碼。)
    > ```
    > $ openssl req -x509 -nodes -days 3650  -newkey rsa:2048  -keyout /etc/nginx/ssl/example.com.key -out  /etc/nginx/ssl/example.com.crt
    > ```
    > (再來填寫一些基本的資料，即可產生example.com.key、example.com.crt 兩個檔)
    > ```
    > Country  Name  (2 letter code)  [XX]:  State  or  Province  Name  (full name)  []:  Locality  Name  (eg, city)  [Default  City]:  Organization  Name  (eg, company)  [Default  Company  Ltd]:  Organizational  Unit  Name  (eg, section)  []:  Common  Name  (eg, your name or your server's hostname) []:
    > Email Address []:
    > ```
    > 在 nginx 網站設定檔加入監聽 443 SSL 設定、與指定憑證位置(原本 listen 80 可保留共存)
    > ```
    > #SSL listen 443 ssl; ssl_certificate /etc/nginx/ssl/example.com.crt; ssl_certificate_key /etc/nginx/ssl/example.com.key;
    > ```
    > 重新讀取設定
    > ```
    > $ systemctl reload nginx
    > ```
    > 若有設定防火牆，設定防火牆允許 https(443 port) 通行，
    > ```
    > $ firewall-cmd --permanent --zone=public  --add-service=https
    > $ firewall-cmd --reload
    > $ firewall-cmd --list-all --zone=public
    > ```
    > **其他：**
    > 
    > -   若「listen 443 ssl;」只寫「listen 443;」，缺了「 ssl」
    >     Chromw 會出現錯誤訊息：「net::ERR_SSL_PROTOCOL_ERROR」
    >     Firefox 會出現錯誤訊息：「SSL 收到含超出最大允許字串長度的記錄。 錯誤代碼: SSL_ERROR_RX_RECORD_TOO_LONG」
    >     參考：<http://serverfault.com/q/605215>
    > -   加 -nodes 參數，不對 private key 加密，產生的檔案內容格式：
    > 
    > example.com.key(私鑰)
    > 
    > ```
    > -----BEGIN PRIVATE KEY-----
    > MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQDeicw2jouYIdb3
    > +re2QwHGWfrAs7+6gdvPzbsZAX+1MaB5CulMOlqTW5R/xJCTyBRegdpc9Oq8Ufsz
    > Nkp5EyABT/1kdACh8HBUd4emaRDdng8nkxi4m9bFuPvDV3eV9b1c44a/PoDrk5Ks
    > .....  
    > GToHKxAElC0nvdYRlTgmm4Gh2AbzaB7uhEkDd8ifuCAt4SssMu0MWvxXgUHNaJKc
    > EVg8zxwJUnHotFVsQajaiVYnMDaMYoMe3PeUjIs5EK5ueEJnlB/jBYYlH6haVN2m
    > CrOa1VRvAkRmWKUAzMObreEm  
    > -----END PRIVATE KEY-----
    > ```
    > 
    > example.com.crt(證書)
    >     
    > ```
    > -----BEGIN CERTIFICATE-----  
    > MIIDkzCCAnugAwIBAgIJAJZQ6uDkx3pPMA0GCSqGSIb3DQEBCwUAMGAxCzAJBgNV  
    > BAYTAmFhMQswCQYDVQQIDAJhYTELMAkGA1UEBwwCYWExCjAIBgNVBAoMAWExCzAJ  
    > ..... 
    > pKE6/3wZ4SXio4oLKFGziBGqg+5kxzla2fb1PDUNRbmyQEzB+ZFtFgVHcgXU55ff 
    > bLprWdbDn4bldhEyl9UHWfwlOs0M6g6yfnc7zmJUxrZ5
    > qmMmMhbkZJ4X30LUYZif Vgo4FV3Ujg==  
    > -----END CERTIFICATE-----
    > ```
    > 
    > -   有加 -nodes 參數，對 private key 加密，產生的檔案內容格式：
    > 
    > example.com.key(私鑰)
    > 
    > ```
    > -----BEGIN ENCRYPTED PRIVATE KEY-----  
    > MIIFDjBABgkqhkiG9w0BBQ0wMzAbBgkqhkiG9w0BBQwwDgQIwU2mXoH/UvICAggA  
    > MBQGCCqGSIb3DQMHBAgnLQEy2LhjSQSCBMiq040M9Ryl5ygXVvNorGkttO3wK0Tl 
    > uRRRZJplhQVBc09zm0N2HyjO93wZPnVycrI2n6m04w0IMSsc6IpbOaflqwcKN7xG 
    > .....  
    > 37mVxQx45mN7f8im23uJDNs5n29yexc21YzaEaP5BNwBpJrJtNAVR0p63h+LRhGJ  
    > ByA24Brmys/RE5xpYkqtp4V47aJcIwYgy4LSyWW6ITGYRMq9FlaziUjyFpEaddIc
    > ho8=  
    > -----END ENCRYPTED PRIVATE KEY-----
    > ```
    > 
    > example.com.crt(證書)
    >     
    > ```
    > -----BEGIN CERTIFICATE-----  
    > MIIDlTCCAn2gAwIBAgIJAIT9a7cvK/EpMA0GCSqGSIb3DQEBCwUAMGExCzAJBgNV  
    > BAYTAmFhMQswCQYDVQQIDAJhYTELMAkGA1UEBwwCYWExCzAJBgNVBAoMAmFhMQsw  
    > ..... 
    > FT9xCMZp+Z6n6LwWdBWkJ1mASwkxgRDKZzSBaiRN35pT/JSbUqwGH8etD8QMXBBq  
    > CqiTJM/D3X6YMpKInKnFV7Z/qAQqpcfYYPzBLNAosOmUkUBVYxwtKbUxNoPJDMQi
    > kEzWv9Oc5VNC 
    > -----END CERTIFICATE-----
    > ```
    > 
    > -   查看 example.com.crt 證書內容
    > 
    > ```
    >     $ openssl x509 -in example.com.crt -text -noout
    > ```
    > 
    > 參考：[DER vs. CRT vs. CER vs. PEM Certificates and How To Convert Them](http://info.ssl.com/article.aspx?id=12149)
    >     
    > -   A certificate contains a public key\
    >     參考：[What is the difference between a certificate and a key with respect to SSL? - Super User](https://superuser.com/a/620124)
    > -   TLS：Transport Layer Security\
    >     SSL：Secure Socket Layer\
    >     .key：私鑰。\
    >     .csr：Certificate Signing Request 證書簽名請求，像憑證機構申請憑證時，給憑證機構的檔案。\
    >     .crt：Certificate，證書。\
    >     X.509：一種證書格式。一般 .crt 附檔名。BASE64編碼(apache、linux)：.pem。二進位編碼(windows、Java)：.der。\
    >     參考：[openssl、x509、crt、cer、key、csr、ssl、tls 这些都是什么鬼? - 菩提树下的杨过 - 博客园](http://www.cnblogs.com/yjmyzz/p/openssl-tutorial.html)
    > -   一般向憑證機構申請憑證流程：\
    >     「產生 public key(CSR)、private key」-->「public key(CSR)給憑證機構簽署認証」-->「憑證機構回覆簽署後的 Certificate(證書、CRT)」\
    >     參考：[SSL憑証(SSL certificate)的原理 - 知識庫 - 無限空間,虛擬主機,網域註冊,網域管理](http://support.unethost.com/knowledgebase.php?action=displayarticle&id=82)
    >     
    >     
    > **查 openssl 指令：**
    > ```
    > $ openssl -h (輸入不存在的指令，例如  -h，會列出可用指令) $ openssl req -h
    > $ man openssl
    > $ man req
    > $ man x509
    > ```
    > 



### Configuring HTTPS servers

- [Configuring HTTPS servers](https://nginx.org/en/docs/http/configuring_https_servers.html#single_http_https_server)

    > #### A single HTTP/HTTPS server
    > 
    > It is possible to configure a single server that handles both HTTP and HTTPS requests:
    > 
    > > server {
    > >     listen              80;
    > >     listen              443 ssl;
    > >     server_name         www.example.com;
    > >     ssl_certificate     www.example.com.crt;
    > >     ssl_certificate_key www.example.com.key;
    > >     ...
    > > }
    > 
    > > Prior to 0.7.14 SSL could not be enabled selectively for individual listening sockets, as shown above. SSL could only be enabled for the entire server using the [ssl](https://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl) directive, making it impossible to set up a single HTTP/HTTPS server. The `ssl` parameter of the [listen](https://nginx.org/en/docs/http/ngx_http_core_module.html#listen) directive was added to solve this issue. The use of the [ssl](https://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl) directive in modern versions is thus discouraged.
    > 
    > #### Name-based HTTPS servers
    > 
    > A common issue arises when configuring two or more HTTPS servers listening on a single IP address:
    > 
    > > server {
    > >     listen          443 ssl;
    > >     server_name     www.example.com;
    > >     ssl_certificate www.example.com.crt;
    > >     ...
    > > }
    > >
    > > server {
    > >     listen          443 ssl;
    > >     server_name     www.example.org;
    > >     ssl_certificate www.example.org.crt;
    > >     ...
    > > }
    > 
    > With this configuration a browser receives the default server's certificate, i.e. `www.example.com` regardless of the requested server name. This is caused by SSL protocol behaviour. The SSL connection is established before the browser sends an HTTP request and nginx does not know the name of the requested server. Therefore, it may only offer the default server's certificate.
    > 
    > The oldest and most robust method to resolve the issue is to assign a separate IP address for every HTTPS server:
    > 
    > > server {
    > >     listen          192.168.1.1:443 ssl;
    > >     server_name     www.example.com;
    > >     ssl_certificate www.example.com.crt;
    > >     ...
    > > }
    > >
    > > server {
    > >     listen          192.168.1.2:443 ssl;
    > >     server_name     www.example.org;
    > >     ssl_certificate www.example.org.crt;
    > >     ...
    > > }
    > 
    > #### An SSL certificate with several names
    > 
    > There are other ways that allow sharing a single IP address between several HTTPS servers. However, all of them have their drawbacks. One way is to use a certificate with several names in the SubjectAltName certificate field, for example, `www.example.com` and `www.example.org`. However, the SubjectAltName field length is limited.
    > 
    > Another way is to use a certificate with a wildcard name, for example, `*.example.org`. A wildcard certificate secures all subdomains of the specified domain, but only on one level. This certificate matches `www.example.org`, but does not match `example.org` and `www.sub.example.org`. These two methods can also be combined. A certificate may contain exact and wildcard names in the SubjectAltName field, for example, `example.org` and `*.example.org`.
    > 
    > It is better to place a certificate file with several names and its private key file at the *http* level of configuration to inherit their single memory copy in all servers:
    > 
    > > ssl_certificate     common.crt;
    > > ssl_certificate_key common.key;
    > >
    > > server {
    > >     listen          443 ssl;
    > >     server_name     www.example.com;
    > >     ...
    > > }
    > >
    > > server {
    > >     listen          443 ssl;
    > >     server_name     www.example.org;
    > >     ...
    > > }


### HTTPS serving with same config as HTTP

- [nginx HTTPS serving with same config as HTTP - Server Fault](https://serverfault.com/questions/10854/nginx-https-serving-with-same-config-as-http)

    > You can combine this into one server block like so:
    > 
    > ```
    > server {
    >     listen 80;
    >     listen 443 default_server ssl;
    > 
    >     # other directives
    > }
    > 
    > ```
    > 
    > [Official How-To](http://nginx.org/en/docs/http/configuring_https_servers.html#single_http_https_server)
    > 

### Error code: ssl_error_rx_record_too_long

- [linux - Error code: ssl_error_rx_record_too_long - Server Fault](https://serverfault.com/questions/497430/error-code-ssl-error-rx-record-too-long)

Solved. You need to add "ssl" to the end of the listen.

```
listen       443 ssl;

```


# elasticsearch

## Course

- [Android Classifieds App Course with Firebase and ElasticSearch - YouTube](https://www.youtube.com/playlist?list=PLgCYzUzKIBE-G0tuxjKGkl_keIW2FFwKX)

