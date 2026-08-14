# AWS PaaS (Platform as a Service)
Collection solutions present at AWS.

- [AWS PaaS (Platform as a Service)](#aws-paas-plataform-as-a-service)
  - [Elastic beanstalk](#elastic-beanstalk)
  - [Communication between applications (Decouple application)](#communication-between-applications-decouple-application)
    - [SQS: Standard queue service](#sqs-standard-queue-service)
      - [Visibility timeout](#visbility-timeout)
      - [Long polling](#long-polling)
      - [FIFO queue](#fifo-queue)
    - [SNS: Simple notification service](#sns-simple-notification-service)
    - [SNS + SQS: Fan out pattern](#sns--sqs-fan-out-pattern)
    - [Amazon Kinesis data streams](#amazon-kinesis-data-streams)
    - [Amazon Data Firehose](#amazon-data-firehose)
    - [Amazon MQ](#amazon-mq)

## Elastic beanstalk
Configure & scale applications/APIs easily. It is a managed service to set al the components (EC2, ASG, ELB, etc). Free, only pay the underlying services.

It is composed of:
1. Application: Source code.
2. Environment: Collection of AWS resources.
3. Tier: Web server vs Worker tier (SQS queue - messages).
4. Deployment mode: Single instance / High availability with Load Balancer.

It uses a pre-defined solution architecture for each tier.

Cloudformation is used in the backend to allocate the AWS resources stack (IaS).

## Communication between applications (Decouple application)
Deploying multiple applications will require communication (ASYNC or SYNC).

SYNC cannot handle on-the-fly increase workload -> decouple applications with ASYNC approach.

### SQS: Standard queue service
Fully managed service to decouple applications. It has unlimited throughput, low latency and a retention period (max 14 days) but it can have duplicate messages & out of order messages.

It requires a producer(s) and a consumer(s) to send & recive messages (up to 1024 KB size). AWS SDK is used to send / recv messages (delete the message after processing it).

CloudWatch metric ApproxNumberOfMessages (queue length) can be used with ASG to horizontally scale an application. ASG can be used as well to use SQS queues a buffers (to put in front of DBs only if no ACKs is required).

Has in-flight encryption + IAM policies to regulate access to SQS API.

#### Visibility timeout
Visibility Timeout (30s by default) is the time that started after the message is returned to a consumer. After this time the message become visible again. The time can be change using API (ChangeMessageVisibility).

#### Long polling
Long polling decreases the number of API calls adding a delay between polling actions. 20s is a preferable and can be enable via API

#### FIFO queue
Same as SQS que but the order is enforced. The throughput is limted (300 msg/s) and the messages are sent exactly-once.

### SNS: Simple notification service
Publishing/Subscribers architecture. 1 producer has N consumers (subscribers).

The data can be send data to emails/Mobile notifications, http(s) endpoints, lambda, kinesis or SQS and can come from any AWS service.

You need to create a topic, subscription and publish the topic via SDK. There is a SDK for mobile also.

Same security as SQS (IAM + SNS Access policies + encryption)

Also it has a FIFO option for topics (only SQS subscription).

Messages can be filtered using a JSON policy to enroute messages.

### SNS + SQS: Fan out pattern
Push once in SNS topic -> SQS are subscribers of this topic. 

### Amazon Kinesis data streams
Collect & store streaming data in real-time. Up to 10 MiB

Real-time data --> producers (apps or kinesis agent) --> Kinesis Data streams --> Consumers (Apps or Lambda functions or Data firehose or Apache Flink)

Retention time up to 365 days, can reprocess (replay) data.

Data can't be deleted from kinesis (until it expires).

KPL & KCL (Kinesis producer / consumer library) to implement applications.

Different capacity modes:
* Provisioned mode: Choose number of shards (1MB/s in - 2MB). Pay per shard per provisioned hour.
* On-demand mode: Default capacity provisiones and it scales automatically (30 days throughput peak). Pay per stream per hour & data in/out per GB.

### Amazon Data Firehose
Send data from producers (or pull by data firehose) to batch writting to AWS Destination(S3/Redshift/OpenSearch) or 3rd party partner destinations or custom destination (HTTP endpoint). This data is flushed periodically.

It has automatic scaling & serverless. It is used for near real-time applications with buffering capacity.

* Paid per use
* The data can be transformed using a Lambda function and/or save to an S3 backup bucket

### Amazon MQ
Managed message broker for RabbitMQ and ActiveMQ (on-premises system).

It doesn't scale as much as SQS/SNS, problems of multiAZ.

