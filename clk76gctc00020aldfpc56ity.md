---
title: "Linux - The HULK of DevOps🏋‍♂️"
datePublished: Sun Jul 16 2023 18:06:17 GMT+0000 (Coordinated Universal Time)
cuid: clk76gctc00020aldfpc56ity
slug: linux-the-hulk-of-devops
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689617048712/db8cee21-c82a-4031-9a26-7372c326b3cf.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689617153575/f8a6811c-1e6d-4787-9dbe-daba7244805b.png
tags: linux, devops, linux-basics, day2, trainwithshubham

---

## Introduction✍️

**Linux** is an absolute powerhouse, just like the mighty **Hulk**!

It can tackle complex tasks with ease, delivering incredible speed and unparalleled reliability.

Although, just like the Hulk, Linux can seem a bit intimidating at first glance.

No need to worry though, its command line interface may seem daunting, but with a bit of practice, you'll find it's incredibly intuitive and user-friendly!

## What is Linux?🐧

> Linux® is an [open-source](https://www.redhat.com/en/topics/open-source/what-is-open-source) operating system (OS). An [operating system](https://www.redhat.com/en/technologies/linux-platforms/old-enterprise-linux) is software that directly manages a system’s hardware and resources, like CPU, memory, and [storage](https://www.redhat.com/en/topics/data-storage/software-defined-storage).

*(source: Internet)*

Let's understand this,

* Linux is a **powerful** and versatile **open-source** operating system.
    
* It's a **Unix**\-like **OS** that can be used in a variety of applications, from small-scale personal use to large-scale enterprise use.
    
* This is the **first** Operating System that becomes **free** for users.
    
* It offers many benefits including, **stability**, **security** and **flexibility**, making it a popular choice for many users and organizations.
    
    %[https://poonam1607.hashnode.dev/a-superhero-linux] 
    

You can also check out my previous blog☝️ which covers the basics.

## Basic Commands🔑

Let's start by doing some tasks directly that will cover a couple of commands itself.

> Note: If you are a Windows or Mac OS user, then you need an account in AWS to play around with Linux. You can use [Killercoda](https://killercoda.com/) also.

### Task-1: Check your present working directory📬

It is very necessary to know where you are right now!

And to check this, there is a command called `pwd` ie, ***Print Working Directory*** will display the present working directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689611094051/69cb8e5b-6f90-4b7a-b7a1-a97d5b66eac8.png align="center")

As you can see in the above picture. Let's break down the words which are newer to you first.

1. **ubuntu**: This refers to the username of the currently logged-in user. In this case, as I am using the AWS EC2 console to play, so the user is "Ubuntu."
    
2. "**@**": This symbol is a separator between the username and the hostname.
    
3. **ip-172-31-86-218**: This is the hostname or the identifier for the specific machine(ubuntu in my case) or system that I have got to log into. This is an IP address or a hostname assigned to that machine.
    
4. `pwd`: This is the command that stands for "**print working directory**." When executed, it displays the absolute path of the current directory.
    
5. `/home/ubuntu`: Where `/home` is the top-level directory in the Linux file system hierarchy. It typically contains user-specific directories, including the home directories for different users.
    
6. So we can look at it based on the output `/home/ubuntu` from the command `pwd`, I am a user named `ubuntu` and I am currently at my `home`.
    

### Task-2: List all the files or directories including hidden files📄

* In your present working directory, there might be some **files** and **folders** present already or you have created some now.
    
* To check those and get **all** of them **listed**, there is a command called `ls` ie **list**, the sub-directories and files available in the present directory.
    
* And there are some hidden files present in the directory by default or you can also create one in order to hide it generally for other reasons.
    

To check those or we can say to list all the files including hidden files and folders, there is a command called `ls -a`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689612543687/e26f1b89-cf87-4452-86a3-5a2d6e96cfb3.png align="center")

In the above picture, you can see, I have a file called `linux.txt1` in my `home` directory.

And see, by running `ls -a` cmd many files showed up that are hidden also.

* When a user account is created, certain files and directories are automatically generated in the user's `home` directory.
    
* These files and directories serve specific purposes and are created by default as part of the user account setup.
    

Let's take a quick look at all those hidden files:

1. `.` and `..`: These entries represent the current directory and the parent directory, respectively. They are automatically present in every directory, including the user's home directory.
    
2. `.bash_logout`, `.bashrc`, and `.profile`: These files contain **configurations** and **settings** for the Bash shell, which is the default command-line interpreter in most Linux distributions.
    
3. `.cache`: This directory is created by the system or certain applications to store **cached** data.
    
4. `.ssh`: This directory is created when **SSH**\-related configurations are set up for the user.
    

### Task-3: Create a nested directory `A/B/C/D/E` 📑

To create a directory there is a command called `mkdir` ie **make directory**.

We can create a directory by running,

```bash
mkdir A
```

And to check this, run `ls` cmd.

```bash
ls
A
```

But in the task, it is saying to create a nested directory `A>B>C>D`. This means if we do `ls` in the `/home` dir it will only display `A` dir and then if we go inside `A` dir will be displaying `B` and respectively.

So we have already created `A` dir now we have to create another inside it.  
We can do this by going inside A and to do so we have cd cmd which will **change** the **directory.**

```bash
$pwd
/home

$ls
A  linux.txt

$cd A

$pwd
A
```

Now, as we are in `A` dir, we can again do `mkdir B` then `cd` to `B` dir then again `mkdir C` then `cd` to `C` dir then again perform `mkdir D`. But this is a repetitive task.

So there is a command called `mkdir -p` and this will do the job that we wanted.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689615304303/c878fb16-bda6-4b90-a7de-abe2b12675e8.png align="center")

In the above picture, I have created `A` and `B` directories in `/home` dir. And did nesting on `B/C/D`.

---

Thank you!🖤