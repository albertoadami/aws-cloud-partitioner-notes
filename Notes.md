# Notes for AWS Cloud Partitioner Certification

# Table of contents
1. [Beginning before a Cloud](#introduction)
2. [Identity and acess management (IAM)](#iam)
3. [Virtual Private Cloud (VPC)](#vpc)
4. [AWS Elastic Compute Cloud (EC2)](#ec2)
5. [AWS Storage Services](#storage)
6. [Elastic Load Balancing (ELB)](#elb)
7. [CloudFront and DNS](#dns)
8. [Monitoring and Logging](#monitoring)
9. [Simple Notifications Services (SNS)](#sns)
10. [Relational Database Service(RDS) and DynamoDB](#db)
11. [Serverless](#lambda)
12. [Security and Compliance Services](#security)
13. [AWS Key Management Service (KNS)](#kns)
14. [Other AWS Services](#others)
15. [AWS Pricing, Billing and Support Services](#pricing)


## Beginning before a Cloud <a name="introduction"></a>
With the client-server architecture multiple computers can use the same applications if they are connected in the same network.
With the cloud the servers are on a remote provider infrastruture. The cloud provides the following things:

1. compute: CPU(Brains) + Memory(RAM);
2. storage: location where data is saved;
3. database: application that stored data in a structure way.
4. network: the connection hw for the server.

The DNS server is the component that's responsible to translate the web adresses into the ip adresses of the servers to use.
The challenges of the data centers are the following:
* Spawl/space;
* Power;
* Cooling.

***Cloud Computing***: hardware and services provided over the internet. In this way the customers don't need to buying and configuring them anymore.
In the cloude there are different king of services:
* SAAS: software provided by 3th party (email, dropbox, Office365, etc..);
* IAAS: hardware that we require to run over the applications (compute, network, storage);
* PAAS: infrastructure and operating system.

AWS provides SAAS + IASS + PAAS services.

The Cloud can be of different types:
1. Corporate cloud: some private datacenter;
2. Public cloud: datacenter on some provider(like AWS);
3. Hybrid: both Corporate + Public solutions.

The main disadvantages on using Corporate cloud are that the physic HW usually has 3-5 years of life and there are maintenance costs. Instead the public cloud is more flexibile, you can setup machines using a web portal and if you don't need some HW/services anymore you can delete all these stuff. 
A public cloud solution is also more scalable.

***Scalable***: the ability to easily grow in size, capacity and/or scope when required.

To be ***highly available*** we don't neeed to have some single point of failure in our system.

The AWS Cloud consists of 21 regions around the world. Each region has multiple availability zones (AZ). Each region contains at leas two availability zones. The ***availability zone*** is where the data center is phisically stored.

In AWS the data can be replicated in multiple availability zones around the world.

Here the list of AWS main services:
- Networking:
    * Direct Connect;
    * Route 53;
- Compute:
    * EC2;
    * Lambda;
- Storage:
    * S3;
    * Glacier (long term storage).

## Identity and acess management(IAM) <a name="iam"></a>
IAM is the AWS service to handle the AWS accounts and their access to the various AWS services. The users created by opening a new AWS account is the ***root*** account.

After that you can add multiple ***IAM users*** into the AWS account, in this way you don't need to share the root users credentails with other people. 

If multiple accounts needs to have the same access level/permissions to the various AWS services you can put all them inside a ***group*** defined in IAM.

In IAM each user has:
* username;
* password;
* permissions to AWS services.

To enable the access for an IAM user to a sepcific resource, we need to set a full-access policy. The ***IAM roles*** define the policy permissions between multiple AWS services (EC2 to S3 for example).

## Virtual Private Cloud (VPC) <a name="vpc"></a>
***VPC*** let's you provisioning a logically isolated section of AWS cloud where you can launch resources in a virtual network that you define. When you define your own VPC only the users that has grants can access to them.
 
 When you define a VPC you need to configure the IP adress range of the network. After you have defined the VPC you need to add one or more ***subnets***, that is a sub portion of the VPC. When you define the subnet you need also to select an Availablity Zone.
 For example you can define a VPC with IP range like 170.10.0.0/16 and two different subnets with 170.10.1.0/24 and 170.10.2.0/24 as IP ranges. 

 When we wanted to run an EC2 instance for exmaple we need  to select a VPC and a subnet for that, when the EC2 instance will be run.

 If some services/machines needs to be available in the public nework you need also to configure an ***Internet Gateway (IGW)***. 

 ***Internet Gateway:*** a combiantion of hardware and software that provides you network with a route to the world outside of the VPC. You need to associate one IGW to a VPC to make some components available on the internet. In AWS we can have one IGW for each VPC.

 The ***route tables*** contains a set of rules called routes, that are used to determine where network traffic is directed. They are associated with a subnet. In some scenario you need to have a public subnet and a private subnet, the public subnet it's the part of the VPC that is exposed on the internet, instead the private subnet it's not on the internet but maybe the public subnet can acces to their services/servers.

 To enable the access of a public subnet in the internet, you need to add a rule into the route table associated with the public cloud that's enable the traffic between the IGW.

 The rules in the route tables have a number, the first rules have more priority that the following ones.

 To define some security rules on subnet level you need to configure the ***Network Access Control Level(NACL)***. NACL is a firewall/security layer on the subnet. It's responsibile to block some connection/traffic that's not allowed to enter on the subnet level. For example you can need to enable the SSH and HTTP only from some other subnet.

 Exists also the concept of ***Security Group***, that's similar to the NACL but it's apply on an instance level (an EC2 machine for example). The security group is some extra check performed after the NACL to check if the network request is allowed.

## AWS Elastic Compute Cloud (EC2) <a name="ec2"></a>
EC2 is basically a computer. It provides computing capacity in the AWS cloud.
EC2 can be used to launch how many computer servers you need, they can be configured from the AMI (Amazon Machine Image), AWS supports Windows or Linux servers.

With EC2 you can be very flexible and delete some intances when you don't need them anymore (on Demand). It's possible to buy instances only for a set of time period (Reserved).

You can configure the server with some different configurations of hardware, the configurations change the final price for the machine.

***AMI*** is a pre-configured package to launch an EC2 instance. There are different types of AMIs:
* community: free to use;
* AWS marketpalce: pay to use;
* my AMIs: create by yourself.

When you launch an EC2 instance, a security group acts as a virutal firewall that controls the traffic for one or more instance. We can define multiple security groups for different use cases. Each EC2 instance can have only one security group associated.

To connect to your EC2 instance via SSH, it has to be enable on security group level. When you create the instance you need to configure the key-value certification file (.pem) that you need to provide when you connect via ssh protocol.

The command to connect to the instance is:
```
ssh -i "pem_file.pem" ec2-user@EC2-public-name
```
## AWS Storage Services <a name="storage"></a>
***Simple Storage Service (S3):*** online, bulk storge service that you can access from almost any device. S3 it's the primary storage service on AWS, you can store any type of file on it.

Buckets:
1. Root level "folders" you create are referred as buckets;
2. Any sub folder you create in a bucket is referred to as a folder;
3. Files stored in a bucket are referred to as objects.

The bucket names need to be unique along all AWS accounts. (not only yours)

The objects can be stored directly on the bucket or in a folder inside it.

You can configure S2 to encrypt the files. An other configuration it's the visibility level,  usually you don't want to configure S3 to have a public access on the internet.

When you create a new S3 bucket you have to select an AWS region, the best practice is to select one region that's near the users of your application.

Each S3 object has a "classification" assigned to it. The classification can be:
* Standard: for frequent access;
* Standard IA: infrequent access;
* One Zone IA: infrequent access with AZ >=1;
* Glacier: long ime archival (>= 90 days);
* Glacier Deep Archive: long time (>= 180 days);
* Reduced Redundancy: not reccomended;
* Intelligent Tiering: long lived data with changing or unknown patterns.

On S3 you can also configure a lifecycle rule, to change the classification class after some times. For example you can configure the classification rule of the provious version of a file to become a glacier.

***AWS Storage Service*** is a way to integrate your cloud service with AWS cloud without migrate it. Application in your private cloud will connect to AWS cloud using a virtual server.

## Elastic Load Balancing (ELB) <a name="elb"></a>
***Elastic Load Balancing (ELB)*** disribuites traffic between multiple EC2 instances that are associaed with it. The traffic goes to the ELB that redirect the request to the appropiate EC2 IP adress.

The ELB can contains multiple EC2 insance of different subnet, in different availability zones. In this way if we loose one AZ, the services remain available. We increase the fault tolerance of our applications. The ELB distribuite the traffic to all the EC2 instances associated with it in an equal way.

***Auto scaling*** automates the process of adding or removing EC2 instances based on your applications traffic demand.
For example we can configure that if the CPU usage of an instance is greater of a certain value (80 for example), then a new EC2 instance will be added. Also the maximum and minimum number of instances in an ELB can be configured.

## CloudFront and DNS <a name="dns"></a>
***Route53*** is the AWS service to configure and manage web domains for applications running on AWS. You can buy domains direcly from the AWS service.


On Route53 you associate the domain with an IP adress(of a AWS machine). In this way someone from the internet world will call the domain name and the service is responsible to transalte it with the correct IP adress.

Route53 also sends automated requests over the internet to your applications associated with it, to check if the services are available/running.

***CloudFront*** is a content delivery network that allows you to store (cache) your content att "edge locations". This allows to your users to access the contents more quickly. The ***pointts of presence*** are in varius location of the world and in this way the users can access the content also it the original service is not working. The data of the original service will be propagated to all the poins of presence. Route53 can be configured to use CloudFront. If the request is not stored on the edge locations the request is forwareded to the original environment and the response is propagated to all the locations for future requests.

## Monitoring and Logging <a name="monitoring"></a>
***Cloudwatch*** is a service that allows you to monitor various elements of your AWS account. With it you can monitor your resources in real-time. You can configure Cloudwatch with tthe notification service to receive notification via email when an EC2 instance goes down for example.

With Cloudwatch you need to configure a dashboard to view the metrics that you select. For example you can configure an alarm if CPU usage of EC2 instance goes up of 80%. Or you can configure an alarm also if the month billing exceed 500$.

Instead ***Cloudtrail*** allows you to monitor all the actions taken by all IAM users into your AWS account. Cloudtrail allows also to see the history of actions taken in your account. You can see tthe recent events performed by all IAM users. 

Cloudtrail saves the log into an S3 bucket using a gzip file format.

## Simple Notifications Service (SNS) <a name="sns"></a>
***SNS*** is an AWS service that allows you to automate the sending of email/message notifications based on events that happen in your AWS account. Like said before can be cofnigured with the Cloudwatch service.

In SNS there are two types of clients:
* Subscribers: receive the message or nottification when they are subscribed ot a topic;
* Publishers: communicate with the subscribers by sending a message to a topic.

In SNS you can configure the topics from the AWS console. After that you need to add some subscriber to that topic.

## Relational Database Service(RDS) and DynamoDB < a name = "db"></a>
In the world there are two kind of databases:
* Relational databases (SQL): RDS service;
* Non-relatitonal databases (NO-SQL): DynamoDB service.

***Relatitonal database service (RDS)*** is a SQL database service that provides a wide range of SQL database options to select from. You can select Amazon Aurora, MySQL, Postres, SQL Server, Oracle or MariaDB as a dabatabase.

With RDS it's easy to setup and manager your databases on the cloud.

Instead ***DyanmoDB*** is a NO-SQL database service, it does not provide other NO-SQL database options. It's a database similar to MongoDB or Cassandra. It save it's own data using a key-value structure with JSON as a value.

***Elasticache*** is a cache service that can be used to improve your applications speed/performance. Elasticache supports Redis and Memcached. It allow you to deploy and configure easily the cache service instance.

***Redshift*** is a data warehouse database service designed tto handle petabytes of data for analysis.

## Serverless <a name= "lambda"></a>
***Lambda*** is serverless computing. It is the next generation of cloud computing that will replace EC2 instances. It's a compute service that let's you run code without provisioning or managing servers. You pay only for the compute time that you consume.

AWS Lambda supports Java, C#, Node.js, Ruby, Go, .NET Core and Python as programming languages.

AWS manage all the infrastructure for you, one of the advantages of using serverless is that you don't need to mangage all the infrastructure where your code is running.

## Security and Compliance Services <a name="security"></a>
The ***Shared Responsibility Model*** defines that you (as AWS account) and AWS are reresponsible for when it comes to securiy and compliance.
AWS is responsibile for the AWS layer and physical security. Instead AWS user is responsibile for the updates of the operating system/software.

Many organizations required ***penetration testing***. Penetration testing is when the cloud is validated with tests that simulate attackers. There are some security tests that can be performed on AWS and some that are not allowed. Cloudfront is helping to mitigate DDOS attacks, because the user don't access to the EC2 instance directly.

There are some AWS security services: AWS Organizations, AWS GuardDuty, AWS Inspector, AWS Shield, AWS Web Application Firewall and AWS Artifact.

## AWS Key Management Service (KNS)
***KNS*** enables encryption of data and provides centralized encryption, key storage, management and auditing. Using KNS the users cannot see the values without using a corret key.

KNS integrates wiht other AWS services like S3, Storage Gateway, EBS, RDS, DynamoDB, SNS, CloudTrail.

## Other AWS services <a name = "others"></a>
Sometimes your organization need to conect from the on-premise data center yo the AWS VPC. ***AWS Direct Connect Location*** is a service that enable you to do that using a private connection.

***Amazon Athen*** instead is a serverless query service used to analyze data in S3 using a SQL language for query data.

***Amazon EMR*** is a AWS service that provides Hadoop framework.

## AWS Pricing, Billing and Support Services <a name="pricing"></a>
***AWS Organizations*** allows to handle billing for multiple AWS accounts from a single interface. If you are in a big organization the company can have multiple AWS accounts (one for department for example). Using AWS Organizations you can handle the billing in a more easily way (in a single user interface).

In AWS you "pay-as-you-go", so you pay for the services that you are using. This allows you to remove/adapt services when you are not using them anymore. In this way you can pay less and save more money.

For S3 service you pay for how much data you store and for request pricing (number of request using REST API).

***Total Cost of Ownership (TCC)*** is a free tool that allow you to see the cost saving of using AWS instead that on premises solutions.

***AWS Simple Calculator*** instead is a tool to estimate the AWS bill based on some scenario. The new version is called ***AWS Pricing Calculator***.

***Cost Explorer*** is a free tool that allows you to view charts of your AWS costs.


There are different kind of AWS accounts:
* Basic: included with any AWS account;
* Developer: 29$/month;
* Business: 100$/month;
* Enterprise: 15K$/month.

There are differences for the AWS support, the enterprise and business accounts get 24/7 Cloud Support. Developer account instead gets business hours to access to a Cloud Supports. Basic instead don't have any access to a Cloud Support.

***AWS Truster Advisor*** is a service that help you to optimize aspects of your AWS account. It helps you to reduce costs, increase performance and improve security.

***AWS Whitepapers*** is a collection of technical documents that outline many AWS relevant topics. ***AWS Service Documentation*** instead is a collection of documents specific to each AWS service.