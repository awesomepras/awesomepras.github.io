---
layout: page
title: ""
permalink: /monitoring/
---
---

# Monitoring and Logging for Google Cloud DevOps

This page covers practice questions on Google Cloud Monitoring, Logging, metric scopes, and alerting policies, critical for the Google Cloud Professional DevOps Engineer certification.

---

_A curated list of practice questions, with explanations, compiled during my study sessions. Credit: ChatGPT (GPT-5)._

> **Disclaimer:**  
> These practice questions are **original, ChatGPT-generated scenarios** based on the [Google Cloud documentation](https://cloud.google.com/) and the **exam guide**.  
> They are *not* actual exam questions. Sharing exam content verbatim violates Google’s NDA and policies.  
> The goal here is to help learners prepare with realistic, scenario-style problems.


## Key Points
- **Cloud Logging**: Default retention is 30 days; export to Cloud Storage or BigQuery for longer retention (e.g., 1 year).
- **Aggregated Sinks**: Use org or folder-level sinks for compliance (e.g., audit logs to BigQuery). Ensure sink service accounts have proper IAM roles (e.g., storage.objectCreator).
- **Metrics**: GAUGE (snapshots, e.g., CPU %), CUMULATIVE (counters, e.g., bytes read), DELTA (interval changes, e.g., errors/min), DISTRIBUTION (histograms, e.g., latency percentiles).
- **Metric Scopes**: Allow centralized monitoring across projects in one org (up to 375 projects default). Scoping projects should be minimal for simplicity.
- **Alerting**: Use metric threshold conditions for alerts (e.g., CPU > 80%). App Hub provides app-centric views, and dashboards are shared via IAM.

## Practice Questions

### Q1. Audit Log Export
Your security team requires that all audit logs across every project in your organization be exported to a BigQuery dataset for compliance review. What should you do?  
A. Create a log sink in each project and export to the same BigQuery dataset  
B. Create an aggregated log sink at the organization level with a filter for audit logs, and export to BigQuery  
C. Create a log sink at the folder level for each business unit  
D. Configure VPC Service Controls to send logs to BigQuery automatically  
✅ **Correct Answer: B**  
👉 Compliance across all projects → always org-level aggregated sink. BigQuery is the correct destination for querying.

### Q2. IAM Role for Log Sink
You configured an aggregated log sink to export logs to Cloud Storage, but no logs are appearing. What is the most likely cause?  
A. Cloud Storage bucket retention is too short  
B. The aggregated log sink service account does not have roles/storage.objectCreator on the bucket  
C. Cloud Logging does not support aggregated sinks with GCS  
D. The aggregated sink must be created at the project level, not the organization level  
✅ **Correct Answer: B**  
👉 Always check IAM. The sink’s writer identity needs the correct role on the destination.

### Q3. Filtering Logs
You are asked to export only ERROR-level logs from all projects in a folder to Pub/Sub for real-time monitoring. What’s the best solution?  
A. Create a project-level sink in each project with a filter  
B. Create an aggregated log sink at the folder level with filter severity=ERROR, destination Pub/Sub  
C. Use Cloud Monitoring to export only error logs  
D. Create an aggregated sink at org level and filter by ERROR  
✅ **Correct Answer: B**  
👉 Folder scope + specific severity filter → folder-level aggregated sink is correct.

### Q4. Log Retention
By default, Cloud Logging retains logs for 30 days. Your team needs to store all logs for 1 year. What’s the most efficient solution?  
A. Create a Cloud Function to copy logs to BigQuery every day  
B. Extend Cloud Logging retention to 1 year  
C. Create an aggregated log sink to Cloud Storage, set bucket retention to 1 year  
D. Manually download logs each month  
✅ **Correct Answer: C**  
👉 Retention period in Cloud Logging cannot be arbitrarily extended; you must export logs to storage for longer retention.

### Q5. CPU Utilization Metric
CPU utilization (%) on a Compute Engine VM is:  
A. CUMULATIVE  
B. GAUGE  
C. DELTA  
D. DISTRIBUTION  
✅ **Correct Answer: B**  
👉 CPU utilization is an instantaneous value (snapshot at time). GAUGE fits.
❌ CUMULATIVE = counters.
❌ DELTA = interval changes.
❌ DISTRIBUTION = histograms.


### Q6. Disk Read Bytes Metric
The metric compute.googleapis.com/instance/disk/read_bytes_count is:  
A. GAUGE – DOUBLE  
B. CUMULATIVE – INT64  
C. GAUGE – INT64  
D. DISTRIBUTION – DOUBLE  
✅ **Correct Answer: B**  
👉 It’s a monotonically increasing counter of bytes read, stored as INT64.

### Q7. Latency Histogram Metric
Which value type does a latency histogram (p50, p95, p99) use?  
A. DOUBLE  
B. INT64  
C. STRING  
D. DISTRIBUTION  
✅ **Correct Answer: D**  
👉 Percentiles are derived from bucketed histograms → DISTRIBUTION type.

### Q8. Cumulative Metric Reset
What happens to a CUMULATIVE metric when a VM restarts?  
A. Continues counting  
B. Resets to zero  
C. Freezes  
D. Converts to GAUGE  
✅ **Correct Answer: B**  
👉 Counters reset on process/VM restart.

### Q9. Memory Usage Metric
What value type is used for memory usage in bytes?  
A. DOUBLE  
B. INT64  
C. STRING  
D. DISTRIBUTION  
✅ **Correct Answer: B**  
👉 Bytes = integer count (INT64).

### Q10. HTTP Request Counts
You are analyzing HTTP request counts for a Cloud Run service. Which metric kind applies?  
A. GAUGE  
B. CUMULATIVE  
C. DELTA  
D. DISTRIBUTION  
✅ **Correct Answer: B**  
👉 Request count increases over time (counter).

### Q11. Request Latency Metric
Which metric is most likely to be DISTRIBUTION?  
A. CPU utilization  
B. Network packets sent  
C. Request latency per percentile  
D. Request count  
✅ **Correct Answer: C**  
👉 Only latency requires bucketed histogram.

### Q12. Project Cost Metric
If you want to measure current cost ($) of a project, the Cloud Billing metric is:  
A. GAUGE – DOUBLE  
B. GAUGE – INT64  
C. CUMULATIVE – DOUBLE  
D. DELTA – DOUBLE  
✅ **Correct Answer: A**  
👉 Cost “now” is a snapshot, stored as floating-point currency.

### Q13. GAUGE Metrics
Which is true about GAUGE metrics?  
A. Only increase  
B. Reset on restart  
C. Snapshot at a point in time  
D. Store event counts  
✅ **Correct Answer: C**  
👉 GAUGE = snapshot, can go up or down.

### Q14. Network Bytes Metric
The metric instance/network/received_bytes_count is:  
A. GAUGE – DOUBLE  
B. CUMULATIVE – INT64  
C. GAUGE – INT64  
D. DISTRIBUTION – DOUBLE  
✅ **Correct Answer: B**  
👉 Byte counters are CUMULATIVE INT64.

### Q15. SLI Latency Metric
Which type of metric is required for Service Level Indicator (SLI) latency percentiles?  
A. GAUGE – DOUBLE  
B. GAUGE – DISTRIBUTION  
C. CUMULATIVE – INT64  
D. DELTA – DOUBLE  
✅ **Correct Answer: B**  
👉 Percentiles come from histograms → GAUGE DISTRIBUTION.

### Q16. Uptime Metric
Which metric kind is best suited to capture uptime in seconds?  
A. GAUGE  
B. CUMULATIVE  
C. DELTA  
D. DISTRIBUTION  
✅ **Correct Answer: B**  
👉 Uptime accumulates (counter).

### Q17. Failed Login Attempts
You want to measure number of failed login attempts over time. Which is correct?  
A. GAUGE – INT64  
B. CUMULATIVE – INT64  
C. GAUGE – DOUBLE  
D. DISTRIBUTION – INT64  
✅ **Correct Answer: B**  
👉 Failed login attempts are counted cumulatively.

### Q18. Rate Function for Metrics
For a CUMULATIVE metric, what must you often do in Metrics Explorer to see meaningful rates?  
A. Convert to GAUGE  
B. Apply a rate() function  
C. Apply percentile filter  
D. Multiply by 100  
✅ **Correct Answer: B**  
👉 rate() converts counters into per-second values.

### Q19. Percentage Metrics
Which value type is typically used for percentage values (0–100%)?  
A. INT64  
B. DOUBLE  
C. DISTRIBUTION  
D. STRING  
✅ **Correct Answer: B**  
👉 Percentages are fractional → DOUBLE.

### Q20. API Latency Metric
What kind of metric is API request latency average (ms)?  
A. GAUGE – DOUBLE  
B. CUMULATIVE – INT64  
C. GAUGE – DISTRIBUTION  
D. DELTA – DOUBLE  
✅ **Correct Answer: A**  
👉 Average latency = snapshot double.

### Q21. DELTA Metric Use
Which would be most appropriate to measure with DELTA?  
A. Instantaneous CPU utilization  
B. Number of errors in a 1-minute interval  
C. Total cost of project  
D. Uptime seconds  
✅ **Correct Answer: B**  
👉 Interval events → DELTA.

### Q22. Bytes Per Second Metric
The metric kind for "bytes read from disk per second" after applying a rate() is:  
A. GAUGE  
B. CUMULATIVE  
C. DELTA  
D. DISTRIBUTION  
✅ **Correct Answer: A**  
👉 rate() converts counters into per-second GAUGE values.

### Q23. Invalid Metric Type
Which is NOT a valid value type in GCP metrics?  
A. INT64  
B. DOUBLE  
C. STRING  
D. BOOLEAN  
✅ **Correct Answer: D**  
👉 GCP metric value types: INT64, DOUBLE, STRING, DISTRIBUTION. Boolean isn’t supported.

### Q24. Latency Distribution Metric
Which service metric often uses DISTRIBUTION type to store request time buckets?  
A. Cloud Logging  
B. Cloud Monitoring  
C. Cloud Run / GKE request latency  
D. BigQuery query counts  
✅ **Correct Answer: C**  
👉 Latency metrics → DISTRIBUTION.

### Q25. CUMULATIVE vs DELTA
What is the difference between CUMULATIVE and DELTA metrics?  
A. Snapshots  
B. CUMULATIVE never resets  
C. CUMULATIVE = since start, DELTA = per interval  
D. DELTA more accurate  
✅ **Correct Answer: C**  
👉 CUMULATIVE is monotonically increasing, DELTA is interval change.

### Q26. Default Metric Kind
Which is the default metric kind when creates system metrics (like CPU, memory)?  
A. GAUGE  
B. CUMULATIVE  
C. DELTA  
D. DISTRIBUTION  
✅ **Correct Answer: A**  
👉 System metrics are snapshots (e.g., CPU %, memory).

### Q27. IAM for GKE Monitoring
You want GKE metrics to be visible in Cloud Monitoring. Which role is needed?  
A. Monitoring Admin  
B. Monitoring Metric Writer  
C. Monitoring Viewer  
D. Logging Admin  
✅ **Correct Answer: B**  
👉 GKE writes metrics → needs roles/monitoring.metricWriter.

### Q28. Aggregated Log Sinks Scopes
Which scopes support aggregated sinks?  
A. Project only  
B. Organization, folder, billing account  
C. Service account  
D. GCS  
✅ **Correct Answer: B**  
👉 Aggregated sinks can be at org, folder, billing account levels.

### Q29. Alerting Policies
You want to alert if CPU > 80% for 5 min. Which condition type?  
A. Rate  
B. Ratio  
C. Metric threshold  
D. Log-based  
✅ **Correct Answer: C**  
👉 Standard CPU utilization alert → metric threshold condition.

### Q30. Service Monitoring
You want an app-centric view. Which tool?  
A. Logs Explorer  
B. App Hub  
C. Cloud Storage  
D. Pub/Sub  
✅ **Correct Answer: B**  
👉 App Hub provides an application-centric view for monitoring.

### Q31. Monitoring Dashboards
How do you share dashboards org-wide?  
A. Use IAM roles + Monitoring dashboards  
B. Export JSON  
C. Screenshots  
D. Export to BigQuery  
✅ **Correct Answer: A**  
👉 IAM roles control access to dashboards for org-wide sharing.

### Q32. Metric Scope Definition
What is a Metric Scope?  
A. A list of metric descriptors your project can create  
B. The time range for which metrics are retained  
C. A construct defining which projects’ time-series data your project can chart and monitor  
D. A logging configuration for monitoring tools  
✅ **Correct Answer: C**  
👉 A metric scope determines which projects' metrics your selected (scoping) project can access and visualize.

### Q33. Scoping Project
What is a Scoping Project?  
A. A project used solely for storing logs  
B. The project whose metric scope includes other projects and where dashboards, alerts, and groups are stored  
C. Any project that is included in a metric scope  
D. A project dedicated to API management  
✅ **Correct Answer: B**  
👉 The scoping project hosts a metric scope and contains configurations like alerting policies, dashboards, uptime checks, and monitoring groups.

### Q34. Metric Scope Membership
A project can be added to:  
A. Multiple metric scopes at once  
B. Only one metric scope at a time  
C. Either zero or multiple metric scopes  
D. None of the above  
✅ **Correct Answer: B**  
👉 Projects belong to exactly one metric scope.

### Q35. Multi-Project Monitoring
You want a central SRE team to monitor CPU usage across 10 projects. What should you do?  
A. Create 10 monitoring workspaces  
B. Export metrics to BigQuery  
C. Add all 10 projects into the metric scope of a central monitoring workspace  
D. Enable aggregated logging sinks  
✅ **Correct Answer: C**  
👉 Metric scope lets one workspace monitor multiple projects.

### Q36. Org-wide Monitoring
Can a monitoring workspace span projects across two different organizations?  
A. Yes, with aggregated metric scopes  
B. Yes, if you enable org-level APIs  
C. No, metric scope is limited to one org  
D. Only with BigQuery export  
✅ **Correct Answer: C**  
👉 Metric scopes are limited to a single org.

### Q37. Metric Scope Permissions
To modify a metric scope via the API, you need:  
A. Monitoring Viewer (roles/monitoring.viewer) only  
B. Monitoring Editor (roles/monitoring.editor) only  
C. Monitoring Admin (roles/monitoring.admin) or permission monitoring.metricsScopes.link  
D. BigQuery Admin  
✅ **Correct Answer: C**  
👉 Modifying metric scopes via API or console requires roles/monitoring.admin or permission monitoring.metricsScopes.link.

### Q38. VPC Service Controls Impact
If you enable VPC Service Controls after creating a metric scope, what’s the impact?  
A. Nothing changes; access remains the same  
B. Projects outside the perimeter will still be visible without restrictions  
C. The projects remain accessible even if they’re not in the same VPC perimeter  
D. Perimeter checks do not block existing scoped projects  
✅ **Correct Answer: D**  
👉 Creating the metric scope before establishing perimeter allows continued access, even if projects are in different perimeters.

### Q39. Metric Scope Quota
What is the default maximum number of monitored projects in a single metric scope?  
A. 100  
B. 375  
C. 500  
D. Unlimited  
✅ **Correct Answer: B**  
👉 Monitoring provides a default quota of 375 projects per metric scope, though higher quotas can be requested.

### Q40. Removing Project from Metric Scope
What happens when removing a project from a metric scope?  
A. Deletes all its dashboards and alerts  
B. Immediately stops its metrics from being charted, but dashboards remain configured  
C. Alerts continue but charts fail  
D. Disallows chart editing altogether  
✅ **Correct Answer: B**  
👉 Time-series data stops appearing, but dashboard and alert configurations—though orphaned—remain.

### Q41. App-enabled Folders
When using App Hub with app-enabled folders, what happens to metric scopes?  
A. You must manually manage all projects  
B. Google automatically syncs folder projects to the metric scope until the quota is exceeded  
C. Metric scopes are disabled in this scenario  
D. Metrics are only visible in BigQuery  
✅ **Correct Answer: B**  
👉 For app-enabled folders, Cloud Observability syncs projects into the metric scope automatically unless quota limits are reached.

### Q42. Scoping Project Best Practice
For a clean and clear metrics setup, your scoping project should ideally:  
A. Contain lots of resources to test performance  
B. Be empty or only serve as a monitoring project  
C. Contain all development and production VMs  
D. Only store logs  
✅ **Correct Answer: B**  
👉 It’s recommended that scoping projects have minimal resources to simplify setup and reduce configuration errors.

### Q43. 
Which combination is correct for compute.googleapis.com/instance/cpu/utilization?
A. ✅ GAUGE – DOUBLE
B. GAUGE – INT64
C. CUMULATIVE – DOUBLE
D. DELTA – DOUBLE

👉 Explanation: CPU utilization is percentage → GAUGE DOUBLE.

### Q44.
You need to export ERROR logs from all projects in a folder to Pub/Sub.
A. Create project-level sinks in each project.
B. Create an aggregated sink at folder level with severity=ERROR.
C. Export logs via Monitoring.
D. Org-level sink with ERROR filter.

✅ Correct Answer: B
👉 Folder-scope requirement → folder-level aggregated sink is correct.

### Q45.Log Buckets

Which statement is correct?
A. Logs must always stay in same project.
B. Logs can be routed to log buckets in any project in same org.
C. Logs cannot be routed.
D. Export only to BigQuery.

✅ Correct Answer: B
👉 Cross-project routing allowed within same org.


### Q46. 
 How Many Metric Scopes Can a Project Belong To?

A single project can be included in:
A. Multiple metric scopes at once.
B. Only one metric scope at a time.
C. An unlimited number of metric scopes.
D. Zero only.

✅ Correct Answer: B
Explanation: A monitored project can belong to exactly one metric scope at a time. 

### Q47.
What Permission Is Required to Configure Metric Scope via API?

To modify a metric scope via the API, you need:
A. Monitoring Viewer (roles/monitoring.viewer) only.
B. Monitoring Editor (roles/monitoring.editor) only.
C. Monitoring Admin (roles/monitoring.admin) or permission monitoring.metricsScopes.link.
D. BigQuery Admin.

✅ Correct Answer: C
Explanation: Modifying metric scopes via API or console requires roles/monitoring.admin or permission monitoring.metricsScopes.link. 


...