Dynamic Form System
📋 Overview
A full-stack dynamic form submission system with:

✅ React Frontend (Dynamic form rendering)

✅ FastAPI Backend (REST API + validation)

✅ PostgreSQL Database (Data persistence)

✅ Redis Cache (Performance optimization)

✅ NGINX (Reverse proxy)

✅ Docker Compose (Service orchestration)

🏗️ Architecture
text
┌─────────────────────────────────────────┐
│      NGINX (Reverse Proxy)              │
│     Port 80 (Frontend + API)            │
└──────────────────┬──────────────────────┘
        │                     │
        ▼                     ▼
   ┌─────────┐         ┌──────────────┐
   │ Frontend│         │  FastAPI     │
   │ React   │         │  Gateway     │
   │Port3000 │         │  Port 8000   │
   └────┬────┘         └──┬────┬──────┘
        │                 │    │
        │             ┌───▼─┐  │
        │             │Cache│  │
        │             │Redis│  │
        │             └──────┘  │
        │                       │
        └───────────┬───────────┘
                    ▼
            ┌────────────────┐
            │   Database     │
            │  PostgreSQL    │
            │   Port 5432    │
            └────────────────┘
🔄 Data Flow
Form Submission:
text
User → Frontend (React)
     ↓ (Form Data)
     NGINX (Port 80)
     ↓
     FastAPI Gateway
     ↓ (Validation)
     ✅ Check Email Duplicate?
     ✅ Validate Form Data
     ↓
     PostgreSQL (Save)
     ↓
     Response → Frontend
Fetch Submissions:
text
User → Frontend
     ↓
     NGINX
     ↓
     FastAPI Gateway
     ↓
     Redis Cache? → YES → Return (Fast!)
     ↓ NO
     PostgreSQL (Query)
     ↓
     Save to Cache (TTL: 1 hour)
     ↓
     Response → Frontend
🐳 Services & Ports
Service	Port	Role
NGINX	80	Main entry point
Frontend	3000	React application
API	8000	FastAPI backend
PostgreSQL	5432	Database
Redis	6379	Cache layer
📁 Project Structure
text
Dynamic-Form-System/
├── app/                    # Python Backend
│   ├── api/               # Routes + Gateway
│   ├── services/          # Database + Cache
│   └── core/              # Configuration
├── frontend/              # React Frontend
│   ├── src/
│   │   ├── components/    # React Components
│   │   ├── api/           # HTTP Client
│   │   └── styles/        # CSS
│   └── package.json
├── docker-compose.yml     # Orchestration
├── nginx.conf             # Proxy config
├── Dockerfile             # Backend build
└── requirements.txt       # Python deps
⚡ Features
✅ Email validation & duplicate detection
✅ Redis caching with 1-hour TTL
✅ Pagination support
✅ Responsive UI
✅ Multi-stage Docker build
✅ Health checks
✅ CORS enabled

🔐 Security
Non-root user in containers

Environment variables stored in .env (gitignored)

Health checks on all services

CORS properly configured