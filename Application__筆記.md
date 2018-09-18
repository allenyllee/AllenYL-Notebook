# Application__筆記

[toc]
<!-- toc --> 

# Firefox

## my settings

### Do not load pinned tabs on launch until selected

- [Do not load pinned tabs on launch until selected - config not working | Firefox 技術支援討論區 | Mozilla 技術支援](https://support.mozilla.org/zh-TW/questions/1016880)

```
browser.sessionstore.restore_pinned_tabs_on_demand;true
```

### Load link in background tab

```
browser.tabs.loadDivertedInBackground;true
```

### Search in new tab

```
browser.search.openintab;true
```

### open newtab from url bar

- [How to make Firefox 57 to always open new tab from address bar? - Super User](https://superuser.com/questions/1269934/how-to-make-firefox-57-to-always-open-new-tab-from-address-bar)


```
browser.urlbar.openintab;true
```

### closeing tab policy

```
browser.tabs.selectOwnerOnClose;true
```

### mousewheel 1

- [How to change the tab scroll speed in FF Quantum : firefox](https://www.reddit.com/r/firefox/comments/73q8t0/how_to_change_the_tab_scroll_speed_in_ff_quantum/)

- [Enable Firefox's Secret Mousewheel Scrolling Acceleration](https://lifehacker.com/5458328/enable-firefoxs-secret-mousewheel-scrolling-acceleration)


```
general.smoothScroll.mouseWheel.durationMaxMS = 600
general.smoothScroll.mouseWheel.durationMinMS = 400
mousewheel.acceleration.factor;30
mousewheel.acceleration.start;7
mousewheel.default.delta_multiplier_y = 150
```

### mousewheel 2
```
general.smoothScroll.mouseWheel.durationMaxMS;300 #(滾輪一格的延遲時間, 適合細看文章時慢慢滾動, 太長會覺得移動一小格要很久才會停, 太短會覺得中間的字一下就滑過去眼睛跟不上)
general.smoothScroll.mouseWheel.durationMinMS;250 #(滾動多格的延遲時間, 適合概略掃過全篇文章, 快速捲動到目標, 時間太長會覺得反應遲鈍, 沒辦法一直滾一直滾, 太短畫面又捲太快, 眼睛跟不上)
mousewheel.acceleration.factor;10 #(加速的倍數, 適合想要一次滑動到頁面底部)
mousewheel.acceleration.start;7 #(啟動加速所需移動的格數, 7格比較不容易誤觸發)
mousewheel.default.delta_multiplier_y;150 #(單格移動的距離)
```

### youtube lag

- [Firefox is really lagging on youtube : firefox](https://www.reddit.com/r/firefox/comments/74mxjk/firefox_is_really_lagging_on_youtube/)

    > All of youtube started being really slow for me a few months ago but I recently found that a add-on called block unreachable scripts that made me it run great
    > 
    > <https://addons.mozilla.org/en-US/firefox/addon/block-unreachable-scripts/?src=api>
    > 

- [Updated firefox and now computer is slow and videos on youtube do not work. | Firefox 技術支援討論區 | Mozilla 技術支援](https://support.mozilla.org/zh-TW/questions/1189173)



```
layers.acceleration.force-enabled;true
layers.gpu-process.enabled;true
media.windows-media-foundation.use-nv12-format;true
```


## keyboard shortcut

### go back to the previous tab

- [What is the Keyboard shortcut to go back to the previous tab (I mean most recent tab)? | Firefox 技術支援討論區 | Mozilla 技術支援](https://support.mozilla.org/zh-TW/questions/851489)

    > `CTRL + Tab` key -> for Switching to Next tab
    > `CTRL + SHIFT + Tab` key -> for Switching Back to Previous Tab
    > 
    > ***
    > You can set the pref `browser.ctrlTab.previews` to true on the `about:config` page.

## settings page


### extension id
```
about:support
```

### memory usage
```
about:memory
```

## addon settings

### lazy scholar
```
userid: 226242
```

### Select After Closing Current
```
* 右側 子標籤頁
* 右側 同級標籤頁
* 右側 標籤頁
* 最近訪問標籤頁
```

### Load Background Tabs Lazily

```
* position where new tabs are opened: `relatedAfterCurrent`
* tab removal delay: 1000 (milliseconds)
* make block tabs session proof
* place a time limit of 60 seconds on a loading tab.
* display the number of tabs in the line on the paused button badge
```


## appearence

### Custom CSS tweaks for Firefox Quantum (57+) 

- [Aris-t2/CustomCSSforFx at 1.2.9](https://github.com/Aris-t2/CustomCSSforFx/tree/1.2.9)

    > WebExtensions can not modify browsers appearance in Firefox 57+
    > ---------------------------------------------------------------\
    > The only way to modify ui is adding custom CSS code to **userChrome.css** and **userContent.css** files inside browsers profile folder.\
    > Keep in mind CSS code can not create entirely new items, buttons or toolbars. It only can modify already present ui items.



## check if multiprocess e10s option is enabled

- [Firefox 開啟 multi-process（e10s）的方法及感想 | 婉麗河畔旁](https://kreen.org/2078/firefox-multi-process-e10s)

- [How to check if multiprocess e10s option is enabled in your Firefox - Super User](https://superuser.com/questions/1096974/how-to-check-if-multiprocess-e10s-option-is-enabled-in-your-firefox)

    > Open the site `about:support` in Firefox, which indicates if e10s is enabled.
    > 
    > There is a line "Multi-process staged rollout", which would be set to `true` if e10s is enabled. Also look for a number higher than 0 in the "Multiprocess Windows" entry.
    > 
    > e.g., accessibility, add-ons can trigger disabling this feature.
    > 
    > On this site you can check, if add-ons, you are using are compatible: <http://arewee10syet.com/>. There is also a [mozilla site to check compatibility](https://compatibility-lookup.services.mozilla.com/), you find the addon-id in the extension-filenames in your profile folder, for example the "Tab Groups" add-on has the id `tabgroups@quicksaver` and is incompatible with e10s.
    > 
    > If you would like to opt-in to test the feature anyway, open `about:config` and toggle `browser.tabs.remote.autostart` to `true`. On your next restart, e10s should be active.
    > 
    > ### Force Enable
    > 
    > If you've tried enabling e10s but about:support indicates that e10s is disabled (e.g., accessibility, add-ons can trigger this), you can force e10s on for testing purposes. Within `about:config` create a new `boolean` pref named `browser.tabs.remote.force-enable` and set it to `true`. This is not encouraged, use it at your own risk!
    > 
    > (I tried it anyway and it worked, even with Tab Groups Addon still enabled but it's risky!)
    > 
    > *Source: <https://wiki.mozilla.org/Electrolysis#Force_Enable>*



## Enable WebGL

- [1365492 – Firefox refuses to use my nvidia GPU, it uses the intel integrated GPU instead](https://bugzilla.mozilla.org/show_bug.cgi?format=default&id=1365492)

    Just so that we're on the same page, I'm assuming you're in Nvidia control panel, and in the Manage 3D Settings->Program settings, you find Mozilla Firefox (firefox.exe) and set the preferred graphics processor to High-performance Nvidia processor.


- [How can I enable WebGL in my browser? - Super User](https://superuser.com/questions/836832/how-can-i-enable-webgl-in-my-browser)

    > Firefox
    > 
    > First, enable WebGL:
    > 
    >     Go to about:config
    >     Search for webgl.disabled
    >     Ensure that its value is false (any changes take effect immediately without relaunching Firefox)
    > 
    > Then inspect the status of WebGL:
    > 
    >     Go to about:support
    >     Inspect the WebGL Renderer row in the Graphics table:
    >         If the status contains a graphics card manufacturer, model and driver (eg: "NVIDIA Corporation -- NVIDIA GeForce GT 650M OpenGL Engine"), then WebGL is enabled.
    >         If the status is something like "Blocked for your graphics card because of unresolved driver issues" or "Blocked for your graphics driver version", then your graphics card/driver is blacklisted.
    > 
    > If your graphics card/drivers are blacklisted, you can override the blacklist. Warning: this is not recommended! (see blacklists note below). To override the blacklist:
    > 
    >     Go to about:config
    >     Search for webgl.force-enabled
    >     Set it to true
    > 
    > (Like Chrome, Firefox has a Use hardware acceleration when available checkbox, in Preferences > Advanced > General > Browsing. However, unlike Chrome, Firefox does not require this checkbox to be checked for WebGL to work.)
    > 


## Disable content security policy

- [javascript - How to override content security policy while including script in browser JS console? - Stack Overflow](https://stackoverflow.com/questions/27323631/how-to-override-content-security-policy-while-including-script-in-browser-js-con)

    > You can turn off the CSP for your entire browser in Firefox by disabling `security.csp.enable` in the `about:config` menu.
    > 


## HTTP Strict Transport Security (HSTS)

### clear https cache so that you can link to http without redirect to https

- [How to clear HSTS settings in Chrome and Firefox](https://www.thesslstore.com/blog/clear-hsts-settings-chrome-firefox/)

    > A quick look at what HSTS is and how to clear it on two of the most popular browsers.
    > -------------------------------------------------------------------------------------
    > 
    > HSTS stands for HTTP Strict Transport Security, it's a web security policy mechanism that forces web browsers to interact with websites only via secure HTTPS connections (and never HTTP). This helps to prevent protocol downgrade attacks and cookie hijacking.
    > 
    > HSTS was originally created in response to a vulnerability that was introduced by Moxie Marlinspike in a 2009 BlackHat Federal talk titled "New Tricks for Defeating SSL in Practice." The particular vulnerability that HSTS defends against is the one illustrated by Marlinspike's SSLStrip tool.
    > 
    > Essentially the tool works by converting secure HTTPS connections back to unsecured HTTP ones. HSTS remedies this by communicating to the browser that an HTTPS connection should always be in place. HSTS can also help to prevent cookie-based login credentials from being stolen by common tools such as Firesheep.
    > 
    > Unfortunately, some HSTS settings can inadvertently cause browser errors. For instance, if you're using Chrome, you might run into:
    > 
    > **"Privacy error: Your connection is not private" (NET::ERR_CERT_AUTHORITY_INVALID).**
    > 
    > If you attempt to reach the same site on another browser and don't run into the same issues, it could just be a problem with how the HSTS settings have affected your original browser. In that case, you will need to clear them. Here's how to clear HSTS settings on Google Chrome and Mozilla Firefox.
    > 
    > Clear and Forget HSTS Settings In Popular Browsers.
    > ---------------------------------------------------
    > 
    > If your browser has stored HSTS settings for a domain and you later try to connect over HTTP or a broken HTTPS connection (mis-match hostname, expired certificate, etc) you will receive an error. Unlike other HTTPS errors, [HSTS-related errors cannot be bypassed](https://subdomain.preloaded-hsts.badssl.com/). This is because the browser has received explicit instructions from the browser not to allow anything but a secure connection.
    > 
    > HSTS settings include a "max-age" option, which tells the browser how long to cache and remember the settings before checking again. In order to immediately proceed past the error, you will need to delete your browser's local HSTS settings for that domain. Instructions on how to do so are below.
    > 
    > These settings need to be cleared in each browser. As a developer, you may run into this error if you are testing an HSTS configuration. In Chrome, you can receive this error on localhost. If you have deployed HSTS onto a live site for end users, it may be infeasible to correct the errors they are having depending on the size of your audience. Each user needs to delete their local HSTS settings or wait for them to expire according to the 'max-age' that was set.
    > 
    > Also note that if the website is still serving the HSTS header, your browser will store it as soon as you visit the site again. So you must first stop sending that header if you don't want the error to reoccur.
    > 
    > Neither Chrome nor Firefox have a unique error code for HSTS errors, but the interstitial error pages will include information about HSTS.
    > 
    > Delete HSTS Settings
    > --------------------
    > 
    > Note that these instructions are mainly useful for developers who were testing HSTS and now need to delete the settings. For a website you do not control, deleting your browser's local HSTS settings will not help if the website is still serving an HSTS header as your browser will simply save the settings again on each visit/refresh.
    > 
    > In Chrome you may see the error "NET::ERR_CERT_COMMON_NAME_INVALID." If you click "Advanced" in Chrome the error message will include "You cannot visit *domain.com* right now because the website uses HSTS." That will confirm the error is HSTS-related. On localhost you may see the error "This site can't provide a secure connection."
    > 
    > In Firefox the interstitial page will read: "This site uses HTTP Strict Transport Security (HSTS) to specify that Firefox may only connect to it securely. As a result, it is not possible to add an exception for this certificate."
    > 
    > If you have determined the error is due to cached HSTS settings, follow the following instructions to resolve the error:
    > 
    > How to Delete HSTS Settings in Chrome:
    > --------------------------------------
    > 
    > 1.  Navigate to **chrome://net-internals/#hsts**
    > 
    > This is Chrome's UI for managing your browser's local HSTS settings.
    > 
    > 1.  First, to confirm the domain's HSTS settings are recorded by Chrome, type the hostname into the **Query Domain** section at the bottom of the page. Click Query.If the Query box returns **Found** with settings information below, the domain's HSTS settings are saved in your browser.
    > 
    > ![HSTS Settings Chrome](https://www.thesslstore.com/blog/wp-content/uploads/2016/12/HSTS-settings-Chrome.png)
    > 
    > Note that this is a very sensitive search. Only enter the hostname, such as *www.example.com* or *example.com* without a protocol or path.
    > 
    > 1.  Type the same hostname into the **Delete domain** section and click
    > 
    > Your browser will no longer force an HTTPS connection for that site! You can test if its working properly by refreshing or navigating to the page.
    > 
    > Note that depending on the HSTS settings provided by the site, you may need to specify the proper subdomain. For example, the HSTS settings for *staging.yoursite.com* may be separate from *yoursite.com* so you may need to repeat the steps as appropriate.
    > 
    > How to Delete HSTS Settings in Firefox:
    > ---------------------------------------
    > 
    > We will cover two different methods for deleting HSTS settings in Firefox. The first method should work in most cases -- but we also included a manual option if needed.
    > 
    > 1.  Close all open tabs in Firefox.
    > 2.  Open the full History window with the keyboard shortcut **Ctrl + Shift + H** (Cmd + Shift + H on Mac). You must use this window or the sidebar for the below options to be available.
    > 3.  Find the site you want to delete the HSTS settings for -- you can search for the site at the upper right if needed.
    > 4.  Right-click the site from the list of items and click **Forget About This Site**.This should clear the HSTS settings (and other cache data) for that domain.
    > 5.  **Restart Firefox and visit the site.** You should now be able to visit the site over HTTP/broken HTTPS.If these instructions did not work, you can try the following manual method:
    > 
    > **Manual Method for Firefox** 
    > 
    > If the above steps do not work, you can try the following method.
    > 
    > Start by locating your Firefox profile folder through your operating system's file explorer. You can find this folder through Firefox by navigating to **about:support**
    > 
    > Halfway down the page, in the Application Basics section, you will see **Profile Folder**. Click **Open Folder.**
    > 
    > Now **close Firefox** so that the browser does not overwrite any settings we are about to change.
    > 
    > In your Profile folder find and open the file **SiteSecurityServiceState.txt**. This file contains cached HSTS and HPKP (Key Pinning, a separate HTTPS mechanism) settings for domains you have visited. It may be very disorganized.
    > 
    > Search for the domain you want to clear the HSTS settings for and delete it from the file. Each entry beings with the domain name. Delete the entirety of the entry from the beginning of the desired domain name to the next listed domain. As an alternative, you can rename the existing file from a .txt to a .bak (in order to save the existing file, just in case) and allow Firefox to create an entirely new file on next start up.
    > 
    > Here is an example of a simple HSTS listing:
    > ```
    > www.thesslstore.com:HSTS          0               17312   1527362896190,1,0
    > ```
    > 
    > As mentioned, the formatting for this file can be messy. Below is a sample from my profile. Each domain's settings are shown in a unique color to make separation clear. In this case, part of the settings for the previous domain appear the beginning in red:
    > 
    > ```
    > 1527363079029,1,0www.thesslstore.com:HSTS                                  0               17312
    > 1527362896190,1,0scotthelme.co.uk:HPKP       0               17312 1498419087277,1,1,9dNiZZueNZmyaf3pTkXxDgOzLkjKvI+Nza0ACF5IDwg=X3pGTSOuJeEVw989IJ/cEtXUEmy52zs1TZQrU06KUKg=V+J+7lHvE6X0pqGKVqLtxuvk+0f+xowyr3obtq8tbSw=9lBW+k9EF6yyG9413/fPiHhQy5Ok4UI5sBpBTuOaa/U=ipMu2Xu72A086/35thucbjLfrPaSjuw4HIjSWsxqkb8=+5JdLySIa9rS6xJM+2KHN9CatGKln78GjnDpf4WmI3g=MWfCxyqG2b5RBmYFQuLllhQvYZ3mjZghXTRn9BL9q10=
    > api.github.com:HSTS       0               17312   1527362865303,1,1
    > ```
    > 

- [Firefox redirects to https - Stack Overflow](https://stackoverflow.com/questions/30532471/firefox-redirects-to-https)

    > "Sites preferences" are the culprit. Wasted 45min of my life finding how to fix it despite all the kb/support.mozilla tricks which does not solve your issue nor did mine. I dunno what triggers this issue but several of my websites started to go pear-shaped in a few weeks only affecting me and only firefox.
    > 
    > That's the solution you are all looking for:
    > 
    > 1.  Go to **Preferences**
    > 2.  **Privacy**
    > 3.  Click '**Clear your history**' (nothing will happen yet, click safely)
    > 4.  Once the pop-up appears, click **Details**.
    > 5.  Untick everything except '**Sites Preferences**'
    > 6.  Select '**Everything**' in the select box at the top
    > 7.  Click **Ok**
    > 8.  Try now
    > 
    > [![Firefox capture](https://i.stack.imgur.com/CZbQR.png)](https://i.stack.imgur.com/CZbQR.png)
    > 

- [Open Source For Geeks: Understanding HTTP Strict Transport Security (HSTS)](https://opensourceforgeeks.blogspot.com/2017/03/understanding-http-strict-transport.html)

    > #### Background
    > 
    > Have you any time tried to visit a site by typing "http://" in your web browser and the site that loads corresponds to "https://". Well it happens a lot of time. A website may support only https - secure connections and browser is smart enough to know this. How? We will see that in a moment.\
    > My use case was for using a proxy to intercept browser traffic. As you know any proxy will intercept traffic and then send it's own certificate to the browser and if browser does not recognize the cert it shows the error -
    > 
    > -   "Your connection is not secure"... **SEC_ERROR_UNKNOWN_ISSUER**
    > 
    > You may go in Advanced tab and then add exception to start trusting the new certs for your testing. But it is not always possible and well see why?
    > 
    > **NOTE** : If you are not trying something on your own and dont understand why above prompt came its time to turn back. Your network traffic may be getting intercepted by some hacker using MITM (Man in the middle) attach to steal sensitive data like passwords.
    > 
    > **WARNING** : All the below information is provided only for the use case of pen testing and other security testing. Please do not use it otherwise. All of the below features are provided for your security. Playing around with it without understanding can compromise your security. So proceed on your own risk.
    > 
    > [![](https://2.bp.blogspot.com/-KYjGSyIMnrI/WMzK_s14BVI/AAAAAAAAN6M/BxiAIdDmPtUqlLNErIfrYvQjzlgPVaXKACLcB/s400/whatishsts.jpeg)](https://2.bp.blogspot.com/-KYjGSyIMnrI/WMzK_s14BVI/AAAAAAAAN6M/BxiAIdDmPtUqlLNErIfrYvQjzlgPVaXKACLcB/s1600/whatishsts.jpeg)
    > 
    > #### HTTP Strict Transport Security (HSTS)
    > 
    > As per [Wiki](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security),
    > 
    > HTTP Strict Transport Security (HSTS) is a web security policy mechanism which helps to protect websites against protocol downgrade attacks and cookie hijacking. It allows web servers to declare that web browsers (or other complying user agents) should only interact with it using secure HTTPS connections,[1] and never via the insecure HTTP protocol. HSTS is an IETF standards track protocol and is specified in [RFC 6797](https://tools.ietf.org/html/rfc6797).
    > 
    > How this works is that your webserver eg. **Apache** or **NGINX** is configured so that in each response header it sends header corresponding to  HSTS
    > 
    > -   **Strict-Transport-Security "max-age=63072000"**
    > 
    > max-age is the expiry time. So the HSTS will be applicable till this much time.
    > 
    > **NOTE** : This is updated every time you visit the site. So if this time period is 2 years them each time you visit the site this will be set for next 2 years.
    > 
    > For eg see below in case of techcrunch -
    > 
    > [![](https://3.bp.blogspot.com/-J3lczi3qfTk/WMzDBYgp7GI/AAAAAAAAN5U/-84Q9qkz8QYVdKAAqhqUMQuLGpfglCZfQCLcB/s640/tc_header.png)](https://3.bp.blogspot.com/-J3lczi3qfTk/WMzDBYgp7GI/AAAAAAAAN5U/-84Q9qkz8QYVdKAAqhqUMQuLGpfglCZfQCLcB/s1600/tc_header.png)
    > 
    > #### Working of HTTP Strict Transport Security (HSTS)
    > 
    > Browser once it receives stores this data corresponding to each site. In case of Firefox you can see it as follows -
    > 
    > 1.  Type **about:support** in firefox tab
    > 2.  Click on "Show in Folder". This should open your firefox profile folder.
    > 3.  In this search for a file called **SiteSecurityServiceState.txt** and open it.
    > 4.  Firefox stored HSTS data for sites in this file.
    > 
    > Steps in screenshots -
    > 
    > [![](https://3.bp.blogspot.com/-JwrYKBrKDnM/WMzEZiXZj7I/AAAAAAAAN5g/KPKd0Na1Yk05C5SRj1OIEUAyTEBhJAAFgCLcB/s640/showinfolder.png)](https://3.bp.blogspot.com/-JwrYKBrKDnM/WMzEZiXZj7I/AAAAAAAAN5g/KPKd0Na1Yk05C5SRj1OIEUAyTEBhJAAFgCLcB/s1600/showinfolder.png)
    > 
    > [![](https://1.bp.blogspot.com/-yqO2wMK9CV8/WMzEc_L2Y4I/AAAAAAAAN5k/VXTHSZhlhd0StX9JdD3-c6jjE9KVGpDrQCLcB/s640/file.png)](https://1.bp.blogspot.com/-yqO2wMK9CV8/WMzEc_L2Y4I/AAAAAAAAN5k/VXTHSZhlhd0StX9JdD3-c6jjE9KVGpDrQCLcB/s1600/file.png)
    > 
    > [![](https://2.bp.blogspot.com/-Kn4gq3j4uH8/WMzE7ekcpSI/AAAAAAAAN5o/03UTYtfaiuwXxwJuFfSsyjYGj2ICgf5FACLcB/s640/tc_entry.png)](https://2.bp.blogspot.com/-Kn4gq3j4uH8/WMzE7ekcpSI/AAAAAAAAN5o/03UTYtfaiuwXxwJuFfSsyjYGj2ICgf5FACLcB/s1600/tc_entry.png)
    > 
    > **NOTE** : As mentioned earlier this entry is updated every time you hit the url in your browser. Exception is incognito mode in which case entry from this file is removed once incognito is close. However note that if you have visited the site even once in non incognito mode then the security restrictions will be obeyed even in incognito mode.
    > 
    > **Working** :
    > 
    > -   This tells browser that every subsequent connection should always be https (secure). So even if you try to access http version of the site browser will convert it to https and proceed. 
    > 
    > -   For eg. You can try hitting "**http://techcrunch.com/**" and it will automatically hit "**https://techcrunch.com/**"
    > 
    > -   Another effect it has it that if this header is set then you cannot add exception for the certificate which does not match the original one (the one browser does not trust). Eg in screenshot below -
    > 
    > [![](https://2.bp.blogspot.com/-Qz_0GC_xhaU/WMzGIUQdbQI/AAAAAAAAN50/dFcbqaldP5kBEkIZGapi36lbsx2j-x-DgCLcB/s640/techcrunch_before.png)](https://2.bp.blogspot.com/-Qz_0GC_xhaU/WMzGIUQdbQI/AAAAAAAAN50/dFcbqaldP5kBEkIZGapi36lbsx2j-x-DgCLcB/s1600/techcrunch_before.png)
    > 
    > **NOTE** : I am using **Zap** proxy. You can use any others like **Fiddler** or **Burp**. I have written posts on this before you can revisit them if needed.
    > 
    > -   [Using OWASP Zed Attack Proxy (ZAP) and Plug-n-Hack as a proxy for your browser](http://opensourceforgeeks.blogspot.in/2016/03/using-owasp-zed-attack-proxy-zap-and.html)
    > -   [Intercepting Android network calls using Fiddler Web Proxy](http://opensourceforgeeks.blogspot.in/2015/03/intercepting-android-network-calls.html)
    > 
    > #### How to bypass HSTS?
    > 
    > Well now that we know where firefox stores this data it is easy to bypass this. All you have to do is remove the entry from this file. You can probably change the permission of this file so that new entry is not made in it. When tried for techcrunch you can see you can get back option to add certificate exception -
    > 
    > [![](https://3.bp.blogspot.com/-5KZUzgYWaRU/WMzIUX_yYAI/AAAAAAAAN6A/jSvePnvLJTw-Yw-ukOnr7cqLXDLMnJo8ACLcB/s640/techcrunch_ater.png)](https://3.bp.blogspot.com/-5KZUzgYWaRU/WMzIUX_yYAI/AAAAAAAAN6A/jSvePnvLJTw-Yw-ukOnr7cqLXDLMnJo8ACLcB/s1600/techcrunch_ater.png)
    > 
    > **NOTE** : For above to work make sure firefox is closed else it can overwrite the file.
    > 
    > **NOTE** : Above workaround will not work for the well known sites like google since for them the entries are hardcoded into browser code. Please do share if you know of any workaround for this.
    > 
    > **NOTE** : In the above mentioned file you might also see entries corresponding to **HPKP**. A **HTTP Public Key Pinning (HPKP)** header instructs clients to pin a specific public key to a domain. So, if a HPKP-supporting browser encounters a HPKP header, it will remember the specified public key hashes and associate them with that domain. In the future (until the specified max-age timeout expires), the browser will only accept a certificate for that domain if any key in the certificate's trust chain matches one of the associated hashes.
    > 
    > -   [What is HPKP and how does it work in case of websites](https://security.stackexchange.com/questions/154173/what-is-hpkp-and-how-does-it-work-in-case-of-websites/154179#154179)
    > -   [Can HSTS be disabled in Firefox?](https://security.stackexchange.com/questions/102279/can-hsts-be-disabled-in-firefox/154176#154176)
    > 
    > #### Related Links
    > 
    > -   [HTTP Strict Transport Security (Wiki)](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security)
    > -   [Using OWASP Zed Attack Proxy (ZAP) and Plug-n-Hack as a proxy for your browser(OSFG)  ](http://opensourceforgeeks.blogspot.in/2016/03/using-owasp-zed-attack-proxy-zap-and.html)
    > -   [Intercepting Android network calls using Fiddler Web Proxy(OSFG)](http://opensourceforgeeks.blogspot.in/2015/03/intercepting-android-network-calls.html)  
    > -   [HTTP Strict Transport Security for Apache, NGINX and Lighttpd](https://raymii.org/s/tutorials/HTTP_Strict_Transport_Security_for_Apache_NGINX_and_Lighttpd.html)
    > -   [How to prevent HSTS tracking in Firefox](http://www.ghacks.net/2015/10/16/how-to-prevent-hsts-tracking-in-firefox/)
    > -   [Test HTTP Strict Transport Security (OTG-CONFIG-007)](https://www.owasp.org/index.php/Test_HTTP_Strict_Transport_Security_(OTG-CONFIG-007))
    > -   [What is HPKP and how does it work in case of websites](https://security.stackexchange.com/questions/154173/what-is-hpkp-and-how-does-it-work-in-case-of-websites/154179#154179)
    > -   [Can HSTS be disabled in Firefox?](https://security.stackexchange.com/questions/102279/can-hsts-be-disabled-in-firefox/154176#154176)
    > 


## Firefox doesn't recognize telegramdesktop's tg link

- [Firefox doesn't recognize telegramdesktop's tg link. : firefox](https://www.reddit.com/r/firefox/comments/6p6470/firefox_doesnt_recognize_telegramdesktops_tg_link/)

    > -   Go to `about:config`
    > 
    > -   Add new boolean named `network.protocol-handler.expose.tg` and set it to `false`
    > 
    > -   Create the link by opening an empty tab and typing the following in the location bar `data:text/html,<a href="tg://resolve?domain=Bold">Link</a>`
    > 
    > -   Click on Link and Firefox should ask you to choose the program
    > 
    > -   Check the box in order to remember it for future use

## set search to open in new tab

- [How do i set search to open in new tab? | Firefox 技術支援討論區 | Mozilla 技術支援](https://support.mozilla.org/zh-TW/questions/954276)

    > Look in the about:config window for these settings and change them:
    > 
    > -   `browser.search.openintab` - if true, will open a search from the searchbar in a new tab if you use the return key to trigger the search
    > -   `browser.tabs.loadBookmarksInBackground` - if true, bookmarks that open in a new tab will not steal focus
    > -   `browser.tabs.loadDivertedInBackground` - Load the new tab in the background, leaving focus on the current tab if true
    > -   `browser.tabs.loadInBackground` - Do not focus new tabs opened from links (load in background) if true
    > -   `browser.tabs.opentabfor.middleclick` - if true, links can be forced to open a new tab if middle-clicked. Useful for search results.



# Resilio Sync

## Sync Does Not Have Permission To Access This Folder

- [Sync Does Not Have Permission To Access This Folder · Issue #182 · tuxpoldo/btsync-deb](https://github.com/tuxpoldo/btsync-deb/issues/182)

    > Snip from [my thread in the BTSync forums](http://forum.bittorrent.com/topic/34641-sync-does-not-have-permission-to-access-this-folder/):
    > 
    > > I recently upgraded from 1.4 to 2.0 on my Debian server box. When attempting to recreate my 1.4 sync folder in 2.0, I am getting the error "Sync does not have permission to access this folder".
    > >
    > > I double checked, and Sync does have permission for this folder. The daemon is running as the same user it was in 1.4. If I make a 1.4 style sync folder, it appears to have no issue reading the data and no error is thrown.
    > >
    > > Unfortunately this is my "target" box for some one way syncing from a remote host, so I need to be able to add the key from my remote server. Even using the 1.4 style key, it throws permission errors.
    > 
    > After some troubleshooting with the btsync support team, we determined it was due to the "directory_root" property that is found in the debconf-default.conf file in the webui section. Removing this property fixed this error.
    > 
    > Here is what the support team said in regards to this property:
    > 
    > > Check please your config. Most likely you'll find there "directory_root" (or "dir_whitelist") parameter.\
    > > This parameters specify the locations where Sync can create folders. Try to remove these parameters.
    > >
    > > By the way, this is not and official repository and as I understand the repository maintainer included\
    > > this parameter in the default config.
    > > 
    > 
    > ---
    > 
    > add folders you want to access in `dir_whitelist`
    > 
    > ```json
    > {
    >     "listening_port" : 55555,
    >     "storage_path" : "/mnt/sync/config",
    >     "vendor" : "docker",
    >     "display_new_version": false,
    > 
    >     "directory_root_policy" : "belowroot",
    >     "directory_root" : "/mnt/",
    > 
    >     "webui" :
    >     {
    >       	"listen" : "0.0.0.0:8888",
    >       	"allow_empty_password" : false,
    >         "dir_whitelist" : [ "/mnt/sync/folders", "/mnt/mounted_folders", "/mnt/sync/ResilioSyncFolder" ]
    >     }
    > }
    > ```
    > [name=Ya-Lun Li]

- [When adding shared folder with btsync: "Don't have permissions to write to selected folder" - Ask Ubuntu](https://askubuntu.com/questions/817712/when-adding-shared-folder-with-btsync-dont-have-permissions-to-write-to-selec/1073677#1073677)

    > As BTSync team answers:
    > 
    > [Sync Does Not Have Permission To Access This Folder - Sync Troubleshooting - Sync Forums](https://forum.resilio.com/topic/34641-sync-does-not-have-permission-to-access-this-folder/)
    > 
    > > In the config file for btsync, remove the "directory_root" or "dir_whitelist" parameter from the config. This parameter specifies the location where Sync can create folders. You could also modify it to include the specific folder you want to sync.
    > 
    > Here is the default sync.conf file:
    > 
    > ```
    > {
    >     "listening_port" : 55555,
    >     "storage_path" : "/mnt/sync/config",
    >     "vendor" : "docker",
    >     "display_new_version": false,
    > 
    >     "directory_root_policy" : "belowroot",
    >     "directory_root" : "/mnt/",
    > 
    >     "webui" :
    >     {
    >         "listen" : "0.0.0.0:8888",
    >         "allow_empty_password" : false,
    >         "dir_whitelist" : [ "/mnt/sync/folders", "/mnt/mounted_folders"]
    >     }
    > }
    > 
    > ```
    > 
    > you can add custum folder into `dir_whitelist`
    > 


## get Resilio to assign 0777 to all folders it writes

- [[Support] Linuxserver.io - Resilio Sync - Page 2 - Docker Containers - Unraid](https://forums.unraid.net/topic/51613-support-linuxserverio-resilio-sync/?page=3)

    > just set umask to 000 before Resilio Sync run
    > ```sh
    > umask 000
    > ```
    > [name=Ya-Lun Li]
    > 

