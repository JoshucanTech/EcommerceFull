# Docker Setup Guide

This project uses Docker and Docker Compose to manage all services including the backend, frontend, database, and caching services.

## Prerequisites

- Docker installed on your system
- Docker Compose installed on your system

## Quick Start

1. Create a `.env` file from `.env.example`:
   ```bash
   cp .env.example .env
   ```

2. Start all services:
   ```bash
   docker-compose up
   ```

3. Access the services:
   - Frontend: http://localhost:2000
   - Backend API: http://localhost:4000/api
   - Prisma Studio: http://localhost:5555

## Services Overview

- **Frontend** (Next.js): Port 2000 (internally 3000)
- **Backend** (NestJS): Port 4000
- **PostgreSQL**: Port 5432
- **Redis**: Port 6379
- **Prisma Studio**: Port 5555

## Environment Variables

All environment variables are defined in the `.env` file. Make sure to update them according to your needs, especially the secrets for production.

## Commands

### Start all services
```bash
docker-compose up
```

### Start services in detached mode
```bash
docker-compose up -d
```

### View logs
```bash
docker-compose logs
```

### View logs for a specific service
```bash
docker-compose logs backend
```

### Stop all services
```bash
docker-compose down
```

### Stop all services and remove volumes
```bash
docker-compose down -v
```

### Rebuild services
```bash
docker-compose up --build
```

## Security Notes

1. The default passwords in `.env.example` are only for development.
2. Always use strong passwords in production.
3. Don't commit your `.env` file to version control.
4. All services run as non-root users for security.

## Resource Management

Each service has resource limits defined to prevent any single service from consuming all system resources:
- Backend: 512MB RAM, 0.5 CPU
- Frontend: 512MB RAM, 0.5 CPU
- PostgreSQL: 512MB RAM, 0.5 CPU
- Redis: 256MB RAM, 0.25 CPU
- Prisma Studio: 256MB RAM, 0.25 CPU

## Health Checks

All services have health checks implemented:
- PostgreSQL: `pg_isready`
- Redis: `redis-cli ping`
- Backend: HTTP request to `/api/health`

Services will automatically restart if they fail health checks.