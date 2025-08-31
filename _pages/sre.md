---
layout: page
permalink: /sre/
title: ""
---
---
# SRE Concepts for Google Cloud DevOps

This page contains practice questions related to Site Reliability Engineering (SRE) concepts, including SLOs, error budgets, DORA metrics, and incident management, tailored for the Google Cloud Professional DevOps Engineer certification.

---

_A curated list of practice questions, with explanations, compiled during my study sessions. Credit: ChatGPT (GPT-5)._

> **Disclaimer:**  
> These practice questions are **original, ChatGPT-generated scenarios** based on the [Google Cloud documentation](https://cloud.google.com/) and the **exam guide**.  
> They are *not* actual exam questions. Sharing exam content verbatim violates Google’s NDA and policies.  
> The goal here is to help learners prepare with realistic, scenario-style problems.



## Key Points
- **SLOs and Error Budgets**: Define acceptable downtime (e.g., 99.9% SLO = ~43 min/month downtime). Error budgets balance reliability and innovation.
- **DORA Metrics**: Focus on deployment frequency, lead time, MTTR, and change failure rate to measure DevOps performance.
- **SLIs**: Measurable indicators (e.g., request latency) form the basis for SLOs.
- **Alerting Best Practices**: Alerts should be actionable, tied to SLOs, and reduce toil; avoid noisy alerts like CPU spikes.
- **Incident Management**: Starts with detection and alerting, followed by response, remediation, and blameless postmortems.

## Practice Questions

### Q1. What is an SLO Error Budget?
You are designing an SLO with 99.9% availability. How much monthly downtime is allowed?  
A. ~4 min  
B. ~43 min  
C. ~8 hr  
D. ~7 hr  
✅ **Correct Answer: B**  
👉 99.9% → 0.1% downtime → ~43 min/month.

### Q2. Error Budget Policy
You have 99.99% SLO. How much downtime per month?  
A. ~43 min  
B. ~4.3 min  
C. ~7 hr  
D. 1 hr  
✅ **Correct Answer: B**  
👉 0.01% → ~4.3 min/month.

### Q3. DORA Metrics
Which of these is not part of the DORA metrics? 
A. System Availability  
B. Lead Time  
C. Deployment Frequency  
D. Change Failure Rate  
✅ **Correct Answer: A**  
👉 Availability is an SRE metric, not part of 4 DORA.

### Q4. SLI Example
Which is an SLI?  
A. SLO = 99.9% uptime  
B. Error budget 43 min  
C. Percentage of requests < 100 ms latency  
D. 99% uptime guarantee  
✅ **Correct Answer: C**  
👉 SLI = measurable indicator.

### Q5. SRE Alerting
Which is not a good alerting practice?  
A. Alerts only on SLO violation  
B. Alert on every CPU spike  
C. Alerts reduce toil  
D. Focus on actionable  
✅ **Correct Answer: B**  
👉 Alerting on every CPU spike increases noise and toil, not actionable.

### Q6. Error Budget Burn Rate
What’s the main use?  
A. Count errors  
B. Set IAM  
C. Create logs  
D. Detect if SLO is at risk early  
✅ **Correct Answer: D**  
👉 Burn rate monitors how quickly the error budget is consumed, indicating SLO risk.

### Q7. Incident Response
What’s the first step in incident management?  
A. Root cause analysis  
B. Remediation  
C. Detection & alerting  
D. Blameless postmortem  
✅ **Correct Answer: C**  
👉 Detection and alerting initiate the incident response process.

### Q8. Deployment Frequency (DORA)
You deploy daily. Which DORA metric is this?  
A. Deployment frequency  
B. Lead time  
C. MTTR  
D. Change failure rate  
✅ **Correct Answer: A**  
👉 Daily deployments reflect high deployment frequency, a DORA metric.

---