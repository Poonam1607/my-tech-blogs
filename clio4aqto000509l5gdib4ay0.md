---
title: "Terraform State Management"
datePublished: Fri Jun 09 2023 05:18:56 GMT+0000 (Coordinated Universal Time)
cuid: clio4aqto000509l5gdib4ay0
slug: terraform-state-management
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686287830497/d0aa27de-14bc-4e4d-a824-91acabad0d37.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1686287920718/9956cf5b-ee94-4318-a02e-0a8480c97626.png
tags: devops, terraform, trainwithshubham, terraweek, terraweekchallenge

---

## Introduction✍️

Imagine that you and a teammate are working on creating an infrastructure using Terraform. You both start by creating a `.tf` file, which contains the configuration details of your resources, such as the **instance type, size**, and **number of instances**.

Terraform generates a `.tfstate` file which contains the **current state** of the infrastructure. This **state file** includes information such as the **running state of your resources, their IP addresses, and storage**.

### Problem⁉️

When multiple developers are working on the same infrastructure project.

For example, your teammate decides to add another instance to the infrastructure but forgets to tell you. When they run the command to `apply` the changes, their `.tfstate` file will show two instances running, while your `.tfstate` file still shows only one.

This creates a **conflict** because both state files are different, even though you're working on the same project. If this conflict goes unnoticed, it could lead to serious issues with your infrastructure.

### Solution‼️

This is where **State Management** comes in.

## What is State Management?

In Terraform, state management refers to the process of **managing** and **tracking** the **current** **state** of your infrastructure. To avoid conflicts, you need a proper state management strategy.

By using a **remote backend** or **Terraform Cloud**, you can manage your state files in a centralized location and work collaboratively with your team. This ensures consistency and prevents conflicts in the configuration of your infrastructure.

### Why not GIT?

* GIT is a version control system and you're thinking now, to avoid the conflicts of working with multiple developers, we can use GIT because it keeps track of each and every change.
    
* But we cannot, because, the infrastructure state files have a lot of information about the objects we've created e.g. **access keys, secret values, and private IP addresses of instances**.
    
    If these details get exposed, it could put your infrastructure and data at risk.
    
* Git is only designed to handle source code changes, not the infrastructure state.
    
* Because infrastructure state files can become quite large and complex depending on the size and scale of your project.
    
* Git is not designed to handle these types of large binary files, and can quickly become bloated, slow and difficult to work with as a result.
    

### Remote Backend

* So, you know how when you're working on a project with your team, you need to have a central location to store and share your configuration data so everyone's on the same page? And we just saw above that GIT cannot be the option.
    
* That's where **remote** backends in Terraform come in handy!
    
* Instead of storing your Terraform state file on your **local** machine, remote backends allow you to store it in a cloud storage system like **Amazon S3 or Microsoft Azure**.
    

### State Locking **\-**

* Now, state locking is a cool feature in Terraform that helps to prevent any accidents from happening.
    
* When two or more people are working on the same file at the same time, this can cause **data loss**, incorrect updates or inconsistencies with the state of infrastructure.
    
* To **prevent** this from happening, Terraform has a state-locking feature, which ensures that only one person is changing the file at a time.
    
* When one team member runs the `terraform apply` command, Terraform requests a lock on the state file to make sure that no one else can modify it at the same time.
    
* Once the changes are made, the lock is released so others can make changes.
    

## Other methods of Storing Terraform State file

We saw a method above to store `tfstate` file. There are a few different ways to store Terraform state files. Here are a few examples:

**1\. Locally:** One way to store the state file is on your **local machine**. This is the simplest method but is **not recommended** for production use cases. You can simply specify the path of the state file in your Terraform code and Terraform will generate the state file locally.

```bash
terraform {
  backend "local" {
    path = "relative/path/to/terraform.tfstate"
  }
}
```

**2\. S3 Bucket:** Another option is to store the state file in an **S3 bucket**. This is a great choice when working in production because the S3 bucket can be accessed securely and can handle multiple users accessing it concurrently.

This comes under **remote backend** storage.

```bash
terraform {
  backend "s3" {
    bucket = "my-terraform-state-bucket"
    key    = "terraform.tfstate"
    region = "us-west-2"
  }
}
```

**3\. HashiCorp Consul:** It is possible to store the state file in Consul, a service discovery and orchestration platform. This method is best suited for small teams and projects. And HashiCorp consul is one of the.

```bash
terraform {
  backend "consul" {
    address = "consul.example.com:8500"
    path    = "/terraform/state"
  }
}
```

**4\. Azure Blob Storage:** Azure Blob Storage can also be used to store the state file. This is a good option if you are using **Azure** for your infrastructure.

```bash
terraform {
  backend "azurerm" {
    storage_account_name = "mystorageaccount"
    container_name       = "myterraformstate"
    key                  = "terraform.tfstate"
  }
}
```

As you can see, there are many different options and you can choose the one that best fits your needs and preferences.

## Creating Remote backend storage for `tfstate` files

Now let's jump right into the hands-on part!

1. Again, First thing first, create an **EC2 instance** manually from the **AWS** dashboard with the free tier architecture to perform further procedures on it.
    
2. Copy the **public IP** address of the created instance id👇
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686283319911/9e47baf5-11ea-45fa-9cb0-188c21a6c62e.png align="center")
    
    See☝️
    
3. Run this command to connect the instance to your local system.
    
    ```bash
     $ ssh -i /my-key-pair ubuntu@<ip-add>
    ```
    
    Give the correct path of your **generated key** and provide the correct **IP add**.
    
4. Make sure you've Terraform **installed** in it by running,
    
    ```bash
     $ terraform --version
    ```
    
    And if not, then install it from [**here**](https://developer.hashicorp.com/terraform/downloads).
    
5. Also, check `aws-cli` is **installed** and **configured**.
    
    ```bash
    $ sudo apt install aws cli
    $ aws configure
    ```
    
6. Now firstly, we will look how `.tf` created `.tfstate` file automatically in the local system if not specified.
    
7. Create a directory `remote_infra`
    
    ```bash
    $ mkdir remote_infra
    $ cd remote_infra
    ```
    
8. Now create separate files for `providers`, `resources` and `main.tf` file
    
    ```bash
    provider "aws" {
    	 region = "us-east-1"
    }
    ```
    
    `providers.tf` file☝️
    
    ```bash
    resource "aws_s3_bucket" "my_s3_bucket_2" {
    	bucket = "terraweek-demo-state-bucket-123"
    }
    
    resource "aws_dynamodb_table" "my_dynamo_table" {
    	name = "terraweek-demo-state-table"
    	billing_mode = "PAY_PER_REQUEST"
    	hash_key = "LockID"
    	attribute {
    	name = "LockID"
    	type = "S"
    	}
    }
    ```
    
    `resource.tf` file☝️
    
    ```bash
    terraform {
    	required_providers {
    	aws = {
    	source = "hashicorp/aws"
    	version = "4.66.1"
    }
    }
    }
    ```
    
    `terraform.tf` file☝️
    
9. Now run,
    
    ```bash
    $ terraform init
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686284346765/2b147b0b-3fde-409b-bdff-c569a3d40f48.png align="center")
    
10. Run `terraform plan` and `terraform apply` command to make the changes. And when now you see, a `tfstate` file is created in the same directory
    
    ```bash
    $ ls
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686284448626/df806207-fe69-46f7-9053-1ad7a89e975d.png align="center")
    
11. Now make another directory in which we will make a remote backend so that `tfstate` file will be created on the **AWS S3 bucket**.
    
    ```bash
    $ mkdir remote_demo
    ```
    
12. Here, create the required files.
    
    ```bash
    terraform {
    
    required_providers {
    	aws = {
    	source = "hashicorp/aws"
    	version = "4.66.1"
    	}
     }
    
    backend "s3" {
    	bucket = "terraweek-demo-state-bucket-123"
    	key = "terraform.tfstate"
    	region = "us-east-1"
    	dynamodb_table = "terraweek-demo-state-table"
    }
    }
    ```
    
    `terraform.tf` file☝️
    
    the `bucket` is where the `tfstate` file is going to store, and
    
    `dynamodb_table`: Specifies the name of the **DynamoDB table** to use for state **locking**.
    
    ```bash
    provider "aws" {
    	region = "us-east-1"
    }
    
    resource "aws_instance" "my_ec2_instance" {
    	count = 3
    	ami = "ami-04a0ae173da5807d3"
    	instance_type = "t2.micro"
    	tags = {
    	Name = "terraweek-instance"
    }
    }
    ```
    
    In the above `main.tf` file we're creating three **aws-instance**.☝️
    
13. Now run,
    
    ```bash
    $ terraform init
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686285174497/262c5964-e286-45f0-99bc-88e1718c7b89.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686285195092/98bf01e8-a4d9-4350-8817-6642d89ceb98.png align="center")
    
    You can see the success message!☝️
    
14. Now run,
    
    ```bash
    $ terraform plan
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686285274398/0a0409d5-a30e-4b42-a9ec-79a2337a4f5f.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686285284002/44d17bb1-8dff-47ae-838e-f976acaccbe9.png align="center")
    
    You can see what we are going to do with the infrastructure.☝️
    
15. Now finally run,
    
    ```bash
    $ terraform apply
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686285388973/eff2bb7f-2bc6-43d5-b66b-af88ebc4714a.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686285400082/4d80e5bf-faf5-4ff1-be08-34371febb451.png align="center")
    
    The three instances have been created now.☝️
    
16. Now run the `ls` command and let see `tfstate` file is created or not?
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686285557472/73230a02-e01b-4816-988e-331a65048281.png align="center")
    
    See, there is no file called .tfstate locally.☝️ Let's check the **AWS console** now.
    
17. Go to **S3 buckets** and click on the newly created bucket.👇
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686285721060/f8ca069a-8cc2-4ce5-874e-982648c8a789.png align="center")
    
    Our `.tfstate` file is here!☝️
    
18. Go to the **DynamoDB table** section, you can see the table is created.👇
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686285818286/ce15e783-e81d-4cba-8d9f-83176f4e469d.png align="center")
    
19. By running terraform state list command, you can see the listed state
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686285881762/77a68fed-7060-444d-a535-2b8637790875.png align="center")
    

This is how we can store the Terraform state files remotely.

---

This blog is a part of the 7-day #TerraWeek Challenge initiated by @[Shubham Londhe](@TrainWithShubham) sir!

Thank you!🖤