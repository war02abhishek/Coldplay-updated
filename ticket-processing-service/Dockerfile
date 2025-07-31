# ---------- Stage 1: Build the JAR ----------
FROM openjdk:11-jdk-slim AS builder

WORKDIR /app

COPY gradlew .
COPY gradle gradle
COPY build.gradle .
COPY settings.gradle .
COPY src src

RUN chmod +x gradlew && ./gradlew build -x test

# ---------- Stage 2: Copy only the JAR ----------
FROM openjdk:11-jdk-slim

WORKDIR /app

COPY --from=builder /app/build/libs/ticket-processing-service-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8082

ENTRYPOINT ["java", "-jar", "app.jar"]
