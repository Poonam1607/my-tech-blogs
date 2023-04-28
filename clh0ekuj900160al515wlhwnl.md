---
title: "Kubernetes PODS & SERVICES Discovery"
datePublished: Thu Apr 27 2023 10:20:20 GMT+0000 (Coordinated Universal Time)
cuid: clh0ekuj900160al515wlhwnl
slug: kubernetes-pods-services-discovery
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682677104782/e328fc94-0921-42f1-ae30-600f966b58a9.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1682677194031/6deb6688-c53e-464c-ae57-0225c5695b55.png
tags: kubernetes, devops, trainwithshubham, kubeweek, kubeweekchallenge

---

# Introduction✍️

In the previous blogs, we have learned about different kinds of k8s workloads. We have covered the topics of Services, Ingress, DNS etc for **networking**. We have also seen how the Deployments, ReplicaSets, StatefulSets, DaemonSets, Jobs and CronJobs can be created.🫡

Now in this particular blog, we are going to talk about how all these **workloads** can be **exposed** outside to the world with the help of these **Services** and **DNS**. So that external users can also access your application.

# How to expose Kubernetes workloads to the outside world using Services?🌏

Before heading to these topics you must have the knowledge of all the **workloads**.

## Pre-requisites👇

### PODS📦

### DNS🧑‍💻

### Services⚙️

Services are available in three main types:

* ClusterIP
    
* NodePort
    
* LoadBalancer
    

**ClusterIP** is the default service created by k8s. With the help of this type, you can access your application just within your cluster. It will provide you with the benefit of load balancing and discovery, which we will learn about in the below section in detail.

If you want to check all your created services, use `get` command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682671189979/aad8804f-fd93-4623-80c4-fbcfd5436780.png align="left")

Also, you can write with the alias:

`kubectl` aka `k`

`services` aka `svc`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682671317544/9efa942f-c56b-4f29-aaee-20bbeeacbf79.png align="left")

Trust me, this saves a lot of time.🥺

And also, I have covered the file creation already in detail.

**NodePort** can provide you to access your application within the cluster as well as to those who have access to the worker nodes you have set up during the creation.

Creating a `service` of `NodePort` type, the `/root/service-definition-1.yaml` file as follows:

```yaml
---
apiVersion: v1
kind: Service
metadata:
  name: webapp-service
  namespace: default
spec:
  ports:
  - nodePort: 30080
    port: 8080
    targetPort: 8080
  selector:
    name: simple-webapp
  type: NodePort
```

Run the following command to create a `webapp-service` service as follows: -

```sh
kubectl apply -f /root/service-definition-1.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682671387235/91895839-0e52-4abb-9c90-2dd34136fc91.png align="left")

> *Create the service-definition-1.yaml -&gt; Add the service template using* `vi/vim` *\-&gt; Edit the details in the file -&gt; Use command* `apply` *to create it*

I am not going into details about the types of services because I have covered everything in my previous blog learnings.🫣

We will only be focusing on:

## Exposing Kubernetes workloads to the outside world👶

**LoadBalancer** is the type of service that will expose your application to outside the world.

This will only work on **cloud** **providers**. There will be an elastic load balancer that will be created by the cloud providers which is a public IP address through which you can access your application.

**Cloud Control Manager** which is inside your master node will generate public IP adders using any cloud provider eg **AWS** and returns to the service so that anyone can access your application using that IP address.

To create a `service` obviously, we need all the `pods` and `deployment-definition` file.

So here it is:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webapp
  template:
    metadata:
      labels:
        app: webapp
    spec:
      containers:
      - name: webapp
        image: my/webapp:latest
        ports:
        - containerPort: 80
```

Now, time to create a `service-definition-2` yaml file with `LoadBalance` type:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: webapp-service
spec:
  selector:
    app: webapp
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

First run,

```bash
kubectl apply -f /root/service-definition-2.yaml
```

Now the **service** is created. You can access this through the internet with the correct **IP address** and **port number** provided by this service.

Check the IP address and Ports by `get` command:

```bash
kubectl get svc <name>
```

# How to discover Services and Pods within a Kubernetes cluster using DNS and other mechanisms?🧐

As we know how service works and its purpose But did you think how it tackled the problems? How does it send requests to the users? How does it provide everything requested by the users?

Let's see the solution:

**Service** act as a **load balancer** by using a component known as `kube-proxy`.

So instead of accessing the IP addresses, it helps the users to give a specific service name to the users to access the application.

`kube-proxy` will forward the requests coming from several users.

So without Services, your application will not work even if you have everything like pods, deployments, etc ready. When a pod goes down then you're unable to provide your applications to the users in case of no service available.

But the question remains the same. How service is handling the IP addresses, as every time a pod goes down, it comes up with a different address. So how this is going on?

If three of the pods are deployed in the cluster and each one has its IP address and whenever a pod goes down and comes up always with the new IPs then how service is managed all the time with the new IPs and managing all the user's requests?

This is handled by **Service Discovery**.

## Service Discovery🕵️

This comes up with a new process called **Labels** & **Selectors**

Instead of working with IP addresses and keeping track of it. Service is using the concept of labels & selectors.

### Labels📋

* It is just a key-value pair.
    
* You can name it by your conventions.
    
* It is used to organize and select the objects in the cluster
    
* You can label Pods, Deployments, and Services.
    
* Example, `key=app` and `value=myapp`
    

```yaml
metadata:
  labels:
    app: myapp
```

### Selectors✅

* It must be defined same name as the labels defined.
    
* It is used to select objects based on their labels.
    
* It can be used for a single or a groped objects that matches specific labels.
    
* Example, create a Service that selects all Pods with the label `app=myapp`:
    

```yaml
yamlCopy codespec:
  selector:
    app: myapp
```

We will give labels in our pod definition yaml file so that whenever a pod goes down and comes up with new IPs, it will always have the same label in it as we defined in the template. A new pod is always created with the given template.

* The **replica** **sets** will deploy the **pods** using the **labels**.
    
* **Services** will keep track of all the **deployments** by the **labels**.
    
* Labels are just a name given to a pod nothing else.
    

So this is the **service** **discovery** mechanism that uses labels & selectors.

So you created a deployment definition yaml file and on that the `metadata` section you will define a `label` which can be any name provided by you for your deployed application.

## Pod Discovery Using DNS🌐

The CoreDNS server is deployed as a POD in `kube-system` namespace in the k8s cluster.

It creates a service to make it available to other components within a cluster. And the `service` is named `kube-dns` by default.

```bash
kubectl get service -n kube-system
```

It uses a file called `Corefile` which is located at `/etc/coredns`

```bash
cat /etc/coredns/Corefile
```

In this file, you have all the configurations of **plugins**.

One of the plugins that make `CoreDNS` work with k8s is the Kubernetes plugin.

A top-level domain name is set as a `cluster.local`

The **DNS** configuration on **PODS** is done by k8s automatically when the pod is created.

`config` file of the `kubelet` will give you the IP of the DNS server and the domain:

```bash
cat /var/lib/kubelet/config.yml
```

You can access your `service` by just

`name-service` or

`name-service.default` or

`name-service.default.svc` or

`name-service.default.svc.cluster.local`

```bash
<service-name>.<namespace>.svc.cluster.local
```

Example, `service-name=mywebapp` and `namespace=default` which is created automatically as default. Then,

```bash
mywebapp.default.svc.cluster.local
```

If you try to manually lookup for the service using nslookup or the host command

```bash
host <name-service>
```

## Pod Discovery Using Environment Variables🔗

The container which has the information of **Services** and **PODS** that are running inside the k8s cluster has an environment variable **automatically** set by Kubernetes.

These **variables** are used to discover the IP address, port numbers and hostname for the services and running pods.

Example,

the `SERVICE_HOST` and `SERVICE_PORT` environment variables are automatically set in containers running inside a Service's Pod.

the `HOSTNAME` environment variable is set to the hostname of the Pod and the `MY_POD_IP` environment variable is set to the Pod's IP address.

Let's create a simple `service` yaml file to use for further process with type `ClusterIP`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
  labels:
    app: myapp
spec:
  type: ClusterIP
  selector:
    app: myapp
  ports:
  - name: http
    port: 80
    targetPort: 8080
```

Now, let's create a `pod` YAML file that runs `image=nginx` by setting two `env` variables `MYAPP_SERVICE_HOST` and `MYAPP_POD_IP`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: nginx
    env:
    - name: MYAPP_SERVICE_HOST
      value: "myapp-service.default.svc.cluster.local"
    - name: MYAPP_POD_IP
      valueFrom:
        fieldRef:
          fieldPath: status.podIP
```

`MYAPP_SERVICE_HOST` is set to `myapp.default.svc.cluster.local` and

`MYAPP_POD_IP` is set using a `fieldRef` that retrieves the Pod's IP address from its status.

Together, these files define a web application that can be accessed using the virtual IP address assigned to the Service.

When a client sends a request to the Service's IP address on port 80, the request will be forwarded to one of the Pods with the `app: myapp` label and the response will be sent back to the client.

This is how you can discover pods using environment variables.

---

Thank you!🖤