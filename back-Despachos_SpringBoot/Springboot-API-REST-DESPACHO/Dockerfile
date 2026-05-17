# ========================================================
# ETAPA 1: Compilación del código Java (Builder)
# ========================================================
FROM maven:3.8.6-eclipse-temurin-17-alpine AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

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

# TRUCO DE INGENIERÍA: Forzamos a Despachos a usar el puerto 8082
ENV SERVER_PORT=8082
EXPOSE 8082

CMD ["java", "-jar", "app.jar"]