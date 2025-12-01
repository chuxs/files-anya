# Student TradeHub – Frontend

This is the **frontend** of the Student TradeHub project — a student-only marketplace platform built for Memorial University students to buy, sell, and trade items safely within their community.

## 🧭 Overview

The frontend is built using **Next.js 15** (App Router) and **Tailwind CSS v4**, providing a responsive and modern interface for browsing, posting, and managing listings. It connects to a Node.js backend via a REST API.

---

## ⚙️ Tech Stack

-   **Framework:** [Next.js 15.5.4](https://nextjs.org/) (App Router)
-   **Language:** JavaScript (React 19)
-   **Styling:** [Tailwind CSS v4](https://tailwindcss.com/)
-   **Icons:** [React Icons](https://react-icons.github.io/react-icons/)
-   **State Management:** React Context API (`AuthContext`, `SearchContext`)
-   **Authentication:** JWT-based (Custom implementation)
-   **Build Tool:** Turbopack (via Next.js)

---

## � Project Structure

The project follows the Next.js App Router structure. Here is a detailed breakdown of the key directories and files:

### `app/`
Contains the application routes and pages.
-   **`layout.js`**: The root layout that wraps the entire application. It includes global providers (`AuthProvider`, `SearchProvider`) and the `Navbar`.
-   **`page.js`**: The landing page of the application.
-   **`login/` & `signup/`**: Authentication pages.
-   **`forgot-password/` & `reset-password/`**: Password recovery flow.
-   **`products/`**: Dynamic routes for product details (e.g., `products/[id]`).
-   **`buy/`**: The marketplace browsing page with filters.
-   **`sell/`**: Form for listing new items.
-   **`orders/`**: Order management for buyers and sellers.
-   **`checkout/`**: Payment and order confirmation flow.
-   **`address/`**: Address management page.
-   **`payment/`**: Payment method management page.

### `components/`
Reusable UI components used across the application.
-   **`Navbar.jsx`**: The main navigation bar. It handles:
    -   Navigation links (Buy, Sell, Orders).
    -   Search input (updates `SearchContext`).
    -   Context-aware filters (shows different filters on Buy vs. Sell pages).
    -   User profile dropdown and logout.
-   **`ProductCard.jsx`**: Displays individual product summaries in lists.
-   **`ProductForm.jsx`**: A reusable form for creating and editing listings.
-   **`ProductManagementCard.jsx`**: Card component for managing user's own listings.
-   **`EditProfile.jsx`**: Modal for updating user information.
-   **`AddPaymentMethod.jsx`**: Form for adding new payment methods.
-   **`ProtectedRoute.js`**: Higher-order component/wrapper to protect routes requiring authentication.

### `context/`
React Context providers for global state management.
-   **`AuthContext.js`**: Manages user authentication state.
    -   Checks for a valid JWT token in `localStorage` on app mount.
    -   Provides `user`, `loading`, `login`, `signup`, and `logout` to the app.
-   **`SearchContext.js`**: Manages global search and filter state.
    -   Stores `searchTerm`, `selectedCategory`, `selectedCondition`, and `selectedStatus`.
    -   Allows the `Navbar` search bar to filter results on the `buy` and `sell` pages.

### `libs/`
Utility functions and API helpers.
-   **`auth.js`**: Contains `fetch` wrappers for authentication endpoints (`/api/auth/login`, `/api/auth/signup`, etc.).
-   **`utlis.js`**: General utility functions (e.g., formatting dates, currency).

---

## �🚀 Getting Started

### 1. Prerequisites
-   Node.js (v18 or higher recommended)
-   npm or yarn

### 2. Clone the repository
```bash
git clone https://github.com/<your-team>/StudentTradeHub.git
cd StudentTradeHub/Web\ Application/frontend
```

### 3. Install dependencies
```bash
npm install
```

### 4. Run Development Server
Start the development server with Turbopack for faster HMR:
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

### 5. Build for Production
To create an optimized production build:
```bash
npm run build
npm start
```

---

## 🔑 Key Features & Implementation Details

### 🔐 Authentication
Authentication is handled via **JWT (JSON Web Tokens)**.
1.  **Login/Signup**: Users submit credentials via `libs/auth.js`.
2.  **Token Storage**: On success, the JWT is stored in `localStorage`.
3.  **Session Persistence**: `AuthContext` checks for this token on initialization. If valid, it fetches user details (`/api/auth/me`) and sets the `user` state.
4.  **Protection**: Protected routes (like `/sell` or `/orders`) check the `user` state and redirect to `/login` if not authenticated.

### 🔍 Search & Filtering
The search functionality is global and persistent across the `buy` and `sell` pages.
-   **State**: Managed by `SearchContext`.
-   **Input**: The search bar in `Navbar` updates the context.
-   **Filtering**: The `buy` page subscribes to `SearchContext` to filter the displayed product list in real-time.
-   **Dynamic Filters**: The `Navbar` detects the current route (using `usePathname`) and displays relevant filters (e.g., "Status" filter is only shown on the `/sell` page).

### 📱 Responsive Design
The UI is fully responsive, built with Tailwind CSS.
-   **Mobile**: Shows a bottom navigation bar or simplified menu.
-   **Desktop**: Full navigation bar with expanded search and profile options.

---

## 🛠️ Development Guidelines

### Adding a New Page
Create a new folder in `app/` with a `page.js` file.
```javascript
// app/newpage/page.js
export default function NewPage() {
  return <div>My New Page</div>;
}
```
The route will be accessible at `/newpage`.

### Using Authentication in Components
Use the `useAuth` hook to access user data or auth methods.
```javascript
import { useAuth } from '@/context/AuthContext';

export default function MyComponent() {
  const { user, logout } = useAuth();

  if (!user) return <p>Please log in.</p>;

  return <button onClick={logout}>Logout {user.firstName}</button>;
}
```

### Styling
Use **Tailwind CSS** utility classes.
-   Global styles are in `app/globals.css`.
-   Avoid inline styles; use Tailwind classes for consistency (e.g., `text-slate-900`, `bg-white`).

---

## 👥 Contributors

-   Olaiya Oluwatomisin – tomisiiiin
-   Labib Islam – labib-islam
-   Nafiur Rahman – Nafiur-rhyme
-   Anya Anya – Chuxs
-   Md Minhajul Abedin – Minhajul99
-   Yi Zhang – 1mag1ne1
-   Yixuan Liu – Yixuan-Liu1
