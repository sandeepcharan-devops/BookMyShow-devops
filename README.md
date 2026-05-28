# 🎬 BookMyShow Frontend Kubernetes Deployment

![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Deployed-success)
![Traefik](https://img.shields.io/badge/Ingress-Traefik-orange)
![Status](https://img.shields.io/badge/Status-Working-brightgreen)

---

# 🔗 GitHub Repository

[https://github.com/sandeepcharan-devops/bookmyshow-helm-chart.git](https://github.com/sandeepcharan-devops/bookmyshow-helm-chart.git)

---

# 📌 Project Overview

This project demonstrates deploying a frontend application to Kubernetes using Docker, Kubernetes manifests, Services, and Traefik Ingress.

The deployment includes:

* Dockerized frontend application
* Kubernetes Deployment
* Kubernetes Service
* Traefik Ingress
* GitHub integration
* Kubernetes troubleshooting

---

# 🛠 Technologies Used

| Technology | Purpose                 |
| ---------- | ----------------------- |
| Docker     | Containerization        |
| Kubernetes | Container orchestration |
| Traefik    | Ingress controller      |
| GitHub     | Version control         |
| Ubuntu EC2 | Hosting environment     |

---

# 📂 Project Structure

```text
BookMyShow-devops/
 ├── Dockerfile
 ├── deployment.yaml
 ├── service.yaml
 ├── ingress.yaml
 ├── .dockerignore
 └── README.md
```

---

# 🐳 Docker Setup

## Build Docker Image

```bash
docker build -t bookmyshow .
```

---

## Tag Docker Image

```bash
docker tag bookmyshow yourdockerhub/bookmyshow:latest
```

---

## Push Image to DockerHub

```bash
docker push yourdockerhub/bookmyshow:latest
```

---

# ☸️ Kubernetes Deployment

## Apply Deployment

```bash
kubectl apply -f deployment.yaml
```

---

## Apply Service

```bash
kubectl apply -f service.yaml
```

---

## Apply Ingress

```bash
kubectl apply -f ingress.yaml
```

---

# 📄 Deployment YAML Example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: bms-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: bms
  template:
    metadata:
      labels:
        app: bms
    spec:
      containers:
      - name: bms
        image: yourdockerhub/bookmyshow:latest
        ports:
        - containerPort: 3000
```

---

# 📄 Service YAML Example

```yaml
apiVersion: v1
kind: Service
metadata:
  name: bms-service
spec:
  selector:
    app: bms
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
```

---

# 📄 Ingress YAML Example

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: bms-ingress
spec:
  ingressClassName: traefik
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: bms-service
            port:
              number: 80
```

---

# 🌐 Access Application

Application accessible using:

```text
http://<EC2-PUBLIC-IP>
```

Example:

```text
http://18.209.69.62
```

⚠️ Do NOT use:

```text
https://IP:80
```

Because:

* Port 80 = HTTP
* Port 443 = HTTPS

---

# 📊 Kubernetes Verification Commands

## Check Pods

```bash
kubectl get pods
```

---

## Check Deployments

```bash
kubectl get deploy
```

---

## Check Services

```bash
kubectl get svc
```

---

## Check Ingress

```bash
kubectl get ingress
```

---

## Describe Ingress

```bash
kubectl describe ingress
```

---

## View Pod Logs

```bash
kubectl logs <pod-name>
```

---

# 🔥 Errors Faced and Solutions

---

## ❌ Error 1

```text
connection refused
```

### Cause

Application was not exposed correctly.

### Solution

Verify:

```bash
kubectl get svc
kubectl get ingress
```

Ensure Traefik ingress is configured properly.

---

## ❌ Error 2

```text
https://IP:80 not working
```

### Cause

HTTPS cannot run on port 80 without TLS configuration.

### Solution

Use:

```text
http://<EC2-PUBLIC-IP>
```

---

## ❌ Error 3

```text
ImagePullBackOff
```

### Cause

Docker image not found or incorrect repository name.

### Solution

Verify image:

```bash
docker push yourdockerhub/bookmyshow:latest
```

Update deployment image properly.

---

## ❌ Error 4

```text
CrashLoopBackOff
```

### Cause

Application crashing inside container.

### Solution

Check logs:

```bash
kubectl logs <pod-name>
```

Fix application/container issues.

---

## ❌ Error 5

```text
No space left on device
```

### Cause

EC2 storage full due to Docker images and node_modules.

### Solution

Clean Docker resources:

```bash
docker system prune -a
```

Remove unnecessary files.

---

## ❌ Error 6

```text
Ingress not routing traffic
```

### Cause

Ingress class mismatch.

### Solution

Set:

```yaml
ingressClassName: traefik
```

inside ingress.yaml.

---

# 🚀 Scaling Application

Increase replicas:

```yaml
replicas: 3
```

Apply changes:

```bash
kubectl apply -f deployment.yaml
```

Verify:

```bash
kubectl get pods
```

---

# 📌 GitHub Integration

## Initialize Git

```bash
git init
```

---

## Add Files

```bash
git add .
```

---

## Commit Changes

```bash
git commit -m "Added Kubernetes deployment"
```

---

## Add Remote Repository

```bash
git remote add origin git@github.com:sandeepcharan-devops/bookmyshow-helm-chart.git
```

---

## Push Code

```bash
git branch -M main
git push -u origin main
```

---

# 🎯 Final Outcome

✅ Frontend application containerized using Docker

✅ Kubernetes Deployment created

✅ Kubernetes Service created

✅ Traefik Ingress configured

✅ Application accessible through EC2 public IP

✅ Source code pushed to GitHub

---

# 🚀 Future Improvements

* Add backend deployment
* Add ConfigMaps and Secrets
* Use custom domain
* Enable HTTPS/TLS
* Add monitoring and logging
* Add CI/CD pipeline
* Add autoscaling

---

# 👨‍💻 Author

Sandeep Charan

GitHub:

```text
https://github.com/sandeepcharan-devops
```

---

# ⭐ Conclusion

This project demonstrates a beginner-to-intermediate DevOps workflow using:

* Docker
* Kubernetes
* Services
* Traefik Ingress
* GitHub

It covers:

* Containerization
* Kubernetes deployment
* Networking
* Troubleshooting
* Git integration
* Resource management

---

# 🎉 Kubernetes Deployment Successful
