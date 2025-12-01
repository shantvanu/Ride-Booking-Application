# Frontend - Ride Booking App

## 📖 Overview
The frontend of this application is built with **React** and **TypeScript**, utilizing **Vite** for a lightning-fast development experience. It provides a seamless user interface for booking rides, managing driver status, and processing payments. The application is designed to be responsive and intuitive, with a focus on clean component architecture.

## ✨ Key Features
- **User Authentication**: Secure Login and Registration pages with JWT integration.
- **Ride Booking Flow**: Interactive form to select pickup and drop-off locations (simulated).
- **Real-time Status**: `BookingStatus` page updates users on their ride state (Pending, Confirmed, Completed).
- **Driver Dashboard**: Dedicated view for drivers to manage availability and view assigned rides.
- **Payment Integration**: Mock payment flow to complete bookings.
- **Responsive Design**: Optimized for various screen sizes.

## 📂 Folder Structure
```
src/
├── api/            # Axios instances and API service calls
├── assets/         # Static assets (images, icons)
├── components/     # Reusable UI components (Navbar, Inputs, Buttons)
├── pages/          # Main application views (Home, Login, Booking, etc.)
├── redux/          # Redux slices and store configuration
├── types/          # TypeScript interfaces and type definitions
├── utils/          # Helper functions and constants
├── App.tsx         # Main application component & Routing
└── main.tsx        # Entry point
```

## 🛠 Architecture & State Management
- **Redux Toolkit**: Used for global state management. We store user authentication status (`authSlice`) and current booking details (`bookingSlice`) globally to ensure data persistence across navigation.
- **TypeScript**: Strictly typed interfaces for all data models (User, Booking, Driver) ensure code reliability and easier refactoring.
- **Component Design**: Components are functional and use Hooks (`useEffect`, `useState`, `useDispatch`, `useSelector`) for logic.

## 🔐 Authentication & Security
- **JWT Handling**: Tokens received from the backend are stored in `localStorage` (or HTTP-only cookies in a full prod setup) and attached to subsequent API requests via an Axios interceptor.
- **Protected Routes**: A `ProtectedRoute` wrapper component ensures that unauthenticated users cannot access the Dashboard or Booking pages.

## 🚀 How to Run Locally
1. **Install Dependencies**:
   ```bash
   npm install
   ```
2. **Start Development Server**:
   ```bash
   npm run dev
   ```
3. **Access Application**:
   Open [http://localhost:5173](http://localhost:5173) in your browser.

## 🧪 Assumptions & Edge Cases
- **Location Data**: For this assignment, location selection is simplified (text-based or dropdown) rather than a full Google Maps integration to focus on the booking logic.
- **Payment**: The payment process is a simulation and does not process real transactions.
- **Error Handling**: Network errors and validation errors are caught and displayed to the user via toast notifications or inline messages.
