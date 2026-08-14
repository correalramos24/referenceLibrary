# AWS Scalability
Increase computation resources on-demand.

- [AWS Scalability](#aws-scalability)
  - [Elastic Load Balancing (ELB)](#elastic-load-balacing-elb)
  - [Health checks \& security](#health-checks--security)
  - [Types of load balancers](#types-of-load-balancers)
    - [Application load balancer (ALB v2)](#application-load-balancer-alb-v2)
    - [Network load balancer (NLB)](#network-load-balancer-nlb)
    - [Gateway load balancer (GWLB)](#gateway-load-balancer-gwlb)
  - [Sticky sessions (Session affinity)](#sticky-sessions-session-affinity)
  - [Cross-zone load balancing](#cross-zone-load-balancing)
  - [SSL/TLS certificates](#ssltls-certificates)
  - [Connection draining](#connection-draining)
- [Auto Scaling groups (ASG)](#auto-scaling-groups-asg)
  - [ASG scaling policies](#asg-scaling-policies)


## Elastic Load Balancing (ELB)
Server that forward traffic to multiple servers.

An ELB is a managed load balancer, which means that AWS guarantees that it will be working & maintained.

## Health checks & security
Health checks are crucial for load balancing, as we don't want to sent traffic if the instance is down.

The EC2 instances downstream should only allow traffic coming from the load balancer (using the Security group).

## Types of load balancers
* Classic Load balancer - (CLB) : Don't use, is deprecated!
* Application load Balancer (ALB): HTTP/S & WebSocket
* Network load balancer (NLB): TCP, UDP & TLS
* Gateway load balancer (GWLB): IP protocol

ELB provides static IP and static DNS while NLB provides both static DNS and static IP.

### Application load balancer (ALB v2)
Targeting OSI Model lvl 7 (Application level - HTTP) it distributes the users: 
A) to multiple applications across machines using targets groups (EC2 instances)
B) multiple applications on the same machine (containers)

ALB uses routing tables based on path, hostname or query strings/headers. Rules have a priority number.

This ELB fits into micro-services & container-based applications.

An ALB can route to multiple targets groups(each with an own health check), which could be:
* EC2 instances (auto scaling group)
* ECS tasks
* Lambda functions (AWS server-less)
* IP private addresses

Under the scenes, the client is connected to the ALB which via a connection termination distributes the traffic into the real client using X-Forwarded-For header.

### Network load balancer (NLB)
Targeting OSI model lvl 4 (TCP-UDP traffic) and is designed to handle millions of requests/sec with ultra-low latency.

* A NLB has one static IP per AZ (can be elastic IP per AZ).
* A NLB is fits for ultra-performance use cases.
* It can target EC2 instances, private IPs or ALB.
* Health checks supports TCP,  HTTP & HTTPs.

### Gateway load balancer (GWLB)
Targeting OSI model lvl 3 (IP) and used for traffic analysis/firewalling/instrusion detection mechanism.

Use case of deploy, scale & manage a fleet of 3rd party network virtual appliances in AWS.

* GENEVE protocol at port 6081.

## Sticky sessions (Session affinity)
Same user always is redirect to the same instance using a cookie. This enforce that a user doesn't lose his user data session information.

The cookies can be application based or duration based.

This is set under the target group configuration.

## Cross-zone load balancing
Traffic can be distributed across AZs to have a more distributed workload.
* ALB has this feature enabled by default.
* NLB & GWLB is disabled by default; enable this has a fee.

## SSL/TLS certificates
Public SSL certificates are issued by Certificate Authorities (CA) and it allows traffic between your clients with in-flight encryption.

AWS Certificate manager (ACM) can manage the certificates to your instances/services.

Server Name Indication (SNI) solves the problem of loading multiple SSL certificates and is only supported by ALB & NLB. The initial handshake of the protocol will indicate the hostname for the targeting server.

## Connection draining
Also named deregistration delay. Is the time to complete in-flight request while the instances is unhealthy or de-registering.

# Auto Scaling groups (ASG)
Capability to automate the number of instances to match the load of the system (also replace unhealthy instances).

The ASG is defined using a minimum, desired and maximum capacity number.

An ASG Launch template is the recipe used to create new EC2 instances (EC2 parameters). They are used to:

* Scale out: add EC2 instances.
* Scale in: remove EC2 instances.

Behind the scenes, a CloudWatch alarm triggers the scale out and scale in policies based on metrics (Avg CPU usage)

## ASG scaling policies
AWS provides several options to configure the scale in/out events:
!TODO: Add explanation
* Dynamic scaling
  * Target Tracking scaling
  * Simple / Step scaling
* Scheduling scaling: Increase instances based on know habits.
* Predictive scaling: Based on forecast, schedule.  

The used metrics are CPU Utilization (across instances), RequestsCountPerTarget, AverageNetworkInOut or any other cloudWatch metric.

After all scale out/in event, a cooldown period (300s as default) is happening, allowing the system to stabilize.