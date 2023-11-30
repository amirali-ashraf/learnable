# Developer Learning Plan
https://explore.skillbuilder.aws/learn/lp/84/developer-learning-plan

## Introduction to Container

Inefficient Way
Bare Metal Servers > Server Hardware > Operating System > Libraries > Application A, B, C

Virtual Machine > Server Hardware > OS > Virtialization Platform > VMs

Containers > Server Hardware > OS > Containerization Platform > Libraries > Shared Libraries

Docker Benefits:
1- Portable
2- Package in images
3- Different versions are supported
4- Faster


To build your own image we need to create a Dockerfile to create the image

A simple docker file:
``` Dockerfile
From ubuntu:latest
CMD echo "Hello world"
```

This is to run a java code:
``` Dockerfile
FROM openjdk:8
COPY /hello.jar /usr/src/hello.jar
CMD java -cp /usr/src/hello.jar org.example.App
```

Each command within a docker file creates a layer within the image which is **immutable**:

``` Dockerfile
FROM centos:7 => first layer

RUN yum -y update && yum -y install httpd => second layer

EXPOSE 80 => third layer

ADD run-httpd.sh /run-httpd.sh => fourth layer
RUN chmod -v +x /run-httpd.sh => last layer

CMD ["/run-httpd.sh"]
```

Each layer has a thin read/write layer on top of the existing image when it is instantiated. The underlying image remains unchanged.


### Microservice Architecture
This is designed to speed up the deployment side. In microservice architecture we have the ability to start fast, fail fast and recover fast.

The characterstics of microservices:
1- Decentrialized
2- Smart endpoints, dumb pipes => service should be smart
3- Independent products => each microservice is a independent product
4- Designed for failure => services should be resilient to handle bad input
5- Disposability => Anything breaks should be recovered fast. Add and remove containers easily
6- Development and production parity => The program that works on developers system should work the same on production system too.


## Introduction to AWS Fargate
What is fargate? It is a new technology to deploy and manage the containers. 

1- With Fargate you don't need to provision and scale the servers and your clusters
2- You don't need to patch and update the underlaying infrustructure.
3- Fargate supports both ECS (Elastic Container Service) and EKS (Elastinc Kube Service)
4- We can choose the orchetration solutions based on ECS and EKS
5- With Fargate only you use based on what you use.
6- Fargate is easy to use for all types of users on AWS
7- We can use Fargate through AWS Management Console, AWS CLI, AWS ECS CLI
8- In Fargate we can choose our CPU and Memory usage
9- This would allow us to run a container behind an nginx in our environment.


Differences between Fargate and EC2:
1- All tasks run in virtual cloud on a VPC that we decide. We can define which VPC, what subnets and which security conditions to apply.
2- Fargate enforces the configuration once the tasks are started.
3- Fargate supports both ALB (Application Load Balancing) and NLB (Network Load Balancing) and to this date ELB (Elastic Load Balancing) is not supported by Fargate.
4- Fargate supports advanced task level networking which makes it to have security groups and monitoring tools

Fargate Security:
1- Tasks can be accessed by the ones who own the task
2- No SSH accesss to the infrustructure
4- Isolated cluster

When to use EC2 instead of Fargate:
1- If you're a heavier user of EC2 spot or paied for the instances
2- If our app is running on windows

Amazon services:
1- ECS to manage and launch containers on AWS
2- EKS uses Kubernetes
3- ECR is the registry to store containers







