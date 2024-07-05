# NodeJS Application Deployment To Azure Kubernetes Cluster(AKS)

I'm going to cover two ways to deploy nodejs application on AKS.
1) Azure DevOps Pipeline
2) VS code

   ## 1) Azure DevOps Pipeline

Azure Repo: Here, source code, dockerfile & manifest files are present.

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/207ae9ba-12f6-4602-b007-12b105939997)

Create ACR(Azure Container Registry) & AKS(Azure Kuberentes Service) on Azure cloud.<br>
Give necessary permission in ACR (Under Access Policies, enable Admin user checkbox) so that AKS woould not face any issue while pulling the image from ACR repository.

ACR:
![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/66b997fe-b498-4bf6-9df3-4a6a0f3bfe53)

AKS:
![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/a131cb1e-1484-4b20-955f-f4a8aefd78e0)

Create a service connection to Azure Resource Manager using SPN in ADO and give the necessary IAM permissions to this SPN at subscription/resourcegroup/resource level on Azure for the secure access & deployment to ACR/AKS.<br>

We need to build the docker image and push it to private azure container registry (ACR) on Azure Cloud. <br>
Then, need to perform Deploy To AKS task, which will pull the image from ACR with the help of manifest file and deploy it on AKS container pods.

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/f668c1d1-5d51-4630-a4c2-b0309d388fc2)

Deployment is succeeded!! Hurrray :)

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/985fe42b-4bf7-4d60-85f5-cde55dfa14c4)

Now, let's run some kubectl commands, get the load balancer external ip and run our application at http port 80. (default port for Node.js is 3000; port mapping 80:3000 is done in manifest file)

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/d96e15d4-2a04-4eaf-84a7-a095b33e0a0c)

Copy load balancer external ip and run on any browser.<br>
Here, we go :) Our Node Js application is successfully deployed on Azure Kuberentes cluster.

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/1ea0cc73-dd8b-457d-adfa-2e001c76c984)

When we paste load_balancer_ip:80 (80 is http port) in browser, AKS service component load balancer maps port 80  with port 3000 and returns the response from the containers running at port 3000 as mentioned in manifest.yaml file.

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/38b8b832-b042-4133-901e-3471d06fae2d)

For better understanding of port mapping, please check manifest.yaml file provided in the repo.

  ## VS Code
We can deploy our nodejs app to Azure Kuberenetes Cluster(AKS) using VS code.

Pre-requisite: Install Azure CLI, Docker & Kubectl to your local machine<br>

Start docker engine and open your VS code IDE. <br>

### Step 1: Build the Docker Image

![Screenshot 2024-07-05 115113](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/31054992-041b-4dd9-b66d-e66afa6057a2)

Image is built successfully!!

![Screenshot 2024-07-05 131454](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/a4a5d30d-9d5a-461a-b53c-7a5b8d0232b0)

### Step 2: Push the Image to Private registry on Azure (ACR-Azure Container Registry).

First login to ACR, tag our built image with azercr.io standard image then push tagged image to ACR.

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/da4616fc-ad6a-4f2a-bd04-9c2adbfeb6c0)

Image is successfully pushed to the ACR.

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/e4c3b5c2-37a0-4868-bdb3-122b2afd7343)

Let's verify on ACR repository:<br>
It conatins our latest pushed image! :)

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/c8051801-85d1-47a4-8415-110fb6e0bdf6)

### Step 3: Deploy manifest.yaml to AKS using Kubectl commands.

Let's create 2 pods of our nodejs application and deploy it on AKS.(Mention replicas: 2 in your manifest.yaml file)

Initially, pod count was 0 after the kubectl apply command, pod count got increased to 2.

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/234f8f01-b157-4f78-8c2f-2afb70d4416f)

Let's copy this exteranl ip of load balancer and test it on our browser.

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/8baa2c93-95a9-44ec-818d-7e2f45e1a763)

We have successfully deployed our nodejs application on AKS. 
