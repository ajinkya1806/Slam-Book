# 🔧 Cloudinary Storage Fix

## Issue
```
TypeError: Cannot read properties of undefined (reading 'uploader')
```

## Root Cause
The `multer-storage-cloudinary` package expects the full cloudinary object (which has a `v2` property), but we were passing only `cloudinary.v2`. 

When the package tries to access `cloudinary.v2.uploader`, it's actually trying to access `(cloudinary.v2).v2.uploader`, which doesn't exist.

## Solution
Pass the full cloudinary object (with `v2` property) instead of just `cloudinary.v2`:

**Before:**
```javascript
const cloudinary = require('cloudinary').v2;
const storage = cloudinaryStorage({
  cloudinary: cloudinary, // ❌ This is just v2, missing the v2 property
});
```

**After:**
```javascript
const cloudinaryLib = require('cloudinary');
const cloudinary = cloudinaryLib.v2;
const storage = cloudinaryStorage({
  cloudinary: cloudinaryLib, // ✅ Full object with v2 property
});
```

## Files Modified
- `server/config/cloudinary.js` - Fixed cloudinary object passing

## Verification
The storage object is now created correctly and should work with multer file uploads.

