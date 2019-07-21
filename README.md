   * [Route 53](#route-53)
      * [Simple routing](#simple-routing)
      * [Weighted Routing Policy](#weighted-routing-policy)
      * [Latency-Based Routing](#latency-based-routing)
      * [Failover Routing](#failover-routing)
      * [Geolocation Routing](#geolocation-routing)
      * [Geoproximity Routing](#geoproximity-routing)
      * [Multivalue Answer Policy](#multivalue-answer-policy)
   * [IAM 101](#iam-101)
      * [Create A Billing Alarm](#create-a-billing-alarm)
   * [S3 101 (Simple Storage Service)](#s3-101-simple-storage-service)
      * [Create a S3 bucket](#create-a-s3-bucket)
      * [S3 Security And Encryption](#s3-security-and-encryption)
      * [Lifecycle Management with S3 - LAB](#lifecycle-management-with-s3---lab)
      * [Cross Region Replication (CRR)](#cross-region-replication-crr)
      * [Transfer Acceleration](#transfer-acceleration)
      * [CloudFront Overview](#cloudfront-overview)
      * [Create A CloudFront Distribution - LAB](#create-a-cloudfront-distribution---lab)
      * [Snowball](#snowball)
      * [Snowball Lab](#snowball-lab)
      * [Storage Gateway](#storage-gateway)
   * [EC2 101](#ec2-101)
   * [EBS](#ebs)
      * [EBS Volumes &amp; Snapshots (4-6 questions)](#ebs-volumes--snapshots-4-6-questions)
      * [CloudWatch 101](#cloudwatch-101)
      * [AWS Command Line](#aws-command-line)
      * [Identity Access Management Roles](#identity-access-management-roles)
      * [Using BootStrap Scripts - LAB](#using-bootstrap-scripts---lab)
      * [Instance Metadata - LAB](#instance-metadata---lab)
      * [EFS - LAB](#efs---lab)
   * [Lambda](#lambda)
   * [Database 101](#database-101)
      * [DynamoDB](#dynamodb)
      * [Redshift](#redshift)
      * [Aurora](#aurora)
      * [Elasticache](#elasticache)
   * [VPC Overview](#vpc-overview)
      * [VPC Peering](#vpc-peering)
      * [Create Your Own Custom VPC](#create-your-own-custom-vpc)
      * [VPC Flow Logs - LAB](#vpc-flow-logs---lab)
      * [Bastions](#bastions)
      * [Direct Connect](#direct-connect)
      * [VPC End Points](#vpc-end-points)
   * [Load Balancers Theory](#load-balancers-theory)
      * [Load Balancers &amp; health check - LAB](#load-balancers--health-check---lab)
      * [Path Patterns](#path-patterns)
      * [HA Word Press Site](#ha-word-press-site)
      * [CloudFormation](#cloudformation)
      * [Elastic Beanstalk (1-2 questions)](#elastic-beanstalk-1-2-questions)
   * [Applications](#applications)
      * [SQS](#sqs)
      * [SWF (Simple Workflow Service)](#swf-simple-workflow-service)
         * [SWF Actors](#swf-actors)
            * [Workflow Starters](#workflow-starters)
            * [Deciders](#deciders)
            * [Activity Workers](#activity-workers)
      * [SNS](#sns)
      * [Elastic Transcoder](#elastic-transcoder)
      * [API Gateway (5 to 10 marks)](#api-gateway-5-to-10-marks)
      * [Kinesis (5 to 10 marks)](#kinesis-5-to-10-marks)
      * [Web Identity Federation - Cognito](#web-identity-federation---cognito)
   * [OpsWorks](#opsworks)
   * [Consolidated Billing](#consolidated-billing)

130 Minutes, 60+ questions, MC, 720 out of 1000 passing score, Scenario based questions

# Route 53

ELBs do not have pre-defined IPV4 addressess; you resolve to them using a DNS names

Understand diff between an Alias Record and a CNAME (Given the choice, always choose Alias Record in exam)

SOA Record (Start of Authority)

TTL (48 hours to take into effect the new DNS name)

NS Record (Name Server)

monster.com -> TLD (Top Level Domain) server -> NS Server -> SOA

A Record

monster.com => 192.168.0.1

CNAMEs

www.mon.com => www.monster.com or 192.168.0.1

Cannot be used for naked domain names (zone apex record)

Alias Record

mon.com => monster ELB, CloudFront distributions, S3 buckets that configured as websites

Alias Record > CNAME

MX Record

use for mail

PTR Record (The reverse of A Record)



You can buy domain names directly with AWS

take up to 3 days to register

## Simple routing

1 to m IP addressess

if one fails health check, Route 53 returns all values in a random order

no health check

## Weighted Routing Policy

distribute traffic based on weight

Health check

You can set health check on individual record sets.

If a record fails health check it will be removed from Route53

You can set SNS alert for health check failing.

## Latency-Based Routing

distribute traffic with lowest latency

## Failover Routing

Active <-> health check failed

## Geolocation Routing

Continent/Country

Compare with Latency-Based Routing

Use when you want to route traffic based on the location of your users.

## Geoproximity Routing

must use Route 53 traffic flow

Use when you want to route traffic based on the location of your resources

## Multivalue Answer Policy

Diff from Failover Routing? 

If you associate a health check with a multivalue answer record, Route 53 responds to DNS queries with the corresponding IP address only when the health check is healthy.

If you don't associate a health check with a multivalue answer record, Route 53 always considers the record to be healthy.

If you have eight or fewer healthy records, Route 53 responds to all DNS queries with all the healthy records.

When all records are unhealthy, Route 53 responds to DNS queries with up to eight unhealthy records.





# IAM 101

Users, Groups, Policies (JASON formatted), Roles

Mange MFA to active root account

IAM is universal, It does not apply to regions at this time.

New Users have No permissions when first created

New Users are assigned Access Key ID & Secret Access Keys when first created.

These are not the same as password. You cannot use the Access key ID & Secret Access Key to Login in to the console. You can use this to access AWS via the APIs and Command Line, however. (download .csv file when adding a new user. If lost the key then have to regenerate the key)

Always setup Multifactor Authentication on your root account.

You can create and customise your own password rotation policies.

Support PCI DSS Compliance

If a website takes credit card, it need to follow certain rules. 

## Create A Billing Alarm

Cloudwatch -> create alarm

# S3 101 (Simple Storage Service)

Bucket

Objects (files from 0 to 5 TB)

Key, Value, Version Id, Metadata, Subresources (e.g. permission)

S3 is a universal namespace. It must be unique globally. E.g. [http://s3-eu-west-1.amazonaws.com/acloudguru](http://s3-eu-west-1.amazonaws.com/acloudguru)

Not suitable to install an operating system on.

Turning on MFA Delete to prevent someone accidentally delete files.

Read after Write consistency (for PUTS of new Objects)

Eventual Consistency (for overwrite PUTS and DELETES)

Take some time to propagate

Tiered Storage Available

Lifecycle Management

S3 standard (highly available)

S3 - IA (Infrequently Accessed)

S3 One Zone - IA

Low cost

S3 - Intelligent Tiering

S3 Glacier

S3 Glacier Deep Archive

Lowest-cost

Get data in 12 hours

How it get charged?

Storage, Requests, Storage Management Pricing, Data Transfer Pricing, Transfer Acceleration, Cross Region Replication Pricing

[READ S3 FAQs before the exam](https://aws.amazon.com/s3/faqs/)

Individual S3 objects can range in size from 0 to 5TB. A single PUT limit is 5GB

## Create a S3 bucket

Buckets are a universal name space

Upload an object to S3 receive a HTTP 200 code

S3, *S3 Intelligent-Tiering, S3 - IA, S3 - IA (One Zone), S3 Glacier, S3 Glacier Deep Archive

Control access to buckets using either a bucket ACL or using Bucket Policies

## S3 Security And Encryption

Newly created buckets are PRIVATE

Encryption At Rest (Server Side) is achieved. 

S3 Managed Keys - SSE - S3

*AWS Key Management Service, Managed Keys - SSE - KMS

Certified Security Specialty Certificate

Server Side Encryption With Customer Provided Keys - SSE - C

Client Side Encryption

Version Control

Stores all versions of an object (including all writes and even if you delete an object)

Great backup tool.

Once enabled, Versioning cannot be disabled, only suspended.

Integrates with Lifecycle rules

Versioning’s MFA Delete capability, which uses multi-factor authentication, can be used to provide an additional layer of security.

After uploading the same file again, it changes back to private.

Size of the file is keep on increasing by versions!

## Lifecycle Management with S3 - LAB

Automates moving your objects between the different storage tiers.

Can be used in conjunction with versioning.

Can be applied to current versions and previous versions.

## Cross Region Replication (CRR)

Versioning must be enabled on both the source and destination buckets.

Regions must be unique.

Files in an existing bucket are not replicated automatically.

All subsequent updated files will be replicated automatically.

Delete markers are not replicated.

Deleting individual versions or delete markers will not be replicated.

## Transfer Acceleration

Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your client and your Amazon S3 bucket. S3 Transfer Acceleration leverages Amazon CloudFront’s globally distributed AWS Edge Locations. As data arrives at an AWS Edge Location, data is routed to your Amazon S3 bucket over an optimized network path.

## CloudFront Overview

Edge Location - This is the location where content will be cached. This is separate to an AWS Region/AZ

Origin - This is the origin of all the files that the CDN will distribute. This can be either an S3 Bucket, an EC2 Instance, an ELB, or Route53.

Distribution - This is the name given the CDN which consists of a collection of Edge Locations.

Web Distribution - Typically used for Websites.

RTMP - Used for Media Streaming. (Adobe?)

Edge locations are not just READ only - you can write to them too. (ie put an object on to them.)

Objects are cached for the life of the TTL

*You can clear cached objects, but you will be charged.

## Create A CloudFront Distribution - LAB

Invalidation by regular expression

Disabled take about 15 min

You can invalidate cached objects, but you will be charged.

## Snowball

Can import/export data to/from S3

Snowball, Snowball Edge, Snowmobile

When should I use snowball?

## Snowball Lab

How to use snowball

## Storage Gateway

File Gateway

Once transferred, files are treated as S3 objects

For flat files, stored directly on S3.

Volume Gateway(iSCSI)

Stored Volumes

Stores entire data center and is asynchronously backed up to S3.

Cached Volumes

Only stores most frequently accessed data

Tape Gateway

# EC2 101

Pricing Models

On Demand

Fixed rate by the hour

Reserved

Contract from 1-3 years

Spot

Bid price for flexible start and end time

Dedicated Hosts

Allowing you to use your existing server-bound software licenses

On Demand charges more than Spot

EC2 Instance Types

F - For FPGA

I For IOPS (input/output operations per second)

G - Graphics

H - High Disk Throughput

T - Cheap general purpose

D - For Density

R - For RAM

M - Main choice for general purpose apps

C - For Compute

P - Graphis

X - Extreme Memory

Z1d - Extreme Memory AND CPU

A - Arm-based workloads

U - Bare Metal

Amazon EC2 is a web service that provides resizable compute capacity in the cloud. It reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change.

If the Spot instance is terminated by EC2, you will not be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for any hour in which the instance ran.

Security Groups Basis

Termination Protection is turned off by default, you must turn it on.

On an EBS-backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated.

*Compare *Additional volumes that are attached to that EC2 instance will continue to persist.

EBS Root Volumes of your DEFAULT AMI (Amazon Machine Image)’s cannot be encrypted. You can also use a third party tool (such as bit locker etc) to encrypt the root volume, or this can be done when creating AMI’s (lab to follow) in the AWS console or using the API.

Additional volumes can be encrypted.

Security Group Basics

0.0.0.0 means allow every IP address.

All Inbound traffic is blocked by default.

All Outbound traffic is allowed.

Changes to Security Groups take effect immediately.

You can have any number of EC2 instances within a security group.

You can have multiple security groups attached to EC2 Instances.

Security Groups are STATEFUL.

If you create an inbound rule allowing traffic in, that traffic is automatically allowed back out again.

You cannot block specific IP addresses using Security Groups, instead use Network Access Control Lists.

You can specify allow rules, but not deny rules.

Security Group do not span multiple VPCs

# EBS

General Purpose (SSD)

Most Work Loads

Provisioned IOPS (SSD)

Databases

Throughput Optimised Hard Disk Drive

Big Data & Data Wharehouses

Cold HDD

File Servers

EBS Magnetic (Not include in exam)

Workloads where data is infrequently accessed

## EBS Volumes & Snapshots (4-6 questions)

Volumes exist on EBS. Think of EBS as a virtual hard disk

Snapshots exist on S3. Think of snapshots as a photograph of the disk. (But they are not visible in your S3 buckets)

Snapshots are point in time copies of Volumes.

Snapshots are incremental - this means that only the blocks that have changed since your last snapshot are moved to S3. 

If this is your first snapshot, it may take some time to create.

To create a snapshot for Amazon EBS volumes that serve as root devices, you should stop the instance before taking the snapshot.

However you can take a snap while the instance is running.

You can create AMI’s from both Volumes and Snapshots

You can change EBS volume sizes on the fly, including changing the size and storage type.

Volumes will ALWAYS be in the same availability zone as the EC2 instance.

You cannot modify standard type of Volume. 

To move an EC2 volume from one AZ(availability zone) to another, take a snapshot of it create an AMI from the snapshot and then use the AMI to launch the EC2 instance in a new AZ.

-> Actions -> Create Snapshot ->

Wait when done -> Actions -> Create Image - > Under IAM tab ->

Launch-> Choose Instance Type -> Choose subnet (new AZ)

Or take a snapshot of it, create Volume with the new AZ and create another snapshot. Then create an AMI from it and use the AMI to launch the EC2 instance. 

To move an EC2 volume from one region to another, take a snapshot of it, create an AMI from the snapshot and then copy the AMI from one region to the other. Then use the copied AMI to launch the new EC2 instance in the new region. 

-> AMIs -> Actions -> Copy AMI

Or take a snapshot of it, copy the snapshot with the new region and create AMI from the copied snapshot. Then use the new AMI to launch the new EC2 instance. 

Difference of the two way:

Second way when creating AMI, you can choose EC2 types.

AMI Types (EBS vs Instance Store)

Categorized either backed by Amazon EBS or backed by instance store.

EBS Volumes: The root device for an instance launched from the AMI is an Amazon EBS volume created from an Amazon EBS snapshot.

-> EC2 -> Launch Instance -> Amazon Linux 2 AMI -> [Leave everything rest as default]

Instance Store Volumes: The root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3.

-> EC2 -> Launch Instance -> Community AMIs and filter as Instance stored volumes -> [pick one and leave everything rest as default]

Instance Store Volumes are sometimes called Ephemeral Storage.

Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data.

EBS backed instances can be stopped. You will not lose the data on this instance if it is stopped.

You can reboot both, you will not lose your data.

By default, both ROOT volumes will be deleted on termination. However, with EBS volumes, you can tell AWS to keep the root device volume. 

(EBS backed instance is better?)

Encrypted Root Device Volumes & Snapshots

Snapshots of encrypted volumes are encrypted automatically. Copying encrypted snapshots cannot be unencrypted.

Volumes restored from encrypted snapshots are encrypted automatically.

You can only share unencrypted snapshots

These snapshots can be shared with other AWS accounts of made public. 

Steps:

Create a Snapshot of the unencrypted root device volume

Create a copy of the Snapshot and select the encrypt option

Create an AMI from the encrypted Snapshot

Use the AMI to launch new encrypted instances

## CloudWatch 101

CloudTrail vs CloudWatch

CloudWatch is used for monitoring performance.

CloudWatch can monitor most of AWS as well as your applications that run on AWS

CloudWatch with EC2 will monitor events every 5 minutes by default.

You can have 1 minute intervals by turning on detailed monitoring.

You can create CloudWatch alarms which trigger notifications.

CloudWatch is all about performance. CloudTrail is all about auditing. 

CloudWatch Lab

-> Configure Instance-> Enable CloudWatch

Set Alarm

CloudWatch -> Alarms -> Create Alarms -> Select Instance Id -> Put alarm bar and set Actions. 

Standard Monitor: 5 min

Detailed Monitoring: 1 min

Dashboards - Creates awesome dashboards to see what is happening with your AWS environment.

Alarms - Allows you to set Alarms that notify you when particular thresholds are hit.

Events - CloudWatch Events helps you to respond to state changes in your AWS resources.

Logs - CloudWatch Logs helps you to aggregate, monitor, and store logs.

## AWS Command Line

You can interact with AWS from anywhere in the world just by using the CLI

You will need to set up access in IAM

IAM -> Groups -> Add User -> Programmatic access -> Create group -> Administrator -> Download .csv

Basic commands (Not in the exam)

Aws configure, aws s3 ls, aws s3 mb s3://[unique s3 name]...

## Identity Access Management Roles

IAM -> Roles -> Create role -> [Choose the service that will use this role] EC2 -> [attach permissions policies] Administrator -> [Review]

[SSH to EC2] -> [delete .aws hidden folder] => Cannot list s3 instances

EC2 -> Actions - Instance Settings - Attach/Replace IAM Role -> Ok

Roles are more secure than storing your access key and secret access key on individual EC2 instances.

Roles are easier to manage.

Roles can be assigned to an EC2 instance after it is created using both the console & command line.

Roles are universal - you can use them in any region. 

## Using BootStrap Scripts - LAB

-> Choose AIM -> Choose Instance Type -> Configure Instance Details -> [Finish rest settings]

Bootstrap scripts run when an EC2 instance first boots.

Can be a powerful way of automating software installs and updates.

## Instance Metadata - LAB

Used to get information about an instance (such as public ip)

-> curl http://169.254.169.254/latest/meta-data/

-> curl http://169.254.169.254/latest/user-data/

-> curl http://169.254.169.254/latest/meta-data/local-ipv4

-> curl http://169.254.169.254/latest/meta-data/public-ipv4

## EFS - LAB

Elastic File System

EBS vs EFS

One EBS can only has one EC2 instance

EFS can have multiple. 

*Following instructions to demo how one EFS be shared by two EC2 instances*

-> EFS -> [Choose a region] -> create file system -> [Choose an AC] -> [check encryption option] Configure optional setting -> [review] -> Create -> [wait a while]

-> Launch new EC2 instance -> Configure Instance -> [choose number of instances] 2 -> yum install -y amazon-efs-utils -> [select security group] -> [finish the rest settings] -> 

(if security groups between EC2 and EFS are different, change the EC2 security group to match) ->Actions -> Networking -> Change Security Groups -> [select security group]

-> [SSH one of those EC2 instances] -> [go to /var/www folder] -> [back to aws console] -> EFS -> [mount instructions] -> [back to ssh] -> [paste command from instruction] mount -t efs -o tls [file system id] /var/www/html ->  cd html -> [create a index.html file]

-> [SSH the other EC2 instance] -> cd /var/www -> [paste command from instruction]

EFS mount vs TLS mount

TLS mount means communication between EFS is encrypted

Supports the Network File System version 4 (NFSv4) protocol

You only pay for the storage you use (no pre-provisioning required.)

Can scale up to the petabytes

Can support thousands of concurrent NFS connections

Data is stored across multiple AZ’s within a region

Read After Write Consistency

EC2 Placement Groups

Clustered Placement Group

Low network latency, high throughput

Cannot span multiple AC

Spread Placement Group

Each instance put on distinct hardware

Critical instances that should be kept separate from each other.

Can span multiple AC

Name of PG must be unique within your AWS account

Only certain types of instances can be launched in a PG 

Compute Optimized,

GPU,

Memory Optimized,

Storage Optimized

AWS recommend homogenous instances within PG

You cannot merge PG.

You cannot move an existing instance into a PG. You can create an AMI from your existing instance, and then launch a new instance from the AMI into a PG.

# Lambda

Lambda scales out (not up) automatically

Lambda functions are independent, 1 event = 1 function

Lambda is serverless

Know what services are serverless!

Not

RDS (you have to deal with maintenance down time), EC2

Is

DynamoDB, S3, Lambda gateway

Lambda functions can trigger other lambda functions, 1 event can = x functions if functions trigger other functions

Architectures can get extremely complicated, AWS X-ray allows you to debug what is happening

Lambda can do things globally, you can use it to backup S3 buckets to other S3 buckets etc

Know your triggers

RDS cannot trigger

API Gateway, AWS loT, Application Load Balancer, CloudWatch Events, CloudWatch Logs, CodeCommit, Cognito Sync Trigger, DynamoDB, Kinesis, S3, SNS, SQS

Build A Serverless Webpage

-> Lambda -> Create function -> Save -> Configure Trigger -> API Gateway -> Save -> [follow the link to API Gateway] -> Actions -> Create Method -> Selecting method type: [GET, PUT, DELETE, POST] -> [choose lambda region] -> [input Lambda Function name] -> Save -> Actions -> Deploy API -> [input description] -> Deploy -> [Test the method by clicking on GET method link]

-> [Create S3 bucket] -> [upload index.html and make it public]

Let’s Build An Alexa Skill - LAB

First a million requests are free

# Database 101

Multi-AZ - Disaster Recovery

Read Replicas - Enhance Performance

RDS (OLTP)

SQL, MySQL, PostgreSQL, Oracle, Aurora, MariaDB

DynamoDB (No SQL)

OLTP (Online Transaction Processing) < OLAP (Online Analytics Processing)

Red Shift (OLAP): AWS data warehouse

ElastiCache supports two in-memory caching engines:

Memcached

Redis

ElastiCache to speed up performance of existing databases (frequent identical queries).

Redshift for Business Intelligence or Data Warehousing

Elastic Map Reduce for Big Data Processing

Create RDS in Amazon

RDS -> Create Database ->. Select engine -> Use case -> DB instance class (t2.micro) ->  [finish the rest settings] -> Create database (slower than creating EC2)

-> RDS -> Databases -> Connectivity -> [find db url under Endpoint]

RDS runs on virtual machines

You cannot log in to these operating systems however.

Patching of the PDS OS and DB is Amazaon’s responsibility

RDS is NOT serverless

Aurora Serverless IS Serverless

RDS - Back Ups, Multi-AZ & Read Replicas

Automated Backups

DB Snapshots

Create a new NDS endpoint

Encryption at rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB & Aurora. Encryption is done using the AWS Key Management Service (KMS) service. Once encrypted, the automated backups, replicas and snapshots are encrypted as well.

Multi-AZ

Available for SQL Server, Oracle, MySQL, PostgreSQL, MariaDB

Read Replica

Primary db asynchronously created READ-ONLY replicas

You can manually point url to any copy

Available for MySQL, PostgreSQL, MariaDB, Aurora

Used for scaling, not for disaster recovery!

Must have automatic backups turned on in order to deploy a read replica

You can have up to 5 read replica copies of any db

You can have read replicas of read replicas (but watch out for latency.)

Each read replica will have its own DNS end point.

You can have read replicas that have Multi-AZ.

You can create read replicas of Multi-AZ source db,

Read replicas can be promoted to be their own db. This breaks the replication

You can have a read replica in a second region.

RDS Backups, Multiple AZs - Lab

RDS -> Databases -> Modify -> Multi-AZ deployment - Yes -> Modify DB instance -> [wait a while]

You cannot create read replica until you turn on back up. So, 

RDS -> Databases -> Modify -> Backup (select backup frequency) -> Modify DB instance -> [wait a while] -> Actions -> Create read replica -> [set destination region] -> [leave rest settings default value] -> Create

There are two different types of Backups for RDS: 

Automated Backups (enabled by default)

Database snapshot

Read Replicas

Can be Multi-AZ

Used to increase performance

Must have backups turned on

Can be in different regions

Can be Aurora or MySQL

Can be promoted to master, this will break the Read Replica

Multi-AZ

Used for Disaster Recovery

You can force a failover from one AZ to another by rebooting the RDS instance

## DynamoDB

Eventual Consistent Reads

All copies’ data is consistent. 

Strongly Consistent Reads

Write and Read Consistency

The basics of DynamoDB are as follows;

Stored on SSD storage

Spread across 3 geographically distinct data centres

Eventual Consistent Reads,

Strongly Consistent Reads

## Redshift

Use for OLAP. Redshift is used for business intelligence.

Advanced Compression

Massively Parallel Processing

Backups

Enabled by default with a 1 day retention period.

Maximum retention period is 35 days.

Redshift always attempts to maintain at least three copies of your data (the original and replica on the compute nodes and a backup in Amazon S3).

Redshift can also asynchronously replicate your  snapshots to S3 in another region for disaster recovery.

Pricing

Compute Node Hours 

Backup

Data transfer (only within a VPC, not outside it)

Security Considerations:

Encrypted in transit using SSL

Encrypted at rest using AES-256 encryption

By default Redshift takes care of key management.

Manage your own keys through HSM

AWS Key Management Service

Redshift Availability:

Currently only available in 1 AZ

Can restore snapshots to new AZs in the event of an outage.

## Aurora

-> RDS -> Databases -> Actions -> Create Aurora read replica -> [leave rest setting default setting] -> Create

-> Actions -> Promote read replica -> [Migrate data from MySQL to Aurora]

[to stop a db instance] -> Actions -> Stop

2 Copies of your data is contained in each AZ, with minimum of 3 AZs, 6 copies of your data.

You can share Aurora Snapshots with other AWS accounts.

2 types of replicas available. Aurora Replicas and MySQL replicas. Automated failover is only available with Aurora Replicas.

What and how to promoting replica.

Migrate data from MySQL to Aurora

Creating a snapshot and then restoring from that snapshot

Aurora has automated backups turned on by default. You can also take Snapshots with Aurora. You can share these snapshots with other AWS accounts.

## Elasticache

Supports Memcached and Redis

Use Elasticache to increase database and web application performance.

Use cases e.g. *Database is overloaded what should you do?*

**Reddis is Multi-AZ

You can do backups and restores of Redis

If you need to scale horizontally, use Memcached

# VPC Overview

What can we do with a VPC (Virtual Private Cloud)

Launch instances into a subnet of your choosing

Assign custom IP address ranges in each subnet

Configure route tables between subnets

Create internet gateway and attach it to your VPC

Much better security control over your AWS resources

Instance security groups

Subnet network access control lists (ACLS)

Default VPC vs Custom VPC

Default VPC is user friendly, allowing you to immediately deploy instances.

All Subnets in default VPC have a route out to the internet.

Each EC2 instance has both a public and private IP address. 

## VPC Peering

Allows you to connect one VPC with another via a direct network route using private IP addresses.

Instances behave as if they were on the same private network

You can peer VPC’s with other AWS accounts as well as with other VPCs in the same account. 

Peering is in a star configuration: ie 1 central VPC peers with 4 others. NO TRANSITIVE PEERING!!!

You can peer between regions.

Think of a VPC as a logical datacenter in AWS

Consists of IGWs (Or Virtual Private Gateways), Route Tables, Network Access Control Lists, Subnets, and Security Groups

1 Subnet = 1 Availability Zone

Security Groups are Stateful; Network Access Control Lists are Stateless

ACLS’s deny rules, allow roles, inbound rule, outbound rules are independent

No Transitive PEERING

## Create Your Own Custom VPC

-> VPC -> Subnets -> Create a subnets

-> Internet Gateways -> Attach to VPC -> Attach

-> Create internet gateway

You can only have one gateway attach for one VPC

-> Route Tables -> Create Route Table

-> Route Tables -> Edit Route -> -> [edit description] -> [select target] -> Subnet Associations -> Edit subnet associations -> [select subnet]

-> EC2 -> [launch an EC2] -> [select subnet be the public one] -> [create a new Security Group]

-> EC2 -> [launch an EC2] -> [select subnet be the private one] -> [use just created Security Group]

When you create a VPC a default Route Table, NACL and a default Security Group.

It won’t create any subnets, nor will it create a default internet gateway.

US-East-1A in your AWS account can be a completely different AZ to US-East-1A in another AWS account. The AZ’s are randomized.

Amazon always reserve 5 IP address within your subnets. (e.g. for route table, for DNS)

You can only have 1 Internet Gateway per VPC

Security Groups can’t span VPCs.

-> Security Group -> [select VPC] -> Create -> Inbound -> Protocol Type: All ICMP - IPv4; Source: IP address range -> Add HTTP, HTTPS, MySQL, SSH [with same source]

-> EC2 -> Actions -> Networking -> Change Security Group -> [select security group] -> Save

-> [ssh public VPC] -> [create private key file] -> [ssh private VPC]

NAT Instances & NAT Gateways - LAB

NAT gateways is a highly available gateway

NAT instance is an EC2 instance

-> EC2 -> Community AMI -> [choose nat instances] -> [set the public subnet] -> [finish the rest setting] -> Launch

-> [check the NAT instance] -> Actions -> Networking -> Enable Source/Destination Check -> Yes, Disable

-> Route Tables -> [check the route table] -> Routes -> Edit routes -> [select target to NAT instance]

 -> [ssh to the public EC2] -> [ssh to the private EC2] -> [try accessing public network]

NAT Instances

When creating a NAT instance, Disable Source/Destination Check on the Instance.

NAT instances must be in a public subnet.

There must be a route out of the private subnet to the NAT instance, in order for this to work.

The amount of traffic that NAT instances can support depends on the instance size. If you are bottlenecking, increase the instance size.

You can create high availability using Auto Scaling Groups, multiple subnets in different AZs, and a script to automate failover.

Behind a Security Group

NAT Gateways

-> VPC -> NAT Gateways -> Create NAT Gateway -> [choose public subnet] -> [choose an IP] -> Create -> [edit route table] -> Add route -> [choose NAT gateway as Target] -> [0.0.0.0/0]

Redundant inside the AZ

Preferred by the enterprise

Starts at 5Gbps and scales automatically to 45 Gbps

No need to patch

Not associated with security groups

Automatically assigned a public ip address

Remember to update your route tables.

No need to disable Source/Destination Checks

If you have resources in multiple AZ and they share one NAT gateway, in the event that the NAT gateway’s AZ is down, resources in the other AZ lose internet access. To create an AZ-independent architecture, create a NAT gateway in each AZ and configure your routing to ensure that resources use the NAT gateway in the same AZ

ACL

-> VPC -> Network ACLs -> Create network ACL -> [select VPC] -> Create

You can create custom network ACLs. By default, each custom network ACL denies all inbound and outbound traffic until you add rules.

-> [ssh to public subnet instance] -> [create an index.html]

-> VPC -> Network ACLs -> [check the newly created ACL] ->Subnet associations -> Edit Subnet associations -> [select a subnet] -> Save

-> Inbound -> Edit inbound rules -> Add Rule -> [for https (433) and ssh (22)]

-> Outbound -> Edit outbound rules -> Add Rule -> [for http (80) and https (433) and Ephemeral port (1024-65535)] -> [Add deny rules] -> [for http (80)]

Rule # comes in earlier order overwrites ones in later order.

Your VPC automatically comes a default network ACL, and by default it allows all outbound and inbound traffic. (*Compare with Security Group*)

Each subnet in your VPC must be associated with a network ACL. If you don’t explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL.

Block IP Addresses using network ACLs not Security Groups

You can associate a network ACL with multiple subnets; however, a subnet can be associated with only one network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed.

Network ACLs contain a numbered list of rules that is evaluated in order, starting with the lowest numbered rule. 

Network ACLs have separate inbound and outbound rules, and each rule can either allow or deny traffic.

Network ACLs are stateless; responses to allowed inbound traffic are subject to the rules for outbound traffic (and vice versa.)

Custom VPCs and ELBs - LAB

-> EC2 -> Load Balancers -> Create Application Load Balancer -> [select at least two subnets]

## VPC Flow Logs - LAB

-> CloudWatch -> Logs -> Create log group

-> VPC -> Your VPCs -> [select a VPC] -> Actions -> Create flow log -> [select destination] -> [select log group] -> Set up permissions [or select IAM roles] -> Create

You cannot enable flow logs for VPCs that are peered with your VPC unless the peer VPC is in your account.

You cannot tag a flow log. 

After you’ve created a flow log, you cannot change its configuration; for example, you can’t associate a different IAM role with the flow log. 

Not all IP Traffic is monitored;

Traffic generated by instances when they contact the Amazon DNS server. If you use your own DNS server, then all traffic to that DNS server is logged.

Traffic generated by a Windows instance for Amazon Windows license activation. 

Traffic to and from 169.254.169.254 for instance metadata.

DHCP traffic

Traffic to the reserved IP addresses for the default VPC router. 

## Bastions

A NAT Gateway or NAT Instance is used to provide internet traffic to EC2 instances in a private subnets.

A Bastion is used to securely administer EC2 instances (Using SSH or RDP). Bastions are called Jump Boxes in Australia. 

You cannot use a NAT Gateway as a Bastion host.

## Direct Connect

Customer -Last Mile Pseudowire/LAN Extension-> Cust/Part Router -X-Connect-> DX Router -DX Connection-> AWS 

Direct Connect directly connects your data center to AWS

Useful for high throughput workloads (ie lots of network traffic)

Or if you need a stable and reliable secure connection.

## VPC End Points

Interface Endpoints

An interface endpoint is an elastic network interface with a private IP address that serves as an entry point for traffic destined to a supported service. The following services are supported:

Amazon API Gateway

AWS CloudFormation

Amazon CloudWatch

…

Gateway Endpoints

Currently Gateway Endpoints Support

Amazon S3

DynamoDB

-> IAM ->  Roles -> Create a role -> EC2 -> S3Access -> Create

-> EC2 -> Instances -> Actions -> Instance Settings -> Attach/Replace IAM Role -> [select role] -> Apply

-> VPC -> Network ACLs -> Associate subnets

-> [SSH to public EC2] -> [SSH to private EC2] -> [test it can access S3 buckets]

-> [delete the route table for the private EC2]

-> VPC -> Endpoints -> Create Endpoint -> [select VPC] -> [select route table] -> Create

-> [wait about 5 min for route table creation]

-> [back to ssh] -> aws s3 ls --region us-east-2

A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon network.

Endpoints are virtual devices. They are horizontally scaled, redundant, and highly available VPC components that allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic

# Load Balancers Theory

Application LB (Layer 7, intelligent)

Network LB (Layer 4, x performance)

Classic LB (Layer 7 or 4 that are purely on TCP protocol)

504 error means the gateway has timed out. This means that the application not responding within the idle timeout period. 

Troubleshoot web application layer or db layer.

If you need the IPv4 address of your end user, look for the X-forwarded-for header.

## Load Balancers & health check - LAB

-> [create two EC2 in separate AZ]

-> Load Balancer -> Classic Load Balancer -> [leave security group settings default] -> Configure Health Check -> Response Timeout, Interval, Unhealthy threshold, Healthy threshold (wait time maximum: (max(Response Timeout, Interval)) * Unhealthy threshold) -> [finish the rest settings] -> Create -> [wait for a while until see those LB instances are InService status]

-> Load Balancer -> DNS ->[copy the url and paste in a browser] -> [refresh page]

-> [Stop one of the EC2] -> Load Balancer -> Instances -> (One of the instance status changed to OutOfService) -> [refresh page]

Enable Cross-Zone Load Balancing means distributes traffic evenly across all targets in the AZ that is enabled

Enable Connection Draining means the number of seconds to allow existing traffic to continue flowing

-> [delete the LB] -> Target Group -> Create target group-> Targets -> Edit -> [select targets] -> Save

-> Load Balancer -> Application LB -> [select AZ] -> [select security groups] -> [select target group] -> [finish the rest setting] -> Create

-> Target Groups -> Targets -> Edit -> [select security groups] -> Add to register -> Save -> [wait a while]

-> Load Balancer -> Listeners -> View and Edit Rules -> [add rules] -> Save

Instances monitored by ELB are reported as; InService, or OutOfService

Health Checks check the instance health by talking to it.

Load Balancer have their own DNS name. You are never given an IP address.

Read the ELB FAQ for Classic Load Balancers. About 10 questions

Advanced Load Balancer

E.g. How to fix the issue that all traffic go to one EC2 rather than the other? 

A: Disable sticky session. If you want to write a file to a EC2 instance, you need to enable.  

No Cross Zone Load Balancing vs. Cross Zone Load Balancing

E.g. How to fix the issue that with Route53, if all traffic go to AZ1 but no traffic go to AZ2?

A: enable Cross Zone Load Balancing

## Path Patterns

E.g. How to deal with the scenario that with Route53, if all traffic go to AZ1 with an application LB but no traffic go to AZ2? Suppose you want [www.myurl.com](www.myurl.com) go to AZ1 and [www.myurl.com/images/](www.myurl.com/images/) go to AZ2?

A: Enable Path Patterns

Sticky Sessions enable your users to stick to the same EC2 instance. Can be useful if you are storing information locally to that instance.

Cross Zone Load Balancing enables you to load balance across multiple availability zones.

Path patterns allow you to direct traffic to different EC2 instances based on the URL contained in the request.

Autoscaling Groups Lab

-> [delete all EC2 instances]

-> Launch Configuration -> Create Launch Configuration -> [finish creation with default settings] -> Create an AutoScaling group using this launch configuration -> Group size to 3 -> [select subnets] -> Use scaling policies to adjust the capacity of this group -> [finish the rest setting] -> Create

-> [Terminate instances] -> [wait and see minimum number of instances automatically created]

-> [delete auto scaling group] -> (newly created instances will get deleted as well)

HA Architecture (High Availability Architecture)

Plan for failure

E.g. Scenario: You have a website that requires a minimum of 6 instances and it must be HA. You must also be able to tolerate the failure of 1 AZ. What is the ideal architecture for this environment while also being the most cost effective?

3 AZ with 3 instances in each AZ (so if one fails, there are still 6 available instances)

Always Design for failure.

Use Multiple AZ’s and Multiple Regions where ever you can.

Know the difference between Multi-AZ and Read Replicas for RDS.

Know the difference between scaling out and scaling up.

 Scaling out: scaling groups

Scaling up: increase EC2 capability from t2 to m

Read the question carefully and always consider the cost element.

Know the different S3 storage classes.

## HA Word Press Site

-> [Create S3] -> [Create CloudFront Distribution] -> VPC -> [Create Security Groups] -> RDS -> [Create MySQL] -> IAM -> [Create role] -> [Launch EC2 instance with downloaded htaccess file]

-> [ssh to the EC2] -> 

How to make S3 bucket public?

What does .htaccess file use for? Url rewrite?

Diff between image and volumes?

-> [Create Load Balancer] -> [Create Route53] -> [Create A name] -> [Create Target Groups]

--------------------------------------Sync S3 and wordpress site’s files---------------------------------------

-> [ssh to EC2] -> [edit /etc/crontab] -> [add command of aws s3 sync --delete s3://[bucket name] [EC2 path]-> service crond restart

-> EC2 -> Instances -> Actions -> image -> Create image

-> [ssh to EC2] -> [edit crontab] -> aws s3 sync -- delete [source name] [target name] -> service crond restart

-> EC2 -> Auto Scaling Group -> Create Auto Scaling Group -> MyAMIs-> t2 micro -> IMA role -> [edit script] -> Create launch configuration -> Create Auto Scaling Group -> [select all subnets] ->Target Groups ->  Keep the initial size -> Create Auto Scaling Group -> Close

---------------------------------------Cleaning Up--------------------------------------------------------------------

-> Target Groups -> Targets -> Edit -> [Remove one from this group]

-> EC2 -> [terminate one EC2 for reading] -> (auto scaling will create another one)

-> RDS -> Actions -> Reboot - > (Refresh webpage and get 504 error) -> RDS -> Actions -> Delete -> uncheck Create final snapshot and Retain automated backups -> Delete -> Auto Scaling Groups -> Actions -> Delete -> Target Groups -> Targets -> Edit -> [check all targets] -> Remove -> Save -> [delete Load Balancer] -> (auto created EC2 instances are terminated) -> [terminate running instances] 

-> CloudFront -> [select disabled distributions] -> Delete -> [select running distributions] -> Disable -> [delete disabled distributions]

## CloudFormation

-> CloudFormation -> Create stack -> [Select a sample templates] -> Next -> [finish the rest settings] -> Create -> [wait a while]

Is a way of completely scripting your cloud environment

Quick Start is a bunch of CloudFormation templates already built by AWS Solutions Architects allowing you to create complex environments very quickly.

## Elastic Beanstalk (1-2 questions)

What it is and how is it different from CloudFormation?

CloudFormation > Elastic Beanstalk

-> Elastic Beanstalk -> Create a web app -> Create -> [wait a while] -> Configuration -> [modify ec2, s3, load balancer, monitoring, security...] -> (a server is created)

With Elastic Beanstalk, you can quickly deploy and manage applications in the AWS Cloud without worrying about the infrastructure that runs those applications. You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling and application health monitoring. 

# Applications

## SQS

SQS is pull based, not pushed based.

SNS is pushed based.

Messages are 256 KB in size.

Messages can be kept in the queue from 1 min to 14 days; the default retention period is 4 days.

Visibility Time Out is the amount of time that the message is invisible in the SQS queue after a reader picks up that message. Provided the job is processed before the visibility timeout expires, the message will then be deleted from the queue. If the job is not processed within that time, the message will become visible again and another reader will process it. This could result in the same message being delivered twice. 

Visibility timeout max is 12 hours.

SQS guarantees that your messages will be processed at least once. 

SQS long polling is a way to retrieve messages from your Amazon SQS queues. While the regular short polling returns immediately (even if the message queue being polled is empty), long polling doesn’t return a response until a message arrives in the message queue, or the long poll timeout. 

Standard Queues (default)

Can have duplicates

Fifo Queues

First in first out

No duplicates

## SWF (Simple Workflow Service)

SWF vs SQS

SQS has a retention period. SWF workflow executions can last up to 1 year.

SWF presents a task-oriented API, whereas Amazon SQS offers a message-oriented API. 

Losely decoupled scenario is SQS

SWF ensures that a task is assigned only once and is never duplicated. SQS needs to handle duplicate messages and may also need to ensure that a message is processed only once. 

SWF keeps track of all the tasks and events in an application. With SQS, you need to implement your own application-level tracking, especially if your application uses multiple queues. 

### SWF Actors

#### Workflow Starters

An application that can initiate a workflow. 

E.g. e-commerce website following the order placement

Or a mobile app searching for bus times.

#### Deciders

Control the flow of activity tasks in a workflow execution.

A Decider decides what to do next.

#### Activity Workers

Carry out the activity tasks.

E.g. a human have some work in a data warehouse and you need a way of managing it

## SNS 

Instantaneous, push-based delivery (no polling)

Simple APIs and easy integration with applications

Flexible message delivery over multiple transport protocols

Inexpensive, pay-as-you-go model with no up-front costs

Web-based AWS Management Console offers the simplicity of a point-and-click interface

SNS vs SQS

Both Messaging Services in AWS

Push vs Pull

## Elastic Transcoder

Media Transcoder in the cloud.

Convert media files from their original source format in to different formats that will play on smartphones, tablets, PCs, etc.

Provides transcoding presets for popular output formats, which means that you don’t need to guess about which settings work best on particular devices.

Pay based on the minutes that you transcode and the resolution at which you transcode.

S3 Bucket => Lambda Function=>Elastic Transcoder=>S3 Bucket

[https://read.acloud.guru](https://read.acloud.guru)

## API Gateway (5 to 10 marks)

API caching with TTL

Same-origin policy

Enforced by web browsers.

Ignored by tools like PostMan and curl.

CORS (Cross-origin resource sharing)

E.g. If read "Origin policy cannot be read at the remote resource?", what do you do?

A: enable CORS on API Gateway.

Remember what API Gateway is at a high level

API Gateway has caching capabilities to increase performance.

API Gateway is low cost and scales automatically

You can throttle API G to prevent attacks

You can log results to CloudWatch

If you are using Javascript/AJAX that uses multiple domains with API Gateway, ensure that you have enabled CORS on API Gateway

CORS is enforced by the client

"Massive request", “increase number of visit”, “throttling limit”

## Kinesis (5 to 10 marks)

It is a platform on AWS to send your streaming data to.

Know the difference between Kinesis Streams and Kinesis Firehose. 

Kinesis Streams

Producers => Shard (24 hour to 7 days retention) => EC2 consumers to analysis => output

Store data by default for 24 hours

Streaming

Services of Shards

Kinesis Firehose

Producers => Kinesis Firehose to analysis => output (=> Redshift)

Producers

No data persistency

Analysis data on the fly automatically

Lambda

Output can be Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk

Understand what Kinesis Analytics is.

Capacity of both Kinesis Streams and Kinesis Firehose

## Web Identity Federation - Cognito

Sign-up and sign-in to your apps

Access for guest users

Acts as an Identity Broker between your application and Web ID providers, so you don’t need to write and additional code.

Recommended for all mobile applications AWS services.

User Pools

It is user based. It handles things like user registration, authentication, and account recovery.

JSON Web token (JWTs)

Identity Pools

Authorise access to your AWS resources.

User => Facebook/Google/Amazon => User Pool =JWT Token=> User =JWT=> Identity Pool =AWS Credentials=> User => Access AWS resources

Cognito tracks where the user sign-in from

It synchronize user data across multiple devices.

It users SNS to send notification to all the devices associated whenever cloud data changes.

Federation allows users to authenticate with a Web Identity Provider

# OpsWorks

Orchestration Service that uses Chef

Chef consists of recipes to maintain a consistent state

Look for the term "chef" or “recipes” or “cook books” and think OpsWorks

# Consolidated Billing

Will be tested for saving money

Unused reserved instances for EC2 are applied across the group.

Always enable multi-factor authentication on root account.

Always use a strong and complex password on root account

Paying account should be used for billing purposes only. Do not deploy resources in to paying account. 

CloudTrail

Per AWS Account and is enabled per region.

Can consolidate logs using an S3 bucket

1. Turn on CloudTrail in the paying account

2. Create a bucket policy that allows cross account access

3. Turn on CloudTrail in the other accounts and use the bucket in the paying account

Power User Access allows Access to all AWS services except for management of groups and users within IAM

For configuring AWS accounts for multiple region, you will need to configure Users and Policy Documents only once, as these are applied globally. 

RAID = Redundant Array of Independent Disks

RAID 0 - Striped, No Redundancy, Good Performance

RAID 1 - Mirrored Redundancy

RAID 5 - Good for reads, bad for writes, AWS doesn’t recommend for EBS

RAID 10 - Striped & Mirrored, Good Redundancy, Good Performance.

E.g. you are not getting the disk IO that you require. Maybe the RDS service is down and you need to use db on EC2. What is your solution? A: You need to add multiple EBS volumes and configure them as a RAID array. 

-> EC2 -> Choose Instance Type -> Windows R2 Server -> Add Storage -> [add 4 EBS volumes, each for 8GB] -> Security Group -> [add one for RDP] -> Launch

-> Log into Windows ->Disk Management -> [delete those EBS disk and create RAID]

E.g. How to take a snapshot over a RAID array? 

Problem - A snapshot excludes data held in the cache by applications and the OS. This tends not to matter on a single volume, however, using multiple volumes in a RAID array, this can be a problem due to interdependencies of the array. 

Solution - Take an application consistent snapshot. Ways of flush all caches to the disk.

1. Freeze the file system

2. Unmount the RAID Array

3. Shutting down the associated EC2 instance.




