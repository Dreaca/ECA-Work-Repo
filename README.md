# Cloud Enabled Deployment In Action with AWS

This repository contains four projects:

- course-service (Spring Boot + MySQL)
- student-service (Spring Boot + MongoDB)
- media-service (Spring Boot + Local file storage, can be extended to S3/MinIO)
- frontend-app (React + TypeScript)

## Backend Services

### 1. course-service
- Entity: Course(id, name, duration)
- Endpoints:
  - GET /courses
  - GET /courses/{id}
  - POST /courses
  - DELETE /courses/{id}
- Default port: 8081
- Configure MySQL settings

### 2. student-service
- Document: Student(registrationNumber, fullName, address, contact, email)
- Endpoints:
  - GET /students
  - GET /students/{id}
  - POST /students
  - DELETE /students/{id}
- Default port: 8082
- Configure MongoDB settings

### 3. media-service
- Resource: files
- Endpoints:
  - POST /files (multipart/form-data: file)
  - GET /files (list)
  - GET /files/{id} (fetch)
  - DELETE /files/{id} (delete)
- Default port: 8083
- Uses local disk storage at `./data/media` by default (override with env var `MEDIA_STORAGE_DIR`).

## Frontend (frontend-app)
- React + TypeScript + MUI + Axios + Vite app with 3 sections: Courses, Students, Media
- Scripts:
  - npm run dev (Vite dev server)
  - npm run build (TypeScript build + Vite build)
  - npm run preview (Preview built app)

## Build

- Backend: run `mvn -q -e -DskipTests package` at repo root to build services.
- Frontend: run `npm install` then `npm run dev` inside `frontend-app`.

## Switching Environments (Spring Profiles)

- Each backend service can run in different environments using Spring profiles. The available profiles are:

  - dev – Local/Docker development

  - gcp – Google Cloud Platform

  - aws – AWS deployment

## How to set the active profile:

- Via application.properties (less flexible)

`spring.profiles.active=aws`


- Via command line (recommended)

- #### Run with AWS profile
`mvn spring-boot:run -Dspring-boot.run.profiles=aws`

- #### Run with GCP profile
`mvn spring-boot:run -Dspring-boot.run.profiles=gcp`

- #### Run with dev profile
`mvn spring-boot:run -Dspring-boot.run.profiles=dev`


- Via environment variable

`export SPRING_PROFILES_ACTIVE=aws
java -jar target/<service-name>.jar`


**Change the profile to aws, gcp, or dev depending on where you want the service to run. This applies to course-service, student-service, and media-service.**

## **Notes**

- Make sure to configure database credentials and endpoints in the respective `application-<profile>.properties`.

- For media-service, ensure the `MEDIA_STORAGE_DIR` exists or is writable if you override it.

- Frontend communicates with backend services on their respective ports (`8081–8083`). Update API URLs in `frontend-app/src/`config if needed.

## Additional

- GCP currently working on Public API to work it on your machine you will need to create a GCP SQL database then whitelist your public (Not the local ip) ip in the networking tab of your mysql instance.
- Sensitive info such as IP addresses and Passwords are removed from `application-<profile>.properties` files. Use your own.

## Video For the assignment

[Watch the Video](https://drive.google.com/file/d/1KPJCb7pRBHHsuUTaZo3M19D8YmF9uA6e/view?usp=drive_link)


## License

This project is licensed under the [MIT License](LICENSE).

## Details About the Assignee
- Name : W.P. Buddhika Pathum
- Reg. No. : 2301671076
- Email : buddhikadreaca@gmail.com
