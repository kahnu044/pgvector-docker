# PostgreSQL + pgvector + Adminer — Docker Setup

This repository provides a quick-start setup for running PostgreSQL with the pgvector extension using Docker Compose, along with Adminer for easy database management.

## 📦 Services

- **PostgreSQL**: With `pgvector` pre-installed
- **Adminer**: Simple web-based SQL client

## 🚀 Getting Started

### 1️⃣ Clone Repository

```bash
git clone https://github.com/kahnu044/pgvector-docker.git
cd pgvector-docker
```

### 2️⃣ Run Containers

```bash
docker-compose up -d
```

### 3️⃣ Access Adminer

- URL: [http://localhost:8087](http://localhost:8087)
- System: PostgreSQL
- Server: `db`
- Username: `postgres`
- Password: `postgres`
- Database: `vector_db`

## 🛠️ Usage Guide

### ✅ Create the Extension

Run this in Adminer or psql:

```sql
CREATE EXTENSION IF NOT EXISTS vector;
```

### ✅ Create a Table with Vector Column

Example:

```sql
CREATE TABLE items (
    id SERIAL PRIMARY KEY,
    name TEXT,
    embedding VECTOR(3) -- adjust length as needed
);
```

### ✅ Insert Data

```sql
INSERT INTO items (name, embedding) VALUES
('Item 1', '[0.1, 0.2, 0.3]'),
('Item 2', '[0.4, 0.5, 0.6]');
```

### ✅ Fetch Nearest Vectors

Using L2 distance:

```sql
SELECT * FROM items
ORDER BY embedding <-> '[0.1, 0.2, 0.25]'
LIMIT 5;
```

### ✅ Add an Index (Optional for Large Datasets)

```sql
CREATE INDEX ON items USING ivfflat (embedding vector_l2_ops) WITH (lists = 100);

-- After creating, ANALYZE:
ANALYZE items;
```

## ⚙️ Environment Variables

You can customize these in `docker-compose.yml`:

- `POSTGRES_USER`
- `POSTGRES_PASSWORD`
- `POSTGRES_DB`

## 📚 References

- [pgvector GitHub](https://github.com/pgvector/pgvector)
- [pgvector Docker Hub](https://hub.docker.com/r/pgvector/pgvector)
- [Adminer](https://www.adminer.org/)

## 🤝 Author

- [kahnu044](https://github.com/kahnu044)
