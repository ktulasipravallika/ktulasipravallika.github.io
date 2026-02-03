# **Linux**

# Track A — Linux Fundamentals

## A0. Setup + Terminal Survival
  
  * Getting a Linux environment (VM/cloud), terminal basics, editors
  * Help systems: `man`, `--help`, `info`
  * Shell prompt, environment, command history
  * `man`, `which`, `type`, `history`, `sudo`
---
## A1. Filesystem + Navigation + Text Viewing

* Paths, directories, globbing (`*`, `?`)
* Viewing files safely (big logs!)
* Pipes + redirection basics (the heart of DevOps)
* `pwd`, `ls -la`, `cd`, `cat`, `less`, `head`, `tail -f`
* `>`, `>>`, `2>`, `2>&1`, `|`, `tee`

## A2. Permissions + Ownership + Users/Groups

* Permission bits, octal notation, sticky bit, setuid/setgid
* Users/groups, `sudo`, least privilege
* Common permission debugging (“why can’t my app read this?”)
* `chmod`, `chown`, `chgrp`, `umask`, `id`, `groups`, `getent`

## A3. Processes + Signals + Job Control

* Process lifecycle, foreground/background, signals
* Finding what’s consuming CPU/memory
* Safe killing, graceful stop vs hard kill
* `ps`, `top`, `htop`, `pgrep`, `pkill`, `kill`, `nice`, `renice`, `nohup`

## A4. Disks + Filesystems + Storage Troubleshooting

* Partitions, mounts, inode vs disk-full
* Finding large files, log growth, cleanup safety
* Basic LVM/RAID awareness (interview level)
* `df -h`, `du -sh`, `lsblk`, `mount`, `find`, `lsof`

## A5. Packages + Repos + Software Installation

* Installing/upgrading packages safely
* Repo basics, version pinning, troubleshooting installs
* `apt`, `dpkg`, `yum/dnf` (conceptually), `snap` (awareness)

## A6. systemd + Services + Boot Basics

* Services, unit files, logs, start/stop/restart
* Why a service fails and how to fix it
* Boot targets and dependencies (interview + oncall)
* `systemctl`, `journalctl`, unit file structure

## A7. Scheduling + Automation Basics

* `cron`, `at`, timers (systemd timers intro)
* Writing safe scheduled jobs and logging them
* `crontab -e`, `/etc/cron.*`, `date`

## A8. Logging + Observability Basics

* Log locations, journald vs files
* Rotation basics, searching patterns
* Intro to metrics mindset (CPU/mem/disk/net)
* `journalctl`, `grep`, `awk`, `tail -f`, `logrotate` (awareness)

# Track B — Shell + Scripting 

## B1. Shell Essentials: Variables, Quoting, Exit Codes

* Correct quoting (most common interview trap)
* Exit codes, `set -euo pipefail`
* Command substitution, environment variables
* `echo`, `printf`, `$?`, `export`, quotes `' "`, `$(...)`

## B2. Conditionals + Loops + Functions

* `if`, `case`, `for/while`, functions, return codes
* Reading args, validations, usage messages
* `[ ]`, `[[ ]]`, `case`, `shift`, `$1..$@`

## B3. Text Processing Toolkit

* Grep/regex, sed edits, awk extraction
* Sorting/uniquing, CSV-ish parsing
* JSON with `jq` (DevOps essential)
* `grep`, `sed`, `awk`, `cut`, `sort`, `uniq`, `tr`, `xargs`, `jq`

## B4. Files + Archives + Transfers

* `tar`, gzip, checksum verification
* SSH + SCP/RSYNC basics
* Permissions + ownership across transfers
* `tar`, `gzip`, `sha256sum`, `ssh`, `scp`, `rsync`

## B5. “Production-grade Bash” patterns

* Logging, retries, timeouts, traps, cleanup
* Idempotency mindset, safe temp files
* Basic testing patterns for scripts
* `trap`, `mktemp`, `getopts` (or manual parsing), `timeout`

# Track C — Networking (from basics to deep troubleshooting)

## C1. Networking Fundamentals: IP, Subnets, Routing

* IP vs MAC, ARP, gateways, CIDR
* What subnetting means in cloud/VPC terms
* `ip addr`, `ip route`, `arp` (or `ip neigh`)

## C2. Ports, Sockets, Firewalls

* TCP vs UDP, 3-way handshake, ephemeral ports
* Listening vs established connections
* Firewall basics (interview level)
* `ss -lntp`, `ss -antp`, `lsof -i`
* `ufw` (Ubuntu), `iptables/nft` (awareness)

## C3. DNS (most common real-world failure)

* DNS resolution path, TTL, records, common failures
* Debugging from client and server side
* `dig`, `nslookup`, `resolvectl` (or `/etc/resolv.conf`)

## C4. HTTP/HTTPS + TLS Basics

* HTTP methods, status codes, headers
* TLS handshake basics, certificates, SNI
* Diagnosing 4xx/5xx vs network/TLS issues
* `curl -v`, `curl -I`, `openssl s_client` (interview level)

## C5. Packet Capture + Deep Debug (advanced but interview-winning)



* When to use tcpdump, reading captures
* Latency, retransmits, MTU issues (concepts)
* Traceroute pitfalls, asymmetric routing awareness



* `tcpdump`, `traceroute`, `mtr` (if available)



* You can produce evidence for network issues.

---

# Track D — Real On-call Scenarios (Interview Simulation)

## D1. Linux Triage Playbook

Scenarios like:

* Disk full, CPU pinned, memory leak symptoms
* Service crash loop, permission denied, cert expired



* You can follow a structured triage: observe → isolate → fix → prevent.

---

## D2. Network Incident Playbook

Scenarios like:

* “Can’t SSH”
* “DNS broken”
* “API latency spike”
* “Load balancer healthy but app down”



* You can separate layers: DNS → routing → firewall → service → app.

---

# Track E — Capstone Projects (proves you’re job-ready)

## E1. Log Analyzer CLI

* Bash tool that:

  * accepts a log file,
  * extracts errors by timeframe,
  * outputs summary + top offenders,
  * supports JSON output (via `jq`)

## E2. Service Health Checker

* Script that:

  * checks process/service health,
  * checks port connectivity,
  * checks DNS resolution,
  * prints a single “PASS/FAIL + reason”
  * suitable for cron/CI

## E3. Networking Debug Workbook

* You’ll create a personal “runbook”:

  * commands + expected outputs,
  * decision trees for common outages.

---

# What you’ll be able to do by the end

* Answer Linux/network interview questions with confidence **and** demonstrate with commands.
* Write safe Bash scripts used for automation/oncall/CI.
* Debug real issues quickly: permissions, services, logs, disk, CPU, DNS, ports, TLS.
* Speak like an SRE: evidence-based troubleshooting, not guessing.

---
---
---
---
---
---

# **AWS**

## Master plan: AWS for DevOps/SRE interviews

### Phase 0 — Cloud fundamentals and AWS mental models

* What is cloud (IaaS / PaaS / SaaS)
* AWS global infrastructure
  * Regions, Availability Zones, edge locations
  * High availability vs fault tolerance vs disaster recovery
* AWS pricing basics
  * Pay-as-you-go concepts, major cost drivers
  * Tagging for cost allocation (why it matters in DevOps)
* AWS support model (conceptually)
* Core mental models you’ll use in every answer
  * Shared Responsibility Model
  * Security-first + least privilege mindset
  * “Design for failure” mindset
---

### Phase 1 — Identity, access, and security foundations (IAM first)

**Goal:** Be able to reason about “who can do what” and secure systems by default.

* IAM building blocks

  * Users, groups, roles, policies
  * Temporary credentials (STS), role assumption
* Policy evaluation logic

  * implicit deny vs explicit deny
  * resource policies vs identity policies
* Common auth patterns in DevOps

  * EC2 instance roles
  * CI/CD role assumption
  * cross-account access basics
* MFA, password policies
* Security “must know” services (intro)

  * KMS basics (encryption concepts)
  * Secrets Manager / Parameter Store (what/when)
  * CloudTrail (audit logging of API calls)

**Deliverable:** Write and debug IAM policies + explain least privilege like an SRE.

---

### Phase 2 — Networking (VPC) like a DevOps engineer

**Goal:** This is the #1 interview differentiator. Build and explain networks.

* VPC fundamentals

  * CIDR, subnets (public/private), route tables
  * Internet Gateway vs NAT Gateway
  * Security Groups vs NACLs (stateful vs stateless)
* Traffic flow and reachability reasoning

  * “Can this instance talk to X? Why/why not?”
* DNS + name resolution basics (in AWS context)
* VPC endpoints (private access to AWS services)
* Peering / Transit Gateway concepts (when/why)
* Hybrid connectivity concepts

  * VPN, Direct Connect (high-level)
* Load balancing networking basics

  * ALB vs NLB (what problems they solve)

**Deliverable:** You can draw a VPC diagram and explain every arrow.

---

### Phase 3 — Compute fundamentals (how workloads run)

**Goal:** Operate compute reliably and cost-effectively.

* EC2 fundamentals

  * AMIs, instance types (CPU/RAM/network tradeoffs)
  * EBS volumes, snapshots, encryption basics
  * User data, bootstrapping, golden images concept
* Autoscaling

  * Auto Scaling Groups, scaling policies, health checks
* Load balancing deeper

  * target groups, listener rules, health checks
* Bastion vs SSM access patterns (operational security)
* Basic hardening practices (patching, minimal exposure)

**Deliverable:** Deploy a resilient web workload across multiple AZs.

---

### Phase 4 — Storage (object/block/file) + data lifecycle

**Goal:** Know which storage to pick and how to secure/operate it.

* S3 (object storage)

  * bucket policies, ACLs (conceptually), versioning
  * lifecycle policies, storage classes (conceptually)
  * encryption and access logging concepts
  * static website hosting (optional)
* EBS (block storage) deepening

  * snapshot strategy, restore patterns, performance concepts (IOPS/throughput)
* EFS (shared file storage)

  * common use cases + pitfalls
* Backup/restore patterns (basic)

**Deliverable:** Confident “S3 vs EBS vs EFS” decisions + secure bucket patterns.

---

### Phase 5 — Databases and caching (what DevOps needs)

**Goal:** Enough to design, operate, and troubleshoot—without becoming a DBA.

* Relational basics (managed RDBMS)

  * backups, multi-AZ concepts, read replicas conceptually
* NoSQL basics

  * partition key concept, scaling model (high level)
* Caching basics

  * cache-aside pattern, TTL, invalidation pitfalls
* HA/DR concepts for data

  * RPO/RTO thinking (interview gold)

**Deliverable:** You can discuss DB tradeoffs and operational concerns.

---

### Phase 6 — Observability and operations (SRE core)

**Goal:** Monitor, debug, respond, and prevent incidents.

* Metrics, logs, traces (concepts + how AWS supports them)
* CloudWatch

  * metrics, alarms, dashboards
  * logs, log retention, filters/insights concepts
* CloudTrail (audit)

  * who changed what? incident investigation flow
* Event-driven operations

  * EventBridge concepts
* Systems Manager (SSM)

  * patching, inventory, Run Command, Session Manager
* Operational excellence practices

  * runbooks, alerts vs noise, on-call hygiene
  * incident response flow + postmortems

**Deliverable:** You can explain an incident and the AWS tools you’d use to investigate.

---

### Phase 7 — Infrastructure as Code (IaC) and configuration

**Goal:** Move from “click-ops” to reproducible infrastructure (major interview focus).

* IaC fundamentals

  * desired state, idempotency, drift, environments
* CloudFormation concepts (and/or Terraform concepts)

  * modules/stacks, parameters/outputs, state management (if Terraform)
* Multi-environment patterns (dev/stage/prod)
* Tagging strategy, naming, guardrails in IaC
* Secrets handling in IaC (what NOT to do)
* Config management concepts (when IaC ends and config begins)

**Deliverable:** Rebuild your environment from scratch using IaC.

---

### Phase 8 — CI/CD and deployment strategies (DevOps core)

**Goal:** Build pipelines that ship safely.

* Pipeline stages

  * build → test → security checks → deploy → verify → rollback
* Deployment strategies

  * rolling, blue/green, canary
* Artifact management concepts
* GitOps mindset (conceptually)
* Environment promotion, approvals, release hygiene
* Common failure modes

  * config drift, secrets leakage, bad rollouts, missing alarms

**Deliverable:** A working pipeline and a clear “zero-downtime deploy” explanation.

---

### Phase 9 — Containers and orchestration (modern platform skills)

**Goal:** Be fluent in container conversations (common in interviews).

* Container fundamentals

  * images vs containers, registries, tagging
* AWS container building blocks (conceptual + hands-on)

  * container registry
  * managed orchestration options
  * serverless containers vs node-based
* Load balancing with containers
* Service discovery basics
* Autoscaling for container services
* Logging/monitoring container workloads
* Secrets/config patterns for containers

**Deliverable:** Deploy a containerized service behind a load balancer with autoscaling.

---

### Phase 10 — Serverless and event-driven architecture (common in AWS shops)

**Goal:** Understand when serverless is best and how to operate it.

* Serverless fundamentals

  * stateless compute, cold starts, concurrency concepts
* Event sources and integrations (high-level)
* Retry behavior, idempotency, DLQ concepts
* Security + least privilege for serverless
* Observability for serverless

**Deliverable:** Build a small event-driven workflow and explain reliability behaviors.

---

### Phase 11 — Messaging, integration, and async patterns

**Goal:** Design systems that handle spikes, decouple services, and fail gracefully.

* Queues vs pub/sub patterns
* Fan-out, backpressure, retries, poison messages
* Ordering vs at-least-once tradeoffs
* DLQ patterns and alerting on DLQ depth
* Workflow orchestration concepts

**Deliverable:** Explain async patterns clearly and apply them to real scenarios.

---

### Phase 12 — Security, governance, and multi-account strategy

**Goal:** Sound like someone who can run production AWS responsibly.

* Account structure concepts

  * multi-account strategy, separation of duties
* Guardrails and org-level control concepts
* Centralized logging, audit trails
* Security posture monitoring concepts
* Key management and data protection patterns
* Least privilege at scale
* Incident response readiness

  * forensics-friendly logging, access review

**Deliverable:** Explain how you’d set up AWS for an enterprise (even at a high level).

---

### Phase 13 — Reliability, DR, performance, and cost optimization (advanced)

**Goal:** “Senior” design thinking.

* Reliability engineering

  * AZ failure handling, health checks, graceful degradation
* DR strategies (conceptual)

  * backup/restore, pilot light, warm standby, active/active (high level)
* Performance optimization

  * caching strategies, scaling bottlenecks, network constraints
* Cost optimization

  * right-sizing, autoscaling, storage lifecycle, avoiding NAT surprises, log retention control
* Limits/quotas and capacity planning basics

**Deliverable:** You can answer architecture questions with tradeoffs, not buzzwords.

---

### Phase 14 — Troubleshooting playbooks (interview scenarios)

**Goal:** Be able to “debug out loud.”

* “Website is down” playbook

  * DNS → LB → targets → security groups/routes → instance health → logs/metrics
* “Latency increased” playbook

  * dashboards, saturation, throttles, DB, caching, network
* “Cost spiked overnight” playbook

  * billing explorer concepts, top services, NAT, logs, runaway scaling
* “Access denied” playbook

  * IAM evaluation, resource policies, SCP/guardrails concept, CloudTrail evidence
* “Deploy broke prod” playbook

  * rollback, blast radius, progressive delivery, postmortem

**Deliverable:** You can walk an interviewer through diagnosis step-by-step calmly.

---

## Capstones (what you’ll build to prove competence)

You’ll complete these hands-on projects as “proof you can do the job”:

1. **Production-style VPC + app stack** (multi-AZ, private subnets, NAT/endpoints, ALB, autoscaling)
2. **Observability pack** (metrics + logs + alarms + incident runbook)
3. **IaC rebuild** (recreate the whole stack from code)
4. **CI/CD pipeline** (safe deploy + rollback strategy)
5. **Containers OR serverless** (pick one based on your target roles; both if you want “any interview” coverage)

---

## Interview mastery layers (what you’ll practice continuously)

* “Explain like I’m 10” answers (clear + simple)
* “Production-grade” answers (tradeoffs + failure modes)
* Design questions (requirements → architecture → risks → cost → ops)
* Behavioral + incident stories (STAR + metrics + ownership)

---
---
---
---
---
---

## Python

# L0 — Setup, workflow, and “DevOps way” of running Python

**Goal:** be comfortable running, packaging, and debugging scripts like you would at work.

**Topics**

* Installing Python (system vs pyenv)
* `python`, `python3`, `pip`, `pipx`
* Virtual environments: `venv`, dependency isolation
* Running scripts: shebang (`#!/usr/bin/env python3`), chmod +x, PATH
* REPL vs script vs modules: `python -c`, `python -m`
* Basic debugging: print debugging, `pdb` overview
* Editor setup: formatting, linting, type hints basics (intro only)

**Outputs**

* A working `devops-python/` repo with a consistent layout
* A “hello ops” script + Makefile targets (`make run`, `make test`)

---

# L1 — Core Python foundations (must become automatic)

**Goal:** write correct basic code fast without thinking.

**Topics**

* Syntax + style
* Variables and built-in types: `int`, `float`, `bool`, `str`, `None`
* Operators: arithmetic, comparisons, boolean logic
* Strings deeply:

  * indexing/slicing, `split/join`, `strip`, `replace`
  * f-strings, formatting
* Collections:

  * `list`, `tuple`, `set`, `dict`
  * membership (`in`), iteration
* Control flow:

  * `if/elif/else`
  * `for`, `while`, `break/continue`
  * `range`, `enumerate`, `zip`
* Functions:

  * `def`, `return`, parameters, defaults
  * `*args`, `**kwargs` (intro)
  * scope, mutability basics
* Imports and modules:

  * `import`, `from x import y`
  * `__name__ == "__main__"`

**DevOps interview patterns**

* Count frequencies
* Parse key=value logs
* Transform lists/dicts
* Implement small utilities cleanly

**Outputs**

* 20+ mini problems solved cleanly
* “log parser v1” script (no regex yet)

---

# L2 — Data handling + reliability (turn scripts into tools)

**Goal:** handle real-world inputs safely: files, errors, messy data.

**Topics**

* Exceptions:

  * `try/except/else/finally`
  * raising errors, custom exceptions
  * common exceptions in scripting
* Files and directories:

  * `pathlib` (preferred), `os`
  * reading/writing text + binary
  * safe file handling with `with`
  * walking directories, globbing
* Encodings + newline issues
* Serialization:

  * JSON: `json.loads/dumps`, file read/write
  * YAML (common in DevOps): safe load/dump patterns
* Date/time:

  * `datetime`, time zones basics
  * timestamps, ISO-8601 parsing
* Text processing upgrade:

  * `re` regex basics (just enough for logs)
* Hashing + integrity:

  * `hashlib` (md5/sha256), checksums
* Environment variables:

  * `os.environ`, `os.getenv`
* Deterministic behavior and reproducibility (seeds, config)

**Outputs**

* “log parser v2” (regex + JSON output)
* “config loader” tool that merges env vars + YAML + CLI args

---

# L3 — Build real DevOps CLI tools (what interviews love)

**Goal:** write production-style command-line tools with proper UX.

**Topics**

* CLI interfaces:

  * `argparse` (required)
  * subcommands (like `kubectl` style)
  * stdin/stdout/stderr, exit codes
* Logging:

  * `logging` levels, formats, timestamps
  * log to file and console
* Running external commands:

  * `subprocess.run`, `Popen` basics
  * timeouts, capturing output, return codes
  * quoting issues & security
* Process and system info:

  * `platform`, `getpass`, `socket`
  * cpu/mem basics via `/proc` (Linux) approach
* Working with archives:

  * `tarfile`, `zipfile` (for build artifacts)
* Stream processing:

  * reading big files line-by-line
  * generators (memory efficiency)
* Structured output formats:

  * plain text, JSON output modes (`--json` pattern)

**Outputs**

* A “system inventory” CLI: `opsinfo --json`
* A “safe shell runner” CLI: `runx --timeout 5 -- cmd args...`

---

# L4 — Networking + APIs (core for Cloud / SRE roles)

**Goal:** confidently automate REST APIs, handle failures, and integrate with cloud services.

**Topics**

* HTTP fundamentals:

  * methods, status codes, headers, query params
  * idempotency
* `requests` patterns:

  * timeouts (must)
  * retries with backoff
  * sessions, connection pooling
  * pagination patterns
* Authentication patterns:

  * bearer tokens, API keys
  * env-var secrets handling (no hardcoding)
* Basic sockets (just conceptually): DNS, TCP basics (no deep dive)
* Webhooks and JSON payload validation
* Rate limiting and backoff strategy
* Observability: log correlation IDs

**Cloud SDK exposure (DevOps-relevant)**

* AWS automation patterns:

  * boto3 core patterns (clients/resources)
  * pagination, retries, credential resolution
  * common services: S3, EC2, IAM, Lambda, DynamoDB
* (Optional) GCP/Azure at a “script” level if needed

**Outputs**

* “API health checker” CLI (multi-endpoint, retry + report)
* “S3 cleaner” (list objects by prefix + delete safely with dry-run)

---

# L5 — Concurrency + performance (SRE-ready, interview-friendly)

**Goal:** write faster tools and explain tradeoffs.

**Topics**

* Performance basics:

  * Big-O intuition for common ops
  * profiling basics (`cProfile` overview)
* Concurrency models:

  * threads vs processes vs async (when to use each)
* `concurrent.futures`:

  * `ThreadPoolExecutor` for I/O
  * `ProcessPoolExecutor` for CPU
  * timeouts, cancellations
* `asyncio` fundamentals:

  * event loop concept
  * async/await syntax
  * when async is useful in DevOps tooling
* Queues and coordination basics
* Rate-limited parallel API calls pattern

**Outputs**

* “parallel log scanner” (search across many files fast)
* “concurrent endpoint probe” tool (threaded with limits)

---

# L6 — Software engineering quality (what makes you stand out)

**Goal:** write maintainable, testable code—common in senior screens.

**Topics**

* Code organization:

  * modules/packages, `src/` layout (simple version)
  * reusable library + CLI entry point
* Testing:

  * `pytest` essentials
  * fixtures, parametrize
  * mocking (`unittest.mock`) for subprocess/API
* Type hints:

  * `typing` basics, `mypy` mindset
* Linting/formatting:

  * `ruff`/`flake8` concepts
  * `black` formatting concepts
* Documentation:

  * docstrings, README usage examples
* Security basics for scripts:

  * handling secrets, avoiding shell injection
  * least privilege mindset
* Error handling strategy:

  * consistent return codes
  * actionable error messages
* Packaging & release:

  * `pyproject.toml` basics
  * pinned deps, lockfiles concept
* CI basics:

  * run tests in CI (GitHub Actions overview)

**Outputs**

* A “real” mini-project shipped like a tool:

  * installable package
  * `--help` UX
  * unit tests + CI
  * README examples

---

# Final phase — DevOps Python interview drills (the “crack interviews” part)

**Goal:** be able to *solve + explain* common interview tasks quickly.

## Common interview question categories we will master

* **Log parsing & aggregation**

  * filter, count, percentiles, top N
  * detect anomalies, compute error rates
* **File operations**

  * scan dirs, rotate logs, cleanup by age/size
* **Config processing**

  * merge YAML/JSON/env + validate required keys
* **Subprocess automation**

  * run commands safely, parse outputs, handle failures
* **API automation**

  * pagination, retries, concurrency, rate limits
* **Data transformations**

  * dict/list manipulations, grouping, sorting
* **Reliability & production thinking**

  * timeouts, backoff, idempotency, observability
* **Testing & maintainability**

  * structure code into functions, add tests, mocks

## Capstone “interview simulator” projects

1. **Log Inspector CLI**

   * Reads large logs, filters by time/level/service
   * Outputs JSON summary + top errors
2. **Cloud Cleanup Tool**

   * Dry-run + delete old artifacts by policy
3. **Health Check + Alert Report**

   * Concurrently checks endpoints with retries
   * Generates a report (JSON + text table)

---
---
---
---
---
---

## Terraform

## 0) Foundations

### 0.1 IaC fundamentals

* Declarative vs imperative
* Idempotency
* Desired state vs actual state
* Drift (what it is, why it happens)
* Immutable vs mutable infrastructure

### 0.2 CLI + Linux basics for Terraform usage

* folders, files, env vars
* exit codes, piping
* secrets hygiene in terminals

### 0.3 Git for Terraform workflows

* branching strategy
* PR reviews
* tags/releases
* rollback strategy

---

## 1) Terraform Core: How Terraform works

This is the mental model interviewers test first.

### 1.1 Terraform components

* Terraform CLI
* Providers (plugin model)
* Resources / Data sources
* Modules (root vs child)
* State and backends

### 1.2 The lifecycle of a run

* `init`, `validate`, `fmt`
* `plan` (diff + what will change)
* `apply` (execution + state update)
* `destroy`
* Exit codes and automation-friendly patterns

### 1.3 Dependency graph basics

* Implicit dependencies (references)
* Explicit dependencies (`depends_on`) and when needed

**Milestone:** You can explain Terraform in 60 seconds clearly.

---

## 2) HCL Language Mastery (Terraform syntax + expressions)

This is where you become strong in writing real configs.

### 2.1 Blocks and structure

* `terraform {}`, `provider {}`, `resource {}`, `data {}`, `module {}`, `output {}`, `locals {}`

### 2.2 Variables and types

* input variables: defaults, descriptions, validation
* types: string, number, bool, list, set, map, object, tuple
* `nullable`, `sensitive`
* variable precedence (tfvars, env vars, CLI args)

### 2.3 Expressions and functions

* interpolation
* conditionals (`condition ? a : b`)
* `for` expressions
* functions: `lookup`, `try`, `coalesce`, `merge`, `flatten`, `zipmap`, `regex`, `jsonencode`, `yamldecode`, etc.

### 2.4 Loops and dynamic config

* `count` vs `for_each` (address stability, refactors)
* `dynamic` blocks (when to use, when to avoid)

### 2.5 Common patterns

* naming/tagging conventions (env/app/owner/cost)
* optional attributes in objects
* “defaults + overrides” patterns

**Milestone:** You can read any Terraform codebase and understand it.

---

## 3) State: the most important real-world topic

Most production incidents happen here, so we go deep.

### 3.1 State basics

* what state contains
* why state exists
* sensitivity (secrets risk)

### 3.2 Backends

* local vs remote backend concepts
* locking and concurrency
* state encryption at rest (backend-dependent)
* state file structure (high level)

### 3.3 State operations

* `terraform state list/show`
* `state mv` (refactors safely)
* `state rm` (when it’s dangerous)
* `import` (adopt existing resources)

### 3.4 Drift handling

* how drift happens (manual console changes, automation, external controllers)
* detection and response patterns

### 3.5 Workspaces (what they are + pitfalls)

* workspaces vs separate directories
* when workspaces are okay vs a foot-gun

**Milestone:** You can explain team-safe Terraform and state locking.

---

## 4) Providers & Resource Design (cloud + SaaS APIs)

This is where Terraform meets real infrastructure.

### 4.1 Provider configuration

* provider version constraints
* provider aliases (multi-region / multi-account)
* authentication patterns (env vars, profiles, workload identity)

### 4.2 Resource vs data source

* when to create vs read
* importing vs re-creating
* “source of truth” decisions

### 4.3 Read-before-write and plan-time unknowns

* unknown values during plan
* computed attributes
* dependency issues caused by unknowns

### 4.4 Common provider gotchas

* eventual consistency
* rate limits/retries
* ordering quirks

**Milestone:** You can design Terraform for an API-driven platform reliably.

---

## 5) Modules: building reusable infrastructure like a pro

This is a big differentiator in interviews.

### 5.1 Module fundamentals

* module boundaries: what belongs inside
* inputs/outputs design
* exposing only what callers need

### 5.2 Module structure & standards

* folder layout (`main.tf`, `variables.tf`, `outputs.tf`, `README`)
* naming conventions
* examples folder patterns

### 5.3 Versioning and release strategy

* pinning module versions
* breaking vs non-breaking changes
* module registry concepts (public/private)

### 5.4 Composition patterns

* “base module” + environment wrapper
* shared networking module + app modules
* DRY without over-abstracting

**Milestone:** You can create a module library your team can reuse safely.

---

## 6) Environment Strategy (dev/stage/prod done right)

Interviewers love “how do you organize Terraform?”

### 6.1 Patterns

* single repo with `envs/` folders
* separate repos per environment
* monorepo vs multirepo tradeoffs

### 6.2 Configuration layering

* variables per env
* global defaults + env overrides
* avoiding copy/paste hell

### 6.3 Multi-account / multi-subscription patterns

* account boundaries, blast radius
* separate state per environment/account/region

**Milestone:** You can propose a clean org structure for a company.

---

## 7) Safe Changes, Refactors, and Lifecycle Controls

This is advanced—but very practical.

### 7.1 Lifecycle meta-argument

* `prevent_destroy`
* `create_before_destroy`
* `ignore_changes`
* when lifecycle is appropriate vs hiding drift

### 7.2 Refactor safety

* renaming blocks without replacement (state moves)
* dealing with `count`/`for_each` changes safely
* minimizing downtime during replacements

### 7.3 Targeting & partial applies

* why `-target` is risky
* safe emergency usage patterns

**Milestone:** You can refactor production Terraform without outages.

---

## 8) CI/CD for Terraform (how it’s run in real companies)

This is essential for DevOps/SRE roles.

### 8.1 Pipeline stages

* format + validate
* lint/static checks
* plan in PR
* apply with approvals
* drift detection schedules

### 8.2 Secrets in pipelines

* injecting secrets safely (never in `.tfstate` intentionally)
* using secret managers (conceptually)
* avoiding secrets in logs

### 8.3 Remote execution patterns

* centralized runs vs local runs
* approvals and audit trails

**Milestone:** You can describe an enterprise Terraform workflow confidently.

---

## 9) Quality & Guardrails (testing, linting, policy)

This is where “senior” signals show up.

### 9.1 Code quality

* formatting standards
* naming conventions & tagging
* documentation expectations

### 9.2 Static analysis & linting (tools conceptually)

* validating module interfaces
* catching common errors early

### 9.3 Policy as code (conceptually)

* enforcing rules (no public S3, required tags, allowed regions)
* where policy checks run (pre-merge, pre-apply)

### 9.4 Testing strategies (conceptually + practical)

* module unit-ish tests (validate inputs/outputs)
* integration tests (apply in sandbox)
* smoke tests after apply

**Milestone:** You can explain how to prevent unsafe infrastructure changes.

---

## 10) Debugging & Troubleshooting (interview gold)

You’ll practice solving issues fast.

### 10.1 Common errors

* provider auth failures
* dependency cycles
* “forces replacement”
* state lock contention
* drift surprises
* import mismatches

### 10.2 Reading plans like a pro

* spotting destructive changes
* understanding computed values
* recognizing noisy diffs

### 10.3 Operational recovery

* stuck resources
* manual fix + state reconciliation
* safe rollback strategies

**Milestone:** You can debug Terraform under pressure.

---

## 11) Cloud Track (choose a primary cloud for labs)

Terraform is cloud-agnostic, but interviews often want real cloud examples.

We’ll do **one main track** deeply (typically AWS), and optionally map equivalents to Azure/GCP.

### 11.1 Core cloud building blocks (Terraform implementation)

* networking: VPC/VNet, subnets, routes, NAT/IGW
* security: SG/NSG/firewalls, IAM/RBAC patterns
* compute: VM/instances, autoscaling
* load balancing
* storage basics
* logging/monitoring basics
* DNS basics

### 11.2 “DevOps-style” stacks (end-to-end)

* baseline networking module
* app module + deployment plumbing
* shared services module (logging, DNS, etc.)

**Milestone:** You can describe a full infra design and how Terraform manages it.

---

## 12) Capstone Projects (portfolio + interview stories)

You’ll complete 2–3 capstones to be truly confident.

### Capstone A: “Single environment production-grade baseline”

* remote state + locking
* networking module
* compute + LB
* security + tagging
* CI plan/apply flow

### Capstone B: “Multi-environment (dev/stage/prod)”

* environment structure
* separate state per env
* promotion strategy (module version pinning)

### Capstone C (optional): “Multi-account / multi-region”

* provider aliases
* cross-account boundaries
* blast radius control

**Milestone:** You have real artifacts and stories for interviews.

---

## 13) Interview Mastery Layer (Q&A + scenario drills)

We’ll train answers like an interview.

### 13.1 Core questions (must-master)

* state/backends/locking
* workspaces vs folders
* modules + versioning
* `count` vs `for_each`
* drift handling
* import/refactor strategy
* CI workflow + approvals
* secrets and security

### 13.2 Scenario drills

* “Terraform wants to replace everything—what do you do?”
* “Two engineers applied at once—what happened?”
* “We need to rename resources without downtime—how?”
* “We have existing infra—how do we adopt it?”

### 13.3 “Explain like I’m five” + “Deep dive” versions

---
---
---
---
---
---

# Kubernetes

# Phase 0 — Foundations (K8s “literacy”)

### 0.1 Linux + container basics (K8s depends on this)

* What is a container vs VM
* Images, tags, registries
* `docker`/`containerd` concepts (pull/run/exec/logs)
* Process model: PID 1, signals, exit codes
* Filesystems: overlayfs (conceptual)
* Networking basics: ports, NAT, DNS, localhost vs 0.0.0.0
* TLS basics: certificates, CA, chain (high level)

### 0.2 Kubernetes big picture

* Why Kubernetes exists (problems it solves)
* Cluster components:

  * Control plane: API server, scheduler, controller manager, etcd
  * Node: kubelet, container runtime, kube-proxy, CNI plugin
* Declarative desired state: controllers reconcile reality → desired

### 0.3 kubectl + YAML fundamentals

* YAML structure: maps/lists/indentation
* K8s API basics: `apiVersion`, `kind`, `metadata`, `spec`, `status`
* `kubectl` essentials:

  * get/describe/logs/exec/events
  * apply/delete
  * context, kubeconfig, namespaces
* Labels/selectors/annotations
* Resource discovery: `kubectl api-resources`, `kubectl explain`

**Deliverable:** You can read and write simple YAML and debug with basic kubectl.

---

# Phase 1 — Core Workloads (most asked)

### 1.1 Pods (the base unit)

* Pod lifecycle and restarts
* Multi-container pods (sidecar pattern)
* Init containers
* Ephemeral containers (debug concept)
* Pod conditions and status fields
* Image pull policy, imagePullSecrets

### 1.2 Controllers for stateless apps

* Deployment + ReplicaSet
* Rolling updates, rollbacks
* Revision history
* Strategies: RollingUpdate vs Recreate
* Scaling (manual), autoscaling preview

### 1.3 Jobs

* Job patterns and backoff
* CronJobs: schedule, concurrency policy, startingDeadlineSeconds

### 1.4 Stateful and node-specific controllers

* StatefulSet: stable identity, stable storage
* DaemonSet: one-per-node workloads
* When to use each (interview framing)

**Deliverable:** You can choose the right controller and explain why.

---

# Phase 2 — Configuration & App Delivery

### 2.1 Config management

* ConfigMaps:

  * env vars
  * mounted files
* Secrets:

  * types
  * how they’re stored and common misconceptions
* Downward API (pod info into env/files)
* Environment variable precedence patterns

### 2.2 Probes & lifecycle hooks

* Liveness vs readiness vs startup probes
* HTTP/TCP/exec probes
* preStop hooks, terminationGracePeriodSeconds
* Deployment rollout safety with readiness

### 2.3 Resource management

* Requests vs limits
* QoS classes: Guaranteed / Burstable / BestEffort
* OOMKilled vs CPU throttling
* LimitRanges and ResourceQuotas

**Deliverable:** You can make apps reliable and predictable under load.

---

# Phase 3 — Networking (highest interview weight)

### 3.1 Cluster networking fundamentals

* Pod IP model (each pod gets an IP)
* Service discovery and DNS
* CNI plugin concept: who provides pod networking
* kube-proxy concept (iptables/ipvs high-level)

### 3.2 Services

* ClusterIP vs NodePort vs LoadBalancer
* Endpoints / EndpointSlices concept
* Headless service (esp. StatefulSet)
* Session affinity, source IP, externalTrafficPolicy (high-level)

### 3.3 Ingress and traffic entry

* Ingress basics (controller required)
* TLS termination and certs
* Path-based routing, host-based routing
* When to use Ingress vs LoadBalancer
* (Advanced overview) Gateway API vs Ingress (conceptual)

### 3.4 Network Policies

* Default allow vs default deny
* Ingress/egress rules
* Common patterns (allow DNS, allow namespace-to-namespace)

### 3.5 DNS deep dive (common troubleshooting topic)

* CoreDNS basics
* How service names resolve
* Debugging DNS from inside a pod

**Deliverable:** You can explain traffic flow end-to-end and debug connectivity.

---

# Phase 4 — Storage (stateful workloads)

### 4.1 Volumes basics

* emptyDir, hostPath, configMap/secret volumes
* Persistent volumes concept

### 4.2 PV/PVC and dynamic provisioning

* PV vs PVC
* StorageClass
* Access modes: RWO/ROX/RWX
* VolumeBindingMode (WaitForFirstConsumer concept)
* CSI drivers (what they do)

### 4.3 Stateful patterns

* StatefulSet + volumeClaimTemplates
* Backups (conceptual: snapshots, Velero idea)
* Anti-patterns (databases in Deployments)

**Deliverable:** You can debug “PVC Pending” and design stateful apps correctly.

---

# Phase 5 — Scheduling & Cluster Operations

### 5.1 Scheduling decisions

* Node selectors
* Affinity/anti-affinity
* Taints/tolerations
* Topology spread constraints (conceptual)
* PriorityClasses and preemption (conceptual)

### 5.2 Disruptions & availability

* PodDisruptionBudgets (PDB)
* Safe node drains and maintenance windows
* Rolling updates + PDB interactions

### 5.3 Node lifecycle

* Node conditions: Ready/NotReady
* Cordon/drain/uncordon
* Why pods get evicted

**Deliverable:** You can control placement and keep services stable through failures.

---

# Phase 6 — Security (must-have for SRE/Platform)

### 6.1 Authentication & authorization

* kubeconfig users/contexts
* RBAC:

  * Role vs ClusterRole
  * RoleBinding vs ClusterRoleBinding
* Least privilege design

### 6.2 Service Accounts

* ServiceAccount usage
* Token mounting and implications
* Workload identity patterns (cloud concept)

### 6.3 Pod security hardening

* SecurityContext: runAsUser, runAsNonRoot, fsGroup
* Linux capabilities, readOnlyRootFilesystem
* Seccomp (conceptual)
* Pod Security Admission (baseline/restricted concept)

### 6.4 Supply chain basics

* Image scanning concepts
* ImagePullSecrets
* Signed images concept (high-level)

**Deliverable:** You can design RBAC + workload hardening stories for interviews.

---

# Phase 7 — Observability & Troubleshooting (real-world operator skills)

### 7.1 Debugging methodology (interview gold)

* The standard triage flow:

  * `get` → `describe` → `events` → `logs` → `exec` → deeper
* Common failure modes:

  * CrashLoopBackOff
  * ImagePullBackOff
  * Pending pods
  * OOMKilled
  * Readiness never becomes true
  * Node pressure evictions

### 7.2 Logging

* Container stdout/stderr model
* Centralized logging concept (Fluent Bit/Fluentd, Loki/ELK high-level)
* Log querying patterns

### 7.3 Metrics

* metrics-server basics
* Prometheus concepts (scrape, exporters)
* Key SRE metrics: latency, errors, saturation, traffic

### 7.4 Tracing (high-level)

* Why distributed tracing matters
* OpenTelemetry concept

### 7.5 Health + SLO thinking (interview edge)

* SLI/SLO basics
* Alert fatigue principles

**Deliverable:** You can debug quickly and speak in production terms.

---

# Phase 8 — Autoscaling & Performance

### 8.1 HPA (Horizontal Pod Autoscaler)

* How HPA decides to scale
* CPU/memory metrics and common pitfalls
* Stabilization windows (conceptual)

### 8.2 VPA (conceptual)

* What it does, why it’s risky in production

### 8.3 Cluster autoscaler (conceptual)

* When nodes scale, interaction with scheduling

### 8.4 Performance tuning

* Right-sizing requests/limits
* Resource contention scenarios
* Network and storage bottleneck patterns (high-level)

**Deliverable:** You can explain scaling architecture and avoid common footguns.

---

# Phase 9 — Packaging, Releases, GitOps (DevOps reality)

### 9.1 Helm

* Charts, values, templates
* Install/upgrade/rollback
* Release management

### 9.2 Kustomize

* Bases and overlays
* Patches (strategic merge concept)
* Environments (dev/stage/prod)

### 9.3 GitOps (conceptual but important)

* Desired state in Git
* Reconciliation loop tools:

  * Argo CD / Flux (high-level)
* Promotion and drift detection

### 9.4 Progressive delivery (conceptual)

* Canary vs blue/green
* Feature flags vs deployment strategies

**Deliverable:** You can discuss delivery pipelines and environment management.

---

# Phase 10 — Cluster Architecture & “How it really works”

*(You don’t need to be a cluster admin, but interviews love this depth.)*

* API server request flow (kubectl → API → etcd)
* etcd importance (why it’s critical)
* Controller reconciliation model
* Scheduler decision factors
* kubelet responsibilities
* CRI/CNI/CSI roles (runtime/network/storage plugins)
* Add-ons: CoreDNS, metrics-server, ingress-controller
* Upgrade strategy (high-level)
* Backup/restore basics (etcd snapshot concept)

**Deliverable:** You can explain Kubernetes internals clearly without hand-waving.

---

# Phase 11 — Advanced topics (only after strong basics)

* Custom Resource Definitions (CRDs) + Operators (conceptual)
* Admission controllers & webhooks (conceptual)
* Service mesh overview (Istio/Linkerd conceptual) — when it’s useful vs overkill
* Multi-cluster patterns (conceptual)
* Namespaces as tenancy boundaries (pros/cons)
* Cost controls and capacity planning (conceptual)
* Disaster recovery playbooks (conceptual)

**Deliverable:** You can answer “senior” questions and design tradeoffs.

---

# Phase 12 — Interview mastery (we practice this continuously)

### 12.1 “Explain like I’m 5” answers (simple)

* What is a pod?
* What is a service?
* What is ingress?

### 12.2 “Production engineer” answers (deep + practical)

* How do you do zero downtime?
* How do you debug CrashLoopBackOff?
* How do you control blast radius?
* How do you secure workloads?

### 12.3 Scenario drills (the real test)

* “Users can’t reach service” (network/DNS/ingress)
* “Pods pending” (scheduling/resources)
* “Latency spikes” (autoscaling/limits)
* “Node not ready” (node triage)
* “Secret rotation” (config patterns)
* “RBAC breaks deploy” (authz debugging)

### 12.4 Cheat sheets + flashcards

* Command cheat sheet
* Common errors + fixes
* YAML templates library

---

## How we’ll know you’re “interview ready”

You’ll pass these milestones:

1. Build and expose an app (Deployment + Service + Ingress)
2. Debug 8 common failures quickly (with correct commands)
3. Explain networking and services clearly end-to-end
4. Design safe rollouts and rollbacks
5. Explain security approach (RBAC + pod hardening)
6. Present a full production story (deploy → observe → scale → secure)

---

