# nodejs-demo-app
simple nodejs app for CI/CD demo
## Tools Used

- **GitHub** – Code hosting & CI/CD trigger
- **GitHub Actions** – Automate build, test & deployment
- **Node.js** – Sample app
- **Docker** – Containerization
- **DockerHub** – Docker image registry

---

# Project Structure

nodejs-demo-app/
├── app.js
├── Dockerfile
├── package.json
└── .github/
└── workflows/
└── main.yml

# app.js

const http = require("http");

const PORT = process.env.PORT || 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.end("Hello from Node.js CI/CD App!");
});

server.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});

# package.json

{
  "name": "nodejs-demo-app",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "test": "echo \"No tests yet\" && exit 0"
  }
}

# Dockerfile

FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]

# create github repository (nodejs-demo-app)
push your local code

# Added Dockerhub secrets to github
# Setup github action and workflows
# commit and push
git add .
git commit -m "Add CI/CD GitHub Actions workflow"
git push

# Run the Docker Image Locally
docker pull yourusername/nodejs-demo-app
docker run -p 3000:3000 yourusername/nodejs-demo-app

Visit: http://localhost:3000
You should see: "Hello from Node.js App deployed via GitHub Actions on AWS EC2!"

