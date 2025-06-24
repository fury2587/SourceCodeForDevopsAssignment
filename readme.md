# 🧪 DevOps Intern Assignment: Nginx Reverse Proxy + Docker

## Overview

This project demonstrates a simple microservices setup using Docker Compose, with two backend services and an Nginx reverse proxy. All services run in Docker containers and communicate over a custom bridge network.

---

## 📦 Tech Stack

- **service_1:** Go HTTP server (listens on port 8001)
- **service_2:** Python Flask API (listens on port 8002)
- **nginx:** Reverse proxy (routes `/service1` and `/service2`)

---

## 📁 Project Structure

```
.
├── docker-compose.yml
├── nginx
│   ├── default.conf
│   └── Dockerfile
├── service_1
│   ├── main.go
│   ├── go.mod
│   └── Dockerfile
├── service_2
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
└── README.md
```

---

## 🚀 Setup Instructions

1. **Clone the repository:**
   ```bash
   git clone < repo link>
   cd <project-directory>
   ```

2. **Build and start all services:**
   ```bash
   docker-compose up --build
   ```

   This will:
   - Build and run both backend services and Nginx in containers
   - Use bridge networking (no host networking)
   - Wait for both services to be healthy before starting Nginx

3. **Access the services via Nginx:**
   - [http://localhost:8080/service1/ping](http://localhost:8080/service1/ping)
   - [http://localhost:8080/service2/ping](http://localhost:8080/service2/ping)
   - [http://localhost:8080/service1/hello](http://localhost:8080/service1/hello)
   - [http://localhost:8080/service2/hello](http://localhost:8080/service2/hello)
   - [http://localhost:8080/health](http://localhost:8080/health) (Nginx health endpoint)

---

## 🔀 How Routing Works

- **Nginx** listens on port 80 (exposed as 8080 on the host).
- Requests to `/service1/*` are proxied to `service_1` (Go) on port 8001.
- Requests to `/service2/*` are proxied to `service_2` (Flask) on port 8002.
- Nginx logs all incoming requests with timestamp and path.

---

## ✅ Health Checks

- Both backend services expose a `/ping` endpoint returning JSON:
  - `service_1`: `{"status": "ok", "service": "1"}`
  - `service_2`: `{"status": "ok", "service": "2"}`
- Docker Compose healthchecks ensure services are healthy before Nginx starts routing.
- Nginx exposes `/health` for its own health status.

---

## 📝 Example Responses

- **GET `/service1/ping`**  
  `{"status": "ok", "service": "1"}`
- **GET `/service2/ping`**  
  `{"status": "ok", "service": "2"}`
- **GET `/service1/hello`**  
  `{"message": "Hello from Service 1"}`
- **GET `/service2/hello`**  
  `{"message": "Hello from Service 2"}`

---

## 🛠️ Bonus Features

- Health checks for both backend services and Nginx
- Custom Nginx access logs with timestamp and path
- Clean, modular Docker setup for each service

---

## 📦 Tech Constraints

- **Nginx runs in a Docker container, not on host**
- **All services use bridge networking (no host networking)**

---
