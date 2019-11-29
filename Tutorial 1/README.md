# AWS-TERRAFORM-TUTORIAL 1
In this tutorial we are going to use the version 0.12.7 of Terraform. We are going to create a very very simple ec2 instance in AWS using nothing but Terraform. I will try to stay very informative, very direct, straight to the point. This means that in this tutorials we are not going to cover every single feature provided by Terraform. Later on other tutorials will be written to cover more advanced features such as different types of resources, modules, as well as how to origanize your code, etc... So don't panic there will be more to learn on Terraform in the future. For now, here are the topic that we are going to cover in this tutorial :
- AWS Provider, State and Validation
- AWS VPC Resource and Terraform apply
- AWS IGW (Internet Gateway) and Subnets
- AWS Route table, NACL and Security Groups
- Elastic IP, SSH KEY and Dynamic AMI
- AWS EC2 Instance
- Terraform destroy

## AWS Provider, State and Validation
In this part we are going to set up a AWS Provider as well as the Terraform State initialisation and finaly how we can perform code validation in Terraform. First things first, create a brand new directory and in it create a file named main.tf (the name does not realy matter)

```hcl
provider "aws"{
  profile = "default"
  region  = "eu-west-3"
}
```

## AWS VPC Resource and Terraform apply



## AWS IGW (Internet Gateway) and Subnets



## AWS Route table, NACL and Security Groups



## Elastic IP, SSH KEY and Dynamic AMI



## AWS EC2 Instance



## Terraform destroy