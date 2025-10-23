=========================================================
                    MyShop – Next.js Dockerized Application
=========================================================

Project Overview
----------------
A containerized Next.js e-commerce application deployed using Docker.
Optionally, GitHub Actions can be used for CI/CD automation.

Setup Instructions
------------------
1. Clone the repository:
   $ git clone https://github.com/pawanpk87/MyShop.git
   $ cd MyShop

2. Install dependencies:
   $ npm install

3. Local Run:
   - Development server:
     $ npm run dev
   - Build application:
     $ npm run build
   - Start server:
     $ npm start

4. Access the application:
   Open browser and go to:
   http://localhost:3000

Deployment Steps
----------------
1. Launch an EC2 instance (Ubuntu)
2. SSH into the instance:
   $ ssh -i <your-key.pem> ubuntu@<EC2-IP>

3. Install Docker:
   $ sudo apt update
   $ sudo apt install docker.io -y
   $ sudo systemctl start docker
   $ sudo systemctl enable docker

4. Build Docker image:
   $ docker build -t myshop:latest .

5. Run Docker container:
   $ docker run -d -p 3000:3000 --name myshop \
     -e MONGODB_URL="<your-mongodb-uri>" \
     -e NEXTAUTH_URL="http://<EC2-IP>:3000" \
     -e NEXTAUTH_SECRET="myshopsecret123" \
     -e NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME="<cloud-name>" \
     -e NEXT_PUBLIC_CLOUDINARY_API_KEY="<api-key>" \
     -e CLOUDINARY_SECRET="<cloud-secret>" \
     myshop:latest

6. Accessing the Application:
   Open browser and go to:
   http://<EC2-IP>:3000

7. Check logs:
   $ docker logs -f myshop

Deployment Notes
----------------
- Use Elastic IP for EC2 to avoid changing URL after server restart
- Ensure MongoDB Atlas is accessible from EC2
- Cloudinary account should contain images for proper display

GitHub Actions CI/CD Workflow
-----------------------------
- Triggered on push to main branch
- Steps:
  1. Checkout repository
  2. Set up Node.js
  3. Install dependencies
  4. Build Next.js app
  5. Login to Docker Hub
  6. Build Docker image & push with proper tagging
  7. Deploy container on EC2 via SSH
