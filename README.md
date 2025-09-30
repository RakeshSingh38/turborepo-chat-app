# ⚡ Turborepo - Chat Application

Real-time chat app built with Turborepo. Monorepo with React frontend, Express backend, and WebSocket messaging.

## What it does

- Real-time chat with WebSockets
- User authentication
- Message history
- Online user indicators
- Monorepo setup with shared packages

## Project Structure

```
Turborepo/
├── apps/
│   ├── server/              # Backend API and WebSocket
│   └── web/                 # Frontend React app
├── packages/
│   ├── ui/                  # Shared UI components
│   ├── eslint-config/       # Shared configs
│   └── typescript-config/   # Shared configs
```

## Quick Start

1. Clone and install:
```bash
git clone <repository-url>
cd Turborepo
pnpm install
```

2. Set up environment:
```bash
cp .env.example .env
# Edit .env with your settings
```

3. Start everything:
```bash
pnpm dev
```

This starts:
- Web app on http://localhost:3000
- Server on http://localhost:3001

## Available Commands

```bash
pnpm dev              # Start all servers
pnpm build            # Build everything
pnpm lint             # Lint all packages
pnpm test             # Run all tests
```

## API Endpoints

```http
POST /api/auth/login      # Login
POST /api/auth/register   # Register
GET  /api/messages        # Get messages
POST /api/messages        # Send message
GET  /api/users           # Get online users
```

## WebSocket Events

- `join-room` / `leave-room`
- `send-message`
- `typing` / `stop-typing`
- `user-joined` / `user-left`
- `new-message`

## Deployment

### Docker
```dockerfile
FROM node:18-alpine AS base
WORKDIR /app
COPY package.json pnpm-lock.yaml ./
RUN npm install -g pnpm && pnpm install --frozen-lockfile

FROM base AS build
COPY . .
RUN pnpm build

FROM base AS production
COPY --from=build /app/dist ./dist
EXPOSE 3000 3001
CMD ["pnpm", "start"]
```

### Environment Variables
```bash
DATABASE_URL="postgresql://user:password@localhost:5432/chat"
JWT_SECRET="your-jwt-secret"
PORT=3001
NODE_ENV=production
```

## Tech Stack

- Frontend: Next.js, React, TypeScript
- Backend: Express.js, WebSockets
- Database: PostgreSQL/MongoDB
- Build: Turborepo, pnpm
- Styling: Tailwind CSS

## License

MIT License

---

**Made by**: Rakesh Singh  
**Email**: contact@iamrakesh.codes