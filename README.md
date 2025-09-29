# web-breakages-taxonomy

## A Taxonomy of Test Case Breakages in the Web Application Domain

This repository contains the infrastructure of the thesis project **"A Taxonomy of Test Case Breakages in the Web Application Domain"**.  
It provides a **Spring Boot backend**, a **React frontend**, and a **MySQL database** that together form a web application for analyzing test case breakages in web applications.

---

## 📂 Project Structure

```
.
├── backend/ # Spring Boot backend application
├── frontend/ # React frontend application
└── database/ # MySQL database dump with all records
```

---

## ⚙️ Backend (Spring Boot)

- The backend is built with **Spring Boot** and exposes REST APIs consumed by the frontend.
- Configuration file: `application.properties`

### Key Properties

```properties
spring.application.name=Benchmark
server.port=8090

# MySQL datasource
spring.datasource.url=jdbc:mysql://localhost:3306/thesis?serverTimezone=UTC
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.username=root
spring.datasource.password=12345r

spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update

# Logging & file upload
logging.level.org.springframework.security=DEBUG
spring.servlet.multipart.enabled=true
spring.servlet.multipart.max-file-size=10MB
spring.servlet.multipart.max-request-size=10MB
```

### Running the Backend

```
cd backend
./mvnw spring-boot:run
```

The backend will start on:
👉 http://localhost:8090

## 🎨 Frontend (React)

- The frontend is located under the frontend/ folder.

- It is connected to the backend using a proxy configuration.

- Before running, make sure the backend is up.

### Running the Frontend

```
cd frontend
npm install
npm start
```

### Proxy Fix

Update the package.json file in frontend/ to ensure requests are correctly proxied to the backend:

```
"proxy": "http://localhost:8090"
```

## 🗄️ Database (MySQL)

A MySQL database dump is provided under the database/ folder.

Create a database named thesis and import the dump.

### Setup Example

```
mysql -u root -p
CREATE DATABASE thesis;
USE thesis;
SOURCE database/thesis_dump.sql;
```

Make sure the application.properties matches your database credentials.

## 🚀 Quick Start

Start MySQL and import the database/ dump.

Run the backend (Spring Boot) → http://localhost:8090

Run the frontend (React) → http://localhost:3000

The application should now be accessible via the frontend.

## 📊 Querying Results

The backend provides REST endpoints that return aggregated results used in the thesis tables:

- **Table 6.4: Test Case Breakage Cause Counts for Training vs Validation Projects**  
  👉 [http://localhost:8090/api/breakages/count-breakages-by-app](http://localhost:8090/api/breakages/count-breakages-by-app)

- **Table 6.3: Repair Counts and Percentages**  
  👉 [http://localhost:8090/api/repairs/explanation-stats-validation](http://localhost:8090/api/repairs/explanation-stats-validation)

- **Table 6.1: Test Case Breakage Error Outputs**  
  👉 [http://localhost:8090/api/breakages/count-reasons](http://localhost:8090/api/breakages/count-reasons)

- **Table 6.2: Locating Methods of "Unable to locate element" Errors**  
  👉 [http://localhost:8090/api/breakages/count-locating-methods](http://localhost:8090/api/breakages/count-locating-methods)
