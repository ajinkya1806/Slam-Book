# 🔧 MongoDB Atlas Setup Guide

## Issue: IP Address Not Whitelisted

If you're getting a 500 error with a message about IP whitelisting, your MongoDB Atlas cluster needs to allow your IP address.

## Quick Fix

### Option 1: Whitelist Your Current IP (Recommended)

1. Go to [MongoDB Atlas Dashboard](https://cloud.mongodb.com)
2. Click on **Network Access** in the left sidebar
3. Click **Add IP Address**
4. Click **Add Current IP Address** (or enter your IP manually)
5. Click **Confirm**

### Option 2: Allow All IPs (Development Only)

⚠️ **Warning:** Only use this for development, not production!

1. Go to **Network Access** in MongoDB Atlas
2. Click **Add IP Address**
3. Enter `0.0.0.0/0` (allows all IPs)
4. Click **Confirm**

## Verify Connection

After whitelisting, restart your server:

```bash
cd server
npm start
```

You should see:
```
✅ MongoDB Connected
Database: your-database-name
```

## Alternative: Use Local MongoDB

If you prefer to use local MongoDB instead:

1. Install MongoDB locally
2. Update `server/.env`:
   ```env
   MONGO_URI=mongodb://localhost:27017/memoir-app
   ```
3. Start MongoDB service
4. Restart your server

## Troubleshooting

- **Connection timeout**: Check your internet connection
- **Authentication failed**: Verify your MongoDB URI has correct username/password
- **Database not found**: MongoDB will create the database automatically on first write

