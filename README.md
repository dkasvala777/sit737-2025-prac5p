# SIT737-2025-Prac5P – Dockerised Node.js Web Application

Hi, I’m Dhruv Kaswala 👋  
This repository contains my submission for SIT737 Task 5.1P – Containerisation of a simple web application using Docker. I’ve documented each step I followed to containerise and test my Node.js app using Docker and Docker Compose, and push it to GitHub and Docker Hub.

---

## 🧰 Tools I Used

- [Node.js](https://nodejs.org/en/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker](https://www.docker.com/)
- [GitHub](https://github.com)
- [Docker Compose](https://docs.docker.com/compose/install/)

---

## 🚀 Steps I Followed

### 1. Clone the Project or Start a New Node App

I cloned the project  Node.js application.


### 2. The the `app.js` File

```javascript
const express = require('express');
const app = express();

// Serve the HTML file
app.get('/', (req, res) => {
  res.send('<h1>Hello, World!</h1>');
});

// Health check endpoint
app.get('/health', (req, res) => {
  res.status(200).send('OK');
});

const port = 3000;
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});


```

### 3. Create the `Dockerfile`

Here is the `Dockerfile` I wrote:

```Dockerfile
# Use Node.js base image
FROM node:16

# Set working directory
WORKDIR /app

# Copy dependency files and install
COPY package*.json ./
RUN npm install

# Copy all project files
COPY . /app

# Start the app
CMD ["node", "app.js"]
```

### 4. Create `docker-compose.yml`

Then I wrote a Docker Compose file to build and run my app and include a health check.

```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "3000:3000"
    restart: always
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
```

---

## 🧪 How I Ran It

### 🔧 Build the Docker Image

```bash
docker-compose build
```

### ▶️ Run the Container

```bash
docker-compose up -d
```

### 🌐 Access the App

- Open in browser: `http://localhost:3000`
- Health check: `http://localhost:3000/health`

### ✅ Check Container Health

```bash
docker ps
```

Look under the `STATUS` column — it will show `(healthy)` if the container is passing the health check.

---

## 🐳 Push to Docker Hub

### 1. Tag the image

```bash
docker tag <image-id> dkasvala/test-app:latest
```

### 2. Login to Docker Hub

```bash
docker login
```

### 3. Push the image

```bash
docker push dkasvala/test-app:latest
```

---

## 🔁 Push to GitHub

### 1. Initialize Git

```bash
git init
```

### 2. Add and Commit

```bash
git add .
git commit -m "code"
```

### 3. Set Remote and Push

```bash
git remote set-url origin https://github.com/dkasvala777/sit737-2025-prac5p.git
git push -u origin master
```

---

## ✅ Final Notes

- My application is successfully containerised and health-checked.
- The container auto-restarts if it fails.
- The Docker image is live on Docker Hub under `dkasvala/test-app`.
- All source code and config files are pushed to [my GitHub repository](https://github.com/dkasvala777/sit737-2025-prac5p).
