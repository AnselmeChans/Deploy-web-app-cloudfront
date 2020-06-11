# Deploy-web-app-cloudfront

## Introduction 

we will deploy an application (Apache Web Server) and also pick up code (JavaScript and HTML) from S3 Storage and deploy it in the appropriate folder on the web server.

There will be two parts to this project:

You'll first develop a diagram that you can present as part of your portfolio and as a visual aid to understand the CloudFormation script.
The second part is to interpret the instructions as well as your own diagram and create a matching CloudFormation script.

## Problem 

Your company is creating an Instagram clone called Udagram. Developers pushed the latest version of their code in a zip file located in a public S3 Bucket.
You have been tasked with deploying the application, along with the necessary supporting software into its matching infrastructure.
This needs to be done in an automated fashion so that the infrastructure can be discarded as soon as the testing team finishes their tests and gathers their results.

## Project Requirements

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

### Starter Code


### Auto-scaling concept 

In these part of autoscaling our server, we will follow this 2 important steps : 

#### Scaling Policy 
A Scaling Policy is the criteria used to decide when to Add or Remove Servers from your Auto Scaling Group.
It's here where we  decide based on the criteria to choose to turn those servers off when they are not needed and then turn them back on when there is demand.
We could too, create a CloudWatch Alarm with a custom metric that counts the number of web visitors in the last 2 hours, if the number is less than 100, for example, perhaps a single server is enough. This will be a trigger to Scale Down if there is more than one server running at the time.

#### Launch configuration
We should thing of launch configuration as a template or a recipe. We are instructing the Auto Scaling service HOW to run your web application. For example: My application requires 2GB RAM , 4 vCPUs, 10GB of Disk Space, The Java runtime version 8 Or NodeJS 10.0, for example. All this on top of a standard distribution of Linux or Windows Read more about Launch Configuration.

Once an Auto Scaling group knows how to launch new copies of your application, then the process of scaling up and down can take place.






# Resolution of the work 

## Settting Up of our Environment 

## Deploy security groups



## Creating Autoscalling groups 

Create server based on the criteria. 