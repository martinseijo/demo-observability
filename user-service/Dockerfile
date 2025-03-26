FROM maven:3.9.9-eclipse-temurin-21 AS builder
WORKDIR /app

# Copy the POM and source code
COPY pom.xml /app/pom.xml
COPY user-service/pom.xml /app/user-service/pom.xml
COPY user-service/src /app/user-service/src

# Build the user-service module
WORKDIR /app/user-service
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre
WORKDIR /app
COPY --from=builder /app/user-service/target/user-service-1.0.0.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]