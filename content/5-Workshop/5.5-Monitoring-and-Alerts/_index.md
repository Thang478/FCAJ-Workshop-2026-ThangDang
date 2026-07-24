---
title: "Logs, metrics, and alarms"
date: 2026-07-24
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

# Monitoring MalScanAI

The team uses Amazon CloudWatch to centralize logs from both containers, view default ECS and ALB metrics, and create an alarm for target-group health.

## 1. ECS CPU and memory

The ECS service **Health and metrics** tab provides `CPUUtilization` and `MemoryUtilization`. The captured interval shows low CPU use during most of the test and memory use of approximately 23.7% at the time of observation. This indicates that the current 2-vCPU and 4-GB configuration has spare capacity for the demonstration workload.

![ECS CPU and memory metrics](ecs-metrics.png)

## 2. ALB metrics

The Application Load Balancer provides request, response-time, HTTP-status, and target-health metrics. These graphs confirm that the ALB receives traffic and forwards requests to the target.

![Application Load Balancer metrics](alb-metric.png)

Important operational metrics include:

- `RequestCount`
- `TargetResponseTime`
- `HTTPCode_Target_5XX_Count`
- `HealthyHostCount`
- `UnHealthyHostCount`

## 3. Streamlit logs

The Streamlit container records file reception, ZIP extraction, sample checks, and analysis progress. A separate log stream makes it possible to troubleshoot each task without directly connecting to the container.

![Streamlit processing logs](streamlit-log.png)

## 4. URL Engine logs

The URL Engine log confirms that the AI model was loaded and the Flask service listens internally on port `5000`. Streamlit calls this service inside the same task through `127.0.0.1:5000`.

![URL Engine startup logs](url-engine-log.png)

The log also contains a model-library version warning and the Flask development-server warning. The team records these as limitations to address by aligning library versions and using a production WSGI server.

## 5. Create a target-health CloudWatch alarm

The alarm uses the `UnHealthyHostCount` metric for the exact Application Load Balancer and target-group pair.

![Select UnHealthyHostCount](alarm-select-metric.png)

Configuration:

```text
Metric: UnHealthyHostCount
Statistic: Minimum
Period: 1 minute
Threshold type: Static
Condition: Greater than or equal to 1
Datapoints to alarm: 2 out of 2
Missing data: Treat missing data as good
```

![Alarm condition configuration](alarm-conditions.png)

No SNS action is attached during alarm creation. The alarm still records its state and history in CloudWatch.

![No SNS action configured](alarm-no-actions.png)

The alarm is named `malscanai-unhealthy-target-alarm`. Immediately after creation, it can remain in `Insufficient data` while CloudWatch waits for enough evaluation datapoints.

![Created CloudWatch alarm](alarm-created.png)

## 6. Deliver alarm events with AWS User Notifications

To avoid adding Amazon SNS to the architecture, the team creates an AWS User Notifications configuration for **CloudWatch Alarm State Change** events. The rule receives only the MalScanAI alarm event when its new state is `ALARM`.

![Create the User Notifications configuration](user-notification-rule.png)

The advanced filter limits the event by alarm name and state:

```json
{
  "detail": {
    "alarmName": ["malscanai-unhealthy-target-alarm"],
    "state": {
      "value": ["ALARM"]
    }
  }
}
```

An email address is added as a delivery channel and must be verified before notifications can be delivered.

![Add the email delivery channel](ser-notification-email-channel.png)

![Verify the email address](user-notification-email-verify.png)

After setup, both the notification configuration and the email channel are `Active`.

![Active User Notifications configuration](user-notification-active.png)

{{% notice note %}}
A CloudWatch alarm sends state-change events; it does not generate a PDF report. A scheduled report with charts and attachments requires a separate workflow such as EventBridge, Lambda, and Amazon SES.
{{% /notice %}}

