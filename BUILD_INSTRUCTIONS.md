# SoloAtlas Build Instructions

## Prerequisites Required

You need to install these tools first:

### 1. Install Node.js (includes npm)
- Download from: https://nodejs.org/
- Install version 18 or higher
- This will also install npm automatically

### 2. Install Docker Desktop (Optional but Recommended)
- Download from: https://www.docker.com/products/docker-desktop/
- Required for running databases and services

## Build Steps

Once you have Node.js installed, run these commands:

### Option 1: Quick Build with Docker (Recommended)
```bash
# Navigate to project directory
cd c:\Users\arpit\OneDrive\Desktop\repo\SoloAtlas

# Build and start all services with Docker
docker-compose up --build -d

# View logs
docker-compose logs -f
```

### Option 2: Manual Build
```bash
# Navigate to project directory
cd c:\Users\arpit\OneDrive\Desktop\repo\SoloAtlas

# Install all dependencies
npm install

# Build API
cd apps/api
npm install
npm run build

# Build Web App
cd ../web
npm install
npm run build

# Return to root and build everything
cd ../..
npm run build
```

### Option 3: Development Mode
```bash
# Install dependencies
npm install

# Start development servers
npm run dev
```

## Service URLs After Build

- **Web App**: http://localhost:3000
- **API**: http://localhost:3001
- **Database**: localhost:5432 (PostgreSQL)
- **Redis**: localhost:6379
- **Meilisearch**: http://localhost:7700
- **Grafana**: http://localhost:3002

## Troubleshooting

### If you get "command not found" errors:
1. Make sure Node.js is installed: `node --version`
2. Make sure npm is available: `npm --version`
3. Restart your terminal after installing Node.js

### If Docker commands fail:
1. Make sure Docker Desktop is running
2. Check if ports are available (3000, 3001, 5432, 6379, 7700)

### If build fails:
1. Delete node_modules: `rm -rf node_modules apps/*/node_modules`
2. Clear npm cache: `npm cache clean --force`
3. Reinstall: `npm install`

## Next Steps After Build

1. Copy environment files:
   ```bash
   cp .env.example .env
   cp apps/api/.env.example apps/api/.env
   cp apps/web/.env.example apps/web/.env
   ```

2. Set up database (if using Docker):
   ```bash
   cd apps/api
   npm run db:generate
   npm run db:push
   npm run db:seed
   ```

3. Access the application at http://localhost:3000

The complete SoloAtlas platform will be ready with all 4 EPICs:
- City Discovery & Best Dates
- Trip Plan Generator  
- Transport Comparison
- Itinerary Management
