# 📁 PROJECT FILE STRUCTURE

Complete guide to understanding the codebase organization.

---

## 🏗️ Overall Structure

```
social-media-tool/
├── backend/                          # Node.js Express Backend
├── frontend/                         # React Vite Frontend
├── PROJECT_SETUP.md                  # THIS FILE - Setup instructions
├── PROJECT_FILES.md                  # File structure documentation
├── API_REFERENCE.md                  # API endpoints reference
├── TROUBLESHOOTING.md                # Common issues & fixes
├── README.md                         # Project overview
├── .gitignore                        # Git ignore rules
└── node_modules/                     # (Auto-created by npm)
```

---

## 📂 BACKEND STRUCTURE

### `/backend` - Express.js Server

```
backend/
├── src/                              # Source code
│   ├── config/                       # Configuration
│   │   ├── config.js                 # Environment variables loader
│   │   └── database.js               # MongoDB connection setup
│   │
│   ├── models/                       # Database Schemas
│   │   ├── User.js                   # User schema (email, password, name)
│   │   └── Workspace.js              # Workspace schema (profile, competitors)
│   │
│   ├── controllers/                  # Business Logic
│   │   ├── authController.js         # Signup & login logic
│   │   ├── workspaceController.js    # Workspace CRUD operations
│   │   └── analysisController.js     # Analytics & insights logic
│   │
│   ├── routes/                       # API Endpoint Routes
│   │   ├── authRoutes.js             # POST /auth/signup, /auth/login
│   │   ├── workspaceRoutes.js        # CRUD workspaces endpoints
│   │   └── analysisRoutes.js         # GET /analysis/:workspaceId
│   │
│   ├── middleware/                   # Express Middleware
│   │   ├── authenticateToken.js      # JWT verification (protects routes)
│   │   └── errorHandler.js           # Global error handling
│   │
│   └── services/                     # Service Layer
│       └── aiService.js              # AI insights generation (OpenAI/mock)
│
├── server.js                         # Main entry point - starts Express app
├── package.json                      # Dependencies & scripts
├── .env                              # Environment variables
├── .env.example                      # Example environment file
├── .env.production                   # Production config template
├── .gitignore                        # Git ignore rules
├── node_modules/                     # Installed packages (auto-created)
└── README.md                         # Backend-specific documentation
```

### Backend Key Files

#### `/src/config/config.js`
Loads environment variables from `.env`:
```javascript
- MONGO_URI: MongoDB connection string
- JWT_SECRET: Secret key for JWT tokens
- OPENAI_API_KEY: OpenAI API key (optional)
- PORT: Server port (default 5000)
- NODE_ENV: development or production
```

#### `/src/models/User.js`
MongoDB User schema:
```javascript
{
  email: String (unique),
  password: String (hashed),
  name: String,
  createdAt: Date,
  updatedAt: Date
}
```

#### `/src/models/Workspace.js`
MongoDB Workspace schema:
```javascript
{
  name: String,
  userId: ObjectId (references User),
  instagramProfile: String,
  competitors: [String],
  createdAt: Date,
  updatedAt: Date
}
```

#### `/src/controllers/authController.js`
Handles: Signup and Login
- `exports.signup` - Create new user account
- `exports.login` - Authenticate user and return JWT token

#### `/src/controllers/workspaceController.js`
Handles: Workspace CRUD
- `exports.createWorkspace` - Create new workspace
- `exports.getWorkspaces` - Get all user workspaces
- `exports.getWorkspaceById` - Get single workspace
- `exports.updateWorkspace` - Update workspace
- `exports.deleteWorkspace` - Delete workspace

#### `/src/controllers/analysisController.js`
Handles: Analytics and AI insights
- `exports.getAnalysis` - Get mock analytics + AI insights for workspace

#### `/src/services/aiService.js`
AI Service Layer:
- Can use OpenAI API or mock data
- Generates gaps, suggestions, content ideas
- Easy to replace with Claude or other AI

#### `/src/middleware/authenticateToken.js`
JWT verification middleware:
- Checks `Authorization: Bearer <token>` header
- Validates token and adds `req.user` to request
- Returns 401 if invalid

#### `/src/middleware/errorHandler.js`
Global error handler:
- Catches all errors
- Returns proper error responses
- Handles validation, JWT, and database errors

#### `/src/routes/authRoutes.js`
Auth endpoints:
```
POST /api/auth/signup  - Create account
POST /api/auth/login   - Login user
```

#### `/src/routes/workspaceRoutes.js`
Workspace endpoints (all require JWT):
```
POST /api/workspaces         - Create
GET /api/workspaces          - Get all
GET /api/workspaces/:id      - Get one
PUT /api/workspaces/:id      - Update
DELETE /api/workspaces/:id   - Delete
```

#### `/src/routes/analysisRoutes.js`
Analysis endpoint (requires JWT):
```
GET /api/analysis/:workspaceId - Get analytics + insights
```

#### `server.js`
Main entry point:
- Loads `.env` with dotenv
- Creates Express app
- Connects to MongoDB
- Mounts all routes
- Adds error handler
- Starts server on configured PORT

---

## 📂 FRONTEND STRUCTURE

### `/frontend` - React Vite Application

```
frontend/
├── src/                              # Source code
│   ├── components/                   # Reusable React components
│   │   └── NavBar.jsx                # Navigation bar with auth state
│   │
│   ├── pages/                        # Page-level components
│   │   ├── HomePage.jsx              # Home page with hero section
│   │   ├── LoginPage.jsx             # Login form page
│   │   ├── SignupPage.jsx            # Signup form page
│   │   ├── DashboardPage.jsx         # List workspaces, create form
│   │   └── WorkspacePage.jsx         # Workspace analytics detail page
│   │
│   ├── services/                     # API service layer
│   │   └── api.js                    # Axios HTTP client with interceptors
│   │
│   ├── styles/                       # CSS styling
│   │   └── global.css                # Global styles, buttons, forms, cards
│   │
│   ├── App.jsx                       # Main app component with routing
│   └── main.jsx                      # React entry point (renders App)
│
├── index.html                        # HTML template
├── vite.config.js                    # Vite build configuration
├── package.json                      # Dependencies & scripts
├── .env                              # Environment variables
├── .env.example                      # Example environment file
├── .env.production                   # Production config template
├── .gitignore                        # Git ignore rules
├── node_modules/                     # Installed packages (auto-created)
└── README.md                         # Frontend-specific documentation
```

### Frontend Key Files

#### `index.html`
HTML template:
- Single `<div id="root">` for React
- Links Vite module: `<script src="/src/main.jsx">`
- Minimal, renders everything from JavaScript

#### `src/main.jsx`
React entry point:
- Imports React and ReactDOM
- Creates root element
- Renders `<App />` component

#### `src/App.jsx`
Main app component:
- Sets up React Router
- Defines all routes
- Renders `<NavBar />`
- Routes:
  - `/` → HomePage
  - `/login` → LoginPage
  - `/signup` → SignupPage
  - `/dashboard` → DashboardPage (protected)
  - `/workspace/:id` → WorkspacePage (protected)

#### `src/pages/HomePage.jsx`
Home/landing page:
- Hero section with gradient background
- "Sign Up" and "Login" buttons
- Feature highlights
- Not authenticated required

#### `src/pages/LoginPage.jsx`
Login page:
- Email input
- Password input
- "Login" button
- Link to signup
- Stores JWT in localStorage
- Redirects to /dashboard on success

#### `src/pages/SignupPage.jsx`
Signup page:
- Name input
- Email input
- Password input
- Confirm password input
- "Sign Up" button
- Link to login
- Auto-login after signup
- Redirects to /dashboard

#### `src/pages/DashboardPage.jsx`
Workspace dashboard:
- List all user workspaces
- "Create New Workspace" button
- Form to create workspace
- Workspace cards with info
- Button to view analytics for each workspace

#### `src/pages/WorkspacePage.jsx`
Analytics detail page:
- Workspace profile info
- Analytics metrics:
  - Engagement rate
  - Followers
  - Total posts
  - Competitor engagement
- AI Insights section:
  - Gaps & opportunities
  - Actionable suggestions
  - Content ideas
- "Refresh" button for new insights

#### `src/components/NavBar.jsx`
Navigation bar:
- Logo/brand name
- Links (Home, Dashboard)
- User name (if logged in)
- Logout button
- Responsive layout

#### `src/services/api.js`
Axios HTTP client:
- Base URL: http://localhost:5000/api
- Request interceptor: Adds JWT token to all requests
- Response interceptor: Handles 401 errors (auto-logout)
- Exports API methods:
  - `authAPI.signup()`
  - `authAPI.login()`
  - `workspaceAPI.create()`
  - `workspaceAPI.getAll()`
  - `workspaceAPI.getById()`
  - `workspaceAPI.update()`
  - `workspaceAPI.delete()`
  - `analysisAPI.getAnalysis()`

#### `src/styles/global.css`
Global styling:
- Buttons: primary, secondary, danger
- Forms: input, textarea, labels
- Cards: styling with shadow
- Grid layouts
- Responsive design
- Loading spinner
- Error/success messages
- Workspace grid
- Analytics boxes
- Insights sections

#### `vite.config.js`
Vite configuration:
- React plugin
- Dev server port: 3000
- Build output: dist/
- Source map: disabled for production

---

## 🔄 Data Flow

### Signup Flow
```
User fills form (SignupPage.jsx)
    ↓
Calls: authAPI.signup(email, password, name)
    ↓
POST /api/auth/signup (authController.js)
    ↓
Creates User in MongoDB
    ↓
Hashes password with bcryptjs
    ↓
Creates JWT token
    ↓
Returns {user, token}
    ↓
Stores in localStorage
    ↓
Redirects to /dashboard
```

### Workspace Creation Flow
```
User fills form (DashboardPage.jsx)
    ↓
Calls: workspaceAPI.create()
    ↓
POST /api/workspaces (with JWT token)
    ↓
workspaceController.createWorkspace()
    ↓
Creates Workspace in MongoDB
    ↓
Links to user via userId
    ↓
Returns workspace data
    ↓
Added to list on dashboard
```

### Analytics Flow
```
User clicks workspace (DashboardPage.jsx)
    ↓
Navigates to /workspace/:workspaceId
    ↓
Calls: analysisAPI.getAnalysis(workspaceId)
    ↓
GET /api/analysis/:workspaceId (with JWT)
    ↓
analysisController.getAnalysis()
    ↓
Fetches workspace from MongoDB
    ↓
Generates mock analytics
    ↓
Calls AIService.generateInsights()
    ↓
Returns mock or OpenAI insights
    ↓
Sends full response to frontend
    ↓
Displays on WorkspacePage.jsx
```

---

## 🔐 Authentication Flow

```
1. User signs up/logs in
2. Password hashed with bcryptjs (User model)
3. Server returns JWT token
4. Frontend stores token in localStorage
5. All API requests include: Authorization: Bearer <token>
6. Middleware (authenticateToken.js) verifies token
7. Request has req.user.userId for database queries
8. If token invalid: 401 error, auto-logout
9. Protected routes in frontend redirect to /login if no token
```

---

## 📦 Dependencies

### Backend (package.json)
```json
{
  "dependencies": {
    "express": "^4.18.2",        // Web framework
    "mongoose": "^7.5.0",         // MongoDB ORM
    "bcryptjs": "^2.4.3",         // Password hashing
    "jsonwebtoken": "^9.0.2",     // JWT tokens
    "dotenv": "^16.3.1",          // Environment variables
    "axios": "^1.5.0",            // HTTP client
    "cors": "^2.8.5"              // Cross-origin support
  },
  "devDependencies": {
    "nodemon": "^3.0.1"           // Auto-reload on changes
  }
}
```

### Frontend (package.json)
```json
{
  "dependencies": {
    "react": "^18.2.0",            // UI library
    "react-dom": "^18.2.0",        // React DOM
    "react-router-dom": "^6.16.0", // Routing
    "axios": "^1.5.0"              // HTTP client
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.0.3",
    "vite": "^4.5.0"               // Build tool
  }
}
```

---

## 🗄️ Database Schema

### Users Collection
```json
{
  "_id": ObjectId,
  "email": "user@example.com",
  "password": "hashed_password",
  "name": "John Doe",
  "createdAt": ISODate,
  "updatedAt": ISODate
}
```

### Workspaces Collection
```json
{
  "_id": ObjectId,
  "name": "My Brand",
  "userId": ObjectId,
  "instagramProfile": "@mybrand",
  "competitors": ["@comp1", "@comp2"],
  "createdAt": ISODate,
  "updatedAt": ISODate
}
```

---

## 🚀 Build Output

### Frontend Build
```
frontend/dist/
├── index.html          # Main HTML file
├── assets/
│   ├── index-xxx.js    # Bundled JavaScript
│   └── index-xxx.css   # Bundled CSS
└── vite.svg
```

Deploy `/dist` folder to hosting service (Vercel, Netlify, etc.)

---

## 📝 File Organization Principles

1. **Models** - Database schemas (one per file)
2. **Controllers** - Business logic (one per feature)
3. **Routes** - API endpoints (grouped by feature)
4. **Middleware** - Request/response processing
5. **Services** - Reusable business logic (AI service)
6. **Pages** - Full-page components (React)
7. **Components** - Reusable UI components (React)
8. **Services** - API calls and utilities (React)
9. **Styles** - CSS files
10. **Config** - Configuration files

---

## 🔗 File Relationships

```
User → (one-to-many) → Workspaces

Frontend:
- HomePage.jsx → No API calls (public page)
- LoginPage.jsx → Calls authAPI.login()
- SignupPage.jsx → Calls authAPI.signup()
- DashboardPage.jsx → Calls workspaceAPI.getAll()
- WorkspacePage.jsx → Calls analysisAPI.getAnalysis()

Backend:
- authRoutes → authController → User model
- workspaceRoutes → workspaceController → Workspace model
- analysisRoutes → analysisController → Workspace model + AIService
```

---

**Each file has a specific purpose and follows MVC architecture principles.** ✨
