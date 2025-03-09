# Uses the Maven image with JDK 11 - slim tag to build the project.
FROM maven:3.6.3-jdk-11-slim AS build

# Creates a directory for the workspace.
RUN mkdir -p /workspace

# Sets the working directory.
WORKDIR /workspace

# Copies the Maven project file from /workspace.
COPY pom.xml /workspace

# Copies the source code from /workspace/src
COPY src /workspace/src

# Builds the project (skip tests).
RUN mvn -B -f pom.xml clean package -DskipTests

# Uses the OpenJDK image to run the application.
FROM openjdk:11-jdk-slim

# Copies the built JAR file from the build stage.
COPY --from=build /workspace/target/*.jar app.jar

# Exposes port 8080.
EXPOSE 8080

# Sets the entry point to run the JAR file.
ENTRYPOINT ["java", "-jar","app.jar"]


