📚 Project Overview
**Live Demo:** [Your Website URL]

## 🛠️ Technologies & Tools Used

1 Category | Tools |

 ->**Version Control**  Git, GitHub 
 ->**CI/CD**  Jenkins 
 ->**Code Quality**  SonarQube 
 ->**Containerization**  Docker 
-> **Cloud Platform**  AWS EC2 

2. Git - Version Control System
-->Git is a distributed version control system that tracks changes in your code during development.

3.Jenkins - CI/CD Automation Server.
-  Automate repetitive deployment tasks
-  Reduce human errors in deployment
-  Faster time from development to production
-  Integrate multiple tools (Git, Docker, SonarQube, AWS)
-  Monitor build and deployment status.

      Jenkins Pipeline Stages:

        1. Checkout Code from GitHub
                ↓
        2. Run SonarQube Analysis
                ↓
        3. Build Docker Image
                ↓
        4. Push Image to Docker Hub
                ↓
        5. Deploy to AWS EC2
               ↓
       6. Send Notification

4.SonarQube - Code Quality Platform.

SonarQube is a platform for continuous inspection of code quality that performs automatic reviews to detect bugs, code smells, and security vulnerabilities.

- Detect bugs before they reach production
-  Identify security vulnerabilities
-  Ensure code quality standards
-  Measure code coverage
-  Track technical debt

5.Docker - Containerization Platform


Docker is a platform that packages applications and dependencies into containers, ensuring consistent behavior across different environments.


**Dockerfile for LMS:**
```dockerfile
# Use Node.js base image
FROM node:16-alpine

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy application code
COPY . .

# Build application -0-
RUN npm run build

# Expose application port
EXPOSE 3000

# Start application
CMD ["npm", "start"]

**Docker Commands Used:**
```bash
# Build image
docker build -t lms:latest .

# Run container locally
docker run -d -p 3000:3000 --name lms-app lms:latest

6.AWS EC2 - Cloud Computing

  Specification  Details 

**Instance Type** t2.micro (1 vCPU, 1 GB RAM) 
**OS** | Ubuntu 22.04 LTS 
**Storage**  30 GB SSD
 **Region** |us-east-1 
**Availability Zone** us-east-1a 
**EC2 Setup Steps:**

```bash
# 1. Connect to EC2
ssh -i "ssh-jenkin.pem.pem" ubuntu@54.16.95.36

# 2. Update system
sudo apt update && sudo apt upgrade -y

# 3. Install Docker
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu

Complete CI/CD Architecture

 Developer  
└──────┬──────┘
       │ git push
       ↓
┌─────────────┐
│   GitHub    │
└──────┬──────┘
       │ webhook
       ↓
┌─────────────┐
│   Jenkins   │◄────┐
└──────┬──────┘     │
       │            │
    ┌──┴──────┬─────┴──┐
    ↓         ↓        ↓
┌─────────┐ ┌────────┐ ┌──────┐
│SonarQube│ │Docker  │ │AWS   │
│Analysis │ │Build   │ │Deploy│
└─────────┘ └────────┘ └──────┘
                          ↓
                    ┌──────────┐
                    │Live Site │
                    └──────────┘






