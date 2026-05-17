# ========================================================
# ETAPA 1: Compilación del código Java (Builder)
# ========================================================
FROM maven:3.8.6-eclipse-temurin-17-alpine AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests -Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true

# ========================================================
# ETAPA 2: Entorno de ejecución ligero y seguro
# ========================================================
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# BUENA PRÁCTICA (Mínimo Privilegio): Usuario no-root
RUN addgroup -S spring && adduser -S spring -G spring
USER spring

# Copiamos el compilado
COPY --from=builder /app/target/*.jar app.jar

# TRUCO DE INGENIERÍA: Forzamos a Ventas a usar el puerto 8081
ENV SERVER_PORT=8081
EXPOSE 8081

CMD ["java", "-jar", "app.jar"]