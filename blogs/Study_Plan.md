# DevOps / Cloud Learning Plan

## Phase 0 – Absolute Foundations

- [ ] **0.1 Programming Foundations (Python)**
  - [ ] Understand why you’re learning Python (AWS automation, tools, ETL, CI/CD helpers)
  - [ ] Syntax basics: variables, types, `if/else`, loops, functions
  - [ ] Data structures: lists, dicts, sets, tuples
  - [ ] File I/O (read/write files)
  - [ ] Error handling (`try/except`)
  - [ ] Modules and virtual environments (`venv`)
  - [ ] OOP basics: classes, objects, methods
  - [ ] Working with JSON & YAML
  - [ ] Calling REST APIs with Python (`requests`)
  - [ ] **Boto3 basics**
    - [ ] Create/list EC2 instances
    - [ ] Create/list S3 buckets and objects
    - [ ] Create/list IAM users/roles
    - [ ] Create basic CloudWatch alarms

- [ ] **0.2 Linux & Bash – Everyday DevOps skill**
  - [ ] Basic commands: `ls`, `cd`, `cp`, `mv`, `rm`, `cat`, `less`, `grep`, `find`
  - [ ] Permissions: `chmod`, `chown`, `sudo`
  - [ ] Processes: `ps`, `top`/`htop`, `kill`, `journalctl`
  - [ ] SSH: key-based auth, `ssh` config, `scp`
  - [ ] Bash scripting
    - [ ] Variables, conditionals, loops
    - [ ] Small scripts to automate tasks (backups, log parsing)
    - [ ] Working with exit codes (`$?`)

- [ ] **0.3 Git & GitHub – Non-negotiable**
  - [ ] `git init`, `clone`, `add`, `commit`, `push`, `pull`
  - [ ] Branching: `branch`, `checkout`, `merge`
  - [ ] Pull Requests & code review flow
  - [ ] Resolving merge conflicts
  - [ ] GitHub basics: repos, issues, PRs, branch protection

---

## Phase 1 – Networking & Web Basics

- [ ] Understand IP address, subnet, gateway
- [ ] TCP vs UDP
- [ ] Ports: 80, 443, 22, common ones
- [ ] DNS basics: A, CNAME, MX, TXT records
- [ ] HTTP/HTTPS basics: methods, response codes
- [ ] Load balancers: why we need them, L4 vs L7
- [ ] SSL/TLS basics: certificates, HTTPS, why we need them

---

## Phase 2 – Core AWS

- [ ] **2.1 IAM**
  - [ ] Users, groups, roles
  - [ ] Policies (inline vs managed)
  - [ ] Least privilege principle
  - [ ] Cross-account access basics
  - [ ] IAM roles for EC2, Lambda, ECS tasks

- [ ] **2.2 VPC & Networking in AWS**
  - [ ] VPC, subnets (public vs private)
  - [ ] Route tables, Internet Gateway, NAT Gateway
  - [ ] Security Groups vs NACLs
  - [ ] VPC endpoints (S3, DynamoDB, etc.)
  - [ ] Basic multi-AZ setup

- [ ] **2.3 Compute & Storage**
  - [ ] EC2: AMIs, instance types, EBS, user-data scripts
  - [ ] S3: buckets, versioning, lifecycle rules, encryption, static website hosting
  - [ ] DynamoDB: tables, primary key + sort key, provisioned vs on-demand, basic GSIs/LSIs

- [ ] **2.4 Routing & Load Balancing**
  - [ ] Route53: hosted zones
  - [ ] Routing policies: simple, weighted, latency, failover
  - [ ] ALB vs NLB: use cases, target groups, health checks

- [ ] **2.5 CloudWatch**
  - [ ] Metrics & alarms
  - [ ] Logs & log groups
  - [ ] Dashboards
  - [ ] Log Insights (basic queries)

---

## Phase 3 – Infrastructure as Code (Terraform & CloudFormation)

- [ ] **3.1 Terraform**
  - [ ] HCL basics: providers, resources, variables, outputs
  - [ ] Commands: `init`, `plan`, `apply`, `destroy`
  - [ ] State & remote backends (S3 + DynamoDB locking)
  - [ ] Modules (for multi-env dev/stage/prod)
  - [ ] Workspaces or separate states per environment
  - [ ] Tagging strategy & reusable patterns

- [ ] **3.2 CloudFormation**
  - [ ] Templates: YAML/JSON structure
  - [ ] Stacks, parameters, mappings, outputs
  - [ ] Change sets
  - [ ] Nested stacks (for larger infra)

---

## Phase 4 – CI/CD: Jenkins, GitHub Actions, AWS CodePipeline

- [ ] **4.1 CI/CD Concepts**
  - [ ] Build → Test → Package → Deploy stages
  - [ ] Artifacts and versioning
  - [ ] Environments: dev, stage, prod
  - [ ] Blue/green & rolling deployments (conceptually)

- [ ] **4.2 Jenkins**
  - [ ] Jobs & pipelines
  - [ ] Declarative pipeline syntax (Jenkinsfile)
  - [ ] Pipeline stages & environment variables
  - [ ] Integrating with GitHub (webhooks)
  - [ ] Using agents/nodes & credentials binding

- [ ] **4.3 GitHub Actions**
  - [ ] Workflows & triggers (`push`, `pull_request`, `schedule`)
  - [ ] Jobs & steps
  - [ ] Reusable actions, secrets, environments
  - [ ] Deploying to AWS via Actions (OIDC or access keys)

- [ ] **4.4 AWS CodePipeline / CodeBuild / CodeDeploy**
  - [ ] End-to-end pipeline:
    - [ ] Source (GitHub/CodeCommit)
    - [ ] Build (CodeBuild)
    - [ ] Deploy (CodeDeploy/CloudFormation/ECS)
  - [ ] Hooks & approvals

---

## Phase 5 – Containers & ECS

- [ ] **5.1 Docker**
  - [ ] Images vs containers
  - [ ] Dockerfile basics: `FROM`, `RUN`, `COPY`, `CMD`, `EXPOSE`
  - [ ] Building & running containers
  - [ ] Volumes & networks (basic)
  - [ ] Multi-stage builds (optional but useful)

- [ ] **5.2 ECS (Fargate or EC2)**
  - [ ] Task definitions
  - [ ] Services & desired count
  - [ ] ECS + ALB integration
  - [ ] IAM roles for tasks
  - [ ] Sending logs to CloudWatch

---

## Phase 6 – Monitoring & Observability

- [ ] **CloudWatch**
  - [ ] Metrics & alarms (thresholds, anomaly detection basics)
  - [ ] Logs & log groups
  - [ ] Creating dashboards

- [ ] **Logging patterns**
  - [ ] Structured logs (JSON)
  - [ ] Correlation IDs

- [ ] **Prometheus basics**
  - [ ] Metrics model: counters, gauges, histograms
  - [ ] Basic PromQL queries

- [ ] **Grafana**
  - [ ] Adding data sources (CloudWatch, Prometheus)
  - [ ] Building dashboards & alerts

---

## Phase 7 – AWS Automation & Serverless

- [ ] **Lambda**
  - [ ] Writing functions in Python
  - [ ] Permissions (execution role, resource policies)
  - [ ] Environment variables, layers

- [ ] **EventBridge**
  - [ ] Rules, schedules, event patterns
  - [ ] Linking services (e.g., DynamoDB stream → Lambda → S3)

- [ ] **Boto3 deeper**
  - [ ] Paginators
  - [ ] Error handling & retries
  - [ ] Idempotency patterns

- [ ] **Example automations to build**
  - [ ] Script to create/update CloudWatch alarms for all EC2 instances
  - [ ] Script to rotate IAM access keys and notify via email
  - [ ] Daily export: DynamoDB table → S3 (full & incremental)
  - [ ] Lambda triggered by EventBridge cron schedule
  - [ ] Lambda triggered by DynamoDB streams
  - [ ] Lambda triggered by S3 put events (e.g., process uploaded files)

---

## Phase 8 – Reliability, On-Call & Ops Practices

- [ ] **Incident management basics**
  - [ ] Severity levels
  - [ ] MTTR, MTTD
  - [ ] Postmortems & action items

- [ ] **Troubleshooting AWS**
  - [ ] IAM access denied issues
  - [ ] Subnet routing & Security Group misconfigurations
  - [ ] Tagging gaps and cost/monitoring impact

- [ ] **Zero-downtime deployments (conceptually)**
  - [ ] Blue/green
  - [ ] Rolling
  - [ ] Canary (high-level)

---

## Phase 9 – Extra Items (Long-term / Parallel)

- [ ] **9.1 SQL & Backend Automation**
  - [ ] SQL basics: `SELECT`, `INSERT`, `UPDATE`, `DELETE`
  - [ ] Joins: inner, left, right
  - [ ] Filtering, aggregation, `GROUP BY`
  - [ ] Simple stored procedures/triggers

- [ ] **9.2 Java Basics**
  - [ ] Syntax basics
  - [ ] Classes, interfaces, inheritance
  - [ ] Collections API: `List`, `Map`, `Set`
  - [ ] Exceptions

- [ ] **9.3 Frontend (Node.js + React.js)**
  - [ ] Node.js basics (Express server)
  - [ ] React basics: components, props, state, hooks
  - [ ] Consuming APIs from frontend
