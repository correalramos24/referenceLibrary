# AWS DNS

- [AWS DNS](#aws-dns)
  - [Route 53](#route-53)
    - [Routing policies](#routing-policies)
    - [Health-checks](#health-checks)
    - [3rd Party domains \& route 53](#3rd-party-domains--route-53)
    - [Route 53 resolvers \& hybrid DNS](#route-53-resolvers--hybrid-dns)


## Route 53
Amazon DNS service (highly available, scalable, fully managed and authoritative DNS).

Route53 is a domain registrar as well.

* A/ AAAA record: Maps a hostname to IPv4/IPv6.
* CNAME record: maps a hostname to another hostname (non-root domains only!).
* NS record: Name servers for the hosted zone(private/public hosted zones).
* Alias: Points to an AWS resource (ELB, CloudFront, S3Website, etc) .It is an extension on DNS standard & TTL cannot be set.

TTL (time-to-live): Client will keep the record for TTL seconds
Hosted zones: Container that holds your DNS records.

### Routing policies
How Route 53 responds to DNS queries. It supports:

* Simple: Route traffic to a single resource (random if multivalued).
* Weighted: Control the % of request that go to each resource.
* latency-based: Redirect to the resource with least latency. Associated with heat-checks.
* Failover: If the health check is bad, redirect the traffic to a secondary instance.
* Geolocation: Based on the user location. It requires a Default record in case there is no match.
* Geoproximity: Route traffic based on bias values (higher values move the geographic lines). Helpful to shift traffic between regions.
* IP-Based: Provide a list of CIDRs for your clients. Route specific ISP to a specific endpoints.
* Multi-value: Route to multiple resources associated with health-checks

### Health-checks
Check the status of public resources. Route53 will check the specific port and Automate the DNS failover.

Route 53 Health checks are check from all the regions used. 

* Monitor and endpoint: If 18% of health checks -> OK 
* Calculated health-checks: Combine health-checks from different child health-checks into one only health check.
* For private resources use CloudWatch metric

### 3rd Party domains & route 53
Even for other DNS registrar you can use route 53 nameserver.

### Route 53 resolvers & hybrid DNS
Resolver endpoints can be linked into On-premises data centers (private).