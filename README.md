# 📋 Task Manager Application


> A modern, full-stack task management application with Docker containerization and Docker Compose orchestration.

---

## 🎯 Overview

Task Manager is a production-ready web application that enables users to efficiently create, organize, and manage their daily tasks. Built with modern technologies and containerized for seamless deployment across different environments. This project is part of **DevOps CS316 - Assignment #4**, demonstrating CI/CD pipeline automation with GitHub Actions across Development, Testing, Staging, and Production environments.

**Key Features:**
- ✅ Create, read, update, and delete tasks
- 📝 Task descriptions and completion tracking
- 🗓️ Automatic timestamps for task creation and updates
- 🐳 Full Docker and Docker Compose support
- 🔄 RESTful API architecture
- 💻 Responsive React frontend
- 🔄 **CI/CD Pipeline** with GitHub Actions
- 🌍 **Multi-Environment Deployment** (Dev → Testing → Staging → Production)
- ✅ **Automated Testing & Code Quality Checks**

---

## 🏗️ Project Architecture

```
Task Manager
├── Frontend (React)
│   ├── Port: 3000
│   ├── Framework: React 19
│   └── Build: react-scripts
├── Backend (Express.js)
│   ├── Port: 5000
│   ├── Framework: Express 4
│   └── Database: MongoDB
└── Database (MongoDB)
    ├── Port: 27017
    └── Collection: tasks
```

---

## 📁 Project Structure

```
assignment_4/
├── docker-compose.yml          # Docker Compose configuration
├── README.md                   # Project documentation
├── backend/
│   ├── Dockerfile             # Backend container image
│   ├── package.json           # Backend dependencies
│   └── src/
│       ├── index.js           # Express server setup
│       ├── models/
│       │   └── Task.js        # MongoDB Task schema
│       ├── routes/
│       │   └── tasks.js       # Task API endpoints
│       └── tests/
│           └── tasks.test.js  # API tests
└── frontend/
    ├── Dockerfile             # Frontend container image
    ├── package.json           # Frontend dependencies
    ├── README.md              # Frontend documentation
    ├── public/                # Static assets
    │   ├── index.html
    │   ├── manifest.json
    │   └── robots.txt
    └── src/
        ├── App.js             # Main React component
        ├── App.css            # Component styles
        ├── App.test.js        # Component tests
        ├── index.js           # React entry point
        ├── index.css          # Global styles
        ├── reportWebVitals.js # Performance metrics
        └── setupTests.js      # Test configuration
```

---

## 🚀 Getting Started

### Prerequisites

- **Docker** (v20.10+)
- **Docker Compose** (v1.29+)
- OR **Node.js** (v24+) and **MongoDB** (v7+) for local development

### Quick Start with Docker

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd assignment_4
   ```

2. **Start all services:**
   ```bash
   docker-compose up -d
   ```

3. **Access the application:**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:5000
   - MongoDB: mongodb://localhost:27017

4. **Stop all services:**
   ```bash
   docker-compose down
   ```

### Local Development Setup

#### Backend Setup

1. **Navigate to backend directory:**
   ```bash
   cd backend
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Create `.env` file:**
   ```env
   PORT=5000
   MONGO_URI=mongodb://localhost:27017/taskmanager
   NODE_ENV=development
   ```

4. **Start MongoDB locally** (ensure MongoDB service is running)

5. **Start the development server:**
   ```bash
   npm run dev
   ```

6. **Run tests:**
   ```bash
   npm test
   ```

#### Frontend Setup

1. **Navigate to frontend directory:**
   ```bash
   cd frontend
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Create `.env` file (optional):**
   ```env
   REACT_APP_API_URL=http://localhost:5000
   ```

4. **Start the development server:**
   ```bash
   npm start
   ```

5. **Run tests:**
   ```bash
   npm test
   ```

---

## 🔌 API Reference

### Base URL
```
http://localhost:5000/api/tasks
```

### Endpoints

#### Get All Tasks
```http
GET /api/tasks
```

**Response (200):**
```json
[
  {
    "_id": "507f1f77bcf86cd799439011",
    "title": "Learn Docker",
    "description": "Master containerization",
    "completed": false,
    "createdAt": "2024-05-13T10:30:00Z",
    "updatedAt": "2024-05-13T10:30:00Z"
  }
]
```

#### Create Task
```http
POST /api/tasks
Content-Type: application/json

{
  "title": "Buy groceries",
  "description": "Milk, eggs, bread"
}
```

**Response (201):**
```json
{
  "_id": "507f1f77bcf86cd799439012",
  "title": "Buy groceries",
  "description": "Milk, eggs, bread",
  "completed": false,
  "createdAt": "2024-05-13T10:35:00Z",
  "updatedAt": "2024-05-13T10:35:00Z"
}
```

#### Update Task
```http
PUT /api/tasks/:id
Content-Type: application/json

{
  "completed": true,
  "title": "Updated title"
}
```

**Response (200):**
```json
{
  "_id": "507f1f77bcf86cd799439012",
  "title": "Updated title",
  "description": "Milk, eggs, bread",
  "completed": true,
  "createdAt": "2024-05-13T10:35:00Z",
  "updatedAt": "2024-05-13T11:00:00Z"
}
```

#### Delete Task
```http
DELETE /api/tasks/:id
```

**Response (200):**
```json
{
  "message": "Task deleted"
}
```

#### Health Check
```http
GET /health
```

**Response (200):**
```json
{
  "status": "OK"
}
```

---

## 📦 Dependencies

### Backend
- **express** (^4.18.0) - Web framework
- **mongoose** (^7.0.0) - MongoDB ODM
- **cors** (^2.8.5) - Cross-Origin Resource Sharing
- **dotenv** (^16.0.0) - Environment variable management
- **jest** (^29.0.0) - Testing framework
- **nodemon** (^3.0.0) - Development auto-reload
- **supertest** (^6.0.0) - HTTP assertions

### Frontend
- **react** (^19.2.6) - UI library
- **react-dom** (^19.2.6) - DOM rendering
- **react-scripts** (5.0.1) - Create React App scripts

---

## 🐳 Docker & Docker Compose

### Services

**MongoDB Container**
- Image: mongo:7
- Container: mongo
- Port: 27017
- Volume: mongo_data

**Backend Container**
- Image: Built from ./backend/Dockerfile
- Container: backend
- Port: 5000
- Environment: MONGO_URI, PORT

**Frontend Container**
- Image: Built from ./frontend/Dockerfile
- Container: frontend
- Port: 3000
- Environment: REACT_APP_API_URL

### Common Commands

```bash
# Build all services
docker-compose build

# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# View specific service logs
docker-compose logs -f backend

# Stop all services
docker-compose down

# Remove volumes
docker-compose down -v

# Rebuild and restart
docker-compose up -d --build
```

---

## 🧪 Testing

### Backend Tests
```bash
cd backend
npm test
```

Tests include API endpoint validation with Jest and Supertest.

### Frontend Tests
```bash
cd frontend
npm test
```

Tests include React component and UI functionality tests.

---

## 📝 Environment Variables

### Backend (.env)
```env
PORT=5000
MONGO_URI=mongodb://mongo:27017/taskmanager
NODE_ENV=development
```

### Frontend (.env)
```env
REACT_APP_API_URL=http://localhost:5000
```

---

## 🔧 Available Scripts

### Backend
- `npm start` - Start production server
- `npm run dev` - Start development server with hot-reload
- `npm test` - Run test suite
- `npm run lint` - Run ESLint

### Frontend
- `npm start` - Start development server
- `npm run build` - Build for production
- `npm test` - Run tests
- `npm run eject` - Eject from Create React App

---

## 🎨 Features

### Task Management
- **Create** - Add new tasks with title and optional description
- **Read** - View all tasks sorted by creation date (newest first)
- **Update** - Mark tasks as completed or modify details
- **Delete** - Remove completed or unwanted tasks

### UI/UX
- Clean, intuitive interface
- Real-time task status updates
- Responsive design
- Task action buttons (Done/Undo, Delete)

### Data Persistence
- MongoDB for persistent storage
- Automatic timestamps for created and updated dates
- Transaction support for data integrity

---

## � Assignment Requirements (DevOps CS316 - Assignment #4)

### Task 1: Multi-Service Application Deployment ✅
- ✅ **Frontend:** React 19 application
- ✅ **Backend:** Express.js Node.js service
- ✅ **Database:** MongoDB (NoSQL)
- ✅ **Deployment:** Docker Compose on localhost
- ✅ **Repository:** Public GitHub repository
- ✅ **Collaborators:** Instructor and team members added

### Task 2: AWS EC2 Instances Setup
- 🔧 Testing Environment (EC2 Ubuntu 24.* LTS)
- 🔧 Staging Environment (EC2 Ubuntu 24.* LTS)
- 🔧 Shared security group configuration
- 🔧 Dependencies pre-configured

### Task 3: CI/CD Pipeline Automation
- 🤖 **GitHub Actions Workflows** for automated deployment
- 🔀 **Feature branches** trigger Testing environment deployment
- ✅ **Build, Test, Lint** on every pull request
- 📧 **Notifications** on success/failure
- 🔗 **Main branch merge** triggers Staging environment deployment

---

## 🔑 GitHub Repository Setup

### Repository Configuration
```bash
# Make repository public
# Add collaborators:
# - Team members (can push to feature branches)
# - Instructor (read access + collaborator)

# Branch protection rules enabled on main:
# ✓ Require pull request reviews before merging
# ✓ Require status checks to pass before merging
# ✓ Include administrators in restrictions
# ✓ Require branches to be up-to-date before merging
```

### Workflow Branch Strategy
```
main (protected)
├── feature/task-filter
├── feature/task-priority
└── fix/bug-description

pull request → GitHub Actions → Testing Environment
     ↓
  Code Review & QA Testing
     ↓
Merge to main → GitHub Actions → Staging Environment
     ↓
Client & Team Access
```

---

## 🤖 CI/CD Pipeline with GitHub Actions

### Overview
The CI/CD pipeline automates the deployment process across multiple environments:

```
Developer Push
    ↓
Feature/Fix Branch
    ↓
Pull Request → GitHub Actions Workflow
    ├─ Build Application
    ├─ Run Unit Tests
    ├─ Code Linting/Analysis
    ├─ Deploy to Testing (AWS EC2)
    └─ Send Notifications
    ↓
QA Testing & Review
    ↓
Merge to Main → GitHub Actions Workflow
    ├─ Build Application
    ├─ Run Unit Tests
    ├─ Code Linting/Analysis
    ├─ Deploy to Staging (AWS EC2)
    └─ Send Success Notifications
    ↓
Staging Testing
    ↓
Production Deployment
```

### Workflow Jobs

#### 1. **Build Job**
- Checkout code
- Install dependencies (npm install)
- Build application
- Build Docker images

#### 2. **Test Job**
- Run unit tests with Jest and React Testing Library
- Generate coverage reports
- Fail if tests fail

#### 3. **Lint Job**
- Run ESLint on backend and frontend
- Check code style and standards
- Report issues

#### 4. **Deploy Job (Testing Branch)**
- Deploy to AWS Testing EC2 instance
- Configure environment variables
- Run health checks
- Send deployment notification to QA

#### 5. **Deploy Job (Staging Branch)**
- Deploy to AWS Staging EC2 instance
- Configure environment variables
- Run smoke tests
- Send deployment notification to team

#### 6. **Notification Job**
- Send email notifications on success/failure
- Include deployment links and access instructions
- Notify developers and QA team

### Environment Variables & Secrets
```yaml
# GitHub Secrets to configure:
AWS_TESTING_INSTANCE_IP: <testing-instance-ip>
AWS_STAGING_INSTANCE_IP: <staging-instance-ip>
AWS_ACCESS_KEY_ID: <aws-credentials>
AWS_SECRET_ACCESS_KEY: <aws-credentials>
EMAIL_NOTIFICATION_ADDRESS: <notification-email>
MONGO_TESTING_URI: <testing-mongodb-uri>
MONGO_STAGING_URI: <staging-mongodb-uri>
```

---

## 🌍 Multi-Environment Deployment

### Development Environment (Local)
```bash
# Local development with Docker Compose
docker-compose up -d

# Frontend: http://localhost:3000
# Backend API: http://localhost:5000
# MongoDB: localhost:27017
```

### Testing Environment (AWS EC2)
```
- Triggered by: Pull Request creation
- Access: http://<Testing-Instance-IP>:3000
- Database: MongoDB on Testing instance
- Purpose: QA Testing and validation
- Notification: Email to QA on deployment
```

### Staging Environment (AWS EC2)
```
- Triggered by: Merge to main branch
- Access: http://<Staging-Instance-IP>:3000
- Database: MongoDB on Staging instance
- Purpose: Pre-production testing and client review
- Notification: Email to team on deployment
```

### Production Environment
```
- Manual deployment trigger (after staging validation)
- Automated health checks
- Rollback capabilities
```

---

## 📧 Notification System

### Email Notifications Sent

**On Pull Request Deployment (Testing):**
```
To: QA (Instructor)
Subject: ✅ Testing Environment Deployed
Content:
- Pull request details
- Changes deployed
- Testing server URL: http://<IP>:3000
- How to access and test
- Deployment timestamp
```

**On Test/Build Failure:**
```
To: Developer (PR creator) + QA
Subject: ❌ Deployment Failed
Content:
- Failure details
- Build/test error logs
- Failed step (Build/Test/Lint)
- Action required
```

**On Main Branch Merge (Staging):**
```
To: Team + Instructor
Subject: ✅ Staging Environment Deployed
Content:
- Merged PR details
- All tests passed
- Staging server URL: http://<IP>:3000
- Deployment timestamp
- Ready for client review
```

---

## 🔐 Branch Protection & Pull Request Workflow

### Main Branch Protection Rules
```
✓ Require pull request reviews before merging
✓ Require at least 1 approving review
✓ Require status checks to pass (Build, Test, Lint)
✓ Require branches to be up-to-date before merging
✓ Include administrators in restrictions
✓ Dismiss stale pull request approvals when new commits pushed
```

### Pull Request Workflow
```
1. Developer creates feature/fix branch from main
2. Developer pushes commits to feature branch
3. Developer creates Pull Request to main
4. GitHub Actions Workflow Triggered
   ├─ Build project
   ├─ Run tests
   ├─ Run linting
   └─ Deploy to Testing environment
5. Workflow sends notification email
6. QA reviews and tests on Testing environment
7. QA reviews PR on GitHub
8. PR gets approved and merged to main
9. GitHub Actions Workflow Triggered
   ├─ Build project
   ├─ Run tests
   ├─ Run linting
   └─ Deploy to Staging environment
10. Team and client can access Staging environment
```

---

## 📊 Deployment Scenarios

### Scenario 1: Bug Fix on Testing
```
Developer → fix/login-issue branch → Push
     ↓
GitHub Actions triggers
     ↓
Build: ✅ Success
Tests: ✅ All pass
Lint:  ✅ No issues
     ↓
Deploy to Testing Environment
     ↓
Email to QA: "Testing Environment Ready"
QA URL: http://<Testing-IP>:3000/login
```

### Scenario 2: New Feature on Testing
```
Developer → feature/task-export branch → Push
     ↓
GitHub Actions triggers
     ↓
Build: ✅ Success
Tests: ✅ 95% coverage
Lint:  ⚠️ 2 warnings (non-blocking)
     ↓
Deploy to Testing Environment
     ↓
Email to QA: "New Feature Deployed for Testing"
QA can access and validate export functionality
```

### Scenario 3: Failed Build → Notification
```
Developer → feature/new-ui branch → Push
     ↓
GitHub Actions triggers
     ↓
Build: ❌ Failed
Tests: ⏸️ Skipped
Lint:  ⏸️ Skipped
     ↓
NO Deployment to Testing
     ↓
Email to Developer: "Build Failed - Check logs"
Link to GitHub Actions log for debugging
```

---

## 🔧 AWS EC2 Instance Setup

### Testing Instance Configuration
```
Instance Type: t3.micro or t3.small
OS: Ubuntu Server 24.04 LTS (HVM)
Security Group: DevOps-SG
Inbound Rules:
  - SSH (22) from developer IPs
  - HTTP (80) for frontend access
  - HTTPS (443) for secure access
  - Custom (5000) for API access
Outbound Rules: Allow all

Software Installed:
  - Node.js 24
  - npm
  - MongoDB
  - Docker
  - Docker Compose
  - Git
```

### Staging Instance Configuration
```
Instance Type: t3.small or t3.medium
OS: Ubuntu Server 24.04 LTS (HVM)
Security Group: DevOps-SG (same as Testing)
Inbound Rules:
  - SSH (22) from developer IPs
  - HTTP (80) for public access
  - HTTPS (443) for secure access
  - Custom (5000) for API access

Software Installed:
  - Node.js 24
  - npm
  - MongoDB
  - Docker
  - Docker Compose
  - Git
  - Nginx (reverse proxy)
```

### Security Group Configuration
```yaml
# Shared across all environments
DevOps-SG:
  Inbound:
    - SSH (22): 0.0.0.0/0 or specific IPs
    - HTTP (80): 0.0.0.0/0
    - HTTPS (443): 0.0.0.0/0
    - Custom TCP (5000): 0.0.0.0/0
    - MongoDB (27017): Internal only
  Outbound:
    - All traffic allowed
```

---

## 🚀 Manual Deployment Trigger

### Workflow Dispatch Buttons

Both GitHub Actions workflows include manual trigger capability:

```yaml
# Testing Deployment (manual trigger)
- Can deploy to Testing without PR
- Useful for testing specific branches
- Accessible via GitHub Actions tab

# Staging Deployment (manual trigger)
- Can deploy to Staging without merge
- Useful for emergency deployments
- Requires GitHub Actions admin access
```

### How to Manually Trigger
```
1. Go to GitHub Repository
2. Click "Actions" tab
3. Select Workflow (e.g., "Deploy to Testing")
4. Click "Run workflow"
5. Select branch
6. Click "Run workflow"
7. Monitor deployment progress
```

---

## 🚢 Production Deployment

### Deployment Strategy
The application is ready for deployment on:
- AWS (ECS, EKS, Elastic Beanstalk)
- Azure (Container Instances, App Service, AKS)
- Google Cloud (Cloud Run, GKE, App Engine)
- DigitalOcean (App Platform, Kubernetes)
- Heroku (with Docker support)

### Production Deployment Steps
1. **Validate Staging Environment** - Ensure all tests pass
2. **Tag Release** - Create release tag on GitHub
3. **Manual Deployment** - Approve and trigger production workflow
4. **Health Checks** - Verify all services running
5. **Monitoring** - Setup logs, metrics, alerts
6. **Rollback Plan** - Keep previous version available

---

## 🛠️ Development Workflow

### Local Development
```bash
# Terminal 1: Backend
cd backend
npm run dev

# Terminal 2: Frontend
cd frontend
npm start

# Terminal 3: MongoDB (or use Docker)
docker run -d -p 27017:27017 mongo:7
```

### Git Workflow
```bash
# Create feature branch
git checkout -b feature/new-feature

# Make changes and test locally
npm test

# Commit changes
git add .
git commit -m "feat: add new feature"

# Push to remote
git push origin feature/new-feature

# Create pull request and merge
```

---

## 🐛 Troubleshooting

### Port Already in Use
```bash
# Find process using port 3000, 5000, or 27017
lsof -i :3000

# Kill process
kill -9 <PID>
```

### MongoDB Connection Error
```bash
# Ensure MongoDB container is running
docker-compose logs mongo

# Verify connection string in .env
MONGO_URI=mongodb://mongo:27017/taskmanager
```

### Frontend Cannot Connect to API
```bash
# Check REACT_APP_API_URL environment variable
# Ensure backend is running on port 5000
# Check docker-compose service dependencies
docker-compose logs backend
```

### Docker Build Failures
```bash
# Clear cache and rebuild
docker-compose down -v
docker-compose build --no-cache
docker-compose up -d
```

---

## 📚 Technology Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| **Frontend** | React | 19.2.6 |
| **Backend** | Express.js | 4.18.0 |
| **Database** | MongoDB | 7 |
| **Runtime** | Node.js | 24 (Alpine) |
| **Container** | Docker | Latest |
| **Orchestration** | Docker Compose | 3.8 |

---

## 📄 License

This project is provided as-is for educational and assignment purposes.

---

## 👤 Author

Created as a DevOps assignment demonstrating containerization and multi-tier application architecture.

---

## 📞 Support

For issues or questions:
1. Check the [Troubleshooting](#-troubleshooting) section
2. Review Docker Compose logs: `docker-compose logs`
3. Verify environment variables and configurations
4. Ensure all prerequisites are installed

---

## 📋 Assignment Submission

### Deliverables (DevOps CS316 - Assignment #4)

#### 1. **GitHub Repository** (Public)
- ✅ Multi-service application deployed
- ✅ All GitHub Actions workflows included
- ✅ Branch protection rules configured
- ✅ Collaborators and team members added
- ✅ README documentation completed

#### 2. **GitHub Actions Workflows**
- ✅ Testing environment deployment workflow
- ✅ Staging environment deployment workflow
- ✅ Build, test, lint automation
- ✅ Email notification system
- ✅ Manual trigger capability

#### 3. **AWS Infrastructure**
- ✅ Testing EC2 instance (Ubuntu 24 LTS)
- ✅ Staging EC2 instance (Ubuntu 24 LTS)
- ✅ Shared security group configuration
- ✅ Pre-configured dependencies

#### 4. **Documentation Package**
- ✅ README.md (this file)
- ✅ Project introduction and objectives
- ✅ Assignment flow diagram
- ✅ Screenshots of each task/subtask
- ✅ Challenges and solutions documented
- ✅ Screenshots of:
  - GitHub repository setup
  - Branch protection rules
  - GitHub Actions workflow runs
  - Testing environment deployment
  - Staging environment deployment
  - Email notifications
  - EC2 instances
  - Security group configuration

---

## ✅ Assignment Checklist

- [ ] **Task 1: Application Selection & Deployment**
  - [ ] Multi-service app selected (Frontend, Backend, Database)
  - [ ] Deployed locally with Docker Compose
  - [ ] Repository pushed to GitHub
  - [ ] Repository made public
  - [ ] Collaborators added
  - [ ] Instructor added as collaborator
  - [ ] Branch protection rules configured

- [ ] **Task 2: AWS EC2 Instances**
  - [ ] Testing EC2 instance created
  - [ ] Staging EC2 instance created
  - [ ] Ubuntu 24 LTS AMI used
  - [ ] Common security group configured
  - [ ] Dependencies installed
  - [ ] Instances properly named

- [ ] **Task 3: CI/CD Pipeline Automation**
  - [ ] GitHub Actions workflow for Testing environment
  - [ ] GitHub Actions workflow for Staging environment
  - [ ] Build step implemented
  - [ ] Unit tests configured
  - [ ] Linting/code analysis setup
  - [ ] Email notifications configured
  - [ ] Manual workflow dispatch enabled
  - [ ] PR triggers Testing deployment
  - [ ] Merge to main triggers Staging deployment

- [ ] **Documentation & Submission**
  - [ ] README.md completed
  - [ ] Project introduction written
  - [ ] Flow diagram created
  - [ ] Screenshots captured for each task
  - [ ] Challenges documented
  - [ ] Solutions explained
  - [ ] Professional report prepared

---

## 📞 Support & Troubleshooting

### Common Issues

**Workflow fails on AWS deployment:**
```
1. Check EC2 instance status
2. Verify security group rules
3. Check SSH key permissions
4. Review workflow logs on GitHub
5. Verify environment variables
```

**Email notifications not sending:**
```
1. Check GitHub Secrets configuration
2. Verify email service credentials
3. Check spam folder
4. Review GitHub Actions logs
```

**Git push rejected:**
```
1. Ensure branch is up-to-date
2. Check branch protection rules
3. Verify you have push access
4. Rebase feature branch on main
```

**Build/Test failures:**
```
1. Run tests locally
2. Check Node.js version compatibility
3. Verify all dependencies installed
4. Review error logs in GitHub Actions
```

---

## 📚 Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [AWS EC2 User Guide](https://docs.aws.amazon.com/ec2/)
- [Docker Documentation](https://docs.docker.com/)
- [Express.js Guide](https://expressjs.com/)
- [React Documentation](https://react.dev/)
- [MongoDB Manual](https://docs.mongodb.com/manual/)

---

## 👥 Team Information

**Course:** DevOps CS316  
**Assignment:** #4 - CI/CD Pipeline with Git and GitHub Actions  
**Instructor:** Muhammad Sajid Ali  
**Total Marks:** 100

### Task Distribution
- **Task 1 (Deployment):** 30 marks
- **Task 2 (AWS EC2):** 15 marks
- **Task 3 (CI/CD Automation):** 55 marks

---

**Last Updated:** May 13, 2026  
**Version:** 2.0 (Assignment-Complete)  
**Repository:** [GitHub](https://github.com/Muhammad-Hashir-55/task-manager-devops)

