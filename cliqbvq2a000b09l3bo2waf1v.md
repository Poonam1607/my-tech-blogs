---
title: "Terraform Providers"
datePublished: Sat Jun 10 2023 18:26:44 GMT+0000 (Coordinated Universal Time)
cuid: cliqbvq2a000b09l3bo2waf1v
slug: terraform-providers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686420528533/08e046b6-ad76-4b46-aaae-aed1fe184c8d.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1686421586630/313e9ecf-cb3f-4c43-8620-8caa5c23033d.png
tags: devops, terraform, trainwithshubham, terraweek, terraweekchallenge

---

# What are Terraform Providers?

* As a developer, you might have worked with **APIs** before (but I didn't. Trust me🥲),
    
* But with Terraform providers, you can easily configure and set up infrastructure without needing to write complex API calls.
    
* Providers are like **entities** which are downloaded or installed all the necessary **plugins** which are required in order to interact with the **cloud platforms** once you perform terraform init command automatically.
    
* Terraform is a powerful tool for managing resources across various cloud platforms.
    
* By using it, developers can write code in a **declarative** way that describes the desired state of their infrastructure, and the tool handles the provisioning and configuring resources part on various cloud platforms like **AWS, Azure, GCP,** etc.
    
* Terraform becomes like a Swiss Army Knife🔪 for cloud infrastructure, allowing developers to easily manage complex deployments without having to dive deep into the inner workings of each service's API.
    
* It's like having a handy assistant that can talk to different cloud services on your behalf so you can focus on what really matters, *building great software*.
    

### Example

Let's say you want to create a **virtual machine** on AWS. You would specify the AWS provider in your Terraform configuration, and then in your code, you would simply declare the specific resources (in this case, a virtual machine) you want to create.

Terraform then takes care of making the **API calls** to AWS to create the VM for you, without you needing to worry about how to specifically write those API calls.

Overall, Terraform providers make it simpler for developers to create and manage the infrastructure while **abstracting** away much of the complexity involved in interacting with APIs and different cloud services.

# Comparing the Features, Services & Resources of T-P for various cloud platform

Terraform supports several cloud providers, including **AWS** (Amazon Web Services), **Azure**, Google Cloud Platform (**GCP**), and **DigitalOcean**, among others.

**Click** on the picture👇 to see all the cloud platforms supported by Terraform.

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686406635948/d26f7f35-3c5a-4bf3-b35c-17ab11c6f4ed.png align="center")](https://registry.terraform.io/browse/providers?ajs_aid=422cd352-392b-444b-99ca-c1bf46b03dc2&product_intent=terraform)

```bash
# Just for the sake of writing. Sorry:)
$ alias t-p="terraform provider"
```

## AWS Provider

Let's start with **AWS**!

Till now we have seen many services created in Terraform like **EC2 instances, S3 buckets, DynamoDB tables,** etc.

The AWS provider for Terraform allows you to manage a variety of AWS resources such as **EC2 instances, RDS databases, ELBs,** and much more.

One of the key features of the AWS provider is **Autoscaling**, which allows you to define autoscaling groups and automatically scales resources based on predefined metrics.

**Example**

```bash
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}

# Create a VPC
resource "aws_vpc" "example" {
  cidr_block = "10.0.0.0/16"
}
```

### Configuration and Authentication

* Adding an `access_key`, `secret_key`, and optionally `token`, to the `aws` provider block.
    
    ```bash
    provider "aws" {
      region     = "us-west-2"
      access_key = "my-access-key"
      secret_key = "my-secret-key"
    }
    ```
    
* Adding `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, and `AWS_SESSION_TOKEN` environment variables. The region can be set using the `AWS_REGION` or `AWS_DEFAULT_REGION` environment variables.
    
    ```bash
    $ export AWS_ACCESS_KEY_ID="anaccesskey"
    $ export AWS_SECRET_ACCESS_KEY="asecretkey"
    $ export AWS_REGION="us-west-2"
    ```
    
    For more detail check out here👇
    
    [![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686407401339/62ea7347-1674-4643-90b1-af9701229478.png align="left")](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#authentication-and-configuration)
    

## Azure Provider

Now coming to **Azure**,

The Azure provider for Terraform is designed to manage Azure resources, including **virtual machines, storage accounts, databases,** and much more.

The provider follows the same resource model of Azure which makes it easy to map Terraform configurations to Azure resources.

The Azure provider allows us to do **Multi-Factor** authentication and **RBAC** to secure access to Azure resources.

```bash
# Strongly recommend using the required_providers block to set the
# Azure Provider source and version being used
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=3.0.0"
    }
  }
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}

# Create a resource group
resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "West Europe"
}

# Create a virtual network within the resource group
resource "azurerm_virtual_network" "example" {
  name                = "example-network"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  address_space       = ["10.0.0.0/16"]
}
```

### GCP Provider

Moving on to Google Cloud Platform.

The **GCP** provider allows you to manage resources in the Google Cloud environment, including **Compute Engine instances, Google Kubernetes Engine clusters,** and much more.

With the help of the GCP provider, you can provision and create machine learning models leveraging services such as **AutoML, BigQuery, or TensorFlow**.

**Example**

```bash
provider "google" {
  project     = "my-project-id"
  region      = "us-central1"
}
```

### Digital Ocean Provider

Lastly, we have **Digital Ocean**'s Terraform provider,

It offers features like Kubernetes cluster management with **DOKS** (DigitalOcean Kubernetes Service), the ability to provision load balancers, and health checks for **droplets**.

For more details and to start it for free click [*here*](https://www.digitalocean.com/go/cloud-hosting?utm_campaign=apac_brand_kw_en_cpc&utm_adgroup=digitalocean_droplet_bmm&_keyword=cloud%20digitalocean&_device=c&_adposition=&utm_content=conversion&utm_medium=cpc&utm_source=google&gad=1&gclid=CjwKCAjwvpCkBhB4EiwAujULMkwIZhXLbb-GHbAdITFWeu1aRL3RBgsinaZlB5qtSlM-L46GYUbT1xoCyTsQAvD_BwE).

Overall, all Terraform providers aim to provide comprehensive coverage to manage cloud resources in a consistent and declarative way.

> P.S. I used AWS to create terraform providers, and didn't go through all the platforms. The above note is collected from various resources including [official documentation](https://developer.hashicorp.com/terraform/docs) of terraform. So don't quote me on this. Thank you:)🙂

# Practice T-P on AWS

Now it's time to gain some **hands-on** of it. Yes, obviously we are going to do it in the AWS cloud platform because till now we've done everything on it😅.

1. Log in to the AWS **console**.
    
2. Create an EC2 instance and connect it to your local machine by doing **ssh**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686418888851/6fa8eb77-1211-4c3f-8f69-ccc318571f01.png align="center")
    
3. Now copy that Public **IP** address.
    
4. Go to the **IAM** dashboard, now here can be three scenarios
    
    a) You have a user and access key **already** created.
    
    * If this is the case, then go directly to **step 5.**
        
    
    b) You have a user but **not** an **access** key (which means, you forgot to download the credentials while creating it)
    
    * If this is the case then, click on "**Create Access key"** and get your credentials.
        
    
    c) **No** user, **no** key.
    
    * If this is the key, then click on the **"Add User"** button and perform all the followed up steps in order to generate one.
        
5. Go to your terminal and run,
    
    ```bash
    $ ssh -i /<key-pair-path> ubuntu@<ip-add>
    ```
    
    To **connect** the instance to the local machine.
    
6. Now make a directory using `mkdir` cmd.
    
    ```bash
    $ mkdir terraform-provider
    $ cd terraform-provider
    ```
    
7. Now create a file in which we will define the providers.
    
    ```bash
    $ vim provider.tf
    
    # Authentication using access key
    
    provider "aws" {
    	access_key = "AKIAZDXMNSUCC64NNYJQ"
    	secret_key = "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"
    	region = "us-east-1"
    }
    ```
    
8. Now create another file so that we can perform some actions.
    
    ```bash
    $ vim resource.tf
    
    resource "aws_instance" "practice" {
    	ami = "ami-053b0d53c279acc90"
    	instance_type = "t2.micro" # free tier
    	security_groups = ["default"]
    	key_name = "my-key-pair"
    	tags = {
    		Name = "PracticeInstance"
    	}
    }
    ```
    
9. Now run the `init` command to initialize in order to download and install all the plugins required to run AWS.
    
    ```bash
    $ terraform init
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686419559351/42353905-38d6-4f82-b25a-db27fb8152fc.png align="center")
    
10. Now run `terraform plan` command to see the architecture of our configurations.
    
    ```bash
    $ terraform plan
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686419637796/ac38bf30-99de-4887-8122-3b1aa4d0a2df.png align="center")
    
11. Now to check the **syntax** of everything, run
    
    ```bash
    $ terraform validate
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686419695801/bdf47d71-3222-4f23-ae45-aeff83d1c84f.png align="center")
    
12. Now finally to **apply** and see your changes visually, run
    
    ```bash
    $ terraform apply
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686419764928/8ea3245d-897b-47c0-aec6-6baadbaa5a65.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686419773492/38c593e3-3541-4f5b-aa78-78c031cb8d36.png align="center")
    
13. Now go to the AWS console in the EC2 instance dashboard, you can see there the instance has been created and running.
    
    I am unable to put a screenshot here because I `terraform destroy` without taking ss. Sorry!
    
    But I have done a recording of the whole process, you can check here if you wish to.
    
14. Now, we have to run `terraform destroy`. It's a good practice to do so, it will save you from any accident.🚨💸
    
    ```bash
    $ terraform destroy
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686420057666/95ca4231-985a-4a9b-8159-03f73e6bc5c5.png align="center")
    

Okay! So, we have created a service by using Terraform Providers..

---

This blog is a part of the 7-day #TerraWeek Challenge initiated by @[Shubham Londhe](@TrainWithShubham) sir!

Thank you!🖤