# Automated Portfolio Website Deployment

This is a complete, beginner-friendly DevOps project designed for college viva evaluations. It demonstrates a simple CI/CD pipeline using **GitHub**, **Jenkins**, and **AWS EC2**.

---

## 🏗️ Architecture Diagram

```text
Developer
   ↓ (git push)
GitHub Repository
   ↓ (Webhook triggers build)
Jenkins CI/CD Pipeline
   ↓ (Deploys code)
AWS EC2 Server (Apache/Nginx)
   ↓
Live Website
```

---

## 🛠️ Technologies Used
* **Frontend:** HTML, CSS, JavaScript (Responsive, Modern UI)
* **Version Control:** Git & GitHub
* **CI/CD:** Jenkins
* **Cloud Platform:** AWS EC2 (Ubuntu)
* **Web Server:** Apache

---

## 🚀 AWS EC2 Setup (Beginner Steps)

1. **Log into AWS Console** and go to **EC2**.
2. **Launch Instance**:
   * **Name**: `DevOps-Portfolio-Server`
   * **OS**: Ubuntu 22.04 LTS
   * **Instance Type**: t2.micro (Free Tier)
   * **Key Pair**: Create a new `.pem` key (e.g., `devops-key`) and download it.
3. **Configure Security Group (Firewall)**:
   * Allow **SSH** (Port 22) - To connect to the terminal.
   * Allow **HTTP** (Port 80) - To access the website.
   * Allow **Custom TCP** (Port 8080) - To access Jenkins.
4. **Launch Instance**.

---

## 💻 Server Configuration & Deployment Steps

Connect to your EC2 instance using SSH:
```bash
ssh -i "devops-key.pem" ubuntu@<your-ec2-public-ip>
```

### 1. Install Java (Required for Jenkins)
```bash
sudo apt update
sudo apt install openjdk-11-jre -y
java -version
```

### 2. Install Jenkins
```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
```

### 3. Install Git & Apache Web Server
```bash
sudo apt install git -y
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```

### 4. Configure Permissions
Jenkins needs permission to write files to the Apache web directory (`/var/www/html/`).
```bash
sudo chown -R jenkins:jenkins /var/www/html/
sudo chmod -R 755 /var/www/html/
```
*(Alternatively, you can give Jenkins sudo access without password by editing `visudo`, but the above is simpler for a college project).*

---

## ⚙️ Jenkins CI/CD Setup

1. **Access Jenkins**: Open `http://<your-ec2-public-ip>:8080` in your browser.
2. **Unlock Jenkins**: Retrieve the password by running:
   ```bash
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```
3. **Install Suggested Plugins** and create an Admin User.
4. **Create a Pipeline**:
   * Click **New Item** -> Name it `Portfolio-Deployment` -> Select **Pipeline** -> Click OK.
5. **Configure GitHub Integration**:
   * Under **Build Triggers**, select **GitHub hook trigger for GITScm polling**.
   * Under **Pipeline**, select **Pipeline script from SCM**.
   * SCM: Git
   * Repository URL: `<Your-GitHub-Repo-URL>`
   * Branch: `*/main`
6. **Save & Build**: Click **Build Now** to test.

---

## 📝 GitHub Workflow Explanation

For the viva, you should explain standard Git practices:
1. `git init` - Initializes the local repository.
2. `git add .` - Stages all files.
3. `git commit -m "Initial commit"` - Saves changes locally with a descriptive message.
4. `git push origin main` - Pushes the code to the remote GitHub repository.

Whenever a new `git push` happens, Jenkins automatically pulls the latest code and copies the HTML/CSS/JS files into `/var/www/html/`.

---

## 📸 Screenshots

*(Add screenshots here for your project report)*
- [ ] Website Homepage
- [ ] Jenkins Pipeline Success Screen
- [ ] AWS EC2 Instance Running

---

## 🔮 Future Improvements
If asked how you would improve this in the future:
* Add Docker to containerize the application.
* Add SonarQube for code quality checks.
* Use Nginx instead of Apache for better performance.
* Host images on an AWS S3 bucket.
