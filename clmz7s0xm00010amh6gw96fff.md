---
title: "Sailing Smoothly: Navigating Deployment Strategies for Success"
datePublished: Mon Sep 25 2023 18:20:38 GMT+0000 (Coordinated Universal Time)
cuid: clmz7s0xm00010amh6gw96fff
slug: sailing-smoothly-navigating-deployment-strategies-for-success
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694424861314/3cd9c302-a14a-43ed-9481-5962bcffbbe0.png
tags: deployment, devops, strategies

---

## Introduction

Deployment strategies are like smooth operators of the tech world. They help us introduce cool new stuff to our apps without messing things up for users.

The key? Picking the right strategy **saves** **money**, **minimizes** **risk**, and makes our apps work even **better**.

It's like a secret sauce for hassle-free updates!

## Types of Deployment Strategies

*Whether it's traditional physical servers, virtual machines, containers, or cloud-based resources, deployment strategies are versatile tools to manage updates and new features efficiently. To make the understanding easier, I'll refer to* ***pods*** *as* ***servers***. So, you can tailor deployment strategies to suit your specific server environment, making them applicable across the board.

### All at Once/Recreate Deployment

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693911457596/deca7178-483e-4e0b-9406-ea1f9d65aefe.png align="center")

* **Dangerous** deployment strategy.
    
* All users experience the changes at the same time.
    
* Also known as **Recreate Deployment**.
    
* The new version replaces the old version **entirely**.
    
* No incremental update, the new version is fully created and tested before availability.
    
* Ensures independence and avoids potential issues.
    
* Requires less resources and time compared to Rolling Update.
    

**Process:**

* The update is rolled out to the entire user base.
    
* The old pod is terminated.
    
* The pod with the newer version is created from scratch.
    
* Service and Ingress are updated to point to a new pod.
    
* There is a temporary downtime during recreation.
    

**When to use:**

* Suitable for minor updates with low risk.
    
* Useful when there's **limited time** for testing.
    
* Simplifies the deployment process for smaller updates.
    
* **Development**/Testing environment.
    
* **Limited Resource** - If you have one node that can run only one pod for deployment purposes, then the default rolling update strategy will put the new pod in a **pending** state as per its nature. So recreate will be helpful to use here.
    

**On Failure**: To perform a **Rollback** in the Recreate strategy, you create a new deployment with the previous version of your application and scale down the current deployment to zero replicas.

> ***Rollback*** *is a process that allows you to revert to a previous version of your application when issues or unexpected problems arise with the new version.*

### Ramped/Rolling Update Deployment

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693909649696/71cd254a-d527-4107-a6d0-56349d1ce234.png align="center")

* One-By-One strategy.
    
* Default strategy used by Kubernetes objects.
    
* Update application with zero downtime by gradually replacing old with new pods.
    
* Instead of deploying all at once, the changes are released incrementally to a subset of users before being rolled out to everyone.
    

**Process**:

* Ensures application availability during deployment.
    
* Gradual update of pods without downtime.
    
* New pods are deployed while old ones are gradually scaled down.
    
* By default, **maxUnavailable** and **maxSurge** are set to **25%**
    
    * **maxUnavailable** = How many pods will go down at the same time.
        
        * If you have 4 pods running then 25% of it will go down i.e., 1 pod will **not be available** for the users during the update.
            
    * **maxSurge =** How many additional pods will be created while keeping the desired number of replicas.
        
        * If you have 4 pods as desired replicas, 25% of it will be created at a time and will not exceed the limit of more than 100% i.e., it will not create more than 4 pods.
            
* You can always change the percentage or also, can give a specific number to perform actions based on the number of pods.
    

**When to use**:

* Suitable when continuous updates are needed without causing major disruptions.
    
* Ideal for applications requiring uninterrupted user access during updates.
    

**On Failure -** If the issue is severe or critical, consider rolling back to the previously known good version of your application. As we've considered pods here, this can be done by updating the deployment's replica set to the previous image version.

### Blue-Green Deployment

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693910124577/255e7aed-8c33-4f5f-8765-7e49de0f6d26.png align="center")

* Uses two identical environments - blue and green.
    
* The new version deployed to an inactive environment, tested and switched if successful.
    
* Enables zero-downtime updates and quick rollback if needed.
    

**Process:**

* Both blue and green environments exist.
    
* New version pods are deployed to a green environment.
    
* Service and Ingress send traffic to the blue environment initially.
    
* After testing, the traffic switch is triggered from blue to green.
    
* Green becomes active and blue remains as a backup.
    
* If everything is fine with the new version then the older version is removed after some time and the current (new version) becomes blue.
    

**When to use:**

* Zero Downtime: Best for scenarios demanding seamless updates with no user-facing downtime.
    
* Quick Rollback: Beneficial when immediate rollback to the previous version is required in case of issues.
    

**On Failure -** Rolling back typically involves switching traffic back to the previous "Blue" environment. This can be done by updating the routing or load balancing configuration to direct traffic to the "**Blue**" **environment**.

### Canary Deployment

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693912078171/a46cda3b-a53b-4fd0-ba8e-a58b919adcea.png align="center")

* Controlled strategy for deploying new versions gradually.
    
* Involves releasing updates to a small subset of users.
    

**Process:**

* New version pods are created alongside old ones.
    
* Service and Ingress distribute most traffic to old pods.
    
* A small percentage of traffic is directed to new pods.
    
* The percentage includes some users and more testing team.
    
* User responses and system health are monitored.
    
* Based on success, more traffic is directed to new pods.
    
* If unsuccessful, traffic can be reverted.
    

**When to use:**

* Suitable for gradually exposing new features to a subset of users for testing.
    
* Helpful in reducing risks by testing new versions on a small portion of user traffic.
    

**On Failure -** In this, rolling back usually involves reducing the **percentage** of traffic directed to the new version and increasing the percentage of traffic to the previous version. This is done by adjusting the routing or load-balancing configuration.

### Shadow Deployment

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693037965193/d0cc2d2e-51b3-403b-bb97-a7a05888492a.png?height=650 align="center")

* Technique to test updates without affecting end-users.
    
* New code deployed alongside existing one with a small traffic percentage.
    

**Process:**

1. The new version is deployed alongside the old one, but user traffic doesn't reach it immediately.
    
2. Some user requests are copied to the new version to see how it performs without affecting users.
    
3. Needs careful handling to avoid duplicate requests and manage both versions effectively.
    
4. Helps in testing the stability and performance of the new version in a real environment.
    
5. Setup and management can be tricky and resource-intensive, potentially leading to issues.
    

**When to use:**

* Useful when testing new software versions in a live environment before full release.
    
* To closely monitor the performance, stability, and user experience of the new version.
    
* When you want to minimize the impact of potential issues by isolating new version tests.
    

**On Failure -** In this, rolling back can be as simple as stopping the shadow deployment and ensuring that all traffic is directed back to the original version of the application.

### A/B Deployment:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693037594074/be043730-f420-43a6-9caa-4ca048f44e16.png align="center")

* Release two versions to different user groups for comparison.
    
* Users are divided into groups A and B, each getting a version.
    

**Process:**

1. Users are divided into groups A and B.
    
2. Version A to group A, version B to group B.
    
3. Developers made some specific conditions and parameters to choose users.
    
4. These can be the location of the user or the type of devices, things like this.
    
5. Analyze user behavior and feedback for each version.
    

**When to use:**

* Compare versions to identify the better-performing ones.
    
* Avoid impacting all users with untested changes.
    
* When data analysis is crucial, this lets you compare user behavior and feedback.
    
* When enhancing user interfaces, helps evaluate which version performs better.
    

**On Failure -** In A/B testing, rolling back typically involves disabling the variant (the new version) that was being tested and directing all traffic to the control group (the previous version).

### Feature Toggles

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693037816669/65199d8a-5582-4b1f-9ba6-a009efab5a03.png?height=650 align="center")

* Technique to control feature release without deploying new code.
    
* Enables turning features on or off dynamically.
    

**Process:**

1. Code is written to conditionally enable or disable features.
    
2. Feature toggles are managed through configuration settings.
    
3. Features can be gradually enabled for specific users.
    

**When to use:**

* Controlled Rollouts: Avoid sudden, risky feature releases.
    
* Bug Avoidance: Detect and fix issues before full release.
    
* User-Centric: Prioritize user experience and feedback.
    
* Continuous Delivery: Enable continuous testing and updates.
    

**On Failure** - In this, rollback involves disabling the feature toggle or flag that activated the new feature. This effectively reverts the application to the previous state where the feature was turned off.

### Conclusion

The right strategy can make all the difference. Whether you're going with blue-green deployments, canary releases, or any other strategy, the key lies in continuous evaluation, adaptation, and a willingness to embrace change.

---

Thank you!