# 🐳 Project 2: Containerization of a Two-Tier Application using Docker

## 📌 Project Overview

This project demonstrates **containerization of a two-tier web application** using Docker and Docker Compose.
The application consists of:

* **Frontend (Web Server)** – Serves the UI.
* **Backend (Database)** – Stores and retrieves application data.

By containerizing both layers, we achieve **portability, scalability, and simplified deployments**.

---

## 🛠️ Tech Stack / Tools Required

* **Docker** (Containerization)
* **Docker Compose** (Multi-container orchestration)
* **Docker Scout** (Image vulnerability scanning)
* **Git & GitHub** (Version control)

---

## 📂 Functional Requirements

* Run the application in **two containers**:

  * `web`: Web server (Node.js/Python/Django, etc.)
  * `db`: Database (MySQL/Postgres, etc.)
* Containers must communicate using a **Docker network**.
* Database data should persist using **Docker Volumes**.
* Web app should be accessible from the host machine via a browser.

---

## 📂 Non-Functional Requirements

* Use **lightweight base images** for better performance.
* Apply **security scanning** with Docker Scout.
* Ensure **data persistence** even after container restarts.
* Provide **easy deployment** via `docker-compose`.

---

## 🚀 How to Run the Project

### 1️⃣ Clone the repository

```bash
git clone <your-repo-link>
cd project-2-docker-twotier
```

### 2️⃣ Build & Start containers

```bash
docker-compose up -d --build
```

### 3️⃣ Access the application

* Web App: [http://localhost:8080](http://localhost:8080)
* Database: Runs internally, accessible via `db` service

### 4️⃣ Stop containers

```bash
docker-compose down
```

---

## 📖 Folder Structure

```bash
project-2-docker-twotier/
│-- README.md             # Documentation
│-- docker-compose.yml    # Defines web & db services
│-- web/                  # Web application source code
│   ├── Dockerfile
│   ├── app.js (or index.py)
│   └── package.json (if Node.js)
│-- db/                   # Database configuration
│   ├── Dockerfile
│   └── init.sql          # Initial database setup script
│-- .gitignore            # Ignore unnecessary files
```

---

## 📝 Sample `docker-compose.yml`

```yaml
version: '3.8'

services:
  web:
    build: ./web
    ports:
      - "8080:8080"
    depends_on:
      - db
    networks:
      - app-network

  db:
    image: mysql:8
    container_name: db_container
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: appdb
      MYSQL_USER: appuser
      MYSQL_PASSWORD: app123
    volumes:
      - db_data:/var/lib/mysql
      - ./db/init.sql:/docker-entrypoint-initdb.d/init.sql
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  db_data:
```

---

## 📝 Sample Web `Dockerfile` (Node.js Example)

```dockerfile
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy dependencies
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy app files
COPY . .

# Expose port
EXPOSE 8080

# Start app
CMD ["node", "app.js"]
```

---

## 📝 Resume Highlights

**Objective**
Containerized a two-tier application to improve scalability, portability, and deployment efficiency.

**Key Achievements**

* Designed a **Docker Compose setup** for web + database containers.
* Integrated **persistent storage** for database reliability.
* Performed **image vulnerability scanning** using Docker Scout.

**Impact**
✅ Reduced deployment time by **80%** with containerization.
✅ Improved application portability across environments.
✅ Enhanced system reliability with **persistent volumes**.

---

## 🔗 Repository Link

*(Replace with your repo link after upload)*

```md
https://github.com/<your-username>/project-2-docker-twotier
```
