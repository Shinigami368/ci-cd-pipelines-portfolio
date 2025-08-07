# GitHub Actions CI/CD Pipelines – Portfolio

This repository contains **template-based CI/CD pipelines** designed with reusability, modularity, and security in mind. All workflows are built using GitHub Actions and follow AWS best practices for deploying Dockerized applications via ECR and ECS.

---

## 📁 Folder Structure

- `monorepo/` – Multi-service architecture with change detection
- `multi-env/` – Branch-based (dev/prod) deployments with caching
- `single-repo/` – Minimal pipelines for isolated services

---

## 🔧 Key Features

- ✅ **Reusable Templates**: Each workflow is designed as a portable template — copy-paste ready for different projects.
- 🔒 **Secrets-Based Configuration**: All environment values are expected to be passed via GitHub Secrets. No credentials or hardcoded values exist in the YAML files.
- 🧱 **Modular Build Steps**: Built primarily using `uses:` syntax from GitHub’s official and community actions, instead of manual shell commands.
- 🔁 **Rolling Deployments**: All ECS deployments are done via `rolling update` strategy for zero-downtime releases.

---

## 🚀 Included Pipelines

### 1. Single Repo – ECS Deployment

- Detects changes on the `master` branch
- Builds Docker image from project root
- Pushes image to Amazon ECR
- Updates ECS task definition
- Triggers rolling deployment to ECS service

📄 [`single-repo/Single-Repo-CICD-ECS-Deployment.yaml`](https://github.com/Shinigami368/ci-cd-pipelines-portfolio/blob/main/single-repo/Single-Repo-CICD-ECS-Deployment.yaml)

---

### 2. Multi-Environment – Dev/Prod ECS Deployments

- Deploys based on the target branch (`main` → production, `dev` → development)
- Separate ECR repositories, task definitions, and ECS services per environment
- Supports Docker build caching for faster deployment (especially Bun & Next.js apps)
- Ideal for frontend/backend workflows where build size matters

📄 [`multi-env/Multi-Environment-CICD-ECS-Deployment.yaml`](https://github.com/Shinigami368/ci-cd-pipelines-portfolio/blob/main/multi-env/Multi-Environment-CICD-ECS-Deployment.yaml)  
📄 [`multi-env/Multi-Environment-CICD-Nextjs-ECS-Deployment.yaml`](https://github.com/Shinigami368/ci-cd-pipelines-portfolio/blob/main/multi-env/Multi-Environment-CICD-Nextjs-ECS-Deployment.yaml)  
📄 [`multi-env/Multi-Environment-CICD-Bun-ECS-Deployment.yaml`](https://github.com/Shinigami368/ci-cd-pipelines-portfolio/blob/main/multi-env/Multi-Environment-CICD-Bun-ECS-Deployment.yaml)

---

### 3. Monorepo – Change Detection & Reusable Workflow

- Detects which specific folder/service was changed
- Triggers deploy only for affected service(s)
- Calls a centralized reusable deployment workflow
- Names, branches, and folder paths have been anonymized for security
- Can be repurposed by adjusting folder names and secrets

📄 [`monorepo/Monorepo-CICD-Change-Detection.yaml`](https://github.com/Shinigami368/ci-cd-pipelines-portfolio/blob/main/monorepo/Monorepo-CICD-Change-Detection.yaml)  
📄 [`monorepo/Monorepo-CICD-ECS-Deployment.yaml`](https://github.com/Shinigami368/ci-cd-pipelines-portfolio/blob/main/monorepo/Monorepo-CICD-ECS-Deployment.yaml)

---

## 📌 Notes

- 🚫 **Sensitive Data Masked**: All names, secrets, repository paths, and container IDs have been altered to prevent any data leakage.
- ♻️ **Easily Reusable**: You can reuse any pipeline by replacing the service name, ECR repo, ECS settings, and GitHub secrets.
- ⚙️ **Built for Production**: All pipelines have been tested and used in real deployment scenarios with active ECS clusters and services.

---

Thanks for visiting the CI/CD portfolio!  
Feel free to fork, copy, or reach out for improvements or collaboration.
