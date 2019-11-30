# AWS-TERRAFORM-TUTORIAL 1
In this tutorial we are going to use the version 0.12.15 of Terraform. We are going to create a very simple [ec2](https://aws.amazon.com/en/ec2/) instance in AWS using nothing but [Terraform](https://www.terraform.io/). I will try to stay very informative and straight to the point. This means that in this tutorials we are not going to cover every single feature provided by Terraform. Later on other tutorials will be written to cover more advanced features such as different types of resources, modules, as well as how to origanize your code, etc... So don't panic there will be more to learn on Terraform in the future. For now, here are the topics that we are going to cover in this tutorial :

## Roadmap
- [AWS Admin IAM User setup and Access Tokens](#AWS-Admin-IAM-User-setup-and-Access-Tokens)
- [AWS Provider, terraform init, terraform validate, terraform plan](#AWS-Provider,-terraform-init,-terraform-validate,-terraform-plan)
- [AWS VPC Resource and terraform apply](#AWS-VPC-Resource-and-terraform-apply)
- [AWS IGW (Internet Gateway) and Subnets](#AWS-IGW-(Internet-Gateway)-and-Subnets)
- [AWS Route table, NACL and Security Groups](#AWS-Route-table,-NACL-and-Security-Groups)
- [Elastic IP, SSH KEY and Dynamic AMI](#Elastic-IP,-SSH-KEY-and-Dynamic-AMI)
- [AWS EC2 Instance](#AWS-EC2-Instance)
- [Terraform destroy](#Terraform-destroy)

## AWS Admin IAM User setup and Access Tokens
Before Terraform can interact with AWS, we need to **create** a dedicated **user** within AWS **with Programatic access and** give this user **administrative permission**. Finaly we will have to grab the **Access Tokens**.
Here are the steps :
- Sign in to the AWS Management Console and open the IAM console at https://console.aws.amazon.com/iam/.
- In the navigation pane, choose **Users** and then choose **Add user**.![](assets/aws-new-programatic-user-step1.png)
- Type the user name for the new user. This is the sign-in name for AWS.
- Select the type of access this set of users will have.
Select **Programmatic access**. This creates an access key for each new user. You can view or download the access keys when you get to the Final page.
- Choose **Next: Permissions**![](assets/aws-new-programatic-user-step2.png)
- On the **Set permissions** page, specify how you want to assign permissions to this set of new users. choose **Attach Existing Policies Directly** and in the Policy Filter type **AmazonEC2FullAccess**, you can choose any permission level, but in this example, I’ll click on the checkbox next to **AmazonEC2FullAccess**![](assets/aws-new-programatic-user-step3.png)
- Choose **Next: Tags –> Next: Review** to see all of the choices you made up to this point. When you are ready to proceed, choose **Create user**.
- To view the users’ access keys (access key IDs and secret access keys), choose **Show** next to each password and access key that you want to see. To save the access keys, choose **Download .csv** and then save the file to a safe location. **You will not have access to the secret keys again after this step**.![](assets/aws-new-programatic-user-step4.png)

Since it is a very bas pratice to save creadentials in a configuration file, we must use what is known in Terraform as a [Shared Credentials file](https://www.terraform.io/docs/providers/aws/index.html#shared-credentials-file). To generate this file we will use the [AWS Command Line Interface](https://aws.amazon.com/en/cli). Once installed using python packages manager pip, simply run ```aws configure``` and provide the 'Key ID' and 'Secret Access Key' when prompted.

```
$ sudo pip install awscli
$ aws configure
AWS Access Key ID [None]: *********************
AWS Secret Access Key [None]: *******************
Default region name [None]:
Default output format [None]:
```

We now have everything setup regarding AWS Authentification and we can now start using Terraform with AWS.

## AWS Provider, terraform init, terraform validate, terraform plan
In this part we are going to set up a AWS Provider as well as initializing our terraform state. Finaly we are going to perform code validation. Before we can do anything we have to create a brand new directory and in it create a file named main.tf (the name does not realy matter).

In this file, the first thing we need to do is tell Terraform that we want to use the [AWS Provider](https://www.terraform.io/docs/providers/aws/index.html). Now, for the AWS Provider to work properly it has to know the aws region that you wan to deploy on.

```hcl
provider "aws"{
  region  = "eu-west-3"
}
```
Now, since we have our first terraform code, it's time to initialize our workspace directory with ```terraform init```
```bash
$ terraform init                                                                  
                                                                                  
Initializing the backend...                                                       
                                                                                  
Initializing provider plugins...                                                  
- Checking for available provider plugins...                                      
- Downloading plugin for provider "aws" (hashicorp/aws) 2.40.0...                 
                                                                                  
The following providers do not have any version constraints in configuration,     
so the latest version was installed.                                              
                                                                                  
To prevent automatic upgrades to new major versions that may contain breaking     
changes, it is recommended to add version = "..." constraints to the              
corresponding provider blocks in configuration, with the constraint strings       
suggested below.                                                                  
                                                                                  
* provider.aws: version = "~> 2.40"                                               
                                                                                  
Terraform has been successfully initialized!                                      
                                                                                  
You may now begin working with Terraform. Try running "terraform plan" to see     
any changes that are required for your infrastructure. All Terraform commands     
should now work.                                                                  
                                                                                  
If you ever set or change modules or backend configuration for Terraform,         
rerun this command to reinitialize your working directory. If you forget, other   
commands will detect it and remind you to do so if necessary.                     
```
This command performs several different initialization steps in order to prepare a working directory for use. During init, Terraform searches the configuration for both direct and indirect references to providers and attempts to load the required plugins. init will automatically download and install plugins if necessary.

Next, let's perform a ```terraform validate```. Validate runs checks that verify whether a configuration is syntactically valid and internally consistent.

```
$ terraform validate
Success! The configuration is valid.
```

Last but not least we can run ```terraform plan``` to see any changes that are required in our infrastructure. 

```
$ terraform plan
Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but will not be
persisted to local or remote state storage.


------------------------------------------------------------------------

No changes. Infrastructure is up-to-date.

This means that Terraform did not detect any differences between your
configuration and real physical resources that exist. As a result, no
actions need to be performed.
```
This command is a convenient way to check whether the execution plan for a set of changes matches your expectations without making any changes to real resources or to the state. Since we didn't declared any ressource yet in our main.tf, there is no differences between our configuration and the real physical resources.



## AWS VPC Resource and Terraform apply



## AWS IGW (Internet Gateway) and Subnets



## AWS Route table, NACL and Security Groups



## Elastic IP, SSH KEY and Dynamic AMI



## AWS EC2 Instance



## Terraform destroy