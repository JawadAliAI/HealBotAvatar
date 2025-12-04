FROM nikolaik/python-nodejs:python3.10-nodejs20

# Install ffmpeg
RUN apt-get update && apt-get install -y ffmpeg

WORKDIR /app

# Copy root package files
COPY package*.json ./

# Copy backend package files
COPY apps/backend/package*.json ./apps/backend/

# Copy frontend package files
COPY apps/frontend/package*.json ./apps/frontend/

# Install root dependencies
RUN npm install

# Install backend dependencies
WORKDIR /app/apps/backend
RUN npm install
RUN pip install edge-tts

# Install frontend dependencies
WORKDIR /app/apps/frontend
RUN npm install

# Copy source code
WORKDIR /app
COPY . .

# Build frontend
WORKDIR /app/apps/frontend
RUN npm run build

# Expose port
EXPOSE 3000

# Start backend
WORKDIR /app/apps/backend
CMD ["node", "server.js"]
