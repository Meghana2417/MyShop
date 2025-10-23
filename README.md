MyShop – Next.js Dockerized Application
Project Overview

A containerized Next.js e-commerce application deployed using Docker and optionally GitHub Actions for CI/CD.

Setup Instructions

Clone the repository:

git clone https://github.com/pawanpk87/MyShop.git
cd MyShop

Install dependencies:

npm install

Local Run
npm run dev       
npm run build    
npm start         

Access 
Open browser: http://localhost:3000

Deployment Steps

Launch an EC2 instance (Ubuntu)

SSH into the instance:

ssh -i <your-key.pem> ubuntu@<ec2-ip>


Install Docker:

sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker

Docker Run

Build Docker image:

docker build -t myshop:latest .
Run Docker container:

docker run -d -p 3000:3000 --name myshop \
  -e MONGODB_URL="<your-mongodb-uri>" \
  -e NEXTAUTH_URL="http://<your-ec2-ip>:3000" \
  -e NEXTAUTH_SECRET="myshopsecret123" \
  -e NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME="<cloud-name>" \
  -e NEXT_PUBLIC_CLOUDINARY_API_KEY="<api-key>" \
  -e CLOUDINARY_SECRET="<cloud-secret>" \
  myshop:latest

  Accessing the Application

  Browser URL: http://<your-ec2-ip>:3000


Check logs:

docker logs -f myshop

Deployment Notes

Use Elastic IP for EC2 to avoid changing URL after server restart

Ensure MongoDB Atlas is accessible from EC2

Cloudinary account should contain images for proper display



GitHub Actions CI/CD Workflow

Triggered on push to main branch

Steps:

Checkout repository

Set up Node.js

Install dependencies

Build Next.js app

Login to Docker Hub

Build Docker image & push with proper tagging

Deploy container on EC2 via SSH





