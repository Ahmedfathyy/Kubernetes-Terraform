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

