# Railway Deployment Guide

## Prerequisites

1. Railway account at [railway.app](https://railway.app)
2. GitHub repository with your code
3. MongoDB Atlas account (or Railway MongoDB service)

## Deployment Steps

### 1. Connect Your Repository

1. Go to [Railway Dashboard](https://railway.app/dashboard)
2. Click "New Project"
3. Select "Deploy from GitHub repo"
4. Choose your repository
5. Select the `backend` folder as the root directory

### 2. Configure Environment Variables

In Railway dashboard, go to your project → Variables tab, and add:

```bash
# Google Gemini API Key
GOOGLE_API_KEY=your_google_api_key_here

# Stability AI API Key
STABILITY_API_KEY=your_stability_ai_api_key_here

# MongoDB Configuration
MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/art-therapy-db

# Server Configuration
PORT=5000
NODE_ENV=production

# CORS Configuration
CLIENT_URL=https://your-frontend-domain.com

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

### 3. Build Settings

Railway will automatically detect Node.js. Ensure:

- **Root Directory**: `backend` (if deploying from monorepo)
- **Build Command**: (Auto-detected, no build command needed)
- **Start Command**: `npm start`

**Important**: The Dockerfile has been updated to:
- ✅ Only build the backend (no frontend dependencies)
- ✅ Works without frontend directory
- ✅ Optimized for Railway deployment

### 4. Port Configuration

Railway automatically assigns a PORT. Your `server.js` should use:
```javascript
const PORT = process.env.PORT || 5000;
```

✅ Already configured in your server.js!

### 5. Health Check

Railway will use the `/api/health` endpoint to verify deployment.

### 6. CORS Configuration

Update the CORS origin in `server.js` to include your frontend URL:

```javascript
app.use(cors({
  origin: [
    'http://localhost:3000',
    'https://your-frontend-domain.com', // Add your production frontend URL
  ],
  credentials: true
}));
```

## Important Notes

- ✅ `.env` file is in `.gitignore` - your secrets are safe!
- ✅ Use Railway's environment variables instead of `.env` file
- ✅ MongoDB URI should be set in Railway variables
- ✅ All API keys should be set in Railway variables

## Testing Deployment

1. Get your Railway deployment URL
2. Test health endpoint: `https://your-app.railway.app/api/health`
3. Update frontend `.env` with production API URL

## Troubleshooting

### Build Fails
- Check Node.js version in `package.json`
- Ensure all dependencies are listed in `package.json`

### Connection Errors
- Verify MongoDB URI is correct in Railway variables
- Check MongoDB Atlas IP whitelist includes Railway IPs

### CORS Errors
- Update CORS origins in `server.js` to include frontend URL

