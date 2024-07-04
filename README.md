# NodeJS Application Deployment To Azure Kubernetes Cluster(AKS)

I'm going to cover two ways to deploy nodejs application on AKS.
1) Azure DevOps Pipeline
2) VS code

   ## 1) Azure DevOps Pipeline

Azure Repo: Here, source code, dockerfile & manifest files are present.

![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/207ae9ba-12f6-4602-b007-12b105939997)

Create ACR & AKS on Azure cloud. Give necessary permission in ACR(Admin user) so that AKS woould not face any issue while pulling the image from ACR repository.

ACR:
![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/66b997fe-b498-4bf6-9df3-4a6a0f3bfe53)

AKS:
![image](https://github.com/samirwadkar31/NodeJs_Application_AzureKubernetesCluster/assets/74359548/a131cb1e-1484-4b20-955f-f4a8aefd78e0)

Create a service connection to Azure Resource Manager using SPN in ADO and give the necessary IAM permissions to this SPN at subscription/resourcegroup/resource level on Azure for the secure access & deployment to ACR/AKS.<br>

We need to build the image and push it to private azure container registry (ACR) on Azure Cloud. <br>
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
