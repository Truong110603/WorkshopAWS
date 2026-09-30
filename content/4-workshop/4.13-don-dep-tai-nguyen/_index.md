---
title: "Cleaning Up Resources"
weight: 13
pre: " <b> 4.13 </b> "
---

# Cleaning Up Resources

## Objectives

Delete AWS resources that are no longer used after completing the Workshop.

Cleaning up unused resources helps avoid maintaining unnecessary resources and reduces the possibility of additional costs.

---

## 1. Stop and Terminate EC2

Go to:

```text
AWS Console

→ EC2

→ Instances
```

Select the Expense Tracker instance.

Perform:

```text
Instance state

→ Terminate instance
```

After termination, check that the instance is no longer in the `Running` state.

---

## 2. Delete the Security Group

Go to:

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

---

## 3. Delete the Public Subnet

Go to:

```text
AWS Console

→ VPC

→ Subnets
```

Select:

```text
expense-tracker-public-subnet
```

Perform:

```text
Delete subnet
```

---

## 4. Delete the Route Table

Go to:

```text
AWS Console

→ VPC

→ Route Tables
```

Select the Route Table created for Expense Tracker.

Delete the Route Table after the Subnet has been deleted or after it no longer has any associations.

---

## 5. Detach and Delete the Internet Gateway

Go to:

```text
AWS Console

→ VPC

→ Internet Gateways
```

Select:

```text
expense-tracker-igw
```

Perform:

```text
Detach from VPC
```

Then:

```text
Delete Internet Gateway
```

---

## 6. Delete the VPC

Go to:

```text
AWS Console

→ VPC

→ Your VPCs
```

Select:

```text
expense-tracker-vpc
```

Perform:

```text
Delete VPC
```

Only perform this step after all dependent resources have been deleted.

---

## 7. Delete the Lambda Function

Go to:

```text
AWS Console

→ Lambda

→ Functions
```

Select:

```text
expense-tracker-statistics
```

Perform:

```text
Actions

→ Delete function
```

Confirm the deletion of the Function.

---

## 8. Delete the EventBridge Scheduler

Go to:

```text
AWS Console

→ EventBridge

→ Scheduler
```

Select:

```text
expense-tracker-daily-statistics
```

Perform:

```text
Delete
```

Confirm the deletion of the Scheduler.

---

## 9. Delete CloudWatch Logs

Go to:

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

Perform:

```text
Delete
```

---

## 10. Check IAM

Check the Users, Groups, or Policies created specifically for the Workshop.

If they are no longer required, the corresponding IAM resources can be deleted.

Do not delete IAM accounts or permissions that are currently being used by other systems.

---

## 11. Check MongoDB Atlas

MongoDB Atlas is outside the AWS environment.

If the Expense Tracker is no longer being used, the database or cluster can be removed according to the MongoDB Atlas configuration.

If the application will continue to be developed or used, the MongoDB Atlas database can be kept.

---

## 12. Check AWS Resources

After completing the cleanup, check the following resources:

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

Make sure that unused resources have been properly deleted or otherwise handled.

---

## 13. Result

The AWS resources created for the Workshop have been reviewed and cleaned up after completion.

Resources that are still required for development can be kept, especially the MongoDB Atlas database if the application will continue to be used.