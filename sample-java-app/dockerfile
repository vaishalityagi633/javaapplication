# Stage 1: Build the application
FROM maven:3.8.5-eclipse-temurin-17 AS builder

WORKDIR /app

# Copy pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:resolve

# Copy source code and build the application
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Create a smaller runtime image
FROM eclipse-temurin:17-jre

WORKDIR /app
COPY --from=builder /app/target/demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
