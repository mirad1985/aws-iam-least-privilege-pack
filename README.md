# AWS Least Privilege IAM Role Deployment Pack 
*A hands-on cloud security project demonstrating IAM role creation, trust policies, and least-privilege access control.*

### **Overview**

This project automates the deployment of a least-privilege IAM role using AWS CLI and custom JSON policies.

The project includes:
- A deploy script ('deploy.sh')
- A trust policy controlling who can assume the role
- A least-privilege policy defining what the role can do
- EC2, Lambda, and S3 least-privilege JSON files
- A before/after comparison showing how privilege reduction works

This project demonstrates the skills of:
- IAM architecture
- Identity-based vs resource-based policies
- Trust policies and role assumption
- Least privilege enforcement
- AWS CLI automation
- Policy testing and validation

### **Features**
- Automated IAM Role Creation
- Automated IAM Policy Attachment
- Testable CLI commands
- Complete least-privilege JSON
- No manual AWS Console steps required

### **Architecture Diagram**
flowchart TD

    DevLaptop["Developer Machine (AWS CLI)"]
    DeployScript["deploy.sh"]
    IAMRole["IAM Role: least-privilege-demo-role"]
    TrustPolicy["trust-policy.json"]
    IAMPolicy["iam-policy.json"]

    DevLaptop --> DeployScript
    DeployScript --> IAMRole
    IAMRole --> TrustPolicy
    IAMRole --> IAMPolicy

### **Project Directory Structure**

<img width="239" height="315" alt="project-directory-structure" src="https://github.com/user-attachments/assets/1d250365-f598-4597-a645-578e28e90bbf" />


### **How to Run the Project (Step-by-Step)**

### Prerequisites
- AWS CLI installed
- IAM user with permissions to:
  - iam: CreateRole
  - iam:PutRolePolicy
  - iam: ListRoles
  - sts:GetCallerIdentity
 
### Deployment
chmod +x deploy.sh
./deploy.sh

#Validate Role Created
aws iam list-roles | grep least-privilege-demo-role

### **Before & After**

### Before
{
  "Effect": "Allow",
  "Action": "*",
  "Resource": "*"
}

### After (least-privilege)
{
  "Effect": "Allow",
  "Action": ["s3:PutObject"],
  "Resource": ["arn:aws:s3:::mybucket/uploads/*"]
}

  
### **Security Concepts Demonstrated**
- Principle of Least Privilege: Role and policy grant only what is required and nothing more
- IAM Trust vs Permissions Policy
  - Trust policy: who can assume the role
  - Permissions policy: what the role is allowed to do
- Infrastructure-as-Code Style Scripting: Bash workflow automates IAM resource creation
- Defense-in-Depth: Include EC2, Lambd, and S3 least-privilege patterns

### **Use Cases**
- Creating secure IAM roles for applications
- Auditing over-permissioned AWS environments
- Demonstrating IAM best practices
- Teaching least-privilege patterns for EC2/Lambda/S3

**Author:** Michelle Radecker
Linkedin: https://www.linkedin.com/in/mradecker/
GitHub: https://github.com/mirad1985



