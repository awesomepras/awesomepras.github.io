---
layout: page
title: ""
permalink: /practice-questions/
---

---

# Scenario-Based misc Practice Questions

This page contains scenario-based practice questions for the Google Cloud Professional DevOps Engineer certification, covering CI/CD, Cloud Build, Cloud Deploy, and other practical scenarios.

---

_A curated list of practice questions, with explanations, compiled during my study sessions. Credit: ChatGPT (GPT-5)._

> **Disclaimer:**  
> These practice questions are **original, ChatGPT-generated scenarios** based on the [Google Cloud documentation](https://cloud.google.com/) and the **exam guide**.  
> They are *not* actual exam questions. Sharing exam content verbatim violates Google’s NDA and policies.  
> The goal here is to help learners prepare with realistic, scenario-style problems.


## Key Points
- **Scenario-Based Approach**: Exam questions often present real-world scenarios requiring practical application of CI/CD, security, and monitoring concepts.
- **Cloud Build Integration**: Supports multi-cloud and hybrid setups, with secure artifact management and optimized build strategies.
- **Cloud Deploy**: Orchestrates multi-environment deployments with rollback and approval mechanisms.
- **Security in CI/CD**: Emphasize Secret Manager, Binary Authorization, and Workload Identity for secure pipelines.
- **Cost and Performance**: Optimize builds with caching, right-sizing resources, and efficient triggers.

## Practice Questions

### Q1. Cloud Build & Secret Rotation
Your application runs on Cloud Run and requires a password rotated every 24 hours with zero downtime. What’s the best deployment strategy?  
A. Use Cloud Build to bake the password into the container  
B. Store the rotated password in Secret Manager and mount it as a volume  
C. Use Secret Manager and refresh the secret via environment variables  
D. Hard-code the password and rebuild daily  
✅ **Correct Answer: B**  
👉 Mounting secrets as volumes from Secret Manager ensures zero downtime and automatic refresh. (env variables will expose secrets in logs)

### Q2. Attestation for Supply Chain Security
Your organization demands verifiable build provenance so production deployment only uses authorized builds. What should you implement?  
A. Artifact Registry alone  
B. Cloud Build with Binary Authorization and attestations  
C. Local builds and manual approval  
D. Cloud Deploy without provenance checks  
✅ **Correct Answer: B**  
👉 Binary Authorization with attestations ensures only trusted, verifiable builds are deployed.

### Q3. Caching Docker Builds
Your team complains about slow Docker builds in Cloud Build. What change best speeds up builds?  
A. Add --cache-from referencing Artifact Registry and optimize Dockerfile layering (less modified files early)  
B. Use Cloud Storage as cache and place frequently modified files early  
C. Always use latest tags; rely on default Dockerfile  
D. Remove multi-stage builds for simplicity  
✅ **Correct Answer: A**  
👉 --cache-from plus optimized Dockerfile layering allows efficient reuse of cached layers.

### Q4. Artifacts & Multi-Cloud CI/CD
You deliver artifacts to both GCP and AWS. How should Cloud Build handle storage and access across clouds securely?  
A. Store in GCR only  
B. Push to Artifact Registry and use Cloud Build to replicate to AWS securely  
C. Manually download and upload during deploy  
D. Store in Cloud Storage and manually transfer  
✅ **Correct Answer: B**  
👉 Artifact Registry supports multi-cloud artifact sharing and grants secure access via IAM.

### Q5. CI Trigger Management at Scale
Your enterprise has dozens of microservices in separate repos. You need a scalable CI solution in GCP. What’s best?  
A. Manually create Cloud Build triggers per repo  
B. Use Terraform/Deployment Manager to provision build triggers and pipeline templates  
C. Poll repos externally  
D. Use local Jenkins for triggers  
✅ **Correct Answer: B**  
👉 IaC ensures repeatable, consistent build trigger definitions at scale.

### Q6. Workload Identity for Builds
Your Cloud Build needs to push images to Artifact Registry with least-privilege access. Which approach is best?  
A. Provide Owner role on project  
B. Use default service account with broad permissions  
C. Use Workload Identity to grant minimal push permissions  
D. Embed credentials in build config  
✅ **Correct Answer: C**  
👉 Workload Identity avoids key management and enforces least privilege practices.

### Q7. Build in Private VPC
Your build needs access to internal resources through a private VPC (no public internet). How do you configure this?  
A. Build on public Cloud Build pool  
B. Use private Cloud Build worker pools within your VPC  
C. Use Jenkins on VM  
D. Expose internal resources publicly temporarily  
✅ **Correct Answer: B**  
👉 Private worker pools inside your VPC enable build access while maintaining network isolation.

### Q8. Cloud Deploy Pipeline Setup
You’re configuring a secure multi-stage deployment (dev → staging → prod). What resource defines this path?  
A. Cloud Build trigger  
B. Cloud Deploy delivery pipeline  
C. Artifact Registry tag policy  
D. Kubernetes deployment YAML  
✅ **Correct Answer: B**  
👉 Delivery pipeline orchestrates releases across environmental stages.

### Q9. Releasing with Skaffold
How does Cloud Deploy use Skaffold in a delivery pipeline?  
A. Skaffold builds the container images only  
B. Skaffold defines rendering and deployment logic  
C. Skaffold manages approval gates  
D. Skaffold is not supported  
✅ **Correct Answer: B**  
👉 Skaffold config drives manifest rendering and deploy steps in Cloud Deploy pipelines.

### Q10. Manual Approval Gate
Your production deployment policy requires human approval before rollout. Which feature supports that?  
A. IAM admin only  
B. Cloud Build approvals  
C. Cloud Deploy approvals  
D. Skaffold profile  
✅ **Correct Answer: C**  
👉 Cloud Deploy allows configuration of approval gates before promotion to production.

### Q11. Rollback Strategy
A rollout fails in staging. What can Cloud Deploy do to recover?  
A. Delete the release  
B. Wait and retry deployment with same release  
C. Initiate rollback to previously successful rollout  
D. Abort pipeline; no recovery possible  
✅ **Correct Answer: C**  
👉 Cloud Deploy supports retry or rollback to previous successful release.

### Q12. Traceable Build Provenance
Your security team requires build traceability for compliance. What do you enable?  
A. Plain Cloud Build logs  
B. Build provenance metadata and attestations  
C. Manual build tagging  
D. Dockerfile comments  
✅ **Correct Answer: B**  
👉 Provenance with metadata ensures traceable, audit-ready build info.

### Q13. Hybrid Deployment via Anthos
You need CI/CD that spans on-prem and GKE. Which approach is best?  
A. Separate unrelated pipelines  
B. Use Cloud Deploy with Anthos target clusters  
C. Export and import artifacts manually  
D. Use only Jenkins on-prem  
✅ **Correct Answer: B**  
👉 Cloud Deploy integrates with Anthos, allowing consistent pipelines across environments.

### Q14. Secrets in CI/CD
Sensitive credentials are needed during deployment. Where should you store them?  
A. In source code  
B. As environment vars in build config  
C. Secret Manager with secure injection  
D. In external Git file  
✅ **Correct Answer: C**  
👉 Secret Manager is secure and integrates with Cloud Build and Cloud Deploy.

### Q15. Artifactory vs Artifact Registry
Your pipeline uses Artifact Registry heavily. Which role is essential for Cloud Build to push artifacts?  
A. Storage Admin  
B. Artifact Registry Writer  
C. Owner  
D. Monitoring Admin  
✅ **Correct Answer: B**  
👉 roles/artifactregistry.writer gives precise push access while enforcing least privilege.

### Q16. Multi-Cloud Workload Execution
You want build steps to deploy to AWS EKS after building. How?  
A. Not possible  
B. Use Cloud Build steps invoking AWS CLI  
C. Manually download image  
D. Use GCP-only tools  
✅ **Correct Answer: B**  
👉 Cloud Build can orchestrate multi-cloud CD by invoking AWS commands.

### Q17. Build Cost Efficiency
Your builds are slow and expensive. What combination helps optimize performance and cost?  
A. Smaller machine + no caching  
B. Cache layers + optimized VM size + efficient triggers  
C. No artifact retention  
D. Unlimited concurrent runs  
✅ **Correct Answer: B**  
👉 Caching, right-sizing builds, and efficient triggering reduce cost and latency.

### Q18. Artifact Signing and Trust
Your deployment system must ensure only signed images deploy. What do you enable?  
A. Ignore signing  
B. Binary Authorization with attestation  
C. Manual review logs  
D. Local signature in Docker  
✅ **Correct Answer: B**  
👉 Binary Authorization enforces trust policy on container artifacts.

### Q19. Handling Build Failures
A build in Cloud Build fails. How can the pipeline ensure rollback?  
A. Cloud Deploy automatically resets  
B. Cloud Build aborts deployment  
C. Cloud Deploy doesn't proceed to rollout  
D. Nothing happens; manual cleanup needed  
✅ **Correct Answer: C**  
👉 Cloud Deploy will not continue rollout if Cloud Build fails, protecting production.

### Q20. Full CI/CD Lifecycle Trace
Your compliance policy states every deploy must show full lineage (source → build → deploy). You should implement:  
A. Source control logs only  
B. Build logs only  
C. End-to-end provenance via Cloud Build, Artifact Registry, attestations, and Cloud Deploy  
D. Manual spreadsheet tracking  
✅ **Correct Answer: C**  
👉 Full traceability requires coordinated metadata across CI and CD systems.

### Q21. Deployment Strategy
Which reduces risk by gradually shifting traffic?  
A. Canary  
B. Rolling restart  
C. Blue-green  
D. A/B test  
✅ **Correct Answer: A**  
👉 Canary deployments gradually shift traffic to minimize risk.

### Q22. CI/CD Caching
Which improves build performance?  
A. Cloud Run  
B. Cloud Build caching  
C. Pub/Sub  
D. BigQuery  
✅ **Correct Answer: B**  
👉 Caching in Cloud Build (e.g., --cache-from) improves build performance.

### Q23. GKE Upgrade
Which reduces downtime during GKE upgrades?  
A. Surge upgrades  
B. Blue-green clusters  
C. Manual node upgrade  
D. In-place upgrade  
✅ **Correct Answer: A**  
👉 Surge upgrades minimize downtime by adding new nodes before removing old ones.

---
