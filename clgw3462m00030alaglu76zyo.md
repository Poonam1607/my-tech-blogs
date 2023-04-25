---
title: "Kubernetes: Architecture, Components, Installation & Configuration"
datePublished: Mon Apr 24 2023 09:48:12 GMT+0000 (Coordinated Universal Time)
cuid: clgw3462m00030alaglu76zyo
slug: kubernetes-architecture-components-installation-configuration
tags: kubernetes, kubernetes-architecture, trainwithshubham, kubeweek, kubeweekchallenge

---

## Introduction🧑‍🦯

There are many ways to learn Kubernetes aka k8s. And one of the best ways to learn is by the official documentation itself. But for very beginners, it gets quite difficult to understand all the terms and technology directly through it.

So, in this blog, I will break it down into as many pieces as I can. I will share how I learn in the simplest form.

### Kubernetes🕸️ -

> Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.

Let me break down this definition.

Container⛴️+ Orchestration🛟

Let's imagine you have your application ready inside the Docker container🐬 to run. Now the next thing that should come to your mind is the further process of deployment, scaling and updating your application.

The complete process of automatically deploying and managing is known as Container Orchestration.

K8s provides you with an orchestration platform through which you can perform these tasks smoothly.

## Architecture👾

Now that you got a basic understanding of what k8s do, let's jump into the architecture of it.

Everything you're seeing in the below architecture is needed to set up your k8s cluster. And before going into the k8s cluster let us first understand the other main components of the architecture.

This includes the two major nodes ie Master node and the Worker node

![What is Kubernetes? and Architecture of Kubernetes - UrClouds](https://urclouds.com/wp-content/uploads/2022/08/Architecture-of-Kubernetes.jpg align="left")

Before figuring out who is the <mark>master</mark> and who is the <mark><s>slave</s></mark> worker node, first, understand all about **<mark>NODES</mark>**.

### Nodes📦 -

A node is a worker machine where we're going to install our k8s and the containers with your application ready will be launched by k8s.

To scale up and down as per the demand there has to be more than one node.

So here Cluster comes!

### Cluster🗂️ -

A cluster is a set of nodes grouped together which will help your application is always running state if other nodes fail to perform.

This means if you have a cluster with multiple nodes running your application inside a container. And if one node goes down then the other one is up and running to save your application from crashing.

### Master Node📑 -

Let's imagine you have a factory where all the machines are placed together in a room and working simultaneously as per the demand and requirements.

Now if you noticed there is always a control room where everything is managed and controlled inside that room. This is the Master Node in our case scenario.

This node keeps an eye about:

* Keeps watches on the nodes in the cluster.
    
* Responsible for the actual orchestration of containers on the worker node.
    
* Information about the member cluster node is stored in it.
    
* Responsible for managing the cluster.
    
* Node monitoring configuration.
    
* Managing workload balance.
    
* Controls the scheduling of containers onto worker nodes.
    
* Provides an API endpoint that can be used to interact with the cluster.
    

### Worker Node🧾 -

The factory room where all the machines are placed to work ie, worker node in our case scenario.

Let's see what the worker nodes do:

* Responsible for running the containers where your application resides.
    
* Receives commands from the master node to run which and when node specifically.
    
* Reports back to the master node of their entire performance structure.
    

## Components🧰

Now let's deep dive into all the components you have seen on the architecture diagram quickly.

1. ### kube-apiserver🔗:
    
    To interact with the k8s cluster, this API server helps to get done all the talks of it. It acts as the front end of the k8s. The command-line interface, management devices, and everything covers under this server.
    
2. ### etcd🖇️:
    
    All data is stored to manage the cluster in the key-value pair format. Basically, it is a backing storage of your k8s cluster. It implements the locks within the cluster to avoid conflicts between multiple nodes and masters.
    
3. ### kube-scheduler🧷:
    
    The distribution of workload and containers is done by the scheduler. It also assigns the container to the correct and required node. When anything goes down it notices and responds to the master and brings up the new container into the node as per the requirements.
    
    All these above components come under the <mark>master node</mark>.
    
4. ### Container runtime📎:
    
    It is the software that is responsible to run the containers eg, Docker.
    
5. ### kubelet🔎:
    
    It is the agent that runs on each node in the cluster.
    
6. ### kube-proxy📈:
    
    This handles network traffic between your containers.
    
    All the above three are the <mark>worker node</mark> category component.
    

## Installation⚙️ & Configuration🌐

To run the Kubernetes cluster in your local machine environment you need pre-requisite software to install.

Let's start with step-by-step guidance:

1. Update your Ubuntu package list:
    
    ```bash
     sudo apt-get update
    ```
    
2. For installing k8s, first you have to Install Docker:
    
    ```bash
     sudo apt install docker.io -y
     sudo systemctl start docker
     sudo systemctl enable docker
    ```
    
3. Install the necessary packages for Kubernetes:
    
    ```bash
     sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
    ```
    
4. Add the Kubernetes signing key:
    
    ```bash
     echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
    ```
    
5. Update the system and install Kubernetes:
    
    ```bash
     sudo apt update -y
     sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
    ```
    
6. Initialize the cluster (Master):
    
    ```bash
     sudo su
     kubeadm init
    ```
    
7. Run this command on the Master Node:
    
    ```bash
     mkdir -p $HOME/.kube
     sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
     sudo chown $(id -u):$(id -g) $HOME/.kube/config
    ```
    
    ```bash
     kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
    ```
    
8. Generate the Token for the configuration of Worker Node:
    
    ```bash
     kubeadm token create --print-join-command
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682358458204/51b49476-b380-4253-86ba-9c208704e58a.png?auto=compress,format&format=webp align="left")
    
    ### Worker Node
    
9. Paste the generated token output in the Worker Node:
    
    ```bash
     sudo su
     ---Paste the Join command on worker node with `--v=5`
    ```
    

Now execute this command in the Master Node :

```bash
kubectl get nodes
```

---

Installation differ with the differnet operating system. If you are using other OS please checkout the steps [here](https://kubernetes.io/docs/setup/)!

---

Thankyou!🖤