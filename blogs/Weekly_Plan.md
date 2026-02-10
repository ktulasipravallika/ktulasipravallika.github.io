
## Week 1 — Linux + Bash “Ops Core”

**Goal:** be comfortable debugging common Linux failures.

1. Shell & navigation: pipes/redirection, quoting, env vars, exit codes
2. Files & permissions: chmod/chown, groups, umask, links
3. Processes: ps/top, signals, systemd basics
4. Logs: journalctl, grep/awk/sed, tail, find
5. Networking basics: ip/ss/curl/dig basics

* Mini-lab: run a simple web server as a systemd service; break/fix it.
* Write a short runbook: “service down” checklist.

**Deliverables**

* Repo: `linux-ops-labs`

  * `runbooks/service-down.md`
  * `labs/systemd-web-service.md`
  * `labs/log-triage.md`

---

## Week 2 — Networking for Cloud + Troubleshooting

**Goal:** explain + debug traffic flow.
* CIDR/subnetting drills (15 min daily)
* DNS: records, caching, dig exercises
* HTTP basics: headers, status codes
* TLS basics: cert chain concept
* Tools: curl -v, traceroute/mtr (concept), tcpdump (basic)

* Lab: simulate “DNS broken / port blocked / app down” locally with notes.

**Deliverables**

* Add to `linux-ops-labs/runbooks/`

  * `dns-debug.md`, `http-debug.md`, `network-debug.md`

---

## Week 3 — Git/GitHub + Python Automation Foundations

**Goal:** start writing automation scripts and using real repo hygiene.
* Git: branching, PRs, rebase vs merge, tags
* Python: venv, logging, requests, JSON/YAML
* CLI tool: argparse
* Add pytest basics

* Build script #1: “log analyzer” (parse log file, output summary JSON)
* Build script #2: “health check” (HTTP checks with retries + timeout)

**Deliverables**

* Repo: `python-devops-tools`

  * `tools/log_analyzer.py`
  * `tools/http_healthcheck.py`
  * `tests/`
  * `README.md` with usage examples

---

## Week 4 — AWS Core (IAM + VPC + EC2) + First Terraform

**Goal:** deploy a VM in a correct VPC using IaC.
* IAM: users vs roles, policies, least privilege patterns
* VPC: public/private subnets, route tables, IGW, NAT
* EC2: user-data bootstrap, SGs, key auth
* Terraform basics: providers/resources/vars/outputs

* Terraform: create VPC + subnets + EC2 (public) + SG
* SSH in, install nginx via user-data

**Deliverables**

* Repo: `terraform-aws-foundations`

  * `modules/vpc/`
  * `environments/dev/`
  * `README.md` with diagram + deploy steps

---

## Week 5 — Terraform Job-Ready (State, Modules, Environments)

**Goal:** Terraform like a real team.
* Remote state: S3 backend + DynamoDB lock
* Modules: inputs/outputs, naming conventions
* Environments: dev/stage/prod layout
* tf linting + formatting (`fmt`, `validate`, tflint basic)

* Convert Week 4 into proper modules + remote state
* Add tags everywhere

**Deliverables**

* Update `terraform-aws-foundations`

  * `backend/` docs
  * `modules/`
  * `runbooks/terraform-workflow.md`

---

## Week 6 — AWS Storage + Observability (CloudWatch)

**Goal:** logs/metrics/alarms in place.
* S3: versioning, encryption, lifecycle basics
* EBS concepts (snapshots)
* CloudWatch logs vs metrics
* Alarms + dashboards
* CloudTrail concept (awareness)

* Add CloudWatch agent (or at least basic metrics)
* Create alarm for CPU high; document response steps

**Deliverables**

* In `terraform-aws-foundations`:

  * `monitoring/` (alarms + dashboard Terraform or documented steps)
  * `runbooks/high-cpu.md`

---

## Week 7 — Docker + Compose (Local “Mini-Prod”)

**Goal:** containerize and run an app + dependencies locally.
* Images vs containers, layers
* Dockerfile best practices, multi-stage basics
* Compose: networks, env vars, volumes
* Logs + debugging

* Build a simple app stack: `app + db` (Compose)
* Add healthcheck + restart policies

**Deliverables**

* Repo: `docker-compose-microstack`

  * `Dockerfile`
  * `docker-compose.yml`
  * `runbooks/local-debug.md`

---

## Week 8 — CI/CD with GitHub Actions (Build/Test/Scan)

**Goal:** pipeline that looks like production.
* GitHub Actions: workflows, jobs, secrets
* Run tests + lint on PR
* Build container image
* Add security scan (dependency + container scan basic)

* Full pipeline: PR → test → build image → (optional push to registry)

**Deliverables**

* Add `.github/workflows/ci.yml` to:

  * `python-devops-tools` OR `docker-compose-microstack`
* README section: “CI/CD pipeline”

---

## Week 9 — Deploy to AWS (ECS or EC2) + CD

**Goal:** running service in AWS with CD (simple but real).

**Option A (fast + common): ECS Fargate**

* ALB → ECS service → container
* CloudWatch logs

**Option B: EC2 + systemd**

* GitHub Actions deploy via SSH (okay, but less modern)
* Learn ECS basics (task/service)
* ALB basics + health checks
* IAM roles for tasks

* Deploy your containerized app to AWS
* Add CD trigger on merge

**Deliverables**

* Repo: `aws-app-platform`

  * Terraform for ECS + ALB + logs
  * `runbooks/deploy.md`

---

## Week 10 — Kubernetes Basics (Minimum Job Depth)

**Goal:** deploy + debug in k8s.
* Pods/Deployments/Services
* ConfigMaps/Secrets
* Ingress concept
* Debugging: logs/describe/events/exec
* Requests/limits concept

* Use local k8s (kind/minikube) and deploy your app
* Break/fix: CrashLoopBackOff, bad config, wrong service port

**Deliverables**

* Repo: `k8s-app-basics`

  * `manifests/`
  * `runbooks/k8s-debug.md`

---

## Week 11 — SRE/Ops Readiness: Incidents, Runbooks, Postmortems

**Goal:** demonstrate you can operate systems.
* SLIs/SLOs basics, golden signals
* Alert design (page vs ticket)
* Postmortem format
* On-call hygiene & communication

* Create “Ops Simulator”

  * CPU spike → alarm → mitigation
  * Service crash → restart/rollback
* Write 1 postmortem

**Deliverables**

* Repo: `ops-sre-simulator`

  * `incidents/incident-001.md`
  * `runbooks/`
  * `monitoring/`

---

## Week 12 — Interview + Resume + Applications (Job Conversion Week)

**Goal:** convert skills into offers.
* 30 min: Linux/networking troubleshooting drills
* 30 min: Terraform + AWS review (explain your architecture)
* 30–60 min: 1 mock interview question + improve answer
* 30 min: apply + tailor resume to 3–5 jobs/day

* Final polish: READMEs, diagrams, pinned repos, LinkedIn update

**Deliverables**

* Resume updated (DevOps-focused)
* GitHub profile: 3 pinned repos + clean descriptions
* “Portfolio landing” README in a `portfolio` repo

---
