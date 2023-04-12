---
title: "A SuperHero: LINUX"
datePublished: Thu Mar 23 2023 12:41:07 GMT+0000 (Coordinated Universal Time)
cuid: clfl3qyrx000109le4jopftt0
slug: a-superhero-linux
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679574773557/89feaf78-f459-4dea-9326-73e28d86c60c.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1679575038607/93d5b2b3-377f-4a5c-872b-8c7240faf641.png
tags: blogging, linux, linux-for-beginners, wemakedevs

---

## Introduction

Linux is a powerful and versatile open-source operating system that is a Unix-like os that can be used in a variety of applications, from small-scale personal use to large-scale enterprise use.

It offers many benefits including, stability, security and flexibility, making it a popular choice for many users and organizations.

## Shell

The Linux shell is a program that allows text-based interaction between the user and the operating system.

This interaction is carried out by typing commands into the interface and receiving the response in the same way.

## Types of shell

| **Bourne Shell (sh)** |
| --- |
| **Korn Shell (ksh)** |
| **C Shell (csh or tcsh)** |
| **Z Shell (zsh)** |
| **Bourne again Shell (bash)** |

These shells may differ in their core concepts but all of them have one common thing to communicate between the users and os.

When we log into the shell, the first thing to show up to you is your home directory.

**Home Directory**\- `/home` is a system-created directory that contains the home directories for almost all users in the Linux system.

It allows user to store their personal data in the form of files and folders.

Each user in the system gets their own unique home directory with all access.

**Representation**\- It is represented by the "tilde ~" symbol in the command line.

```plaintext
Home Directory = ~ (tilde)
```

```bash
[~]$
```

## Commands and Arguments

To interact with the Linux system using the shell, a user has to give ***Commands***. Like-

**echo**: to print a line of text on the screen use the `echo` command.

```bash
[~]$ echo
[~]$
```

when you used `echo` cmd, you did not tell what you want to print and as a result, it prints nothing.

That's where an Argument comes into the picture.

An ***Argument*** acts as an input to the command.

```bash
[~]$ echo Hello
Hello
[~]$
```

It's not always necessary to give arguments. There can be a lot of commands which can run without any arguments. eg:

```bash
[~]$ uptime
12:53  up 2 days, 22:05, 3 users, load averages: 2.89 2.61 2.79
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679547595046/b5a47cfc-0d31-4cab-8307-6927d5d48c91.png align="center")

This `uptime` is used to print information about how long the system has been running since the last reboot.

```plaintext
command <arguments>
echo = command
Hello = argument
```

To check your current shell use-

```bash
[~]$ echo $SHELL
/bin/bash
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679551245263/433db67f-8c6b-4d2d-a943-fa970e051817.png align="center")

### Fun Task:

Let's do a quick task with some basic and most important Linux commands so that you can learn by doing.

**Task** - Create a directory structure with 3 directories under the home directory which is already created `/home/dev`. These directories' name represents the categories of animal herbivorous, carnivorous and omnivorous which comes under home dir like `/home/dev/herbivorous` under each category there are some animals and under this some foods. Each item is a directory.

Let me explain this to you more easily with a diagram-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677926532166/dc5b60a0-73a9-4792-bfeb-0a0b29881937.png align="center")

We will be in our home directory by default

```bash
[~]$ pwd
/home/dev
```

`pwd` command prints the present working directory which is `home` in our case and `dev` is our username.

```bash
[~]$ mkdir herbivorous
```

`mkdir` command is used to make a new directory on the given path

```bash
[~]$ mkdir carnivorous omnivorous
```

we can create as many directories as we want by writing them in one go as the above done.

now all three directories have been created in our home path.

```bash
[~]$ ls
herbivorous carnivorous omnivorous
```

`ls` command is used to show the list of files and folders on that particular directory.

Now we have to make directories of `cows` and `giraffes` in the herbivorous directory.

To do this, we have to change our dir from `home` and go inside the `herbivorous` dir.

```bash
[~]$ cd herbivorous
[~/herbivorous]$
```

the `cd` command is used to change the directory.

```bash
[~/herbivorous]$ pwd
/home/dev/herbivorous
```

```bash
[~/herbivorous]$ mkdir cow giraffe
```

```bash
[~/herbivorous]$ mkdir cow/grasses
```

here we made a new directory of `grasses` inside `cow` dir without going inside it.

```bash
[~/herbivorous]$ mkdir -p cow/grasses
```

here we're creating directories cow and under that grasses together by using the `<-p>` option.

Let's check out some more of the basic commands

`mv` This mv command is used to move dir from src A to dest B

```bash
[~]$ mv /home/dev/source_dir /home/dev/destination_dir
```

`cp` This command is used to copy file/dir from one src to another

```bash
$ ls
a.txt  b.txt  new

#Initially new is empty
$ ls new
#empty

$ cp a.txt b.txt new
#copying file a and b a file named new

$ ls new
a.txt  b.txt
```

`rm` This command is used to remove file/dir

```bash
$ ls
a.txt b.txt new
$ rm new
$ ls
a.txt b.txt
# file named new is being removed now
```

`cat` This command can be used in several ways. Some of them are:

```bash
$ cat a.txt
This will show the content of file a.txt
```

```bash
$ cat a.txt > b.txt
This will copy the content of file a.txt to b.txt file
```

```bash
$ cat > newfile
This will create a new file named newfile
```

`touch` This command is used to create a new file

```bash
[~]$ touch /home/dev/omnivorous/human/food.txt
```

### Some Tips:

* The alternative of cd cmd is `pushd` cmd. This cmd remembers the current working directory before changing to the directory you want.
    

let's say you're in home dir and want to go to /etc

```bash
[~] pushd /etc
/etc ~
```

now you can dir as many times as you want `cd /var` `cd /tmp`

and to go back to the original dir use `popd`

```bash
[/tmp] popd
[~]
```

* To change the prompt - If you want to change the way how your prompt look to something else like your server name or your name itself
    

```bash
[~]: echo $PS1
[~]$
# current prompt lool like

[~]$ PS1="ubuntu-server:"
ubuntu-server:
# now it changes to the server name

ubuntu-server: PS1="[\d \t \u@\h:\w ] $ "
[Mon Mar 06 13:30:54 dev@macair:~ ] $
# now displaying with current date and time with user name too
```

date, time and username before '@' and /h /w give the hostname and the present working directory of the user, followed by '$' indicating a regular user.

## Kernel

The major component of the operating system and an interface between the system's hardware and processes.

It can be thought of as a bridge between the hardware and the software components of a computer system.

```bash
[~]$ uname
Linux
```

Let's say you are running a program that needs access to the computer's memory. when the request is made, the kernel is responsible for granting the program access to the memory.

```bash
[~]$ uname -r
4.15.0.72-generic
```

This shows up in the kernel versions.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679550326679/8d8a1096-251d-4920-85d5-369fafcf4949.png align="center")

The kernel looks up the four major tasks-

* Memory Management - Keeps track of how much memory is used.
    
* Process Management - Which process can use the CPU?
    
* Device Drivers - An interpreter between the hardware and the processes.
    
* System Calls & Security - Receive requests for services from the processes.
    

## Some Core Concepts

* File Compression:
    
    To inspect the size of the file use `du` command
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679552290183/ee155d57-ee60-4124-a5cc-41927ee498aa.png align="center")

`du` stands for Disk Usage and `-sh` is a humanly readable size format.

* Archive File:
    
    Grouping multiple files into a single directory or a single file, you can use `tar` command
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679552968328/682bfd52-2237-4097-9c89-2b15a9005d79.png align="center")
    
    `-c` flag specifies that the `tar` should create a new archive.
    
    `-v` flag specifies that the `tar` will display the name of the file added to the archive.
    
    `-f` flag specifies the name of the archive file that `tar` should create.
    
    `-cvf` together, it will create a new archive with the specified name and add the specified files to it while displaying their names as they are added.
    
    `-xf` flag is used to extract the contents from the `tar` file.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679561590561/870edfc0-3410-4fba-9511-7da836472f13.png align="center")
    
    `-czvf` flag is used to compress the tar file to reduce its size.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679562069820/943b05fa-28a6-476b-a149-7ff76959fd5c.png align="center")
    
    the tar archive "mydoc.tar" was created, and its content was compressed using gzip to create a compressed tar archive named "my
    
    ```bash
    $tar -czvf mydoc.tar.gz mydoc/
    mydoc/
    mydoc/file1.txt
    mydoc/file2.txt
    mydoc/file3.txt
    ```
    
    `-c` creates a new archive file.
    
    `-z` compress the archive using gzip.
    
    `-v` displays the verbose output during the creation of the archive.
    
    `-f` specify the name of the archive file.
    

---

source:

[KodeKloud](https://kodekloud.com/courses/the-linux-basics-course/)

[geeksforgeeks](https://www.geeksforgeeks.org/cp-command-linux-examples/)

And that's all for you to start your Linux ride. I have done my certifications in Linux Basics Course from [KodeKloud](https://kodekloud.com/courses/the-linux-basics-course/).

%[https://twitter.com/pawartwt/status/1638837660092342273] 

I am not promoting anything, just sharing my learning resources if you want to check them out.

You can have the training and get certified by Linux Foundation itself.

%[https://twitter.com/LF_Training/status/1601246558720229376] 

---

Thanks for the read!🖤🐧