# ---------- Build stage ----------
  FROM maven:3.9-eclipse-temurin-17 AS build

  # Inside the image, we work in /app
  WORKDIR /app
  
  # Copy Maven config and source code
  COPY pom.xml .
  COPY src ./src
  
  # Build the Spring Boot jar (skip tests for speed)
  RUN mvn -q -DskipTests package
  
  # ---------- Runtime stage ----------
  FROM eclipse-temurin:17-jre
  
  WORKDIR /app
  
  # Copy the jar built in the first stage
  COPY --from=build /app/target/*.jar app.jar
  
  # Spring Boot runs on 8080
  EXPOSE 8080
  
  # Start the app
  ENTRYPOINT ["java", "-jar", "/app/app.jar"]
  