---
title: "AWS resource clean-up"
date: 2026-07-24
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

# Clean up after the workshop

Fargate, the NAT Gateway, and the Application Load Balancer create most of the time-based cost. After the demonstration and evidence collection are complete, resources should be removed in the dependency-aware order below.

{{% notice danger %}}
Deleting Amazon EFS permanently removes the database, accounts, scan history, and application data under `/app/data`. Back up any required data before continuing.
{{% /notice %}}

## 1. Prepare before deletion

- Download or back up required data from `/app/data`, especially `malscan.db`.
- Preserve the demo video, configuration screenshots, testing evidence, and AWS Pricing Calculator estimate.
- Confirm that no resource is shared with another project.
- Record required domain names, resource names, and ARNs for the report.

## 2. Remove the application DNS record

Open **Route 53 → Hosted zones**, select the hosted zone, and remove only the record for:

```text
malscanai.sadc.io.vn
```

Do not delete the entire `sadc.io.vn` hosted zone when other subdomains or systems still depend on it.

## 3. Delete AWS User Notifications and the CloudWatch alarm

1. Open **AWS User Notifications → Notification configurations**.
2. Delete `malscanai-alarm-email` and any delivery channel that is no longer required.
3. Open **CloudWatch → Alarms**.
4. Select `malscanai-unhealthy-target-alarm` and choose **Delete**.

These resources are not the primary cost drivers, but removing them prevents events from obsolete resources.

## 4. Disable and delete the CloudFront distribution

1. Open **CloudFront → Distributions → malscanai-cloudfront**.
2. Choose **Disable**.
3. Wait until the configuration change has finished deploying.
4. Select the distribution and choose **Delete**.
5. Confirm that the Flat-Rate Plan is no longer attached to the deleted distribution.

A CloudFront distribution must be disabled before it can be deleted.

## 5. Delete the ECS service

1. Open **ECS → Clusters → malscanai-cluster → Services**.
2. Select `malscanai-service`.
3. Choose **Delete service** and confirm force deletion when requested.
4. Wait for the task to become `Stopped` and for its network interface to be released.

The desired count can be reduced to `0` first for observation, but deleting the service through the Console also stops its service tasks.

## 6. Delete the Application Load Balancer and target group

After the ECS service no longer has a running target:

1. Open **EC2 → Load Balancers** and delete `malscanai-alb`.
2. Wait for the load balancer deletion to complete.
3. Open **EC2 → Target Groups** and delete `malscanai-streamlit-tg`.

The ALB is billed over time, so it should be removed immediately after the ECS service.

## 7. Delete the ECS cluster and old task definitions

1. Delete the ECS cluster after it contains no service or task.
2. Open **ECS → Task definitions → malscanai-task**.
3. Deregister revisions that are no longer required.

Stored task definitions do not create compute charges, but cleaning old revisions reduces the risk of deploying an obsolete version.

## 8. Delete EFS

1. Confirm that no ECS task still mounts the file system.
2. Open **EFS → Access points** and delete `malscanai-data-ap`.
3. Open `malscanai-efs` and review its mount targets.
4. Delete the mount targets, or use the Console file-system deletion flow so the Console handles the associated mount targets.
5. Delete the file system and confirm the correct file-system ID.

EFS cannot be deleted while active mount targets or dependent resources remain.

## 9. Delete ECR images and repositories

Open **ECR → Private repositories** and process:

```text
malscanai-streamlit
malscanai-url-engine
```

- Delete image tags that are no longer required.
- Choose **Delete repository** and use forced deletion when images remain.

To preserve recovery capability, retain only the required rollback images. ECR continues to charge for stored data.

## 10. Delete the Secrets Manager secret

1. Open **Secrets Manager → Secrets**.
2. Select `malscanai/virustotal-api-key`.
3. Choose **Delete secret**.
4. Select an appropriate recovery window and confirm scheduled deletion.

Never copy the secret value into the report or clean-up screenshots.

## 11. Delete CloudWatch logs

1. Open **CloudWatch → Log groups**.
2. Select `/ecs/malscanai`.
3. Delete the log group after preserving the evidence required by the report.

When immediate deletion is not desired, set a seven-day retention period instead of retaining logs indefinitely.

## 12. Delete the NAT Gateway and release the Elastic IP

1. Open **VPC → NAT gateways**.
2. Select the MalScanAI NAT Gateway and choose **Delete NAT gateway**.
3. Wait until its state becomes `Deleted`.
4. Open **EC2 → Elastic IP addresses**.
5. Select the Elastic IP that was attached to the NAT Gateway and choose **Release Elastic IP address**.

{{% notice warning %}}
Deleting a NAT Gateway disassociates its Elastic IP but does not release the address. An unreleased public IPv4 address can continue to incur charges.
{{% /notice %}}

## 13. Delete the remaining network resources

After the ALB, ECS task, EFS mount targets, and NAT Gateway are gone:

1. Remove custom routes that still reference the NAT Gateway.
2. Delete custom route tables and subnet associations.
3. Delete the private and public subnets.
4. Delete the ALB, ECS, and EFS security groups.
5. Detach the Internet Gateway from the VPC and delete it.
6. Delete `malscanai-vpc`.

When a security group or subnet cannot be deleted, inspect remaining network interfaces created by the ALB, ECS, EFS, or NAT Gateway.

## 14. Handle ACM and Route 53

- A public ACM certificate has no separate charge, but it can be deleted when it is dedicated to MalScanAI and is no longer attached to CloudFront.
- Delete the hosted zone only when the entire domain is no longer required. For a shared domain, remove only the MalScanAI record.

## 15. Final verification

Review:

- **Billing and Cost Management → Cost Explorer**
- **EC2 → Elastic IP addresses**
- **VPC → NAT gateways**
- **EC2 → Load Balancers**
- **ECS → Clusters**
- **EFS → File systems**
- **ECR → Repositories**
- **CloudWatch → Log groups**

Verification table:

| Resource | Expected post-clean-up state |
|---|---|
| ECS service and task | Deleted or `Stopped` |
| ALB and target group | Removed |
| NAT Gateway | `Deleted` |
| Elastic IP | Released |
| EFS | Deleted after backup |
| ECR | Deleted or intentionally retained |
| CloudWatch log group | Deleted or short retention configured |
| Secret | Deletion scheduled |
| Route 53 record | MalScanAI record removed |

{{% notice note %}}
Billing and Cost Explorer can update with a delay. Continue reviewing charges for several days after clean-up to ensure that no billable resource remains unexpectedly active.
{{% /notice %}}

