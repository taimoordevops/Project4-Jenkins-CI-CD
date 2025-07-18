# 📦 Project 4: GitHub → Jenkins → EC2 CI/CD Pipeline

This project demonstrates a simple yet real-world **CI/CD pipeline**:  
A GitHub push automatically triggers a **Jenkins job on an EC2 instance**, which runs a shell script (`build.sh`). It’s a foundational DevOps flow for automated deployments.

---

## 🚀 Workflow

1. Developer pushes code to GitHub
2. GitHub webhook triggers Jenkins job
3. Jenkins (on EC2) pulls the latest code
4. `build.sh` runs inside Jenkins workspace
5. Output is logged in Jenkins console

---

## 🔧 Components Used

| Component         | Purpose                            |
|------------------|------------------------------------|
| **GitHub**        | Source code + webhook trigger      |
| **Jenkins (EC2)** | CI/CD server running on Ubuntu     |
| **Shell Script**  | Simulated deployment logic         |
| **Amazon EC2**    | Jenkins hosted here                |

---

## 📜 Shell Script: `build.sh`

```bash
#!/bin/bash
echo "Hello from Jenkins GitHub CI/CD Demo!"

```
---
### 🧨 Common Error & Fix

Sometimes, line endings from Windows can break shell scripts in Jenkins.

❌ "/bin/bash^M: bad interpreter: No such file or directory"

✅ Fix:

```bash
dos2unix build.sh
git add build.sh
git commit -m "Fix: convert CRLF to LF"
git push origin main
```
---
### 🔁 CI/CD Workflow Diagram (Mermaid)

```mermaid
graph LR
  A[Developer pushes to GitHub] --> B[GitHub Webhook triggers Jenkins]
  B --> C[Jenkins EC2 Server]
  C --> D[Pull latest code from GitHub]
  D --> E[Run build.sh]
  E --> F[Deployment step or output shown]
  F --> G[Console output: SUCCESS or FAIL]
```
---
### 🔧 GitHub Webhook Setup

To trigger Jenkins when code is pushed to GitHub:

1. Go to your GitHub repo → **Settings → Webhooks**
2. Click **Add Webhook**
3. **Payload URL**:  
   `http://<your-jenkins-ec2-ip>:8080/github-webhook/`
4. **Content type**: `application/json`
5. Select: **Just the push event**
6. Click **Add Webhook**
   
✅ Now, every `git push` will trigger a Jenkins job automatically.

---
### 📸 Jenkins Console Output (Example)

```bash
Started by user Taimoor DevOps
Running as SYSTEM
Building in workspace /var/lib/jenkins/workspace/GitHub-CI-Demo
+ chmod +x build.sh
+ ./build.sh
Hello from Jenkins GitHub CI/CD Demo!
Finished: SUCCESS
```
---
### 👤 Author

**Taimoor DevOps**  
[GitHub](https://github.com/taimoordevops)  
[LinkedIn](#) <!-- (Optional) Add your LinkedIn profile later -->

---
### 🧠 Future Enhancements

- Replace shell script with full app deployment (Node.js / Flask)
- Use Jenkins Pipelines (Jenkinsfile)
- Add test automation step
- Dockerize app + Jenkins
- Enable rollback on failure
- Secure Jenkins access
