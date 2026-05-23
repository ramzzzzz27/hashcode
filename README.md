# 🎬 HashCode - Virtual Watch Party Application

A fully functional, production-style virtual watch-party web application that enables users to watch synchronized HD videos together in real-time with live chat and voice communication.

## 🌟 Features

### Core Functionality
- **User Authentication**: Google OAuth + Mobile OTP
- **Virtual Rooms**: Create public/private synchronized viewing rooms
- **Real-time Video Sync**: Synchronized play/pause/seek/volume across all participants
- **Live Chat**: Real-time messaging with emojis, GIFs, and mentions
- **Voice Chat**: Crystal-clear audio communication with noise suppression
- **Room Management**: Host controls for kicking users, transferring host, and more
- **Video Processing**: Upload or stream videos with HLS adaptive streaming
- **Notifications**: Real-time alerts for room invites and friend activity
- **Admin Panel**: Complete moderation and analytics dashboard

### Advanced Features
- Friend system with activity tracking
- Watch history and favorites
- Video quality selector and playback controls
- Subtitle support
- Theater mode UI
- Push-to-talk voice option
- Chat moderation and user muting
- Multi-device session persistence
- AI movie recommendations
- Theme customization

## 🛠️ Tech Stack

### Frontend
- **React.js** - UI framework
- **Tailwind CSS** - Styling
- **Framer Motion** - Smooth animations
- **React Router** - Navigation
- **Zustand** - State management
- **Socket.IO Client** - Real-time communication
- **Plyr/Video.js** - Video player
- **Axios** - HTTP client

### Backend
- **Node.js + Express.js** - Server framework
- **Socket.IO** - Real-time events
- **JWT** - Authentication
- **Google OAuth 2.0** - Social login
- **Multer** - File uploads
- **FFmpeg** - Video processing
- **Mongoose** - MongoDB ORM
- **Bcryptjs** - Password hashing
- **Nodemailer** - Email notifications

### Database & Storage
- **MongoDB** - Primary database
- **Cloudinary/AWS S3** - Video & image storage
- **Redis** - Session & cache management

### Deployment
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **Environment Variables** - Configuration management

## 📁 Project Structure

```
hashcode/
├── frontend/                 # React application
│   ├── src/
│   │   ├── components/      # Reusable React components
│   │   ├── pages/           # Page components
│   │   ├── hooks/           # Custom React hooks
│   │   ├── store/           # Zustand state management
│   │   ├── services/        # API services
│   │   ├── utils/           # Utility functions
│   │   ├── styles/          # Global styles
│   │   ├── sockets/         # Socket.IO configuration
│   │   ├── config/          # Configuration files
│   │   └── App.jsx          # Main app component
│   ├── public/              # Static assets
│   ├── package.json
│   ├── tailwind.config.js
│   └── vite.config.js
│
├── backend/                  # Node.js/Express API
│   ├── src/
│   │   ├── routes/          # API routes
│   │   ├── controllers/     # Request handlers
│   │   ├── models/          # MongoDB schemas
│   │   ├── middleware/      # Custom middleware
│   │   ├── services/        # Business logic
│   │   ├── sockets/         # Socket.IO events
│   │   ├── utils/           # Utility functions
│   │   ├── config/          # Configuration
│   │   ├── validators/      # Input validation
│   │   └── server.js        # Server entry point
│   ├── .env.example         # Environment variables template
│   ├── package.json
│   └── Dockerfile
│
├── docker-compose.yml       # Multi-container setup
├── .gitignore
└── DEPLOYMENT.md            # Deployment instructions

```

## 🚀 Quick Start

### Prerequisites
- Node.js >= 16
- MongoDB >= 4.4
- FFmpeg
- Git

### Installation

#### 1. Clone Repository
```bash
git clone https://github.com/ramzzzzz27/hashcode.git
cd hashcode
```

#### 2. Backend Setup
```bash
cd backend
npm install
cp .env.example .env
# Edit .env with your credentials
npm run dev
```

#### 3. Frontend Setup
```bash
cd ../frontend
npm install
cp .env.example .env
# Edit .env with API URL
npm run dev
```

#### 4. Access Application
- Frontend: http://localhost:5173
- Backend: http://localhost:5000
- MongoDB: mongodb://localhost:27017/hashcode

## 🔐 Environment Variables

### Backend (.env)
```
# Server
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/hashcode

# JWT
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRE=7d

# Google OAuth
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

# Cloudinary (or AWS S3)
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Email Service
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password

# Redis (Optional)
REDIS_URL=redis://localhost:6379

# CORS
FRONTEND_URL=http://localhost:5173

# FFmpeg Path
FFMPEG_PATH=/usr/bin/ffmpeg
```

### Frontend (.env)
```
VITE_API_URL=http://localhost:5000
VITE_SOCKET_URL=http://localhost:5000
VITE_GOOGLE_CLIENT_ID=your_google_client_id
VITE_CLOUDINARY_CLOUD_NAME=your_cloud_name
VITE_CLOUDINARY_UPLOAD_PRESET=your_preset
```

## 📚 API Documentation

### Authentication Endpoints
- `POST /api/auth/google` - Google OAuth login
- `POST /api/auth/otp/send` - Send OTP to phone
- `POST /api/auth/otp/verify` - Verify OTP
- `POST /api/auth/logout` - Logout user
- `GET /api/auth/me` - Get current user

### Room Endpoints
- `POST /api/rooms` - Create room
- `GET /api/rooms` - Get all rooms
- `GET /api/rooms/:roomId` - Get room details
- `PUT /api/rooms/:roomId` - Update room
- `DELETE /api/rooms/:roomId` - Delete room
- `POST /api/rooms/:roomId/join` - Join room
- `POST /api/rooms/:roomId/leave` - Leave room

### Video Endpoints
- `POST /api/videos/upload` - Upload video
- `GET /api/videos/:videoId` - Get video streaming URL
- `POST /api/videos/process` - Process video to HLS

### Chat Endpoints
- `GET /api/messages/:roomId` - Get room messages
- `POST /api/messages` - Send message
- `DELETE /api/messages/:messageId` - Delete message

### User Endpoints
- `GET /api/users/:userId` - Get user profile
- `PUT /api/users/:userId` - Update profile
- `POST /api/users/friends/:userId` - Add friend
- `GET /api/users/friends` - Get friends list

## 🔌 Socket.IO Events

### Playback Events
- `video:play` - Start playing video
- `video:pause` - Pause video
- `video:seek` - Seek to time
- `video:sync-request` - Request sync
- `video:quality-change` - Change quality

### Chat Events
- `message:send` - Send message
- `message:delete` - Delete message
- `chat:typing` - Typing indicator

### Room Events
- `room:user-joined` - User joined
- `room:user-left` - User left
- `room:user-kicked` - User kicked
- `room:state-update` - Room state change
- `room:lock` - Lock room

### Voice Events
- `voice:mute` - Mute audio
- `voice:unmute` - Unmute audio
- `voice:speaking` - Speaking indicator

## 🐳 Docker Deployment

### Build and Run with Docker Compose
```bash
docker-compose up --build
```

This will start:
- Frontend (port 5173)
- Backend (port 5000)
- MongoDB (port 27017)
- Redis (port 6379)

## 📦 Production Deployment

See [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed instructions on deploying to:
- Heroku
- AWS
- DigitalOcean
- Vercel (Frontend)
- Railway
- Render

## 🔒 Security Features

- JWT token-based authentication
- Password hashing with bcryptjs
- Input validation and sanitization
- XSS protection with helmet
- Rate limiting on API endpoints
- CORS configuration
- Secure file upload validation
- SQL injection prevention
- CSRF protection
- Secure session management

## 📊 Database Schema

### Users Collection
```javascript
{
  _id: ObjectId,
  username: String,
  email: String,
  phone: String,
  passwordHash: String,
  avatar: String,
  googleId: String,
  friends: [ObjectId],
  blockedUsers: [ObjectId],
  watchHistory: [{videoId, timestamp, progress}],
  favorites: [ObjectId],
  settings: {theme, language, notifications},
  createdAt: Date,
  updatedAt: Date
}
```

### Rooms Collection
```javascript
{
  _id: ObjectId,
  roomCode: String (unique),
  roomName: String,
  hostId: ObjectId,
  description: String,
  thumbnail: String,
  type: String (public/private),
  password: String (optional),
  videoSource: {type, url, duration, title},
  participants: [ObjectId],
  maxParticipants: Number,
  chatEnabled: Boolean,
  voiceEnabled: Boolean,
  currentTime: Number,
  isPlaying: Boolean,
  playbackSpeed: Number,
  quality: String,
  createdAt: Date,
  expiresAt: Date,
  updatedAt: Date
}
```

### Messages Collection
```javascript
{
  _id: ObjectId,
  roomId: ObjectId,
  senderId: ObjectId,
  message: String,
  mentions: [ObjectId],
  reactions: [{emoji, users}],
  createdAt: Date,
  updatedAt: Date,
  deletedAt: Date
}
```

## 🎨 UI/UX Features

- **Modern Dark Theme**: Netflix-inspired dark cinematic design
- **Glassmorphism**: Frosted glass effect cards
- **Smooth Animations**: Framer Motion transitions
- **Responsive Design**: Mobile, tablet, desktop optimized
- **Loading States**: Skeleton screens for better UX
- **Theater Mode**: Immersive full-screen experience
- **Adaptive UI**: Collapsible sidebars, responsive layouts

## 🧪 Testing

```bash
# Backend tests
cd backend
npm run test

# Frontend tests
cd ../frontend
npm run test
```

## 📝 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

## 👥 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 🐛 Issue Reporting

Found a bug? Please create an issue on GitHub with:
- Clear title
- Detailed description
- Steps to reproduce
- Expected vs actual behavior
- Screenshots/videos if applicable

## 📞 Support

For support, email support@hashcode.app or open an issue on GitHub.

## 🙏 Acknowledgments

- Netflix for UI/UX inspiration
- Discord for real-time features inspiration
- Teleparty & Watch2Gether for watch-party concepts
- Open-source community for amazing libraries

---

**Made with ❤️ by HashCode Team**

**Status**: 🚀 Production Ready | **Version**: 1.0.0 | **Last Updated**: 2026
