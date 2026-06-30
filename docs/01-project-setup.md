# Day 1 - Project Setup

## Objective

Set up the initial backend project using NestJS with PostgreSQL, Prisma, Docker, and development tooling.

---

## Tech Stack

- NestJS
- TypeScript
- PostgreSQL
- Prisma ORM
- Docker & Docker Compose
- ESLint
- Prettier
- Swagger
- class-validator
- class-transformer

---

## 1. Initialize NestJS Project

### Command

```bash
nest new dev-flow-api
```

### Result

- Created the NestJS project.
- Installed dependencies.
- Generated the initial folder structure.

---

## 2. Configure ESLint & Prettier

### Installed

```bash
bun add -D prettier eslint-config-prettier eslint-plugin-prettier
```

### Configuration

- Added `.prettierrc`
- Added `.prettierignore`
- Updated ESLint configuration to avoid conflicts with Prettier.

### Result

- Consistent code formatting.
- Automatic linting support.

---

## 3. Setup PostgreSQL with Docker

### docker-compose.yml

```yaml
services:
  postgres:
    image: postgres:16
    restart: always
    ports:
      - '5432:5432'
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
      POSTGRES_DB: nestdb
```

### Start Database

```bash
docker compose up -d
```

### Result

- PostgreSQL running inside Docker.
- Database accessible on localhost:5432.

---

## 4. Configure Prisma

### Install

```bash
npm install prisma @prisma/client
```

```bash
npx prisma init
```

### Updated

- schema.prisma
- DATABASE_URL

### Result

Prisma connected successfully to PostgreSQL.

---

## 5. Create First Migration

### Schema

Created initial model(s).

Example:

```prisma
model User {
  id    Int @id @default(autoincrement())
  email String @unique
}
```

### Migration

```bash
npx prisma migrate dev --name init
```

### Result

- Database tables created.
- Prisma Client generated.

---

## 6. Configure Environment Variables

Created

```
.env
```

Example

```env
DATABASE_URL="postgresql://postgres:password@localhost:5432/nestdb"
PORT=3000
```

Result

Application configuration separated from source code.

---

## 7. Global Configuration Module

Installed

```bash
npm install @nestjs/config
```

Configured

```ts
ConfigModule.forRoot({
  isGlobal: true,
});
```

Result

Environment variables are available throughout the application.

---

## 8. Swagger Setup

Installed

```bash
npm install @nestjs/swagger swagger-ui-express
```

Configured Swagger in `main.ts`.

Access

```
http://localhost:3000/api
```

Result

Interactive API documentation available.

---

## 9. Global Validation Pipe

Configured

```ts
app.useGlobalPipes(
  new ValidationPipe({
    whitelist: true,
    transform: true,
    forbidNonWhitelisted: true,
  }),
);
```

Result

- Automatic request validation
- Removes unwanted fields
- Converts payload types automatically

---

## 10. Verification

Verified the following:

- NestJS server starts successfully.
- PostgreSQL container is running.
- Prisma migration completed.
- Prisma Client generated.
- Swagger UI accessible.
- Validation pipe working.
- Environment variables loaded correctly.

---

# Folder Structure

```
dist
docs
test
src/
prisma/
docker-compose.yml
.env
package.json
```

---

# Challenges Faced

| Issue                            | Solution                                   |
| -------------------------------- | ------------------------------------------ |
| Example: Prisma couldn't connect | Verified DATABASE_URL and restarted Docker |

---

# Commands Used

```bash
nest new dev-flow-api
docker compose up -d
bunx prisma init
bunx prisma migrate dev --name init
bun run start:dev
```

---

# Outcome

The backend project is fully configured and ready for feature development. The application now includes:

- NestJS project structure
- PostgreSQL database
- Docker environment
- Prisma ORM
- Global configuration
- Swagger API documentation
- Request validation
- Code formatting and linting
