# E-commerce API Project

This project provides a complete REST API for user authentication, product management, cart, orders, and admin operations.

## Features

- User registration and login
- JWT authentication with protected routes
- Password hashing with bcrypt
- User profile API
- Product CRUD and listing
- Product categories and search/filtering
- Cart management
- Order placement and tracking
- Admin dashboard and user management
- Validation with express-validator
- MongoDB models and Mongoose schemas

## Tech Stack

- Node.js
- Express.js
- MongoDB + Mongoose
- JWT
- bcryptjs
- express-validator

## Installation

1. Install dependencies:
   npm install
2. Create a local environment file:
   cp .env.example .env
3. Update MongoDB URL and JWT secret values in .env
4. Start the server:
   npm run dev

## Environment Variables

PORT=5000
MONGO_URI=mongodb://localhost:27017/event-store
JWT_SECRET=change_this_super_secret_key
JWT_EXPIRES_IN=7d

## API Routes

### Auth

- POST /api/auth/register
- POST /api/auth/login
- POST /api/auth/admin-login
- GET /api/auth/profile

### Products

- GET /api/products
- GET /api/products/:id
- POST /api/products
- PUT /api/products/:id
- DELETE /api/products/:id
- GET /api/products/categories

### Cart

- GET /api/cart
- POST /api/cart
- PUT /api/cart/:productId
- DELETE /api/cart/:productId

### Orders

- POST /api/orders
- GET /api/orders
- GET /api/orders/:id
- PUT /api/orders/:id/status
- DELETE /api/orders/:id/cancel

### Admin

- POST /api/admin/login
- GET /api/admin/users
- GET /api/admin/products
- GET /api/admin/orders
- GET /api/admin/dashboard
- POST /api/admin/categories

## Sample API Requests

### Register user

curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Alice Johnson",
    "email": "alice@example.com",
    "password": "secret123"
  }'

### Login user

curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "alice@example.com",
    "password": "secret123"
  }'

### Get products with filters

curl "http://localhost:5000/api/products?category=electronics&minPrice=100&maxPrice=500&search=laptop&sort=-price&page=1&limit=10"

### Add product (admin only)

curl -X POST http://localhost:5000/api/products \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Gaming Laptop",
    "description": "High performance laptop",
    "price": 1499,
    "category": "66c0d7e7e903d7a63f7be5d8",
    "stock": 5
  }'

### Place order

curl -X POST http://localhost:5000/api/orders \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "shippingAddress": {
      "street": "12 Main Street",
      "city": "New York",
      "country": "USA",
      "postalCode": "10001"
    },
    "paymentMethod": "card"
  }'

## Notes

- Admin users are created by setting the role field to admin when creating the user or by a database seed script.
- The project is ready to be extended with frontend integration, pagination UI, or additional validation logic.
