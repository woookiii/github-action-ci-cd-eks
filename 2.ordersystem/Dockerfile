# # 필요프로그램 설치
# FROM openjdk:17-jdk-slim AS stage1
# WORKDIR /app
# #make dir in docker's linux env
# #copy and paste all the neccessary files and folders
# COPY gradle gradle
# COPY src src
# COPY build.gradle .
# COPY settings.gradle .
# COPY gradlew .
# #give the authority to execute gradlew
# RUN chmod +x gradlew
# RUN ./gradlew bootJar

# # 두번째 스테이지 we exclude all source files from stage 1 except .jar file
# FROM openjdk:17-jdk-slim
# WORKDIR /app
# COPY --from=stage1 /app/build/libs/*.jar app.jar

# # to execute image to container this cmd is java -jar app.jar  comma is spacebar
# ENTRYPOINT ["java", "-jar", "app.jar"]

# FROM openjdk:17-jdk-slim
# WORKDIR /app
# COPY build/libs/*.jar app.jar
# ENTRYPOINT ["java", "-jar", "app.jar"]

# Stage 1: Build the JAR
FROM openjdk:17-jdk-slim AS build
WORKDIR /app
COPY gradle gradle
COPY src src
COPY build.gradle .
COPY settings.gradle .
COPY gradlew .
RUN chmod +x gradlew
RUN ./gradlew bootJar

# Stage 2: Run the JAR
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY --from=build /app/build/libs/*.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]