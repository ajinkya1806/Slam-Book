# 🔧 Troubleshooting Guide

## Common Issues and Solutions

### 1. ERR_CONNECTION_REFUSED / Network Error

**Symptoms:**
- `ERR_CONNECTION_REFUSED` in browser console
- `Network Error` from axios
- Frontend can't connect to backend

**Solutions:**

#### Check if Server is Running
```bash
cd server
npm start
```

You should see:
```
✅ MongoDB Connected
🚀 Server running on port 5000
```

#### Check Port Availability
```bash
# Windows PowerShell
Test-NetConnection -ComputerName localhost -Port 5000

# Or check if something is using port 5000
netstat -ano | findstr :5000
```

#### Verify Environment Variables
Check `server/.env` has:
- `MONGO_URI` - MongoDB connection string
- `CLOUDINARY_CLOUD_NAME` - Your Cloudinary cloud name
- `CLOUDINARY_API_KEY` - Your Cloudinary API key
- `CLOUDINARY_API_SECRET` - Your Cloudinary API secret
- `PORT` - Server port (default: 5000)

#### Check API URL in Frontend
Verify `client/.env` has:
```env
VITE_API_URL=http://localhost:5000
```

Or check `client/src/utils/api.js` is using the correct URL.

---

### 2. MongoDB Connection Errors

**Symptoms:**
- `❌ DB Connection Error` in server logs
- IP whitelist errors

**Solutions:**

#### MongoDB Atlas IP Whitelist
1. Go to [MongoDB Atlas Dashboard](https://cloud.mongodb.com)
2. **Network Access** → **Add IP Address**
3. Add your current IP or `0.0.0.0/0` for development
4. Wait 1-2 minutes for changes to propagate

#### Local MongoDB
If using local MongoDB:
```env
MONGO_URI=mongodb://localhost:27017/memoir-app
```

Ensure MongoDB service is running:
```bash
# Windows
net start MongoDB

# Mac/Linux
sudo systemctl start mongod
```

---

### 3. Cloudinary Upload Errors

**Symptoms:**
- `Cannot read properties of undefined (reading 'uploader')`
- File uploads fail

**Solutions:**

#### Verify Cloudinary Credentials
1. Go to [Cloudinary Dashboard](https://cloudinary.com/console)
2. **Settings** → **Account Details**
3. Copy:
   - Cloud Name
   - API Key
   - API Secret
4. Update `server/.env`

#### Check File Size Limits
- Cloudinary free tier: 10MB per file
- Check file sizes before upload

---

### 4. CORS Errors

**Symptoms:**
- `Access-Control-Allow-Origin` errors
- Requests blocked by browser

**Solutions:**

#### Update CORS Configuration
In `server/index.js`, ensure:
```javascript
app.use(cors({ origin: process.env.CLIENT_ORIGIN || '*' }));
```

In `server/.env`:
```env
CLIENT_ORIGIN=http://localhost:5173
```

---

### 5. Tailwind CSS Not Loading

**Symptoms:**
- No styles applied
- Components look unstyled

**Solutions:**

#### Verify PostCSS Config
Check `client/postcss.config.js`:
```javascript
export default {
  plugins: {
    '@tailwindcss/postcss': {},
    autoprefixer: {},
  },
};
```

#### Check CSS Import
In `client/src/index.css`, ensure:
```css
@import "tailwindcss";
```

#### Restart Dev Server
```bash
cd client
npm run dev
```

---

### 6. Port Already in Use

**Symptoms:**
- `EADDRINUSE` error
- Server won't start

**Solutions:**

#### Find Process Using Port
```bash
# Windows
netstat -ano | findstr :5000

# Mac/Linux
lsof -i :5000
```

#### Kill Process or Change Port
1. Kill the process using the port
2. Or change `PORT` in `server/.env`:
   ```env
   PORT=5001
   ```
3. Update `VITE_API_URL` in `client/.env`:
   ```env
   VITE_API_URL=http://localhost:5001
   ```

---

## Quick Health Checks

### Backend Health
```bash
curl http://localhost:5000/api/health
```
Should return: `{"status":"ok"}`

### Frontend API Config
Check browser console for API calls and verify the URL is correct.

### Server Logs
Check server console for:
- ✅ MongoDB Connected
- ✅ Server running on port X
- Any error messages

---

## Still Having Issues?

1. **Check all logs** (server console, browser console)
2. **Verify environment variables** are set correctly
3. **Restart both servers** (backend and frontend)
4. **Clear browser cache** and hard refresh (Ctrl+Shift+R)
5. **Check firewall/antivirus** isn't blocking connections

