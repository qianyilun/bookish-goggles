## Introduction

- Apache Spark is a fast and general-purpose cluster computing system for large scale data processing
- 是一种通用的大数据计算框架
- High-level APIs in Java, Scala, Python and R



## Overview 

#### Spark and Hadoop structures

![Screen Shot 2019-03-10 at 4.51.56 PM](https://ws2.sinaimg.cn/large/006tKfTcly1g0yiul93k8j31sl0u07wh.jpg)

 

#### Spark and MapReduce computation process
![Screen Shot 2019-03-10 at 5.53.38 PM](https://ws3.sinaimg.cn/large/006tKfTcly1g0yklmqp6rj32200u0e81.jpg)

Spark 是基于内存的计算，因此速度比 MapReduce 更快。



## Constructure

![Screen Shot 2019-03-10 at 4.27.02 PM](https://ws1.sinaimg.cn/large/006tKfTcly1g0yi3aixjxj31no0sinm5.jpg)

- Spark Core (not included above)
  - for offline computation
- Spark SQL
  - query structured data
    - e.g. `csv`, `json` file… 
- Sparking Streaming
  - uses "micro batching"
  - real-time processing 
    - not real-time, but close
- MLlib (machine learning)
- GraphX
  - for graph processing 
  - computation related to graph



#### Spark vs Hadoop

* Spark: mainly for big data computation
* Hadoop: mainly for big data storage
* Spark + Hadoop will be the future



Spark Abstractions & Concepts

* RDD: Resilient Distributed Dataset
* DAG: Direct Acyclic Graph
* SparkContext
* Transformations
* Actions





## Reference

https://www.bilibili.com/video/av19995678?from=search&seid=7892226631828619394