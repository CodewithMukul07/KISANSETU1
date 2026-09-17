# KisanSetu - Quick Start (5 Minutes)

## One-Command Setup (PowerShell)

Copy and run this complete setup script:

```powershell
# Navigate to project directory
cd "E:\SIH\site 3"

# Install all dependencies
Write-Host "Installing dependencies..." -ForegroundColor Green
npm install
cd backend
npm install
cd ../frontend
npm install
cd ..

# Start MongoDB (if not already running)
Write-Host "`nStarting MongoDB..." -ForegroundColor Green
Start-Process mongod -WindowStyle Hidden

# Seed demo data
Write-Host "`nSeeding demo data..." -ForegroundColor Green
cd backend
npm run seed
cd ..

# Start the application
Write-Host "`nStarting KisanSetu..." -ForegroundColor Green
Write-Host "Backend: http://localhost:5000" -ForegroundColor Cyan
Write-Host "Frontend: http://localhost:5173" -ForegroundColor Cyan
Write-Host "`nDemo Accounts:" -ForegroundColor Yellow
Write-Host "Farmer: ramesh@demo.com / demo123" -ForegroundColor White
Write-Host "Admin: admin@demo.com / admin123" -ForegroundColor White
npm run dev
```

## Manual Setup (Step by Step)

### 1. Install Dependencies (2 min)
```powershell
npm install
cd backend && npm install
cd ../frontend && npm install && cd ..
```

### 2. Start MongoDB
```powershell
mongod
# Or if MongoDB is a service: net start MongoDB
```

### 3. Seed Demo Data (30 sec)
```powershell
cd backend
npm run seed
cd ..
```

### 4. Run Application (1 min)
```powershell
npm run dev
```

Wait for both servers to start, then open:
- **Frontend:** http://localhost:5173
- **Backend API:** http://localhost:5000

## First Login

### Option 1: Use Demo Buttons
1. Click "Login"
2. Click "Demo Farmer" or "Demo Admin" button
3. Click "Sign In"

### Option 2: Manual Entry
**Farmer:**
- Email: ramesh@demo.com
- Password: demo123

**Admin:**
- Email: admin@demo.com
- Password: admin123

## Quick Demo Flow (2 Minutes)

### As Farmer:
1. Login → See active token K-001 on dashboard
2. Click "View Queue" → See live position
3. Click "Why Delayed?" → See analysis
4. Try Voice Assistant (Chrome/Edge only)
5. Switch language to Hindi (हिंदी)

### As Admin:
1. Login → See today's statistics
2. Click "Queue Management" on Meerut Mandi
3. Click "Call Next" → Process next farmer
4. Change token status using dropdown
5. See stats update in real-time

### See Real-Time Updates:
1. Open two browser windows
2. Window 1: Login as farmer
3. Window 2: Login as admin
4. Admin: Change farmer's token status
5. Watch farmer's dashboard update instantly! ⚡

## Troubleshooting

### MongoDB Not Running
```powershell
# Check if MongoDB is running
Get-Process mongod

# Start MongoDB
mongod
```

### Port Already in Use
```powershell
# Find and kill process on port 5000
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# Or change port in backend/.env
```

### Cannot Find Module Errors
```powershell
# Clear and reinstall
Remove-Item -Recurse -Force node_modules, backend/node_modules, frontend/node_modules
npm install
cd backend && npm install
cd ../frontend && npm install
```

### Frontend Not Loading
```powershell
# Check if backend is running
curl http://localhost:5000/api/health

# Check frontend is running
curl http://localhost:5173
```

## What's Working?

✅ **Authentication** - Login/Register/Logout
✅ **Real-Time Updates** - Socket.IO live queue updates
✅ **Farmer Portal** - Dashboard, Booking, Queue Tracking
✅ **Admin Portal** - Queue Management, Status Updates
✅ **Multilingual** - English ⇄ Hindi
✅ **Voice Assistant** - Voice commands (Chrome/Edge)
✅ **3D Graphics** - Animated hero section
✅ **Notifications** - Real-time alerts
✅ **Responsive** - Mobile/Tablet/Desktop
✅ **Demo Mode** - Full working data

## Next Steps

1. Read [README.md](README.md) for full documentation
2. Read [TESTING.md](TESTING.md) for testing guide
3. Read [setup.md](setup.md) for detailed setup
4. Explore the application features
5. Customize for your needs

## Support

**Common Issues:**
- MongoDB connection: Check if MongoDB is running
- Socket not connecting: Check CORS settings in backend/server.js
- Voice not working: Use Chrome or Edge
- 3D not rendering: Check browser WebGL support

**Check Console for Errors:**
- Browser: Press F12 → Console tab
- Backend: Check terminal running backend
- Frontend: Check terminal running frontend

---

**🚀 You're all set! Happy coding!**

**Built for SIH 2026 - SIH26032**
