# 🚀 CD - Deploy Application from Jenkins Pipeline on EC2 Instance Using Docker-Compose

### 🛠️ Technologies Used:
1. **AWS** ☁️
2. **Jenkins** ⚙️
3. **Java** ☕
4. **Maven** 📦
5. **Git** 🔧
6. **Docker Hub** 🐳
7. **Docker** 🛳️
8. **Linux** 🐧

---

## ✅ Pre-requisites:
1. An **AWS Account** set up and ready.
2. A **private Docker Hub repository**.
3. **Docker image** of the Java-Maven app pushed to Docker Hub.

---

## 🧰 Installing Docker Compose on AWS EC2 Instance
1. Download Docker Compose:
   ```bash
   sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
   ```
2. Fix permissions:
   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```
3. Verify installation:
   ```bash
   docker-compose -v
   ```
> 📚 Steps referenced from [this guide](https://gist.github.com/npearce/6f3c7826c7499587f00957fee62f8ee9)

---

## 🧾 Creating `docker-compose.yaml`
We will start **two containers**:
- `java-maven-appr` (Java app) on port **8080**
- `postgres` (Database) on port **5432**

> 🐳 Make sure the image for `java-maven-appr` is from your private Docker Hub repo.

---

## 📝 Creating `server-cmds.sh`
This file will contain the shell commands needed to start up and manage the Docker Compose stack.

---

🎉 **That's it! You're now deploying your Java Maven app from Jenkins to AWS using Docker Compose!**