# AWS Containers

- [AWS Containers](#aws-containers)
  - [ECS: Elastic container service](#ecs-elastic-container-service)
    - [ECS Autoscaling](#ecs-autoscaling)
  - [ECR: Elastic container registry](#ecr-elastic-container-registry)
  - [EKS: Elastic Kubernetes service](#eks-elastic-kubernetes-service)

## ECS: Elastic container service
Different launch types for our containers:
* EC2 launch type: It uses an ECS task on ECS cluster.
* Fargate launch: It's serverless (no EC2 instances management), just create task definitions.

It requires IAM roles + ECS task role + it can be used with load balancer integrations.

For data persistance, you require data volumes via EFS filesystem. It cannot use S3

EventBridge is used in some solutions to orchestrate actions based on events.

### ECS Autoscaling
Automatically increase/decrease number of ECS tasks, according to CPU usage/memory usage, ALS request count, ...

You can schedule scaling, step scaling or target tracking scaling policies. Easy to do this with Fargate launch.

ECS Cluster capacity provider: Automatically provision & scale the infrastructure.

## ECR: Elastic container registry
Store & mange docker images on AWS (public(gallery) or private). Fully integrated with ECS (backed by S3).

IAM controls the access to the images.

It adds vulnerability scanning, versioning & image lifecycle.

## EKS: Elastic Kubernetes service
Kubernetes implementation on the cloud. Alternative to ECS (as this is not opensource).

It supports EC2 or Fargate modes. Fits the use case when on-premises the company uses already Kubernetes. EKS pods == ECS tasks

Managed nodes, self-managed nodes or fargate node types.

The storage is defined in the manifest and supports (EBS, EFS(fargate), FSx lustre & NetApp).
