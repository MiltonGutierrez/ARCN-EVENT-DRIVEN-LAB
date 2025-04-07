### ARCN - Arquitectura centrada en el negocio

#  Taller Event Driven

Este laboratorio muestra el desarrollo  de los pasos necesarios para crear los servicios de consumidor y productor mediante una sencilla API REST y utilizando el Broker RABBITMQ.

## Desarrollo del laboratorio

### Creación de contenedores Docker

- **PRODUCER**
```dockerfile
# producer-service/Dockerfile
# Usa una imagen base de JRE ligera que coincida con tu JDK de compilación
FROM openjdk:17-jdk-slim

# Argumento para el JAR (se pasa durante la construcción en docker-compose)
ARG JAR_FILE=target/*.jar

# Establece el directorio de trabajo
WORKDIR /app

# Copia el JAR construido a la imagen
COPY ${JAR_FILE} app.jar

# Expone el puerto de la aplicación
EXPOSE 8080

# Comando para ejecutar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]
```
![image](https://github.com/user-attachments/assets/8261d3e6-1702-4f76-9537-ac784249311c)
![image](https://github.com/user-attachments/assets/9a6b0cfd-e4b4-4eac-a0ee-cbd8141f0ceb)
![image](https://github.com/user-attachments/assets/8f97030e-7483-4b85-a199-f2b74c9bf02f)

- **CONSUMER**
```dockerfile
# consumer-service/Dockerfile
# Usa una imagen base de JRE ligera
FROM eclipse-temurin:17-jre-jammy

# Argumento para el JAR
ARG JAR_FILE=target/*.jar

# Directorio de trabajo
WORKDIR /app

# Copia el JAR
COPY ${JAR_FILE} app.jar

# No necesita exponer puerto si solo consume mensajes
# EXPOSE 8081

# Comando de ejecución
ENTRYPOINT ["java", "-jar", "app.jar"]
```
![image](https://github.com/user-attachments/assets/c7f3f04d-fdcd-4e6f-929d-92af86ee2b57)
![image](https://github.com/user-attachments/assets/068f62eb-70c2-42a3-8e40-5a333eee037a)
![image](https://github.com/user-attachments/assets/b14762e6-0477-4d59-89e3-4bd184d38d2c)

### Despliegue con Play with docker
