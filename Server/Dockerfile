# Stage 1: Build stage
FROM maven:3.8.4-openjdk-8 AS build

# Set the working directory
WORKDIR /app

# Copy the Maven project files
COPY pom.xml .

# Copy the source code
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests

# Stage 2: Runtime stage
FROM openjdk:17-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the built JAR file from the build stage
COPY --from=build /app/target/*.jar ./application.jar

# Expose the application port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "application.jar"]
