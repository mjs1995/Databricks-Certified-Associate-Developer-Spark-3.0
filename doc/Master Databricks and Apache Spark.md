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
- why use sql with Pyspark?
  - Its easy to load Pyspark dataframe using SQL
  - SQL is very expressive and powerful
  - Everyone knows SQL
  - SQL Tables are the ideal place to store and query data
  - SQL Tables and Views can be accessed from any Spark language 
  - ```python
    df = (sqlContext.read.fromat("csv")
                    .option("header", "false")
                    .option("inferScheam", "true")
                    .load("dbfs:/Filestore/tables/FactInternetSalesReason.csv")
                    .toDF("SalesOrderNumber", "SalesOrederLineNumber", "SalesReasonKey"))
    df.show(4) / df.take(4)
    
    df.toPandas()
    type(df.toPandas())
    
    df.cache() # cache data for faster reuse
    
    df.withColumnRenamed("before","after")
    
    display(df.take(5))
    
    display(df.describe(['SalesAmount', 'UnitPrice'])
    
    df = spark.sql('''select customerkey, geographykey, commuteDistance, BirthDate, Gender
                      from awproject.dimcustomer''')
    ```
  - ![image](https://user-images.githubusercontent.com/47103479/223428999-521be573-821d-4b35-80a6-c283b6b2d2a3.png)
  - ![image](https://user-images.githubusercontent.com/47103479/223428849-58ddc5b1-7a88-4cc9-9aeb-1d277298bd58.png)
  - Broadcast
    - 한 테이블은 크고 다른 하나는 작음 
    - ```python
      from pyspark.sql.functions import broadcast
      spdf_salesterritory = spdf_sales.join(broadcase(spdf_salesterritory) , ['SalesTerritoryKey', 'SalesTerritoryKey'], how = 'left')
      ```
- dataframes_scalar_udf
  - ```python
    # show all spark configuration settings 
    sc.getConf().getAll()
    
    # get a specific spark configuration setting value
    spark.conf.get("spark.sql.execution.arrow.enabled")
    spark.conf.get("spark.sql.execution.arrow.enabled", "true)
    ```
  - instr : 문자열찾기 
    - ![image](https://user-images.githubusercontent.com/47103479/224026047-df71675a-0e0d-4d09-ac26-82f7564c8a8b.png)
    - ![image](https://user-images.githubusercontent.com/47103479/224026203-7973f696-ba84-4ad2-975b-b8701c30413e.png)
- Running Python on Cluster Nodes
  - ![image](https://user-images.githubusercontent.com/47103479/224026917-ae4b7675-fff3-4c4b-bcec-714e33f99083.png)
    - 파이썬 코드를 병렬로 만들때 직렬화 역직렬화를 해야해서 많은 오버헤드를 유발함(scalar가 자바기반으로 키-값 형태로 JVMd에서 연산을 작업해야해서) 
  - Apache Arrow
    - ![image](https://user-images.githubusercontent.com/47103479/224027231-68e11dcd-a6e3-42a9-8786-7b74c6c110b2.png)
      - Arrow가 판다스 데이터프레임을 대체하는 형식으로 파이썬 코드가 스칼라나 다른 언어들만큼 빠르게 동작할 수 있음
    - <img width="1091" alt="image" src="https://user-images.githubusercontent.com/47103479/224027522-62b32fca-b04d-4dd6-8817-59bd95c983ab.png">
    
    - <img width="1032" alt="image" src="https://user-images.githubusercontent.com/47103479/224031322-a2bf97eb-895f-43bb-8ad8-3539bc52e70f.png">

    - <img width="711" alt="image" src="https://user-images.githubusercontent.com/47103479/224032184-b16312a9-4c77-40a7-9576-31140e5ff26a.png">

    - 장점
      - Arrow가 없으면 데이터를 (역)직렬화하고 행을 전송해야 합니다. 비효율적인 인코딩을 사용하여 JVM과 R 사이의 행별 최신 CPU 설계를 채택하지 않는 형식
      - Apache Spark 3.0에서 새로운 벡터화된 구현은 Apache Arrow를 활용하여 SparkR에 도입되어 JVM과 R 드라이버/실행기 간에 최소한의  데이터 (비)직렬화 비용
      - createDataFrame()
      - collect()
      - dapply()
      - dapplyCollect()
      - gapply()
      - gapplyCollect()
      - Any Custom R Code Running on the Cluster Nodes

## PySpark Parallel Database
- Partionining Parameters
  - numPartitions : the number of data Splits
  - column : the column to partition by, e.g. id
  - lowerBound : the minimum value for the column - inclusive
  - upperBound : the maximum value of the column -be careful, it is exclusive 
  - ![image](https://user-images.githubusercontent.com/47103479/224029514-69274b26-c5d4-4177-8bd8-6ca79ebe45f4.png)
  - ![image](https://user-images.githubusercontent.com/47103479/224030208-1bd0032c-4ebf-4a73-a9dd-51fdb1142f0a.png)
  - ![image](https://user-images.githubusercontent.com/47103479/224030402-03378b60-b307-491f-8194-4801b9f44d0c.png)

## Scala
- when should you use scala?
  - need to do a lot of work directly with RDDs
  - want to use the strongly typed dataset API
  - Other edge cases 
  - need the features of Scala 
