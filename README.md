# Kafka-SparkStreming-MySQL
Exactly-Once-Semantics

We have some logs like the below:

2017-07-30 14:09:08 ERROR some message
2017-07-30 14:09:20 INFO  some message
2017-07-30 14:10:50 ERROR some message

We aim to count "ERROR" logs by showing in the table, "error_log" .

 log_time             log_count

 2017-07-30 14:09:00          9 
 2017-08-30 14:09:00          9 



1) Run Spark Server under the project root directory via the command, "sbin/start-all.sh" .

Note: For MACOS in case of port 22 refusing, go to system preference -> sharing -> remote repository ( and put tick).

2) Run Kafka Server by following the link:

https://kafka.apache.org/quickstart

Note: Your topic name will pass into exactlyonce.scala file code as topic parameter.

3) Install MySQL 8.0.20 Server and MySQL Client

  * create database named as "pipeline" and run the command "use pipeline;".
  
  * create table, error_log like the below:
  
      create table error_log (
        log_time datetime primary key,
        log_count int not null default 0
      );
  * create table, kafka_offset like the below:
      create table kafka_offset (
        topic int primary key,
        `partition` int,
        offset int
      );
  

4) Run the command, "sbt clean assembly".
5) Run the command, "spark-submit --class ExactlyOnce --master local target/scala-2.11/kafka-sparkstreaming-mysql-assembly-0.1.0.jar"

