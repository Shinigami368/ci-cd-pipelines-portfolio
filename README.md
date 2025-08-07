# GitHub Actions CI/CD Pipelines – Portfolio

This repository contains **template-based CI/CD pipelines** designed with reusability and security in mind. All workflows are modular, environment-aware, and follow AWS best practices for deploying Dockerized applications using ECR and ECS.

---

## 📁 Folder Structure

- `monorepo/` – Multi-service architecture with change detection
- `multi-env/` – Branch-based (dev/prod) deployments with build caching
- `single-repo/` – Minimal pipelines for isolated services

---

## 🔧 Key Features

- ✅ **Reusable Templates**: Each pipeline is designed to be reused across projects with minimal changes. Copy-paste ready.
- 🔒 **Secrets Management**: All environment variables are expected to be defined as GitHub Secrets — no hardcoding, no security leaks.
- 🧱 **Fully Modular**: All steps are built using `uses:`-based GitHub Actions where possible — avoids manual shell scripts.
- 🔁 **Rolling Deployments**: All ECS deployments are done with zero downtime via rolling update strategy.

---

## 🚀 Included Pipelines

### 1. Single Repo – ECS Deployment
- Detects code push to `master`
- Builds Docker image from repo
- Pushes to Amazon ECR
- Updates ECS task definition
- Triggers ECS rolling deployment

📂 Path: `single-repo/Single-Repo-CICD-ECS-Deployment.yaml`

---

### 2. Multi-Environment – Dev/Prod ECS Deployments
- Detects code push to `main` (production) or `dev` (development)
- Uses different ECS services & clusters based on branch
- Supports build caching for faster deploys (Next.js, Bun, etc.)
- Designed for performance without compromising flexibility

📂 Path:  
- `multi-env/Multi-Environment-CICD-ECS-Deployment.yaml`  
- `multi-env/Multi-Environment-CICD-Nextjs-ECS-Deployment.yaml`  
- `multi-env/Multi-Environment-CICD-Bun-ECS-Deployment.yaml`

---

### 3. Monorepo – Service-Specific Deployments
- Detects which subfolder (service) was changed
- Only deploys affected services (`auth`, `frontend`, `api`, etc.)
- Calls reusable deploy workflow using `workflow_call`
- Names, paths, and branches are anonymized for data security

📂 Path:  
- `monorepo/Monorepo-CICD-ECS-Deployment.yaml`  
- `monorepo/Monorepo-CICD-Change-Detection.yaml`

---

## 📌 Notes

- 🚫 **Sensitive Names Masked**: Folder names, service identifiers, and secrets have been modified to prevent data exposure.
- ♻️ **Can Be Reused**: Simply rename services, secrets, and paths — ready to go.
- ⚙️ **Production-Ready**: All pipelines tested in production-like environments, following AWS ECS & GitHub Actions best practices.

---
