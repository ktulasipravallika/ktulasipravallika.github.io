### Metrics

  * Metrics represents what is happening.
  * These trigger the alerts.
  * Metrics → Alarms → SNS → On-call
  * Example: CPU %, Latency, Error Rate
     * **Latency:**
         * How long requests take
         * Example: p95 latency >2s
           
     * **Traffic:**
         * How much load system gets
         * RPS (Requests Per Second) drops suddenly.
           
     * **Errors:**
         * Failed requests
         * 5xx error rate > 2%
           
     * **Saturation:**
         * Resource exhaustion
         * CPU > 90%, disk full

### Dashboards

  * Dashboards are used for real-time incident monitoring and shift handover.
  * Dashboards → Visibility
  * Dashboards show: p95 latency, RPS, Error rate, Saturation.. etc metrics in a single view.
### Logs

  * Logs represents why did it happen.
  * Logs → Logs Insights → Root cause
  * Example: Applincation Logs, Error Logs
    
### Traces

  * Traces represent where did it happen.
  * Example: Request Flow Across services

**Note: Metrics tell me something is wrong, logs tell me why, and traces tell me where.**

#### Alerting

* Every alert should be actionable, urgent, and tied to customer impact.
**Threshold** 
  * Used in case of predictable resources. (CPU, disk)
  * Sets the Static limits
  * Example: CPU > 80% for 5 mins.
    
**Anomaly**
  * Used in case of traffic, latency, business metrics.
  * Sets the baseline deviation
  * Example: Traffic drops 70% suddenly.

### Typical Severity Model

* Sev-1	→ Customer impact	→ Immediate escalation
* Sev-2	→ Partial degradation	→ Fix during on-call
* Sev-3	→ Non-urgent	→ Ticket
* **Escalation Rules**
  * No acknowledgment → page next engineer.
  * No mitigation → escalate to owning team.
  * Always document actions.

##### Alarm Types

* Static threshold	→ CPU > 80%
* Anomaly detection	→ Traffic drop
* Log-based	→ Error pattern
* Composite	→ Deduplication


### Cloud Watch

##### Logs

* `CloudWatchAgentServerPolicy` Policy needs to be attached to make use of cloud watch logs.

* CloudWatch does NOT automatically read log files.
  
* The agent must be configured AND running.

*  ```
   #### Install agent
   sudo yum install -y amazon-cloudwatch-agent

   #### Run config wizard
   sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard

   #### Answer the log groups, stream and other details as prompted.
   
   #### Force start the agent
   
   sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl \
   -a fetch-config -m ec2 \
   -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s

   ```
   
*  ```
   Application writes log file
         ↓
   CloudWatch Agent reads the file
         ↓
   Agent sends logs to CloudWatch Logs
         ↓
   Logs appear in Log Group
         ↓
   Each instance = Log Stream
         ↓
   Query with Logs Insights
      
   ```

**Log Groups**: 
  * A log group is a folder that holds logs for one application or service.
  * Groups logs by application/service.
  * Controls retention (7 days, 30 days, etc.)
  * Used for permissions and queries.
    
**Log Streams**:
  * A log stream is a single source of logs inside a log group.
  * Usually one EC2 Instance, One Container, One Lambda Function.
  * Separates logs per instance.
  * Makes troubleshooting easier.
    
**Log Amomalies**:
  * Detects the unusual patterns in logs.
    
**Log Event**:
  * A log event is one line in a log.
    
**Log Insights**:
  * Logs Insights is a query engine for CloudWatch logs.
  * Used for faster logs search, Filter errors, Count occurrences, Correlate with alarms




































