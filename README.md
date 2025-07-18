Personal AKS + ArgoCD GitOps Automation 🚀
✅ Overview
This project automates:

🎉 AKS Cluster creation via GitHub Actions

🎉 ArgoCD installation via Helm

🎉 GitOps Application deployment via ArgoCD

🎉 Easy deletion of AKS to avoid costs

📁 Folder Structure
graphql
Copy
Edit
.
├── .github/workflows/           # GitHub Actions for create & delete AKS
├── helm/                        # ArgoCD Helm chart values
├── manifests/                   # ArgoCD GitOps app definitions
└── README.md                    # This file
⚙️ Pre-requisites
✅ Azure subscription

✅ GitHub repository with these files

✅ GitHub Secrets configured:

AZURE_CREDENTIALS (SP JSON)

RESOURCE_GROUP

CLUSTER_NAME

LOCATION (e.g., southindia)

🚀 AKS & ArgoCD Deployment Steps
1. Create AKS and Deploy ArgoCD
Go to GitHub → Actions → Run Workflow on create-aks.yml

It will:
✅ Create AKS
✅ Install ArgoCD via Helm
✅ Deploy GitOps applications via ArgoCD

2. Access ArgoCD UI
🔵 If LoadBalancer Service:
bash
Copy
Edit
kubectl -n argocd get svc argocd-server
✅ Access via https://<external-ip>

🔵 If ClusterIP (Default):
bash
Copy
Edit
kubectl port-forward svc/argocd-server -n argocd 8080:443
✅ Access via https://localhost:8080

🔑 Get ArgoCD Admin Password:
bash
Copy
Edit
kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 -d
✅ Username: admin
✅ Password: (output above)

3. Delete AKS Cluster
Go to GitHub → Actions → Run Workflow on delete-aks.yml

✅ This will delete AKS and avoid costs.

🟢 Bonus Commands (Local Setup)
Get Kubeconfig in WSL:

bash
Copy
Edit
az aks get-credentials --resource-group <rg> --name <aks-name> --overwrite-existing
For WSL:

bash
Copy
Edit
export KUBECONFIG=/mnt/c/Users/<your-user>/.kube/config
📌 Notes
Port-forwarding is simplest for local testing.

You can optionally configure Ingress + DNS (argocd.kasi.com) for custom domains.

🎉 Summary
✅ Automated AKS creation
✅ ArgoCD GitOps deployments
✅ Easy cost-saving via on-demand cluster deletion
✅ Clean, simple setup!