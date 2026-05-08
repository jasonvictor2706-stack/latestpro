# ⚡ Quick Start Guide - 5 Minutes to Running XCI

## Option 1: Local Development (Fastest) ⭐

### Prerequisites Check
```bash
python --version        # Need 3.10+
node --version         # Need 18+
```

### Terminal 1: Backend
```bash
cd backend
python -m venv venv
# Windows: venv\Scripts\activate
# macOS/Linux: source venv/bin/activate
cp .env.example .env
pip install -r requirements.txt
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### Terminal 2: Frontend
```bash
cd frontend
npm install
cp .env.example .env.local
npm run dev
```

### Terminal 3: Databases (if not running)
```bash
# MongoDB
mongod

# Redis (in another terminal)
redis-server
```

**Open browser:**
- Frontend: http://localhost:5173
- Backend: http://localhost:8000/health
- API Docs: http://localhost:8000/docs

---

## Option 2: Docker (One Command) 🐳

### Prerequisites
- Docker installed: https://www.docker.com/products/docker-desktop

### Run Everything
```bash
docker-compose up
```

**Wait 1 minute, then open:**
- Frontend: http://localhost:5173
- Backend: http://localhost:8000/health

**To stop:**
```bash
docker-compose down
```

---

## Option 3: Cloud Deployment (15 Minutes) ☁️

### Step 1: Push to GitHub
```bash
git init
git add .
git commit -m "XCI deployment"
git remote add origin https://github.com/YOUR_USERNAME/XCI-Deployment.git
git branch -M main
git push -u origin main
```

### Step 2: Deploy Backend
1. Go to https://render.com (Sign up with GitHub)
2. New → Web Service
3. Select `XCI-Deployment` repo
4. Build: `pip install -r backend/requirements.txt`
5. Start: `cd backend && uvicorn main:app --host 0.0.0.0 --port 8000`
6. Add env vars from `.env.example`
7. Deploy!
8. **Copy backend URL** ⭐

### Step 3: Deploy Frontend
1. Go to https://vercel.com (Sign up with GitHub)
2. New Project
3. Select `XCI-Deployment` repo
4. Root Directory: `frontend`
5. Add env: `VITE_API_BASE_URL=YOUR_BACKEND_URL`
6. Deploy!
7. **Copy frontend URL** ⭐

### Step 4: Update Backend
1. Render → Backend → Environment
2. Set `FRONTEND_URL=YOUR_FRONTEND_URL`
3. Save (redeploys)

### Done! ✅
- Frontend: `https://xci-frontend.vercel.app`
- Backend: `https://xci-backend.onrender.com`

---

## Environment Files Setup

### Create `backend/.env`
```bash
cp backend/.env.example backend/.env
```

Edit and fill in:
```env
MONGO_URI=mongodb://localhost:27017/agrisen
DB_NAME=agrisen
JWT_SECRET=dev-secret-key
REDIS_URL=redis://localhost:6379
FRONTEND_URL=http://localhost:5173
```

### Create `frontend/.env.local`
```bash
cp frontend/.env.example frontend/.env.local
```

Edit and fill in:
```env
VITE_API_BASE_URL=http://localhost:8000
```

---

## Test Everything Works

```bash
# Backend health
curl http://localhost:8000/health
# Should return: {"status":"ok"}

# API Docs
curl http://localhost:8000/docs
# Should return HTML with API documentation

# Frontend
open http://localhost:5173
# Should show login page
```

---

## Common Issues

| Problem | Solution |
|---------|----------|
| `ModuleNotFoundError` | Run `pip install -r backend/requirements.txt` |
| MongoDB error | Start MongoDB: `mongod` or `brew services start mongodb-community` |
| Redis error | Start Redis: `redis-server` or `brew services start redis` |
| Port 8000 in use | Use different port: `--port 8001` |
| npm dependencies error | Delete `node_modules` and run `npm install` again |
| CORS error | Check `FRONTEND_URL` in `.env` |

---

## Next Steps

1. ✅ Get app running locally
2. 📝 Configure `.env` files properly
3. 🌐 (Optional) Set up MongoDB Atlas & Redis Cloud
4. 🚀 Deploy to Render & Vercel
5. 🔗 (Optional) Buy custom domain

See **DEPLOYMENT_GUIDE.md** for detailed instructions.

---

## Project Structure

```
XCI-Xplainable-Crop-Intelligence-/
├── backend/              # FastAPI application
│   ├── main.py          # Entry point
│   ├── routes/          # API endpoints
│   ├── services/        # Business logic
│   ├── models/          # ML models (.pkl files)
│   ├── data/            # CSV datasets
│   ├── requirements.txt  # Dependencies
│   └── .env.example     # Configuration template
│
├── frontend/            # React + Vite application
│   ├── src/            # React components
│   ├── package.json    # Dependencies
│   └── .env.example    # Configuration template
│
├── docker-compose.yml  # Local containerized setup
├── Dockerfile.backend  # Backend container config
└── DEPLOYMENT_GUIDE.md # Detailed deployment steps
```

---

## Support Resources

- **FastAPI Docs:** https://fastapi.tiangolo.com/
- **React Docs:** https://react.dev/
- **MongoDB:** https://docs.mongodb.com/
- **Render:** https://render.com/docs
- **Vercel:** https://vercel.com/docs

---

**You're all set! 🚀 Choose your option above and start building!**
