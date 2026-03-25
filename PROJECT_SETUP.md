# 📖 PROJECT SETUP GUIDE

Complete setup instructions for Social Media Analytics SaaS tool.

## 🎯 Quick Start (5 minutes)

### Prerequisites
- Node.js 16+ ([Download](https://nodejs.org))
- MongoDB ([Download](https://www.mongodb.com/try/download/community))
- Git

### Three Commands to Run Everything

```bash
# Terminal 1: Start MongoDB
mongod

# Terminal 2: Start Backend
cd backend
npm install
npm run dev

# Terminal 3: Start Frontend
cd frontend
npm install
npm run dev
```

Then visit: **http://localhost:3000**

---

## 📋 Step-by-Step Setup

### Step 1: Check Prerequisites

```powershell
node --version      # Should be 16 or higher
npm --version       # Should be 8 or higher
git --version       # Any version
```

### Step 2: Install MongoDB (Windows)

1. Download: https://www.mongodb.com/try/download/community
2. Choose "Windows .msi"
3. Run installer: Click "Next" → "Install" → "Finish"
4. MongoDB installs to `C:\Program Files\MongoDB\Server\5.0\bin`

**Or use MongoDB Atlas (Cloud):**
1. Go to: https://www.mongodb.com/cloud/atlas
2. Create free account
3. Create cluster
4. Get connection string
5. Update `backend/.env`: Replace MONGO_URI

### Step 3: Install Dependencies

**Backend:**
```powershell
cd backend
npm install
```

**Frontend:**
```powershell
cd frontend
npm install
```

### Step 4: Configure Environment

**Backend** (`backend/.env`):
```env
MONGO_URI=mongodb://localhost:27017/social-media-analytics
JWT_SECRET=your_secret_key_here
PORT=5000
NODE_ENV=development
OPENAI_API_KEY=          # Optional - leave empty
```

**Frontend** (`frontend/.env`):
```env
VITE_API_URL=http://localhost:5000/api
```

### Step 5: Start All Services

**Open 3 Terminals:**

**Terminal 1 - MongoDB:**
```powershell
mongod
```
✅ Should show: `waiting for connections on port 27017`

**Terminal 2 - Backend:**
```powershell
cd backend
npm run dev
```
✅ Should show:
```
╔════════════════════════════════════════════════════╗
║   Social Media Analytics Backend                   ║
║   Server running on http://localhost:5000          ║
╚════════════════════════════════════════════════════╝
```

**Terminal 3 - Frontend:**
```powershell
cd frontend
npm run dev
```
✅ Should show:
```
VITE v4.5.0  ready in XXX ms
➜  Local:   http://localhost:3000/
```

### Step 6: Test Application

1. Visit: **http://localhost:3000**
2. Click **"Sign Up"**
3. Enter email and password
4. Create account
5. Click **"Create New Workspace"**
6. Fill in workspace details
7. Click **"View Analytics"**
8. See mock analytics and AI insights ✅

---

## 🚀 Available Commands

### Backend
```bash
npm run dev      # Start development server with auto-reload
npm start        # Start production server
```

### Frontend
```bash
npm run dev      # Start Vite dev server
npm run build    # Build for production
npm run preview  # Preview production build
```

---

## 🔐 Optional: Add Real AI Insights

Get OpenAI API key and add to `backend/.env`:

```env
OPENAI_API_KEY=sk-proj-your_key_here
```

Restart backend for real AI insights instead of mock data.

---

## 🆘 Common Issues

### MongoDB Error: "mongod not found"
**Solution:** 
1. Install MongoDB from: https://www.mongodb.com/try/download/community
2. Or use MongoDB Atlas (cloud)

### Port Already in Use
**Backend (5000):**
```powershell
netstat -ano | findstr :5000
taskkill /PID <PID> /F
```

**Frontend (3000):**
```powershell
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

### Module Not Found
```powershell
# In that directory:
rm -r node_modules -Force
npm install
```

### Cannot Connect to MongoDB
- Check MongoDB is running: `mongod` in Terminal 1
- Or update `MONGO_URI` in `.env` to MongoDB Atlas connection string

### Frontend Blank Page
1. Press `F12` to open DevTools
2. Check Console tab for errors
3. Check Network tab for failed requests
4. Ensure all 3 servers are running

---

## 📊 API Endpoints

### Authentication
- `POST /api/auth/signup` - Register user
- `POST /api/auth/login` - Login user

### Workspaces
- `POST /api/workspaces` - Create workspace
- `GET /api/workspaces` - Get all workspaces
- `GET /api/workspaces/:id` - Get workspace by ID
- `PUT /api/workspaces/:id` - Update workspace
- `DELETE /api/workspaces/:id` - Delete workspace

### Analysis
- `GET /api/analysis/:workspaceId` - Get analytics and insights

---

## 🔄 Project Structure

```
social-media-tool/
├── backend/                    # Node.js Express Server
│   ├── src/
│   │   ├── config/            # Database & app config
│   │   ├── controllers/       # Business logic
│   │   ├── models/            # MongoDB schemas
│   │   ├── routes/            # API endpoints
│   │   ├── middleware/        # Auth & error handling
│   │   └── services/          # AI service layer
│   ├── server.js              # Main entry point
│   ├── package.json           # Dependencies
│   ├── .env                   # Environment config
│   └── README.md
│
└── frontend/                   # React Vite App
    ├── src/
    │   ├── components/        # React components
    │   ├── pages/             # Page components
    │   ├── services/          # API client
    │   ├── styles/            # Global CSS
    │   ├── App.jsx            # Main app component
    │   └── main.jsx           # React entry point
    ├── index.html             # HTML template
    ├── vite.config.js         # Vite build config
    ├── package.json           # Dependencies
    ├── .env                   # Environment config
    └── README.md
```

---

## 💾 Technology Stack

### Backend
- Express.js 4.18.2 - Web framework
- MongoDB 5.0+ - Database
- Mongoose 7.5.0 - ODM
- JWT 9.0.2 - Authentication
- bcryptjs 2.4.3 - Password hashing
- Nodemon 3.0.1 - Dev auto-reload

### Frontend
- React 18.2.0 - UI library
- Vite 4.5.0 - Build tool
- React Router 6.16.0 - Routing
- Axios 1.5.0 - HTTP client

---

## 📚 Additional Resources

- [Project File Structure](PROJECT_FILES.md) - Detailed file organization
- [API Reference](API_REFERENCE.md) - Complete API documentation
- [Troubleshooting](TROUBLESHOOTING.md) - Common issues and solutions

---

## 🎯 Features

✅ User authentication with JWT  
✅ Password hashing with bcryptjs  
✅ Multiple workspaces per user  
✅ Mock analytics data  
✅ AI-powered insights (OpenAI optional)  
✅ Protected routes  
✅ Error handling middleware  
✅ CORS enabled  
✅ Clean, responsive UI  
✅ Production-ready code  

---

## 🚀 Deployment

### Backend (Heroku, Railway, AWS, etc.)
1. Set environment variables in deployment platform
2. Deploy from Git
3. MongoDB Atlas required (not local)

### Frontend (Vercel, Netlify, etc.)
1. Set `VITE_API_URL` to production backend URL
2. Deploy from Git
3. Automatic builds

---

## 📞 Support

For issues:
1. Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
2. Review browser console (F12)
3. Check terminal output
4. Verify all 3 servers running

---

## 📄 License

MIT License - Free for personal and commercial use

---

**Everything is ready to use. Just follow the 3 commands above!** 🎉
