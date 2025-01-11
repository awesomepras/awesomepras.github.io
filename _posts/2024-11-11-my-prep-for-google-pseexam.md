---
layout: default
title: My Prep For Google Professional Cloud Engineer Exam
---
![Image description](/assets/images/pse_cert.png)

# Overview
There’s plenty of information available on the structure of the Google Cloud Professional Security Engineer exam, so here I'll focus on study strategies, resources, and practical advice for those preparing to take it.

I started my preparation on Sept 5 as part of a google cohort study group as part of https://cloud.google.com/innovators. I also got access to cloudskills boost portal at my work which benefited me in covering all the courses/required labs etc. I spent an average of 2-3 hours a day in a week until Nov 1st just targeting cloudskills boost courses and labs. Five Days before the exam I just want hard core 4-5 hours a day to cover all the google documentation reading through them. 

I did not spend a lot of time trying to review questions in examtopics as I personally felt that the questions are misleading and answers are wrong but neverthless it does help explore the discussions to understand the concepts. So do what you please with that information.

## Recommended Resources
### 1. Courses
Google Cloud Skills Boost: If your organization provides free access, this is one of the most comprehensive resources. There is a cloud Security engineering path. I skipped core infrastructure courses completely only focussed on Network/Security topics.
Coursera Google Cloud Security Engineer Professional Certificate: A great option if you don’t have company-sponsored access. This course offers structured guidance through the core exam topics. You will miss out on the quizes at end of each module (most likely) if you chose the free route. I did not take this but have done other courses in Coursera so my feedback is based on that experience. 

### 2. Core Focus Areas:
Google Documentation and Exam Blueprint: Google’s official documentation remains a primary resource. Focus on understanding each topic rather than exhaustive deep dive reading. Aim to know the "what," "when," and "how" for each concept. 

What is it and what does it do? (e.g., IAM, GCDS, Interconnect, service account, KMS etc.)  

When to use it: Know the scenarios where each service fits best.  

Security Measures: Top down approach ( or perimeter first )  

Detection & Logging :  Preventative (mitigating via Threat detection/SCC) versus reporting and analysis (logging/Bigquery).  

### 3. Deep Dives for High-Impact Topics
`CI/CD Security`: Familiarize yourself with securing build and deployment pipelines. Focus on vulnerability scanning, applying security policies, and enforcing compliance in your CI/CD workflows.  
`DLP and Compliance`: You’ll need a solid grasp of data loss prevention and when to use specific tools like Key Management Service (KMS). It’s essential to understand how these tools protect data and align with compliance.
Networking and DNS Peering: Networking is critical for exam scenarios.   
`Governance and Compliance`:  Understand the requirements and differences (GDPR versus HIPAA) and when to use what solution (Assured workload versus Security Health Analytics)  

### 4. Additional Resources

I am a visual person, this particular guide really helped me 
https://cloud.google.com/blog/topics/developers-practitioners/google-cloud-security-overview

Some Chart:  
https://cloud.google.com/static/architecture/security-foundations/images/efb-key-decisions.svg 

which is part of 
https://cloud.google.com/architecture/security-foundations

Read everything under this page: 
https://cloud.google.com/architecture/configure-networks-fedramp-dod-google-cloud?hl=en

Ammett W's Google Cloud Security Engineer Prep Guide on Start Cloud Now offers a targeted approach for each topic. 

[Tarran Ivory](https://www.linkedin.com/in/tarran-ivory-2b7554145/?lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3BxaiYyb%2B0TImNZxl%2F346Dzw%3D%3D) has an excellent document that covers everything in the exam blue-print, reach out to him on Linkedin for access to the google doc. 

Some important pages to review in google documentation:

https://cloud.google.com/architecture/security-iam?hl=en

https://cloud.google.com/docs/authentication/token-types


`KMS deep dive `: https://cloud.google.com/docs/security/key-management-deep-dive

https://jryancanty.medium.com/kms-fundamentals-for-enterprises-moving-to-the-cloud-part-1-74ebf20c26d7


####  Youtube videos: 
Getting started with Websecurity scanner: 

https://www.youtube.com/watch?v=1BengAd2_cI&list=PLIivdWyY5sqKd-Cu1HZ7v5RiYE8gVsM7P&index=4 

`VPC deep dive` : https://www.youtube.com/watch?v=wmP6SQe5J7g 

`GCP security best practice`: https://www.youtube.com/watch?v=ZQHoC0cR6Qw&list=PLAFY3hrExHFF4Df4TTXlvKCdiKIF7SZz2 

`Level UP from Zero` : https://www.youtube.com/watch?v=04xtKFwvYMc&list=PLGX9vnJSE_clwMyvnbAB1rnJJGgy0p-q3



### Exam Day Tips
I took the exam in the exam center.  
I finished the exam in 1 hour 10 mins so had 50 mins to review the marked questions.   
I had about 15 questions marked for review but ended up reviewing all .  
The Exam browser interface in the test center has "back - next and submit exam" buttons next to each other, make sure you dont click submit exam button. Dont worry, there is a prompt to confirm you are "Submitting the exam". 

To review the questions , there is a button to "Review Marked, which also shows all question numbers hyperlinked" so you can go back and forth  
No notepad or white paper is allowed, so practice mental note-taking or use mental visualization to remember key points.  

#### Post-Exam: 
Google’s certification badge from Credly arrives within a day in an email that just says "
`<your name> `You’ve earned a badge from Google Cloud'.   

You will get an email to choose a swag. The swag takes forever to arrive but it eventually arrives.     

The exam is challenging and drains you a lot - during preparation, but thorough preparation will leave you well-equipped and confident. 

Good luck!

After the exam - Have fun with Arcade: https://cloud.google.com/blog/topics/training-certifications/the-arcade-with-google-cloud-game-helps-boost-cloud-skills



