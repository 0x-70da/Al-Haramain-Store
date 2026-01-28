# Tech Stack
  - Next.js
  - Shadcn/ui
  - Prisma
  - Neon
  - Tailwindcss
  - Next Auth
  - Redux/Toolkit
  - Axios

# Requirements

## 🧑‍💻 User Requirements (Customer Side)
- User sign up using email & password
- User login & logout
- Optional social login (Google)
- Forgot / reset password flow
- User profile management (name, email, password)
- Manage multiple shipping addresses
- Browse products with pagination
- Search products by keyword
- Filter products by category, price, rating, brand
- View product details (images, price, description, stock)
- Add products to cart
- Update cart item quantity
- Remove items from cart
- Persistent cart (saved per user)
- Add / remove products from wishlist
- Checkout process (address → payment → review)
- Online payment (Stripe)
- Cash on delivery option (optional)
- View order history
- Track order status
- Submit product reviews and ratings

## 🛒 Product & Catalog Requirements
- Product categories and sub-categories
- Product availability (in stock / out of stock)
- Product images gallery
- Discounted prices and offers
- Related / recommended products
- Product reviews & average rating
- SEO-friendly product pages

## 📦 Order & Checkout Requirements
- Create order after checkout
- Order lifecycle management:
- pending
- paid
- processing
- shipped
- delivered
- cancelled
- Automatic stock deduction after order creation
- Order total calculation (subtotal, discounts, taxes)
- Order confirmation email
- Store payment information securely
- Support order cancellation (before shipping)

## 🏬 Warehouse & Inventory Requirements
- Track product stock quantity
- Prevent overselling
- Low-stock alerts
- Manual stock adjustments (admin)
- Order preparation confirmation

## 🧑‍💼 Admin Dashboard Requirements
- Admin authentication & role-based access
- Dashboard overview (sales, orders, revenue)
- Manage products (create, update, delete)
- Upload and manage product images
- Manage categories
- View and manage orders
- Update order status manually
- Add tracking number to orders
- Manage users (view, block, change roles)
- View customer reviews
- Manual override for exceptional cases

## ⚙️ System & Technical Requirements
- Built with Next.js 16 (App Router)
- TypeScript for type safety
- Global state management using Redux Toolkit
- Database using PostgreSQL (Neon)
- Prisma ORM for database access
- Server-side rendering & SEO optimization
- Responsive design (mobile & desktop)
- Modern UI using Tailwind CSS & shadcn/ui
- Secure authentication & authorization
- Input validation (Zod)
- Error handling & loading states
- Environment-based configuration (.env)

## 🔐 Security Requirements
- Secure password hashing
- Protected routes (user & admin)
- CSRF protection
- Rate limiting on sensitive endpoints
- Secure cookies for auth
- Data validation & sanitization

## 🚀 Future Enhancements (Optional)
- Admin analytics & charts
- Coupons & promo codes
- Multi-vendor support
- Product returns & refunds
- Email & push notifications
- Internationalization (i18n)
- Dark mode


# Design

## 1️⃣ System Overview
The system is a full-stack e-commerce platform that allows users to browse products, place orders, and complete payments, while providing an admin dashboard for managing products, orders, users, and inventory.

The system follows a modular architecture with clear separation between:
- Presentation layer (UI)
- Application logic
- Data layer
- External services

## 2️⃣ High-Level Architecture
System Layers:
- Client (Browser)
- Frontend Application (Next.js)
- Backend Logic (API Routes / Server Actions)
- Database (PostgreSQL via Prisma)
- External Services (Payment, Email, Storage)
- 📐 Diagram Placeholder
- [High-Level System Architecture Diagram]

## 3️⃣ Main System Actors
- Guest User (unauthenticated)
- Authenticated User (customer)
- Admin User
- Warehouse Staff (admin role)
- External Services (Stripe, Email Provider)

## 4️⃣ Database Design (Relational Model)
The database follows a relational schema using PostgreSQL.

Core Tables:
- users
- addresses
- products
- categories
- product_images
- carts
- cart_items
- orders
- order_items
- payments
- reviews
- wishlists

## 5️⃣ Database Relationships
### User Relationships:
- One user can have multiple addresses
- One user can place multiple orders
- One user can write multiple reviews
- One user has one cart
- One user has one wishlist

### Product Relationships
- One product belongs to one category
- One product has multiple images
- One product can appear in many cart items
- One product can appear in many order items
- One product can have multiple reviews

### Order Relationships
- One order belongs to one user
- One order contains multiple order items
- One order has one payment record
- One order is shipped to one address

📐 Diagram Placeholder

[Entity Relationship Diagram – ERD]

## 6️⃣ Data Flow – User Order Lifecycle
- User browses products
- User adds product to cart
- Cart state is stored in Redux and synced with backend
- User proceeds to checkout
- Order record is created in database
- Stock quantity is reduced automatically
- Payment is processed via external payment service
- Order status is updated based on payment result
- Admin / warehouse prepares the order
- Order is shipped and tracking number is stored
- User can track order status

📐 Diagram Placeholder

[Order Flow Sequence Diagram]

## 7️⃣ Component Design (Frontend)
The frontend follows a component-based architecture.

### Component Categories:
#### Layout Components
- Navbar
- Footer
- Sidebar (admin)

#### Page Components
- Home Page
- Product Listing Page
- Product Details Page
- Cart Page
- Checkout Page
- Orders Page
- Admin Dashboard Pages

#### Reusable UI Components
- ProductCard
- ProductGallery
- CartItem
- AddressForm
- CheckoutSteps
- ReviewCard

### Component Communication
- Parent → Child via props
- Global state (cart, user) via Redux Toolkit
- Async data via server components or API calls

📐 Diagram Placeholder

[Frontend Component Hierarchy Diagram]

## 8️⃣ State Management Design (Redux Toolkit)
Redux is used for global, cross-page state, including:
- Cart state
- Authenticated user state
- Wishlist state
- Local UI state (modals, inputs) is handled inside components.

### Redux Flow:
- UI dispatches action
- Reducer updates state
- UI re-renders
- Optional async logic via thunks

📐 Diagram Placeholder

[Redux Data Flow Diagram]

## 9️⃣ Backend Design (API & Server Actions)
Backend responsibilities include:
- Authentication & authorization
- CRUD operations for products and categories
- Order creation and management
- Payment verification
- Admin operations

Each API route is responsible for:
- Input validation
- Business logic
- Database interaction
- Returning standardized responses

## 🔐 10 Security Design
- Authentication using secure cookies / tokens
- Role-based access control (RBAC)
- Protected admin routes
- Input validation using Zod
- Secure password hashing
- Environment variables for secrets

## 11 Error Handling & Edge Cases
- Out-of-stock products
- Failed payments
- Duplicate orders
- Unauthorized access
- Invalid input data
- Network failures

### Errors are handled gracefully with:
- User-friendly messages
- Logging
- Fallback UI states

## 12 Scalability & Future Design Considerations
Modular codebase for easy extension
Separation of concerns

### Ready for:
- Multi-vendor support
- Analytics
- Caching
- Background jobs
- Microservices (future)