# ?? DevOps Portfolio - Serverless Infrastructure

[![Live Site](https://img.shields.io/badge/Live-gdawsonkesson.com-blue?style=for-the-badge)](https://gdawsonkesson.com)
[![AWS](https://img.shields.io/badge/AWS-Certified%20SAA--C03-orange?style=for-the-badge&logo=amazon-aws)](https://aws.amazon.com/certification/)
[![Terraform](https://img.shields.io/badge/IaC-Terraform-7B42BC?style=for-the-badge&logo=terraform)](https://www.terraform.io/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

> **Production-grade serverless portfolio with comprehensive Architecture Decision Records**  
> Built with AWS, Terraform, and GitHub Actions CI/CD | **88% cost savings documented**

[**?? View Live Site »**](https://gdawsonkesson.com)

---

## ?? Overview

This project showcases a **fully automated, cost-optimized serverless architecture** deployed on AWS, demonstrating real-world DevOps engineering skills with **documented architectural decisions** and **production-grade practices**:

- ? **Zero-downtime deployments** via GitHub Actions
- ? **Infrastructure as Code** with 500+ lines of Terraform
- ? **Architecture Decision Records** (4 comprehensive ADRs)
- ? **88% cost savings** (serverless vs EC2, documented in ADR-001)
- ? **Modern security** (CloudFront OAC vs legacy OAI, ADR-002)
- ? **Custom domain with SSL** (gdawsonkesson.com)
- ? **Serverless visitor counter** (Lambda + DynamoDB)
- ? **Runs on AWS Free Tier** ($1.70/month after free tier)

**Live Stats:**
- ?? **Cost:** $1.70/month (~$20/year with domain)
- ? **Response Time:** <200ms globally
- ?? **Security:** HTTPS with ACM certificate + CloudFront OAC
- ?? **Uptime:** 99.99% (CloudFront SLA)
- ?? **Documentation:** 4 ADRs + cost analysis

---

## ??? Architecture
```
                        Internet
                            ?
                      HTTPS (TLS 1.2+)
                            ?
       +----------------------------------------+
       ¦  Route 53 DNS ? gdawsonkesson.com      ¦
       +----------------------------------------+
                            ? Alias Record
       +----------------------------------------+
       ¦  CloudFront CDN + ACM SSL Certificate  ¦
       ¦  Global Edge Locations                 ¦
       ¦  PriceClass_100 (NA/EU)                ¦
       +----------------------------------------+
                            ? Origin Access Control (OAC)
       +----------------------------------------+
       ¦  S3 Bucket (Private)                   ¦
       ¦  + Versioning + Encryption (AES-256)   ¦
       ¦  Static Website Content                ¦
       +----------------------------------------+

       +----------------------------------------+
       ¦  API Gateway (HTTP)                    ¦
       ¦  /count endpoint                       ¦
       +----------------------------------------+
                            ? Lambda Proxy Integration
       +----------------------------------------+
       ¦  Lambda Function    ¦  DynamoDB        ¦
       ¦  (Node.js 18)       ¦  PAY_PER_REQUEST ¦
       ¦  + CloudWatch Logs  ¦  (Visitor Count) ¦
       +----------------------------------------+
```

---

## ?? Architecture Decision Records

This project documents all major architectural decisions using ADRs (Architecture Decision Records):

| ADR | Decision | Outcome | Savings |
|-----|----------|---------|---------|
| [**ADR-001**](docs/adrs/ADR-001-serverless-architecture.md) | Serverless vs EC2 | **88% cost reduction** | $14.85/month |
| [**ADR-002**](docs/adrs/ADR-002-cloudfront-oac.md) | CloudFront OAC vs OAI | Modern security, future-proof | N/A |
| [**ADR-003**](docs/adrs/ADR-003-dynamodb-ondemand.md) | DynamoDB On-Demand vs Provisioned | **$2.35/month savings** | Cost optimization |
| [**ADR-004**](docs/adrs/ADR-004-github-actions.md) | GitHub Actions vs Jenkins | Simplicity, no infrastructure | Operational efficiency |

**Total Documented Savings:** **$17.20/month** ($206/year)

### Why ADRs Matter

Architecture Decision Records are an industry best practice that:
- ?? Document **why** decisions were made, not just **what**
- ?? Provide **measurable cost analysis** with real numbers
- ?? Enable **informed reversals** when requirements change
- ?? Demonstrate **strategic thinking** to hiring managers
- ?? Show **data-driven decision making**

[**?? View All ADRs »**](docs/adrs/README.md)

---

## ?? Features

### **Production-Grade Portfolio Website**
- ? Responsive design (mobile-first approach)
- ? WCAG 2.1 accessibility compliant
- ? Real-time visitor counter (serverless API)
- ? Custom domain with free SSL certificate
- ? Font Awesome 6.4 professional icons
- ? Modern UI with gradients and animations

### **Serverless Backend**
- ? AWS Lambda for visitor counter logic
- ? API Gateway HTTP API (REST endpoint)
- ? DynamoDB on-demand billing (**cost-optimized**, see ADR-003)
- ? CloudWatch monitoring with alarms

### **DevOps Best Practices**
- ? **Infrastructure as Code:** 500+ lines of Terraform HCL
- ? **CI/CD:** GitHub Actions auto-deploy on push
- ? **Zero-Downtime Deployments:** CloudFront cache invalidation
- ? **Rollback Capability:** S3 versioning + Terraform state
- ? **Cost Optimization:** 88% savings documented (ADR-001)
- ? **Monitoring:** CloudWatch alarms for errors/throttles
- ? **Security:** Private S3, OAC (ADR-002), encryption at rest
- ? **Documentation:** 4 comprehensive ADRs + cost analysis

---

## ??? Tech Stack

### **Frontend**
- HTML5 + CSS3 (Modern gradients, animations)
- Vanilla JavaScript (no framework overhead)
- Font Awesome 6.4 (professional icons)
- Responsive design (mobile-first approach)

### **Backend & Infrastructure**
- **Compute:** AWS Lambda (Node.js 18)
- **API:** API Gateway HTTP API
- **Database:** DynamoDB (on-demand, see ADR-003)
- **CDN:** CloudFront (PriceClass_100)
- **Storage:** S3 (private bucket + versioning)
- **DNS:** Route 53 (hosted zone)
- **SSL:** AWS Certificate Manager (free)
- **IaC:** Terraform 1.0+
- **CI/CD:** GitHub Actions (see ADR-004)

### **Monitoring & Observability**
- CloudWatch Logs (Lambda execution)
- CloudWatch Metrics (API latency, Lambda errors)
- CloudWatch Alarms (error/throttle alerts)
- AWS Budgets ($5/month limit with alerts)

---

## ?? Deployment Strategy

### **Zero-Downtime Deployments**

This architecture achieves zero-downtime deployments without blue/green complexity:
```yaml
Deployment Flow:
1. Push to GitHub main branch
2. GitHub Actions triggers
3. S3 sync (atomic update)
4. CloudFront cache invalidation (paths: /*)
5. New content live in 30-60 seconds
```

**Why Not Blue/Green?** *(See ADR-004 for full analysis)*

Blue/Green deployments are excellent for:
- Container-based apps (ECS/EKS)
- EC2 instances behind load balancers
- Complex microservices requiring traffic splitting

**For serverless static sites:**
- CloudFront cache invalidation = instant updates
- S3 versioning = instant rollback
- No infrastructure duplication needed
- **Lower cost, same zero-downtime result**

### **Rollback Procedures**

**Website Rollback:**
```bash
# S3 versioning enabled - instant rollback
aws s3api list-object-versions --bucket portfolio-bucket
aws s3api copy-object --copy-source "bucket/index.html?versionId=xyz"
aws cloudfront create-invalidation --distribution-id E16FSV0SJ20B4I --paths "/*"
```

**Infrastructure Rollback:**
```bash
# Terraform state management
terraform state list
terraform apply -target=<resource>

# Git-based rollback
git revert <commit-hash>
git push origin main  # Auto-deploy via GitHub Actions
```

---

## ?? Cost Breakdown

### **Documented Cost Analysis** *(from ADR-001 and ADR-003)*

**Traditional EC2 Approach:**
| Service | Monthly Cost |
|---------|-------------|
| t2.micro instance | $8.50 |
| Elastic IP | $3.60 |
| EBS storage (8GB) | $0.80 |
| Data transfer | $3.60 |
| **Total** | **$16.50/month** |

**Serverless Approach (This Project):**
| Service | Usage | Cost/Month |
|---------|-------|------------|
| **S3** | 1GB storage, 10k requests | $0.02 |
| **CloudFront** | 10GB data transfer | $0.85 |
| **Lambda** | 100k invocations | $0.00 (free tier) |
| **DynamoDB** | On-demand (low traffic) | $0.13 |
| **API Gateway** | 100k requests | $0.10 |
| **Route 53** | 1 hosted zone | $0.50 |
| **ACM SSL** | 1 certificate | **FREE** |
| **CloudWatch** | Basic monitoring | $0.10 |
| **TOTAL** | | **$1.70/month** |

**Domain Cost:** $10/year (Porkbun)  
**Grand Total:** **~$30/year** (~$2.50/month)

### **Cost Savings Analysis**

- **vs EC2:** $16.50 - $1.70 = **$14.80/month saved**
- **Percentage:** **88% cost reduction**
- **Annual Savings:** **$177.60/year**

**Optimization Strategies:** *(from ADR-003)*
- ? **On-Demand DynamoDB** (saves $2.35/month vs provisioned)
- ? **CloudFront PriceClass_100** (North America/Europe only)
- ? **S3 Lifecycle Policies** (expire old versions after 30 days)
- ? **Lambda Memory Optimization** (128MB sufficient)
- ? **CloudWatch Log Retention** (7 days, not indefinite)

[**?? View Full Cost Analysis »**](docs/cost-analysis.md)

---

## ?? Setup & Deployment

### **Prerequisites**

- AWS Account (Free Tier eligible)
- Terraform >= 1.0
- AWS CLI configured
- GitHub account
- Domain name (optional but recommended)

### **Local Development**
```bash
# Clone repository
git clone https://github.com/gdawsonkesson/aws-serverless-platform.git
cd aws-serverless-platform/aws-free-tier

# Initialize Terraform
cd terraform
terraform init

# Review infrastructure plan
terraform plan

# Deploy infrastructure
terraform apply

# Upload website
cd ../website
aws s3 sync . s3://your-bucket-name/
```

### **GitHub Actions CI/CD**

The project includes automated deployment via GitHub Actions *(see ADR-004)*:
```yaml
Trigger: Push to main branch
Workflow:
  1. Checkout code
  2. Configure AWS credentials (from secrets)
  3. Sync website to S3
  4. Invalidate CloudFront cache
  5. Deployment summary
```

**Required GitHub Secrets:**
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`

**Setup:**
```bash
# GitHub Settings ? Secrets ? Actions ? New repository secret
AWS_ACCESS_KEY_ID: <your-access-key>
AWS_SECRET_ACCESS_KEY: <your-secret-key>
```

---

## ?? Security

### **Implementation** *(from ADR-002)*

- ? **S3 Bucket:** Private (no public access)
- ? **CloudFront OAC:** Exclusive S3 access (modern, not legacy OAI)
- ? **Encryption:** AES-256 at rest
- ? **HTTPS:** TLS 1.2+ enforced
- ? **SSL Certificate:** AWS Certificate Manager (auto-renewal)
- ? **IAM:** Least privilege policies
- ? **Secrets:** GitHub Actions secrets (not in code)

### **Why CloudFront OAC?** *(from ADR-002)*

**Origin Access Control (OAC)** is the modern successor to Origin Access Identity (OAI):
- ? Supports all S3 buckets (including encrypted)
- ? Better security with SigV4 signing
- ? AWS-recommended best practice
- ? Future-proof (OAI being deprecated)

### **Security Best Practices**
```hcl
# S3 Public Access Block
resource "aws_s3_bucket_public_access_block" "portfolio_website" {
  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}

# CloudFront OAC (not legacy OAI)
resource "aws_cloudfront_origin_access_control" "portfolio_oac" {
  signing_behavior = "always"
  signing_protocol = "sigv4"
}
```

---

## ?? Monitoring & Alerts

### **CloudWatch Alarms**
```hcl
# Lambda Error Rate
- Threshold: > 5 errors in 5 minutes
- Action: SNS notification

# Lambda Throttles
- Threshold: > 10 throttles in 5 minutes
- Action: SNS notification

# API High Latency
- Threshold: > 1000ms average
- Action: SNS notification
```

### **AWS Budgets**
```hcl
# Monthly Budget Alert
- Limit: $5.00/month
- Alerts: 80%, 100% thresholds
- Email notifications configured
```

### **Observability**

- **CloudWatch Logs:** Lambda execution traces
- **CloudWatch Metrics:** Custom visitor count metric
- **X-Ray:** Distributed tracing (optional)

---

## ?? Key Learnings & Decisions

### **Why Serverless?** *(from ADR-001)*

**Serverless vs EC2 Analysis:**
- **Cost:** 88% reduction ($16.50 ? $1.70/month)
- **Scalability:** Auto-scales with traffic (0 to millions)
- **Maintenance:** Zero server management
- **Availability:** 99.99% SLA (CloudFront)
- **Security:** Reduced attack surface (no SSH, no OS patching)

**Trade-offs Considered:**
- ? Cold start latency (~200ms first request)
- ? Vendor lock-in (AWS-specific)
- ? Acceptable for static portfolio use case
- ? Cost savings justify trade-offs

[**?? Read Full Analysis: ADR-001 »**](docs/adrs/ADR-001-serverless-architecture.md)

### **Why CloudFront OAC over OAI?** *(from ADR-002)*

**Modern Security Best Practice:**
- ? Supports encrypted S3 buckets
- ? SigV4 signing (more secure)
- ? AWS-recommended (OAI being deprecated)
- ? Future-proof architecture

[**?? Read Full Analysis: ADR-002 »**](docs/adrs/ADR-002-cloudfront-oac.md)

### **Why DynamoDB On-Demand?** *(from ADR-003)*

**Cost Optimization:**
- **Provisioned Capacity:** $2.48/month (minimum)
- **On-Demand:** $0.13/month (actual traffic)
- **Savings:** $2.35/month (95% reduction)

**Best for:**
- Unpredictable traffic patterns
- Low-volume applications
- Cost-sensitive projects

[**?? Read Full Analysis: ADR-003 »**](docs/adrs/ADR-003-dynamodb-ondemand.md)

### **Why GitHub Actions over Jenkins?** *(from ADR-004)*

**For This Project:**
- ? No infrastructure to maintain
- ? Free for public repositories
- ? Integrated with GitHub
- ? Simple YAML configuration
- ? Secrets management built-in

**Jenkins is Better For:**
- Complex enterprise pipelines
- Self-hosted requirements
- Advanced plugin ecosystems

[**?? Read Full Analysis: ADR-004 »**](docs/adrs/ADR-004-github-actions.md)

### **Why Custom Domain?**

**Professional Benefits:**
- ? Brand credibility (gdawsonkesson.com vs cloudfront.net)
- ? SEO optimization
- ? Custom email (info@gdawsonkesson.com)
- ? Professional appearance on resume/LinkedIn
- ? Demonstrates DNS/SSL knowledge

**Cost:** ~$16/year (minimal for professional impact)

---

## ?? Project Structure
```
aws-serverless-platform/
+-- .github/
¦   +-- workflows/
¦       +-- manual-deploy.yml          # GitHub Actions CI/CD
+-- aws-free-tier/
¦   +-- terraform/
¦   ¦   +-- main.tf                    # CloudFront, S3, Lambda, API, DynamoDB
¦   ¦   +-- security.tf                # S3 encryption, versioning, lifecycle
¦   ¦   +-- cost-monitoring.tf         # SNS, budgets, alarms
¦   ¦   +-- route53.tf                 # DNS hosted zone, nameservers
¦   ¦   +-- acm.tf                     # SSL certificate (us-east-1)
¦   ¦   +-- dns-records.tf             # A records for custom domain
¦   ¦   +-- variables.tf               # Input variables
¦   ¦   +-- outputs.tf                 # Terraform outputs
¦   ¦   +-- provider.tf                # AWS provider config
¦   +-- lambda/
¦   ¦   +-- index.js                   # Visitor counter logic
¦   +-- website/
¦       +-- index.html                 # Production-ready portfolio UI
+-- docs/
¦   +-- adrs/
¦   ¦   +-- README.md                  # ADR index
¦   ¦   +-- ADR-001-serverless-architecture.md
¦   ¦   +-- ADR-002-cloudfront-oac.md
¦   ¦   +-- ADR-003-dynamodb-ondemand.md
¦   ¦   +-- ADR-004-github-actions.md
¦   +-- cost-analysis.md               # Detailed cost breakdown
¦   +-- diagrams/                      # Architecture diagrams (ready)
¦   +-- runbooks/                      # Operational runbooks (ready)
+-- testing/
¦   +-- results/                       # Test results (ready)
+-- README.md                          # This file
```

---

## ?? Testing

### **Infrastructure Validation**
```bash
# Terraform syntax check
terraform fmt -check
terraform validate

# Infrastructure plan review
terraform plan

# Cost estimation
terraform plan -out=plan.tfplan
terraform show -json plan.tfplan | jq
```

### **Website Testing**
```bash
# Local testing
python -m http.server 8000
# Visit http://localhost:8000

# CloudFront testing
curl -I https://gdawsonkesson.com
# Expected: 200 OK, SSL certificate valid

# API testing
curl https://o618nkadvg.execute-api.us-east-2.amazonaws.com/count
# Expected: {"count": N}
```

### **Performance Testing**
```bash
# CloudFront response time
curl -w "@curl-format.txt" -o /dev/null -s https://gdawsonkesson.com
# Expected: < 200ms globally

# Lighthouse audit (Google Chrome DevTools)
# Expected: 90+ Performance, 100 Accessibility, 100 Best Practices
```

---

## ?? Related Projects

This serverless portfolio is part of a **3-repository DevOps ecosystem** demonstrating both serverless and Kubernetes expertise:

### **Enterprise Kubernetes DevOps Ecosystem** (140+ commits)

| Repository | Focus | Commits |
|------------|-------|---------|
| [**eks-infra-automation**](https://github.com/gdawsonkesson/eks-infra-automation) | Infrastructure layer: EKS, Istio, ArgoCD, Kyverno, Prometheus | 68 |
| [**online-boutique-gitops**](https://github.com/gdawsonkesson/online-boutique-gitops) | GitOps layer: Kustomize overlays, HPA, PDB, NetworkPolicies | 45 |
| [**online-boutique-application**](https://github.com/gdawsonkesson/online-boutique-application) | Application layer: 11 microservices, Trivy scanning, CI/CD | 27 |

**Combined Tech Stack:**
- Kubernetes (EKS) + Istio Service Mesh
- ArgoCD GitOps + Kustomize
- Kyverno Policy Engine + Trivy Security Scanning
- Prometheus + Grafana + AlertManager
- Multi-AZ High Availability

**This demonstrates:**
- ? Serverless expertise (this repo)
- ? Kubernetes expertise (3-repo ecosystem)
- ? GitOps practices (ArgoCD)
- ? Security hardening (Kyverno + Trivy)
- ? Production observability (Prometheus stack)

---

## ?? Contributing

This is a personal portfolio project, but feedback and suggestions are welcome!

**How to suggest improvements:**
1. Open an issue describing your suggestion
2. Include architectural reasoning
3. Consider cost/complexity tradeoffs
4. Reference relevant ADRs if applicable

---

## ?? License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## ?? Author

**George Dawson-Kesson**  
AWS Certified Solutions Architect - Associate (SAA-C03)

- ?? Portfolio: [gdawsonkesson.com](https://gdawsonkesson.com)
- ?? LinkedIn: [linkedin.com/in/gdawsonkesson](https://www.linkedin.com/in/gdawsonkesson)
- ?? GitHub: [github.com/gdawsonkesson](https://github.com/gdawsonkesson)
- ?? Email: [info@gdawsonkesson.com](mailto:info@gdawsonkesson.com)

---

## ?? Acknowledgments

- AWS Well-Architected Framework for architectural guidance
- Terraform Registry for module documentation
- AWS Free Tier for enabling cost-effective learning
- ADR documentation practices from Michael Nygard's work

---

## ?? Project Status

? **Production** - Live and actively maintained

**Last Updated:** March 2026  
**Infrastructure Version:** 1.0.0  
**Terraform Version:** 1.0+  
**AWS Region:** us-east-2 (Ohio)  
**Documentation:** 4 ADRs + cost analysis

---

<div align="center">

**Built with ?? using AWS, Terraform, and DevOps best practices**

[![Deploy Status](https://img.shields.io/badge/Deploy-Passing-success?style=for-the-badge)](https://github.com/gdawsonkesson/aws-serverless-platform/actions)
[![Uptime](https://img.shields.io/badge/Uptime-99.99%25-brightgreen?style=for-the-badge)](https://gdawsonkesson.com)
[![Cost Optimized](https://img.shields.io/badge/Cost%20Savings-88%25-orange?style=for-the-badge)](docs/adrs/ADR-001-serverless-architecture.md)
[![Documented](https://img.shields.io/badge/ADRs-4-blue?style=for-the-badge)](docs/adrs/README.md)

</div>
