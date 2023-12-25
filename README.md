# Containerization-and-deployment-of-nodejs-application

## Goal
To containerize a nodejs application and deploy it onto an Azure Kubernetes Cluster

## Objectives
1. Containerize application and run it locally.
2. Push docker image onto Azure Container Registry.
3. Deploy application onto Azure Kubernetes Cluster.

## Objective 1 Steps:

1.Install docker onto your machine and start the docker engine
$ sudo service docker start
2. Clone the application onto your local machine.
$ git clone <url>
3. Build the application image using the Dockerfile
$ docker build -t <noettie/nodejs-webapp> . 
4. Check the image built.
$ docker image
5. Create a container by running the image and publish a port to access the conatiner.
$ docker run -p 3000:3000 <image_name:tag>
6. Access the container using localhost:port_number 

The application should look like this :

![application_live](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/3166d2d5-db12-4105-9c7d-717cd253f0e6


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

![akscluster](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/8e5063db-858b-4dfd-82e6-1cf6c38395bd)


![acr-imagepush](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/326f96dd-5755-4674-85e1-f5dc01af592f)

** Congratulations ! You have successfully pushed an image to the Azure container registry** 













