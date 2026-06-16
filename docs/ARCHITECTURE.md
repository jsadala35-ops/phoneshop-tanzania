# Architecture - PhoneShop Pro Edition

System architecture and technical design documentation.

## System Overview

```
┌─────────────────────────────────────────────────────┐
│                   Client Layer                       │
│              (React/Next.js Frontend)                │
└──────────────────┬──────────────────────────────────┘
                   │
                   │ HTTP/HTTPS
                   ▼
┌─────────────────────────────────────────────────────┐
│               API Layer (Express)                    │
│   - Authentication & Authorization                  │
│   - Request Validation                              │
│   - Error Handling                                  │
└──────────────────┬──────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────┐
│            Business Logic Layer                      │
│   - Dashboard Service                               │
│   - Inventory Service                               │
│   - Sales Service                                   │
│   - Customer Service                                │
│   - Return Service                                  │
│   - Reporting Service                               │
└──────────────────┬──────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────┐
│            Data Access Layer (ORM)                   │
│              - Database Queries                     │
│              - Caching                              │
└──────────────────┬──────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────┐
│         Database Layer (PostgreSQL)                 │
│   - Inventory Tables                                │
│   - Sales Tables                                    │
│   - Customer Tables                                 │
│   - User Tables                                     │
│   - Transaction Tables                              │
└─────────────────────────────────────────────────────┘
```

## Frontend Architecture

### Technology Stack
- **Framework**: Next.js 12+
- **State Management**: Redux or Context API
- **UI Library**: React Components
- **Styling**: CSS/SCSS/Tailwind CSS
- **Form Management**: React Hook Form
- **HTTP Client**: Axios

### Directory Structure

```
src/
├── components/
│   ├── Common/          # Reusable components
│   ├── Dashboard/       # Dashboard components
│   ├── Inventory/       # Inventory module components
│   ├── Sales/          # Sales module components
│   └── ...
├── pages/
│   ├── api/            # API routes
│   ├── dashboard/
│   ├── inventory/
│   ├── sales/
│   └── ...
├── store/              # Redux or Context
├── services/           # API services
├── hooks/              # Custom React hooks
├── styles/             # Global styles
└── utils/              # Utility functions
```

## Backend Architecture

### Technology Stack
- **Runtime**: Node.js
- **Framework**: Express.js or Next.js API Routes
- **Database**: PostgreSQL
- **ORM**: Sequelize or Prisma
- **Authentication**: JWT (JSON Web Tokens)
- **Validation**: Joi or Yup

### API Structure

```
api/
├── middleware/
│   ├── auth.js         # JWT authentication
│   ├── validation.js   # Request validation
│   └── error.js        # Error handling
├── routes/
│   ├── auth.js         # Authentication routes
│   ├── dashboard.js    # Dashboard routes
│   ├── inventory.js    # Inventory routes
│   ├── sales.js        # Sales routes
│   ├── customers.js    # Customer routes
│   ├── returns.js      # Return routes
│   ├── reports.js      # Reporting routes
│   └── users.js        # User management routes
├── controllers/        # Route handlers
├── models/            # Database models
├── services/          # Business logic
└── utils/             # Utility functions
```

## Database Schema

### Core Tables

#### Users Table
- id (UUID)
- email (String, Unique)
- passwordHash (String)
- name (String)
- phone (String)
- role (Enum: admin, manager, staff, viewer)
- active (Boolean)
- createdAt (DateTime)
- updatedAt (DateTime)

#### Devices Table
- id (UUID)
- brand (String)
- model (String)
- imei (String, Unique)
- purchasePrice (Decimal)
- sellingPrice (Decimal)
- quantity (Integer)
- supplierId (UUID, FK)
- dateAdded (DateTime)
- status (Enum: available, sold, reserved)
- createdAt (DateTime)
- updatedAt (DateTime)

#### Customers Table
- id (UUID)
- name (String)
- phone (String, Unique)
- email (String)
- address (String)
- city (String)
- idType (String)
- idNumber (String)
- dateOfBirth (Date)
- totalPurchases (Integer)
- totalSpent (Decimal)
- lastPurchaseDate (DateTime)
- createdAt (DateTime)
- updatedAt (DateTime)

#### Transactions Table
- id (UUID)
- customerId (UUID, FK)
- totalAmount (Decimal)
- paymentMethod (Enum: cash, mpesa, bank, card)
- status (Enum: pending, completed, cancelled)
- soldBy (UUID, FK)
- transactionDate (DateTime)
- notes (String)
- createdAt (DateTime)
- updatedAt (DateTime)

#### Transaction Items Table
- id (UUID)
- transactionId (UUID, FK)
- deviceId (UUID, FK)
- quantity (Integer)
- unitPrice (Decimal)
- totalPrice (Decimal)

#### Returns Table
- id (UUID)
- transactionId (UUID, FK)
- deviceId (UUID, FK)
- reason (String)
- returnDate (DateTime)
- replacementId (UUID, FK)
- refundAmount (Decimal)
- status (Enum: pending, approved, completed)
- createdAt (DateTime)
- updatedAt (DateTime)

## Authentication Flow

```
1. User enters credentials
   ↓
2. Frontend sends POST /api/auth/login
   ↓
3. Backend validates credentials
   ↓
4. Backend generates JWT token
   ↓
5. Frontend stores token in localStorage/cookie
   ↓
6. Frontend includes token in Authorization header
   ↓
7. Backend verifies token on each request
```

## Security Measures

- **Password Hashing**: bcrypt with salt rounds
- **JWT Tokens**: HS256 signature algorithm
- **HTTPS**: Encrypted data transmission
- **CORS**: Cross-origin resource sharing
- **Input Validation**: Joi schema validation
- **SQL Injection Prevention**: Parameterized queries
- **Rate Limiting**: 100 requests per minute
- **Data Encryption**: Sensitive data encryption

## Performance Optimization

### Caching Strategy
- **Client-side**: React Query, SWR
- **Server-side**: Redis caching
- **CDN**: Static asset caching

### Database Optimization
- Indexing on frequently queried columns
- Query optimization
- Connection pooling
- Pagination for large result sets

### Code Optimization
- Code splitting in React
- Lazy loading of components
- Asset minification
- Image optimization

## Deployment Architecture

### Development
- Local development server (port 3000)
- Hot module reloading
- Mock database

### Staging
- Containerized with Docker
- PostgreSQL database
- Environment variables for configuration

### Production
- Docker containers
- Load balancing
- Database replication
- Backup and disaster recovery
- Monitoring and logging

## Monitoring & Logging

- **Application Logging**: Winston or Pino
- **Error Tracking**: Sentry
- **Performance Monitoring**: New Relic or DataDog
- **Log Aggregation**: ELK Stack (Elasticsearch, Logstash, Kibana)

## Scalability

- **Horizontal Scaling**: Multiple app server instances
- **Database Scaling**: Read replicas
- **Caching**: Redis for improved performance
- **Load Balancing**: Nginx or AWS Load Balancer
- **Queue System**: Optional job queue for async tasks

## Backup & Disaster Recovery

- **Database Backups**: Daily automated backups
- **Backup Location**: Separate server/cloud storage
- **Retention**: 30-day retention policy
- **Recovery Time Objective (RTO)**: 4 hours
- **Recovery Point Objective (RPO)**: 24 hours

## Future Enhancements

- Mobile app (React Native)
- Real-time notifications (WebSocket)
- Advanced analytics (Machine Learning)
- Multi-store support
- Payment gateway integration
- Supplier management system
- Accounting integration

---

**Last Updated:** June 2026
