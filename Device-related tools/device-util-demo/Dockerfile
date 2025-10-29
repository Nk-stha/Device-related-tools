# Stage 1: Build the application
FROM maven:3.8.5-openjdk-11 AS build
WORKDIR /app
COPY pom.xml .
COPY brezze-communication/pom.xml ./brezze-communication/
COPY utils-common/pom.xml ./utils-common/
COPY settings.xml .
COPY . .
RUN mvn clean install -DskipTests

# Stage 2: Create the final image
FROM eclipse-temurin:11-jre-focal
WORKDIR /app
COPY --from=build /app/brezze-communication/target/*.jar /app/app.jar
EXPOSE 10000
ENTRYPOINT ["java","-Dfastdfs.jmx.enable=false","-jar","/app/app.jar"]