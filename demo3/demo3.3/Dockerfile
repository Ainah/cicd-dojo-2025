# Step 1: Build the JAR using Maven (or Gradle) on OpenJDK 21
FROM maven:3.9.9-eclipse-temurin-21-alpine AS builder

WORKDIR /app

# Copy the pom.xml and the source code
COPY ./pom.xml .
COPY ./src ./src

# Build the JAR file (skip tests for faster builds)
RUN mvn clean package -DskipTests

 
# Step 2: Run the JAR file using OpenJDK 21
FROM openjdk:21-jdk-slim

WORKDIR /app


# Copy the built JAR file from the builder stage
COPY --from=builder /app/target/demo-0.0.1-SNAPSHOT.jar /app/app.jar

# Expose port 8080 (default Spring Boot port)
EXPOSE 8080

# Run the Spring Boot app
ENTRYPOINT ["java", "-jar", "app.jar"]
