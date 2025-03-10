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
_________________________________________
Use below links to create docker lab to proceed further
https://labs.play-with-docker.com/ 
https://labs.play-with-k8s.com/

Or use Docketdesktop - Installation process can be found on Youtube.
--- Pavan to do a end to end video on how to install Docker desktop

Working on DockerDesktop - There difference components in Docker Desktop but we only use Container and Images. Rest are not needed now.
 ---Pavan to do a end to end video on how to use Dockerdesktop

- Open Dockerdesktop and hit on Terminal on right bottom to open Powershell session.
- Now create a folder with command "mkdir Day02_code1"
- Do "ls", you will see it empty.
- Now we need an application installed on it to play with it. Use below link to clone it  - git clone https://github.com/docker/getting-started-app.git
- In my case git commands are not recognized so have installed Git from below linke
---Pavan to find out how this can be fixed/Git using Dockerdesktop
  
- Install Git - I used https://git-scm.com/downloads link to install Git.
- Open Git Bash and try to clone the repository into the folder created (Day02_code1)
- Come back to Dockerdesktop and now do "ls", you will find files in it.
- So till now we have pulled an image from repository and now lets create a docker file.
- Since we are using powershell execute below command to create a docker file with the name "Dockerfile"
  "New-Item -Path "C:\Users\Pavan Kumar\day02_code1\Dockerfile" -ItemType File"

## Using https://labs.play-with-docker.com/ 


https://labs.play-with-docker.com/ 

It is a 4hr windows created to do the handon. One the 4hr window completes you need to create anew window to do the handon.
Lets dig-in further.
Here we will follow the Docker flow, so first we need a application file in you local repository to create a local file.
Lets create a file now for that in you local repository create a folder.

> mkdir Day02
- This will create a folder with name Day02.

Now CD into this folder
> cd Day02/
- This will make Day02 as your working directory

Now lets create a file
> git clone https://github.com/docker/getting-started-app.git
- This will clone the git repository into you local repository

Now lets create a dockerfile for that lets create an empty file
> touch Dockerfile
 - This command will create a file with Dockerfile

Now lets edit the Dockerfile
> vi Dockerfile
- This command will give you to edit the file

By default it will be escape mode so enter "i" to start insert mode.

## Instructions to write a docker file (All the key words you will be using here will be in upper case)

To run any image you need a base image to run the application.

> FROM node:18-alpine
- This step will call the image onto the node, which means it is a platform to run your application. you can also use different OS but choose the light weight. You can find them from Dockerhub repository. In this case we are choosing alpine image which is aLinux light weight OS.

> WORKDIR /app
- Is the working directory where you will be doing all your work inside a container at root level and every work will be done on this container.

> COPY .  .
- The files we cloned from git repo should be moved/copy them inside the container so that they will be used as source code.
- first . is current directory
- second . is work directory where I am currently on of container.

> RUN  yarn install --production
- Will install all the dependencies of the application, we are using yarn as package manager.

> CMD ["node", "src/index.js"]
- Which is actually responsible to executing the application.

> EXPOSE 3000
- This will used to expose your application and make it available on this port.

Now lets exist the editor.

Hit Esc
Hold Shift key and enter :
Type wq!

This will save the file.

Now we have the Docker file created, lets create Docker image.

Enter the docker commands
For beginners you can type docker --help, which will list all the commands and help you futher. Since w are building the image choose build, lets further take help on this

> docker build -- help

> "docker build -t day02-todo ."
- This means you are building the docker image with the name day02-todo and you are asking to take the input file from the current directory by enter "."

Now do the cat of the Docker file, we have 6 lines of codein that file and when you do docker build it will do the building the same way line by line.

Now lets see the created image by entering below command

> docker images
- You will have the file name, size of it, image version(collected from Docker hub), docker id.

So till now we have created the Docker file by cloning the app files from dockerhub, created in a local repository. Using this dockerfile we have build docker image and stored in local repository.


Now lets push the docker image into image repository example docker hub.

Login to Dockerhub, create a new repository. Lets name it test-repo and make it public and create.

Now when you are ready to push the image, use the below command to do it and before pushing the image we need to tag it.

> docker tag day02-todo:latest pk98723/test-repo:latest

This will create a new repository pk98723/test-repo

Now lets push the image

> docker push pkdocker1103/test-repo:latest
- Initially it will throw an error we haven't authenticated to docker hub.

So lets authenticate

> docker login
- It will ask for username and password.

Once auth is successful, push the image again

> docker push pk98723/test-repo:latest
- This step will push the image onto repo, one key difference to observe here is the size of the image in local repository will be more comparing to the image on the dockerhub. By default the image size will be compressed


Now lets pull the image

> docker pull pk98723/test-repo:latest
 - Since the image is in my local system, it will say that image is up to date incase there is any diference, it will download the latest.


Now lets run the image

> docker run -dp 3000:3000 pk98723/test-repo:latest
- d stands for detach mode, it means it will run the process in backend
- p stands for port which we wil expose.

Now after you hit the above command it will spitout the container ID which is a unique ID for this container.

> docker ps
- To see if the container is actually running, use above command to see the details


Inorder to troubleshoot the container incase it is not working as expected then you need to go inside the container.

> docker exec -it "add friendly name or container id" sh
- Now you will enter the container /app which is our working directory
- Now exit the container with command "exit"





















