#Dockerfile
```
# First stage: build the application
FROM maven:3.8.3-jdk-11 AS build
COPY . /app
WORKDIR /app
RUN mvn package -DskipTests

# Second stage: create a slim image
FROM openjdk:11-jre-slim
COPY --from=build /app/target/my-application.jar /app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

# docker-compose.yml
```
version: '3'
services:
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: my-secret-pw
      MYSQL_DATABASE: my-database
    volumes:
      - db_data:/var/lib/mysql
  web:
    build: .
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://db:3306/my-database
      SPRING_DATASOURCE_USERNAME: root
      SPRING_DATASOURCE_PASSWORD: my-secret-pw
volumes:
  db_data:
```

# Use environment variables
```
FROM openjdk:11
ENV SPRING_PROFILES_ACTIVE=production
COPY target/my-application.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```
# Proxy
```
version: '3'
services:
  web:
    build: .
    environment:
      SPRING_PROFILES_ACTIVE: production
    ports:
      - "8080:8080"
  proxy:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - web
```
