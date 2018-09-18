# DataBase__筆記

[toc]
<!-- toc --> 


# Introduction

## RDBMS vs. NoSQL

- [邁向王者的旅途: [筆記] RDBMS v.s. NoSQL](https://shininglionking.blogspot.com/2018/04/rdbms-vs-nosql.html)

    > 
    > 現在主流的資料庫像是 MySQL 之類的是關聯式資料庫 (RDBMS)，不過隨著網路的發展，關聯式資料庫的特性在某些應用上其實沒有那麼適合。比方說，你對於資料間的關聯性沒那麼在意，你在意的是特定人、事或物的 "狀態" 變動，特別是這種狀態的變動非常大量且頻繁時，關聯式資料庫在處理這種需求就會變得力不從心，也因此後來有發展出了 NoSQL 這東西是專門針對這種應用設計的。而這次被主管要求要看的 MongoDB 正是一種 NoSQL DB。
    > 
    > **RDBMS (Relational Database Management System)**\
    > 關聯式資料庫在意的是資料之間的關聯性，也因此在設計關聯式資料庫時**綱要 (Schema)** 就顯得非常重要。因為這關係的是你要如何設計你的資料表 (像是要擁有那些欄位)、資料表之間的關聯性如何設計，接著就可以透過 SQL (structural language) 在不同資料表之間利用他們的關聯性組合 / 過濾出你要的資訊。
    > 
    > 基於上述的特徵， **RDBMS 有一件事情非常重要：正規化 (normalization)** 。藉由正規化避免不同資料表儲存了重複的資訊，如此一來在資料更新時可以 DB 中有重複的資料沒有同時被更新。不過也正因為這件事，綱要的設計就變得更重要，因為這時綱要的設計牽涉到的不只是正規化的問題，該怎麼更新、儲存資料到資料表就跟你的綱要有密切的關連性。
    > 
    > 從上面的說明應該足以了解綱要的設計對於 RDBMS 的重要性，不過這同時也引出了一個問題：**如果一開始的綱要設計不良，使用一段時間後才想要變更怎麼辦**? 嗯，通常這就是一件大工程，因為第一件事情是要把所有的資料表變更成新的綱要架構，資料量大的時候這很費工；另一件事情就是所有用到這個 DB 的程式也都要更新修改，因此這也是一件大工程。
    > 
    > RDBMS 的另一個問題也是從綱要 & 正規化來的。想想看現今網路應用的資料量會有多龐大 (像是 FB 或 google 在處理的資料量)，這些資料絕對不可能只讓一台主機去處理，一定會分散在許多主機。當 RDBMS 的資料表分散在不同主機時，想要取得某個查詢的結果或者是要更新資料時會變得相當麻煩：因為你可能會需要從主機 A 的資料表 X 去跟主機 B 的資料表 Y 先利用關鍵字找出你有興趣的資料區間，接著再這把這些資料統合成你要的結果。如果資料量又更多時，問題也不會因為僅僅多加幾台主機就能緩解，因為如何維護著這些資料表的關聯性也會是一大挑戰。所以**就結論而言，在分散式系統的環境下 RDBMS 的優勢就難以發揮了**。這些都是導致後來提出 NoSQL 的契機。
    > 
    > **NoSQL (Not Only SQL)**
    > 
    > 相較於 RDBMS，NoSQL 其中一大特色就是設計 DB 時可以無綱要吧，他儲存資料的方法不像 RDBMS 有固定的欄位與綱要，他的概念偏向於 
    > 
    > 1.  每一筆資料都當成一個文件 (而且每個文件可以長得不一樣)
    > 2.  每一個文件都給他一個唯一的編號
    > 
    > 其實這樣的組合就有點像是一個 hash table 的概念。NoSQL 在意的是某個編號底下的文件有沒有需要更新、需不需要新增/刪除某份/些文件等等，因此相較於 RDBMS，文件之間是否有重複的資料以及是否有任何關連性比較不是 NoSQL 在意的重點，也因此早期 NoSQL 好像真的就是指不用 SQL，不過現在普遍認為 NoSQL 應該是 Not Only SQL，其中一個原因應該是來自於 NoSQL 其實也是可以支援部分 SQL 語法的。
    > 
    > 要舉例的話，比較常看到的例子就是某個遊戲的玩家資料，又或者是社群網站上的個人資料 (像是 FB 就自己開發了一套 NoSQL 叫 Cassandra) 等等。
    > 
    > NoSQL 基於這樣的特性，要隨時增減伺服器的數量會變得比 RDBMS 容易許多，當然相對的也會有一些問題。舉例來說，RDBMS 通常都會提供 ACID (下面會介紹) 的保證，而 NoSQL因為儲存資料的方式本來就已經沒有固定的格式甚至可能有大量的重複資料 (想像一下：線上遊戲的廠商想要把某項武器修改調整他的屬性甚至是移除?) 這種狀況下還要 NoSQL 提供 ACID 的保證無疑會浪費掉 NoSQL 的優勢，也因此現在 NoSQL DB 提供的則是 CAP (也是下面會介紹)。
    > 
    > ### Scaling
    > 
    > Scaling 指的是 DB 如何提升他的處理能力，分成 vertical 跟 horizontal
    > 
    > -   **Vertical scaling**
    > 
    >     -   直接提升主機本身的處理能力 (EX: 加大硬碟或是 CPU 處理速度加快)
    >     -   就像早期個人電腦變快的方法都是直接加速 CPU 的時脈，這種針對零件本身的效能提升
    > 
    > -   **Horizontal Scaling**
    > 
    >     -   一台主機不夠你有沒有用兩台?
    >     -   增加主機的數量就是 horizontal scaling 的精神，就像現在 CPU 都是多核心那樣，藉由增加數量來增加可處理的餘裕
    >     -   不過增加數量跟能提升效能不見得是正比，比方說 CPU 是八核心，結果每次都只讓其中 一個核心做事的話你的電腦跑起來還是會很慢
    > 
    > 以 RDBMS 跟 NoSQL 來看，RDBMS 用 vertical scaling 比較容易看到效能的提升，而 NoSQL 的架構則是非常容易採用 horizontal scaling，也是現在 web-base 應用最需要的特色
    > 
    > ### ACID
    > 
    > -   **A = Atomicity**
    > 
    >     -   Each transaction be "all or nothing"
    > 
    > -   **C = Consistency**
    > 
    >     -   Any transaction will bring the database from one valid state to another
    > 
    > -   **I = Isolation**
    > 
    >     -   Concurrent execution of transactions results in a system state that would be obtained if transactions were executed sequentially
    > 
    > -   **D = Durability**
    > 
    >     -   Once a transaction has been committed, it will remain so, even in the event of power loss, crashes, or errors.
    > 
    > RDBMS 很講究資料的正確性，因此通常都會提供 ACID 的保證：\
    > A: 一道指令下去要嘛成功不然就是完全沒影響 (all or nothing)。比方說轉帳這件事，你不會希望轉帳失敗後對方沒收到錢但你的帳戶還是被扣錢了\
    > C: 資料庫的一致性。同樣是轉帳這件事當例子，A 轉了 10 元給 B，結果 B 只拿到 5 元就是不一致，這時候資料庫比須取消這項操作\
    > I: 數道指令同時執行跟他們以某項順序依序執行，最後的結果必須完全一樣。還是拿轉帳當例子，A 轉給 B 10，B也要轉給C10，A、B 同時轉帳跟 A 先轉再換 B 以及 B 先轉帳再換 A 最後的結果必須都要一樣。\
    > D: 一道指令成功後就永遠都是有效的。你不會希望轉帳成功後因為突然停電結果發現剛剛轉帳的結果不見了。
    > 
    > NoSQL 因為其特性難以保證 ACID，特別是 consistency 這一項有時候只會提供 eventually consistent (也就是現在不一致沒關係，過了一段時間後會一致就好)，所以 NoSQL 是有可能出現同一筆資料現在讀跟晚點再讀結果不一樣這種情形...而且由於 NoSQL 比較常被用在分散式的儲存環境，相較於 ACID，更加注重的是下面的 CAP。
    > 
    > ### CAP Theorem
    > 
    > -   **C =  Consistency**
    > 
    >     -   Every read receives the most recent write or an error
    > 
    > -   **A = Availability**
    > 
    >     -   Every request receives a (non-error) response -- without guarantee that it contains the most recent write
    > 
    > -   **P = Partition tolerance**
    > 
    >     -   The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes
    > 
    > #### Theorem
    > 
    > It is impossible for a distributed data store to provide more than two out of the above three guarantees.
    > 
    > CAP 特別針對的是分散式的儲存環境 (所以就是 NoSQL DB 最常被應用的環境)。而且根據這個理論會發現不可能同時提供三個保證，因此目前 NoSQL 通常是提供 2 個，至於是哪 2 個就要看設計者了。不過要說 MongoDB 提供了哪兩個...根據[這一篇](https://stackoverflow.com/questions/11292215/where-does-mongodb-stand-in-the-cap-theorem?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)來看似乎可以根據你的設定有所改變。
    > 
    > 這邊要特別注意的是提供 CAP 的保證根提供 ACID 的保證是兩回事，ACID 就算不會全部提供也不代表都不會有，像是 MongoDB 就有提供 [Read Isolation 跟 Consistency](https://docs.mongodb.com/manual/core/read-isolation-consistency-recency/) 的保證，而且 MongoDB 也是會[依據情況提供 Atomicity 的保證](https://docs.mongodb.com/manual/core/write-operations-atomicity/)的。
    > 



# SQL

## Introduction

- [閃開！讓專業的來：SQL 與 NoSQL - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10187443)

    > 資料庫的存取方式，是靠著指令來進行的。這個指令就叫做：SQL，Structured Query Language。你只要對著資料庫下指令，你想查詢的資料就會迅速地來到你的身邊。
    > 
    > 對於資料的存取，最基本的方式就是四種，建立、讀取、更改、刪除，簡稱 CRUD
    > 
    > 1.  Create
    > 2.  Read
    > 3.  Update
    > 4.  Delte
    > 
    > 假設我們的 table 現在長這樣：\
    > ![http://ithelp.ithome.com.tw/upload/images/20161225/200913469RQB6lmxMw.png](http://ithelp.ithome.com.tw/upload/images/20161225/200913469RQB6lmxMw.png)
    > 
    > ### Create
    > 
    > ```
    > insert into users(name, phone) values (peter, 1234)
    > insert into users(name) values (peter)
    > insert into members(username) values (username)
    > 
    > ```
    > 
    > 提供給你三句不一樣的語句，你從裡面可以觀察出一些規律。`insert into TABLE_NAME(a,b..) values(a,b..)`這個指令是不會變的，變得只有你的 table 名稱以及你要新增資料的欄位。上面的第一句`insert into users(name, phone) values (peter, 1234)`，翻譯成白話文就是：「插入一筆 name 是 peter, phone 是 1234 的資料到 users 這個 table 裡面去。」
    > 
    > ### Read
    > 
    > ```
    > select phone from users
    > select name, phone from users
    > select * from users
    > select phone from users where name=peter
    > 
    > ```
    > 
    > 一樣給你幾句，所以你一樣可以從這幾句裡面很聰明地找出一些規律，不變的就是`select...from`，我可以把每一句翻成白話文給你聽：
    > 
    > 1.  `select phone from users`，讀出 users 這個 table 裡面所有的 phoen 這個欄位
    > 2.  `select name, phone from users`，讀出 users 這個 table 裡面所有的 name 跟 phone 這兩個欄位
    > 3.  `select * from users`，讀出 users 這個 table 裡面所有的欄位（`*`是特殊符號，代表所有的意思）
    > 4.  `select phone from users where name=peter，`讀出 users 這個 table 裡面，符合條件`name=peter`的一筆資料的 phone 這個欄位
    > 
    > ### Update
    > 
    > ```
    > update users set phone=123
    > update users set phone=123 where name=peter
    > 
    > ```
    > 
    > 1.  把 users 裡面的所有資料的 phone 更新成 123
    > 2.  把 users 裡面符合`name=peter`這筆資料的 phone 更新成 123
    > 
    > 實務上在做事情的時候，在用第一種類型的語句時絕對要千千萬萬分注意。因為你一個不小心忘記加上`where`的話，資料庫裡面所有的資料都會被你更新...這是一件很可怕的事情。
    > 
    > ### Delete
    > 
    > ```
    > delete from users where name=peter
    > delete from users where name=peter and phone=123
    > 
    > ```
    > 
    > 1.  把 users 裡面所有符合`name=peter`的資料刪除
    > 2.  把 users 裡面所有符合`name=peter`而且`phone=123`的資料刪除
    > 
    > 這個指令跟上面那個更新一樣，要用的時候絕對要非常小心。
    > 
    > 上面的這些指令都是最基本的用法，但很多時候你會需要更多更多不同的指令才能組合出你想要的資料。
    > 
    > 有興趣的朋友可以到[codecademy](https://www.codecademy.com/learn/learn-sql)去練習，或者是參考我個人強力推薦的一系列教學：[MySQL 超新手入門](http://www.codedata.com.tw/database/mysql-tutorial-getting-started/)。


## PostgreSQL


# NoSQL

## Introduction

- [閃開！讓專業的來：SQL 與 NoSQL - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10187443)

    > 首先，SQL 就是一個拿來查詢資料庫的語言。因為他只是一個語言，所以你沒辦法說「我的程式是用 SQL 當資料庫」。SQL 並不是一個資料庫系統，MySQL 才是。現在比較多人用的資料庫系統一般就三個：MySQL, PostgreSQL 還有 Microsoft SQL Server。共通點就是名字裡面都有 SQL。
    > 
    > 
    > 任何一種以 SQL 為基礎的資料庫系統，都有差不多的特性，例如說他們必須事先定義好 Schema，你可以想成是資料庫的規格書。就是資料庫裡面要有哪些欄位、每一個欄位的資料型態是什麼。你在建立一張 Table 的時候，也是要用資料庫指令去新建的：
    > 
    > ```
    > CREATE TABLE users(
    >   id int,
    >   name char(50),
    >   phone  char(20)
    > );
    > 
    > ```
    > 
    > 會先把每一個欄位的名稱跟型態都先固定住。這個就是 SQL 的一個特點。還有另外一個特點是「關聯式資料庫」，這是什麼意思呢？就是因為要讓資料儲存跟取得容易，所以會用「關聯」的方式把一些東西切開來。
    > 
    > 舉例來說好了，你現在要寫一個部落格系統，於是你需要一個可以儲存文章的 Table，欄位的部分你可能會這樣設計：
    > 
    > ```
    > id, author, content, create_time
    > 
    > ```
    > 
    > 接著你要加入一個可以在文章底下留評論的功能，你就需要另外一張 Comments 的 Table。因為你必須知道這個評論是屬於哪一篇留言的評論，所以你要在裡面新增一個欄位叫做`post_id`，才能把某篇文章跟這一堆評論「關聯」起來。所以文章跟評論的關係就是「一對多」，一篇文章可以有很多個評論。
    > 
    > ```
    > id, post_id, content, create_time
    > 
    > ```
    > 
    > 如果你想撈出文章 id 是 123 的所有評論，你只要 `select * from comments where post_id=123` 這樣就好了。當然這個是屬於比較簡單的範例，還有更複雜的場景以及更複雜的關係。這些你在我上面提供的那個超新手入門應該都看得懂，我就先不講了。
    > 
    > 鋪陳了這麼久，終於可以來講 NoSQL，這個名詞只是為了強調他跟上面我們講的那些關聯式資料庫系統不太一樣，所以用了 NoSQL 這個詞。其中最大的差別大概就是 NoSQL 沒有 schema 這種東西，所以你不必事先知道你要存哪些資料。這樣的好處當然就是比較彈性，可是相對的你在查詢資料的時候速度也會比較慢一點。而且這些 NoSQL 系統，儲存資料的格式通常都是 JSON。
    > 
    > 以上面那個文章跟評論的系統為例，如果你把資料存在 NoSQL 的資料庫裡面，可能就會長這樣：
    > 
    > ```
    > {
    >   id: 1,
    >   author: 'huli',
    >   content: '大家好',
    >   create_time: 12345,
    >   comments: [
    >     {
    >       id: 1,
    >       content: 'comment 1',
    >       create_time: ...
    >     }, {
    >       id: 2,
    >       content: 'comment2',
    >       create_time: ...
    >   }
    >   ]
    > }
    > 
    > ```
    > 
    > 有沒有發現哪邊不一樣？他把評論直接跟文章本身存在一起了！這點是 SQL 做不到的事情。（其實硬要做也是可以啦，但你會發現非常麻煩而且根本沒必要，查詢的時候也很不方便。你可以想想看怎麼做。不過最近 MySQL, postgreSQL 提供了資料格式是 JSON 的欄位，這又是另外一回事了）。
    > 
    > 根據我個人的使用經驗來說，NoSQL 最適合的一點是搜集數據。例如說現在很多手機 App 其實會偷偷搜集你資料傳回去，做一些數據分析之類的。他可能會搜集：手機廠牌、型號、作業系統版本、安裝過的 App 等等的。這時候如果你是用一般傳統的 SQL 資料庫，你要怎麼定義 Schema？你的欄位會有超級多個，而且一旦你想要儲存新的追蹤資訊的時候，你就必須去改一次資料庫，這是很麻煩的行為。這時候用 NoSQL 就很方便了，你只要直接把資料存進去就好，什麼都不用想。你不必知道到底有多少項的追蹤資訊。
    > 
    > ---
    > 
    > SQL 跟 NoSQL 並不是互斥的概念，你可以在你的系統裡面用 SQL 類的資料庫系統儲存文章、評論，同時也用 NoSQL 類的資料庫來搜集使用者資訊。這些本來就是根據你的業務不同而定的。最慘的是那種根本不知道為什麼要用的，或者是盲目追求潮流的。再強調一遍，你要根據你的業務來選擇適合的技術棧。沒有最好的技術棧，只有最適合自己的。就算 NoSQL 聽起來比較潮，但是適合用 SQL 的地方，就乖乖用 SQL 就好。
    > 



## List Of NoSQL Databases
- [NOSQL Databases](http://nosql-database.org/)


## Doucment Database

### MongoDB

## Graph Database

### Neo4j

### OrientDB

- [Case Studies, White Paper, and Success Stories | OrientDB](https://orientdb.com/case-studies/)


- [mongodb - Is there any reason not to use OrientDB? - Stack Overflow](https://stackoverflow.com/questions/39445325/is-there-any-reason-not-to-use-orientdb)

- [Is there any reason not to use OrientDB? Is there any reason to opt for MongoDB or Neo4j? - Quora](https://www.quora.com/Is-there-any-reason-not-to-use-OrientDB-Is-there-any-reason-to-opt-for-MongoDB-or-Neo4j)


- [OrientDB vs MongoDB: The Power of a Graph-Document DB | OrientDB](https://orientdb.com/orientdb-vs-mongodb/)

    > Relationships
    > -------------
    > 
    > ![](https://orientdb.com/wp-content/uploads/json_embedded.jpg)
    > 
    > This is a JSON document representing a simplified Order. Note the "customer" property, which is embedded inside the parent Order object.
    > 
    > This is a very common method with Document Databases to overcome the performance bottlenecks of Relational DBMS when a JOIN is executed. With MongoDB, you can store the _id of the connected customer, but this is still similar to doing JOINs that have a *high run-time cost* and do not scale when the database size increases (to know more about this topic, please look at the presentation ["Why Relationships are cool, but JOIN sucks"](http://www.slideshare.net/lvca/why-relationships-are-cool-but-join-sucks-28997951)).
    > 
    > OrientDB can embed documents like any other Document Database, but it can also connect documents like a Relational Database. The main difference is that OrientDB doesn't use the costly JOIN, but rather uses direct, super-fast links taken from the Graph Database world.
    >
    >
    > The illustration on the right shows how the original document has been split in two documents linked using the Customer's Record ID #8:124 to connect the Order to the Customer document. Links can be thought of as in-memory pointers, but persistent on the disk.
    > 
    > Why connect documents rather than embedding them? For two reasons: 1. there are no duplicates, resulting in a smaller and lighter database, and 2. because it's faster. A smaller database means better usage of RAM, thus allowing more caching.
    > 
    > Upon loading the Order document, OrientDB will assemble the entire document by fetching all the connections transparently.
    > 
    > ![](https://orientdb.com/wp-content/uploads/json_linked.jpg)

- [OrientDB vs Neo4j - Graph Power and Document Flexibility | OrientDB](https://orientdb.com/orientdb-vs-neo4j/)


    > Performance
    > -----------
    > 
    > According to an [independent benchmark by Tokyo Institute of Technology and IBM Research **](https://orientdb.com/wp-content/uploads/xgdbench_cloudcom2012.pdf), OrientDB is 10X faster than Neo4j on Graph operations among all the workloads. Numbers are the throughput as operations per second. Higher is better.
    > 
    > Price and Licensing
    > -------------------
    > 
    > With OrientDB Community, we opted for the completely permissive Apache 2 Open Source license. Free for any purpose, even commercial! We also didn’t disable the features allowing horizontal scale and fault tolerance. Cluster, shard and replicate to your heart’s content. Let your project expand globally without the fear of license restrictions. With a (A)GPL DBMS, you can embed it only if your project is Open Source as well otherwise you need a Commercial license from Neo4j.
    > 
    >
    > Scalability
    > -----------
    > 
    > Neo4j supports replication, but this is an Enterprise feature not released in the FREE Open Source Community Edition. Furthermore, the replication follows the Master/Slave architecture with a huge bottleneck on write operations: only one server can be the master, so the Neo4j write throughput is limited to the capacity of the single Master server. This means that Neo4j isn't able to scale on writes.
    > 
    > OrientDB, instead, supports a Multi-Master + Sharded architecture: all the servers are masters. The throughput is not limited by a single server. With OrientDB, the global throughput is the sum of the throughput of all the servers.
    > 
    > This is also called Linear Scalability.
    > 
    > Complex Domains
    > ---------------
    > 
    > OrientDB, instead, supports the [creation of schemas around graphs](http://orientdb.com/docs/last/Graph-Schema.html). Furthermore, the true *inheritance* and *polymorphism* allow you to create subclasses of Vertex and Edge. For example, you can have "Customer" and "Provider" that extend the common vertex class "Account" by inheriting all of the fields. By using the schema, you can also setup complex constraints against vertices and edges properties.
    > 
    > ![](https://orientdb.com/wp-content/uploads/flexible-domain.png)
    > 
    > 
    > Complex Types
    > -----------------
    > 
    > While OrientDB supports a [rich set of types](http://orientdb.com/docs/last/Types.html), Neo4 supports only primitive types. With Neo4j, it's not possible to store decimal numbers (amounts, currencies, salaries, etc.) without losing precision, because "float" and "double" Java types use the floating point technique. OrientDB, instead, provides the "decimal" type to handle numbers with no precision lost.
    > 
    > The same is for dates. Neo4j [has no direct support for date types](https://groups.google.com/d/msg/neo4j/bG4NH0ltvpg/Xp2pw3YogvMJ), so the management of temporal data is the responsibility of the developer that must convert it into milliseconds from 1970. OrientDB, instead, provides DATE and DATETIME types to handle dates easily.
    > 
    > OrientDB supports other complex types such as Binary to store BLOB (Binary Large Objects), Embedded to store embedded objects recursively, Collections and Maps.
    > 
    > Deleted Records
    > ----------------
    > 
    > One of the most important features of an Operational DBMS is that it shouldn't require a restart or downtime for maintenance. Neo4j [isn't able to automatically reclaim the space of deleted records](https://multi-model-dba.blogspot.it/2016/10/solving-neo4js-space-reclaim-issue-with.html) and it requires a complete restart of the server. In comparison, OrientDB automatically reuses the freed space and such operations are transparent and occur while the server is online.
    > 


