FROM maven:3.9.9-eclipse-temurin-21 AS builder
WORKDIR /app

# Copy the POM and source code
COPY pom.xml /app/pom.xml
COPY order-service/pom.xml /app/order-service/pom.xml
COPY order-service/src /app/order-service/src

# Build the order-service module
WORKDIR /app/order-service
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre
WORKDIR /app
COPY --from=builder /app/order-service/target/order-service-1.0.0.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]