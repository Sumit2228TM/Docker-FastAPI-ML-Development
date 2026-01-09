# 🐳 Docker Development with FastAPI (Live Reload)

This repository demonstrates **Docker-based development workflow** using **FastAPI**, focusing on **live reload**, **volume mounting**, and **developer productivity**.

🚫 This repo is intentionally **NOT about deployment or production**.  
✅ It focuses purely on **local development with Docker**.

---

## 🚀 What This Project Demonstrates

- ✅ Dockerizing a FastAPI application for development
- ✅ Live code reload using Docker (`--reload`)
- ✅ Volume mounting instead of rebuilding images
- ✅ Clear separation between **development** and **production**
- ✅ Understanding of Docker images vs containers

---

## 🧠 Why This Matters

In real-world projects:
- Rebuilding Docker images on every code change is **slow**
- Developers need **instant feedback**
- Docker should improve productivity, not slow it down

This setup solves that problem.

---

## 📁 Project Structure
```
.
├── app.py # FastAPI application
├── requirements.txt # Python dependencies
├── Dockerfile.dev # Development Dockerfile
├── .dockerignore # Ignore unnecessary files
└── README.md
```


---

## 🧩 Application Overview

### `app.py`
A minimal FastAPI app with:
- Root endpoint
- Health check
- Example API response

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def root():
    return {"message": "Docker Dev API is running 🚀"}

@app.get("/health")
def health():
    return {"status": "healthy"}
```
🐳 Dockerfile (Development)
Dockerfile.dev
```
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
```
Why this works well for development:
--reload → auto-restarts server on code changes

App code is not copied into the image

Code is mounted using Docker volumes

▶️ How to Run (Development Mode)
1️⃣ Build the image
```
docker build -f Dockerfile.dev -t fastapi-dev .
```
2️⃣ Run with volume mounting
```
docker run -d --name fastapi-dev -p 8000:8000 -v $(pwd):/app fastapi-dev
```
Any change to app.py will instantly reload the server 🚀
No rebuild required.

## 🌐 Access the App
API Root: http://localhost:8000/

Swagger UI: http://localhost:8000/docs

Health Check: http://localhost:8000/health

## 🧪 What I Learned from This Project
Difference between Docker images and containers

Why volume mounting is ideal for development

How FastAPI + Uvicorn reload works inside Docker

How to design Dockerfiles based on use-case

Why production Dockerfiles should be different

## ⚠️ Notes
This setup is for development only

Production deployments require:

No --reload

Code copied into image

Multiple workers

Proper security configs

(Handled in a separate project.)

## 🏁 Conclusion
Docker is not just for deployment.
When used correctly, it becomes a powerful development tool.
