# API Documentation - PhoneShop Pro Edition

Complete API reference for PhoneShop Pro Edition backend.

## Base URL

```
http://localhost:3000/api
```

## Authentication

All API requests require authentication via JWT token.

### Login

```http
POST /auth/login
Content-Type: application/json

{
  "email": "jsadala35@gmail.com",
  "password": "your_password"
}
```

**Response:**

```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "user": {
    "id": "user_123",
    "email": "jsadala35@gmail.com",
    "role": "admin"
  }
}
```

### Using Token

Include token in request headers:

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

## API Endpoints

### Dashboard

#### Get Dashboard Stats

```http
GET /dashboard/stats
```

**Response:**

```json
{
  "totalDevices": 1250,
  "totalRevenue": 25500000,
  "totalSales": 85,
  "totalCustomers": 340,
  "monthlyRevenue": 5200000,
  "devicesSold": 45,
  "topBrands": [
    {"brand": "Samsung", "count": 320},
    {"brand": "iPhone", "count": 280}
  ]
}
```

### Inventory (Hifadhi)

#### List Devices

```http
GET /inventory/devices?page=1&limit=20&search=iphone
```

**Response:**

```json
{
  "success": true,
  "data": [
    {
      "id": "device_123",
      "brand": "Apple",
      "model": "iPhone 13 Pro",
      "imei": "351234567890123",
      "price": 1500000,
      "quantity": 5,
      "dateAdded": "2024-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "total": 150,
    "page": 1,
    "limit": 20
  }
}
```

#### Add Device

```http
POST /inventory/devices
Content-Type: application/json

{
  "brand": "Samsung",
  "model": "Galaxy S21",
  "imei": "352341234567890",
  "price": 1200000,
  "quantity": 10
}
```

#### Update Device

```http
PUT /inventory/devices/device_123
Content-Type: application/json

{
  "price": 1300000,
  "quantity": 8
}
```

#### Delete Device

```http
DELETE /inventory/devices/device_123
```

### Sales (Mauzo)

#### Create Sale

```http
POST /sales/transactions
Content-Type: application/json

{
  "customerId": "customer_123",
  "deviceId": "device_123",
  "quantity": 1,
  "price": 1500000,
  "paymentMethod": "cash",
  "notes": "Regular customer"
}
```

**Response:**

```json
{
  "success": true,
  "transaction": {
    "id": "transaction_123",
    "amount": 1500000,
    "date": "2024-06-16T12:00:00Z",
    "status": "completed"
  }
}
```

#### Get Sales History

```http
GET /sales/transactions?startDate=2024-01-01&endDate=2024-06-30&page=1
```

### Customers (Watumiaji)

#### List Customers

```http
GET /customers?page=1&limit=20&search=john
```

#### Add Customer

```http
POST /customers
Content-Type: application/json

{
  "name": "John Doe",
  "phone": "255673409790",
  "email": "john@example.com",
  "location": "Dar es Salaam"
}
```

#### Get Customer Details

```http
GET /customers/customer_123
```

**Response:**

```json
{
  "success": true,
  "customer": {
    "id": "customer_123",
    "name": "John Doe",
    "phone": "255673409790",
    "email": "john@example.com",
    "totalPurchases": 5,
    "totalSpent": 7500000,
    "lastPurchase": "2024-06-15T14:30:00Z"
  }
}
```

### Returns & Exchanges (Kurundisha)

#### Create Return

```http
POST /returns/create
Content-Type: application/json

{
  "transactionId": "transaction_123",
  "deviceId": "device_123",
  "reason": "Defective unit",
  "replacementId": "device_456"
}
```

#### Get Return History

```http
GET /returns/history?page=1&limit=20
```

### Reports (Ripoti)

#### Get Sales Report

```http
GET /reports/sales?startDate=2024-01-01&endDate=2024-06-30&groupBy=monthly
```

#### Get Inventory Report

```http
GET /reports/inventory?lowStockOnly=true
```

#### Get Financial Report

```http
GET /reports/financial?month=6&year=2024
```

### Users (Usajili)

#### List Users

```http
GET /users?role=staff
```

#### Create User

```http
POST /users
Content-Type: application/json

{
  "name": "Staff Member",
  "email": "staff@phoneshop.tz",
  "phone": "255700000000",
  "role": "staff",
  "password": "SecurePassword123!"
}
```

## Error Handling

### Error Response Format

```json
{
  "success": false,
  "error": "Invalid request",
  "code": "INVALID_REQUEST",
  "details": "Email is required"
}
```

### Common Error Codes

| Code | Status | Description |
|------|--------|-------------|
| UNAUTHORIZED | 401 | Invalid or missing token |
| FORBIDDEN | 403 | Insufficient permissions |
| NOT_FOUND | 404 | Resource not found |
| INVALID_REQUEST | 400 | Invalid request parameters |
| SERVER_ERROR | 500 | Internal server error |

## Rate Limiting

- Rate limit: 100 requests per minute
- Headers returned:
  - `X-RateLimit-Limit: 100`
  - `X-RateLimit-Remaining: 95`
  - `X-RateLimit-Reset: 1624892400`

## Pagination

Default page size: 20 items
Max page size: 100 items

```http
GET /inventory/devices?page=2&limit=50
```

## Data Types

- **TZS**: Tanzanian Shilling (amount in cents)
- **Date**: ISO 8601 format (YYYY-MM-DD)
- **DateTime**: ISO 8601 format (YYYY-MM-DDTHH:mm:ssZ)
- **Phone**: E.164 format (+255...)

## Webhooks

Webhooks for real-time events (optional):

```json
{
  "event": "sale.completed",
  "timestamp": "2024-06-16T12:00:00Z",
  "data": {
    "transactionId": "transaction_123",
    "amount": 1500000
  }
}
```

## Support

For API issues:
- Email: jsadala35@gmail.com
- Phone: +255 673 409 790

---

**Last Updated:** June 2026
