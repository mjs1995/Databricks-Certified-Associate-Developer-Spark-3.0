# Master Databricks and Apache Spark 
## plan
- Learn Apache Spark & Databricks in Parallel
- The Tools of the Trade
- Real World Use Case
- The Data Science Process
- Padawan to Jedi Knight 
- Core Concepts and Services
- Fellowship of the Cluster 

## Introduction
- <img width="1141" alt="image" src="https://user-images.githubusercontent.com/47103479/222966980-e018cd50-334b-4736-a14a-ce85d331eeae.png">
- General spark cluster architecture
  - ![image](https://user-images.githubusercontent.com/47103479/222966701-3fdc3330-5f16-4e37-9751-6594bacafad0.png)
  - Driver runs the user's main function and executes the various parallel operations on the worker nodes
  - The results of the operations are collected by the driver 
  - The worker nodes read and write data from/to Data Sources including HDFS
  - Worker node also cache transformed data in memory as RDDs (Resilient Data Sets)
  - Worker nodes and the Driver Node execute as VMs in public clouds (AWS, Google and Azure) 
- Apache Spark
  - A unified, open source, paralle, data processing framework for Big Data Analytics 
  - <img width="677" alt="image" src="https://user-images.githubusercontent.com/47103479/222966992-16f986f0-695f-4a5e-87b9-1d4c96f11eef.png">
- HDInsight(Azure)
  - Hortonworks Hadoop Distribution
  - Various Hadoop Platform as a Service (PaaS) Options 
  - Several Types of Clusters
  - <img width="730" alt="image" src="https://user-images.githubusercontent.com/47103479/222967927-c064c2bd-dbce-48b7-8911-951ea48566eb.png">

## Data Science Process
- The Data Science Process
  - ![image](https://user-images.githubusercontent.com/47103479/223128535-d072c19b-14fc-4d3e-948f-bd60bf021a7a.png)
  - Data Engineering
    - ![image](https://user-images.githubusercontent.com/47103479/223129228-5172a24f-becc-4160-a714-3f05fc2b34a9.png)


## Understanding Spark SQL
- Spark SQL
  - Structure Query Language(SQL) Support on Spark
  - Backbone of Data Engineering on Spark
  - Integrated with Other Spark Services 
  - Supports Most Standard SELECT syntax
  - Does not have a database catalog
  - Does not support stored procedures or functions 
  - Does not support referential integrity(참조무결성)
  - Limited security Support, i.e. Grant and Revoke 
- why Structure Query Language(SQL)?
  - It's a Very Expressive and Readable Query Language
  - Supports Complex Queries
  - People Already Know It
  - Can Be Used from Other Spark Languages
  - Supports Performance Tuning and Optimization

## Pyspark 
- Spark RDD to Dataframe - Win/Win
  - Originally had to use Resilient Distributed Dataset (블랙박스 모델이라 문제) 
  - Dataframe Support Added in 1.x 
  - Dataframes provide a Native Language Paradigm/Feel
  - Easier to Read 
  - Performs much better(Catalyst Optimizer 때문) 
  - we will focus on the DataFrame API 
- what is an RDD?
  - Resilient Distributed Dataset(탄력적인 분산 데이터 세트)
  - Fault-tolerant colection of elements that can be operated on in parallel 
  - RDDs are Immutable 
  - Fundamental Spark Data Structure 
- Lazy Evalutaion
  - Spark will only do something when forced to 
  - Transformations are not done until an Action is called
  - Transformations create a new RDD from an existing RDD 
  - Actions return the results to the Driver 
- Transformation
  - Applies logic to the dataset to change it 
  - map() - Pass each element through a function
  - filter() - Select elements to retain
  - sample() - Return a subset of the dataset 
- Action
  - Executes pending transformations
  - Returns results to the driver 
  - count() - Return the number of elements 
  - reduce() - Return an aggregation
  - collect() - Return the results to the driver (caution)
  - take(n) - Returns n rows to the driver 
