# AI Knowledge Copilot — Azure, Terraform, Kubernetes & CI/CD
**DevOps Trainee Capstone Project**

Enterprise-grade RAG AI Copilot built and automated on Microsoft Azure using Terraform, Docker, Azure Kubernetes Service (AKS), Azure App Service, and CI/CD pipelines.

---

## 📁 Repository Structure

```
├── backend/                       # Python FastAPI RAG Service & Vector Engine
│   ├── app.py                     # Ingestion, chunking, cosine retrieval, grounded Q&A
│   ├── requirements.txt           # Dependencies
│   └── Dockerfile                 # Multi-stage minimal non-root image
├── frontend/                      # Responsive Knowledge Copilot Web Interface
│   ├── index.html                 # Modern responsive chat and document manager
│   ├── app.js                     # Dynamic API host connection & RAG handler
│   ├── nginx.conf                 # Reverse proxy & routing config
│   └── Dockerfile                 # Non-root alpine NGINX container
├── terraform/                     # Modular Infrastructure as Code
│   ├── modules/
│   │   ├── resource-group/        # Resource group definition
│   │   ├── networking/            # VNet, AKS Subnet, AppService Subnet
│   │   ├── acr/                   # Azure Container Registry
│   │   ├── aks/                   # Azure Kubernetes Service Cluster + RBAC
│   │   ├── app-service/           # Linux Web App + Service Plan
│   │   ├── storage/               # Blob Storage for RAG documents
│   │   ├── key-vault/             # Azure Key Vault secret management
│   │   └── monitoring/            # Log Analytics & Application Insights
│   └── environments/
│       ├── dev/                   # Development environment configuration
│       ├── staging/               # Staging environment configuration
│       └── prod/                  # Production environment configuration
├── kubernetes/                    # Declarative Kubernetes Manifests
│   ├── namespace.yaml             # Isolated ai-copilot namespace
│   ├── configmap.yaml             # Runtime application configuration
│   ├── secrets.yaml               # Encrypted secret parameters
│   ├── backend-deployment.yaml    # 2 Replicas, rolling update, probes, requests/limits
│   ├── backend-service.yaml       # Internal ClusterIP service
│   ├── frontend-deployment.yaml   # 2 Replicas, non-root user
│   ├── frontend-service.yaml      # Public LoadBalancer service
│   ├── ingress.yaml               # Routing ingress controller rules
│   └── hpa.yaml                   # Horizontal Pod Autoscaler (CPU 75%)
├── helm/                          # Production Helm 3 Chart
│   └── ai-knowledge-copilot/      # Chart.yaml, values.yaml, templates
├── .github/workflows/             # Continuous Integration & Delivery
│   └── ci-cd.yaml                 # Lint, test, docker build & scan, terraform validate, deploy
├── tests/                         # Automated Test Suite
│   └── test_backend.py            # Unit tests, RAG chunking & vector search tests
└── docs/                          # Architecture & Operational Documentation
    ├── architecture.md            # System architecture & AKS vs App Service analysis
    ├── deployment.md              # Complete deployment manual
    ├── troubleshooting.md         # Incident response runbooks & RCA
    └── rollback.md                # Rollback procedures for AKS & App Service
```

---

## 🚀 Quick Start

### 1. Run Automated Tests
```powershell
python -m pytest tests/test_backend.py -v
```

### 2. Provision Infrastructure via Terraform
```powershell
cd terraform/environments/dev
terraform init
terraform plan
terraform apply -auto-approve
```

### 3. Deploy to AKS
```powershell
az aks get-credentials --resource-group aicopilot-dev-rg --name aicopilot-dev-aks
kubectl apply -f kubernetes/
```

