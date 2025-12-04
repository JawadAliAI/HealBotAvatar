# Talking Avatar with AI - Deployment Guide

## 🚀 Deployment Options

This project is configured to be deployed as a single Docker container, which hosts both the Node.js backend and the React frontend.

### Option 1: Render (Recommended)

Render is a unified cloud to build and run all your apps and websites.

1.  **Create Render Account**
    - Go to https://render.com
    - Sign up with GitHub

2.  **Create New Web Service**
    - Click "New +" -> "Web Service"
    - Connect your GitHub repository
    - Render should automatically detect the `render.yaml` or `Dockerfile`.
    - If asked, choose **Docker** as the runtime.

3.  **Configuration**
    - **Name**: `healbot-avatar` (or your choice)
    - **Region**: Choose one close to you
    - **Branch**: `main`
    - **Runtime**: Docker
    - **Plan**: Free (or higher)

4.  **Deploy**
    - Click "Create Web Service"
    - Render will build the Docker image (this may take a few minutes) and deploy it.

### Option 2: Hugging Face Spaces

You can deploy this application to Hugging Face Spaces using their Docker SDK.

1.  **Create Hugging Face Account**
    - Go to https://huggingface.co
    - Sign up

2.  **Create New Space**
    - Click on your profile -> "New Space"
    - **Space Name**: `healbot-avatar`
    - **License**: MIT (optional)
    - **SDK**: Docker
    - **Hardware**: CPU Basic (Free) is usually sufficient, but Upgrade if needed for faster TTS.

3.  **Upload Code**
    - You can sync your GitHub repo with the Space, or push your code directly to the Space's repo.
    - Ensure the `Dockerfile` is in the root directory.

4.  **Configuration**
    - Hugging Face Spaces usually listen on port 7860. You might need to update the `Dockerfile` or `server.js` if HF doesn't map port 3000 automatically.
    - **Note**: For Hugging Face, it is recommended to change the port in `apps/backend/server.js` to `7860` or use an environment variable.
    - Add a variable `PORT` = `7860` in the Space Settings -> "Variables and secrets".

## 📋 Pre-Deployment Checklist

- ✅ Removed Vercel and Railway configurations
- ✅ Added `Dockerfile` for multi-stage build
- ✅ Added `render.yaml` for Render Blueprints
- ✅ Backend serves Frontend static files
- ✅ `edge-tts` and `ffmpeg` included in Docker image

## 🔧 Environment Variables

**Render / Hugging Face:**
- `PORT`: Defaults to `3000`. Set to `7860` for Hugging Face if needed.

## 🧪 Testing After Deployment

1.  Open your deployed URL (e.g., `https://healbot-avatar.onrender.com` or `https://huggingface.co/spaces/username/healbot-avatar`)
2.  The frontend should load.
3.  Send a message. The backend should process it using `edge-tts` and return the audio and animation.

## 🆘 Troubleshooting

- **Build Fails**: Check the logs. Ensure `ffmpeg` and `python` are correctly installed in the Docker image.
- **Audio Issues**: If TTS fails, check if `edge-tts` is working. The logs will show python errors.
- **Connection Refused**: Ensure the port matches the environment variable.
