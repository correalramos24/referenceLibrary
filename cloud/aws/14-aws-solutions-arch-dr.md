# Disaster recovery & migrations

- [Disaster recovery \& migrations](#disaster-recovery--migrations)
  - [Strategies](#strategies)
  - [DRS: Elastic Disaster Recovery](#drs-elastic-disaster-recovery)
  - [DMS: Database Migration serivce](#dms-database-migration-serivce)
    - [RDS \& Aurora migrations](#rds--aurora-migrations)
  - [AWS Backup](#aws-backup)
  - [MGN: Application migration service](#mgn-application-migration-service)
  - [VMware cloud on AWS](#vmware-cloud-on-aws)


Any event that has a negative impact on a company business. It is based on:

RPO (Recovery point objective): How often do you backup data?
RTO (Recovery time objective): How much downtime is expected?

## Strategies
1. Backup & restore.
2. Pilot light: Small version of the app is always running in the cloud.
3. Warm standby: Full system up & running but at minimum size.
4. Hot site / multi site approach: On-premises + AWS running in parallel

Costs, RPO, RTO will decided one strategi or the other.

On-premises there are some strategies to work with AWS:
* Download Amazon Linux 2 AMI as a virtual machine locally
* Migrate/Export VM
* Discovery service (plan migrations) -> migration service
* Application migration service (MGN)

## DRS: Elastic Disaster Recovery
Allows & easily recover physical, virtual & cloud-based servers into AWS.
It uses Continuous block-level replication for your servers.

## DMS: Database Migration serivce
Quick and securey service to migrate a DBs (Homogeneous & heterogeneous migrations). It requires an EC2 intance to perform the migration.

Schema conversion tool (SCT) to change the schema

### RDS & Aurora migrations
Different options from RDS(MySQL or PostgreSQL):
1. RDS Snapshot
2. Create an Aurorar Read Replica from your RDS

From on-permises:
1. Percona XtraBackup to create a backup in S2
2. mysqlDump utility

Or Use DMS if both DBs are up & running.

## AWS Backup
Centrally & automate backups. No need custom scripts.

Backup policies (backup plans) to set the frequency, retention period, etc...

It has vault locks (enforce WORM) state

## MGN: Application migration service
Plan migration project by gathering information of on-premises data-centers

1. Agentless discovery
2. Agent-based discovery

To move the data, use MGN (to lift-and-shift) solution.

## VMware cloud on AWS
VMware client on AWS and allows then to start using the AWS services.
