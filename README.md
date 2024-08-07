# Spring Boot CRUD Application with Docker and MySQL

This project is a simple CRUD (Create, Read, Update, Delete) application built with Spring Boot and MySQL, running inside Docker containers.

## Prerequisites

- Docker and Docker Compose installed
- Java 8 or higher
- Maven or Gradle

## Project Structure

- `src/main/java/com/example/CurdProj`: Java source files
- `src/main/resources`: Application configuration files
- `Dockerfile`: Docker configuration for the Spring Boot application
- `docker-compose.yml`: Docker Compose configuration to set up MySQL and the Spring Boot application

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/CurdProj.git
cd CurdProj

### 2. Build the Project
Using Maven

### 3. Set Up Docker Containers

If Docker file is not using

docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=mydatabase -e MYSQL_USER=myuser -e MYSQL_PASSWORD=mypassword -p 3307:3306 -d mysql:latest

Create docker-compose.yml
Create a docker-compose.yml file in the root directory with the following content:

version: '3.1'

services:

  mysql:
    image: mysql:8.0
    container_name: mysql-container
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: mydatabase
      MYSQL_USER: myuser
      MYSQL_PASSWORD: mypassword
    ports:
      - "3307:3306"
    volumes:
      - mysql-data:/var/lib/mysql

  app:
    image: openjdk:8-jdk-alpine
    container_name: springboot-app
    restart: always
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://mysql:3306/mydatabase
      SPRING_DATASOURCE_USERNAME: myuser
      SPRING_DATASOURCE_PASSWORD: mypassword
    ports:
      - "8080:8080"
    depends_on:
      - mysql
    volumes:
      - .:/app
    working_dir: /app
    command: sh -c 'java -jar target/CurdProj-0.0.1-SNAPSHOT.jar'

volumes:
  mysql-data:

  
### 4. Start the Containers
	docker-compose up -d
	
	This command will start both the MySQL and Spring Boot application containers.

### 5. Verify the Setup
MySQL: The MySQL server should be running and accessible at localhost:3307.
Spring Boot Application: The application should be running and accessible at http://localhost:8080.

### 6. Check the Database
To check the MySQL database, you can use any MySQL client tool (e.g., MySQL Workbench, DBeaver, command-line client).

Using MySQL Command-Line Client
mysql -h 127.0.0.1 -P 3307 -u myuser -p

Then run:

sql
USE mydatabase;
SHOW TABLES;

Application Configuration
Ensure your application.properties or application.yml file is correctly configured:

spring.datasource.url=jdbc:mysql://localhost:3307/mydatabase
spring.datasource.username=myuser
spring.datasource.password=mypassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true


Troubleshooting
Ports Not Available: Ensure the ports 3307 and 8080 are not being used by other applications.
Database Not Selected Error: Ensure the database is selected before running any SQL queries.
Contributing
Feel free to submit issues and enhancement requests.
