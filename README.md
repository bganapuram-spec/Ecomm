# Ecomm: E-commerce REST API

A small Node.js/Express backend for an e-commerce store. It handles users, products and orders, and stores data in MongoDB through Mongoose.

## Features

- User registration and login (login returns the user's ID)
- Create and list products
- Place orders with multiple products and quantities, and fetch a user's order history

## API

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/users/register` | Register a user (`name`, `email`, `password`) |
| `POST` | `/api/users/login` | Log in and get back the `userId` |
| `POST` | `/api/products` | Create a product (`name`, `description`, `price`, `quantity`) |
| `GET` | `/api/products` | List all products |
| `POST` | `/api/orders` | Create an order (`user`, `products: [{ product, quantity }]`); the total is computed on the server from product prices |
| `GET` | `/api/orders/user/:userId` | Get all orders for a user |

## Data model

- **User**: `name`, `email` (unique), `password`
- **Product**: `name`, `description`, `price`, `quantity`
- **Order**: `user` → User, `products[]` → `{ product → Product, quantity }`, `total`, `createdAt`

## Project structure

```
app.js            # Express app, route mounting, MongoDB connection
controllers/      # user, product, order handlers
models/           # Mongoose schemas
routes/           # Express routers
```

## Getting started

1. Install dependencies:

   ```bash
   npm install
   ```

2. Create a `config.js` in the project root. `app.js` expects it, but it isn't committed:

   ```js
   module.exports = {
     mongoURI: 'mongodb://localhost:27017/ecomm',
   };
   ```

3. Start the server (default port `5000`, or set `PORT`):

   ```bash
   node app.js
   ```

## Roadmap

- Hash passwords with `bcryptjs` (already a dependency)
- Issue JWTs on login with `jsonwebtoken` (already a dependency) and protect the product and order routes
- Move configuration into `.env` with `dotenv`

## Tech stack

Node.js · Express · MongoDB · Mongoose
