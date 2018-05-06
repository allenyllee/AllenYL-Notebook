# Scrum__敏捷開發

[toc]
<!-- toc --> 

- [Scrum懶人包 – 10分鐘讀懂Scrum與敏捷軟體開發入門（含中文英文名詞對照） – 敏捷進化趣 Agile FunEvo](https://funevo.com/2015/06/27/scrum-ru-men-jie-shao-xin-shou-zhi-nan-introduce/)

    > [![2015-06-27_070937](https://funevo.files.wordpress.com/2015/06/2015-06-27_070937.png?w=840&h=577)](https://funevo.files.wordpress.com/2015/06/2015-06-27_070937.png)
    > 
    > 江湖上軟體開發有兩個大門派，第一個門派歷史跟軟體一樣久，心法是以流程為主軸，正式名稱[瀑布式開發（Waterfall）](http://wiki.mbalib.com/zh-tw/%E7%80%91%E5%B8%83%E6%A8%A1%E5%9E%8B)，最具代表的武功就是 [CMMI](http://baike.baidu.com/item/CMMI)，幾年前台灣政府大力推動支持。另一個門派在1990年代異軍突起，心法是以人為主軸，正式名稱為[敏捷式開發（Agile）](http://wiki.mbalib.com/zh-tw/%E6%95%8F%E6%8D%B7%E5%BC%80%E5%8F%91)，最知名的武功是 Scrum，但在台灣則是這一兩年才開始熱門起來。（註：Scrum 的原始意思是[橄欖球的爭球動作](http://weedyc.pixnet.net/blog/post/15119991-%E8%B6%B3%E7%90%83%E3%80%81%E6%A9%84%E6%AC%96%E7%90%83%E3%80%81%E7%BE%8E%E5%BC%8F%E8%B6%B3%E7%90%83)，在軟體界沒有翻譯成中文，都是直接叫 Scrum）
    > 
    >  兩個門派最大的不同在中心思想，用中國的哲學流派來比喻，**瀑布式開發是[法家](http://baike.baidu.com/view/22147.htm)，法為主，人為輔，強調「不別親疏，不殊貴賤，一斷於法」**。只要規則定下去，照著做就會有好產品，鐵打的營盤流水的官，人的因素要盡可能排除以利產出的一致性。
    > 
    > 而**敏捷式開發是[道家](http://baike.baidu.com/view/2762.htm)，人為主，法為輔，主張「道法自然」**。道是沒有一定的形式，要觀察目前的情境，考量人的天性，因勢利導，以求功成事遂，百姓皆謂我自然。
    > 
    > 總之敏捷式軟體開發門派更注重在人的層面，講求的是從**快速從經驗中學習反應和團隊的自我管理**。
    > 
    > 而 Scrum 這套武功之所以比起其他的武功如看板、極限開發（XP）更有名，是因為一般認為比較容易導入或入門。因為 Scrum 裡角色和活動定義明確，又不提技術細節，讓不懂技術的老闆也可以聽懂（技術活也是很重要滴，請參考XP）。 很多堂口導 Scrum 就落[入了做敏捷，而不是變敏捷](http://tdwi.org/articles/2010/06/02/being-agile-vs-doing-agile.aspx)的陷阱，如果組織已經在跑敏捷，可以[看看這清單確認一下是真敏捷，還是拜飛機式的敏捷](https://funevo.com/2016/04/06/cargo-cult-agile-min-jie-bai-fei-ji/) XD。
    > 
    > 如果還沒導入，恭喜你，可以先考慮 [Scrum 會帶你上天堂還是地獄](https://funevo.com/2015/05/27/scrum%e5%b8%b6%e4%bd%a0%e4%b8%8a%e5%a4%a9%e5%a0%82%ef%bc%9f/)，並可參考 [Scrum 不包生導入指南](https://funevo.com/2015/05/27/scrum%e4%b8%8d%e5%8c%85%e7%94%9f%e7%b0%a1%e6%98%93%e5%b0%8e%e5%85%a5%e6%8c%87%e5%8d%97/)，還有[破除敏捷=快的迷信](https://funevo.com/2015/05/28/%e5%a4%a9%e4%b8%8b%e6%ad%a6%e5%8a%9f%ef%bc%8c%e5%94%af%e5%bf%ab%e4%b8%8d%e7%a0%b4%ef%bc%9f-%e6%95%8f%e6%8d%b7%e9%96%8b%e7%99%bc%e6%98%af%e7%82%ba%e4%ba%86%e5%bf%ab%e5%97%8e%ef%bc%9f/)。
    > 
    > Scrum 角色
    > --------
    > 
    > Scrum 只有三種角色，至於其他角色如部門主管在 Scrum 框架外~裝作看不到~不討論。所有成員都要抱持[敏捷的精神和態度](https://funevo.com/2015/06/06/%e9%9b%9e%e7%8a%ac%e5%8d%87%e5%a4%a9%ef%bc%8cscrum%e9%81%a9%e5%90%88%e6%89%80%e6%9c%89%e4%ba%ba%e5%97%8e%ef%bc%9f/)。
    > 
    > 1.  **Development Team（Dev Team，開發團隊）**：可以獨立完成任務的特種部隊，人數5-9人（7+/-2）。大絕是我決定該怎麼做（How），武器是自我管理和持續改善的能力。每個人都有自己的特長，但依任務需求自行安排工作內容。類似射雕英雄傳裡全真七子所部的天罡北斗陣，如任一人受敵時，左右會來相救。
    > 2.  **Product Owner（PO，產品負責人）：：**[產品的守護者](https://funevo.com/2015/05/31/%e5%82%b3%e8%aa%aa%e4%b8%ad%e7%9a%84product-owner/)。大絕是要做什麼我說了算（What），武器是敏銳的市場嗅覺的和擺平利害關係人。如同射雕英雄傳裡北極星位對天罡北斗陣的影響，當郭靖站到了北極星位就可以驅動全真七子。PO 要決定產品的規劃和為產品的成敗負責，可以參考一些 [PO 常常絆倒的地方](https://funevo.com/2015/06/03/%e4%b8%80%e4%ba%9bpo%e7%9a%84%e6%80%aa%e5%91%b3%e9%81%93/)。
    > 3.  **ScrumMaster（SM，無中文名稱）：**[Scrum 功夫的傳道者](https://funevo.com/2015/06/04/%e5%a6%82%e7%a5%9e%e4%b8%80%e8%88%ac%e7%9a%84%e5%ad%98%e5%9c%a8%e4%b9%8bscrum-master/)，唯一的大絕是影響力，武器是異於常人的信心與耐心。有人覺的他是 Team Lead 或是 PM 的角色。但其實他沒人事權不能管人，沒財務權不能編預算，更可憐的是不能決定產品的走向，是個令人摧心的角色。最常見的安排是 [PM 直接轉 Scrum Master](https://funevo.com/2015/06/02/%e6%8f%9b%e4%ba%86%e6%96%b0%e5%90%8d%e7%89%87%ef%bc%8c%e6%88%91%e5%b0%b1%e6%98%afscrum-master%e4%ba%86-pm%e7%af%87%ef%bc%89/)，或是[主管自己跳下來兼 Scrum Master](https://funevo.com/2015/06/14/%e6%8f%9b%e4%ba%86%e6%96%b0%e5%90%8d%e7%89%87%ef%bc%8c%e6%88%91%e5%b0%b1%e6%98%afscrum-master%e4%ba%86-%e9%83%a8%e9%96%80%e4%b8%bb%e7%ae%a1%e7%af%87%ef%bc%89/)，[會把 Scrum Master絆倒的地方](https://funevo.com/2015/06/08/%e9%97%9c%e6%96%bcscrum-master%e7%9a%84%e4%b8%80%e4%ba%9b%e6%80%aa%e5%91%b3%e9%81%93/)也不少。
    > 
    > 以上三者又統稱 [Scrum Team 或 Team](https://funevo.com/2015/06/05/%e5%9c%98%e9%9a%8a%e5%92%8c%e9%96%8b%e7%99%bc%e5%9c%98%e9%9a%8a%e6%9c%89%e5%b7%ae%e5%97%8e%ef%bc%9f-%e8%ab%87scrum-team-vs-development-team/)。
    > 
    > Scrum 物件
    > --------
    > 
    > Scrum 中常會提到的物件與中文名稱。
    > 
    > 1.  **Item（物件）：** 又稱 Story，是 PO 定義的產品產出。Item 大小要講究，要可以讓團隊在一般的速率下，可以完成3-5個。太多太繁雜，太少萬一沒做完就感覺整個 Sprint 一事無成，對團隊信心是個打擊。
    > 2.  **Task（工作）：** 是 Dev Team 針對 Item（不是 PO 也不是 SM 哦），列出完成 Item 所需的工作。工作分配是開發團隊自己安排。
    > 3.  **Product Backlog（產品待辦清單）：** 由 PO 負責整理的產品願景圖，以 Item 為單位，施工順序由上而下。
    > 4.  **Sprint Backlog（衝刺待辦清單）：** Dev Team 向 PO 承諾這個 Sprint 會盡力完成的 Item List。以 Task 為單位。
    > 5.  **Potentially Shippable Product Increment（潛在可交付產品增量）：** 開發團隊的產出，簡單的說就是 PO 說要上線就可以馬上上線的東西才算數。
    > 6.  **Burndown Chart（燃盡圖）：** 有點類似怪物的血條，看看還剩多少血怪（Sprint Backlog）才死。以 Task 大小為單位。
    > 
    > Scrum活動
    > -------
    > 
    > Scrum 活動每一個都是有他的目的和時間限制（Time Boxed）。
    > 
    > 1.  **Sprint（衝刺）：** 顧名思義，當團隊決定要哪些 Item 後，就著手去衝。Sprint 長度定義上是1-4個禮拜，但實務上不要多過2個禮拜。而且 Sprint 長度應該要保持穩定盡可能不變。這樣才容易讓團隊掌握節奏，也容易預估和比較 Sprint 內的工作量。大原則是 Sprint 內的 Sprint Backlog 不改變（有原則就有例外）。
    > 2.  **Daily Scrum（每日站立會議）：** 每天10-15分鐘不能超時，目的是讓團隊資訊同步。一定要站著~罰站~為了讓大家長話短說。
    > 3.  **Sprint Planning（衝刺規劃會議）：** Sprint 開始時，討論一下這個 Sprint 團隊可以交付哪些Item。Item 優先順序 PO 決定，要選多少 Item 由 Dev Team 決定。
    > 4.  **Product Backlog Refinement / PBR（產品待辦清單精煉會議）：** PO 跟 Team 一起討論近期內會開始施工的 Item，主要是從商業和使用者角度切入，盡可能不觸及技術細節。
    > 5.  **Sprint Review（衝刺檢視會議）：** Sprint 結束時針對產品的會議，PO邀請利害關係人對產出給意見，是要可用的軟體才算產出。不準備Powerpoint或其他簡報，單純就軟體操作取得回饋。
    > 6.  **Sprint Retrospective / Sprint Retro（衝刺回顧會議，我偏好稱為『自省』會議）：** Sprint Review 後，Scrum Team 成員（Dev Team 或包含 PO），針對這個 Sprint 團隊的工作模式討論改善，并定出下個 Sprint 改善事項。為了創造一個安全的環境，原則上只有團隊成員才能參加。
    > 
    > Scrum 是個易學難精的架構，導入一個月就似模似樣入門了，但背後的精神如團隊自我組織、持續改善要數個月到數年才能見效。[持續學習](https://funevo.com/2015/06/01/scrum%e8%88%87%e6%95%8f%e6%8d%b7%e9%96%8b%e7%99%bc%e6%9b%b8%e5%96%ae/)是必要的。
    > 
    > Scrum 的架構適合一個產品配合1-3個開發團隊。如果一個產品需要更多人~打群架~，有兩套基礎於Scrum 的終極陣法，一套是同樣以人為本的 [LeSS（Large Scale Scrum）](http://less.works/)，另一套是加入流程控制的[SAFe（Scaled Agile Framework）](http://www.scaledagileframework.com/)，可以[參考 LeSS 和 SAFe 的比較](http://www.slideshare.net/gosei/xp2015-scaling-agility-explored-less-safe-comparison)，和[兩者運用組織權力的差異](http://gosei.fi/scaling-agility-or-bureaucracy/)。
    > 