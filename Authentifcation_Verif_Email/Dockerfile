# Étape de build
FROM eclipse-temurin:17-jdk AS build
WORKDIR /app
COPY .mvn/ .mvn
COPY mvnw pom.xml ./
COPY src ./src 

RUN chmod +x mvnw
RUN ./mvnw -B package    

# Étape d'exécution
FROM eclipse-temurin:17-jre AS runtime
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
