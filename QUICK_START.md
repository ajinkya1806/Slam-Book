# ⚡ Quick Start Guide

## Prerequisites Checklist

- [x] Node.js installed (v16+)
- [ ] MongoDB running (local or Atlas)
- [ ] Cloudinary account created
- [ ] Environment variables configured

## 🚀 Run the Application

### Option 1: Using Setup Script (Recommended)

**Windows (PowerShell):**
```powershell
.\setup.ps1
```

**Mac/Linux:**
```bash
chmod +x setup.sh
./setup.sh
```

### Option 2: Manual Setup

**1. Install Dependencies**

Backend:
```bash
cd server
npm install
```

Frontend:
```bash
cd client
npm install
```

**2. Configure Environment**

Edit `server/.env`:
```env
MONGO_URI=mongodb://localhost:27017/memoir-app
PORT=5000
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
CLIENT_ORIGIN=http://localhost:5173
```

Edit `client/.env` (optional):
```env
VITE_API_URL=http://localhost:5000
```

**3. Start Servers**

Terminal 1 - Backend:
```bash
cd server
npm start
```

Terminal 2 - Frontend:
```bash
cd client
npm run dev
```

**4. Open Browser**

- Frontend: http://localhost:5173
- Backend Health: http://localhost:5000/api/health

## ✅ Verification

1. Backend console shows:
   - `✅ MongoDB Connected`
   - `🚀 Server running on port 5000`

2. Frontend opens at http://localhost:5173

3. Health check returns: `{"status":"ok"}`

## 🎯 First Steps

1. **Fill the Slam Book**: Click "Sign Book" or go to `/fill`
2. **View Entries**: Go to `/` to see the flipbook
3. **Share Link**: Copy the share link to invite friends

## 🐛 Common Issues

**MongoDB Connection Failed**
- Ensure MongoDB is running: `mongod` (local) or check Atlas connection
- Verify connection string in `server/.env`

**Cloudinary Upload Errors**
- Check API credentials in `server/.env`
- Verify Cloudinary account is active

**Port Already in Use**
- Change `PORT` in `server/.env`
- Update `VITE_API_URL` in `client/.env` if changed

**CORS Errors**
- Ensure `CLIENT_ORIGIN` in `server/.env` matches frontend URL

## 📚 Need Help?

See `README.md` for detailed documentation.

