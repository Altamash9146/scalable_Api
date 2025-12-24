# Scalable REST API with Authentication & Role-Based Access

A full-stack task management application built with Node.js, Express, MongoDB, and React. This project demonstrates secure backend API development with JWT authentication, role-based access control, and a modern frontend interface.

## 🚀 Features

### Backend (Primary Focus)
- ✅ **User Authentication**: Registration and login with JWT tokens
- ✅ **Password Security**: Bcrypt hashing with salt rounds
- ✅ **Role-Based Access Control**: User and Admin roles with different permissions
- ✅ **CRUD Operations**: Complete task management functionality
- ✅ **API Versioning**: Structured v1 API endpoints
- ✅ **Input Validation**: Comprehensive validation using express-validator
- ✅ **Error Handling**: Centralized error handling middleware
- ✅ **Security Features**: CORS, Helmet, Rate limiting
- ✅ **API Documentation**: Interactive Swagger/OpenAPI documentation
- ✅ **Database**: MongoDB with Mongoose ODM

### Frontend (Supportive)
- ✅ **React Application**: Modern React with hooks and context
- ✅ **Authentication UI**: Login and registration forms
- ✅ **Protected Routes**: JWT-based route protection
- ✅ **Task Management**: Full CRUD interface for tasks
- ✅ **Admin Panel**: User management for administrators
- ✅ **Responsive Design**: TailwindCSS for modern UI
- ✅ **Error Handling**: Toast notifications for user feedback

## 🛠️ Technology Stack

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB with Mongoose
- **Authentication**: JWT (jsonwebtoken)
- **Password Hashing**: bcryptjs
- **Validation**: express-validator, Joi
- **Documentation**: Swagger (swagger-jsdoc, swagger-ui-express)
- **Security**: Helmet, CORS, express-rate-limit
- **Logging**: Morgan

### Frontend
- **Framework**: React 18
- **Routing**: React Router DOM
- **HTTP Client**: Axios
- **Forms**: React Hook Form
- **Styling**: TailwindCSS
- **Icons**: Lucide React
- **Notifications**: React Hot Toast

## 📁 Project Structure

```
├── backend/
│   ├── config/
│   │   ├── database.js          # Database connection
│   │   └── swagger.js           # API documentation setup
│   ├── middleware/
│   │   ├── auth.js              # Authentication & authorization
│   │   ├── errorHandler.js      # Global error handling
│   │   └── validation.js        # Input validation rules
│   ├── models/
│   │   ├── User.js              # User schema
│   │   └── Task.js              # Task schema
│   ├── routes/
│   │   ├── auth.js              # Authentication routes
│   │   ├── tasks.js             # Task CRUD routes
│   │   └── users.js             # User management routes
│   ├── .env                     # Environment variables
│   ├── .env.example             # Environment template
│   ├── package.json             # Dependencies
│   └── server.js                # Application entry point
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   └── Navbar.js        # Navigation component
│   │   ├── contexts/
│   │   │   └── AuthContext.js   # Authentication context
│   │   ├── pages/
│   │   │   ├── Login.js         # Login page
│   │   │   ├── Register.js      # Registration page
│   │   │   ├── Dashboard.js     # Dashboard with stats
│   │   │   ├── Tasks.js         # Task management
│   │   │   └── Users.js         # User management (Admin)
│   │   ├── App.js               # Main application
│   │   └── index.js             # React entry point
│   └── package.json             # Frontend dependencies
└── README.md                    # This file
```

## 🚀 Quick Start

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local or cloud instance)
- npm or yarn

### Backend Setup

1. **Clone and navigate to the project**
```bash
git clone <repository-url>
cd scalable-rest-api
```

2. **Install backend dependencies**
```bash
npm install
```

3. **Environment Configuration**
```bash
cp .env.example .env
# Edit .env with your configuration
```

4. **Start MongoDB**
```bash
# If using local MongoDB
mongod

# Or use MongoDB Atlas cloud connection
```

5. **Run the backend server**
```bash
# Development mode
npm run dev

# Production mode
npm start
```

The backend server will start on `http://localhost:5000`

### Frontend Setup

1. **Navigate to frontend directory**
```bash
cd frontend
```

2. **Install frontend dependencies**
```bash
npm install
```

3. **Start the React application**
```bash
npm start
```

The frontend will start on `http://localhost:3000`

## 📚 API Documentation

Once the backend is running, visit `http://localhost:5000/api-docs` for interactive Swagger documentation.

### Key API Endpoints

#### Authentication
- `POST /api/v1/auth/register` - User registration
- `POST /api/v1/auth/login` - User login
- `GET /api/v1/auth/me` - Get current user profile
- `POST /api/v1/auth/refresh` - Refresh JWT token

#### Tasks
- `GET /api/v1/tasks` - Get all tasks (with pagination & filters)
- `POST /api/v1/tasks` - Create new task
- `GET /api/v1/tasks/:id` - Get specific task
- `PUT /api/v1/tasks/:id` - Update task
- `DELETE /api/v1/tasks/:id` - Delete task
- `GET /api/v1/tasks/stats/overview` - Get task statistics

#### Users (Admin Only)
- `GET /api/v1/users` - Get all users
- `GET /api/v1/users/:id` - Get specific user
- `PATCH /api/v1/users/:id/toggle-status` - Activate/deactivate user
- `PATCH /api/v1/users/:id/role` - Update user role

## 🔐 Authentication & Authorization

### JWT Token Structure
```json
{
  "userId": "user_object_id",
  "role": "user|admin",
  "iat": "issued_at_timestamp",
  "exp": "expiration_timestamp"
}
```

### Role-Based Permissions
- **User Role**: Can manage own tasks, view own profile
- **Admin Role**: Full access to all tasks and user management

### Security Features
- Password hashing with bcrypt (12 salt rounds)
- JWT token expiration (7 days default)
- Rate limiting (100 requests per 15 minutes)
- CORS protection
- Helmet security headers
- Input validation and sanitization

## 🗄️ Database Schema

### User Model
```javascript
{
  username: String (unique, 3-30 chars),
  email: String (unique, valid email),
  password: String (hashed, min 6 chars),
  role: String (enum: 'user', 'admin'),
  isActive: Boolean (default: true),
  createdAt: Date,
  updatedAt: Date
}
```

### Task Model
```javascript
{
  title: String (required, max 100 chars),
  description: String (required, max 500 chars),
  status: String (enum: 'pending', 'in-progress', 'completed'),
  priority: String (enum: 'low', 'medium', 'high'),
  dueDate: Date (optional),
  assignedTo: ObjectId (ref: User),
  createdBy: ObjectId (ref: User),
  createdAt: Date,
  updatedAt: Date
}
```

## 🧪 Testing the Application

### Demo Accounts
Create these accounts for testing or use the registration form:

**Admin Account:**
- Email: `admin@example.com`
- Password: `Admin123!`

**Regular User:**
- Email: `user@example.com`
- Password: `User123!`

### Testing Workflow
1. Register a new account or login with demo credentials
2. Create tasks with different priorities and statuses
3. Test role-based access (admin vs user permissions)
4. Explore the API documentation at `/api-docs`
5. Test pagination, filtering, and search functionality

## 🚀 Scalability Considerations

### Current Architecture
- **Modular Structure**: Separated concerns with middleware, models, routes
- **Database Indexing**: Optimized queries with MongoDB indexes
- **Pagination**: Efficient data loading with limit/offset
- **Caching Ready**: Structure supports Redis integration
- **Error Handling**: Centralized error management

### Future Scalability Enhancements

#### Microservices Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Auth Service  │    │   Task Service  │    │   User Service  │
│                 │    │                 │    │                 │
│ - JWT handling  │    │ - CRUD ops      │    │ - User mgmt     │
│ - User auth     │    │ - Task logic    │    │ - Role mgmt     │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 │
                    ┌─────────────────┐
                    │   API Gateway   │
                    │                 │
                    │ - Rate limiting │
                    │ - Load balancing│
                    │ - Request routing│
                    └─────────────────┘
```

#### Caching Strategy
- **Redis**: Session storage and frequently accessed data
- **Application-level**: In-memory caching for static data
- **Database**: Query result caching

#### Load Balancing
- **Horizontal Scaling**: Multiple server instances
- **Database Sharding**: Distribute data across multiple databases
- **CDN**: Static asset delivery

#### Monitoring & Logging
- **Application Monitoring**: Performance metrics
- **Error Tracking**: Centralized error logging
- **Health Checks**: Service availability monitoring

## 🐳 Docker Deployment

### Docker Compose Setup
```yaml
version: '3.8'
services:
  mongodb:
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db

  backend:
    build: .
    ports:
      - "5000:5000"
    environment:
      - MONGODB_URI=mongodb://mongodb:27017/scalable-api
    depends_on:
      - mongodb

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend

volumes:
  mongodb_data:
```

## 📊 Performance Metrics

### API Response Times (Target)
- Authentication: < 200ms
- Task CRUD: < 150ms
- User Management: < 100ms
- Database Queries: < 50ms

### Scalability Targets
- **Concurrent Users**: 1000+
- **Requests per Second**: 500+
- **Database Records**: 1M+ tasks, 100K+ users
- **Response Time**: 95th percentile < 300ms

## 🔧 Environment Variables

```bash
# Database
MONGODB_URI=mongodb://localhost:27017/scalable-api
DB_NAME=scalable_api

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key
JWT_EXPIRES_IN=7d

# Server
PORT=5000
NODE_ENV=development

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100

# CORS
FRONTEND_URL=http://localhost:3000
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Developer

**Backend Developer Intern Assignment**
- Scalable REST API with Authentication
- Role-Based Access Control
- Modern Frontend Integration
- Production-Ready Architecture

---

## 🎯 Assignment Completion Checklist

### ✅ Backend Requirements
- [x] User registration & login APIs with password hashing
- [x] JWT authentication implementation
- [x] Role-based access (user vs admin)
- [x] CRUD APIs for tasks entity
- [x] API versioning (/api/v1/)
- [x] Comprehensive error handling
- [x] Input validation and sanitization
- [x] API documentation (Swagger)
- [x] Database schema (MongoDB)
- [x] Security features (CORS, Helmet, Rate limiting)

### ✅ Frontend Requirements
- [x] React.js application
- [x] User registration & login UI
- [x] Protected dashboard (JWT required)
- [x] CRUD interface for tasks
- [x] Error/success message handling
- [x] Responsive design

### ✅ Security & Scalability
- [x] Secure JWT token handling
- [x] Input sanitization & validation
- [x] Scalable project structure
- [x] Production-ready configuration
- [x] Documentation for deployment

### ✅ Deliverables
- [x] GitHub repository with complete code
- [x] Working authentication & CRUD APIs
- [x] Functional frontend UI
- [x] Interactive API documentation
- [x] Comprehensive README with setup instructions
- [x] Scalability architecture notes
