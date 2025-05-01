
```markdown
# 🌾 Farm App – GitOps with ArgoCD & Kubernetes

A complete GitOps-based deployment pipeline for a multi-service (frontend + backend) farm management app using **ArgoCD**, **Kustomize**, and **Kubernetes**.

---

## 🚀 Project Overview

This project demonstrates the power of GitOps by automatically deploying and syncing a microservices-based application (frontend and backend) using declarative manifests stored in Git. ArgoCD watches the Git repo and ensures the cluster state always matches the Git state.

---

## 🧰 Tech Stack

- ⚙️ **Kubernetes (K3s on Azure VM)**
- 🚀 **ArgoCD** for GitOps delivery
- 🧩 **Kustomize** for YAML composition
- 🐳 **Docker** for containerization
- 🐙 **GitHub** for source control
- 🌐 **NodePort Services** for VM-based access

---

## 🗂️ Repository Structure

```
repo-root/
├── backend/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── kustomization.yaml
├── frontend/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── kustomization.yaml
├── namespace.yaml
└── kustomization.yaml
```

---

## 🔁 GitOps Workflow

### 1. 💻 Development
- Code changes are made to the backend/frontend.
- Deployment YAML files are updated as needed.

### 2. ⬆️ Git Commit & Push
- Changes are committed to the GitHub repository.
- Kustomize structures the manifests with overlays.

### 3. 🤖 ArgoCD Sync
- ArgoCD auto-detects changes from Git.
- Sync is performed to update the cluster state.

### 4. 🔄 Rollback (if needed)
- Previous states can be rolled back from ArgoCD UI using the **History and Rollback** feature.

---

## 🌐 Accessing the Application

### Frontend:
```bash
http://<VM-PUBLIC-IP>:30460
```

### Backend:
```bash
http://<VM-PUBLIC-IP>:30488
```

> Replace `<VM-PUBLIC-IP>` with your Azure VM's public IP address. Make sure the required ports are open in the firewall.

---

## 📽️ Demo Video / Notes

Check out the [GitOps Demo Notes](GitOps-Flow.md) for a breakdown of the setup and sync process.

---

## 🛡️ Future Improvements

- Add Ingress + TLS (Ingress-NGINX + Cert-Manager)
- Auto-sync with webhooks or ApplicationSets
- Helm integration for complex apps
- CI pipeline to build & push Docker images

---

## 🧠 Key Learnings

- How GitOps enforces cluster consistency
- Declarative infrastructure is more traceable
- ArgoCD offers full Git history, rollback, and audit

---

## 👨‍💻 Author
prasad suryavanshi

---

## ⭐ Show your support

If this helped you learn GitOps, consider giving this repo a ⭐!
```

---
