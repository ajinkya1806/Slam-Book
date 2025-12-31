# 🚀 Deployment Guide: Digital Slam Book

Deploy your Digital Slam Book app using **Vercel** (frontend) and **Render** (backend) - both on free tiers!

---

## 📋 Prerequisites

Before deploying, make sure you have:
- ✅ GitHub account
- ✅ Vercel account (free) - [Sign up here](https://vercel.com/signup)
- ✅ Render account (free) - [Sign up here](https://render.com/)
- ✅ MongoDB Atlas cluster (free tier)
- ✅ Cloudinary account (free tier)

---

## 🗄️ Part 1: Backend Deployment (Render)

### Step 1: Prepare Your Backend

1. **Push your code to GitHub** (if not already done):
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin YOUR_GITHUB_REPO_URL
   git push -u origin main
   ```

2. **Verify server configuration**:
   - Your `server/index.js` should use `process.env.PORT` (already configured ✅)
   - CORS should allow your Vercel frontend URL (we'll set this up)

### Step 2: Deploy to Render

1. **Go to Render Dashboard**:
   - Visit [https://dashboard.render.com](https://dashboard.render.com)
   - Sign in or create an account

2. **Create a New Web Service**:
   - Click **"New +"** → **"Web Service"**
   - Connect your GitHub repository
   - Select the repository containing your app

3. **Configure the Service**:
   - **Name**: `memoir-app-backend` (or any name you prefer)
   - **Environment**: `Node`
   - **Region**: Choose closest to you (Oregon, Frankfurt, Singapore)
   - **Branch**: `main` (or your main branch)
   - **Root Directory**: `server`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Plan**: **Free**

4. **Set Environment Variables**:
   Click **"Advanced"** → **"Add Environment Variable"** and add:
   
   ```
   NODE_ENV=production
   PORT=10000
   MONGO_URI=your_mongodb_atlas_connection_string
   CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
   CLOUDINARY_API_KEY=your_cloudinary_api_key
   CLOUDINARY_API_SECRET=your_cloudinary_api_secret
   CLIENT_ORIGIN=https://your-vercel-app.vercel.app
   ```
   
   > **Note**: For `CLIENT_ORIGIN`, use a placeholder for now. We'll update it after deploying the frontend.

5. **Important: MongoDB Atlas IP Whitelist**:
   - Go to MongoDB Atlas → **Network Access**
   - Click **"Add IP Address"**
   - Click **"Allow Access from Anywhere"** (0.0.0.0/0)
   - This allows Render's dynamic IPs to access your database

6. **Deploy**:
   - Click **"Create Web Service"**
   - Render will start building and deploying your backend
   - Wait for deployment to complete (usually 2-5 minutes)

7. **Get Your Backend URL**:
   - Once deployed, Render will show your service URL
   - Example: `https://memoir-app-backend.onrender.com`
   - **Save this URL** - you'll need it for the frontend!

8. **Note on Free Tier**:
   - Render free tier spins down after 15 minutes of inactivity
   - First request after spin-down may take 30-60 seconds (cold start)
   - Consider upgrading to paid tier for production use

---

## 🎨 Part 2: Frontend Deployment (Vercel)

### Step 1: Prepare Your Frontend

1. **Verify API configuration**:
   - Your `client/src/utils/api.js` uses `VITE_API_URL` environment variable ✅
   - We'll set this in Vercel

### Step 2: Deploy to Vercel

1. **Go to Vercel Dashboard**:
   - Visit [https://vercel.com/dashboard](https://vercel.com/dashboard)
   - Sign in or create an account

2. **Import Your Project**:
   - Click **"Add New..."** → **"Project"**
   - Import your GitHub repository
   - Select the repository

3. **Configure the Project**:
   - **Framework Preset**: Vite (should auto-detect)
   - **Root Directory**: `client`
   - **Build Command**: `npm run build` (default)
   - **Output Directory**: `dist` (default)
   - **Install Command**: `npm install` (default)

4. **Set Environment Variables**:
   Click **"Environment Variables"** and add:
   
   ```
   VITE_API_URL=https://your-render-backend-url.onrender.com
   ```
   
   > Replace `your-render-backend-url` with your actual Render backend URL from Step 7 above!

5. **Deploy**:
   - Click **"Deploy"**
   - Vercel will build and deploy your frontend
   - This usually takes 1-2 minutes

6. **Get Your Frontend URL**:
   - Once deployed, Vercel will show your app URL
   - Example: `https://memoir-app.vercel.app`
   - Your app is now live! 🎉

---

## 🔄 Part 3: Update Backend CORS

After deploying the frontend, update the backend CORS to allow your Vercel URL:

1. **Go back to Render Dashboard**
2. **Navigate to your backend service**
3. **Go to "Environment" tab**
4. **Update `CLIENT_ORIGIN`**:
   ```
   CLIENT_ORIGIN=https://your-vercel-app.vercel.app
   ```
5. **Save changes** - Render will automatically redeploy

---

## ✅ Part 4: Verify Deployment

1. **Test Backend**:
   - Visit: `https://your-backend.onrender.com/api/health`
   - Should return: `{"status":"ok"}`

2. **Test Frontend**:
   - Visit: `https://your-app.vercel.app`
   - Should load the Digital Slam Book app

3. **Test Full Flow**:
   - Fill out a slam entry
   - Add a doodle and/or voice note
   - Submit and verify it appears in the book

---

## 🔧 Troubleshooting

### Backend Issues

**Problem**: Backend won't start
- **Solution**: Check Render logs → Ensure all environment variables are set correctly

**Problem**: MongoDB connection fails
- **Solution**: 
  - Verify MongoDB Atlas IP whitelist includes `0.0.0.0/0`
  - Check `MONGO_URI` environment variable format
  - Ensure MongoDB Atlas cluster is running

**Problem**: Cloudinary uploads fail
- **Solution**: 
  - Verify Cloudinary credentials in environment variables
  - Check Cloudinary dashboard for API key and secret

**Problem**: CORS errors
- **Solution**: 
  - Update `CLIENT_ORIGIN` in Render with your exact Vercel URL
  - Include protocol: `https://your-app.vercel.app`

### Frontend Issues

**Problem**: API calls fail (404 or CORS)
- **Solution**: 
  - Verify `VITE_API_URL` is set correctly in Vercel
  - Ensure backend URL doesn't have trailing slash
  - Check browser console for specific error messages

**Problem**: Environment variables not working
- **Solution**: 
  - In Vercel, environment variables starting with `VITE_` are needed
  - Redeploy after adding new environment variables
  - Clear browser cache

**Problem**: Build fails
- **Solution**: 
  - Check Vercel build logs
  - Ensure all dependencies are in `package.json`
  - Verify `vercel.json` is correct (already included)

---

## 📝 Environment Variables Summary

### Backend (Render)
```
NODE_ENV=production
PORT=10000
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/dbname?retryWrites=true&w=majority
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
CLIENT_ORIGIN=https://your-app.vercel.app
```

### Frontend (Vercel)
```
VITE_API_URL=https://your-backend.onrender.com
```

---

## 🎯 Quick Deploy Checklist

- [ ] Push code to GitHub
- [ ] Deploy backend to Render
- [ ] Set backend environment variables
- [ ] Whitelist MongoDB Atlas IP (0.0.0.0/0)
- [ ] Get backend URL from Render
- [ ] Deploy frontend to Vercel
- [ ] Set `VITE_API_URL` in Vercel
- [ ] Get frontend URL from Vercel
- [ ] Update `CLIENT_ORIGIN` in Render with frontend URL
- [ ] Test both URLs in browser
- [ ] Verify full app functionality

---

## 💡 Tips for Free Tier

### Render (Backend)
- **Cold starts**: First request after 15 min inactivity takes 30-60 seconds
- **Sleep**: Service sleeps after 15 minutes of no traffic
- **Solution**: Use a service like [UptimeRobot](https://uptimerobot.com/) (free) to ping your backend every 10 minutes to keep it awake

### Vercel (Frontend)
- **No sleep**: Vercel doesn't sleep on free tier
- **Fast CDN**: Your frontend is served from a global CDN
- **Automatic deployments**: Every push to main branch auto-deploys

---

## 🔐 Security Notes

1. **Never commit `.env` files** to GitHub
2. **Use environment variables** in Vercel and Render dashboards
3. **Keep MongoDB Atlas IP whitelist** as restrictive as possible in production (but 0.0.0.0/0 is fine for free tier)
4. **Rotate API keys** if accidentally exposed

---

## 📚 Additional Resources

- [Render Documentation](https://render.com/docs)
- [Vercel Documentation](https://vercel.com/docs)
- [MongoDB Atlas Setup](https://www.mongodb.com/docs/atlas/getting-started/)
- [Cloudinary Setup](https://cloudinary.com/documentation)

---

## 🎉 You're Done!

Your Digital Slam Book is now live on the internet! Share the Vercel URL with friends and family to collect memories.

**Need help?** Check the logs:
- Render: Dashboard → Your Service → Logs
- Vercel: Dashboard → Your Project → Deployments → View Logs

