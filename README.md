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


# Important URLs

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

# Spring Cloud Config Server

