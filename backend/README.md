# Quiz Management System - Backend

A comprehensive role-based quiz and poll management system backend built with Node.js, Express, and MySQL.

## Features

- 🔐 **Role-based Authentication** (Admin, Professor, Student)
- 📝 **Quiz Management** with multiple question types
- 👥 **Class Management** with student enrollment
- 📊 **Real-time Analytics** and reporting
- 🔍 **Comprehensive Audit Logging**
- 📁 **File Upload/Download** capabilities
- 🛡️ **Security Features** (Rate limiting, CORS, Helmet)

## Prerequisites

- Node.js (v14 or higher)
- MySQL (v8.0 or higher)
- npm or yarn package manager

## Installation

1. **Clone the repository and navigate to backend:**
   ```bash
   cd backend
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Set up environment variables:**
   ```bash
   cp .env.example .env
   ```
   
   Edit `.env` file with your configuration:
   ```env
   DB_HOST=localhost
   DB_USER=root
   DB_PASSWORD=your_password
   DB_NAME=quiz_management
   JWT_SECRET=your-super-secret-key
   ```

4. **Set up the database:**
   ```bash
   # Create database
   mysql -u root -p -e "CREATE DATABASE quiz_management;"
   
   # Run migrations
   npm run migrate
   
   # Seed sample data (optional)
   npm run seed
   ```

## Usage

### Development Mode
```bash
npm run dev
```

### Production Mode
```bash
npm start
```

### Testing
```bash
# Test API endpoints
node test-api.js
```

## API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/verify` - Verify JWT token
- `POST /api/auth/logout` - User logout
- `POST /api/auth/change-password` - Change password

### Users (Admin only)
- `GET /api/users` - Get all users
- `GET /api/users/:id` - Get user by ID
- `PUT /api/users/:id` - Update user
- `DELETE /api/users/:id` - Delete user
- `PUT /api/users/:id/role` - Update user role

### Classes (Professor)
- `GET /api/classes` - Get user's classes
- `POST /api/classes` - Create new class
- `PUT /api/classes/:id` - Update class
- `DELETE /api/classes/:id` - Delete class
- `POST /api/classes/:id/students` - Add student to class
- `DELETE /api/classes/:id/students/:studentId` - Remove student

### Quizzes (Professor)
- `GET /api/quizzes` - Get user's quizzes
- `POST /api/quizzes` - Create new quiz
- `GET /api/quizzes/:id` - Get quiz details
- `PUT /api/quizzes/:id` - Update quiz
- `DELETE /api/quizzes/:id` - Delete quiz
- `GET /api/quizzes/:id/results` - Get quiz results

### Submissions (Student)
- `POST /api/submissions/start` - Start quiz submission
- `POST /api/submissions/answer` - Submit answer
- `POST /api/submissions/complete` - Complete submission
- `GET /api/submissions/my-submissions` - Get user's submissions

### Admin
- `GET /api/admin/dashboard` - Admin dashboard data
- `GET /api/admin/analytics` - System analytics
- `GET /api/admin/audit-logs` - Audit logs
- `GET /api/admin/export` - Export data

## Database Schema

### Core Tables
- `users` - User accounts and authentication
- `classes` - Course/class information
- `quizzes` - Quiz definitions and settings
- `questions` - Individual quiz questions
- `quiz_submissions` - Student quiz attempts
- `submission_answers` - Individual question answers
- `audit_logs` - System activity tracking

## Security Features

- **JWT Authentication** with configurable expiration
- **Rate Limiting** to prevent abuse
- **CORS Protection** with configurable origins
- **Password Hashing** with bcrypt
- **Input Validation** and sanitization
- **Audit Logging** for all activities

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `DB_HOST` | Database host | localhost |
| `DB_USER` | Database username | root |
| `DB_PASSWORD` | Database password | (required) |
| `DB_NAME` | Database name | quiz_management |
| `DB_PORT` | Database port | 3306 |
| `PORT` | Server port | 5000 |
| `JWT_SECRET` | JWT signing secret | (required) |
| `JWT_EXPIRES_IN` | JWT expiration time | 24h |
| `CORS_ORIGIN` | CORS allowed origin | http://localhost:3000 |
| `NODE_ENV` | Environment mode | development |

## Error Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request / Validation Error |
| 401 | Unauthorized / Authentication Required |
| 403 | Forbidden / Access Denied |
| 404 | Not Found |
| 409 | Conflict / Duplicate Resource |
| 429 | Too Many Requests |
| 500 | Internal Server Error |

## Troubleshooting

### Common Issues

1. **Database Connection Failed**
   ```bash
   # Check MySQL is running
   sudo systemctl status mysql
   
   # Verify credentials in .env file
   # Test connection manually
   mysql -u root -p
   ```

2. **AuditLogger.logAuthentication is not a function**
   - Fixed in latest version
   - Ensure proper import: `const AuditLogger = require('./middleware/auditLogger')`

3. **Invalid configuration option warnings**
   - Remove deprecated MySQL2 options
   - Use only supported connection parameters

4. **CORS Errors**
   ```bash
   # Update CORS_ORIGIN in .env
   CORS_ORIGIN=http://localhost:3000
   ```

5. **JWT Secret Warning**
   ```bash
   # Set a strong JWT secret
   JWT_SECRET=your-256-bit-secret-key-here
   ```

### Database Reset
```bash
# Drop and recreate database
mysql -u root -p -e "DROP DATABASE IF EXISTS quiz_management; CREATE DATABASE quiz_management;"

# Re-run migrations
npm run migrate
npm run seed
```

### Logs
```bash
# View server logs
npm start

# Enable debug logging
LOG_LEVEL=debug npm start
```

## Project Structure

```
backend/
├── src/
│   ├── config/
│   │   ├── config.js          # Application configuration
│   │   └── database.js        # Database connection and helpers
│   ├── middleware/
│   │   ├── auth.js            # JWT authentication middleware
│   │   ├── auditLogger.js     # Activity logging middleware
│   │   └── errorHandler.js    # Global error handling
│   ├── routes/
│   │   ├── auth.js           # Authentication routes
│   │   ├── users.js          # User management routes
│   │   ├── classes.js        # Class management routes
│   │   ├── quizzes.js        # Quiz management routes
│   │   ├── submissions.js    # Quiz submission routes
│   │   └── admin.js          # Admin panel routes
│   └── server.js             # Main application entry point
├── database/
│   ├── migrations/
│   │   └── migrate.js        # Database schema setup
│   └── seeds/
│       └── seed.js           # Sample data insertion
├── test-api.js               # API testing script
├── package.json              # Dependencies and scripts
└── README.md                 # This file
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is licensed under the ISC License.

## Support

For issues and questions:
1. Check the troubleshooting section
2. Review server logs
3. Test with the provided test script
4. Create an issue with full error details 