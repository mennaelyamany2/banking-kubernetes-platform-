# 🏦 Banking Platform on Kubernetes

A production-style banking microservices platform deployed on **Kubernetes (Minikube)** using **Node.js**, **PostgreSQL**, and **Docker**.  
This project was built to apply real-world DevOps practices like auto-scaling, self-healing, persistent storage, and zero-downtime updates — not just theory.

---

## 🚀 What’s inside?

- ✅ Banking API (Node.js + Express + PostgreSQL)
- ✅ Dashboard UI (HTML/CSS/JS) served via Nginx
- ✅ PostgreSQL with StatefulSet + Persistent Storage
- ✅ Liveness & Readiness Probes for self-healing
- ✅ Rolling Updates with zero downtime
- ✅ Horizontal Pod Autoscaler (HPA) based on CPU
- ✅ NetworkPolicy for internal security
- ✅ Fluentd DaemonSet for log collection
- ✅ RBAC for API service account
- ✅ Ingress ready (NGINX)

---

## 🛠️ Technologies Used

| Category | Tools |
|----------|-------|
| Containerization | Docker |
| Orchestration | Kubernetes (Minikube) |
| Backend | Node.js, Express |
| Database | PostgreSQL 15 |
| Frontend | HTML, CSS, JS + Nginx |
| Observability | Liveness/Readiness probes, Fluentd |
| Scaling | HPA (Horizontal Pod Autoscaler) |
| Storage | PersistentVolumeClaim (PVC) |
| Security | Secrets, ConfigMaps, NetworkPolicy, RBAC |

---
📁 Project Structure
banking-kubernetes-platform/
├── app/
│   ├── banking-api/
│   │   ├── Dockerfile
│   │   ├── app.js
│   │   └── package.json
│   └── banking-dashboard/
│       ├── Dockerfile
│       ├── index.html
│       └── nginx.conf
├── k8s/
│   ├── 00-namespace.yaml
│   ├── 01-configmap.yaml
│   ├── 02-secret.yaml
│   ├── 03-postgres-statefulset.yaml
│   ├── 04-api-deployment.yaml
│   ├── 05-dashboard-deployment.yaml
│   ├── 06-services.yaml
│   ├── 07-ingress.yaml
│   ├── 08-hpa-vpa.yaml
│   ├── 09-rbac.yaml
│   ├── 10-networkpolicy.yaml
│   └── 11-daemonset.yaml
└── README.md
⚙️ How to Run
1️⃣ Start Minikube
minikube start --nodes 2
2️⃣ Build & Push Images (Docker Hub)
docker build -t mennaelyamany/banking-api:v2.0 -f app/banking-api/Dockerfile ./app/banking-api
docker build -t mennaelyamany/banking-dashboard:v2.0 -f app/banking-dashboard/Dockerfile ./app/banking-dashboard

docker push mennaelyamany/banking-api:v2.0
docker push mennaelyamany/banking-dashboard:v2.0
3️⃣ Apply Kubernetes Manifests
kubectl apply -f k8s/
4️⃣ Access the Dashboard
minikube service -n banking banking-dashboard-service
🧪 What I Learned (the hard way)
What I thought	What actually happened
Running means everything is fine	❌ Nope — probes matter
PostgreSQL can be a normal Deployment	❌ Data disappears — need StatefulSet
HPA scales instantly	❌ It depends on metrics and thresholds
NetworkPolicy is optional	✅ It's critical for real security
Local registry is easy	✅ Docker Hub is simpler for multi-node
🔥 Key Features Demonstrated
Feature	How it's implemented
Self-healing	Liveness probe restarts failed containers
Zero downtime	RollingUpdate strategy with maxUnavailable: 0
Data persistence	PVC + StatefulSet for PostgreSQL
Auto-scaling	HPA scales API pods from 2 to 5 based on CPU
Log collection	Fluentd DaemonSet on every node
Security	Secrets, NetworkPolicy, RBAC
Traffic routing	Ingress + ClusterIP + NodePort
📸 Screenshots (suggested)
Dashboard UI in browser
kubectl get pods -n banking -o wide showing 2 nodes
curl http://localhost:3000/api/health response
PostgreSQL data still alive after pod deletion
🚧 Future Improvements
Add Prometheus + Grafana monitoring
CI/CD pipeline with GitHub Actions
Deploy to cloud (EKS, AKS, or GKE)
Add GitOps with ArgoCD
👩‍💻 Author

Menna Elyamany
DevOps Engineer | Cloud & Kubernetes Enthusiast

GitHub: mennaelyamany2
LinkedIn: menna-elyamany