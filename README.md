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

## Steps to Set Up the CI/CD Pipeline

# Step 1: Clone or Create the Node.js App

```bash
mkdir nodejs-demo-app && cd nodejs-demo-app

app.js

const http = require("http");

const PORT = process.env.PORT || 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.end("Hello from Node.js CI/CD App!");
});

server.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});

package.json

{
  "name": "nodejs-demo-app",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "test": "echo \"No tests yet\" && exit 0"
  }
}

Dockerfile

FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]

 Step 2: Create a GitHub Repository

    Go to https://github.com

    Create a new public repository: nodejs-demo-app

    Push your local code:

git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/nodejs-demo-app.git
git push -u origin main

Step 3: Add DockerHub Secrets to GitHub

Go to your repository on GitHub:

    Click Settings > Secrets and variables > Actions > New repository secret

    Add the following:

Name	Value
DOCKER_USERNAME	Your DockerHub username
DOCKER_PASSWORD	Your DockerHub password or token

    🔐 If you use 2FA on DockerHub, create a personal access token and use it as the password.

 Step 4: Set Up GitHub Actions Workflow

Create the folder and file:

mkdir -p .github/workflows
touch .github/workflows/main.yml

main.yml

name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: 18

    - name: Install dependencies
      run: npm install

    - name: Run test
      run: npm test

    - name: Log in to DockerHub
      run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin

    - name: Build Docker image
      run: docker build -t ${{ secrets.DOCKER_USERNAME }}/nodejs-demo-app:latest .

    - name: Push Docker image to DockerHub
      run: docker push ${{ secrets.DOCKER_USERNAME }}/nodejs-demo-app:latest

 Step 5: Commit and Push

git add .
git commit -m "Add CI/CD GitHub Actions workflow"
git push

 Output: What This Will Do

    On push to main:

        Installs dependencies

        Runs tests

        Builds a Docker image

        Pushes the image to your DockerHub repo

 Optional: Run the Docker Image Locally

Make sure Docker is running, then:

docker pull yourusername/nodejs-demo-app
docker run -p 3000:3000 yourusername/nodejs-demo-app

Visit: http://localhost:3000
You should see: "Hello from Node.js App deployed via GitHub Actions on AWS EC2!"

