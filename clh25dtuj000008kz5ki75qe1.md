---
title: "Kubernetes Cluster Maintenance"
datePublished: Sat Apr 29 2023 15:38:41 GMT+0000 (Coordinated Universal Time)
cuid: clh25dtuj000008kz5ki75qe1
slug: kubernetes-cluster-maintenance
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682778120400/99bd053c-b3f5-4c6a-b382-4788018e8625.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1682782679740/7df47307-d184-4453-bb40-7339133b0ff1.png
tags: kubernetes, cluster, trainwithshubham, kubeweek, kubeweekchallenge

---

## Introduction✍️

Till now we have done a lot of things!!🥹

Recap👇

**Kubernetes Installation & Configurations**

**Kubernetes Networking, Workloads, Services**

**Kubernetes Storage & Security**

kudos to you!👏🫡 This is literally a lot...!😮‍💨

By doing all these workloads your cluster is tiered now🤕. You have to give the energy back and make it faster. It is very important to make your **cluster** **healthy😄** and fine.

So it's high time to understand the Kubernetes **cluster** **maintenance** stuff now.

In our today's learning, we will be covering **cluster** **upgradation**, **backing** **up** and **restoring** the data and **scaling** our Kubernetes cluster. So, let's get started!🚀

## Cluster Upgradation♿

* Let's say you are running your application in the Kubernetes cluster having **master** node and **worker** nodes. Pods and replicas are up and running.
    
* Now you want to **upgrade** your nodes. As everyone wants to keep updated themselves and so do the **nodes**.
    
* When a node is in upgradation mode, it generally goes down and is no longer in use. So you cannot keep your master and worker node together in the upgrade state.
    
* So firstly, you will upgrade the **master node**. While it's upgrading, your worker node cannot deploy new pods or do any modifications. The Pods that are running already, only they will be available for the users to access.
    
* Though the users are not going to be impacted as they still have the application up and **running**.
    
* When the master node is done with the upgradation and again up and running, now we can upgrade our **worker nodes**. But in this also, we cannot make worker nodes goes down altogether as this may impact the users who are using the applications.
    
* If we have three Worker nodes in our cluster, they will go one after the other in the upgrade state. When `node01` goes down, the pods and replicas running in that node will shift to the other working nodes for a while ie in `node02` and `node03`.
    
* Then `node02` will go down after `node01` is upgraded and available again for the users. The pod distribution of `node02` will go to `node01` and `node03`.
    
* And the same procedure will follow up to **upgrade** `node03`. This is how we upgrade our cluster in Kubernetes.
    
* There is another way to upgrade the cluster, you can deploy a worker node with the **updated version** into your cluster and shift the workloads of the older one to the new ones then delete the older node. This is how you can achieve the **upgradation**.
    

Now let's do this practically. First, the **master node**:

`kubeadm` which is a tool for managing clusters has an upgrade command that helps in upgrading the clusters. Run:

```bash
kubeadm upgrade plan
```

Run the above command to see the detailed information on the upgrade plan and gives you the information of the upgrade plan if your system is needed.

Then run the `drain` command to make it `un-schedulable`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682770424692/dbe6ed19-800e-4fd4-9c0b-7f3a95b2a9c7.png align="left")

Now install all the packages to use `kubelet` as it is a must in running `controlplane` node:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682770440476/70349103-86bb-433b-9f83-1b14b233a33c.png align="left")

Now, Run the below command to upgrade the version:

```bash
apt-get upgrade -y kubeadm=1.12.0-00
```

Now to `upgrade` the cluster, run:

```bash
kubeadm upgrade apply v1.12.0
```

It will pull the necessary images and upgrade the cluster components.

Now run the below command to see the changes

```bash
systemctl restart kubelet
```

Now it's time to upgrade the **worker node** one at a time. Follow these commands:

```bash
# First move all the workloads of node-1 to the others

$ kubectl drain node-1
# this terminate all the pods from a node & reschedule them on others

$ apt-get upgrade -y kubeadm=1.12.0-00
$ apt-get upgrade -y kubelet=1.12.0-00

$ kubeadm upgrade node config --kubelet-version v1.12.0
# upgrade the node config for the new kubelet version

$ systemctl restart kubelet

# as we marked the node un-schedulable above, wee need to make schedule again
$ kubectl uncordon node-1
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682770205446/c37794f4-b4d9-490a-a3c3-e3dbe6a2bed2.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682770064720/db56372b-296c-430e-adcf-3418312113f8.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682769960745/87c5a777-de04-4d53-b34a-44ef60fcde3d.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682770295309/a71ac012-1ef8-4dd8-afb3-f50489da7e03.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682770479668/92436070-7291-4c78-aad4-9c83602693fb.png align="left")

`kubectl` command will not work on the worker node, it will only work on the master node that's why after applying all the commands come back on the `controlplane` and make the node available again for scheduling.

## Backup & Restore Methods🛗

* We have till now deployed many numbers of applications in the Kubernetes cluster using pods, deployments and services.
    
* So there are many files that are important to be backed up. Like the **ETCD** cluster where all the information about clusters is stored.
    
* **Persistent volumes storage** is where we store the pod's data as we learned above.
    
* You can store all these files in a source code repository like **GitHub** which is a good practice. In this even if you lost your whole cluster you still can deploy it again if you're using GitHub.
    
* A better approach to back up your file is to query the `kube-api` server using the `kubectl` or by accessing the **API server** directly and saving all resource configurations for all objects created on the cluster as a copy.
    
* You can also choose to back up the **ETCD** server itself instead of the files.
    

Like the screenshots on your phone, you take snapshots here of the database by using the `etdctl` utilities `snapshot save` command.

```bash
ETCDCTL_API=3 etcdctl \ snapshot save <name>
```

Now, if you want to restore the snapshot. First, you have to stop the server as the restore process requires the restart `ETCD` cluster and `kube-api` server

```bash
service kube-apiserver stop
```

Then run the `restore` command:

```bash
ETCDCTL_API=3 etcdctl \ snapshot restore <name> \ --data-dir <path>
```

Now `restart` the services which we stopped earlier

```bash
$systemctl daemon-reload
$service etcd restart
$service kube-apiserver start
```

## Scaling Clusters📶

* We have done the scaling of **pods** in the Kubernetes cluster very well. Now what if you want to scale your **cluster**? Let's see how it can be done.
    
* According to the capacity worker nodes adjust themselves by adding or removing from the cluster.
    
* Kubernetes provides several tools and methods for scaling a cluster, like:
    

### Manual Scaling🫥

### Horizontal Pod Autoscaler (HPA)▶️

### Cluster Autoscaler↗️

### Vertical Pod Autoscaler (VPA)⏫

Let's have a look at all one by one

1. **Manual Scaling** - As the name suggests, we have to scale it manually using the `kubectl` command. Or if you're using any cloud provider, increase or decrease the number of worker nodes manually.
    
2. **Horizontal Pod Autoscaler (HPA)** - It automatically scales the number of replicas of a deployment or a replica set based on the observed CPU utilization or other custom metrics.
    
    When defining the definition file, you must ensure the usage of `memory` and `cpu`
    
    To use utilization-based resource scaling, like this:
    
    ```yaml
    type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 60
    ```
    
    This is also known as "scaling out". It involves adding more replicas of a pod to a deployment or replica set to handle the increased load.
    
3. **Cluster Autoscaler** - Based on the pending pods and the available resources in the cluster, it automatically scales the number of worker nodes in a cluster.
    
    Read more about this scaler in detail [here](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler)!
    
4. **Vertical Pod Autoscaler (VPA)**\- It automatically adjusts the resource requests and limits of the containers in a pod based on the observed resource usage.
    
    It is also known as "scaling up," which involves increasing the CPU, memory, or other resources allocated to a single pod.
    

---

Thank you!🖤