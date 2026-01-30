# Linux & OS Fundamentals

## Shell & CLI essentials
- [ ] Shell basics: `bash`/`zsh`, quoting, escaping, globbing
- [ ] Environment variables: `export`, PATH, subshells
- [ ] Redirection: `>`, `>>`, `<`, `2>`, `2>&1`, pipes `|`
- [ ] Text processing:
  - [ ] `grep` (regex basics), `egrep`, `ripgrep` concept
  - [ ] `awk` (fields, simple aggregates)
  - [ ] `sed` (substitution, delete lines)
  - [ ] `cut`, `sort`, `uniq`, `tr`, `paste`
- [ ] File ops: `cp`, `mv`, `rm`, `ln -s`, `stat`
- [ ] Find: `find` + `xargs` + safe quoting
- [ ] Archives: `tar`, `gzip`, `xz`, `zip`
- [ ] Permissions:
  - [ ] `chmod` symbolic vs octal (644/755)
  - [ ] `chown`, `chgrp`, groups
  - [ ] `umask`
  - [ ] SUID/SGID/sticky bit

## 2.2 Processes, signals, and job control
- [ ] Process lifecycle, PID/PPID, zombie/defunct concept
- [ ] `ps`, `top/htop`, `pgrep`, `pkill`, `kill`
- [ ] Signals:
  - [ ] SIGTERM vs SIGKILL
  - [ ] SIGINT, SIGHUP
- [ ] Foreground/background jobs: `&`, `jobs`, `fg`, `bg`, `nohup`
- [ ] Priorities: `nice`, `renice` (concept + use)

## 2.3 Systemd & logging
- [ ] `systemctl status/start/stop/restart/enable/disable`
- [ ] Unit file basics: `ExecStart`, `Environment`, `User`, `Restart`, `After/Wants`
- [ ] `journalctl`:
  - [ ] time filtering, unit filtering
  - [ ] follow logs, severity
- [ ] Log rotation concept (`logrotate`)

## 2.4 Filesystems & disk
- [ ] `df -h`, `du -sh`, inode exhaustion concept (`df -i`)
- [ ] Mounting: `mount`, `/etc/fstab` basics
- [ ] Disk performance terms: IOPS vs throughput vs latency
- [ ] File descriptors concept; “Too many open files” (`ulimit -n`)
- [ ] RAID levels
- [ ] LVM basics

## 2.5 Memory/CPU basics
- [ ] `free -m`, swap, paging
- [ ] Load average meaning vs CPU utilization
- [ ] OOM killer concept
- [ ] Context switching concept; thread vs process (high level)

## 2.6 Linux networking tools
- [ ] `ip addr`, `ip route`, `ip link`
- [ ] `ss -tulpn` (ports) vs `netstat` legacy
- [ ] `lsof -i` (who listens on port)
- [ ] `dig`/`nslookup`, `curl -v`, `wget`
- [ ] `tcpdump` concept + basic usage

## 2.7 Security basics on Linux
- [ ] SSH keys, permissions on `~/.ssh`
- [ ] `sudo` basics, `visudo` concept
- [ ] Basic hardening: disable password auth, least privilege
- [ ] SELinux/AppArmor concept

---

# 3) Networking Fundamentals

## 3.1 Core concepts
- [ ] OSI and TCP/IP models (practical mapping)
- [ ] IPv4 addressing + CIDR subnetting (calculate quickly)
- [ ] Public vs private IP ranges
- [ ] Routing vs switching (concept)
- [ ] NAT (SNAT/DNAT) concept
- [ ] Ports, ephemeral ports

## 3.2 TCP/UDP behavior
- [ ] TCP 3-way handshake
- [ ] Retransmissions, timeouts
- [ ] TIME_WAIT meaning
- [ ] UDP use cases (DNS, streaming)
- [ ] Common failure patterns:
  - [ ] “Connection refused” vs “timeout” vs “DNS failure”
  - [ ] “TLS handshake failure” basics

## 3.3 DNS
- [ ] Records: A/AAAA/CNAME/TXT/MX
- [ ] Recursive vs authoritative
- [ ] TTL caching behavior
- [ ] Split-horizon (private vs public) concept

## 3.4 HTTP/HTTPS
- [ ] Methods, idempotency (GET vs POST vs PUT)
- [ ] Status codes (200/201/301/302/400/401/403/404/409/429/500/502/503/504)
- [ ] Headers (Host, Authorization, Content-Type, User-Agent)
- [ ] Keep-alive, connection pooling (concept)

## 3.5 TLS
- [ ] Certificate chain (root/intermediate/leaf)
- [ ] SAN vs CN
- [ ] SNI
- [ ] Termination at LB vs end-to-end
- [ ] mTLS concept

## 3.6 Load balancing patterns
- [ ] Layer 4 vs Layer 7
- [ ] Health checks
- [ ] Sticky sessions concept
- [ ] Reverse proxy concept

---

# 4) AWS Deep Dive

## 4.1 IAM
- [ ] Users/Groups/Roles
- [ ] Identity vs Resource policies
- [ ] Managed vs inline policies
- [ ] Policy evaluation logic:
  - [ ] Explicit deny overrides allow
  - [ ] Default deny
- [ ] STS AssumeRole flow + role chaining concept
- [ ] Trust policy vs permission policy
- [ ] Conditions and common keys:
  - [ ] `aws:SourceIp`, `aws:PrincipalArn`, `aws:RequestedRegion`, MFA condition
- [ ] Debug AccessDenied:
  - [ ] wrong principal/role
  - [ ] missing trust
  - [ ] missing permission
  - [ ] resource policy deny (S3)
  - [ ] KMS key policy deny
  - [ ] SCP/permission boundary
- [ ] IAM best practices:
  - [ ] least privilege
  - [ ] avoid long-lived keys
  - [ ] role-based access
- [ ] IAM Identity Center (SSO) concept

## 4.2 VPC fundamentals
- [ ] VPC, subnets (public/private defined by routes)
- [ ] Route tables, longest prefix match concept
- [ ] IGW vs NAT Gateway (when/why)
- [ ] Security Groups (stateful) vs NACLs (stateless)
- [ ] VPC DNS resolution + DHCP options
- [ ] VPC Flow Logs (what included/excluded)
- [ ] VPC endpoints:
  - [ ] Gateway endpoints (S3/DynamoDB)
  - [ ] Interface endpoints (PrivateLink)
- [ ] Peering vs Transit Gateway
- [ ] IPv6 basics in VPC

## 4.3 EC2 + EBS
- [ ] Instance lifecycle + AMIs
- [ ] User-data bootstrapping
- [ ] IMDSv2 concept
- [ ] EBS types (gp3/io1 etc) high-level tradeoffs
- [ ] Snapshots, encryption basics
- [ ] Auto Scaling Groups basics
- [ ] Placement groups/capacity reservations

## 4.4 ALB/NLB
- [ ] ALB:
  - [ ] listeners/rules
  - [ ] target groups
  - [ ] health checks
  - [ ] path/host-based routing
  - [ ] TLS termination
- [ ] NLB:
  - [ ] L4 pass-through, static IP use cases
- [ ] Debug unhealthy targets:
  - [ ] wrong port/path
  - [ ] SG/NACL/routing
  - [ ] app not listening
  - [ ] wrong health check matcher

## 4.5 S3
- [ ] Bucket vs object
- [ ] Bucket policy vs ACLs (why ACLs avoided)
- [ ] Public access block settings
- [ ] Versioning + lifecycle policies
- [ ] Encryption:
  - [ ] SSE-S3 vs SSE-KMS
- [ ] Pre-signed URLs concept
- [ ] Event notifications (S3 → Lambda/EventBridge/SQS)
- [ ] Replication basics
- [ ] Storage classes

## 4.6 DynamoDB
- [ ] Partition key/sort key
- [ ] Query vs scan
- [ ] On-demand vs provisioned
- [ ] RCU/WCU meaning
- [ ] Hot partitions + mitigation strategies
- [ ] GSI vs LSI
- [ ] TTL
- [ ] Streams (trigger ETL)
- [ ] Conditional writes, transactions concept

## 4.7 Lambda
- [ ] Invocation models (sync/async), event sources
- [ ] Retries, error handling, DLQ/destinations concept
- [ ] Timeouts, memory, CPU allocation
- [ ] Concurrency (reserved/provisioned)
- [ ] Idempotency strategies for at-least-once events
- [ ] Cold start concept
- [ ] Packaging/dependencies basics

## 4.8 EventBridge
- [ ] Event bus, rules, patterns
- [ ] Scheduled rules (cron)
- [ ] Retries + DLQ concept
- [ ] Event-driven design basics

## 4.9 CloudWatch
- [ ] Metrics: namespaces, dimensions
- [ ] Alarm types: threshold, composite
- [ ] Logs: log groups/streams, retention, subscription concept
- [ ] Logs Insights query thinking
- [ ] Dashboards

## 4.10 Route 53 (MUST/SHOULD)
- [ ] Hosted zones (public/private)
- [ ] Records and routing policies
- [ ] Health checks + failover routing
- [ ] Weighted/latency/geolocation

## 4.11 CloudFormation basics
- [ ] Template structure, parameters, outputs
- [ ] Change sets
- [ ] Stack updates, rollbacks
- [ ] Nested stacks concept

## 4.12 Common AWS “supporting” services
- [ ] CloudTrail (audit)
- [ ] AWS Config (compliance/drift)
- [ ] KMS fundamentals
- [ ] SSM Session Manager concept
- [ ] ECR basics (for containers)
- [ ] Secrets Manager vs Parameter Store

---

# 5) Infrastructure as Code (Terraform + CloudFormation)

## 5.1 IaC principles
- [ ] Declarative configs
- [ ] Idempotency
- [ ] Drift detection & reduction
- [ ] Environment separation (dev/stage/prod)
- [ ] Tagging standards (owner, cost-center, env)

## 5.2 Terraform deep dive
- [ ] Provider configuration and version pinning
- [ ] Resources vs data sources
- [ ] Variables/outputs/locals
- [ ] Module design:
  - [ ] module inputs/outputs
  - [ ] versioning strategy
  - [ ] reusable patterns
- [ ] State management:
  - [ ] remote state (S3)
  - [ ] state locking (DynamoDB)
  - [ ] drift detection
  - [ ] import existing resources
  - [ ] state mv/rm safety
- [ ] Dependency graph, `depends_on`
- [ ] Lifecycle meta-args: `prevent_destroy`, `ignore_changes`
- [ ] Workspaces vs separate states
- [ ] Secrets handling patterns (don’t leak into state)
- [ ] Common errors:
  - [ ] provider auth failures
  - [ ] dependency cycles
  - [ ] state lock stuck
  - [ ] drift causing unexpected plan

## 5.3 CloudFormation deep dive
- [ ] Intrinsics concepts (Ref, GetAtt)
- [ ] Conditions
- [ ] Change sets + approvals
- [ ] Rollback behavior and debugging failed updates

## 5.4 IaC in CI
- [ ] Linting/format checks
- [ ] Policy-as-code concept (OPA/Sentinel)
- [ ] Plan review + mandatory approvals

---

# 6) CI/CD + Release Engineering

## 6.1 CI/CD foundations
- [ ] Build/test/package/deploy stages
- [ ] Artifact immutability + versioning
- [ ] Promotion: dev → stage → prod
- [ ] Rollback plans and safety
- [ ] GitOps concept

## 6.2 Jenkins
- [ ] Declarative vs scripted pipeline concept
- [ ] Agents/nodes/executors
- [ ] Credentials management (secret hygiene)
- [ ] Webhooks/triggers
- [ ] Shared libraries concept
- [ ] Debugging pipeline failures:
  - [ ] workspace issues
  - [ ] missing credentials
  - [ ] agent offline
  - [ ] flaky tests

## 6.3 GitHub Actions
- [ ] Workflows/jobs/steps
- [ ] Runners: hosted vs self-hosted
- [ ] Secrets/environments/approvals
- [ ] Artifacts + caching
- [ ] Matrix builds
- [ ] Workflow triggers: push, PR, schedule, manual

## 6.4 Deployment strategies
- [ ] Rolling
- [ ] Blue/Green
- [ ] Canary
- [ ] Feature flags concept
- [ ] Zero-downtime principles

## 6.5 Testing types (MUST/SHOULD)
- [ ] Unit tests
- [ ] Integration tests
- [ ] End-to-end tests
- [ ] Smoke tests
- [ ] Contract tests concept

## 6.6 Supply chain & build security
- [ ] Dependency pinning, SBOM concept
- [ ] Signing artifacts concept
- [ ] Secrets scanning concept

---

# 7) Containers + ECS

## 7.1 Docker fundamentals
- [ ] Image vs container
- [ ] Layers, caching, build context
- [ ] Dockerfile:
  - [ ] FROM/RUN/COPY/ADD/WORKDIR/ENV
  - [ ] CMD vs ENTRYPOINT
  - [ ] multi-stage builds
- [ ] Networking:
  - [ ] bridge, host (concept)
  - [ ] port mapping
- [ ] Storage:
  - [ ] volumes vs bind mounts
- [ ] Resource limits: CPU/memory
- [ ] Debugging containers:
  - [ ] logs, exec into container
  - [ ] env vars, ports, DNS resolution

## 7.2 ECS fundamentals
- [ ] Cluster, service, task definition
- [ ] Fargate vs EC2 launch type tradeoffs
- [ ] IAM task role vs execution role
- [ ] ALB integration: target groups/health checks
- [ ] Deployments: rolling update behavior
- [ ] CloudWatch logs integration
- [ ] Auto scaling basics

## 7.3 Container best practices
- [ ] least privilege (non-root)
- [ ] minimal images
- [ ] image scanning concept
- [ ] secrets injection pattern

---


---

# 8) Kubernetes (Core + EKS-ready)
> Kubernetes isn’t on your resume, but **many DevOps/SRE roles expect it anyway**. This section is an **interview-complete** K8s prep map.  
> If you can handle this section + your AWS/IaC skills, you can crack a much wider set of roles.

## 8.1 Kubernetes fundamentals
- [ ] What Kubernetes is (control plane + worker nodes) and what it solves
- [ ] Declarative desired state vs imperative commands
- [ ] Core objects vocabulary:
  - [ ] Cluster, Node, Pod, Container
  - [ ] Deployment, ReplicaSet
  - [ ] Service (ClusterIP/NodePort/LoadBalancer)
  - [ ] Namespace, Labels, Selectors, Annotations
- [ ] The reconciliation loop concept (controllers continuously converge state)
- [ ] `kubectl` basics:
  - [ ] `get`, `describe`, `logs`, `exec`, `apply`, `delete`
  - [ ] output formats: `-o yaml/json`, `-o wide`
  - [ ] contexts and kubeconfig

## 8.2 Control plane architecture
- [ ] API Server: authentication/authorization/admission
- [ ] etcd: what it stores, why it’s critical
- [ ] Scheduler: how pods get assigned (high-level)
- [ ] Controller Manager: controllers (Deployment, Node, etc.)
- [ ] Cloud Controller Manager (cloud integrations)
- [ ] Node components:
  - [ ] kubelet
  - [ ] container runtime (containerd)
  - [ ] kube-proxy (concept)

## 8.3 Workloads
- [ ] Pod lifecycle:
  - [ ] init containers
  - [ ] restart policy
  - [ ] probes (see below)
- [ ] Deployments:
  - [ ] rolling updates, rollback, revision history
  - [ ] maxUnavailable/maxSurge
- [ ] StatefulSets:
  - [ ] stable network identity, ordered rollout
  - [ ] PVC per replica
- [ ] DaemonSets:
  - [ ] one pod per node use cases (logging/monitoring agents)
- [ ] Jobs and CronJobs:
  - [ ] completions, parallelism, backoffLimit
  - [ ] Cron schedule, missed schedules concept
- [ ] Horizontal Pod Autoscaler (HPA)
- [ ] Vertical Pod Autoscaler (VPA) concept
- [ ] Cluster Autoscaler concept (SHOULD, especially for EKS)

## 8.4 Configuration and secrets
- [ ] ConfigMaps:
  - [ ] env var injection
  - [ ] mounted files
- [ ] Secrets:
  - [ ] env vars vs volume mounts
  - [ ] risks of env vars (process listing, logs)
- [ ] Best practices:
  - [ ] External Secrets / CSI driver concepts
  - [ ] rotation strategy concept
- [ ] Downward API concept

## 8.5 Health checks, reliability, and rollouts
- [ ] Probes:
  - [ ] livenessProbe
  - [ ] readinessProbe
  - [ ] startupProbe
- [ ] What happens when readiness fails (traffic stops) vs liveness fails (restarts)
- [ ] Resource management:
  - [ ] requests vs limits (CPU/memory)
  - [ ] QoS classes: Guaranteed/Burstable/BestEffort
  - [ ] OOMKilled scenarios
- [ ] Disruption control:
  - [ ] PodDisruptionBudget (PDB)
  - [ ] node drain behavior

## 8.6 Networking
- [ ] Pod-to-Pod networking model (every pod gets an IP)
- [ ] Services:
  - [ ] ClusterIP (internal)
  - [ ] NodePort (node-level port)
  - [ ] LoadBalancer (cloud LB)
- [ ] Ingress:
  - [ ] Ingress resource vs Ingress Controller (what is required)
  - [ ] path/host routing
  - [ ] TLS termination at ingress
- [ ] DNS in K8s:
  - [ ] CoreDNS concept
  - [ ] service discovery: `<svc>.<ns>.svc.cluster.local`
- [ ] NetworkPolicies:
  - [ ] allow/deny model, namespace selectors, pod selectors

## 8.7 Storage
- [ ] Volumes vs Persistent Volumes
- [ ] PV/PVC/StorageClass
- [ ] Access modes: RWO/ROX/RWX (high-level)
- [ ] StatefulSets + PVC patterns
- [ ] Dynamic provisioning concept
- [ ] CSI drivers concept

## 8.8 Security (MUST/SHOULD)
- [ ] RBAC:
  - [ ] Role/ClusterRole, RoleBinding/ClusterRoleBinding
  - [ ] ServiceAccounts
- [ ] Authentication vs Authorization vs Admission (concept)
- [ ] Pod security:
  - [ ] runAsNonRoot, capabilities, readOnlyRootFilesystem
  - [ ] Pod Security Standards (baseline/restricted) concept
- [ ] Image security:
  - [ ] scanning concept
  - [ ] signed images concept
- [ ] Secrets hygiene in clusters

## 8.9 Packaging and environments (MUST/SHOULD)
- [ ] YAML basics: indentation, lists/maps, anchors concept
- [ ] Helm:
  - [ ] chart structure, values.yaml
  - [ ] templates and overrides
  - [ ] helm install/upgrade/rollback
- [ ] Kustomize concept:
  - [ ] overlays per env
- [ ] GitOps concept:
  - [ ] Argo CD / Flux concept
  - [ ] desired state in git

## 8.10 Observability in Kubernetes
- [ ] `kubectl logs` vs cluster-level logging
- [ ] Metrics:
  - [ ] metrics-server concept
  - [ ] Prometheus scraping model
- [ ] Tracing concept (OpenTelemetry)
- [ ] Common dashboards and SLO signals at service level

## 8.11 Kubernetes troubleshooting
You must be able to debug these quickly:
- [ ] Pod stuck `Pending`:
  - [ ] insufficient resources
  - [ ] taints/tolerations
  - [ ] node selectors/affinity
  - [ ] PVC not bound
- [ ] Pod `CrashLoopBackOff`:
  - [ ] bad command/env vars
  - [ ] app exits immediately
  - [ ] failed liveness probe causing restarts
- [ ] ImagePullBackOff:
  - [ ] wrong image tag
  - [ ] registry auth/secret missing
- [ ] Service not reachable:
  - [ ] selector mismatch (service points to no pods)
  - [ ] readiness failing
  - [ ] wrong targetPort/port
- [ ] Ingress not working:
  - [ ] controller not installed
  - [ ] wrong class annotation
  - [ ] TLS secret missing
- [ ] DNS issues:
  - [ ] CoreDNS down
  - [ ] wrong namespace/service name
- [ ] Networking blocked:
  - [ ] NetworkPolicy deny
- [ ] Node issues:
  - [ ] NotReady
  - [ ] disk pressure / memory pressure
- [ ] Handy commands to master:
  - [ ] `kubectl describe pod`
  - [ ] `kubectl get events --sort-by=.metadata.creationTimestamp`
  - [ ] `kubectl logs -p`
  - [ ] `kubectl exec -it`
  - [ ] `kubectl rollout status/history/undo`
  - [ ] `kubectl top pods/nodes`

## 8.12 EKS (AWS Kubernetes) essentials
- [ ] EKS architecture at high level:
  - [ ] managed control plane
  - [ ] worker nodes as managed node groups or Fargate profiles
- [ ] IAM integration:
  - [ ] IAM roles for service accounts (IRSA) concept
- [ ] Networking:
  - [ ] VPC CNI concept
  - [ ] security groups for pods concept
- [ ] Load balancing:
  - [ ] AWS Load Balancer Controller concept (ALB/NLB)
- [ ] Storage:
  - [ ] EBS CSI driver concept
- [ ] Upgrades:
  - [ ] version compatibility and node rolling upgrade concept


# 9) Observability (CloudWatch / Prometheus / Grafana)

## 8.1 Metrics
- [ ] Golden signals: latency/traffic/errors/saturation
- [ ] Percentiles p50/p95/p99 (why percentiles matter)
- [ ] Dimensions/labels + cardinality issues
- [ ] SLI vs SLO vs SLA

## 8.2 Logging
- [ ] Structured logging (JSON)
- [ ] Log levels
- [ ] Correlation/request IDs
- [ ] Retention policies
- [ ] Querying patterns (filter, group, aggregate)

## 8.3 Alerting
- [ ] Alert fatigue/noise reduction
- [ ] Actionable alerts only
- [ ] Severity levels (page vs ticket)
- [ ] Composite alarms
- [ ] Anomaly detection concept

## 8.4 Prometheus
- [ ] Scrape model; exporters concept
- [ ] Labels and cardinality
- [ ] PromQL basics:
  - [ ] `rate()`, `sum by()`, `avg_over_time()`
  - [ ] histogram concept, quantiles concept
- [ ] Alertmanager concept

## 8.5 Grafana
- [ ] Panels/dashboards
- [ ] Alert rules concept
- [ ] Data sources concept

## 8.6 Tracing
- [ ] Traces/spans basics
- [ ] Correlate logs + metrics + traces

---

# 10) Security (Cloud + DevOps)

## 9.1 Core security principles
- [ ] Least privilege
- [ ] Defense in depth concept
- [ ] Secure defaults
- [ ] Auditability (who did what when)

## 9.2 AWS security (MUST/SHOULD)
- [ ] IAM best practices
- [ ] S3 public access controls
- [ ] KMS basics:
  - [ ] key policy concept
  - [ ] encryption at rest vs in transit
- [ ] CloudTrail auditing
- [ ] AWS Config concept
- [ ] Organizations/SCP concept
- [ ] GuardDuty/WAF concept

## 9.3 TLS & certificates
- [ ] Certificate chain
- [ ] Rotation strategy concept
- [ ] Termination choices (ALB vs app)

## 9.4 Secrets management (MUST/SHOULD)
- [ ] Avoid secrets in code
- [ ] Secrets in CI: masked variables
- [ ] Parameter Store vs Secrets Manager concept

---

# Python + Boto3 Automation

## Python fundamentals
- [ ] Data structures + when to use each
- [ ] Exceptions and error handling
- [ ] File IO, JSON/YAML parsing concept
- [ ] Logging best practices
- [ ] Basic OOP concepts (only as needed)

## Production-quality automation patterns
- [ ] Idempotency (repeat safe)
- [ ] Retries with backoff + jitter (concept)
- [ ] Timeout handling
- [ ] Rate limiting and throttling handling
- [ ] Pagination
- [ ] Partial failures and rollback strategy
- [ ] Configuration patterns:
  - [ ] env vars
  - [ ] CLI args
  - [ ] config files
- [ ] Unit tests with mocks concept (pytest)

## Boto3 deep basics
- [ ] client vs resource
- [ ] paginators
- [ ] waiters
- [ ] error types and retry-worthy failures
- [ ] common service usage:
  - [ ] IAM
  - [ ] CloudWatch
  - [ ] DynamoDB
  - [ ] S3
  - [ ] Lambda
  - [ ] EventBridge

---

# 12) Incident Management & Troubleshooting

## 11.1 Reliability vocabulary
- [ ] SLI/SLO/SLA
- [ ] Error budgets concept
- [ ] MTTR/MTTD/MTBF
- [ ] Toil definition + reduction

## 11.2 Incident lifecycle
- [ ] Detect → triage → mitigate → resolve → postmortem
- [ ] Incident roles: commander, communications, investigators
- [ ] Safe rollback decision-making
- [ ] Postmortem quality:
  - [ ] timeline
  - [ ] root cause vs contributing factors
  - [ ] action items (prevent/detect/mitigate)

## 11.3 Troubleshooting playbooks
- [ ] Service down:
  - [ ] recent deploy?
  - [ ] health checks?
  - [ ] DNS?
  - [ ] LB target health?
  - [ ] app logs?
- [ ] High latency:
  - [ ] p95/p99 focus
  - [ ] downstream dependencies
  - [ ] saturation signals
- [ ] Error spikes:
  - [ ] 4xx vs 5xx
  - [ ] throttling (429)
  - [ ] retries amplifying load
- [ ] AWS permission failures:
  - [ ] role/trust/policy/resource policy/KMS
- [ ] VPC networking failures:
  - [ ] SG/NACL/routes/DNS/NAT/endpoint

---

# 13) System Design (DevOps/SRE flavored)

## 12.1 Core design thinking
- [ ] Define requirements (functional + non-functional)
- [ ] Scalability, availability, latency
- [ ] Failure modes and recovery
- [ ] Monitoring/alerting/runbooks
- [ ] Cost awareness and simplicity

## 12.2 Canonical AWS designs
- [ ] Highly available web service design
- [ ] Multi-region provisioning strategy (high level)
- [ ] CI/CD pipeline for multiple services
- [ ] Event-driven ETL pipeline (DynamoDB → S3)

## 12.3 Multi-account / multi-tenant models
- [ ] account boundaries and blast radius
- [ ] role assumption strategy
- [ ] centralized logging/audit patterns concept

---

# 14) Data, Messaging, and ETL Pipelines

## 13.1 Storage & database fundamentals
- [ ] Relational vs NoSQL tradeoffs
- [ ] Consistency, availability concepts
- [ ] Index basics, query patterns

## 13.2 DynamoDB → S3 ETL patterns
- [ ] Trigger options:
  - [ ] DynamoDB Streams → Lambda
  - [ ] EventBridge scheduled ETL
- [ ] Idempotency keys / dedup strategy
- [ ] Exactly-once vs at-least-once semantics (concept)
- [ ] Backfill and reprocessing strategy
- [ ] Data partitioning in S3 (prefix design)
- [ ] Error handling: retries + DLQ patterns

## 13.3 Messaging services
- [ ] SQS basics (polling, visibility timeout, DLQ)
- [ ] SNS basics (pub/sub) concept
- [ ] Fanout patterns (SNS → SQS)
- [ ] Ordering + FIFO queues (concept)
- [ ] Kinesis basics (streaming) concept
- [ ] Step Functions basics (workflow orchestration) concept

---

# 15) Git + SDLC + Engineering Practices

## 14.1 Git essentials
- [ ] clone, fetch, pull, push
- [ ] branches, merges, rebases (concept + when to use)
- [ ] resolving conflicts
- [ ] PR workflow, code review etiquette
- [ ] tags/releases
- [ ] revert vs reset

## 14.2 SDLC practices
- [ ] code reviews and standards
- [ ] testing pyramid
- [ ] release notes and changelogs
- [ ] semantic versioning concept
- [ ] documentation: runbooks/SOPs/README patterns

---

# 16) Coding + DSA for DevOps

## 15.1 Practical scripting problems
- [ ] Parse logs and compute error rates
- [ ] Compare two JSON configs and report diffs
- [ ] Implement retry/backoff wrapper
- [ ] Paginate AWS API results and aggregate

## 15.2 DSA minimum set
- [ ] Arrays/strings
- [ ] Hash maps/sets
- [ ] Sorting and searching
- [ ] Two pointers / sliding window
- [ ] Basic recursion
- [ ] BFS/DFS at concept level

## 15.3 Complexity
- [ ] explain time/space complexity for your solution

---

# 17) Behavioral / Leadership (incl. Amazon-style)

## 16.1 STAR framework
- [ ] Situation / Task / Action / Result
- [ ] quantify impact
- [ ] mention tradeoffs and lessons learned

## 16.2 Your must-have story bank
- [ ] A major incident you handled end-to-end
- [ ] Automation that removed toil (Python/Boto3)
- [ ] Terraform/IaC standardization story
- [ ] Handling a difficult stakeholder/cross-team dependency
- [ ] A failure/mistake and what you changed
- [ ] On-call prioritization story

## 16.3 Amazon-style leadership themes
- [ ] Ownership
- [ ] Dive Deep
- [ ] Bias for Action
- [ ] Customer Obsession
- [ ] Earn Trust
- [ ] Deliver Results

---

# 18) Hands-on Labs Checklist
> Do these and you will *actually* be interview-ready.

## 19.1 AWS + Networking labs
- [ ] Build VPC with public/private subnets, IGW, NAT
- [ ] Prove internet access from public, not from private (until NAT added)
- [ ] Add VPC endpoint for S3 and validate private S3 access
- [ ] ALB + target group + health checks with simple app

## 19.2 IaC labs
- [ ] Terraform remote state in S3 + DynamoDB lock
- [ ] Write a reusable module (VPC or IAM role)
- [ ] Import an existing AWS resource into Terraform state
- [ ] Use CloudFormation change set and explain what will change

## 19.3 CI/CD labs
- [ ] Jenkins pipeline: lint → test → package → deploy
- [ ] GitHub Actions equivalent workflow
- [ ] Add approval gate for production deploy
- [ ] Add artifact upload/download and caching

## 19.4 Observability labs
- [ ] Create CloudWatch dashboards + alarms for:
  - [ ] latency (p95)
  - [ ] error rate
  - [ ] saturation signal
- [ ] Write a Logs Insights query to find top errors
- [ ] Grafana dashboard basics (if available)

## 18.0 Kubernetes labs
- [ ] Install a local cluster (kind or minikube)
- [ ] Deploy an app with Deployment + Service + Ingress (if supported)
- [ ] Configure ConfigMap + Secret (mounted + env var)
- [ ] Add readiness/liveness probes
- [ ] Create HPA (if metrics-server available)
- [ ] Debug CrashLoopBackOff, Pending, ImagePullBackOff using events/describe/logs
- [ ] Rollout + rollback a Deployment

## 19.5 Automation labs
- [ ] Python Boto3 script with:
  - [ ] pagination
  - [ ] retries/backoff
  - [ ] structured logs
  - [ ] safe idempotent operations

---

# 19) Mock Interview Question Bank

## 19.0 Kubernetes questions (MUST/SHOULD)
- [ ] What is the difference between a Deployment and StatefulSet?
- [ ] Pod Pending — how do you debug it?
- [ ] CrashLoopBackOff — most common root causes and fixes?
- [ ] Service not routing traffic — what do you check first?
- [ ] Readiness vs liveness probes — explain with impact.
- [ ] How does Ingress work? What is an Ingress Controller?
- [ ] requests vs limits — explain outcomes and QoS.
- [ ] RBAC: Role vs ClusterRole; RoleBinding vs ClusterRoleBinding.
- [ ] (EKS) What is IRSA and why is it used?

## 19.1 AWS/IAM/VPC questions
- [ ] Walk through IAM policy evaluation with an example (allow + explicit deny)
- [ ] EC2 in private subnet can’t reach internet — debug steps
- [ ] ALB shows unhealthy targets — most common causes?
- [ ] S3 AccessDenied — where do you check and in what order?
- [ ] DynamoDB hot partition — what is it and how to fix?
- [ ] Lambda duplicates events — why and how to handle?

## 19.2 Terraform/IaC questions
- [ ] What is Terraform state? why remote state?
- [ ] Drift: how do you detect and prevent?
- [ ] Module design: how do you structure reusable modules?
- [ ] `ignore_changes`: when is it safe? when dangerous?

## 19.3 CI/CD questions
- [ ] Design CI/CD for microservices
- [ ] Handling flaky tests
- [ ] Rollback strategy for production deploy

## 19.4 Observability/incident questions
- [ ] Design alerts that don’t spam on-call
- [ ] Walk through an incident: detection → mitigation → postmortem
- [ ] Difference between p95 and average; why p95 matters

## 19.5 Coding/scripting questions
- [ ] Parse a log file and compute error rate per endpoint
- [ ] Implement exponential backoff retry wrapper
- [ ] Merge two config dicts with precedence rules

---

## Completion Tracker
- [ ] Linux complete
- [ ] Networking complete
- [ ] AWS core complete
- [ ] Terraform/CloudFormation complete
- [ ] CI/CD complete
- [ ] Containers/ECS complete
- [ ] Observability complete
- [ ] Security complete
- [ ] Python/Boto3 complete
- [ ] Incident playbooks complete
- [ ] System design complete
- [ ] Behavioral story bank complete
- [ ] Labs complete
