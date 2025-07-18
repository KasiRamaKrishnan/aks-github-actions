# 🟣 Personal AKS + ArgoCD GitOps Setup 🚀

## ✅ Overview
This repository automates:
- ✅ Azure AKS cluster creation using GitHub Actions
- ✅ ArgoCD installation via Helm
- ✅ Application deployment using GitOps with ArgoCD
- ✅ AKS cluster deletion to save daily costs

---

## 📁 Project Structure
├── .github/workflows/ # GitHub Actions (create-aks.yml, delete-aks.yml)
├── helm/ # ArgoCD values.yaml
├── manifests/ # ArgoCD GitOps Application manifest
└── README.md # This file


---

## ⚙️ Prerequisites
- Azure Subscription
- GitHub Repository (this project)
- GitHub Secrets configured:
  - `AZURE_CREDENTIALS` – Azure Service Principal credentials (JSON output from az ad sp create-for-rbac --sdk-auth)
  - `RESOURCE_GROUP` – Resource Group for AKS
  - `CLUSTER_NAME` – AKS Cluster Name
  - `LOCATION` – Azure region (e.g., southindia)

---

## 🚀 Usage Guide

### ✅ 1. Create AKS + Install ArgoCD
- Trigger `create-aks.yml` from GitHub Actions → Run Workflow
- This will:
  - Create AKS Cluster
  - Install ArgoCD via Helm
  - Deploy applications using ArgoCD GitOps

---

### ✅ 2. Access ArgoCD UI

#### Option A: **If LoadBalancer Service is used**
```bash
kubectl -n argocd get svc argocd-server

Open browser: https://<EXTERNAL-IP>


### ArgoCD Login Credentials:

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
Username: admin

Password: (output of above command)

