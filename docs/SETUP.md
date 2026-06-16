# Setup Guide - PhoneShop Pro Edition

This guide will help you set up the PhoneShop Pro Edition development environment.

## Prerequisites

- **Node.js**: Version 16.x or higher
- **npm**: Version 8.x or higher (or yarn 1.22+)
- **Git**: For version control
- **Database**: PostgreSQL 12+
- **Git Account**: GitHub account for repository access

## System Requirements

### Minimum
- 4GB RAM
- 2GB free disk space
- Modern web browser (Chrome, Firefox, Safari, Edge)

### Recommended
- 8GB RAM
- 5GB free disk space
- Latest stable Node.js LTS

## Installation Steps

### 1. Clone Repository

```bash
git clone https://github.com/jsadala35-ops/phoneshop-tanzania.git
cd phoneshop-tanzania
```

### 2. Install Dependencies

```bash
npm install
```

Or with yarn:

```bash
yarn install
```

### 3. Configure Environment

```bash
# Copy example environment file
cp .env.example .env.local

# Edit with your settings
nano .env.local
```

### 4. Database Setup

```bash
# Create database
createdb phoneshop_db

# Run migrations (if applicable)
npm run migrate

# Seed initial data (optional)
npm run seed
```

### 5. Start Development Server

```bash
npm run dev
```

The application will be available at: `http://localhost:3000`

## Verification

### Check Installation

```bash
# Verify Node.js
node --version
# Expected: v16.0.0 or higher

# Verify npm
npm --version
# Expected: 8.0.0 or higher

# Verify dependencies
npm list
```

### Login

1. Open `http://localhost:3000`
2. Admin credentials (from `.env.local`):
   - Email: jsadala35@gmail.com
   - Password: (set in .env.local)

## Development Workflow

### Available Commands

```bash
# Start development server
npm run dev

# Build for production
npm run build

# Start production server
npm run start

# Run tests
npm test

# Run linting
npm run lint

# Format code
npm run format

# Run database migrations
npm run migrate

# Seed database
npm run seed
```

## Troubleshooting

### Port Already in Use

```bash
# Run on different port
PORT=3001 npm run dev
```

### Database Connection Error

```bash
# Check PostgreSQL is running
sudo systemctl status postgresql

# Verify connection string in .env.local
echo $DATABASE_URL
```

### Node Modules Issues

```bash
# Clear npm cache
npm cache clean --force

# Remove node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

## IDE Setup

### VS Code

1. Install extensions:
   - ES7+ React/Redux/React-Native snippets
   - Prettier - Code formatter
   - ESLint
   - Thunder Client or REST Client

2. Settings (`.vscode/settings.json`):

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

## Docker Setup (Optional)

```dockerfile
FROM node:16-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000
CMD ["npm", "run", "dev"]
```

```bash
# Build Docker image
docker build -t phoneshop-tz .

# Run container
docker run -p 3000:3000 phoneshop-tz
```

## Next Steps

1. Read [API Documentation](API.md)
2. Review [Module Guide](MODULES.md)
3. Check [Architecture](ARCHITECTURE.md)
4. Read [Contributing Guidelines](../CONTRIBUTING.md)

## Support

- Email: jsadala35@gmail.com
- Phone: +255 673 409 790
- GitHub Issues: https://github.com/jsadala35-ops/phoneshop-tanzania/issues

---

**Last Updated:** June 2026
