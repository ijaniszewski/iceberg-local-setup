# 🧊 Apache Iceberg Local Setup

This repo accompanies the blog post:  
**[Getting Started with Apache Iceberg: Local Setup with MinIO, PyIceberg, and REST Catalog](https://medium.com/@ijaniszewski/getting-started-with-apache-iceberg-local-setup-with-minio-pyiceberg-and-rest-catalog-7a2428c54e6e)**  

> A hands-on guide to building a local Lakehouse using Apache Iceberg — without Spark or cloud infrastructure.

---

---

## 📦 What’s Inside?

| Component                | Purpose                                                                  |
|--------------------------|--------------------------------------------------------------------------|
| **MinIO**                | Local S3-compatible object store for data & metadata                     |
| **Iceberg REST Catalog** | Lightweight catalog service to manage Iceberg tables                     |
| **PyIceberg**            | Official Python client for creating & querying Iceberg tables            |
| **StarRocks**            | Fast, SQL-based MPP engine to query and explore Iceberg tables           |
| **Jupyter Notebooks**    | Explore and manipulate data using PyIceberg interactively                |
| **Docker Compose**       | One command to run the whole stack locally                               |

---

## 🚀 Quickstart Guide

Follow these steps to spin up the full stack locally:

### 1. Clone the Repository

```bash
git clone https://github.com/ijaniszewski/iceberg-local-setup
cd iceberg-local-setup
```

### 2. Configure Environment

```bash
cp .env.example .env
```

This `.env` file includes default values for MinIO credentials and endpoints.

### 3. Start the Stack

```bash
docker compose up --build
```

This will start:
- 🪣 **MinIO** at `http://localhost:9001`  
- 🧠 **Iceberg REST Catalog** at `http://localhost:8181`  
- 📓 **JupyterLab** at `http://localhost:8888` (no login required)

---

## 🌐 Access Points

| Service            | URL                     | Notes                         |
|--------------------|-------------------------|-------------------------------|
| MinIO Console      | http://localhost:9001   | Login: `admin` / `password`   |
| Iceberg REST API   | http://localhost:8181   | Used by PyIceberg & StarRocks |
| Jupyter Notebooks  | http://localhost:8888   | Contains example notebooks    |

---

## 🛠 Connecting to StarRocks

If you're running the optional **StarRocks** SQL engine (via `docker-compose.override.yml`), you can connect to it in two ways:

### 🔗 From the CLI (inside the container)

```bash
docker exec -it starrocks-fe   mysql -P 9030 -h 127.0.0.1 -u root --prompt="StarRocks > "
```

Then test the connection:

```sql
SELECT 1;
```

You should see:

```
+---+
| 1 |
+---+
| 1 |
+---+
```

### 🧪 From Python (Jupyter notebook)

You can also run SQL queries from inside a notebook using `mysql-connector-python`:

```python
import mysql.connector

conn = mysql.connector.connect(
    host="starrocks-fe",
    port=9030,
    user="root",
    password=""
)

cursor = conn.cursor()
cursor.execute("SELECT 1;")
print(cursor.fetchall())
cursor.close()
conn.close()
```

This is helpful when writing end-to-end workflows that combine **PyIceberg for data writing** and **StarRocks for SQL analytics** — all from the same Jupyter environment.

---


## 📒 What You Can Do

Once running, open the notebook:  
📁 `notebooks/intro-to-iceberg.ipynb`

You’ll learn how to:
- ✅ Create an Iceberg table from Python
- 📥 Append data using Pandas + PyArrow
- 🧠 Query metadata (snapshots, schema, partitions)
- 🕰 Time travel to previous versions
- 🔄 Apply schema evolution (e.g. add `tip_amount`)
- 💬 Connect and query using **StarRocks SQL**

---

## 🔐 Credentials (for local dev)

```env
AWS_ACCESS_KEY_ID=admin
AWS_SECRET_ACCESS_KEY=password
AWS_REGION=us-east-1
```

> ⚠️ **Do not use in production.** These are fixed local credentials for educational use only.

---

## 📁 Directory Layout

```bash
.
├── docker-compose.yml             # Base stack (MinIO, REST, PyIceberg)
├── docker-compose.override.yml   # Optional: StarRocks (SQL engine)
├── pyiceberg/                     # Custom PyIceberg image + Dockerfile
├── notebooks/                     # Jupyter notebooks for interactive work
│   └── intro-to-iceberg.ipynb
├── .env                           # Local environment config
└── README.md
```

---

## 🧰 Requirements

Make sure you have:
- 🐳 [Docker](https://www.docker.com/)
- 🧱 [Docker Compose](https://docs.docker.com/compose/)
- 🧬 [Git](https://git-scm.com/)

---

## 🎯 Next Steps

- Experiment with schema evolution & time travel  
- Add your own tables and simulate real data  
- Try connecting StarRocks, Flink, or Trino  
- Stay tuned for the [Delta Lake + Polars follow-up](https://medium.com/@ijaniszewski)

---

## 🙌 Credits

Built for the data engineering community to explore the power of **Apache Iceberg** — with zero cloud required.

---

**Happy Iceberging! 🧊**  
Give it a ⭐ if you find it useful!