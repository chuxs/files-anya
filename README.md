# Student TradeHub – Frontend

A modern, responsive student-only marketplace platform built for Memorial University students to buy, sell, and trade items safely within their community.

---

## 🧭 Overview

The frontend provides an intuitive interface for students to browse products, manage listings, handle orders, and interact with the platform. It features a clean, minimalist design with full mobile responsiveness.

---

## ⚙️ Tech Stack

| Technology       | Version  | Purpose                         |
| ---------------- | -------- | ------------------------------- |
| **Next.js**      | 15.5.4   | React framework with App Router |
| **React**        | 19.1.0   | UI library                      |
| **Tailwind CSS** | 4.x      | Utility-first styling           |
| **React Icons**  | 5.5.0    | Icon library                    |
| **Turbopack**    | Built-in | Fast bundler for development    |

---

## 📁 Project Structure

```
frontend/
├── app/                        # Next.js App Router pages
│   ├── layout.js               # Root layout with providers
│   ├── page.js                 # Homepage (redirects to /buy)
│   ├── globals.css             # Global styles
│   ├── address/                # Address preferences page
│   ├── admin/                  # Admin dashboard
│   │   ├── layout.jsx          # Admin layout wrapper
│   │   ├── page.jsx            # Admin dashboard home
│   │   ├── products/           # Product management
│   │   └── users/              # User management
│   ├── buy/                    # Browse products page
│   ├── checkout/               # Checkout flow
│   ├── forgot-password/        # Password recovery
│   ├── login/                  # User login
│   ├── orders/                 # Order management
│   │   ├── page.jsx            # Orders list
│   │   └── [id]/               # Order details
│   ├── payment/                # Payment methods
│   ├── product/                # Product details
│   │   └── [pid]/              # Dynamic product page
│   ├── reset-password/         # Password reset
│   ├── sell/                   # Seller dashboard
│   ├── signup/                 # User registration
│   └── verify-email/           # Email verification
├── components/                 # Reusable UI components
│   ├── AddPaymentMethod.jsx    # Payment form component
│   ├── AdminRoute.js           # Admin route protection
│   ├── EditProfile.jsx         # Profile editing modal
│   ├── Navbar.jsx              # Global navigation bar
│   ├── ProductCard.jsx         # Product display card
│   ├── ProductForm.jsx         # Product create/edit form
│   ├── ReviewModal.jsx         # Review submission modal
│   ├── ReviewPrompt.jsx        # Review reminder prompt
│   └── UserRoute.js            # User route protection
├── context/                    # React Context providers
│   ├── AuthContext.js          # Authentication state
│   └── SearchContext.js        # Search & filter state
├── libs/                       # Utility functions
│   ├── auth.js                 # Authentication helpers
│   └── utlis.js                # API functions & utilities
├── next.config.mjs             # Next.js configuration
├── postcss.config.mjs          # PostCSS configuration
├── jsconfig.json               # Path aliases configuration
└── package.json                # Dependencies & scripts
```

---

## ✨ Features

### 🔐 Authentication

- JWT-based authentication with MUN email verification
- Login, signup, and password recovery flows
- Email verification requirement for new accounts
- Protected routes for authenticated users

### 🛒 Marketplace (Buy)

- Browse products from other students
- Advanced filtering by:
  - **Category**: Electronics, Books, Furniture, Clothing, Sports & Outdoors, Tools, Home & Kitchen, Other
  - **Condition**: Brand New, Like New, Good, Used, Damaged
- Real-time search functionality
- Responsive product grid layout
- Product cards with images, pricing, and seller info

### 📦 Seller Dashboard (Sell)

- Create new product listings with image upload
- Manage existing products (edit/delete)
- Filter products by status: Active, Draft, Inactive
- Track product visibility and inventory

### 🧾 Orders Management

- View orders as buyer or seller
- Track order status through fulfillment pipeline:
  - **Pickup flow**: Pending → Ready for Pickup → Picked Up
  - **Delivery flow**: Pending → Confirmed → Out for Delivery → Delivered
- Filter orders by status
- Detailed order information with product and user details

### 💳 Checkout

- Secure checkout flow with order summary
- Quantity selection with inventory validation
- Payment method management (save cards for future use)
- Delivery options:
  - **Pickup**: Collect from seller's location
  - **Delivery**: Ship to your address
- Address management with save option

### ⭐ Reviews

- Leave reviews for sellers after completed orders
- Star rating system with comments
- Review prompts for pending reviews
- Seller rating display on profiles

### 👤 User Profile

- Edit profile information (name, profile picture)
- Password change functionality
- Payment method management
- Address preferences (delivery & pickup)

### 🛡️ Admin Panel

- User management (view, suspend accounts)
- Product moderation
- Order monitoring
- Platform overview and metrics

---

## 🧩 Components

| Component          | Description                                                                   |
| ------------------ | ----------------------------------------------------------------------------- |
| `Navbar`           | Global navigation with search, filters, profile dropdown, and navigation tabs |
| `ProductCard`      | Displays product info with image, price, condition badge, and action buttons  |
| `ProductForm`      | Form for creating and editing products with image upload                      |
| `EditProfile`      | Modal for editing user profile with picture upload                            |
| `ReviewModal`      | Modal for submitting product/seller reviews                                   |
| `ReviewPrompt`     | Prompt component for pending reviews                                          |
| `UserRoute`        | HOC for protecting user-authenticated routes                                  |
| `AdminRoute`       | HOC for protecting admin-only routes                                          |
| `AddPaymentMethod` | Form for adding new payment methods                                           |

---

## 🔄 Context Providers

### AuthContext

Manages authentication state across the app:

- `user` – Current user object
- `loading` – Authentication loading state
- `login()` – Login function
- `signup()` – Registration function
- `logout()` – Logout function
- `checkAuth()` – Verify authentication status

### SearchContext

Manages search and filter state:

- `searchTerm` – Current search query
- `selectedCategory` – Active category filter
- `selectedCondition` – Active condition filter
- `selectedStatus` – Active status filter

---

## 🔌 API Utilities (`libs/utlis.js`)

### User Functions

- `fetchUserProfile(userId)` – Get user profile
- `updateUserInfo(userId, data)` – Update user information
- `updateUserInfoWithPicture(userId, data, file)` – Update profile with picture

### Product Functions

- `fetchAllProducts()` – Get all products
- `fetchUserProducts()` – Get current user's products
- `fetchProductById(productId)` – Get single product
- `createProduct(formData)` – Create new product
- `updateProduct(productId, formData)` – Update product
- `deleteProduct(productId)` – Delete product

### Order Functions

- `fetchOrders(role)` – Get orders (buyer/seller)
- `fetchOrderById(orderId)` – Get single order
- `createOrder(payload)` – Place new order
- `updateOrderStatus(orderId, status)` – Update order fulfillment status

### Preference Functions

- `fetchUserPreferences()` – Get saved payment/address
- `updateUserPreferences(payload)` – Update preferences

### Review Functions

- `createReview(orderId, rating, comment)` – Submit review
- `skipReview(orderId)` – Skip review prompt
- `getSellerReviews(sellerId, page, limit)` – Get seller reviews
- `getReviewByOrder(orderId)` – Get review for order

---

## 🚀 Getting Started

### Prerequisites

- Node.js 18+
- npm or yarn
- Backend API running (default: `http://localhost:8800`)

### 1. Clone the repository

```bash
git clone https://github.com/<your-team>/StudentTradeHub.git
cd StudentTradeHub/Web\ Application/frontend
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

Create a `.env.local` file in the frontend directory:

```env
NEXT_PUBLIC_API_URL=http://localhost:8800
```

### 4. Run the development server

```bash
npm run dev
```

Then open [http://localhost:3000](http://localhost:3000) in your browser.

### 5. Build for production

```bash
npm run build
npm start
```

---

## 📜 Available Scripts

| Command         | Description                             |
| --------------- | --------------------------------------- |
| `npm run dev`   | Start development server with Turbopack |
| `npm run build` | Build for production                    |
| `npm start`     | Start production server                 |

---

## 🌐 Environment Variables

| Variable              | Description          | Default                 |
| --------------------- | -------------------- | ----------------------- |
| `NEXT_PUBLIC_API_URL` | Backend API base URL | `http://localhost:8800` |

---

## 📱 Responsive Design

The application is fully responsive with breakpoints for:

- **Mobile**: < 640px
- **Tablet**: 640px - 1024px
- **Desktop**: > 1024px

Key responsive features:

- Collapsible navigation
- Mobile-optimized search bar
- Adaptive grid layouts (1-4 columns)
- Touch-friendly interactions

---

## 🎨 Design System

- **Colors**: Slate-based neutral palette with accent colors for status badges
- **Typography**: System font stack for optimal performance
- **Spacing**: Consistent padding and margins using Tailwind's scale
- **Components**: Rounded corners, subtle shadows, and clean borders

---

## 👥 Contributors

| Name                | GitHub                                           |
| ------------------- | ------------------------------------------------ |
| Olaiya Oluwatomisin | [@tomisiiiin](https://github.com/tomisiiiin)     |
| Labib Islam         | [@labib-islam](https://github.com/labib-islam)   |
| Nafiur Rahman       | [@Nafiur-rhyme](https://github.com/Nafiur-rhyme) |
| Anya Anya           | [@Chuxs](https://github.com/Chuxs)               |
| Md Minhajul Abedin  | [@Minhajul99](https://github.com/Minhajul99)     |
| Yi Zhang            | [@1mag1ne1](https://github.com/1mag1ne1)         |
| Yixuan Liu          | [@Yixuan-Liu1](https://github.com/Yixuan-Liu1)   |

---

## 📄 License

This project is part of Memorial University's coursework.
