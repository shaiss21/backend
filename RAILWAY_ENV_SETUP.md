# Railway Environment Variables Setup

## ⚠️ IMPORTANT: Set These Variables in Railway Dashboard

Your backend needs these environment variables to run. **They must be set in Railway, not in .env file!**

## Quick Setup Steps

1. Go to your Railway project dashboard
2. Click on your **backend** service
3. Go to the **Variables** tab
4. Click **"New Variable"** for each variable below
5. Add the variable name and value
6. Click **"Deploy"** or wait for auto-deploy

## Required Environment Variables

### 1. MongoDB Connection (REQUIRED)
```
Variable Name: MONGODB_URI
Variable Value: mongodb+srv://228w1a12i8_db_user:MyQ8kmRpZUN4DRLq@cluster0.uolgbwd.mongodb.net/art-therapy-db
```

### 2. Google Gemini API Key (REQUIRED)
```
Variable Name: GOOGLE_API_KEY
Variable Value: AIzaSyBBmVvKXP82--RLCnsJNa5E_Ip-Iy2cIwM
```

### 3. Stability AI API Key (REQUIRED)
```
Variable Name: STABILITY_API_KEY
Variable Value: sk-yXdVYsP08J3I3WCiZUNdUpK8uP08zpCu2WcUfupSYbEB9e3E
```

### 4. Server Configuration
```
Variable Name: NODE_ENV
Variable Value: production
```

```
Variable Name: PORT
Variable Value: (Leave empty - Railway sets this automatically)
```

### 5. CORS Configuration (Update with your frontend URL)
```
Variable Name: CLIENT_URL
Variable Value: https://your-frontend-domain.com
```

Or if testing locally:
```
Variable Name: CLIENT_URL
Variable Value: http://localhost:3000
```

### 6. Rate Limiting (Optional - has defaults)
```
Variable Name: RATE_LIMIT_WINDOW_MS
Variable Value: 900000
```

```
Variable Name: RATE_LIMIT_MAX_REQUESTS
Variable Value: 100
```

## How to Add Variables in Railway

### Method 1: Via Dashboard
1. Open your Railway project
2. Select the **backend** service
3. Click **"Variables"** tab
4. Click **"+ New Variable"**
5. Enter variable name and value
6. Click **"Add"**

### Method 2: Via Railway CLI (Alternative)
```bash
railway variables set MONGODB_URI="mongodb+srv://..."
railway variables set GOOGLE_API_KEY="AIzaSy..."
railway variables set STABILITY_API_KEY="sk-yX..."
railway variables set NODE_ENV="production"
```

## Verification

After setting variables:
1. Railway will automatically redeploy
2. Check the deployment logs
3. Look for: `🍃 MongoDB Connected: ...`
4. If you see errors, verify all variables are set correctly

## Common Issues

### Error: "MongoDB URI not configured"
- **Solution**: Add `MONGODB_URI` variable in Railway Variables tab

### Error: "Google API key not configured"
- **Solution**: Add `GOOGLE_API_KEY` variable in Railway Variables tab

### Error: "Stability AI API key not configured"
- **Solution**: Add `STABILITY_API_KEY` variable in Railway Variables tab

### MongoDB Connection Timeout
- Check your MongoDB Atlas IP whitelist includes Railway IPs (or use `0.0.0.0/0` for testing)
- Verify the MongoDB URI is correct
- Check MongoDB Atlas cluster is running

## Security Notes

✅ **DO**: Set variables in Railway dashboard  
✅ **DO**: Keep variables secret (they're encrypted in Railway)  
❌ **DON'T**: Commit `.env` files to git  
❌ **DON'T**: Share API keys in public repositories  

Your `.env` file is already in `.gitignore` - it won't be committed!

## Testing After Setup

1. Check deployment logs for: `🍃 MongoDB Connected`
2. Test health endpoint: `https://your-app.railway.app/api/health`
3. Should return: `{"status":"OK","timestamp":"...","environment":"production"}`

