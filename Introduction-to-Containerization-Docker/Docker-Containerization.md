## Docker-Containerization-Introduction

## Notes:Understanding -Docker
### Docker is a container engine
<img width="510" alt="image 1" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/6b730a64-603c-446b-9784-74ced0eb59d9">

### What is Virtualization?
* Virtualization is technology or software called hypervisor ,it is use to create virtual representations of servers, storage, networks, and other physical machines
### What is a hypervisor? 
* A hypervisor is a software that is use to run multiple virtual machines on a single physical machine. Example: EC2, Zen, VM ware, Oracle virtual box.. are hypervisor's
* Virtualization aims to run multiple OS instances on a single server...like ec2

### What is containerization?
* Containerization is a software (eg Docker engine) deployment process that bundles or packages  an application's code with all the files and libraries it needs to run on any infrastructure.
* It is a lightweight engine
<img width="588" alt="image 2b" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/a3af2d87-6e8e-44ec-b0dd-6e02ac1b2720">

### How to create a docker image?
* The developer bundles the Application code, Dependencies, Libraries, Binaries, Directory structures etc in a file called docker file, and ship to docker hub or github,
* The operations personel downloads the docker file to create docker image and creates a docker container.
* A docker container is a runing instance of a docker images or containers
* You can create as many containers of same image

  ### Docker Life-Cycle
<img width="621" alt="image3" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/49e05d13-e801-48eb-9a1d-34388e0346c8">



### Installing Docker
* Launch an ec2
* Connect to AWS cloudshell terminall
* Run "which docker" command to check if docker is installed
* sudo apt update -y
* sudo apt install docker.io to install lastest version of docker

 <img width="912" alt="0ne docker not yet installed" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/b69e454a-6ee9-454d-9263-db55280581c8">
<img width="905" alt="two install docker lastest version after update -y" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/eab73a21-a79e-4627-b96f-fdee2d7de01e">
<img width="817" alt="three" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/7e8c6f1f-fe8a-467a-b30e-4feb8cbcfcc7">
 
### Docker Architecture
<img width="536" alt="image 3 docker architecture" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/22262b66-b42f-473a-9046-24cd10298947">
<img width="927" alt="four" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/52d77bbf-87d2-4e40-8d4b-766236086dad">
* There is a docket client and docker server 
* The client communicate with the docker host.
* Every command I input on my terminal is from the client side
* It then interacts and get feedback from the docker deamon also called docker engine on the host side of the docker architecture
* And retures the feedback on the client terminal..feeback can be images etc
* The Registery side of the docker diagram is like a backup storage

### Best way to run docket is from root
<img width="732" alt="five best way to run docker" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/5145d89b-5756-4a66-a927-c26c38d4308d">
* Im no longer geting permission denied because I am runing from the root 
* Server communicates back info about server like numbers of server running etc
<img width="810" alt="six no permission denied" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/53200151-c1cb-484d-bf9f-f522c334f731">

* When I dont have access to the root command, I can use the "usermod" command
* -a appends G, and ubuntu is added as a user in docker
* The goal is to give user ubuntu permision to run docker info without error
* In other case ,I will have to "exit" and login back, but in this case I didnt
* Thsi is the same command to add a new user to docker
<img width="732" alt="eight" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/f718a10f-b2ae-40c5-be3e-d75ab0438daf">

# use docker scout to security tool for scaning images or trivy

### Example 1: How to use existing images tto run a docker image "hello-world" from dockerhub
* When i run the command "docker run hello-world"  , two things will happen:
* first,through the docker daemon, docker it will check my local computer for that image, it didnt find it, then It want to docker hub to pull it down
* gave it an id
* and a tag (lastest)
<img width="890" alt="nineb" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/87ffab6a-481a-44ad-83be-c016746fbb8a">

* I can also pull it from dockerhub  to run on my terminal
<img width="960" alt="ten" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/806c0f08-57c8-4eeb-ae20-a0e8c1430165">
* "docker pull hello-world" successful
<img width="919" alt="11 docker pull hello-world successful" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/b03c9d8b-74c4-4ce5-adae-7e704dd2e21b">
# When i run an image, it means it already exit on my local machine but to pull it, is just to have it on my local system, I should also run it after pulling it down

* Name of the repo is same name with the image.
* Lastest is the defualt name for tag. Tag is like version. I can also rename it to a name of choice
<img width="919" alt="12" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/d89fe851-8153-45d7-8bf3-d6d12bd908f2">


### Example 2: pull down busybox image from docker libraries
* "docker pull busybox" to pull the image from dockerhub
* It gave it a defualt tag name; lastest and Id
* "docker images" to display image content
* To run the image,  "docker run busybox"
<img width="916" alt="13" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/828eb996-4d0e-46ad-bb5a-97abba6c86e7">

### Testing docker process
* "docker ps" to check docker process currently running. No container currently running
* "docker ps -a" to check all process ever ran 
<img width="873" alt="14 docker process" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/7c93d344-b7ea-4035-9b11-1e2f27f0ec20">

* Busybox is a compressed and minimized version operating system. it doesnt run all commands
*  "docker run -it busybox" command iteracts with the image and does not exit.
<img width="869" alt="15" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/046e8054-e56a-4037-beb5-9a60cd574a8c">

* "docker ps -a" (a stands for all) displays all current process of the container
* By default, containers are giving random name
* To rename the defualt random name and give a container a name, I run the command, "docker run -it --name containerV1 busybox"
* and "docker ps -a" to view all process
<img width="917" alt="16" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/b83a9666-04de-4781-86c1-5754e96292d8">
### Note: Image is different from container. Image is use to create a container. A container is a running instance of an image

* "docker container ps" to check if there is any containers
<img width="916" alt="17" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/9d4f5cee-54f5-42eb-9645-e4baa0901c41">
* I had to run another container in root as I made a mistake runing the container in ubuntu
<img width="915" alt="17b" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/8c900215-694a-4b73-868e-68bf23fd79c1">

* Container is running behind, to view this I switch into cloudshell
* An image can create three duplicate containers of that same image
<img width="911" alt="18" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/e8c6b747-6be5-4c51-9166-38b97d33ba61">

* I didnt config an external port so it couldnt connect hence I had to inprovised
* To connect to my instance,  I copied the  Public DNS from ssh client and uploaded the private key pem file
<img width="960" alt="19" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/23b83313-e8e2-4cf0-8994-e648c740ef80">

* Open the private key-file
<img width="467" alt="20a" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/8e136be7-e90f-4356-a58d-77a2185ff41f">

  * File uploaded successfully
<img width="960" alt="20" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/6091b67a-dfd1-46c4-8959-789b6a1434f6">

* ls to see the pem file uploaded
* chomod 400 (can also use chmod 600)
* run the ssh client again
* <img width="960" alt="21" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/65e8e81b-b2bf-43e9-be3c-a2fcfdef112c">

* And viola! I am in
<img width="955" alt="22" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/b386d8c5-7c39-4f88-81e5-c672f5542dba">

* "docker ps" displays current running containers only
* While "docker ps -a" displays all container exited
<img width="928" alt="23" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/6230a030-e43a-4a77-bfc7-f0944f60a43b">

