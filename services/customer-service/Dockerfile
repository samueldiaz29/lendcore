# Etapa 1: construcción
FROM maven:3.9-eclipse-temurin-25 AS build

WORKDIR /workspace

# POM raíz y POM del microservicio
COPY pom.xml .
COPY services/customer-service/pom.xml services/customer-service/pom.xml

# Descargar dependencias
RUN mvn -f pom.xml -pl services/customer-service -am dependency:go-offline

# Copiar código fuente
COPY services/customer-service/src services/customer-service/src

# Construir el microservicio
RUN mvn -f pom.xml -pl services/customer-service -am -DskipTests package

# Etapa 2: ejecución
FROM eclipse-temurin:25-jre

WORKDIR /app

COPY --from=build /workspace/services/customer-service/target/customer-service-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8081

ENTRYPOINT ["java", "-jar", "app.jar"]
