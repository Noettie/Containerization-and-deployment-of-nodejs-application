# Containerization-and-deployment-of-nodejs-application

## Goal
To containerize a nodejs application and deploy it onto an Azure Kubernetes Cluster

## Objectives
1. Containerize application and run it locally.
2. Push docker image onto Azure Container Registry.
3. Deploy application onto Azure Kubernetes Cluster.

## Tools:

<div>
  <img src="https://github.com/devicons/devicon/blob/master/icons/docker/docker-original-wordmark.svg" width="60"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/kubernetes/kubernetes-plain.svg" width="60"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/nodejs/nodejs-original-wordmark.svg" width="80"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/azure/azure-original-wordmark.svg" width="80"/>
<div>
  

## Objective 1 Steps:

1. Install docker onto your machine and start the docker engine.
$$ sudo service docker start.
2. Clone the application onto your local machine.
$ git clone <url>
3. Build the application image using the Dockerfile.
$ docker build -t <noettie/nodejs-webapp> . 
4. Check the image built.
$ docker image
5. Create a container by running the image and publish a port to access the conatiner.
$ docker run -p 3000:3000 <image_name:tag>
6. Access the container using localhost:port_number. 

The application should look like this :

![localhost-app](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/6c3098b9-53b4-48a6-95f3-c7819de7c127)



** Congratulations! You have successfuly containerized a nodejs application** 

## Objective 2 Steps:

1. Login to azure
$ az login
2. Create a resource group
$ az group create --name <resourceGroup_name> --location <region>
3. Create registry inside the resource group
$ az acr create --resource-group <nottie-myResourceGroup> --name <nottieacr> --sku Standard --location <eastus>
4. Login to Azure Container registery (acr)
$ az acr login --name <nottieacr>
5. Tag the image using the access keys of the registry i.e name of registry and login server 
You have to tag the image first before pushing with the specific azure registry name otherwise will be denied access
$ docker tag nottie/nodejswebapp:latest nottieacr.azurecr.io/nodejswebapp:v1
$ docker push nottieacr.azurecr.io/nodejswebapp:v1
$  az acr repository list --name notieacr --output table
$ az acr repository show-tags --name nottieacr --repository nodejswebapp --output table

Terminal commands:

![image-push](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/6891e8d2-12b1-4537-b9cd-06868e5470b0)

The output from the Azure ui will look liks this:

Resource group: 
![akscluster](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/8e5063db-858b-4dfd-82e6-1cf6c38395bd)


Container registry with image:

![acr-imagepush](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/326f96dd-5755-4674-85e1-f5dc01af592f)



** Congratulations ! You have successfully pushed an image to the Azure container registry** 

## Objective 3 Steps:

1. Create the aks cluster in your region.
$ az aks create --resource-group nottie-myResourceGroup --name nottieCluster --node-count 2 --generate-ssh-keys --enable-addons monitoring
If this is your first cluster creation on aks it may be necessary register microsft.insights and microsft.network
$ az provider register --namespace microsoft.insights

![registering-msinsights](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/1f52d1d8-4566-4e05-8988-8771ac56ec71)

![registrations](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/31eaa190-f4be-4fd7-a078-91b1ecd8e8f7)

2. Confirm cluster was created. 
$ az aks show --name <noenoe-cluster> --resource-group <nottie-myResourceGroup>
3. Connect to the cluster.
$ az aks get-credentials --resource-group <nottie-myResourceGroup> --name <noenoe-cluster> --overwrite-existing
$ az aks update -n noenoe-Cluster -g nottie-myResourceGroup --attach-acr nottieacr
4. Apply the deployment Confirm that pods have been created
$ kubectl apply -f deployment.yml
$ kubectl get pods
5. Check the load balancer ip and access the application.

Terminal commands:

![loadbalancer_ip](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/d2aa71ea-219b-426b-bbb7-3beaa83ee988)

Application Live!

![load-balancer-app](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/683d0bf7-0d2b-4e23-8b36-e61e4ee94dee)

** Congratulations! You have successfully deployed a nodejs application onto an azure kubernetes cluster.**

## Summary 
- Dockerized an application.
- Tested it locally.
- Pushed image to ACR to store image.
- Created AKS cluster.
- Deployed application onto cluster. 
- Accessed the application via the web.
























