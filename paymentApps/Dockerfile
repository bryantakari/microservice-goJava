# Step 1: Build the Spring Boot application
FROM maven:3.8.6-amazoncorretto-17 AS builder

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy the pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy the source code into the container
COPY src ./src

# Build the Spring Boot application
RUN mvn clean package -DskipTests

# Step 2: Create a minimal container to run the Spring Boot application
FROM openjdk:17-jdk-slim

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy the JAR file from the previous stage
COPY --from=builder /app/target/paymentApps-1.0.jar .

# Expose port 8080 to the outside world
EXPOSE 8080

# Command to run the executable JAR
CMD ["java", "-jar", "paymentApps-1.0.jar"]
