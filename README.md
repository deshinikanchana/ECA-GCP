# Cloud Enabled Deployment In Action with AWS & GCP

This repository demonstrates a cloud-enabled full-stack application deployed across multiple environments.  
It contains four services:

- **course-service** (Spring Boot + MySQL)
- **student-service** (Spring Boot + MongoDB)
- **media-service** (Spring Boot + Local file storage, can be extended to S3/MinIO)
- **frontend-app** (React + TypeScript)

---

## 🔹 Backend Services

### 1. course-service
- **Entity**: `Course(id, name, duration)`
- **Endpoints**:
  - `GET /courses`
  - `GET /courses/{id}`
  - `POST /courses`
  - `DELETE /courses/{id}`
- **Default port**: `8081`
- **Database**: MySQL (configurable for AWS or GCP)


#### Environment Configuration
The `course-service` supports multiple environments:
- `application-aws.properties` → AWS MySQL RDS configuration
- `application-gcp.properties` → GCP Cloud SQL configuration
- `application-dev.properties` → Local development configuration


To switch environments, update `spring.profiles.active` in `application.properties`:
  
```properties
    spring.profiles.active=aws   # for AWS RDS
    spring.profiles.active=gcp   # for GCP Cloud SQL
    spring.profiles.active=dev   # for local development
```
---

### 2. student-service
- Entity: `Student(registrationNumber, fullName, address, contact, email)`
- Endpoints:
  - `GET /students`
  - `GET /students/{id}`
  - `POST /students`
  - `DELETE /students/{id}`
- Default port: `8082`
- Configure MongoDB settings

---

### 3. media-service
- Resource: `files`
- Endpoints:
  - `POST /files (multipart/form-data: file)`
  - `GET /files (list)`
  - `GET /files/{id} (fetch)`
  - `DELETE /files/{id} (delete)`
- Default port: `8083`
- Uses local disk storage at `./data/media` by default (override with env var `MEDIA_STORAGE_DIR`).

---

## 🔹 Frontend (frontend-app)
- **Stack:** React + TypeScript + MUI + Axios + Vite
- **Sections:** 
  - Courses
  - Students
  - Media
  

- Scripts:
  ```bash
    npm install      # install dependencies
    npm run dev      # start Vite dev server
    npm run build    # build for production
    npm run preview  # preview the production build
  ```
  
---

## 🚀 Running the Project


**1. Clone the repository**
```bash
git clone https://github.com/deshinikanchana/ECA-GCP.git
```
**2. Build backend services**
  ```bash
  mvn -q -e -DskipTests package
```
**3. Run backend services**

 - Each Spring Boot service can be started individually:
  ```bash
  cd course-service
mvn spring-boot:run
```
**4. Configure database environment (for course-service)**

- Open `course-service/src/main/resources/application.properties`
Set the active profile:
 ```properties
 spring.profiles.active=aws   # or gcp / dev
```

- This automatically loads the corresponding configuration file:

    - `application-aws.properties` → AWS RDS
    
    - `application-gcp.properties` → GCP Cloud SQL
    
    - `application-dev.properties` → local MySQL instance


**5. Run frontend**
  ```bash
  cd frontend-app
npm install
npm run dev
```
- Frontend will start on `http://localhost:3000`

---

## 🎥 Demo Video
**A walkthrough of this project is available here:**
[Watch Demo](https://drive.google.com/file/d/1nMe5sv5NGdfBVDdwzFlkhUzJOM3Bs9ok/view?usp=sharing)

---

## ⚡ Tech Stack

- **Backend :** Spring Boot, Maven

- **Databases :** MySQL (AWS/GCP), MongoDB

- **Frontend :** React, TypeScript, Vite, MUI

- **Storage :** Local disk (extendable to S3/MinIO)

- **Cloud Providers :** AWS RDS, GCP Cloud SQL
