# Etapa 1: construir o JAR (compilação)
FROM maven:3.9.6-eclipse-temurin-17 AS builder
WORKDIR /app

# Copia o POM e baixa dependências primeiro (para aproveitar cache)
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copia o restante do código e compila o projeto
COPY src ./src
RUN mvn clean package -DskipTests

# Etapa 2: rodar o JAR gerado
FROM eclipse-temurin:17-jdk
WORKDIR /app

# Copia o JAR do estágio de build
COPY --from=builder /app/target/sistema-moeda-backend-1.0.0.jar app.jar

# Expõe a porta padrão do Spring Boot
EXPOSE 8080

ENV SPRING_DATASOURCE_URL=jdbc:postgresql://dpg-d4kacvvgi27c73ckkgvg-a.oregon-postgres.render.com:5432/sistema_moeda_banco
ENV SPRING_DATASOURCE_USERNAME=senhorjesus
ENV SPRING_DATASOURCE_PASSWORD=hPv9rXigYPyJkq2CPawhN4EzXIrpZvyS

ENTRYPOINT ["java", "-jar", "app.jar"]
