# Setup Guide

This guide will help you get started with PinkFlow development quickly.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Initial Setup](#initial-setup)
- [Component-Specific Setup](#component-specific-setup)
- [Common Tasks](#common-tasks)
- [Troubleshooting](#troubleshooting)
- [Next Steps](#next-steps)

---

## Prerequisites

Before you begin, ensure you have the following installed:

### Required Tools

- **Git**: Version control
  ```bash
  git --version  # Should be 2.x or higher
  ```

- **Node.js**: For frontend and real-time services (v16 or higher)
  ```bash
  node --version  # Should be v16.x or higher
  npm --version   # Should be 7.x or higher
  ```

- **Python**: For backend services (3.8 or higher)
  ```bash
  python --version  # Should be 3.8 or higher
  pip --version     # Latest version
  ```

### Recommended Tools

- **VS Code** or your preferred IDE
- **Docker** (for containerized development)
- **Postman** or **curl** (for API testing)

---

## Initial Setup

### 1. Clone the Repository

```bash
# Clone the repository
git clone https://github.com/pinkycollie/PinkFlow.git
cd PinkFlow

# Verify the clone
ls -la
```

### 2. Explore the Project Structure

```bash
# View project overview
cat overview

# Read backend documentation
cat backend.md

# Check README
cat README.md
```

### 3. Set Up Git Configuration

```bash
# Configure your name and email
git config user.name "Your Name"
git config user.email "your.email@example.com"

# Create a feature branch
git checkout -b feature/your-feature-name
```

---

## Component-Specific Setup

### Frontend Setup (React + TypeScript)

**Status**: 🚧 Component structure to be added

When the frontend component is added:

```bash
# Navigate to frontend directory
cd frontend  # or wherever the frontend code is

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# Start development server
npm start
```

### Backend Setup (FastAPI)

**Status**: 🚧 Component structure to be added

When the backend component is added:

```bash
# Navigate to backend directory
cd backend  # or wherever the backend code is

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Linux/Mac:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# Run database migrations (when implemented)
alembic upgrade head

# Start development server
uvicorn main:app --reload
```

### PinkSync Setup (Real-time Service)

**Status**: 🚧 Component structure to be added

When the PinkSync component is added:

```bash
# Navigate to PinkSync directory
cd pinksync  # or wherever the service is

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# Start WebSocket server
npm run dev
```

---

## Common Tasks

### Running Tests

```bash
# Frontend tests (when implemented)
npm test

# Backend tests (when implemented)
pytest

# Run tests with coverage
pytest --cov
```

### Linting Code

```bash
# Frontend linting (when implemented)
npm run lint

# Backend linting (when implemented)
flake8 .
black --check .

# Fix linting issues automatically
npm run lint:fix  # Frontend
black .           # Backend
```

### Building for Production

```bash
# Frontend build (when implemented)
npm run build

# Backend build (when implemented)
# FastAPI doesn't require building, but you may want to:
# - Run tests
# - Check code quality
# - Generate API documentation
```

### Database Management

```bash
# Create a new migration (when implemented)
alembic revision --autogenerate -m "Description of changes"

# Apply migrations
alembic upgrade head

# Rollback migrations
alembic downgrade -1
```

---

## Environment Variables

### Frontend Environment Variables

Create a `.env` file in the frontend directory:

```env
# API Configuration
REACT_APP_API_URL=http://localhost:8000
REACT_APP_WS_URL=ws://localhost:3001

# Feature Flags
REACT_APP_ENABLE_GEMINI=true
REACT_APP_ENABLE_GOVERNANCE=true

# Development
REACT_APP_ENV=development
```

### Backend Environment Variables

Create a `.env` file in the backend directory:

```env
# Database
DATABASE_URL=postgresql://user:password@localhost/pinkflow

# Authentication
JWT_SECRET=your-secret-key-change-in-production
JWT_ALGORITHM=HS256
JWT_EXPIRATION_MINUTES=60

# External APIs
GEMINI_API_KEY=your-gemini-api-key

# Server
HOST=0.0.0.0
PORT=8000
DEBUG=True

# CORS
ALLOWED_ORIGINS=http://localhost:3000,http://localhost:5173
```

### PinkSync Environment Variables

Create a `.env` file in the PinkSync directory:

```env
# Server
PORT=3001
NODE_ENV=development

# Authentication
JWT_SECRET=your-secret-key-change-in-production

# Redis (for scaling)
REDIS_URL=redis://localhost:6379
```

**⚠️ Security Warning**: Never commit `.env` files to version control!

---

## Troubleshooting

### Common Issues

#### Port Already in Use

```bash
# Find process using the port
lsof -i :8000  # Replace 8000 with your port

# Kill the process
kill -9 <PID>
```

#### Module Not Found

```bash
# Frontend
rm -rf node_modules package-lock.json
npm install

# Backend
pip install --upgrade pip
pip install -r requirements.txt
```

#### Database Connection Error

1. Verify PostgreSQL is running
2. Check DATABASE_URL in .env
3. Ensure database exists
4. Check user permissions

#### CORS Errors

1. Verify ALLOWED_ORIGINS in backend .env
2. Check frontend API_URL matches backend URL
3. Ensure credentials are included in fetch requests

### Getting Help

- Check the [FAQ](https://github.com/pinkycollie/PinkFlow/wiki) (when available)
- Search [existing issues](https://github.com/pinkycollie/PinkFlow/issues)
- Join [GitHub Discussions](https://github.com/pinkycollie/PinkFlow/discussions) (when enabled)
- Read [CONTRIBUTING.md](CONTRIBUTING.md)

---

## Next Steps

After setup is complete:

1. **Read Documentation**
   - [CONTRIBUTING.md](CONTRIBUTING.md) - Contribution guidelines
   - [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) - Community standards
   - [API.md](API.md) - API documentation

2. **Explore the Codebase**
   - Understand the architecture
   - Review existing code
   - Run the application locally

3. **Pick an Issue**
   - Browse [open issues](https://github.com/pinkycollie/PinkFlow/issues)
   - Look for "good first issue" labels
   - Comment on the issue before starting work

4. **Start Contributing**
   - Create a feature branch
   - Make your changes
   - Write tests
   - Submit a pull request

---

## Development Tips

### Code Quality

- Run linters before committing
- Write meaningful commit messages
- Keep functions small and focused
- Add comments for complex logic

### Testing

- Write tests for new features
- Test edge cases
- Run full test suite before PR
- Test manually in the browser/API client

### Accessibility

- Test with screen readers
- Verify keyboard navigation
- Check color contrast
- Ensure captions/transcripts for media

### Performance

- Monitor bundle size
- Optimize database queries
- Use caching where appropriate
- Profile slow operations

---

## Useful Commands

```bash
# Git workflow
git status                              # Check status
git add .                               # Stage changes
git commit -m "message"                 # Commit changes
git push origin feature/branch-name     # Push to remote

# Package management
npm install <package>                   # Install npm package
pip install <package>                   # Install Python package

# Development servers
npm start                               # Start frontend dev server
uvicorn main:app --reload              # Start FastAPI with hot reload
node server.js                          # Start Node.js server

# Testing
npm test                                # Run frontend tests
pytest                                  # Run backend tests
npm run test:e2e                        # Run E2E tests

# Database
alembic upgrade head                    # Apply migrations
alembic downgrade -1                    # Rollback one migration
psql -d pinkflow                        # Connect to database
```

---

## Resources

- [React Documentation](https://react.dev/)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Socket.io Documentation](https://socket.io/docs/)
- [WCAG Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)

---

## Support

Need help? Here's how to get support:

1. **Documentation**: Check this guide and README.md
2. **Issues**: Search or create an [issue](https://github.com/pinkycollie/PinkFlow/issues)
3. **Discussions**: Join [GitHub Discussions](https://github.com/pinkycollie/PinkFlow/discussions) (when enabled)
4. **Community**: Connect with other contributors

---

**Welcome to PinkFlow! We're excited to have you here. 🎉**

**Last Updated**: 2025-10-17
