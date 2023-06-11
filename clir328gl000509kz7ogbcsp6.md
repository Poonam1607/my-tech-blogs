---
title: "Advance Terraform Concepts"
datePublished: Sun Jun 11 2023 07:07:37 GMT+0000 (Coordinated Universal Time)
cuid: clir328gl000509kz7ogbcsp6
slug: advance-terraform-concepts
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686467048284/081e90be-9682-42e3-9523-1883f8fbc2cb.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1686467234775/bb1cceef-0f1f-492d-a203-d341f45665e8.png
tags: devops, terraform, trainwithshubham, terraweek, terraweekchallenge

---

## Introduction

This particular blog is based on the higher concepts in Terraform that includes workspaces, remote execution, collaboration, cloud, enterprises, registries and some best practices used by Terraform.

Let's get started!

## What are Worksapces?

Ok So Let's start imagining.

You want to create a simple configuration file that creates an EC2 instance in AWS "**us-east-1**" region for a project called **project-a** in a configuration directory.

```bash
resource "aws_instance" "projectA" {
    ami = "ami-0edab43b6fa892279"
    instance_type = "t2.micro"
    tags = {
        Name = "ProjectA"
    }
}
```

Now say, you want to create an instance again but with a different "**ami-id**" for another project in a different directory called **project-b.**

The approach here we follow is to copy and paste the whole configuration file and change it with the respective "**ami-id"**.

```bash
resource "aws_instance" "projectA" {
    ami = "ami-0edab43b6fa892279"
    instance_type = "t2.micro"
    tags = {
        Name = "ProjectA"
    }
}
```

But the main of Terraform or any other IAC tool is to eliminate the repetitive steps and efficiently use the existing code that we saw earlier in the **module's** use case.

So Terraform offers you a feature that allows configuration files within a directory to reuse multiple times in diffenet use cases within the same directory.

This feature is called **workspaces**.

* Workspace is a powerful feature that allows you to manage multiple environments or instances of the same resources within the same directory.
    
* With workspaces, you can create multiple copies of the same configuration and store them under different workspaces, making it easier to manage different environments like development, staging, and production.
    
* You don't need to create separate directories or copies of the configuration files for each environment. Instead, you can use Terraform workspaces to store the state of each environment in a separate workspace.
    

Taking forward the above example, you create a workspace by running,

```bash
$ terraform workspace new ProjectA
Created and switched to workspace "ProjectA"!
```

To list all the workspaces you have, run `list` cmd,

```bash
$ terraform workspace list
default
* ProjectA
```

the `default` workspace is created by default.

`*` sign tells you that you're on **ProjectA** workspace that you just have created.

Now let's see how can we use the workspace for **project-a** and **project-b** environments.

```bash
# variables.tf
variable region {
    default = "us-east-1"
}
variable instance_type {
    default = "t2.micro"
} 
variable ami {
    type = map
    default = {
        "ProjectA" = "ami-0edab43b6fa892279"
        "ProjectB" = "ami-0c2f25c1f66a1ff4d"
    }
}
```

```bash
# main.tf
resource "aws_instance" "projectA" {
    ami = lookup(var.ami, terraform.workspace)
    instance_type = var.instance_type
    tags = {
        Name = terraform.workspace
    }
}
```

Now, if you run `terraform plan` cmd, you can see the instance will be created for **ami-id** of **project-a**.

If you want to create for **project-b** just run,

```bash
$ terraform workspace new ProjectB
Created and switched to workspace "ProjectB"!
```

If you want to go back to **project-a**, then run

```bash
$ terraform worlspace select ProjectA
Switched to workspace "ProjectA"
```

We know that running `.tf` file it will generate `.tfstate`, and where does it get stored? Let's see!

```bash
$ ls
main.tf terraform.tfstate.d variable.tf 
$ tree terraform.tfstate.d/
  |--ProjectA
  |   |-- terraform.tfstate
  |--ProjectB
     |-- terraform.tfstate
```

This is how you can create **workspaces**.

## Remote Execution

* Terraform remote execution simply means you can run your Terraform commands on a different machine or remote server, instead of running them on your local machine.
    
* This is useful when you have a large infrastructure to manage and need the processing power of a more powerful machine.
    
* Terraform **Cloud** is a service that provides you with secure storage for your state files and allows for remote execution of your Terraform commands.
    
* Another option is to use version control systems like **Git**, which allow you to keep track of code changes made by other team members.
    
* You can also store your state files remotely and use **SSH** or Windows Remote Management (**WinRM**) to remotely execute your Terraform commands on machines.
    
* Remote State Storage allows you to store your state files in remote **storage** backends like Amazon S3, Azure Storage, or HashiCorp's Consul.
    

## Power of Collaboration

Collaboration is a powerful aspect of working with Terraform, enabling teams to collectively build and manage infrastructure. Here are some key benefits of collaboration in Terraform:

1. **Shared Understanding**: Collaboration brings diverse perspectives, skills, and expertise together, leading to a shared understanding of infrastructure design, provisioning, and management.
    
2. **Division of Responsibilities**: Different team members can focus on specific aspects of infrastructure provisioning, such as networking, security, or application deployment.
    
3. **Code Review and Validation**: Collaboration allows for code reviews, where team members can provide feedback, suggest improvements, and identify potential issues in the infrastructure code.
    
4. I**nfrastructure as Code (IaC) Sharing**: Collaboration in Terraform enables sharing reusable Infrastructure as Code (IaC) components, such as modules, across teams. It promotes code reuse, standardization, and consistency in infrastructure provisioning.
    

## Best Practices

Sure, here are some quick Terraform best practices:

1. **Code Organization**: Organize your Terraform code into modular components such as modules, resources and variables for easy management, testing, and reuse.
    
2. Avoid duplication of Terraform code and use Terraform modules and workspaces whenever possible.
    
3. **Version Control**: Use a version control system like Git to manage your Terraform code and collaborate with your team.
    
4. Keep the version control rules strict and keep track of changes/commits thoroughly to be able to revert to a previous version if required.
    
5. Keeping the Terraform codebase and infrastructure state files in separate repositories is the best practice.
    
6. Use environment-specific configuration files to avoid hardcoding values and secure sensitive information like credentials and API keys.
    
7. Store your Terraform state files remotely in a secure backend like Terraform Cloud, AWS S3 or Consul, to ensure you don't lose your data.
    
8. **Automate** testing and validation of your Terraform code to identify syntax issues and avoid dependency conflicts.
    
9. **Continuous Integration and Continuous Deployment (CI/CD)**: By ensuring automated testing, validation, and deployment of Terraform code by integrating it with CI/CD pipelines.
    
10. Use tools like Terraform Cloud, Jenkins, GitLab CI/CD or Circle CI to achieve continuous integration and deployment. This will allow developers to find and fix issues before releasing them to production.
    
11. **Document** your Terraform codebase and deployment steps to ensure everyone on the team is aware of what's happening and why it's happening.
    

## Terraform Cloud

* Terraform Cloud is a SaaS platform offered by HashiCorp.
    
* It provides a collaborative environment to manage Terraform code, state, and infrastructure.
    
* With Terraform Cloud, you can store your infrastructure state remotely, share configurations with your team members, and automate your deployment pipeline from a single dashboard.
    
* It also provides features like cost estimation, policy enforcement, and audit logging.
    
* This also includes -
    
    * Remote state management
        
    * Collaboration and access management
        
    * Version control integration
        
    * API-driven infrastructure as code
        

Example,

Let's say you're building a web application that you want to deploy to AWS. With Terraform Cloud, you can write code in Terraform language to define your AWS resources, like EC2 instances, S3 buckets, and more. Once you've written your code in the Terraform language, you can connect to Terraform Cloud and upload the code like till now we have done it.

Log in to Terraform Cloud from here

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686466567890/54f51b84-ffbe-4bc8-be60-0014f199c419.png align="center")](https://app.terraform.io/session)

## Terraform Enterprise

* Terraform Enterprise is an on-premise version of Terraform Cloud.
    
* It can be installed on your own servers and use behind your company's firewall for additional security.
    
* It provides all the features of Terraform Cloud, but it's tailored for enterprise-level infrastructure management.
    
* Terraform Enterprise offers multi-tenancy support, enhanced security controls, and integrations with existing CI/CD pipelines.
    
* This also includes -
    
    * Role-based access control
        
    * LDAP, SSO, and MFA support
        
    * Private networking support
        
    * High availability and scale-out capabilities
        

Example,

Let's say you have a team of developers working on a project that's hosted on GitLab. With Terraform Enterprise, you can integrate GitLab with your instance of Terraform, allowing the team to manage infrastructure as code directly from GitLab. It also provides additional features like audit logging, single sign-on (SSO), and remote state storage.

Learn more about Terraform Enterprise here

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686466654782/13d94bc4-ded5-4513-8e9d-dfeb722b2407.png align="center")](https://developer.hashicorp.com/terraform/enterprise)

## Terraform Registry

* Terraform Registry is a public repository of Terraform modules.
    
* We can use it to share, discover, and reuse code snippets.
    
* It provides an easy way to find pre-built modules for common infrastructure patterns such as Kubernetes clusters, databases, and load balancers.
    
* Terraform Registry integrates seamlessly with Terraform CLI, allowing you to download and use modules directly in your code.
    
* This also includes -
    
    * Searchable module index
        
    * Module versioning and tagging
        
    * Code examples and documentation
        
    * Public and private module availability
        

Example,

Let's say you want to deploy a Kubernetes cluster on Google Cloud Platform. You can search the Terraform Registry for Kubernetes modules that have been developed and contributed by other users. You can use this pre-built codes in your own Terraform configuration file to quickly set up your infrastructure without having to write everything from scratch.

Checkout Terraform Registry by clicking on this image.

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686466753123/160dbb80-628a-433f-b02b-9cd08c3649f4.png align="center")](https://registry.terraform.io/)

---

This blog is a part of the 7-day #TerraWeek Challenge initiated by @[Shubham Londhe](@TrainWithShubham) sir!

Thank you!🖤