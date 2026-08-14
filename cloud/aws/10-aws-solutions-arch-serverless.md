# AWS serverless serevices (FaaS)

- [AWS serverless serevices (FaaS)](#aws-serverless-serevices-faas)
  - [AWS Lambda](#aws-lambda)
    - [Limits](#limits)
    - [Concurrency \& throttling](#concurrency--throttling)
    - [Cold start \& provisioned concurrency](#cold-start--provisioned-concurrency)
    - [Lambda SnapStart](#lambda-snapstart)
    - [Lambda networking](#lambda-networking)
  - [Lambda@Edge \& CloudFront functions](#lambdaedge--cloudfront-functions)
  - [DynamoDB](#dynamodb)
    - [DynamoDB Accelerator (DAX)](#dynamodb-accelerator-dax)
    - [DynamoDB Streams processing](#dynamodb-streams-processing)
    - [Global tables](#global-tables)
    - [Bakcups and disaster recovery](#bakcups-and-disaster-recovery)
  - [API Gateway](#api-gateway)
  - [Step functions](#step-functions)
  - [Amazon cognito](#amazon-cognito)

Just deploy code, no infrastructure management is required. Paradigm pioneered by AWS

## AWS Lambda
Virtual functions "containers" build for short executions, run on-demand and the scaling is automated. It supports many programming langs 

* Is integrated with the whole AWS suite of services (roles required)
* Easy to monitor through AWS CloudWatch
* Increase RAM will improve CPU & network
* Supports the execution of container images
* Check way to execute code.

### Limits
Executions limits:
  * Memory allocation: 128 MB - 10 GB
  * Max. exec time: 900s (15min)
  * Env variables: 4 KB
  * /tmp : 512MB to 10 GB
  * 1000 concurrent executions
Deployment file:
  * Deployment file: 50 MB (compressed) - 250MB(uncompressed+dependencies)

### Concurrency & throttling
Reserved conccurrency (per function) will limit the concurrent executions.

Over the concurrency limit will trigger a "Throttle" (if SYNC : 429 thotthelERror if ASYNC retry + DLQ)

Without any limit per-function can happens that some functions make others to throttle (the limit is by user, not by function!)

ASYNC invocation uses an event queue and as it is queued.

### Cold start & provisioned concurrency
If the init of the code is large (cold start) you need to use provisioned concurrency. This makes some instances warmed to be user and skip the initial latency.

In lambda V4 this effect is mitigated.

### Lambda SnapStart
Improves x10 for Java, Python and .NET languagues applications.

It pre-initalize the function for the real invoke of the function skip the initialization and executes & shutdowns only.

### Lambda networking
By default, the function is launched outside your own VPC.

It can be launched using a security group and ENI in your subnets.

Usually is used using a RDS proxy in some solutions. Is also possible to invoke lambda function from within your DB instance (RDS for postgreSQL & Aurora MySQL).

## Lambda@Edge & CloudFront functions
Miminize latency on CloudFront distributions for the custommize content of the CDN

Used for SEO, Dynamic web apps, security, Real-time image transformations, etc...

CloudFront functions are lightweight function in Javascript for high-scale, latency-sensitive CND customizations (sub-ms start up times). It is managed at cloudfront.

Lamda@Edge are function written in NodeJS or Python and scales to 1000s of request/second.

## DynamoDB
NoSQL Fully managed, highly availabile with replication across multiple AZs, scales to massive workloads (as it is a distributed databases) and has fast & consistent in performance. Usefull for rapidly evolve schemas.

It has low cost and auto-scaling capabilities.

Each table has a primary key (decided at creation time) and infinite number of items (rows). Each items has attributed (can be added over time) and the max size is 400KB

Capacity modes:
1. Provisioned mode (default): read/write in advance & you pay for the RCU and WCU. Can be aut-scaling mode. Usefull for predictable workloads.
2. On-demand: More expensive but useful for unpredictable workloads & steep sudden spikes.

Items can be deleted after an expiry timestamp (TTL). 

DyamoDB can be exported/imported to/from S3 (requires Point-in-time-recovery PITR). Useful to query the bucket with Athena. 

### DynamoDB Accelerator (DAX)
Seanless in-memory cache for DyamoDB. Achieve mirroseconds latency for cached data. It is transparent to the programming logic.

Default 5mins TTL.

### DynamoDB Streams processing
Ordered stram of item-level modifications in a table (triggers).

It can be a kisesis data streams for the same use case but DynamoDB allows to have a processing layer to invoke a lambda function or use a KCL adapter.

### Global tables
Tables replicated across all the world with low-latency. Uses a two-way replication. Requires DyamoDB streams (used in the backed to sync between tables)

### Bakcups and disaster recovery
Continuos(last 35 days) or on-demand backups (long-term retention) available.

Recovery process creates a new table.

## API Gateway
Bridge between the client and the lambda function to be invoked. It creates REST API to proxy the request to the lamdba function.

It provides these features, because this service could be and ALB:
* WebSocket protocol
* Handle security
* Handle envs
* Create API keys, request throttling
* Swagger/OpenAPI to quickly define APIs
* Transform & validate request/responses

It is also integrated with HTTP and all the AWS services (SQS, functional workflow, etc)

Some types of endpoints:
* edge-optimized
* regional deployment
* private

The users can be auth using IAM roles, AWS cognito or a custom authorizer. Also there is HTTPS security.

## Step functions
Serverless visual workflow to orchestrate lambda functions. Integration with a lot of AWS services. Useful for many use cases.

It provides Human approval for steps.

## Amazon cognito
Give an identity to intereact with our web/mobile application. §Integration with API Gateway & ALBs. 

Two ways to identify users:
* User pools(CUP): Sign in functionality for app users. serverless DB with a lot features (TFA, facebook login, etc)
* Identity pools(federated ids): Provide AWS credentials to users. Usefull for 3rd party logins, cognito users pools. IAM policies & roles must be applied.