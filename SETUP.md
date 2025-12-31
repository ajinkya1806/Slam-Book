# 🚀 Setup Instructions

## Step-by-Step Setup Guide

### 1. Install Dependencies

**Backend:**
```bash
cd server
npm install
```

**Frontend:**
```bash
cd client
npm install
```

### 2. Configure Environment Variables

**Backend (`server/.env`):**
Create a `.env` file in the `server` directory with:

```env
MONGO_URI=mongodb://localhost:27017/memoir-app
PORT=5000
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
CLIENT_ORIGIN=http://localhost:5173
```

**Frontend (`client/.env`):**
Create a `.env` file in the `client` directory (optional):

```env
VITE_API_URL=http://localhost:5000
```

### 3. Get Cloudinary Credentials

1. Sign up at [cloudinary.com](https://cloudinary.com) (free)
2. Go to Dashboard → Settings → Account Details
3. Copy:
   - Cloud Name
   - API Key
   - API Secret
4. Paste into `server/.env`

### 4. Setup MongoDB

**Option A: Local MongoDB**
- Install MongoDB locally
- Start MongoDB service
- Use: `mongodb://localhost:27017/memoir-app`

**Option B: MongoDB Atlas (Recommended)**
- Sign up at [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
- Create a free cluster
- Get connection string
- Use: `mongodb+srv://username:password@cluster.mongodb.net/memoir-app`

### 5. Run the Application

**Terminal 1 - Backend:**
```bash
cd server
npm start
```

**Terminal 2 - Frontend:**
```bash
cd client
npm run dev
```

### 6. Open Browser

- Frontend: http://localhost:5173
- Backend: http://localhost:5000/api/health

## ✅ Verification

1. Backend should show: `✅ MongoDB Connected` and `🚀 Server running on port 5000`
2. Frontend should open at http://localhost:5173
3. Health check: http://localhost:5000/api/health should return `{"status":"ok"}`

## 🐛 Troubleshooting

- **MongoDB not connecting**: Check connection string and ensure MongoDB is running
- **Cloudinary errors**: Verify API credentials in `.env`
- **Port conflicts**: Change PORT in server `.env` and update VITE_API_URL in client `.env`
- **CORS errors**: Ensure CLIENT_ORIGIN matches frontend URL

