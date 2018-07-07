# Spark__快速上手


## tutorial

- [Spark and Python for Big Data with PySpark | Udemy](https://www.udemy.com/spark-and-python-for-big-data-with-pyspark/?siteID=BoHFIyu6APU-Tla_hhvJJ8L.Wm4oXNCGBw&LSNPUBID=BoHFIyu6APU)

- [給初學者的Spark教學](https://www.slideshare.net/popcornylu/spark-77220371)

    > <iframe src="//www.slideshare.net/slideshow/embed_code/key/155DYFCkZDfuhi" width="510" height="420" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/popcornylu/spark-77220371" title="給初學者的Spark教學" target="_blank">給初學者的Spark教學</a> </strong> from <strong><a href="//www.slideshare.net/popcornylu" target="_blank">Chen-en Lu</a></strong> </div>

- [Spark(一): 基本架构及原理 - 天戈朱 - 博客园](https://www.cnblogs.com/tgzhu/p/5818374.html)

- [Spark(二): 内存管理 - 天戈朱 - 博客园](https://www.cnblogs.com/tgzhu/p/5822370.html)

- [Spark(三): 安装与配置 - 天戈朱 - 博客园](https://www.cnblogs.com/tgzhu/p/5821421.html)

- [Spark(四): Spark-sql 读hbase - 天戈朱 - 博客园](https://www.cnblogs.com/tgzhu/p/5829242.html)

## Relation Between Spark and SQL

- [Difference Between Apache Spark SQL and MongoDB? - Stack Overflow](https://stackoverflow.com/questions/39653769/difference-between-apache-spark-sql-and-mongodb)

    > 1) Apache Spark: Apache Spark for doing Parallel Computing Operations on Big Data in SQL queries.
    > 
    > MongoDB: MongoDB is a document Store and essentially is a database so cannot be compared with Spark which is a computing engine and not a store.
    > 
    > 2) SparkSQL can be ideal for processing Structure Data imported in the Spark Cluster where you have millions of data available for big computing. Mongodb can be use where you need NoSQL functionalities(It has full NoSQL Capabilities, compare to SparkSQL).
    > 
    > 3) No Apache Spark is use for different purpose , you can not replace it with mondoDB,cassandra.It is like computing engine to give you predict results on large data sets
    > 
    > 4) Use third party service like SLAM DATA http://slamdata.com/ to apply mongodb analytics also use spark data-frame to read in the data from MongoDB

- [What is the difference between sql and Spark? - Quora](https://www.quora.com/What-is-the-difference-between-sql-and-Spark)


    > Basically, there is no comparison occur between Spark and SQL. So, we can not point out their differences. However they both differ in every sense. To understand better, lets understand each in detail:
    > 
    > **Apache Spark**
    > 
    > Apache Spark is a general-purpose & lightning fast cluster computing system. It provides high-level API. For example, Java, [**Scala**](http://data-flair.training/blogs/why-you-should-learn-scala-introductory-tutorial/), Python and[**R**](http://data-flair.training/blogs/r-programming-tutorial/). Apache Spark is a tool for Running Spark Applications. Spark is 100 times faster than [**Bigdata**](http://data-flair.training/blogs/history-big-data/) Hadoop and 10 times faster than accessing data from disk.
    > 
    > ![](https://qph.ec.quoracdn.net/main-qimg-f9ea3105faf895da707b33b168f2cdb0)
    > 
    > Spark is written in Scala but provides rich APIs in Scala, Java, Python, and R.
    > 
    > It can be integrated with [**Hadoop**](http://data-flair.training/blogs/hadoop-introduction-comprehensive-tutorial-guide-beginners/)[](http://data-flair.training/blogs/hadoop-introduction-comprehensive-tutorial-guide-beginners/)and can process existing Hadoop [**HDFS**](http://data-flair.training/blogs/introduction-tutorial-hdfs/) data.
    > 
    > It is saying that the images are the worth of thousand words. To keep this in mind we have also provided Spark video tutorial for more understanding of Apache Spark.
    > 
    > To learn complete information on Spark, follow link;[ **Apache Spark -- A Complete Spark Tutorial for Beginners**](https://goo.gl/jsU2Pt)
    > 
    > **SQL**
    > 
    > SQL is a standard language for accessing and manipulating databases. Structure Query Language(SQL) is a programming language used for storing and managing data in RDBMS. SQL was the first commercial language introduced for E.F Codd's Relational model. Today almost all RDBMS(MySql, Oracle, Infomix, Sybase, MS Access) uses SQL as the standard database language. SQL is used to perform all type of data operations in RDBMS.
    > 
    > Although there might be question arises, what is Spark SQL then, So to understand it, i am also adding brief introduction on Spark SQL.
    > 
    > **Spark SQL**
    > 
    > Apache Spark SQL is a module for structured data processing in Spark. Using the interface provided by Spark SQL we get more information about the structure of the data and the computation performed.
    > 
    > ![](https://qph.ec.quoracdn.net/main-qimg-68d95846ebf05c47b0c615bbaaf148e6)
    > 
    > With this extra information, one can achieve extra optimization in Apache Spark. We can interact with Spark SQL in various ways like [**DataFrame**](http://data-flair.training/blogs/apache-spark-sql-dataframe-tutorial/) and the [**Dataset API**](http://data-flair.training/blogs/apache-spark-dataset-tutorial/). The Same execution engine is used while computing a result, irrespective of which API/language we use to express the computation. Thus, the user can easily switch back and forth between different APIs, it provides the most natural way to express a given transformation.
    > 
    > To learn more about Spark SQL, follow link: [**Spark SQL -- An Introductory Guide for Beginners**](https://goo.gl/CcdZf1)
    > 
    > Also test your Spark knowledge, by link [**Top 50+ Apache Spark Interview Questions and Answers**](https://goo.gl/vqKCJG)
    > 


