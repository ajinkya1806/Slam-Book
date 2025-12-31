# ✅ Deployment Checklist

Use this checklist to track your deployment progress.

## 📦 Pre-Deployment

- [ ] Code is pushed to GitHub
- [ ] MongoDB Atlas account created
- [ ] MongoDB Atlas cluster created and running
- [ ] MongoDB connection string obtained
- [ ] Cloudinary account created
- [ ] Cloudinary credentials obtained (Cloud Name, API Key, API Secret)
- [ ] Vercel account created
- [ ] Render account created

## 🗄️ Backend Deployment (Render)

- [ ] GitHub repo connected to Render
- [ ] New Web Service created in Render
- [ ] Root Directory set to `server`
- [ ] Build Command: `npm install`
- [ ] Start Command: `npm start`
- [ ] Environment variables added:
  - [ ] `NODE_ENV=production`
  - [ ] `PORT=10000`
  - [ ] `MONGO_URI=<your-mongodb-uri>`
  - [ ] `CLOUDINARY_CLOUD_NAME=<your-cloud-name>`
  - [ ] `CLOUDINARY_API_KEY=<your-api-key>`
  - [ ] `CLOUDINARY_API_SECRET=<your-api-secret>`
  - [ ] `CLIENT_ORIGIN=<placeholder-for-now>`
- [ ] Service deployed successfully
- [ ] Backend URL obtained: `https://__________.onrender.com`
- [ ] Health check working: `https://__________.onrender.com/api/health`
- [ ] MongoDB Atlas IP whitelist updated (0.0.0.0/0)

## 🎨 Frontend Deployment (Vercel)

- [ ] GitHub repo connected to Vercel
- [ ] New Project created in Vercel
- [ ] Root Directory set to `client`
- [ ] Framework auto-detected as Vite
- [ ] Environment variable added:
  - [ ] `VITE_API_URL=<your-render-backend-url>`
- [ ] Project deployed successfully
- [ ] Frontend URL obtained: `https://__________.vercel.app`
- [ ] Frontend loads without errors

## 🔄 Post-Deployment Configuration

- [ ] Backend `CLIENT_ORIGIN` updated with Vercel URL
- [ ] Backend auto-redeployed after CORS update
- [ ] Verified CORS is working (no CORS errors in browser console)

## ✅ Testing

- [ ] Backend health check: `https://__________.onrender.com/api/health`
- [ ] Frontend loads: `https://__________.vercel.app`
- [ ] Can view existing entries (if any)
- [ ] Can fill out new slam entry
- [ ] Can add doodle
- [ ] Can add voice note
- [ ] Entry submission works
- [ ] Entry appears in slam book
- [ ] Doodle displays correctly
- [ ] Audio plays correctly
- [ ] All form fields are saved and displayed

## 🎉 Final Steps

- [ ] Bookmarked both URLs
- [ ] Tested on mobile device
- [ ] Shared app with friends
- [ ] Monitored logs for any errors
- [ ] Set up uptime monitoring (optional, for Render free tier)

## 🔧 Optional: Keep Render Awake (Free Tier)

Render free tier spins down after 15 minutes. To keep it awake:

- [ ] Created account on [UptimeRobot](https://uptimerobot.com/)
- [ ] Added monitor for backend URL
- [ ] Set interval to 10 minutes
- [ ] Monitor active

---

**Deployment Complete! 🎉**

Your app is live at: `https://__________.vercel.app`

