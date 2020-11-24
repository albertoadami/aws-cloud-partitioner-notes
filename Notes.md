# Notes for AWS Cloud Partitioner Certification

# Table of contents
1. [Beginning before a Cloud](#introduction)
2. [Identity and acess management (IAM)](#iam)
3. [Virtual Private Cloud (VPC)](#vpc)


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