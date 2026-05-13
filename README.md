# 📋 Task Manager Application

> A modern, full-stack task management application with Docker containerization and Docker Compose orchestration.

---

## 🎯 Overview

Task Manager is a production-ready web application that enables users to efficiently create, organize, and manage their daily tasks. Built with modern technologies and containerized for seamless deployment across different environments.

**Key Features:**
- ✅ Create, read, update, and delete tasks
- 📝 Task descriptions and completion tracking
- 🗓️ Automatic timestamps for task creation and updates
- 🐳 Full Docker and Docker Compose support
- 🔄 RESTful API architecture
- 💻 Responsive React frontend

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

## 🚢 Deployment

### Production Deployment with Docker Compose

1. **Set environment variables:**
   ```bash
   export REACT_APP_API_URL=https://your-api-domain.com
   ```

2. **Start services:**
   ```bash
   docker-compose up -d
   ```

3. **Configure reverse proxy** (Nginx, Apache) for production URLs

### Cloud Deployment
The application is ready for deployment on:
- AWS (ECS, EKS)
- Azure (Container Instances, AKS)
- Google Cloud (Cloud Run, GKE)
- DigitalOcean (App Platform)
- Heroku

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

**Last Updated:** May 13, 2026  
**Version:** 1.0.0
