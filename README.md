# nodejs-demo-app
simple nodejs app for CI/CD demo
## Tools Used

- **GitHub** – Code hosting & CI/CD trigger
- **GitHub Actions** – Automate build, test & deployment
- **Node.js** – Sample app
- **Docker** – Containerization
- **DockerHub** – Docker image registry

---

## 📂 Project Structure

nodejs-demo-app/
├── app.js
├── Dockerfile
├── package.json
└── .github/
└── workflows/
└── main.yml


---

## ⚙️ How It Works

1. **Push to main** branch triggers the workflow.
2. Workflow:
   - Installs dependencies
   - Runs test
   - Builds Docker image
   - Pushes image to DockerHub

---

## 🛠️ Setup Steps

### 1. Create App Files

- `app.js` (basic HTTP server)
- `package.json` with start/test scripts
- `Dockerfile`

### 2. Push to GitHub Repo

```bash

git init
git add .
git commit -m "init"
git remote add origin https://github.com/YOUR_USERNAME/nodejs-demo-app.git
git push -u origin main

```

## 3. Add GitHub Secrets

In your repo > Settings > Secrets > Actions, add:

    DOCKER_USERNAME

    DOCKER_PASSWORD (use token if 2FA enabled)

## 4. Add GitHub Actions Workflow

Create .github/workflows/main.yml with the CI/CD pipeline steps (checkout, test, build, push to DockerHub).


## 5. Push Changes

git add .
git commit -m "Add CI/CD pipeline"
git push

## Optional: Run the Docker Image Locally

Make sure Docker is running, then:

docker pull yourusername/nodejs-demo-app
docker run -p 3000:3000 yourusername/nodejs-demo-app

Visit: http://localhost:3000
You should see: "Hello from Node.js App deployed via GitHub Actions on AWS EC2!"

