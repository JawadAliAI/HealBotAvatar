# Talking Avatar with AI - Deployment Guide

## 🚀 Deployment Options

### Option 1: Railway (Backend) + Vercel (Frontend) - Recommended

#### Deploy Backend to Railway:

1. **Create Railway Account**
   - Go to https://railway.app
   - Sign up with GitHub

2. **Create New Project**
   - Click "New Project"
   - Select "Deploy from GitHub repo"
   - Choose your repository
   - Railway will auto-detect the Node.js app

3. **Configure Environment**
   - No environment variables needed (custom API is external)
   - Railway will automatically install dependencies

4. **Deploy**
   - Railway will build and deploy automatically
   - Copy your Railway URL (e.g., `https://your-app.railway.app`)

#### Deploy Frontend to Vercel:

1. **Create Vercel Account**
   - Go to https://vercel.com
   - Sign up with GitHub

2. **Import Project**
   - Click "New Project"
   - Import your GitHub repository
   - Framework Preset: Vite
   - Root Directory: `apps/frontend`

3. **Configure Build Settings**
   - Build Command: `npm run build`
   - Output Directory: `dist`
   - Install Command: `npm install`

4. **Add Environment Variable**
   - Name: `VITE_API_URL`
   - Value: Your Railway backend URL (e.g., `https://your-app.railway.app`)

5. **Deploy**
   - Click "Deploy"
   - Vercel will build and deploy your frontend

### Option 2: Railway Only (Full Stack)

You can deploy both backend and frontend on Railway:

1. **Deploy Backend** (same as above)

2. **Deploy Frontend as Separate Service**
   - Create another Railway service
   - Point to same repo
   - Root Directory: `apps/frontend`
   - Build Command: `npm run build`
   - Start Command: `npx serve -s dist -l $PORT`
   - Add environment variable: `VITE_API_URL` = your backend URL

## 📋 Pre-Deployment Checklist

- ✅ Removed OpenAI dependencies
- ✅ Removed ElevenLabs dependencies  
- ✅ Using custom API for chat
- ✅ Using local Python TTS
- ✅ Health check endpoint added
- ✅ CORS enabled for all origins

## 🔧 Important Notes

### Python Requirement
The backend uses Python for TTS. Make sure Python is available in your deployment environment:

**For Railway:**
- Add a `nixpacks.toml` file (Railway auto-detects Python)

**For Render/Other:**
- Use a buildpack that includes Python

### Environment Variables

**Backend:** None required (custom API URL is hardcoded)

**Frontend:**
- `VITE_API_URL` - Your backend URL

## 🧪 Testing After Deployment

1. Test backend health: `https://your-backend-url/health`
2. Test frontend: `https://your-frontend-url`
3. Send a message and verify avatar responds

## 🆘 Troubleshooting

**Backend Issues:**
- Check Railway logs for Python errors
- Verify `/health` endpoint returns 200
- Check if TTS script is executable

**Frontend Issues:**
- Verify `VITE_API_URL` is set correctly
- Check browser console for CORS errors
- Ensure backend URL doesn't have trailing slash

## 📱 URLs After Deployment

**Backend:** `https://your-app.railway.app`  
**Frontend:** `https://your-app.vercel.app`

Share the frontend URL with anyone!
