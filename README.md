# 📚 EduVault — Backend API

REST API for **EduVault**, a full-stack educational resource-sharing platform with role-based access for Students, Educators and Admins.

This repository is the **Spring Boot backend**. The React frontend lives in **[eduvault-frontend](https://github.com/MohammedSaif29/eduvault-frontend)** · 🔗 [Live demo](https://fsad-project-frontend-mu.vercel.app)

![Java](https://img.shields.io/badge/Java-17-ED8B00?logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.2-6DB33F?logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-JWT_%2B_OAuth2-6DB33F?logo=springsecurity&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white)
![Railway](https://img.shields.io/badge/Deployed_on-Railway-0B0D0E?logo=railway)

---

## ✨ Features

- **Authentication & authorization** — Spring Security with stateless **JWT**, a custom JWT filter, and **Google OAuth 2.0** login
- **Role-based access** — Student, Educator and Admin permissions
- **Resource management** — upload files, search and filter by category, approval workflow before resources go public
- **Engagement tracking** — views, downloads, saved resources and feedback per resource
- **Recommendations** — suggests resources to each student based on their download and viewing history
- **Analytics** — admin statistics, downloads trend, category stats, recent activity and dashboard overviews
- **Admin tools** — approve resources, manage users, change roles, delete content

## 🛠️ Tech Stack

Java · Spring Boot 3 · Spring Security · Spring Data JPA (Hibernate) · OAuth2 Client · JJWT · Bean Validation · MySQL · Maven · deployed on **Railway**

## 🏗️ Architecture

Layered design: **Controller → Service → Repository → Entity**, with DTOs for all request/response bodies.

```
controller/   Auth, Resource, Download, Student, Admin, Analytics, Recommendation, Activity, Health
service/      Business logic (13 services)
repository/   Spring Data JPA repositories
model/        User, Resource, Download, ResourceView, SavedResource, Feedback
dto/          Request / response objects
config/       SecurityConfig, JwtAuthenticationFilter, JwtUtil, OAuth2LoginSuccessHandler, WebConfig
```

## 🔌 Main API Endpoints

| Area | Endpoints |
|---|---|
| Auth | `POST /api/auth/register` · `POST /api/auth/login` · `GET /api/auth/me` · Google OAuth |
| Resources | `GET /api/resources/all` · `/search` · `/filter` · `GET /api/resources/{id}` · `POST /api/resources/upload` · `GET /api/resources/download/{id}` · `GET/POST /api/resources/{id}/feedback` |
| Students | `GET /api/student/dashboard/{userId}` · `POST /api/save/{resourceId}` · `POST /api/view/{resourceId}` · `GET /api/user/saved/{userId}` · `GET /api/user/activity/{userId}` |
| Recommendations | `GET /api/recommendations/{userId}` |
| Analytics | `GET /api/analytics/overview` · `GET /api/analytics/downloads` |
| Admin | `GET /api/admin/stats` · `/downloads-trend` · `/category-stats` · `/pending-resources` · `POST /api/admin/resources/{id}/approve` · `PUT /api/admin/users/{id}/role` · `DELETE /api/admin/users/{id}` |
| Health | `GET /api/health` |

## 🚀 Run Locally

**Requirements:** Java 17+, Maven, MySQL 8

```bash
# 1. Create your local config (keep secrets out of git)
cp backend-local.properties.example backend-local.properties   # add Google OAuth credentials

# 2. Set database and JWT environment variables
export SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/eduvault?createDatabaseIfNotExist=true
export SPRING_DATASOURCE_USERNAME=root
export SPRING_DATASOURCE_PASSWORD=your_password
export JWT_SECRET=a-long-random-secret

# 3. Run
mvn spring-boot:run
```

**Railway deployment:** build with `mvn clean package -DskipTests`, start with `java -Dserver.port=$PORT -jar target/*.jar`, and set the variables above plus `FRONTEND_URL`, `APP_CORS_ALLOWED_ORIGINS` and the Google OAuth credentials.

## 👤 Author

**Mohammed Saif** — B.Tech CSE
[LinkedIn](https://www.linkedin.com/in/saif-mohammed-939902335/) · [GitHub](https://github.com/MohammedSaif29)
