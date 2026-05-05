# Dockerfile para microservicios Spring Boot
# Copiar este archivo en la raíz de CADA microservicio como "Dockerfile"

FROM maven:3.9.6-eclipse-temurin-21 AS builder
WORKDIR /app

# Copia el pom primero para cachear dependencias
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copia el código fuente y compila
COPY src ./src
RUN mvn clean package -DskipTests

# Imagen final liviana
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]