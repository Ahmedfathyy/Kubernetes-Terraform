# Terraform Network and EKS Module

This Terraform module creates a network and an EKS cluster in AWS Cloud provider . The network can have subnets, security groups, and other resources, and the EKS cluster can have worker nodes and other resources.


## Usage
To use EKS Module you can edit this section of code  
```
resource "aws_eks_cluster" "demo" {
  name     = "demo"
  version  = "1.24"
  role_arn = aws_iam_role.demo.arn

  vpc_config {
    subnet_ids = [
      aws_subnet.private_us_east_1a.id,
      aws_subnet.private_us_east_1b.id,
      aws_subnet.public_us_east_1a.id,
      aws_subnet.public_us_east_1b.id
    ]
  }

  depends_on = [aws_iam_role_policy_attachment.demo_amazon_eks_cluster_policy]
}
```
## Network infrastructure 
In this architecture, the AWS VPC is divided into two public subnets and two private subnets. Each public subnet has an internet gateway attached and a route table that directs traffic to the internet gateway. Each private subnet has a NAT gateway attached and a route table that directs traffic to the NAT gateway.

The EKS cluster consists of a control plane with master nodes and worker nodes launched in an auto scaling group. The worker nodes use a launch configuration that specifies the AMI, instance type, and other configuration settings. The worker nodes are also associated with a security group that controls inbound and outbound traffic.

the network is configured to this graph

![image](https://user-images.githubusercontent.com/100867143/230746080-a07f1494-c4bd-41f1-bea4-28842c2098ca.png)


