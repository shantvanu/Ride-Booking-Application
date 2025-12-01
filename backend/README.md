# Backend - Ride Booking API

## 📖 Overview
The backend is a robust RESTful API built with **Node.js** and **Express**, backed by **MongoDB**. It handles user authentication, ride management, driver coordination, and payment processing simulations. The architecture focuses on scalability and separation of concerns.

## 📂 Project Structure
```
src/
├── controllers/    # Request handlers (logic layer)
├── middleware/     # Auth checks, error handling, validation
├── models/         # Mongoose schemas (User, Driver, Booking)
├── routes/         # API route definitions
├── services/       # Business logic (optional, for complex operations)
├── utils/          # Logger, helper functions
├── app.ts          # Express app configuration
└── server.ts       # Server entry point
```

## 🗄 Database Schema (MongoDB)
- **User**: Stores profile info (`name`, `email`, `password` hash, `role`).
- **Driver**: Stores driver details (`vehicleType`, `licensePlate`, `status`, `currentLocation`).
- **Booking**: Core entity linking User and Driver. Contains `source`, `destination`, `fare`, `status` (PENDING, ACCEPTED, COMPLETED), and timestamps.

## 🔐 Authentication Flow
1. **Register**: User signs up; password is hashed (bcrypt).
2. **Login**: User logs in; server validates credentials and issues a **JWT**.
3. **Protected Access**: Subsequent requests include the JWT in the `Authorization` header (`Bearer <token>`). Middleware validates this token before granting access to protected routes (e.g., `/booking`).

## 📡 API Endpoints

### Auth Routes (`/auth`)
- `POST /auth/register`: Register a new user.
- `POST /auth/login`: Authenticate user and return token.

### Booking Routes (`/booking`)
- `POST /booking/create`: Create a new ride request (Protected).
- `GET /booking/:id`: Get status of a specific booking.
- `GET /booking/user/history`: Get booking history for the logged-in user.

### Driver Routes (`/driver`)
- `GET /driver/available`: List available drivers (for matching logic).
- `PUT /driver/status`: Update driver availability or location.

## 📝 Example Request/Response
**POST /booking/create**
*Request Body:*
```json
{
  "source": "Central Station",
  "destination": "Airport Terminal 1",
  "vehicleType": "sedan"
}
```
*Response (201 Created):*
```json
{
  "success": true,
  "booking": {
    "id": "64f1a2b3c4d5e6f7g8h9i0j1",
    "status": "PENDING",
    "fare": 450,
    "estimatedTime": "15 mins"
  }
}
```

## 🚀 How to Run Locally
1. **Install Dependencies**:
   ```bash
   npm install
   ```
2. **Environment Setup**:
   Create a `.env` file:
   ```env
   PORT=5000
   MONGO_URI=mongodb://127.0.0.1:27017/rideApp
   JWT_SECRET=your_secret_key
   ```
3. **Start Server**:
   ```bash
   npm run dev
   ```
   The server will start on `http://localhost:5000`.

## 🛡 Security & Error Handling
- **Input Validation**: Requests are validated before processing to prevent injection or bad data.
- **Global Error Handler**: A centralized middleware captures exceptions and returns consistent JSON error responses.
- **Password Security**: Passwords are never stored in plain text; `bcrypt` is used for hashing.
