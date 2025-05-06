```markdown
# 📘 GitOps Flow Notes – Farm App Deployment with ArgoCD

This document outlines the end-to-end GitOps journey of deploying the `farm-app` using ArgoCD on a K3s cluster inside an Azure VM. It covers the validation, setup, deployment, sync process, and lessons learned.

---

## 1️⃣ Initial Validation

- ✅ Confirmed that K3s was successfully installed on the Azure VM
- 🧪 Verified Kubernetes cluster health using `kubectl get nodes`
- 🔐 Ensured that necessary ports (for ArgoCD UI and NodePorts) were opened in the Azure Network Security Group

---

## 2️⃣ ArgoCD Setup

- 📦 Installed ArgoCD in the `argocd` namespace using the official manifest
- 🌐 Patched `argocd-server` to NodePort to make the UI accessible
- 🔑 Retrieved the admin password from Kubernetes secrets
- 👨‍💻 Logged in to the ArgoCD web UI via the VM public IP and NodePort

---

## 3️⃣ Git Repository & Manifest Structure

- 🗂️ Created a GitHub repository to hold deployment manifests
- 📁 Structured the repo with separate `frontend` and `backend` directories, each containing:
  - `deployment.yaml`
  - `service.yaml`
- 🧩 Added a `namespace.yaml` and a root `kustomization.yaml` to aggregate all components
- 🧪 Validated manifests locally using Kustomize before committing

---

## 4️⃣ ArgoCD Application Deployment

- 🛠️ Created an ArgoCD `Application` pointing to the GitHub repo’s root
- 🔄 Configured automatic sync with:
  - `prune: true` – removes obsolete resources
  - `selfHeal: true` – auto-recovers from drift
- 🎯 Set target revision to `main` and path to `.`
- ✅ On committing the `Application.yaml`, ArgoCD auto-synced and deployed the manifests

---

## 5️⃣ GitOps Sync in Action

- 📝 Made a change in the deployment manifest (e.g., image tag update)
- ⬆️ Committed and pushed the change to GitHub
- 🔁 ArgoCD automatically:
  - Detected the change
  - Synced it to the cluster
  - Updated the affected pods
- 🟢 Status reflected as “Synced” and “Healthy” in the UI

---

## 6️⃣ Observations from the Workflow

- 📌 Git acted as the **single source of truth** for deployments
- 🧠 Zero need to manually `kubectl apply` manifests after ArgoCD setup
- 👁️ ArgoCD UI provided clear visibility into:
  - Sync history
  - Commit hashes
  - Application health
- 🔁 Sync policies made recovery from cluster drift automatic

---

## 7️⃣ Lessons Learned

- 💡 Validate manifests with `kustomize build .` before pushing
- 🔍 Be cautious of YAML indentation and spacing – small mistakes can cause sync failure
- 🔓 Configure firewall rules early to avoid debugging connectivity later
- 🛡️ Auto-sync with self-heal is powerful for production safety

---

## 🧠 Key Observations & Takeaways

### ✅ What Went Well
- Git became the **single source of truth**
- ArgoCD provided live feedback and complete visibility
- Auto-sync ensured drift correction without intervention
- Kustomize helped modularize the configuration cleanly

### ⚠️ Challenges Faced
- Required manual NAT/firewall rules in Azure
- Sync failure occurred due to a subtle YAML error
- ArgoCD sessions expired after a while without persistent login

### 💡 Final Takeaways
- GitOps provides **traceability, repeatability, and automation**
- It's not just CI/CD — it’s **declarative infrastructure with full control**
- This setup proved simple, reproducible, and transparent for cloud-native deployments

---

> ✅ “GitOps made deploying to Kubernetes as simple as pushing to Git — no guesswork, just clarity and automation.”

```
