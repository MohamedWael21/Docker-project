# Recruit AI - Docker Setup

Docker setup for Recruit AI application with Backend API, MongoDB, Redis, and worker services.

## Prerequisites

- Docker (v20.10+) - [Install](https://docs.docker.com/get-docker/)
- Docker Compose (v1.29+)

Verify installation:

```bash
docker --version
docker-compose --version
```

## Quick Start

### 1. Create .env File

Create `.env` in the project root with these variables:

| Variable                | Value                                                   | Description                 |
| ----------------------- | ------------------------------------------------------- | --------------------------- |
| `PORT`                  | `5000`                                                  | Backend port                |
| `NODE_ENV`              | `development`                                           | Environment                 |
| `MONGO_URI`             | `mongodb+srv://user:pass@cluster.mongodb.net/recruitai` | MongoDB connection          |
| `REDIS_HOST`            | `redis`                                                 | Redis host (Docker service) |
| `REDIS_PORT`            | `6379`                                                  | Redis port                  |
| `JWT_SECRET`            | `your_secret_key`                                       | JWT secret                  |
| `JWT_EXPIRES_IN`        | `7d`                                                    | Token expiration            |
| `GOOGLE_API_KEY`        | `your_key`                                              | Google API key              |
| `GOOGLE_CLOUD_PROJECT`  | `project_id`                                            | Google Cloud project        |
| `GROQ_API_KEY`          | `your_key`                                              | Groq AI API key             |
| `OPENROUTER_API_KEY`    | `your_key`                                              | OpenRouter API key          |
| `PINECONE_API_KEY`      | `your_key`                                              | Pinecone API key            |
| `PINECONE_INDEX`        | `recruit-ai`                                            | Pinecone index name         |
| `CLIENT_URL`            | `https://naqla-recruiter.vercel.app`                    | Frontend URL                |
| `CLOUDINARY_CLOUD_NAME` | `your_name`                                             | Cloudinary cloud name       |
| `CLOUDINARY_API_KEY`    | `your_key`                                              | Cloudinary API key          |
| `CLOUDINARY_API_SECRET` | `your_secret`                                           | Cloudinary secret           |
| `EMAIL_USER`            | `your_email@gmail.com`                                  | Gmail address               |
| `EMAIL_PASS`            | `app_password`                                          | Gmail app password\*        |

\*For `EMAIL_PASS`: Use Gmail app password (not regular password). Enable 2FA, then get it from https://myaccount.google.com/apppasswords

### 2. Start Services

```bash
# Start all containers in background
docker-compose up -d

# View logs
docker-compose logs -f

# Check status
docker-compose ps
```

### 3. Access Services

- **Backend API**: http://localhost:5000
- **MongoDB**: mongodb://localhost:27017
- **Redis**: localhost:6380

## Services

| Service           | Container               | Port  | Purpose          |
| ----------------- | ----------------------- | ----- | ---------------- |
| Backend           | naqla_backend           | 5000  | REST API server  |
| MongoDB           | naqla_mongodb           | 27017 | Database         |
| Redis             | naqla_redis             | 6380  | Cache & queue    |
| Frontend          | naqla_frontend          | 8080  | Web interface    |
| Worker Background | naqla_worker_background | -     | Background jobs  |
| Worker CV         | naqla_worker_cv         | -     | CV processing    |
| Worker Automation | naqla_worker_automation | -     | Automation tasks |

## Common Commands

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# View logs (all services)
docker compose logs -f

# View specific service logs
docker compose logs -f backend

# Restart service
docker compose restart backend

# Stop specific service
docker compose stop backend

# Access container shell
docker compose exec backend sh

# Test Redis
docker compose exec redis redis-cli ping

# Test MongoDB
docker compose exec mongodb mongosh --eval "db.adminCommand('ping')"

# Pull latest images
docker compose pull

# Rebuild and start
docker compose up -d --build

# Remove volumes
docker compose down -v
```
