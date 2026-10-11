---
title: "Resource Cleanup"
weight: 13
pre: " <b> 4.13 </b> "
---

# Resource Cleanup

## Objective

Delete AWS resources that are no longer needed after completing the Workshop.

Cleaning up resources helps avoid maintaining unnecessary resources and prevents additional costs.

---

## 1. Stop and Terminate the EC2 Instance

Navigate to:

```text
AWS Console
→ EC2
→ Instances
```

Select the Expense Tracker instance.

Perform the following action:

```text
Instance state
→ Terminate instance
```

After termination, verify that the instance is no longer in the Running state.

![alt text](/WorkshopAWS/images/4-Workshop/4.13/EC2_clear.png)

---

## 2. Delete the Security Group

Navigate to:

```text
AWS Console
→ EC2
→ Security Groups
```

Select:

```text
expense-tracker-sg
```

Delete the Security Group after the EC2 instance has been terminated.

![alt text](/WorkshopAWS/images/4-Workshop/4.13/SecurityGr_clear.png)

---

## 3. Delete the Public Subnet

Navigate to:

```text
AWS Console
→ VPC
→ Subnets
```

Select:

```text
expense-tracker-public-subnet
```

Perform the following action:

```text
Delete subnet
```

![alt text](/WorkshopAWS/images/4-Workshop/4.13/Subnet_clear.png)

---

## 4. Delete the Route Table

Navigate to:

```text
AWS Console
→ VPC
→ Route Tables
```

Select the Route Table created for Expense Tracker.

Delete the Route Table after the subnet has been deleted or is no longer associated with it.

![alt text](/WorkshopAWS/images/4-Workshop/4.13/Routetable_clear.png)

---

## 5. Detach and Delete the Internet Gateway

Navigate to:

```text
AWS Console
→ VPC
→ Internet Gateways
```

Select:

```text
expense-tracker-igw
```

Perform the following action:

```text
Detach from VPC
```

Then:

```text
Delete Internet Gateway
```

![alt text](/WorkshopAWS/images/4-Workshop/4.13/internet_gate_clear.png)

---

## 6. Delete the VPC

Navigate to:

```text
AWS Console
→ VPC
→ Your VPCs
```

Select:

```text
expense-tracker-vpc
```

Perform the following action:

```text
Delete VPC
```

Only perform this step after all dependent resources have been deleted.

![alt text](/WorkshopAWS/images/4-Workshop/4.13/VPC_clear.png)

---

## 7. Delete the Lambda Function

Navigate to:

```text
AWS Console
→ Lambda
→ Functions
```

Select:

```text
expense-tracker-statistics
```

Perform the following action:

```text
Actions
→ Delete function
```

Confirm the deletion of the function.

![alt text](/WorkshopAWS/images/4-Workshop/4.13/Lambda_clear.png)

---

## 8. Delete the EventBridge Scheduler

Navigate to:

```text
AWS Console
→ EventBridge
→ Scheduler
```

Select:

```text
expense-tracker-daily-statistics
```

Perform the following action:

```text
Delete
```

Confirm the deletion of the Scheduler.

![alt text](/WorkshopAWS/images/4-Workshop/4.13/EventBridge_clear.png)

![alt text](/WorkshopAWS/images/4-Workshop/4.13/Alarms_clear.png)

---

## 9. Delete CloudWatch Logs

Navigate to:

```text
AWS Console
→ CloudWatch
→ Logs
→ Log groups
```

Select:

```text
/aws/lambda/expense-tracker-statistics
```

Perform the following action:

```text
Delete
```

![alt text](/WorkshopAWS/images/4-Workshop/4.13/Cloudwatch_clear.png)

---

## 10. Review IAM Resources

Review the Users, Groups, or Policies created specifically for the Workshop.

If they are no longer needed, the corresponding IAM resources can be deleted.

Do not delete IAM accounts or permissions that are still being used by other systems.

---

## 12. Verify AWS Resources

After completing the cleanup process, review the following resources:

```text
EC2
VPC
Subnet
Internet Gateway
Security Group
Lambda
EventBridge Scheduler
CloudWatch Logs
IAM
```

Ensure that all unused resources have been properly handled.

---

## 13. Results

The AWS resources created during the Workshop have been reviewed and cleaned up after completion.

Resources that are still required for development may be retained, particularly the MongoDB Atlas database if the application continues to be used.
