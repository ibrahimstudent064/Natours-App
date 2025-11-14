# 🏔️ Natours Application

A full-stack tour booking application built with Node.js, Express, MongoDB, and modern web technologies. This application allows users to browse, book, and review nature tours with secure payment processing and comprehensive user management.

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Project Structure](#project-structure)
- [Security Features](#security-features)
- [Scripts](#scripts)
- [License](#license)

## ✨ Features

### Core Functionality
- **Tour Management**: Browse, search, filter, and view detailed tour information
- **User Authentication**: Secure registration, login, and password reset functionality
- **User Authorization**: Role-based access control (user, guide, lead-guide, admin)
- **Reviews & Ratings**: Users can leave reviews and ratings for tours
- **Booking System**: Secure tour booking with payment processing via Stripe
- **Email Notifications**: Automated emails for welcome, password reset, and booking confirmations
- **Image Upload**: Tour and user profile image upload with automatic resizing
- **Interactive Maps**: Tour location visualization using Mapbox
- **Server-Side Rendering**: Dynamic web pages using Pug templating engine

### Advanced Features
- **Advanced Filtering**: Filter tours by price, duration, difficulty, ratings, and more
- **Sorting & Pagination**: Efficient data retrieval with customizable sorting and pagination
- **Geospatial Queries**: Find tours within a specified distance from a location
- **Aggregation Pipeline**: Complex data analysis and statistics
- **Error Handling**: Comprehensive error handling with custom error classes
- **API Rate Limiting**: Protection against brute-force attacks
- **Data Validation**: Input validation and sanitization

## 🛠️ Tech Stack

### Backend
- **Node.js** - JavaScript runtime
- **Express.js** - Web application framework
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB object modeling

### Security & Middleware
- **Helmet** - Security HTTP headers
- **Express Rate Limit** - Rate limiting middleware
- **Express Mongo Sanitize** - NoSQL injection protection
- **XSS Clean** - XSS attack prevention
- **HPP** - HTTP parameter pollution protection
- **CORS** - Cross-origin resource sharing
- **Compression** - Response compression

### Authentication & Authorization
- **JSON Web Tokens (JWT)** - Token-based authentication
- **Bcryptjs** - Password hashing

### Payment Processing
- **Stripe** - Payment gateway integration

### Email
- **Nodemailer** - Email sending functionality
- **HTML-to-Text** - Email template conversion

### File Upload & Processing
- **Multer** - File upload handling
- **Sharp** - Image processing and resizing

### Frontend
- **Pug** - Template engine for server-side rendering
- **Parcel** - JavaScript bundler
- **Axios** - HTTP client
- **Mapbox** - Interactive maps

### Development Tools
- **Nodemon** - Development server auto-restart
- **ESLint** - Code linting
- **Prettier** - Code formatting

## 📦 Prerequisites

Before you begin, ensure you have the following installed:
- **Node.js** (v10 or higher)
- **MongoDB** (local installation or MongoDB Atlas account)
- **npm** or **yarn** package manager
- **Git**

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd after-section-14
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   Create a `config.env` file in the root directory with the following variables:
   ```env
   NODE_ENV=development
   PORT=3000
   DATABASE=mongodb://localhost:27017/natours
   DATABASE_PASSWORD=your_password
   
   JWT_SECRET=your_jwt_secret_key
   JWT_EXPIRES_IN=90d
   JWT_COOKIE_EXPIRES_IN=90
   
   EMAIL_FROM=noreply@natours.io
   EMAIL_USERNAME=your_email
   EMAIL_PASSWORD=your_email_password
   EMAIL_HOST=smtp.mailtrap.io
   EMAIL_PORT=2525
   
   STRIPE_SECRET_KEY=your_stripe_secret_key
   STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret
   
   MAPBOX_TOKEN=your_mapbox_token
   ```

## ⚙️ Configuration

### Database Setup
1. **Local MongoDB**: Ensure MongoDB is running on your local machine
2. **MongoDB Atlas**: Update the `DATABASE` connection string in `config.env`

### Import Sample Data
To populate the database with sample tours, users, and reviews:
```bash
node dev-data/data/import-dev-data.js --import
```

To delete all data:
```bash
node dev-data/data/import-dev-data.js --delete
```

## 🏃 Running the Application

### Development Mode
```bash
npm run dev
```
The application will start on `http://localhost:3000` (or the port specified in your config).

### Production Mode
```bash
npm start
```

### Build Frontend Assets
```bash
npm run build:js
```

### Watch Frontend Assets (Development)
```bash
npm run watch:js
```

## 📚 API Documentation

### Base URL
```
http://localhost:3000/api/v1
```

### Authentication
Most endpoints require authentication via JWT token. Include the token in the Authorization header:
```
Authorization: Bearer <your_jwt_token>
```

### Main Endpoints

#### Tours
- `GET /tours` - Get all tours (with filtering, sorting, pagination)
- `GET /tours/:id` - Get a specific tour
- `POST /tours` - Create a new tour (Admin/Lead Guide only)
- `PATCH /tours/:id` - Update a tour (Admin/Lead Guide only)
- `DELETE /tours/:id` - Delete a tour (Admin/Lead Guide only)
- `GET /tours/top-5-cheap` - Get top 5 cheapest tours
- `GET /tours/tour-stats` - Get tour statistics (Admin/Lead Guide only)
- `GET /tours/monthly-plan/:year` - Get monthly tour plan (Admin/Lead Guide only)
- `GET /tours/tours-within/:distance/center/:latlng/unit/:unit` - Get tours within distance
- `GET /tours/distances/:latlng/unit/:unit` - Get distances to all tours

#### Users
- `POST /users/signup` - Register a new user
- `POST /users/login` - Login user
- `GET /users/logout` - Logout user
- `POST /users/forgotPassword` - Request password reset
- `PATCH /users/resetPassword/:token` - Reset password
- `PATCH /users/updateMyPassword` - Update current user's password
- `GET /users/me` - Get current user profile
- `PATCH /users/updateMe` - Update current user profile
- `DELETE /users/deleteMe` - Delete current user account
- `GET /users` - Get all users (Admin only)
- `GET /users/:id` - Get a specific user (Admin only)
- `PATCH /users/:id` - Update a user (Admin only)
- `DELETE /users/:id` - Delete a user (Admin only)

#### Reviews
- `GET /reviews` - Get all reviews
- `GET /reviews/:id` - Get a specific review
- `POST /reviews` - Create a new review (User only)
- `PATCH /reviews/:id` - Update a review (User/Admin only)
- `DELETE /reviews/:id` - Delete a review (User/Admin only)

#### Bookings
- `GET /bookings/checkout-session/:tourId` - Get Stripe checkout session
- `POST /webhook-checkout` - Stripe webhook endpoint
- `GET /bookings` - Get all bookings (Admin/Lead Guide only)
- `GET /bookings/my-bookings` - Get current user's bookings
- `POST /bookings` - Create a booking (Admin/Lead Guide only)
- `GET /bookings/:id` - Get a specific booking (Admin/Lead Guide only)
- `PATCH /bookings/:id` - Update a booking (Admin/Lead Guide only)
- `DELETE /bookings/:id` - Delete a booking (Admin/Lead Guide only)

### Query Parameters Examples

**Filtering:**
```
GET /api/v1/tours?duration[gte]=5&price[lte]=1000&difficulty=easy
```

**Sorting:**
```
GET /api/v1/tours?sort=price,-ratingsAverage
```

**Pagination:**
```
GET /api/v1/tours?page=2&limit=10
```

**Field Limiting:**
```
GET /api/v1/tours?fields=name,price,duration
```

### Postman Collection
A Postman collection is included in the project (`natours-postman-collection.json`) for easy API testing.

## 📁 Project Structure

```
after-section-14/
├── controllers/          # Route controllers
│   ├── authController.js
│   ├── bookingController.js
│   ├── errorController.js
│   ├── handlerFactory.js
│   ├── reviewController.js
│   ├── tourController.js
│   ├── userController.js
│   └── viewsController.js
├── models/              # Mongoose models
│   ├── bookingModel.js
│   ├── reviewModel.js
│   ├── tourModel.js
│   └── userModel.js
├── routes/              # Express routes
│   ├── bookingRoutes.js
│   ├── reviewRoutes.js
│   ├── tourRoutes.js
│   ├── userRoutes.js
│   └── viewRoutes.js
├── utils/               # Utility functions
│   ├── apiFeatures.js
│   ├── appError.js
│   ├── catchAsync.js
│   └── email.js
├── views/               # Pug templates
│   ├── email/
│   ├── account.pug
│   ├── base.pug
│   ├── error.pug
│   ├── login.pug
│   ├── overview.pug
│   └── tour.pug
├── public/              # Static files
│   ├── css/
│   ├── img/
│   └── js/
├── dev-data/            # Development data
│   ├── data/
│   ├── img/
│   └── templates/
├── app.js               # Express app configuration
├── server.js            # Server entry point
└── package.json         # Dependencies and scripts
```

## 🔒 Security Features

- **Helmet.js**: Sets various HTTP headers for security
- **Rate Limiting**: Prevents brute-force attacks (100 requests per hour per IP)
- **Data Sanitization**: Protection against NoSQL injection and XSS attacks
- **Parameter Pollution Protection**: Prevents HTTP parameter pollution
- **Password Hashing**: Bcrypt with salt rounds
- **JWT Authentication**: Secure token-based authentication
- **Password Reset**: Secure token-based password reset flow
- **CORS**: Configurable cross-origin resource sharing

## 📝 Scripts

- `npm start` - Start the production server
- `npm run dev` - Start the development server with nodemon
- `npm run start:prod` - Start production server with nodemon
- `npm run build:js` - Build frontend JavaScript bundle
- `npm run watch:js` - Watch and rebuild frontend JavaScript
- `npm run debug` - Start server with Node debugger

## 🎓 Project Highlights

This project demonstrates:
- RESTful API design
- MVC architecture pattern
- Authentication and authorization
- Payment processing integration
- Email functionality
- File upload and processing
- Error handling best practices
- Security best practices
- Database modeling with Mongoose
- Advanced MongoDB queries and aggregation

## 📄 License

👨‍💻 Developed by: Ibrahim Saudi
📧 Contact: ibrahimstudent064@gmail.com

---

Built with ❤️ using Node.js, Express, and MongoDB

