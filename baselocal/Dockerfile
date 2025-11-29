# Etapa 1: Build (compilación con Maven)
FROM maven:3.9.6-eclipse-temurin-21 AS build

WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests  # Compila el JAR, salta tests para rapidez

# Etapa 2: Runtime (imagen ligera para ejecución)
FROM eclipse-temurin:21-jre-alpine

WORKDIR /app
COPY --from=build /app/target/*.jar app.jar  

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]