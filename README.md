# kafka-compose
docker-compose kafka `multiple broker` sample  
***!!!offers varios tips, check it out!!!***

# Motivation
It is very difficult to reproduce kafka's system requirements with docker-compose
For details, see [here](https://github.com/wurstmeister/kafka-docker/wiki/Connectivity#kafka-requirements)

a bit summary,
> Kafka Requirements
> There are three main requirements for configuring Kafka networking.
>
> 1. Each Broker must be able to talk to Zookeeper - for leader election etc.
> 2. Each Broker must be able to talk to every other Broker - for replication etc.
> 3. Each Consumer/Producer must be able to talk to every Broker - for reading/writing data etc.
>
> The following diagram represents the different communication paths:
> ![KafkaRequirements](https://github.com/wurstmeister/kafka-docker/wiki/kafka-communication.png)

# Quick Start
1. add alias `kafka.local` to `127.0.0.1`(if you are not using docker-for-mac, set proper ip address for docker)
2. run commands below
```sh
$ git clone https://github.com/ShotaOd/kafka-compose.git
$ docker-compose up -d --scale kafka_node=2
```
3. O.K.! send messsage and recive message  

open 2 shell window

first shell is for sending message (and creating topic if not exist)
this scripts send date message every 5sec
```sh
watch -n5 'echo "{\"date\": \"$(date)\"}" | docker-compose run --rm kafkacat -b kafka.local:9092 -t myTopic -P'
```

second shell is for waiting message

```sh
$ docker-compose run --rm kafkacat -b kafka.local:9092 -t myTopic -C
```

then receive streaming message at first shell

# Utilities
To communicate kafka, including some utilities below

|               | type                                    | link                                    |
|---------------|-----------------------------------------|-----------------------------------------|
| kafkacat      | Command                                 | https://github.com/edenhill/kafkacat    |
| kafka_manager | GUI([port:9000](http://localhost:9000)) | https://github.com/yahoo/kafka-manager  |
| trifecta      | GUI([port:9001](http://localhost:9001)) | https://github.com/ldaniels528/trifecta |

# Links

## kafka support tools
- [x] [kafkacat](https://github.com/edenhill/kafkacat)
- [x] [kafka_manager](https://github.com/yahoo/kafka-manager)
- [x] [trifecta](https://github.com/ldaniels528/trifecta)

## guides
- https://github.com/wurstmeister/kafka-docker/wiki/Connectivity
- https://davidfrancoeur.com/post/kafka-on-docker-for-mac/
- https://www.ianlewis.org/en/almighty-pause-container
