# Knowledge_Graph__資料蒐集

[toc]
<!-- toc --> 

## 知識圖譜(Knowledge Graphs)


- [知識圖譜技術原理介紹 - 壹讀](https://read01.com/zh-tw/QQ7QP.html)

- [FRED - Home](http://wit.istc.cnr.it/stlab-tools/fred/)

- [T2KG: An End-to-End System for Creating Knowledge Graph from Unstructured Text
Natthawut Kertkeidkachorn, Ryutaro Ichise](https://aaai.org/ocs/index.php/WS/AAAIW17/paper/viewPaper/15129)

- [[1711.01714] End-to-End Video Classification with Knowledge Graphs](https://arxiv.org/abs/1711.01714)

- [A*STAR OAR: Object Detection Meets Knowledge Graphs](http://oar.a-star.edu.sg/jspui/handle/123456789/2147)


- [[1709.02314] Representation Learning for Visual-Relational Knowledge Graphs](https://arxiv.org/abs/1709.02314)

- [[1610.00782] Network Structure Inference, A Survey: Motivations, Methods, and Applications](https://arxiv.org/abs/1610.00782)

- [[1709.05584] Representation Learning on Graphs: Methods and Applications](https://arxiv.org/abs/1709.05584)


- [[1503.00759v1] A Review of Relational Machine Learning for Knowledge Graphs: From Multi-Relational Link Prediction to Automated Knowledge Graph Construction](https://arxiv.org/abs/1503.00759v1)

- [Challenges of Knowledge Graphs – Sebastien Dery – Medium](https://medium.com/@sderymail/challenges-of-knowledge-graph-part-1-d9ffe9e35214)

- [Building The LinkedIn Knowledge Graph | LinkedIn Engineering](https://engineering.linkedin.com/blog/2016/10/building-the-linkedin-knowledge-graph)

- [(3) Big Tree: Using Machine Learning to Create a Knowledge Graph of Mankind - YouTube](https://www.youtube.com/watch?v=xohuO5l4ak8)


- [Getting Started with Knowledge Graphs](https://www.slideshare.net/phaase/getting-started-with-knowledge-graphs)

- [Knowledge graph refinement: A survey of approaches and evaluation methods - Semantic Scholar](https://www.semanticscholar.org/paper/Knowledge-graph-refinement%3A-A-survey-of-approaches-Paulheim/93b6329091e215b9ef007a85c07635f09e7b8adb)


### Graph tools

- [What tools are you using for knowledge graph building? | Hacker News](https://news.ycombinator.com/item?id=14315129)


#### Graph Commons

- [Graph Commons – Map networks together](https://graphcommons.com/)

#### Nifty

- [Nifty - Forbidden Forest - Access Knowledge discovery in education and reference.](http://nifty.works/)

#### GRAKN.AI

- [GRAKN.AI - The Knowledge Graph](https://grakn.ai/)


#### google cayley

- [cayleygraph/cayley: An open-source graph database](https://github.com/cayleygraph/cayley)

    - [Build a Small Knowledge Graph Part 1 of 3: Creating and Processing Linked Data - YouTube](https://www.youtube.com/watch?v=W9pRpSW_KqA)


    - [Build a Small Knowledge Graph Part 2 of 3: Managing Graph Data With Cayley - YouTube](https://www.youtube.com/watch?v=0oOwrBEeQss)

    - [Build a Small Knowledge Graph Part 3 of 3: Activating Graph Data With Actions - YouTube](https://www.youtube.com/watch?v=KB94dIamAQc)

#### NOUS

- [[1606.02314] NOUS: Construction and Querying of Dynamic Knowledge Graphs](https://arxiv.org/abs/1606.02314)

    - [streaming-graphs/NOUS: NOUS: Construction, Querying and Reasoning with Knowledge Graphs](https://github.com/streaming-graphs/NOUS)

#### OrientDB

- [Why relationships are cool but "join" sucks](https://www.slideshare.net/lvca/why-relationships-are-cool-but-join-sucks-28997951)

    > ![](https://screenshotscdn.firefoxusercontent.com/images/34a800a2-9b99-41ba-bdd1-249164e4bed6.png) 


### Datasets

- [Datasets for Knowledge Graph Creation](http://ri-www.nii.ac.jp/VSim/index.html)

- [Wikidata](https://www.wikidata.org/wiki/Wikidata:Main_Page)

    - [Google 宣佈關閉知識庫 FreeBase，將資料移轉至 WikiData | TechNews 科技新報](https://technews.tw/2014/12/18/google-shut-down-freebase-will-import-the-entries-into-wikidata/)

### Introduction

- [What Are Knewton’s Knowledge Graphs? – Knerd – Medium](https://medium.com/knerd/what-are-knewtons-knowledge-graphs-f6a118acc722)

    > In many cases, a given learning objective can have multiple direct prerequisites. A simple example of a learning objective with two prerequisites can be found by looking at the learning objective requiring students to **divide fractions.** To divide fraction X by fraction Y, you multiply X times the reciprocal of Y. This means that in order to be able to divide fractions, you must already be able to (1) **multiply fractions** and (2) **find reciprocals of fractions**.
    > 
    > ![](https://cdn-images-1.medium.com/max/1000/1*0keLRee_m4g87hEuNowAEw.png)
    > 
    > Figure 2: An example learning objective with more than one prerequisite
    > 
    > By connecting each learning objective to its prerequisites, we can create a large Knowledge Graph full of connections between our content.

- [【ReadingNotes】知识图谱导学 Knowledge Graph Tutorial - Part 1](https://zhuanlan.zhihu.com/p/29848125)
    - [Mining Knowledge Graphs from Text | A Tutorial](https://kgtutorial.github.io/)

    > **Part 1 - Knowledge Graph Primer**
    > -----------------------------------
    > 
    > **1.What is a Knowledge Graph?**
    > 
    > 简而言之，就是表现为图形式的知识，用以刻画实体（entity），属性（attribute），关系（relationship）三者之间的关系。如下图所示，节点表示为实体，每个节点都有相关属性，而节点之间的边则刻画了两实体之间的关系。
    > 
    > ![](https://pic4.zhimg.com/80/v2-df8509f5981b617ecd40e072cf7f0f98_hd.jpg)
    > 
    > 来看一个例子，在下面这个简单的知识图谱中，
    > 
    > entity = {John Lennon, Beatles, Liverpool} ；
    > 
    > 对于John Lennon， 他的attributes可能有：person(比较宽泛)、年龄、性别等；
    > 
    > 他和Liverpool之间的关系，则是 John Lennon - bornIn - Liverpool
    > 
    > ![](https://pic3.zhimg.com/80/v2-07dcc6982092cf8e02aa4e89f9f461df_hd.jpg)
    > 
    > **2.Why Are Knowledge Graphs Important?**
    > 
    > For Humans：
    > 
    > -   Combat information overload （应对信息过载，信息过载指社会信息超过了个人或系统所能接受、处理或有效利用的范围）：我的理解就是，去除文本预料中的无用信息，通过知识图谱存储最简洁有效的信息；
    > -   explore via intuitive structure：通过这种直观的结构理解探索数据
    > -   Tool for supporting knowledge-driven tasks
    > 
    > For AIs：
    > 
    > -   Key ingredient for many AI tasks
    > -   Bridge from data to human semantics
    > -   Use decades of work on graph analysis
    > 
    > Applications：
    > 
    > -   QA/Agents
    > 
    > ![](https://pic4.zhimg.com/80/v2-b551c95e3c77ad757fb2722db9da5ec2_hd.jpg)
    > 
    > -   Decision Support：微软推出的Waston Knowledge Studio，理解语言的细微差别、意义以及具体的行业、专家和知识领域之间的关系，让用户在数周内打造个性化的认知应用
    > 
    > ![](https://pic2.zhimg.com/80/v2-fb881fd3aaa15ddb51983ee142db3aff_hd.jpg)
    > 
    > -   Fueling Discovery
    > 
    > ![](https://pic3.zhimg.com/80/v2-eb9567365810048e840d5b5ee7821005_hd.jpg)
    > 
    > Knowledge Graphs & Industry
    > 
    > ![](https://pic2.zhimg.com/80/v2-a7c4e5435931ddbed2fe76126c1c4a71_hd.jpg)
    > 
    > **3.Where Do Knowledge Graphs Come From?**
    > 
    > 回答：当然是所有有信息的地方啊！
    > 
    > -   Structured Text : Wikipedia Infoboxes, tables, databases, social nets
    > -   Unstructured Text : WWW, news, social media, reference articles
    > -   Images
    > -   Video : YouTube, video feeds
    > 
    > **4.Knowledge Representation Choices**
    > 
    > 1) Most knowledge graph implementations use RDF triples (Resource Description Framework)
    > 
    >     > RDF是一种处理元数据的应用，元数据是指描述数据的数据或者说是描述信息的信息\
    >     > eg: 书的内容是书的数据，作者的名字、出版社、地址是书的元数据。\
    >     >\
    >     > RDF的基本构造为陈述(或者叫做声明，statement)了一个资源-资源具有的属性(attribute)-属性值(value) (即，subject-predicate/relation-object)的三元组。它表现的是一个数据模型，通俗的说一个陈述就是一个什么事物（资源）具有什么属性（属性），这个属性是怎样的属性（属性值）。\
    >     > 每一个被描述的资源拥有一个统一资源标识符(URI)。URI可以是URL或者是其他诸如电话号码、国际标准图书编号ISBN和地理坐标等能唯一标识对象的符号。\
    >     > 属性同样也需要用URI来标识，防止同义词造成的混乱。[1]
    > 
    > 2) ABox (assertions) versus TBox (terminology)
    > 
    >      Tbox是关于概念术语的断言 ，Abox是关于个体的断言
    >     
    >      Tbox声明概念和角色间的包含关系，而Abox是关于个体的实例断言集合，断言包括声明个体是某概念的实例，以及个体之间的二元关系。
    >     
    >      例如：
    >     
    >      Abox -> A is an instance of B / John is a Person
    >     
    >      Tbox -> All Students are Persons / There are two types of Persons: Students and Teachers
    > 
    > 3) Common ontological primitives
    > 
    > -   rdfs:domain, rdfs:range, rdf:type, rdfs:subClassOf, rdfs:subPropertyOf, ...
    > -   owl:inverseOf, owl:TransitiveProperty, owl:FunctionalProperty, ...
    > 
    >     > RDF是领域无关的，而使用RDFS(RDF Schema)可以定义应用领域所使用的术语和概念。\
    >     > 但是无论是RDF或是RDFS都只能表示二元谓词（连接两个客体的谓词就叫二元谓词，比如A和B是好朋友，C比D高，其中的...和...是好朋友以及...比...高就是二元谓词），不足以支持web上的复杂应用，因此W3C又发展了Web本体语言(OWL)，OWL是RDF的扩张，有相同的语法结构，可以定义词汇之间的关系，类与类的关系，属性与属性之间的关系等等。[1]
    > 
    > 4) Semantic Web
    > 
    >     Standards for defining and exchanging knowledge
    > 
    >     > 语义Web的核心思想就是通过提升描述信息的语义本体以及规范化程度来支持更加方便迅速和智能化的信息集成、聚合与融合。[1]
    > 
    >     Annotated data provide critical resource for automation
    > 
    >     Major weakness: annotate everything?
    > 
    >     被标注的数据可以为自动化的一些操作提供关键的资源，但是这一点也是它的弱点所在，对于大量的不标准的语义表达，难道要标注所有数据吗。
    > 
    > 5) Information Extraction from Text (will be illustrated in Part 2)
    > 
    >     Answer to the knowledge acquisition bottleneck
    > 
    >     Many challenges:
    > 
    >     chunking, polysemy/word sense disambiguation (多义词) , entity coreference , relational extraction
    > 
    >     > Parsing "猴子喜欢吃香蕉。"\
    >     > POS Tagging == "猴子/NR 喜欢/VV 吃/VV 香蕉/NN 。/PU"\
    >     > Chunking == "(NP 猴子)(VP 喜欢吃香蕉)"
    > 
    > **5\. Problem Overview**
    > 
    > ![](https://pic2.zhimg.com/80/v2-fb68c3bf63b33cbe9d13594944d1283e_hd.jpg)
    > 
    > ![](https://pic1.zhimg.com/80/v2-60c61483e8ca5a71ddc8569b1c5c70a2_hd.jpg)
    > 
    > [1] 语义网格：模型、方法与应用。 吴朝晖 陈华钧著
    > 

- [Knowledge Graph Tutorial](http://sumitbhatia.net/source/knowledge-graph-tutorial.html)

    - [CIKM-part1 - KG_Tutorial_CIKM17_part1.pdf](http://sumitbhatia.net/papers/KG_Tutorial_CIKM17_part1.pdf)

    - [Knowledge Graphs: In Theory and Practice - KG_Tutorial_CIKM17_part2.pdf](http://sumitbhatia.net/papers/KG_Tutorial_CIKM17_part2.pdf)


- [WSDM 2018 - Neural Networks for Information Retrieval](http://nn4ir.com/wsdm2018/)

    - [Neural Networks for Information Retrieval - NN4IR.pdf](http://nn4ir.com/wsdm2018/slides/NN4IR.pdf)

    - [Neural Networks for Information Retrieval - 06_Entities.pdf](http://nn4ir.com/wsdm2018/slides/06_Entities.pdf)



### Building a Knowledge Graph

- [Knowledge extraction from unstructured texts |](https://blog.heuritech.com/2016/04/15/knowledge-extraction-from-unstructured-texts/)

- [QuickGraph#6 Building the Wikipedia Knowledge Graph in Neo4j (QG#2 revisited) – Jesús Barrasa](https://jbarrasa.com/2017/04/26/quickgraph6-building-the-wikipedia-knowledge-graph-in-neo4j-qg2-revisited/)

    - [Build a Searchable Knowledge Base](https://www.slideshare.net/jimmy_lai/build-a-searchable-knowledge-base?qid=04bb5c45-1bd5-40f7-b6c1-43ec644ab2aa&v=&b=&from_search=3)

- [PyVideo.org · Building a Knowledge Graph - the new search engine technology](https://pyvideo.org/pycon-apac-2014/building-a-knowledge-graph-the-new-search-engin.html)

- [(3) Building and Using a Knowledge Graph to Combat Human Trafficking](https://www.researchgate.net/publication/284545341_Building_and_Using_a_Knowledge_Graph_to_Combat_Human_Trafficking)

- [Center on Knowledge Graphs](https://usc-isi-i2.github.io/home/)

- [Knowledge graph refinement: A survey of approaches and evaluation methods - Semantic Scholar](https://www.semanticscholar.org/paper/Knowledge-graph-refinement%3A-A-survey-of-approaches-Paulheim/93b6329091e215b9ef007a85c07635f09e7b8adb)

- [Building and Using a Knowledge Graph to Combat Human Trafficking | SpringerLink](https://link.springer.com/chapter/10.1007/978-3-319-25010-6_12)

- [An Intrepid Guide to Ontologies | AI3:::Adaptive Information](http://www.mkbergman.com/374/an-intrepid-guide-to-ontologies/)

- [WTF is a knowledge graph? – Hacker Noon](https://hackernoon.com/wtf-is-a-knowledge-graph-a16603a1a25f)



- [Course - Building Knowledge Graphs](https://classes.usc.edu/term-20173/course/csci-563/)

    - [INF558_Syllabus_v5 - 32438.pdf](https://web-app.usc.edu/soc/syllabus/20173/32438.pdf)


    - [Cheng-Lin-Li/Market-Trend-Prediction: This is a project of build knowledge graph course. The project leverages historical stock price, and integrates social media listening from customers to predict market Trend On Dow Jones Industrial Average (DJIA).](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction)



- [algorithm - How to build a knowledge graph? - Stack Overflow](https://stackoverflow.com/questions/29461062/how-to-build-a-knowledge-graph)

    > Knowledge graph is a buzzword. It is a sum of models and technologies put together to achieve a result. The first stop on your journey starts with [Natural language processing](http://en.wikipedia.org/wiki/Natural_language_processing), [Ontologies](http://en.wikipedia.org/wiki/Ontology_learning) and [Text mining](http://en.wikipedia.org/wiki/Text_mining). It is a wide field of artificial intelligence, go [here](http://soda.swedish-ict.se/3600/1/SICS-T--2009-06--SE.pdf) for a research survey on the field.
    > 
    > ---
    > 
    > A good processing pipeline can be built "easily" on top of Apache Spark, "the current-gen Hadoop". It provides a resilient distributed datastore which is mandatory if you want to scale.
    > 
    > If you want to keep your data as a graph, as in graph theory (like pagerank), for live querying, I suggest you use Bulbs which is framework which "Like an ORM for graphs, but instead of SQL, you use the graph-traveral language Gremlin to query the database". You can switch backend from Neo4j to OpenRDF (useful if you do ontologies) for instance.
    > 
    > For graph analytics you can use Spark, GraphX module or GraphLab.
    > 

- [How do you build and maintain a knowledge graph, i.e, what is the suggested path to extract, model, generate a database and visualize a graph that is similar in concept to Google knowledge graph? - Quora](https://www.quora.com/How-do-you-build-and-maintain-a-knowledge-graph-i-e-what-is-the-suggested-path-to-extract-model-generate-a-database-and-visualize-a-graph-that-is-similar-in-concept-to-Google-knowledge-graph)

    > To build a knowledge graph, you must first answer two questions required to build *any* graph:
    > 
    > 1.  What are the *nodes*? In a knowledge graph, they will be related to semantic concepts such as persons, entities, events *etc.*
    > 2.  What are the *edges*? They will be defined by *relationships* between nodes based on semantics.
    > 
    > Once you answered these two key questions, you can go to the next phase which is the *data acquisition strategy*. At this day and age, one should feel very fortunate to be able to leverage unfathomable amounts of information openly available.
    > 
    > There are several possibilities, which are not exclusive, and in fact largely complementary:
    > 
    > -   **Reputable open semantic database** such as [Wikipedia](http://wikipedia.org) or [Freebase](https://developers.google.com/freebase/). They are easy to work with, are manageable in size and have pretty good quality , making them ideal as first steps. You will want to go beyond them eventually as relying on them exclusively might cause people to perceive your work as derivative-only.
    > -   **General web content of higher quality** such as newspaper and other article archives where content has been cleaned up from low quality stuff such as spam, porn and low quality ads. You will have to be careful about the license and terms of service though there is still lots of gray in that area. You will also likely need to write specialized software agents, also known as wrappers, which are simple custom software agents capable of extracting information you desire from the target content.
    > -   **Open crawl database** such as [Common Crawl](http://commoncrawl.org), comprising of unprocessed dumps of crawls of high quality links. They are a great source as selection of quality links saves you a tremendous amount of time and effort wasted in eliminating junk.
    > -   **Crawling yourself** is always an alternative where you have full control and with open source crawlers and cheap machines and bandwidth you can set up cheaply and quickly a rig crawling tens of millions of documents per day, which should be your target for serious crawling. Keep in mind that you will be amazed how much junk and bloat is out there, a very rough rule of thumb is that half will be porn, remaining half will be spam and the rest will be bloated with ads. But with even a half-decent junk removal strategy you will be able to get lots and lots of good data.
    > 
    > 
    > 
    
    ---

    > Here is a step by step guide for building a knowledge graph:
    > 
    > **1\. Understanding the field and defining the actors**
    > 
    > The first question should be what actors there are in the field that you are interested to research. The actors can vary from real persons to concepts, from institutions to inanimate objects. Let's say that a researcher is interested in fish farms, the market relations between the farms and the vendors and how this ecosystem of fishing operates in its processual cycle. The reproduction of fish then would not only rely upon the human subjects in the field, but also would rely on companies that produce fish meal or the fish themselves. In other words, you have to first investigate and list the actants within your field.
    > 
    > **2\. Detecting the relationships**
    > 
    > The second step is to come up with relations that make the interaction or some other relation possible between the actors. These could be from interactions like "sending email", "collaborating", "influencing", to affiliations such as "being a member", "belonging to a category", "similarity", or more ontological "is a", "part of" relations. For instance, if one is interested in understanding the lobbying activities of a certain push group, one would expect to find official and as well as organic links that make up the bigger social network. Or another relation one would expect to detect would be bribery, which is somewhat neither organic nor official. It is therefore good idea to start with an educated guess of what kind of relations that one can encounter. However, it is also vital not to assume the categories beforehand and overlook the ones that we are not deliberately pursuing. Also remember that the number of actors can also be limited by your definition of your field and research topic.
    > 
    > **3\. Compiling data & building the graph**
    > 
    > After you listed the actor and relation types just fill in these with data. The best way to organize your data is to put it into a spreadsheet. Depending on your skills, you can start scanning large documents, scrap tables from websites, or query APIs to collect data and fit in your graph model.
    > 
    > **4\. Reading & analyzing the graph**
    > 
    > After a network is mapped, you should can examine its *centrality* and *clustering* metrics.
    > 
    > ![](https://qph.ec.quoracdn.net/main-qimg-8a2f661e43586c128dc258bc3477421d)
    > 
    > These will help you to discover and use the intelligence embedded in your knowledge graph. Read more about [analyzing data networks.](https://medium.com/graph-commons/analyzing-data-networks-f4480a28fb4b)
    > 
    > This is more or less the general structure for building a knowledge base. No need to say, from cleaning data to maintaining updates running a knowledge graph is not an easy task.
    > 
    > This problem inspired us to build the [Graph Commons](https://graphcommons.com) platform to enable people and organizations to transform their data into interactive graphs and untangle complex relations that impact them and their communities. Graph Commons is currently used for a variety purposes including investigative journalism, data science, organizational analysis, advocacy, digital humanities, policy analysis, data activism, archival exploration, design research, and art curating.
    > 
    
    ---

    > ***A quick (historical) overview***
    > 
    > An approach to contextualise entities can be done by *elevating properties to entities*. This is an approach that is also used by *Wikidata* (see their APIs specifications).
    > 
    > Google Knowledge Graph first used Wikipedia; then acquired Freebase; then move onward to Wikidata as base structure.
    > 
    > Bing used collaborative data as well, adopting Britannica originally.
    > 
    > The value of **collaborative data** is that humans, somehow, already organised and polish databases to ingest and model a knowledge graph with a good approximation reflecting complexity of correlations between entities.
    > 
    > If you would like to get hands dirty with a similar approach, you may want to look at knowledge bases such as Wikipedia dumps; Wikidata; Google Patents or other corpuses of relevance in a specific sector - like scientific articles; or networks between companies, investors and employes in new tech (CrunchBase, AngelList).
    > 
    > ---
    > 
    > ***A technical quick introduction***
    > 
    > Technically, one technique was to adopt bi-partite graphs; as example, you could describe like that (at least in their beginning phase) knowledge graphs of Linkedin or item-to-item recommendation system by Amazon, where a product (entity) is liked by a set of customers (properties), so recommendations are pushed to similar customers.
    > 
    > Another approach, is to iterate on the type of entities you can encompass in your graph, modelling a knowledge graph as an [**Hypergraph**](https://en.wikipedia.org/wiki/Hypergraph) or multi-partite graphs.
    > 
    > Hypergraphs can be weighted or not, very likely they are by means of internal ranking systems based on recommendation, topology, or machine learning approaches.
    > 
    > For graph modelling and representation, you may want to read through some introductory literature on complex networks; **Barabasi** and **Mark Newman** are some good starting point **-** and this bookvastly inspired the innovation I developed in my research on data visualisation [Networks: An Introduction](https://books.google.it/books?dq=neuman+graph+similarity&hl=en&id=LrFaU4XCsUoC&printsec=frontcover&sa=X&ved=0ahUKEwiY37b0oIHKAhVKDxoKHRh-Bg4Q6AEILzAD#v=onepage&q&f=false)
    > 
    > For weighting your graph, you may explore different types of graph similarities and what they encode - keep in mind graph similarity is only an approach to organise linked structures, and graph similarity does not scale very well - although industry is going fast, have a look at final chapter -data maintanance- for an overview on graph technology and data-persistence in modern architectures.
    > 
    > ---
    > 
    > ***Where to begin ?***
    > 
    > Let's break it down.
    > 
    > ***Data modelling***- you need some programming skills here. Python language and scientific libraries can be help there, and there are *many* works on github you can explore. Or also node.js is coming up with powerful tools. Or use **Wolfram Mathematica** embedded symbolic functions. Or use <https://www.tensorflow.org/>
    > 
    > You may want to explore what **Natural Language Processing** is, first (check for nltk nlp toolkit) and understand differences between semantic processing and semantic web, not to get confused where someone calls "semantic" out.
    > 
    > As example, semantic meta-tagging are what <http://schema.org> and open graph protocol are using to organise web objects in the web in their own knowledge graph.
    > 
    > They are useful if you want to make an object be found in their own knowledge graph.
    > 
    > ***Data visualisation*** - once you come up with a model, **gephi, D3.js, sigma.js, vivagraph.js, arbor.js** and so on will be your friend. You may consider to explore **WebGL.**
    > 
    > Keep in mind that data-modelling may not be needed depending on your goal: e.g. knowledge graph of google or pushing recommendation systems (e.g. recommendations about places and routes on maps) may not need a graph visualisation interface.
    > 
    > But here you are entering a User Experience sphere : what people need to do, what kind of insight they want to have, what kind of personal or tech constraints have : they are the most important things in declining science and technology to be useful, either for masses either for a niche.
    > 
    > ***Data maintenance -*** if you are here, you are very far away with your journey! And it means you may have chose and yet iterated a few times on the design of your technological architecture.
    > 
    > In fact, depending on your knowledge graph model and scope, you may design your service with different technologies.
    > 
    > Very briefly now, for the sake of introduction only.
    > 
    > You have SQLs databases, and NoSQL databases.
    > 
    > NoSQL databases can be "easier" to represent and persist complex correlations by redounding data.
    > 
    > That is, as simple example, you may want represent a graph as an (or several) adjacency matrix. In this class, you find key-value databases and such, like Cassandra (developed by Facebook), key-value stored in memory Redis; you want to look at Mongo-db as well (not a key-value store but NoSQL).
    > 
    > Another class, is graph db. Here you find Neo4J, or OrientDb, or Arango, or Titan.
    > 
    > If you are starting to get curious, I suggest you to think well what you want to achieve, disregarding the technology at first glance, and then pick up a tool with a good community support.
    > 
    > Keep your first toy model simple, and take time to very much think well what you would like to achieve, gradually.
    > 
    > For maintaining data, it depends where your data-warehouse is stored - is it in you house? a data-warehouse? on the cloud? Are you sure you want to learn also tech skills for maintianing a server? Which is the core knowledge you want to develop and apply ?
    > 
    > If you want to check around cloud services where to store your data and serve data as API REST over the web, you may have a look at Parse or Firebase and store your data-model there.
    > 
    > ---
    >
    > Here you can find a knowledge graph of genomics.
    > 
    > [Knowledge discovery - Genomics.](http://genomics.nifty.works)
    > 
    > *Proof-of-concepts. Search for genes interactions and genes associated to diseases. TargetValidation database (GlaxoSmithKlein).\
    > Below: Cartographic layout experience designed to simplify "hair-balls" (highly dense networks).*
    > 
    > ![](https://qph.ec.quoracdn.net/main-qimg-52f684394b10a9d065b44a334ff00db5)
    > 
    > ![](https://qph.ec.quoracdn.net/main-qimg-483d1fa27bc75e530a316bb225806f39)
    > 

- [Build Knowledge Graph from unstructured corpus using Machine Learning | LinkedIn](https://www.linkedin.com/pulse/build-knowledge-graph-from-unstructured-corpus-using-machine-anish/)

    > Problem of creating knowledge graph from unstructured data is a well known machine learning problem. Not even a single org has achieved 100% accuracy for completely enriched knowledge graph . I have few findings that will help to kick-start for a person who is new in to this .
    > 
    > Before move to findings , i will let you to walk through the problem of building knowledge graph from unstructured corpus . Lets consider this scenario . Suppose we have very small corpus :
    > 
    > "Apple was founded by Steve jobs and current CEO is Tim Cook. Apple launched several products like Ipad, iphone , MAC etc. "
    > 
    > Corpus may be very complex sentences also . Problem is how can we build a knowledge graph out of this unstructured corpses . If we create generic knowledge graph , then our system should be able to provide answers like "who founded Apple ?" , " What are products launched by Apple ?" etc .
    > 
    > ![](https://media.licdn.com/dms/image/C4E12AQEAzrEAgmRYVg/article-inline_image-shrink_1500_2232/0?e=2130105600&v=beta&t=zrq6zeAFwbO2aul-KKrwqxeFbAYVgwMHc3f19h-TWM0)
    > 
    > Few techniques to create knowledge graph :
    > 
    > **1.) Supervised Technique :**
    > ------------------------------
    > 
    > Supervised models used in the field of information extraction involve formulation of the problem as a classification problem and they generally learn a discriminative classifier given a set of positive and negative examples. Such approaches extract a set of features from the sentence which generally include context words, 3 part of speech tags, dependency path between entity, edit distance, etc. and the corresponding labels are obtained from a large labelled training corpus.
    > 
    > ![](https://media.licdn.com/dms/image/C4E12AQHZ9FEzK0RyTQ/article-inline_image-shrink_1000_1488/0?e=2130105600&v=beta&t=nPgxxozygF8Pb4KJWr4qdC8hR2DoZ7uYcBQqeyXlvkQ)
    > 
    > -   Sentence Segmentation : It will take input as a raw corpus and split it in to multiple sentences which is basically a list of strings.
    > -   Tokenization : It will take list of splitted sentences and convert it in to tokens which is basically a list of list of strings.
    > -   POS Tagging : It will convert in to pos tagged sentences which is basically list of list of tuples.
    > -   Entity detection : it will detect entity and create chunk of sentences which is basically a list of trees.
    > -   Relation detection: It will classify whether the particular relation satisfies the given entity set.
    > 
    > **Here is few more points about supervised approach and its pros and cons.**
    > 
    > -   It needs a set of relation types.
    > -   A named entity tagger
    > -   Lots of Labeled data (Break into training set, development set and test set)
    > -   Feature representation
    > -   A classifier (Naïve Bayes, MaxEnt, SVM, ...)
    > 
    > **Here is all the features that we can have in supervised approach**
    > 
    > -   Lightweight features -- require little pre-processing
    > 
    >     Words: headwords, bag of words, bigrams (between, before or after)
    > 
    >     Entity type: PERSON, ORGANIZATION, FACILITY, LOCATION & Geo-Polotical Entity/GPE
    > 
    >     Entity level: NAME, NOMIAL & PRONOUN
    > 
    > -   Medium-weight features -- require base phrase chunking
    > 
    >     Base phrase chunk paths
    > 
    >     Bags of chunk heads
    > 
    > -   Heavyweight features -- require full syntactic parsing
    > 
    >     Dependency tree paths between entities
    > 
    >     Parse tree paths between entities
    > 
    > **Pros** :
    > 
    > -   Could be adapted to a different domain
    > -   High accuracy with enough hand-labeled training data and test similar enough to training
    > 
    > **Cons**:
    > 
    > -   Have to label a large training set (expensive)
    > -   Could not generalize well to different genres
    > -   Extension to high order Entity relation is difficult as well.
    > 
    > **2.) Semi-supervised technique**
    > ---------------------------------
    > 
    > Such methods start with some known relation triples and then iterate through the text to extract patterns that match the seed triples. These patterns are used to extract more relations from the data set and the learned relations are then added to the seed examples. This method is repeated till no more relations can be learned from the data set.
    > 
    > ![](https://media.licdn.com/dms/image/C4E12AQF22NpoNMY0sw/article-inline_image-shrink_1000_1488/0?e=2130105600&v=beta&t=HPqQhtY0QGVLKRuBFDdIlHEuLkABRCjnToDY3H6-pfs)
    > 
    > One more popular algorithms algorithm of it is Snowball ML algorithm.
    > 
    > **SnowBall algorithm:**
    > 
    > 1.)  Start with seed set R of tuples.
    > 
    > 2.)  Generate set P of patterns from R . Compute support and confidence for each Pattern in P and discard those pattern with low support or confidence.
    > 
    > 3.)  Generate new Set T of tuples matching patterns P . Compute confidence of each tuple in T , add to R the tuples t in T with conf(t) > threshold.
    > 
    > 4.)  Go back to step 2.
    > 
    > Further illustration of algorithm:
    > 
    > 1.)            Start with Seed examples 
    > 
    > ![](https://media.licdn.com/dms/image/C4E12AQH108tg_MXvnQ/article-inline_image-shrink_1500_2232/0?e=2130105600&v=beta&t=fQupKZeARB3wKjeUMOPmWC0AMAysQ73KWSS0Eaour5M)
    > 
    > 2.)             Use entity tagger to tag entities 
    > 
    > 3.)             Grab the extracted pattern
    > 
    > In general , pattern is of the 5-tuple form : (left,tag1,mid,tag2,right)
    > 
    > ![](https://media.licdn.com/dms/image/C4E12AQFhX2h8WZ2AmQ/article-inline_image-shrink_1000_1488/0?e=2130105600&v=beta&t=XUZaHCRoqTPMJxcFXWCoUDAxy3XMUD85VLeh3EqFo8A)
    > 
    >  Tag1,tag2 are named entity tags. Left,mid,right are vectors of weighted terms   
    > 
    > 4.) Cluster the patterns and filter the pattern in each cluster by compute support and confidence
    > 
    > 5.) Using the patterns , scan the collection to generate new seed tuples
    > 
    > Initial seed tuple will be of the form : (tag1,tag2,tag3,tag4 etc)
    > 
    > Example : (organization , product,location etc) so seed example may be (Apple,ipad,california) or (ibm,db2,Armonk ) etc.
    > 
    > **Pros** :
    > 
    > -   avoid labeling manually lots of data
    > 
    >  **Cons**:
    > 
    > -   Require seeds for each relation (quality of the original set of seeds is important)
    > -   Big problem of semantic drift at each iteration
    > -   Not high precision
    > 
    > 3.) Distant Supervision approach
    > --------------------------------
    > 
    > It uses a database of relations Freebase to get lots of training examples. We build a feature vector in the training phase for an 'unrelated' relation by randomly selecting entity pairs that do not appear in any Freebase relation and extracting features for them .
    > 
    > We use a multi-class logistic classifier optimized using L-BFGS with Gaussian regularization. Our classifier takes as input an entity pair and a feature vector, and returns a relation name and a confidence score based on the probability of the entity pair belonging to that relation. Once all of the entity pairs discovered during testing have been classified, they can be ranked by confidence score and used to generate a list of the n most likely new relation instances.
    > 
    > ![](https://media.licdn.com/dms/image/C4E12AQEsOBmPXMEw0w/article-inline_image-shrink_1500_2232/0?e=2130105600&v=beta&t=KzXYXX-fXcVtuCJd6wos3K7TtN4tuZiJg1GaDq8NRZ4)
    > 
    > **Pros :**
    > 
    > -   Leverage unlimited amounts of text data
    > -   Allows for very large number of weak features
    > -   Not sensitive to training corpus: genre-independent
    > 
    > You can find my blogspot link here : <https://www.linkedin.com/redir/invalid-link-page?url=http%3A%2F%2Flcso-ldsis%2eblogspot%2ein%2F> or [anishratnawat.com](http://anishratnawat.com)







### Graph Convolutional Networks

- [kegra: Deep Learning on Knowledge Graphs with Keras](https://towardsdatascience.com/kegra-deep-learning-on-knowledge-graphs-with-keras-98e340488b93)

    > Here is an example of a knowledge graph ontology in OrientDB:
    > 
    > ![](https://cdn-images-1.medium.com/max/1200/0*eygCktVkmHlL8tXa.png)
    > 
    > Source: [OrientDB demo page](https://orientdb.com/docs/3.0.x/gettingstarted/demodb/queries/DemoDB-Queries-Shortest-Paths.html)



### R-GCN

- [[1703.06103] Modeling Relational Data with Graph Convolutional Networks](https://arxiv.org/abs/1703.06103)



### GraphRNN: Generating Realistic Graphs

- [[1802.08773] GraphRNN: Generating Realistic Graphs with Deep Auto-regressive Models](https://arxiv.org/abs/1802.08773)

### NeVAE: A Variational Autoencoder for Graphs

- [[1802.05283] Designing Random Graph Models Using Variational Autoencoders With Applications to Chemical Design](https://arxiv.org/abs/1802.05283)

### GT-GAN

- [[1805.09980] Deep Graph Translation](https://arxiv.org/abs/1805.09980)

### MolGAN

- [[1805.11973] MolGAN: An implicit generative model for small molecular graphs](https://arxiv.org/abs/1805.11973)


### ConvE

- [[1707.01476] Convolutional 2D Knowledge Graph Embeddings](https://arxiv.org/abs/1707.01476)




## Visual-relational knowledge graph

- [[1709.02314] Representation Learning for Visual-Relational Knowledge Graphs](https://arxiv.org/abs/1709.02314)

- [A*STAR OAR: Object Detection Meets Knowledge Graphs](http://oar.a-star.edu.sg/jspui/handle/123456789/2147)

    - [knowvision.pdf](http://oar.a-star.edu.sg/jspui/bitstream/123456789/2147/1/knowvision.pdf)

- [[1711.01714] End-to-End Video Classification with Knowledge Graphs](https://arxiv.org/abs/1711.01714)

### Graph Networks

- [DeepMind等機構提出「圖網絡」：面向關係推理 - 幫趣](http://bangqu.com/Tuu646.html#utm_source=Facebook_PicSee&utm_medium=Social)

    - [[1806.01261] Relational inductive biases, deep learning, and graph networks](https://arxiv.org/abs/1806.01261)

    > **論文其他圖與表**
    > 
    > ![](http://i2.bangqu.com/j/news/20180614/Tuu6461528963211211r6447.png)*表 1：標準深度學習組件中的各種關係歸納偏置。詳見論文原文第 2 節。*
    > 
    > ![](http://i2.bangqu.com/j/news/20180614/Tuu6461528963212756FZ97N.png)*圖 1：重複使用和共享常見的深度學習構件。（a）全連接層，其中所有權重都是獨立的，沒有共享。（b）卷積層，其中局部核函數在輸入端被多次使用。共享權重由具有相同顏色的箭頭指示。（c）循環層，其中相同的功能在不同的處理步驟中重複使用。*
    > 
    > ![](http://i2.bangqu.com/j/news/20180614/Tuu6461528963214649689h9.png)*圖 2：不同的圖表徵。（a）一個分子，其中每個原子表示爲對應關係的節點和邊（Duvenaud 等，2015）。（b）一個質量彈簧系統，其中繩索由在圖中表示爲節點的質量序列定義（Battaglia 等，2016；Chang 等，2017）。（c）一個 n 主體系統，其中主體是節點，底層圖是完全連接的（Battaglia 等，2016 年；Chang 等，2017）。（d）一個精密的主體系統，其中球和壁是節點，底層圖形定義球之間以及球和壁之間的相互作用（Battaglia 等，2016 年；Chang 等，2017）。（e）一個句子，其中單詞對應於樹中的葉子，其他節點和邊可以由解析器提供（Socher 等，2013）。或者，可以使用完全連接的圖（Vaswani 等，2017 年）。（f）一張圖像，可以分解成與完全連接圖像中的節點相對應的圖像塊（Santoro 等，2017；Wang 等，2018）。*
    > 

- [【CNN已老，GNN来了】DeepMind、谷歌大脑、MIT等27位作者重磅论文，图网络让深度学习也能因果推理](https://zhuanlan.zhihu.com/p/38071963)

    > DeepMind提出的"图网络"究竟是什么
    > ---------------------
    > 
    > 在这里，有必要对说了这么多的"图网络"做一个比较详细的介绍。当然，你也可以跳过这一节，直接看后面的解读。
    > 
    > 在《关系归纳偏置、深度学习和图网络》这篇论文里，作者详细解释了他们的"图网络"。图网络（GN）的框架定义了一类用于图形结构表示的关系推理的函数。GN 框架概括并扩展了各种的图神经网络、MPNN、以及 NLNN 方法，并支持从简单的构建块（building blocks）来构建复杂的结构。
    > 
    > GN 框架的主要计算单元是 GN block，即 "graph-to-graph" 模块，它将 graph 作为输入，对结构执行计算，并返回 graph 作为输出。如下面的 Box 3 所描述的，entity 由 graph 的节点（nodes），边的关系（relations）以及全局属性（global attributes）表示。
    > 
    > ![](https://pic2.zhimg.com/80/v2-a1ceda7fdc7a00b7a06823ba7832074e_hd.jpg)
    > 
    > 论文作者用 "graph" 表示具有全局属性的有向（directed）、有属性（attributed）的 multi-graph。一个节点（node）表示为 $\textbf{v}_{i}$，一条边（edge）表示为 $\textbf{e}_{k}$，全局属性（global attributes）表示为$u$。
    > 
    > $s_{k}$ 和 $r_{k}$
    > 
    > 
    > 表示发送方（sender）和接收方（receiver）节点的指标（indices）。具体如下：
    > 
    > -   Directed：单向，从 "sender" 节点指向 "receiver" 节点。
    > -   Attribute：属性，可以编码为矢量（vector），集合（set），甚至另一个图（graph）
    > -   Attributed：边和顶点具有与它们相关的属性
    > -   Global attribute：graph-level 的属性
    > -   Multi-graph：顶点之间有多个边
    > 
    > GN 框架的 block 的组织强调可定制性，并综合表示所需关系归纳偏置（inductive biases）的新架构。
    > 
    > 用一个例子来更具体地解释 GN。考虑在任意引力场中预测一组橡胶球的运动，它们不是相互碰撞，而是有一个或多个弹簧将它们与其他球（或全部球）连接起来。我们将在下文的定义中引用这个运行示例，以说明图形表示和对其进行的计算。
    > 
    > "graph" 的定义
    > 
    > 在我们的 GN 框架中，一个 graph 被定义为一个 3 元组的 $G=(u,V,E)$。
    > 
    > $u$ 表示一个全局属性；例如，$u$ 可能代表重力场。
    > 
    > $V=\{\textbf{v}_i\}_{i=1:N^v}$
    > 
    > 是节点集合（基数是 $N^v$ ），其中每个 $\textbf{v}_i$ 表示节点的属性。例如，$V$ 可能表示每个球，带有位置、速度和质量这些属性。
    > 
    > $E=\{(\textbf{e}_k,r_k,s_k)\}_{k=1:N^e}$
    > 
    > 
    > 是边（基数是 $N^e$ ）的集合，其中每个 $\textbf{e}_k$ 表示边的属性，$r_k$ 是接收节点的 index，$s_k$ 是发送节点的 index。例如，$E$ 可以表示不同球之间存在的弹簧，以及它们对应的弹簧常数。
    > 
    > 算法 1：一个完整的 GN block 的计算步骤
    > 
    > ![](https://pic4.zhimg.com/80/v2-d9fbe20a62b19eee67614d689ddcfa9a_hd.jpg)\
    > GN block 的内部结构
    > 
    > 一个 GN block 包含三个 "update" 函数 $\phi$ ，以及三个 "aggregation" 函数 $\rho$ ：
    > 
    > $$
    > \begin{align}
    > \textbf{e}'_k&=\phi^e(\textbf{e}_k,\textbf{v}_{r_k},\textbf{v}_{s_k},\textbf{u})&  \bar{\textbf{e}}'_i=\rho^{e \rightarrow v}(E'_i) & \\
    > \textbf{v}'_i&=\phi^v(\bar{\textbf{e}}'_i,\textbf{v}_i,\textbf{u})&\bar{\textbf{e}}'=\rho^{e \rightarrow u}(E')& \tag{1} \\
    > \textbf{u}'&=\phi^u(\bar{\textbf{e}}',\bar{\textbf{v}}',\textbf{u})&\bar{\textbf{v}}'=\rho^{v \rightarrow u}(V')&
    > \end{align}
    > $$
    > 
    > 
    > 其中：
    > 
    > ![](https://pic2.zhimg.com/80/v2-f48225f49aeaf54d2d908e48d4fdb31d_hd.jpg)
    > 
    > ![](https://pic1.zhimg.com/80/v2-0e00b38c5cef53d972bda881c8e757d6_hd.jpg)\
    > 图：GN block 中的 Updates。蓝色表示正在 update 的元素，黑色表示 update 中涉及的其他元素
    > 
    > 把知识图谱和深度学习相结合的难点
    > ----------------
    > 
    > 要把知识图谱和深度学习相结合，邓侃博士认为有几大难点。
    > 
    > 1\. 点向量：
    > 
    > 知识图谱由点和边构成，点（node）用来表征实体（entity），实体又包含属性（attribute）和属性的值（value）。传统知识图谱中的实体，通常由概念符号构成，譬如自然语言的词汇。
    > 
    > 传统知识图谱中的边，连接两个单点，也就是两个实体，边表达的是关系，关系的强弱，由权重表达，传统知识图谱的边的权重，通常是常数。
    > 
    > 如果想把传统知识图谱与深度学习相融合，首先要做的是实现点的可微分化。用数值化的词向量来替代自然语言的词汇，是实现点的可微分化的有效方法，通常的做法是用语言模型来分析大量的文本，给每个词汇找到最贴合上下文语义的词向量。但在图谱中，传统的词向量的生成算法，不十分奏效，需要改造。
    > 
    > 2\. 超点：
    > 
    > 前文说到，传统知识图谱中的边，连接两个单点，表达两个单点之间的关系。这个假定制约了图谱的表达能力，因为在很多场景下，多个单点组合在一起，才与其它单点或者单点组合，存在关系。我们把单点组合，称之为超点（hyper-node）。
    > 
    > 问题是哪些单点组合在一起构成超点？人为的先验指定，当然是一个办法。从大量训练数据中，通过 dropout 或者 regulation 算法，自动学习出超点的构成，也是一个思路。
    > 
    > 3\. 超边：
    > 
    > 传统的知识图谱中的边，表达了点与点之间的关系，关系的强弱由权重表达，通常权重是个常数。但在很多场景下，权重并非是常数。随着点的取值不同，边的权重也发生变化，而且很可能是非线性变化。
    > 
    > 用非线性函数来表达图谱的边，称为超边（hyper-edge）。
    > 
    > 深度学习模型可以用于模拟非线性函数。所以，知识图谱中每条边都是一个深度学习模型。模型的输入是若干个单点组成的超点，模型的输出是另一个超点。如果把每个深度学习模型，视为一棵树，根是输入，叶子是输出。那么鸟瞰整个知识图谱，实际上是深度学习模型的森林。
    > 
    > 4\. 路径：
    > 
    > 训练知识图谱，包括训练点向量，超点、和超边的时候，一条训练数据往往是在图谱中行走的一条路径，通过拟合海量的路径，获得最贴切的点向量、超点和超边。
    > 
    > 用拟合路径来训练图谱，存在的一个问题是，训练过程与过程结束后的评价，两者的脱节。打个比方，给你若干篇文章的提纲，以及相应的范文，让你学习如何写作文。拟合的过程，强调逐字逐句的模仿。但是评价文章的好坏，重点并不在于字句的亦步亦趋，而在于通篇文章的顺畅。
    > 
    > 如何解决训练过程与最终评价的脱节？很有潜力的办法，是用强化学习。强化学习的精髓，在于把最终的评价，通过回溯和折现的方法，给路径过程中每一个中间状态，评估它的潜力。
    > 
    > 但是强化学习面临的困难，在于中间状态的数量不可太多。当状态数量太多时，强化学习的训练过程，无法收敛。解决收敛问题的办法，是用一个深度学习模型，来估算所有状态的潜力值。换句话说，不需要估算所有状态的潜力值，而只需要训练一个模型的有限参数。
    > 
    > DeepMind 前天发表的这篇文章，提议把深度强化学习与知识图谱等相融合，并梳理了大量的相关研究。但是，论文并没有明确说明 DeepMind 偏向于哪一种具体方案。
    > 
    > 或许，针对不同应用场景会有不同方案，并没有通用的最佳方案。
    > 

