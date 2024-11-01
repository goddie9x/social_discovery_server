# Discovery Server

The `Discovery Server` is a Spring Boot application configured as a Eureka Server for service discovery within a microservices social media. It uses Netflix Eureka for registry and service management, enabling microservices to discover each other.

To view all services for this social media system, lets visit: `https://github.com/goddie9x?tab=repositories&q=social`

## Prerequisites

- Java 17
- Maven
- Docker and Docker Compose

## Configuration

### Application Configuration

Create an `application.yml` file in `src/main/resources/` with the following configuration:

```yaml
spring:
  application:
    name: DiscoveryServer
server:
  port: 8761
eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
    wait-time-in-ms-when-sync-empty: 100
logging:
  level:
    com.netflix.eureka: DEBUG
    com.netflix.discovery: DEBUG
```

This configuration sets up Eureka server properties and enables debug logging for Eureka.

## Running the Application Locally

To run the Discovery Server locally:

1. Build the project using Maven:

   ```bash
   mvn clean install
   ```

2. Start the application:

   ```bash
   mvn spring-boot:run
   ```

The Discovery Server will be accessible at `http://localhost:8761`.

## Running with Docker

1. **Dockerfile**:

   Create a `Dockerfile` in the project root with the following content:

   ```dockerfile
   FROM openjdk:17
   ARG JAR_FILE=target/*jar
   COPY ${JAR_FILE} app.jar
   ENTRYPOINT ["java","-jar","/app.jar"]
   EXPOSE 8761
   ```

2. **Build and Run the Docker Container**:

   To build and start the Discovery Server in Docker:

   ```bash
   # Build the JAR file
   mvn clean package
   
   # Build the Docker image
   docker build -t discovery-server .
   
   # Run the Docker container
   docker run -p 8761:8761 discovery-server
   ```

## Running with Docker Compose

To run the Discovery Server within a Docker Compose setup, include the following service definition in your `docker-compose.yml`:

```yaml
discovery-server:
  image: discovery-server
  build:
    context: .
  ports:
    - 8761:8761
  networks:
    - social-media-network
```

Start all services with Docker Compose:

```bash
docker-compose up --build
```

## Accessing the Server

Once running, the Discovery Server will be available at `http://localhost:8761`.

### Useful Commands

- **Stop Containers**: Use `docker-compose down` to stop all services and remove the containers.
- **Restart Containers**: Run `docker-compose restart` to restart the services without rebuilding the images.

This setup enables seamless orchestration of the social media microservices with an API Gateway for managing external client requests.

## Contributing

Contributions are welcome. Please clone this repository and submit a pull request with your changes. Ensure that your changes are well-tested and documented.

## License

This project is licensed under the MIT License. See `LICENSE` for more details.

