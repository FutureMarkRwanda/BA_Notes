# **Learning Outcome 1: Configure the Environment**

### 📘 Learning Hours: 30

---

## Objective

By the end of this section, learners will be able to:
- Describe cloud computing concepts per Cloud Security Alliance (CSA) guidelines.
- Containerize and deploy microservices using Docker and Kubernetes.
- Configure and secure servers for optimal performance.
- Install and manage version control systems (e.g., Git).
- Create and manage CI/CD pipelines for automated software delivery.

---

## 1. **Cloud Concepts**

### 1.1 Definition
Cloud computing provides on-demand computing resources (e.g., servers, storage) over the internet, following CSA guidelines for scalability and security.

### 1.2 Example: Infrastructure as Code (IaC)
```bash
# Using Terraform to define a cloud server
provider "aws" {
  region = "us-east-1"
}
resource "aws_instance" "app_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

### 1.3 Key Concepts
| Concept                | Description                              |
|------------------------|------------------------------------------|
| Cloud Computing        | Scalable, on-demand resources            |
| Infrastructure as Code | Programmatic infrastructure management    |
| CI/CD                  | Continuous integration/deployment        |
| Microservices          | Modular, independent services            |

---

## 2. **Containerization of Microservices**

### 2.1 Definition
Containerization packages applications with dependencies for consistent deployment.

### 2.2 Example: Dockerizing a Microservice
```dockerfile
# Dockerfile for a Node.js app
FROM node:14
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "app.js"]
```

### 2.3 Tools
| Tool        | Purpose                              |
|-------------|--------------------------------------|
| Docker      | Container creation and management    |
| Kubernetes  | Orchestrates multiple containers      |

---

## 3. **Server Configuration**

### 3.1 Definition
Setting up servers with provisioning, autoscaling, and security configurations.

### 3.2 Example: Server Provisioning with Ansible
```yaml
# Ansible playbook for server setup
- hosts: webservers
  tasks:
    - name: Install Apache
      apt: name=apache2 state=present
```

---

## 4. **Version Control Installation**

### 4.1 Definition
Version control systems (e.g., Git) track code changes for collaboration.

### 4.2 Example: Git Workflow
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/user/repo.git
git push -u origin main
```

---

## 5. **CI/CD Pipeline Creation**

### 5.1 Definition
CI/CD pipelines automate building, testing, and deploying software.

### 5.2 Example: Jenkins Pipeline
```groovy
pipeline {
  agent any
  stages {
    stage('Build') {
      steps { sh 'npm install' }
    }
    stage('Test') {
      steps { sh 'npm test' }
    }
    stage('Deploy') {
      steps { sh 'docker push myapp:latest' }
    }
  }
}
```

---

## ✅ Summary Table
| Concept               | Description                              | Example                        |
|-----------------------|------------------------------------------|--------------------------------|
| Cloud Computing       | On-demand resource delivery              | Terraform IaC script           |
| Containerization      | Packaging apps with dependencies         | Dockerized Node.js app         |
| CI/CD Pipeline        | Automated build/test/deploy              | Jenkins pipeline configuration |

---

## 📚 Practice Exercises
1. Write a Terraform script to deploy an AWS EC2 instance.
2. Create a Dockerfile for a Python web app and deploy it using Docker.
3. Set up a basic CI/CD pipeline in GitHub Actions to build and test a sample app.