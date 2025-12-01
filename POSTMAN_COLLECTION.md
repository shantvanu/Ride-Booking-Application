# Postman Collection - Ride Booking App

## 📦 Collection Info
- **Name**: Ride Booking API
- **Description**: A set of requests to test the full flow of the Ride Booking application, from authentication to booking completion.

## 📥 How to Import
1. Open Postman.
2. Click **Import** (top left).
3. Paste the raw JSON content (if provided) or manually create a collection with the structure below.

## 🔑 Authentication Setup
Most endpoints require a JWT token.
1. **Environment Variable**: Create a Postman Environment with a variable `authToken`.
2. **Login Request**: In the "Tests" tab of the Login request, add:
   ```javascript
   var jsonData = pm.response.json();
   pm.environment.set("authToken", jsonData.token);
   ```
3. **Authorization**: For protected requests, set **Auth Type** to `Bearer Token` and use `{{authToken}}`.

## 📂 Endpoints Structure

### 1. Auth
- **Register User**
  - `POST {{baseUrl}}/auth/register`
  - Body:
    ```json
    {
      "name": "John Doe",
      "email": "john@example.com",
      "password": "password123",
      "role": "user"
    }
    ```
- **Login User**
  - `POST {{baseUrl}}/auth/login`
  - Body:
    ```json
    {
      "email": "john@example.com",
      "password": "password123"
    }
    ```

### 2. Bookings
- **Create Booking** (Requires Auth)
  - `POST {{baseUrl}}/booking/create`
  - Body:
    ```json
    {
      "source": "Downtown",
      "destination": "Airport",
      "vehicleType": "auto"
    }
    ```
- **Get Booking Status** (Requires Auth)
  - `GET {{baseUrl}}/booking/:bookingId`

### 3. Drivers
- **Get Available Drivers** (Requires Auth)
  - `GET {{baseUrl}}/driver/available`

## 🌍 Environment Variables
Set these in your Postman Environment:
- `baseUrl`: `http://localhost:5000`
