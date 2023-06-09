---
title: "Terraform Modules"
datePublished: Fri Jun 09 2023 17:30:39 GMT+0000 (Coordinated Universal Time)
cuid: clioufr0v03zp32nv2i0dgbul
slug: terraform-modules
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686318094436/5b11e63f-1ed7-454b-b3ef-08552688d58f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1686318212779/8112d40c-af2c-4b6a-9d41-ad441a4f20cd.png
tags: devops, terraform, trainwithshubham, terraweek, terraweekchallenge

---

## Why do we need Modules?

Till now we have made many **resource** blocks consisting of aws **instances**, **s3** buckets, **dynamodb** tables, **aws-key-pair** etc.

If we have created multiple instances with different names in the same configuration.

Example,

```bash
resource "aws_instance" "my_instance_1" {
}

resource "aws_key_pair" "my_key" {
}

resource "aws_s3_bucket" "my_bucket" {
}

resource "aws_dynamodb_table" "table_1" {
}

resource "aws_instance" "my_instance-2" {
}
```

These two **ec2** instances must be quite similar which made them duplicate configuration blocks in the above file.

And if it's a scalable project there will be hundreds and thousands of resources imposed in a single file like this which will make it difficult to re-use.

To avoid this, we can separate the configuration blocks into a single file.

```bash
# main.tf
resource "aws_instance" "my_instance-1" {
}
```

```bash
# s3_bucket.tf
resource "aws_s3_bucket" "my_bucket" {
}
```

```bash
# dynamodb_table.tf
resource "aws_dynamodb_table" "table_1" {
}
```

By doing this, it would be much better than the first approach but still, there are a lot of disadvantages it suffers from, like won't able to fix the **complexity** of the file.

Due to complexity, it becomes difficult to **update** the resource. And if you want to share these files then the only way is to **copy** and **paste** and due to this, it limits the reusability of the code.

To overcome these issues we have **modules**.

## What are the Modules in Terraform

Any configuration directory containing a set of configuration files is called a **Module**.

A container for multiple resources that are used together.

Basically an essential tool for building and managing infrastructure configurations in a scalable and efficient way.

Essentially, a module is just a directory containing Terraform files that define a set of configurations for a specific infrastructure resource or set of resources.

By creating modules, you can encapsulate **reusable** infrastructure configuration in a modular and scalable manner, which is especially useful for larger projects.

Modules can be used to group and organize resource configurations, making them easier to manage and reuse.

Example,

```bash
$ pwd
/root/terraform/aws-instance
$ ls
main.tf variable.tf
```

```bash
# main.tf
resource "aws_instance" "my_instance_1" {
   ami = var.ami
   instance_type = var.instance_type
}
```

```bash
# variables.tf
variable ami {
   type = string
   default = "ami-0edab43b6fa892279"
   description = "Ubuntu AMI ID"
}
```

We have a directory `aws-instance` in which two files present one `main.tf` and another `variables.tf` Now if we make a file to create an **ec2** instance in another directory then we don't need to write it from scratch.

```bash
$ mkdir dev-2
main.tf
```

```bash
# main.tf
module "dev-2-instance" {
  source = "../aws-instance"
}
```

By giving the **absolute/relative** path to the source, it will create an instance referring to that file.

## Benefits of using Modules in Terraform

There are a number of benefits to using modules in Terraform. Like,

* It simplifies the code and makes it more **reusable**.
    
* If you have multiple instances of the same resource with different names, modules allow you to avoid duplicating configuration blocks.
    
* This makes it easier to manage and **update** your code since you only need to make changes to the module and all instances using that module will be updated automatically.
    
* Another benefit is that modules help us better organize our code by grouping related resources together in a directory. This makes it easier to navigate your code and maintain it as your infrastructure grows.
    
* It enables to scale the infrastructure deployments efficiently.
    
* By defining infrastructure components as modules, one can easily **replicate** and reuse them to deploy multiple instances of the same resource, such as multiple EC2 instances, databases, or load balancers.
    
* It improves the **maintainability** of the infrastructure code. By separating concerns into modular components, it becomes easier to update, test, and manage different parts of your infrastructure without impacting the entire configuration.
    

## Creating a module configuration in Terraform

To create a module for an **AWS EC2 instance**, we can simply create a new directory for the module and write the configuration code inside those files. Here's an example of what that might look like:

```bash
# modules/aws-ec2-instance/main.tf

resource "aws_instance" "my_ec2_instance" {
  ami           = var.ec2_ami
  instance_type = var.ec2_instance_type
}

variable "ec2_ami" {
  description = "AMI ID for the EC2 instance"
  type        = string
}

variable "ec2_instance_type" {
  description = "EC2 instance type"
  type        = string
}
```

Here, we have a module that defines an AWS EC2 instance. Notice that we've defined the `resource` and `variable` blocks inside the module directory.

Now, to use this module in other parts of your code, you can simply call it like this:

```bash
# main.tf

module "my_ec2_instance" {
  source = "./modules/aws-ec2-instance"

  ec2_ami           = "ami-1234567890"
  ec2_instance_type = "t2.micro"
}
```

As you can see, we're calling the `aws-ec2-instance` module and passing in values for the `ec2_ami` and `ec2_instance_type` variables that are defined in the module.

## Modular Composition & Module Versioning

### Composition

* Modular composition in Terraform is like playing with building blocks.
    
* It refers to the process of combining multiple modules together to create a more complex infrastructure.
    
* You can think of it as building blocks where you can combine smaller modules into larger ones to create a bigger infrastructure.
    
* This is particularly useful for large projects where you might have many different modules for different resources.
    
* This is super handy when you're working on big projects with lots of different resources.
    

### Versioning

* Module versioning is important in Terraform because it helps to avoid any issues that may arise when different versions are used together.
    
* Terraform uses a system called Semantic Versioning to manage module versions.
    
* So when you make changes to a module, you need to update the version number based on the changes you've made.
    
* This way it's easy to keep track of changes and manage dependencies between modules.
    

## Ways to Lock Terraform Module Versions

Terraform provides several options for locking module versions to ensure consistent infrastructure configurations across different environments and team members.

1. One way to achieve this is to use a `version` attribute in the `module` block as shown below:
    
    ```bash
    module "my_s3_bucket" {
      source  = "./modules/s3-bucket"
      version = "=1.0.0"
      bucket_name = "example-bucket"
    }
    ```
    
    In this example, we are locking the `my_s3_bucket` module to the version `1.0.0`. We can update the version number when necessary to ensure that the correct version is used.  
    
    ```bash
    module "ec2_instance" {
      source  = "github.com/example/modules//ec2-instance?ref=v1.0.0"
    }
    ```
    
    This locks the module to version `v1.0.0`.
    
2. **Using version constraints**: Instead of specifying an exact version, you can use version constraints to allow updates within a certain range. For example:
    
    ```bash
    module "ec2_instance" {
      source  = "github.com/example/modules//ec2-instance?ref=~>1.0"
    }
    ```
    
    This allows any version within the `1.0` range but prevents breaking changes.
    
3. **Using version constraints from a module registry**: If you're using a module registry like the Terraform Registry, you can specify version constraints directly in the `version` attribute. For example:
    
    ```bash
    module "ec2_instance" {
      source  = "registry.terraform.io/example/ec2-instance/aws"
      version = "~>1.0"
    }
    ```
    
4. Another way to lock modules is to use a `.terraform.lock.hcl` file, which contains the specific module versions the project requires.
    
    This file is automatically generated and updated by the `terraform init` command and ensures that the specified versions are used consistently across all environments and team members.
    

By using specific versions or version constraints, we can ensure that our infrastructure deployments are consistent and predictable. When we're ready to update a module, one can review the changes in the new version before explicitly updating the version constraint in the configuration.

---

This blog is a part of the 7-day #TerraWeek Challenge initiated by @[Shubham Londhe](@TrainWithShubham) sir!

Thank you!🖤