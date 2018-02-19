# Javascript___練習

## Useful Tool
* 線上JavaScript編輯器
    * [Dashboard - JSFiddle - Online JavaScript Editor - jQuery, Angular, Backbone, Underscore, Knockout, YUI](https://jsfiddle.net/user/dashboard/)
* 線上 Javascript code 清理工具
    * [JavaScript Cleaner - Free Online JS Beautifyer](https://html-cleaner.com/js/)
* 線上 Bookmarklet 產生器
    * [Bookmarklet Creator with Script Includer - Peter Coles](https://mrcoles.com/bookmarklet/)

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