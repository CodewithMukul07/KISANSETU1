<<<<<<< HEAD
# KISANSETU1
=======
# KisanSetu - Smart Queue Management for Mandi Procurement

**SIH 2026 - Problem Statement SIH26032**

A fully functional, production-quality full-stack web application that connects farmers with procurement centres/mandis, eliminating long waiting times with real-time queue tracking, smart notifications, and multilingual support.

## 🌟 Features

### For Farmers
- **Digital Token Generation**: Get instant token upon slot booking
- **Real-Time Queue Tracking**: See live queue position and estimated wait time
- **Smart Notifications**: Receive updates on queue position, turn approaching, and status changes
- **Multilingual Support**: English and Hindi language support
- **Voice Assistant**: Voice commands for hands-free interaction
- **Why Delayed?**: AI-powered delay analysis with explanations
- **Mandi Discovery**: Search and explore nearby mandis with live queue info

### For Mandi Administrators
- **Queue Management**: Call next farmer, update status, manage counters
- **Live Dashboard**: Real-time statistics and analytics
- **Procurement Tracking**: Complete procurement lifecycle management
- **Farmer Management**: View farmer details and procurement history
- **Analytics**: Daily reports, average processing time, capacity utilization

### Technical Features
- **Real-Time Updates**: Socket.IO for live queue and status updates
- **3D Animations**: Three.js hero section with interactive elements
- **Smooth Animations**: Framer Motion throughout the application
- **Responsive Design**: Mobile-first, works on all devices
- **Offline Fallback**: Graceful degradation when real-time connection fails

## 🚀 Tech Stack

### Frontend
- React 18
- Vite
- Tailwind CSS
- Framer Motion (animations)
- Three.js / React Three Fiber (3D graphics)
- Recharts (data visualization)
- Socket.IO Client (real-time)
- Zustand (state management)
- Axios (API calls)

### Backend
- Node.js
- Express.js
- MongoDB (database)
- Mongoose (ODM)
- Socket.IO (real-time)
- JWT (authentication)
- Bcrypt (password hashing)

## 📋 Prerequisites

- Node.js (v16 or higher)
- MongoDB (v5 or higher)
- npm or yarn

## 🛠️ Installation & Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd site 3
```

### 2. Install Dependencies
```bash
# Install root dependencies
npm install

# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
cd ..
```

### 3. Setup MongoDB
Make sure MongoDB is running on your system:
```bash
# Start MongoDB (if not running)
mongod
```

### 4. Configure Environment Variables
The `.env` file is already configured in `backend/.env`:
- MongoDB URI: `mongodb://localhost:27017/kisansetu`
- Port: `5000`
- JWT Secret: Pre-configured (change in production)

### 5. Seed Demo Data
```bash
cd backend
npm run seed
```

This will create:
- **3 Demo Farmers**:
  - ramesh@demo.com / demo123
  - suresh@demo.com / demo123
  - vijay@demo.com / demo123
- **1 Demo Admin**:
  - admin@demo.com / admin123
- **3 Mandis** with active queues and tokens
- Sample notifications and procurement records

### 6. Run the Application

#### Option A: Run Both (Frontend + Backend)
```bash
# From root directory
npm run dev
```

#### Option B: Run Separately
```bash
# Terminal 1 - Backend
cd backend
npm run dev

# Terminal 2 - Frontend
cd frontend
npm run dev
```

### 7. Access the Application
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:5000
- **API Health Check**: http://localhost:5000/api/health

## 🎯 Demo Flow

### As a Farmer:
1. **Login**: Use `ramesh@demo.com` / `demo123`
2. **Dashboard**: View your active token (K-001) with real-time queue position
3. **Live Queue**: See farmers ahead, estimated wait time, and turn time
4. **Why Delayed?**: Get intelligent delay analysis
5. **Mandi Explorer**: Browse other mandis and their queues
6. **Voice Assistant**: Try voice commands

### As an Admin:
1. **Login**: Use `admin@demo.com` / `admin123`
2. **Admin Dashboard**: View today's statistics across all mandis
3. **Queue Management**: Select Meerut Mandi to manage queue
4. **Call Next**: Process the next farmer in queue
5. **Update Status**: Change procurement status (verification → quality check → procurement → completed)
6. **Analytics**: View processing times, completion rates, and capacity utilization

## 🔑 Demo Accounts

### Farmers
| Email | Password | Token | Status |
|-------|----------|-------|--------|
| ramesh@demo.com | demo123 | K-001 | Being Verified |
| suresh@demo.com | demo123 | K-002 | Arrived |
| vijay@demo.com | demo123 | K-003 | Booked |

### Admin
| Email | Password | Role |
|-------|----------|------|
| admin@demo.com | admin123 | Mandi Administrator |

## 📱 Key Pages

### Public
- `/` - Landing page with 3D hero
- `/login` - Login page
- `/register` - Registration page

### Farmer Portal
- `/dashboard` - Farmer dashboard with token details
- `/mandis` - Mandi explorer
- `/mandis/:id` - Mandi details
- `/book-slot/:mandiId` - Slot booking flow
- `/my-tokens` - All tokens history
- `/queue/:tokenId` - Live queue tracking
- `/voice-assistant` - Voice assistant
- `/notifications` - Notification center

### Admin Portal
- `/admin` - Admin dashboard
- `/admin/queue/:mandiId` - Queue management

## 🔧 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user

### Mandis
- `GET /api/mandis` - Get all mandis
- `GET /api/mandis/:id` - Get mandi details
- `GET /api/mandis/:id/slots` - Get available slots

### Tokens
- `POST /api/tokens/book` - Book a slot
- `GET /api/tokens/my-tokens` - Get farmer's tokens
- `GET /api/tokens/active` - Get active token
- `GET /api/tokens/:id` - Get token by ID

### Queue
- `GET /api/queue/mandi/:mandiId` - Get mandi queue
- `GET /api/queue/token/:tokenId` - Get token queue status
- `GET /api/queue/delay-analysis/:tokenId` - Get delay analysis

### Admin
- `GET /api/admin/dashboard` - Get dashboard stats
- `GET /api/admin/queue/:mandiId` - Get queue for management
- `POST /api/admin/call-next/:mandiId` - Call next farmer
- `PUT /api/admin/token/:tokenId/status` - Update token status
- `GET /api/admin/analytics/:mandiId` - Get analytics

### Notifications
- `GET /api/notifications` - Get user notifications
- `PUT /api/notifications/:id/read` - Mark as read
- `PUT /api/notifications/read-all` - Mark all as read

## 🔄 Real-Time Features

The application uses Socket.IO for real-time updates:

### Socket Events
- `queue-update` - Emitted when queue changes
- `status-update` - Emitted when token status changes
- `notification` - Emitted for new notifications

### Socket Rooms
- `mandi-{mandiId}` - For mandi-specific updates
- `token-{tokenId}` - For token-specific updates

## 🌐 Multilingual Support

Switch between English and Hindi:
- UI translations for all text
- Status messages in both languages
- Notifications in both languages
- Mandi names in local language

## 🎤 Voice Assistant

Supported voice commands:
- "What is my token?"
- "How many farmers are ahead of me?"
- "When is my turn?"
- "Why is my procurement delayed?"

Fallback to text input if voice API unavailable.

## 📊 Database Models

- **User**: Farmers and admins
- **Mandi**: Procurement centers with capacity and timings
- **Token**: Booking and queue tokens
- **Queue**: Daily queue for each mandi
- **Notification**: User notifications
- **ProcurementRecord**: Completed procurement history

## 🎨 Design System

### Colors
- Primary Green: `#22c55e` (Agriculture/Growth)
- Variants: 50-900 scale
- Agri palette: Wheat, Rice, Green, Earth tones

### Components
- Glass morphism cards
- Gradient backgrounds
- Smooth transitions
- Floating animations
- Skeleton loaders

## 🚧 Future Enhancements

- SMS/WhatsApp notifications
- GPS-based mandi recommendations
- Payment gateway integration
- Multi-crop price tracking
- Weather-based queue predictions
- Mobile app (React Native)
- Admin analytics dashboard expansion

## 📄 License

MIT License

## 👥 Team

SIH 2026 - Team KisanSetu

---

**Note**: This is a demo application for SIH 2026. All data is seeded and simulated. For production deployment, ensure proper security measures, environment configuration, and infrastructure setup.
>>>>>>> 467b13a (first commit)
