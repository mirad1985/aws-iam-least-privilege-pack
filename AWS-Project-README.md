 # AWS IAM Least-Privilege Security Pack

This repo contains a small set of reusable IAM policies that follow the principle of least privilege. It is meant to be a portfolio project to demonstrate practical cloud security skills.

## What's included

### 1. S3 Upload-Only Policy

- File: `policies/s3-upload-only.json`
- Allows:
  - `s3:ListBucket` on a single bucket, limited to the `uploads/` prefix
  - `s3:PutObject` and `s3:AbortMultipartUpload` on `uploads/*`
- Blocks:
  - Deletes
  - Reads from other prefixes
  - Access to other buckets
- Use case: locked-down role for uploading assets to a dedicated path in one bucket.

### 2. EC2 Read-Only Policy

- File: `policies/ec2-read-only.json`
- Allows:
  - `ec2:Describe*`, ELB `Describe*`, ASG `Describe*`
  - CloudWatch `Describe*`, `Get*`, `List*`
- Use case: auditors, monitoring tools, or engineers who need visibility without the ability to start/stop/terminate resources.

### 3. Lambda Execution Logs Policy

- File: `policies/lambda-exec-role.json`
- Allows:
  - CloudWatch Logs creation + writes
  - AWS X-Ray trace + telemetry
- Use case: basic execution role permissions for Lambda without extra, unused privileges.

## Before / After: Fixing IAM Anti-Patterns

- Insecure example: `before_after/s3-full-access-insecure.json`
  - Grants `s3:*` on `*` (full admin across all buckets).
- Secure replacement: `before_after/s3-upload-only-secure.json`
  - Restricts to upload-only on a single bucket + prefix.

This shows how to go from `*` wildcard admin patterns to tightly scoped actions and resources.

## Deploying with AWS CLI

Prereqs:

- AWS account and IAM user/role with permission to create policies.
- AWS CLI configured: `aws configure`

Then run:

```bash
chmod +x deploy.sh
./deploy.sh
