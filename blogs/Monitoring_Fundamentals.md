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

  * Dashboards gives visibility.
  * Dashboards → Visibility
     
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





































