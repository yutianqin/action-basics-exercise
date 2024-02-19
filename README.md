# spring-cloud-reference-app 
This repo is a collection of spring cloud base REST API application with AWS services


🌟 Quick Access
---------------

Quickly navigate to key sections of the documentation:

*   [🔗 URLs](#important-urls)
*   [🌐 Spring Cloud Config Server](#spring-cloud-config-server)
*   [📝 S3 JSON Doc Service Guide](#s3-json-doc-service-guide)
*   [📊 Limits Service](#limits-service) 
*   [🔽 Currency Exchange Service](#currency-exchange-microservice)
*   [🔽 Currency Conversion Service](#currency-conversion-microservice)
*   [🔽 Netflix Eureka Naming Server](#netflix-eureka-naming-server)
*   [🔽 Netflix Zuul API Gateway Server](#netflix-zuul-api-gateway-server)
*   [🔽 Zipkin Distributed Tracing Server](#distributed-tracing-server-zipkin-w-docker)
*   [🔽 Docker](#docker)
*   [🔽 Docker Compose](#docker-compose)

* * *

🛠️ Service Ports
-----------------

A quick reference for the ports used by each application:

| **Application** | **Port** |
| --- | --- |
| Spring Cloud Config Server | 8888 |
| S3 JSON Doc Management Service | 8200 |
| Limits Microservice | 8080, 8081, … |
| Currency Exchange Microservice | 8000, 8001, 8002, … |
| Currency Conversion Microservice | 8100, 9101, 8102 |
| Netflix Eureka Naming Server | 8761 |
| API Gateway (Zuul) | 8765 |
| Zipkin Distributed Tracing Server | 9411 |


* * *
<br>


🚀 Quick Start Guide
--------------------

Follow these steps to set up and run your local environment efficiently and effectively.

### 🛠️ Setting Up Services

1.  **Build Each Service with Maven**:
    *   Open your terminal and build each service by navigating to its directory and executing the Maven build command. For instance:

        `cd netflix-eureka-naming-server`
    
        `mvn clean install`

    *   **Services to Build**:
        *   `netflix-eureka-naming-server`
        *   `netflix-zuul-api-gateway-server`
        *   `currency-conversion-service`
        *   `currency-exchange-service`
        *   `spring-cloud-config-server`
        *   `limits-service`
        *   `s3-doc-service`

### 🌟 Running the Services

For each subsequent service, use either the Maven command, the shell script, or IntelliJ's tool.
* **Method 1**
   1.  Open a terminal
   2.  `cd` to the directory of the service you'd like to run
        *  Either - **Maven Command**: `mvn spring-boot:run`
        *  Or - **Shell Script**: `sh run_service.sh`
  
* **Method 2**
   *   **IntelliJ Option**: Use the built-in services tool (`Command + 8`)
       *   Right click the service you'd like to run (e.g.`DemoApplication[devtools]` as it in the picture below)
       *   Click `run`
  
    ![Intellij Service Run](img/run-services-2.png)

    When they are ran:

    ![IntelliJ Service Run](img/run-services.png)

Ensure to run the services in the specified order for proper inter-service communication:

1.  **Netflix Eureka Naming Server** (Service Registry):
  
2.  **Netflix Zuul API Gateway Server** (Gateway Server)
    
3.  **Currency Exchange Service**
    
4.  **Currency Conversion Service**
    
5.  **Spring Cloud Config Server**
    
6.  **Limits Service**

7.  **S3 Doc Service**
    



### 🔍 Testing the Services

*   **Final Step**: After successfully starting all services, test their integration and functionality by accessing the [provided URLs](#important-urls) below. This will confirm that each service is operational and communicating correctly.
    *   To test S3 JSON doc management service, check [📝 S3 JSON Doc Service Guide](#s3-json-doc-service-guide)



---
<br>




<a name="important-urls"></a>
<br>

🔗 Important URLs
-----------------

Access these URLs to interact with and test the various services in your project:

### 🌐 Eureka Naming Server

*   **URL**: `http://localhost:8761/`
*   **Description**: Access the Eureka Service Dashboard to view the list of connected services.

### 💱 Currency Exchange Service

*   **URL**: `http://localhost:8000/currency-exchange/from/USD/to/INR`
*   **Description**: Retrieve the currency exchange rate from USD to INR.

### 💹 Currency Conversion Service

*   **URLs**:
    *   Direct Access: `http://localhost:8100/currency-conversion/from/USD/to/INR/quantity/10`
    *   Using Feign Client: `http://localhost:8100/currency-conversion-feign/from/USD/to/INR/quantity/10`
*   **Description**: Convert currency from USD to INR for a specific quantity.

### 🚦 Spring Cloud API Gateway

*   **URLs**:
    *   Exchange: `http://localhost:8765/currency-exchange/from/USD/to/INR`
    *   Conversion: `http://localhost:8765/currency-conversion/from/USD/to/INR/quantity/10`
    *   Feign Conversion: `http://localhost:8765/currency-conversion-feign/from/USD/to/INR/quantity/10`
    *   New Conversion Route: `http://localhost:8765/currency-conversion-new/from/USD/to/INR/quantity/10`
*   **Description**: Access various currency services via the API Gateway.

### 🌐 Zipkin Distributed Tracing

*   **URL**: `http://localhost:9411/`
*   **Description**: View distributed tracing information. For setup instructions, see [Run Zipkin](#run-zipkin).

### 📈 Limits Service

*   **URL**: `http://localhost:8080/limits`
*   **Description**: Access the Limits Service to view the current configuration limits.

<a name="config-server-url"></a>
### ⚙️ Spring Cloud Config Server

*   **URLs**:
    *   **S3-Doc-Service Properties**:
        
        *   Default Profile: `http://localhost:8888/s3-doc-service/default`
        *   Dev Profile: `http://localhost:8888/s3-doc-service/dev`
        *   Prod Profile: `http://localhost:8888/s3-doc-service/prod`
        *   Test Profile: `http://localhost:8888/s3-doc-service/test`
  
    *   **Limits-Service Properties**:
        
        *   Default Profile: `http://localhost:8888/limits-service/default`
        *   Dev Profile: `http://localhost:8888/limits-service/dev`
        *   Prod Profile: `http://localhost:8888/limits-service/prod`
        *   Test Profile: `http://localhost:8888/limits-service/test`
  
*   **Description**: Access configuration profiles for the S3 Doc Service and Limits Service. 

    [Back to spring cloud config server testing guide](#config-server-testing-guide)



---
[🔼 Back to top](#spring-cloud-reference-app)
<br><br><br><br><br>





<a name="spring-cloud-config-server"></a>

🌐 Spring Cloud Config Server
-----------------------------

This guide outlines the setup and usage of the Spring Cloud Config Server for centralized management of configuration files. The server supports various sources like Git, SVN, and HashiCorp Vault.

### 📦 Dependencies

1.  **Config Server**: For centralized configuration management.
2.  **Spring Boot DevTools**: Offers useful features like live reload for an improved development experience.

### 💡 Overview

*   The **Config Client** (e.g., `limits-service`) interacts with the **Config Server** (`spring-cloud-config-server`).
*   The **Config Server** fetches configurations from a specified repository.

**Repository Contents**: Our example repository includes 6 property files:

![Property Files in Repository](img/spring-cloud-config-data.png)

### ⚙️ Configuring the Spring Cloud Config Server

*   **File**: `spring-cloud-config-server/src/main/resources/application.properties`
*   **Configuration**:

    ```properties
    spring.application.name=spring-cloud-config-server
    server.port=8888 
    spring.cloud.config.server.git.uri=git@github.com:PalmerSoftwareConsulting/psc-spring-cloud-reference-app.git 
    spring.cloud.config.server.git.searchPaths=spring-cloud-config-data
    ```
    
### 🔌 Enabling the Config Server

In `SpringCloudConfigServerApplication.java`, activate the Config Server:

```java
import org.springframework.cloud.config.server.EnableConfigServer;    

@EnableConfigServer
```

<a name="config-server-testing-guide"></a>

### 🧪 Testing the Setup

#### 1\. Verify Properties Retrieval

* Check if the Config Server can retrieve properties from the `spring-cloud-config-data` directory:
  
    1.  **Start the Spring Cloud Config Server**:
        *   Launch the Config Server to ensure it's actively serving configuration data.
    
    2.  Try access these [Spring Cloud Config Server Testing URLs](#config-server-url).

#### 2\. Validate Config Server and Limits Service Communication

*   **Procedure**:

    1.  **Start the Spring Cloud Config Server**:
        *   Launch the Config Server to ensure it's actively serving configuration data.
  
    2.  **Launch the Limits Service**:
        *   Start the Limits Service which will fetch its configuration from the Config Server.

    3.  **Verify Configuration Retrieval**:
        
        *   Access the Limits Service at `http://localhost:8080/limits`. This endpoint should reflect the properties defined in `spring-cloud-config-data/limits-service-dev.properties`, as the Limits Service is set to the `dev` profile.
        *   **Configuration in `limits-service/src/main/resources/application.properties`**:
            
            ```properties
            spring.profiles.active=dev 
            spring.cloud.config.profile=dev
            ```

        *   Testing Different Profiles

            You can experiment with different profiles by adjusting the `spring.profiles.active` and `spring.cloud.config.profile` in the limit service's `application.properties`. This flexibility allows you to test various configurations under different environmental settings, ensuring robustness and adaptability of the Limits Service. 

            Available profiles: **default**, **dev**, **prod** and **test**.

            [Check Limits Service](#limits-service)





---
[🔼 Back to top](#spring-cloud-reference-app)
<br><br><br><br><br>






<a name="s3-json-doc-service-guide"></a>

📝 S3 JSON Document Service Guide
---------------------------------

This guide provides a comprehensive walkthrough for using the S3 JSON Document Service with the Talend API Tester, enabling you to upload and retrieve JSON documents effectively.

### 🛠️ Setup

1.  **Install the Talend API Tester Extension**:
    
    *   Download and install the **Talend API** Tester Chrome extension for an API testing.
2.  **Accessing the Talend API Tester**:
    
    *   Click the Talend API Tester icon in your browser toolbar to launch the tool.
  
* ![Talend API Test UI](img/talend-api-1.png)

### 🌐 Using the Service

#### 📤 POST Method: Upload a Document

*   **Endpoint**: `http://localhost:8200/api/documents`
*   **Method**: `POST`
*   **Request Body**: JSON format
*   **Instructions**:
    *   Use this method to upload a new JSON document to our AWS S3 Bucket.
    *   The document will be stored in the service and assigned a unique ID.

    ![Talend API Tester - POST Method](img/talend-api-2.png)
    


#### 📥 GET Methods: Retrieve Documents

1.  **Retrieve a Specific Document**:
    
    *   **URL**: `http://localhost:8200/api/documents/{id}`
    *   **Method**: `GET`
    *   **Usage**: Replace `{id}` with the desired document ID to fetch its JSON content from the S3 bucket.
2.  **List All Documents**:
    
    *   **URL**: `http://localhost:8200/api/documents/all`
    *   **Method**: `GET`
    *   **Purpose**: Displays the metadata of all documents stored in the H2 database.

### ⚠️ Important Note

*   The H2 database is temporary and will reset when the service is stopped. Documents created in previous service runs will not be available after a restart.






* * *
[🔼 Back to top](#spring-cloud-reference-app)
<br><br><br><br><br>




<a name="limits-service"></a>

📊 Limits Service
-----------------

This section outlines the setup and integration of the Limits Service with the Spring Cloud Config Server, emphasizing its dependencies and configuration.

### 🛠️ Dependencies

1.  **Config Client**: Connects to the Spring Cloud Config Server to fetch the application's configuration.
2.  **Spring Web**: Enables the building of web, including RESTful applications, using Spring MVC. It utilizes Apache Tomcat as the default embedded container.
3.  **Spring Boot Actuator**: Provides production-ready features to help monitor and manage the application.
4.  **Spring Boot DevTools**: Offers a set of tools for efficient development, including automatic restart.

### 📝 Configuration Steps

1.  **Include Dependency**: Ensure the following dependency is included in your `pom.xml` to use the Config Client:
    
    ```xml
    <dependency>
        <groupId>org.springframework.cloud<groupId>
        <artifactId>spring-cloud-starter-config</artifactId>
    </dependency>
    ```

    
2.  **Configure the Client**: Update the `application.properties` to enable the connection to the Spring Cloud Config Server:
    
    ```properties
    spring.config.import=optional:configserver:http://localhost:8888
    ```

### 🧪 Testing the Service

To test the Limits Service, follow the steps in the [Spring Cloud Config Server Test Guide](#2-validate-config-server-and-limits-service-communication). This ensures that the Limits Service correctly retrieves the maximum and minimum values from the data config directory via the Config Server.

**Note**: The Limits Service relies on the Spring Cloud Config Server to access configuration data, crucial for its functionality.





* * *
[🔼 Back to top](#spring-cloud-reference-app)
<br><br><br><br><br>







## Currency-Exchange-Microservice
Dependencies:
1. Spring Boot Actuator<br>
2. Spring Boot DevTools<br>
3. Spring Web<br>
4. Config Client

<br>

Definition: what is the exchange rate of one currency in another<br>
Eg. "How many Indian Ruppe can you get from one US dollar?"<br>
Response for http://localhost:8000/currency-exchange/from/USD/to/INR looks like:
```
{
   "id":10001,
   "from":"USD",
   "to":"INR",
   "conversionMultiple":65.00,
   "environment":"8000 instance-id"
}
```

### Load Balancing (Dynamic port)<br>
Add 'environment' member var into CurrencyExchange class:
```java
private String environment 
```
Purpose: get the port number of a specific response in order to check which instance of currency exchange that is responding.

### Configure Spring Data JPA
```xml
<!-- currency-exchange-service/pom.xml -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
</dependency>
```
```properties
# currency-exchange-service/src/main/resources/application.properties
spring.jpa.show-sql=true
spring.datasource.url=jdbc:h2:mem:name_of_your_database
spring.h2.console.enabled=true
```

Try it out:
1. Run the currencyExchangeServiceApplication<br>
2. Response for http://localhost:8000/h2-console looks like:

![alt text](img/h2-console1.png)


After clicking the 'connect' button in the UI above, you may find the database empty if you haven't properly set up the database.<br>
To insert some data into the database(data.sql):
```sql
-- currency-exchange-service/src/main/resources/data.sql
insert into currency_exchange
(id,currency_from,currency_to,conversion_multiple,environment)
values(10001,'USD','INR',65,'');
insert into currency_exchange
(id,currency_from,currency_to,conversion_multiple,environment)
values(10002,'EUR','INR',75,'');
insert into currency_exchange
(id,currency_from,currency_to,conversion_multiple,environment)
values(10003,'AUD','INR',25,'');
```

```properties
# currency-exchange-service/src/main/resources/application.properties
spring.jpa.defer-datasource-initialization=true # For >2.5.0
```

Boom
![alt text](img/h2-console2.png)


Set up JPA repository(skip for now)



---
[🔼 Back to top](#spring-cloud-reference-app)
<br><br>



## Currency-Conversion-Microservice
Dependencies:
1. Spring Boot Actuator<br>
2. Spring Boot DevTools<br>
3. Spring Web<br>
4. Config Client

<br>

Eg. converting 10 USD into INR.<br>
Response for http://localhost:8100/currency-conversion/from/USD/to/INR/quantity/10 look like:
```
{
  "id": 10001,
  "from": "USD",
  "to": "INR",
  "conversionMultiple": 65.00,
  "quantity": 10,
  "totalCalculatedAmount": 650.00,
  "environment": "8000 instance-id"
}
```

<br>

## Ways for conversion service to talk with exchange service
### 1. Rest Template
Invoking Currency Exchange from Currency Conversion 
```java
@RestController
public class CurrencyConversionController 
{	
	@GetMapping("/currency-conversion/from/{from}/to/{to}/quantity/{quantity}")
	public CurrencyConversion calculateCurrencyConversion(
			@PathVariable String from,
			@PathVariable String to,
			@PathVariable BigDecimal quantity
			) {
		
		HashMap<String, String> uriVariables = new HashMap<>();
		uriVariables.put("from",from);
		uriVariables.put("to",to);
		
		ResponseEntity<CurrencyConversion> responseEntity = new RestTemplate().getForEntity
		("http://localhost:8000/currency-exchange/from/{from}/to/{to}", 
				CurrencyConversion.class, uriVariables);
		
		CurrencyConversion currencyConversion = responseEntity.getBody();
		
		return new CurrencyConversion(currencyConversion.getId(), 
				from, to, quantity, 
				currencyConversion.getConversionMultiple(), 
				quantity.multiply(currencyConversion.getConversionMultiple()), 
				currencyConversion.getEnvironment()+ " " + "rest template");	
	}
}
```
Try it out:<br>
1. Launch CurrencyExchangeServiceApplication
2. Launch CurrencyConversionServiceApplication
3. http://localhost:8100/currency-conversion/from/USD/to/INR/quantity/10

This way of connect conversion service to exchange service is not very practical, especially in real-world projects where hundreds of microservices are typically running.

<br>

### 2. Feign
Using Feign REST Client for Service Invocation.

Add dependencies
```xml
<!-- currency-conversion-service/pom.xml -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

In the CurrencyExchangeProxy, the values('from' and 'to') retrieved from currency-exchange microservice will be automatically mapped into the currency conversion bean
```java
@FeignClient(name="currency-exchange", url="localhost:8000")
public interface CurrencyExchangeProxy {
    @GetMapping("/currency-exchange/from/{from}/to/{to}")
    public CurrencyConversion retrieveExchangeValue(
            @PathVariable("from") String from,
            @PathVariable("to") String to);
}
```

Try it out:<br>
Launch exchange & conversion services, then:<br>
http://localhost:8100/currency-conversion-feign/from/USD/to/INR/quantity/10



---
[🔼 Back to top](#spring-cloud-reference-app)
<br><br>



## General idea for currency conversion & exchange microservices:
**First, currency conversion microservice talks to currency exchange microservice**<br>
(Logistically, we need to get the exhange rate first to be able to do the conversion)<br>

**Then,  currency exchange microservice talks to an in memory database(A Rest API)**<br>
(Actually search and convey the data from the database)



---
<br><br>



## Netflix-Eureka-Naming-Server
Dependencies:
1. Spring Boot Actuator<br>
2. Spring Boot DevTools<br>
3. **Eureka Server -> spring-cloud-netflix Eureka Server**

<br>

To dynamically launch currency exchange instances and distribute load between them

Things to add:

In 'naming-server/src/main/java/com/example/microservices/namingserver/NamingServerApplication.java'
```java
@EnableEurekaServer
```
In 'microservices-spring-cloud/naming-server/src/main/resources/application.properties'
```properties
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

Try it out:<br>
1. Launch the NamingServerApplication<br>
2. http://localhost:8761/
![alt text](img/eureka-page.png)

<br>

Get the currency exchange microservice and the currency conversions microservice to register with the naming server:<br>

-> To add Eureka client dependency
```xml
<!-- currency-conversion-service/pom.xml -->
<!-- currency-exchange-service/pom.xml -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

-> To make it 'safer'
```properties
# currency-conversion-service/src/main/resources/application.properties
# currency-exchange-service/src/main/resources/application.properties
eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka
```

<br>

Try it out:
1. Launch namingServerApplication<br>
2. Launch either conversion or exchange application, or launch both<br>
3. Response for http://localhost:8761/ should list all the services connected to naming-server

---

### General idea of naming server with currency exchange microservice and currency conversion microservice

All the microservices would register with the service registry(netflix-eureka-naming-server)

In our example, if the currency conversion microservice want to talk to the currency exchange microservice, it will ask the naming-server for the addresses of the currency exchange microservices. The naming-server will return those addresses back to the currency conversion microservice, and then the currency conversion microservice can send the request out to the exchange microservice.



---
[🔼 Back to top](#spring-cloud-reference-app)
<br><br>



## Load Balancing with Eureka, Feign & Spring Cloud LoadBalancer

1. Launch namingServerApplication; <br>
2. Launch currencyExchangeApplication on **both port 8001 and 8000**; <br>
3. Launch currencyConversionApplication; <br>
    Check http://localhost:8761 <br>
    -> You may see something like this:
    ![alt text](img/registered-services.png) 

4. Now, if you refresh http://localhost:8100/currency-conversion-feign/from/USD/to/INR/quantity/10 multiple times, you may find the 'environment' value switches between 8000 and 8001(it's doing automatically load balancing);

    ### What's happening in step 4 above?
    It's client side load balancing. It's happening through Feign. Inside the currency conversion microservice, there is load balancer component which is talking to the naming server, finding the instances of currency exchange microservice and doing automatic load balancing between them. <br>
    Further detail: There is a load balancer ('spring-cloud-starter-loadbalancer') which is brought into the class path by 'spring-cloud-starter-netfilx-eureka-client'. And this is ther load balancer framework that is used by Feign to distribute the load among the multiple instances which are returned by Eureka.



---
<br><br>



## Netflix-Zuul-API-Gateway-Server

Dependencies:
1. Spring Boot Actuator<br>
2. Spring Boot DevTools<br>
3. **Eureka Discovery Client -> A REST based service for locatin services for the purpose of load balancing and failover of middle-tier servers**<br>
4. **Gateway -> Provides a simpl.≥...,e, yet effective way to route to APIs and provide cross cutting concerns to them such as security, monitoring/metrics, and resiliency**

Make sure this is added.
```properties
# api-gateway/src/main/resources/application.properties
spring.cloud.gateway.discovery.locator.enabled=true
```
First launch netflix-eureka-naming-server,<br>
Then launch netflix-zuul-api-gateway-server, currency-exchange-service and currency-conversion-service;<br>
Try to access the exchange service or conversion service through API gateway:<br>
http://localhost:8765/CURRENCY-EXCHANGE/currency-exchange/from/USD/to/INR<br>
http://localhost:8765/CURRENCY-CONVERSION/currency-conversion-feign/from/USD/to/INR/quantity/10


## Custom Route
The example code snippet below maps '/get' to a specific URL (the URL could be our microservice).
```java
// api-gateway/src/main/java/com/example/apigateway/ApiGatewayConfiguration.java
@Configuration
public class ApiGatewayConfiguration {
    @Bean
    public RouteLocator gatewayRouter(RouteLocatorBuilder builder) {
        return builder.routes()
                .route(p -> p
                        .path("/get")
                        .filters(f -> f
                                .addRequestHeader("MyHeader", "MyURI")
                                .addRequestParameter("Param", "MyValue"))
                        .uri("URL we want to map to"))
                .build();
    }
}
```
For our project:<br>
If a request URL starts with "currency-exchange", redirect it using the Eureka naming server to find the location of this service, and do load balancing between the instances which are returned.
```java
.route(p -> p.path("/currency-exchange/**").uri("lb://currency-exchange"))
```
From now, the old clumsy URL for exchange server will not work.<br>
Try this:<br>
http://localhost:8765/currency-exchange/from/USD/to/INR<br>

Same techniques are applied to other services.<br>
Try them out:<br>
http://localhost:8765/currency-conversion/from/USD/to/INR/quantity/10<br>
http://localhost:8765/currency-conversion-feign/from/USD/to/INR/quantity/10<br>
http://localhost:8765/currency-conversion-new/from/USD/to/INR/quantity/10



---
[🔼 Back to top](#spring-cloud-reference-app)
<br><br>



## Distributed Tracing Server Zipkin w/ Docker
https://hub.docker.com/r/openzipkin/zipkin <br>

General Idea: <br>
All the microservices involved would send all the information out to a single distributed tracing server. And this distributed tracing server would store everything to a database, and would provide a UI which we can query against, so we could find information about the requests which are executed. In a word, we could track the way how microservices are connected.<br>
Benefit of using docker for zipkin: <br>
Instead of creating a Java project for zipkin, we are launching it as a docker container. <br>

Try it out: <br>
1. Make sure that the **Docker Desktop** is running; <br>
2. Launching up the distributed tracing server **zipkin** using docker:
    ```sh
    docker run -p 9411:9411 openzipkin/zipkin:2.23  
    ```
3. Response for http://localhost:9411 looks like:
    ![alt text](img/zipkin1.png)

There are nothing shown(to be tracked) after you hit the "RUN QUERY" if microservices haven't got connected to Zipkin.

<br>


### Get microservices connect to zipkin
For Spring Boot 2: Sleuth(configuration) -> Brave(Tracer Lib) -> Zipkin

In our project, we use Spring Boot 3:
> Micrometer(metrics, logs & traces)<br>
> -> OpenTelemetry(metrics, logs & traces)<br>
> -> Zipkin

Add these below to each microservice you would like it to be connected to the zipkin:
```xml
<!-- In pom.xml -->
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-observation</artifactId>
</dependency>

<!-- Open Telemetry as Bridge -->
<!-- Open Telemetry - Simplified Observability (metrics, logs, and traces) -->

<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-tracing-bridge-otel</artifactId>
</dependency>

<dependency>
    <groupId>io.opentelemetry</groupId>
    <artifactId>opentelemetry-exporter-zipkin</artifactId>
</dependency>
```

```properties
# In .property files
management.tracing.sampling.probability=1.0
logging.pattern.level=%5p [${spring.application.name:},%X{traceId:-},%X{spanId:-}]
```

<br>

<a id="run-zipkin"></a>
Here is instruction of how to run zipkin: <br>
1. First thing first, in order to make the distributed tracing works, make sure that the **openzipkin** container is running. <br>
    Use command below to check:
    ```sh
    docker containler ls
    ```
    If there is nothing similar to this:
    ```sh
    CONTAINER ID   IMAGE                    COMMAND          CREATED        STATUS                                     PORTS                              NAMES
    1632f90b14d7   openzipkin/zipkin:2.23   "start-zipkin"   23 hours ago   Up Less than a second (health: starting)   9410/tcp, 0.0.0.0:9411->9411/tcp   docker-compose-zipkin-server-1
    ```
    Run:
    ```sh
    docker run -p 9411:9411 openzipkin/zipkin:2.23
    ```

2. Stop all applications which are running in the IDE; <br>
3. Launch up microservices you want to check (**Of course, they should be connected to the Zipkin already**); <br>
 For a caveat, if you want to test the currency exchange microservice, you need to launch up the naming server first.
1. Make a request; <br>
Eg. http://localhost:8000/currency-exchange/from/USD/to/INR if you are testing currency exchange service.
1. Go back to Zipkin and hit the "RUN QUERY" button; <br>
-> This is what it may look like
![alt text](img/zipkin2.png)



---
[🔼 Back to top](#spring-cloud-reference-app)
<br><br>



## Docker 
### Playing with Docker Images
```sh
docker images
docker pull image-name #gets latest
docker search image-name
docker image history in28min/hello-world-java:0.0.1.RELEASE
docker image history 100229ba687e
docker image inspect 100229ba687e
docker image remove image-name
sudo docker system prune -af #remove all the iamges
```
Reminder: <br>
"docker pull" command just downloads the image from the registry; <br>
**"docker run" checks if the image is available in the local, if it's not available in the local, then it pulls it and creates a container.**

---

### Playing with Docker Containers
```sh
docker run -p -d 5000:5000 in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
docker container rm 3e657ae9bd16
docker container ls -a
docker container pause 832
docker container unpause 832
docker container stop 832 #SIGTERM
docker container kill 832 #SIGKILL
docker container inspect ff521fa58db3
docker container prune

docker run -p -d 5000:5000 --restart=always in28min/todo-rest-api-h2:0.0.1-SNAPSHOT #automatically  starts after docker desktop is restarted
```

---

### Playing with Docker Commands - stats, system
```sh
docker events #track events - launch and stop containers
docker top 9009722eac4d
docker stats 
docker stats 9009722eac4d
docker system
docker system df
docker system info
docker system prune -a
docker container run -p 5000:5000 -d -m 512m in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
docker container run -p 5000:5000 -d -m 512m --cpu-quota=50000  in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
docker system events
```



---
[🔼 Back to top](#spring-cloud-reference-app)
<br><br>



## Docker Compose
https://docs.docker.com/compose <br>
Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services. Then, with a single command, you create and start all the services from your configuration.<br>

To make it work: <br>
1. Add this chunck of configuration code into the "plugin" section of the pom.xml of the microservice:
    ```xml
    <configuration>
        <image>
            <!--in28min: docker ID-->
            <!--mmv3: master microservices v3-->
            <!--${project.version}: tag of the image-->
            <name>in28min/mmv3-${project.artifactId}:${project.version}</name>
        </image>
        <pullPolicy>IF_NOT_PRESENT</pullPolicy>
    </configuration>
    ```
    "pullPolicy": <br>
    To create a Docker image, the 'spring-boot-maven-plugin' make use of a lot of other docker images. pullPolicy could potentially prevent the spring boot from fetching all the base images since it will check if those images are already present locally.

2. Get the image for the microservices ready: <br>
    Run:
    ```sh
    docker images
    ```
    To make sure you have all the images listed below on your local machine:

    ![alt text](img/required-images.png)

    If there is anything missing, follow the rest of step 2 to build the images. Otherwise, go to step 3. <br>

    > Example below is for **Intellij**.

    Make sure that the maven projects(of each microservices) have been loaded properly. <br>
    2.1. Click the "M"(Maven) tab in the right sidebar of the Intellij; <br>
    2.2. Pick the microservice that you want to build an image for; <br>
    2.3. Plugins -> spring-boot -> spring-boot:build-image; <br>
    ![alt text](img/image-build.png)

    Optional: <br>
    If you have the image of the currency-exchange microservice built already, you could do the quick test:
    ```sh
    # docker run -p 8000:8000 repository-name:image-tag
    docker run -p 8000:8000 in28min/mmv3-currency-exchange-service:0.0.1-SNAPSHOT
    ```
    And http://localhost:8000/currency-exchange/from/USD/to/INR should work.

3. Create "docker-compose.yaml" <br>
    Here is the snippet of it:
    ```yaml
    version: '3.7'
    services:
    currency-exchange:
        image: in28min/mmv3-currency-exchange-service:0.0.1-SNAPSHOT
        mem_reservation: 700m
        ports:
        - "8000:8000"
        networks:
        - currency-network

    networks:
    currency-network:
    ```
    [Complete .yaml file](docker-compose/docker-compose.yaml)

4. "Change directory"(cd) to .yaml file's location
5. Run it:
    ```sh
    docker-compose up 
    ```
    After a few minutes, all those urls should work except which access "currency-conversion" [🔼 Back to URLs](#url)

---
[🔼 Back to top](#spring-cloud-reference-app)
<br><br>
