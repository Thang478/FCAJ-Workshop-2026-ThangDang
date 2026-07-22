---
title: "Restrict Direct Access to the ALB"
date: 2026-07-22
weight: 17
chapter: false
pre: " <b> 5.3.17. </b> "
---

# Forward only requests with the CloudFront custom header

The ALB is Internet-facing, so its DNS name can still be accessed directly. If the default listener rule forwards every request, users can bypass CloudFront and WAF. The team uses a custom origin header to identify requests sent by CloudFront.

## 1. Add a Custom Origin Header in CloudFront

Open the CloudFront Distribution, select the ALB Origin, and choose **Edit**. Under **Add custom header**, enter:

- **Header name:** `X-MalScanAI-Origin`
- **Value:** a long random string

![Redacted Custom Origin Header](custom-header-redacted.png)

The header value is treated as a configuration secret. The real value is not included in public Markdown or screenshots.

## 2. Create a listener rule that checks the header

On the ALB, open **Listeners and rules → Manage rules**.

![Open the listener rules](listener-rules.png)

Add the condition:

```text
HTTP header: X-MalScanAI-Origin
Value: <CUSTOM_SECRET_VALUE>
```

![HTTP header condition](header-condition.png)

Set the action to:

```text
Forward to: malscanai-streamlit-tg
```

![Forward to the Target Group](forward-action.png)

Set the rule priority so that the header rule is evaluated before the default rule.

![Set listener rule priority](rule-priority.png)

![Review the listener rule](rule-review.png)

## 3. Change the default rule to 403

Change the default action to **Return fixed response**:

```text
Status code: 403
Content type: text/plain
Response body: Forbidden
```

![Default rule returns 403](default-403.png)

After this configuration:

- A request through CloudFront has the correct header and is forwarded to ECS.
- A direct request to the ALB has no header and receives `403`.

{{% notice warning %}}
The custom header is suitable for limiting direct ALB access in this student architecture, but it does not replace user authentication. If the value is exposed, update it in both the CloudFront Origin and the ALB listener rule.
{{% /notice %}}
