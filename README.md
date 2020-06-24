# Deploy a highly available web application using CloudFormation

## Introduction 

The project consist to deploy an application (Apache Web Server) and also pick up code (JavaScript and HTML) from S3 Storage and deploy it in the appropriate folder on the web server.

There will be two parts to this project:
-   The first one consist of creating a diagram that we can present as part of your portfolio and as a visual help to understand the CloudFormation script.
-   The second part is to interpret the instructions as well as our own diagram and create a matching CloudFormation script.

This diagram below shows various cloud infrastructure resources that we will use to provision on the AWS cloud using the AWS command line and CloudFormation tools. 

![alt text](https://github.com/AnselmeChans/Deploy-web-app-cloudfront/blob/master/capture_tools_AWS.png?raw=true)

## COnfiguration to run create stack 

### Create IAM User
-   Add User
-   Attach existing policies directly
-   Administrator Access 
-   Download CSV 

### Configure AWS Command line 
-   pip install awscli
-   aws configure => Enter your AWS access key and your AWS         secret key and default region name « us-west-2 ».
-   To verify all is working : aws s3 ls

To Deploy our stack we will use CLoudFormation (Concept of Insfrastructure As Code).
It s a declarative langage where you declare the ressources what you want. We have to declare with a YAML format in cloud formation 


## Problem 

Our company is creating an Instagram clone called Udagram. Developers pushed the latest version of their code in a zip file located in a public S3 Bucket.
You have been tasked with deploying the application, along with the necessary supporting software into its matching infrastructure.
This needs to be done in an automated fashion so that the infrastructure can be discarded as soon as the testing team finishes their tests and gathers their results.

### Server specs

Create a Launch Configuration for your application servers in order to deploy four servers, two located in each of your private subnets.
The launch configuration will be used by an auto-scaling group.
We'll need two vCPUs and at least 4GB of RAM. The Operating System to be used is Ubuntu 18. So, choose an Instance size and Machine Image (AMI) that best fits this spec. Be sure to allocate at least 10GB of disk space so that you don't run into issues. 

### Security Groups and Roles

Since you will be downloading the application archive from an S3 Bucket, you'll need to create an IAM Role that allows your instances to use the S3 Service.

Udagram communicates on the default HTTP Port: 80, so your servers will need this inbound port open since you will use it with the Load Balancer and the Load Balancer Health Check. As for outbound, the servers will need unrestricted internet access to be able to download and update its software.

The load balancer should allow all public traffic (0.0.0.0/0) on port 80 inbound, which is the default HTTP port. Outbound, it will only be using port 80 to reach the internal servers.

The application needs to be deployed into private subnets with a Load Balancer located in a public subnet.

One of the output exports of the CloudFormation script should be the public URL of the LoadBalancer.

Bonus points if you add http:// in front of the load balancer DNS Name in the output, for convenience.


# Resolution

## Architecture Diagram


Diagrams are a very important starting point for planning our cloud infrastructure. DevOps engineers start with a visual representation of the required cloud infrastructure before they turn it into code.

![alt text](https://github.com/AnselmeChans/Deploy-web-app-cloudfront/blob/master/Udacity_Project2_Diagram.jpeg?raw=true)



## Instructions to follow

You will found in the dir many file: 
    -   network.yml => file for creating the network (VPC, Subnets etc...)
    -   jump-box


The network.yaml file is for creating the network (VPC, Subnets etc...). We have to use network.json as input parameters. 
The bastion.yaml creates a Bastion Host to remote into the Web Servers using bastion-params.json as the input. The webservers which include the Load Balancer, AutoScaling Groups and Security Groups are created using udacity-servers.yaml using the server-params.json file as the input. There is also a single-server.yaml file which creates a single server for some troubleshooting and debugging if needed. 

You will found 2 bash files suche as : 
    -   create.sh => allow to create the infrastructure 
    -   update.sh => allow to update the infrastructure


There are also a couple of batch files which ease the creation and updating of the stacks. Please ensure that you have a pre-created Key Pair for the Bastion Host. Ensure that you use the same environment variable for all the stacks.

# Instructions 

First create the network by running the create.sh file as below:
./create.sh udacity-network network.yml network-parameters.json 

Then create servers and bastion host as below: 
./create.sh udacity-instances servers.yml server-parameters.json 

if you want to update somethings make sure to use the update script: 
./update.sh udacityProject2 jump-box.yml jumpBox-parameters.json
