# ---------- Build Stage ----------
FROM maven:3.9.6-eclipse-temurin-17 AS build

WORKDIR /build

# Copy pom and download dependencies (cache layer)
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy source code and build
COPY src ./src
RUN mvn clean package -DskipTests


# ---------- Runtime Stage ----------
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

# Copy only the built JAR from build stage
COPY --from=build /build/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]

