

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

## Processes, signals, and job control
- [ ] Process lifecycle, PID/PPID, zombie/defunct concept
- [ ] `ps`, `top/htop`, `pgrep`, `pkill`, `kill`
- [ ] Signals:
  - [ ] SIGTERM vs SIGKILL
  - [ ] SIGINT, SIGHUP
- [ ] Foreground/background jobs: `&`, `jobs`, `fg`, `bg`, `nohup`
- [ ] Priorities: `nice`, `renice` (concept + use)

## Systemd & logging
- [ ] `systemctl status/start/stop/restart/enable/disable`
- [ ] Unit file basics: `ExecStart`, `Environment`, `User`, `Restart`, `After/Wants`
- [ ] `journalctl`:
  - [ ] time filtering, unit filtering
  - [ ] follow logs, severity
- [ ] Log rotation concept (`logrotate`) 

## Filesystems & disk
- [ ] `df -h`, `du -sh`, inode exhaustion concept (`df -i`)
- [ ] Mounting: `mount`, `/etc/fstab` basics
- [ ] Disk performance terms: IOPS vs throughput vs latency
- [ ] File descriptors concept; “Too many open files” (`ulimit -n`) 
- [ ] RAID levels 
- [ ] LVM basics 

## Memory/CPU basics
- [ ] `free -m`, swap, paging
- [ ] Load average meaning vs CPU utilization
- [ ] OOM killer concept
- [ ] Context switching concept; thread vs process (high level)

## Linux networking tools
- [ ] `ip addr`, `ip route`, `ip link`
- [ ] `ss -tulpn` (ports) vs `netstat` legacy
- [ ] `lsof -i` (who listens on port)
- [ ] `dig`/`nslookup`, `curl -v`, `wget`
- [ ] `tcpdump` concept + basic usage 

## Security basics on Linux
- [ ] SSH keys, permissions on `~/.ssh`
- [ ] `sudo` basics, `visudo` concept
- [ ] Basic hardening: disable password auth, least privilege
- [ ] SELinux/AppArmor concept 



# Networking Fundamentals

## Core concepts 
- [ ] OSI and TCP/IP models (practical mapping)
- [ ] IPv4 addressing + CIDR subnetting (calculate quickly)
- [ ] Public vs private IP ranges
- [ ] Routing vs switching (concept)
- [ ] NAT (SNAT/DNAT) concept
- [ ] Ports, ephemeral ports

## TCP/UDP behavior 
- [ ] TCP 3-way handshake
- [ ] Retransmissions, timeouts
- [ ] TIME_WAIT meaning
- [ ] UDP use cases (DNS, streaming)
- [ ] Common failure patterns:
  - [ ] “Connection refused” vs “timeout” vs “DNS failure”
  - [ ] “TLS handshake failure” basics

## DNS 
- [ ] Records: A/AAAA/CNAME/TXT/MX
- [ ] Recursive vs authoritative
- [ ] TTL caching behavior
- [ ] Split-horizon (private vs public) concept

## HTTP/HTTPS 
- [ ] Methods, idempotency (GET vs POST vs PUT)
- [ ] Status codes (200/201/301/302/400/401/403/404/409/429/500/502/503/504)
- [ ] Headers (Host, Authorization, Content-Type, User-Agent)
- [ ] Keep-alive, connection pooling (concept)

## TLS 
- [ ] Certificate chain (root/intermediate/leaf)
- [ ] SAN vs CN
- [ ] SNI
- [ ] Termination at LB vs end-to-end
- [ ] mTLS concept 

## Load balancing patterns 
- [ ] Layer 4 vs Layer 7
- [ ] Health checks
- [ ] Sticky sessions concept
- [ ] Reverse proxy concept



# AWS Deep Dive

## IAM 
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

## VPC fundamentals 
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

## EC2 + EBS 
- [ ] Instance lifecycle + AMIs
- [ ] User-data bootstrapping
- [ ] IMDSv2 concept
- [ ] EBS types (gp3/io1 etc) high-level tradeoffs
- [ ] Snapshots, encryption basics
- [ ] Auto Scaling Groups basics 
- [ ] Placement groups/capacity reservations 

## ALB/NLB 
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

## S3 
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

## DynamoDB 
- [ ] Partition key/sort key
- [ ] Query vs scan
- [ ] On-demand vs provisioned
- [ ] RCU/WCU meaning
- [ ] Hot partitions + mitigation strategies
- [ ] GSI vs LSI
- [ ] TTL
- [ ] Streams (trigger ETL)
- [ ] Conditional writes, transactions concept 

## Lambda 
- [ ] Invocation models (sync/async), event sources
- [ ] Retries, error handling, DLQ/destinations concept
- [ ] Timeouts, memory, CPU allocation
- [ ] Concurrency (reserved/provisioned)
- [ ] Idempotency strategies for at-least-once events
- [ ] Cold start concept
- [ ] Packaging/dependencies basics 

## EventBridge 
- [ ] Event bus, rules, patterns
- [ ] Scheduled rules (cron)
- [ ] Retries + DLQ concept
- [ ] Event-driven design basics

## CloudWatch 
- [ ] Metrics: namespaces, dimensions
- [ ] Alarm types: threshold, composite 
- [ ] Logs: log groups/streams, retention, subscription concept 
- [ ] Logs Insights query thinking
- [ ] Dashboards

## Route 53 (MUST/SHOULD)
- [ ] Hosted zones (public/private)
- [ ] Records and routing policies
- [ ] Health checks + failover routing 
- [ ] Weighted/latency/geolocation 

## CloudFormation basics 
- [ ] Template structure, parameters, outputs
- [ ] Change sets
- [ ] Stack updates, rollbacks
- [ ] Nested stacks concept 

## Common AWS “supporting” services 
- [ ] CloudTrail (audit)
- [ ] AWS Config (compliance/drift)
- [ ] KMS fundamentals
- [ ] SSM Session Manager concept
- [ ] ECR basics (for containers)
- [ ] Secrets Manager vs Parameter Store 

# Infrastructure as Code (Terraform + CloudFormation)

## IaC principles 
- [ ] Declarative configs
- [ ] Idempotency
- [ ] Drift detection & reduction
- [ ] Environment separation (dev/stage/prod)
- [ ] Tagging standards (owner, cost-center, env)

## Terraform deep dive 
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

## CloudFormation deep dive 
- [ ] Intrinsics concepts (Ref, GetAtt)
- [ ] Conditions
- [ ] Change sets + approvals
- [ ] Rollback behavior and debugging failed updates

## IaC in CI 
- [ ] Linting/format checks
- [ ] Policy-as-code concept (OPA/Sentinel)
- [ ] Plan review + mandatory approvals



# CI/CD + Release Engineering

## CI/CD foundations 
- [ ] Build/test/package/deploy stages
- [ ] Artifact immutability + versioning
- [ ] Promotion: dev → stage → prod
- [ ] Rollback plans and safety
- [ ] GitOps concept 

## Jenkins 
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

## GitHub Actions 
- [ ] Workflows/jobs/steps
- [ ] Runners: hosted vs self-hosted
- [ ] Secrets/environments/approvals
- [ ] Artifacts + caching
- [ ] Matrix builds 
- [ ] Workflow triggers: push, PR, schedule, manual

## Deployment strategies 
- [ ] Rolling
- [ ] Blue/Green
- [ ] Canary
- [ ] Feature flags concept
- [ ] Zero-downtime principles

## Testing types (MUST/SHOULD)
- [ ] Unit tests
- [ ] Integration tests
- [ ] End-to-end tests
- [ ] Smoke tests
- [ ] Contract tests concept 

## Supply chain & build security 
- [ ] Dependency pinning, SBOM concept
- [ ] Signing artifacts concept 
- [ ] Secrets scanning concept



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



# 8) Observability (CloudWatch / Prometheus / Grafana)

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



# 9) Security (Cloud + DevOps)

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



# 10) Python + Boto3 Automation

## 10.1 Python fundamentals 
- [ ] Data structures + when to use each
- [ ] Exceptions and error handling
- [ ] File IO, JSON/YAML parsing concept
- [ ] Logging best practices
- [ ] Basic OOP concepts (only as needed)

## 10.2 Production-quality automation patterns 
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

## 10.3 Boto3 deep basics 
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



# 11) Incident Management & Troubleshooting

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



# 12) System Design (DevOps/SRE flavored)

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



# 13) Data, Messaging, and ETL Pipelines

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



# 14) Git + SDLC + Engineering Practices

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



# 15) Coding + DSA for DevOps

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



# 16) Behavioral / Leadership (incl. Amazon-style)

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



# 17) Hands-on Labs Checklist
> Do these and you will *actually* be interview-ready.

## 17.1 AWS + Networking labs 
- [ ] Build VPC with public/private subnets, IGW, NAT
- [ ] Prove internet access from public, not from private (until NAT added)
- [ ] Add VPC endpoint for S3 and validate private S3 access
- [ ] ALB + target group + health checks with simple app

## 17.2 IaC labs 
- [ ] Terraform remote state in S3 + DynamoDB lock
- [ ] Write a reusable module (VPC or IAM role)
- [ ] Import an existing AWS resource into Terraform state
- [ ] Use CloudFormation change set and explain what will change

## 17.3 CI/CD labs 
- [ ] Jenkins pipeline: lint → test → package → deploy
- [ ] GitHub Actions equivalent workflow
- [ ] Add approval gate for production deploy
- [ ] Add artifact upload/download and caching

## 17.4 Observability labs 
- [ ] Create CloudWatch dashboards + alarms for:
  - [ ] latency (p95)
  - [ ] error rate
  - [ ] saturation signal
- [ ] Write a Logs Insights query to find top errors
- [ ] Grafana dashboard basics (if available)

## 17.5 Automation labs 
- [ ] Python Boto3 script with:
  - [ ] pagination
  - [ ] retries/backoff
  - [ ] structured logs
  - [ ] safe idempotent operations



# 18) Mock Interview Question Bank

## 18.1 AWS/IAM/VPC questions 
- [ ] Walk through IAM policy evaluation with an example (allow + explicit deny)
- [ ] EC2 in private subnet can’t reach internet — debug steps
- [ ] ALB shows unhealthy targets — most common causes?
- [ ] S3 AccessDenied — where do you check and in what order?
- [ ] DynamoDB hot partition — what is it and how to fix?
- [ ] Lambda duplicates events — why and how to handle?

## 18.2 Terraform/IaC questions 
- [ ] What is Terraform state? why remote state?
- [ ] Drift: how do you detect and prevent?
- [ ] Module design: how do you structure reusable modules?
- [ ] `ignore_changes`: when is it safe? when dangerous?

## 18.3 CI/CD questions 
- [ ] Design CI/CD for microservices
- [ ] Handling flaky tests
- [ ] Rollback strategy for production deploy

## 18.4 Observability/incident questions 
- [ ] Design alerts that don’t spam on-call
- [ ] Walk through an incident: detection → mitigation → postmortem
- [ ] Difference between p95 and average; why p95 matters

## 18.5 Coding/scripting questions 
- [ ] Parse a log file and compute error rate per endpoint
- [ ] Implement exponential backoff retry wrapper
- [ ] Merge two config dicts with precedence rules



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
