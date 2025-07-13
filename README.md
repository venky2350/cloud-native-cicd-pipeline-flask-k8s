# 📘 Cloud-Native CI/CD Pipeline for Flask App on Kubernetes

This project demonstrates a complete **CI/CD pipeline for a Python Flask application** using:

- **GitHub Actions** for continuous integration
- **SonarQube** for static code analysis
- **Docker & DockerHub** for containerization
- **Helm** for Kubernetes deployment
- **Argo CD** for GitOps-based delivery

---

## 🧱 Project Structure

```bash
cloud-native-cicd-pipeline-flask-k8s/
├── app/                      # Flask App Source Code
│   ├── src/app.py            # Flask API
│   ├── requirements.txt      # Dependencies
│   ├── Dockerfile            # Container build config
│   └── sonar-project.properties
├── helm/                     # Helm chart for Kubernetes deployment
│   ├── values.yaml           # Image tag replaced during CI
│   └── templates/
│       ├── deployment.yaml
│       └── service.yaml
├── .github/
│   └── workflows/cicd.yml    # GitHub Actions pipeline
├── argocd/
│   └── flask-app.yaml        # Argo CD Application manifest
├── README.md
└── .gitignore
```

---

## 🔧 Tools Used

| Category           | Tool           |
| ------------------ | -------------- |
| CI/CD Pipeline     | GitHub Actions |
| Code Quality       | SonarQube      |
| Containerization   | Docker         |
| Container Registry | DockerHub      |
| Deployment         | Helm           |
| GitOps CD          | Argo CD        |
| Runtime Platform   | Kubernetes     |
| Language           | Python (Flask) |

---

## 🔁 CI/CD Pipeline Flow

                          +--------------------------+
                          |     Developer Pushes     |
                          |        to GitHub         |
                          +------------+-------------+
                                       |
                                       v
                          +--------------------------+
                          |     GitHub Actions CI     |
                          | - Run Unit Tests          |
                          | - Run SonarQube Scan      |
                          | - Build Docker Image      |
                          | - Push to DockerHub       |
                          | - Update Helm Chart       |
                          +------------+-------------+
                                       |
                                       v
                          +--------------------------+
                          |        GitHub Repo        |
                          |   (Updated values.yaml)   |
                          +------------+-------------+
                                       |
                                       v
                          +--------------------------+
                          |         Argo CD          |
                          | - Watches Git Changes     |
                          | - Auto-sync Enabled       |
                          +------------+-------------+
                                       |
                                       v
                          +--------------------------+
                          |     Kubernetes Cluster    |
                          | - Deploy via Helm Chart   |
                          | - Flask App Exposed       |
                          +--------------------------+

---

## 🚀 How to Run This Project (on AWS EC2 or Minikube)

### 1. Clone the repository

```bash
git clone https://github.com/your-username/cloud-native-cicd-pipeline-flask-k8s.git
cd cloud-native-cicd-pipeline-flask-k8s
```

### 2. Build and run Flask locally (optional test)

```bash
cd app
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python src/app.py
```

Visit: http://localhost:5000

### 3. Build & Push Docker Image (manually or via GitHub Actions)

```bash
docker build -t <your-dockerhub-username>/flask-cicd-app:v1 .
docker push <your-dockerhub-username>/flask-cicd-app:v1
```

### 4. Set up Kubernetes (Minikube or EC2-based K8s)

```bash
minikube start
```

### 5. Install Helm & Deploy App

```bash
helm install flask-app helm/
```

### 6. Install Argo CD (if not already)

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### 7. Apply Argo CD Application

```bash
kubectl apply -f argocd/flask-app.yaml
```

---

## 🔐 GitHub Secrets to Configure

| Secret Name       | Purpose                  |
| ----------------- | ------------------------ |
| `DOCKER_USERNAME` | DockerHub login          |
| `DOCKER_PASSWORD` | DockerHub password/token |
| `SONAR_TOKEN`     | SonarQube auth token     |

---

## 📷 Screenshots (add in GitHub)

- Screenshot 1: CI/CD pipeline success in GitHub Actions
- Screenshot 2: Docker image on DockerHub
- Screenshot 3: Helm deployment using Argo CD UI
- Screenshot 4: App running in Kubernetes (kubectl get pods, services)

---

## 📝 Resolving Git Merge Conflict When Pushing to Remote Repository

### 🧩 Problem Overview

When you attempt to push your local repository to a newly created GitHub repository that already contains files (such as a `README.md`, `.gitignore`, or LICENSE), you may see the following error:

```bash
git push -u origin master
To https://github.com/username/repo.git
! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/username/repo.git'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
```

### 🚫 Root Cause

This error occurs because:

- The **remote GitHub repository** already has commits (e.g., README.md)
- Your **local repository** does not contain those commits
- Git refuses to overwrite history to prevent data loss

### ✅ Solution (Safe & Recommended)

#### Step-by-Step Fix:

#### 1️⃣ Pull the Remote Branch to Your Local Machine

```bash
git pull origin master --allow-unrelated-histories
```

> `--allow-unrelated-histories` tells Git to merge two unrelated histories (local and remote).

#### 2️⃣ Resolve Any Merge Conflicts (if prompted)

If there's a conflict, such as in `README.md`, Git will mark it like this:

```md
<<<<<<< HEAD
Your local content
=======
Remote GitHub content

> > > > > > > origin/master
```

Edit the file to keep the correct content, then:

```bash
git add .
git commit -m "Resolve merge conflict between local and remote"
```

#### 3️⃣ Push Your Changes to GitHub

```bash
git push -u origin master
```

✅ Now your entire local project is pushed successfully.

---

### 📌 Pro Tips

- Avoid this problem by initializing an **empty GitHub repository** (no README or license)
- If you already added files in GitHub, always run `git pull` before pushing
- Use meaningful commit messages when resolving merge conflicts

---

### ✅ Summary

> This conflict happens because Git protects you from accidentally overwriting remote history. The solution is to pull remote changes, merge them safely (resolving conflicts if needed), then push your full project.

---

## 📌 License

This project is open-source and free to use for learning and portfolio building.
