# NestJS + Fastify + TypeORM Boilerplate

A production-ready NestJS boilerplate with Fastify, TypeORM, PostgreSQL, JWT authentication, and comprehensive API documentation.

## ✨ Features

- 🚀 **Fastify** - High-performance web framework (2x faster than Express)
- 🔐 **JWT Authentication** - Complete auth system with access & refresh tokens
- 🗄️ **TypeORM + PostgreSQL** - Type-safe database operations
- 📚 **Swagger + Scalar** - Beautiful interactive API documentation
- 🛡️ **Rate Limiting** - Built-in throttling protection
- 🎯 **Guards & Interceptors** - Global auth guards, response formatting, and logging
- ✅ **Validation** - Request validation with class-validator
- 🏥 **Health Checks** - Ready-to-use health monitoring endpoints
- 🧹 **Code Quality** - Biome for linting and formatting
- 📦 **Modular Architecture** - Clean, scalable project structure

## 🛠️ Tech Stack

- **Framework**: NestJS 11
- **Runtime**: Node.js
- **HTTP Server**: Fastify 5
- **Database**: PostgreSQL with TypeORM
- **Authentication**: JWT (access & refresh tokens)
- **Documentation**: Swagger + Scalar API Reference
- **Validation**: class-validator, class-transformer, Zod
- **Security**: bcryptjs for password hashing, throttler for rate limiting
- **Testing**: Jest

## 📋 Prerequisites

- Node.js >= 18.x
- PostgreSQL >= 14.x
- pnpm (recommended) or npm

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd nestjs-fastify-node
```

### 2. Install dependencies

```bash
pnpm install
```

### 3. Environment setup

Copy the example environment file and configure it:

```bash
cp .env.example .env
```

Edit `.env` with your configuration:

```env
NODE_ENV=development
PORT=5000
PG_URL=postgresql://postgres:password@localhost:5432/your_database
JWT_ACCESS_SECRET=your-secret-key
JWT_REFRESH_SECRET=your-refresh-secret-key
JWT_ACCESS_EXP=3600
JWT_REFRESH_EXP=3600
```

### 4. Run the application

```bash
# Development mode with hot reload
pnpm run start:dev

# Production mode
pnpm run build
pnpm run start:prod
```

The application will start on `http://localhost:5000`

### 5. Access API Documentation

Open your browser and navigate to:

```
http://localhost:5000/api/docs
```

You'll see the beautiful Scalar API documentation interface (available in development mode only).

## 📁 Project Structure

```
src/
├── config/              # Configuration files
│   ├── env.config.ts    # Environment variables
│   └── swagger.config.ts # API documentation config
├── database/            # Database configuration
│   └── database.module.ts
├── health/              # Health check endpoints
│   ├── health.controller.ts
│   └── health.module.ts
├── modules/             # Feature modules
│   ├── auth/            # Authentication module
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   ├── auth.module.ts
│   │   └── dto/         # Auth DTOs
│   └── users/           # User management module
│       ├── user.controller.ts
│       ├── user.service.ts
│       ├── user.module.ts
│       └── dto/         # User DTOs
├── shared/              # Shared utilities
│   ├── decorators/      # Custom decorators
│   ├── dtos/            # Common DTOs
│   ├── entities/        # Base entities
│   ├── enums/           # Enums
│   ├── filters/         # Exception filters
│   ├── guards/          # Auth & rate limit guards
│   ├── interceptors/    # Response & logging interceptors
│   ├── mappers/         # Data mappers
│   ├── services/        # Shared services
│   └── shared.module.ts
├── app.module.ts        # Root application module
└── main.ts              # Application entry point
```

## 📜 Available Scripts

```bash
# Development
pnpm run start          # Start in normal mode
pnpm run start:dev      # Start with hot reload
pnpm run start:debug    # Start in debug mode

# Build
pnpm run build          # Build for production

# Production
pnpm run start:prod     # Run production build

# Testing
pnpm run test           # Run unit tests
pnpm run test:watch     # Run tests in watch mode
pnpm run test:cov       # Run tests with coverage
pnpm run test:e2e       # Run end-to-end tests

# Code Quality
pnpm run format         # Format code with Prettier
pnpm run lint           # Lint and fix with ESLint
```

## 🔑 Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `NODE_ENV` | Application environment | `development` |
| `PORT` | Server port | `5000` |
| `PG_URL` | PostgreSQL connection URL | - |
| `JWT_ACCESS_SECRET` | Secret for access tokens | - |
| `JWT_REFRESH_SECRET` | Secret for refresh tokens | - |
| `JWT_ACCESS_EXP` | Access token expiry (seconds) | `3600` |
| `JWT_REFRESH_EXP` | Refresh token expiry (seconds) | `3600` |

## 🔐 Authentication

The boilerplate includes a complete JWT-based authentication system:

- **Register**: Create new user accounts with password hashing
- **Login**: Authenticate and receive access & refresh tokens
- **Token Refresh**: Renew access tokens using refresh tokens
- **Protected Routes**: Global auth guard with `@Public()` decorator for open endpoints

## 🛡️ Security Features

- **Rate Limiting**: Public endpoints are rate-limited (10 requests per minute by default)
- **Password Hashing**: Bcrypt for secure password storage
- **JWT Tokens**: Separate access and refresh token mechanism
- **Global Guards**: Authentication enforced by default
- **CORS**: Enabled for cross-origin requests
- **Validation**: Automatic request validation and sanitization

## 🏥 Health Checks

The application includes health check endpoints using `@nestjs/terminus`:

- Database connectivity check
- Memory & disk usage monitoring
- Custom health indicators

Access health endpoints at `/health` (configure in health module).

## 📖 API Documentation

API documentation is automatically generated using Swagger and displayed with Scalar:

- **Development**: Available at `/api/docs`
- **Production**: Documentation is disabled for security
- **Interactive**: Test endpoints directly from the docs
- **Type-Safe**: Auto-generated from TypeScript decorators

## 🧪 Testing

```bash
# Run all tests
pnpm run test

# Run tests in watch mode
pnpm run test:watch

# Generate coverage report
pnpm run test:cov

# Run e2e tests
pnpm run test:e2e
```

## 🚢 Deployment

### Build for production

```bash
pnpm run build
```

### Run production build

```bash
NODE_ENV=production pnpm run start:prod
```

### Docker (Optional)

Create a `Dockerfile`:

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
COPY pnpm-lock.yaml ./

RUN npm install -g pnpm
RUN pnpm install --frozen-lockfile

COPY . .

RUN pnpm run build

EXPOSE 5000

CMD ["node", "dist/main"]
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a pull request

## 📄 License

This project is licensed under the UNLICENSED license.

## 🙏 Acknowledgments

Built with [NestJS](https://nestjs.com/) - A progressive Node.js framework

---

**Happy Coding!** 🚀
