## What is DevOps?

- **DevOps** is a way of working where **development** and **operations** teams work together to deliver software **faster, safer, and more reliably**.
- It improves application delivery by using:
  - **Automation** (reduce manual work)
  - **CI/CD** (build, test, deploy continuously)
  - **Code quality checks** (linting, reviews, security scans)
  - **Monitoring / Observability** (logs, metrics, traces to detect issues early)
  - **Continuous testing** (unit, integration, end-to-end tests)
- The goal is to reduce manual effort, reduce release risk, and ship changes quickly.

---

## Why DevOps?

### Before DevOps

- **Developer** writes code and pushes to the repo.
- **System Administrator** manually creates servers.
- **Build/Release Engineer** builds and deploys the application.
- **Ops/Server Admin** configures the application server and fixes production issues.

**Cons**
- Slow releases
- Lots of manual steps
- More deployment mistakes
- Hard to trace issues quickly
- “Dev vs Ops” blame game

---

### DevOps (Modern Flow)

- **Developer + DevOps** use automated pipelines to build/test/deploy.
- Infrastructure is created using **Infrastructure as Code (IaC)** (Terraform/CloudFormation).
- Deployments are automated using **CI/CD**.
- Environments are consistent using **containers** and **configuration management**.
- Apps are continuously monitored using **observability tools**.
- Fast rollback and reliable releases (blue/green, canary).

**Pros**
- Faster delivery
- Stable systems
- Fewer outages
- Easier debugging
- Better collaboration

---

## Activities performed by a DevOps Engineer

### CI/CD
- Set up pipelines (Jenkins, GitHub Actions, GitLab CI).
- Automate: **build → test → scan → deploy**.
- Manage versioning and release workflows.

### Infrastructure & Cloud
- Provision servers/services using **IaC**.
- Manage cloud services: compute, storage, network, load balancers, databases.
- Cost optimization and resource cleanup.

### Containers & Orchestration
- Create and manage **Docker** images.
- Deploy apps using **Kubernetes/ECS**.
- Handle scaling, service discovery, deployments, and rollbacks.

### Monitoring & Observability
- Set up dashboards and alerts (Prometheus, Grafana, CloudWatch).
- Central logging (ELK, Loki, Splunk).
- Tracing and performance monitoring (Jaeger, Datadog, New Relic).
- On-call support, incident response, postmortems.

### Security & Compliance (DevSecOps)
- Add security scans in pipelines (SAST/DAST, container scans).
- Manage secrets (Vault, AWS Secrets Manager).
- Enforce least privilege access (IAM, RBAC).

### Configuration & Reliability
- Standardize environments (dev/test/prod).
- Use configuration management (Ansible, Chef, Puppet).
- Improve uptime, backups, and disaster recovery.

### Collaboration & Process Improvements
- Work with developers to improve deployments and debugging.
- Document runbooks and operational procedures.
- Improve release speed and reduce failures.
```
