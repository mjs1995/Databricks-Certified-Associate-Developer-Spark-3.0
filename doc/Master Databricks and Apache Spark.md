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
