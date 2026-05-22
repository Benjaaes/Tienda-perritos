# ETAPA 1: Construcción (Maven)
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
# Descarga las dependencias de internet
RUN mvn dependency:go-offline
COPY src ./src
# Compila el código ignorando los tests para que sea más rápido
RUN mvn clean package -DskipTests

# ETAPA 2: Ejecución (Ligera y Segura)
FROM openjdk:17-jdk-slim
WORKDIR /app

# CREAR USUARIO NO ROOT (Principio de mínimo privilegio - Exigencia del profesor)
RUN useradd -m miusuarioapp
USER miusuarioapp

# Copiamos el archivo .jar generado en la Etapa 1
COPY --from=build /app/target/*.jar app.jar

EXPOSE 3001
# Comando para iniciar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]
