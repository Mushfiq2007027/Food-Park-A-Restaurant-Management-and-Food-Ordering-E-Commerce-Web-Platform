# Food Park — Restaurant Management and Food Ordering Platform

Food Park is a full-stack, production-ready e-commerce web application built with Laravel 10. It provides a complete restaurant management solution — from a customer-facing food ordering storefront to a fully featured administrative backend — including multi-gateway payment processing, real-time notifications, table reservations, and live customer support chat.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [System Requirements](#system-requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Project Structure](#project-structure)
- [Admin Panel](#admin-panel)
- [Payment Gateways](#payment-gateways)
- [Real-Time Features](#real-time-features)
- [License](#license)

---

## Overview

Food Park serves both customers and restaurant administrators through two distinct interfaces:

- **Customer Storefront** — Browse the menu, filter by category, view daily offers, manage a shopping cart, apply coupons, select a delivery area, and complete checkout through one of three payment gateways.
- **Admin Panel** — A comprehensive backend dashboard for managing every aspect of the restaurant: products, categories, orders, reservations, chefs, promotions, site content, and payment settings.

---

## Features

### Customer-Facing

- Home page with dynamic hero sliders, banners, and "Why Choose Us" sections
- Product catalog with category filtering, product galleries, size options, and add-on options
- Quick-view product modal for fast cart additions
- Full shopping cart with real-time quantity updates and item removal
- Discount coupon system with validation
- Delivery area selection with dynamic charge calculation at checkout
- Checkout flow with address management (create, update, delete)
- Secure payment processing via PayPal, Stripe, and Razorpay
- Customer dashboard for viewing order history and managing account details
- Table reservation booking with selectable time slots
- Real-time live chat with the admin support team (powered by Pusher)
- User authentication, registration, email verification, and password reset (Laravel Breeze)

### Admin Panel

- Dashboard with key business metrics and new-order notifications
- Full product management: create, edit, publish/unpublish products with image galleries, size variants, and customization options
- Category management
- Order management: view all orders, filter by status (Pending, In-Process, Delivered, Declined), update order status in real time
- Coupon management with expiry date and usage-limit support
- Delivery area management with configurable pricing
- Chef profile management
- Daily offer management with product-search integration
- Banner slider and hero slider management
- Table reservation management with time-slot configuration
- Site-wide settings: general configuration and Pusher credentials
- Payment gateway configuration for PayPal, Stripe, and Razorpay (credentials stored per environment)
- Admin profile and password management
- Real-time customer support chat
- DataTables-powered listing pages with server-side processing

---

## Technology Stack

| Layer | Technology |
|---|---|
| Backend Framework | Laravel 10 (PHP 8.1+) |
| Frontend Build Tool | Vite 5 |
| CSS Framework | Tailwind CSS 3 |
| JavaScript | Alpine.js 3, Axios |
| Real-Time | Laravel Echo, Pusher JS, Pusher PHP Server |
| Payment — PayPal | srmklive/paypal |
| Payment — Stripe | stripe/stripe-php |
| Payment — Razorpay | razorpay/razorpay |
| Shopping Cart | anayarojo/shoppingcart |
| Data Tables | Yajra Laravel DataTables |
| Notifications (Toast) | yoeunes/toastr |
| Authentication | Laravel Breeze |
| API Layer | Laravel Sanctum |
| Database | MySQL |
| HTTP Client | Guzzle 7 |

---

## System Requirements

- PHP >= 8.1
- Composer
- Node.js >= 18 and npm
- MySQL >= 8.0
- A Pusher account (for real-time features)
- Payment gateway credentials for one or more of: PayPal, Stripe, Razorpay

---

## Installation

**1. Clone the repository**

```bash
git clone https://github.com/your-username/food-park.git
cd food-park
```

**2. Install PHP dependencies**

```bash
composer install
```

**3. Install JavaScript dependencies**

```bash
npm install
```

**4. Create the environment file**

```bash
cp .env.example .env
```

**5. Generate the application key**

```bash
php artisan key:generate
```

**6. Create the database**

Create a MySQL database named `food_park` (or any name of your choice — update `DB_DATABASE` accordingly).

**7. Run migrations and seeders**

```bash
php artisan migrate --seed
```

---

## Configuration

Open `.env` and update the following sections:

### Database

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=food_park
DB_USERNAME=root
DB_PASSWORD=your_password
```

### Pusher (Real-Time)

```env
PUSHER_APP_ID=your_app_id
PUSHER_APP_KEY=your_app_key
PUSHER_APP_SECRET=your_app_secret
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1
```

### Mail

```env
MAIL_MAILER=smtp
MAIL_HOST=your_mail_host
MAIL_PORT=587
MAIL_USERNAME=your_email@example.com
MAIL_PASSWORD=your_mail_password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=hello@yourdomain.com
MAIL_FROM_NAME="${APP_NAME}"
```

### Payment Gateways

Payment gateway credentials (PayPal Client ID/Secret, Stripe Secret Key, Razorpay Key/Secret) are configured directly from the Admin Panel under **Settings > Payment Gateway**, and are stored in the database. No manual `.env` entries are required for payment credentials.

---

## Running the Application

**Development mode (runs both PHP server and Vite HMR simultaneously):**

```bash
# Terminal 1 — Laravel dev server
php artisan serve

# Terminal 2 — Vite asset bundler
npm run dev
```

Visit `http://127.0.0.1:8000` in your browser.

**Build frontend assets for production:**

```bash
npm run build
```

---

## Project Structure

```
food-park/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── Admin/          # 21 admin panel controllers
│   │   │   └── Frontend/       # 8 customer-facing controllers
│   │   ├── Middleware/
│   │   └── Requests/
│   ├── Models/                 # 23 Eloquent models
│   ├── Events/                 # Real-time event classes (Pusher)
│   ├── Listeners/
│   ├── Mail/
│   ├── Services/
│   ├── Helpers/
│   ├── Traits/
│   └── DataTables/
├── database/
│   ├── migrations/             # 27 migration files
│   ├── seeders/
│   └── factories/
├── resources/
│   ├── views/
│   └── js/
├── routes/
│   ├── web.php                 # Customer-facing routes
│   ├── admin.php               # Admin panel routes
│   ├── api.php
│   └── auth.php
├── public/
├── .env.example
├── composer.json
├── package.json
├── tailwind.config.js
└── vite.config.js
```

---

## Admin Panel

The admin panel is accessible at `/admin/login`.

Default admin credentials are set via the database seeder. It is strongly recommended to change the password immediately after the first login.

The admin panel includes the following management sections:

| Section | Description |
|---|---|
| Dashboard | Business summary and new order alerts |
| Products | Full CRUD with gallery, sizes, and options |
| Categories | Product category management |
| Orders | Order lifecycle management (Pending to Delivered) |
| Coupons | Discount code creation and management |
| Delivery Areas | Service area and delivery fee configuration |
| Chefs | Chef profile management |
| Daily Offers | Featured product offer with section title control |
| Sliders | Hero slider image management |
| Banner Sliders | Promotional banner management |
| Reservations | Incoming table booking management |
| Reservation Times | Available time-slot configuration |
| Why Choose Us | Editable feature highlight section |
| Chat | Real-time customer support inbox |
| Settings | General settings and Pusher configuration |
| Payment Gateway | Per-gateway credential configuration |

---

## Payment Gateways

Food Park integrates three payment gateways. Each can be enabled and configured independently from the Admin Panel without requiring code changes or redeployment.

- **PayPal** — Implemented using the `srmklive/paypal` package. Supports sandbox and live modes.
- **Stripe** — Implemented using the official `stripe/stripe-php` SDK.
- **Razorpay** — Implemented using the official `razorpay/razorpay` SDK.

Successful and cancelled payment callbacks are handled through dedicated routes, ensuring reliable order status updates regardless of network conditions at payment time.

---

## Real-Time Features

Real-time functionality is powered by **Pusher** via **Laravel Echo** on the frontend and the **pusher/pusher-php-server** package on the backend.

- **Order Notifications** — When a customer places an order, the admin dashboard receives an instant notification without requiring a page refresh.
- **Live Chat** — Two-way real-time messaging between customers and the admin support team.

To enable real-time features, ensure your Pusher credentials are configured in the `.env` file and the broadcast driver is set to `pusher`:

```env
BROADCAST_DRIVER=pusher
```

---


