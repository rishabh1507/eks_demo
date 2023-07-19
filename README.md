# DevOps Assignment- EKS

As part of this assignment, we would like to evaluate candidate’s skills and knowledge related to AWS. Candidate is supposed to complete the following assignment to the best of their abilities.

Please perform the below projects on a free AWS account(create a new one if required).

## Assignment scenario:

Design a highly available and scalable containerised application on Amazon EKS. Below are the requirements and deliverables:

## Requirements:

1. Create an EKS cluster along with a node-group with t3.small instances using [eksctl](https://eksctl.io/)(using config files).
2. Deploy a simple [Hello World container](https://hub.docker.com/r/amazon/amazon-ecs-sample) on EKS this cluster.
3. Expose this application on internet using Application Load balancer.
4. Configure this application to autoscale based on CPU utilisation(70% CPU)

**Note-** Please use manifest files to create all the resources and avoid using UI. 

## Deliverables:

1. Complete setup by showcasing the application accessible from internet.- Done
2. Link of a Github repo hosting the config files used to create the above setup. - Done
3. Provide suggestions on how you would make this application more secure and cost-effective. -
Rightnow the ekscluster uses 2 public and private subnet each. I will try to slim down the setup by only keeping 2 private subnets, nat gateway and will attach an ALB to access the application this will make the setup secure and cost effective. 
Example sample
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: prodigal-vpc
  region: ap-northeast-1

vpc:
  id: "vpc-0f3622456d4d54898"
  cidr: 172.31.0.0/16
  subnets:
    private:
      ap-northeast-1a:
        cidr: 192.168.1.0/24
  
      ap-northeast-1c:
        cidr: 192.168.2.0/24
  nat:
    gateway: HighlyAvailable 

NodeGroups:
- name: prodigal-node1
  instanceType: t3.small
  minSize: 1
  maxSize: 5  
  desiredCapacity: 1
  privateNetworking: true
  availabilityZones: ["ap-northeast-1a"] 

- name: prodigal-node2
  instanceType: t3.small
  minSize: 1
  maxSize: 5  
  desiredCapacity: 1
  privateNetworking: true
  availabilityZones: ["ap-northeast-1c"]

```

Good luck! We look forward to seeing your work.