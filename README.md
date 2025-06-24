# 🧊 Apache Iceberg Local Setup

This repo accompanies the blog post:  
**[Getting Started with Apache Iceberg: Local Setup with MinIO, PyIceberg, and REST Catalog](https://medium.com/@ijaniszewski/getting-started-with-apache-iceberg-local-setup-with-minio-pyiceberg-and-rest-catalog-7a2428c54e6e)**  
> A hands-on guide to running Apache Iceberg locally using Docker, MinIO (S3-compatible), PyIceberg, and the Iceberg REST catalog.

---

## 📦 What’s Included

- **MinIO**: Acts as an S3-compatible object store (for Iceberg warehouse storage)
- **Iceberg REST Catalog**: Lightweight REST-based catalog server
- **PyIceberg**: Python client for interacting with Iceberg tables
- **Jupyter Notebooks**: For querying and exploring Iceberg tables using PyIceberg
- **Docker Compose**: Spins up everything in one command

---

## 🚀 Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/ijaniszewski/iceberg-local-setup
cd iceberg-local-setup
```

### 2. Copy .env.example

```bash
cp .env.example .env
```

### 3. Start the services

```bash
docker-compose up --build
```

This will start:
- **MinIO** (9000 for API, 9001 for console)
- **REST Catalog** (8181)
- **PyIceberg environment** (8888)

---

## 🌐 Access Points

| Service         | URL                    |
|-----------------|------------------------|
| MinIO Console   | http://localhost:9001  |
| Iceberg REST API| http://localhost:8181  |
| Jupyter Notebook| http://localhost:8888  |

---

## 📝 Example Usage

Jupyter notebooks are located in the `/notebooks` directory.

Inside, you can:
- Create Iceberg tables
- List tables
- Read/write data
- Interact with the REST catalog using PyIceberg

---

## 🔐 Credentials

All services use the following credentials (defined in `.env`):

```env
AWS_ACCESS_KEY_ID=admin
AWS_SECRET_ACCESS_KEY=password
AWS_REGION=us-east-1
```
⚠️ Note: 
>These credentials are hardcoded for simplicity and educational use in this local setup.
Do not use them in production environments. Always manage secrets securely using environment-specific .env files, secret managers, or CI/CD tools.

---

## 📁 Directory Structure

```bash
.
├── docker-compose.yml
├── pyiceberg/
│   └── Dockerfile
├── notebooks/
│   └── intro-to-iceberg.ipynb
├── .env
└── README.md

```

---

## 🧰 Requirements

- Docker
- Docker Compose
- Git

---

**Happy Iceberging! 🧊**
