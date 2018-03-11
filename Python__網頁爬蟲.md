# Python__網頁爬蟲

<!-- toc --> 
[toc]

## Tools
* 線上 Regex 教學
    * [RegexOne - Learn Regular Expressions - Lesson 1: An Introduction, and the ABCs](https://regexone.com/)

* facebook
    * [圖形 API 測試工具 - Facebook for Developers](https://developers.facebook.com/tools/explorer)

## Library

* [Beautiful Soup Documentation — Beautiful Soup 4.4.0 documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

* [afunTW/ptt-web-crawler: PTT 網路版爬蟲](https://github.com/afunTW/ptt-web-crawler)

- [afunTW/Python-Crawling-Tutorial: Python crawling tutorial](https://github.com/afunTW/Python-Crawling-Tutorial)

- [afunTW/Test-Crawling-Website: Using Bootstrap Template as demo page](https://github.com/afunTW/Test-Crawling-Website)

## HTTP Basic
* [HTTP request methods - HTTP | MDN](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Methods)

    [`GET`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET)

    The `GET` method requests a representation of the specified resource. Requests using `GET` should only retrieve data.

    [`POST`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST)

    The `POST` method is used to submit an entity to the specified resource, often causing a change in state or side effects on the server

* [HTTP 狀態碼 - HTTP | MDN](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Status)

    __成功回應__

    [`200 OK`](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Status/200 "The documentation about this has not yet been written; please consider contributing!")

    請求成功。成功的意義依照 HTTP 方法而定：  
    GET: 資源成功獲取並於 message body 內發送。  
    HEAD: entity 標頭已於 message body 內。  
    POST: 已傳送 message body 內的 resource describing the result of the action。  
    TRACE: 伺服器已接收到 message body 內含的請求訊息。

    __用戶端錯誤回應__

    [`403 Forbidden`](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Status/403 "The documentation about this has not yet been written; please consider contributing!")

    用戶端並無訪問權限，所以伺服器給予應有的回應。

    [`404 Not Found`](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Status/404 "The documentation about this has not yet been written; please consider contributing!")

    伺服器找不到請求的資源。因為在 web 上它很常出現，這回應碼也許最為人所悉。

* [淺談 HTTP Method：表單中的 GET 與 POST 有什麼差別？ - Soul & Shell Blog](https://blog.toright.com/posts/1203/%E6%B7%BA%E8%AB%87-http-method%EF%BC%9A%E8%A1%A8%E5%96%AE%E4%B8%AD%E7%9A%84-get-%E8%88%87-post-%E6%9C%89%E4%BB%80%E9%BA%BC%E5%B7%AE%E5%88%A5%EF%BC%9F.html)

    假設 GET 表示信封內不得裝信件的寄送方式，如同是明信片一樣（感謝網友 Kevin 的建議，採用明信片來詮釋 GET），你可以把要傳遞的資訊寫在信封(http-header)上，寫滿為止，價格比較便宜。然而 POST 就是信封內有裝信件的寄送方式（信封有內容物），不但信封可以寫東西，信封內 (message-body) 還可以置入你想要寄送的資料或檔案，價格較貴。

    使用 GET 的時候我們直接將要傳送的資料以 Query String（一種Key/Vaule的編碼方式）加在我們要寄送的地址(URL)後面，然後交給郵差傳送。使用 POST 的時候則是將寄送地址(URL)寫在信封上，另外將要傳送的資料寫在另一張信紙後，將信紙放到信封裡面，交給郵差傳送。


## facebook graph API

* [facebook.com/robots.txt](https://www.facebook.com/robots.txt)

* [變更紀錄 - 圖形 API](https://developers.facebook.com/docs/graph-api/changelog)
* [Versioning - 應用程式開發](https://developers.facebook.com/docs/apps/versions)


* [如何不寫程式取得 Facebook 粉絲專頁永久 Access Token？](https://goodjack.blogspot.tw/2017/08/how-to-get-facebook-permanent-page-access-token.html)

    __步驟 4：延長/換取長期 Token__

    授權後，會拿到一組短期的用戶存取權杖（short-lived user access token）。點擊 Access Token 欄位中的 ⓘ 可以看到這個 token 的相關資訊，目前這組 token 是有到期時間的。這時選擇下方的「以存取權杖工具開啟（Open in Access Token Tool）」。  
    ![enter image description here](https://i.imgur.com/soDctZE.png)

    網頁會跳轉至 [Access Token Tool](https://developers.facebook.com/tools/debug/accesstoken)，我們可以在這裡看到這個 token 詳細的屬性。  
    ![enter image description here](https://i.imgur.com/FxakUsw.png)

    點擊下方的「展延存取權杖（Extend Access Token）」  
    ![enter image description here](https://i.imgur.com/emDeKO9.png)

    即可取得長期權杖（long-lived access token）。  
    **注意：這時候的「長期」可能只有 60 天**  
    ![enter image description here](https://i.imgur.com/AS3dT2a.png)

    __步驟 5：取得永久粉絲專頁 Access Token__

    將以上 long-lived access token 複製貼回 Graph API Explorer 的 Access Token 欄位，按下右方提交（Submit）按鈕。  
    ![enter image description here](https://i.imgur.com/V0usIBx.png)

    此時點擊 Access Token 欄位中的 ⓘ，可以看到這組 user access token 的資訊中，已經沒有顯示 Expiration Time，代表此組 user access token 已經沒有時效限制。  
    ![enter image description here](https://i.imgur.com/kWwDKDJ.png)

    保險起見，我們可以進到 Access Token Tool 確認，確實顯示到期日（Expires）欄位顯示為永不（Never）。  
    ![enter image description here](https://i.imgur.com/BiVdZp3.png)

    回到剛剛的 Graph API Explorer 頁面，將下方的 GET 要求（GET request）欄位的網址修改為 `me/accounts`，即可一次取得所有粉絲專頁的永久權杖（permanent page access token）。  
    ![enter image description here](https://i.imgur.com/uMxeVn8.png)

    可以個別拿去 Access Token Tool 確認，這裡就不再贅述了。



* 如何取得粉絲團的id, name, fan_count, about?

    1. 先取得url 上的英文id 
    ![](https://screenshotscdn.firefoxusercontent.com/images/ad696a8d-4d24-4fde-9c8a-8631325d7c3b.png)
    
    2. 貼到 [圖形 API 測試工具 - Facebook for Developers](https://developers.facebook.com/tools/explorer) Get 欄位
    ![](https://screenshotscdn.firefoxusercontent.com/images/ec1479d6-3b99-48b6-9a8f-b85f70c4db70.png)
    
    