---
title: "$ kubectl get cluster  -o architecture"
datePublished: Tue Aug 15 2023 04:38:47 GMT+0000 (Coordinated Universal Time)
cuid: cllbtd6qx000308jo58968tes
slug: kubectl-get-cluster-o-architecture
tags: docker, kubernetes, architecture, components, containers

---

If you have seen the logo of k8s carefully, it's a **Helm of a Ship**, clarifying the concept of steering and **orchestrating** containers within a complex system.

The complete process of automatically deploying and managing the application is known as **Container Orchestration**.

**Kubernetes** provides you with an orchestrating platform through which you can perform these tasks smoothly.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691991448439/4a4591a2-d37c-441a-92d4-df89d5f5db34.png align="center")

Let's dive deep into the ocean of cluster together.🏊🏻🛟

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691867053876/92d75b46-4a2b-479d-b748-7bb85dae6ea1.webp align="left")

### Components -

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691999785169/d6e92e45-4c56-44d0-9639-5c6521593777.png align="center")

Kubernetes architecture consists of two main components:

the **Master Node** and the **Worker Node**.

The **Master** Node is responsible for managing the overall state of the Kubernetes cluster, while the **Worker** Node runs the containerized applications.

Just like there is a control room and many other working rooms in any industry, the master and worker plane is just like that respectively.

### $ kubectl run nginx --replica=2 **— image=nginx**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691991694888/84ee6163-1c96-4956-bdef-bf24d667e45d.png align="center")

When you enter "`$ kubectl run`" cmd, as you can see above, request firsts go to the **API** server which resides on the **control plane**.

Then all three checks start processing and if everything is fine and correct, the API server communicates with the ETCD to store the information in a key-value format.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692001032656/8a65cd46-fea6-484c-b372-f5fdcbb00108.png align="center")

Then the API server sends success response to the client that is "`$ nginx/pod created`"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691987243778/bf6ee0bf-35c5-424d-865a-2eac7bdb220e.png align="center")

### Behind the scene

This is how everything works under the hood👇

Let's see step by step.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692003125152/59e59d45-eaf0-4090-85c1-f938a3b5ad0b.png align="center")

**ETCD** and **Control Manager** are continuously watching to API Server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692001132335/c5c92eb7-3b25-4dbd-90c6-2a183813e983.png align="center")

Controller Manager(**C-M**) watching API Server and noticed that there is a demand for three replicas for a pod, then it informs the **replica set controller** to meet the desired state.☝️

While the scheduler watching the kube-api server, it detects the new configuration done by the replica set controller in etcd through the API server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691984295870/10e0d984-7e04-4f49-9ff9-e284b0d52b85.png align="center")

In the above☝️diagram, the `scheduler` is selecting the perfect fit for the demanded pod.

It will check the CPU, memory, storage, affinity, non-affinity, taints & tolerations as such requirements of the pod.

Now,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691994420995/efea7bde-1fee-4506-9721-72048dde44c2.png align="center")

When a node got selected, the request is redirected from the API server to `kubelet` (agent, resides on worker node) with pod specifications so that it can create the pod.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691994554838/45bed6df-1cc7-43f0-a0d7-524fbfd153f8.png align="center")

If we go deeper inside the kubelet's work, many more things are happening under the hood. Let's see that.

In the above☝️diagram, `kubelet` is now interacting with `containerd` to make things manageable at the kernel level.

In the main architecture diagram, have a look once again, there we have **cri** and **CNI**, both are open standards by Kubernetes itself. We are using **containerd** as **cri** implementation.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692010026020/4320019b-f06d-4fed-8599-8811101ca2e8.png align="center")

CNI uses different networking plugins, such as **Calico**, **Flannel**, **Weave**, and others, to provide network connectivity and isolation for pods.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691984392605/e1075bb9-5c11-4f0f-8abb-c6e1df44a4f0.png align="center")

Meanwhile, CNI is doing its job by setting up all the requirements related to networking (containers joining the network, assigning IP addresses, and routing traffic between containers and to the external world.) in order to achieve communication.

> Note: Container runtime invokes the CNI plugin when a container is added/deleted for it to do the necessary network configurations.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691984422919/c9a13c90-91b5-4df1-b32e-563538543cae.png align="center")

After completion of every process, `containerd` starts initiating the creation of the container.

Throughout this procedure, numerous other components are involved, each of which holds enough value to warrant a dedicated blog post.

* CNI plugins
    
* CRI plugnis
    
* Core/kube DNS
    
* Runc
    
* kube-proxy
    
* cgroups
    
* namespaces
    
* Different types of controllers.
    
* OCI Runtime Specification
    
* Pod Admission
    
* Scheduler — Filtering, Scoring, Selection
    
* image layer Snapshotter
    

---

Thanks for reading the blog. Please let us know if a blog is needed for the above topics. Feel free to hit me up for any AWS/DevOps/Open Source-related discussions. 👋

Manoj Kumar — [LinkedIn.](https://www.linkedin.com/in/musalannagari-manoj-kumar-21601b168/)

Poonam Pawar — [LinkedIn](https://www.linkedin.com/in/poonampawar7/)

**Happy Clustering!!**

![](https://miro.medium.com/v2/resize:fit:852/1*RmYSd1eEwQJod_vac-66Tg.gif align="left")