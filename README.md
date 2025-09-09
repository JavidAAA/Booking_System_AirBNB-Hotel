[![Facebook][facebook-shield]][facebook-url]
[![Instagram][instagram-shield]][instagram-url]
[![Twitter][twitter-shield]][twitter-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Github][github-shield]][github-url]

![Frontend Screenshot](https://raw.githubusercontent.com/SamiurRahmanMukul/Hotel-Room-Booking-System/main/frontend-screenshot.png)

# 🏖️ Beach Resort | Hotel Room Booking System

A comprehensive full-stack hotel room booking and management system built with modern web technologies. This application provides a complete solution for hotel room reservations, user management, and administrative operations.

## 🌐 Live Demo

<div align="center">

### ✨ Experience the Application Live ✨

| Application         | Link                                        | Description                                       |
| ------------------- | ------------------------------------------- | ------------------------------------------------- |
| 🖥️ **Admin Panel**  | [`🚀 Launch Admin Panel`][admin-panel-link] | Complete management dashboard for administrators. |
| 🌟 **Frontend App** | [`🚀 Launch Frontend`][frontend-link]       | Beautiful user interface for room booking.        |

</div>

## 📋 Table of Contents

- [Features](#-features)
- [Technology Stack](#️-technology-stack)
- [System Architecture](#️-system-architecture)
- [Database Schema](#-database-schema)
- [API Documentation](#-api-documentation)
- [Installation & Setup](#-installation--setup)
- [Usage](#-usage)
- [Contributing](#-contributing)
- [License](#-license)

## ✨ Features

### 🔐 Authentication & Authorization

- **User Registration/Login** with email verification
- **JWT-based authentication** with access and refresh tokens
- **Password reset** functionality with secure token system
- **Role-based access control** (Admin/User)
- **Account status management** (Active/Blocked/Verified)

### 🏠 Room Management

- **Room CRUD operations** with image uploads
- **Room categorization** (Single, Couple, Family, Presidential)
- **Room status tracking** (Available, Unavailable, Booked)
- **Featured rooms** highlighting
- **Advanced room filtering** and search capabilities
- **Room capacity and pricing** management

### 📅 Booking System

- **Date-based booking** with validation
- **Booking status management** (Pending, Approved, Cancelled, etc.)
- **Booking history** for users
- **Admin booking management** panel
- **Automatic room status updates**

### ⭐ Review System

- **Room reviews and ratings** (1-5 stars)
- **User review management**
- **Review editing and deletion**
- **Average rating calculations**

### 👤 User Management

- **User profile management** with avatar uploads
- **Admin dashboard** with comprehensive statistics
- **User role management**
- **Account blocking/unblocking**

### 📊 Admin Dashboard

- **Real-time statistics** (Users, Rooms, Bookings)
- **Data visualization** with charts and counters
- **User and booking management**
- **Room inventory management**

## 🛠️ Technology Stack

### Backend

- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB object modeling
- **JWT** - Authentication tokens
- **Bcrypt.js** - Password hashing
- **Multer** - File upload handling
- **SendGrid** - Email service
- **Winston** - Logging
- **Morgan** - HTTP request logging
- **Helmet** - Security headers
- **CORS** - Cross-origin resource sharing
- **Express Rate Limit** - API rate limiting

### Frontend (Client)

- **Next.js 13** - React framework with SSR
- **React 18** - UI library
- **Redux Toolkit** - State management
- **Ant Design** - UI component library
- **Styled Components** - CSS-in-JS styling
- **Axios** - HTTP client
- **Day.js** - Date manipulation
- **React Icons** - Icon components

### Admin Panel

- **React 18** - UI library
- **Redux Toolkit** - State management
- **Ant Design** - UI component library
- **Tailwind CSS** - Utility-first CSS framework
- **React Router Dom** - Client-side routing
- **React CountUp** - Animated counters
- **JWT Decode** - Token decoding

## 🏗️ System Architecture

```drawio
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   Admin Panel   │    │    Backend      │
│   (Next.js)     │    │   (React.js)    │    │   (Node.js)     │
│                 │    │                 │    │                 │
│ • User Interface│    │ • Admin Dashboard│   │ • REST API      │
│ • Room Booking  │◄──►│ • Management    │◄──►│ • Authentication│
│ • User Profile  │    │ • Analytics     │    │ • Business Logic│
│ • Reviews       │    │ • CRUD Operations│   │ • File Upload   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                                        │
                                                        ▼
                                               ┌─────────────────┐
                                               │    MongoDB      │
                                               │                 │
                                               │ • Users         │
                                               │ • Rooms         │
                                               │ • Bookings      │
                                               │ • Reviews       │
                                               └─────────────────┘
```

## 📊 Database Schema

### User Model

```javascript
{
  userName: String (unique),
  fullName: String,
  email: String (unique),
  phone: String,
  password: String (hashed),
  avatar: String,
  gender: Enum ['male', 'female'],
  dob: Date,
  address: String,
  role: Enum ['admin', 'user'],
  verified: Boolean,
  status: Enum ['register', 'login', 'logout', 'blocked']
}
```

### Room Model

```javascript
{
  room_name: String (unique),
  room_slug: String,
  room_type: Enum ['single', 'couple', 'family', 'presidential'],
  room_price: Number,
  room_size: Number,
  room_capacity: Number,
  allow_pets: Boolean,
  provide_breakfast: Boolean,
  featured_room: Boolean,
  room_description: String,
  extra_facilities: [String],
  room_images: [{ url: String }],
  room_status: Enum ['available', 'unavailable', 'booked'],
  created_by: ObjectId (ref: Users)
}
```

### Booking Model

```javascript
{
  room_id: ObjectId (ref: Rooms),
  booking_dates: [Date],
  booking_status: Enum ['pending', 'cancel', 'approved', 'rejected', 'in-reviews', 'completed'],
  booking_by: ObjectId (ref: Users),
  reviews: ObjectId (ref: Reviews)
}
```

### Review Model

```javascript
{
  user_id: ObjectId (ref: Users),
  room_id: ObjectId (ref: Rooms),
  booking_id: ObjectId (ref: Bookings),
  rating: Number (1-5),
  message: String
}
```

## 📚 API Documentation

### Authentication Routes

```curl
POST /api/v1/auth/registration          - User registration
POST /api/v1/auth/login                 - User login
POST /api/v1/auth/logout                - User logout
POST /api/v1/auth/forgot-password       - Request password reset
POST /api/v1/auth/reset-password/:token - Reset password
POST /api/v1/auth/change-password       - Change password
POST /api/v1/auth/verify-email/:token   - Verify email
GET  /api/v1/auth/refresh-token         - Refresh JWT token
```

### Room Routes

```curl
GET    /api/v1/all-rooms-list                   - Get all rooms
GET    /api/v1/get-room-by-id-or-slug-name/:id  - Get room details
GET    /api/v1/featured-rooms-list              - Get featured rooms
POST   /api/v1/create-room                      - Create room (Admin)
PUT    /api/v1/edit-room/:id                    - Edit room (Admin)
DELETE /api/v1/delete-room/:id                  - Delete room (Admin)
```

### Booking Routes

```curl
POST /api/v1/placed-booking-order/:id     - Place booking order
GET  /api/v1/get-user-booking-orders      - Get user bookings
PUT  /api/v1/cancel-booking-order/:id     - Cancel booking
GET  /api/v1/get-all-booking-orders       - Get all bookings (Admin)
PUT  /api/v1/updated-booking-order/:id    - Update booking (Admin)
```

### User Routes

```curl
GET    /api/v1/get-user           - Get current user
GET    /api/v1/get-user/:id       - Get user by ID (Admin)
PUT    /api/v1/update-user        - Update user profile
PUT    /api/v1/avatar-update      - Update user avatar
DELETE /api/v1/delete-user        - Delete current user
DELETE /api/v1/delete-user/:id    - Delete user by ID (Admin)
GET    /api/v1/all-users-list     - Get all users (Admin)
PUT    /api/v1/blocked-user/:id   - Block user (Admin)
PUT    /api/v1/unblocked-user/:id - Unblock user (Admin)
```

### Review Routes

```curl
POST /api/v1/room-review-add/:id            - Add room review
GET  /api/v1/get-room-reviews-list/:room_id - Get room reviews
PUT  /api/v1/edit-room-review/:review_id    - Edit review
```

## 🚀 Installation & Setup

### Prerequisites

- Node.js (v14 or higher)
- MongoDB (local or cloud)
- npm or yarn package manager

### 1. Clone the Repository

```bash
git clone https://github.com/SamiurRahmanMukul/Hotel-Room-Booking-System.git
cd Hotel-Room-Booking-System
```

### 2. Backend Setup

```bash
cd backend
npm install
```

Create `.env` file in backend directory with your configuration values.

### 3. Frontend Setup

```bash
cd frontend
npm install
```

Create `.env.local` file in frontend directory with your API configuration.

### 4. Admin Panel Setup

```bash
cd admin-panel
npm install
```

Create `.env` file in admin-panel directory with your API configuration.

### 5. Start the Applications

#### Start Backend Server

```bash
cd backend
npm run dev  # Development mode
npm start    # Production mode
```

#### Start Frontend Application

```bash
cd frontend
npm run dev  # Runs on http://localhost:3034
```

#### Start Admin Panel

```bash
cd admin-panel
npm start    # Runs on http://localhost:3033
```

## 📖 Usage

### For End Users (Frontend)

1. **Register/Login**: Create account or login with existing credentials
2. **Browse Rooms**: View available rooms with filters and search
3. **Book Rooms**: Select dates and book available rooms
4. **Manage Bookings**: View, track, and cancel bookings
5. **Leave Reviews**: Rate and review booked rooms
6. **Profile Management**: Update personal information and avatar

### For Administrators (Admin Panel)

1. **Dashboard**: View system statistics and analytics
2. **User Management**: Manage user accounts, roles, and status
3. **Room Management**: Add, edit, delete, and manage room inventory
4. **Booking Management**: Oversee all bookings and update statuses
5. **Review Moderation**: Monitor and manage user reviews

## 🔒 Security Features

- **JWT Authentication** with access and refresh tokens
- **Password hashing** using bcrypt
- **Input validation** and sanitization
- **Rate limiting** to prevent abuse
- **CORS configuration** for secure cross-origin requests
- **Helmet** for security headers
- **File upload restrictions** and validation
- **Environment variable protection**

## 📱 Responsive Design

All applications are fully responsive and optimized for:

- Desktop computers
- Tablets
- Mobile devices
- Various screen sizes and orientations

## 🛡️ Testing

### Backend Testing

```bash
cd backend
npm test        # Run tests
npm run coverage # Run tests with coverage
```

### Linting

```bash
# Backend
cd backend && npm run lint

# Frontend
cd frontend && npm run lint

# Admin Panel
cd admin-panel && npm run lint
```

## 🚀 Deployment

### Backend Deployment

- Deploy to platforms like Heroku, Railway, or AWS
- Ensure MongoDB connection (MongoDB Atlas recommended)
- Set production environment variables
- Configure CORS for production domains

### Frontend Deployment

- Deploy to Vercel, Netlify, or similar platforms
- Update API URLs for production
- Configure environment variables

### Admin Panel Deployment

- Build and deploy to static hosting platforms
- Update API configurations for production

## 👥 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

### Md. Samiur Rahman (Mukul)

- 🌐 Website: [srmukul.com](https://srmukul.com)
- 📧 Email: [contact@srmukul.com](mailto:contact@srmukul.com)
- 🐙 GitHub: [@SamiurRahmanMukul](https://github.com/SamiurRahmanMukul)
- 💼 LinkedIn: [@SamiurRahmanMukul](https://www.linkedin.com/in/SamiurRahmanMukul)

## 🙏 Acknowledgments

- Express.js team for the robust web framework
- MongoDB team for the flexible database solution
- React and Next.js teams for the powerful frontend frameworks
- Ant Design team for the comprehensive UI component library
- All open-source contributors who made this project possible

---

<p align="center">
  <strong>⭐ If you found this project helpful, please give it a star! ⭐</strong>
</p>

<!-- my social media links -->

[facebook-url]: https://www.facebook.com/SamiurRahmanMukul
[instagram-url]: https://www.instagram.com/samiur_rahman_mukul
[twitter-url]: https://www.twitter.com/SamiurRahMukul
[linkedin-url]: https://www.linkedin.com/in/SamiurRahmanMukul
[github-url]: https://www.github.com/SamiurRahmanMukul

<!-- shield icon links -->

[facebook-shield]: https://img.shields.io/badge/-Facebook-black.svg?style=flat-square&logo=facebook&color=555&logoColor=white
[instagram-shield]: https://img.shields.io/badge/-Instagram-black.svg?style=flat-square&logo=instagram&color=555&logoColor=white
[twitter-shield]: https://img.shields.io/badge/-Twitter-black.svg?style=flat-square&logo=twitter&color=555&logoColor=white
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555
[github-shield]: https://img.shields.io/badge/-Github-black.svg?style=flat-square&logo=github&color=555&logoColor=white

<!-- live preview links -->

[admin-panel-link]: https://admin-beach-resort.vercel.app
[frontend-link]: https://mukul-beach-resort.vercel.app
