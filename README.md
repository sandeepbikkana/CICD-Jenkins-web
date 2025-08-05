# CICD-Jenkins-web
🚀 CI/CD Pipeline with Jenkins on AWS EC2
This guide helps you set up a Jenkins-based CI/CD pipeline on an AWS EC2 instance, with Docker integration, to automatically build and deploy a sample application whenever you push code to GitHub.

📌 Prerequisites
AWS account

EC2 instance (Amazon Linux 2 or Ubuntu)

GitHub account

Basic understanding of Linux & Git

🧰 Tools Used
Jenkins (automation server)

Docker (container platform)

GitHub (source code hosting)

EC2 (deployment host)

🛠️ Setup Steps
Step 1: Launch EC2
Launch a new EC2 instance (Amazon Linux 2 or Ubuntu).

Allow ports 22 (SSH), 8080 (Jenkins), and 5000  (application).

SSH into the instance.

Step 2: Install Java 17
Install Amazon Corretto 17 (Java runtime) using official AWS instructions.
sudo rpm --import https://yum.corretto.aws/corretto.key
sudo curl -Lo /etc/yum.repos.d/corretto.repo https://yum.corretto.aws/corretto.repo
sudo yum install java-17-amazon-corretto -y
java -version

Step 3: Install Jenkins
Add the Jenkins repo and import the GPG key.
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins


Install Jenkins via your package manager.

Start and enable Jenkins service.

Step 4: Install Docker
Install Docker.
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user
newgrp docker

Start and enable the Docker service.

Add your EC2 user to the Docker group and refresh the group permissions.

Step 5: Configure Jenkins
Access Jenkins at http://<your-ec2-ip>:8080.

Unlock it using the admin password located in Jenkins secrets.

Install suggested plugins.

Set up your admin user.

Step 6: Create a New Pipeline Job
In Jenkins, create a new Pipeline project.

Set the GitHub repo as the source.

Add a Jenkinsfile to your repo with the pipeline definition.

Step 7: Add Webhook for GitHub Auto-Trigger
Go to GitHub → Repository Settings → Webhooks.

Add a webhook pointing to http://<jenkins-ip>:8080/github-webhook/.

In Jenkins, configure the job to use GitHub hook trigger for GITScm polling.

Step 8: Test the Pipeline
Make a change in your code and push it to GitHub.

Jenkins will automatically build and deploy your application using Docker.

Access your deployed app at http://<your-ec2-ip>:5000 or :80.

🔁 CI/CD Flow
Developer commits and pushes code to GitHub.

GitHub triggers Jenkins via webhook.

Jenkins pulls the code, builds the Docker image, and runs the container.

Application is served on your EC2 public IP.

