---
title: "DevOps"
datePublished: Sat Feb 25 2023 10:47:09 GMT+0000 (Coordinated Universal Time)
cuid: clejpzllb000809i88no01wb0
slug: devops
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1677313539547/9ce2be2b-ba43-4ca7-ba45-04a612221437.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1677314717447/ef9bb67d-8953-4ee9-b662-68ee717b08f9.png
tags: devops, hashnode, wemakedevs

---

Those who are new to DevOps, find it quite difficult to know where to start their journey, I find it too. So, In this blog, I'll be sharing all my learnings (pre-requisite) so that you can start yours too and get your basics done.

### **What is DevOps?**

DevOps combines development and operations to increase the efficiency, speed and security of software development, to automate all the processes and delivery compared to the traditional process.

The main key🗝 practices involved in DevOps are:

CI/Cd, IaC, Monitoring and Logging

Let me break down this for you🫵 guys!

> *Development +* *Operations =* ***DevOps***

Development, "**Dev**" is the process of generating code that requires any software to work which involves practices like designing, writing and testing code.

The operation, "**Ops**" is the process of deploying, maintaining and monitoring the software application.

Both teams work closely to ensure that the code is properly integrated with the infrastructure and other components of the system. In DevOps, they work together as a single team to break down the traditional silos between these two groups so that development and operation can be more effective and efficient.

More simply, you can think of it as making a toy house building🏢.

In the making🏗 process, it's a teamwork game to play. You need to work together with your friends to make a strong building with different tools and materials like toy bricks, glue, paint🎨 etc.

DevOps is the same, as working together in a team to build a software program using different tools and techniques like coding, testing and automation.

### **Learning Path:**

Now, the following is the step-by-step learning path to begin your journey:-

**Step 1: Getting started with GIT & GITHUB**

The first and most important tool you have to learn to get started with DevOps is GIT & GITHUB.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677135192699/ad4833d4-ffb5-44dc-9972-9cb0c76f3491.jpeg align="center")

> Learn the fundamentals of version control and collaboration with Git and Github.

**Git**: An open-source distributed version control system that allows developers and operations teams to collaborate and keep records and save the changes made on a project. It's like saving the history of your project so that you can make changes as as many times you want without losing your previous one.

**Github**: A web-based platform that provides hosting for Git repositories and offers additional features for managing software development projects.

I'll not be going into the deep. I'll share the resources at the end instead.

%[https://youtu.be/apGV9Kg7ics] 

**Step 2: Understanding Linux and Shell Scripting**

> Explore the power of the Linux operating system and learn how to automate tasks with shell scripting.

**Linux** is a free and open-source operating system based on Unix os.

**Shell** **Scripting** is a way of writing programs that can be run on a Linux or Unix command-line interface, called a shell.

**Step 3: Programming Fundamentals with Golang and Python**

The next step is to learn a programming language, don't worry, you don't have to master anyone. Just for getting started you must know the basics of these.

> Learn these two popular programming languages for DevOps and how they can be used to automate infrastructure and application deployments.

```go
# This program prints Hello, world!
package main
import "fmt"

func main() {
  fmt.Println("Hello World!")
}
```

**Step 4: Building and Deploying applications with Docker**

![An illustration of a docker container ](https://www.devteam.space/wp-content/uploads/2017/03/01-docker-container-min.jpg align="center")

> Learn how to package, deploy and manage applications with a docker container.

**Docker** is an essential tool in DevOps. It allows developers to package and deploy their applications using containerization technology.

Docker Deployment of your application:

![cports_800-min](https://www.devteam.space/wp-content/uploads/2022/07/cports_800-min.jpg align="center")

**Step 5: Automating workflows with Jenkins**

> Master the basics of CI and learn how to automate builds, tests, and deploy with Jenkins.

![Creating new item on Jenkins Dashboard to set up Job](https://browserstack.wpenginepowered.com/wp-content/uploads/2022/09/Creating-new-item-on-Jenkins-Dashboard-to-set-up-Job.png align="center")

**Jenkin** is an open-source automation server that supports continuous integration(CI) and continuous delivery(CD) workflows which enables teams to automatically build, test and deploy their code.

**Step 6: Orchestrating with Kubernetes**

> Dive into the world of orchestration and learn how to deploy, scale and manage containerized applications across the cluster of servers.

**Kubernetes** was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF). It is an open-source platform for managing and orchestrating containerized applications.

![images/flower.svg](https://d33wubrfki0l68.cloudfront.net/69e55f968a6f44613384615c6a78b881bfe28bd6/42cd3/_common-resources/images/flower.svg align="left")

Click here to: [Learn Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-interactive/)

resource: [https://kubernetes.io/](https://kubernetes.io/)

**Step 7: Infrastructure as Code with Ansible**

> Explore the power of configuration management and learn how to automate infrastructure with Ansible.

**Ansible** is a configuration management tool that allows you to define infrastructure as code and automate tasks such as configuration updates, software installation and system updates. It is a "push-based" configuration model.

```plaintext
sudo apt update sudo apt install software-properties-common sudo add-apt-repository --yes --update ppa:ansible/ansible sudo apt install ansible
```

To master the configuration management tools like Ansible, check out this amazing article packed with a complete tutorial from zero to hero knowledge in it by [**Ioannis Moustakis**](https://spacelift.io/blog/author/ionannism)

%[https://spacelift.io/blog/ansible-tutorial] 

**Step 8: Provisioning cloud resources with Terraform**

> Discover how to define, provision and manage infrastructure with Terraform, a popular tool for infrastructure as code.

**Terraform** is a tool for the provisioning and management of cloud resources that allows you to create, update and destroy cloud resources such as virtual machines, databases and storage services.

%[https://youtu.be/l5k1ai_GBDE] 

**Step 9: Automating configuration with Chef and Puppet**

> Learn how to automate server configurations with two popular configuration tools, Chef and Puppet.

Both have similar functionality used for automating the deployment and configuration of infrastructure. Chef is a *Ruby-based* system automation-friendly. The automation tool used to configure, manage, deploy and orchestrate applications. These are "pull-based" configuration models.

**Step 10: Integrating Security into DevOps with DevSecOps**

> Understand the principles of DevSecOps and how to integrate security into your DevOps workflow.

An approach to software development that integrates building security controls into every stage of the software development lifecycle from development and testing to deployment and operations.

That's all to get your basics done.

This is not the exact path you have to follow, you can jumble. There are a lot of tools out there to learn for DevOps, once you start your journey you get to know about many more. I have just given you one way of learning. Start your journey and find your own way.

### **Learning Project Ideas:**

Some beginner-level project ideas that you should do while learning~

1. **System Monitor** - Develop a shell script that monitors system usage such as CPU, memory, and disk usage. It can send an alert to the user when certain thresholds are reached.
    
2. **Multi-container** application with Docker Compose - Create a multi-container application using docker-compose, which allows you to define and run a multi-docker container as a single service.
    
3. **Load-balancing with Kubernetes** - Configure load balancing for a Kubernetes cluster by creating a service that distributes traffic across multiple pods.
    
4. **Ansible playbook for security hardening** - Develop an ansible playbook that automates security hardening tasks, such as disabling unnecessary services and setting up firewalls.
    
5. **Jenkins pipeline** - Create a Jenkins pipeline that automates the entire software delivery process including building, testing and deploying applications.
    

### **Learning Resources:**

There are a few free amazing resources that you must check out and get started with:

* Kunal Kushwaha: This is an amazing free DevOps boot camp by @[Kunal Kushwaha](@kunalk) on his [youtube channel](https://youtube.com/playlist?list=PL9gnSGHSqcnoqBXdMwUTRod4Gi3eac2Ak) to get started with.
    
* TechWorld with Nana: To learn basic concepts of various tools, you can check this [youtube channel](https://www.youtube.com/@TechWorldwithNana/featured).
    
* That DevOps Guy: This [youtube channel](https://www.youtube.com/results?search_query=that+devops+guy) is completely based on DevOps learnings by MarcelDempers.
    
* Pradumna Saraf: This is one of the best resources by @[Pradumna Saraf](@Pradumnasaraf) you can find on his [GitHub](https://github.com/Pradumnasaraf/DevOps/blob/main/Kubernetes/README.md) to get notes, play labs or anything else to get started.
    

Sometimes it becomes quite difficult to set up systems for running DevOps tools getting head clear with the doubts. So a paid course can also be an option in this scenario.

* Kodekloud: This is one of the best [DevOps course](https://kodekloud.com/)s out there by Mumshad Mannambeth. They have hands-on lab practices after lecture videos and also have a playground where you can do whatever you have learned through the lectures. And that's what I'm doing too.
    
* TechWorld with Nana: Another amazing paid course by Nana you can do.
    
    Check out the course [here](https://www.techworld-with-nana.com/devops-bootcamp)!
    

%[https://github.com/EddieHubCommunity] 

Join this amazing GitHub community to get started with your open-source journey while learning DevOps to grow faster. They welcome newcomers open handedly.

> **Learn** -&gt; **Contribute** -&gt; **Collaborate** -&gt; **Grow**

That's All!! GO🏄‍♀️ and start your DevOps journey today!!

---

This blog is written for the hashnode blogging challenge on track DevOps organized by #wemakedevs. ThankYou @[Kunal Kushwaha](@kunalk) for giving this motivation to write blogs!