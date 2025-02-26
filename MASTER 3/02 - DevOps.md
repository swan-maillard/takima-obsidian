---
cover: "[[devops.png]]"
---
# 💠 Table of Contents
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 2 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```
---

# 💠 What is DevOps?

DevOps is a **set of practices, tools, and a cultural mindset** that aims to **bridge the gap between development (Dev) and operations (Ops)**. It focuses on **automating, integrating, and improving collaboration** between software development teams and IT operations to deliver software faster, more reliably, and with higher quality.

### **Key Principles of DevOps**

- **Continuous Integration & Continuous Deployment (CI/CD)** – Automates building, testing, and deploying applications.
- **Infrastructure as Code (IaC)** – Manages infrastructure through code (e.g., Terraform, Ansible).
- **Monitoring & Logging** – Ensures system health and performance with tools like Prometheus, Grafana, and ELK.
- **Collaboration & Automation** – Breaks down silos between teams and automates repetitive tasks.

---

# 💠 **Application Performance Monitoring (APM), Monitoring & Alerting**

Observability is crucial in DevOps to **detect, analyze, and resolve issues** before they impact users. This includes **metrics, logs, and traces** to monitor system health and performance.

- **Prometheus** – The industry-standard **time-series monitoring system**, widely used with Kubernetes for collecting and storing metrics.
- **Grafana** – A **visualization tool** that integrates with Prometheus (and other data sources) to create real-time dashboards and alerts.
- **ELK Stack (Elasticsearch, Logstash, Kibana)** – The most popular **log management stack**:
    - **Elasticsearch** – Efficiently indexes and searches logs.
    - **Logstash** – Processes and transforms log data.
    - **Kibana** – Provides visual insights into logs through dashboards.
- **Datadog** – A powerful **cloud-based APM** that combines metrics, logs, and traces (**but expensive**).
- **Sentry** – Focused on **error tracking** and application performance monitoring.

---

# 💠 **Provisioning, Environments, Infrastructure & Orchestration**

Infrastructure automation simplifies **deployment, scaling, and configuration management**. DevOps teams rely on **containerization, orchestration, and Infrastructure as Code (IaC)** to ensure consistency and scalability.

- **Docker** – The leading **containerization platform**, packaging applications into portable, lightweight containers.
- **Kubernetes (K8s)** – The industry-standard **orchestration tool** for automating the deployment, scaling, and management of containers.
- **Helm** – A package manager for Kubernetes that **simplifies deployment** using Helm charts.
- **Terraform** – The most widely used **Infrastructure as Code (IaC) tool** for provisioning and managing cloud resources.
- **Ansible** – A leading **configuration management tool**, using simple YAML-based playbooks to automate provisioning.
- **Other tools**
    - **Istio** – A **service mesh** that enhances security, observability, and traffic management in Kubernetes.
    - **Puppet** / **Chef** – Alternative configuration management tools to automate server setup and deployment.
    - **Vagrant** – Used for managing **virtual machine environments**, useful for development and testing.

---

# 💠 **CI/CD, Quality Gates & Pipeline Tools**

CI/CD automates **building, testing, and deploying** software, ensuring **continuous integration and delivery**. Quality gates guarantee only **high-quality** code reaches production.

- **GitLab CI/CD** – A popular **self-hosted CI/CD tool**, widely used in enterprises with GitLab repositories.
- **Jenkins** – One of the **most widely used CI/CD automation servers**, highly customizable with **plugins**.
- **GitHub Actions** – **Integrated into GitHub**, simplifying CI/CD workflows for GitHub repositories.
- **Other tools**
    - **ArgoCD** – A **GitOps-based CD tool**, Kubernetes-native for managing deployments.
    - **Tekton** – A Kubernetes-based **CI/CD framework** for cloud-native applications.
    - **SonarQube** – A powerful **static code analysis tool**, ensuring code quality and security.
    - **Artifactory** – A **universal artifact repository** for storing build artifacts, Docker images, and dependencies.

---

# 💠 **Security & Compliance in DevOps (DevSecOps)**

Security should be **integrated into every stage** of development and deployment to ensure compliance and protect applications from vulnerabilities.

- **Vault (by HashiCorp)** – A leading tool for **secrets management**, encrypting API keys, passwords, and sensitive data.
- **Trivy** – A widely used **vulnerability scanner** for Docker images, Kubernetes, and repositories.
- **Snyk** – Detects and fixes security vulnerabilities in **dependencies, container images, and infrastructure code**.
- **Aqua Security** – Focused on **container and Kubernetes security**.
- **Other tools**
    - **Falco** – A **Kubernetes runtime security tool**, detecting threats and anomalies.
    - **Clair** – A **container vulnerability scanner**, used to detect security risks in Docker images.
    - **OWASP ZAP** – An open-source **penetration testing tool** for identifying vulnerabilities in web applications.