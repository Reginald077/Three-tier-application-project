# Three-Tier Application Project

A full-stack three-tier web application deployed on AWS EC2 and containerised using Docker and Docker Compose.

## 🏗️ Architecture

The application follows the classic three-tier architecture:

- **Web Tier** — React frontend served by NGINX
- **App Tier** — Node.js backend REST API (port 4000)
- **Database Tier** — MySQL database

## 🛠️ Technologies Used

- **Frontend:** React.js
- **Backend:** Node.js, Express.js
- **Database:** MySQL 8.0
- **Web Server:** NGINX
- **Containerisation:** Docker, Docker Compose
- **Cloud:** AWS EC2 (Ubuntu 24.04)
- **Process Manager:** PM2

## 🚀 Getting Started

### Prerequisites
- Docker and Docker Compose installed
- AWS EC2 instance (t2.medium recommended)

### Run with Docker Compose

```bash
# Clone the repository
git clone https://github.com/Reginald077/Three-tier-application-project.git
cd Three-tier-application-project

# Start all containers
docker compose up --build
```

Access the app at `http://localhost/#/db`

### Run Manually (without Docker)

1. **Database Setup**
```bash
sudo mysql -u root
CREATE DATABASE webappdb;
CREATE USER 'webappuser'@'localhost' IDENTIFIED BY 'StrongPassword123!';
GRANT ALL PRIVILEGES ON webappdb.* TO 'webappuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

2. **App Tier**
```bash
cd app-tier
npm install
npm install mysql2 dotenv
# Create .env file with DB credentials
npm start
```

3. **Web Tier**
```bash
cd web-tier
npm install
npm run build
```

4. **NGINX** — configure to serve the build folder and proxy /api/ to port 4000

## 🐳 Docker Setup

The project includes:
- `app-tier/Dockerfile` — Node.js container
- `web-tier/Dockerfile` — Multi-stage build: React build + NGINX
- `docker-compose.yml` — Orchestrates all three containers

## 📚 What I Learned

- Deploying a multi-tier application on AWS EC2
- Configuring NGINX as a reverse proxy
- Debugging Node.js and MySQL connection issues
- Containerising applications with Docker
- Using Docker Compose to manage multi-container applications
- Managing processes with PM2
- Fixing file permission issues on Linux
- Working with environment variables and dotenv

## 🔧 Issues Solved Along the Way

- Fixed MySQL authentication issues by migrating from `mysql` to `mysql2`
- Resolved NGINX permission denied errors with `chmod`
- Fixed dotenv loading order in `DbConfig.js` and `TransactionService.js`
- Added swap memory to handle npm install on t2.micro
- Configured Docker Compose `restart: on-failure` for app-tier startup timing

## 👤 Author

**Ogbemudia Otabor** — System Analyst transitioning into Cloud Engineering  
[GitHub](https://github.com/Reginald077) | [LinkedIn](#)
