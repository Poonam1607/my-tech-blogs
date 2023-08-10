---
title: "Kubernetes Networking"
datePublished: Tue Apr 25 2023 14:36:01 GMT+0000 (Coordinated Universal Time)
cuid: clgxsu4si00030ampag8c5mg8
slug: kubernetes-networking
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682519613264/40d8da2c-9a12-45b5-a237-1a033bc819d8.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1682519741263/c5b35da3-6498-4460-804b-ade5e7937c75.png
tags: kubernetes, devops, trainwithshubham, kubeweek, kubeweekchallenge

---

## Introduction✍️

Networking in k8s is such a crucial topic to understand and a must for working in k8s. Here we will discuss networking, particularly in the work use of k8s directly. So before you come to this topic you must have knowledge of basic computer networking.

* **Switching**
    
* **Routing**
    
* **Gateways**
    
* **Bridges**
    

### PODS📦

* Before jumping right into the Kubernetes networking stuff. First, let's recall the Pods concept because we will be using Pods in every sentence further.
    
* Whatever we are doing, the main goal is to **deploy** our application in the form of **containers** on a worker **node** in the **cluster** which must be up and **running**.
    
* As Kubernetes does not deploy the containers directly on the nodes.
    
* The containers are encapsulated into an object known as Pods
    
* The Pod is a single instance of an application.
    
* A Pod is the smallest object that you can create in Kubernetes.
    
* A simple **yaml** pod file:
    
* ```yaml
          apiVersion: v1
          kind: Pod
          metadata:
            name: demo-pod
          spec:
            containers:
            - name: demo-container
              image: nginx
              ports:
              - containerPort: 80
    ```
    
* Then run the `kubectl apply` command once you have created the **YAML** file to deploy it in the Kubernetes cluster with the necessary file name you have given.
    
* ```bash
          kubectl apply -f demo-pod.yaml
    ```
    
    This is how you can start creating PODs.
    

## Network Policies📋

* In Kubernetes, every routing network traffic instruction is set by the network policies.
    
* A set of tools that defines the communication between the pods in a cluster.
    
* It is a powerful tool used for the security of network traffic in k8s clusters.
    
* Allowance of traffics from one specific pod to another one.
    
* Restricting traffic to a specific set of ports and protocols.
    
* Implementation is done by Network APIs.
    
* It can be applied to namespaces or individual pods.
    
* A simple network policy yaml file:
    
    ```yaml
    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: demo-network-policy
    spec:
      podSelector:
        matchLabels:
          app: my-app
      policyTypes:
      - Ingress
      ingress:
      - from:
        - podSelector:
            matchLabels:
              app: allowed-app
        ports:
        - protocol: TCP
          port: 80
    ```
    
* For the deployment of the Network Policy YAML file, use the `kubectl apply` command:
    
    ```yaml
    kubectl apply -f demo-network-policy.yaml
    ```
    
    This is how you can define your own network policies.
    

## Services🪖

Let's say, you deployed a pod having a web application running on it and you want to access your application outside the pod. Then how to access the application as an external user?

The k8s cluster setup in your local machine has an **IP** **address** similar to your system IP but the pod has a different IP address which is inside the node.

As the pod and your system share different addresses, there is no way to access the application directly into the system.

So we need something in-between to fill the gap and gives us access to web application directly from our systems.

![Getting started with Kubernetes Services - Spectro Cloud](https://www.spectrocloud.com/static/c6684c832b815a832c004f4dee0fe3c5/7fe1f/58-image-2.png align="left")

This is where **Kubernetes Services** comes into the picture.

* k8s services **activate** the communication between several components inside-out the application.
    
* It helps us to connect the application together with other applications and users.
    
* It is an **object** just like PODs, Replicas and Deployments.
    
* It listens to a port on the node and forwards the requests to the port where the application is running inside the pod.
    

A simple service yaml file:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: demo-service
spec:
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```

## Services Types📑:

* ### NodePort Service
    
* ### ClusterIP Service
    
* ### LoadBalancer Service
    

1. **NodePort Service** - It makes an internal POD accessible to the Port on the Node.
    
    ![Figure 1: Kubernetes NodePort service](https://www.spectrocloud.com/static/0d864536e5cae1e3a9fcc4f783c5f5c5/7fe1f/58-image-1.png align="left")
    
    * the port number inside the pod is the target port
        
    * the port number in the service area is the 2nd Port
        
    * and the port on the node is NodePort where we're going to access the web server externally.
        
    
    *the* ***valid*** ***range*** *of* ***NodePort*** *(by default):* ***3000*** *to* ***32767***
    
    * labels & selectors are necessary to describe in the spec section in case of multiple pods in a node or multiple nodes in a cluster.
        
2. **ClusterIP Service** - It creates a **virtual** IP inside the cluster to enable communication between different services.
    
    ![Figure2: Kubernetes ClusterIP service](https://www.spectrocloud.com/static/c6684c832b815a832c004f4dee0fe3c5/7fe1f/58-image-2.png align="left")
    
    * a service created of a tier of your application like backend or frontend which helps to group all the pods of a tier and provide a single interface for other pods to access this service.
        
3. **LoadBalancer Service** - It **exposes** the service on a publicly accessible IP address in a supported cloud provider.
    
    ![Figure3: Kubernetes LoadBalancer service](https://www.spectrocloud.com/static/edaf9a1bfb66732937cb50e991569c62/7fe1f/58-image-3.png align="left")
    

A demo **NodePort** **yaml** file:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-demo-service
spec:
  type: NodePort
  selector:
    run: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

now run,

```bash
kubectl create -f myservice.yaml
```

This is how you can create your service of NodePort type. By changing the `spec` `type` to `ClusterIP` or `LoadBalancer`, whatever you wish to work with just change it with the name and port according to it.

## CNI (Container Network Interface)🌐

* CNI is a set of **standards** that defines how to **configure** networking challenges in a container runtime environment like Docker and Kubernetes.
    
* It is a simple plugin-based architecture.
    
* It defines how the plugin should be developed.
    
* Plugins are responsible for configuring the network interface.
    
* CNI comes with a set of supported plugins already. Like **bridge**, **VLAN**, **IPVLAN**, **MACVLAN.**
    
* **Docker** **does** **not** implement CNI. It has its own set of standards known as **CNM** ie, Container Network Model.
    
* We cannot run a docker container to specify the network plugin to use CNI.
    
* But you can do it **manually** by creating a docker container without any network configuration
    
* ```bash
          docker run --network=none nginx
    ```
    
* then invoke the bridge plugin by yourself.
    

### CNI in k8s🕸️

* Kubernetes is responsible for creating container network namespaces
    
* Attaching those namespaces to the right network
    
* You can see the network plugins set to CNI by running the below command
    
* ```bash
          ps -aux | grep kubelet
    ```
    
* The CNI plugin is configured in the kubelet service on each node in the cluster
    
* The CNI bin directory has all the supported CNI plugins as executables.
    
* ```bash
          ls /opt/cni/bin
    ```
    
* k8s supports various CNI plugins like **Calico**, **Weave** **Net**, **Flannel**, **DHCP** and many more.
    
* You can identify which plugin is currently used with the help of this command
    
* ```bash
          ls /etc/cni/net.d
    ```
    
* kubelet finds out which plugin will be used.
    

## DNS in k8s📡

* Kubernetes deploys a built-in DNS server by default when you set up a cluster.
    
* Let's say we have three nodes k8s cluster having pods and services deployed in it having node name and IP address assigned to each one.
    
* All pods and services can connect to each other using their IPs and to make the web app available to external users we have services defined on them.
    
* Every new entry of a pod goes into the DNS server record by
    
* ```bash
          cat >> /etc/resolv.conf
    ```
    
* The k8s DNS keeps the record of the created services and maps the service name to the IP address. So anyone can reach by the service name itself.
    
* DNS implemented by Kubernetes was known as **kube-dns** and later versions **CoreDNS**.
    
* The CoreDNS server is deployed as a POD in the **kube-system** namespace in the k8s cluster.
    
* To look for DNS Pods, run the command
    
* ```bash
          kubectl get pods -n kube-system
    ```
    

## Ingress🔵

* Let's say you have an application deployed in the k8s cluster with a database pod having required services for external accessing with the NodePort in it. The replicas are going up and down as per the demand of the application.
    
* You configured the DNS server so that anyone can access the web app by typing their name instead of IP address every time
    
* like, `http://my-app.com:port` instead of `http://<node-ip>:port` and if you do not want others to `type` port number also then you served a **proxy-server** layer between your cluster and DNS server. so that anyone can access it by just
    
    `http://my-app.com`
    
* Now, you want some new features to be added to your application. You developed the code and deployed the webapp again for the new features of pods and services into the cluster. Again setting up the proxy server in-between to access the webapp in just a single domain.
    
* Maintaining all these outside the cluster is a tedious task to do when your application scales. Every time a new feature adds on, you have to do all the layerings again and again.
    
* This is where **Ingress** comes in. Ingress helps users to access your application with a single URL.
    
* Ingress is just another **k8s definition** file inside the cluster
    
* You have to **expose** it one time to make it **accessible** outside the cluster either with **NodePort** or the cloud provider like GCP which uses the **LoadBalancer** service.
    

### Ingress Controller🔹

* In the case of using ingress in a k8s cluster, an ingress controller must be **deployed** and **configured**.
    
* Mostly used ingress controllers are **Nginx**, **Traefik**, and **Istio**.
    
* Deploy the application on the k8s cluster and configure them to **route** **traffic** to other services.
    
* The configuration involves defining **URL** Routes, Configuring **SSL** certificates etc. This set of rules to configure ingress is called an **Ingress Resource**.
    
* Once the controller is running, resources can be created next and configured to route traffic to different services in the cluster.
    
* It is created using definition files like the previous ones we created for Pods, Services and Deployments.
    
* Ingress Controller is not built-in in them by default. You have to create it **manually**.
    
* A simple **ingress** **yaml** **file** for the sake of explanation:
    
* ```yaml
          apiVersion: networking.k8s.io/v1
          kind: Ingress
          metadata:
            name: minimal-ingress
            annotations
              nginx.ingress.kubernetes.io/rewrite-target: /
          spec:
            ingressClassName: nginx-example
            rules:
            - http:
                paths:
                - path: /testpath
                  pathType: Prefix
                  backend:
                    service:
                      name: test
                      port:
                        number: 80
    ```
    
* **Create a single ingress called 'simple' that directs requests to** [**foo.com/bar**](http://foo.com/bar) **to svc # svc1:8080 with a tls secret "my-cert"**
    
* ```yaml
          kubectl create ingress simple --rule="foo.com/bar=svc1:8080,tls=my-cert"
    ```
    
    This is how you can start working with Ingress in Kubernetes.
    

---

Thankyou!🖤