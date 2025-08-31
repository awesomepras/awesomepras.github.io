---
layout: page
title: ""
permalink: /security/
---

---
# Security Practices for Google Cloud DevOps

This page contains practice questions on security practices, including IAM, Binary Authorization, secret management, and VPC Service Controls for the Google Cloud Professional DevOps Engineer certification.

---

_A curated list of practice questions, with explanations, compiled during my study sessions. Credit: ChatGPT (GPT-5)._

> **Disclaimer:**  
> These practice questions are **original, ChatGPT-generated scenarios** based on the [Google Cloud documentation](https://cloud.google.com/) and the **exam guide**.  
> They are *not* actual exam questions. Sharing exam content verbatim violates Google’s NDA and policies.  
> The goal here is to help learners prepare with realistic, scenario-style problems.



## Key Points
- **Binary Authorization**: Enforces trusted image deployment with attestations, ensuring only verified builds deploy to GKE or Cloud Run.
- **Secret Management**: Use Secret Manager for secure storage and runtime access to credentials, avoiding hardcoding or source repo storage.
- **IAM Best Practices**: Follow least privilege by assigning minimal predefined roles (e.g., artifactregistry.writer, clouddeploy.approver).
- **VPC Service Controls**: Protect against data exfiltration in CI/CD by isolating private pools and restricting repo access.
- **Build Provenance**: Use Cloud Build with KMS and Workload Identity for secure, traceable attestations.

## Practice Questions

### Q1. Binary Authorization for GKE
You need to enforce that only images scanned and approved are deployed to GKE. Which tool helps you enforce this?  
A. Cloud Deploy Rollout Policies  
B. Binary Authorization  
C. Artifact Registry IAM  
D. Cloud Build Triggers  
✅ **Correct Answer: B**  
👉 Binary Authorization enforces deployment policies, requiring attestations before an image can be deployed.

### Q2. Provenance & Attestation
You want to ensure only artifacts that passed load testing are deployed to GKE with Binary Authorization. How should you configure the pipeline?  
A. Have QA engineer manually sign attestations  
B. Use Cloud Build to create an attestation with a KMS-managed key + Workload Identity after tests pass  
C. Store JSON keys as Kubernetes Secrets  
D. Let developers push directly to production  
✅ **Correct Answer: B**  
👉 The best practice is: Cloud Build generates attestation after passing load tests. Workload Identity + KMS key secure signing, no plain secrets. Binary Authorization validates attestation before deployment.

### Q3. Secret Handling in Cloud Build
In Cloud Build, what’s the recommended way to use secrets?  
A. Store them as environment variables in cloudbuild.yaml  
B. Retrieve them at runtime from Secret Manager  
C. Commit them to Git in encrypted form  
D. Store them as plaintext in Artifact Registry  
✅ **Correct Answer: B**  
👉 Google best practice: integrate Secret Manager with Cloud Build to fetch secrets securely at build time. Avoid embedding in YAML.

### Q4. Artifact Registry vs Container Registry
Why use Artifact Registry instead of Container Registry?  
A. It’s cheaper  
B. Supports multiple artifact formats (Docker, Maven, npm)  
C. Doesn’t require IAM  
D. Automatically scales clusters  
✅ **Correct Answer: B**  
👉 Artifact Registry is the modern replacement for Container Registry. It supports multi-format artifacts, regional repositories, and fine-grained IAM.

### Q5. Cloud Build Security
You need to restrict builds to only pull from private GitHub repos. What do you configure?  
A. Build triggers with IAM  
B. Service per repo  
C. VPC Service Controls perimeter  
D. Secret Manager  
✅ **Correct Answer: C**  
👉 Cloud Build with private repos → use VPC SC for data exfiltration protection.

### Q6. IAM Principle of Least Privilege
Best practice?  
A. Assign owner role  
B. Assign minimal predefined roles  
C. Always use custom roles  
D. Assign broad roles first  
✅ **Correct Answer: B**  
👉 Assigning minimal predefined roles follows the principle of least privilege.

### Q7. Secret Storage
Where should you store DB passwords?  
A. Secret Manager  
B. ConfigMap  
C. Source repo  
D. Cloud Storage  
✅ **Correct Answer: A**  
👉 Secret Manager is the secure choice for storing sensitive credentials like DB passwords.

### Q8. Build Credentials Management
What practice is recommended for managing build credentials?  
A. Hardcode secrets in build templates  
B. Store secrets in source repo  
C. Use Secret Manager and avoid hard-coding  
D. Use environment variables only  
✅ **Correct Answer: C**  
👉 Securely store credentials in Secret Manager.

### Q9. Private Build Pools Isolation
What security control should you configure when using private pools in Cloud Build to avoid data exfiltration?  
A. Disable authentication  
B. Assign broad IAM roles  
C. Enforce VPC Service Controls perimeter  
D. Expose build logs publicly  
✅ **Correct Answer: C**  
👉 Private pools, when used with VPC Service Controls, provide boundary protection for secure build environments.

### Q10. Workload Identity for Builds
Which is a best practice for synthetic access control during Cloud Build execution?  
A. Use the default Cloud Build service account exclusively  
B. Enable Workload Identity Federation for least-privilege access  
C. Run builds as root user  
D. Store keys in code repository  
✅ **Correct Answer: B**  
👉 Workload Identity allows you to apply least-privileged, secure identity to builds without long-lived service account keys.

### Q11. Policy Enforcement for Builds
To enforce container signing and provenance on build, you should incorporate:  
A. No policy management  
B. Binary Authorization tied with Cloud Build artifacts  
C. IAM only  
D. Pub/Sub triggers  
✅ **Correct Answer: B**  
👉 Using Binary Authorization ensures only signed, policy-compliant container images are allowed to deploy.

### Q12. Terraform State
Where to store Terraform state for teams?  
A. Cloud Storage bucket with locking  
B. Local disk  
C. Secret Manager  
D. Pub/Sub  
✅ **Correct Answer: A**  
👉 Cloud Storage with locking ensures safe, collaborative Terraform state management.

---
