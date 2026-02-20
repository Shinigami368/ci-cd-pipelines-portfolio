# GitHub Actions CI/CD Pipelines – Portfolio

This repository contains **template-based CI/CD pipelines** designed with reusability, modularity, and security in mind. All workflows are built using GitHub Actions and follow AWS best practices for deploying Dockerized applications via ECR and ECS.

These templates reflect the architecture I used to reduce production deployment times by up to 60% in my previous roles.
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
- 🕒 **Versioned Image Tagging with Timestamps**: Docker images are tagged using timestamp-based versions (e.g., `20250808T152045`) instead of `latest`, ensuring reliable rollbacks and avoiding deployment collisions. This creates a deterministic deployment history across ECR and ECS.

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
- Triggers deployment only for affected service(s)
- Built using centralized reusable workflows
- Two alternative strategies available:
  - **Static Job-Based**: Each service has its own deployment job with conditional logic
  - **Matrix-Based**: Uses a matrix to dynamically loop through services, reducing code duplication and improving scalability
- Easily extensible for large microservice setups

📄 [`monorepo/Monorepo-CICD-Change-Detection.yaml`](https://github.com/Shinigami368/ci-cd-pipelines-portfolio/blob/main/monorepo/Monorepo-CICD-Change-Detection.yaml)  
📄 [`monorepo/Monorepo-CICD-ECS-Deployment.yaml`](https://github.com/Shinigami368/ci-cd-pipelines-portfolio/blob/main/monorepo/Monorepo-CICD-ECS-Deployment.yaml)  
📄 [`monorepo/Monorepo-CICD-Matrix-Change-Detection.yaml`](https://github.com/Shinigami368/ci-cd-pipelines-portfolio/blob/main/monorepo/Monorepo-CICD-Matrix-Change-Detection.yaml)

---

## 📌 Notes

- 🚫 **Sensitive Data Masked**: All names, secrets, repository paths, and container IDs have been altered to prevent any data leakage.
- ♻️ **Easily Reusable**: You can reuse any pipeline by replacing the service name, ECR repo, ECS settings, and GitHub secrets.
- ⚙️ **Built for Production**: All pipelines have been tested and used in real deployment scenarios with active ECS clusters and services.
- 🔁 **Built-In Rollback Friendly**: Each deploy creates a unique ECS task definition revision and timestamp-tagged Docker image. ECS automatically preserves a full version history, enabling seamless rollback to any previous state without requiring custom tooling or external version tracking.

Open to B2B/Contract Cloud & DevOps opportunities. Let's connect on https://www.linkedin.com/in/berkay-cakibey/ or reach out via cakibey368@gmail.com.

---

Thanks for visiting the CI/CD portfolio!  
Feel free to fork, copy, or reach out for improvements or collaboration.
