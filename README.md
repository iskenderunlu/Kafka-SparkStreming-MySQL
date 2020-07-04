# Kafka-SparkStreming-MySQL
Exactly-Once-Semantics

We have some logs like the below:


Kafka logs come into the topic, then streaming then mysql. 
We aim to count "ERROR" logs by showing in the table, "error_log" .

Have used java 1.8, pay attention for all version configaritions.


1) Run Spark Server under the project root directory via the command, "sbin/start-all.sh" .

Note: For MACOS in case of port 22 refusing, go to system preference -> sharing -> remote repository ( and put tick).

2) Run Kafka Server by following the link:

https://kafka.apache.org/quickstart

Note: Your topic name will pass into exactlyonce.scala file code as topic parameter.

3) Install MySQL 8.0.20 Server and MySQL Client

  * create database with specific name "db_name" and run the command "use db_name;".
       * specify username and password
       * specify conf db info in the exactlyonce.scala file code line as "ConnectionPool.singleton("jdbc:mysql://localhost:3306/db_name", "root", "yourpassword")".

  
  * create tables, error_log and kafka_offset according the folder, "table format"(You can find the table structure in for the both txt files.) 
  
4) Run the command, "sbt clean assembly".
5) Run the command, "spark-submit --class ExactlyOnce --master local target/scala-2.11/kafka-sparkstreaming-mysql-assembly-0.1.0.jar"


To see the results, have a look at the table, "error_log" by using "select * from error_log;".

