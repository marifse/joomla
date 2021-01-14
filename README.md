### Installing Joomla on IBM Cloud
This document will describe how to install Joomla on IBM Cloud using Kubernetes services.

### Contents

1. Introduction
2. Provision Kubernetes Cluster
3. Deploy IBM Cloud Block-Storage Plugin
4. Deploy Joomla
5. Verifying the Joomla Installation

### Introduction
To complete this tutorial, you should have an IBM Cloud account, if you do not have one, please [register/signup here](https://cloud.ibm.com/registration).
For installing Joomla, we have used the Kubernetes cluster, and used the IBM Cloud Block-Storage plugin for our persistent volume. Upon the completion of this tutorial, you would have the Joomla up and running on the Kubernetes cluster.

1. Provision the Kubernetes cluster, if you have already setup one, skip to step 2.
2. Deploy the IBM Cloud Block-Storage Plugin to the created cluster, if you have already done this, skip to step 3.
3. Deploy the Joomla.

### Provision Kubernetes Cluster
* Click on the **Catalog** button on top center. Open [Catalog](https://cloud.ibm.com/catalog) ![alt text](Kubernetes1.png)
* In search catalog box, search for **Kubernetes Service** and click on it ![alt text](Kubernetes2.png)
* You are now at Create Kubernetes Cluster page, there you have the two plans to create the Kubernetes cluster, either using **free plan** or **standard plan**.

**Option1- Using Free Plan:**
* Select Pricing Plan as “**Free**”. ![alt text](Kubernetes3.png)
* Click on **Create**.
* Wait a few minutes, and then your Cloud would be ready.

>**Note**:  _Please be careful when choosing free cluster, as your pods could be stuck at pending state due to insufficient compute and memory resources, if you face such kind of issue please increase your resource by creating them choosing the standard plan._

**Option2- Using Standard Plan:**
* Select Pricing Plan as “**Standard**”
* Select your **Kubernetes Version** as latest available or desired one by application. In our example we have set it to be '**1.18.13**'.  

  ![alt text](Kubernetes4.png)

* Select Infrastructure as “**Classic**”

  ![alt text](Kubernetes5.png)

* Leave Resource Group to “**Default**”
* Select Geography as “**Asia**” or your desired one.
* Select Availability as “**Single Zone**”.
> _This option allows you to create the resources in either single or multi availability zones. Multi availability zone provides you the option to create the resources in more than one availability zones so in case of catastrophe, it could sustain the disaster and continues to work._
* Select Worker Zone as **Chennai 01**.
* In Worker Pool, input your desired number of nodes as “**2**” ![alt text](Kubernetes6.png)
* Leave the Encrypt Local Disk option to “**On**”
* Select Master Service Endpoint to “**Both private and public endpoints**”
* Give your cluster-name as “**Joomla-Cluster**”
* Provide tags to your cluster and click on **Create**.
* Wait a few minutes, and then your Cloud would be ready.

  ![alt text](Kubernetes7.png)

### Deploy IBM Cloud Block-Storage Plugin
* Click on the **Catalog** button on top center.
* In search catalog box, search for **IBM Cloud Block Storage Plug-In** and click on it ![alt text](Storage1.png)
* Select your cluster as "**Joomla-Cluster**"
* Provide Target Namespace as “**joomla-storage**”, leave name and resource group to **default values**. ![alt text](Storage2.png)
* Click on Install

### Deploy Joomla
* Again go to the **Catalog** and search for **Joomla**.

  ![alt text](Joomla1.png)

* Provide the details as below. ![alt text](Joomla2.png)

*	Target: **IBM Kubernetes Service**
*	Method: **Helm chart**
*	Kubernetes cluster: **Joomla-Cluster(jp-tok)**
*	Target namespace: **joomla**
*	Workspace: **joomla-01-07-2021**
*	Resource group: **Default**
* Click on **Additional Parameters** with **Default Values**, you can set the deployment values or use the default ones, we have used the default ones except for setting the **Auth. Root Password**.

* Click on **Install**.

### Verifying the Joomla Installation
* Go to the **Resources List** in the Left Navigation Menu and click on **Kubernetes** and then **Clusters**
* Click on your created **Joomla-Cluster**.

  ![alt text](JoomlaVerify1.png)

* A screen would come up for your created cluster, click on **Actions**, and then **Web Terminal** ![alt text](JoomlaVerify2.png)
* When the terminal is installed, click on the action button again and click on web terminal and type the following command in below command window. It will show you the workspaces of your cluster, you can see Joomla active.

```sh
     $ kubectl get ns 	
     $ kubectl get pod –n Namespace –o wide 
```
![alt text](JoomlaVerify3.png)
```sh
     $ kubectl get service –n Namespace
```
![alt text](JoomlaVerify4.png)

You can browse the external IP listed and can see the Joomla Sample Website Working.![alt text](JoomlaVerify5.png)
	 
The installation is done. Enjoy!
