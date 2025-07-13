<<<<<<< HEAD
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

| Category           | Tool            |
|--------------------|------------------|
| CI/CD Pipeline     | GitHub Actions   |
| Code Quality       | SonarQube        |
| Containerization   | Docker           |
| Container Registry | DockerHub        |
| Deployment         | Helm             |
| GitOps CD          | Argo CD          |
| Runtime Platform   | Kubernetes       |
| Language           | Python (Flask)   |

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
|-------------------|--------------------------|
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

## 🎤 Interview Explanation Sample

> I implemented a cloud-native CI/CD pipeline using GitHub Actions to automate the build and deployment of a Flask application. The pipeline runs a SonarQube quality scan, builds and pushes a Docker image to DockerHub, and updates the Helm chart with the new image tag. Argo CD automatically syncs the changes and deploys the app into Kubernetes. This project demonstrates my hands-on experience with containerization, continuous delivery, Helm templating, and GitOps workflows.

---

## 📌 License
This project is open-source and free to use for learning and portfolio building.
=======
# cloud-native-cicd-pipeline-flask-k8s
>>>>>>> 2e5a39a33e994d32a28e0401fea6b5e86e874025
