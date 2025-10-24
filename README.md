PRD — Subscription Management Dashboard (SaaS)

1\. Product Purpose

A SaaS web app for individuals, freelancers, or SMBs to:



Track all SaaS tool subscriptions and renewal dates.



Get renewal alerts.



Analyze expenses, optimize spend.



Centralize invoices and subscription details.



Cancel subscriptions via API (where available).



Support multiple users, roles, and secure authentication.



2\. User Stories

“As a user, I can add/edit/delete subscriptions.”



“I get notified by email before renewals.”



“I see a dashboard and analytics of my software spend.”



“I can invite team members and assign them roles.”



“I attach invoices/documents to my subscriptions.”



“I can view all my subscriptions in a calendar view.”



“Admins can export spend reports and analyze trends.”



“Premium: cancel subscriptions via integration (Stripe/PayPal API).”



3\. Features \& Functional Requirements

MVP

User authentication (signup/login/forgot password).



Dashboard with subscription list, renewal dates, spend, payment methods.



Add/edit/delete subscriptions.



Attach invoices (file upload).



Email notifications for renewals.



Analytics charts (monthly/annual spending, top categories).



Multi-user support (invite members, assign roles).



RESTful API for all operations.



Premium/Pro Features (extend later)

API integration with Stripe/PayPal for billing and cancellation.



Advanced analytics (trend forecasting, export CSV/PDF reports).



Billing automation (auto-renew, invoice fetching).



Tiered tenancy: support for multiple orgs/companies.



4\. How It Works (Workflow)

User Point-of-View

User registers → logs in.



Adds their subscriptions via a simple form (name, price, renewal date, payment method, category, attachment for invoice).



The dashboard auto-updates with analytics graphs (using a chart library).



AWS Lambda runs a scheduled job (via EventBridge) to check for upcoming renewals and sends emails using AWS SES.



Team members can be invited (AWS Cognito user pools, RBAC).



All actions go through RESTful APIs (hosted on Lambda/API Gateway).



File uploads go to S3, details stored in DynamoDB.



Admins see team management, analytics, and can export data.



5\. AWS Free Tier — What to Use

Component	AWS Service	Free Tier Benefits

Frontend (React)	S3 Static Hosting + CloudFront	12 months/50GB storage/month

Backend/API	AWS Lambda + API Gateway	1M requests/month (Lambda), 1M/month (API GW)

Database	DynamoDB	25GB storage, 25WCU/25RCU/month

Users/Auth	Cognito User Pools	50,000 MAUs/month

File Uploads	S3 Bucket	5GB (general, not just frontend)

Email Notifications	Simple Email Service (SES)	62,000 emails/month to verified addresses

Scheduling (Reminders)	CloudWatch Events/EventBridge	Free tier included for most use cases

Analytics/Logs	CloudWatch + Lambda Insights	Basic logging; Free usage limit

DevOps CI/CD	GitHub Actions (free, or CodePipeline free tier)	1,000 build minutes/month (CodeBuild)

Monitoring	CloudWatch	Free tier logs/metrics

All these services support learning/practice—and are widely used by real SaaS apps.​



6\. DevOps \& Cloud Learning (Every Major Skill)

Serverless APIs (Lambda/API Gateway): Try endpoint creation, securing APIs.



Auth \& RBAC (Cognito): User pools, password policies, roles.



NoSQL Database (DynamoDB): Table schema, CRUD, querying, handling attachments.



Object Storage (S3): File upload, lifecycle management.



Email Automation (SES): Set up verified domains, send dynamic notifications.



Job Scheduling (EventBridge): Cron jobs for reminders.



Infrastructure-as-Code (CloudFormation/SAM/CDK): Define/auto-deploy stacks.



CI/CD Pipeline (CodePipeline/CodeBuild): Auto-build/test/deploy frontend/backend via GitHub.



Monitoring/Auditing (CloudWatch): Metrics, error alerts, user logs.



Multi-tenancy (optional): Add partition keys or tenant isolation in DB.



Security: IAM roles, resource policies, secrets (AWS Secrets Manager for API keys).



Frontend hosting: S3 + CloudFront for performance CDN.



API integrations: Extend with Stripe/PayPal APIs for cancelation/usage analytics.



7\. High-Level System Architecture

User → Browser (React, S3 Static Website, CloudFront CDN) → API Gateway → Lambda → DynamoDB → S3 (attachments) → Cognito (auth) → SES (outbound email) → EventBridge (scheduled jobs) → CloudWatch (monitoring/logs)



You’ll use DevOps practices everywhere: GitHub Actions to auto-deploy, IaC for infra, end-to-end logs, monitoring, testing, containerization (optional), role-based access, cost optimization.



8\. Free Tier Limitations/Wisdom

Start with a single workspace/tenant (multi-tenancy later).



Keep Lambda functions light; optimize DB for free limits.



SES only sends to verified email addresses in an unverified region.



Use GitHub Actions free minutes for most student hobby deployments.

