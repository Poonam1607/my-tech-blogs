---
title: "Terraform: Managing Resources"
datePublished: Thu Jun 08 2023 18:30:02 GMT+0000 (Coordinated Universal Time)
cuid: clinh49kq000609l80rgf7krn
slug: terraform-managing-resources
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686248701093/19f91334-3de9-4be5-9687-ba30bfca3998.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1686248983064/d9a148ee-ef88-40f1-902f-3f83797a5b8f.png
tags: devops, terraform, trainwithshubham, terraweek, terraweekchallenge

---

## Introduction✍️

In this blog, we will see how to define and manage resources. And also we will be creating a Terraform configuration file to define a resource of AWS EC2 instance and S3 bucket along with provisioners and life cycle management.

Let's go!🚀

## How to Define and Manage Resources?🤔

To define and manage resources using Terraform, we will follow these steps:

1. **Infrastructure as Code (IaC)**: As we saw earlier, IAC is the one in which we can define our desired infrastructure configuration in code using the HashiCorp Configuration Language (**HCL**) or **JSON** format.
    
    This includes the resources, the properties, and any dependencies between them.
    
    We define the configuration in Terraform files with a `.tf` extension.
    
2. **Provider Block**: We can declare the providers we want to use in our Terraform configuration.
    
    Providers are responsible for managing resources in a specific infrastructure platform, such as **AWS, Azure, or Google Cloud.**
    
    ```bash
     provider "aws" {
       region = "us-west-2"
     }
    ```
    
    By specifying the provider and any required configuration details like **access credentials** we can work on it.
    
3. **Resource Block**: We define the resources we want to create and manage using Terraform.
    
    Resources represent infrastructure components like **virtual machines, databases, networks, storage**, etc.
    
    Just specify the resource type, its properties, and any dependencies on other resources.
    
    We can create multiple instances of the same resource type by using a resource block with a unique name.
    
4. **Variable Block**: Variables allow us to pass inputs to our Terraform code, making it more flexible and **reusable**.
    
    Instead of making changes again and again into the `main.tf` file, just declare variables in another file like `variables.tf`
    
    ```bash
     variable "aws_access_key" {
       type = string
     }
    ```
    
    We can define variables with types, descriptions, and default values.
    
5. **Output Block**: Outputs allow us to retrieve and **display** useful information about the created resources, such as **IP addresses, URLs**, or **connection strings**.
    
    We can define the output variables using the `output` block and Terraform will display them after successful execution.
    
    ```bash
     output "public_ip" {
       value = aws_instance.my-instance.public_ip
     }
    ```
    
    Don't worry! We will use all of these just right after the theory part.
    
6. **Terraform Init**: By running `terraform init` command in our Terraform directory to **initialize** the working directory. This command downloads the necessary provider **plugins** and sets up the **backend** configuration for storing the Terraform state ie, `.tfstate`
    
7. **Terraform Plan**: By running `terraform plan` to see a **preview** of the changes that Terraform will make to our infrastructure.
    
    It gives the design kind of a thing which they will go to build.
    
    The plan shows **additions**, **modifications**, or **deletions** of resources. Review the plan and verify it aligns with your expectations.
    
8. **Terraform Apply:** Then, executing `terraform apply` to apply the changes and create/update resources as defined in the configuration.
    
9. **Terraform Destroy**: If we no longer need the resources created by Terraform, we can use the `terraform destroy` command to disrupt everything in the infrastructure.
    
    This command will remove all the resources defined in the Terraform configuration.
    

By following the above steps, we can define and manage the resources using Terraform.

## Creating Terraform Configuration file using AWS📄

Every resource we have just seen above to define and manage now will go to do it practically.

1. First thing first, create an **EC2 instance** manually from the **AWS** dashboard in order to perform further procedures on it. And you already know how to do that from our previous learnings. So I am not going to repeat the same thing.
    
2. Your running **instance** will look like this.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686244194669/d188dd20-ddfc-4ba7-b9c2-747c1dd53859.png align="center")
    
3. Copy the **public IP address** from the instance id dashboard and go to the terminal and run this command in order to connect the instance to your local system.
    
    ```bash
    $ ssh -i /my-key-pair ubuntu@<ip-add>
    ```
    
    Give the correct path of your **generated key** and provide the correct **IP add**.
    
4. Now check that you have **Terraform** installed in it by running,
    
    ```bash
    $ terraform --version
    ```
    
    And if not, then install it from [here](https://developer.hashicorp.com/terraform/downloads).
    
5. Now as we know, we're creating a configuration file using AWS. So it is necessary to install **AWS CLI**. To do so, run
    
    ```bash
    $ sudo apt install aws cli
    ```
    
6. Now create an **access key** for a user in order to configure it from **IAM**
    
    * Go to IAM from the search bar.
        
    * Then click on "**users"** from the **IAM resources** section
        
    * Now click on the "**Add users"** button and give it appropriate permissions including the **AWS CLI** permission.
        
    * Now download the `.csv` file which has information about your access key and secrets.
        
7. Now run `aws configure` command and give the details of it.
    
8. Now to export it in Terraform run the `export` cmd
    
    ```bash
    $ export AWS_ACCESS_KEY_ID=<ID>
    $ export AWS_SECRET_ACCESS_KEY=<secret>
    ```
    
9. Now everything is fine to start writing terraform files.
    
10. Create a directory and inside that create a `main.tf` file
    
    ```bash
    ubuntu@ip$ mkdir terraform-aws
    ubuntu@ip$ cd terraform-aws
    ```
    
11. Now firstly we will create a resource block that creates an **EC2 instance** within the terraform block.
    
    ```bash
    terraform {
         required_providers {
         aws = {
         source = "hashicorp/aws"
         version = "4.16"
    }
    }
    required_version = ">= 1.2.0"
    }
    provider "aws" {
    region = "us-east-1"
    }
    resource "aws_instance" "my_ec2_instance" {
    	count = 2
    	ami = "ami-053b0d53c279acc90"
    	instance_type = "t2.micro"
    	tags = {
    		Name = "TerraformLearnings-Instance"
    }
    }
    ```
    
    1. `terraform { ... }` block:
        
        * This block is used to configure Terraform itself.
            
        * `required_providers` block specifies the providers required for this configuration. In this case, it specifies that the `aws` provider from HashiCorp is required, and it should be sourced from the `hashicorp/aws` namespace with a minimum version of `4.16`.
            
        * `required_version` specifies the minimum version of Terraform required to run this configuration, which is `1.2.0` in this case.
            
    2. `provider "aws" { ... }` block:
        
        * This block configures the AWS provider, which allows Terraform to interact with the AWS API.
            
        * `region = "us-east-1"` sets the region to "us-east-1" for all the AWS resources in this configuration.
            
    3. `resource "aws_instance" "my_ec2_instance" { ... }` block:
        
        * This block defines an AWS EC2 instance resource.
            
        * `count = 2` specifies that two EC2 instances will be created using this resource definition.
            
        * `ami = "ami-053b0d53c279acc90"` sets the Amazon Machine Image (AMI) to be used for the instances. In this case, it uses the **AMI** with the specified ID.
            
        * `instance_type = "t2.micro"` sets the instance type to "t2.micro".
            
        * `tags = { ... }` define the tags to be applied to the instances. In this case, it sets the "**Name**" tag to "**TerraformLearnings-Instance**".
            
12. Now further we will go to create **S3 bucket**.
    
    ```bash
    resource "aws_s3_bucket" "my_s3_bucket" {
    	bucket = "terraform-learnings-123"
    	tags = {
    		Name = "terraform-bucket-123"
    		Environment = "Dev"
    	}
    }
    ```
    
    * `bucket = "terraform-learnings-123"`: We are defining name of the S3 bucket to "**terraform-learnings-123**". The bucket name must be unique within AWS S3.
        
    * `tags = { ... }`: Tags are key-value pairs used to categorize resources. In this case, the block specifies two tags:
        
        * `"Name = "terraform-bucket-123"`: This tag sets the "**Name**" tag key to "**terraform-bucket-123**".
            
        * `"Environment = "Dev"`: This tag sets the "**Environment**" tag key to "**Dev**".
            
13. To use the output block we will write this content
    
    ```bash
    output "ec2_public_ips" {
    	value = aws_instance.my_ec2_instance[*].public_ip
    }
    ```
    
    * The `output "ec2_public_ips" { ... }` block in the configuration defines an output variable named "`ec2_public_ips`". This output variable will capture the **public IP** addresses of the **EC2 instances** created by the resource block `resource "aws_instance" "my_ec2_instance" { ... }`.
        
    * The `aws_instance.my_ec2_instance[*].public_ip` expression retrieves the public **IP** addresses of all **instances** created by the `aws_instance` resource using the wildcard `[*]`.
        
    * This allows capturing the public IP addresses of all instances even when the `count` parameter is used to create multiple instances.
        
14. Now our configuration file is complete, it's time to run that ***three magical commands***.
    
15. Run `terraform init` command to **initialize** and downloads the necessary provider plugins.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686246194227/1a4a905c-ecce-48c2-bce9-91f3d72e5ee2.png align="center")
    
    You will see a successful message like this.👆
    
16. Now run `terraform plan` command to see what changes we are going to make in our configuration file.👇
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686246288633/12772f8d-3a74-44e3-88df-b5fb48fe0c43.png align="center")
    
    See. it's saying, it will create `aws_instance` and `aws_s3_bucket` which we defined in the `main.tf` file👇
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686246373750/09443320-f551-4f0b-b430-910b20a41596.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686246423832/bfa86f0b-cdef-4d20-bd44-b30e22908b3d.png align="center")
    
17. Now run `terraform apply` command to have things to be done actually.👇
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686246494204/f6a0f07a-8d97-47a5-b88d-928cedb4bb56.png align="center")
    
    You can see the successful message with the output which we have defined to print on the screen.👇
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686246557295/b0c4d50b-5fc5-4354-b29d-0476d5cde8b1.png align="center")
    
18. Now, go to the AWS console and check the **EC2** and **S3 bucket** section and you will notice that two new instances and a new s3 bucket have been created with the given names of it.👇
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686246861561/784f59d2-80ef-4156-b60a-3b634eeec4b8.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686246890566/7f63d408-56a6-476c-8017-7aa71905014b.png align="center")
    
19. Now it's time to run terraform destroy command.👇
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686246920592/d438f3f1-514b-4228-936d-12b1be987b99.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686246932150/62ebe490-4d20-474d-8a72-505fb3a654dd.png align="center")
    
20. Now by refreshing the AWS console of EC2 and S3, you will see that newly created services are now gone.👇
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686247089596/557d4ee0-7f7d-4b44-bb01-e702e5252949.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686247107426/924bef2d-97d0-4af5-bec7-2e5fd4147e97.png align="center")
    

This is how you have created a Terraform configuration file by defining a resource of AWS EC2 instance and S3 bucket.☝️

## Terraform Provisioner to the configuration file🧷

### Provisioning

Suppose you want to install a specific version of Apache **HTTP** Server on an EC2 **instance** created using Terraform. You can use the `remote-exec` provisioner to **SSH** into the instance and run the installation commands:

```bash
resource "aws_instance" "my-instance" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  provisioner "remote-exec" {
    inline = [
      "sudo yum update -y",
      "sudo yum install httpd24 -y"
    ]
  }
}
```

The above code creates an EC2 instance and uses the `remote-exec` provisioner to run the specified commands after the instance is created.

For example, the commands are used to update the instance's packages and install Apache HTTP Server version 2.4.

Alternatively, if you prefer to run the installation commands on your local computer, you can use the `local-exec` provisioner instead:

```bash
resource "aws_instance" "my-instance" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  provisioner "local-exec" {
    command = "bash scripts/install-apache.sh"
  }
}
```

This creates an EC2 instance and uses the `local-exec` provisioner to run a local script called [`install-apache.sh`](http://install-apache.sh). This script can contain any commands needed to install Apache HTTP Server.

## Terraform Lifecycle Management🛟

Now, let's say you want to prevent the accidental destruction of an S3 bucket created using Terraform. You can use the `prevent_destroy` lifecycle configuration to achieve this:

```bash
resource "aws_s3_bucket" "my-bucket" {
  bucket = "my-bucket"

  lifecycle {
    prevent_destroy = true
  }
}
```

This creates an **S3 bucket** and sets the `prevent_destroy` configuration to `true`. This means that Terraform will throw an error if you attempt to destroy the bucket using the `terraform destroy` command.

Similarly, suppose you want to update an RDS instance's backup retention period without replacing the resource.

You can use the `ignore_changes` lifecycle configuration to achieve this:

```bash
resource "aws_db_instance" "my-db" {
  engine           = "mysql"
  instance_class   = "db.t2.micro"
  allocated_storage = 20
  backup_retention_period = 7

  lifecycle {
    ignore_changes = [backup_retention_period]
  }
}
```

This creates an **RDS** instance and sets the `backup_retention_period` configuration to 7 days.

The `ignore_changes` configuration is also included, with the `backup_retention_period` attribute specified.

This means that Terraform will not replace the RDS instance if the `backup_retention_period` configuration is changed.

---

This blog is a part of the 7-day #TerraWeek Challenge initiated by @[Shubham Londhe](@TrainWithShubham) sir!

Thank you!🖤