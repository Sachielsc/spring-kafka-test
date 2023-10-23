# Spring Kafka test example
## My fork info
Originally forked from [kasramp's spring-kafka-test](https://github.com/kasramp/spring-kafka-test)

Click [here](https://www.geekyhacker.com/test-spring-kafka-consumer-and-producer-with-embeddedkafka/) to check its first tutorial "Test Spring Kafka consumer and producer with EmbeddedKafka"

Click [here](https://www.geekyhacker.com/write-kafka-integration-test-with-testcontainers/) to check the next tutorial "Write Kafka integration test with Testcontainers"

## My Readme
This article is useful for anyone who uses Spring or Spring Boot with Spring Kafka library. If you use the low-level Apache Kafka library or even Spring Cloud Stream Kafka, you need to look somewhere else. Here, we only cover how to test Spring Kafka components.

For testing, we are going to use another Spring library that is called spring-kafka-test. It provides much functionality to ease our job in the testing process and takes care of lots of headaches. Additionally, we use JUnit 5, not 4. If you still are using JUnit 4, you may need to change some of the annotations accordingly.

The first article is about using `EmbeddedKafka` only. But this repo working example contains both EmbeddedKafka and Kafka Testcontainers examples. Click [here](https://www.geekyhacker.com/write-kafka-integration-test-with-testcontainers/) to check the next article about using test containers.

## How to test
After initialize and run the app as per the official steps, use this command in the Unix terminal:
1. Run the Kafka integration test with Testcontainers
```bash
$ ./mvnw test -Dtest=UserKafkaTestcontainersTest
```

## Official site Readme
Spring Kafka example with JUnit 5 using EmbeddedKafka/`spring-kafka-test` and also using [Testcontainers](https://www.testcontainers.org/).

For the tutorials check the links below,

- [Test Spring Kafka consumer and producer with EmbeddedKafka](https://www.geekyhacker.com/test-spring-kafka-consumer-and-producer-with-embeddedkafka/)
- [Write Kafka integration test with Testcontainers](https://www.geekyhacker.com/write-kafka-integration-test-with-testcontainers/)
- [Database migration with Spring Boot and Flyway](https://www.geekyhacker.com/database-migration-with-spring-boot-and-flyway/)
- [Spring Boot MySQL integration tests with Testcontainers](https://www.geekyhacker.com/spring-boot-mysql-integration-tests-with-testcontainers/)

## How to run

First start the docker-compose which contains ZooKeeper, Kafka, Kafdrop, and MySQL.

```bash
$ docker-compose -f docker-compose.yml up -d
```

Once all the containers are healthy start the application,

```bash
$ ./mvnw spring-boot:run
```

Open the browser `localhost:8080/apidocs`. 

You can interact with the `random` API to create a random user which then will be sent to Kafka and consumed by the consumer (see [`consumer/UserKafkaListener.java`](https://github.com/kasramp/spring-kafka-test/blob/master/src/main/java/com/madadipouya/springkafkatest/consumer/UserKafkaListener.java) file) and finally saves into the database.

To see whether the message has been sent to Kafka, open your browser `http://localhost:8085/topic/com.madadipouya.kafka.user` (Kafdrop environment), 
you should be able to see all messages that sent to `kafka.user` topic.

To run Flyway migration scripts only run,

```bash
$ ./mvnw flyway:migrate
```
