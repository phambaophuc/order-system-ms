# Order System Microservices 🛒

A demo microservices project implementing an order system using Spring Boot, Spring Cloud, and Eureka for service discovery.

## Table of Contents 

- [Project Title & Badges](#order-system-microservices-)
- [Description](#description)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [License](#license)
- [Footer](#footer)

## Description 

This project demonstrates a microservices architecture for an order system. It comprises several independent services, including an API Gateway, Authentication Service, Eureka Server for service discovery, Order Service, Product Service, and Review Service. Each service is built with Spring Boot and designed to communicate with each other within a distributed system.

## Features 

- **Microservices Architecture**: Deploys multiple independent services for better scalability and maintainability. 🚀
- **Service Discovery**: Utilizes Spring Cloud Netflix Eureka for robust service registration and discovery. 🗺️
- **API Gateway**: Centralizes external requests and routes them to appropriate microservices. 🚪
- **Authentication Service**: Handles user authentication and authorization (implementation details not fully visible in provided files, but its presence indicates security measures). 🔐
- **Order Management**: Core service for managing orders. 📦
- **Product Management**: Service for managing product information. 🏷️
- **Review Service**: Handles product reviews (uses MongoDB as indicated by `spring-boot-starter-data-mongodb`). ⭐
- **Spring Boot**: Leverages Spring Boot for rapid application development and configuration. ⚙️
- **Spring Cloud**: Employs Spring Cloud for distributed system patterns like configuration management and service discovery. ☁️
- **Swagger UI**: Integrated for API documentation and exploration (e.g., `springdoc-openapi-starter-webmvc-ui`). 📄

## Tech Stack 

- **Languages**: Java 17
- **Frameworks**: Spring Boot (3.2.3), Spring Cloud (2023.0.0)
- **Databases**: MySQL (for Order and Product services), MongoDB (for Review service)
- **Service Discovery**: Eureka
- **API Gateway**: Spring Cloud Gateway
- **Build Tool**: Maven
- **Dependencies**: JWT (jjwt), Spring Data JPA, Spring Kafka, Spring Web, Spring Actuator, Springdoc OpenAPI, Lombok.

## Installation 

This project is a collection of Spring Boot microservices. To run it, you will need to have Java Development Kit (JDK) 17 or higher and Apache Maven installed.

### Prerequisites 

- **JDK 17+**: Ensure you have Java 17 or a later version installed.
- **Maven**: Apache Maven should be installed and configured in your system's PATH.

### Setting up the Services 

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/phambaophuc/order-system-ms.git
   cd order-system-ms
   ```

2. **Build Each Microservice**:
   Navigate to each microservice directory and build it using Maven. For example, for the Eureka Server:
   ```bash
   cd eureka-server
   mvn clean install
   cd ..
   ```
   Repeat this for `config-server`, `api-gateway`, `auth-service`, `order-service`, `product-service`, and `review-service`.

3. **Run the Services**:
   The services are typically run using their respective Maven Spring Boot plugins or by executing the generated JAR files.

   *   **Eureka Server**: Start this service first to enable service discovery.
       ```bash
       cd eureka-server
       mvn spring-boot:run
       ```
       Access the Eureka dashboard at `http://localhost:8761`.

   *   **Config Server**: Start the config server to manage externalized configurations.
       ```bash
       cd config-server
       mvn spring-boot:run
       ```

   *   **API Gateway**: This service routes requests to other microservices.
       ```bash
       cd api-gateway
       mvn spring-boot:run
       ```
       The API Gateway will likely expose endpoints for the other services.

   *   **Other Services (Auth, Order, Product, Review)**: Start these services in any order after Eureka and the Config Server are running.
       ```bash
       cd auth-service
       mvn spring-boot:run
       ```
       ```bash
       cd order-service
       mvn spring-boot:run
       ```
       ```bash
       cd product-service
       mvn spring-boot:run
       ```
       ```bash
       cd review-service
       mvn spring-boot:run
       ```

   **Note**: The exact ports for each service are determined by their Spring Boot configuration (e.g., `application.properties` or `application.yml`), which are not fully detailed in the provided analysis. The `docker-compose.yaml` file is present but its content was not provided, suggesting it might be used for orchestration but requires further setup.

## Usage 

This project is designed as a set of microservices that work together to form an order system. The primary interaction point is the **API Gateway**, which acts as the entry point for all client requests.

### Core Functionality 

- **Order Placement**: Users can place orders, which interact with the `order-service`.
- **Product Browsing**: Users can view products via the `product-service`.
- **Review Submission**: Users can submit reviews for products, managed by the `review-service`.
- **Authentication**: The `auth-service` handles user authentication, likely providing tokens for protected API access.

### How to Use 

1. **Ensure all microservices are running** as described in the Installation section, starting with Eureka Server and Config Server.
2. **Access the API Gateway**: Use your browser or an API client (like Postman) to interact with the endpoints exposed by the API Gateway. The base URL is typically `http://localhost:PORT` where `PORT` is the port configured for the API Gateway.
3. **Interact with Services**: The API Gateway will route your requests to the appropriate microservice based on the defined routes (likely configured in the API Gateway's application properties/YAML).

**Example Workflow (Conceptual):**

1. **User Login**: Authenticate via an endpoint on the API Gateway that forwards to the `auth-service`. You might receive a JWT token upon successful login.
2. **View Products**: Request product listings from the API Gateway, which forwards to `product-service`.
3. **Place an Order**: Send a POST request with order details to the API Gateway, which routes it to `order-service`. This might involve calls to `product-service` to verify product availability.
4. **Add a Review**: Submit a review via the API Gateway to `review-service`, potentially associating it with a specific order or product.

*Specific API endpoints and request/response formats would be detailed in the Swagger UI documentation for each service (accessible via their respective endpoints, e.g., `http://localhost:PORT/swagger-ui.html`).*

## Project Structure 

The project is organized into several microservices, each residing in its own directory:

```
order-system-ms/
├── api-gateway/
│   └── pom.xml
├── auth-service/
│   └── pom.xml
├── config-server/
│   ├── pom.xml
│   └── .mvn/
│       └── wrapper/
│           ├── maven-wrapper.jar
│           └── maven-wrapper.properties
├── eureka-server/
│   └── pom.xml
├── order-service/
│   └── pom.xml
├── product-service/
│   └── pom.xml
├── review-service/
│   └── pom.xml
├── docker-compose.yaml
├── .idea/
│   ├── ... (IDE specific files)
└── README.md
```

Each subdirectory (e.g., `api-gateway`, `order-service`) contains a Spring Boot application managed by Maven, defined by its `pom.xml` file.

## API Reference 

Detailed API documentation can be found by accessing the Swagger UI for each microservice. Once the services are running, you can typically find the UI at the following endpoints:

- **API Gateway**: (Endpoint not specified, but usually the main entry point)
- **Auth Service**: `http://localhost:<auth-port>/swagger-ui.html`
- **Order Service**: `http://localhost:<order-port>/swagger-ui.html`
- **Product Service**: `http://localhost:<product-port>/swagger-ui.html`
- **Review Service**: `http://localhost:<review-port>/swagger-ui.html`

*Note: The specific ports are not provided in the analysis and would need to be determined from the service's configuration files.*

## License 

This project is **not** currently under any specified license. Please refer to the repository owner for licensing details.

## Footer 

<p align="center">
  Developed with ❤️ by <a href="https://github.com/phambaophuc">phambaophuc</a>
</p>

--- 

✨ *Feel free to fork, star, and contribute to this project!* ✨
