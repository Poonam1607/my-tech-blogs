---
title: "Introduction to Terraform"
datePublished: Wed Jun 07 2023 06:22:30 GMT+0000 (Coordinated Universal Time)
cuid: clilbosif000608lg10q2888s
slug: introduction-to-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686113067205/972f4d37-0270-4aba-b875-17be5e0a8718.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1687846191504/2971e9e4-cf40-4c6b-9bbe-5459b5ba6874.png
tags: devops, terraform, devops-tools, wemakedevs, terraweek

---

## Introduction🧑‍🦯

Once your code base is ready for your project, it must be **delivered** to the customer/users smoothly. And make sure the **continuing** the delivery process is going on.

For the sake of an example, WhatsApp📞 is your project, you are the founder🥸 of it. You made a fantastic chatting application with many features. Your source code and everything are ready in your local system, and the only thing left is users using your application. So there is a whole **infrastructure** to be set up in order to deliver your application. And also once you delivered your project and made it live, you have to be there to serve continuously to the customers.

## Traditional IT Infrastructure Model👴

So let's go back in time and see how **continuous delivery** works as a traditional model.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686112010108/3b762b33-450d-49c9-98f4-313f5143c050.png align="center")

*(pics credit: kodekloud)*

Different teams do different jobs. Like, a **business analyst** gathers the whole requirements by analyzing them. Then with the given requirements, the **solution architects** design the architecture of the deployment process of the application. All the hardware requirements need to be ordered way before months. And to reach these in the data center takes months. Then every process of **installation**, **configuration**, and **allotting storage** takes place.

This traditional process takes a lot of time to deliver the application. This model has many **disadvantages** in itself like,

* **Slow Deployment**: Deployments take weeks and even months just to give everything to the deployment team in order to serve the customers.
    
* **Scaling**: Scaling up and down as per the demand cannot achieve quickly.
    
* **Expense**: It increases the expense of the developer because purchasing servers, hardware, storage spaces etc has to be taken care of.
    
* **Limited Automation**: While some aspects can be automated but still there are many things that can only be done by manual process.
    
* **Human Errors**: As many teams are working in many different aspects, the chances of occurring errors are high.
    
* **Wasted Resources**: Everything needs to order previously, like if you have purchased storage of 10GB and the time of utilization, it occupied only 7GB, then you're unintentionally wasting resources.
    

To overcome all these problems, every organization is moving to **virtualization** and **cloud platforms**. There are many cloud providers, the popular ones are **AWS**, **GCP**, and **Azure**.

These provide you with many services like **time reductions**. You now don't have to manage all the hardware installations and configurations by yourself. Everything has been taken care of by the cloud providers.

It reduces the **delivery time** from weeks to just a matter of minutes. By using this, the manual approach is vanish and it deducted the human errors. It supports **auto-scaling** up and down as per the demand which solves the **resource wastage** issue.

But still, using the management console of the cloud providers is not the ideal solution. This can be good enough with limited resources but not with highly scalable organizations. Because it still goes through many teams which increases time and error as well.

Many organizations solve this problem by writing their own scripts in Python, Shell etc. These evolve to be a set of code called **Infrastructure as Code**.

## What is Infrastructure as Code?♾️

We discussed above the use of management consoles of different cloud providers. By making all the processes of **defining, provisioning, configuring, updating and destroying** inside a block, a set of code which includes the whole infrastructure known as Infrastructure as Code or **IaC**.

The code is written in a **shell script** which is not a human-friendly readable format and is difficult to manage it. It requires a skill set in order to use it. And this is where tools like Terraform and Ansible come into the picture.

There are human-friendly readable terraform configuration files with the `.tf` extension which is easy to learn and maintain the code base.

There are many IAC tools in the market with specific use cases of it. Although you can use any of them as IAC there are key differences that make every tool different from others. There are three major categories of it

| Configuration Management | Server Templating | Provisioning Tools |
| --- | --- | --- |
| Ansible | Docker | Terraform |
| Puppet | Packer | CloudFormation |
| SaltStack | Vagrant |  |

This is a terraform learning, so we will not go on the other tools, we'll stick to Terraform only.

Provisioning tools are used to provision infrastructure components using a simple code base.

While **CloudFormation** is specifically used to deploy services on AWS, **Terraform** supports almost all the major cloud providers.

## What & Why Terraform?☦️

* Terraform is a **free** and **open-source** IAC tool developed by **HashiCorp**.
    
* It installs as a **single binary** which is easy to set up.
    
* It allows the infrastructure to deploy across many **cloud** and **on-premise** platforms.
    
* Providers help Terraform to manage these platforms through their **APIs**.
    
* Terraform enables you to define your infrastructure requirements and desired state using simple and easy-to-understand configuration files.
    
* With Terraform, you can **automate** the deployment and management of infrastructure resources, as well as define all the required dependencies and relationships between resources.
    

## Key Concepts & Components of Terraform🔐

* Terraform supports **HCL** ie, HashiCorp Configuration Language, which is a simple **declarative language** to define infrastructure as a block of code.
    
* There are two states, **desired** state and the **current** state. The desired state is the state in which we declare the resources we want in our infra. And the current state gives you the information which our state is currently.
    
* Every **object** in the terraform is called a **Resource**.
    
* A resource is a basic building block of Terraform. It represents a physical or logical component of your infrastructure like a virtual machine, database server, or network interface.
    
* The resource can be **EC2 instances, S3 buckets, ECS, DynamoDB tables, IM users, groups, policies** etc.
    
* Terraform allows you to create **reusable** infrastructures as code modules that can be shared across different teams, projects, and organizations called **Modules**.
    
* Terraform has a life cycle containing three phases, **terraform init**, **terraform plan** and **terraform apply**.
    
* `terraform init` **initializes** the project and identifies the providers which are going to be used.
    
* `terraform plan` phase plans the structure to meet the desired state.
    
* Terraform generates an execution plan that outlines the changes to be made to your infrastructure to move from the current state to the desired state. This helps you avoid mistakes and minimize disruptions to your infrastructure during updates.
    
* `terraform apply` command applies all the changes to complete the target state.
    
* Terraform records every change in a file with the `.tfstate` extension
    

All these above points make Terraform an outstanding infrastructure provisioning tool to use.

## Installing Terraform🛠️

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686077239745/770bc3c1-6b2d-4eb6-bc25-50aa748a29dc.png align="center")](https://developer.hashicorp.com/terraform/downloads)

Install Terraform by selecting your specific machine requirements. Everything is given on the official page you can refer to it by clicking the above picture.

After installing Terraform, run this command:

```bash
$ terraform --version
Terraform v1.4.6
on linux_amd64
```

You will get the output like this.

## Creating Terraform Configuration💻

* Now, firstly we will create folders and files manually by using the `mkdir` cmd then we will perform the same steps with the terraform to automate the process.
    
* By doing this we will create our first terraform **configuration**.
    
* If you're using a cloud provider like **AWS** to create **instances** then run:
    
    ```bash
    ssh -i "my-key-pair.pem" ubuntu@172.31.93.241
    ```
    
* `my-key-pair.pem` is the key that I generated while creating instances. Give the correct path where you have downloaded your **generated key**.
    
* Give the correct **IP address** which will show in your instance id dashboard.
    
* Now, create a folder using the `mkdir` cmd.
    
    ```bash
    ubuntu@172.31.93.241: mkdir terraform-course
    ```
    
* Now change the directory,
    
    ```bash
    ubuntu@172.31.93.241: cd terraform-course
    ```
    
* Now inside this directory create a file using `vim` cmd.
    
    ```bash
    ubuntu@172.31.93.241:~/terraform-course$ vim devops.txt
    ```
    
* By doing this a text editor will open up and write some text.
    
    ```bash
    This is the file we are creating manually.
    Next are going to automate this process by using terraform.
    -
    -
    -
    :wq!
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686109991909/88ba0283-517e-4b2b-a69d-3f125811f73d.png align="center")
    
* Now in the same directory make another folder by running `mkdir` cmd
    
    ```bash
    ubuntu@172.31.93.241:~/terraform-course$ mkdir terraform-local
    ```
    
* Change the directory by using `cd` cmd.
    
    ```bash
    ubuntu@172.31.93.241:~/terraform-course$ cd terraform-local
    ubuntu@172.31.93.241:~/terraform-course/terraform-local$
    ```
    
* Now we will create a terraform file with `.tf` extension and inside that, we will write content in **HCL** ie, HashiCorp Configuration Language.
    
* It is very much similar to **JSON**. It is in the form of **key-value** pair. We will look at this in the upcoming topics.
    
    ```bash
    ubuntu@172.31.93.241:~/terraform-course/terraform-local$ vim local.tf
    ```
    
* Inside this file, write this content
    
    ```bash
    resource "local_file" "devops" {
            filename = "/home/ubuntu/terraform-course/terraform-local/devops_automated.txt
            content = "This is the day-1 of terraweek challenge in which we will learn basics of it."
    }
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686110084384/9f15901c-725a-45e3-83a1-d19639e8333e.png align="center")
    
* `"local_file"`: This is the resource **type**.
    
* `"devops"`: This is the **name** of the resource instance.
    
* In the filename section give the correct path where you have to create the `devops_automated.txt` file
    
* You can check your path by running the `pwd` cmd.
    
* Now, after creating this terraform file, it's time to initialize this working directory.
    
    ```bash
    ubuntu@172.31.93.241:~/terraform-course/terraform-local$ terraform init
    ```
    
* After running this `init` cmd you will see the output like this
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686110158883/21d366b9-c950-4dd3-b24f-2e98b278ca9b.png align="center")
    
* Now run the `terraform validate` cmd to check the validation of the **syntax** and configuration of Terraform files.
    
    ```bash
    ubuntu@172.31.93.241:~/terraform-course/terraform-local$ terraform validate
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686110206833/292a511e-7ac3-4a7f-8603-8203486087f3.png align="center")
    
* Now, to examine the current state, compares it with the desired state defined in the configuration files, and generates a plan that outlines the proposed changes by running `terraform plan` cmd.
    
    ```bash
    ubuntu@172.31.93.241:~/terraform-course/terraform-local$ terraform plan
    ```
    
* Now finally to execute the planned changes, provisions or modifies the resources, and update the Terraform state accordingly run the `apply` cmd.
    
    ```bash
    ubuntu@172.31.93.241:~/terraform-course/terraform-local$ terraform apply
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686110367988/7f050de4-1760-4bcf-ad53-f7855e9e0717.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686110390414/ee3b9b8a-aabd-43c4-961a-f61008620356.png align="center")
    
* Now to check our execution run the `ls` command. And you will see output like this.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686110419795/0a09a19f-a7eb-4488-8547-f7a907a30a75.png align="center")
    
* Here you can see the file `devops_automated.txt` has been created.
    

### Congratulations!🎉 You have made your first terraform configuration.👍

## Important Terminologies in Terraform

Important terminologies in Terraform along with examples:

1. Resource:
    
    * A resource represents an infrastructure component that Terraform manages, such as an AWS EC2 instance, an Azure virtual machine, or a Google Cloud Storage bucket.
        
    * Example:
        
        ```bash
        resource "aws_instance" "example" {
          ami           = "ami-0123456789"
          instance_type = "t2.micro"
        }
        ```
        
        In this example, the resource type is "aws\_instance" representing an EC2 instance, and the resource label is "example".
        
2. Provider:
    
    * A provider is responsible for managing and interacting with a specific infrastructure platform or service, such as AWS, Azure, or Google Cloud Platform.
        
    * Example:
        
        ```bash
        provider "aws" {
          region = "us-west-2"
        }
        ```
        
        This example configures the AWS provider with the specified region.
        
3. Variable:
    
    * A variable allows you to parameterize your Terraform configuration and provide flexibility. Variables can be defined to accept different values based on the environment or specific requirements.
        
    * Example:
        
        ```bash
        variable "instance_count" {
          description = "Number of EC2 instances"
          default     = 1
        }
        ```
        
        This example defines a variable named "instance\_count" with a default value of 1.
        
4. Output:
    
    * An output allows you to define values that are exposed to the user once the Terraform configuration is applied. Outputs are typically used to display information or provide data to other systems.
        
    * Example:
        
        ```bash
        output "instance_ip" {
          value       = aws_instance.example.private_ip
          description = "Private IP address of the EC2 instance"
        }
        ```
        
        This example defines an output named "instance\_ip" that retrieves the private IP address of the "aws\_instance" resource.
        
5. Module:
    
    * A module is a self-contained and reusable Terraform configuration that encapsulates a set of resources and their dependencies. Modules promote code reusability, and modularity, and help organize complex configurations.
        
    * Example:
        
        ```bash
        module "vpc" {
          source = "./vpc"
          region = "us-west-2"
        }
        ```
        
        In this example, a module named "vpc" is instantiated using the configuration defined in the "./vpc" directory.
        

These terminologies are fundamental to understanding and working with Terraform. They provide the building blocks for defining and managing infrastructure-as-code configurations in a flexible and scalable manner.

If you are not getting the examples then don't worry we will understand all of these things in the upcoming blogs. I have given examples just for the sake of explanation.

---

Thank you🖤!