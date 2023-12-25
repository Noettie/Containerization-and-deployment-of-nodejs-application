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
![application_live](https://github.com/Noettie/Containerization-and-deployment-of-nodejs-application/assets/108426517/3166d2d5-db12-4105-9c7d-717cd253f0e6)





