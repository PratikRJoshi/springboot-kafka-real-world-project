# Spring Boot & Kafka Real-World Project

This project demonstrates a real-world data streaming pipeline using Spring Boot and Apache Kafka. It captures real-time data from the Wikimedia event stream, processes it through a Kafka topic, and persists it into a MySQL database.

## Project Architecture

The architecture consists of two main microservices:

1.  **`kafka-producer-wikimedia`**: A Spring Boot application that connects to the Wikimedia real-time event stream, produces messages, and sends them to a Kafka topic.
2.  **`kafka-consumer-database`**: A second Spring Boot application that consumes messages from the Kafka topic and saves the data into a MySQL database.

This setup showcases a decoupled, scalable, and resilient system for handling real-time data feeds.

---

## Modules

### 1. `kafka-producer-wikimedia`

This module is responsible for fetching real-time data and producing it to Kafka.

-   **Functionality**: It uses an EventSource client to connect to the Wikimedia stream URL (`https://stream.wikimedia.org/v2/stream/recentchange`).
-   **Technology**: It leverages `okhttp-eventsource` to handle the streaming connection and `spring-kafka` to send messages to a topic named `wikimedia_recentchange`.

### 2. `kafka-consumer-database`

This module consumes the data from Kafka and persists it.

-   **Functionality**: It listens to the `wikimedia_recentchange` topic. For each message received, it deserializes the data and saves it as an entity in a MySQL database.
-   **Technology**: It uses `spring-kafka` for consuming messages and `Spring Data JPA` with Hibernate to interact with the MySQL database.

---

## How to Run

To run this project, you will need:

-   Java 17+
-   Maven
-   Docker (for running Kafka and MySQL)

1.  **Start Services**: Make sure you have Kafka and MySQL instances running. You can use Docker Compose for a quick setup.
2.  **Configure Consumer**: Update the `application.properties` file in the `kafka-consumer-database` module with your MySQL database URL, username, and password.
3.  **Run Producer**: Start the `SpringBootProducerApplication` in the `kafka-producer-wikimedia` module.
4.  **Run Consumer**: Start the `SpringBootConsumerApplication` in the `kafka-consumer-database` module.

Once running, the producer will start sending live data from Wikimedia to Kafka, and the consumer will begin storing it in your database.

## Technologies Used

- **Spring Boot 2.6.7**
- **Apache Kafka** with Spring Kafka
- **MySQL** database
- **Spring Data JPA**
- **Maven** for dependency management
- **Java 17**