# Day 1 - Introduction and basics of K8s

Today the topic we are going to cover is Docker amd its understanding:
Fundamental of Docker is Build, Ship and Run the application code. Docker is nothing but a platform that helps you to build, ship and run the application code.
## Container vs VM
VM - is a virtual computer which has OS

Consider VM as an independent house and contrainer as an apartment
On VM
- You have Buneries and dependendies which are windows of the house
- Application as your family
- Isolated OS - means this OS is common for one family on for application installed on the house
On Container
-  Has shared infra between different flats in that aprtment
-  But they share the infra, building, land
-  Every container(flat) has independent Application, Binaries dependency OS etc.

## Docker flow:
                       push
                     --------------Registry--------------------
                   |                    | |_pull___           |
          Build    |                    |          |          |
Dockerfile --> Docker Image            Dev        Test        Prod
                                        |          |          |
                                        |_________ Run _______|
## Exlaining above flow:
What is Docker file
- WHich is usually a set of intruction
- Like install some app, Run these commands on the OS etc.,

What is Docker Image
- Now we will build docker file using docker image
- A package of liberaries, binaries, Application, OS is called docker image. This image is shipable image, we can ship this image from one environment into another.
- If we run "Docker Build" command, docker file will build docker image.
  
What is Registry
- Once the image is ready, we cannot push that onto Dev/Test/Prod this is not best practice/
- We need intermediate storage to store the image and from that the imanges are pushed onto different environment
- A Docker registry is does the work for us. Ex:  Docker Hub, which help to store images. There are many registries.
- With the help of "Docker Pull" command the image will be pulled onto different environment.
- Then run "Docker Run" - this will convert your package into running instance.

## Docker Architecture:
Please refer Untitled Diagram.drawio
Explaining inbuild componenets:

## docker build 
- When we run docker build command, it will pull the image from source code (baasically a dockerfile will be pulled) and Docker daemon(dockerd) will create an image with the help of dockerfile.
- Now the image is issues to local host
- next step is you need an intermediate storage to store the image.
  
## docker push
- Now docker push command will be run and the created image will be pushed to a registry.
- There are different types of registries the most used is DockerHub.
- So when docker push command is ran, the image is stored in DockerHub registry by dockerd.
- Now the image is ready and it should be pulled into different environments
  
## docker pull
- Now docker pull will be issued to the dockerd and image will be pulled into the environment, lets say you are running on Devlopment environment then the image will be pulled onto Dev environment from the Dockerhub registry.
  
# docker run
- Now docker run command will be issued to dockerd and dockerd instruct container runtime to run the image pulled from registry.


## Day 2 How to Dockerize an application
Use below links to create docker lab to proceed further
https://labs.play-with-docker.com/
https://labs.play-with-k8s.com/

Working on DockerDesktop - There difference components in Docker Desktop but we only use Container and Images. Rest are not needed now.
 ---Pavan to do a end to end video on how to use Dockerdesktop

- Open Dockerdesktop and hit on Terminal on right bottom to open Powershell session.
- Now create a folder with command "mkdir Day02_code1"
- Do "ls", you will see it empty.
- Now we need an application installed on it to play with it. Use below link to clone it  - git clone https://github.com/docker/getting-started-app.git

 Install Git - I used https://git-scm.com/downloads link to install Git.



 Open Git Bash and try to clone























