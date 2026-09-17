# KisanSetu Setup Guide

## Quick Start (5 minutes)

### 1. Install Dependencies
```powershell
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

### 2. Start MongoDB
Make sure MongoDB is running on your system. If not installed:
- Download from: https://www.mongodb.com/try/download/community
- Or use MongoDB Atlas (cloud)

### 3. Seed Demo Data
```powershell
cd backend
npm run seed
```

This creates:
- 3 Demo Farmers (ramesh@demo.com, suresh@demo.com, vijay@demo.com - all with password: demo123)
- 1 Demo Admin (admin@demo.com / admin123)
- 3 Mandis with active queues
- Sample tokens and notifications

### 4. Run the Application
```powershell
# From root directory
npm run dev
```

This will start:
- Backend on http://localhost:5000
- Frontend on http://localhost:5173

### 5. Test the Application

#### Farmer Flow:
1. Open http://localhost:5173
2. Click "Login" (or use demo button on login page)
3. Login as: `ramesh@demo.com` / `demo123`
4. View your active token K-001 on dashboard
5. Check live queue status
6. Try voice assistant
7. View "Why is my procurement delayed?"

#### Admin Flow:
1. Open http://localhost:5173/login
2. Click "Demo Admin" button or login as: `admin@demo.com` / `admin123`
3. View today's statistics
4. Click on "Meerut Mandi" to manage queue
5. Click "Call Next" to process next farmer
6. Update token status using dropdown
7. See real-time updates

## Features to Demonstrate

### 1. Real-Time Queue Updates
- Login as both farmer and admin in different browsers
- Admin calls next farmer → Farmer sees immediate update
- Admin changes status → Farmer dashboard updates live

### 2. Multilingual Support
- Click language icon in navbar
- Switch between English and Hindi
- All text, notifications, and messages translate

### 3. Voice Assistant
- Navigate to Voice Assistant page
- Click microphone button
- Say: "What is my token?"
- Say: "How many farmers are ahead?"
- Say: "When is my turn?"
- Say: "Why is my procurement delayed?"

### 4. Smart Notifications
- Check notifications page
- See real-time updates when admin changes status
- Notifications in both English and Hindi

### 5. 3D Hero Section
- Visit homepage (logout first)
- See floating 3D spheres with animations
- Smooth parallax scrolling

### 6. Booking Flow
- Login as vijay@demo.com
- Go to Mandis → Select any mandi
- Book a new slot
- See token generation
- Track in dashboard

## API Testing

Test API endpoints using curl or Postman:

```powershell
# Health Check
curl http://localhost:5000/api/health

# Login
curl -X POST http://localhost:5000/api/auth/login `
  -H "Content-Type: application/json" `
  -d '{\"email\":\"ramesh@demo.com\",\"password\":\"demo123\"}'

# Get Mandis
curl http://localhost:5000/api/mandis
```

## Troubleshooting

### MongoDB Connection Error
- Ensure MongoDB is running: `mongod`
- Check connection string in `backend/.env`

### Port Already in Use
- Change ports in:
  - `backend/.env` (PORT=5000)
  - `frontend/.env` (VITE_API_URL)
  - `frontend/vite.config.js` (server.port)

### Socket.IO Not Connecting
- Check CORS settings in `backend/server.js`
- Verify frontend SOCKET_URL in `frontend/.env`

### Dependencies Not Installing
- Delete `node_modules` and `package-lock.json`
- Run `npm install` again
- Ensure Node.js version is 16+

## Project Structure

```
site 3/
├── backend/
│   ├── config/          # Database configuration
│   ├── models/          # MongoDB models
│   ├── routes/          # API routes
│   ├── middleware/      # Auth middleware
│   ├── utils/           # Helper functions
│   ├── seeders/         # Demo data seeder
│   └── server.js        # Express + Socket.IO server
├── frontend/
│   ├── src/
│   │   ├── components/  # Reusable components
│   │   ├── pages/       # Page components
│   │   ├── store/       # Zustand state management
│   │   ├── utils/       # API, socket, translations
│   │   └── App.jsx      # Main app with routes
│   └── index.html
└── README.md
```

## Demo Accounts

| Role | Email | Password | Description |
|------|-------|----------|-------------|
| Farmer | ramesh@demo.com | demo123 | Has active token K-001 (being verified) |
| Farmer | suresh@demo.com | demo123 | Has active token K-002 (arrived) |
| Farmer | vijay@demo.com | demo123 | Has active token K-003 (booked) |
| Admin | admin@demo.com | admin123 | Can manage all mandis |

## Performance Tips

1. **Real-time Updates**: Socket connections auto-reconnect
2. **Fallback Polling**: If sockets fail, app polls API every 30s
3. **Voice Assistant**: Works in Chrome, Edge, Safari (not Firefox)
4. **3D Graphics**: May lag on low-end devices, optimized for modern browsers

## Next Steps

After setup, you can:
1. Customize mandi data in `backend/seeders/index.js`
2. Add more translations in `frontend/src/utils/translations.js`
3. Modify 3D scene in `frontend/src/components/3D/Hero3D.jsx`
4. Add more voice commands in `frontend/src/pages/VoiceAssistant.jsx`
5. Extend analytics in admin dashboard

## Support

For issues or questions:
- Check console for errors (F12)
- Verify all services are running
- Check MongoDB logs
- Review API responses in Network tab

---

**Built for SIH 2026 - Problem Statement SIH26032**
