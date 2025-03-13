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



## Day 3 Multistage Dockerize an application
_________________________________________
https://labs.play-with-docker.com/  - Used this to do day 3 praticals

1. Create a directory
>mkdir Day03
2. Make created directory as working directory
>cd Day03
3. Clone a project into it
>git clone https://github.com/piyushsachdeva/todoapp-docker.git
4. Check what are all files are there in the docker
>ls -lrt
5. A new directory will be created wih the name "todoapp-docker" and make this as working directory
>cd todoapp-docker
6. Lets create a Docker file to create a docker image from it.
>touch Dockerfile
- By entering above command it will create a docker file inside
7. Now lets enter the code inside it by view editor
> vi Dockerfile
- This command will open the file in edit mode.
8. Lets start updating the code in the file, initially the file will be in escape mode so lets make it into insert mode by entering "i"
9. Lets update the code
  > FROM node:18-alpine AS installer
  > WORKDIR /app
  > COPY package*.json ./
  > RUN npm install
  > COPY . .
  > RUN npm run build
  > FROM nginx:latest AS deploye
  > COPY --from=installer app/build /usr/share/ngnix/html
10. Lets save the code
  > "wq!
11. Now lets build the docker image from docker file
  > docker build -t todoapp-docker .
  - This command will build the docker image with the name todoapp-docker
12. Lets see if the image was create or not
  > docker images
  - This command will list all the images available
13. Lets see if there is any container available if not we need to create one.
 > docker ps
  - This command will list all the available containers
  - In current case there is no container available, lets run the docker image to create the container
14. Lets run the docker image to create a container
 > docker run -it -dp 3000:3000 todoapp-docker
  - This command will run the docker image todoapp-docker on a contianer
15. Now if you do below command it will show the running container
 > docker ps
16. If you want to see the logs of any container, you can run below command
 > docker logs "container id" (generates when you run 14th step)
17. To go into a container, use below command to do
 > docker exec -it "container id" sh
 > By default you will be in working directory as we havent provided any specific directory
18. To see configuration of any container use below command
 > docker inspect "container id"














## ALIAS
k=kubectl
svc=service











## Important Commands Output:
--------------------------------------------------------------------------------------------------------------------------------
### CLUSTER MANAGEMENT:
___________________________
## controlplane ~ ➜  k cluster-info 
Kubernetes control plane is running at https://127.0.0.1:6443
CoreDNS is running at https://127.0.0.1:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://127.0.0.1:6443/api/v1/namespaces/kube-system/services/https:metrics-server:https/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.


## controlplane ~ ➜  k config 
Modify kubeconfig files using subcommands like "kubectl config set current-context my-context".

 The loading order follows these rules:

  1.  If the --kubeconfig flag is set, then only that file is loaded. The flag may only be set once and no merging takes
place.
  2.  If $KUBECONFIG environment variable is set, then it is used as a list of paths (normal path delimiting rules for
your system). These paths are merged. When a value is modified, it is modified in the file that defines the stanza. When
a value is created, it is created in the first file that exists. If no files in the chain exist, then it creates the
last file in the list.
  3.  Otherwise, ${HOME}/.kube/config is used and no merging takes place.

Available Commands:
  current-context   Display the current-context
  delete-cluster    Delete the specified cluster from the kubeconfig
  delete-context    Delete the specified context from the kubeconfig
  delete-user       Delete the specified user from the kubeconfig
  get-clusters      Display clusters defined in the kubeconfig
  get-contexts      Describe one or many contexts
  get-users         Display users defined in the kubeconfig
  rename-context    Rename a context from the kubeconfig file
  set               Set an individual value in a kubeconfig file
  set-cluster       Set a cluster entry in kubeconfig
  set-context       Set a context entry in kubeconfig
  set-credentials   Set a user entry in kubeconfig
  unset             Unset an individual value in a kubeconfig file
  use-context       Set the current-context in a kubeconfig file
  view              Display merged kubeconfig settings or a specified kubeconfig file

Usage:
  kubectl config SUBCOMMAND [options]

Use "kubectl config <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).

## controlplane ~ ➜ k version 
Client Version: v1.32.0+k3s1
Kustomize Version: v5.5.0
Server Version: v1.32.0+k3s1

## controlplane ~ ➜ k get nodes 
NAME           STATUS   ROLES                  AGE   VERSION
controlplane   Ready    control-plane,master   11m   v1.32.0+k3s1

## controlplane ~ ➜  k get pods
No resources found in default namespace.

For single service
## controlplane ~ ➜  k get service
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   12m

For many services
## controlplane ~ ➜  k get services
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   12m

### POD MANAGEMENT:
____________________________
k create pod

k get pod

k describe pod

k logs

k exec

k delete pod

### RESOURCE MONITORING
____________________________

## controlplane ~ ➜ k top node 
NAME           CPU(cores)   CPU(%)   MEMORY(bytes)   MEMORY(%)   
controlplane   48m          0%       770Mi           1%  

k top pods

k top pods

k get quota

k describe

### SERVICE MANAGEMENT
___________________________

k create service

## controlplane ~ ➜ k get service
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   35m

k expose 

## controlplane ~ ➜ k describe service
Name:                     kubernetes
Namespace:                default
Labels:                   component=apiserver
                          provider=kubernetes
Annotations:              <none>
Selector:                 <none>
Type:                     ClusterIP
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.43.0.1
IPs:                      10.43.0.1
Port:                     https  443/TCP
TargetPort:               6443/TCP
Endpoints:                192.168.183.228:6443
Session Affinity:         None
Internal Traffic Policy:  Cluster
Events:                   <none>

k delete service 

k port-forward

### CONFIGURATON & SECRETS
______________________________

k create configmaps

## controlplane ~ ➜ k get configmaps 
NAME               DATA   AGE
kube-root-ca.crt   1      39m

k create secret

k get secret

## controlplane ~ ➜  k describe configmaps 
Name:         kube-root-ca.crt
Namespace:    default
Labels:       <none>
Annotations:  kubernetes.io/description:
                Contains a CA bundle that can be used to verify the kube-apiserver when using internal endpoints such as the internal service IP or kubern...

Data
====
ca.crt:
----
-----BEGIN CERTIFICATE-----
MIIBdzCCAR2gAwIBAgIBADAKBggqhkjOPQQDAjAjMSEwHwYDVQQDDBhrM3Mtc2Vy
dmVyLWNhQDE3NDE4NDQwNTYwHhcNMjUwMzEzMDUzNDE2WhcNMzUwMzExMDUzNDE2
WjAjMSEwHwYDVQQDDBhrM3Mtc2VydmVyLWNhQDE3NDE4NDQwNTYwWTATBgcqhkjO
PQIBBggqhkjOPQMBBwNCAAQ601I4GtjUUTZkPw/DismKT2uWLDe84J3D3MfyHeAr
iIWuVg1S8w1KWy59sWd1cdewCIouUOeBgW5sjWGAY5Zto0IwQDAOBgNVHQ8BAf8E
BAMCAqQwDwYDVR0TAQH/BAUwAwEB/zAdBgNVHQ4EFgQUZQglFpB4nVFKw3e+m2wa
WFz0KXgwCgYIKoZIzj0EAwIDSAAwRQIgRQga5ZLQwCRyGLO++pWOrMDWIc6DmwaL
bj8XZm5GZ5ACIQD3U4TynZNRKNC8B51hCNcpdbwh0fCKPq+D/yAi2r3jjw==
-----END CERTIFICATE-----



BinaryData
====

Events:  <none>

k describe secret

### DEPLOYMENT MANAGEMENT
_______________________________

k create deployment 

## controlplane ~ ➜  k get deployments
NAME                       READY   UP-TO-DATE   AVAILABLE   AGE
simple-webapp-deployment   4/4     4            4           2m46s

k scale

k rollout status

k rollout history

k delete deployment


### NAMAESPACE MANAGEMENT
______________________________
k create namespace

## controlplane ~ ➜  k get namespaces 
NAME              STATUS   AGE
default           Active   49m
kube-node-lease   Active   49m
kube-public       Active   49m
kube-system       Active   49m

## controlplane ~ ✖ k describe namespaces 
Name:         default
Labels:       kubernetes.io/metadata.name=default
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource.

Name:         kube-node-lease
Labels:       kubernetes.io/metadata.name=kube-node-lease
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource.

Name:         kube-public
Labels:       kubernetes.io/metadata.name=kube-public
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource.

Name:         kube-system
Labels:       kubernetes.io/metadata.name=kube-system
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource.

k delete namespace

k apply -n <namespace>

k switch -n <namespace>


Q.  Create a new service to access the web application using the service-definition-1.yaml file.

Name: webapp-service
Type: NodePort
targetPort: 8080
port: 8080
nodePort: 30080
selector:
  name: simple-webapp

















