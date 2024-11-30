# Use the official Maven image as the base image
FROM maven:3.8.7-openjdk-18 AS build

# Set the working directory
WORKDIR /app

# Copy the pom.xml and any other necessary configuration files
COPY ./pom.xml /app
COPY ./src /app/src

# Build the application
RUN mvn clean package -Dmaven.test.skip=true

# Create a new image for running the application
FROM openjdk:18-jdk

# Set the working directory
WORKDIR /app

# Copy the built JAR file from the previous stage
COPY --from=build /app/target/*.jar app.jar

ENV SPRING_DATASOURCE_URL=jdbc:mysql://mysql:3306/product
ENV SPRING_DATASOURCE_USERNAME=product_user
ENV SPRING_DATASOURCE_PASSWORD=product_user_password

# Expose the port on which the Spring Boot application will run
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "app.jar"]