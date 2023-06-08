---
title: "Terraform Configuration Language"
datePublished: Thu Jun 08 2023 07:24:56 GMT+0000 (Coordinated Universal Time)
cuid: climtcxqv000809ie5bjs45r8
slug: terraform-configuration-language
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686208909548/81a5a942-190e-4981-a8e8-607e4b536f4f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1686209080615/5c14e78c-3da9-4d0d-bdce-957b2030307a.png
tags: devops, terraform, trainwithshubham, terraweek, terraweekchallenge

---

## What is HashiCorp Configuration Language?

* Terraform uses a configuration language called **HCL**, which stands for HashiCorp Configuration Language.
    
* HCL is incredibly easy to understand, even for those who might not have a background in programming or software development.
    
* It's designed to be both human-friendly and machine-readable, so you'll have no trouble understanding the syntax and meaning of your code.
    
* HCL makes it a breeze to define your infrastructure resources and their configurations, ensuring that your resources are deployed and managed exactly as you want them to be.
    
* HCL follows a **declarative** approach. You just need to tell HCL what you need, and it will take care of the complex process of actually setting up those resources in a way that is reliable and easy to manage.
    
* HCL can promote the **reusability** of the code through **modules**.
    
* With modules, you can easily encapsulate and reuse configurations across different projects.
    

### Syntax of HCL

HCL file consists of **blocks** and **arguments.**

```bash
<block> <parameter> {
      key1 = value1
      key2 = value2
}
```

The **block** contains information about the infrastructure platform.

Let's take the example which we did in the previous blog,

```bash
$ mkdir terraform-local 
$ cd terraform-local
```

Now the terraform file `local.tf` looks like this

```bash
resource "local_file" "devops" {
        filename = "/home/ubuntu/terraform-course/terraform-local/devops_automated.txt
        content = "This is the day-1 of terraweek challenge in which we will learn basics of it."
}
```

Let's break down each and every step of it.

* `resource`: This represents the **block** **name**.
    
    This keyword indicates that we are defining a resource block in Terraform.
    
* **Resources** represent infrastructure components that Terraform manages.
    
* `local_file`: local = **provider** & file = **resource**.
    
    This represents the resource type. In this case, it represents a local file that will be created by Terraform.
    
* `devops`: This is the **name** of the resource instance.
    
* It serves as a unique identifier for this specific resource block.
    

Within the resource block, there are two **arguments** specified:

* `filename`: This is the argument that defines the path and name of the file to be created.
    
* In this example, the file will be created at the specified path: `/home/ubuntu/terraform-course/terraform-local/devops_automated.txt`.
    
* `content`: This argument specifies the content that should be written into the file. The provided string will be written as the **content** of the file.
    

The resource block defines the **desired** state of the local file resource. When Terraform is executed, it will ensure that the file specified in the `filename` argument exists with the specified content.

It's worth noting that this is a simplified example and that Terraform supports many other resource types and configuration options.

The provided example demonstrates the basic structure of a resource block in Terraform.

## Variables

* So, variables are like **placeholders** in your Terraform code that allow us to set values that can be used throughout our configuration.
    
* We can use variables to set things like instance types or subnet IDs or to define other dynamic configuration settings.
    

For example, let's say we're creating an **AWS** **instance** in our config.

* We might use variables to specify the region we want to use, the instance type, and the subnet ID.
    
* That way, we can reuse those values in other parts of our configuration too.
    

```bash
variable "instance_type" { description = "Type of EC2 instance" type = string default = "t2.micro" }
```

In this example, we define a variable named "**instance\_type**" of type "**string**" with a default value of "**t2.micro**".

## Datatypes

Data types are just different kinds of data that we can work with in Terraform. There are things like **strings**, **numbers**, and **lists** that we can use to define values for our resources.

Here's an example of how we can define a variable with a data type in HCL in Terraform:

```bash
variable "instance_count" {
  type    = number
  default = 2
}
```

In this example, `instance_count` is a variable of type `number`, and it has a default value of `2`.

We can use this variable throughout our Terraform configuration to create two **instances** of a resource, such as **EC2** instances in **AWS**.

## Expressions

Expressions allow us to perform operations on our variables and data types. We can use expressions to fetch values from AWS resources, **perform mathematical or logical operations, or construct strings and lists**.

Here's an example: let's say we're using a Terraform template file to create a script that we'll use to set up an **S3** **bucket** object.

* We might define variables for the name of our bucket and the environment we're creating it.
    
* Then, we can use an expression to construct the bucket name with those variables.
    
* Plus, we can use that same expression to reference our bucket in other resources we create, so we don't have to copy-paste the same bucket name all over the place.
    

## Terraform Configurations using HCL syntax

Let's practice writing some Terraform configurations using HCL syntax.

Continuing from the previous blog, take the same repository or a new one, your choice and let's create a file called `main.tf`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686168481493/3b9ec734-04c1-4dbb-a05d-c813e8ee21c6.png align="center")

```bash
resource "local_file" "passwords" {
        filename = "/root/pass.txt"
        content = "abcdef"
}
```

In the above configuration, we have made a file of resource type **local** which stores our password.

*Don't take this example seriously to store your password, I am doing it just for the sake of explanation:)*

So, in the **content** section, we have given a random text, which we are defining here as our password.

Now do all the jazz!

```bash
$ terraform init
```

```bash
$ terraform validate
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686168529889/4de71990-d431-432d-ac80-322e3f261e61.png align="center")

```bash
$ terraform plan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686168621821/ae2d69c4-9fe0-4654-b5b3-a86a174f1849.png align="center")

```bash
$ terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686168657748/71f30c09-62fd-4ee3-b077-94985db6d021.png align="center")

Now notice one thing that, while we're performing `terraform plan` and `apply` cmd, our content is visible to us and every detail is printed on the screen.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686168761272/cf95a055-0402-4393-87bb-a1aedf09398b.png align="center")

And imagine, if we have saved our password as content and another developer is performing these steps, then it's a risk of doing it.

So there is another resource type called `local_sensitive_file`

This will hide the content while printing on the screen. To edit the `main.tf` file do changes in it.

```bash
resource "local_sensitive_file" "passwords" { 
       filename = "/root/pass.txt"
       content = "abcdef"
}
```

Now to apply these changes, we have to run `terraform init` cmd again to initialize the changes. And then `terraform plan` and `terraform apply` cmd.

```bash
$ terraform init
```

```bash
$ terraform plan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686168907158/88d4affb-2844-4c67-a2eb-1d328e4824f1.png align="center")

You can see in the planning stage, it will first destroy the `local_file` file because it is not in the configuration now.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686168999044/927b8427-2a61-4809-8276-daa1d7618eb8.png align="center")

And then, it will go into the creation of a new `local_sensitive_file`.

```bash
$ terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686169132640/d8b5b2a3-abc2-4d79-a352-6d9f1ba3f765.png align="center")

Now by running `terraform apply` cmd, it is doing all the changes that we have given to do by **destroying** the previous **resource** `type`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686169196706/bc745f4c-dd35-4a23-9157-42e23ec4be65.png align="center")

And creating the new one of `local_sensitive_file`

Now if you again take a look closely, you can see how the content is **hidden** and showing "**sensitive value"** as a display message.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686169316303/6292d4ce-9725-4eba-acb6-15a249e8641c.png align="center")

Now you can check the changes made that we wanted by running `ls` cmd,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686169381439/b400ed80-a420-401c-aba2-d649a27afa76.png align="center")

We made it with another terraform **configuration** using **HCL** syntax!

### Using `variables.tf` file

Now we will do the same thing but this time by creating a separate file for variables called `variables.tf`

```bash
$ vim variables.tf
variable "file_content" {
  description = "Content of the file"
  type        = string
  default     = "abcdef"
}
```

Let's break down each component:

* `variable`: This keyword is used to declare a variable in Terraform. It indicates that we are defining a new variable.
    
* `file_content`: This is the name of the variable. It is enclosed in double quotes to represent it as a string value.
    
* `description`: This attribute is used to provide a description or explanation of the variable. It is a human-readable string that helps convey the purpose or usage of the variable.
    
* `type`: This attribute specifies the data type of the variable. In this case, the type is set to "`string`", indicating that the variable will hold a string value.
    
* `default`: This attribute sets a default value for the variable. If no value is explicitly provided when running Terraform, the default value will be used. In this example, the default value is set to "`abcdef`".
    

This is the whole process that we did above, it's just this is what we separated from the file from the `content` section.

Now we will change the `main.tf` file

```bash
# Add the required_providers block
terraform {
  required_providers {
    local = {
      source  = "hashicorp/local"
      version = "2.1.0"
    }
  }
}

# Use the local_file resource
resource "local_file" "passwords" {
  filename = "/root/pass.txt"
  content  = var.file_content
}
```

We are using the `required_providers` block and then creating a `local_file` resource in Terraform. Let's go through each step:

1. `terraform` block: This block is used to configure Terraform settings. In this case, it includes the `required_providers` block.
    
2. `required_providers` block: This block specifies the providers required for the Terraform configuration. In the example, the required provider is `local`. It specifies the source as "`hashicorp/local`" and the required `version as "2.1.0"`.
    
3. `resource` block: This block is used to define a resource that Terraform manages. In this example, it creates a `local_file` resource named "passwords".
    
4. `filename` attribute: This attribute specifies the path and filename for the `local` sensitive file to be created. In this case, it is set to `"/root/pass.txt"`.
    
5. `content` attribute: This attribute sets the content of the `local` sensitive file. It references the `var.file_content` variable, which means the value of the `file_content` variable will be used as the content of the file.
    

By using the `required_providers` block, we ensure that the necessary **provider** is available, and then we create a `local_file` resource that represents a file with the specified filename and content.

This is how we can perform the same by using `variables.tf` and `required_providers`

## Terraform with Docker

As we above used and saw the case of `required_providers` block, we will give `docker` as a **provider** here.

```bash
$ mkdir terraform-docker
$ cd terraform-docker
```

```bash
$ vim main.tf
terraform {
        required_providers {
        docker = {
        source = "kreuzwerker/docker"
	version = "2.21.0"
}
}
}

provider "docker" {}

resource "docker_image" "nginx" {
   name         =  "nginx:latest"
   keep_locally = false
}

resource "docker_container" "nginx" {
   image = docker_image.nginx.latest
   name = "nginx-tf"
   ports {
         internal = 80
	 external = 80
}
}
```

Let's go through each step and understand what is happening:

1. `terraform` block: This block specifies the required provider for the configuration. In this case, it declares that the Docker provider is needed. The `required_providers` block specifies the `source` and `version` of the Docker provider.
    
2. `provider "docker"` block: This block declares the Docker provider and configures it to be used in the configuration.
    
3. `resource "docker_image" "nginx"` block: This block defines a Docker image resource named "nginx". It specifies the name of the image as "`nginx:latest`" and sets the `keep_locally` attribute to false, indicating that the image should not be kept locally after use.
    
4. `resource "docker_container" "nginx"` block: This block defines a Docker container resource named "nginx". It uses the Docker image resource defined earlier (`docker_image.nginx.latest`) as the image for the container. It sets the name of the container as "`nginx-tf`".
    
5. `ports` block: This block is nested inside the `docker_container` resource block and specifies the port mappings for the container. It maps the internal `port 80` to the `external port 80`, allowing traffic to access the Nginx web server running inside the container.
    

These configuration blocks work together to define the infrastructure resources (Docker image and container) that Terraform will manage. When you run `terraform apply`, Terraform will create the specified Docker resources based on this configuration.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686207396499/90656b12-cca9-4ed5-9039-38710183b5b9.png align="center")

Now run `terraform init` cmd to **initialize** the change we want.

```bash
$ terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686207489665/9d597b43-f07a-451c-b9ec-16086d286b3e.png align="center")

Now if you try to run `terraform plan` cmd, it will give you an error because we didn't install docker in the system.

So before doing `terraform plan`, run

```bash
$ sudo apt-get install docker.io
```

Now run, `terraform plan` cmd. Again you will see an error that says "**permission denied** **while connecting to the Docker daemon".**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686207672531/971c727f-9a86-4cb2-91a3-d4e8e5caaa20.png align="center")

So, to remove this error give the required **permissions** to the `user`

```bash
sudo chown $USER /var/run/docker.sock
```

Now run `terraform plan` cmd and it will **success** message finally.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686207796443/0f35be25-39b4-4a42-8953-5b295db65b1e.png align="center")

Now run,

```bash
$ terraform apply
```

And you will see "**Apply complete!"** message.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686207874637/854bf43c-024c-4dc0-a56e-33cb87ffc2c1.png align="center")

Now take the correct **public IP address** of your instance from the **instance id** dashboard and open a new browser and you can see the **nginx** is running.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686207989191/aa0dc6ae-8185-4f00-891f-65b706244b44.png align="center")

---

This is a part of the 7-day TerraWeek Challenge initiated by @[Shubham Londhe](@TrainWithShubham) sir.

Thank you!🖤