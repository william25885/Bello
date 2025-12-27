# 💬 Bello — Social Meetup & Real-time Chat System

🌐 **Live Version:** [https://bello-tw.vercel.app/](https://bello-tw.vercel.app/)

Bello is a database-driven web-based social networking system that provides a relaxed and secure platform for users to create or participate in physical meetups such as lunch, coffee, language exchange, and more, with support for cross-language communication. The system is divided into two main roles: User and Admin. Users can freely register accounts, edit profiles, host and join meetups, and communicate with others through the built-in chat rooms, while administrators can manage meetup content and user behavior to maintain platform order.

## ✨ Features

### 👤 User Features
- **Multiple Login Methods**: Support for account/password login and Google OAuth login
- **Profile Management**: Complete profile editing, including avatar upload and cropping functionality
- **Meetup Management**: Create, join, and cancel meetups, supporting various meetup types (lunch, coffee, dinner, drinks, language exchange)
- **Meetup Password Protection**: Set passwords for meetups; other users must enter the correct password to join
- **Location Integration**: Support for Google Places autocomplete for location input and map viewing of meetup locations
- **Real-time Messaging**:
  - One-on-one private chat
  - Meetup group chat rooms
  - Online status display
- **Friend System**:
  - Search and add friends (supports account, name, nickname search)
  - Friend request management (send, accept, reject)
  - Friend list with online status (including avatar display)
  - View other users' public profiles (complete basic and detailed information)
  - Social media account display (shows all social accounts when willing to exchange)
  - All user lists display avatars (private chat, friend list, search results)

### 🔐 Admin Features
- **Meetup Management**: View all meetups, view meetup details, cancel meetups, end meetups
- **User Management**: Browse all user lists, view user detailed information, delete users, support ID search
- **Chat History Viewing**:
  - View all private chat conversation lists (shows both users, message count, last message time)
  - View all meetup chat lists (shows meetup information, message count, status)
  - Click to view detailed chat history
  - Support pagination browsing and ID search

### 🎨 User Experience
- Page loading state management (prevents data flickering)
- Responsive design adapted to various screen sizes
- Loading animations and operation feedback
- User-friendly error messages

### 🛡️ Security Features
- JWT Token authentication mechanism
- Route permission control (Navigation Guards)
- API endpoint protection (`@require_auth`, `@require_admin` decorators)
- Embedded browser detection and prompts (LINE, Facebook, etc.)

## 🛠️ Tech Stack

### Frontend
- **Framework**: Vue.js 3.5.13
- **Routing**: Vue Router 4.4.5
- **UI Framework**: Bootstrap 5.3.3
- **Build Tool**: Vite 6.0.1
- **Image Processing**: Cropper.js 1.6.2 (avatar cropping)
- **HTTP Client**: Axios 1.7.9

### Backend
- **Framework**: Flask 3.1.0
- **Database**: PostgreSQL (Neon cloud database)
- **Database Driver**: psycopg2-binary 2.9.9
- **Authentication**: PyJWT 2.8.0
- **Password Hashing**: bcrypt 4.1.2
- **OAuth**: google-auth 2.25.2
- **CORS**: Flask-CORS 5.0.0

### Deployment
- **Frontend Deployment**: Vercel
- **Backend Deployment**: Vercel Serverless Functions
- **Database**: Neon PostgreSQL

## 📁 Project Structure

```
Bello_system/
├── frontend/                 # Frontend project
│   ├── src/
│   │   ├── components/      # Vue components
│   │   ├── views/           # Page views
│   │   ├── router/          # Route configuration
│   │   ├── utils/           # Utility functions (API, authentication, etc.)
│   │   └── config/          # Configuration files
│   ├── public/              # Static resources
│   └── package.json
├── backend/                 # Backend project
│   ├── actions/             # API endpoints
│   │   ├── auth/            # Authentication related
│   │   ├── meeting/         # Meetup management
│   │   ├── profile/         # User profiles
│   │   ├── chat/            # Chat functionality
│   │   ├── friend/          # Friend system
│   │   └── admin/           # Admin features
│   ├── DB_utils.py          # Database utility class
│   ├── jwt_utils.py         # JWT utility functions
│   ├── app.py               # Flask application entry point
│   ├── config.py            # Configuration file
│   ├── init_bello_db.sql    # Database initialization script
│   └── requirements.txt     # Python dependencies
├── api/                     # Vercel Serverless Function
│   ├── index.py             # Entry file
│   └── requirements.txt
├── vercel.json              # Vercel deployment configuration
└── README.md
```

## 🚀 Quick Start

### Requirements

- Python 3.10.9+
- Node.js 21.5.0+
- PostgreSQL database (Neon recommended)

### 1. Clone the Project

```bash
git clone <repository-url>
cd final-project/Bello_system
```

### 2. Backend Setup

#### Install Dependencies

```bash
cd backend
pip install -r requirements.txt
```

#### Environment Variables Configuration

Copy `backend/.env.example` and rename it to `backend/.env`, then fill in the following configuration:

```env
# Database connection
DATABASE_URL=postgresql://user:password@host:port/database?sslmode=require

# Server configuration
SERVER_HOST=127.0.0.1
SERVER_PORT=8800

# JWT configuration
JWT_SECRET_KEY=your-secret-key-here
JWT_EXPIRATION_HOURS=24

# Google OAuth configuration
GOOGLE_CLIENT_ID=your-google-client-id
```

#### Initialize Database

1. Log in to [Neon Console](https://console.neon.tech/)
2. Use SQL Editor to execute the SQL statements in the `backend/init_bello_db.sql` file
3. Or use psql command:
   ```bash
   psql <your-neon-connection-string> -f backend/init_bello_db.sql
   ```

#### Start Backend Service

```bash
cd backend
python app.py
```

The backend service will start at `http://127.0.0.1:8800`.

### 3. Frontend Setup

#### Install Dependencies

```bash
cd frontend
npm install
```

#### Environment Variables Configuration (Optional, required for Google Maps functionality)

Copy `frontend/.env.example` and rename it to `frontend/.env`, then fill in the following configuration:

```env
# Google Maps API Key (for location autocomplete and map display)
VITE_GOOGLE_MAPS_API_KEY=your-google-maps-api-key
```

> 📍 You need to enable **Maps JavaScript API** and **Places API** in [Google Cloud Console](https://console.cloud.google.com/apis/credentials)

#### Start Development Server

```bash
npm run dev
```

The frontend service will start at `http://127.0.0.1:5173`.

### 4. Access the Application

Open your browser and visit `http://127.0.0.1:5173`

## 📦 Deployment

### Vercel Deployment

This project is configured for Vercel deployment with automatic deployment support:

1. Push the project to GitHub
2. Import the project in Vercel
3. Set environment variables (same as `.env`)
4. Vercel will automatically build and deploy

For detailed configuration, please refer to `vercel.json`.

### Environment Variables Setup

Add the following environment variables in Vercel project settings:

- `DATABASE_URL`
- `JWT_SECRET_KEY`
- `JWT_EXPIRATION_HOURS`
- `GOOGLE_CLIENT_ID`
- `VITE_GOOGLE_MAPS_API_KEY` (for frontend, used for location features)

## 🏗️ System Architecture

### Frontend Architecture

- **Component-based Design**: Uses Vue 3 Composition API
- **Route Management**: Vue Router implements SPA routing with permission guards
- **State Management**: Uses localStorage to store authentication state
- **API Encapsulation**: Unified API request handling with automatic JWT Token addition

### Backend Architecture

- **RESTful API**: Follows REST design principles
- **Modular Design**: Uses Flask Blueprint to organize routes
- **Authentication Mechanism**: JWT Token authentication with decorator-protected endpoints
- **Database Abstraction**: `DB_utils.py` encapsulates all database operations

### Database Design

- **Normalization**: Complies with 4NF normalization
- **Main Tables**:
  - `USER`: User basic information
  - `USER_DETAIL`: User detailed information
  - `MEETING`: Meetup information
  - `PARTICIPATION`: Participation records
  - `FRIENDSHIP`: Friend relationships
  - `PRIVATE_MESSAGE`: Private messages
  - `CHATTING_ROOM`: Meetup chat records

## 🔑 Key Features

### Authentication System

- **JWT Token**: Issues JWT Token upon login, valid for 24 hours
- **Route Protection**: Unauthenticated users accessing protected routes are automatically redirected to the login page
- **Google OAuth**: Supports Google account login (embedded browsers will show prompts)

### Friend System

- **Friend Requests**: Send, accept, and reject friend requests
- **Friend List**: View all friends and their online status
- **User Search**: Search users and send friend requests
- **Profile Viewing**: View other users' public profiles

### Chat System

- **Private Chat**: One-on-one real-time chat
- **Meetup Chat**: Group chat rooms with support for viewing all participants
- **Online Status**: Real-time display of user online/offline status
  - Heartbeat mechanism: Frontend sends status updates every 30 seconds
  - Logic: Active within 60 seconds is considered online
- **Message History**: Saves and displays chat records

### Meetup System

- **Meetup Types**: Lunch, coffee/afternoon tea, dinner, drinks, language exchange
- **Language Filtering**: Supports multiple language tags
- **Participation Management**: Join, leave, cancel meetups
- **Status Management**: Ongoing, finished, cancelled

## 🧪 Development

### Frontend Development

```bash
cd frontend
npm run dev      # Start development server
npm run build    # Build production version
npm run lint     # Code linting
```

### Backend Development

```bash
cd backend
python app.py    # Start Flask development server
```

### Database Operations

All database operations are performed through the `DatabaseManager` class in `DB_utils.py`, ensuring consistent connection management and error handling.

## 📝 API Endpoints

### Authentication
- `POST /login` - User login
- `POST /signup` - User registration
- `POST /auth/google` - Google OAuth login
- `GET /auth/google/client-id` - Get Google Client ID

### Meetups
- `GET /meetings` - Get meetup list
- `POST /create-meeting` - Create meetup
- `POST /join-meeting` - Join meetup
- `POST /leave-meeting` - Leave meetup
- `GET /my-meetings/:user_id` - Get my meetups

### Chat
- `GET /my-chats` - Get chat list
- `GET /private-chat/history` - Get private chat history
- `POST /private-chat/send` - Send private message
- `GET /meeting-chat/:meeting_id` - Get meetup chat history
- `POST /meeting-chat/send` - Send meetup message

### Friends
- `GET /friends` - Get friend list
- `POST /friends/add` - Send friend request
- `POST /friends/accept` - Accept friend request
- `POST /friends/reject` - Reject friend request
- `GET /friends/status/:user_id` - Check friendship status

### Profile
- `GET /user-profile/:user_id` - Get user profile
- `GET /friends/user-profile/:user_id` - Get other user's public profile
- `POST /update-profile` - Update profile
- `POST /update-avatar` - Update avatar

### Admin
- `GET /admin/users` - Get all user list (supports pagination and search)
- `GET /admin/users/:user_id` - Get user detailed information
- `POST /admin/users/:user_id/remove` - Remove user
- `GET /admin/meetings` - Get all meetup list
- `GET /admin/all-private-chats` - Get all private chat conversation lists
- `POST /admin/chat-history` - Get chat history between two specified users
- `GET /admin/all-meeting-chats` - Get all meetup chat lists with chat records
- `GET /admin/meeting-chat/:meeting_id` - Get specified meetup's chat history

All endpoints requiring authentication need to include `Authorization: Bearer <token>` in the request header.

## 🔒 Security Features

- **JWT Authentication**: All API requests require a valid JWT Token
- **Role Permissions**: Admin features require `Admin` role
- **CORS Configuration**: Properly configured cross-origin requests
- **Input Validation**: Backend validates all input parameters
- **SQL Injection Protection**: Uses parameterized queries

## 📄 License

This project is a final project work.

## 👥 Contributing

This project is for educational purposes. Suggestions and improvements are welcome.

---

**Developers**: Final Project Team  
**Last Updated**: January 2025
