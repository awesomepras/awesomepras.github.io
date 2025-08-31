---
layout: default
title: Google Cloud Certified - Professional Cloud DevOps Engineer – Exam Prep
---
![Image description](/assets/images/pdevopse_cert.png)

# Google Cloud Certified - Professional Cloud DevOps Engineer – Exam Prep

## Overview

There’s plenty of information available on the structure of the Google Cloud Professional DevOps Engineer exam, so this guide focuses on study strategies, resources, and practical advice for effective preparation.

My feedback on Skillboost track for Devops:
After attempting the  exam I felt that all the skillboost courses are not necessary to pass the exam. A thorough and effective preparation with google documentation focussing areas from google exam blueprint is sufficient to pass this exam. I utlitized ChatGPT and perplexity.ai to strengthen my knowledge for every topic by creating self assessment. This is just my opinion as i have gone through few other google exams so have a solid understanding of lot of areas in google services. I felt that this exam is easier than Google Associate cloud Engineer exam due to the amount of topics/services covered. I still believe that ACE should be made pre-requisite to take any  google cloud professional exams.

### Exam Day Tips

I took the exam in the exam center.  
I finished the exam in  less than 1 hour. Since i marked about 15 questions to review I went back to eliminate the most obvious answers and choose the closest one. In the end i was not sure of 3 questions which I felt is good enough to pass. The answer choices were not tricky.

The Exam browser interface in the test center has "back - next and submit exam" buttons next to each other, make sure you dont click submit exam button. Dont worry, there is a prompt to confirm you are "Submitting the exam".

To review the questions , there is a button to "Review Marked, which also shows all question numbers hyperlinked" so you can go back and forth  
No notepad or white paper is allowed, so practice mental note-taking or use mental visualization to remember key points.  

---

## Courses (Optional)

- **CloudSkills Boost DevOps/SRE Track**  
  [cloudskillsboost.google/paths/20](https://www.cloudskillsboost.google/paths/20)
- **Coursera: Developing a Google SRE Culture**  
  [coursera.org/learn/developing-a-google-sre-culture](https://www.coursera.org/learn/developing-a-google-sre-culture)

> *SRE books are often recommended, but the above course suffices for exam prep. Notes on SRE appear below.*

---

## Core Focus Areas

### 1. Bootstrap & Maintain Google Cloud Organizations

- Understand org structure and resource management:  
```Org > Folder > Project > Resources```
- Key policies:
- Restrict service account key creation
- Allow/deny policies, and where to apply them

> *Best practices involve using folders for teams/projects and managing resources with the correct organizational policies.*

Understand what AppHub is and how resources are organized.

---

### 2. Building and Implementing CI/CD Pipelines

- Study Cloud Build, Artifact Registry, deployment automation.
- Know private worker pools, scan attestation, provenance.
- Artifact Registry vs Container Registry, deployment stages, rollback methods.
- How cloud builds can made faster, how rollback and outage(downtime) affect SLA , how to mitigate using google SRE principles. (Almost every question will say how will you... using google SRE recommended practice)

#### Key Exam Concepts

1. **Build Performance Optimization**
  - Use `--cache-from` for cached Docker images.
  - Cloud Storage cache for build outputs.
  - Separate build/runtime stages for smaller images.

2. **Customizing Compute Resources**
  - Increase vCPU with `--machine-type`.
  - Private pools can use high-CPU machines (higher startup latency).

3. **Security & Assurance**
  - Required SLSA level 1 automation and SLSA level 3 provenance.
  - Ephemeral builds, least privilege, Secret Manager, org policy restrictions.
  - VPC Service Controls for private pools.

4. **CI/CD Triggers & Workflow**
  - Cloud Build triggers on Git push/PR for CI automation.

> *Know how to configure triggers, integrate secrets, and implement blue/green & canary deployments.*

#### Useful Documentation

- [Cloud Run Revisions](https://cloud.google.com/run/docs/rollouts-rollbacks-traffic-migration)
  - New revision per deploy; split traffic; use tags for direct routing.
- [Traffic Management](https://cloud.google.com/run/docs/rollouts-rollbacks-traffic-migration)
  - Split traffic for canary releases.
- [Managing Tags](https://cloud.google.com/run/docs/rollouts-rollbacks-traffic-migration)
  - Use tags for blue/green deployments.

---

### 3. Site Reliability Engineering (SRE) Practices

- Apply SLOs, SLIs, SLAs, error budgets, incident frameworks.

#### Notes

***

| **Topic**                  | **Exam-Focused Insight**                                                                |
| -------------------------- | --------------------------------------------------------------------------------------- |
| **SLO Setting**            | Set SLO just below current reliability levels to balance user satisfaction and realism. |
| **Low Error Budget Usage** | If <5% used and SLO good, tighten SLO and accelerate releases.                          |
| **Error Budget Breach**    | Freeze launches; don’t borrow or escalate.                                              |
| **Error Budget Math**      | Divide minutes in window by 1,000 for 99.9% (or 10,000 for 99.99%).                     |

*** 


### 4. Implementing Observability (Monitoring & Logging)
Dont attempt the exam without knowing this topic thoroughly. You will need to understand how to utlize monitoring for GKE, Cloud Run, Network, Export logs to different destinations, Dashboard creation on projects, log sinks. 

Identify use cases for Cloud Trace, Profiler and Debugger. You may need to read the introduction on Cloud Tasks and scheduling.

#### Exam Hints

- **Aggregated log sink**: Centralized export (compliance/audit/security).
- **IAM Gotchas**: Sink service account must have writer role.
- **Scope Keywords**:  
    Organization → org-level sink,  
    Folder → folder-level sink,  
    Project → project-level sink.  
- **Destinations**: 
  - Compliance → BigQuery
  - Long-term → GCS
  - Real-time → Pub/Sub
  
  Exam traps: Forgetting IAM, confusing retention vs export, assuming project sinks cover all logs (they don’t).
---

### 5. Security & IAM

- Few questions here; since I had prior Google security engineering certification, it was not too hard to answer the questions.

---

### 6. Networking (VPC, Firewalls, Hybrid Connectivity)

- Load balancer logging questions (not complicated).
- VPCSC effect on CloudBuild, CloudRun.

---

### Additional Notes for SRE Topics

#### Categories of People

- **Critic**: Passionate and energetic, don't ignore their fears.
- **Navigator**: Success drivers, make them champions.
- **Bystander**: Unaware, communicate to gauge feelings.
- **Victim**: Take change personally, need to vent.

#### 5 Steps of Design Thinking

1. Empathize  
2. Define  
3. Ideate  
4. Prototype  
5. Test  

> Change is best delivered in small and frequent increments.

#### Types of Bias

- **Affinity Bias**: Like attracts like.
- **Confirmation Bias**: Seek confirming data.
- **Selective Attention Bias**: Focus on familiar ideas/sources.
- **Labeling Bias**: Judge based on appearance.

#### Incident Response Roles

- **Incident Commander (IC)**
- **Communications Lead (CL)**
- **Ops Lead (OL)**

> IC commands and coordinates, delegates roles, communicates, and keeps control.

#### MTTR vs MTBF

- **MTBF**: `Total uptime / # of failures`
- **MTTR**: `Total downtime / # of failures`

---

### Metric Kinds & Value Types

#### Metric Kinds

- **GAUGE**: Snapshot at a moment (CPU %)
- **CUMULATIVE**: Increases, resets on restart (bytes sent)
- **DELTA**: Value per window (requests/minute)

#### Value Types

- **INT64**: Counts (requests)
- **DOUBLE**: Percentages/ratios (CPU %)
- **DISTRIBUTION**: Histogram (latency buckets)
- **STRING**: Rare

#### Example Metrics Table

| **Metric (Service Example)**                                   | **Metric Kind** | **Value Type** | **Notes (Exam tips)**                                  |
| -------------------------------------------------------------- | --------------- | -------------- | ------------------------------------------------------ |
| **CPU Utilization %** (Compute Engine, GKE, Cloud Run)         | **GAUGE**  (snapshot)     | DOUBLE  (ratio/percentages)       | Snapshot in time, always 0–100.                        |
| **Memory Usage (bytes)**                                       | **GAUGE**  (snapshot)     | INT64   (count)       | Point-in-time value.                                   |
| **Disk I/O (bytes read/written)**                              | **CUMULATIVE** (increases only) | INT64  (count)        | Must convert to rate (bytes/sec).                      |
| **Network Packets Sent/Received**                              | **CUMULATIVE** (increases only) | INT64  (count)        | Reset on VM restart.                                   |
| **Request Count (e.g., HTTP 2xx/5xx in Cloud Run / GKE / LB)** | **CUMULATIVE** (increases only)  | INT64  (count)        | Increments over time, reset on restart.                |
| **Error Count**                                                | **CUMULATIVE**  (increases only) | INT64  (count)        | Same as requests, just filtered to errors.             |
| **Request Latency (avg/mean)**                                 | **GAUGE**    (Snapshot)   | DOUBLE  (ratio/percentage)       | Represents snapshot of average latency at that moment. |
| **Request Latency (distribution)**                             | **GAUGE**       | DISTRIBUTION (histogram)  | Needed for percentiles (p50, p95, p99).                |
| **Process Uptime**                                             | **CUMULATIVE**  | INT64          | Seconds since process started.                         |
| **Billing/Cost Metric** (Cloud Billing export)                 | **GAUGE**       | DOUBLE         | Snapshot cost values.                                  |

---

## Useful Links

1. [Monitoring IAM Roles](https://cloud.google.com/monitoring/access-control#mon_roles_desc)
2. [Logging IAM Considerations](https://cloud.google.com/logging/docs/access-control#considerations)
3. [Complete Guide: Cloud Build, Cloud Deployment Manager, Cloud Source](https://medium.com/@williamwarley/a-complete-guide-to-gcp-cloud-build-cloud-deployment-manager-operations-cloud-source-d9226200ed9f)
4. [GCP Exam Notes (Google Drive)](https://drive.google.com/file/d/1cCCTwulZuSBa4XmEh9bGzEwotaaOz9Wt/view?pli=1)
5. [Preparing for the Cloud DevOps Engineer Exam](https://medium.com/google-cloud/preparing-for-the-google-cloud-professional-cloud-devops-engineer-exam-30e9d5fe07e4)
6. [How to Pass the Google Professional Cloud DevOps Exam](https://medium.com/google-cloud/how-to-pass-the-google-professional-cloud-devops-exam-fc8754af0203)
7. [Certification Guide](https://jinaldesai.com/google-professional-cloud-devops-engineer-certification-guide/)
8. [SatishVJ's repo (outdated)](https://github.com/sathishvj/awesome-gcp-certifications/blob/master/professional-cloud-devops-engineer.md)

---

## MATH on SLO

For common “three nines” use:

- **99.9%**: minutes ÷ 1,000
- **99.99%**: minutes ÷ 10,000

#### Minute Counts

- Day: 1,440
- Week: 10,080
- 30-day month: 43,200
- 31-day month: 44,640
- Year: 525,600

#### Examples

- Month (30 days):  
    - 99.9% ⇒ `43,200 ÷ 1,000 = 43.2` min  
    - 99.99% ⇒ `43,200 ÷ 10,000 = 4.32` min
- Week:  
    - 99.9% ⇒ `10,080 ÷ 1,000 = 10.08` min  
    - 99.99% ⇒ `10,080 ÷ 10,000 = 1.008` min
- Day:  
    - 99.9% ⇒ `1,440 ÷ 1,000 = 1.44` min  
    - 99.99% ⇒ `1,440 ÷ 10,000 = 0.144` min
- Year:  
    - 99.9% ⇒ `525,600 ÷ 1,000 = 525.6` min  
    - 99.99% ⇒ `525,600 ÷ 10,000 = 52.56` min

##### Other handy examples (30-day month):

- 99.95% ⇒ `43,200 × 0.0005 = 21.6` min
- 99.5% ⇒ `43,200 × 0.005 = 216` min
- 99% ⇒ `43,200 × 0.01 = 432` min

> *Exam tip: If the window isn’t specified, assume 30-day month. Divide by 1,000/10,000 for 99.9/99.99%.*

---
_Sources: ChatGPT, Perplexity.ai