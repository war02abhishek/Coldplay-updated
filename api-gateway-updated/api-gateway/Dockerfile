FROM openjdk:11-jdk-slim

WORKDIR /app

# Copy Gradle files separately to leverage Docker layer caching
COPY gradlew .
COPY gradle gradle
COPY build.gradle .
COPY settings.gradle .
COPY src src

# Build the project (skip tests)
RUN chmod +x gradlew && ./gradlew build -x test

# Copy the built JAR (after building)
COPY build/libs/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
