# Javascript__快速上手

<!-- toc --> 
[toc]

## Useful Tool
* 線上JavaScript編輯器
    * [Dashboard - JSFiddle - Online JavaScript Editor - jQuery, Angular, Backbone, Underscore, Knockout, YUI](https://jsfiddle.net/user/dashboard/)
* 線上 Javascript code 清理工具
    * [JavaScript Cleaner - Free Online JS Beautifyer](https://html-cleaner.com/js/)
* 線上 Bookmarklet 產生器
    * [Bookmarklet Creator with Script Includer - Peter Coles](https://mrcoles.com/bookmarklet/)
* 線上 Regex 教學
    * [RegexOne - Learn Regular Expressions - Lesson 1: An Introduction, and the ABCs](https://regexone.com/)
* 線上執行 require() 從npm 取得module
    * [RequireBin](http://requirebin.com/)
    Welcome! require() some modules from npm (like you were using browserify)
    and then hit Run Code to run your code on the right side.
    Modules get downloaded from browserify-cdn and bundled in your browser.
* 線上 npm 模組瀏覽器化
    * [browserify/wzrd.in: browserify as a service.](https://github.com/browserify/wzrd.in)
        -   The module gets pulled down from [npm](http://npmjs.org) and installed
        -   The module gets [browserified](http://browserify.org) as a standalone bundle
        -   The module gets sent to you, piping hot
        -   The module gets cached so that you don't have to wait later on


## Reference

### W3schools

* Javascript
    * [JavaScript DOM EventListener](https://www.w3schools.com/js/js_htmldom_eventlistener.asp)
    * [JavaScript Events](https://www.w3schools.com/js/js_events.asp)
    * [JavaScript String Methods](https://www.w3schools.com/js/js_string_methods.asp)

* HTML DOM
    * [HTML DOM getElementsByClassName() Method](https://www.w3schools.com/jsref/met_document_getelementsbyclassname.asp) 
    * [Location Object](https://www.w3schools.com/jsref/obj_location.asp)

### MDN

* [Blob - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Blob)

* [import - JavaScript | MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/import)

    引入整個模組的內容。將插入 `myModule` 到當前的範圍中，包含所有來自 my-module 模組的 exported binding。大多數源自於 my-module.js。

    ```javascript=
    import * as myModule from 'my-module';
    ```
    引入模組中多個成員屬性，並使用別名命名。

    ```javascript=
    import {
      reallyReallyLongModuleMemberName as shortName,
      anotherLongModuleName as short
    } from 'my-module';
    ```
    
    __Examples__

    Importing a secondary file to assist in processing an AJAX JSON request.

    ```javascript=
    // --file.js--
    function getJSON(url, callback) {
      let xhr = new XMLHttpRequest();
      xhr.onload = function () { 
        callback(this.responseText) 
      };
      xhr.open('GET', url, true);
      xhr.send();
    }

    export function getUsefulContents(url, callback) {
      getJSON(url, data => callback(JSON.parse(data)));
    }

    // --main.js--
    import { getUsefulContents } from 'file';
    getUsefulContents('http://www.example.com', data => {
      doSomethingUseful(data);
    });
    ```

## Library

* [eligrey/FileSaver.js: An HTML5 saveAs() FileSaver implementation](https://github.com/eligrey/FileSaver.js/)

## Debug

* [如何使用Visual Studio Code偵錯Node.js？ - 黑暗執行緒](http://blog.darkthread.net/post-2016-08-06-debug-nodejs-with-vscode.aspx)

    點選最左側的偵錯（禁行蟲蟲）圖示(1)會切換到偵錯視窗，偵錯鈕(2)右側顯示目前沒有組態，別擔心，按下偵錯鈕就對了。

    ![](http://www.darkthread.net/Photos/3530-5bd2-o.gif)

    因為沒有組態，依VSCode跳出提示，選取環境清單選取「Node.js」：

    ![](http://www.darkthread.net/Photos/3531-f188-o.gif)

    點選Node.js後VSCode會自動建立launch.json範本，預設有「啟動」「附加」「Attach to process」三種組態，要做到如Visual Studio按F5開始測試，請修改"啟動"組態中的program屬性，改為要測試的js檔。

    ![](http://www.darkthread.net/Photos/3532-7132-o.gif)

    設好組態再按一次偵錯鈕，VSCode就會呼叫Node.js執行JS程式，餘下的操作對有Visual Studio或瀏覽器F12偵錯經驗的大家應不是問題，VSCode支援設定中斷點(1)，可以查看變數(2)、新増監看算式(3)、查詢呼叫堆疊（Callstack）(4)，當然也可以即時執行指令(5)。

    ![](http://www.darkthread.net/Photos/3533-967e-o.gif)

    另外，身為Visual Studio家族，Goto Definition、Fill All Reference、Rename、重排程式碼… 等經典功能一定不能少，在編輯區按右鍵可由選單查到快速鍵。

    ![](http://www.darkthread.net/Photos/3535-3613-o.gif)

    補充：如果要測試互動輸入，組態檔有個externalConsole要設為true，不然遇到sget等函式會等不到輸入發生逾時錯誤。

* [Visual Studio Code 前端调试不完全指南 | 咀嚼之味](http://jerryzou.com/posts/vscode-debug-guide/)

    1\. launch / attach
    -------------------

    要使用 vscode 的调试功能，首先就得配置 `.vscode/launch.json` 文件。以最简单的 Node 调试配置为例：

    ```json
    {
        "version": "0.2.0",
        "configurations": [
            {
                "type": "node",
                "request": "launch",
                "name": "Launch",
                "program": "${workspaceRoot}/index.js"
            },
            {
                "type": "node",
                "request": "attach",
                "name": "Attach",
                "port": 5858
            }
        ]
    }
    ```

    其中最重要的参数是 `request` ，它的取值有两种 `launch` 和 `attach`。

    -   **launch**模式：**由 vscode 来启动**一个独立的具有 debug 模式的程序
    -   **attach**模式：附加于（也可以说“监听”）一个**已经启动的程序**（必须已经开启 Debug 模式）

    2\. 调试前端代码
    ----------

    通过 vscode 调试前端代码主要依赖于一个插件：[Debugger for Chrome](https://github.com/Microsoft/vscode-chrome-debug)，该插件主要利用 [Chrome 所开放出来的接口](https://chromedevtools.github.io/devtools-protocol/) 来实现对其渲染的页面进行调试。可以通过 `Shift + Cmd + X` 打开插件中心，搜索对应插件后直接安装。安装完成并重新加载 vscode 后，可以直接点击调试按钮并创建新的启动配置。如果你之前已经创建过启动配置了，就可以直接打开 `.vscode/launch.json` 进行修改。

    ![vscode-debug-chrome](http://jerryblog-image.b0.upaiyun.com/blog/posts/vscode-debug-chrome.png)

    其中调试 Chrome 页面的配置如下所示：

    ```json
    {
        "version": "0.2.0",
        "configurations": [
            {
                "type": "chrome",
                "request": "launch",
                "name": "启动一个独立的 Chrome 以调试 frontend",
                "url": "http://localhost:8091/frontend",
                "webRoot": "${workspaceRoot}/frontend"
            }
        ]
    }
    ```

    如之前所述，通过第一个 launch 配置就能启动一个通过 vscode 调试的 Chrome。大家可以直接使用我组织好的项目 [zry656565/vscode-debug-sample](https://github.com/zry656565/vscode-debug-sample) 进行测试，测试方法在该项目的 README 里面写得很清楚了。简要步骤概括为：

    1.  `npm run frontend`
    2.  启动调试配置：“启动一个独立的 Chrome 以调试 frontend”
    3.  在 `frontend/index.js` 中加断点
    4.  访问 `http://localhost:8091/frontend/`

    ### 延伸问题

    使用 `launch` 模式调试前端代码存在一个问题，就是 vscode 会以新访客的身份打开一个新的 Chrome 进程，也就是说你**之前在 Chrome 上装的插件都没法在这个页面上生效**（如下图所示）。

    ![vscode-debug-launch](http://jerryblog-image.b0.upaiyun.com/blog/posts/vscode-debug-launch.png)

    在这种情况下 `attach` 模式就有它存在的意义了：对一个已经启动的 Chrome 进行监听调试。

    ```json
    {
        "version": "0.2.0",
        "configurations": [
            {
                "type": "chrome",
                "request": "attach",
                "name": "监听一个已经启动调试模式的 Chrome",
                "port": 9222,
                "url": "http://localhost:8091/frontend",
                "webRoot": "${workspaceRoot}/frontend"
            }
        ]
    }
    ```

    其中 9222 是 Chrome 的调试模式推荐的端口，可以根据需要进行修改。不过目前我并没有成功实施这个设想，对此有兴趣的同学可以从下面这两个链接入手去研究一下：

    -   [Chrome DevTools Protocol Viewer](https://chromedevtools.github.io/devtools-protocol/)
    -   [Debugger for Chrome / Attach](https://github.com/Microsoft/vscode-chrome-debug/blob/master/README.md#attach)

    有一部分遇到的问题可以直接在 Debugger for Chrome 的 FAQ 中得到解答。


## NPM
* [get npm](https://www.npmjs.com/get-npm?utm_source=house&utm_medium=homepage&utm_campaign=free%20orgs&utm_term=Install%20npm)
    npm makes it easy for JavaScript developers to share and reuse code, and makes it easy to update the code that you’re sharing, so you can build amazing things.



* [requiring npm modules in the browser console](https://gist.github.com/mathisonian/c325dbe02ea4d6880c4e)

    [![demo gif](https://camo.githubusercontent.com/bf330eecd4a06ce86d32b6bd9e72a50d7b1ac31a/687474703a2f2f692e696d6775722e636f6d2f715675397335332e676966)](https://camo.githubusercontent.com/bf330eecd4a06ce86d32b6bd9e72a50d7b1ac31a/687474703a2f2f692e696d6775722e636f6d2f715675397335332e676966)

    injecting the require() function
    ================================

    And finally, we have to inject the `require()` function into the browser. There is a script hosted on amazon s3 that properly defines the function: [https://s3.amazonaws.com/s3.mathisonian.com/javascripts/requirify-browser.js](https://s3.amazonaws.com/s3.mathisonian.com/javascripts/requirify-browser.js).

    This script can be injected into the body of web pages using a chrome extension ([https://chrome.google.com/webstore/detail/requirify/gajpkncnknlljkhblhllcnnfjpbcmebm](https://chrome.google.com/webstore/detail/requirify/gajpkncnknlljkhblhllcnnfjpbcmebm)) or a simple javascript boomarklet.


    ```javascript=
    javascript:(function(){var body=document.getElementsByTagName('body')[0];var script=document.createElement('script');script.type='text/javascript';script.src='https://s3.amazonaws.com/s3.mathisonian.com/javascripts/requirify-browser.js';body.appendChild(script);})();

    ```

    is a bookmarklet containing the following code:

    ```javascript=
       var body= document.getElementsByTagName('body')[0];
       var script= document.createElement('script');
       script.type= 'text/javascript';
       script.src= 'https://s3.amazonaws.com/s3.mathisonian.com/javascripts/requirify-browser.js';
       body.appendChild(script);
    ```
    
    update
    ======

    The script has been updated to interact directly with browserify-cdn, and now looks like this:

    ```javascript=
    var request = require('browser-request');

    window.require = function(name, moduleName) {
        _require = require;

        if(!moduleName) {
            moduleName = name;
        }

        console.log('Fetching ' + moduleName + '... just one second');
        request('http://wzrd.in/bundle/' + moduleName + '@latest/', function(er, res, body) {

            require = null;
            eval(body);
            window[name] = require(moduleName);
            require = _require;
            console.log('Finished getting ' + moduleName);
        });
    };

    ```

    > great ideas! but why not simple use the "bundle" version from [http://wzrd.in/](http://wzrd.in/) ?
    > 
    > For example: `<script src="http://wzrd.in/bundle/backbone@latest"></script>`
    > 
    > And then, simply: `Backbone = require('Backbone')` ?
    > 


    > Can you use require to load request module before it is defined? Not work for me. Instead, I use chrome built in function fetch to accomplish it. Also I change wzrd.in's schema from "http" to "https" to prevent "Mixed Content" problem.
    > 
    > ```
    > window.require = function(name, moduleName) {
    >     _require = require;
    > 
    >     if(!moduleName) {
    >         moduleName = name;
    >     }
    > 
    >     console.log('Fetching ' + moduleName + '... just one second');
    >     fetch('https://wzrd.in/bundle/' + moduleName + '@latest/')
    >         .then(response => response.text())
    >         .then(body => {
    >             require = null;
    >             eval(body);
    >             window[name] = require(moduleName);
    >             require = _require;
    >             console.log('Finished getting ' + moduleName);
    >         });
    > };
    > 
    > ```




    
### Library

* [iriscouch/browser-request: Browser library compatible with Node.js request package](https://github.com/iriscouch/browser-request)

    Fetch a resource:

    ```javascript=
    request('/some/resource.txt', function(er, response, body) {
      if(er)
        throw er;
      console.log("I got: " + body);
    })
    ```

* [Browserify](http://browserify.org/#install)
    Browsers don't have the require method defined, but Node.js does. With Browserify you can write code that uses require in the same way that you would use it in Node.


* [require.js - cdnjs.com - The best FOSS CDN for web related libraries to speed up your websites!](https://cdnjs.com/libraries/require.js/)

    RequireJS is a JavaScript file and module loader. It is optimized for in-browser use, but it can be used in other JavaScript environments, like Rhino and Node

* [prose/gatekeeper: Enables client-side applications to dance OAuth with GitHub.](https://github.com/prose/gatekeeper#setup-your-gatekeeper)

    Because of some [security-related limitations](http://blog.vjeux.com/2012/javascript/github-oauth-login-browser-side.html), Github prevents you from implementing the OAuth Web Application Flow on a client-side only application.

    This is a real bummer. So we built Gatekeeper, which is the missing piece you need in order to make it work.
    
* [maxogden/requirebin: write browser JavaScript programs using modules from NPM](https://github.com/maxogden/requirebin)





### Execrise

* [將big5 編碼的中文轉成url 可接受的格式輸出到瀏覽器 console - JSFiddle](https://jsfiddle.net/allenyllee/ccu2xtf1/)

    ```javascript=
    // Welcome! require() some modules from npm (like you were using browserify)
    // and then hit Run Code to run your code on the right side.
    // Modules get downloaded from browserify-cdn and bundled in your browser.

    // =============
    // 將big5 編碼的中文轉成url 可接受的格式輸出到瀏覽器 console
    // =============

    // =============
    // bnoordhuis/node-iconv: node.js iconv bindings - text recoding for fun and profit!
    // https://github.com/bnoordhuis/node-iconv
    // =============
    // 原本是用'iconv', 但是一直出現error
    // stderr: Error: Cannot find module '../build/Release/iconv.node' from '/tmp/iconv118120-29969-m4a781/node_modules/iconv/lib'
    // 在本機上rebuild 也無法解決，參考:
    // error: Error: Cannot find module '../build/Debug/iconv.node' · Issue #167 · bnoordhuis/node-iconv
    // https://github.com/bnoordhuis/node-iconv/issues/167
    // 和
    // require('iconv') fails · Issue #69 · bnoordhuis/node-iconv
    // https://github.com/bnoordhuis/node-iconv/issues/69
    // 試過很多方法都無法解決，只好改用'iconv-lite'
    //
    //var Iconv = require('iconv').Iconv;
    //var iconv = new Iconv('utf8', 'BIG5');

    // ============
    // ashtuchkin/iconv-lite: Convert character encodings in pure javascript.
    // https://github.com/ashtuchkin/iconv-lite
    // ============
    // 一開始瀏覽器 console 出現error: 
    // iconv-lite warning: javascript files are loaded not with utf-8 encoding. See https://github.com/ashtuchkin/iconv-lite/wiki/Javascript-source-file-encodings for more info.
    // 解法:
    // add <meta charset="utf-8"> to the html file.
    //
    var iconv = require('iconv-lite');
    var Buffer = require('buffer').Buffer

    // Convert from an encoded buffer to js string.
    str = iconv.decode(new Buffer([0x68, 0x65, 0x6c, 0x6c, 0x6f]), 'win1251');
    console.log(str);

    // Convert from js string to an encoded buffer.
    buf = iconv.encode("Sample input string", 'win1251');
    console.log(buf);

    // 將utf-8 中文轉成big5
    buf = iconv.encode("耶穌", 'big5');
    console.log(buf);

    // Check if encoding is supported
    str2 = iconv.encodingExists("us-ascii")
    console.log(str2);

    // ==============
    // javascript - how to get big5 urlencode in node.js? - Stack Overflow
    // https://stackoverflow.com/questions/27621643/how-to-get-big5-urlencode-in-node-js
    // ==============
    // 此處將big5 編碼轉成url 可接受的格式
    function big5_encode(chr) {
        var rtn = "";
        var buf = iconv.encode(chr, 'big5');
        for(var i=0;i<buf.length;i+=2) {
            rtn += '%' + buf[i].toString(16).toUpperCase();
            rtn += ((buf[i+1] >= 65 && buf[i+1] <= 90)
                ||(buf[i+1]>=97 && buf[i+1]<=122))
                ? String.fromCharCode(buf[i+1])
                : '%' + buf[i+1].toString(16).toUpperCase();
        }
        return rtn;
    }

    // 測試輸入
    var chr = '十尢我'; // 結果應為 %A4Q%A4q%A7%DA
    console.log(big5_encode(chr));

    var chr = '耶穌'; // 結果應為 %ADC%BFq
    console.log(big5_encode(chr));

    ```


### Trouble shooting

* [Running Python on Windows for Node.js dependencies - Stack Overflow](https://stackoverflow.com/questions/15126050/running-python-on-windows-for-node-js-dependencies)

    __symptom__
    ```
    gyp ERR! stack Error: Can't find Python executable "python", you can set the PYT
    HON env variable.
    ```
    __solution__
    
    If you haven't got python installed along with all the node-gyp dependecies, simply execute:

    ```
    npm install --global --production windows-build-tools
    ```

    and then to install the package:

    ```
    npm install --global node-gyp
    ```

    once installed, you will have all the node-gyp dependencies downloaded, but you still need the environment variable. Validate Python is indeed found in the correct folder:

    ```
    C:\Users\ben\.windows-build-tools\python27\python.exe 
    ```

    _[Note - it uses python 2.7 not 3.x as it is not supported](https://github.com/nodejs/node-gyp)_

    If it doesn't moan, go ahead and create your (user) environment variable:

    ```
    setx PYTHON "%USERPROFILE%\.windows-build-tools\python27\python.exe"
    ```

    restart cmd, and verify the variable exists via `set PYTHON` which should return the variable

    Lastly re-apply `npm install <module>`





## HTML5

* [HTML5筆記–Object URL - 黑暗執行緒](http://blog.darkthread.net/post-2014-03-12-html5-object-url.aspx)

    Data URI的格式為="data:image/gif;base64,R0lGOD...."，Object URL則是"blob:"再串上網址以及GUID，例如: blob:http%3A//www.darkthread.net/c94d498b-7818-49b3-8e79-d3959938ba0f

    Object URL不像Data URI包含內容的Base64編碼，不管背後代表的File或Blob物件有多大，都只有一個短短的GUID，真正的內容被儲存在瀏覽器記憶體中，Object URL像個號碼牌，憑著它可以向瀏覽器提領內容。換個角度，http%3A//www.darkthrad.net/c94d498b-7818-49b3-8e79-d3959938ba0f的形式，有點像是跟http: //www.darkthread.net網站取得名為c94d498b-7818-49b3-8e79-d3959938ba0f的資源，但讀取時不需真的發出HTTP Request，直接由瀏覽器提取即可。

    由於物件內容被儲存在瀏覽器記憶體，註定了Object URL的生命週期得緊緊地跟網頁綁在一起，就像JavaScript變數一般，需等到網頁載入後，透過[URL.createObjectURL()](https://developer.mozilla.org/en-US/docs/Web/API/URL.createObjectURL)為File或Blob物件建立Object URL，網頁結束後自動失效，或是確定不要後呼叫[URL.revokeObjectURL()](https://developer.mozilla.org/en-US/docs/Web/API/URL.revokeObjectURL)主動將其註銷節省記憶體。


* [淺嚐Data URI - 黑暗執行緒](http://blog.darkthread.net/post-2010-11-05-data-uri.aspx)


    在HTML裡link的href及img的src，並沒有指向某個URL，而是直接嵌入一段Base64編碼，而IE8+, Firefox, Safari, Opera, Chrome都能正確顯示其中的圖檔與CSS設定。

    這種表示方法叫做[data URI schema](http://en.wikipedia.org/wiki/Data:_URL)，是新一代瀏覽器支援的檔案資料表現格式，允許在網頁裡以字串形式直接內嵌圖檔、CSS檔案，進而達到以下好處:

    1.  瀏覽器不用為了下載圖檔、CSS另外發動HTTP Request。每次HTTP傳輸產生的額外資料量(HTTP Header、TCP/IP Header...等)，累積下來多半會大於使用Base64編碼二進位資料所增加的資料量(每3個Byte增加一個Byte)，事實上內嵌成Base64字串反而較節省頻寬。
    2.  基於TCP傳輸特性，傳送一個大檔案會比連續傳送多個拆解的小檔更快速有效率。(HTTP Keep-Alive可以改善傳送多個小檔案效率不佳的問題，但並不能徹底解決)
    3.  使用HTTPS(SSL)傳輸時，因為HTTPS Request的額外程序更多，內嵌資料做法的改善更明顯。
    4.  瀏覽器通常會有同時使用HTTP連線數的上限(例如: 兩條)，將所有需要資料一次下載回來，可以避免持續佔用寶貴的連線資源。
    5.  以往在網頁式的Rich Text編輯器裡處理貼上圖檔，得將圖檔上傳至伺服器端某處，再將URL丟回編輯器中。使用內嵌資料寫法，可讓網頁編輯文字要內嵌圖檔容易多了。

    當然，凡事不會有利無害，網頁內嵌資料的做法也有其缺點:

    1.  因圖檔內容被綁在網頁中，若為動態網頁每次內容都會變化，就無法透過快取加速及節省頻寬，網頁內容含圖檔資料，每次都得重新下載。
    2.  當檔案資料有變化時，所有內嵌它的網頁都要重新產生編碼。
    3.  IE8以上的版本才有支援，且限制大小不可超過32KB
    4.  Base64會讓內容變大33%，但若Web Server端啟用GZIP壓縮，增加的大小可以縮小到2-3%。
    5.  對資安軟體來說，Data URI增加了網頁內容檢驗的難度。

    IE從IE8開始才支援這種Data URI的做法，且基於安全、效率的考量，加入了一些限制:

    -   不支援Javascript檔內嵌，避免惡意程式藏匿其中，逃避Script過濾機制。
    -   內嵌檔案大小不可超過32KB。
    -   支援格式包含: `object` (images only) , `img,` `input type=image,` `link  
        以及CSS宣告，例如:``background-image`, `background`, `list-style-type`, `list-style等。`

## Trigger Download

* [How to create a file and generate a download with Javascript in the Browser (without a server) | Our Code World](https://ourcodeworld.com/articles/read/189/how-to-create-a-file-and-generate-a-download-with-javascript-in-the-browser-without-a-server)

    __Self-implemented download function__
    
    The following simple function allow you to generate a download of a file directly in the browser without contact any server. It works on all HTML5 Ready browsers as it uses the download attribute of the `<a>` element:
    
    [How to create a file and generate a download with Javascript in the Browser (without a server) - JSFiddle](https://jsfiddle.net/allenyllee/vqb3tm2c/)
    
    ```javascript=
    function download(filename, text) {
      var element = document.createElement('a');
      element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(text));
      element.setAttribute('download', filename);

      element.style.display = 'none';
      document.body.appendChild(element);

      element.click();

      document.body.removeChild(element);
    }

    // Start file download.
    download("hello.txt","This is the content of my file :)");

    ```
    
    __Using a library__

    [FileSaver.js](https://github.com/eligrey/FileSaver.js) implements the `saveAs()` FileSaver interface in browsers that do not natively support it.

    ```javascript=
    var content = "What's up , hello world";
    // any kind of extension (.txt,.cpp,.cs,.bat)
    var filename = "hello.txt";

    var blob = new Blob([content], {
     type: "text/plain;charset=utf-8"
    });

    saveAs(blob, filename);
    ```

* [小tip:JS前端创建html或json文件并浏览器导出下载 « 张鑫旭-鑫空间-鑫生活](http://www.zhangxinxu.com/wordpress/2017/07/js-text-string-download-as-html-json-file/)

    __借助HTML5 Blob实现文本信息文件下载__
    
    
    
    ```javascript=
    var funDownload = function (content, filename) {
        // 创建隐藏的可下载链接
        var eleLink = document.createElement('a');
        eleLink.download = filename;
        eleLink.style.display = 'none';
        // 字符内容转变成blob地址
        var blob = new Blob(\[content\]);
        eleLink.href = URL.createObjectURL(blob);
        // 触发点击
        document.body.appendChild(eleLink);
        eleLink.click();
        // 然后移除
        document.body.removeChild(eleLink);
    };

    ```
    [using html5 blob object to donwload textarea content as file - JSFiddle](https://jsfiddle.net/allenyllee/r33z5fd8/)
    
    __借助Base64实现任意文件下载__

    ```javascript=
    var funDownload = function (domImg, filename) {
        // 创建隐藏的可下载链接
        var eleLink = document.createElement('a');
        eleLink.download = filename;
        eleLink.style.display = 'none';
        // 图片转base64地址
        var canvas = document.createElement('canvas');
        var context = canvas.getContext('2d');
        var width = domImg.natureWidth;
        var height = domImg.natureHeight;
        context.drawImage(domImg, 0, 0);
        // 如果是PNG图片，则context.toDataURL('image/png')
        eleLink.href = context.toDataURL('image/jpeg');
        // 触发点击
        document.body.appendChild(eleLink);
        eleLink.click();
        // 然后移除
        document.body.removeChild(eleLink);
    };

    ```
    
* [firefox - Bookmarklet to save file - Stack Overflow](https://stackoverflow.com/questions/17900671/bookmarklet-to-save-file)

    To trigger the "Save As" dialog for any resource (`blob:`, `http:`, whatever permitted scheme), use the [`download` attribute](http://www.whatwg.org/specs/web-apps/current-work/multipage/links.html#downloading-resources) of an anchor. This is supported since Firefox 20.

    Example: A bookmarklet that presents the current page as a download:

    ```javascript=
    javascript:(function() {
        var a = document.createElement('a');
        a.href = location.href;
        a.download = 'filename.html';
        document.body.appendChild(a);
        a.click();
        a.parentNode.removeChild(a);
    })();

    ```
    [Bookmarklet to save file - JSFiddle](https://jsfiddle.net/allenyllee/8rsx01aq/)

    
### __Exercise__
* [create a blob object and trigger download you should include FileSaver.js in HTML - JSFiddle](https://jsfiddle.net/allenyllee/osu0njpp/)
* [using jQuery to register click event with HTML button, you need to create a script element load FileSaver.js and attach it to the document. - JSFiddle](https://jsfiddle.net/allenyllee/x5xt78wc/)


## Dynamically load JS

* [javascript - Dynamically load JS inside JS - Stack Overflow](https://stackoverflow.com/questions/14521108/dynamically-load-js-inside-js)

    My guess is that in your DOM-only solution you did something like:

    ```javascript=
    var script = document.createElement('script');
    script.src = something;
    //do stuff with the script
    ```

    First of all, that won't work because the script is not added to the document tree, so it won't be loaded. Furthermore, even when you do, execution of javascript continues while the other script is loading, so its content will not be available to you until that script is fully loaded.

    You can listen to the script's `load` event, and do things with the results as you would. So:

    ```javascript=
    var script = document.createElement('script');
    script.onload = function () {
        //do stuff with the script
    };
    script.src = something;

    document.head.appendChild(script); //or something of the likes
    ```

    
### __Exercise__
* [create a blob object and trigger download while the FileSaver.js was loaded - JSFiddle](https://jsfiddle.net/allenyllee/g98gsx7L/)



## Register event

### __Exercise__
* [using jQuery to register mouseover and click event - JSFiddle](https://jsfiddle.net/allenyllee/p5ze4m1k/)
* [using jQuery to register mouse event - mousedown mouseup mouseenter mouseleave mouseover click dblclick - JSFiddle](https://jsfiddle.net/allenyllee/3shpawkm/)
* 

## Bookmarklet

* [Making Bookmarklets](https://gist.github.com/caseywatts/c0cec1f89ccdb8b469b1)

    To make a bookmarklet we have three steps:

    1.  Write some javascript code that you want in a bookmarklet (using the console)
    2.  Put `javascript:` in front of the code
    3.  Wrap everything in an [IIFE](http://en.wikipedia.org/wiki/Immediately-invoked_function_expression) so the page doesn't freak out

    Here is our cloud-to-butt function:

    ```javascript=
    document.body.innerHTML = document.body.innerHTML.replace(/cloud/g, "butt").replace(/Cloud/g, "Butt");

    ```

    Try just putting `javascript:` in front of it

    ```javascript=
    javascript:document.body.innerHTML = document.body.innerHTML.replace(/cloud/g, "butt").replace(/Cloud/g, "Butt");

    ```
    
    The page did SOMETHING but it seemed to refresh and then the CSS/images didn't load! :(

    We can get around this by putting this in an [Immediately Invoked Functional Expression](http://en.wikipedia.org/wiki/Immediately-invoked_function_expression).

    Here are two example ways to write a standard IIFE:

    ```javascript=
    (function(){})();
    // or
    function(){}();
    ```

    Here's the general template I always use:

    ```javascript=
    javascript:(function(){CONTENTGOESHERE})();

    ```

    Try it with your cloud to butt code!

    ```javascript=
    javascript:(function(){
      document.body.innerHTML = document.body.innerHTML.replace(/cloud/g, "butt").replace(/Cloud/g, "Butt");
    })();

    ```

### __Exercise__

* [HackMD markdown file download bookmarklet](https://gist.github.com/allenyllee/2f5dfd1984d2278e9a483958d9c6d974)

    ```javascript=
    // Location href Property
    // https://www.w3schools.com/jsref/prop_loc_href.asp
    // 透過HTML DOM 的 Location Object 的 href Property 取得目前頁面的URL
    var str = location.href;
    // JavaScript String Methods
    // https://www.w3schools.com/js/js_string_methods.asp
    // 分析HackMD 的網址，知道是以字串"https%3A%2F%2Fhackmd.io%2F"開頭到結束的整串去除%符號，作為iframe 的id
    // 利用 indexOf() 方法找出字串位置，再利用slice() 進行切割
    // 最後利用replace()方法使用RegEx 將所有%符號移除
    var pos = str.indexOf("https%3A%2F%2Fhackmd.io%2F");
    str = str.slice(pos);
    str = str.replace(/%/g, "");
    // javascript - Get element from within an iFrame - Stack Overflow
    // https://stackoverflow.com/questions/1088544/get-element-from-within-an-iframe
    // 從iframe 的id 取回裡面的內容
    var iframe = document.getElementById(str);
    var innerDoc = iframe.contentDocument || iframe.contentWindow.document;
    // HTML DOM getElementsByClassName() Method
    // https://www.w3schools.com/jsref/met_document_getelementsbyclassname.asp
    // 從iframe 取回的內容找到"ui-download-markdown"類別
    // x 包含兩個物件，我們要的是第二個x[1]
    var x = innerDoc.getElementsByClassName("ui-download-markdown");
    //How to trigger event in JavaScript? - Stack Overflow
    //https://stackoverflow.com/questions/2490825/how-to-trigger-event-in-javascript
    // 模仿按下下載連結時觸發click event
    var event = new CustomEvent('click', { bubbles: true, cancelable: true });
    x[1].dispatchEvent(event);
    ```
    
    清理後得到Bookmarklet
    
    * 先用 [JavaScript Cleaner - Free Online JS Beautifyer](https://html-cleaner.com/js/) 清理註解與排版
    * 再用 [Bookmarklet Creator with Script Includer - Peter Coles](https://mrcoles.com/bookmarklet/) 轉成一行Bookmarklet
    
    ```javascript=
    javascript:(function()%7Bvar%20str%20%3D%20location.href%3Bvar%20pos%20%3D%20str.indexOf(%22https%253A%252F%252Fhackmd.io%252F%22)%3Bstr%20%3D%20str.slice(pos)%3Bstr%20%3D%20str.replace(%2F%25%2Fg%2C%20%22%22)%3Bvar%20iframe%20%3D%20document.getElementById(str)%3Bvar%20innerDoc%20%3D%20iframe.contentDocument%20%7C%7C%20iframe.contentWindow.document%3Bvar%20x%20%3D%20innerDoc.getElementsByClassName(%22ui-download-markdown%22)%3Bvar%20event%20%3D%20new%20CustomEvent('click'%2C%20%7B%20bubbles%3A%20true%2C%20cancelable%3A%20true%20%7D)%3Bx%5B1%5D.dispatchEvent(event)%7D)()
    ```
    
    

### __Example__
* [KLVN/MediasiteDownloader: A Bookmarklet (Favelet) for your browser to simply download lectures from a SonicFoundry Mediasite website, that is often used by colleges and universities.](https://github.com/KLVN/MediasiteDownloader)

    ```javascript=
    javascript:(function() {
        var page = window.location.href;
        if(new RegExp(".+Mediasite\\/Play\\/.+\\?usehtml5=true", "i").test(page)) {
            var vidSource = (document.getElementById("MediaElement").children)\[0\].src;
            var a = document.createElement("a");
            a.href = vidSource;
            a.setAttribute("download", "");
            document.body.appendChild(a);
            a.click();
            a.remove();
        } else if(new RegExp(".+Mediasite\\/Play\\/.+", "i").test(page)) {
            alert("Redirecting to HTML5 website...\\nClick again on Bookmarklet to download video.\\n\\nhttps://github.com/KLVN/MediasiteDownloader");
            location.href = page + "?usehtml5=true";
        }
    })();
    ```


---
↩️ back to [SUMMARY](SUMMARY.md)