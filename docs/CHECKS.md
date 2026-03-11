# Security Checks

Cloud Auditor performs over 200+ automated security audits across your AWS environment. Below is a summary of the key areas covered.

## 🛡️ Core Audit Categories

### Identity & Access Management (IAM)
- Root account MFA status and usage.
- Over-privileged IAM users and roles.
- Access key rotation and age monitoring.
- Passwords policies and strength validation.

### Networking & Content Delivery (VPC/CloudFront)
- Security Group rules allowing unrestricted access (0.0.0.0/0).
- Publicly accessible VPC subnets and endpoints.
- CloudFront distribution security headers and WAF integration.

### Storage (S3 / EBS / RDS)
- Publicly accessible S3 buckets and objects.
- Unencrypted S3 buckets, EBS volumes, and RDS databases.
- S3 Bucket Policy and ACL sanity checks.

### Compute (EC2 / Lambda)
- EC2 instance vulnerability scanning (metadata service, IMDSv2).
- Lambda function permission and environment variable security.
- Security Group configurations for critical ports (SSH, RDP, DB).

### Compliance Mappings
Every scan result is automatically mapped to:
- **SOC 2 Type II**
- **HIPAA Security Rule**
- **CIS AWS Foundations Benchmark**
- **ISO 27001:2022**

> [!NOTE]
> The exact logic of these checks is proprietary. For enterprise inquiries regarding custom check development, please contact us.
