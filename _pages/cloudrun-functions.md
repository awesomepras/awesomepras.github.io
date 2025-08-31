---
layout: page
title: ""
permalink: /cloudrun-functions/
---

---

# Cloud Run and Cloud Functions for Google Cloud DevOps

This page includes practice questions on Cloud Run (services, jobs, worker pools) and Cloud Functions, key components for serverless deployments in Google Cloud.

_A curated list of practice questions, with explanations, compiled during my study sessions. Credit: ChatGPT (GPT-5)._

> **Disclaimer:**  
> These practice questions are **original, ChatGPT-generated scenarios** based on the [Google Cloud documentation](https://cloud.google.com/) and the **exam guide**.  
> They are *not* actual exam questions. Sharing exam content verbatim violates Google’s NDA and policies.  
> The goal here is to help learners prepare with realistic, scenario-style problems.


## Key Points
- **Cloud Run Services**: Handle request-driven workloads with traffic splitting and tagged revisions for gradual rollouts and testing.
- **Cloud Run Jobs**: Designed for batch or one-off tasks (e.g., ETL, data processing) without HTTP endpoints.
- **Worker Pools**: Run background tasks in isolated environments without autoscaling, ideal for secure or hybrid setups.
- **Cloud Functions**: Event-driven, lightweight functions triggered by Pub/Sub, HTTP, or other events.
- **IAM and Deployment**: Use roles like run.invoker and run.admin for execution and management; tags provide stable URLs for revisions.

## Practice Questions

### Q1. Cloud Run vs Cloud Functions
What is the key difference between Cloud Run and Cloud Functions?  
A. Cloud Run only supports Python, while Cloud Functions supports any language  
B. Cloud Functions is event-driven, while Cloud Run runs containerized applications  
C. Cloud Run automatically retries failed functions, while Cloud Functions does not  
D. Cloud Run requires Kubernetes, while Cloud Functions does not  
✅ **Correct Answer: B**  
👉 Cloud Functions is event-driven (responds to triggers like Pub/Sub, HTTP, etc.), while Cloud Run runs full containers you deploy.

### Q2. Traffic Splitting
Your company has a Cloud Run service running v1 (stable). A new release v2 needs to be tested gradually. You want 20% of traffic to go to v2 while 80% remains on v1. What is the best approach?  
A. Deploy v2 as a new service with its own URL  
B. Deploy v2 as a new revision of the existing service and configure traffic splitting to send 20% of requests to v2  
C. Replace v1 with v2 and roll back if issues occur  
D. Use Cloud Load Balancing to distribute traffic manually  
✅ **Correct Answer: B**  
👉 Cloud Run supports built-in traffic splitting between revisions. Deploying v2 as a revision of the same service and splitting traffic ensures gradual rollout with rollback capability.

### Q3. Tagged Revisions
You want to create a URL that points only to a specific revision of a Cloud Run service, regardless of traffic splitting. What should you do?  
A. Use the service’s default URL  
B. Tag the revision, which creates a dedicated URL for it  
C. Deploy it to a separate project  
D. Use Cloud DNS to alias the revision  
✅ **Correct Answer: B**  
👉 Cloud Run tags provide dedicated, stable URLs for revisions. Useful for testing or internal users without affecting production traffic.

### Q4. Jobs vs Services
When should you use a Cloud Run Job instead of a Service?  
A. For long-running HTTP servers  
B. For batch or data processing tasks that don’t require HTTP requests  
C. For WebSocket-based apps  
D. For apps that need to scale to zero  
✅ **Correct Answer: B**  
👉 Cloud Run Jobs are for batch workloads (ETL, cron-triggered jobs, data cleanup), while Services are for request/response workloads.

### Q5. Zero-Downtime Deployment
Which Cloud Run feature allows zero-downtime deployment of new versions?  
A. Blue-green deployments  
B. Traffic splitting  
C. Horizontal Pod Autoscaling  
D. Service Mesh  
✅ **Correct Answer: B**  
👉 Cloud Run supports traffic splitting natively, enabling progressive rollouts by routing % of traffic to new revisions.

### Q6. Cloud Run Jobs Purpose
What are Cloud Run Jobs used for?  
A. Long-running microservices  
B. Stateless, request-based workloads  
C. Batch or data processing tasks  
D. Stateful streaming applications  
✅ **Correct Answer: C**  
👉 Jobs in Cloud Run are designed for one-off or batch workloads (ETL, ML batch inference, migrations).

### Q7. Deploying a New Revision
You deploy a new revision of a Cloud Run service but want only 10% of traffic to go to it while keeping 90% on the stable revision. How do you configure this?  
A. Use gcloud run services update-traffic with --to-latest=10 and --to-revisions for the stable revision  
B. Deploy the revision with --traffic 10 directly in the deploy command  
C. Manually edit the YAML file to set traffic split and redeploy  
D. All of the above are possible  
✅ **Correct Answer: D**  
👉 Cloud Run supports traffic splitting via deploy command, update-traffic, or editing the YAML. For the exam, know both CLI and declarative methods.

### Q8. Pinning Clients to a Revision
You want QA testers to access only the new revision of your Cloud Run service, without affecting production users. What should you do?  
A. Configure a traffic split with 0% to new revision, then give testers the direct revision URL  
B. Create a tag for the new revision and share the tag-based URL with testers  
C. Add testers to a special IAM policy that routes them to the new revision  
D. Deploy a separate Cloud Run service for QA  
✅ **Correct Answer: B**  
👉 Tags give custom URLs (like tag---service-xyz.a.run.app) that always point to that revision. This is the recommended approach for QA/blue-green testing.

### Q9. Gradual Rollout Strategy
Your service must deploy new versions gradually (10% → 25% → 50% → 100%) to minimize risk. Which Cloud Run feature do you use?  
A. Manual traffic splitting  
B. Auto-scaling policies  
C. Cloud Run Jobs  
D. Cloud Scheduler  
✅ **Correct Answer: A**  
👉 Cloud Run has no built-in canary automation — you implement rollout manually by updating traffic percentages step by step.

### Q10. Rollback
You deployed a new revision that is failing. What’s the fastest rollback method?  
A. Delete the new revision  
B. Use gcloud run services update-traffic to shift 100% back to the previous revision  
C. Redeploy the old Docker image  
D. Use tags to reroute production traffic  
✅ **Correct Answer: B**  
👉 Rollback = reassign traffic instantly, without deleting revisions. Very fast compared to redeploy.

### Q11. Revision URLs vs Service URLs
Which statement is true about Cloud Run revision URLs?  
A. Revision URLs are permanent and tied to a specific revision  
B. Service URL always points to the latest traffic-splitting config  
C. Tag URLs always point to the tagged revision, regardless of traffic split  
D. All of the above  
✅ **Correct Answer: D**  
👉 Revision URL = fixed, per revision. Service URL = obeys traffic split. Tag URL = fixed alias to revision.

### Q12. Blue-Green Deployment
You want 0 downtime when switching traffic between old and new revisions. Which approach is correct?  
A. Deploy new revision, assign tag "green", test, then shift 100% traffic  
B. Delete old revision before deploying new one  
C. Use Cloud Run Jobs  
D. Use Cloud Scheduler to route traffic  
✅ **Correct Answer: A**  
👉 Classic blue-green = run both in parallel → test new (via tag) → switch all traffic in one step. Cloud Run fully supports this.

### Q13. Multiple Environments with Tags
You have staging, canary, and production environments in one service. How do you expose them?  
A. Deploy separate services per environment  
B. Use tags (e.g., staging---service.run.app, canary---service.run.app)  
C. Create a VPC for each environment  
D. Use Cloud Run Jobs  
✅ **Correct Answer: B**  
👉 Tags allow environment-like separation within the same service. Separate services (A) is also valid in real life, but exam emphasizes tags.

### Q14. Cloud Run Definition
What is Cloud Run?  
A. Managed container service with cluster management  
B. Serverless platform for event-driven functions only  
C. Fully managed platform running containers or functions with minimal infra work  
D. Requires cluster setup and Kubernetes  
✅ **Correct Answer: C**  
👉 Cloud Run lets you run containers (or functions) without managing clusters.

### Q15. Execution Environments
Which statement is true about Cloud Run execution environments?  
A. Services use always second-gen; jobs first-gen  
B. Services default to auto-select; jobs are always second-gen  
C. Both services and jobs can opt between first and second-gen  
D. All workloads must run on first-gen only  
✅ **Correct Answer: B**  
👉 Services default to auto-select, while jobs always use second-gen.

### Q16. Traffic Splitting Options
Which method can you use for Cloud Run traffic splitting?  
A. gcloud run services update-traffic  
B. YAML edits in deployment config  
C. --to-latest flag in CLI  
D. All of the above  
✅ **Correct Answer: D**  
👉 All these methods allow traffic splitting.

### Q17. Revisions
What are revisions?  
A. Mutable instances running in parallel  
B. Immutable snapshots of deployed code/config  
C. Rollback-only artifacts  
D. Only for backing up services  
✅ **Correct Answer: B**  
👉 Each deploy creates an immutable revision.

### Q18. Tags Benefit
What is a primary use of tags in Cloud Run?  
A. Version control rollback  
B. Load balancing multiple services  
C. Named alias to route traffic to a specific revision  
D. Container image labels  
✅ **Correct Answer: C**  
👉 Tags generate a stable URL that targets a single revision.

### Q19. Cloud Run Jobs
Which best describes a Cloud Run job?  
A. Serves HTTP events  
B. Continuously running background service  
C. Runs tasks to completion and exits  
D. Autoscaling container  
✅ **Correct Answer: C**  
👉 Jobs run to completion, not serve requests.

### Q20. Executing Jobs
Which role allows you to execute a Cloud Run job?  
A. roles/run.admin  
B. roles/run.invoker  
C. roles/run.viewer  
D. roles/monitoring.editor  
✅ **Correct Answer: B**  
👉 run.invoker is required to execute jobs.

### Q21. Job Execution Visibility
How many recent executions are visible in the UI?  
A. Only latest one  
B. Last 100  
C. Last 1,000  
D. Unlimited  
✅ **Correct Answer: C**  
👉 UI shows details for last 1,000.

### Q22. Worker Pools Purpose
Cloud Run worker pools are designed for:  
A. Serving HTTP traffic  
B. Background batch workloads without autoscaling  
C. Autoscaled microservices  
D. Event-driven functions  
✅ **Correct Answer: B**  
👉 Worker pools run background tasks and don’t auto-scale nor have endpoints.

### Q23. Worker Pools Revisions
Deploying changes to a worker pool:  
A. Does not create a new revision  
B. Always creates a new immutable revision  
C. Only if image changes  
D. Only for autoscaled pools  
✅ **Correct Answer: B**  
👉 Any config change generates new revision.

### Q24. IAM for Worker Pools
What roles must the deployer have to manage worker pools?  
A. Cloud Run Developer + Service Account User  
B. Monitoring Admin  
C. Storage Admin  
D. No permissions  
✅ **Correct Answer: A**  
👉 These roles allow deployment and identity management.

### Q25. Manual Scaling Worker Pools
To scale a worker pool manually, you:  
A. Use --autoscale=manual  
B. Set --scaling=0  
C. Set manual instance count in config or console  
D. Use Traffic Split  
✅ **Correct Answer: C**  
👉 Manual instance count via console or CLI config.

### Q26. Disabling Worker Pools
To disable a worker pool without deleting it, set scaling to:  
A. OFF  
B. -1  
C. 0  
D. 1  
✅ **Correct Answer: C**  
👉 Setting manual instances to 0 disables it.

### Q27. Deleting Worker Pools
Deleting a worker pool:  
A. Is reversible  
B. Removes all revisions  
C. Removes container images automatically  
D. Doesn’t affect revisions  
✅ **Correct Answer: B**  
👉 Deleting deletes all pool revisions.

### Q28. Service Identity
What must the service account user have to configure worker pool’s service identity?  
A. Cloud Run Admin  
B. IAM Service Account User  
C. Artifact Registry Reader  
D. Logging Admin  
✅ **Correct Answer: B**  
👉 Allows deploying with specified service identity.

### Q29. Deploy from Source Code
Cloud Run supports deploying from source via:  
A. Docker Build only  
B. Cloud Build using built-in buildpacks  
C. Manual Docker push only  
D. None of these  
✅ **Correct Answer: B**  
👉 Source deploy uses Cloud Build and buildpacks.

### Q30. Functions on Cloud Run
Deploying a function to Cloud Run involves:  
A. Pushing container only  
B. Uploading code, building image, deploying service  
C. Only pushing script to console  
D. Not supported  
✅ **Correct Answer: B**  
👉 Cloud Build builds container; Cloud Run executes.

### Q31. Authentication Defaults
By default, Cloud Run services are:  
A. Publicly accessible  
B. Private—invoker role required  
C. Open to all authenticated users  
D. Disabled  
✅ **Correct Answer: B**  
👉 Defaults to private; only allowed with IAM roles.

### Q32. IAM Roles for Services
Which predefined role gives full Cloud Run resource control?  
A. run.viewer  
B. run.invoker  
C. run.admin  
D. run.serviceAgent  
✅ **Correct Answer: C**  
👉 roles/run.admin covers full control.

### Q33. AI App Hosting
Cloud Run can host AI workloads integrated with:  
A. Gemini API, Vertex AI, Cloud SQL  
B. Only compute jobs  
C. Only logging apps  
D. Machine learning APIs not supported  
✅ **Correct Answer: A**  
👉 Cloud Run integrates with AI and DB tools.

### Q34. Quickstarts
Which is a Cloud Run quickstart?  
A. Solidity contract  
B. Deploy Go service or job  
C. Set up Kubernetes cluster  
D. Pure VM deploy  
✅ **Correct Answer: B**  
👉 Quickstarts offer samples for various languages and jobs.

### Q35. Build Worker Pools Usage
Build worker pools are used to:  
A. Serve traffic  
B. CI/CD for source deploys with VPC isolation  
C. Logging only  
D. Not supported  
✅ **Correct Answer: B**  
👉 Custom build pools integrate Cloud Build with VPC controls.

### Q36. First-gen vs Second-gen
First-gen Cloud Run environment is ideal when:  
A. You need high Linux system call compatibility  
B. You have low memory (<512 MiB) or need fast cold start  
C. You need NFS support  
D. You require full system call support  
✅ **Correct Answer: B**  
👉 First-gen supports small memory and fast startup.

### Q37. Service URL Behavior
Default service URL:  
A. Always latest revision explicitly  
B. Follows traffic split configuration  
C. Randomly picks revision  
D. Disabled by default  
✅ **Correct Answer: B**  
👉 Default URL adheres to traffic split.

### Q38. Worker Pool Image Limit
What is the maximum layer size for Docker Hub images?  
A. 5 GB  
B. 9.9 GB  
C. 20 GB  
D. Unlimited  
✅ **Correct Answer: B**  
👉 Supports up to 9.9 GB per layer.

---