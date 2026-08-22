# Coding Academy Backend Starter

A Node.js backend service supporting the Coding Academy E2E starter project. This service provides RESTful APIs, real-time WebSocket functionality, and MongoDB integration.

## 🚀 Quick Start

1. Install dependencies:
```bash
npm install
```

2. Start the server:
```bash
npm run dev     # Development mode with hot reload
npm start       # Production mode
```

## 📡 API Endpoints



### Users API
- `POST /api/auth/signup` - Register new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/logout` - Logout user
- `GET /api/user` - Get all users
- `GET /api/user/:id` - Get user by ID

### Reviews API
- `GET /api/review` - Get all reviews
- `POST /api/review` - Create new review
- `DELETE /api/review/:id` - Delete review

## 🏗️ Project Structure

```
api/
├── auth/         # Authentication routes and logic
├── user/         # User management

└── review/       # Review system
services/
├── db.service.js       # Database connectivity
├── socket.service.js   # WebSocket functionality
├── logger.service.js   # Logging utility
└── util.service.js     # Helper functions
middlewares/
├── requireAuth.js      # Authentication middleware
└── setupAls.js        # Async local storage setup
```

## 💾 Database Schema



### User Collection
```js
{
  username: String,
  password: String,
  fullname: String,
  imgUrl: String,
  isAdmin: Boolean,
  score: Number,
  isAdmin: Boolean
}
```
### Stay Collection
```js
{
  _id: ObjectId,
  name: String,
  host: {
    _id: String,       
    fullname: String,
    imgUrl: String
  },
  loc: {
    city: String,
    lat: Number,
    lng: Number
  },
  price: Number,
  imgUrls: [String]
}
```
### Order Collection
```js
{
  _id: ObjectId,
  hostId: String,
  buyer: {
    _id: String,
    fullname: String
  },
  stay: {
    _id: String,
    name: String,
    price: Number
  },
  startDate: String,
  endDate: String,
  guests: {
    adults: Number,
    children: Number,
    infants: Number,
    pets: Number
  },
  totalPrice: Number,
  imgUrl: String,
  status: String  // Kind of still unimplemented..
}
```
### Review Collection
```js
{
   byUserId: ObjectId,
  targetType: String,
  targetId: ObjectId,
  txt: String,
  rating: Number,
  createdAt: Date
}
```

## 🔒 Authentication

Uses JWT (JSON Web Tokens) for stateless authentication. Tokens are stored in cookies and validated through middleware.

## 🔌 WebSocket Events

- `user-watch` - User status updates
- `chat-new-msg` - New chat messages
- `review-about-you` - New review notifications
- `review-added` - Review created
- `review-removed` - Review deleted

## 🛠️ Development

### Error Handling
```js
try {
  // Your code
} catch (err) {
  logger.error('Failed to do something', err)
  throw err
}
```

### Async Local Storage
Used for tracking request context, especially for logging and user sessions.

## 📝 Logging

Logs are stored in the `/logs` directory with the following levels:
- DEBUG - Development information
- INFO - General application events
- WARN - Warning conditions
- ERROR - Error events

## 🔥 Production Deployment

1. Set production environment variables
2. Build the frontend:
```bash
cd ../frontend-react && npm run build
```
3. Start the server:
```bash
npm start
```

## 📄 License

Coding Academy - Built with ❤️ for teaching modern fullstack development
