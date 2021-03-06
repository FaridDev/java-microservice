# Hands-on Microservices with Java

Read the post talking about this project https://medium.com/hands-on-microservices-with-java/hands-on-microservices-with-java-e8a5b5b022ee
 
“Microservices Architecture” example with many concepts and technologies put in place and combined within a whole system composed with different microservices. 
Some patterns, tools and technologies that you will see in this system:

Spring Boot, Spring Data, Spring Cloud Eureka, Load Balancing with Ribbon, 
Declarative REST Clients with Feign, Software Circuit Breakers with Hystrix, 
Monitoring using Hystrix dashboard and Turbine, Administrating using Spring admin,
Log management with Elastic search, Logstash and Kibana (ELK), Server load balancing with Nginx,
Infrastructure management with Docker-compose, JMX application monitoring,
Security with Spring Security OAuth, Oauth2 with JWT, Aspect Oriented Programing, 
Distributed events with Kafka, Maven Multimodule project, Event Sourcing, 
CQRS, REST, Web Sockets and all developed using Java 8.

![Alt text](microservices-architecture.jpg?raw=true "microservices architecture")


## How to use

### Spring boot embedded tomcat
* run package-projects.sh
* Start all services -> sudo sh start_all.sh  

### Using Docker
* run package-projects.sh
* run docker-orchestrate.sh
* docker-compose -f infra-docker-compose.yml -p todo up
* docker-compose -p todo up 

### Accessing the services
* Authenticate -> curl -X POST -vu todo-app:123456 http://localhost:8017/oauth/token -H "Accept: application/json" -d "password=1234&username=apssouza22@gmail.com&grant_type=password&scope=write&client_secret=123456&client_id=todo-app"  

* Get data using the access_token -> localhost:8018/accounts?access_token={access_token} or curl -H "Authorization: Bearer $TOKEN" "localhost:8018/path"

### URLs
Monitoring stream - http://localhost:8022/turbine.stream

To-dos http://localhost:8015/todos

Users http://localhost:8016/accounts 

Eureka server - http://localhost:8010/

Config server - http://localhost:8888/

Boot admin - http://localhost:8026

Kimbana - http://localhost:5601

Elasticsearch Info: http://localhost:9200

Elasticsearch Status: http://localhost:9200/_status?pretty

NGINX Status: localhost/nginx_status

docker-compose -p todo up
docker-compose -p todo down

## OBS
* In order to make ELK work we need to reserve 3GB RAM to docker(docker settings - advanced - memory )

## Useful Commands

### Stopping, Starting, Restarting...

```
# orchestrate start-up of containers, tailing the logs...
docker-compose -p music up -d container-name && docker logs elk --follow # ^C to break

# stopping containers
docker-compose todo stop
docker-compose todo down

# starting containers
docker-compose -p todo up

# removing containers
docker-compose todo rm

```

## Application Startup Issues

```bash
# stop / start Tomcat
docker exec -it container-name sh /usr/local/tomcat/bin/startup.sh
docker exec -it container-name sh /usr/local/tomcat/bin/shutdown.sh

# check logs for start-up issues...
docker exec -it container-name cat /usr/local/tomcat/logs/catalina.out
docker logs container-name
```

## TODO
* Integrate mail service to reminder-service
* Add spring config support