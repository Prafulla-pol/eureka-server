# eureka-server
Configuring a highly available and a resilient Eureka server cluster and test it on local machine.

## Good Resources
1. Spring Cloud: Service Discovery With Eureka: https://medium.com/swlh/spring-cloud-service-discovery-with-eureka-16f32068e5c7
2. Spring Cloud: High Availability for Eureka: https://medium.com/swlh/spring-cloud-high-availability-for-eureka-b5b7abcefb32

# Starting Up Eureka Server Cluster and Client on Local Machine
###### Step 1 — Edit the hosts file (Windows):
C:\Windows\System32\drivers\etc\hosts

127.0.0.1 default-eureka-server.com
127.0.0.1 peer-1-server.com
127.0.0.1 peer-2-server.com
127.0.0.1 peer-3-server.com

###### Step 2 — Build the Eureka server:

prafulla.pol@ppol-2214 MINGW64 /c/learn/Microservices/gitbranches/eureka-server/eureka-server (master)
$ ./mvnw clean package


###### Step 3 — Start the Eureka Server:
prafulla.pol@ppol-2214 MINGW64 /c/learn/Microservices/gitbranches/eureka-server/eureka-server (master)
$ java -jar target/eureka-server-0.0.1-SNAPSHOT.jar

Single Instance Available: http://default-eureka-server.com:9000/

OR start the cluster

prafulla.pol@ppol-2214 MINGW64 /c/learn/Microservices/gitbranches/eureka-server/eureka-server (master)
$ java -jar -Dspring.profiles.active=peer-1 target/eureka-server-0.0.1-SNAPSHOT.jar
$ java -jar -Dspring.profiles.active=peer-2 target/eureka-server-0.0.1-SNAPSHOT.jar
$ java -jar -Dspring.profiles.active=peer-3 target/eureka-server-0.0.1-SNAPSHOT.jar

1. http://peer-1-server.com:9001/
2. http://peer-2-server.com:9002/
3. http://peer-3-server.com:9003/

# An Eureka Client

1. spring.application.name property is used to indicate the service name. Eureka client service registers in the Eureka server with whatever the name you have provided for this property. Service’s network location will be attached to it’s service name. This value will be used by other microservices to obtain the network location via the service registry
2. bootstrap.yml file is picked up before the application.yml file by Spring Boot
3. eureka.client.serviceUrl.defaultZone indicates the location of the Eureka server. Client service will use this list of URLs to access the Eureka server application. You have to mention the URLs of all available peers as comma separated values

## Starting Eureka Client
Step 1 — Build Eureka client:

prafulla.pol@ppol-2214 MINGW64 /c/learn/Microservices/gitbranches/eureka-server/eureka-client-service (master)
$ mvn clean package

Step 2 — Run Eureka Client:
prafulla.pol@ppol-2214 MINGW64 /c/learn/Microservices/gitbranches/eureka-server/eureka-client-service (master)
$ java -jar target/eureka-client-service-0.0.1-SNAPSHOT.jar
