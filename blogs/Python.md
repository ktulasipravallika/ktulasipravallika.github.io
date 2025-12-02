1. Explain the concept (with AWS/DevOps angle where relevant)
2. Give **code examples**
3. Give **exercises + typical interview questions** (with sample answers later in the same section)

You can go through section by section at your own pace today.

---

## 0. Why Python for AWS DevOps (your “why”)

You’re learning Python to:

* **Automate AWS**: create EC2s, VPCs, S3 buckets, IAM users, alarms, etc.
* **Build tools**: health checks, config validators, deployment helpers.
* **ETL**: move data between DynamoDB → S3, or S3 → Redshift, etc.
* **Support CI/CD**: glue code around Jenkins/GitHub Actions/Terraform (pre/post steps).

Keep this mental map:

> **Python basics → Data structures → Files & errors → Modules & OOP → JSON/YAML → REST → Boto3 AWS automation**

We’ll build towards a small AWS “inventory + alarm” script.

---

## 1. Syntax basics: variables, types, if/else, loops, functions

### 1.1 Variables & types

```python
# Basic types
x = 10            # int
pi = 3.14         # float
name = "Tulasi"   # str
is_active = True  # bool
nothing = None    # NoneType

print(type(x), type(pi), type(name), type(is_active), type(nothing))
```

Important: Python is **dynamically typed**, but you *can* add type hints:

```python
age: int = 30
env: str = "dev"
```

This matters in larger AWS tools: type hints help you avoid bugs in complex scripts.

---

### 1.2 if / elif / else

```python
cpu_usage = 85

if cpu_usage > 90:
    print("Critical: scale up NOW")
elif cpu_usage > 70:
    print("Warning: watch closely")
else:
    print("All good")
```

Indentation with spaces is significant. No `{}`.

---

### 1.3 Loops

**for loop** – iterate over a sequence:

```python
regions = ["us-east-1", "us-west-2", "eu-west-1"]

for region in regions:
    print("Checking region:", region)
```

**while loop** – run until condition breaks:

```python
retries = 0
max_retries = 3

while retries < max_retries:
    print("Attempt", retries + 1)
    retries += 1
```

---

### 1.4 Functions

```python
def add(a: int, b: int) -> int:
    return a + b

result = add(3, 5)
print("Result:", result)
```

Default arguments:

```python
def greet(name: str, env: str = "dev") -> None:
    print(f"Hello {name}, welcome to {env} environment")

greet("Tulasi")
greet("Tulasi", env="prod")
```

---

### 1.5 Quick exercises (Basics)

Try these mentally / in your editor:

1. Write a function `is_high_cpu(usage)` that:

   * Returns `"CRITICAL"` if usage ≥ 90
   * `"WARN"` if 70–89
   * `"OK"` otherwise

2. Print all even numbers from 1 to 20 using a `for` loop.

3. Given `env = "prod"`, `region = "us-east-1"`, print:
   `"Deploying to prod in us-east-1"` using an f-string.

**Sample solutions (peek after trying):**

```python
def is_high_cpu(usage: int) -> str:
    if usage >= 90:
        return "CRITICAL"
    elif usage >= 70:
        return "WARN"
    else:
        return "OK"


for i in range(1, 21):
    if i % 2 == 0:
        print(i)


env = "prod"
region = "us-east-1"
print(f"Deploying to {env} in {region}")
```

**Interview-style questions**

* What’s the difference between `==` and `is`?

  * `==` compares values, `is` compares object identity.
* How does indentation work in Python?

  * Blocks are defined by indentation (usually 4 spaces). Mis-indentation causes `IndentationError`.

---

## 2. Data structures: list, dict, set, tuple

These are heavily used for AWS resource lists, configs, tags, etc.

### 2.1 Lists (ordered, mutable)

```python
instances = ["i-123", "i-456", "i-789"]
instances.append("i-999")
instances.remove("i-456")
print(instances)        # ['i-123', 'i-789', 'i-999']
print(len(instances))   # 3
```

Typical use: list of regions, list of instance IDs, list of alarms.

---

### 2.2 Dicts (key-value maps)

```python
instance_meta = {
    "id": "i-123",
    "type": "t3.micro",
    "state": "running",
    "tags": {"Name": "web-server", "Env": "prod"},
}

print(instance_meta["id"])
print(instance_meta.get("zone", "unknown"))
```

Iterating:

```python
for key, value in instance_meta.items():
    print(key, "=>", value)
```

---

### 2.3 Sets (unique, unordered)

```python
regions = {"us-east-1", "us-west-2", "us-east-1"}
print(regions)  # {'us-east-1', 'us-west-2'} – duplicates removed

regions.add("eu-west-1")
```

Useful for: unique list of AZs, unique error codes, etc.

---

### 2.4 Tuples (immutable sequences)

```python
coords = (37.77, -122.41)  # (lat, lon)
env_region = ("prod", "us-east-1")
```

Often used as fixed pairs/records or as dictionary keys.

---

### 2.5 Exercises (Data structures)

1. Given this list of instance types:
   `types = ["t3.micro", "t3.micro", "t3.small", "t3.medium", "t3.small"]`

   * Print unique types
   * Print how many times each type occurs (use a dict)

2. Represent an S3 object as a dict with keys: `bucket`, `key`, `size`, `storage_class`.

3. Given:

   ```python
   alarms = [
       {"name": "HighCPU", "metric": "CPUUtilization", "threshold": 80},
       {"name": "HighLatency", "metric": "Latency", "threshold": 200},
   ]
   ```

   Print each alarm in the format:
   `"Alarm HighCPU on CPUUtilization > 80"`

**Sample solutions:**

```python
types = ["t3.micro", "t3.micro", "t3.small", "t3.medium", "t3.small"]

unique_types = set(types)
print(unique_types)

counts = {}
for t in types:
    counts[t] = counts.get(t, 0) + 1
print(counts)


s3_object = {
    "bucket": "my-logs-bucket",
    "key": "logs/2025/12/01/app.log",
    "size": 10240,
    "storage_class": "STANDARD",
}


alarms = [
    {"name": "HighCPU", "metric": "CPUUtilization", "threshold": 80},
    {"name": "HighLatency", "metric": "Latency", "threshold": 200},
]

for alarm in alarms:
    print(f"Alarm {alarm['name']} on {alarm['metric']} > {alarm['threshold']}")
```

**Interview-style**

* Time complexity for:

  * List `append` ~ O(1) amortized
  * Dict get/set ~ O(1) average
  * Set add/contains ~ O(1) average

---

## 3. File I/O (read/write)

Very common for reading configs, logs, and writing reports.

```python
# Write
with open("instances.txt", "w") as f:
    f.write("i-123\n")
    f.write("i-456\n")

# Read
with open("instances.txt", "r") as f:
    lines = f.readlines()

print(lines)  # ['i-123\n', 'i-456\n']
```

Modes:

* `"r"` read
* `"w"` write (truncate)
* `"a"` append
* `"b"` binary (e.g., `"rb"`)

**Exercise**

Create a file `regions.txt` with one region per line, read it into a list of regions, strip `\n`, and print.

**Solution:**

```python
with open("regions.txt", "r") as f:
    regions = [line.strip() for line in f]

print(regions)
```

---

## 4. Error handling (try/except)

You’ll use this a lot with network calls & AWS APIs.

```python
try:
    value = int("abc")  # ValueError
except ValueError as e:
    print("Conversion failed:", e)
```

Multiple excepts:

```python
try:
    with open("config.yaml") as f:
        content = f.read()
except FileNotFoundError:
    print("Config file not found")
except PermissionError:
    print("Not allowed to read config")
else:
    print("Read OK")
finally:
    print("Done (success or fail)")
```

With AWS:

```python
import boto3
from botocore.exceptions import ClientError

s3 = boto3.client("s3")

try:
    s3.head_bucket(Bucket="nonexistent-bucket-12345")
except ClientError as e:
    print("Bucket does not exist or access denied:", e)
```

**Exercise**

Write a function `safe_div(a, b)` that returns `a / b`, but if `b == 0` returns `None` and prints `"Division by zero!"`.

**Solution:**

```python
def safe_div(a: float, b: float) -> float | None:
    try:
        return a / b
    except ZeroDivisionError:
        print("Division by zero!")
        return None
```

---

## 5. Modules & virtual environments (venv)

### 5.1 Imports and your own modules

Assume you have a file `utils.py`:

```python
# utils.py
def format_instance(instance_id: str) -> str:
    return f"Instance: {instance_id}"
```

Use it in `main.py`:

```python
# main.py
from utils import format_instance

print(format_instance("i-123"))
```

---

### 5.2 Virtual environments (very important for Boto3, requests, etc.)

**Create venv (Linux/macOS):**

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install boto3 requests pyyaml
```

**Windows (PowerShell):**

```powershell
python -m venv .venv
.\.venv\Scripts\activate
pip install boto3 requests pyyaml
```

You’ll see `(.venv)` in your shell prompt. Now all `pip install` goes into this isolated environment.

Deactivate: `deactivate`.

---

## 6. OOP basics (classes, objects, methods)

Let’s model an EC2 instance in Python.

```python
class EC2Instance:
    def __init__(self, instance_id: str, instance_type: str, state: str):
        self.instance_id = instance_id
        self.instance_type = instance_type
        self.state = state

    def is_running(self) -> bool:
        return self.state == "running"

    def __repr__(self) -> str:
        return (f"EC2Instance(id={self.instance_id}, "
                f"type={self.instance_type}, state={self.state})")


inst = EC2Instance("i-123", "t3.micro", "running")
print(inst)
print("Running?", inst.is_running())
```

Later, you can create classes like `AwsInventory`, `AlarmManager`, etc. for your tools.

**Exercise**

Create a `S3Bucket` class with attributes `name`, `region`, `versioning_enabled` and a method `enable_versioning()` that sets the flag to `True`.

**Solution:**

```python
class S3Bucket:
    def __init__(self, name: str, region: str, versioning_enabled: bool = False):
        self.name = name
        self.region = region
        self.versioning_enabled = versioning_enabled

    def enable_versioning(self) -> None:
        self.versioning_enabled = True

    def __repr__(self) -> str:
        return (f"S3Bucket(name={self.name}, region={self.region}, "
                f"versioning={self.versioning_enabled})")
```

---

## 7. Working with JSON & YAML

### 7.1 JSON

Common for API responses and configs.

```python
import json

config = {
    "env": "prod",
    "regions": ["us-east-1", "us-west-2"],
    "thresholds": {"cpu": 80, "latency": 200},
}

# Write to file
with open("config.json", "w") as f:
    json.dump(config, f, indent=2)

# Read from file
with open("config.json", "r") as f:
    loaded = json.load(f)

print(loaded["regions"])
```

---

### 7.2 YAML

Friendlier for configs (e.g., pipeline configs, CloudFormation templates). Use `pyyaml`.

```bash
pip install pyyaml
```

```python
import yaml

config_yaml = """
env: prod
regions:
  - us-east-1
  - us-west-2
thresholds:
  cpu: 80
  latency: 200
"""

data = yaml.safe_load(config_yaml)
print(data["thresholds"]["cpu"])  # 80

# Dump to YAML string
print(yaml.safe_dump(data, sort_keys=False))
```

**Exercise**

* Create `aws_config.yaml` with:

  * env: dev
  * regions: [us-east-1, us-west-2]
  * services: [ec2, s3, iam]
* Write a Python script that reads this file and prints:
  `"Scanning dev for services: ec2, s3, iam"`

---

## 8. Calling REST APIs with `requests`

You’ll often hit internal services or external APIs.

Install:

```bash
pip install requests
```

Example: GET with query params

```python
import requests

response = requests.get(
    "https://httpbin.org/get",
    params={"env": "dev", "region": "us-east-1"},
    timeout=5
)

print("Status:", response.status_code)
data = response.json()
print("Args:", data["args"])
```

POST with JSON body:

```python
payload = {"name": "test-job", "env": "dev"}

response = requests.post(
    "https://httpbin.org/post",
    json=payload,
    timeout=5
)

print("Status:", response.status_code)
print("JSON:", response.json())
```

Error handling pattern:

```python
import requests

try:
    resp = requests.get("https://httpbin.org/status/500", timeout=5)
    resp.raise_for_status()
except requests.exceptions.HTTPError as e:
    print("HTTP error:", e)
except requests.exceptions.RequestException as e:
    print("Request failed:", e)
```

**Interview questions**

* How do you send query params?

  * `requests.get(url, params={"key": "value"})`
* How to send JSON body?

  * `requests.post(url, json={"a": 1})`

---

## 9. Boto3 basics (AWS automation)

> **IMPORTANT**: Only run creation code in a test account. Some calls incur cost.

### 9.1 Setup

1. Install:

   ```bash
   pip install boto3
   ```

2. Configure credentials (once):

   ```bash
   aws configure
   ```

   * Access key ID
   * Secret key
   * Default region
   * Output format (`json`)

Boto3 uses these credentials automatically.

---

### 9.2 S3: create/list buckets & objects

```python
import boto3

s3 = boto3.client("s3")

# List buckets
response = s3.list_buckets()
for b in response["Buckets"]:
    print("Bucket:", b["Name"])

# Create bucket (region-specific)
bucket_name = "tpk-dev-demo-bucket-123456"

s3.create_bucket(
    Bucket=bucket_name,
    CreateBucketConfiguration={"LocationConstraint": "us-west-2"},
)

# Upload object
s3.upload_file("config.json", bucket_name, "configs/config.json")
```

---

### 9.3 EC2: list & create instances

```python
import boto3

ec2 = boto3.client("ec2", region_name="us-west-2")

# List instances
resp = ec2.describe_instances()

for reservation in resp["Reservations"]:
    for instance in reservation["Instances"]:
        instance_id = instance["InstanceId"]
        state = instance["State"]["Name"]
        itype = instance["InstanceType"]
        print(instance_id, itype, state)
```

Launching an instance (be careful!):

```python
response = ec2.run_instances(
    ImageId="ami-xxxxxxxx",  # use a valid AMI
    InstanceType="t3.micro",
    MinCount=1,
    MaxCount=1,
    TagSpecifications=[
        {
            "ResourceType": "instance",
            "Tags": [{"Key": "Name", "Value": "demo-instance"}],
        }
    ],
)
```

---

### 9.4 IAM: create/list users/roles

**List IAM users:**

```python
import boto3

iam = boto3.client("iam")

resp = iam.list_users()
for user in resp["Users"]:
    print("User:", user["UserName"])
```

Creating IAM users/roles should be done carefully and usually via Terraform/CloudFormation, but you should know the basics:

```python
iam.create_user(UserName="demo-user")
```

(For interviews, explain you prefer IaC for repeatability, but can script via Boto3.)

---

### 9.5 CloudWatch: basic CPU alarm

Create an alarm on EC2 CPUUtilization:

```python
import boto3

cloudwatch = boto3.client("cloudwatch", region_name="us-west-2")

cloudwatch.put_metric_alarm(
    AlarmName="HighCPU-demo-instance",
    MetricName="CPUUtilization",
    Namespace="AWS/EC2",
    Statistic="Average",
    Period=300,
    EvaluationPeriods=1,
    Threshold=80.0,
    ComparisonOperator="GreaterThanThreshold",
    Dimensions=[
        {"Name": "InstanceId", "Value": "i-1234567890abcdef0"},
    ],
    AlarmActions=[
        # SNS topic ARN here, for notifications
        # "arn:aws:sns:us-west-2:123456789012:my-topic"
    ],
)
```

**Typical interview questions around Boto3:**

* How do you paginate results?

  * Use a paginator: `client.get_paginator("describe_instances")`
* How do you handle AWS errors?

  * Catch `botocore.exceptions.ClientError` and inspect `e.response["Error"]["Code"]`.

---

## 10. Mini-project tying it all together

### Project: AWS inventory & config-driven scan

**Goal:** Build a Python script that:

1. Reads configuration from `config.yaml`:

   * env
   * regions
   * services to scan (`ec2`, `s3`)
2. For each region:

   * List EC2 instances (IDs, type, state)
   * List S3 buckets (global; but you can just list once)
3. Write the result to `inventory.json`.

**config.yaml**

```yaml
env: dev
regions:
  - us-west-2
services:
  - ec2
  - s3
```

**inventory.py (skeleton)**

```python
import json
import yaml
import boto3
from typing import Any


def load_config(path: str) -> dict[str, Any]:
    with open(path, "r") as f:
        return yaml.safe_load(f)


def list_ec2(region: str) -> list[dict[str, Any]]:
    ec2 = boto3.client("ec2", region_name=region)
    instances_info: list[dict[str, Any]] = []

    paginator = ec2.get_paginator("describe_instances")
    for page in paginator.paginate():
        for reservation in page["Reservations"]:
            for inst in reservation["Instances"]:
                instances_info.append(
                    {
                        "id": inst["InstanceId"],
                        "type": inst["InstanceType"],
                        "state": inst["State"]["Name"],
                        "region": region,
                    }
                )
    return instances_info


def list_s3() -> list[dict[str, Any]]:
    s3 = boto3.client("s3")
    resp = s3.list_buckets()
    buckets = []
    for b in resp["Buckets"]:
        buckets.append({"name": b["Name"]})
    return buckets


def main() -> None:
    cfg = load_config("config.yaml")
    env = cfg["env"]
    regions = cfg["regions"]
    services = set(cfg["services"])

    inventory: dict[str, Any] = {
        "env": env,
        "regions": regions,
        "ec2": [],
        "s3": [],
    }

    if "ec2" in services:
        for region in regions:
            inventory["ec2"].extend(list_ec2(region))

    if "s3" in services:
        inventory["s3"] = list_s3()

    with open("inventory.json", "w") as f:
        json.dump(inventory, f, indent=2)

    print("Inventory written to inventory.json")


if __name__ == "__main__":
    main()
```

This single project uses:

* Variables, types, if/else, loops, functions
* Lists, dicts, sets
* File I/O
* Error handling (you can add try/except)
* Modules & venv (`yaml`, `boto3`)
* Basic structured code (`main`, helper functions)
* YAML + JSON
* Boto3 for EC2 & S3

---

## 11. Interview & work checklist for these topics

You should be able to confidently explain and/or write code for:

### Python Foundations

* Difference between list/dict/set/tuple and when to use each
* How `try/except/else/finally` works
* How to read/write files safely with `with open(...)`
* What a virtual environment is and why it’s important
* Basics of OOP: what is a class, object, method, `__init__`, `self`

### JSON/YAML & REST

* Load/dump JSON using `json` module
* Load/dump YAML using `pyyaml`
* Use `requests` to:

  * GET with query params
  * POST with JSON body
  * Handle errors

### Boto3 & AWS automation

* Configure credentials (`aws configure`)
* Use Boto3 clients for S3, EC2, IAM, CloudWatch:

  * List S3 buckets
  * List EC2 instances
  * Explain how you *would* create EC2, S3 buckets, IAM users, CloudWatch alarms
* Explain that for production infra you prefer **Terraform/CloudFormation**, but Boto3 is great for:

  * One-off tools
  * Automation scripts
  * Data/metrics collectors

---

If you’d like, in your **next message** you can:

* Paste any code you tried and I’ll review it like an interviewer, or
* Ask for a **mock interview** just focused on:
  Python basics + JSON/YAML + REST + Boto3, and I’ll rapid-fire questions and correct your answers.
