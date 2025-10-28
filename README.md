# lab-5-word-server-danim

This is a Spring Cloud Eureka client project that is registered and discovered in the **lab-4-eureka-server-danim** to be accessible from the client project **lab-5-sentence-server-danim**
This project acts as a client of **lab-4-eureka-server-danim** and also as a server for **lab-5-sentence-server-danim**, that load-balances several executions of lab-5-word-server-danim

# Starting this client repository

The steps to used it are:
- Start the **lab-3-server-danim** repo, which loads the configuration files from the **spring-cloud-server-config-danim** Git repository
- Start the **lab-4-eureka-server-danim** repo and check it's started correctly in http://localhost:8010
- Start several executions of **lab-5-word-server-danim** in the following way:
  - Run mvn spring-boot:run -Dspring.profiles.active=subject
  - Run mvn spring-boot:run -Dspring.profiles.active=verb
  - Run mvn spring-boot:run -Dspring.profiles.active=article
  - Run mvn spring-boot:run -Dspring.profiles.active=adjective
  - Run mvn spring-boot:run -Dspring.profiles.active=noun
  - Run mvn spring-boot:run -Dspring.profiles.active=cold-noun
- Start the class annotated with @SpringBootApplication in this repo. Check that the 6 application are started in the "Application" section. There should be two for NOUN and one for each other SUBJECT, VERB, ARTICLE and ADJECTIVE

# Dependencies

Spring Web, Config Server, Eureka Discovery Client, Spring Boot Actuator, Spring Boot DevTools

# Tips

- The project starting class is annotated with **@SpringBootApplication** and also with @EnableDiscoveryClient to indicate that acts as an Eureka Client
- The **application.yml** config file specifies the URI of the Git repository where the configuration files are stored, **spring-cloud-server-config-danim** and also the different profiles (subject, verb, article, adjective, noun) to read the correct **application-<profile>.yml** file from this Git repository. It specifies also an additional profile (cold-noun) that specifies the words
- The **WordController** has a variable that points to the words key in the **application.yml**, or in the **application-<profile>.yml** file from the **spring-cloud-server-config-danim** Git repository
