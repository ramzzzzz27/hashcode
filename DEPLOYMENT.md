# 🚀 HashCode Deployment Guide

## Table of Contents
- [Local Development](#local-development)
- [Docker Deployment](#docker-deployment)
- [Cloud Deployment](#cloud-deployment)
- [Environment Setup](#environment-setup)
- [Troubleshooting](#troubleshooting)

## Local Development

### Prerequisites
- Node.js >= 16
- MongoDB >= 4.4
- FFmpeg
- npm or yarn

### 1. Clone Repository
```bash
git clone https://github.com/ramzzzzz27/hashcode.git
cd hashcode
```

### 2. Backend Setup
```bash
cd backend

# Copy environment variables
cp .env.example .env

# Install dependencies
npm install

# Start development server
npm run dev
```

Backend will run on `http://localhost:5000`

### 3. Frontend Setup
```bash
cd ../frontend

# Copy environment variables
cp .env.example .env

# Install dependencies
npm install

# Start development server
npm run dev
```

Frontend will run on `http://localhost:5173`

## Docker Deployment

### Using Docker Compose
```bash
# Build and start all services
docker-compose up --build

# In detached mode
docker-compose up -d --build

# Stop all services
docker-compose down

# View logs
docker-compose logs -f backend
docker-compose logs -f frontend
```

Services will be available at:
- Frontend: http://localhost:5173
- Backend API: http://localhost:5000
- MongoDB: mongodb://admin:password@localhost:27017
- Redis: redis://localhost:6379

### Individual Docker Builds
```bash
# Backend
cd backend
docker build -t hashcode-backend .
docker run -p 5000:5000 --env-file .env hashcode-backend

# Frontend
cd frontend
docker build -t hashcode-frontend .
docker run -p 5173:5173 hashcode-frontend
```

## Cloud Deployment

### Heroku

#### Backend Deployment
```bash
# Install Heroku CLI and login
heroku login

# Create app
heroku create hashcode-api

# Set environment variables
heroku config:set -a hashcode-api MONGODB_URI=your_mongodb_uri
heroku config:set -a hashcode-api JWT_SECRET=your_jwt_secret
heroku config:set -a hashcode-api FRONTEND_URL=your_frontend_url

# Deploy
git subtree push --prefix backend heroku main
```

#### Frontend Deployment (Vercel)
```bash
# Install Vercel CLI
npm install -g vercel

# Deploy frontend
cd frontend
vercel
```

### AWS Deployment

#### Backend (EC2)
1. Launch EC2 instance (Ubuntu 20.04)
2. SSH into instance
3. Install Node.js and MongoDB
4. Clone repository
5. Set environment variables
6. Use PM2 for process management
7. Set up nginx as reverse proxy
8. Configure SSL with Let's Encrypt

#### Frontend (S3 + CloudFront)
1. Build frontend: `npm run build`
2. Create S3 bucket
3. Upload `dist` folder to S3
4. Create CloudFront distribution
5. Configure custom domain

### DigitalOcean Deployment

#### Using App Platform
1. Fork repository
2. Connect GitHub account to DigitalOcean
3. Create new app
4. Set environment variables
5. Deploy automatically

#### Manual VPS Deployment
```bash
# SSH into droplet
ssh root@your_droplet_ip

# Update system
apt update && apt upgrade -y

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
apt install -y nodejs

# Install MongoDB
apt install -y mongodb

# Clone and deploy
git clone https://github.com/ramzzzzz27/hashcode.git
cd hashcode/backend
npm install
npm run build
```

### Railway Deployment

1. Connect GitHub repository
2. Create new project
3. Add services (MongoDB, Redis)
4. Set environment variables
5. Deploy automatically

## Environment Setup

### Required Environment Variables

#### Backend (.env)
```
PORT=5000
NODE_ENV=production
MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/hashcode
JWT_SECRET=very_long_random_secret_key
FRONTEND_URL=https://your-frontend-domain.com

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Email
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password

# Optional
REDIS_URL=redis://your_redis_url
```

#### Frontend (.env)
```
VITE_API_URL=https://your-api-domain.com/api
VITE_SOCKET_URL=https://your-api-domain.com
VITE_GOOGLE_CLIENT_ID=your_google_client_id
VITE_CLOUDINARY_CLOUD_NAME=your_cloud_name
```

## Production Checklist

- [ ] Set secure JWT_SECRET (use strong random string)
- [ ] Enable HTTPS/SSL on both frontend and backend
- [ ] Set NODE_ENV=production
- [ ] Configure CORS properly for frontend domain
- [ ] Set up database backups
- [ ] Configure monitoring and logging
- [ ] Set up error tracking (Sentry)
- [ ] Enable rate limiting on API
- [ ] Configure CDN for static assets
- [ ] Set up automated deployments
- [ ] Test all authentication flows
- [ ] Verify video streaming works
- [ ] Load test the application
- [ ] Set up health monitoring
- [ ] Document deployment process

## Performance Optimization

### Frontend
- Enable code splitting
- Lazy load routes
- Compress images
- Use CDN for assets
- Enable browser caching
- Minify CSS/JS

### Backend
- Enable gzip compression
- Use Redis caching
- Implement database indexing
- Use connection pooling
- Enable response compression
- Optimize queries

### Infrastructure
- Use load balancer
- Auto-scaling
- Database replication
- Multi-region deployment
- DDoS protection

## Monitoring & Logs

### Backend Logs
```bash
# Docker
docker-compose logs -f backend

# Heroku
heroku logs -t

# PM2
pm2 logs
```

### Frontend Errors
- Sentry integration
- Browser console monitoring
- Error tracking dashboard

### Database Monitoring
- MongoDB Atlas monitoring
- Query performance analysis
- Backup verification

## Troubleshooting

### MongoDB Connection Issues
```bash
# Check connection string
# Verify whitelist IP
# Check credentials
# Test connection with mongosh
mongosh "mongodb+srv://user:password@cluster.mongodb.net/hashcode"
```

### Socket.IO Connection Issues
- Verify CORS settings
- Check WebSocket support
- Verify port accessibility
- Check reverse proxy configuration

### Video Streaming Issues
- Verify Cloudinary credentials
- Check video processing status
- Verify HLS stream URL
- Check CORS headers

### High Memory Usage
- Check for memory leaks
- Optimize database queries
- Implement pagination
- Use caching strategies

## Support

For deployment issues:
1. Check logs
2. Verify environment variables
3. Test locally first
4. Check documentation
5. Open GitHub issue with details

---

**Last Updated**: 2026-05-23
