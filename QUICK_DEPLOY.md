# ⚡ Quick Deploy Guide

## TL;DR - Get deployed in 10 minutes!

### Backend (Render)

1. **Push to GitHub**
   ```bash
   git add .
   git commit -m "Ready for deployment"
   git push
   ```

2. **Deploy to Render**
   - Go to [render.com](https://render.com) → New Web Service
   - Connect GitHub repo
   - Settings:
     - Root Directory: `server`
     - Build: `npm install`
     - Start: `npm start`
   - Add Environment Variables:
     ```
     PORT=10000
     MONGO_URI=<your-mongodb-uri>
     CLOUDINARY_CLOUD_NAME=<your-cloud-name>
     CLOUDINARY_API_KEY=<your-api-key>
     CLOUDINARY_API_SECRET=<your-api-secret>
     CLIENT_ORIGIN=<will-update-later>
     ```
   - Deploy! ✅

3. **Copy Backend URL** (e.g., `https://xxx.onrender.com`)

### Frontend (Vercel)

1. **Deploy to Vercel**
   - Go to [vercel.com](https://vercel.com) → New Project
   - Import GitHub repo
   - Settings:
     - Root Directory: `client`
     - Framework: Vite (auto-detected)
   - Add Environment Variable:
     ```
     VITE_API_URL=<your-render-backend-url>
     ```
   - Deploy! ✅

2. **Copy Frontend URL** (e.g., `https://xxx.vercel.app`)

### Final Step

1. **Update Backend CORS**
   - Render Dashboard → Your Service → Environment
   - Update `CLIENT_ORIGIN` with your Vercel URL
   - Save (auto-redeploys)

2. **MongoDB Atlas IP Whitelist**
   - MongoDB Atlas → Network Access
   - Add IP: `0.0.0.0/0` (allow all)

**Done! 🎉** Visit your Vercel URL and test!

---

📖 **Full guide with troubleshooting**: See [DEPLOYMENT.md](./DEPLOYMENT.md)

