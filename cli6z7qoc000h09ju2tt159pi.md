---
title: "AWS Project using SHELL SCRIPTING for DevOps"
datePublished: Sun May 28 2023 05:24:32 GMT+0000 (Coordinated Universal Time)
cuid: cli6z7qoc000h09ju2tt159pi
slug: aws-project-using-shell-scripting-for-devops
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1685251401232/4fad1b9b-8f9e-413a-a185-f13448ef1e02.png
tags: aws, devops, shell-script, wemakedevs

---

## Introduction

In the real-world DevOps scenario, The **AWS Resource Tracker** script is widely used to provide an overview of the AWS resources being utilized within an environment.

It aims to help organizations monitor and manage their AWS resources effectively. The script utilizes the AWS Command Line Interface (**CLI**) to fetch information about different AWS services, such as **S3 buckets**, **EC2 instances**, **Lambda functions**, and **IAM users**.

## What does this project do?

By running the AWS Resource Tracker script, users can quickly obtain a list of S3 buckets, EC2 instances, Lambda functions, and IAM users associated with their AWS account.

This information can be valuable for various purposes, including auditing, inventory management, resource optimization, and security assessment.

## Build the project

### Create EC2 Instance

**Step 1**. Go to your **AWS** account and log in, then search for **EC2** Instances in the search bar. Or you can click on the services button that is on the top left corner of your dashboard, from there also you can search for the same.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685244996944/0347ea5d-3f51-4c5b-9aa2-a0ec11ec2c20.png align="center")

Then click on the **Launch Instance** button.

**Step 2**. Give it a **name** of your choice, **ubuntu** as a machine image, select your **key-pair** or create one if not have any. Leave the instance type **t2.micro** ie free tier as the same and click again on the **Launch** Instance button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685250347695/d775983a-5a9e-4593-a03b-10d9f11a9c87.png align="center")

Now you can see your instance up and **running** like this.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685245640059/75f2879e-945e-4423-9b69-60031523c3a0.png align="center")

**Step 3**. Now click on the **instance id** which will give you detailed information about the running instance, there copy the public **IP address**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685246307849/66af37b8-b5af-4f82-a203-976460953c7d.png align="center")

### Run the Instance

**Step 4**. Now open up your **terminal** and run the below command.

```bash
ssh -i /Users/poonampawar/Downloads/my-key-pair.pem ubuntu@ip_add
```

We have to go inside the directory where you have downloaded your **key-pair** and in my case, it is in `/Downloads` folder.

Check yours and give a path accordingly. And don't forget to replace `ip_add` with your copied one. This will take you to the virtual machine which we have created in AWS.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685246506063/5a1e2d81-58b0-4564-8f5b-d226c9417dd7.png align="center")

### Create the Script

**Step 5**. Now create a shell **script** file named `aws_resource_tracker.sh` and copy and paste the below script.

```bash
#########################
# Author: Your Name
# Date: 28/05/23
# Version: v1
#
# This script will report the AWS resource usage
########################

set -x

# AWS S3
# AWS EC2
# AWS Lambda
# AWS IAM Users

# list s3 buckets
echo "Print list of s3 buckets"
aws s3 ls

# list EC2 Instances
echo "Print list of ec2 instances"
aws ec2 describe-instances | jq '.Reservations[].Instances[].InstanceId'

# list lambda
echo "Print list of lambda functions"
aws lambda list-functions

# list IAM Users
echo "Print list of iam users"
aws iam list-users
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685246683899/ee9f6369-e373-428d-b2d3-f99de65a947b.png align="center")

* It is a good convention to always provide your details so that it will make it easier for other developers to contribute if they want to ie, **metadata**.
    
* The command `set -x` is given here in order to **debug** the script, this will print the command which we are running and then prints the output.
    
* The commands `aws s3 ls`, `aws lambda list-functions` and `aws iam list-users` print the information of the given statement.
    
* The command
    
    `aws ec2 describe instances | jq '.Reservations[].Instances[].InstanceId'` will give you all the **Instance IDs** present in your aws in JSON format.
    

### Test the script

**Step 6**. Run the below command to see the output.

```bash
./aws_resource_tracker.sh
```

The output will look like this.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685247220438/89072872-ff5b-4af1-9968-204a8cff51f8.png align="center")

### Apply CronJob

To use cron jobs with your script, you can schedule it to run at specific intervals using the cron syntax. Here's an example of how you can modify your script to use cron jobs:

1. Open a terminal and run the following command to edit the crontab file:
    
    ```bash
    crontab -e
    ```
    
2. If prompted, choose your preferred text editor.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685247405615/97465d5a-7c64-43d3-9cf3-8224a356057b.png align="center")
    
3. Add a new line to the crontab file to schedule your script. For example, to run the script every day at 9 AM, you can add the following line:
    
    ```bash
    0 9 * * * /path/to/your/script.sh
    ```
    
    Modify the path `/path/to/your/script.sh` to the actual path where your script is located.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685248056665/93aed95e-7a50-4b59-b812-c4c343b9bbde.png align="center")
    
4. Save the crontab file and exit the text editor.
    

The above cron expression (`0 9 * * *`) represents the schedule: minute (0), hour (9), any day of the month, any month, and any day of the week. You can customize the schedule based on your requirements using the cron syntax.

By adding this line to the crontab file, your script will be executed automatically according to the defined schedule. The output of the script will be sent to your email address by default, or you can redirect the output to a file if needed.

Make sure that the script is executable (`chmod +x /path/to/your/script.sh`) and that the necessary environment variables and AWS CLI configurations are set up correctly for the script to run successfully within the cron environment.

## Use Cases

1. **Monitoring and auditing**: By running this script periodically using cron jobs, you can monitor and audit your AWS resources. It provides insights into the status and details of different resources, such as S3 buckets, EC2 instances, Lambda functions, and IAM users.
    
2. **Resource inventory**: The script helps in maintaining an up-to-date inventory of your AWS resources. It lists the S3 buckets, EC2 instances, Lambda functions, and IAM users, allowing you to have a clear understanding of what resources exist in your environment.
    
3. **Troubleshooting**: In case of any issues or incidents, this script can be used to quickly gather information about the relevant AWS resources. For example, if there is an issue with an EC2 instance, you can run the script to get the instance ID and other details for further investigation.
    
4. **Automation and reporting**: The script can be integrated into an automated pipeline or workflow to generate regular reports about AWS resource usage. This information can be valuable for tracking costs, resource utilization, and compliance requirements.
    
5. **Scalability and efficiency**: In larger environments with numerous AWS resources, manually retrieving information about each resource can be time-consuming and error-prone. By using this script, you can automate the process and retrieve resource details in a consistent and efficient manner.
    

Overall, this script simplifies the process of gathering information about AWS resources, enhances visibility into your infrastructure, and supports effective management and monitoring of your DevOps environment.

> Resource: For better understanding and visual learning you can check out this tutorial - [https://youtu.be/gx5E47R9fGk](https://youtu.be/gx5E47R9fGk)

---

This project is purely based on my learnings. It may occur error while performing in your setup. If you find any issue with it, feel free to reach out to me.

Thank you🖤!