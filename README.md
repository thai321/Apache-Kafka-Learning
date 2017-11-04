# Apache-Kafka-Learning


## Topics and partitions
- Topics: a particular stream of data.
  - Similar to a table in a database (without all the constraints).
  - You can have as many topics as you want.
  - A topic is identified by its name.
- Topics are split in partitions
  - Each partition is ordered
  - Each message within a partition gets an increamental id, called offset

## Brokers
- A Kafka cluster is composed of multiple brokers (servers)
- Each broker is identified with its ID (integer)
- Each broker contains certain topic partitions
- After connecting to any broker (called a bootstrap broker), you will be connected to the entire cluster
- A good number to get started is 3 brokers, but some big clusters have over 100 brokers


## Docker for Mac >= 1.12, Linux, Docker for Windows 10
docker run --rm -it \
           -p 2181:2181 -p 3030:3030 -p 8081:8081 \
           -p 8082:8082 -p 8083:8083 -p 9092:9092 \
           -e ADV_HOST=127.0.0.1 \
           landoop/fast-data-dev

## Docker toolbox
docker run --rm -it \
          -p 2181:2181 -p 3030:3030 -p 8081:8081 \
          -p 8082:8082 -p 8083:8083 -p 9092:9092 \
          -e ADV_HOST=192.168.99.100 \
          landoop/fast-data-dev

## Kafka command lines tools
docker run --rm -it --net=host landoop/fast-data-dev bash



## Create Topic
kafka-topics --zookeeper 127.0.0.1:2181 --create --topic first_topic --partitions 3 --replication-factor 1

## List Topic
kafka-topics --zookeeper 127.0.0.1:2181 --list

## Delete Topic
kafka-topics --zookeeper 127.0.01:2181 --topic second_topic --delete


## Describe
kafka-topics --zookeeper 127.0.01:2181 --describe --topic first_topic


## Read data from standard input and publish it to Kafka.
kafka-console-producer

## Publishing messages
kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic


### The console consumer is a tool that reads data from Kafka and outputs it to standard output.
kafka-console-consumer


## Consumer and publising messages
kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic

kafka-console-producer --topic first_topic --broker-list 127.0.0.1:9092

## List all the messages
```txt
root@fast-data-dev / $ kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning
hello
exit
hi
new message
Here is a new message!
thai nguyen
Hello from producer
```

## Read from a partition
```
kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning --partition 0
hello
exit
```


## group id
```
root@fast-data-dev / $ kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --consumer-property group.id=mygroup1 --from-beginning
hello
exit
hi
new message
Here is a new message!
thai nguyen
Hello from producer
```
