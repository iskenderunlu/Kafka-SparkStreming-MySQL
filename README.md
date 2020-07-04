# Kafka-SparkStreming-MySQL
Exactly-Once-Semantics

We have some logs like the below:

We aim to count "ERROR" logs by showing in the table, "error_log" .

1) Run Spark Server under the project root directory via the command, "sbin/start-all.sh" .

Note: For MACOS in case of port 22 refusing, go to system preference -> sharing -> remote repository ( and put tick).

2) Run Kafka Server by following the link:

https://kafka.apache.org/quickstart

Note: Your topic name will pass into exactlyonce.scala file code as topic parameter.

3) Install MySQL 8.0.20 Server and MySQL Client

  * create database named as "pipeline" and run the command "use pipeline;".
  
  * create tables, error_log and kafka_offset according the folder, "table format"(You can find the table structure in for the both txt files.) 
  
4) Run the command, "sbt clean assembly".
5) Run the command, "spark-submit --class ExactlyOnce --master local target/scala-2.11/kafka-sparkstreaming-mysql-assembly-0.1.0.jar"

