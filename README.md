# 🐳 Dockerized ML API – FastAPI Development Setup

This repository demonstrates a **Docker-based development workflow** for a **Machine Learning API** built using **FastAPI** and **scikit-learn**.

The focus of this project is **local development with Docker**, not production deployment.

---

## 🚀 What This Project Does

- Serves a simple **Linear Regression model** via a FastAPI backend
- Uses **Docker for development**, not deployment
- Enables **live reload** without rebuilding images
- Demonstrates clean separation between **ML logic** and **Docker workflow**

---

## 🧠 ML Overview (Simple by Design)

The API loads a pre-trained **Linear Regression** model at startup:

- Input: single numeric value
- Output: predicted value (`y = 2x`)
- Purpose: demonstrate ML inference inside a Dockerized API

This keeps the ML logic simple so the focus remains on **Docker development practices**.

---

## 📁 Project Structure
```
docker-fastapi-ml-dev/
├── app.py # FastAPI app with ML model
├── requirements.txt # Python dependencies
├── Dockerfile.dev # Dockerfile for development
├── .dockerignore # Excludes unnecessary files
└── README.md
```


---

## 🧩 API Endpoints

| Method | Endpoint | Description |
|------|---------|-------------|
| GET | `/` | API status |
| GET | `/health` | Health check |
| POST | `/predict` | ML prediction |
| GET | `/info` | Model metadata |

---

## 🐳 Docker Development Setup

### `Dockerfile.dev`

```dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
```
Why this works well for development:
--reload enables live code updates

Application code is not copied into the image

Code is mounted using Docker volumes

No rebuild required on code changes

## ▶️ How to Run the Project

1️⃣ Build the Docker image
```
docker build -f Dockerfile.dev -t ml-api-dev .
```
2️⃣ Run with volume mounting
```
docker run -d --name ml-api-dev -p 8000:8000 -v $(pwd):/app ml-api-dev
```

## 🌐 Access the API
Swagger UI: http://localhost:8000/docs

Health check: http://localhost:8000/health

Any change to app.py will auto-reload the server 🚀

## 🧪 What This Project Demonstrates
Docker images vs containers
Volume mounting for fast ML development
Live reload inside Docker
FastAPI-based ML inference
Practical Docker usage for ML engineers

## ⚠️ Notes
This setup is for development only
Production deployment requires:
No --reload
Code copied into image
Multiple workers
Security hardening
(Handled in a separate project.)

🏁 Final Thoughts
Docker is not just a deployment tool.
Used correctly, it becomes a powerful environment for ML API development.
