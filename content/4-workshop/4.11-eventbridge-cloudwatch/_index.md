---
title: "Configuring EventBridge and CloudWatch"
weight: 11
pre: " <b> 4.11 </b> "
---

# Configuring EventBridge and CloudWatch

## Objectives

Configure an automatic schedule to invoke the Lambda function and monitor its execution logs using CloudWatch.

---

## 1. EventBridge Scheduler

### a. Create the Scheduler

Create an EventBridge Scheduler:

```text
expense-tracker-daily-statistics
```

![alt text](/WorkshopAWS/images/4-Workshop/4.11/EventBridge1.png)

Set the Target to:

```text
expense-tracker-statistics
```

![alt text](/WorkshopAWS/images/4-Workshop/4.11/EventBridge3.png)

---

### b. Schedule

The Scheduler uses:

```text
rate(1 day)
```

![alt text](/WorkshopAWS/images/4-Workshop/4.11/EventBridge2.png)

The Lambda function is invoked automatically according to the configured schedule.

During testing, a shorter schedule can be used to verify that the Scheduler is working correctly.

---

### c. Input

The Lambda function does not require input data:

```json
{}
```

The processing flow is:

```text
EventBridge

      ↓

Lambda

      ↓

MongoDB Atlas

      ↓

statistics
```

---

## 2. CloudWatch

### a. Lambda Logs

The Lambda function writes execution logs to CloudWatch.

Log Group:

```text
/aws/lambda/expense-tracker-statistics
```

Access the logs through:

```text
AWS Console
→ CloudWatch
→ Logs
→ Log groups
```

![alt text](/WorkshopAWS/images/4-Workshop/4.11/Cloudwatchgroup.png)

---

### b. Log Content

The Lambda execution logs contain information generated during the processing:

![alt text](/WorkshopAWS/images/4-Workshop/4.11/CloudwatchLogStream.png)

The logs can be used to check the Lambda execution process and processing results.

---

### c. CloudWatch Alarms

![alt text](/WorkshopAWS/images/4-Workshop/4.11/CloudwatchAlarms.png)

CloudWatch Alarms can be used to generate notifications when a monitored metric exceeds a configured threshold.

In the configuration shown above, the `CPUUtilization` threshold is set to **80%**.

---

## 3. Monitoring Lambda

CloudWatch is used to monitor:

- Whether Lambda is invoked.
- Execution time.
- Function logs.
- Processing results.
- Messages generated during execution.

![alt text](/WorkshopAWS/images/4-Workshop/4.11/CloudwatchLogEvent.png)

---

## 4. Complete Workflow

The complete processing flow is:

```text
EventBridge Scheduler

          ↓

expense-tracker-statistics

          ↓

MongoDB Atlas

          ↓

statistics

          ↓

Backend API

          ↓

Frontend
```

CloudWatch monitors the Lambda execution:

```text
Lambda

   ↓

CloudWatch Logs
```

---

## 5. Result

EventBridge Scheduler and CloudWatch complete the automatic processing and monitoring components of the Lambda-based statistics system.

The Lambda function is invoked automatically according to the configured schedule, while CloudWatch stores the execution logs for monitoring and verification.