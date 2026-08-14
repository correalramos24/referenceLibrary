# Monitoring & Audit

- [Monitoring \& Audit](#monitoring--audit)
  - [CloudWatch](#cloudwatch)
  - [EventBridge](#eventbridge)
  - [CloudTrail](#cloudtrail)
  - [Config](#config)

## CloudWatch
Service to collect logs from AWS services.

It can generate alarms to take actions to events.

CloudWatch Metric stream streams the data for other AWS services for analysis.

## EventBridge
Service to generate events (or collect & react).

## CloudTrail
Collection of API, SDK or Console events (management, data & Insights events)
90 days of retention, after that it need to we sent to S3 and analyze with Athena.

## Config
Audit & record compliance of your AWS resources, based on AWS managed config rules or custom rules (defined via Lambda). You receive alerts/notifications (EventBridge or SNS) for any changes on this but it doesn't prevent actions from happening => It is a kind of dashboard

AWS Config works per-regions.

Automate remediation of non-compliant resources can set and deactivate whatever happens.

