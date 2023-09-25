---
title: "Envelope encryption in EKS 🔐"
datePublished: Mon Sep 25 2023 08:23:02 GMT+0000 (Coordinated Universal Time)
cuid: clmymfia9000109mf51be28ml
slug: envelope-encryption-in-eks
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695630147170/e8387443-e78d-40e6-b39c-e03bcfe29bdf.png
tags: aws, security, kubernetes, encryption, eks

---

Hola!! 🙋🏻‍♂️

𝗧𝗼𝗽𝗶𝗰 — Security 🔐  
𝗦𝗲𝗿𝗶𝗲𝘀 — “Under the hood” ⛏

The **Envelope encryption** is a vital defense-in-depth security feature that has addressed a crucial need — the protection of secrets that would otherwise be stored in **plain text** format within the `etcd` database. We can use envelope encryption to encrypt the Kubernetes secrets in EKS with our **own master key.**

## **Encoding & Encrypting**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695405331691/cfc17287-ea27-4c6a-8ccf-97bf85bd1de0.png align="center")

**Encoding (without keys):**

Encoding is the process of transforming data into a specific format, often for efficient storage or transmission, without the use of encryption keys.

**Encryption (with keys):**

Encryption is the method of converting data into a secure and unintelligible form using algorithms and encryption keys, primarily to protect it from unauthorized access

## **Envelope Encryption**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695408977305/a469ab28-9347-4365-aabb-2cd8dea825ca.png align="center")

## The Core Architecture

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695409323933/8c97ac39-9f00-4722-a868-3e6930be3f88.png align="center")

Certainly, here's a step-by-step explanation of envelope encrypting secrets in EKS:

1. **User Initiates Secret Creation**: The user runs `$kubectl create secret`, calling the Kubernetes API server.
    
2. **Kube API Server Authorization & Validation**: The Kubernetes API server checks user authorization and validates the request.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695312117033/56995a4f-cfb0-4b22-856b-a68c4cff0ca5.png?height=250 align="center")
    
3. **Generating DEK in-memory**: The Kubernetes API server generates a Data Encryption Key (DEK) locally in memory, unique for this operation, never saved to disk.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695333347876/a5e45a19-c1e4-490f-8828-57f0224d9a29.png align="center")
    
4. **Caching for Performance**: The Kubernetes API server caches the DEK in memory for efficiency and to reduce the API hits to AWS KMS.
    
5. **Secret Encryption:** Kube API server encrypts the secret using DEK in-memory.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695406464891/5ef5ef6d-e6c0-4fae-8f59-db82154bd8e1.png align="center")
    
6. **Kube API Server with KMS**: Meanwhile the Kubernetes API server sends the DEK to KMS for further encryption.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695312269904/ac82f20e-521b-4660-b103-b657d8a31562.png align="center")
    
7. **KMS & CMK Encryption**: KMS employs the Customer Master Key (CMK) to encrypt the DEK securely using a master key.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695312318115/44d5ced6-a0ae-4c43-af20-e172782dcdec.png align="center")
    
8. **Returns Encrypted DEK**: KMS returns encrypted DEK to the Kubernetes API server.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695333245159/a3ca180a-b794-4f6e-8b03-4fc83d5c5972.png align="center")
    
9. **Envelope Encryption:** The envelope contains **<mark>encrypted DEK</mark>** with KMS CMK and **<mark>encrypted secret</mark>** with DEK.
    
10. **Envelope Stored in etcd**: The envelope will now be stored in `etdc`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695409789447/2d3ad5e1-01f4-4e3e-bc36-5d2c380073b9.png align="center")
    
11. **Retrieval**
    
    1. **Secret Retrieval from etcd**: The pod requests a secret from the Kubernetes API server.
        
    2. Now two ways can be followed up by Kube API server:
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695312690202/0b4e2720-8970-42d1-ae07-929a1a8261c6.png align="center")
    
    1. **Using Cached DEK**:
        
        * If the Kubernetes API server has previously cached the encrypted DEK in its memory, it will use this cached DEK to perform decryption.
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695331579483/7e9f44f9-7df9-41e4-9601-62c4ee70f7bf.png align="center")
            
        * Cached data is used to optimize performance and reduce the API hits to AWS KMS when the same secret is accessed multiple times.
            
    2. **Retrieving from etcd**:
        
        * If there is no cached DEK data available or if the cached data has expired, the Kubernetes API server again calls the KMS.
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695407818306/18d7e85a-bf2b-499f-8817-8e527adc9ab8.png align="center")
            
        * This typically happens when the secret is accessed for the first time after a cache miss or expiration.
            

In a nutshell, we have ensured the data at rest is encrypted in etcd.

---

Thanks for reading our blog. Feel free to hit me up for any AWS/DevOps/Open Source-related discussions.

Manoj Kumar — [LinkedIn.](https://www.linkedin.com/in/musalannagari-manoj-kumar-21601b168/)

Poonam Pawar — [LinkedIn](https://www.linkedin.com/in/poonampawar7/)

**Happy Locking!!**

![](https://miro.medium.com/v2/resize:fit:450/0*NKFFOlBhqTQJrcWl align="center")