---
title: "Create the CloudFront Distribution"
date: 2026-07-22
weight: 16
chapter: false
pre: " <b> 5.3.16. </b> "
---

# Place CloudFront and WAF in front of the ALB

CloudFront is the public entry point for MalScanAI. Users connect to CloudFront through HTTPS, and CloudFront forwards valid requests to the ALB.

## 1. Start creating the Distribution

Go to **CloudFront → Distributions** and choose **Create distribution**. If the console displays plan options, select the plan that fits the demonstration and avoid optional paid features that are not required.

![Select the CloudFront plan](cloudfront-plan.png)

![Start creating the Distribution](cloudfront-start.png)

## 2. Select the ALB as the Origin

Under Origin, configure:

- **Origin domain:** the DNS name of `malscanai-alb`
- **Origin type:** Custom origin / ALB
- **Origin protocol:** HTTP in the current setup

![Select the ALB origin](cloudfront-origin.png)

CloudFront does not call the ECS task directly. The ALB continues to perform health checks and sends requests only to healthy targets.

## 3. Configure the Cache Behavior

Streamlit is a dynamic application, so the team does not cache it like a static website. Main settings include:

- **Viewer protocol policy:** Redirect HTTP to HTTPS
- **Allowed methods:** allow the methods required by the application
- Forward the cookies, query strings, and headers required by the Streamlit session

![Cache Behavior configuration](cloudfront-settings.png)

![Allowed HTTP methods](cloudfront-methods.png)

Incorrect caching of HTML or session data can return stale content or disrupt WebSocket connections, so the behavior is configured for a dynamic application.

## 4. Configure WAF

In the protection section, the team keeps the WAF protection included with the selected plan and does not add advanced rules outside the project scope.

![WAF configuration](cloudfront-waf.png)

WAF filters requests before they reach the ALB. The next step prevents users from easily bypassing this layer through the ALB DNS name.

## 5. Review and create the Distribution

Review the Origin, behavior, and WAF settings, then choose **Create distribution**.

![Review CloudFront](cloudfront-review.png)

![Created CloudFront Distribution](cloudfront-created.png)

## 6. Attach the domain and certificate

Add the alternate domain name:

```text
malscanai.sadc.io.vn
```

![Add the alternate domain name](alternate-domain.png)

Select the ACM certificate with status `Issued` in `us-east-1`.

![Select the ACM certificate](certificate-selected.png)

## 7. Create the Route 53 Alias record

After the Distribution becomes `Deployed`, return to Route 53 and create an Alias A record:

```text
Record name: malscanai
Route traffic to: CloudFront Distribution
```

![Create the Alias to CloudFront](route53-alias.png)

The domain `malscanai.sadc.io.vn` now resolves to CloudFront instead of directly to the ALB.
