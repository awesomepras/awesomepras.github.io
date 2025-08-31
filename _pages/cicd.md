---
layout: page
title: ""
permalink: /cicd/
---
---

# CI/CD Practices for Google Cloud DevOps

This page includes practice questions on Continuous Integration and Continuous Deployment (CI/CD) practices, focusing on Google Cloud tools like Cloud Build, Cloud Deploy, and Artifact Registry.

---

_A curated list of practice questions, with explanations, compiled during my study sessions. Credit: ChatGPT (GPT-5)._

> **Disclaimer:**  
> These practice questions are **original, ChatGPT-generated scenarios** based on the [Google Cloud documentation](https://cloud.google.com/) and the **exam guide**.  
> They are *not* actual exam questions. Sharing exam content verbatim violates Google’s NDA and policies.  
> The goal here is to help learners prepare with realistic, scenario-style problems.

---


## Key Points
- **Cloud Build**: Automates CI with triggers, buildpacks, and caching (--cache-from, GCS). Supports hybrid/multi-cloud via worker pools and APIs.
- **Cloud Deploy**: Manages CD with delivery pipelines, targets (e.g., GKE, Cloud Run), and Skaffold for manifest rendering. Supports canary, blue/green, and approvals.
- **Artifact Registry**: Central repository for container images and packages, integrated with Cloud Build and Cloud Deploy.
- **Build Optimization**: Use caching, optimized Docker layering, and appropriate machine types to improve performance and reduce costs.
- **Scalability**: Use IaC (Terraform/Deployment Manager) for consistent pipeline definitions across many repositories.

## Practice Questions

### Q1. Multi-Environment Rollout
You want to promote builds from staging → pre-prod → prod with approvals. Which Cloud Deploy feature should you use?  
A. Cloud Build triggers  
B. A delivery pipeline with targets for each environment  
C. Cloud Scheduler  
D. Manual kubectl apply  
✅ **Correct Answer: B**  
👉 Cloud Deploy uses delivery pipelines with multiple targets representing environments. Approvals can be enforced between stages.

### Q2. Canary Rollout
You want 10% traffic → new version, monitor for 1h, then 100% rollout if healthy. How do you configure this in Cloud Deploy?  
A. Set up manual kubectl rollouts  
B. Define a canary deployment strategy in Cloud Deploy  
C. Use Cloud Functions for rollout control  
D. Split services across namespaces  
✅ **Correct Answer: B**  
👉 Cloud Deploy supports canary and progressive delivery strategies natively. Canary allows partial rollout + monitoring before full promotion.

### Q3. Automatic Load Testing in CI/CD
You are configuring your CI/CD pipeline natively on Google Cloud. You want builds in a pre-production GKE environment to be automatically load-tested before being promoted to production. You need to ensure that only builds that have passed this test are deployed to production. You want to follow Google-recommended practices.  
A. Create an attestation for the builds that pass the load test by requiring the lead QA engineer to sign using a personal key  
B. Create an attestation for the builds that pass the load test by using a private key stored in Cloud KMS authenticated through Workload Identity  
C. Create an attestation using a service account JSON key stored as a Kubernetes Secret  
D. Require a manual KMS signature from the QA lead  
✅ **Correct Answer: B**  
👉 The best practice is Workload Identity + Cloud KMS keys for attestation signing. Avoid personal keys or JSON keys in secrets.

### Q4. Artifact Registry Role
What is Artifact Registry’s role in CI/CD?  
A. Enforces IAM policies on Kubernetes  
B. Stores and manages container images, packages, and Helm charts  
C. Replaces Cloud Functions runtime  
D. Controls rollout speeds  
✅ **Correct Answer: B**  
👉 Artifact Registry is the central container/package repository for builds before deployment.

### Q5. Cloud Build Triggers
To automatically kick off a build in Cloud Build when code is pushed to GitHub, what should you configure?  
A. A Cloud Function triggered on GitHub push  
B. A Cloud Build trigger linked to the GitHub repo  
C. A GitHub Actions workflow pushing to Cloud Run  
D. A Pub/Sub subscription to GitHub webhooks  
✅ **Correct Answer: B**  
👉 Cloud Build supports direct integration with GitHub via build triggers. You register your repo and configure the trigger to launch builds on code events.

### Q6. Source-to-Image Automation
Which mechanism allows Cloud Build to create a container from source repository code?  
A. Manual Dockerfile build only  
B. Cloud Buildpacks from a registered source  
C. VM import tool  
D. Pre-built images only  
✅ **Correct Answer: B**  
👉 Cloud Build supports source builds using buildpacks, streamlining CI pipelines via automated detection and packaging in Cloud Build.

### Q7. Build Caching
To speed up Docker builds, you use a previously built image via which argument in Cloud Build?  
A. --cache-to  
B. --layer-cache  
C. --cache-from  
D. --reuse-cache  
✅ **Correct Answer: C**  
👉 Enables using a previous image as cache to accelerate rebuilds.

### Q8. Build Artifact Caching
How can you reuse build artifacts using Cloud Storage to accelerate builds?  
A. By using --cache-from with a Storage URI  
B. By caching build results in a GCS bucket and reusing them in future builds  
C. Cloud Build automatically caches in GCS  
D. Use Cloud Storage as staging only  
✅ **Correct Answer: B**  
👉 Cache results in GCS and reuse across builds.

### Q9. Container Image Optimization
Which strategy reduces container image size and improves build performance?  
A. Combine build and runtime in one stage  
B. Separate build-time dependencies from runtime container  
C. Always copy entire source into final image  
D. Use multiple RUN commands  
✅ **Correct Answer: B**  
👉 Separate build and runtime stages, keeping artifacts minimal.

### Q10. Increase vCPU for Builds
How to increase vCPU for builds using the CLI?  
A. --cpu-count  
B. --high-vcpu  
C. --machine-type  
D. --build-cpu  
✅ **Correct Answer: C**  
👉 --machine-type via gcloud builds submit or config.

### Q11. High-vCPU Startup Time
Why might choosing a high-vCPU machine increase build startup time?  
A. Scheduling delays  
B. Initialization overhead  
C. Cloud Build must start non-standard VMs on demand  
D. Network delays  
✅ **Correct Answer: C**  
👉 Non-standard machines are started on demand, increasing startup latency.

### Q12. SLSA Level 3 Assurance
What best supports SLSA level 3 build assurance in Cloud Build?  
A. Static build steps  
B. Build provenance metadata (digests, source, toolchain)  
C. One-time builds only  
D. Manual approval  
✅ **Correct Answer: B**  
👉 Build provenance with detailed metadata.

### Q13. Ephemeral Build Environments
Why are ephemeral build environments recommended?  
A. Faster builds  
B. Lower resource cost  
C. Security via isolation from previous builds  
D. Templates are easier  
✅ **Correct Answer: C**  
👉 They ensure clean and secure builds by isolating state.

### Q14. Custom Worker Pools
Custom worker pools are used in Cloud Build primarily for:  
A. Running builds faster on public internet  
B. Isolating builds in VPC environments (e.g., on-prem, hybrid)  
C. Reducing costs only  
D. Building mobile apps exclusively  
✅ **Correct Answer: B**  
👉 Worker pools create isolated build infrastructure inside your VPC, enabling hybrid/secure CI setups.

### Q15. Automated CI/CD at Scale
To use Cloud Build in an enterprise setting with many repos yielding standardized builds, you should:  
A. Manually configure triggers for each repo  
B. Use Terraform or Deployment Manager to define build templates and trigger resources  
C. Use Cloud Functions instead  
D. Export code to storage and scan manually  
✅ **Correct Answer: B**  
👉 IaC tools like Terraform allow consistent, repeatable build pipeline definitions and trigger configurations at scale.

### Q16. Hybrid/Multi-Cloud Build Strategy
For CI across multiple cloud providers, an approach using Cloud Build:  
A. Only works within GCP  
B. Can integrate with other clouds via worker pools or triggers orchestrating remote builds  
C. Requires redeployment of Cloud Build to other vendors  
D. Not supported  
✅ **Correct Answer: B**  
👉 Cloud Build’s flexibility permits hybrid CI/CD by leveraging worker pools or orchestrating multi-cloud pipelines via triggers and APIs.

### Q17. Build Approval Gates
For production releases, you need manual approval. How do you add that?  
A. --manual-approval flag  
B. Use Cloud Build approvers (approval workflow) in pipeline  
C. Use Cloud Functions  
D. Trust auto-deploy  
✅ **Correct Answer: B**  
👉 Cloud Build supports approval workflows to gate stages before proceeding.

### Q18. Third-Party CI Tool Integration
You want to integrate Jenkins with Cloud Build. Which method allows this?  
A. Run Jenkins inside Cloud Build  
B. Jenkins triggers Cloud Build via CLI or REST API  
C. Not supported  
D. Use only Cloud Build triggers  
✅ **Correct Answer: B**  
👉 External CI systems like Jenkins can invoke Cloud Build using APIs or gcloud CLI for uniform pipeline consistency.

### Q19. Cost Control for Builds
Which helps optimize costs of Cloud Build usage?  
A. Unlimited concurrency  
B. Caching, machine-type tuning, and efficient triggers  
C. Build everything daily  
D. No artifact retention  
✅ **Correct Answer: B**  
👉 Using build caching, appropriate VM sizing, and optimizing triggers helps control CI costs.

### Q20. Cloud Deploy Pipeline Definition
In Cloud Deploy, what is a delivery pipeline?  
A. A container image that stores deployment manifests  
B. A resource that defines the deployment process across environments  
C. A job that runs continuous integration tests  
D. A trigger for Cloud Build  
✅ **Correct Answer: B**  
👉 A delivery pipeline defines the progression of releases through stages/environments (e.g., dev → staging → prod).

### Q21. Cloud Deploy Configuration Tool
Which tool does Cloud Deploy rely on for defining deployment configuration?  
A. Kustomize  
B. Skaffold  
C. Terraform  
D. Ansible  
✅ **Correct Answer: B**  
👉 Cloud Deploy uses Skaffold configuration files to define build and deploy steps.

### Q22. Cloud Deploy Target Role
What is the role of a target in Cloud Deploy?  
A. It defines a cluster or runtime environment for deployment  
B. It specifies the build steps for an application  
C. It determines the IAM roles required for deployment  
D. It handles secret injection  
✅ **Correct Answer: A**  
👉 A target represents a deployment destination (e.g., GKE cluster, Cloud Run service).

### Q23. Cloud Deploy Rollouts
Which of the following is true about rollouts in Cloud Deploy?  
A. A rollout represents a new version of source code  
B. A rollout is an artifact stored in Container Registry  
C. A rollout is an instance of deploying a release to a target  
D. A rollout defines IAM permissions  
✅ **Correct Answer: C**  
👉 Each rollout is the execution of deploying a specific release to a target.

### Q24. Release vs Rollout
What is the difference between a release and a rollback in Cloud Deploy?  
A. Release = code commit, Rollout = build log  
B. Release = CI job, Rollout = manual approval  
C. Release = build output (immutable), Rollout = deploy action  
D. Release = Cloud Run job, Rollout = service instance  
✅ **Correct Answer: C**  
👉 Release = immutable snapshot of app/config. Rollout = deploying that release to a target.

### Q25. Cloud Deploy and Cloud Build Integration
How does Cloud Deploy integrate with Cloud Build?  
A. Cloud Deploy automatically builds images  
B. Cloud Build triggers must always create rollouts  
C. Cloud Build outputs artifacts that Cloud Deploy consumes  
D. They cannot be integrated directly  
✅ **Correct Answer: C**  
👉 Cloud Build can produce container images and manifests, which Cloud Deploy consumes for rollout.

### Q26. 
Which feature allows Cloud Deploy to require human intervention before deploying to production?
A. IAM policies
B. Binary Authorization
C. Approvals
D. Workload Identity

✅ Answer: C
Explanation: Approvals can be configured for stages (like prod) to enforce manual verification.
### Q27. 
What is required to deploy to a private GKE cluster from Cloud Deploy?
A. VPC Service Controls
B. Private connectivity using a worker pool
C. External load balancer
D. Cloud Armor policy

✅ Answer: B
Explanation: Private GKE requires a private worker pool for Cloud Deploy to connect securely.

### Q28. 
In Cloud Deploy, what happens if a rollout fails?
A. The release is deleted
B. The target becomes unavailable
C. The rollout can be retried or rolled back
D. The pipeline must be recreated

✅ Answer: C
Explanation: Failed rollouts can be retried, fixed, or rolled back to previous versions.

### Q29. 
Which CI/CD practice is supported directly by Cloud Deploy?
A. Canary or progressive delivery
B. Chaos engineering
C. Load testing automation
D. Secret rotation

✅ Answer: A
Explanation: Cloud Deploy supports progressive delivery patterns like canary rollouts.

### Q30. 
Cloud Deploy uses which Google Cloud resource to store pipeline configuration?
A. Cloud Source Repositories
B. Google Cloud Storage (GCS)
C. Artifact Registry
D. Pub/Sub

✅ Answer: B
Explanation: Cloud Deploy stores pipeline configs in GCS buckets.

### Q31. 
Which of the following can be configured in Cloud Deploy delivery pipeline YAML?
A. IAM role bindings
B. Artifact encryption keys
C. Serial or parallel progression of targets
D. API Gateway endpoints

✅ Answer: C
Explanation: Pipelines define target progression (e.g., dev → staging → prod), either sequentially or in parallel.

### Q32
If you want to integrate Argo CD with Cloud Deploy, what’s the best approach?
A. Replace Skaffold with Argo CD config
B. Use Argo CD for GitOps and Cloud Deploy for release orchestration
C. Migrate Argo CD manifests into Cloud Deploy
D. Argo CD and Cloud Deploy cannot be used together

✅ Answer: B
Explanation: Many enterprises combine Argo CD (GitOps) with Cloud Deploy for multi-environment orchestration.

### Q33.
Cloud Deploy pipelines can be defined in which format?
A. JSON only
B. YAML only
C. YAML or JSON
D. HCL (HashiCorp)

✅ Answer: C
Explanation: Delivery pipelines are defined in YAML or JSON configs.

### Q34
What is the default behavior if you don’t define an approval step in Cloud Deploy?
A. Rollouts require manual confirmation
B. Rollouts auto-progress through all targets
C. Rollouts fail at production
D. Rollouts only deploy to staging

✅ Answer: B
Explanation: If approvals aren’t configured, rollouts progress automatically.

### Q35
Which IAM role is required to approve rollouts in Cloud Deploy?
A. roles/cloudbuild.builds.approver
B. roles/clouddeploy.approver
C. roles/deploymentmanager.editor
D. roles/cloudfunctions.invoker

✅ Answer: B
Explanation: roles/clouddeploy.approver grants approval permissions for rollouts.

### Q36
When using Kustomize with Cloud Deploy, what is its purpose?
A. Automates container builds
B. Applies environment-specific overlays to manifests
C. Provides traffic splitting rules
D. Manages CI jobs

✅ Answer: B
Explanation: Kustomize customizes Kubernetes manifests for different environments (dev, staging, prod).

### Q37
Which deployment strategy is supported natively by Cloud Deploy?
A. Rolling update
B. Canary
C. Blue/Green
D. All of the above

✅ Answer: D
👉 Cloud Deploy supports progressive delivery strategies like rolling, canary, and blue/green.

### Q38.
What does Cloud Deploy use to deploy workloads to GKE or Cloud Run?
A. Terraform modules
B. Skaffold render outputs
C. Jenkins pipelines
D. Helm charts only

✅ Answer: B
👉 Cloud Deploy executes Skaffold-rendered Kubernetes/Cloud Run manifests.

### Q39.
Which statement about rollbacks in Cloud Deploy is TRUE?
A. They automatically trigger after 3 failures
B. They use the last successful rollout of the same release
C. They require a new pipeline definition
D. They only work for Cloud Run

✅ Answer: B
👉 Rollbacks use the last successful rollout of the same release.

### Q40.
How does Cloud Deploy integrate with hybrid or multi-cloud?
A. By directly deploying to AWS Lambda
B. Through Anthos and Config Sync
C. By copying container images to other registries
D. By exporting manifests to Cloud Functions

✅ Answer: B
👉 With Anthos, Cloud Deploy can deliver workloads across multi-cloud and on-prem environments.

### Q41. 
How do you secure Cloud Build in private pools from data exfiltration?
A. Combine with IAM
B. VPC Service Controls
C. IP Whitelisting
D. Firewall rules

Answer: B. Use VPC Service Controls for private pools. 

### Q42. Enforcing Least Privilege in CI/CD

A developer needs to trigger builds but not modify build configs. What role is appropriate?
A. project-owner
B. roles/cloudbuild.builds.viewer
C. admin
D. unprivileged user

✅ Correct: B
Explanation: Least privilege principle suggests limiting access; viewers can trigger but not edit.

### Q43. Cloud Build and Multi-Cloud Deploy

You need to deploy to AWS after passing GCP build. How?
A. Not possible
B. Use Cloud Build step to call AWS CLI or AWS CDK
C. Export artifacts and manually deploy
D. GCP-native tools only allow Cloud Run

✅ Correct: B
Explanation: Cloud Build can orchestrate multi-cloud CD by invoking AWS tools securely.

---