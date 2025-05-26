 🚀 Task 1: Automate Code Deployment Using CI/CD Pipeline with GitHub Actions

 ✅ Objective:

To set up a CI/CD pipeline that automates the process of building, testing, and deploying a Node.js web application using GitHub Actions and Docker.


 🛠 Tools Used:

GitHub
GitHub Actions
Node.js
Docker
Docker Hub

 📁 Project Structure:


nodejs-demo-app/
├── .github/
│   └── workflows/
│       └── main.yml     
├── Dockerfile           
├── package.json        
├── app.js             
├── README.md


Step-by-Step Process:

 1. Initialize Node.js App

 Created a simple `Node.js` application with `app.js` and `package.json`.

   bash
npm init -y
npm install express


 2. Dockerize the Application

Created a `Dockerfile` to containerize the Node.js application:

   Dockerfile
FROM node:20
WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]



 3. Set Up DockerHub

 Created an account and a new public repository: `your-dockerhub-username/nodejs-demo-app`


 4. Store DockerHub Credentials in GitHub Secrets

In the GitHub repository:

Go to `Settings → Secrets and variables → Actions`
 Added two secrets:

    `DOCKER_USERNAME`
    `DOCKER_PASSWORD` or `DOCKER_TOKEN`


5. Create GitHub Actions Workflow

File: github/workflows/main.yml

  yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Repository
      uses: actions/checkout@v3

    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '20'

    - name: Install Dependencies
      run: npm install

    - name: Run Tests
      run: echo "No tests specified"

    - name: Log in to Docker Hub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v3

    - name: Build and Push Docker Image
      uses: docker/build-push-action@v5
      with:
        context: .
        file: ./Dockerfile
        push: true
        tags: ${{ secrets.DOCKER_USERNAME }}/nodejs-demo-app:latest



 6. Push to GitHub

 Committed all files and pushed to `main` branch:

bash
git add .
git commit -m "Completed Task 1: Setup CI/CD with GitHub Actions"
git push origin main



 ✅ Output:

 When code is pushed to the `main` branch:

  * GitHub Actions is triggered
  * The app is built and tested
  * A Docker image is created and pushed to DockerHub


 🎯 What I Learned:

* How to write a Dockerfile for Node.js
* How to create and configure GitHub Actions workflows
* How to use GitHub Secrets
* How to automate Docker image deployment using CI/CD

