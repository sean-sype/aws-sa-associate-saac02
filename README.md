# aws-sa-associate-saac02
Course Files for AWS Certified Solutions Architect Certification Course (SAAC02) - Adrian Cantrill

If you find something wrong feel free to let me know at  saac02-feedback@cantrill.io
- or -
if you want to help fix something, feel free to submit a PR with your suggested fixes and I'll review
If you want to use any portion of this repo in your own projects, just make sure you are aware of the license terms ... and I'd appreciate a friendly heads-up :)


# aws accounts
- many companies use many aws accounts.
- container for identities (resource) and resources
- every account has an account root user - requires unique email address and credit card
- IAM - users, groups, and roles and also be created and given full and limited permissions (identity and access management)

# cli tips
- add user profile to your aws CLI
    ` aws configure --profile iamadmin-prod ` # This adds a profile to your aws cli.

# cloud computing
Set of 5 conditions that makes a platform a "cloud"
+ taken from NIST - national institute of standards and technology - 800-145
- 1. on demand self service - you can provision capabilities as needed **without requiring human interaction**.
- 2. Broad network access - Capabilities are available over the **network** and accessed through **standard mechanisms**.
- 3. Resource Pooling - there is a sense of **location independence** no **control or knowledge** over the exact **location** of the resources. Resources are **pooled** to server multiple consumers using a **multi-tenant model**
- 4. Rapid Elasticity - Capabilities can be **elastically provisioned** and **released** to scale **rapidly** outward and inward with demand. "To the consumer, the capabilities available for provisioning often **appear** to be **unlimited**.
- 5. Measured Service - Resource usage can be **monitored, controlled reported and billed**

## Public vs Private vs Multi vs Hybrid Cloud
* Public Cloud - using 1 public cloud
* private cloud - using on-premisies **real** cloud
* Multi-Cloud - using **more than 1** public cloud
* hybrid cloud - Public and Private Clouds
* hybrid cloud is NOT public cloud + legacy on-premise, that is a Hybrid network

## Cloud Service - X as a Service
* Application Stack - Data/runtime/container/O.S./Virtualization/Servers/Infrastructure/
* on premises - manage the entire stack, hosting, and costs
* ![Alt text](/screenshots/CloudServiceModel.jpg?raw=true "Cloud Service Model")

# YAML
* human readable for data serialization - human readable
* unordered collection key:value pairs, each key has a value
* lists - ordered set of value - lists also have "-" hyphen
* dictionary - data structure -
```
Resources: (dictionary)
    s3bucket: (key which is also a dictionary)
        Type: "AWS::S3::Bucket" (property value string value )
        Properties: (dictionary containing)
            BucketName: "ac1337catpics" (key with the value of)
```

# JSON
* lightweight data-interchange format, easy for humans to read and write, it's easy for machines to parse and generate.
* two main elements
- Object, unordered set of key: value pairs enclosed by {&}
- Array, ordered collection of values, separated by commas & enclosed

# OSI
- Physical - voltage and medium
+ Data - Frames unique Hardware (MAC) - 48 bits in hex and 24 bits for manufacturer - OUI - Control access to the physical medium
1. Preamble 56 bits
2. SFD 8 bits -
3. destination mac
4. Source Mac
5. ET EtherType - Protocol -
6. Payload - Contains the data by the protocol - ethernet frame
7. FCS - Corruption Check
- carrier sense multiple access (CSMA) / CD (collision detection)
- Encapsulation - inside a frame and the payload is extracted from the frame - encapsulated
- switches understand frames and mac addresses. they maintain a mac address table, which starts off empty. as the switch receives frames on its ports, it learns which  devices are connected and populates the mac address table
- unicast 1:1 and broadcast 1:all
## IPV4 addressing
- Decimal Binary - Dotted-Decimal Notation 4x0-255

| Position              | 1     |     2 |     3 |     4 |     5 | 6     | 7     | 8     |
|   :---:               | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Binary Position Value | 128   | 64    | 32    | 16    | 8     | 4     | 2     | 1     |
| Binary Value          |       |       |       |       |       |       |       |       |

- ARP - Address resolution protocol (ARP)
- Network - Cross networking addressing
- ARP/Route/Route Tables/Routers
## Transport and Session
+ TCP/IP and UDP/IP - Transport
- TCP Segments
    - Source port, destination Port
    - Sequence Number - error correction - and ordering
    - acknowledgement (syn/ack)
    - Flags n things
    - window
    - checksum
    - urgent pointer
    - options , padding
    - data
    - three way handshake
     - Syn - sets CS
     - Syn-ack - increment cs+1, picks a random sequence ss (sends segment)
     - ack cs+2 and ss+1
- **Stateless firewall would see two things. Outbound, Response TWO rules for each TCP directions (in and out)**
- **Stateful firewall views see’s one thing outbound, implicitly allows the inbound response**
# NAT Network Address Translation
- Static Nat - 1 private to 1 (fixed) public address (IGW)
- Dynamic Nat - 1 private to 1st available public
- Port address translation (PAT) - many private to 1 public (NATGW)
- Many:1(priateIP:PublicIP) Architecture The nat device records the source (private) IP and Source Port. Replaces the source IP with the single Public IP and public source port allocated from a pool which allows IP overloading (many to one)

# Subnetting
## IPV4
- 4,294,967,296 total addresses available ipv4
- * ![Alt text](/screenshots/subnetting-visual.jpg?raw=true "Subnetting")

# DDoS
* distributed - hard to block individual IP/ranges
* application Layer - http flood
* protocol attack - Syn flood - doesnt send an ACK - fills up the network resources and the connections cant connect.
* volumetric - dns amplification
 - a botnet exploits a protocol where a response is significantly larger than the request. in this case making a spoofed request to dns, dns responds to spoofed IP for our application which is overwhelmed by the amount of data

 # SSL and TLS
 - TLS ensures privacy via encryption - asymmetric and then symmetric , identity (server/client server) verified - reliable connection protection
 - Cipher suites -
 - Authentication
 - Key exchange

 # AWS Fundamentals
 ## Aws Public vs Private Services
 - private and public - relate to the networking only
 - which network zone the service is in
 - aws public zone, directly connected to the internet. IE: s3 bucket - s3 service - hosted in the aws public zone - but doesn't mean you have access to it.
 - aws private zone. No direct connectivity to the aws public or public internet. Isolated by default, and can be isolated via VPC - virtual private cloud - ie: ec2 instance
 - you can allow selective connections to it via the aws public zone

 ## Aws global infrastructure
 - AWS region , full compute storage db ai analytics
 - edge locations - local distribution points - content is stored in edge locations (CDN)
 - Geographic Separation - isolated fault domain
 - geopolitical separation - different governance.
 - Region names: code or name
 - availability zone (multiple locations isolated infrastructure)
 - services can be placed across multiple AV's with VPC - that can work across all AV's
 - define resilience level
    - Globally Resilient - data replication across entire regions
    - region resilient - rds in Sydney - replicate data to multiple AV's
    - AZ Resilient - single av zone service resilient

## VPC
- VPC is a regional service that can operate in multiple AV's
- Private and Isolated - from other VPCs and public AWS
- Default VPC - 1 per region and Custom VPCs - but many custom VPCs
- VPC cidr defines the start and range of the addresses : its always 172.31.0.0/16
    - us-east-2a | us-east-2b    | us-east-2c
    - configured for one subnet in every AV, its a smaller /20
    - subnets assigned a public IPV4 addresses - default vpc they will have public IP addresses
    - tend to not use them on production services as they are too inflexible.

## EC2
- IAAS - Provides Virtual Machines = instances
- Private service by-default - uses VCP networking
- AZ resilient - instance fails if AZ fails
- sizes and capabilities
- on demand billing - per second
- elastic block storage - EBS
- running - stopped - terminated
- storage is still used even if its in a stopped state - EBS
- AMI - amazon machine image
    - attached permissions
    - public - everyone allowed
    - owner - implicit allow
    - explicit - specific aws accounts allowed
    - ami contains the boot drive
    - block device mapping - boot volume or data volume
- create key pairs in advanced

## S3 Buckets
- Global Storage platform - access from anywhere on the Internet. Regional based/resilient - at rest.
- objects and buckets
    - object key is a file name - value is the data or content being stored. the value of the object can range from zero bytes to 5tb...
    - buckets - primary home region unless you configure that data to leave that region - what laws and rules apply to that data
    - bucket name needs to be globally unique
    - bucket unlimited bytes of data - flat structure  
        - there are prefix on names though
        **Flash Cards**
        - exam power-up: - Bucket names are globally unique
        - 3 and 63 characters all lowercase and no underscores
        - limit of 100 buckets in an aws account 1000 hard limit
        - unlimited objects in a bucket 0 bytes to 5tb
        - key = name, value = data
        - S3 is an object store - not file or block. Windows - file based storage.

## Cloud Formation
- Template written in yaml / json
- templates contains resources and all the other things
- Resources are called logical resources - instance: type: aws::EC2::Instance
- stack is a living and representation of a template - physical resource - you update the resource/ it updates the stack

## Cloud Watch
Three Main Jobs
- CWAgent
- Collects and Manages operational data - any logging
1. Metrics - AWS Products, Apps, On-premises
    - cpu metrics, memory, disk, need cloud watch agent
    - gathers and stores this data - api interface to access the data
2. CloudWatch Logs - AWS Products, Apps, on-premises
3. CloudWatch Events - AWS Services & Services
    - generate an event to do something on a schedule or based off another event via SNS (Simple Notification Service)
+ CloudWatch Basics
- * ![Alt text](/screenshots/CloudWatchBasics.jpg?raw=true "CloudWatchBasics")
- Namespace
    - Viewed as a "container" to keep the data in that namespace.
    - AWS/${Service} ex: AWS/Ec2
        - can name them anything you want.
- Metric
    - Time Ordered Set of Data Points
    - Alarm - Metric is not in a good state and you can define an action
- Dimension
    - Separate data points for different things or perspectives within the same metric.

### Demo CloudWatch
- CLI Commands: `sudo amazon-linux-extras install epel -y` & ` sudo yum install stress -y `

## Shared Services
- ![Alt text](/screenshots/SharedServices.jpg?raw=true "SharedServices")

## HA VS FT VS DR
- High Availability vs Fault-Tolerance vs Disaster Recovery
+ HA - aims to ensure an agreed level of operational performance, usually uptime, for a higher than normal period. Minimizing any outages.
+ FT - Fault Tolerance - is the property that enables a system to continue operating properly in the event of the failure of some (one or more faults within) of its components.
+ DR - A set of policies, tools and procedures to enable the recovery or continuation of virtual technology infrastructure and systems following a natural or human induced disaster.

# IAM Identity Policies
- Understanding their architecture and read them is required for the exam
- Grants access or denies access to your aws services
+ ARN: Amazon Resource Name - Uniquely Identify resources within any aws account(s)
+ Effect: action verb to the event: ie: deny,allow
+ Rules: First Priority
    - Explicitly Denies, nothing can overrule
    - 2nd Priority: Explicit Allow
    - DENY, ALLOW, DENY
- Inline Policy (json) and Managed Policies - how they are managed.
- Managed policy is their own object which then can be attached to each identity. THey should be used for the normal default operational rights in your business.
    - Low management overhead, update json, it updates all the identities asap.
    - use inline for special or exceptional allow/deny
- Customer managed policies that you can modify; default aws policies.

## IAM users
- IAM users are an identity used for anything requiring long term aws access. EG: Humans, Applications, Service Accounts
- IAM Starts with a principal which represents an entity trying to access an aws account. They can be individual people, computers, services or a group of any of those things.
    - must be authenticated and authorized.
- ARN: arn:partition:service:region:account-id:resource
- arn: arn:partition:service:region:account-id:resource-type/resource-id
- only **5,000** IAM user per account (remember the 5000)
- max of 10 groups
- Use federation or IAM Roles if there are more than 5k IAM users.

## IAM GROUPS
- IAM groups are containers for Users
- You can NOT log into a group - no credentials
- Organization of IAM users. Users can be on multiple groups.
- Both in-lined and managed - which allow/deny that a user has directly - all still follow deny/allow/deny
- no max group membership - trick question around an "all users group" does not exist natively
- no groups within group.
- groups have users, and permissions.  - 300 groups per account max. can be increased.
- groups are not a true identity - they cant be referenced as a principal in a policy

## IAM Roles - The Tech - Review
- I am roles are also identities - by an unknown number or multiple aws users, humans, applications or services inside or outside of your aws account.
- if you have more than 5,000 principals, it's a good idea to use iam role.
- TEMPORARY of time then stops
- role represents a level of access within an aws account. Short term.
- temporary credentials are time limited before they expire
- STS secure token service - sts:AssumeRole = Roles
- Roles can be Assumed
- When assumed - temporary credentials are generated

## When to use IAM roles - When to use IAM roles - review
- Within the same AWS account - AWS Lambda - execution role , whether a function is executed
- Emergency or out of the usual situation - break glass situation... ie fire alarm
- to re-use...On-premises - existing identities active directory - external accounts or identities can not interact with AWS.
- Web Identity Federation which uses IAM roles
- Partner Accounts - use a role in the partner account - get temp security credentials.

## IAM AWS org
- Management account, can invite existing standard aws account into the AWS organization.
- Change from standard accounts to being member accounts.
- Billing is then removed and passed to the management account. aka Payer account - aws account that contains the payment method of the org.
- use IAM roles in multi account setups
- Most orgs use one clean and one account for the logins.

## AWS Org DEMO Part 1 & 2
- how to role switch into the production account.
- When you create an account within the organization a **role is created within that account which an be role switched into by other accounts within the organization**
- If you invite an existing aws account into the organization, then you need to manually add this role.

## SCP Service Control Policies
- Used to restrict AWS accounts.
- Policies document that can be attached to the root container or one or more org units - even individual aws accounts.
- Service Policies inherit downward. Or OU with inheritance.
- SCP's are account permissions boundaries
- They limit what the account (including the account root user can do)
- they don't grant permissions.
- Explicit deny always wins.

## SCP Demo
-

## CloudWatch Logs
- Public Service - AWS Public Zone - Usable from AWS or On Premises
- Store, Monitor and Access logging data
- AWS Integrations - ec2, vpc flow logs, lambda, CloudTrail, R53...
- Needs connectivity and permissions.
- Security normally provided by IAM roles or service roles
- Custom logs - unified cloud watch agent
- development kit form AWS and integration it directly into your application
- It can contain metrics like failed SSH connections then you can create alarms that watch for the metric.
- Regional Service
- Log events inject it into the region YYYMMDDHHMMSS MESSAGE
    - /var/log/messages - each log log stream is unique, and ordered set
    - log groups - containers for log streams
    - log groups also contain, retention and permissions, metric filters

## Cloud Trail
- Logs API calls/activities as a CloudTrail Event
    - by default stores 90 days in Event History
    - No cost, if 90 days.
    - to customize create 1 or more trails
    - Management events and data events
- Cloud Trail is a regional service OR can be set to ALL regions TRAIL.
- Data events has to be set manually
- stores it in json and compresses them into an s3 bucket it can also go into cloud watch logs. (log parser)
- EXAM -
    * Enabled by default but 90 days
    * Trails are how you configure s3 and CWLogs - Default for Trails is to store management events ONLY (creating instance, stopping, logging into the console)
    * IAM, STS, CloudFront - global services, and that gets logged to the us-east-1
    * and a trail will need to be enabled to capture that.
    * NO REAL TIME - there is a delay - 15 mins normally

## Cloud Trail Demo
- provides a certain amount of free tier service - only a certain amount of data

# S3

## S3 Security
- S3 is private by default
- S3 bucket policy aka a form of resource policy
    - allow/deny same or different accounts
    - Resource perspective permissions
    - Like identity policies but attached to a bucket.  
    - allow/deny anonymous principals
    - two main goals: give access to other aws accounts and
    - ACLs are used, but not recommended.
    - Block Public Access -
* Exam Power Up
    - If you are granting or Denying permissions on lots of different resources across an aws account, then use Identity Policies
    - single place: IAM - IAM is the only single place where you can control permissions for everything.
    - Permissions within the same account (no external access) -
    - if you want to grant a single permission to everybody accessing one resource or everybody in one account, then it's much more efficient to use resource policies to control that base level permission.
    - Anonymous / external identities from other aws accounts: Resource Policies

# S3 Static Hosting
- Index and Error documents are set , HTML files ,
- Static website hosting endpoint. Generating by region and bucket name.
- custom name - bucket name requires the domain
- offloading - static media hosting , static html
- out-of-band pages - an error or a status notification system. Maintenance page, change dns the point it to a backup static HTML page / support page.
- cost, per gig month fee, transfer fee (data / out) per gig charge
- Free
    - 5 gb
    - 20k get requests
    - 2k put requests
## S3 Demo

## Object Versioning & MFA Delete
- Object is controlled at a bucket level - you can not disabled it again
    - you can suspend it, and then re-enabled.
    - lets you store multiple versions of objects within a bucket. Operations which would modify objects generate a new version.
    - new object is known as the current object Latest version OR Current Version
    - individually accessed by specifying the ID.
    - delete marker
    - you can delete the object with the version number
    - MFA is required to change bucket versioning state
    - MFA is required to delete versions
    - need the Serial Number MFA + Code passed with API calls

## S3 Performance Optimization
- Make the upload faster / safer with Multipart Upload
    - minimum size is for 100MB
    - parts can fail and be restarted
    - improves transfer rate
    - transfer acceleration - must be enabled for transfer
        - no periods in name
        - uses edge locations
        - dns compatible in its naming
        - picks the closest, best performing S3 edge location

## Encryption
- Plaintext - unencrypted data - image and applications
- Algorithm - blowfish, aes, rc4, des, rc5, rc6
- key - "password"
- ciphertext - encrypted data - need the key to decrypt
- know what Asymmetric is and how it works
- Signing
    - used to verify identity.
    - encrypt using your private key
    - party can use your public key to decrypt to verify identity
- Steganography
    - message of hiding something
    - hide a message in a image

## Key Management Service KMS
- Regional and Public Service
- Public Service, public zone access from anywhere but need permissions
- can handle symmetric and asymmetric keys (encrypt, decrypt)
- KMS Keys never leave (provides FIPS 140-2)
- CMK Customer Master Key - applications, services, and users can use them
    - logical - ID
    - backed by physical key material
    - generated and or imported
    - CMK can be used for encrypted and decrypt for only up to 4kb of data
- Data Encryption Key (DEKs)
    - Generate Data Key works on larger than 4kb
    - plaintext version first and ciphertext version
    - discard the plaintext one
- Exam PowerUp
    - CMK's are isolated to a region and never leave.
    - They also never leave the KMS service
    - AWS managed CMK or Customer Managed CMK's
        - Customer Much more configurable
    - support key rotation - it can't be disabled every 1095 days (3 years)
    - CMK's backing key and previous backing keys - aliases
        - per region - alias no keys are globally
        - key policies - CMK has a IAM / Principal
        - action KMS
        - identities can manage a key, also may not be able to use a key

## KMS Demo
* using kms on CLI
    -   
        ```
            aws kms encrypt \
            --key-id alias/catrobot \
            --plaintext "path to file" \
            --output text \
            --query CipherTextBlob \
            --profile iamadmin-general | base64 \
            --decode > not_battleplans.enc
        ```

    -
        ```
            aws kms decrypt \
            --ciphertext-blob fileb://not_battleplans.enc \
            --output text \
            --profile iamadmin-general \
            --query Plaintext | base64 --decode > decryptedplans.txt        
        ```

## Object Encryption - PART1 and 2
- Buckets aren't encrypted, objects are
    - client-side encryption
    - server side encryption (both are at rest on S3)
    - Both use in-transit `encryption
- Server side encryption
    - Server-Side Encryption with Customer Provided Keys (SSE-C)
        - Need an plain text object and a key
        - when they arrive at the S3 endpoint | hash is taken and attached to the object, then s3 encrypts the object. Then the key is discarded for security.
    - Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)
        - put just the plaintext artifact
        - s3 handles all encryption
        - it is the default option
        - AES-256
    - Server-Side Encryption with Customer Master Keys (CMKs) Stored in AWS Key Management Service (SSE-KMS)
        - S3 will create an aws managed customer master key (CMK)
        - Roles are important, KMS policy and permissions must have decryption
        - s3 administrators can admin but not have a way to decrypt.
    - Bucket Default Encryption
        - x-amz-server-side-encryption PUT header.
        - objects will not use encryption unless it's passed.

## Demo Object Encryption
-

## Object Storage Classes
- S3 Standard - 3 availability zones - 11 9's
    - has a milliseconds first byte
    - standard for frequently access data which is important and non replaceable
- S3 IA - In frequent access
    - 3 av's
    - first byte is still millisecond
    - Its cost effective using IA
    - There is a retrieval fee + transfer fee
    - bill minimum duration charge of 30 days
    - minimum capacity charge of 128 KB per object
    - Should be used for long lived data which is important but where access is infrequent
- S3 IA - One Zone-IA
    - does not provide the multi-az resilience model - only one az is used
    - used for long lived data, which is infrequently accessed, also non CRITICAL data
    -

## Object Storage Classes Part 2
- S3 Glacier
    - 3 az
    - same durability 7 9's.
    - 1/5th the cost of s3 standard
    - first byte latency = minutes or hours - cold/chilled storage
    - 40kb min size and 90 day min duration
- S3 Glacier Deep Archive
    - standard is 12 hours
    - bulk is up to 48 hours
    - rare or if ever need access   
    - legal and regulatory requirements, throw old archive data at.
- S3 Intelligent-Tiering
    - Intelligent-Tiering monitors and automatically moves any objects not accessed for 30 days to a low cost infrequent access tier and eventually to archive, or deep archive tiers.
    - As objects are accessed, they are moved back to the frequent access tier.
    - no retrieval fees for accessing objects, only a 30 day minimum duration
    - unknown or uncertain usage, use Intelligent-Tiering

## S3 LifeCycle Configuration
- Optimize costs
- Set of rules consist of actions on a bucket, or groups of objects.
- transition action (s3 standard to IA after 30, IA to glacier after 90 days)
- Expire action, objects for cost optimization
- ![Alt text](/screenshots/S3LifecycleConfigurationTransitions.jpg?raw=true "S3 LifeCycle")

# S3 Replication
- Cross-Region Replication (CRR)
- Same-Region Replication (SRR)
- if it's in a different aws account
    - role is configured for replication
    - you need an additional requirement, bucket policy to allow the role in the source account to write to its bucket form the origin bucket
- what to replicate ?
    - All objects or a subset of objects (tags, prefix, ect..)
    - Storage Class - defaults to maintain
    - storage class is the same as the destination and origin
    - ownership - default is the source account
        - different accounts - by the owned source bucket account
    - Replication Time Control
        - 15 min SLA guaranteed replication
        - only use if you have really strict requirements on storage replication
- Exam Power up
    - **Replication is not Retroactive & Versioning needs to be ON**
    - One-way replication Source to Destination only.
    - Unencrypted, SSE-S3 & KMS (with extra config)
    - Source bucket owner needs permissions to objects
    - No System events, Glacier, or Glacier Deep archive
    - no deletes are replicated
    - SRR - Log Aggregation
    - Prod and Test sync - replicate data dev to prod
    - Resilience with strict sovereignty
    -
## DEMO Cross-Region Replication of an S3 Static Website
- Disaster Recovery

## S3 Presigned URLs
- Pre Signed URLs are a way that you can give another person or application access to an object inside an s3 bucket using your credentials in a safe and secure way.
- can enable put or get request via the iamadmin who generates a presignedURL
- Exam Power Ups
    - You can create a URL for an object you have no access too
    - When using the URL, the permissions match the identity which generated it
    - access denied could mean the generating ID never had access or doesnt know
    - Don't generate with a role, URL stops working when temporary credentials expire
    - never a good idea to generate a pre-signed URL using an IAM role. Generally use an IAM user vs role.

## S3 Select and Glacier Select
- Select let you use sql-like statement
- part of the object pre-filtered by s3

## S3 Events
- event notifications on a bucket
- delivered to sns, sqs, lambda functions
- Object created (put,post,copy,completemutlipartUpload)
    - on object creation, send the object to some destination, then have an event driven automated workflow
- EventBridge is a bit newer and has more features.

## Access Logs
- access logging can be enabled via the console UI or via PUT Bucket logging
- S3 Log Delivery Group, bucket acl, allows s3 log delivery group

# Virtual Private Cloud (VPC) Basics
## Networking Refresher Part 1 & 2
- IP - Refresher
- 10.0.0.0`
- 172.16 - 172.31.255
- 192.168.0.0 - 192.168.255
- /8 A /16 B /32 C

## VPC Sizing and Structure - Part 1 & 2
- VPC cidr / range - need to know what range the VPC will use In advance
- what size should your VPC be?
- are there any networks we can't use?
- try to predict the future
- vpc structure - tiers, and resiliency and AV's
- starting point of 10.16 ~
- how many aws regions the aws account will operate in
    - pre-allocating - reserve 2+ networks per region being used per account

- VPC Sizing
    - a subnet is in one AV
    - **how many availability zones your VPC will use**
    - this decision impacts high availability and resilience and it depends somewhat on the region that the VPC is in.
    - generally start with three as the default, because it will work in almost any region, with one spare.
    - need to split the VPC into at least 4 networks or 4 / 18's
    - tier: Web, app, db, spare
    - ![Alt text](/screenshots/VCPSizing.jpg?raw=true "Structure Example")

- Guidelines
    1. You consider the business needs
    2. avoid the ranges that you can't use
    3. allocate the remainder based on your business Physical, or logical layout, and then decide upon and create VPC and subnet structure from there.
    4. work either with top down or bottom up, you can start with the minimum subnet size that you need and work up or reverse

## Custom VPCs
- Nat gateway - which will give private instances outgoing only access
- Internet gateway which will give resources in the VCP public access
- bastion  - connect securely into the VPC
- Regionally Service and ALL Az's in the region
- nothing in or out without explicit configuration
- flexible configuration - simple or multi-tier
- hybrid networking
- default or dedicated tenancy (dedicated hardware)
    - ipv4 private cidr blocks and public
    - 1 primary private ipv4 cidr block
    - min /28 max /16
    - optional secondary ipv4 block
    - optional single assigned ipv6 /56
    - dns in a vpc - base ip + 2
    - Exam - enableDnsHostnames - gives instances DNS Names
    - enableDnsSupport - enables DNS resolution in VPC

## VPC Subnets
- Blue means private subnets, green means public
- Subnet: AZ Resilient
    - a subnetwork of a VCP - within a particular AZ
    - 1 subnet => 1 AZ, 1 AZ => 0+ Subnets
    - IPV4 CIDR is a subset of the VPC Cider
    - Cannot overlap with other cidr
    - Subnets can communicate with other subnets in the VPC
    - Reserved IP addresses (5 in total)
        - example: 10.16.16.0/20 (10.16.16.0 => 10.16.31.255)
        - Network address (10.16.16.0)
        - Network + 1 (10.16.16.1) - VPC Router (dfg)
        - Network + 2 (10.16.16.2) - Reserved DNS
        - Network + 3 (10.16.16.3) - Reserved Future Use
        - Broadcast address (10.16.31.255 last ip in subnet)
    - DHCP Option set applied to one VPC at one time - flows to subnets

## VPC Design Demo
- ipv6 - can be allocated with a /56 CIDEr

## VPC Routing and Internet gateway Bastion Hosts
- simply routes traffic between subnets and VPC'
- local always takes priority
- IGW (internet gateway)
    - Region Resilient gateway attached to a vpc
    - you do not need a gateway per av
    - 1 vpc = 0 or 1 IGW
    - Internet gateway runs from the border of the VPC and the aws Public zone
    - its what allows services inside a PVC which are allocated with public IP's to be reached from the internet.
    - IGW maintains the public IP
    - IPV4 has no public IP on the EC2
- Bastion Host / Jumpbox
    - incoming management connections arrive there
    - access internal VPC resources
    - integrate with SSH

## Network access control lists (NACls)
- "firewalls that surrounds subnets"
- in or out of a specific subnet
- ephemeral ports - inbound and outbound
- nothing is denied by the VPC by default
- Exam power up
    - stateless - initiation and response seen as different (need to add two rules)
    - only impacts data crossing subnet border
    - Can explicitly allow and Deny traffic (one particular deny, use ACL)
    - IP's/network, ports and protocols - no logical resources
    - NACLs cannot be assigned to AWS resources only subnets
    - Use with SG's to add explicit Deny bad ip / s nets
    - One subnet = one NACL at a time

## Security Groups
- Security groups are assigned to an aws resource (network interface of a aws product)
- NACLS are stateless (initiation and response)
- Security groups are stateful
    - only one rule is required for bi-directional traffic
    - a default security group is created on a VPC
    - rule is allow all traffic
    - references itself
    - have a hidden implicit denied | if its not allowed, its denied.
    - you can not explicitly deny a single rule/ip/resource. use ACLs for that.
- Exam Power up
    - Stateful - Traffic and Response = same rule
    - SG's can filter based on AWS logical Resources
        - Resources, other than SG's and even themselves.
    - Implicit Deny and Explicit Allow
        - No Explicit Deny
    - NACLs on subnet for any products which don't work with SG's (eg Nat Gateway)
    - NACLs when adding explicit deny (bad ip's, bad actors)
    - SG's as the default **almost everywhere**

## Network Address Translation (NAT) and NAT Gateways
- giving a private resource outgoing only access to the internet.
- static nat - 1:1 ration
- ip masquerading - hiding CIDR blocks behind one IP - Classes Inter-domain routing
- Runs from a **public subnet** - already need a VPC where it has public subnets (internet gateway/and default routes/pointing at the IG)
- Uses elastic IP's (static ipv4 public)
- AZ resilient Service (HA in that AZ)
    - one nat gateway in each AZ that you are using in a VPC
        - route table to private subnets for each AZ with that NATGW as a target
- Managed, Scales to 45 gbps, $ Duration & data Volume
    - NAT Gateway is HA in the AZ, but you need them in each AZ - not the region
    - enable ec2 as nat: disable source destination checks.
    - no bastion
    - can not do port forwarding
    - only NACL's - NO Security Groups
- EC2 - Nat Instance
    - if the AZ fails, it fails entirely
    - can be cheaper (ie dev/stage)
- NAT isn't required for IPv6
    - if you add IPV6 as a route, you get bi-directional connectivity to the aws public zone
    - will not work with NAT gateway/Nat-Instance
- SSH Agent Forwarding
    - generate ssh key pair
    - public part is added as authorized keys
    - only used in the initial phase connection
    - ssh-add - adds it to the ssh-agent service
    - -A (or ssh agent forwarding)

## NAT Gateway Demo
- Elastic IP doesn't change
- explicitly set a route table with a subnet with that same AZ to enable routing.

# Ec2 Section

## Virtualization 101

## EC2 Architecture
- Use most often on AWS - a lot of exam questions
- ec2 instances run on ec2 hosts
- shared hosts or dedicated hosts
- AV resilient service - if the AZ fails, the Ec2 instance could also fail
- Instances cannot natively move between AV. Hardware, networking, storage, locked inside one AV zone.
- when to use
    - application compute app needed
    - support requirements
    - long running compute needs
    - bust or ready state
    - monolithic application stacks
    - migrated application workloads or DR

## EC2 Instances Part 1 and 2
- General Purpose - default - diverse workloads, equal resource ration
- Compute optimized - media processing, hpc, scientific modelling, gaming, machine learning
- memory optimized - processing large in-memory datasets, some database workloads
- accelerated computing - hardware gpu, field programmable gate arrays (FPGAs)    
- Storage Optimized - Sequential and Random IO - scaled-out transactional databases, data warehousing, elasticsearch, analytics workloads
- R5dn.8xlarge
    - R : Instance Family
    - 5 : Instance Generation
    - 8xLarge : Instance Size
    - dn - Additional Capabilities
- https://instances.vantage.sh/

## Storage Refresher
- Direct (local) attached Storage - Storage on the ECT Host
- Network Attached storage - volumes delivered over network (EBS)
- Ephemeral Storage - Temporary Storage
- Persistent Storage - Permanent storage - lives on past the lifetime of the instance
- Block Storage - volume presented to the OS as a collection of blocks.
    - Mountable, and Bootable
- File Storage - Presented as a file share, mountable, NOT bootable.
- Object Storage - collection of objects **flat** - Not mountable. not bootable.
- Storage Performance
    - IO (block size) X IOPS (input output operations per second) = Throughput
    - IOPS - You can think of the speed at which the engine of a race car uns at, the revolutions per second.
    - IO - as the size of the wheels of the race car.
    - Throughput as the end speed of the race car.

## EBS Elastic Block Store
- Block storage - raw disk allocations (volume) - Can be encrypted using KMS
    - instances see block device, and create file system on this device (ext3/4, xfs/ ntfs)
- storage is provisioned in ONE AZ (resilient in that AZ) - single point of failure
- attached to *one ECT instance (or other services) over a storage.
- can do multi attach - but the cluster application has to manage it, otherwise overwritten data
- can be detached and reattached to one instance .. persistent (on restart)
- snapshots backup into s3 - create volume from snapshot (migrate between az's)
- physical storage types, different sizes, different performance profiles
- billed based on GB-month
- **no cross AV attachment possible**
- snapshot volumes to S3 to backup data - then create ebs volume in another AV - also regions

### EBS Volume Types
- General Purpose SSD - GP2
- as small as a 1gb or large as 16tb
- an IO credit is 16KB - IOPS assume 16KB - 1 IOPS is 1 IO in 1 Second
- 5.4 million IO credits, fills at rate of baseline performance (size / rate)
- 100 IO credits per second
- max 16k
- great for boot volumes, dev/test, low-latency interactive apps.
- GP3
    - SSD based - removes the credit bucket arch
    - standard 3000 iops (3016kb / second 125 MB / second)
    - 1gb to 16 tb
    - !20% cheaper
    - higher max throughput - 1000 mb / second
    - virtual desktops, medium sized single instances DB's MSSQL or Oracle
    - low-latency interactive apps, dev and test, boot volumes.

## EBS Provisioned IOPS SSD
- 3 types - Io1 / io2 / io2 block express
- iops are configurable independently of size -
- highly performant drives
- 256k iops per volume - block express 4/mb/s
- 4gb to 16 tb - express 64 tb volumes
- io1 560IPS / gb max
- io2 500 iops/gb max
- express 1000iops/gb max
- per instance performance:
    - io1 - 260k iops and 7500 mb's
    - io2 - 160 iops & 4750 mb's
    - io2 express 260k 7500 mb's

## EBS HDD Based
- st1 throughput optimized
    - cheap
    - designed for data to be written or read
    - 125gb to 16tb
    - 500 mb / second
    - big data, data warehouses, log processing
- sc1 - cold hdd
    - cheaper
    - in frequent work loads
    - don't care about performance
    - 250 max iops 1mb 250 / mbs
    - 125 gb to 16 tb

## Instance Store Volumes
- provide block storage devices - used as the basis for a filesystem
- physically connected to one ect host
- each ec2 host has its own instance volume
- highest storage performance in AWS
- included in the instance price
- have to attach them at launch time - can't do it afterwards.
- view all instance store volume as ephemeral (temporary) data does not move to new instances, nor faster instances
- D3 = 4.6 gb's throughput
- i3 = 16 gb's seconds - nvme storage
- Exam powerups
    - local on ec2 hosts
    - add only at launch time
    - lost on instance, move, resize, or hardware failure
    - high performance
    - you pay for it anyway - included in instance price
    - temporary

## EC2 Instance STore vs EBS
- Persistence storage = use EBS (avoid instance store)
- Resilience = EBS
- Storage Isolated from instance lifecycle = ebs (attach and reattach)
- Resilience w/ app In-build Replication... it depends
- High performance needs...depends
- Super high performance needs .... instance store
- cost ..instance store (it's often included)
- Cheap = ST1 or SC1
- Throughput..streaming..ST1
- Boot = NOT ST1 OR SC1
- Gp2/3 up to 16k iops per volume
- Io1/2 up to 64k iops (block express 256k iops)
- Raid0 + EBS up to 260k IPS (io1/2-BE/GP2/3)
- More than 260k ips = Instance Store (just keep in mind it's not persistent)
- ![Alt text](/screenshots/InstanceStorevsEBS.jpg?raw=true "Instance store Vs EBS")

## EBS Snapshots
- Efficient way to backup
- snapshots are incremental volume copies ot s3
- new ebs volume = full performance immediately
- snaps restore lazily - fetched gradually
- requested blocks are fetched immediately
- force a read of all data immediately
- FSR (fast snapshot restore) - up to 50 per region
- billing
    - gigabyte - month
    - used not allocated (only bill what you use)
    -

## EBS Snapshot Demo 1 / 2
- set the UUID on the /etc/fstab for the replicated volume
- sudo mount .a
- sudo mount /dev/xvdf /ebstest
- sudo file -s /dev/**drive name**
- sudo mkfs -t xfs /dev/nvme1n1
- sudo mkdir /instancestore

## EBS Encryption
- default no encryption is applied.
- provides at rest encryption for volumes and snapshots
- Exam Powerup
    - Aws accounts can be set to encrypt by default - default CMK or use manually
    - eaches volume uses 1 unique DEK per volume
    - snapshots and future volumes use the same DEK
    - can not change a volume to NOT be encrypted.
    - OS isn't aware of the encryption - no performance loss.
    - if it states in some way that it needs the OS  needs to have the keys and or needs to be encrypted, then you need to perform whole disk encryption
    
## Network Interfaces Instance Ip's and DNS
- In this lesson we deep dive into the Elastic Network Interfaces (ENIs) which can be allocated to EC2 instances - and the DNS, public, private and elastic IPs which can be assigned to those ENIs.
- primary private ip
- 1 or more elastic IP per private ipv4
- Secondary ENI + MAC = Licensing
- multi-homed subnets
- different security groups - multiple interfaces.
- OS never sees the public IPV4. never configure network interface with public IP
- Public = Dynamic / Start/Stop = Change. Or forced migration.
- Static ip = elastic IP
- public dns = private IP in vpc, public IP everywhere else.

## wordpress demo 1/2
- systemctl enable httpd - autostart on system startup
- systemctl enable mariadb - auto start on startup

## Amazon machine Images (AMI)
- AMI's can be used to launch EC2 instances.
- community provided
- marketplace (can include commercial software)
- regional/unique UID e.g ami-0a887e401
- Lifecycle
    1. Launch
    2. Configure
    3. Create Image
    4. Launch
- Exam Powerups
    - AMI's are in One region - in a particular region - can be used to deploy into all AV's
    - AMI Baking - creating an AMI from a configured instance + application
    - AMI can not be edited, launch instance, update configuration and make a new AMI
    - Can be copied between regions (includes it snapshots)
    - Remember permissions default = your account - can make the AMI completely public, or individual aws accounts
    - Will be billed for the EBS snapshots

## AMI Demo 1/2
- configure base image
- shutdown machine
- create ami > image and templates
- create snapshot automatically on the OS drive

## Instance Billing Models
- on-demand
    - instances have an hourly rate
    - billed in seconds or hourly
    - default pricing model
    - no long-term commitments or upfront payments
    - new or uncertain application requirements
    - short term, spiky, unpredictable workloads which can tolerate any disruption
- Spot Instances
    - Spot pricing offers up to 90% off vs on-demand
    - based on spare capacity
    - specify a max price, and if met, instances are terminated.
    - apps which can tolerate failure and continue later
- Reserved Instances
    - up to 75% off on-demand for a commitment
    - 1 or 3 years, all upfront, partial upfront, no upfront.
    - reserved in region or az wich capacity reservation
    - scheduled reservations
    - know steady state usage (email/domain/dns/)
    - lowest cost for app which can handle disruption
    - need reserved capacity

## Instance Status Checks and Auto Recovery
- two default checks
    - system check (power/hardware/network)
    - Instant Status (OS issues, network configuration )
    - can auto recover - re-launch a new host

## Horizontal and Vertical Scaling
- Vertical
    - each resize requires a reboot - disruption
    - larger instances often carry a $ premium
    - there is an upper cap on performance - instance size
    - No application modification required
    - works for ALL applications - even monoliths
- Horizontal Scaling
    - Sessions are critical in your app
    - requires application support or off-host sessions
    - no disruption when scaling
    - no real limits to scaling - other than cost
    - often less expensive - no large instance premium
    - more granular on how you scale
- Exam Power up
    - ![Alt text](/08-EC2-Basics/00_LearningAids/Horizontal_Vertical_scaling.png?raw=true "Horizontal Scaling and Vertical")

## EC2 Instance Metadata
- Data about the instance that can be used or configured about the system/environment
- accessible inside ALL instances: http://169.254.169.254/latest/meta-data/
- Categories information
    - environment
    - networking
    - instance metadata can be used by applications to get IP information
    - authentication
    - user-data
    - not authenticated - authenticated
- Demo
    - curl http://168.254.169.254/latest/meta-data/public-ipv4
    - query tool
    - wget http://s3.amazonaws.com/ec2metadata/ec2-metadata
    - make execute chmod u+x ect-metadata
    - ./ec2-metadata --help

# Containers and ECS
## Intro
- docker image created from scratch or base image.
- dockerfile - used to build docker images.
- Each step creates a file system layer.

## Containers ECS Demo
- review docker make / build commands

## ECS
- Elastic Container Service (ECS)
- Container Definition
    - image and ports to use
    - task definition - security (task role), Containers, resources - what can they access inside aws
    - task role - IAM role which the TASK assumes
    - Service - How many copie, HA, Restarts
- Service Definition

## ECS Cluster Mode Types
- ECS EC2 mode
    - Runs in a VPC which benefits multiple av zones
    - Scheduling and Orchestration - Cluster Manager / Placement Engine
- Fargate Shared Infrastructure
    - No visibility of other customers
    - same task and service definitions
    - allocated resources
    - still have the VPC on your own account - they auto allocate those from the fargate shared environment

## ECS Cluster Mode Types Demo
- EC2 vs ECS (EC2) VS Fargate
    - if you use containers already than use ECS
    - Make sense if you are just wanting to isolate applications
    - small overhead of running the tool
    - Large workload - price conscious - EC2 Mode
        - only if admin overhead is minimized
    - Large workload - overhead conscious - Fargate
    - Small / Burst workloads - Fargate
    - batch / Periodic workload - fargate (pay for what you use)

# Advanced EC2
# Bootstrapping EC2 using user data
- allows EC2 build automation
- user data - accessed via the meta-data ip
- executed only once on launch
- user data is not secure - no passwords or long term credentials
- limited to 16kb in size
- can be modified when instance stopped

## bootstrapping demo
-

## Enhanced Bootstrapping with CFN-INIT
- helper script which is installed on EC2 OS
- works with stack updates.
- listens to the user-data

## Enhanced bootstrapping demo

## EC2 Instance Roles and Profile Advanced Ec2 and Demo
- credentials are inside meta-data
- iam/security credentials/role-name
- temporary secure credentials
- automatically rotate - always valid
- should always be used rather than adding access keys into instance
- Demo
    - create an IAM role
    - s3ReadOnlyAccess
    - attach an IAM role to the instance.

## System Manager Parameter store (SSM) and DEMO
- lets you create configuration and secrets
- String, StringLists, and SecureString
- license codes, database strings, usn/pw's
- plaintext and ciphertext (uses KMS)
- app/lambda/ec2 can have access via IAM to the parameter store
- Demo
    - parameter store is located Under Systems Manager console
    - create parameter

## System and Application Logging on EC2 and DEMO
- CloudWatch is for metrics
- Logs is for logging data..CLoudwatch
- neither nativly capture data inside an instance
- the cloudwatch agent is required
- needs configuration and permissions
- create an IAMRole CloudWatch Logs to the Ec2 instance
- DEMO
    -

## Ec2 Placement Groups
- physically close together or not -
- Cluster - Pack instances close together
    - highest level of performance possible inside of EC2
    - Have to be a part of a single AV zone.
    - Run same physical space (same rack sometimes same host)
    - 10gpbs single stream
    - Exam
        - Can't span AZ
        - Can VPC Peers but impacts performance
        - Requires a supported instance type (not all images work)
        - use the same type of instance (not mandatory) but best practice
        - launch at the same time
        - 10gpbs single stream performance
        - performance, fast speeds, low latency
- Spread - keeps instance separated
    - for max amount of availability and resilience
    - can spread multiple AV zones
    - separate isolated infrastructure racks, own networking, power supply
    - limit 7 instances per AV
    - Exam
        - provides infrastructure isolation- each instance runs from a different rack
        - 7 instances hard limit
        - not supported for dedicated instances or hosts
        - use case: small number of critical instances that need to be kept separated from each other
        - domain controllers
        - file servers
        - it's handled by aws of organization of the spread placement group
- Partition - groups of instances spread apart
    - can be used in multiple AV's
    - max per 7 per region
    - partitions - has its own racks - no sharing between partitions
    - launch as many instances as you want
    - aws can auto decide or you can decide
    - share this information with topology aware information
        - HDFS, Hbase, Cassandra
        - make intelligent data replication decisions
    - you need to administer the partition placement.
    - Exam
        - 7 partitions per AZ
        - Instances can be placed in a specific partition or auto placed
        - partition placement groups are not supported for dedicated hosts
        - great for HDFS, Hbase, Cassandra.

## Dedicated hosts
- dedicated to you entirely
- family e.g a1,c5,m5
- no instance changes you pay for the host
- on demand, and reserved options available
- host hardware has physical sockets and cores
- licensing model comes into play for this (via cpu core ect...)
- A1 - 1 socket - 16 cores
- R5 (nitro host) 2 sockets 48 cores. Use different sizes at one time
- Limitations and Features
    - AMI limits, RHEL, SUSE LInux and Windows AMI's are not supported
    - Amazon RDS instances are not supported
    - Placement groups are not supported for dedicated hosts
    - Hosts can be shared with other ORG accounts...RAM
    - only control the hosts that you create / instances.
    - general solves licensing issues

## Enhanced Networking & EBS Optimized
- USES Single Route I/O Virtualization (SR-IOV) - Nic is virtualization aware
- physical network inside ec2 host is aware of virtualization
- allows for higher I/O and Lower host CPU usage
- More bandwidth faster networking speeds
- dedicated NIC card basically
- available for most ec2 with no charge
- EBS optimized instances
    - its either on or off
    - block storage over the network

# Route 53 (it's always DNS)

## Public Hosted Zones
- dns database (zone file) hosted by r53 (public name servers)
- accessible from public internet and vpcs
- hosted on 4 r53 name servers specific for the zone
- resource records (RR) created within the hosted zone
- externally registered domains can point at R53 Zone
- walking the "dns" tree

## Private Hosted Zone
- associated with VPC's and only accessible in those VPC's
- needs to be associated with the private hosted zone
- split view horizon dns
    - allows ot created a public hosted zone with the same name

## Cname vs ALIAS
- cname maps one name to another name.
- cname can not be used to the TLD record - that requires an alias
- alias record map a name to an aws resource
- make/apex and normal records
    - api gateway, elb, cloudfront, global accelerator and S3

## Routing policies Route 53
- simple routing supports 1 record per name
    - does not support health checks
- each record can have multiple values
- all values are returned in random order

## Health checks and Demo
- health checkers are located globally
- anything accessible over the internet
- every 30 seconds
- tcp/http/https/ and with string matching (layer 7)
- Demo
    -

## Failover Routing && Demo
- multiple records of the same name.
    - primary and secondary
- if the target of the health check is unhealthy, any queries return the secondary record of the same name
- demo
    -

## Multi Value Routing
- many records with the same name
- aims to improve availability by allowing a more active, active approach to DNS.
- ![Alt text](/screenshots/MultiValueRouting.jpg?raw=true "Multi Value Routing")

## Weighted Routing
- Weighted routing lets you associate multiple resources with a single domain name (catagram.io) and choose how much traffic is routed to each resource. This can be useful for a variety of purposes, including load balancing and testing new versions of software.
- can be combined with health checks

## Latency Based routing
- use latency-based routing when optimising for performance and user experience.
- latency-based routing supports one record with the same name in each aws region
- the record returned is the one which offers the lowest estimated latency and is healthy

## Geolocation Routing
- the location of customers and resources are used for routing
- us state, country, continent, or default
- ip check verify the location of the user
- only relevant location records
- ideal for restricting content
    - regional restrictions, language specific content, or load balancing across regional endpoints

## Geo Proximity
- Geo Proximity routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources. You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a bias. A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.
- aims to calculate the distance between a record and a customer
- benefits
    - can define a + or - bias
    - routing is distance based including bias

## interoperability
- This lesson details how Route53 provides Registrar and DNS Hosting features and steps through architectures where it is used for BOTH, or only one of those functions - and how it integrates with other registrars or DNS hosting.
- r53 normally has 2 jobs - domain registrar and domain hosting
- allocates 3 name servers
- creates a zone file
- communicates with the registry of the TLD

# Relational Database Service (RDS)
- Refresher
    - relational (SQL) (RDBMS)
        - structure in and between tables - Schema
        - relationship between tables
    - non-relational (noSQL)
        - no one single thing different models
        - generally a much more relaxed schema
        - relationships handled differently
        - kye-value
            - a key is unique, and has a value - no schema no structure
            - scaleable really fast
            - in memory
        - wide column store
            - partition key
            - DynamoDB - can have a 2nd key
            - unique to that table - groupings of data
        - document database
            - catalogs, user profiles, content management systems
            - whole documents, deep attribute interactions
        - column
            - interact data based on rows
            - online transaction processing (OLTP)
        - column store (redshift)
            - all grouped by the column they are in
            - very inefficient for transactional data
            - great for reporting data and analytics
        - Graph
            - relationships between things are formally defined and stored in the database itself along with the data. they are not calculated each and every time you run a query which makes it great for relationship driven data.
            - social media and HR systems
            - nodes are nouns = objects
            - relationships are known as "edges"
## Acid Vs Base
- both transaction models (to and from)
- CAP theorem - consistency, availability, partition tolerant (choose 2)
- partition tolerance means that the system can be made of multiple network partitions, and the system continues to operate, even if there are a number of dropped messages or errors between these network nodes.
- CAP theorem states that "any database product is only capable of delivery a maximum of two of these different factors"
- ACID = consistency
    - Atomic, Consistent, Isolated, Durable
        - Exam Power up
            - Atomic - ALL or No Components of a transaction Succeeds or Fails
            - Consistent Transactions move the database from one valid state to another - nothing in between is allowed.
            - Isolated - If multiple transactions occur at once, they don't interfere with each other. Each executes as if it's the only one
            - Durable - once committed, transactions are durable. Stored on non-volatile memory, resilient to power outages or crashes
            - RDS (relation) limits scaling
- BASE = Availability
    - Basically Available (BA)
    - Soft state
    - Eventually Consistent
        - Exam Power Up
            - BA read and write operations are available as much as possible but without any consistency guarantees - kinda, maybe
            - base model nosql databases will ensure availability of data by spreading and replicating that data across all of the different nodes of that database.
            - soft state: needs to deal with the data that maybe wasn't written moments ago - if we wait long
            enough, reads form the system will be consistent

## Databases on EC2
- generally one or more ec2 instances
- some instances to run DB's on EC2 (not normally done)
    - Access to the DB instance OS
    - advanced DB option tuning (DBROOT)
    - DB or DB version AWS does not provide
    - vendor demands
    - architecture aws does not provide
- small cost if data is in two AV zones (app in Zone a / DB in Zone B)
- Why you SHOULD NOT do it
    - admin overhead
    - Backup / DR Management
    - EC2 is a Single AZ
    - EC2 is ON or OFF - no serverless - no easy scaling
    - replication - skills, setup time, monitoring and effectiveness
    - performance - aws invest time into optimize and improve.

## RDS Architecture - Relational Database Service
- DBaaS - more accurately described as: DatabaseServer-As-A-Service
- Managed Database Instance 1+ databases
- don't manage the physical hardware or the server os
- or the database system itself
- supports MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL Server
- Implementation
    - cname only accessible
    - db.m5 - db.r5 - db.t3
    - gp2 should be default
    - io1 for higher Iops
    - Magnetic - long term storage use
    - allocated GB/m
    - access is configured via Security group

## RDS Demo
-

## RDS High-Availability (Multi AZ)
- RDS enabled synchronous replication
- rds only the CNAME at the primary instance - cant hit the standby directly
- failover takes 60-120 seconds
- same region only (other AZz in the VPC)
- backups taken from Standby (removes performance impact)
- AZ outage, Primary failure, manual failover, instance type change, and software patching.

## RDS Automatic Backup Snapshot and Restore
- RTO - recovery time objective
    - time between the DR event and full recovery
    - influenced by process, staff, tech and documentation
    - generally lower values cost more
- RPO - recovery point objective
    - time between last backup and the incident
    - amount of maximum data loss
    - influences technical solution and cost
    - generally lower values cost more
- RDS
    - Automatic Backups
        - automatic backups retention are from 0 to 35 days.
    - Manual Snapshots
        - these don't expire
    - Both use AWS managed s3 buckets
    - first snap is full
    - size of consumed data then onward = incremental
    - every 5 mins transaction logs are written to s3
- Examp Powerups
    - Creates a NEW RDS Instance on Restore
    - need to update your new connection string (cname)
    - Snapshots = single point in time, creation time
    - automated = any 5 min point in time
    - the latest snapshot is stored, then the full backup is restored via transaction logs and are replayed to bring the DB to desired point in time
    - restores aren't fast - think about RTO

## RDS Read Replicas
-  a-synchronous means read-replica
- primary first (AZ-B), then sent to ReadReplica (AZ-C)
- you can have 5x direct read-replicas per DB instance in RDS
- Each providing an additional instance of read performance
- read-replicas can have read-replicas but lag starts to be a problem
- Global performance improvements
- availability improvements
    - snapshots and backups improve RPO
    - RTOS are a problem
    - RR's off no. 0 RPO
    - RR's can be promoted quickly - low RTO
    - works on failure only ( can replicate corruption)
- Read only until promoted
- Global availability improvements global resilience

## MultiAZ RDS - snapshots, creating, restoring, failover. DEMO
-

## Amazon RDS Security
- Encryption in transit (ssl/tls) can be mandatory
    - rds supports ebs volume encryption - kms
    - handled by host/ebs
    - aws or customer managed CMK generates data keys
    - data keys used for encryption operations  
    - storage, logs, snapshots, and replicas are encrypted
    - encryption cant be removed.
- RDS MSSQL and RDS oracle support TDE
    - Transparent data encryption (TDE)
    - handled within the db engine
    - RDS oracle supports integration with Cloud HSM
    - IAM Authentication
        - IAM user and EC2 role - creates token with 15 min validity which can be used in place of a db user password

## Aurora RDS
- aurora architecture is very different from RDS
    - uses a cluster
    - single primary instance + 0 or more replicas
    -  no local storage - uses cluster volume
    - faster provisioning and improved availability and performance
- works across a wide range of AV zones -
- shared ssd storage max 128 TIB , 6 replicats az
- replication happens at the storage level
- primary is the only write options - the replicas are able to read
- max 15 replicas
- All SSD based - high IOPS, low latency
- storage is based on what you consumed
- billed on consumption
- High water mark - billed for the MOST used.
- Storage which is freed up can be reused
- to save costs you would create a new cluster and migrate.
- cluster endpoint points to the primary
- reader endpoint will point to the replicas, load balance - for READs
- Costs
    - no free-tier
    - compute - hourly charge per second 10 min minimum
    - storage - gb month consumed IO cost per request
    - 100% db size in backups are included
- backups in aurora work in the same way as rds
- restores create a new cluster
- backtrack can be used which allow in-place rewinds to previous point in time
- fast clone makes a new database much faster than copying all the data copy-on-write

## Aurora RDS Demo
- you can migrate from a RDS db to Aurora via a snapshot
- does not include file system backups on EC2: IE uploaded files to wordpress /upload folder. It's only the metadata surrounding the application.
- will need to enable network file shares to host those static assets

## Aurora Serverless
- overhead of managing individual database instances.
- refer to it as aurora provisioned vs aurora serverless
- ACU's aurora capacity units - scalable
- Min and Max ACU - cluster adjusts based on load
- can go to 0 and be paused
- consumption billing per second basis
- same resilience as aurora
- picking the minimum and max acu for your cost needs - aws manages the hardware
- use cases
    - infrequently used applications
    - new applications (autoscale based on the incoming workload)
    - variable workloads (up and down per customer volume IE: sales websites ecommerce)
    - unpredictable workloads
    - development and test databases
        - can be paused and you are only charged via storage
    - Multi-tenant applications

## migrating to aurora Serverless DEMO
-

## Aurora Global Database
- two or more regions
- 2ndary region: up to 16 read only replicas
- ~1 second replication
- when to use global database
    - Cross Region DR and BC
    - Make the secondary clusters the primary for read-write operations
    - Global Read scaling - low latency performance improvements
    - international customer
    - replication happens at the storage layer
    - currently max 5 secondary regions

## Multi-Master Writes
- Default aurora mode is single-master
- Multi-master - all instances are R/W / capable of doing it


## Database Migration Service
- DMS - managed database migration service
- runs using replication instance
- source and destination endpoints point at the physical source and target databases
- once endpoint MUST be on AWS
- Common DB support
    - MySQL, Aurora, Microsoft SQL, MariaDB, MongoDB, PostgreSQL, Oracle, Azure SQL
- Schema conversion tool SCT can assist with Schema conversion

# Network Storage

## EFS Architecture and DEMO
- The Elastic File System (EFS) is an AWS managed implementation of NFS which allows for the creation of shared 'file systems' which can be mounted within multi EC2 instances.
- EFS is an implementation of NSFv4
- private service via mount targets inside a vpc
- can be access from on-premises - vpn
- Linux Only Instances
- General Purpose and Max I/O Performance
- Bursting and Provisioned throughput modes
- Storage Class - Standard and Infrequent Access Classes
- must install the efs amazon tools for mounting
- add it to the fstab so that it mounts on boot

# HA and Scaling

## Load Balancing Fundamentals
- Exam Power Up
    - clients connect to the load balancer listener
    - LB connects on your behalf of 1+ targets
    - 2 connections, listener and backend
    - client abstracted from individual servers
    - used for high-availability, fault-tolerance and scaling

# Application Load Balancing (ALB)
- CLB - Classic/Legacy
- Application LB
- Network Load balancer
- ALB
    - layer-7 LB - understands Http/s
    - scalable and highly available
    - Internet-Facing or Internal
    - Listens on the outside -> sends to targets (groups)
    - Bill - Hourly rate and LCU Rate (capacity)
    - Cross-zone Load balancing
    - target groups based on paths or host based off dns
    - exam power group
        - targets - target groups which are addressed via rules
        - Support, EC2, ECS, EKS, Lambda, HTTPS, HTTP/2 and web sockets
        - ALB can use SNI, multiple SSL certs - host based rules

## Launch Configuration and Templates
- allow you to define configuration of an ec2 instance
- ami, instance type, storage and key pair
- networking and security groups
- userdata & IAM role
- both are not editable - defined once LT has versions
- LT provide newer features - including T2/T3
- lt provide newer features including t2/t3 unlimited placement groups, capacity reservations, elastic graphics
- LC's are not editable no versioning
- launch templates can be used to save time when provisioning ec2 instances from the console ui/cli

## Auto Scaling groups ASG
- automatic scaling and self healing for ec2
- uses launch templates or configurations
- has a minimum, desired and max size
- provision or terminate instances to keep at desired level
- there is an attempt when autoscaling, to scale out to all AV's accordingly - max 3 = all three AV zones
- Manual
- scheduled scaling - time based - sales
- dynamic scaling
    - simple - cpu above 50% + 1 / below -1
    - some need the cloud watch agent installed.
    - stepped scaling - bigger +/- based on difference
    - target tracking - desired aggregate CPU = 40% asg handle it
- cooldown period helps with cost
- self-healing - restarts / re-provisions ec2 instance
- Final points
    - auto scaling groups are free
    - only billed via the resources created
    - use cool downs to avoid rapid scaling
    - think about more smaller instances - granularity
    - use with ALB's for elasticity - abstraction
    - ASG - defines WHEN and WHERE, LT defines WHAT

## NLB Network Load balancer
- NLB's are layer 4 only understand TCP / UDP
- can't understand HTTP/s but are faster ~ ms vs 400 ms for ALB
- test - anything about performance/ faster/response time select NLB
- rapid scaling millions of requests per second
- 1 interface with static IP per az / elastic IP's
- can do SSL pass through
- can load balancer non http/s applications - doesn't care about anything above tcp/udp

## SSL offload and session stickiness
- bridging - listener is configured for https, connection is terminated on the ELB & needs a certificate
    - ELB initiates a new ssl connection to backend instances - instances need ssl certificates and the coptue required for cryptographic operations
- pass-through
    - each instances needs to have the appropriate ssl cert installed
    - no ssl on the NLB
    - listener is configured for TCP. no encryption or decryption happens on the NLB. COnnection is passed to the backend instance
- offload
    - clients connect to the ELB that needs the ssl
    - ec2 instances don't need ssl
- Connection Stickiness
    - generates a cookie which locks the device to a single backend
    - with no stickiness, connections are distributed across all in-service backend instances. unless application handles user state this could cause user logoffs and shopping cart losses

## Gateway load balancers GWLB
- help you run and scale 3rd party appliances
- like firewalls, intrusion detection and prevention systems
- inbound and outbound traffic (transparent inspection and protection)
- GWLB endpoints traffic enters/leaves via these endpoints
- the GWLB balances across multiple backend appliances
- traffic and metadata is tunneled using GENEVE protocol

# SERVERLESS AND APPLICATION SERVICES

## Architecture Evolution Part 1 / 2- monolithic and Tiered
- Event Driven Architecture
- event producers
    - no constant running or waiting for things
    - producers generate events when something happens
    - events are delivered to consumers via event router
    - actions are taken the system returns to waiting
    - mature event driven only consumes resources while handling events (serverless)
- monolithic
    - fails together
    - scales together
    - bills together
    - one of the least cost effective way
- Queue - messages can be received or polled
    - FIFO First in First outl
- worker fleet architecture - aka Youtube.
    - upload videos for processing
    - goes into a queue
- Microservice Architecture
    - do individual things well

## AWS Lambda
- Function as a Service FaaS
- Event-driven invocation (execution)
- piece of code in one language
- only billed for the duration of your function running
- make it really small but really good at doing 'one' thing
- should never have stored - not persistent
- stateless
- load data into a lambda runtime environment via aws services dynamoDB and also output data
- Exam
    - 15 min execution limit
    - new runtime environment every execution - no persistence
    - execution role provides permissions
    - load data from other services (eg S3)
    - store data TO other services (sg / dynamo)
    - frie tier 1M free requests per month - 400k DB - seconds of compute time per month

## CloudWatch Events and EventBridge
- key concepts
    - if x happens or at y times do z
    - EventBridge is CloudWatch Events V2
    - a default event bus for the account
    - in cloudwatch events this is only bus (implicit)
    - EventBridge can have additional event busses
    - rules match incoming events (or schedules)
    - routes the events to 1+ targets E.G. lambda
- event pattern rule - schedule rule -> Target

## CloudWatch EventBridge DEMO Part 1 and 2
-

## API Gateway
- Key Concepts
- Create, Publish, Monitor and Secure APIs as a service
- Billed based on number of API calls, Data Transfer and additional performance features such as caching
- can be used directly for serverless architecture
- or during architecture evolution

## Serverless Architecture
- serverless isn't one single thing
-  manage few if any servers - low overhead
- small and specialized functions
- Stateless and Ephemeral environments - duration billing
- Event-driven..consumption only when being used.
- FaaS is used where possible for compute functionality
- Managed services are used where possible

## Simple Notification Service (SNS)
- public aws service - network connectivity endpoint
- pub/sub
- coordinates sending and delivery of messages
- messages are 256k payloads
- sns topics are the base entity of sns - permissions and configuration
- a publisher sends messages to a TOPIC
- topics have subscribers which receive messages
- e.g. http(s), email-json, sql, mobile push, sms messages & lambda
- ![Alt text](/15-Serverless-and-AppServices/00_LearningAids/sns.png?raw=true "SNS Diag")

- Offers Delivery status
- delivery retries - reliable delivery
- HA and scalable (region)
- can include SSE server side encryption
- can be cross-account via topic policy

## Step Functions - Long running serverless workflows
- Some limitations with Lambda
    - Lambda is FaaS
    - 15 min max execution
    - can be chained together
    - gets messy at scale
    - runtime environments are stateless
- State machines
    - serverless workflow START - States - END
    - States are *things* inside this workflow
    - maximum duration is 1 year
    - standard workflow and express workflow
    - Generally used for backend programming
    - Amazon States languages - json template
- What are states?
    - SUCCEED and FAIL
    - WAIT
    - CHOICE  - take a different path based on input
    - PARALLEL - parallel branches inside the state machine
    - MAP - accepts a list of things, or order - with certain set of rules
    - TASK (lambda, batch, DynamoDB, ECS, SNS, SQS, Glue, SageMaker, EMR, Step Functions)

## pet-Cuddle-o-tron Serverless Application Part 1-2-3-4-5-6

## Simple Queue Service SQS
- Managed message queues, public, fully managed, highly available - standard or FIFO
- message up to 256kb in size - link to large data
- received messages are hidden (visibilityTimeout)
- then either reappear (retry) or are explicitly deleted.
- dead-letter queues can be used for problem messages
- ASG worker Pool
    - Auto Scaling Group - scaled out when queue length long
    - scaled in when Queue length Short
- ASG Web Pool
    - scaled out when CPU high
    - scaled with CPU LOW
- S3 buckets - Exam Question
    - s3 generates one event then you can take that and with multiple subscribers multiple sqs queues - then that messages added to each of those queues
    - FAN OUT architecture is important to remember for the exam
- Standard = at-least-once,
- FIFO = exactly once - guaranteed
    - performance 3000 messages per second with batching or up to 300 messages per second without
    - billed based on requests
    - 1 request = 1- 10 messages up to 256kb total
    - Short (immediate) vs Long (waitTimeSeconds) polling
    - Encryption at Rest KSM and in transit
    - Queue Policy

## Kinesis and Kinesis Firehose
- is a scalable streaming service
- producers send data into kinesis stream
- streams can scale from low to near infinite data rates
- public service & highly available by design
- stream store a 24-hour moving window of data
- Kinesis Stream provides shards
    - 1 mb ingestion
    - 2 mb consumption
- Kinesis data record (1mb) stored across the shards
- Kinesis data Firehose to send data to other services ie: s3
- SQS vs Kinesis
    - Is that exam question about the ingestion of data or is it about worker pools decoupling?
    - or does it mention synchronous communication?
    - if it's about the ingestion of data or the ingestion of a data at scale, "the large throughput or large numbers of devices" it's likely to be kinesis.
    kinesis designed for large scale ingestion
    - analytics, monitoring, app clicks
- If it's about worker pools, decoupling, or asynchronous communication assume first that its SQS and only change your mind if you have a strong reason to do so.
    - SQL generally has one thing or one group of things sending messages to the queue.
    - no persistence

## Amazon Cognito
- Cognito means
    - User pools
        - sign-in and get a JSON web Token (JWT)
        - Sign up and Sign in services - user directory management and profiles (MFA)
    - Identity Pools
        - allow you to offer access to Temporary AWS Credentials
        - Unauthenticated Identities - Guest Users
        - Federated Identities - SWQP - Google, Facebook, Twitter, SAML 2.0 and user pool for short term aws credentials to access AWS Resources



# Global COntent Delivery and Optimization

## CloudFront Architecture Basics 
- Origin - the source location of your content
- Distribution - the configurion unit of cloudfront
- Edge Location - Local infrastructure whic hosts a cache of your data
- Regional Edge Cache - larger version of an edge location. provides another layer of cache
- S3 buckets accessed configuration by
    - OAI & Bucket Policies

## Aws Certificate Manager
- data is ecnrypted in-transit
- certificates provide identity
- signed by a trusted authority
- create, renew, deploy certificates with acm
- Supported AWS Services ONLY (e.g. CloudFront and ALB's Not EC2)

## Securing CF and S3 using OAI (cloud front)
- Origin Access Identity (OAI)
- Associate the OAI to the CF/S3 orgin / Bucket Policy / Explicit allow for the OAI

## OAI Demo


## Cloudfront Lambda@Edge
- You can run lightweight lambda at edge locations
- adjust data between the viewer & origin
- Curretnly supports nodejs and python
- run in the aws public space (NOT VCP)
- Layers are not supported
- Different limnits vs normal lamnda functions
- Couple of examples
    - A/B Testing - viewer request function
    - Migration between S3 origins - origin request
    - Different objects based on device - origin request
    - Content by Country - Origin Request
    - review https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-examples.html#lambda-examples-redirecting-examples

## Global Accelerator 
- Cloud Front vs. Global Accelerator
    - cloudfront only works on http/https cache
    - GA - 2x anycast IP addresses 
    - **Anycast IP's** allow a single IP to be used in multiple locations. Routing moves traffic to closest location
    - from the edge data transits globally accross the aws backbone network. less hops directly under aws control, better performance
    - GA moves the AWS network closer to the client via location
    - GA is a network product, works on TCP and UDP
    - caching = Cloud Front
    - TCP/UDP = Global Accelerator
    - GA does not cache anything

# Advanced VPC Networking

## VPC Flow Logs
- Capture packet metadata..not packet contents 
- applied to a vpc, subnet or all network interface directly 
- subnet - interfaces in that subnet
- interface directly
- VPC flow logs are not realtime
- logs can be sent to s3 or cloudwatch logs. 
- if you see two log entries one which accepts something and one which rejects something, then generally that can be an interaciton between security groups and network ACL's
- they dont log all traffic

## Egress - only Internet Gateway
- internet gateway which only allows connections to be initiated from inside a VPC to outside. 
- NAT allows private IP's to access public networks
- without allowing externally initiated connections (IN)
- With IPV6 all IP's are public
- Egress-only is outbound-only for IPV6
- no inbound connections, only outgoing

## VPC Endpoint Gateway (Gateway Endpoint)
- Gateway Endpoints
    - provide private access to S3 and DynamoDB - allow a private only resource VPC to access S3 and DynamoDB
    - Prefix List added to route table => Gateway Endpoint
    - Highly Available (HA) across all AZ's in a region by default
    - Endpoint Policy is used to control what it can access
    - grand to certain S3 buckets, with policies 
    - cant access cross-region - same region only 
    - Example: private vpc that want access to S3/Dynamo
    - Prevent Leaky Buckets - S3 buckets can be set to private only by allowing access ONLY from a gateway endpoint

## Interface Endpoints
- Provide private access to AWS public services
- anything NOT s3 and DynamoDB
- crucial difference - Added to specific subnets - an ENI - NOT HA
- for HA .. add one endpoint, to one subnet, per AZ used in the VPC
- Can use security groups to control access to that endpoint (cant do this with gateway endpoints)
- TCP and IPv4 ONLY
- Uses PrivateLink, product that allows external services to be injected into your VPC, either from AWS or from third parties.
- Endpoints provides a new service endpoint DNS
- Endpoint Regional DNS name - one single dns name that works whatever AZ you're usint to access the interface endpoint
- Each AZ gets a Zonal DNS which resolves to that one specific interface in that one specific AV.
- PrivateDNS overrides the default DNS for services


## VPC Endpoints Demos 1-3 - Review
- Accessing S3 using gateway
- Using SNS from private VPC using Interface Endpoints
- Implimenting an Egress Only Internet Gateway

## VPC Peering
- VPC peering is a software define and logical networking connection between two VPC's
- They can be created between VPCs in the same or different accounts and the same or different regions.
- Direct encrypted network link between TWO vpcs (no more than two)
- (optional) public hostnames resolve to private IP's
- VPC peering does not support transitive peering
- Routing configuration is needed, SG's and NACLs can filter
- cant have overlapping CIDR ranges

## VPC Demo - review. 

# Hybrid Environments and Migration

## Border Gateway Protocol 101 
- Autonomous System (AS) - Routers contolled by one entity a networking in BGP
- ASN (autonomous sytem numbers) are unique and allocated by IANA (0-65535), 64512 - 65534
- BGP operates over tcp/179 
- not automatic - peering is manually configured
- BGP is path-vector protocol it exchanges the best path to a destination between peers ... the pat is called aspath
- iBGP - internal eBGP - External
- BGP exchanges the shortest ASPATH between peers. 

## AWS Site-to-Site VPN 
- logical connect between a VPC and on-premis network encrypted using IPSec, running over the public internet
- Full HA - if you design and implement it correctly. 
- Quick to provision ... less than an hour
- Virtual Private Gateway (VGW)
- Customer Gateway (CGW)
- VPN connection bwetween the VGW and CGW
- Static VPN uses static routes \ uses IPSEC
- Dynamic VPN - BGP is configured on both the customer and AWS side USING ASN. Networks are exchanged via BGP. Multiple VPN connections provide HA and traffic distribution
- Considerations
    - Speed Limitations ~ 1.25 GBPS
    - Latency Considerations - inconsistent, public internet
    - Cost - AWS Hourly cost, GB out cost, data cap (on premises)
    - Speed of setup - hours ... all software configuration 
    - can be used as a backup for direct connect
    - can be used with direct connect

## Demo VPC and on prem VPN 1 and 2

## Direct Connect
- a 1 gbps or 10gbps network port into aws
- at a DX (1000-Base-LX or 10GBASE-LR)
    - Uses single mode fiber optics
    - has no encryption by default
- conceptionally single fiber optic cable - connected to your buisness premis
- multiple virtual interfaces (VIFS) over one DX
- Private VIF (VPC) & PUblic VIF (Public Zone Services)
- can take weeks or months for the physical cable to be installed into your equipment 
- Exam
    - Takes much longer to provision vs VPN
    - DX Port provisioning is quick ... the cross-connect takes longer
    - extension to premises can take weeks/months
    - Use VPN first.. then replace with DX (or leave as a backup)
    - Faster 40 GBPS with aggregation with Direct Connect
    - Low consistent latency, doesnt use business bandwidth
    - NO BUILT IN ENCRYPTION

## Direct Connect Resilience and HA
- aws regions have multiple DX locations - 
- Direct Connect Locations - Customer Premises
    - receive a port from the DX Router
- AWS Region between Direct Connect Location are always redundant
- Exam
    - Physical technology
    - will need to build HA into the solution on the DX location and Customer Premiseses 

## AWS Transit Gateway TGW
- Network Transit Hub to connect VPCs to on premises networks
- Significantly reduces network complexity
- single network object - HA and Scaleable
- Attachment to other network types
- works with VPC, Site-to-Site VPN & Direct Connect Gateway
- saves complexity by reducing each VPC having a direct site-to-site to the customer gateway device
- we can also peer directly to other transit gateway's 
- you can also use direct connect with transit gateway
- Exam powerup
    - Supports transitive routing
    - can be used to create global networks
    - share between accounts using aws RAM
    - peer with different regions .. soame or cross account
    - less complexity vs w/o TGW

## TGW Demo 1 and 2
- 

## Directory Service
- Stores objects, Users, Groups, Comptuers, Servers, File Shares) with a structure 
- multiple tress can be grouped into a forest 
- Commonly used in windows environments
- Usn/Pw's
- AWS managed implementation
- Runs within a VPC
- provides HA deploy into multiple AZ's
- Some AWS services need a directory; EG Amazon Workspaces
- can act as a proxy back to on premis
- can be isolated
- Architecture
    - Simple AD mode - cheapest
        - opensource directory thats based on Samba 4
        - integrates with aws services - ect2 instances, SimpleAD and worksapces can use it for login management 
        - 500-5,0000
        - designed to be used in isolation 
    - Managed Microsoft AD mode
        - on-premises and aws
        - can create a trust with vpn between your aem and onprem directory 
        - Microsoft AD - on premis and aws, they mean managed microsoft AD
    - AD Connector
        - its only a proxy, to integrate with AWS services- aka amazon workspaces. 
        - so if the VPN goes down, so will your authentication services
- picking between modes
    - Simple AD - the default. simple requirments. a directory in AWS
    - Microsoft AD- applications in AWS which need MS AD DS, or you need to trust AD DS
    - AD connector - use aws services which need a directory without storing any directory info in the cloud...proxy to your on-premises directory. 

## AWS DataSync
- Data Transfer Service to and from aws
- Migrations, Data Processing Transfers, Archival/Cost Effective Storage or DR/BC
- designed to work at huge scale
- 10 gigabits per second of data transfer
- keeps metadata eg permissions/timestamps
- built in data validation
- Scalable - 10gbps per agent ~100TB per day
- Bandwidth Limiters (avoid link saturation)
- Incremental and Scheduled Transfer options
- Compression and Encryption
- Automatic Recovery from transit errors
- AWS Service integraiton - S3, EFS, FSx
- Pay as you use service... per GB cost for data moved.
- Arch
    - DataSync agent runs on a virtualisation platform such as VMWare and communications with the AWS dataSync Endpoint
    - NFS/SMB SAN/NAS
    - Schedules can be set to ensure transfer of data occurs during or avoding specific time periods 
    - TO or From AWS S3, EFS, FSx, NFS, SMB
    - Task - a job within datasync defines what is being syced, how quickly, from where and to where
    - agent - software used to read or write to on premises data stores using NFS or SMB
    - Location - every task ahs two locations; from/to (NFS/SMB/EFS Amazon FSx)


## FSx for Windows File Serevers
- fully managed native windows file servers (file shares)
- Designed for Integration with windows environments
- integrates with directory service or self-managed AD
- HA system / Single or Multi-AZ within a VPC
- On-demand and Scheduled Backups
- Accessible using VPC, Peering, VPN, Direct Connect 
- native windows file system, supports de-duplication, distrubuted file system DFS, KMS at rest encryption and enforced encryption in-transit
- Performance
    - 8mb/s 2gb's, 100k IOPS <1ms latency
- Key Features
    - VSS - User-Driven Restores
    - Native File System Accessible over SMB
    - Windows Permission Model
    - Supports DFS .. scale-out file share structure 
    - Managed - no file server admin
    - Integrates with DS and your own directory

## FSx for Lustre
- Managed Lustre - Designed for HPC - Linux (Clients POSIX)
- Machine Learning, Big Data, Financial Modelling
- 100s GB/s throughput & Sub millisecond latency 
- Deployment types - Persistent or Scratch
- Scratch - Highly optimised for short term no replication and fast
- persistent - longer term, ha **in one az**, self-healing
- Accessible over VPN or Direct Connect
- Arch
    - Data is 'lazy loaded' from S3 (S3 linked repository) into the file system as its needed
    - Luster does "data"
- Lustre works...
    - Metadata stored on Metadata Targets (MDTs)
    - Objects are stored on called object storage targets (OSTs)
    - Baseline performance based on size
    - Size - min 1.2Tib then increments 2.4 TIB
    - for Scratch - Base 200MB's per TiB of storage
    - persistent offers 50mb's, 100mb/s and 200mbs per TiB of storage
    - Burst up to 1300 MB's per TiB (Credit System)
- Arch Cont 
    - FSX uses a client managed VCP
    - connects via ENI (Elastic network Interface)
    - Scratch is designed for pure performance 
    - Short term or temp workloads
    - no ha ... no replication 
    - larger file systems means more servers, more disks, and more chance of failure
    - persistent has replication within one AZ only
    - auto-heals when hardware failure occurs
    - you can backup to s3 with BOTH! (manual or automatic 0-35 day retention)

## Storage Gateway
- Hybrid Storage Virtual Applicane (on-premises*)
- extension of file and volume storage into AWS
- Volume Storage backups into AWS
- Tape backups into AWS
- 3 modes
    - Tape Gateway (VTL) Mode 
        - stores virtual tapes on S3 and Glacier 
    - File mode - SMB or NFS
        - Storage backed by S3 objects 
    - Volume Mode (Gateway Cache/Stores) - isci
        - Block storage backed by S3 and EBS Snapshots
- File Gateway 
    - SMB Sahres can integrate with AD for File authorization 
    - Lifecycle polices can automatically control storage classes
    - Files are stored ot shares using NFS or SMB
    - mapped directly 1:1 as S3 objects
    - Use file mode either if you need additional capacity or if you want to begin decommissioning on-premises storage infrastrucuture.
- Tape Gateway
    - connects to the media changer / tape drive over iSCSI
    - https public endpoint to S3, anything archived gets moved into VTS in Glacier
    - Virtual tape 100 Gib => 1 PB (peta byte)
- Volume Gateway (Stored)
    - Can create up to 32 16TB per volume
    - Primary data is stored on Premises
    - backup data is asynchronously replicated to AWS
    - https public endpoint EBS snapshots
    - works great for DR and Migrations
- Volume Gateway (cached)
    - Cache moded is designed  for extension into AWS when your capacity is limited or when you are looking to decommission your existing infrastructure. 
    - volumes are made available via iSCSI for network based servers to access single connection per volume
    - Primary data is stored in AWS. Data which is access frequently is cached locally, ideal for extending storage into AWS
    - Primariy data is stored on a S3 backend volume (AWS managed bucket) snapshots are stored as Stadards Elastic block storage
    - 1PB tocal capacity - 32TB per volume, 32 volumes Max

## Snowball, Snowball Edge, and Snomobile
- Key Concepts
    - move large amounts of data IN and OUT of aws. 
    - when and where you need to use the products
    - Physical storage suitecase or truck
    - ordered from AWS Empty, Load Up, Return
    - Ordered from AWS with data, empty & return
    - For the exam which to use
- Physical Process
    - order a device and has KSM local at rest encryption
    - 50tb to 80 TB capacity 
    - 1 Gbps or 10gbps network
    - 10 TB to 10 PD ecomincal range (multiple devices)
    - only storage
- Snowball Edge
    - both storage and compute
    - Larger capacity vs. snowball
    - 10gbps 10/25 (SFP) 45/50/100 GBPS (QSFP+)
    - Storage Optmized (with EC2) - 80 TB, 24 vCPU, 32 Gib Ram, 1 TB SSD
    - Compute Optimized - 100 TB + 7.68 NVME, 52vCPU and 208GIB Ram
    - Compute Optimized with GPU as well (modeling, sci analysis)
- Snowball Edge vs Snowball
    - Snowball is for storage only
    - Edge is for compute, or if you need faster networking 
- Snowmobile 
    - Portable DC within a shipping container on a truck
    - Literally a truck in a shipping crate
    - Ideal for single location when 10 PB is required
    - can store up to 100 PB per snomobile
    - Expect into data center power and network
    - not economical if you have MULTIPLE sites

## AWS Directory Service

# Security, Deployoments and Operations 

## AWS Secrets Manager 
- It does share functionality with paramater store
- designed for secretes (passwords, api keys)
- usable via console, cli, api, or SDK's 
- supports automatic rotation this uses lambda
- directly integrates with some AWS products (RDS)
- Secrets are encrypted using KMS
- Secretes, Key Rotation, RDS, = almost certain to be using Secrets manager 

## AWS Shield and Web application Firewall WAF
- Shield provides aws resources with DDoS protection 
- Shield Standard - free - with Route53 and CloudFront
    - layer 3 and layer 4 ddos attacks
- Shield Advanced - $3000 per month
    - EC2, ELB, CloudFront, Global accelerator and R53
    - DDoS Response Team and Financial Insurance  
- WAF
    - Layer 7 (http/s) Firewall
    - TCP, UDP, 
    - SQL Injections, Cross-site scripoting, Geo blocks, Rate awareness
    - webacl - web access control list integrated with ALB, API Gateway and CloudFront
    - Rules are added to a webacl and evaluated when traffic arrives
- works well when you use both services together. 
- Terms: DDoS with shield
- Layer 7 filtering, http filtering, https filtering, with WAF

## Cloud HSM
- with KMS - aws manage.. shared but separated 
- hardware security module - HSM
- you can run your HSM on premis 
- True single tenant hardare security module
- aws provisioned fully customer managed 
- HSM **FIPS 140-2 Level 3 (KSM is L2 overall, some L3)**
- access it with industy standard API's
    - **PKCS#11** Java Cryptography Extensions **JCE** Microsoft **CryptoNG CNG** 
    - KMS can use CLoudHSM as a custom key store, CLoudHSM Integration KMS
- HA need multiple HSM's - create a cluster one in each AV and VPC
    - get an elastic network interface
- aws provision hsm but have no access to keys
- AWS CloudHSM VPC, managed by AWS not the customer
- Points / Exam / Use Cases
    - no native integration between cloud hsm and aws products
    - Offload the SSL/TLS processing for web servers
    - Enable Transparent Data Encryption (TDE) for Oracle Databases
    - Can be used to Protect the private keys for an issuing Certificate Authority
    - Hardware security model
    - anything that does require AWS integration DO not use HSM
    - HSM **FIPS 140-2 Level 3 (KSM is L2 overall, some L3)**

## AWS Config
- Two main jobs 
    - record configuration changes over time on resources
    - Auditing of changes, complicance with standards
    - does not prevent changes happening...no protection
    - Regional Service ... Supports cross-region and account aggregation
    - Changes can generate SNS notifications and near realtime events via EventBridge & Lamdba 
    - can apply fixes to remidate any issues via **CONFIG RULES**

## Amazon Macie
- Data security and data privacy Service
- Discover, Monitor , and Protect Data ... Stored in S3 Buckets
- Automated discovery of PII, PHI, Finance
- Managed **Data Identifiers** and Built-In Machine Learning Patterns
- Can create custom data - proprietary regex based. 
- Macie create discovery jobs
- Can integrate with Security hub and pass notifications to Event Bridge
- Multi Account Architecture 

# NOSQL Databases & DynamoDB

## DynamoDB - Architecture 
- DynamoDB is a NoSQL fully managed Database-as-a-Service (DBaaS) product available within AWS.
- Key/Value & Document
- No Self-managed servers or infrastructure 
- Manual/Automatic provisioned performance In/Out or On-Demand
- Highly Resilient .. accross AZ's and optional global
- replicated accross multiple storage nodes automaically 
- stored on SSD, backups, point-intime recovery, data encrypted at rest
- event-driven integraiton .. do things when data changes
- Database TABLE as a Service
- Arch
    - table is a grouping of items with the same primary key
    - Capacity means speed in Dynamo Db
    - WCU = 1kb per second (writes capacity unit)
    - RCU - 4 kb per second per table (read capacity unit)
- backups
    - on-demand backups - retained until manually removed
    - same or cross region
    - point in time recovery
        - not enabled by default
        - continous record of changes allows replay to any point in the window
- Exam
    - NoSQL preference DynamoDB in the exam
    - Relational Data .. generally not DynamoDB
    - Key/Value.. preference DynamoDB
    - Access via console, CLI api 'no sql'
    - Billed based on RCU/WCU, Storage and features

## DynamoDB Operations, Consistency and Performance
- two modes
    - on-demand - unknown,m unpredictable, low admin
    - on demand -price per misslion R or W units
    - Provisioned RCU and WCU set on per table basis
    - every operation consumes at least 1 RCU/WCU
    - 1 rcu is 1 x 4KB read operation read per second
- Query 
    - partition key value
    - Query accepts a single PK value and optionally a SK or range. Capacity consumed is the size of all returned items. Futher filtering discards data - capacity is still consumed. 
    - Can only query on PCK or PK and SK
- Scan
    - scan moves through the table consuming the capacity of every item. you have complete control on what data is selected, any attributes can bse used and any filters applied but scan consumes capacity for every ITEM scanned through. 
- Consistensy modes different consistency modes for read operations
    - Eventually consistent - scales better
    - Strongly / Immediately Consistent - more costly to achieve
- WCU Calculation
    - If you need to store 10 items per second 2.5k averge size per ITEM
    - WCU per item - Round Up (Item size / 1KB ) (3)
    - multiple that by average number per second (30) = WCU Required (30)
- RCU CALCULATION
    - 10 ITEMS PER SECOND 2.5K AVERAGE SIZE
    - Cacluate RCU per item = Round up (item Size / 4Kb)(1)
    - multiply by average read ops per second (10)
    - = Strongly Consistent RCU required (10)

## DynamoDB Streams and Lamnda Triggers
- Time ordered list of Itme Changes in a table
- 24-Hour rolling window
- enabled on a per table basis
- Records inserts, Updates, and Deletes 
- Different view types influence what is in the stream
- Serverless way
    - Trigger concepts
    - ITEM changes generate an event
    - that event contains the data which changed
    - a action is taken using that data
    - aws = streams + lambda
    - Reporting & Analytics 

## DynamoDB Indexes (review)
- Primary KEY (PK) Secondary Key (SK)
- Query is the most efficient operation in DDB
- Query can only work on 1 PK value at a time
- Indexes are alternative views on table data
- Different SK (LSI) or Different PK and SK (GSI)
- some or all attributes (projection)
    - Local secondary Indexes
    - Alternative view for a table
    - MUST be created with table
    - 5 LSI's per base table
    - Shares the RCU and WCU with the table
    - Attibutes - All, keys_only & Include

## Dynamo DB Global Tables 
- Global tables provides multi-master cross region replication
- Tables are created in multiple regions and added ot the same global table
- last writer wins is used for conflit resolution 
- Read and writes can occur to any region
- sub second replication between regions
- Global HA and Global DR/BC

## DynamoDB Accelerator (DAX)
- one set of API calls using one SDK
- appljicaiton uses dax sk and makes a single call for the data which is returened by dax, dax returns the data or makes the call for Dynamo
- designed ot be deployed into multiple AV zones in the VPC
- primary node, (read/write) then replicates out to the other AZ's
- Two caches
    - Item cache hodles results (batch)GetItem
    - query cache holds data based on query/scan paramaters
    - in-memory cache - scaling. much faster reads, reduced costs
    - scale up and scale out (bigger or more)
    - Supports write-through
    - Dax Deployed with an VPC

## Amazon Athena
- Serverless Interactive Querying Servbice
- Ad-hoc queries on data - pay only data consumed. 
- 
Schema-on-read table-like translation
- orginal data never changed - remains on s3
- Schema translates data => relatioal-like when read
- output can be sent to other services
- Arch
    - starts source data on S3 - read only
    - XML/JSON/CSV/ARVO/PARQUET/CloudTrail/VPC-FLowLogs
    - inside the product you create the scema
    - then you define the tables
    - athena you are defining a way to get the orginal data and present it in the way that you want to be able ot run queries against it
    -  Examp - questions which talk about data being stored inside s3, and if the data is structured, or semi-structured or unstructured and you need to perform ad hoc queries where you only charged for performing those queries, then athena should be the product. 

## ElastiCache
- In-memory database .. high performance requirements
- Manged redis or memcached as a service
- can be used to cache data for read havy workloads with low latency requirements
- reduces database workloads (expensive)
- cost effective, help reduce reads saving money
- can be used to store session data (stateless servers)
- **Requires application code changes to use elasticache** 
- if data inst in the cache, then it needs to check the underlying database and applicaiton need ot be able to write data and understand acache invalidation. 
- two different engines
    - both
        - sub millisecond access
    - Memcached - 
        - simple data structures
        - no replication
        - multiple nodes (sharding)
        - no backups (no persistance)
        - Multi-threaded
    - redis
        - advanced structures
        - lists/sublists
        - stores order of data / improves performance
        - replication to multi-az - scale reads
        - supports backups and restores
        - transactions - multiple operations as one

## Redshift Architecture 
- petabyte-scale data warehouse
- designed for reporting and analytics 
- OLAP (Column based) not OLTP (row/transaction)
- captures stores and processes data in realtime. 
- OLAP - complex queries from OLTP systems. 
- pay as you use 
- direct query s3 using Redshift spectrum
- direct query other DB's using federated query
- Server based (not serverless)\
- redshift runs with multiple nodes (private)
- not HA
- Leader node - query input planning and aggregation
- compute node - performing queries of data


## Redshift Resilience and Recovery
- only runs in one AV - 
- utilize s3 for backups in form of snapshots
- automatic backups every 8 hours OR 5 gb of change - 1 day retention up to 35 days
- incrimental 
- 

# Exam prep
- Tutorials Dojo Exam Practices. 

## Question Technique
- Questions are 1-2 lines of premable (scenario) - skip this
- Then the question itself - focus on the keywords
- 4-5 answers..multi choice or multi-select
- at the associate level - generally ansewr is simple right and wrong
- occasionally 'most siutable' from some right answers
- Generally 1 or 2 answers which can be excluded, locate those first. 
- Most questions have an overall criteria or restriction
- cost effective
- Cash strapped - 
- Best practice - via instance role
- Highest performance - inverse of cost effiective / cash
    - ebs volumes or instance store volumes - direct connect over site to site
- timeframe restriction
    - one week to perform an impliemntation - no direct connect. 