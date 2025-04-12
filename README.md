# 🚀 CD: Deploy Application from Jenkins Pipeline to EC2 using Docker

### 🛠️ Technologies Used:
1. **AWS** ☁️
2. **Jenkins** 🧪
3. **Docker** 🐳
4. **React** ⚛️
5. **Node.js** 🟩
6. **Git** 🔧
7. **Linux** 🐧
8. **Docker Hub** 📦

---

## ✅ Prerequisites:
1. AWS Account set up and ready.
2. A private Docker Hub repository.
3. Docker image of the Node.js app from [this source code](https://github.com/nanuchi/react-nodejs-example), pushed to your Docker Hub.

---

## 🌐 Setting Up EC2 Instance, Security Group, and SSH Key
1. Launch a new EC2 instance.
2. Configure the **security group** to allow inbound connections on port **3080** and SSH (port 22).
3. Generate and assign a **key pair** for SSH authentication.

---

## ⚙️ Configuring EC2 Instance
Once connected via SSH, install Docker and authenticate:
```bash
sudo yum install docker -y
sudo service docker start
```
Login to Docker:
```bash
docker login
```

---

## 📝 Editing Jenkinsfile for SSH Deployment
1. **Install the SSH Agent Plugin** in Jenkins.
2. **Create a multi-branch pipeline** and configure credentials:
    - Go to **Manage Jenkins > Credentials**
    - Add a new **SSH Username with private key** credential.
3. Convert your `.pem` key to OpenSSH format if needed:
```bash
ssh-keygen -p -m PEM -f <key-name>.pem
```
4. Update your `Jenkinsfile` to include SSH agent steps and run the Docker container:
```groovy
sshagent(['<your-credential-id>']) {
    sh 'ssh -o StrictHostKeyChecking=no ec2-user@<ec2-ip> "docker run -d -p 3080:3080 nateallon/demo-app:2.1"'
}
```

---

🌍 If everything is configured properly, your application will be accessible at:
```
http://<ec2-public-ipv4>:3080
```

🎉 **Your CI/CD pipeline is now deploying to AWS EC2 using Docker!**