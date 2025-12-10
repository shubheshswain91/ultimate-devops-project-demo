# Using the pem file 

After creating the EC2 instance and downloading the pem file, we have to ssh to it.

```bash
ssh -i devops-demo.pem ubuntu@<ec2-public-ip-address>
```

Initiall the access will be denied, in that case:

```bash
chmod 400 devops-demo.pem 
```

and rerun the ssh again.

# Install the docker engine for ec2 instance:

Follow the steps mentioned in this section:

https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

![alt text](assets/image.png)

```bash


```
Add Ubuntu user to the docker group to run the docker commands without the sudo.

```bash
sudo usermod -aG docker ubuntu
```
When you still see the permission denied, then loff out and login again.

# Install kubectl

https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-binary-with-curl-on-linux

![alt text](assets/image1.png)

# Install terraform

https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

![alt text](assets/image2.png)

# Increasing EC2 storage and resizing it

![alt text](assets/image3.png)

![alt text](image4.png)


# Docker compose 

![alt text](image-1.png)

# Security group allow inbound traffic

![alt text](image-2.png)

![alt text](image-3.png)

# Build the product catalog locally

![alt text](image-4.png)

![alt text](image-5.png)

# Building the product-catalog

![alt text](image-6.png)

![alt text](image-7.png)

![alt text](image-8.png)

![alt text](image-9.png)

![alt text](image-10.png)

# Building the Ad service 

https://github.com/iam-veeramalla/ultimate-devops-project-demo/tree/main/src/ad#ad-service

  ## Building locally 

![alt text](image-11.png)

![alt text](image-12.png)

![alt text](image-13.png)

![alt text](image-14.png)

![alt text](image-15.png)

![alt text](image-16.png)

  ## Building using Dockerfile

![alt text](image-17.png)  

![alt text](image-18.png)

![alt text](image-19.png)

# Building the recommendation service

https://github.com/iam-veeramalla/ultimate-devops-project-demo/tree/main/src/recommendation#local-build

  ## Building Dockerfile 

  ![alt text](image-20.png)

# Pushing the images to docker hub

![alt text](image-21.png)


# Docker Compose 

![alt text](image-22.png)

![alt text](image-23.png)

![alt text](image-24.png)

![alt text](image-25.png)

![alt text](image-26.png)

![alt text](image-27.png)

![alt text](image-28.png)

# Docker and Kubernetes

![alt text](image-29.png)

  ## Docker compose vs Kubernetes 

![alt text](image-30.png)

## Kubernetes management 

![alt text](image-31.png)

# Terraform

## Terraform life cycle

![alt text](image-32.png)

## Installing AWS CLI

https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

![alt text](image-33.png)

create from profile -> Security credentials  -> Create access key

```bash
shubhesh@LAPTOP-MD6V0EDU:~/eks$ aws configure
AWS Access Key ID [None]: < Access key ID >
AWS Secret Access Key [None]: < Secret access key >
Default region name [None]: eu-central-1
Default output format [None]:  < Just keep it blank and press Enter >
```


## Terraform backend

![alt text](image-34.png)

![alt text](image-35.png)

![alt text](image-36.png)

## VPC and subnets 

![alt text](image-37.png)

## EKS setup 

![alt text](image-38.png)

## Invoking the modules and creating the EKS and VPC

![alt text](image-39.png)

![alt text](image-40.png)

![alt text](image-41.png)
 
![alt text](image-42.png) 

![alt text](image-43.png)

![alt text](image-44.png)

![alt text](image-45.png)

## kubectl setup and setting kubeconfig

Instal aws_cli and then configure the credentials

```bash
$ aws configure
AWS Access Key ID [None]: < Access key ID >
AWS Secret Access Key [None]: < Secret access key >
Default region name [None]: eu-central-1
Default output format [None]:  < Just keep it blank and press Enter >
```

![alt text](image-46.png)

![alt text](image-47.png)

![alt text](image-48.png)

# Kubernetes Implementation Overview

![alt text](image-49.png)

## Service Account 

![alt text](image-50.png)

## Deployment 

![alt text](image-51.png)

![alt text](image-52.png)

## Services

![alt text](image-53.png)

![alt text](image-54.png)

## Deploying the project on k8s - 1

![alt text](image-55.png)

![alt text](image-56.png)

## Deploying the project on k8s - 2

![alt text](image-57.png)

Service's selector  selects the pods based on the labels
![alt text](image-58.png)

defined inside the deployment yaml metadata labels as shown below:

![alt text](image-59.png)

Target port in the service needs the container port in the deployment

![alt text](image-60.png)

![alt text](image-61.png)

#######################################################################################
#######                                                                    ############
#######             Important sections                                      ###########
#######################################################################################
## Deploying the project on k8s - 3

![alt text](image-62.png)

![alt text](image-63.png)

![alt text](image-64.png)

![alt text](image-65.png)

### Services

![alt text](image-66.png)

After changing the frontendproxy svc to type LoadBalancer:

![alt text](image-67.png)

### Disadvantage of Load Balancer

![alt text](image-68.png)

1. Not declarative approach:  It provides the http link(for making it https we have to use UI and do the manually add the TLS certificates)

2. Cost: We need to create multiple LB if we want to expose the microservices to the external traffic and that's not cost efficient.

3. Lack of flexibility: It is tied to the ALB from AWS, what if we want to use F5, nginx 

4. It is tied to cloud control management(CCM) but when hosted on local machine with minikube it wont work.

## Ingress and Ingress Controller 

Take a look at tthe nslookup of amamzon.com and our deployed E-commerce application and observe the difference. Try to access by IP address.

![alt text](image-70.png)

![alt text](image-69.png)

![alt text](image-71.png)

While Amazon.com blocks it but ours allows it which is a major security issue.

![alt text](image-72.png)

![alt text](image-73.png)

![alt text](image-74.png)

You should give the service name in the ingress because ingress resource is tied to the service. Ingress resource is only created when we need the external access to the microservice like in our case the frontendproxy.

![alt text](image-75.png)

What we are implementing with the Amazon's ALB:

![alt text](image-76.png)

Install eksctl for linux:

https://docs.aws.amazon.com/eks/latest/eksctl/installation.html

![alt text](image-77.png)

### Setting up Ingress controller 
Refer this doc: section-9/07-alb-ingress-controller.md
![alt text](image-78.png)

![alt text](image-79.png)

![alt text](image-80.png)

Install helm from script: https://helm.sh/docs/intro/install#from-script

![alt text](image-81.png)

![alt text](image-82.png)

![alt text](image-83.png)

Checks the logs from pod and see if there are any logs

![alt text](image-84.png)

![alt text](image-85.png)

Now delete the previously set LB by changing back the Type to NodePort

```bash
k edit svc opentelemetry-demo-frontendproxy
```

![alt text](image-86.png)

## Deploying the app using ingress

![alt text](image-87.png)

![alt text](image-88.png)

The DNS name we get from the Load Balancer won't work nor the IP address you get from the nslookup of DNS name because in the ingress controller we mentioned the hosts as example.com.

![alt text](image-91.png)

![alt text](image-89.png)

![alt text](image-90.png)

Go to your local PC /etc/hosts file and update the local machine DNS records as below:
```bash
$ sudo vi /etc/hosts
```
For windows: c:\windows\system32\drivers\etc\hosts

# Add the below line
52.28.202.135 example.com

save and close and try to access the exampple.com and see.

## Setup the new domain name

After getting your own domain name from any domain name website head to Route53

![alt text](image-92.png)

![alt text](image-93.png)

![alt text](image-94.png)

![alt text](image-95.png)

![alt text](image-96.png)

## Configuring ingress yaml file with our domain name 

![alt text](image-97.png)

Compare the IPs in below two pictures

![alt text](image-98.png)

![alt text](image-99.png)

![alt text](image-100.png)

![alt text](image-101.png)

![alt text](image-102.png)

## Our E-commerce shop tour with our domain name

![alt text](image-103.png)

![alt text](image-104.png)

![alt text](image-105.png)

![alt text](image-106.png)


# CI/CD Overview

![alt text](image-107.png)

## GitHub actions 

![alt text](image-108.png)

![alt text](image-109.png)

![alt text](image-110.png)

![alt text](image-111.png)

![alt text](image-112.png)

## GitOps using ArgoCD

![alt text](image-113.png)

![alt text](image-114.png)

### Installing ArgoCD

https://argo-cd.readthedocs.io/en/stable/getting_started/


![alt text](image-115.png)

![alt text](image-116.png)

Chnage the Type to Load Balancer 

ubuntu@ip-172-31-16-170:~$ k edit svc argocd-server -n argocd

![alt text](image-117.png)

![alt text](image-118.png)

![alt text](image-119.png)

ubuntu@ip-172-31-16-170:~$ k edit secret argocd-initial-admin-secret -n argocd

Decode the password using base64 
 echo <randomstring from the admin secret file > | base64 --decode

![alt text](image-120.png)

![alt text](image-121.png)

![alt text](image-122.png)

![alt text](image-123.png)

![alt text](image-124.png)

![alt text](image-125.png)

![alt text](image-126.png)